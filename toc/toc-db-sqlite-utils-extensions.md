---
title: toc-db-sqlite-utils-extensions
tags: [sqlite, toc, utils]
created: 2022-11-04T14:20:17.787Z
modified: 2022-11-04T14:20:37.172Z
---

# toc-db-sqlite-utils-extensions

# rest-api

- https://github.com/olsonpm/sqlite-to-rest
  - Koa routing middleware allowing you to expose a sqlite database via RESTful CRUD

- https://github.com/thevahidal/soul
  - Soul is command line tool, 
  - after installing it, Run soul -d sqlite.db -p 8000 and it'll start a REST API on http://localhost:8000 and a Websocket server on ws://localhost:8000.
  - It should return a list of the tables inside sqlite.db database.

- https://github.com/assafmo/SQLiteProxy
  - A simple HTTP JSON proxy for SQLite.
  - Must use HTTP POST with content-type=application/json.

- https://github.com/TeamThinkpad/express-typescript-api
  - API created using Typescript, Express, and SQLite using the Prisma ORM

- https://github.com/machelslack/api-with-sqlite
  - node express api using a sqlite in memory database
# extensions
- https://github.com/asg017/sqlite-lines  /clang/python
  - A SQLite extension for reading large files line-by-line (NDJSON, logs, txt, etc.)

- https://github.com/wangfenjin/simple
  - 支持中文和拼音的 SQLite fts5 全文搜索扩展
  - A SQLite3 fts5 tokenizer which supports Chinese and PinYin
  - https://www.sqlite.org/fts5.html

- https://github.com/dumblob/mysql2sqlite
  - Converts MySQL dump to SQLite3 compatible dump (including MySQL KEY xxxxx statements from the CREATE block).
  - The script is written in awk (tested with gawk, but should work with original awk, and the lightning fast mawk) and shall be fully POSIX compliant.
- https://github.com/techouse/sqlite3-to-mysql
  - simple Python tool to transfer data from SQLite 3 to MySQL.

- https://github.com/caiiiycuk/postgresql-to-sqlite
  - create sqlite database from postgresql dump.
  - 依赖scala
- https://github.com/nikotrone/sqlite-to-postgres
  - convert an SQLite database dump into a PostgreSQL importable dump

- https://github.com/dimitri/pgloader
  - Migrate to PostgreSQL in a single command!
  - MySQL/SQLite/MSSQL to PSQL
# utils

# mobile

# wasm
- https://github.com/mandel59/sqlite-wasm
  - SQLite compiled to WebAssembly
- https://github.com/rhashimoto/wa-sqlite
  - This is a WebAssembly build of SQLite with experimental support for writing SQLite virtual filesystems and virtual table modules completely in Javascript. 
  - This allows alternative browser storage options such as IndexedDB and File System Access.

- https://github.com/overtone-app/sqlite-wasm-esm
  - The new SQLite WASM build is rather hard to use in modern JS apps, so this wrapper package tries to make this easier.
# gis
- https://github.com/ngageoint/geopackage-js
  - http://ngageoint.github.io/geopackage-viewer-js/
  - an implementation of the OGC GeoPackage spec. 

- https://github.com/jvail/spl.js
  - SpatiaLite for browser & node
# more-conversion-tools
