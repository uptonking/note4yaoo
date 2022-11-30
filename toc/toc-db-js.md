---
title: toc-db-js
tags: [db, js, toc]
created: 2022-11-25T15:50:30.806Z
modified: 2022-11-25T15:50:48.226Z
---

# toc-db-js

# guide

- db-latest
  - sync/collab/local-first

- ref
  - [Offline-First Database Options for Web Applications in 2020](https://joshuatz.com/posts/2020/offline-first-database-options-for-web-applications-in-2020/)
# db-js
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
  - PouchDB is not a self-contained database; 
    - it is a CouchDB-style abstraction layer over other databases. By default, 
    - PouchDB ships with the IndexedDB adapter for the browser, and a LevelDB adapter in Node.js.

- acebase /158Star/MIT/202206/js
  - https://github.com/appy-one/acebase
  - A fast, low memory, transactional, index & query enabled NoSQL database engine and server for node.js and browser with realtime data change notifications.
  - 👉🏻 Inspired by (and largely compatible with) the Firebase realtime database, with additional functionality and less data sharding/duplication.
  - By default, AceBase uses its own binary database format in Node.js environments, and IndexedDB (or LocalStorage) in the browser to store its data. 
    - However, it is also possible to use AceBase's realtime capabilities, and have the actual data stored in other databases. 
    - Currently, AceBase has built-in adapters for MSSQL, SQLite in Node.js environments; and IndexedDB, LocalStorage, SessionStorage for the browser. 
  - When you're using AceBase with an IndexedDB or LocalStorage backend, you might notice that if you change data in one open tab, those changes do not raise change events in other open tabs monitoring that same data.
  - AceBase is designed to run in a Node.js environment, as it (by default) requires the 'fs' filesystem to store its data and indexes. 
    - However, since v0.9.0 it is now also possible to use AceBase databases in the browser! 
  - https://github.com/appy-one/acebase-core
    - rxjs dependency is optional and only needed when using methods that require them
  - https://github.com/appy-one/acebase-server
    - 依赖socket.io、express
  - https://github.com/appy-one/acebase-client
    - 依赖socket.io

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

- realm-js /5kStar/apache2/202211/ts/cpp
  - https://github.com/realm/realm-js
  - Realm is a mobile database that runs directly inside phones, tablets or wearables. This project hosts the JavaScript versions of Realm.
  - Currently we support React Native (JSC & Hermes on iOS & Android), Node.js and Electron (on Windows, MacOS and Linux).
  - Mobile-first: Realm is the first database built from the ground up to run directly inside phones, tablets and wearables.

- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
    - One datastore is the equivalent of a MongoDB collection
  - A copy of the whole database is kept in memory. This is not much on the expected kind of datasets (20MB for 10, 000 2KB documents).
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 

- WatermelonDB /8.7kStar/MIT/202211/js
  - https://github.com/Nozbe/WatermelonDB
  - Reactive & asynchronous database for powerful React and React Native apps
  - And since all querying is performed directly on the rock-solid SQLite database on a separate native thread, most queries resolve in an instant.
  - Lazy: Nothing is loaded until it's requested. 
  - But unlike using SQLite directly, Watermelon is fully observable.

- lovefield /6.8kStar/Apache2/202005/js/inactive
  - https://github.com/google/lovefield
  - Lovefield is a relational database for web apps. 
  - Written in JavaScript, works cross-browser. 
  - 👉🏻 Provides SQL-like APIs that are fast, safe, and easy to use.
  - https://github.com/teambition/ReactiveDB
    - Reactive ORM for Lovefield
    - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS

- LokiJS /6.3kStar/MIT/202203/js/inactive
  - https://github.com/techfort/LokiJS
  - javascript embeddable/in-memory database
  - The super fast in-memory javascript document oriented database.
  - Its purpose is to store javascript objects as documents in a nosql fashion and retrieve them with a similar mechanism. 
  - Runs in node (including cordova/phonegap and node-webkit), nativescript and the browser.

- alasql /6kStar/MIT/202211/js/bi
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

- https://github.com/typicaljoe/taffydb /201509/js/单文件
  - TaffyDB is an open source JavaScript library that provides powerful in-memory database capabilities to both browser and server applications.
  - We created TaffyDB easily and efficiently manipulate these 'tables' with a uniform and familiar SQL-like interface.
  - SQL inspired features such as insert, update, unique, count, and more

- https://github.com/knadh/localStorageDB /202011/js
  - a simple layer over localStorage (and sessionStorage) that provides a set of functions to store structured data like databases and tables. 
  - It provides basic insert/update/delete/query capabilities. 
  - localStorageDB has no dependencies, and is not based on WebSQL. 
  - Underneath it all, the structured data is stored as serialized JSON in localStorage or sessionStorage.

- https://github.com/anywhichway/reasondb /201906/js/不支持同步
  - A multi model 100% JavaScript database supporting: key/values, graphs, documents
  - Industry standard Storage API (except ReasonDB is asynchronous), or a graph API similar to GunDB, or SQL like syntax.
# db-json
- lowdb /18.7Star/MIT/202211/ts
  - https://github.com/typicode/lowdb
  - Simple to use local JSON database.
  - supports Node, Electron and the browser
  - adapters: JSONFile/Memory/LocalStorage/TextFile
    - Change storage, file format (JSON, YAML,XML,remote-storage ...) or add encryption via adapters
    - An adapter is a simple class that just needs to expose two methods: read/write
  - Lowdb doesn't support Node's cluster module.
  - If you have large JavaScript objects (~10-100MB) you may hit some performance issues. 
    - This is because whenever you call `db.write`, the whole `db.data` is serialized using `JSON.stringify` and written to storage.
    - If you plan to scale, it's highly recommended to use databases like PostgreSQL or MongoDB instead.
  - who is using
    - json-server

- https://github.com/sius/fakerdb /202209/js
  - Generate an unlimited stream of JSON schema instances using json-schema-faker, faker, chance and insert the data into a supported database, e.g.: nedb, mongodb, postgres, mssql.

- https://github.com/fwd/database /202210/js
  - SQL-like JSON Database

- https://github.com/Belphemur/node-json-db
  - A simple "database" that use JSON file for NodeJS
  - Every method are now asynchronous

- https://github.com/syamdanda/jsonbase
  - A database software completely built as JSON files in backend
# db-with-fallback-storage
- Nano-SQL /201911/ts/inactive/未实现同步
  - https://github.com/only-cliches/Nano-SQL
  - https://nanosql.io/
  - 依赖snap-db(kv)
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
  - https://github.com/only-cliches/snap-db
    - Simple & Robust LSM Powered Javascript key-value store

- ydn-db /502Star/apache2/201902/js/inactive
  - https://github.com/yathit/ydn-db
  - Unified data access layer on IndexedDB, WebDatabase and WebStorage storage mechanisms.
  - Basic support for high level query using SQL.
  - Client-server Synchronization (via ydn-db-sync module).
  - https://github.com/yathit/ydn-db-fulltext
    - Full text search module for YDN-DB 
    - build on top of two excellent full text search libraries, [natural](https://github.com/NaturalNode/natural) for stemming, normalization, analyzer and fullproof for tokenization.

- localForage /20.5kStar/Apache2/202110/js/inactive
  - https://github.com/localForage/localForage
  - https://localforage.github.io/localForage
  - localForage is a fast and simple storage library for JavaScript. 
  - localForage improves the offline experience of your web app by using asynchronous storage (IndexedDB or WebSQL) with a simple, localStorage-like API.
  - localForage uses localStorage in browsers with no IndexedDB or WebSQL support.
# more-db-js
- https://github.com/ciochetta/learndb /202101/js/mongodb
  - my first attempt at creating my own database from scratch.
  - I will not be doing a SQL database, instead, I will follow his steps but try to create a document database, like MongoDB

- https://github.com/codemix/ts-sql
  - a SQL database implemented purely in TypeScript type annotations.
