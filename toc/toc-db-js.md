---
title: toc-db-js
tags: [db, js, toc]
created: 2022-11-25T15:50:30.806Z
modified: 2022-11-25T15:50:48.226Z
---

# toc-db-js

# guide

- db-features
  - sync/collab/local-first
  - storage-adapter: 支持切换存储层
  - db for excel/markdown

- js-db
  - popular: lowdb, rxdb, gundb, pouchdb, nedb, dexie, watermelon, loki, lovefield, tinybase, acebase
  - reactive: tinybase, dexie, rxdb, watermelon/rxjs, vlcn, fireproof
  - sync: pouchdb, rxdb, watermelon
  - demos: tinybase, pouchdb

- resources
  - [Offline-First Database Options for Web Applications in 2020](https://joshuatz.com/posts/2020/offline-first-database-options-for-web-applications-in-2020/)
# db-js
- pg-mem /1.6kStar/MIT/202310/ts
  - https://github.com/oguimbal/pg-mem
  - https://oguimbal.github.io/pg-mem-playground/
  - An in memory postgres DB instance for your unit tests
  - It works both in Node or in the browser.
  - 依赖immutable.v4、functional-red-black-tree、json-stable-stringify、lru-cache、moment、pgsql-ast-parser、@mikro-orm/core~pg
  - adapter支持pg-native, node-postgres, knex, typeorm
  - The sql syntax parser is home-made. Which means that some features are not implemented, and will be considered as invalid syntaxes.
  - limitations
    - Materialized views are implemented as views (meaning that they are always up-to-date, without needing them to refresh)
    - Indices implementations are basic
    - All number-like types are all handled as javascript numbers, meaning that types like `numeric(x,y)` could not behave as expected.
    - No support for timezones
  - https://github.com/oguimbal/pgsql-ast-parser
    - a Postgres SQL syntax parser. 基于nearley、moo实现
    - This parser does not support (yet) PL/pgSQL.

- pouchdb /15.4kStar/apache2/202211/js
  - https://github.com/pouchdb/pouchdb
  - https://pouchdb.com/
  - PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
  - It enables applications to store data locally while offline, then synchronize it with CouchDB and compatible servers when the application is back online
  - PouchDB is not a self-contained database; 
    - it is a CouchDB-style abstraction layer over other databases. By default, 
    - PouchDB ships with the IndexedDB adapter for the browser, and a LevelDB adapter in Node.js.

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

- WatermelonDB /9.6kStar/MIT/202310/js+flow
  - https://github.com/Nozbe/WatermelonDB
  - https://nozbe.github.io/WatermelonDB/
  - Reactive & asynchronous database for powerful React and React Native apps
  - 依赖sqlite、simdjson、lokijs、rxjs7
  - Relational. Built on rock-solid SQLite foundation
  - Framework-agnostic. Use JS API to plug into other UI frameworks
  - Reactive. (Optional) RxJS API
  - Lazy: Nothing is loaded until it's requested. 
    - And since all querying is performed directly on the rock-solid SQLite database on a separate native thread, most queries resolve in an instant.
    - But unlike using SQLite directly, Watermelon is fully observable.
  - [Disable 'rxjs' dependency_202204](https://github.com/Nozbe/WatermelonDB/issues/1301)
    - rxjs is used by WatermelonDB internals in some places, hence this is not possible to remove it
  - [[Question] More details on offline first?_202207](https://github.com/Nozbe/WatermelonDB/issues/1351)
  - [WatermelonDB, a database for React and React Native apps | Hacker News_201809](https://news.ycombinator.com/item?id=17950992)
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
    - 👉🏻 two phase sync: first pull remote changes to local app, then push local changes to server
    - client resolves conflicts
    - content-based, not time-based conflict resolution
    - eventual consistency (client and server are consistent at the moment of successful pull if no local changes need to be pushed)
    - conflicts are resolved using per-column client-wins strategy: in conflict, server version is taken except for any column that was changed locally since last sync.
    - sync is performed for the entire database at once, not per-collection
    - non-blocking: local database writes (but not reads) are only momentarily locked when writing data but user can safely make new changes throughout the process

- warehouse /188Star/MIT/202309/ts/hexo
  - https://github.com/hexojs/warehouse
  - https://hexojs.github.io/warehouse/
  - A JSON database with Models, Schemas, and a flexible querying interface.
  - It powers the wildly successful static site generator Hexo.
  - 依赖jsonparse、bluebird、graceful-fs
  - the major performance overhead of Hexo is not reading or writing db.json, but processing the cross-refs, e.g. finding posts with a tag or tags of a post.
  - [Why does hexo use this database implementation?](https://github.com/hexojs/warehouse/issues/13)
    - One idea I can think of is that you can index all the assets and get access to it for use synchronously
    - nedb doesn't have schemas

- acebase /279Star/MIT/202310/ts
  - https://github.com/appy-one/acebase
  - A fast, low memory, transactional, index & query enabled NoSQL database engine and server for node.js and browser with realtime data change notifications.
  - 👉🏻 Inspired by (and largely compatible with) the Firebase realtime database, with additional functionality and less data sharding/duplication.
  - By default, AceBase uses its own binary database format in Node.js environments, and IndexedDB (or LocalStorage) in the browser to store its data. 
    - However, it is also possible to use AceBase's realtime capabilities, and have the actual data stored in other databases. 
    - Currently, AceBase has built-in adapters for MSSQL, SQLite in Node.js environments; and IndexedDB, LocalStorage, SessionStorage for the browser. 
    - It also possible to create your own custom storage adapters, so wherever you'd want to store your data
  - When you're using AceBase with an IndexedDB or LocalStorage backend, you might notice that if you change data in one open tab, those changes do not raise change events in other open tabs monitoring that same data.
  - AceBase is designed to run in a Node.js environment, as it (by default) requires the `fs` filesystem to store its data and indexes. 
    - However, since v0.9.0 it is now also possible to use AceBase databases in the browser
  - When you're using AceBase with an IndexedDB or LocalStorage backend, you might notice that if you change data in one open tab, those changes do not raise change events in other open tabs
    - This is because IndexedDB or LocalStorage databases do not raise change events themselves
    - AceBase is now able to communicate with other tabs using the `BroadcastChannel` ,but disabled by default
  - [Protocol for other languages · appy-one/acebase](https://github.com/appy-one/acebase/discussions/79)
  - https://github.com/appy-one/acebase-core
    - Core functionality for AceBase, no need to install manually. See acebase-client and acebase-server
    - some source files have a browser-specific counterpart
    - rxjs is an optional dependency that only needs installing when any of AceBase's observe methods are used.
    -  If for some reason rxjs is not available (eg in test suite), we can provide a shim. 
  - https://github.com/appy-one/acebase-server
    - 依赖socket.io、express
  - https://github.com/appy-one/acebase-client
    - 依赖socket.io
- https://github.com/paradis-A/lendb-server /MIT/202202/ts/inactive
  - a wrapper around another database called Acebase that acts like a client. 
  - Think of Parse-server and Acebase have baby. Hello world!.
  - LenDB Server is a real-time database alternative to Firebase but instead of listening and receive the updated row/node, Stored objects in LenDB Server upon changes it auto propagates the changes on your live data. 
  - With LenDB Browser Client, LenDB is designed for reactive front-end frameworks like Svelte. etc.
  - https://github.com/paradis-A/lendb-client

- LokiJS /6.3kStar/MIT/202203/js/inactive
  - https://github.com/techfort/LokiJS
  - javascript embeddable/in-memory database
  - The super fast in-memory javascript document oriented database.
  - Its purpose is to store javascript objects as documents in a nosql fashion and retrieve them with a similar mechanism. 
  - Runs in node (including cordova/phonegap and node-webkit), nativescript and the browser.
  - [LokiJS – Lightweight JavaScript in-memory database | Hacker News_201411](https://news.ycombinator.com/item?id=8557386)
- https://github.com/LokiJS-Forge/LokiDB /202008/ts/inactive
  - a document oriented feature-rich in-memory database written in TypeScript
  - LokiDB is the official successor of LokiJS.
  - 完全自己实现了 full-text-search
  - [How is LokiDB the official successor of LokiJS?](https://github.com/LokiJS-Forge/LokiDB/issues/190)
    - I tried my best converting it to TypeScript and improving it.
    - But I don't really use LokiDB (web technology in general) very much

- lovefield /6.8kStar/Apache2/202005/js/inactive
  - https://github.com/google/lovefield
  - Lovefield is a relational database for web apps.
  - Written in JavaScript, works cross-browser. 
  - 👉🏻 Provides SQL-like APIs that are fast, safe, and easy to use.
  - 不支持原版SQL，支持`todoDb.select().from(item).where(item.done.eq(false)).exec();` 类SQL方法
  - Lovefield uses a plug-in architecture for data stores. All data stores implement `lf.BackStore` interface so that query engine can be decoupled from actual storage technology.
  - [Lovefield wraps IndexedDB objects in different classes](https://github.com/google/lovefield/blob/master/docs/dd/02_data_store.md)
  - [Is lovefield good for big data storage of 3GB or so?_201611](https://groups.google.com/g/lovefield-users/c/ky60q5DCrs4)
    - Unfortunately no. Lovefield currently has a (significant) limitation that all data is kept in an in-memory cache. 
    - You could instead only store metadata about your blobs/arraybuffers in Lovefield, and place the actual files in some other persistent storage. This approach has already been used by some Lovefield clients
- https://github.com/arthurhsu/lovefield-ts
  - [ブラウザで動くSQLite alternativesとしてのLovefield - console.lealog(); ](https://lealog.hateblo.jp/entry/2023/03/03/092649)
  - Lovefield Typescript port and modernization.
  - All namespaces are flattened
  - no Static schema: it was designed for use with Closure compiler.
- https://github.com/ReactiveDB/core /MIT/ts
  - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS。
  - https://github.com/teambition/ReactiveDB /201707/ts/inactive
    - Reactive ORM for Lovefield
    - 一个 Reactive 风格的前端 ORM。基于 Lovefield 与 RxJS

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
- snap-db /58Star/MIT/202001/ts/NoDeps/Nano-SQL
  - https://github.com/only-cliches/snap-db
  - Simple & Robust LSM Powered Javascript key-value store
  - SnapDB is a pure javascript persistent key-value store that provides ordered mapping from keys to string values. 
  - Data is persisted to disk using a Log Structure Merge Tree (LSM Tree) inspired by LevelDB/RocksDB. 
  - SnapDB has 100% API compatibility with LevelDB & RocksDB and also includes additional functionality.
  - Uses synchronous filesystem methods to exclusively perform append writes to disk, this puts the performance of SnapDB near the theoretical maximum write performance for ACID compliant javascript databases.

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
  - 🍴 forks
  - https://github.com/pdepip/yunodb

- realm-js /5kStar/apache2/202211/ts/cpp
  - https://github.com/realm/realm-js
  - https://www.mongodb.com/developer/products/realm/code-examples/
  - Realm is a mobile database that runs directly inside phones, tablets or wearables. 
  - This project hosts the JavaScript versions of Realm.
  - Currently we support React Native (JSC & Hermes on iOS & Android), Node.js and Electron (on Windows, MacOS and Linux).
  - This is still using Realm Core, but exposed via JavaScript API
  - It's the same C++ core used in the other Realm SDKs that is wrapped in JavaScript. The same API as what has been available in the ReactNative SDK for a while.
  - https://github.com/realm/realm-core /202212/cpp
    - Core database component for the Realm Mobile Database SDKs

- skdb /61Star/NonCommercial/202401/ts/skew/wasm
  - https://github.com/SkipLabs/skdb
  - https://www.skdb.io/
  - an embedded SQL database that stays in sync.
  - Built from the ground up and open source, it runs in the browser or the backend.
  - SKDB is a general-purpose SQL database that lets you subscribe to changes to your queries. 
  - Through a new construction called "virtual views", you can ask the database to keep a particular view up-to-date at all times
  - SKDB can also process ephemeral streams of data which can be used to receive alerts or to compute real-time analytics.
  - SKDB is inspired by SQLite and supports the same subset of SQL (including transactions). 
  - What sets it apart is that it is also highly concurrent. 
    - SKDB supports processing complex queries from multiple simultaneous readers/writers without stalling other database users.
  - https://github.com/SkipLabs/skdb_minimal
    - minimal example using skdb in a browser

- blinkdb /104Star/MIT/202401/ts
  - https://github.com/blinkdb-js/blinkdb
  - https://blinkdb.io/
  - 依赖sorted-btree
  - An in-memory JS database optimized for large scale storage on the frontend.
  - Filter, sort, and implement pagination directly within BlinkDB.
  - It uses the same techniques & data structures as existing databases in order to speed up the retrieval of items, resulting in incredible performance

- alasql /6kStar/MIT/202401/js/bi
  - https://github.com/AlaSQL/alasql
  - https://alasql.org/
  - https://github.com/AlaSQL/alasql/wiki/Examples /简单示例及工具
  - an open source SQL database for JavaScript with a strong focus on query speed and data source flexibility for both relational data and schemaless data. 
  - It works in the web browser, Node.js, and mobile apps.
  - Handles both traditional relational tables and nested JSON data (NoSQL). 
    - We focus on flexibility by making sure you can import/export and query directly on data stored in Excel (both .xls and .xlsx), CSV, JSON, TAB, IndexedDB, LocalStorage, and SQLite files.
  - This library is designed for:
    - Fast in-memory SQL data processing for BI and ERP applications on fat clients
    - Easy ETL and options for persistence by data import / manipulation / export of several formats
    - All major browsers, Node.js, and mobile applications
  - it's working towards a full database engine complying with most of the SQL-99 language, spiced up with additional syntax for NoSQL (schema-less) data and graph networks.
  - https://github.com/agershun/alamdx
    - MDX OLAP JavaScript library for Alasql database
  - https://github.com/dplocki/datamancer
    - https://datamancer.netlify.app/
    - Experiments with AlaSQL library - the project allows for loading data into memory, and manipulate them with SQL queries, all in the browser
- https://github.com/gratico/satya /starter/inactive
  - WIP: Satya is a distributed database using Apache Arrow as a Storage format and aims to support both OTLP(transaction processing) and OLAP(analytical processing) workloads. 
  - 依赖 duckdb-wasm、apache-arrow

- https://github.com/robtweed/glsdb /202401/js
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

- https://github.com/kappa-db/kappa-core /ISC/202011/js/inactive
  - Minimal peer-to-peer database, based on kappa architecture.
  - kappa-core is built on an abstraction called a kappa architecture, or "event sourcing". 
    - This differs from the traditional approach to databases, which is centered on storing the latest value for each key in the database.
    - In contrast, **kappa architecture centers on a primitive called the "append-only log"** as its single source of truth.
    - Each entry in a log is addressable by its "sequence number" (starting at 0, then 1, 2, 3, ...). In the case of kappa-core, which uses hypercore underneath
  - kappa-core still uses tables like the above, though. 
    - However, instead of being the source of truth, these **tables are generated (or materialized) from the log data**, providing a view of the log data in a new or optimized context. 
    - These are called materialized views.

- https://github.com/lideming/btrdb /MIT/202302/ts/inactive
  - a NoSQL database engine with B-tree Copy-on-Write mechanism inspired by btrfs.
  - https://github.com/lideming/btrdb/tree/main/btrdbfs
    - btrdbfs is a project to run filesystem on btrdb using FUSE.
    - btrdbfs implements FUSE filesystem using Node.js with the binding fuse-native.

- https://github.com/mikeal/CADB /202011/js/inactive
  - Experimental single file content addressed database.
  - "Content address" means that data is keyed by a hash digest.
  - CADB is a single file database for storing content addressed block data. 
  - You can think of it like a key/value store where the keys MUST be hash digests, of a sufficient length and security, and the value is arbitrary binary data.
  - CADB is a special B+ tree which is both sorted and balanced using hash digests. 
    - The keys (digests) are sorted by binary comparison 
    - and the tree's structure is chunked using randomness derived from the tail of each hash. 
    - This produces a self-balancing and well sorted structure on-disc.

- https://codeberg.org/small-tech/jsdb /202311/js/NoDeps
  - A zero-dependency, transparent, in-memory, streaming write-on-update JavaScript database for the Small Web that persists to a JavaScript transaction log.
  - A small and simple data layer for basic persistence and querying.
  - For Node.js: will not work in the browser
  - all data is kept in memory and, without tweaks, cannot exceed 1.4GB in size(nodejs limit)
  - Streaming writes on update: writes are streamed to disk to an append-only transaction log as JavaScript statements and are both quick (in the single-digit milliseconds region on a development laptop with an SSD drive) and as safe as we can make them (synchronous at the kernel level).
  - No schema, no migrations: again, this is meant to be a very simple persistence, query, and observation layer for local server-side data
  - JSDB tables are written into JavaScript Data Format (JSDF) files. 
    - A JSDF file is just es6 module 
    - When you load in a JSDB table, JSDB will, by default, compact the JSDF file.

- https://github.com/endpointservices/mps3 /ts
  - Infraless Database over any s3 storage API.
  - [mps3 - Offline-first DB over S3-compatible storage](https://observablehq.com/@tomlarkworthy/mps3-vendor-examples)
  - https://twitter.com/tomlarkworthy/status/1688132733246033920
    - I've been noodling with the concept of a vendorless BaaS by using an s3-compatible API as the backend. 
    - By hacking object versioning you get serialisability and atomic bulk updates. 
    - Its a real DB! Here it's using a local minio instance. Might try backblaze next.
    - Oh I have to expose the ETag header in the CORS config thats improved things to 400ms sometimes but I still have too many preflight requests
    - The sync protocol was designed using object versioning so that the logical names intuitively map to storage names, but then I realised R2, my favourite s3-like doesn't do versions. So now I had to redo it with timestamped suffixes. Total redesign with tricky clock skew defenses

- https://github.com/akirarika/creamdb /202406/ts
  - CreamDB 是一个轻量级的客户端 "数据库"，可以运行在任何能够运行 JavaScript 的地方。
  - 它是为包括 Electron、VS Code Extension、React Native、Capacitor、Taro、MiniProgram 等环境而设计的
  - 基于内存的，这意味着它很快，但同时也不适合海量的数据的用例
  - CreamDB 会在持续 256 毫秒都没有新的数据更改时，将数据从内存中持久化到硬盘中
  - CreamDB 假设你只有一个 "标签页"。当你同时打开多个"标签页"时，CreamDB 。这意味着，如果你使用 Electron 时，需要限制用户只能打开一个进程，且你的 CreamDB 位于主进程中
  - 如果你需要处理多"标签页"间数据同步的情况，这种情况下，RxDB 是一个更好的选择，CreamDB 创作的初衷，是因为 RxDB 使用起来较为繁琐，并且，目前 RxDB 不支持 React Native、Capacitor、Taro、MiniProgram 等环境。
# db-json
- https://github.com/datopian/markdowndb /MIT/202401/ts/sqlite
  - https://markdowndb.com/
  - JS library to turn markdown files into structured queryable database (SQL-based and simple JSON). 
  - It helps you build rich markdown-powered sites easily
  - Parses your markdown files to extract structured data (frontmatter, tags etc) and creates an index in a local `SQLite` database
  - Provides a lightweight javascript API for querying the database and importing files into your application

- https://github.com/sius/fakerdb /202005/js
  - Generate an unlimited stream of JSON schema instances using json-schema-faker, faker, chance and insert the data into a supported database, e.g.: nedb, mongodb, postgres, mssql.

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

- SirDB /493Star/AGPLv3/202012/js
  - https://github.com/c9fe/sirdb
  - A simple database on the file system.
  - JSON files organised into subdirectories for each table.
  - ServeData is a powerful yet simple server for SirDB 
    - with baked-in schemas, users, groups, permissions, authentication, authorization and payments.
  - text-based. 
    - Everything is a JSON file, including the database meta information.
  - is around 500 lines of code and 6.6Kb gzipped.

- https://github.com/Belphemur/node-json-db /MIT/202401/ts
  - A simple "database" that use JSON file for NodeJS
  - Every method are now asynchronous

- https://github.com/syamdanda/jsonbase /202205/js/inactive
  - A database software completely built as JSON files in backend
  - [Json-Base – Database built as JSON files | Hacker News_202007](https://news.ycombinator.com/item?id=23715558)
  - JSON file as backend, So can I directly edit the JSON file?
    - Bind does something like this (but not with JSON).
    - You have to run a “freeze” command before editing the database directly (so it can flush the current version of the database, and redirect writes to memory + log), and then “thaw” so it can read your changes and apply the log of updates to it.
# db-distributed
- orbit-db /7.4kStar/MIT/202301/js
  - https://github.com/orbitdb/orbitdb
  - OrbitDB is a serverless, distributed, peer-to-peer database. 
  - OrbitDB **uses IPFS as its data storage** and Libp2p Pubsub to automatically sync databases with peers.
  - It's an eventually consistent database that uses Merkle-CRDTs for conflict-free database writes and merges
  - OrbitDB provides various types of databases for different data models and use cases
  - All databases are implemented on top of `ipfs-log`, an immutable, cryptographically verifiable, operation-based CRDT
  - https://github.com/berty/go-orbit-db
    - Go version of P2P Database on IPFS
    - The majority of this code was vastly derived from the JavaScript's orbit-db project.
  - https://news.ycombinator.com/item?id=22918714
    - OrbitDB's core is an append-only, immutable log CRDT.The log in OrbitDB is a Merkle-DAG, so, a graph.
    - Key-Value databases, feeds, and other data model types that OrbitDB supports by default, are all built on that log. You can also create your custom database types, ie. custom data models.
- https://github.com/dao-xyz/peerbit /ts
  - P2P database framework with encryption, sharding and search
  - originally as a fork of OrbitDB
  - It’s built on top of Libp2p (and works with IPFS) supporting encryption, sharding and discoverability (searching).
  - Permissioned content based sharding
- https://github.com/dappkit/aviondb /MIT/202010/ts
  - A Distributed, MongoDB-like Database
  - AvionDB uses OrbitDB stores to model MongoDB-like Databases.
- https://github.com/cypsela/sailplane-web /js
  - https://cypsela.github.io/sailplane-web
  - Collaborative p2p file sharing in the browser

- orbit /2.3kStar/MIT/202209/ts
  - https://github.com/orbitjs/orbit
  - https://orbitjs.com/
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is **primarily used as a flexible client-side ORM**, it can also be used server-side in Node.js.
  - Interact with data from a variety of sources: a REST server, a WebSocket stream, an IndexedDB backup, an in-memory store, etc.
  - Work offline, work online, and seamlessly transition between both modes.
  - Support undo、redo
  - [How difficult is to create an offline-first app?](https://github.com/orbitjs/orbit/issues/790)
    - There is currently no CRDT implementation in orbit. There is no server implementation at all.

- https://github.com/genderev/assassin /202009/js/inactive
  - Assassin is a decentralized database that uses background threads to kill slow JavaScript.
  - I ended up creating this database partly because IndexedDB is disabled in private browsing, which means none of these databases work for me.
  - Assassin is a key/value store that supports mapping a key to its corresponding value.
  - System Architecture: The DAT protocol distributes and hosts data between many computers, so there is no one location where data is stored. Assassin relies on the the DAT protocol for data persistence. The metadata of the key-value pairs are stored in a distributed `trie` structure.
  - Storage Model: Assassin sends data to the server, which then stores the metadata in the distributed file system Hyperdrive, which is built on the DAT protocol
  - [Assassin - An open source, free database for killing slow webpages - DEV Community](https://dev.to/ender_minyard/assassin-an-open-source-free-database-for-killing-slow-webpages-3fip)

- https://github.com/mafintosh/hyperdb /201901/js/inactive/作者新作品hypercore
  - HyperDB is a scalable peer-to-peer key-value database.
  - A HyperDB is fundamentally a set of hypercores.
  - The combination of all operations performed on a HyperDB by all of its members forms a DAG (directed acyclic graph). 
  - HyperDB builds an incremental index with every new key/value pairs ("nodes") written
  - [Is this project maintained anymore?_202012](https://github.com/mafintosh/hyperdb/issues/171)
    - @hypercore-protocol is now the parent gh org and `mafintosh/hyperbee` is the best replacement for `hyperdb` atm
  - A HyperDB is fundamentally a set of hypercores
- https://github.com/beakerbrowser/webdb /201807/js
  - A database that reads and writes records on dat:// websites.

- https://github.com/Telios-org/nebula /202301/js/hypercore
  - Real-time distributed storage for files and key value databases built on top of Hypercore Protocol

- https://github.com/holepunchto/hypercore
  - a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data

- https://github.com/jepsen-io/maelstrom /clojure
  - a workbench for learning distributed systems by writing your own. 
  - It uses the Jepsen testing library to test toy implementations of distributed systems. 

## distributed-utils

- https://github.com/jepsen-io/jepsen /clojure
  - https://jepsen.io/
  - A framework for distributed systems verification, with fault injection
  - A test is a Clojure program which uses the Jepsen library to set up a distributed system, run a bunch of operations against that system, and verify that the history of those operations makes sense. 
  - Jepsen has been used to verify everything from eventually-consistent commutative databases to linearizable coordination systems to distributed task schedulers
# db-js-utils
- https://github.com/pubkey/event-reduce /MIT/202401/ts
  - https://pubkey.github.io/event-reduce/
  - An algorithm to optimize database queries that run multiple times
  - 提供了使用示例，包括minimongo、nedb、pouchdb
  - EventReduce only works with queries that have a predictable sort-order for any given documents. (you can make any query predicable by adding the primary key as last sort parameter)
  - [EventReduce: An algorithm to optimize database queries that run multiple times | Hacker News_202004](https://news.ycombinator.com/item?id=22888239)

- https://github.com/serby/save /143Star/ISC/202209/js
  - A simple CRUD based persistence abstraction for storing objects to any backend data store. eg. Memory, MongoDB, Redis, CouchDB, Postgres, Punch Card etc.
  - save comes with a fully featured in memory engine which is super handy for testing your models. 
  - https://github.com/serby/save-mongodb
  - https://github.com/serby/save-memory

- https://github.com/live-change/db /202112/js
  - Database with observable data for live queries
# rewrite-db
- https://github.com/plexidev/quick.db /MIT/202310/ts
  - https://quickdb.js.org/
  - http://docs.plexidev.org/
  - provide an easy way for beginners and people of all levels to access & store data in a low to medium volume environment.
  - All data is stored persistently via either better-sqlite3 or promise-mysql

- https://github.com/ciochetta/learndb /24Star/202101/js/mongodb
  - my first attempt at creating my own database from scratch.
  - I will not be doing a SQL database, instead, I will follow his steps but try to create a document database, like MongoDB
  - [LearnDB: Learn how to build a database | Hacker News_201811](https://news.ycombinator.com/item?id=18557260)

- https://github.com/weinberg/SQLToy /202112/js/sql-db/NoDeps
  - https://github.com/weinberg/SQLToy/wiki
  - SQLToy is an in-memory SQL database written in Javascript. 
  - It is under 500 lines of code and has zero dependencies.
  - [Show HN: SQLToy – a tiny relational database for learning SQL via code | Hacker News_202111](https://news.ycombinator.com/item?id=29385432)

- https://github.com/codemix/ts-sql /ts/inactive
  - a SQL database implemented purely in TypeScript type annotations.
  - [Show HN: A SQL database implemented purely in TypeScript type annotations | Hacker News_202009](https://news.ycombinator.com/item?id=24615185)
# more-db-js
- https://github.com/leoafarias/neardb /ts/inactive
  - Simple document db made for infinitely scalable globally distributed reads.
