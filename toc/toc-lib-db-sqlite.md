---
title: toc-lib-db-sqlite
tags: [database, sqlite, toc]
created: '2021-08-21T07:23:30.321Z'
modified: '2021-08-21T07:25:20.512Z'
---

# toc-lib-db-sqlite

# popular

- https://github.com/jlongster/absurd-sql
  - sqlite3 in ur indexeddb (hopefully a better backend soon)
  - It implements a backend for sql.js (sqlite3 compiled for the web) that treats IndexedDB like a disk and stores data in blocks there. 
  - That means your sqlite3 database is persisted. 
  - And not in the terrible way of reading and writing the whole image at once -- it reads and writes your db in small chunks.

- https://github.com/sql-js/sql.js
  - http://sql.js.org/
  - A javascript library to run SQLite on the web.
  - sql.js is a javascript SQL database. 
  - It allows you to create a relational database and query it entirely in the browser.
  - sql.js uses emscripten to compile SQLite to webassembly (or to javascript code for compatibility with older browsers). 
  - It uses a virtual database file stored in memory, and thus doesn't persist the changes made to the database. 
  - However, it allows you to import any existing sqlite file, and to export the created database as a JavaScript typed array.
# extensions

# examples

# more
