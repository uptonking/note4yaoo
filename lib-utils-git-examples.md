---
title: lib-utils-git-examples
tags: [examples, git]
created: 2023-08-29T10:12:03.868Z
modified: 2023-08-29T10:12:22.345Z
---

# lib-utils-git-examples

# guide

# popular
- https://github.com/isomorphic-git/isomorphic-git /7kStar/MIT/202307/js
  - https://isomorphic-git.org/
  - a pure JavaScript reimplementation of git that works in both Node.js and browser 
  - It can read and write to git repositories, fetch from and push to git remotes (such as GitHub), all without any native C++ module dependencies.
    - rather than relying on the `fs` and `http` modules, isomorphic-git lets you bring your own file system and HTTP client.
    - work with LightningFS/BrowserFS/Filer
  - Isomorphic-git aims for 100% interoperability with the canonical git implementation. 
    - This means it does all its operations by modifying files in a ".git" directory just like the git you are used to.
  - https://github.com/isomorphic-git/lightning-fs /js
    - I wanted to see if I could make something faster than BrowserFS or filer that still implements enough of the fs API to run the isomorphic-git test suite in browsers.
  - https://github.com/fasiha/isomorphic-gatty /ts
    - Append-only log for isomorphic-git, expected to be used as remote sync for local-first web app
    - Gatty saves a stream of events to a git repo and synchronizes it with a remote git server (e.g., GitHub, Gitlab, Gogs, Azure Repos, etc.). The “events” are just plain strings that your app generates and understands: Gatty doesn’t know anything about them.
- https://github.com/creationix/js-git /3.8kStar/MIT/201907/js/inactive
  - A JavaScript implementation of Git.
  - It also enables using git as a database to replace SQL and no-SQL data stores in many applications.
  - https://github.com/es-git/es-git /202012/ts/inactive
    - Git implemented in EcmaScript (a fork of JS-Git)
  - https://github.com/creationix/git-node-fs
    - A node adapter for the fs-db mixin for js-git. This enables access to Git repositories on the filesystem using Node.js.
  - https://github.com/creationix/js-github
    - An implementation of the js-git interface that mounts a live github repo.
- https://github.com/maryrosecook/gitlet /js
  - http://gitlet.maryrosecook.com/
  - http://gitlet.maryrosecook.com/docs/gitlet.html
  - I can only understand something by implementing it. So, I wrote Gitlet, my own version of Git

- https://github.com/Byron/gitoxide /rust
  - an implementation of git written in Rust
  - for the most part, git operations are heavily reliant on memory mapped IO as well as CPU to decompress data, which doesn't lend itself well to async IO out of the box.
- https://github.com/chrisdickinson/git-rs
  - Implementing git in rust for fun and education!

- https://github.com/aergoio/litetree 202003/c/inactive
  - It is a modification of the SQLite engine to support branching, like git!
  - Each database transaction is saved as a commit, and each commit has an incremental number
  - We cannot write to the database when we are in a defined commit, writing is only possible at the head of each branch. If you want to make modifications to some previous commit you must create a new branch that starts at that commit.
  - not-yet: merge
# git-like
- https://github.com/GerritCodeReview/jgit /EDL(BSD)/java
  - https://eclipse.dev/jgit/
  - An implementation of the Git version control system in pure Java.
  - JGit 6.0 and newer requires at least Java 11. Older versions require at least Java 1.8.
  - Native symbolic links are supported, provided the file system supports them. 
  - For Windows you must use a non-administrator account and have the SeCreateSymbolicLinkPrivilege.
  - JGit can use JDBC, HBase, Cassandra, Bigtable and more and it's thread safe.

- https://github.com/jelmer/dulwich /python
  - Pure-Python Git implementation
  - It aims to provide an interface to git repos (both local and remote) that doesn't call out to git directly but instead uses pure Python.

- https://github.com/facebook/sapling /rust
  - Sapling SCM is a cross-platform, highly scalable, Git-compatible source control system.

- https://github.com/drhsqlite/fossil-mirror /c
  - https://fossil-scm.org/home/dir?ci=trunk&type=tree
  - https://fossil-scm.org/
  - A test of the ability of the Fossil DVCS to mirror to GitHub
  - Fossil SCM(Source Control Management) uses SQLite as its database and implements versioning and branching and even merging (which LiteTree doesn't do) on its own, by recording the changes on each item on a separate table.
  - This approach is more complex to implement but a lot more versatile and flexible. Most of times you wouldn't want to version or branch the whole database, but only parts of it.
  - [Fossil: Branching, Forking, Merging, and Tagging](https://fossil-scm.org/home/doc/trunk/www/branching.wiki)
    - The Alternative to Forking: Branching
    - A branch is a named, intentional fork.

- https://github.com/dchest/fossil-delta-js /js
  - https://dchest.github.io/fossil-delta-js/
  - Fossil SCM delta compression in JavaScript
  - The cool thing about it is that plain text inputs generate plain text deltas (binary inputs, of course, may generate binary deltas).
# git-ui
- https://github.com/corylus-git/corylus /ts/electron
  - https://corylus.dev/
  - Corylus is a graphical user interface for Git. 
  - It aims to offer much of the power and flexibility of Git without having to remember CLI commands.
# git-server
- https://github.com/gogs/gogs /MIT/go
  - https://gogs.io/
  - aims to build a simple, stable and extensible self-hosted Git service that can be set up in the most painless way. 
  - 依赖gorm、xorm、tablewriter
  - Access repositories via SSH, HTTP and HTTPS protocols.
  - Rich database backend, including PostgreSQL, MySQL, SQLite3 and TiDB.

- https://github.com/go-gitea/gitea /MIT/go
  - https://about.gitea.com/
  - Painless self-hosted all-in-one software development service, including Git hosting, code review, team collaboration, package registry and CI/CD
# apps
- [Git as a Database | GitRows](https://gitrows.com/)
  - GitRows makes it easy to use and store data in GitHub and GitLab repos and deliver them with a powerful API.
# examples

# utils
- https://github.com/brawnski/git-annex /hs
  - git-annex allows managing files with git, without checking the file contents into git. 
  - While that may seem paradoxical, it is useful when dealing with files larger than git can currently easily handle, whether due to limitations in memory, checksumming time, or disk space.
# git-data
- https://github.com/CodeForPhilly/jawn /js
  - a node.js module that allows distributed version control of Tabular Data. 
  - It's connected to the dat project. 
  - It allows you to import tabular data (rows and columns like CSV or TSV) and track how those data change over time
  - manage and track change history in tabular data
  - create historical checkpoints with metadata (e.g., message, timestamp, author)
  - Jawn relies on `hypercore` to handle the core functions around creating merkle chains

- https://github.com/mirage/irmin /ocaml
  - https://irmin.org/
  - Irmin is an OCaml library for building mergeable, branchable distributed data stores.
  - Irmin applies DVC's principles to large-scale distributed data and exposes similar functions to Git (clone, push, pull, branch, rebase).
  - Irmin was created at the University of Cambridge in 2013 to be the default storage layer for MirageOS applications
  - Irmin is not, strictly speaking, a complete database engine. Instead, similarly to other MirageOS components, it is a collection of libraries designed to solve different flavours of the challenges raised by the CAP Theorem.
  - Due the Content-addressable inherited Git-feature, Irmin allows deduplication and thus, reduced memory-consumption. Some functionally persistent data structures fit perfectly on this database, and the 3-way merge is a novel approach to handle merge conflicts on a CRDT-style.
  - it works well for in-memory databases and slower persistent serialization such as SSDs, hard drives, web browser local storage, or even the Git file format.

- https://github.com/datalad/datalad /python
  - http://datalad.org/
  - it stands on the shoulders of Git and Git-annex to deliver a decentralized system for data exchange. 
  - This includes automated ingestion of data from online portals and exposing it in readily usable form as Git(-annex) repositories, so-called datasets. 
  - The actual data storage and permission management, however, remains with the original data providers.
  - https://github.com/datalad/datalad-next
    - This DataLad extension can be thought of as a staging area for additional functionality, or for improved performance and user experience. 

- https://github.com/janelia-flyem/dvid /BSD/go
  - http://dvid.io/
  - DVID is a Distributed, Versioned, Image-oriented Dataservice written to support neural reconstruction, analysis and visualization efforts at HHMI Janelia Research Center. 
  - It **provides storage with branched versioning** of a variety of data necessary for our research including teravoxel-scale image volumes, JSON descriptions of objects, sparse volumes, point annotations with relationships (like synapses), etc.
  - All versions are available for queries. There is no checkout to read committed data.
  - DVID can be used as a **general-purpose branched versioning file system** that handles billions of files and terabytes of data by creating instances of the keyvalue datatype. 
    - Our team uses the keyvalue datatype for branched versioning of JSON, configuration, and other files using the simple key-value HTTP API.
    - DVID currently handles branched versioning of large-scale data and does not provide domain-specific diff tools to compare data from versions, which would be a necessary step for user-friendly pull requests and truly collaborative data editing.

- https://github.com/gogitdb/gitdb /go/inactive
  - GitDB is a decentralized document database written in Go that uses Git under the hood to provide database-like functionalities via strictly defined interfaces.
  - [GitDB, a distributed embeddable database on top of Git | Hacker News](https://news.ycombinator.com/item?id=31987240)
# more