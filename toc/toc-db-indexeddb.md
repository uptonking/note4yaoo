---
title: toc-db-indexeddb
tags: [indexeddb, toc]
created: '2022-06-03T22:06:01.133Z'
modified: '2022-06-03T22:06:16.249Z'
---

# toc-db-indexeddb

> https://github.com/search?o=desc&q=indexeddb+stars%3A%3E0&s=updated&type=Repositories

- 更适合block-editor的数据结构是否是 mongodb ？
# popular
- Dexie.js /8kStar/Apache2/202206/ts
  - https://github.com/dexie/Dexie.js
  - https://dexie.org/
  - https://dexie.org/docs/Tutorial/Hello-World
  - A Minimalistic Wrapper for IndexedDB
  - Dexie solves three main issues with the native IndexedDB API:
    - Poor queries
    - Code complexity
    - Ambiguous error handling
  - Reactive (Since v3.2)
    - Query the db without boilerplate and let your components mirror the database in real time.
- https://dexie.org/docs/Syncable/Dexie.Syncable.js
  - Enables two-way synchronization with a remote server of any kind.
  - https://github.com/nponiros/sync_server
    - A small node server which uses NeDB to write data to the disk. 
    - The server can be used with a client for example SyncClient to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the ISyncProtocol and Dexie.Syncable. 
    - It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
  - [Offline use with Sync to Server](https://github.com/only-cliches/Nano-SQL/issues/18)
    - Dexie.Syncable the Sync Server just uses Nedb as a quick way to get a sample running. You would replace that with MongoDB or whatever backend DB you wanted so you con isn't relevant here.
- https://github.com/subshell/data-repositories
  - This is a wrapper around Dexie, which itself is already a wrapper around IndexedDB. 
  - This wrapper allows to create repository classes, similar as you might be used to from Java and Spring Data.
  - It is recommended to have separate Dexie databases for every repository (due to some issues with Dexie and the versioning across multiple repositories). 
  - The repositories naturally work with RxJS and Observables. If you want to use JavaScript Promises instead you can just call .toPromise() on every returned Observable. 
  - **Due to the nature of IndexedDB, there is no synchronous way to read or write any data**.
- https://github.com/jaetask/dexie-easy-encrypt
  - Easy, unopinionated, table encryption middleware for Dexie
- more-dexie
  - https://github.com/stutrek/dexie-hooks
  - https://www.npmjs.com/package/@3fv/dexie-orm

- localForage /20.5kStar/Apache2/202110/js
  - https://github.com/localForage/localForage
  - https://localforage.github.io/localForage
  - localForage is a fast and simple storage library for JavaScript. 
  - localForage improves the offline experience of your web app by using asynchronous storage (IndexedDB or WebSQL) with a simple, localStorage-like API.
- https://github.com/dannyconnell/localbase
  - A Firebase-Style Database ... Offline!
  - Localbase is built on top of LocalForage.
  - Localbase gives you an offline database with the simplicity & power of Firebase, all stored in the user's browser (in an IndexedDB database).
  - You can create as many databases as you like.
  - Databases are organised into Collections and Documents (just like Firebase Cloud Firestore).
    - Databases contain Collections (e.g. users)
    - Collections contain Documents (e.g. { id: 1, name: 'Bill', age: 47 }
- https://github.com/creately/rxdata
  - RxData is a schemaless reactive document database for web browsers. 
  - It is inspired by rxdb but uses localForage instead of pouchdb to store data.

- minimongo /1kStar/LGPLv3/202205/ts
  - https://github.com/mWater/minimongo
  - Client-side in-memory mongodb backed by localstorage with server sync over http
  - Uses code from Meteor.js minimongo package, reworked to support more geospatial queries. It was forked in January 2014.
  - It is either IndexedDb backed (IndexedDb), WebSQL backed (WebSQLDb), Local storage backed (LocalStorageDb) or in memory only (MemoryDb).
  - sqlite plugin is also supported when available
- ZangoDB /1kStar/MIT/201710/js
  - https://github.com/erikolson186/zangodb
  - https://erikolson186.github.io/zangodb/
  - a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.

- acebase /158Star/MIT/202206/js
  - https://github.com/appy-one/acebase
  - A fast, low memory, transactional, index & query enabled NoSQL database engine and server for node.js and browser with realtime data change notifications
  - AceBase is designed to run in a Node.js environment, as it (by default) requires the 'fs' filesystem to store its data and indexes. 
    - However, since v0.9.0 it is now also possible to use AceBase databases in the browser! 
  - By default, AceBase uses its own binary database format in Node.js environments, and IndexedDB (or LocalStorage) in the browser to store its data. 
    - However, it is also possible to use AceBase's realtime capabilities, and have the actual data stored in other databases. 
    - Currently, AceBase has built-in adapters for MSSQL, SQLite in Node.js environments; and IndexedDB, LocalStorage, SessionStorage for the browser. 
  - When you're using AceBase with an IndexedDB or LocalStorage backend, you might notice that if you change data in one open tab, those changes do not raise change events in other open tabs monitoring that same data.

- https://github.com/AlaSQL/alasql
  - an open source SQL database for JavaScript with a strong focus on query speed and data source flexibility for both relational data and schemaless data. 
  - It works in the web browser, Node.js, and mobile apps.
  - Handles both traditional relational tables and nested JSON data (NoSQL). 
    - Export, store, and import data from localStorage, IndexedDB, or Excel.
  - This library is designed for:
    - Fast in-memory SQL data processing for BI and ERP applications on fat clients
    - Easy ETL and options for persistence by data import / manipulation / export of several formats
    - All major browsers, Node.js, and mobile applications

- rxdb /17.6kStar/Apache2/202206/ts
  - https://github.com/pubkey/rxdb
  - A realtime Database for JavaScript Applications
  - a NoSQL-database for JavaScript Applications like Websites, hybrid Apps, Electron-Apps and NodeJs. 
  - RxDB is not a self contained database. It is a wrapper around another database that implements the `RxStorage` interface. At the moment you can either use PouchDB or Dexie.js or LokiJS as underlaying storage. Each of them respectively has it's own adapters that can be swapped out, depending on your needs. For example you can use and IndexedDB based storage in the browser, and an SQLite storage in your hybrid app

- https://github.com/gruns/ImmortalDB
  - the best way to store persistent key-value data in the browser. 
  - Data saved to ImmortalDB is redundantly stored in Cookies, IndexedDB, and LocalStorage, and relentlessly self heals if any data therein is deleted or corrupted.

- https://github.com/akirarika/kurimudb
  - 一款渐进式的 Web 端本地存储库，可将数据保存到 LocalStorage、IndexedDB、Cookie 等地方，和订阅值的变更。
  - 除了持久化数据之外，若你愿意，Kurimudb 还能成为你应用的 Model 层 抽象，接任你应用中状态管理库的职责 (如 Vuex、Redux、Mobx)，使你应用真正拥有单一数据来源。

- https://github.com/piotr-cz/swr-idb-cache
  - IndexedDB Cache Provider for SWR
  - Synchronize SWR Cache with IndexedDB to get offline cache.
  - Library reads current state of cache stored in IndexedDB into memory using idb during initialization. Then it resolves into Cache Provider which should be passed to SWR.

- https://github.com/elmarti/camadb
  - CamaDB is a NoSQL embedded database written in pure TypeScript for Node, Electron and browser-based environments
  - I was struggling to find a solution for Electron-based projects that deal with larger datasets in the main thread.
    - I had issues getting SQLite to work with webpack due to its native build
    - SQLite doesn't (by default) return native JS data types (Dates in particular)
    - Other NoSQL embedded databases seem to be largely abandoned
    - Most other NoSQL embedded databases seem to be limited by V8's hard string length limits

- https://github.com/SourceCodeBot/crudodb
  - CrudoDb allows you to write offline-first webapps without any backend implementation.
  - Offline-first IndexedDb wrapper written in TypeScript, which is able to sync with backend services by passing optional service implementation.

- https://github.com/yanli0303/sql-js-worker-test
  - sql.js tests with IndexedDB as storage and Worker

- https://github.com/microsoft/ObjectStoreProvider
  - A cross-browser/platform indexeddb-like client library
  - We developed ObjectStoreProvider after needing a simplified interface toobject storage/retrieval that worked not only across all browsers. We also have built a fully in-memory database provider that has no persistence but supports fully transactional semantics
  - This project has some notable differences to NoSqlProvider
    - It uses red-black tree based indices for better performance of the inMemory provider
- https://github.com/microsoft/NoSQLProvider
  - A cross-browser/platform indexeddb-like client library
  - We developed NoSQLProvider after needing a simplified interface to NoSQL-style object storage/retrieval that worked not only across all browsers, but also for native app development (initially Cordova-based, later moving to React Native.) 
  - Across the browsers, this required unifying WebSQL and IndexedDB, with the nuances of all the different IndexedDB issues
  - We also have built a fully in-memory database provider that has no persistence but supports fully transactional semantics, for a fallback in situations where you don't want persistence 
  - https://github.com/Microsoft/reactxp/tree/master/samples/TodoList
  - https://github.com/microsoft/reactxp /inactive
    - ReactXP is a library for cross-platform app development using React and React Native.

- https://github.com/google/lovefield
  - Lovefield is a relational database written in pure JavaScript. It provides SQL-like syntax and works cross-browser
  - [Lovefield wraps IndexedDB objects in different classes](https://github.com/google/lovefield/blob/master/docs/dd/02_data_store.md)
# indexeddb-query-sql
- https://github.com/ujjwalguptaofficial/JsStore
  - A complete IndexedDB wrapper with SQL like syntax.
- https://github.com/ujjwalguptaofficial/sqlweb
  - SqlWeb is an extension of JsStore which allows to use sql query for performing database operation in IndexedDB.
  - var connection = new JsStore. Instance('jsstore worker path'); 
  - connection.$sql.run("select * from Customers").then(function(result) { console.log(result); }); 

- https://github.com/webqit/objective-sql
  - The object-oriented, adaptive SQL for modern apps - query anything from the plain JSON object, to the client-side IndexedDB, to the server-side DB.

- https://github.com/ScarletsFiction/SFDatabase-js
  - SFDatabase-js is a database library that can help you build a SQL Query and execute it to the server from Nodejs or local browser with WebSQL. 
  - It will fallback to IndexedDB or LocalStorage for saving the database if running on browser.
# indexeddb-orm
- https://github.com/maxgaurav/indexeddb-orm
  - https://maxgaurav.github.io/indexeddb-orm
  - An indexedDB wrapper for accessing indexedDB as a promise base api implementation.
- https://github.com/leegeunhyeok/bxd
  - https://bxd.vercel.app/
  - Object relational mapping for IndexedDB
- https://github.com/BackdoorTech/Beast-ORM
  - ORM for accessing indexedDB as a promise base api implementation.
  - plan to support indexeddb and sqlite
- https://github.com/arashi-dev/local-orm
  - a minified library to manage local storages (e.g. localStorage, sessionStorage, indexedDB etc.) just like a real database with more functionality
# more-indexeddb-repos
- https://github.com/falsandtru/clientchannel
  - Persist objects and sync them between tabs via IndexedDB or LocalStorage.
- https://github.com/pubkey/broadcast-channel
  - BroadcastChannel to send data between different browser-tabs or nodejs-processes satellite + LeaderElection over the channels

- https://github.com/piotr-cz/redux-persist-idb-storage
  - Storage adapter to use IndexedDB via idb v3 with redux-persist ripped from idb v3 

- https://github.com/EmanHerawy/web3Drive
  - This project combines a browser-based frontend with web API crypto, 3box identity, 3box storage, and ifps storage to allow users to upload/share large files securely through end to end clientside based encryption

- https://gist.github.com/robnyman/1894032
  - IndexedDB storing and retrieving files

- https://gist.github.com/inexorabletash/a279f03ab5610817c0540c83857e4295
  - IndexedDB Full Text Search (Proof of Concept)
