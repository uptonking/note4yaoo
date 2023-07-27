---
title: toc-db-sqlite-web-indexeddb
tags: [indexeddb, sqlite, toc, web]
created: 2022-06-03T22:12:22.597Z
modified: 2022-11-06T03:19:28.284Z
---

# toc-db-sqlite-web-indexeddb

# popular

- https://github.com/karlb/litespread /202108/js/inactive
  - https://github.com/karlb/litespread/wiki
  - https://www.litespread.com/
  - Webapp that uses SQLite as a spreadsheet engine
  - Litespread is viewer and editor for SQLite and CSV files with basic spreadsheet functionality.
  - Litespread runs in your browser without the need for any server-side code
  - 依赖sql.js、blueprintjs、file-saver、moment、papaparse、react
  - Sync data via Remote Storage
  - Use SQL syntax in formulas

- https://github.com/uglyer/storelite.js
  - 基于sql.js(sqlite)实现的状态仓库，支持 web worker、react 绑定

- absurd-sql /3.6kStar/MIT/202110/js
  - https://github.com/jlongster/absurd-sql
  - sqlite3 in ur indexeddb (hopefully a better backend soon)
  - It implements a backend for sql.js (sqlite3 compiled for the web) that treats IndexedDB like a disk and stores data in blocks there. 
  - That means your sqlite3 database is persisted. 
  - And not in the terrible way of reading and writing the whole image at once -- it reads and writes your db in small chunks.
- https://github.com/nikochan2k/absurd-sql-ts /202209/ts
  - Typescript version of absurd-sql
- https://github.com/kikko-land/better-absurd-sql /202209/js
  - a fork of absurd-sql.
  - Right now you need to use my fork of sql.js, but I'm going to open a PR and hopefully get it merged. 
- https://github.com/monlovesmango/nostr-absurd-sql
  - nostr utility for sqlite3 saved to indexeddb

- https://github.com/randyl/sqlite3-wasm-demo-extension
  - [SQLite Wasm in the browser backed by the Origin Private File System - Chrome Developers](https://developer.chrome.com/blog/sqlite-wasm-in-the-browser-backed-by-the-origin-private-file-system/)

- sql.js /10.8kStar/MIT/202209/js
  - https://github.com/sql-js/sql.js
  - http://sql.js.org/
  - A javascript library to run SQLite on the web.
  - sql.js is a javascript SQL database. 
  - It allows you to create a relational database and query it entirely in the browser.
  - sql.js uses `emscripten` to compile SQLite to webassembly (or to javascript code for compatibility with older browsers). 
  - It uses a virtual database file stored in memory, and thus doesn't persist the changes made to the database. 
  - However, it allows you to import any existing sqlite file, and to export the created database as a JavaScript typed array.
  - https://github.com/wireapp/websql  /202005/ts/inactive
    - websql is a fork of sql.js 
    - Database is persisted to IndexedDB, and can be synced using the saveChanges API

- sql.js-httpvfs /3kStar/apache2/202209/ts
  - https://github.com/phiresky/sql.js-httpvfs
  - Hosting read-only SQLite databases on static file hosters like Github Pages
  - sql.js is a light wrapper around SQLite compiled with EMScripten for use in the browser (client-side).
  - This repo is a fork of and wrapper around sql.js to provide a read-only HTTP-Range-request based virtual file system for SQLite.
  - It allows hosting an SQLite database on a static file hoster and querying that database from the browser without fully downloading it.
  - sql.js-httpvfs also provides a proof-of-concept level implementation of a DOM virtual table that allows interacting (read/write) with the browser DOM directly from within SQLite queries.
  - [Hosting SQLite databases on Github Pages (or any static file hoster) - phiresky's blog_202104](https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/)
- https://github.com/uktrade/sqlite-s3vfs
  - Python virtual filesystem for SQLite to read from and write to S3.
  - No locking is performed, so client code must ensure that writes do not overlap with other writes or reads.

- https://github.com/ccorcos/tuple-database
  - The local-first, "end-user database" database.
  - All queries are reactive.

- https://github.com/tr1ckydev/great.db /202210/ts
  - human-friendly database library for JavaScript using SQLite. 
  - great.db automatically detects which runtime you are using and uses the respective fastest between better-sqlite3/bun-sqlite
# sqlite-web-examples
- https://github.com/mstrahov/hnsql /实现简单
  - https://mstrahov.github.io/hnsql/
  - a cross between sqlite in a browser (sql.js) and hackernews API.
  - create a reliable searcher for HN Who's hiring thread in SQLite db stored locally.

- https://github.com/lunu-bounir/sqlite-manager
  - a browser extension to read, manipulate, plot and write SQLite databases

- https://github.com/marmelab/ra-sqlite-dataprovider
  - here is a POC to generate a react-admin administration not relying on an API but directly on a SQLite database hosted on a static server (in this case the Github pages server).

- https://github.com/phartenfeller/sveltekit-sqlite-offline-app
  - Offline usable SvelteKit data app using Northwind. 
  - Uses SQLite3 WASM with the Origin-Private-File-System (OPFS).

- https://github.com/kaminskypavel/sqlite-wasm-browser
  - using SQL.js to run sqlite in browser.
  - chinook SQLite sample database: music tracks/playlists/invoices
# sqlite-indexeddb
- https://github.com/yanli0303/sql-js-worker-test
  - sql.js tests with IndexedDB as storage and Worker.

- https://github.com/littledivy/indexeddb-sqlite
  - Indexed DB Implementation
  - 单文件测试idea
# wasm
- https://github.com/overtone-app/sqlite-wasm-esm
  - The new SQLite WASM build is rather hard to use in modern JS apps, so this wrapper package tries to make this easier.
  - Currently only tested with Vite. 

- https://github.com/mizchi/sqlite-wasm-playground
  - sqlite-wasm playground
  - typescript, web worker, vite

- https://github.com/bgrins/opfs-sqlite-demo
  - /js

- https://github.com/rhashimoto/wa-sqlite /js
  - This is a WebAssembly build of SQLite with experimental support for writing SQLite virtual filesystems and virtual table modules completely in Javascript. 
  - This allows alternative browser storage options such as IndexedDB and File System Access.
  - [blobs should be uint8array not int8array?](https://github.com/rhashimoto/wa-sqlite/issues/65)

- https://github.com/mandel59/sqlite-wasm
  - SQLite compiled to WebAssembly

- https://github.com/tomayac/sqlite-wasm
  - SQLite Wasm conveniently wrapped as an ES Module.

- https://github.com/optuna/optuna-dashboard/tree/main/standalone_app
  - 依赖recoil、mui5、optuna超参数优化框架
# more-sqlite-web
