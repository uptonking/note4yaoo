---
title: toc-db-sqlite-utils-extensions
tags: [sqlite, toc, utils]
created: 2022-11-04T14:20:17.787Z
modified: 2022-11-04T14:20:37.172Z
---

# toc-db-sqlite-utils-extensions

# popular
- https://github.com/WiseLibs/better-sqlite3
  - The fastest and simplest library for SQLite3 in Node.js.
  - https://github.com/beenotung/better-sqlite3-proxy
    - Efficiently proxy sqlite tables and access data as typical array of objects

- https://github.com/benbjohnson/litestream /202211/go
  - Streaming replication for SQLite.
  - Litestream is a standalone disaster recovery tool for SQLite. 
  - It runs as a background process and safely replicates changes incrementally to another file or S3. 
  - Litestream only communicates with SQLite through the SQLite API so it will not corrupt your database.
# extensions
- https://github.com/asg017/sqlite-lines  /clang/python
  - A SQLite extension for reading large files line-by-line (NDJSON, logs, txt, etc.)

- https://github.com/wangfenjin/simple
  - 支持中文和拼音的 SQLite fts5 全文搜索扩展
  - A SQLite3 fts5 tokenizer which supports Chinese and PinYin
  - https://www.sqlite.org/fts5.html

- https://github.com/cldellow/sqlite-parquet-vtable
  - A SQLite virtual table extension to expose Parquet files as SQL tables. 
  - You may also find csv2parquet useful.

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

- https://github.com/jayralencar/sqlite-sync.js /202108/js
  - Node module to sqlite sync and async
  - node.js package for database connection with SQLite , and execute SQL commands synchronously or asynchronously.
# excel
- https://github.com/x2bool/xlite /202210/rust
  - SQLite extension for querying Excel (.xlsx, .xls, .ods) files as virtual tables

- https://github.com/thombashi/sqlitebiter /202203/python
  - a CLI tool to convert CSV / Excel / HTML / JSON / Jupyter Notebook / LDJSON / LTSV / Markdown / SQLite / SSV / TSV / Google-Sheets to a SQLite database file.
# search
- https://github.com/kbumsik/blogsearch /202007/ts
  - a pure client-side, full-text search engine for static websites, powered by SQLite compiled to WebAssembly.
  - The search engine basically is SQLite with the FTS5 extension, compiled to WebAssembly. 
  - The SQLite FTS5 offers the built-in BM25 ranking algorithm for the search functionality.
  - https://github.com/kbumsik/sqlite-wasm
    - Run SQLite on the web, using WebAssembly
    - a fork of sql.js with the following changes in typescript
    - This is a reimplementation of sql.js in TypeScript.

- https://github.com/leodr/fulltext-search-static-sqlite
  - An unsuccessful attempt of performing full-text search without a server with static site hosting.
  - I thought it might be possible to do full-text search with SQLite in the browser without loading the entire database, by using HTTP range requests, as sql.js-httpvfs.
  - Turns out this does not really work for queries that use the LIKE keyword. The querying does indeed work, but the whole database is loaded. Then SQL is not really all that helpful, we could easily load a JSON file that contains all the data we want to search through and use something like Fuse.js to perform the search.

- https://github.com/thejimmyg/express-sqlite-search /201901/js
  - Simple express web seach engine backed by SQLite FTS5
- https://github.com/CrispenGari/SQLite3-with-knex-express-API
  - basic search engine with crawling/searching. SQLite for storage.
- https://github.com/sixteenmillimeter/frameworks_search
  - Scripts for building a Postgres database of the frameworks archives and searching that database
# utils
- https://github.com/simonw/sqlite-utils
  - Python CLI utility and library for manipulating SQLite databases

- https://github.com/simonw/csvs-to-sqlite
  - Convert CSV files into a SQLite database

- https://github.com/mandel59/mojidata
  - CJKV character database and search utilities
  - Mojidata Character Database： provides a SQLite database with CJKV character data.
# mobile

# gis
- https://github.com/ngageoint/geopackage-js
  - http://ngageoint.github.io/geopackage-viewer-js/
  - an implementation of the OGC GeoPackage spec. 

- https://github.com/jvail/spl.js
  - SpatiaLite for browser & node
# more-conversion-tools
