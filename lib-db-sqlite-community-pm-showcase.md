---
title: lib-db-sqlite-community-pm-showcase
tags: [community, showcase, sqlite]
created: 2023-04-30T16:50:54.098Z
modified: 2024-08-11T07:21:27.549Z
---

# lib-db-sqlite-community-pm-showcase

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Why I'm using SQLite as the only database for a production SaaS (and the tradeoffs I've hit so far) : r/FastAPI _202602](https://www.reddit.com/r/FastAPI/comments/1ra1xlg/why_im_using_sqlite_as_the_only_database_for_a/)
  - I've been building a discovery engine for solo-built software — think of it as intent-based search where users type a problem ("I need to send invoices") and get matched to tools, instead of browsing by product name or upvotes.
  - The stack is FastAPI + SQLite. No Postgres. No Redis. No managed database service. Just a single .db file.
- Why SQLite
  - Zero operational overhead. No connection pooling, no database server to monitor, no Docker Compose dependency. The app and the data live together.
  - Reads are absurdly fast. My use case is read-heavy (search queries) with infrequent writes (new tool submissions, maybe 10-20/day). SQLite handles this without breaking a sweat.
  - Backups are cp. I rsync the .db file nightly. That's the entire backup strategy. It works.
  - Deployment is simple. One process, one file, one VPS. I deploy with a git pull and a systemd restart. The calm tech dream.
- The tradeoffs I've hit
  - Write concurrency. SQLite uses a file-level lock for writes. With WAL mode enabled, concurrent reads are fine, but if you have multiple processes writing simultaneously, you'll hit SQLITE_BUSY. My solution: a single FastAPI worker handles all writes via a background task queue. If you're running Gunicorn with multiple workers, this is something you have to think about.
  - Full-text search. SQLite's built-in FTS5 is surprisingly capable. I'm using it for intent-based search with custom tokenizers. It's not Elasticsearch, but for a catalog of a few thousand items, it's more than enough. The main limitation: no fuzzy matching out of the box. I handle typo tolerance at the application layer.
  - No native JSON operators (sort of). SQLite has json_extract() and friends, but they're not as ergonomic as Postgres's -> and ->> operators. I store structured metadata as JSON blobs and parse in Python when needed. Minor annoyance, not a blocker.
  - Schema migrations. There's no ALTER COLUMN in SQLite. If you need to change a column type, you're rebuilding the table. I use alembic with the batch mode for this, which wraps the create-copy-drop-rename dance. Works fine, just feels clunky.
- I think SQLite stops being the right choice when:
  - You need concurrent writes from multiple services (microservices, multiple API servers)
  - Your dataset exceeds ~50GB and you need complex analytical queries
  - You need real-time replication to a read replica

- I too was in my "SQLite is amazing" era at some point a few years ago. Now I'm back to boring managed PostgreSQL. Not because SQLite can't handle the load of a lot of products, I agree it can.
  - But managed PG is really not that much harder to operate. I get insurance for the unlikely future I might need to scale beyond 1 machine. And I don't get weird looks or have to waste time explaining. Life is easy.
- Totally fair take. The managed Postgres route removes a lot of operational headaches — you're paying for someone else to handle backups, replication, and upgrades. For a team or anything with multiple services writing to the same DB, Postgres is the obvious choice.
  - For me the calculus is different right now: single service, read-heavy, solo developer (building indiestack.fly.dev). The operational simplicity of "it's just a file" genuinely saves me time every week. But I'm not dogmatic about it — if the requirements change, so will the database.

- Using async web framework (FastAPI) with a non-async database driver sounds like a missed opportunity.
  - I'm on a similar setup (Quart + asyncmy) with sqlite as the caching layer. Webapps wickedly fast even in Python.

- ## Top 5 free SQLite GUIs 
- https://twitter.com/notrab/status/1777708042760376638
- [DB Browser for SQLite](https://sqlitebrowser.org/)
  - visual, open source tool to create, design, and edit database files compatible with SQLite.
  - DB4S is for users and developers who want to create, search, and edit databases. 
  - DB4S uses a familiar spreadsheet-like interface, and complicated SQL commands do not have to be learned.
- [Beekeeper Studio](https://www.beekeeperstudio.io/)
  - modern, easy to use, and good looking SQL client for MySQL, Postgres, SQLite, SQL Server, and more.
- [DBeaver](https://dbeaver.io/) 
  - popular cross-platform database tool for developers and database administrators. 
  - It's free, open-source, works on Windows, macOS, Linux, and support SQLite.
- [Sqlime](https://sqlime.org/) 
  - an online SQLite playground that runs in the browser. You can use it with local or remote SQLite databases.
  - Full-blown database in the browser
  - Sqlime is backed by the latest version of SQLite via the sqlean.js project. It provides a full-featured SQL implementation, including indexes, triggers, views, transactions, CTEs, window functions and execution plans.
  - Connect any local or remote SQLite database.
  - https://github.com/nalgeon/sqlime
- [SQLite Viewer](https://alpha.sqliteviewer.app/)

- ## [Interactive SQLite Documentation: Experiment with Queries in Real-Time | Hacker News _202403](https://news.ycombinator.com/item?id=39600968)
- 
- 
- 

- ## 🪶🌰 [Bluesky migrates to single-tenant SQLite | Hacker News_202311](https://news.ycombinator.com/item?id=38171322)
- I'm not opposed to this setup at all and it does have its place. But we are running away from schema-per-tenant setup at warp speed at work. There are so many issues if you don't invest in it properly and I don't think many are prepared when they initially have the idea.
  - The funny thing is that about a decade ago, the app was born on a SQLite per tenant setup, then it moved to schema per tenant on Postgres, now it's finally moving to a single schema with RLS. So, the exact opposite progression.

- Interesting... I like the strategy of having each user be 1:1 with a DB. What would be done for data that needs to be aggregated across users though?
  - To summarise the relevant details, the "AppView" service is responsible for the sorts of queries that aggregate across users, and that has its own database setup - I think postgres but I'm not 100% sure on that.
- You're right, as usual. AppView is on a Postgres cluster with read replicas doing timeline generation (and other things) on-demand. We're in the process of moving it toward a beefy ScyllaDB cluster designed around a fanout-on-write system.
  - The v1 backend system was optimized for rapid development and served us well. 
  - The v2 backend will be somewhat less flexible (no joins!) but is designed for much higher scale.

- Can someone that knows more about bluesky explain what data is stored in sqlite and not? Because i assume it isnt messages etc between users.
  - It's all your posts and replies as a user. While they currently host the only* PDS themselves, the end goal is for every end user to have their own PDS. Inrupt/SOLID calls this concept a "pod".

- This seems like a very misleading title, the Bluesky PDS is the meant-for-selfhosting thing they distribute, not the bluesky service as experienced and used by most of its users.
- AFAIK there's only one version of the software so "the service" runs the same thing that you self-host. SQLite seems like it will simplify the single-user case though.
  - That's right. This is the same code Bluesky is running on our new PDS hosts. It's all open source.
  - The main motivation in moving from a big central Postgres cluster to single tenant SQLite databases is to make hosting users much more efficient, inexpensive, and operationally simpler.
  - But it's also part of the plan to run regional PDS hosts near users, increasing performance by decreasing end-to-end latency.
  - The most experimental part of this setup is using Litestream to replicate these many SQLite databases (there are almost 2 million user repositories) to cloud storage. But we're not relying on this alone, we're also going to maintain standard SQLite ".backup" snapshots as well.

- I am curious, does the HN folks know if bluesky is more active than nostr or the mastodon network?
  - Less active than Mastodon, I'd assume more active than Nostr.
  - But the interesting thing for me isn't activity — it's the people on there.
  - Of the cohort who had >100k followers on Twitter, I think more of them post regularly on Bluesky than post on Mastodon. Bluesky definitely has a more cohesive feel, especially because there's currently just one instance & mod team.
- My bet is regardless of any initial good intentions, since BlueSky is a company, market pressures will inevitably force them into dark patterns like we see on every other commercial social network (going back to the early days of the companies, Facebook, Twitter, and even Google looked really good early on until all were corrupted by profit motive). My belief is that the profit motive is necessarily at odds with free communication.
  - To me, the ActivityPub network (Mastodon and friends) is relatively unique in the social media space in having no direct commercial pressures (the protocol is developed by W3C) and therefore being inoculated against the causes for these dark patterns.

- Why not use Postgres with RBAC (Row Based Access Control).
  - simpler db client
  - simpler cloud architecture
  - simpler resource management
  - simpler partial backups/restore
  - simpler compliance with law enforcement
  - partitioning might be easier
  - maybe simpler billing for storage ("just" size of DB)

- ## 🔥 [Show HN: WarcDB: Web crawl data as SQLite databases | Hacker News_202206](https://news.ycombinator.com/item?id=31799147)
- 
- 
- 

- ## 🔥 [Wp-SQLite: WordPress running on an SQLite database | Hacker News_202205](https://news.ycombinator.com/item?id=31396732)
- 
- 
- 

- ## [WordPress Core to start using SQLite | Hacker News_202307](https://news.ycombinator.com/item?id=36884806)
- Related - WordPress recently released WordPress Playground
  - These utilize WebAssembly (php-wasm) and an SQLite database backend to run a whole WordPress instance in the browser or a local Node.js instance.

- Did you consider using the `temporal_tables` extension? I think it's basically like **version history for tables**. 
  - I haven't used this before personally though. https://pgt.dev/extensions/temporal_tables
  - Temporal Tables Extension requires PostgreSQL 9.2 or higher.

- ## Announcing Deno KV: A Global Database for Global Apps! Built on FoundationDB and SQLite_202304
- https://twitter.com/deno_land/status/1651972190965837825
  - ACID transactions

- Or, with similar or better levels of performance, you can make the database appear to disappear, and end up with persistent JS objects
  - https://github.com/robtweed/glsdb
    - Global Storage Database Abstraction for Node.js

- Is there a way to create tables / collections with this? It looks like every key is on the same table.

- https://twitter.com/zen0wu/status/1652372212379418626
  - the array-based JSON keys looks a lot like @ccorcos 's tuple-database, and it's also FoundationDB based
  - It’s quite similar. I wonder why Deno opted for manual consistency checks rather than it being automatic on reads though.
- It seems common in distributed KV stores to allow clients to choose a low-latency-but-weak-consistency read or a high-latency-but-strongly-consistent read. It seems like reads default to “strong”

- ## 🚀🔥 [D1: Our SQL database | Hacker News_202205](https://news.ycombinator.com/item?id=31339299)
- [Announcing D1: our first SQL database](https://blog.cloudflare.com/introducing-d1/)
  - D1 is built on SQLite. 
- 
- 
- 

- ## Here is Harika. The offline-first note-taking app on top SQLite (using absurd-sql for web version)
- https://twitter.com/quolpr/status/1558848201771319298
  - It uses LWW per field CRDT and stores all changes on the server, so time travel is possible to implement.
  - And SQLite allows storing huge amount of data with the instant startup time 
  - I managed to pause work on it because I don't have enough resources (money/time) to keep working on it
- 👉🏻 What do you use for text editing?
  - it's mobx-keystone. I partially load data from SQLite into mobx-keystone. Then all the changes are happening in-memory and after short delay are dumped back to SQLite
  - It's just textarea that render to just HTML on unfocus. To parse input to AST I use pegjs
- How does the sync work?
  - Very roughly — every 500ms it collect all the changed that were done to the doc, and saves to the changes table. Then, when you are back only, all of these changes will be sent to the server.
  - The server will have a collection of all changes from all clients, so he will be able to calculate the final view of each entity, and send back to the clients.
  - If some changes came from the past (like you used offline mobile, and you also used desktop online) — it will recalculate the snapshot with the new changes came from phone, so you will never lose your data
  - Change = the diff of the doc between new and old state
- What is your experience with absurd-sql. would you recommend it ?
  - right now, absurd-sql has race condition bug in multi tab usage, and require using COOP headers (that restricts to embed YouTube video, for example)
  - And right now I am working on asyncify version of wasm SQLite, and it will have the same performance as absurd-sql has, but without multi-tab bug and COOP header requirement. I hope my company will open-source it 🙂 Cause then we will be able to use SQLite without any limits
- With it, I was able to unlock x5-20 performance boost, but it's pretty raw to use. I wrote a simple wrapper around absurd-sql  
  - https://github.com/kikko-land/kikko
  - It supports transactions, middlewares, and guide how to set up absurd-sql for CRA/vite
  - if you have performance issues, and don't like IndexedDB — just use absurd-sql (or trong-orm hehe 😜)

- ## 🔥 [Show HN: WunderBase – Serverless OSS database on top of SQLite, Firecracker | Hacker News_202209](https://news.ycombinator.com/item?id=32852478)
- 
- 
- 
