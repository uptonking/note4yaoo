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
  - Build data heavy reactive interfaces on top of SQLite for any platform with any framework or lib.
  - Kikko is a wrapper around SQLite interfaces. 
  - It brings transaction support, middlewares for queries, and SQLite adapters for the most popular platforms.
  - https://github.com/kikko-land/boono
    - While other builders tend to be universal, Boono is specially tailored for SQLite. 
    - That allows supporting all the features SQLite offers.
  - https://github.com/kikko-land/wa-sqlite-web-backend
    - 依赖 wa-sqlite

- https://github.com/quolpr/harika
  - Harika is an offline-first, performance-focused note taking app for organizing your knowledge database.
  - Synchronization with server. It's done with LWW CRDT per field on top of SQLite. 
    - It also stores all changes locally and sends them to server. 
    - Server also store all the changes and recalculate snapshots on new received changes and send those snapshots back to the client. 
    - Due to we store all the changes at server, it is also planned to add time travel, when CRDT is not what user expect at some cases.

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
# more
- https://github.com/haltcase/trilogy
  - trilogy is a simple Promise-based wrapper for SQLite databases. 
  - It supports both the native C++ sqlite3 driver and the pure JavaScript sql.js backend
  - It's not an ORM and isn't intended to be one — it doesn't have any relationship features. 
  - Instead it focuses on providing a simple, clear API that's influenced more by Mongoose than by SQL.

- https://github.com/subzerocloud/showcase
  - subZero is a library implemented in Rust with JS/TypeScript bindings that allows you to expose a PostgREST compatible backend on top of any database.
