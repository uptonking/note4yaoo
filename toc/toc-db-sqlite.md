---
title: toc-db-sqlite
tags: [database, sqlite, toc]
created: 2021-08-21T07:23:30.321Z
modified: 2021-08-30T18:56:18.632Z
---

# toc-db-sqlite

# popular

- kikko /75Star/MIT/202211/ts
  - https://github.com/kikko-land/kikko
  - https://kikko-doc.netlify.app/
  - Powerful SQLite adapter for web, mobile and desktop. Build reactive UI on top of it
  - It brings transaction support, middlewares for queries, and SQLite adapters for the most popular platforms.
  - https://github.com/kikko-land/boono
    - While other builders tend to be universal, Boono is specially tailored for SQLite. 
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

- sqlime /338Star/MIT/202204/js
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
  - https://github.com/libsql/libsql
  - https://libsql.org/
  - a fork of SQLite, to suit many more use cases than SQLite was originally designed for
  - libSQL will always be compatible with the SQLite file format.
  - libSQL will keep 100% compatibility with the SQLite API, but we may add additional APIs.
  - libSQL will always be embeddable, meaning it runs inside your process without needing a network connection. 
  - features
    - randomized ROWID
    - WebAssembly User Defined Functions
- https://github.com/chiselstrike/chiselstrike
  - ChiselStrike abstracts common backends components like databases and message queues, and let you drive them from a convenient TypeScript business logic layer
  - ChiselStrike keeps things as close as possible to pure TypeScript, and a translation layer takes care of index creation, database query generation, and even communicating with external systems like Kafka.
  - Internally, ChiselStrike uses a SQLite database 

- https://github.com/x2bool/xlite /rust
  - Query Excel spredsheets (.xlsx, .xls, .ods) using SQLite
  - allow working with spreadsheets from SQLite exposing them as virtual tables.
  - XLite is a SQLite extension written in Rust. 
# sqlite-viewer
- https://github.com/qwtel/sqlite-viewer-vscode  /ts
  - https://sqliteviewer.app/
  - easy SQLite viewer for VSCode, inspired by DB Browser for SQLite and Airtable.

- https://github.com/inukshuk/sqleton
  - Visualizes your SQLite database schema.

- https://github.com/sqlitebrowser/sqlitebrowser
  - DB Browser for SQLite, Previously known as "SQLite Database Browser"
  - 基于qt和c++实现

- https://github.com/egoist/querybase
  - Desktop GUI for PostgreSQL, SQLite, and MySQL.

- https://github.com/cyrilbois/Web-GUI-for-SQLite
  - a web-based SQLite browser written in JavaScript.

- https://github.com/inloop/sqlite-viewer
  - View SQLite file online
# db-powered-by-sqlite
- https://github.com/rqlite/rqlite
  - distributed relational database built on SQLite
  - https://github.com/rqlite/rqlite-js
    - promise based client library for rqlite
# sqlite-rewrite
- https://github.com/joaoh82/rust_sqlite
  - a simple embedded database modeled off SQLite, but developed with Rust. 
  - The goal is get a better understanding of database internals by building one.

- https://gitlab.com/cznic/sqlite /go
  - a CGo-free port of SQLite/SQLite3 in go

- https://github.com/LMDB/sqlightning
  - SQLite3 ported to use LMDB instead of its original Btree code.
- https://github.com/LumoSQL/LumoSQL
  - a modification (not a fork) of the SQLite
  - LumoSQL adds security, privacy, performance and measurement features to SQLite.
  - LumoSQL can swap back end key-value store engines in and out of SQLite. 
# more
- https://github.com/loladb/nodejs-examples
  - https://loladb.com/
  - LolaDB is an HTTP client that pulls all your db clients on a centralized server infra & wraps the calls into a unified interface 

- https://github.com/haltcase/trilogy
  - trilogy is a simple Promise-based wrapper for SQLite databases. 
  - It supports both the native C++ sqlite3 driver and the pure JavaScript sql.js backend
  - It's not an ORM and isn't intended to be one — it doesn't have any relationship features. 
  - Instead it focuses on providing a simple, clear API that's influenced more by Mongoose than by SQL.

- https://github.com/subzerocloud/showcase
  - subZero is a library implemented in Rust with JS/TypeScript bindings that allows you to expose a PostgREST compatible backend on top of any database.
