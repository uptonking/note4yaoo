---
title: toc-db-sqlite
tags: [database, sqlite, toc]
created: 2021-08-21T07:23:30.321Z
modified: 2021-08-30T18:56:18.632Z
---

# toc-db-sqlite

# guide

- ref
  - [wa-sqlite benchmarks](https://rhashimoto.github.io/wa-sqlite/demo/benchmarks.html)
# popular
- sqlite /3.3kStar/public/202212/clang
  - https://github.com/sqlite/sqlite
  - https://sqlite.org/
  - a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine. 
  - https://github.com/sqlite/sqlite/tree/95e961beaae011113aa2431728fbdc5a1a745f58
    - early code in 200007 
  - https://github.com/mackyle/sqlite
    - Unofficial git mirror of SQLite sources
  - https://github.com/rurban/hardsqlite
    - patches for the Hardened SQLite database engine
    - What is really needed would be a hardened sqlite, to rip out the many openssl-like insanities and insecure defaults. 
    - For those who cannot use Dqlite

- kikko /75Star/MIT/202401/ts
  - https://github.com/kikko-land/kikko
  - https://kikko-doc.netlify.app/
  - Powerful SQLite adapter for web, mobile and desktop. Build reactive UI on top of it
  - It brings transaction support, middlewares for queries, and SQLite adapters for the most popular platforms.
  - https://github.com/kikko-land/boono /ts
    - An advanced SQL builder, specially tailored for SQLite
    - That allows supporting all the features SQLite offers.
  - https://github.com/kikko-land/wa-sqlite-web-backend
    - 依赖 wa-sqlite

- harika-note /111Star/AGPLv3/202208/ts
  - https://github.com/quolpr/harika
  - https://app-dev.harika.io/
  - an offline-first, performance-focused note taking app for organizing your knowledge database.
  - Synchronization with server. 
    - It's done with LWW CRDT per field on top of SQLite. 
    - It also stores all changes locally and sends them to server. 
    - Server also store all the changes and recalculate snapshots on new received changes and send those snapshots back to the client. 
    - Due to we store all the changes at server, it is also planned to add time travel, when CRDT is not what user expect at some cases.
  - [I managed to pause work on it because I don't have enough resources (money/time) to keep working on it_202208](https://twitter.com/quolpr/status/1558852687956951044)

- https://github.com/outerbase/studio /AGPLv3/202412/ts
  - https://studio.outerbase.com/
  - A lightweight Database GUI in your browser. 
  - It supports connecting to Postgres, MySQL, and SQLite.
  - a lightweight, browser-based GUI for managing SQL databases, designed for simplicity and versatility. 
  - Initially built for LibSQL and SQLite, it now supports a broad range of databases
  - Outerbase Studio Desktop is a lightweight Electron wrapper for the Outerbase Studio web version. 

- https://github.com/qwtel/sqlite-viewer-vscode  /202501/ts
  - https://sqliteviewer.app/
  - easy SQLite viewer for VSCode, inspired by DB Browser for SQLite and Airtable.
  - [Next version of SQLite Viewer, handling 3 million rows, 1 GB sqlite file, in a browser.](https://twitter.com/qwtel/status/1639204056622321664)
    - Memory usage low despite 1GB file, thanks to OPFS and SQLite WASM
  - [Opening large SQLite files is solved in the (unreleased) web version though.](https://twitter.com/qwtel/status/1644319722178248708)
    - The limit is now how much the browser permits to write into the Origin Private File System.
  - I'm surprised the current version of SQLite Viewer keeps getting good reviews in the vsc marketplace. It flat out crashes if you open a large file. I suppose most sqlite files are small.
    - Unfortunately fixing it would be hard. 
    - vsc's own `fs` module doesn't let you read with random offsets, and even if it did, it would require writing a custom VFS and juggling buffers across 2-3 layers of iframes and workers.
  - https://alpha.sqliteviewer.app/
    - https://twitter.com/qwtel/status/1649018168839372803
    - Can handle much larger SQLite files (tested up to 1.5GB), only limited by storage quota of your browser
    - Fixed virutal scrolling and resizing for very large tables

- sqlime /338Star/MIT/202401/js
  - https://github.com/nalgeon/sqlime
  - http://sqlime.org/
  - an online SQLite playground for debugging and sharing SQL snippets. 
  - Kinda like JSFiddle, but for SQL instead of JavaScript.
  - backed by SQLite, provided by an excellent sql.js project.
  - Connect any local or remote SQLite database. Both files and URLs are supported. 
    - For example, try loading the Employees database from the GitHub repo.

- https://github.com/WebReflection/sqlite-tag-spawned
  - Template literal tag based sqlite3 queries.
  - The same sqlite-tag ease but without the native sqlite3 dependency, aiming to replace dblite.
  - requires SQLite 3.33 or higher (it uses the -json output mode)
- https://github.com/WebReflection/sqlite-worker
  - persistent, SQLite database for Web and Workers, based on sql.js and sqlite-tag.

- libsql /1.8kStar/MIT/202212/clang
  - https://github.com/tursodatabase/libsql
  - https://github.com/libsql/libsql
  - https://libsql.org/
  - a fork of SQLite, to suit many more use cases than SQLite was originally designed for
  - libSQL will always be compatible with the SQLite file format.
  - libSQL will keep 100% compatibility with the SQLite API, but we may add additional APIs.
  - libSQL will always be embeddable, meaning it runs inside your process without needing a network connection. 
  - features
    - randomized ROWID
    - WebAssembly User Defined Functions

- https://github.com/libsql/sqld /MIT/rust
  - sqld is a server mode for libSQL. 
  - Access over HTTP and WebSockets from any Edge platform
  - SQLite-compatible API that you can drop-in with LD_PRELOAD in your application to switch from local database to a remote database.

- https://github.com/chiselstrike/chiselstrike
  - ChiselStrike abstracts common backends components like databases and message queues, and let you drive them from a convenient TypeScript business logic layer
  - ChiselStrike keeps things as close as possible to pure TypeScript, and a translation layer takes care of index creation, database query generation, and even communicating with external systems like Kafka.
  - Internally, ChiselStrike uses a SQLite database 

- https://github.com/x2bool/xlite /rust
  - Query Excel spreadsheets (.xlsx, .xls, .ods) using SQLite
  - allow working with spreadsheets from SQLite exposing them as virtual tables.
  - XLite is a SQLite extension written in Rust. 

- https://github.com/nalgeon/codapi /apache2/202312/go
  - https://codapi.org/
  - Embeddable code playgrounds for education, documentation, and fun.
  - Codapi is a platform for embedding interactive code snippets directly into your product documentation, online course, or blog post.
  - Codapi manages sandboxes (isolated execution environments) and provides an API to execute code in these sandboxes. 
  - It also provides a JavaScript widget codapi-js for easier integration.
  - Custom sandboxes for any programming language, database, or software.
  - Available as a cloud service and as a self-hosted version.
# sqlite-viewer/manager
- https://github.com/inukshuk/sqleton
  - Visualizes your SQLite database schema.

- https://github.com/sqlitebrowser/sqlitebrowser
  - DB Browser for SQLite, Previously known as "SQLite Database Browser"
  - 基于qt和c++实现

- https://github.com/egoist/querybase /AGPL/202501/ts
  - A simple and smart GUI client for PostgreSQL, MySQL, SQLite

- https://github.com/cyrilbois/Web-GUI-for-SQLite
  - a web-based SQLite browser written in JavaScript.

- https://github.com/inloop/sqlite-viewer /apache2/202401/js
  - http://inloop.github.io/sqlite-viewer
  - View SQLite file online
  - Uses sql.js for parsing sqlite files.
  - You can also load remote files (using JS ajax, remote server must send Access-Control-Allow-Origin:*)
  - No file will be uploaded - uses only JavaScript HTML5 `FileReader`.

- https://github.com/pawelsalawa/sqlitestudio /GPLv3/202309/c/qt
  - https://sqlitestudio.pl/
  - multi-platform SQLite database manager written in C++, with use of Qt framework
# powered-by-sqlite
- https://github.com/datopian/markdowndb /MIT/202401/ts/sqlite
  - https://markdowndb.com/
  - JS library to turn markdown files into structured queryable database (SQL-based and simple JSON). 
  - It helps you build rich markdown-powered sites easily
  - Parses your markdown files to extract structured data (frontmatter, tags etc) and creates an index in a local `SQLite` database
  - Provides a lightweight javascript API for querying the database and importing files into your application

- https://github.com/dpapathanasiou/simple-graph /sql
  - This is a simple graph database in SQLite, inspired by "SQLite as a document database"
  - The schema consists of just two structures: Nodes(json) and Edges({id:json})
  - There are also traversal function templates as native SQLite Common Table Expressions which produce lists of identifiers or return all objects along the path.
  - [SQLite as a document database_202006](https://dgl.cx/2020/06/sqlite-json-support)
  - [SQLite as a Document Database | Hacker News_202011](https://news.ycombinator.com/item?id=25226260)

- https://github.com/thenorthbay/doculite /ts
  - Use SQLite as a Document Database
  - DocuLite lets you use SQLite like Firebase Firestore. 
  - It's written in Typescript and an adapter on top of sqlite3 and sqlite. 
  - It support listeners on documents, collections, and basic queries.
  - [Show HN: Doculite – Use SQLite as a Document Database | Hacker News_202308](https://news.ycombinator.com/item?id=37040359)

- https://github.com/rqlite/rqlite /go
  - distributed relational database built on SQLite
  - How is it different than dqlite?
    - dqlite is library, written in C. rqlite is a standalone application -- it's a full RDBMS (albeit a relatively simple one). rqlite has everything you need to read and write data, and backup, maintain, and monitor the database itself.
  - How is it different than Litestream?
    - Litestream adds reliability to a system using SQLite by periodically backing-up the SQLite database to something like AWS S3. If you lose the node running your SQLite database, you must restore it from your backup.
    - Litestream does this in a very elegant way, and doesn't change how applications interact with SQLite. 
    - rqlite, in contrast, adds reliability and high-availability via clustering. 
  - [Rqlite: The lightweight, distributed relational database built on SQLite | Hacker News_202101](https://news.ycombinator.com/item?id=25871605)
  - https://github.com/rqlite/rqlite-js
    - promise based client library for rqlite
  - https://github.com/dkulchenko/watchdb /go/inactive
    - a tool that enables quick setup of master-slave synchronization for SQLite databases across a network.
    - Synchronization is one-way only (changes made on the master will overwrite changes made on slaves). Slave databases are kept read-only to prevent accidental writes from application code.
    - watchdb replication is eventually consistent by design, so it's AP in CAP. If you need strong consistency (at the expense of performance and required changes to application code), take a look at rqlite.

- https://github.com/rusqlite/rusqlite /MIT/202312/rust
  - an ergonomic wrapper for using SQLite from Rust.
  - Historically, the API was based on the one from rust-postgres. However, the two have diverged in many ways, and no compatibility between the two is intended.

- https://github.com/litements/s3sqlite /python
  - Query SQLite databases in S3 using s3fs
  - [Show HN: Query SQLite files stored in S3 | Hacker News](https://news.ycombinator.com/item?id=32828799)

- https://github.com/benbjohnson/postlite /202203/go/inactive
  - a proof of concept of wrapping SQLite with the Postgres wire protocol.
  - Postlite is a network proxy to allow access to remote SQLite databases over the Postgres wire protocol.
  - The proxy works by translating Postgres frontend wire messages into SQLite transactions and converting results back into Postgres response wire messages.
  - Postlite expects you to connect over the postgres wire protocal. Sqld is compiled into your application so your application behaves like it's talking to an embedded sqlite, the calls are then made over the network (using one of three available transports) before being returning to your application.

- https://github.com/benbjohnson/litestream /202211/go
  - Streaming replication for SQLite.
  - Litestream is a standalone disaster recovery tool for SQLite. 
  - It runs as a background process and safely replicates changes incrementally to another file or S3. 
  - Litestream only communicates with SQLite through the SQLite API so it will not corrupt your database.
  - https://github.com/fly-apps/superfly
# sqlite-rewrite
- https://github.com/joaoh82/rust_sqlite /1kStar/MIT/202207/rust/inactive/代码量不大
  - a simple embedded database modeled off SQLite, but developed with Rust. 
  - The goal is get a better understanding of database internals by building one.
  - [SQLRite – SQLite clone from scratch in Rust | Hacker News_202104](https://news.ycombinator.com/item?id=26749737)
  - [What would SQLite look like if written in Rust? — Part 3_202104](https://medium.com/the-polyglot-programmer/what-would-sqlite-look-like-if-written-in-rust-part-3-edd2eefda473)
  - [Column or row oriented store](https://github.com/sqlrite/design/discussions/6)

- https://github.com/tursodatabase/turso /13kStar/MIT/202508/rust
  - https://github.com/penberg/limbo /legacy
  - Limbo is a work-in-progress, in-process OLTP database management system, compatible with SQLite.
  - In-process OLTP database engine library
  - Asynchronous I/O support with io_uring
  - 已合并: [Rename Limbo to Turso Database _202506](https://github.com/tursodatabase/turso/pull/1835)
  - https://x.com/penberg/status/1809295488933384615 _202407
    - Me and @Peristocles1 have been hacking on an in-process database in Rust that aims for SQLite compatibility, but with an asynchronous architecture (but no Tokio) to support things like io_uring
    - I am not using async Rust because I want more control over memory allocations, for example. With futures, it becomes hard because you end up creating bunch of closures implicitly.
    - Sounds similar to the goals of libsql. Are there any other differences?
      - The two projects have different goals. libSQL extends SQLite with things like replication and vector search, but is SQLite at the core. This is a project to write a SQLite compatible library from scratch.
    - doesn’t durability go to toss when using io_uring (any async primitive)? 
      - Async means you have the opportunity to do other things while I/O is on flight. You don’t lose durability with io_uring because transaction commit won’t happen until I/O is complete
      - The architecture of Limbo is designed for asynchronous I/O like io_uring, but with durability in mind.
    - This sounds very similar to Sled? Minus SQLite compat
      - Sled is a more advanced storage engine than what we have because we’re focusing on reproducing SQLite’s storage model and will improve later.
    - Curious what's the major challenge here? Can you share some insights?
      - The major challenge is compatibility and the volume of the work. The beauty of SQLite is that the core architecture is simple, yet efficient and fast, and as such pretty straight-forward to reimplement, but there's just a lot of it.
    - Are you planning for the library to be for single thread usage only? I see Rc being used instead of Arc.
      - Single-threaded because it allows the application to figure out locking scheme and it makes deterministic simulation testing easy. The current performance numbers suggest you can get to 500k reads per second easily, which should be plenty for the types of workloads SQLite runs

- https://github.com/cstack/db_tutorial /clang
  - Writing a sqlite clone from scratch in C
  - B-Tree Leaf Node Format
  - prepare_statement (our “SQL Compiler”) does not understand SQL right now. In fact, it only understands two words select and insert
  - [How Does a Database Work? | Let’s Build a Simple Database](https://cstack.github.io/db_tutorial/)
  - [Writing a SQLite clone from scratch in C (2017) | Hacker News](https://news.ycombinator.com/item?id=27731966)
- https://github.com/KCNyu/db_tutorial_cpp /cpp
  - 如何用C++实现一个简易数据库, 基于cstack/db_tutorial C语言版本

- https://github.com/c-bata/db_tutorial /rust
  - Writing a sqlite clone from scratch in Rust (and Python3 for testing).
- https://github.com/pmk21/rsqlite /rust
  - A simple SQLite clone in Rust. This is basically a translation of the C code
  - A simple SQLite clone in Rust. This is basically a translation of the C code

- https://github.com/spandanb/learndb-py /202308/python
  - Learn database internals by implementing it from scratch
  - the goal of this project is to better understand the internals of databases by implementing a relational database management system (RDBMS) (sqlite clone) from scratch.
  - [Show HN: I wrote a RDBMS (SQLite clone) from scratch in pure Python | Hacker News_202308](https://news.ycombinator.com/item?id=37114141)

- https://gitlab.com/cznic/sqlite /BSD/go
  - http://godoc.org/modernc.org/sqlite
  - Package sqlite is a sql/database driver using a CGo-free port of the C SQLite3 library.
  - modernc.org/sqlite is an automatically generated translation of the original C source code of SQLite into Go. It passes the full SQLite test suite.
  - [SQLite in Go, with and without cgo_202205](https://datastation.multiprocess.io/blog/2022-05-12-sqlite-in-go-with-and-without-cgo.html)
  - [SQLite in Go, with and Without Cgo | Hacker News_202205](https://news.ycombinator.com/item?id=31364166)
  - https://github.com/zombiezen/go-sqlite /go
    - Low-level Go interface to SQLite 3
    - It is a fork of crawshaw.io/sqlite that uses modernc.org/sqlite
    - It includes APIs for streaming blob I/O, schema migrations, and user-defined functions.
    - [New advanced, CGo-free SQLite package_202104](https://www.reddit.com/r/golang/comments/n1u2b1/new_advanced_cgofree_sqlite_package/)

- https://github.com/LMDB/sqlightning /201504/c/inactive
  - SQLite3 ported to use LMDB instead of its original Btree code.
  - LumoSQL as a fork
  - SQLightning greatly improved SQLite performance but due to LMDB's requirement to have keys fit in 2/3 of a page it wasn't really useful as a general purpose replacement of SQLite's internal b-tree implementation.
- https://github.com/LumoSQL/LumoSQL /MIT/c
  - a modification (not a fork) of the SQLite
  - LumoSQL adds security, privacy, performance and measurement features to SQLite. 
  - LumoSQL can swap back end key-value store engines in and out of SQLite.

## sqlite-like

- https://github.com/lucavallin/gnaro /MIT/202310/clang
  - https://cavall.in/
  - A proto-database inspired by SQLite, written in C for educational purposes. 
  - gnaro takes SQLite as a reference because of the limited feature set, and therefore complexity, when compared to other databases. 

- dqlite /3.6kStar/LGPLv3/202310/clang/canonical
  - https://github.com/canonical/dqlite
  - a C library that implements an embeddable and replicated SQL database engine with high-availability and automatic failover.
  - dqlite extends SQLite with a network protocol that can connect together various instances of your application and have them act as a highly-available cluster, with no dependency on external databases.
  - Data replication based on the Raft algorithm and its efficient `C-raft` implementation.
  - Asynchronous single-threaded implementation using libuv as event loop
  - Custom wire protocol optimized for SQLite primitives and data types.
  - dqlite runs on Linux and requires a kernel with support for native async I/O (not to be confused with POSIX AIO), which is used by the libuv backend of C-raft.
  - [Embeddable, replicated and fault tolerant SQL engine based on Sqlite | Hacker News_202202](https://news.ycombinator.com/item?id=30135401)
    - What I found to be the biggest problem with SQLite is concurrent write operations. WAL helps for concurrent read but not for concurrent write.
      - On a moderate use case (< 20 write operations per s) I kept getting timeouts so I first devised a quick fix system using RQ jobs passing writes to a single process and migrated to postgres as fast as I could.
    - With exclusive access using a single connection in WAL mode, I can insert tens of thousands of rows per second on flash storage no problem.

- https://github.com/CsharpDatabase/csharp-sqlite /201401/inactive
  - C# port of the SQLite library
  - https://code.google.com/archive/p/csharp-sqlite/

- https://github.com/adargut/SQLiteClone /cpp
  - Clone of SQLite written in C/C++, using B-trees
# more
- https://github.com/loladb/nodejs-examples
  - https://loladb.com/
  - LolaDB is an HTTP client that pulls all your db clients on a centralized server infra & wraps the calls into a unified interface 

- https://github.com/haltcase/trilogy /MIT/202205/ts/inactive
  - https://trilogy.js.org/
  - a simple Promise-based wrapper for SQLite databases. 
  - It supports both the native C++ sqlite3 driver and the pure JavaScript sql.js backend
  - It's not an ORM and isn't intended to be one — it doesn't have any relationship features.
  - Instead it focuses on providing a simple, clear API that's influenced more by Mongoose than by SQL.
  - trilogy uses knex internally to build its queries, but it's also exposed so you can use it to build your own. 
  - supports multiple swappable backends ( plus in-memory storage )
    - Both the native sqlite3 module and sql.js (pure JavaScript!) are supported. There is also memory-only storage for fast, unpersisted data handling

- https://github.com/subzerocloud/showcase
  - subZero is a library implemented in Rust with JS/TypeScript bindings that allows you to expose a PostgREST compatible backend on top of any database.
