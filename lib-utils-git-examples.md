---
title: lib-utils-git-examples
tags: [examples, git]
created: 2023-08-29T10:12:03.868Z
modified: 2023-08-29T10:12:22.345Z
---

# lib-utils-git-examples

# guide

- git-powered
  - 对git的统计可参考 https://github.com/pingcap/ossinsight
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
- https://github.com/maryrosecook/gitlet /MIT/201504/js
  - http://gitlet.maryrosecook.com/
  - http://gitlet.maryrosecook.com/docs/gitlet.html
  - I can only understand something by implementing it. So, I wrote Gitlet, my own version of Git

- https://github.com/Byron/gitoxide /7.6kStar/MIT/202402/rust
  - an implementation of git written in Rust
  - for the most part, git operations are heavily reliant on memory mapped IO as well as CPU to decompress data, which doesn't lend itself well to async IO out of the box.
- https://github.com/chrisdickinson/git-rs
  - Implementing git in rust for fun and education
- https://github.com/web3infra-foundation/mega/tree/main/libra /202406/rust
  - a partial implementation of a Git client, developed using Rust.
  - Our goal is not to create a 100% replica of Git (for those interested in such a project, please refer to the gitoxide)
  - A key feature of libra is the replacement of the original Git internal storage architecture with SQLite.

- https://github.com/gitbutlerapp/gitbutler /FSL-1.0-MIT(2y)/202409/rust/ts/svelte
  - https://gitbutler.com/
  - The GitButler version control client, backed by Git, powered by Tauri/Rust/Svelte
  - Git branch management tool, built from the ground up for modern workflows
  - GitButler is a git client that lets you work on multiple branches at the same time
  - ✨ Changes to files or parts of files can be grouped into what we call virtual branches. 
  - 🆚️ How do GB's virtual branches differ from Git branches?
    - The branches that we know and love in Git are separate universes, and switching between them is a full context switch. 
    - GitButler allows you to work with multiple branches in parallel in the same working directory.
    - GitButler is aware of changes before they are committed. This allows it to keep a record of which virtual branch each individual diff belongs to.
    - while in Git it is preferable that you create your desired branch ahead of time, using GitButler you can move changes between virtual branches at any point during development.

- https://github.com/jupyterlab/jupyterlab-git /BSD/202407/python/ts
  - A JupyterLab extension for version control using Git

- https://github.com/aergoio/litetree /202003/c/inactive
  - It is a modification of the SQLite engine to support branching, like git
  - Each database transaction is saved as a commit, and each commit has an incremental number
  - We cannot write to the database when we are in a defined commit, writing is only possible at the head of each branch. If you want to make modifications to some previous commit you must create a new branch that starts at that commit.
  - not-yet: merge

- https://github.com/opral/monorepo /apache2/202311/ts
  - https://github.com/inlang/inlang
  - https://inlang.com/
  - https://opral.com/
  - globalization infrastructure for software && version control for apps
  - Inlang is an ecosystem of interoperable lix apps to globalize software.
  - [Ask HN: Apps that are built with Git as the back end? | Hacker News _202210](https://news.ycombinator.com/item?id=33261862)
  - [discussion about reactivity architecture](https://github.com/inlang/inlang/issues/1122)

- https://github.com/GQL-Project/gql_db /202212/rust/inactive
  - gql-db is an SQL database server with version control integrated into the database itself. 
  - It's written in Rust and uses Protocol Buffers/gRPC for communication
  - We've also implemented a UI for the database server, which can be found at: GQL-Project/gql_client.

- https://github.com/MichaelMure/git-bug /GPLv3/202310/go
  - Distributed, offline-first bug tracker embedded in git, with bridges
  - fully embedded in git: you only need your git repository to have a bug tracker
  - distributed: use your normal git remote to collaborate, push and pull your bugs
  - use bridges to import and export to other trackers.
# git-like
- https://github.com/GerritCodeReview/jgit /EDL(BSD)/202310/java
  - https://eclipse.dev/jgit/
  - An implementation of the Git version control system in pure Java.
  - JGit 6.0 and newer requires at least Java 11. Older versions require at least Java 1.8.
  - Native symbolic links are supported, provided the file system supports them. 
  - For Windows you must use a non-administrator account and have the SeCreateSymbolicLinkPrivilege.
  - JGit can use JDBC, HBase, Cassandra, Bigtable and more and it's thread safe.
  - There are some missing features:
    - shallow and partial cloning
    - support for multiple working trees (git-worktree)
    - using external diff tools
    - git protocol V2 (client side): packfile-uris

- https://github.com/gitblit-org/gitblit /apache2/202311/java
  - http://gitblit.com/
  - pure Java Git solution for managing, viewing, and serving Git repositories. 
  - It can serve repositories over the GIT, HTTP, and SSH transports; 
  - it can authenticate against multiple providers; 
  - Gitblit GO is an integrated, single-stack solution based on Jetty.
  - Gitblit WAR is what you should download if you already have a servlet container available that you wish to use
  - JGit 4.5 release supports GitLFS, this could allow mirroring of repositories using LFS and provide a means for handling LFS files during federation requests.
  - [Support for partial clones? /未实现 _202104](https://github.com/gitblit-org/gitblit/issues/1365)
    - currently partial cloning is not supported.
    - Gitblit uses JGit underneath. I am not sure, but I think right now JGit does not have support for it, at least not fully.

- https://github.com/jelmer/dulwich /python
  - Pure-Python Git implementation
  - It aims to provide an interface to git repos (both local and remote) that doesn't call out to git directly but instead uses pure Python.

- https://github.com/facebook/sapling /rust
  - Sapling SCM is a cross-platform, highly scalable, Git-compatible source control system.

- https://github.com/web3infra-foundation/mega /apache2/202406/rust
  - https://gitmega.dev/
  - Mega is an unofficial open source implementation of Google Piper.
  - It is a monorepo & monolithic codebase management system that supports Git. 
  - Mega is designed to manage large-scale codebases, streamline development, and foster collaboration.
  - Google Piper is not open source
  - When it comes to managing large codebases in a centralized manner, trunk-based development is the way to go. 
  - Mega is working on build a decentralized open source collaboration model with ZTM(Zero Trust Model) and decentralized social network like Nostr, Matrix and Mastodon.

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

- https://github.com/martinvonz/jj /4.8kStar/apache2/202401/rust
  - https://martinvonz.github.io/jj
  - [Other related work](https://martinvonz.github.io/jj/v0.9.0/related-work.html)
  - A Git-compatible DVCS that is both simple and powerful
  - Jujutsu is unlike most other systems, because internally it abstracts the user interface and version control algorithms from the storage systems used to serve your content. This allows it to serve as a VCS with many possible physical backends, that may have their own data or networking models—like Mercurial or Breezy, or hybrid systems like Google's cloud-based design, Piper/CitC.
  - It combines features from Git (data model, speed), Mercurial (anonymous branching, simple CLI free from "the index", revsets, powerful history-rewriting), and Pijul/Darcs (first-class conflicts), with features not found in most of them
  - Jujutsu has two backends. One of them is a Git backend (the other is a native one). This lets you use Jujutsu as an alternative interface to Git.
  - All operations you perform in the repo are recorded, along with a snapshot of the repo state after the operation. This means that you can easily revert to an earlier repo state, or to simply undo a particular operation
  - The tool is quite feature-complete, but some important features like (the equivalent of) git blame are not yet supported. 
  - Git compatibility pretty much rules out the radically different approaches that might actually be better enough to outcompete it. Like:
    - Patch-based VCS (darcs, pijul)
    - CRDT (live collaboration)
    - Image-based systems (Smalltalk)
    - Features that require the server to do stuff that Git protocol won’t do, like push notifications
    - In other words, I can’t imagine leaving Git unless it’s as big of an upgrade as Git was to SVN. And you can’t do that while being wire compatible.
  - [Operation log](https://github.com/martinvonz/jj/blob/main/docs/operation-log.md)
    - Jujutsu records each operation that modifies the repo in the "operation log". You can see the log with jj op log. 
    - Each operation object contains a snapshot of how the repo looked at the end of the operation. We call this snapshot a "view" object. 
    - The view contains information about where each branch, tag, and Git ref pointed, as well as the set of heads in the repo
    - The view contains information about where each branch, tag, and Git ref (in Git-backed repos) pointed, as well as the set of heads in the repo,
    - The operation log allows you to undo an operation (jj [op] undo), which doesn't need to be the most recent one. It also lets you restore the entire repo to the way it looked at an earlier point

- Pijul /GPLv2
  - [Pijul is a free and open source (GPL2) distributed version control system](https://pijul.org/)
  - Pijul is instead a CRDT, meaning that independent patches can be applied in any order without changing the result, which makes rearrangement unnecessary, and the system much faster.
  - https://nest.pijul.com/pijul/pijul /GPLv2/rust
    - fast distributed version control system based on a mathematical theory of asynchronous work
  - https://github.com/jneem/pijul
    - a temporary fork of pijul

- Darcs /GPLv2
  - [Darcs is a free and open source, cross-platform version control system, like git/svn](https://darcs.net/)
  - the primary datastructure in Darcs is indeed a list of patches, and the main operation is rearrangement.
  - [darcs: a distributed, interactive, smart revision control system](https://hackage.haskell.org/package/darcs)

- https://github.com/terabyte/jgit /BSD/201104/java
  - https://www.eclipse.org/jgit/
  - JGit is an EDL (new-style BSD) licensed, lightweight, pure Java library implementing the Git version control system
  - A pure Java library capable of being run standalone, with no additional support libraries.
  - Symbolic links are not supported because java does not support it. Such links could be damaged.
  - [Distributed file system as storage layer over git - Stack Overflow](https://stackoverflow.com/questions/24178074/distributed-file-system-as-storage-layer-over-git)
- https://github.com/spearce/jgit_cassandra /201103/java
  - Cassandra based storage layer for JGit
  - This package is a trivial implementation of the org.eclipse.jgit.storage.dht.spi interface, binding JGit's generic DHT storage onto the Apache Cassandra NoSQL database.
  - Install Cassandra 0.7 or later, and start it on at least one node.
# git-ui
- https://github.com/corylus-git/corylus /ts/electron
  - https://corylus.dev/
  - Corylus is a graphical user interface for Git. 
  - It aims to offer much of the power and flexibility of Git without having to remember CLI commands.

- https://github.com/extrawurst/gitui /MIT/202408/rust
  - fast terminal-ui for git written in rust
# git-server/gitlab-like
- github-alternatives
  - ruby: gitlab
  - go: gitea, gogs
  - java: onedev
  - rust: 多是git的挑战者
  - Git comes with a CGI script called GitWeb
  - https://github.com/ianchanning/awesome-github-alternatives
    - a list of alternatives to GitHub, that by default offer Git management in some way.

- https://github.com/gogs/gogs /43.8kStar/MIT/202312/go
  - https://gogs.io/
  - aims to build a simple, stable and extensible self-hosted Git service that can be set up in the most painless way. 
  - 依赖gorm、xorm、tablewriter
  - Access repositories via SSH, HTTP and HTTPS protocols.
  - Rich database backend, including PostgreSQL, MySQL, SQLite3 and TiDB.
  - https://github.com/gogs/git-module /MIT/202210/go
    - a Go module for Git access through shell commands

- https://github.com/go-gitea/gitea /40.7kStar/MIT/202402/go
  - https://about.gitea.com/
  - Painless self-hosted all-in-one software development service, including Git hosting, code review, team collaboration, package registry and CI/CD
  - forked from Gogs since November of 2016, but a lot has changed
  - [Gitea hosted Gitea /未实现 _201702](https://github.com/go-gitea/gitea/issues/1029)

- https://codeberg.org/forgejo/forgejo /go
  - https://forgejo.org/
  - Forgejo was created in 2022 because we think that the project should be owned by an independent community.
  - A painless, self-hosted Git service
  - [Codeberg: A GitHub alternative from Europe | Hacker News _202210](https://news.ycombinator.com/item?id=33233360)
    - Codeberg is a fork of Gitea
  - https://codeberg.org/Codeberg/forgejo

- https://github.com/harness/gitness /apache2/202402/go/ts
  - https://gitness.com/
  - Gitness is an Open Source developer platform with Source Control management, Continuous Integration and Continuous Delivery.
  - It is largely based on the existing Drone repository, but for Git capabilities we used the Gitea fork of https://github.com/gogs/git-module

- https://github.com/theonedev/onedev /MIT/202401/java/不依赖spring
  - https://onedev.io/
  - Self-hosted Git Server with CI/CD and Kanban
  - 依赖jgit、shiro、hibernate、glassfish
  - We develop OneDev at https://code.onedev.io/ for sake of dogfooding.
  - it is using JGit for most operations. JGit API is very well designed and is a joy to use.
    - The performance is very good, except for long operations such as full clone.
    - So for pull/push I am calling native git, but for other operations which may need to be executed several times during a request I am using JGit which is much faster thanks for the in-process cache.

- https://github.com/mellowagain/gitarena /MIT/202306/rust/inactive
  - Software development platform with built-in vcs, issue tracking and code review
  - lightweight and performant alternative to the likes of GitLab and Gitea, built with self-hosting and cross-platform/cross-architecture support in mind.
  - 依赖libmagic、gitoxide
  - Currently, GitArena is work in progress and is not yet fully featured. The basics such as repositories and pushing/pulling as well as accounts work
  - [switch to using custom backend for git](https://github.com/mellowagain/gitarena/issues/58)
    - libgit2 allows custom backends, should consider this with e.g S3
    - maybe gitoxide also provides such a backend?

- https://github.com/alexwennerberg/mygit /AGPLv3/202108/rust/inactive
  - Simple self-hosted git server, written in Rust
  - Lighter weight than gitea, more modern than cgit or gitweb
  - NOTE: This project is not actively developed. I decided to use cgit instead.
  - [mygit: simple self-hosted git : r/rust](https://www.reddit.com/r/rust/comments/omw4e7/mygit_simple_selfhosted_git/)

- https://gitlab.com/gitlab-org/gitlab-foss /MIT/ruby
  - a read-only mirror of GitLab, with all proprietary code remove
  - This project was previously used to host GitLab Community Edition, but all development has now moved to https://gitlab.com/gitlab-org/gitlab

- https://sr.ht/~sircmpwn/sourcehut/ /go
  - A software development platform for hackers

- https://github.com/clehner/git-ssb
  - https://scuttlebot.io/apis/community/git-ssb.html
  - social coding on secure-scuttlebutt
  - https://github.com/hackergrrl/git-ssb-intro
    - SSB stands for secure scuttlebutt, the database/protocol that powers the peer-to-peer log store scuttlebutt. 
    - git-ssb builds on top of this: things like commits, branches, issues, and pull requests are encoded into log entries on each participant's personal log, while the gossip protocol runs in the background and propagates new content to everyone involved in the git repository.

- https://app.radicle.xyz/seeds/seed.radicle.xyz /rust
  - https://radicle.xyz/
  - Radicle is a sovereign peer-to-peer network for code collaboration, built on top of Git.
  - Radicle is local-first, providing always-available functionality even without internet access.
  - https://twitter.com/vikingmute/status/1765538828167848190
    - 使用 P2P 的方式来进行 git 协作，分布式，无法被禁止
    - git不就是本身就是本地化的么。git clone是所有分支所有代码都在本地。怕个锤子
    - Git 本身是去中心化的，但是现实世界的 Collaboration 是中心化的

- https://github.com/gabrielcsapo/node-git-server /MIT/202208/ts/inactive
  - https://gabrielcsapo.github.io/node-git-server
  - A configurable git server written in Node.js
  - This is a hard fork from pushover.

- https://github.com/stackdot/NodeJS-Git-Server /201703/js/inactive
  - A multi-tenant git server using NodeJS
  - The GitServer is a very easy to get up and running git server. 
  - It uses the Pushover and git-emit modules for listening to git events, and its own layer to do the security for each repo & user.

- https://github.com/georoot/ristretto /GPLv3/201702/js
  - http://rahulbhola.ml/ristretto/docs
  - light-weight git server written in nodejs.
  - Git server that manages requests over ssh
  - Simple api that currently support authentication and creating new user repo.
  - most of the codebase is hack and currently lacks some very important features.

- https://github.com/adobe/git-server /apache2/202011/js/archived
  - A GitHub Protocol & API emulation
  - git-server serves a hierarchy of local Git repositories to Git clients accessing the repository over http:// and https:// protocol.
  - Repositories exposed via git-server can be used just like any repository hosted on GitHub, i.e. you can clone them and push changes to
  - [Explore pure JS alternatives to native nodegit](https://github.com/adobe/git-server/issues/41)

- https://github.com/jasonwhite/rudolfs /MIT/202305/rust/inactive
  - A high-performance, caching Git LFS server with an AWS S3 back-end.
  - Multiple backends: 
    - AWS S3 backend with an optional local disk cache.
    - Local disk backend.
  - Encryption of LFS objects in both the cache and in permanent storage.
  - The back-end storage code is very modular and composable. 
  - There is no client authentication. This is meant to be run in an internal network with clients you trust

- https://github.com/mbostock/git-static /201503/js
  - A versioned static file server backed by Git.
  - Go to `http://localhost:3000/HEAD/path/to/file.html` to view a file from the source repository. You can replace HEAD with a specific commit version, or with short names and aliases for commits such as "0ad4156" or "HEAD~1".
# apps-by-git
- https://github.com/w4/rgit /public/202402/rust
  - https://git.inept.dev/
  - A gitweb/cgit-like interface for the modern age. 
  - Written in Rust using Axum, git2, Askama and RocksDB.
  - On-Demand Loading: Files, trees, and diffs are loaded using git2 directly upon request. A small in-memory cache is included for rendered READMEs and diffs, enhancing performance.
  - RocksDB is used to store all metadata about a repository, including commits, branches, and tags.
- https://github.com/yoannfleurydev/gitweb /apache2/202106/rust
  - Open the current remote repository in your browser
  - gitweb is a command line interface I created mainly to learn Rust.
- https://github.com/TooTallNate/node-gitweb /201302/js
  - Directly invoke and serve GitWeb through NodeJS.
  - This module uses `node-cgi` to invoke the` gitweb.cgi` perl file.

- https://github.com/NostrGit/NostrGit /AGPLv3/202304/ts/inactive
  - https://nostrgit.com/
  - censorship-resistant alternative to GitHub
  - 依赖trpc、nextjs、tailwind、shadcn-ui
  - [What are the backend we're thinking of?](https://github.com/NostrGit/NostrGit/discussions/73)
    - Git is the decentralized storage by itself.
    - of course git is decentralised but we still need a clear web repo that people can push upstream. git torrent looks promising
    - NostrGit hosts git servers on a decentralized storage network and uses nostr for everything else
  - [Backend for git repositories](https://github.com/NostrGit/NostrGit/issues/115)
    - Decentralised file storage on Nostr as per NIP-95 seems like a promising option for hosting code. It'll probably be far better than what we have right now.
  - https://github.com/spearson78/gitnostr /go
    - A proof of concept integration of git and nostr
    - Git integration for Nostr that supports creation and cloning of repositories and managing permissions of to access the repositorie

- https://github.com/realaravinth/gitpad /AGPLv3/202206/rust
  - https://gitpad.org/
  - Self-Hosted alternative to GitHub Gists
  - Versioning through Git

- https://github.com/thomiceli/opengist /AGPLv3/202401/go/ts
  - https://demo.opengist.io/
  - Self-hosted pastebin powered by Git
  - All snippets are stored in a Git repository and can be read and/or modified using standard Git commands, or with the web interface. 
  - It is similiar to GitHub Gist, but open-source and could be self-hosted.
# integrations
- https://github.com/mhutchie/vscode-git-graph /NonCommercial/202109/ts/inactive
  - https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph
  - View a Git Graph of your repository in Visual Studio Code, and easily perform Git actions from the graph.
  - Compare any two commits by clicking on a commit, and then CTRL/CMD clicking on another commit
# apps
- https://github.com/creationix/wheaty /201512/js
  - JS-Git based application hosting platform

- [Git as a Database | GitRows](https://gitrows.com/)
  - GitRows makes it easy to use and store data in GitHub and GitLab repos and deliver them with a powerful API.
# examples

# utils
- https://github.com/brawnski/git-annex /hs
  - git-annex allows managing files with git, without checking the file contents into git. 
  - While that may seem paradoxical, it is useful when dealing with files larger than git can currently easily handle, whether due to limitations in memory, checksumming time, or disk space.

- https://github.com/steveukx/git-js /MIT/202402/ts
  - A lightweight interface for running git commands in any node.js application.
  - Requires git to be installed and that it can be called using the command git.

- https://github.com/filhodanuvem/gitql /go
  - a Git query language

- https://github.com/mergestat/mergestat-lite /202308/go
  - https://mergestat.com/
  - a command-line tool for running SQL queries on git repositories and related data sources. 
  - It's meant for ad-hoc querying of source-code on disk through a common interface (SQL)
  - [Gitqlite: Query Git Repositories with SQL | Hacker News_202007](https://news.ycombinator.com/item?id=23730519)

- https://github.com/src-d/gitbase /201910/go
  - a SQL database interface to Git repositories.
  - It can be used to perform SQL queries about the Git history and about the Universal AST of the code itself. gitbase is being built to work on top of any number of git repositories.
  - gitbase implements the MySQL wire protocol, it can be accessed using any MySQL client or library from any language.
  - https://github.com/src-d/go-mysql-server /201910/go
    - An extensible MySQL server implementation in Go.

- https://github.com/developmeh/diff_event_source /rust
  - Creates a diff event source for a given file filter
  - In preparation for a tool that can identify which files have changed in a repo so they can be incrementally published to a knowledge base. I created my first rust CLI that can give produce an event source from libgit2.

- https://github.com/sosuisen/git-documentdb /MPLv2/202304/ts/inactive
  - https://gitddb.com/
  - Offline-first Database that Syncs with Git
  - GitDocumentDB is compatible with Git that brings us distributed multi-primary databases and efficient CI/CD.
  - The throughput of GitDocumentDB is about the same as Git. It is not as fast as typical databases. Storage size grows when managing many revisions of a document. These are a trade-off for Git features.
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
  - [GitDB, a distributed embeddable database on top of Git | Hacker News_202207](https://news.ycombinator.com/item?id=31987240)
# more
