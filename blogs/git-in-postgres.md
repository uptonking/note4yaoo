---
title: git-in-postgres
tags: [dev, git, postgresql]
created: 2026-03-08T09:34:23.614Z
modified: 2026-03-08T09:34:31.219Z
description: "Instead of using git as a database, what if you used a database as a git?"
---

# git-in-postgres

> original source: https://github.com/andrew/nesbitt.io/blob/master/_posts/2026-02-26-git-in-postgres.md

In December I wrote about [package managers using git as a database](/2025/12/24/package-managers-keep-using-git-as-a-database.html), and how Cargo's index, Homebrew's taps, Go's module proxy, and CocoaPods' Specs repo all hit the same wall once their access patterns outgrew what a git repo is designed for.

[homebrew-core](https://github.com/Homebrew/homebrew-core) has one Ruby file per package formula, and every `brew update` used to clone or fetch the whole repository until it got large enough that [GitHub explicitly asked them to stop](https://github.com/Homebrew/brew/pull/9383). Homebrew 4.0 switched to downloading a JSON file over HTTP, because users wanted the current state of a package rather than its commit history. But updating a formula still means opening a pull request against homebrew-core, because git is where the collaboration tooling lives. Instead of using git as a database, what if you used a database as a git?

A git repository is a content-addressable object store where objects go in indexed by the SHA1 of their content, plus a set of named references pointing at specific objects by hash. The on-disk format (loose objects as individual files, packfiles as delta-compressed archives with a separate index, a ref store split between a directory of files and a packed-refs flat file with a locking protocol that breaks on NFS) is an implementation detail. The protocol for synchronising objects and refs between repositories is what actually matters, and since git-the-program is just one implementation of it, you can swap the storage backend without clients noticing.

The whole data model fits in two tables:

```sql
CREATE TABLE objects (
    repo_id  integer NOT NULL,
    oid      bytea NOT NULL,
    type     smallint NOT NULL,
    size     integer NOT NULL,
    content  bytea NOT NULL,
    PRIMARY KEY (repo_id, oid)
);

CREATE TABLE refs (
    repo_id  integer NOT NULL,
    name     text NOT NULL,
    oid      bytea,
    symbolic text,
    PRIMARY KEY (repo_id, name)
);
```

An object's OID is computed the same way git does it, `SHA1("<type> <size>\0<content>")` , using pgcrypto's `digest()` function, and refs get compare-and-swap updates through `SELECT FOR UPDATE` . A libgit2 backend registers these tables as its storage layer, and if the protocol really is separable from the format, a normal git client should be able to push to and clone from a Postgres database without knowing the difference.

To test this I built [gitgres](https://github.com/andrew/gitgres), about 2, 000 lines of C implementing the libgit2 `git_odb_backend` and `git_refdb_backend` interfaces against Postgres through libpq, plus roughly 200 lines of PL/pgSQL for the storage functions. libgit2 handles pack negotiation, delta resolution, ref advertisement, and the transport protocol while the backend reads and writes against the two tables, and a git remote helper ( `git-remote-gitgres` ) lets you add a Postgres-backed remote to any repo and push or clone with a normal git client that has no idea it's talking to a database. There's a Dockerfile in the repo if you want to try it out without building libgit2 and libpq from source.

The objects table contains the same bytes git would store on disk, and a set of SQL functions parse them into tree entries, commit metadata, and parent links that you can join against like any other table.

```sql
SELECT r.name AS repo, c.author_name, c.authored_at, i.title AS issue
FROM commits c
JOIN repositories r ON r.id = c.repo_id
JOIN issues i ON i.repo_id = c.repo_id
  AND c.message ILIKE '%#' || i.index || '%'
WHERE c.authored_at > now() - interval '30 days';
```

That query joins git commit data against Forgejo's issue tracker, something that currently requires fetching commits through `git log` , pattern-matching issue references in application code, and then querying the database for the matching issues. With both sides in Postgres it's one query.

### Forgejo

A self-hosted Forgejo or Gitea instance is really two systems bolted together: a web application backed by Postgres, and a collection of bare git repositories on the filesystem. Anything that needs to show git data in the web UI has to shell out to the binary and parse text, which is why something as straightforward as a blame view requires spawning a subprocess rather than running a query. If the git data lived in the same Postgres instance as everything else, that boundary disappears.

Forgejo stores issues, pull requests, users, permissions, webhooks, branch protection rules, and CI status in Postgres already, and git repositories are the one thing left on the filesystem, forcing every deployment to coordinate backups between them, and the two systems scale and fail in different ways. The codebase already shows the strain: Forgejo mirrors branch metadata from git into its own database tables ( `models/git/branch.go` ) so it can query branches without shelling out to git every time.

All git interaction goes through `modules/git` , about 15, 000 lines of Go that shells out to the `git` binary and parses text output. With git data in Postgres, reading an object becomes `SELECT content FROM objects WHERE oid = $1` on the database connection Forgejo already holds, and walking commit history is a query against a materialized view rather than spawning `git log` .

The deployment collapses to a single Postgres instance where `pg_dump` backs up forge metadata, git objects, and user data together, and replicas handle read scaling for the web UI without NFS mounts or a Gitaly-style RPC layer. The path there is a Forgejo fork replacing `modules/git` with a package that queries Postgres, where `Repository` holds a database connection and repo_id instead of a filesystem path and `Commit` , `Tree` , `Blob` become thin wrappers around query results.

### Postgres

Postgres has its own primitives for things that forges currently build custom infrastructure around. A trigger on the refs table firing `NOTIFY` means any connected client learns about a push the moment it happens, which is how forges normally end up building a custom webhook polling layer. Multi-tenant repo isolation becomes a database concern through row-level security on the objects and refs tables, and logical replication lets you selectively stream repositories across Postgres instances, a kind of partial mirroring that filesystem-based git can't do. Commit graph traversal for ancestry queries and merge-base computation falls to recursive CTEs, and `pg_trgm` indexes on blob content give you substring search across all repositories without standing up a separate search index.

### Diff, merge, blame

Content-level diffs, three-way merge, and blame stay in libgit2 rather than being reimplemented in SQL, since libgit2 already has that support and works against the Postgres backends through cgo bindings. The Forgejo fork would be "replace `modules/git` with libgit2 backed by Postgres" rather than "replace `modules/git` with raw SQL, " because the read-side queries only cover the simple cases and anything involving content comparison or graph algorithms still needs libgit2 doing the work with Postgres as its storage layer. That's a meaningful dependency to carry, though libgit2 is well-maintained and already used in production by the Rust ecosystem and various GUI clients. SQL implementations of some of this using recursive CTEs would be interesting to try eventually but aren't needed to get a working forge. The remaining missing piece is the server-side pack protocol: the remote helper covers the client side, but a Forgejo integration also needs a server that speaks `upload-pack` and `receive-pack` against Postgres, either through libgit2's transport layer or a Go implementation that queries the objects table directly.

### Storage

Git packfiles use delta compression, storing only the diff when a 10MB file changes by one line, while the objects table stores each version in full. A file modified 100 times takes about 1GB in Postgres versus maybe 50MB in a packfile. Postgres does TOAST and compress large values, but that's compressing individual objects in isolation, not delta-compressing across versions the way packfiles do, so the storage overhead is real. A delta-compression layer that periodically repacks objects within Postgres, or offloads large blobs to S3 the way LFS does, is a natural next step. For most repositories it still won't matter since the median repo is small and disk is cheap, and GitHub's Spokes system made a similar trade-off years ago, storing three full uncompressed copies of every repository across data centres because redundancy and operational simplicity beat storage efficiency even at hundreds of exabytes.

gitgres is a neat hack right now, but if open source hosting keeps moving toward federation and decentralization, with ForgeFed, Forgejo's federation work, and more people running small instances for their communities, the operational simplicity of a single-Postgres deployment matters more than raw storage efficiency. Getting from a handful of large forges to a lot of small ones probably depends on a forge you can stand up with `docker compose up` and back up with `pg_dump` , and that's a lot easier when there's no filesystem of bare repos to manage alongside the database.
