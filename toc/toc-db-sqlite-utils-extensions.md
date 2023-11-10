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

- https://github.com/asg017/sqlite-hello /c
  - The smallest possible "hello world" SQLite extension. 
  - Meant for testing and debugging loadable SQLite extensions.

- https://github.com/nalgeon/sqlean /3.1kStar/MIT/202311/c
  - https://github.com/nalgeon/sqlean/blob/main/docs/stats.md
  - There are a lot of SQLite extensions out there, but they are incomplete, inconsistent and scattered across the internet. sqlean brings them together, neatly packaged into domain modules, documented, tested

- https://github.com/wekan/minio-metadata /202304/js
  - Transfer files from MongoDB GridFS to Minio file server, and MongoDB text to SQLite
  - Bash scripts to transfer attachment and avatar files from MongoDB GridFS to Minio file server
    - To make MongoDB Server database size smaller (like from 800 GB tIo 10 GB), store files elsewhere, and have files visible in upcoming version of WeKan.
    - Meteor WeKan will continue using MongoDB for text data. Files can be stored outside of MongoDB.
    - Upcoming WeKan will use SQLite database for text data. Files are stored outside of SQLite.
# extensions
- https://github.com/asg017/sqlite-loadable-rs
  - A framework for writing fast and performant SQLite extensions in Rust
  - [SQLite-loadable-rs: A framework for building SQLite Extensions in Rust | Hacker News](https://news.ycombinator.com/item?id=33973888)

- https://github.com/asg017/sqlite-lines  /clang/python
  - A SQLite extension for reading large files line-by-line (NDJSON, logs, txt, etc.)

- https://github.com/McMartin/sqlite-undoredo /cpp/py
  - This repository contains code examples written in various programming languages that show how to implement undo/redo logic using SQLite.

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

- https://github.com/chiselstrike/chiselstore /rust
  - an embeddable, distributed SQLite for Rust, powered by Little Raft.
  - ChiselStore extends SQLite to run on a cluster of machines with the Raft consensus algorithm.
  - [Chiselstore: an embeddable, distributed SQLite for Rust | Hacker News_202112](https://news.ycombinator.com/item?id=29572756)
  - https://github.com/andreev-io/little-raft

- [db-helper.ts](https://gist.github.com/surma/53cb57219eea5217d02083b7dd19b711)
  - https://twitter.com/DasSurma/status/1711013536950784460
  - I just wrote a quick JS template tag for SQLite where I can use string interpolation with SQL queries without skipping the driver’s escaping mechanism.
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
  - forks
    - https://github.com/alineacms/sqlite-wasm

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

- https://github.com/froghub-io/ic-sqlite
  - ICSQLite is a cloud SQLite database on Internet Computer and provides SDK for developers to use.
  - Our goal is to help developers quickly migrate web2 applications to Internet Computer.
  - [Internet Computer blockchain](https://internetcomputer.org/)
  - https://github.com/codebase-labs/ic-sqlite

- https://github.com/facebookincubator/CG-SQL /c
  - CG/SQL is a code generation system for the popular SQLite library that allows developers to write stored procedures in a variant of Transact-SQL (T-SQL) and compile them into C code that uses SQLite’s C API to do the coded operations
  - SQLite has no stored procedures of its own. 

- https://github.com/alicebob/sqlittle /202302/go
  - Pure Go SQLite file reader
  - SQLittle reads SQLite3 tables and indexes. It iterates over tables, and can search efficiently using indexes.
  - There is no support for SQL
# file
- https://github.com/narumatt/sqlitefs /202003/rust/inactive
  - allows Linux and MacOS to mount a sqlite database file as a normal filesystem.
  - libfuse(Linux) or osxfuse(MacOS) is requied by fuse-rs

- https://github.com/guardianproject/libsqlfs /LGPLv2/201812/c
  - a library that implements a POSIX style filesystem on top of an SQLite database

- https://github.com/KyleBruene/sqlar /201708/c
  - a proof-of-concept "SQLite Archiver" program. 
  - This program (named "sqlar") operates much like "zip", except that the compressed archive it builds is stored in an SQLite database instead of a ZIP archive.

- https://github.com/alicebob/bakelite /202206/go/inactive
  - Pure Go SQLite file exporter
  - This library writes SQLite files from scratch. You hand it the data you want in the tables, and you get back your . SQLite file.
  - No dependencies. No C. No SQL.
  - dealing with 500Mb files in `Excel` is no fun. Bakelite gives a light way to generate a `.sqlite` file.

- https://github.com/jilio/sqlitefs /202202/go
  - https://github.com/jilio/sqlitefs
- https://github.com/jacobsa/fuse /202310/go
  - This package allows for writing and mounting user-space file systems from Go

- https://github.com/nileshph/Database_Storage_Engine_Implementation /201707/java
  - Relational database storage engine implementation using Java.
  - The goal of this project is to implement a (very) rudimentary database engine that is loosely based on a hybrid between MySQL and SQLite, which I call DavisBase.

- https://github.com/jimsmart/peanut /202301/go
  - a Go package to write tagged data structs to disk in a variety of formats, simply and without ceremony.
  - Its primary purpose is to provide a single consistent interface for easy, ceremony-free persistence of record-based struct data.
  - Currently supported formats are CSV, TSV, Excel (.xlsx), JSON Lines (JSONL), and SQLite. Additional writers are also provided to assist with testing and debugging. 
  - All writers perform atomic file operations, writing data to a temporary location and moving it to the final output location when Close is called.

- https://github.com/simonw/airtable-export /python
  - Export Airtable data to YAML, JSON or SQLite files on disk
  - If you run this command against an existing SQLite database records with matching primary keys will be over-written by new records from the export.
# binary/attachment
- https://gist.github.com/jacobian/5000515 /python
  - Benchmarking MongoDB's GridFS vs PostgreSQL's LargeObjects
# mobile

# gis
- https://github.com/ngageoint/geopackage-js
  - http://ngageoint.github.io/geopackage-viewer-js/
  - an implementation of the OGC GeoPackage spec. 

- https://github.com/jvail/spl.js
  - SpatiaLite for browser & node
# more-conversion-tools
