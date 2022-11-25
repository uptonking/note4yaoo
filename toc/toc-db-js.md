---
title: toc-db-js
tags: [db, js, toc]
created: 2022-11-25T15:50:30.806Z
modified: 2022-11-25T15:50:48.226Z
---

# toc-db-js

# guide

- ref
  - [Offline-First Database Options for Web Applications in 2020](https://joshuatz.com/posts/2020/offline-first-database-options-for-web-applications-in-2020/)
# database-js
- supabase /41.1kStar/apache2/202211/ts
  - https://github.com/supabase/supabase
  - https://supabase.com/
  - an open source Firebase alternative.
  - Hosted Postgres Database
    - PostgREST is a web server that turns your PostgreSQL database directly into a RESTful API
  - Realtime subscriptions
    - Realtime is an Elixir server that allows you to listen to PostgreSQL inserts, updates, and deletes using websockets. 
  - Authentication and authorization
  - Auto-generated APIs
  - Dashboard

- pouchdb /15.4kStar/apache2/202211/js
  - https://github.com/pouchdb/pouchdb
  - https://pouchdb.com/
  - PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
  - It enables applications to store data locally while offline, then synchronize it with CouchDB and compatible servers when the application is back online

- rxdb /17.6kStar/Apache2/202206/ts
  - https://github.com/pubkey/rxdb
  - https://rxdb.info/
  - 依赖rxjs7
  - A fast, offline-first, reactive database for JavaScript Applications
  - a NoSQL-database for JavaScript Applications like Websites, hybrid Apps, Electron-Apps and NodeJs. 
  - 👉🏻 RxDB is not a self contained database. 
    - It is a wrapper around another database that implements the `RxStorage` interface. 
    - At the moment you can either use `PouchDB` or `Dexie.js` or `LokiJS` as underlaying storage. 
    - Each of them respectively has it's own adapters that can be swapped out, depending on your needs. 
    - For example you can use and IndexedDB based storage in the browser, and an SQLite storage in your hybrid app

- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
  - One datastore is the equivalent of a MongoDB collection
  - Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
  - I consider NeDB to be feature-complete, i.e. it does everything I think it should and nothing more. As a general rule I will not accept pull requests anymore
  - [Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)

- WatermelonDB /8.7kStar/MIT/202211/js
  - https://github.com/Nozbe/WatermelonDB
  - Reactive & asynchronous database for powerful React and React Native apps
  - Lazy: Nothing is loaded until it's requested. 
  - And since all querying is performed directly on the rock-solid SQLite database on a separate native thread, most queries resolve in an instant.
  - But unlike using SQLite directly, Watermelon is fully observable.

- https://github.com/sius/fakerdb
  - Generate an unlimited stream of JSON schema instances using json-schema-faker, faker, chance and insert the data into a supported database, e.g.: nedb, mongodb, postgres, mssql.

- lovefield /6.8kStar/Apache2/202005/js/inactive
  - https://github.com/google/lovefield
  - Lovefield is a relational database for web apps. 
  - Written in JavaScript, works cross-browser. 
  - Provides SQL-like APIs that are fast, safe, and easy to use.
  - https://github.com/teambition/ReactiveDB
    - Reactive ORM for Lovefield
    - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS

- LokiJS /6.3kStar/MIT/202203/js/inactive
  - https://github.com/techfort/LokiJS
  - javascript embeddable/in-memory database
  - The super fast in-memory javascript document oriented database.
  - Its purpose is to store javascript objects as documents in a nosql fashion and retrieve them with a similar mechanism. 
  - Runs in node (including cordova/phonegap and node-webkit), nativescript and the browser.

- alasql /6kStar/MIT/202211/js
  - https://github.com/AlaSQL/alasql
  - an open source SQL database for JavaScript with a strong focus on query speed and data source flexibility for both relational data and schemaless data. 
  - It works in the web browser, Node.js, and mobile apps.
  - Handles both traditional relational tables and nested JSON data (NoSQL). 
    - Export, store, and import data from localStorage, IndexedDB, or Excel.
  - This library is designed for:
    - Fast in-memory SQL data processing for BI and ERP applications on fat clients
    - Easy ETL and options for persistence by data import / manipulation / export of several formats
    - All major browsers, Node.js, and mobile applications
  - it's working towards a full database engine complying with most of the SQL-99 language, spiced up with additional syntax for NoSQL (schema-less) data and graph networks.
# db-json
- lowdb /18.7Star/MIT/202211/ts
  - https://github.com/typicode/lowdb
  - a small local JSON database powered by Lodash 
  - supports Node, Electron and the browser
  - adapters: JSONFile/Memory/LocalStorage/TextFile
  - If you have large JavaScript objects (~10-100MB) you may hit some performance issues. 
    - This is because whenever you call `db.write`, the whole `db.data` is serialized using `JSON.stringify` and written to storage.
    - If you plan to scale, it's highly recommended to use databases like PostgreSQL or MongoDB instead.
  - who is using
    - json-server

- https://github.com/fwd/database /202210/js
  - SQL-like JSON Database
# db-with-fallback-storage
- Nano-SQL /201911/ts/inactive
  - https://github.com/only-cliches/Nano-SQL
  - https://nanosql.io/
  - Universal database layer for the client, server & mobile devices. It's like Lego for databases.
  - Graph, Join, Filter, Select and Order your data in dozens of ways.
  - NanoSQL supports a wide range of ways to save your data in the browser, on the phone, and on the server.
    - Memory (Browser/NodeJS/Electron) 
    - Snap DB (NodeJS/Electron; LSM Powered Javascript key-value store) 
    - Indexed DB (Browser) 
    - Local Storage (Browser)
  - [Offline use with Sync to Server](https://github.com/only-cliches/Nano-SQL/issues/18)
  - [Is this project still maintained?](https://github.com/only-cliches/Nano-SQL/issues/217)
    - https://github.com/only-cliches/snap-db  /inactive

- localForage /20.5kStar/Apache2/202110/js/inactive
  - https://github.com/localForage/localForage
  - https://localforage.github.io/localForage
  - localForage is a fast and simple storage library for JavaScript. 
  - localForage improves the offline experience of your web app by using asynchronous storage (IndexedDB or WebSQL) with a simple, localStorage-like API.
  - localForage uses localStorage in browsers with no IndexedDB or WebSQL support.
# more-db-js
- https://github.com/typicaljoe/taffydb /201509/js/单文件
  - TaffyDB is an open source JavaScript library that provides powerful in-memory database capabilities to both browser and server applications.
  - We created TaffyDB easily and efficiently manipulate these 'tables' with a uniform and familiar SQL-like interface.

- https://github.com/codemix/ts-sql
  - a SQL database implemented purely in TypeScript type annotations.
