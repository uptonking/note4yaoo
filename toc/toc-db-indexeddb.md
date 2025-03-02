---
title: toc-db-indexeddb
tags: [indexeddb, toc]
created: 2022-06-03T22:06:01.133Z
modified: 2022-06-03T22:06:16.249Z
---

# toc-db-indexeddb

# guide
- tips
  - big json store/update > json patch
  - react indexeddb， 编辑器数据频繁的更新可参考编辑器实时协作的更新
  - 持久化考虑支持web、web-worker、nodejs

- 更适合block-editor的数据结构是否是 mongodb ？

- 用indexeddb如何保存和更新层数很深的树型数据？
  - 可以将tree打平为索引号 1.1, 1.2.1
# popular
- lo-fi /7Star/MIT/202211/ts/依赖少
  - https://github.com/a-type/lo-fi
  - https://lo-fi.gfor.rest/docs/intro
  - An IndexedDB-powered database and data sync solution for lightweight, local-first web apps.
  - server依赖sqlite、jwt、ws
  - Undo and redo changes
  - it includes an optional server which unlocks the power of sync and realtime
  - One small, generic syncing server is all you need
  - the goal of lo-fi is to be simple and recognizable.
    - NO. Infinitely growing storage usage
    - NO. Having to deeply understand CRDTs
    - NO. Peer to peer networking
    - NO. WASM-compiled databases in your browser
  - https://github.com/a-type/aglio
    - The web app is designed to work local-first and local-only. 
    - React-based PWA.

- minimongo /1kStar/LGPLv3/202207/ts/多种web存储
  - https://github.com/mWater/minimongo
  - A client-side MongoDB implementation which supports basic queries, including some geospatial ones.
  - It is either IndexedDb backed (IndexedDb), Local storage backed (LocalStorageDb) or in memory only (MemoryDb).
  - sqlite plugin is also supported when available
  - Uses code from Meteor.js minimongo package, reworked to support more geospatial queries. It was forked in January 2014.

- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
    - One datastore is the equivalent of a MongoDB collection
  - A copy of the whole database is kept in memory.
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
  - For a Node.js/Node Webkit database it's the file system
  - For a browser-side database it's `localforage`, which uses the best backend available (IndexedDB then localStorage)

- ZangoDB /1kStar/MIT/201710/js/inactive
  - https://github.com/erikolson186/zangodb
  - https://erikolson186.github.io/zangodb/
  - a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.
  - The following aggregation pipeline stages are supported: $match, $project, $group, $unwind, $sort, $skip, and $limit.
  - an implementation of IndexedDB is required. 
    - For environments without a native implementation of IndexedDB, Fake IndexedDB can be used

- ydn-db /502Star/apache2/201902/js/功能丰富/仅支持浏览器
  - https://github.com/yathit/ydn-db
  - Unified data access layer on IndexedDB, WebDatabase and WebStorage storage mechanisms.
  - Library API should be similar to IndexedDB API and use exact terminology and concept in the IndexedDB specification.
  - Basic support for high level query using SQL-like `db.from('people').where('age', '>=', 25)`; 
  - Client-server Synchronization (via ydn-db-sync module).
  - https://github.com/yathit/ydn-db-fulltext
    - Full text search module for YDN-DB 
    - build on top of two excellent full text search libraries, [natural](https://github.com/NaturalNode/natural) for stemming, normalization, analyzer and fullproof for tokenization.

- localForage /23.8kStar/apache2/202108/js/inactive
  - https://github.com/localForage/localForage
  - https://localforage.github.io/localForage
  - localForage is a fast and simple storage library for JavaScript. 
  - localForage improves the offline experience of your web app by using asynchronous storage (IndexedDB or WebSQL) with a simple `localStorage`-like API.
  - localForage uses `localStorage` in browsers with no IndexedDB or WebSQL support.
  - You can store any type in localForage; localForage automatically does `JSON.parse()` and `JSON.stringify()` when getting/setting values.
  - localForage supports storing all native JS objects that can be serialized to JSON, as well as ArrayBuffers, Blobs, and TypedArrays
  - You can create multiple instances of localForage that point to different stores using `createInstance`.
- https://github.com/dannyconnell/localbase /202012/js/localforage/inactive
  - A Firebase-Style Database ... Offline!
  - Localbase is built on top of LocalForage.
  - Localbase gives you an offline database with the simplicity & power of Firebase, all stored in the user's browser (in an IndexedDB database).
  - You can create as many databases as you like.
  - Databases are organised into Collections and Documents (just like Firebase Cloud Firestore).
    - Databases contain Collections (e.g. users)
    - Collections contain Documents (e.g. { id: 1, name: 'Bill', age: 47 }
  - https://github.com/kkosmowski/react-notes-2
    - 依赖localbase操作indexeddb
- https://github.com/creately/rxdata /202106/ts/inactive
  - RxData is a schemaless reactive document database for web browsers. 
  - It is inspired by rxdb but uses localForage instead of pouchdb to store data.
  - 依赖rxjs.v6、mingo、localforage
  - https://github.com/creately/rxdata-persistence
- https://github.com/UltimatePro-Grammer/websystem /202205/js
  - a fully functioning operating system built in pure Javascript, HTML and CSS.
  - Files are Saved Locally Through IndexedDB/WebSQL (localForage)
# db-powered-by-indexeddb
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

- https://github.com/SourceCodeBot/crudodb /202112/ts/archived
  - CrudoDb allows you to write offline-first webapps without any backend implementation.
  - Offline-first IndexedDb wrapper written in TypeScript, which is able to sync with backend services by passing optional service implementation.

- kvs /125Star/MIT/202209/ts
  - https://github.com/azu/kvs
  - Key Value storage for Browser, Node.js, and In-Memory.
  - I want to get universal storage library that works on Browser and Node.js.
  - Previously, I've created localstorage-ponyfill for this purpose. 
    - However `Window.localStorage` does not work on Web Workers or Service Worker
  - @kvs/* packages provide async storage API using IndexedDB etc and resolve this issue.

- https://github.com/gruns/ImmortalDB /202008/js/inactive
  - the best way to store persistent key-value data in the browser. 
  - Data saved to ImmortalDB is redundantly stored in Cookies, IndexedDB, and LocalStorage, and relentlessly self heals if any data therein is deleted or corrupted.

- https://github.com/elmarti/camadb /202110/ts/inactive
  - CamaDB is a NoSQL embedded database written in pure TypeScript for Node, Electron and browser-based environments
  - I was struggling to find a solution for Electron-based projects that deal with larger datasets in the main thread.
    - I had issues getting SQLite to work with webpack due to its native build
    - SQLite doesn't (by default) return native JS data types (Dates in particular)
    - Other NoSQL embedded databases seem to be largely abandoned
    - Most other NoSQL embedded databases seem to be limited by V8's hard string length limits

- lovefield /6.8kStar/Apache2/202005/js
  - https://github.com/google/lovefield
  - Lovefield is a relational database written in pure JavaScript.
  - It provides SQL-like syntax and works cross-browser
  - [Lovefield wraps IndexedDB objects in different classes](https://github.com/google/lovefield/blob/master/docs/dd/02_data_store.md)

- https://github.com/microsoft/ObjectStoreProvider /202207/ts
  - A cross-browser/platform indexeddb-like client library
  - We developed ObjectStoreProvider after needing a simplified interface toobject storage/retrieval that worked not only across all browsers. We also have built a fully in-memory database provider that has no persistence but supports fully transactional semantics
  - This project has some notable differences to NoSqlProvider
    - It uses red-black tree based indices for better performance of the inMemory provider
- https://github.com/microsoft/NoSQLProvider /ts/inactive
  - A cross-browser/platform indexeddb-like client library
  - We developed NoSQLProvider after needing a simplified interface to NoSQL-style object storage/retrieval that worked not only across all browsers, but also for native app development (initially Cordova-based, later moving to React Native.) 
  - Across the browsers, this required unifying WebSQL and IndexedDB, with the nuances of all the different IndexedDB issues
  - We also have built a fully in-memory database provider that has no persistence but supports fully transactional semantics, for a fallback in situations where you don't want persistence 
  - https://github.com/Microsoft/reactxp/tree/master/samples/TodoList
  - https://github.com/microsoft/reactxp /inactive
    - ReactXP is a library for cross-platform app development using React and React Native.
# idb-query-sql
- [Support full text indexes](https://github.com/w3c/IndexedDB/issues/44)

- [IndexedDB Full Text Search (Proof of Concept)](https://gist.github.com/inexorabletash/a279f03ab5610817c0540c83857e4295)
- [IndexedDB+Dexie+Lunr MTG full-text search demo](https://gist.github.com/oppianmatt/e950d647875ed0ad7049287c3e0afc03)
- [indexedDB search by regex](https://gist.github.com/deissh/b4ec45197365fd607fe0367ca275c9ac)

- https://github.com/Treora/indexeddb-full-text-search-comparison
  - 依赖levi
  - https://github.com/raine/taim 
    - measure execution time of functions and promises

- https://github.com/superhuman/fts /201708/js
  - This is a very very minimal search engine (it only allows searching for single terms) designed to test the feasibility of using IndexedDB as a full text search engine.

- https://github.com/ndx-search/ndx /201901/ts
  - https://localvoid.github.io/ndx-demo/
  - ndx is a collection of javascript (TypeScript) libraries for lightweight full-text indexing and searching.
  - Trie based dynamic Inverted Index.
  - Demo application requires modern browser features: WebWorkers and IndexedDB. Comments are stored in the IndexedDB, and search engine is working in a WebWorker.

- JsStore /663Star/MIT/202211/ts
  - https://github.com/ujjwalguptaofficial/JsStore
  - http://jsstore.net/
  - A complete IndexedDB wrapper with SQL like syntax.
  - Executes In Web Worker
  - Sql Support - through an extension sqlweb
  - https://github.com/ujjwalguptaofficial/jsstore-examples
- https://github.com/ujjwalguptaofficial/idbstudio
  - a cli tool for indexeddb library jsstore. It helps users to execute , debug and learn jsstore query.
- https://github.com/ujjwalguptaofficial/idbstudio /202308/ts
  - idbstudio is a management tools for indexeddb library jsstore. It helps users to execute , debug and learn jsstore query.
- https://github.com/ujjwalguptaofficial/sqlweb
  - SqlWeb is an extension of JsStore which allows to use sql query for performing database operation in IndexedDB.
  - var connection = new JsStore. Instance('jsstore worker path'); 
  - connection.$sql.run("select * from Customers").then(function(result) { console.log(result); }); 

- https://github.com/codewithkyle/jsql
  - Asynchronously access and manage your IndexedDB databases using SQL queries.

- https://github.com/jjcapellan/SIXDB /202211/js
  - IndexedDB lacks a query language, is asynchronous and can be complex to manage.
  - SIXDB adds an abstraction layer over indexedDB that hides that complexity.

- https://github.com/webqit/objective-sql
  - The object-oriented, adaptive SQL for modern apps - query anything from the plain JSON object, to the client-side IndexedDB, to the server-side DB.

- https://github.com/ScarletsFiction/SFDatabase-js
  - SFDatabase-js is a database library that can help you build a SQL Query and execute it to the server from Nodejs or local browser with WebSQL. 
  - It will fallback to IndexedDB or LocalStorage for saving the database if running on browser.

- https://github.com/yanli0303/sql-js-worker-test
  - sql.js tests with IndexedDB as storage and Worker

- https://github.com/YeloPartyHat/LocalDatabase
  - A simple queryable embedded database designed for front-end that wraps IndexedDB.
  - A limitation of IndexedDB is that you can only perform 1 write operation at a time. Currently, IndexedDB also limits you to only having 1 instance open per browser!
    - This means that if you implement this you won't be able to run this database in multiple tabs due to limitations of IndexedDB.
# idb-orm
- https://github.com/ahricode/iorm /202211/ts
  - IORM 是 IndexedDB 工具包和对象关系映射器，提供了 IndexdbDB 的全部功能，具有灵活性。

- https://github.com/maxgaurav/indexeddb-orm /201910/ts
  - https://maxgaurav.github.io/indexeddb-orm
  - An indexedDB wrapper for accessing indexedDB as a promise base api implementation.

- https://github.com/arashi-dev/local-orm
  - a minified library to manage local storages (e.g. localStorage, sessionStorage, indexedDB etc.) just like a real database with more functionality

- https://github.com/leegeunhyeok/bxd
  - https://bxd.vercel.app/
  - Object relational mapping for IndexedDB

- https://github.com/BackdoorTech/Beast-ORM
  - ORM for accessing indexedDB as a promise base api implementation.
  - plan to support indexeddb and sqlite
# more-indexeddb
- https://github.com/falsandtru/clientchannel
  - Persist objects and sync them between tabs via IndexedDB or LocalStorage.

- https://github.com/piotr-cz/redux-persist-idb-storage
  - Storage adapter to use IndexedDB via idb v3 with `redux-persist` ripped from idb v3 

- https://github.com/EmanHerawy/web3Drive
  - This project combines a browser-based frontend with web API crypto, 3box identity, 3box storage, and ipfs storage to allow users to upload/share large files securely through end to end clientside based encryption

- https://gist.github.com/robnyman/1894032
  - IndexedDB storing and retrieving files
