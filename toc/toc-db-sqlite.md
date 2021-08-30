---
title: toc-db-sqlite
tags: [database, sqlite, toc]
created: '2021-08-21T07:23:30.321Z'
modified: '2021-08-30T18:56:18.632Z'
---

# toc-db-sqlite

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

- https://github.com/realm/realm-js
  - Realm is a mobile database: an alternative to SQLite & key-value stores
  - Realm is a mobile database that runs directly inside phones, tablets or wearables. 
  - Currently we support React Native (both iOS & Android), Node.js and Electron (on Windows, MacOS and Linux).
# extensions
- https://github.com/olsonpm/sqlite-to-rest
  - Koa routing middleware allowing you to expose a sqlite database via RESTful CRUD

- https://github.com/sqlitebrowser/sqlitebrowser
  - DB Browser for SQLite, Previously known as "SQLite Database Browser"
  - 基于qt和c++实现

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

- more-conversion-tools
  - https://github.com/fitnr/sqlite-json
  - https://github.com/isaiahnields/csv-to-sqlite
# examples
- https://github.com/patrickmoffitt/local-sqlite-example
  - This project demonstrates how to install and use a local SQLite3 database in Electron using SQL.js.

- https://github.com/lana-k/sqliteviz
  - https://lana-k.github.io/sqliteviz/
  - 依赖vue2、jquery、pivottable、plotly.js.v1、sql.js、react-chart-editor
  - 依赖很多plotly的产品
  - Instant offline SQL-powered data visualisation in your browser
  - Sqliteviz is a single-page offline-first PWA for fully client-side visualisation of SQLite databases or CSV files.

- https://github.com/app-generator/api-server-nodejs
  - Express/Nodejs Starter with JWT authentication, and SQLite persistance - Provided by AppSeed App Generator. 
  - Authentication Flow uses json web tokens via Passport library - passport-jwt strategy.
  - 典型的dashboard的后端示例
# more
