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
  - 最好支持切换存储层

- js-db-popular
  - lowdb, rxdb, pouchdb, nedb, loki, Watermelon, lovefield

- ref
  - [Offline-First Database Options for Web Applications in 2020](https://joshuatz.com/posts/2020/offline-first-database-options-for-web-applications-in-2020/)
# db-js
- pg-mem /1.1kStar/MIT/202211/ts
  - https://github.com/oguimbal/pg-mem
  - An in memory postgres DB instance for your unit tests
  - It works both in Node or in the browser.
  - https://github.com/oguimbal/pgsql-ast-parser
    - a Postgres SQL syntax parser. 基于nearley、moo实现
    - This parser does not support (yet) PL/pgSQL.

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

- acebase /279Star/MIT/202212/ts
  - https://github.com/appy-one/acebase
  - A fast, low memory, transactional, index & query enabled NoSQL database engine and server for node.js and browser with realtime data change notifications.
  - 👉🏻 Inspired by (and largely compatible with) the Firebase realtime database, with additional functionality and less data sharding/duplication.
  - By default, AceBase uses its own binary database format in Node.js environments, and IndexedDB (or LocalStorage) in the browser to store its data. 
    - However, it is also possible to use AceBase's realtime capabilities, and have the actual data stored in other databases. 
    - Currently, AceBase has built-in adapters for MSSQL, SQLite in Node.js environments; and IndexedDB, LocalStorage, SessionStorage for the browser. 
    - It also possible to create your own custom storage adapters, so wherever you'd want to store your data
  - When you're using AceBase with an IndexedDB or LocalStorage backend, you might notice that if you change data in one open tab, those changes do not raise change events in other open tabs monitoring that same data.
  - AceBase is designed to run in a Node.js environment, as it (by default) requires the `fs` filesystem to store its data and indexes. 
    - However, since v0.9.0 it is now also possible to use AceBase databases in the browser! 
  - When you're using AceBase with an IndexedDB or LocalStorage backend, you might notice that if you change data in one open tab, those changes do not raise change events in other open tabs
    - This is because IndexedDB or LocalStorage databases do not raise change events themselves
    - AceBase is now able to communicate with other tabs using the `BroadcastChannel` ,but disabled by default
  - [Protocol for other languages · appy-one/acebase](https://github.com/appy-one/acebase/discussions/79)
  - https://github.com/appy-one/acebase-core
    - rxjs dependency is optional and only needed when using methods that require them
  - https://github.com/appy-one/acebase-server
    - 依赖socket.io、express
  - https://github.com/appy-one/acebase-client
    - 依赖socket.io

- Nano-SQL /773Star/MIT/201911/ts/inactive/未实现同步
  - https://github.com/only-cliches/Nano-SQL
  - https://nanosql.io/
  - Universal database layer for the client, server & mobile devices. It's like Lego for databases.
  - 依赖snap-db(kv)
  - Graph, Join, Filter, Select and Order your data in dozens of ways.
  - NanoSQL supports a wide range of ways to save your data in the browser, on the phone, and on the server.
    - Memory (Browser/NodeJS/Electron) 
    - Snap DB (NodeJS/Electron; LSM Powered Javascript key-value store) 
    - Indexed DB (Browser) 
    - Local Storage (Browser)
  - [Offline use with Sync to Server](https://github.com/only-cliches/Nano-SQL/issues/18)
  - [Is this project still maintained?](https://github.com/only-cliches/Nano-SQL/issues/217)
    - I was about halfway through rewriting NanoSQL from the ground up. The plan was to add a query compilation step similar to SQLite
  - https://github.com/only-cliches/snap-db
    - Simple & Robust LSM Powered Javascript key-value store

- ydn-db /502Star/apache2/201902/js/功能丰富/仅支持浏览器
  - https://github.com/yathit/ydn-db
  - Unified data access layer on IndexedDB, WebDatabase and WebStorage storage mechanisms.
  - Library API should be similar to IndexedDB API and use exact terminology and concept in the IndexedDB specification.
  - Basic support for high level query using SQL-like `db.from('people').where('age', '>=', 25)`; 
  - Client-server Synchronization (via ydn-db-sync module 未开源).
  - https://github.com/yathit/ydn-db-fulltext
    - Full text search module for YDN-DB 
    - build on top of two excellent full text search libraries, [natural](https://github.com/NaturalNode/natural) for stemming, normalization, analyzer and fullproof for tokenization.

- yunodb /246Star/CC0/201704/js/leveldb/不支持浏览器环境
  - https://github.com/blahah/yunodb
  - A portable, persistent, electron-embeddable fulltext search + document store database for node.js
  - yuno is a JSON document store with fulltext search. 
  - The document store, which is just the raw JSON objects stored in leveldb/browser-level
  - The inverted search index, powered by search-index
  - yuno is being built to serve my use-case of embedding pre-made databases in electron apps
  - forks
    - https://github.com/pdepip/yunodb

- realm-js /5kStar/apache2/202211/ts/cpp
  - https://github.com/realm/realm-js
  - Realm is a mobile database that runs directly inside phones, tablets or wearables. 
  - This project hosts the JavaScript versions of Realm.
  - Currently we support React Native (JSC & Hermes on iOS & Android), Node.js and Electron (on Windows, MacOS and Linux).
  - This is still using Realm Core(cpp), but exposed via JavaScript API
  - https://github.com/realm/realm-core /202212/cpp
    - Core database component for the Realm Mobile Database SDKs

- blinkdb /59Star/MIT/202211/ts
  - https://github.com/blinkdb-js/blinkdb
  - https://blinkdb.io/
  - 依赖sorted-btree
  - An in-memory JS database optimized for large scale storage on the frontend.
  - Filter, sort, and implement pagination directly within BlinkDB.
  - It uses the same techniques & data structures as existing databases in order to speed up the retrieval of items, resulting in incredible performance

- rxdb /17.6kStar/Apache2/202206/ts
  - https://github.com/pubkey/rxdb
  - https://rxdb.info/
  - 依赖rxjs7
  - A fast, offline-first, reactive database for JavaScript Applications
  - 未实现Full Text Search，但第三方支持
  - a NoSQL-database for JavaScript Applications like Websites, hybrid Apps, Electron-Apps and NodeJs. 
  - 👉🏻 RxDB is not a self contained database. 
    - It is a wrapper around another database that implements the `RxStorage` interface. 
    - At the moment you can either use `PouchDB` or `Dexie.js` or `LokiJS` as underlaying storage. 
    - Each of them respectively has it's own adapters that can be swapped out, depending on your needs. 
    - For example you can use and IndexedDB based storage in the browser, and an SQLite storage in your hybrid app
  - [Add RxDB CRDT Plugin_202210](https://github.com/pubkey/rxdb/pull/4087)
  - [crdt plugin](https://github.com/pubkey/rxdb/blob/master/docs-src/crdt.md)
    - with crdt, all document writes are represented as CRDT operations in plain JSON. 
    - The CRDT **operations are stored together with the document** and each time a conflict arises, the CRDT conflict handler will automatically merge the operations in a deterministic way.
  - [backlog should be implemented in the future](https://github.com/pubkey/rxdb/blob/master/orga/BACKLOG.md)

- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
    - One datastore is the equivalent of a MongoDB collection
  - A copy of the whole database is kept in memory. This is not much on the expected kind of datasets (20MB for 10, 000 2KB documents).
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 

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
  - https://github.com/agershun/alamdx
    - MDX OLAP JavaScript library for Alasql database
- https://github.com/gratico/satya /starter/inactive
  - WIP: Satya is a distributed database using Apache Arrow as a Storage format and aims to support both OTLP(transaction processing) and OLAP(analytical processing) workloads. 
  - 依赖 duckdb-wasm、apache-arrow

- WatermelonDB /8.7kStar/MIT/202211/js
  - https://github.com/Nozbe/WatermelonDB
  - https://nozbe.github.io/WatermelonDB/
  - Reactive & asynchronous database for powerful React and React Native apps
  - Relational. Built on rock-solid SQLite foundation
  - Framework-agnostic. Use JS API to plug into other UI frameworks
  - Reactive. (Optional) RxJS API
  - Lazy: Nothing is loaded until it's requested. 
    - And since all querying is performed directly on the rock-solid SQLite database on a separate native thread, most queries resolve in an instant.
    - But unlike using SQLite directly, Watermelon is fully observable.
  - [Adapters - WatermelonDB documentation](https://nozbe.github.io/WatermelonDB/Implementation/Adapters.html)
    - The idea for the Watermelon architecture is to be database-agnostic.
    - Collection/Model/Query is the reactive layer
    - DatabaseAdapter is the imperative layer
    - SQLiteAdapter is an adapter for React Native, based on SQLite
    - LokiJSAdapter is an adapter for the web, based around LokiJS
  - [Sync - WatermelonDB documentation](https://nozbe.github.io/WatermelonDB/Advanced/Sync.html)
    - Note that Watermelon is only a local database — you need to bring your own backend.
    - You can build your own custom sync engine using synchronization primitives
    - You can use the sync engine(built-in sync adapter) Watermelon provides out of the box, and you only need to provide two API endpoints on your backend that conform to Watermelon sync protocol
    - `synchronize(dbName, pullChanges, pushChanges)` 在客户端调用
    - "Turbo Login" syncing can only be used for the initial (login) sync, not for incremental syncs.
    - WatermelonDB has been designed with the assumption that there is no difference between Local IDs (IDs of records and their relations in a WatermelonDB database) and Remote IDs (IDs on the backend server). 
    - So a local app can create new records, generating their IDs, and the backend server will use this ID as the true ID.
    - sync could only send changed fields and server could automatically always just apply those changed fields to the server version (since that's what per-column client-wins resolver will do anyway)
  - [Sync implementation - WatermelonDB documentation](https://nozbe.github.io/WatermelonDB/Implementation/SyncImpl.html)
    - master/replica - server is the source of truth, client has a full copy and syncs back to server (no peer-to-peer syncs)
    - two phase sync: first pull remote changes to local app, then push local changes to server
    - client resolves conflicts
    - content-based, not time-based conflict resolution
    - eventual consistency (client and server are consistent at the moment of successful pull if no local changes need to be pushed)
    - conflicts are resolved using per-column client-wins strategy: in conflict, server version is taken except for any column that was changed locally since last sync.
    - sync is performed for the entire database at once, not per-collection
    - non-blocking: local database writes (but not reads) are only momentarily locked when writing data but user can safely make new changes throughout the process

- LokiJS /6.3kStar/MIT/202203/js/inactive
  - https://github.com/techfort/LokiJS
  - javascript embeddable/in-memory database
  - The super fast in-memory javascript document oriented database.
  - Its purpose is to store javascript objects as documents in a nosql fashion and retrieve them with a similar mechanism. 
  - Runs in node (including cordova/phonegap and node-webkit), nativescript and the browser.
- https://github.com/LokiJS-Forge/LokiDB /202008/ts/inactive
  - a document oriented feature-rich in-memory database written in TypeScript
  - LokiDB is the official successor of LokiJS.
  - 完全自己实现了 full-text-search
  - [How is LokiDB the official successor of LokiJS?](https://github.com/LokiJS-Forge/LokiDB/issues/190)
    - I tried my best converting it to TypeScript and improving it.
    - But I don't really use LokiDB (web technology in general) very much. 

- lovefield /6.8kStar/Apache2/202005/js/inactive
  - https://github.com/google/lovefield
  - Lovefield is a relational database for web apps. 
  - Written in JavaScript, works cross-browser. 
  - 👉🏻 Provides SQL-like APIs that are fast, safe, and easy to use.
  - 不支持原版SQL，支持`todoDb.select().from(item).where(item.done.eq(false)).exec();` 类SQL方法
  - [Lovefield wraps IndexedDB objects in different classes](https://github.com/google/lovefield/blob/master/docs/dd/02_data_store.md)
  - https://github.com/teambition/ReactiveDB /201707/ts
    - Reactive ORM for Lovefield
    - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS
- https://github.com/arthurhsu/lovefield-ts
  - [ブラウザで動くSQLite alternativesとしてのLovefield - console.lealog(); ](https://lealog.hateblo.jp/entry/2023/03/03/092649)
  - Lovefield Typescript port and modernization.
  - All namespaces are flattened
  - no Static schema: it was designed for use with Closure compiler.
- https://github.com/ReactiveDB/core
  - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS。

- https://github.com/robtweed/glsdb /202209/js
  - Global Storage Database Abstraction for Node.js
  - glsdb is a Node.js/JavaScript abstraction of Global Storage Databases. 
  - With glsdb, a Global Storage Database is abstracted as JavaScript Objects that represent database nodes and provide properties and methods for accessing and navigating between database nodes.
  - glsdb relies on the mg-dbx interfaces which provide access to the following Global Storage databases
  - glsdb can also be used with the mg-dbx-bdb interface

- https://github.com/anywhichway/reasondb /201702/js/不支持同步
  - https://anywhichway.github.io/reasondb
  - JavaScript object database: SQL like syntax, full-text search, auto object sync, swapable persistence engines, asynchronous cursors, 30+ built-in plus in-line fat arrow predicates, predicate extensibility, joins, nested matching.
  - [Client to Server Synchronization](https://github.com/anywhichway/reasondb/issues/4)
    - resolved in v1.0.1b
  - [Is ReasonDB dead?](https://github.com/anywhichway/reasondb/issues/30)
    - ReasonDb is being merged into Thunderclap. but Thunderclap will not get any public updates until several months from now.
- https://github.com/anywhichway/thunderclap /201907/js
  - A key-value, indexed JSON, and graph database plus function oriented server designed for Cloudflare
  - It runs on top of the Cloudflare KV store.
  - [Is Thunderclap dead?](https://github.com/anywhichway/thunderclap/issues/3)
    - In a kind of Forest Gump moment, I simply stopped coding Dec 23rd of last year(2020).

- https://github.com/typicaljoe/taffydb /201509/js/单文件
  - TaffyDB is an open source JavaScript library that provides powerful in-memory database capabilities to both browser and server applications.
  - We created TaffyDB easily and efficiently manipulate these 'tables' with a uniform and familiar SQL-like interface.
  - SQL inspired features such as insert, update, unique, count, and more
- https://github.com/chjj/tiny /201406/js/单文件
  - tiny is an in-process document/object store for node.js.
  - inspired by nStore, however, its goal was to implement real querying which goes easy on the memory.
  - It supports mongo-style querying, or alternatively a "mapreduce-like" interface similar to CouchDB's views.

- https://github.com/knadh/localStorageDB /202011/js
  - a simple layer over localStorage (and sessionStorage) that provides a set of functions to store structured data like databases and tables. 
  - It provides basic insert/update/delete/query capabilities. 
  - localStorageDB has no dependencies, and is not based on WebSQL. 
  - Underneath it all, the structured data is stored as serialized JSON in localStorage or sessionStorage.
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
  - used-by
    - json-server

- https://github.com/sius/fakerdb /202005/js
  - Generate an unlimited stream of JSON schema instances using json-schema-faker, faker, chance and insert the data into a supported database, e.g.: nedb, mongodb, postgres, mssql.

- https://github.com/hexojs/warehouse /188Star/MIT/202211/ts
  - https://hexojs.github.io/warehouse/
  - A JSON database with Models, Schemas, and a flexible querying interface. 
  - It powers the wildly successful static site generator Hexo.

- https://github.com/crisdosyago/sirdb /202203/js
  - A simple database on the file system.
  - JSON files organised into subdirectories for each table.
  - text-based. Everything is a JSON file, including the database meta information.
  - git-diffable, and therefore versionable
  - Index on any property (for nested objects, only index top-level properties)
  - https://github.com/crisdosyago/servedata
    - A simple server based on SirDB with a schema-driven API, for serving all types of data, while attempting to meet ROCA guidelines.

- https://github.com/fwd/database /202210/js
  - SQL-like JSON Database

- https://github.com/Belphemur/node-json-db
  - A simple "database" that use JSON file for NodeJS
  - Every method are now asynchronous

- https://github.com/syamdanda/jsonbase
  - A database software completely built as JSON files in backend
# db-distributed-collab
- orbit-db /7.4kStar/MIT/202301/js
  - https://github.com/orbitdb/orbit-db
  - OrbitDB is a serverless, distributed, peer-to-peer database. 
  - OrbitDB uses IPFS as its data storage and IPFS Pubsub to automatically sync databases with peers. 
  - It's an eventually consistent database that uses CRDTs for conflict-free database merges making OrbitDB an excellent choice for decentralized apps (dApps), blockchain applications and local-first web applications.
  - https://news.ycombinator.com/item?id=22918714
    - OrbitDB's core is an append-only, immutable log CRDT.The log in OrbitDB is a Merkle-DAG, so, a graph.
    - Key-Value databases, feeds, and other data model types that OrbitDB supports by default, are all built on that log. You can also create your custom database types, ie. custom data models.
- https://github.com/dao-xyz/peerbit
  - P2P database framework with encryption, sharding and search
  - originally as a fork of OrbitDB
  - Permissioned content based sharding
- https://github.com/dappkit/aviondb
  - A Distributed, MongoDB-like Database
  - AvionDB uses OrbitDB stores to model MongoDB-like Databases.

- https://github.com/mafintosh/hyperdb /201808/js
  - Distributed scalable database.

- https://github.com/Telios-org/nebula
  - Real-time distributed storage for files and key value databases built on top of Hypercore Protocol

- https://github.com/holepunchto/hypercore
  - Hypercore is a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data
# db-triple-store
- https://github.com/Symatem/SymatemJS /202010/js/inactive
  - A graph database which combines triple-store, key-value-store and distributed version control

- https://github.com/crubier/Hexastore /201506/js/inactive
  - http://crubier.github.io/Hexastore/
  - A fast, pure javascript triple store implementation, also useful as a graph database.
  - Hexastore is based on this research paper. 
    - It is a way to structure RDF data such that queries are really fast. 
    - However, as implemented here, it has a 6 fold increase in memory usage as compared to a naive implementation of a triple store.
  - Go check the factis package and factis.io instead !

- https://github.com/Factisio/factis /201506/js
  - The Factis modular database system in one package !
# db-js-utils
- https://github.com/pubkey/event-reduce /202212/ts
  - https://pubkey.github.io/event-reduce/
  - An algorithm to optimize database queries that run multiple times
  - 提供了使用示例，包括minimongo、nedb、pouchdb
  - EventReduce only works with queries that have a predictable sort-order for any given documents. (you can make any query predicable by adding the primary key as last sort parameter)
# more-db-js
- https://github.com/ciochetta/learndb /24Star/202101/js/mongodb
  - my first attempt at creating my own database from scratch.
  - I will not be doing a SQL database, instead, I will follow his steps but try to create a document database, like MongoDB

- https://github.com/codemix/ts-sql
  - a SQL database implemented purely in TypeScript type annotations.

- https://github.com/mafintosh/hyperdb /201808/js
  - Distributed scalable database

- https://github.com/leoafarias/neardb /ts/inactive
  - Simple document db made for infinitely scalable globally distributed reads.
