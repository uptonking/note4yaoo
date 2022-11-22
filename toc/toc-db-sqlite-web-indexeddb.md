---
title: toc-db-sqlite-web-indexeddb
tags: [indexeddb, sqlite, toc, web]
created: 2022-06-03T22:12:22.597Z
modified: 2022-11-06T03:19:28.284Z
---

# toc-db-sqlite-web-indexeddb

# popular
- https://github.com/uglyer/storelite.js
  - 基于sql.js(sqlite)实现的状态仓库，支持 web worker、react 绑定

- absurd-sql /3.6kStar/MIT/202110/js
  - https://github.com/jlongster/absurd-sql
  - sqlite3 in ur indexeddb (hopefully a better backend soon)
  - It implements a backend for sql.js (sqlite3 compiled for the web) that treats IndexedDB like a disk and stores data in blocks there. 
  - That means your sqlite3 database is persisted. 
  - And not in the terrible way of reading and writing the whole image at once -- it reads and writes your db in small chunks.
  - https://github.com/nikochan2k/absurd-sql-ts
    - Typescript version of absurd-sql
  - https://github.com/monlovesmango/nostr-absurd-sql
    - nostr utility for sqlite3 saved to indexeddb



- sql.js /10.8kStar/MIT/202209/js
  - https://github.com/sql-js/sql.js
  - http://sql.js.org/
  - A javascript library to run SQLite on the web.
  - sql.js is a javascript SQL database. 
  - It allows you to create a relational database and query it entirely in the browser.
  - sql.js uses `emscripten` to compile SQLite to webassembly (or to javascript code for compatibility with older browsers). 
  - It uses a virtual database file stored in memory, and thus doesn't persist the changes made to the database. 
  - However, it allows you to import any existing sqlite file, and to export the created database as a JavaScript typed array.
- https://github.com/wireapp/websql  /202005/inactive
  - websql is a fork of sql.js 
  - Database is persisted to IndexedDB, and can be synced using the saveChanges API

- https://github.com/ccorcos/tuple-database
  - The local-first, "end-user database" database.
  - All queries are reactive.

- https://github.com/tr1ckydev/great.db
  - human-friendly database library for JavaScript using SQLite. 
  - great.db automatically detects which runtime you are using and uses the respective fastest between better-sqlite3/bun-sqlite  
# sqlite-web-examples
- https://github.com/lunu-bounir/sqlite-manager
  - a browser extension to read, manipulate, plot and write SQLite databases
# sqlite-indexeddb
- https://github.com/yanli0303/sql-js-worker-test
  - sql.js tests with IndexedDB as storage and Worker.

- https://github.com/littledivy/indexeddb-sqlite
  - Indexed DB Implementation
  - 单文件测试idea
# wasm
- https://github.com/mandel59/sqlite-wasm
  - SQLite compiled to WebAssembly
- https://github.com/rhashimoto/wa-sqlite
  - This is a WebAssembly build of SQLite with experimental support for writing SQLite virtual filesystems and virtual table modules completely in Javascript. 
  - This allows alternative browser storage options such as IndexedDB and File System Access.

- https://github.com/overtone-app/sqlite-wasm-esm
  - The new SQLite WASM build is rather hard to use in modern JS apps, so this wrapper package tries to make this easier.
# more-sqlite-web
