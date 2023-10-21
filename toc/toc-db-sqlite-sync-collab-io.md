---
title: toc-db-sqlite-sync-collab-io
tags: [collaboration, sqlite, toc]
created: 2022-11-04T14:20:43.842Z
modified: 2022-11-04T14:21:31.365Z
---

# toc-db-sqlite-sync-collab-io

# guide
- 参考sqlite+http-range的部分下载示例(sql.js-httpvfs)
# export/import
- https://github.com/fitnr/sqlite-json

- https://github.com/isaiahnields/csv-to-sqlite
  - A desktop app to convert CSV files to SQLite databases!
# sync
- https://github.com/orbitinghail/sqlsync /rust
  - a collaborative offline-first wrapper around SQLite. 
  - It is designed to synchronize web application state between users, devices, and the edge.
  - Eventually consistent SQLite
  - Optimistic reads and writes
  - Cross-tab sync

- https://github.com/superfly/litefs /apache2/go
  - FUSE-based file system for replicating SQLite databases across a cluster of machines
  - It works as a passthrough file system that intercepts writes to SQLite databases in order to detect transaction boundaries and record changes on a per-transaction level in LTX files.
  - It's a goal of LiteFS to pass the SQLite TCL test suite
  - [Skip the API, Ship Your Database · The Fly Blog](https://fly.io/blog/skip-the-api/)
  - https://github.com/superfly/litevfs
    - a Virtual Filesystem extension for SQLite that uses LiteFS Cloud as a backing store.

- https://github.com/aNinjaMonk/sync-server /201911/js
  - Syncing between local SQLite & remote PostgreSQL

- https://github.com/rla/sql-sync /201306/js
  - Offline replication between SQLite (clients) and MySQL (master). 

- https://github.com/rkusa/do-sqlite
  - Persist SQLite in a Cloudflare Durable Object

- https://github.com/cannadayr/git-sqlite
  - git-sqlite is a collection of shell scripts that allows a sqlite database to be tracked using the git version control system.
  - It can be used on an existing database, however, UUIDs will make multi-master distribution substantially easier.
  - Instead of storing the transactions as a separate lmdb commit, I decided to store the database in a git repository and expose the diffs using sqlite's sqldiff utility. This allowed my workflow to be almost unchanged and limits the dependencies to git, sqlite, sqldiff, & bash.

- https://github.com/StratoKit/strato-db /7Star/MIT/202307/js
  - MaybeSQL with Event Sourcing based on SQLite
  - This project is used in production environments.
  - It works fine with multi-GB databases, and if you choose your queries and indexes well, you can have <1ms query times.
  - Multi-process behavior is not very worked out for the EventSourcingDB
# collab
- https://github.com/samwillis/yjs-sqlite-test
  - http://samwillis.co.uk/yjs-sqlite-test/
  - This is a test project to combine yjs and sqlite wasm, it lets you store yjs documents in a sqlite database, update them in place and query the content. 
  - Perfect for building a local first web app.

- https://github.com/tomatkungen/indexeddb-sqlite-json
  - sqlite3 Json1 Extension Wrapper for Indexeddb

- https://github.com/vlcn-io/cr-sqlite /MIT/rust/ts
  - https://vlcn.io/
  - CR-SQLite is a run-time loadable extension for SQLite and libSQL. 
  - It allows merging different SQLite databases together that have taken independent writes.
  - This project implements CRDTs and CRRs in SQLite, allowing databases that share a common schema to merge their state together.
  - crsqlite works by adding metadata tables and triggers around your existing database schema. 
  - crsqlite only keeps an extra int per column and a clock per row.
  - [expo： [POC][sqlite] Investigate possibility of using crsqlite in expo-sqlite which allows database syncing between clients · expo/expo](https://github.com/expo/expo/pull/23728)
- https://github.com/vlcn-io/vlcn-orm /ts
  - a schema layer whose first goal is to make P2P & Local-First software easy to develop
  - everything in Aphrodite begins with a schema. This schema encodes the application's data, its relationships, consistency rules, allowed mutations and privacy.
  - Aphrodite Schemas are written in a DSL.
  - [IndexedDB support?](https://github.com/vlcn-io/vlcn-orm/issues/48)
- https://github.com/vlcn-io/orm-browser-starter
  - Aphrodite running and saving data locally in the browser
- https://github.com/tantaman/Strut
  - collaborative editing and offline support, powered by vlcn.io

- https://github.com/mycelial/mycelite /rust
  - https://mycelial.com/
  - Mycelite is a SQLite extension that allows you to synchronize changes from one instance of SQLite to another
  - Currently, it only supports one-way synchronization, but eventually, it will support two-way synchronization.
# more
