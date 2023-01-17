---
title: toc-db-sync
tags: [db, synchronization, toc]
created: 2022-11-25T15:41:22.619Z
modified: 2022-11-25T15:41:47.534Z
---

# toc-db-sync

# guide
- sync-protocols
  - sync/collab/local-first
  - 最好支持切换存储层
  - database realtime
  - minimongo/meteor 的replication协议参考 [meteor: Distributed Data Protocol (DDP)](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)
  - [MongoDB Realm: Device Sync Protocol](https://www.mongodb.com/docs/atlas/app-services/sync/details/protocol/)
  - pouchdb的同步协议参考 [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)
  - [remoteStorage Protocol](https://remotestorage.io/protocol/): defines a simple key/value store for apps to save and retrieve data
  - [Watermelon sync protocol](https://nozbe.github.io/WatermelonDB/Advanced/Sync.html)
  - firebase-like: supabase
  - [rxdb alternatives](https://rxdb.info/alternatives.html)

- [RxDB replication protocol](https://rxdb.info/replication.html)
  - 支持websocket、graphql、couchdb、p2p
  - The RxDB replication protocol provides the ability to replicate the database state in realtime between the clients and the server.
  - The backend server does not have to be a RxDB instance; you can build a replication with any infrastructure. For example you can replicate with a custom GraphQL endpoint or a http server on top of a PostgreSQL database.
  - 👉🏻 RxDB resolves all conflicts on the client so it would call the conflict handler of the RxCollection and create a new document state D that can then be written to the master.
  - The default conflict handler will always drop the fork/client state and use the master/server state.
    - This ensures that clients that are offline for a very long time, do not accidentally overwrite other peoples changes when they go online again. 
    - You can specify a custom conflict handler by setting the property `conflictHandler` when calling addCollection().
  - It is not possible to do a multi-master replication, like with CouchDB. RxDB always assumes that the backend is the single source of truth.

- [Comparison of Offline Sync Protocols and Implementations](https://offlinefirst.org/sync/)
  - couchdb/realm/firebase
# db-sync
- synceddb-multi-backends /388Star/MIT/201803/js/indexeddb/支持多种后端存储
  - https://github.com/paldepind/synceddb
  - makes it easy to write offline-first applications with real-time syncing and server-side persistence.
  - SyncedDB is a lightweight layer on top of IndexedDB. 
    - It strips away all the boilerplate that the IndexedDB API requires
    - Uses promises for all async operations — even inside IndexedDB transactions
    - 未暴露cursor api
  - Server side SyncedDB stores a list of changes that clients can request/subscribe and post/publish to. 
    - Synchronizes data through WebSockets and sends only compact diffs down the wire
  - The SyncedDB client communicates with the backend through WebSockets to achieve synchronization in real time. 
    - the client provides elegant conflict handling and events for reacting to changes from the server.
  - Persistence options are provided based on the following currently supported databases:
    - In memory, MySQL, PostgreSQL, CouchDB

- sync_server-nedb /33Star/MIT/201807/js/nedb
  - https://github.com/nponiros/sync_server
  - A simple server which can be used to synchronize data from multiple devices
  - A small node server which uses NeDB to write data to the disk. 
    - The database used to store the data. Currently only NeDB is supported
  - The server can be used with a client for example `SyncClient` to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the `ISyncProtocol` and `Dexie.Syncable`. 
    - 👉🏻 It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
  - The server supports 4 different protocols: http, https, ws and wss
- sync_client-dexie /29Star/MIT/201804/js
  - https://github.com/nponiros/sync_client
  - This module can be used to write data to IndexedDB using `Dexie` and to synchronize the data in IndexedDB with a server.
  - `Dexie.Syncable` is used for the synchronization. This module contains an implementation of the `ISyncProtocol`. 
  - It was primarily written to work with `sync-server` but should work with other servers which offer the same API.

- turtleDB-indexeddb /443Star/MIT/201809/js/代码量少
  - https://github.com/turtle-DB/turtleDB
  - https://turtle-db.github.io/
  - turtleDB is a JavaScript framework and in-browser database for developers to build offline-first, collaborative web applications. 
  - It provides a developer-friendly API to access an in-browser database built on top of IndexedDB.
  - It comes with built in document versioning and automatic server synchronization when paired with our back-end package tortoiseDB
  - Document versioning and developer-controlled conflict resolution
  - Synchronization with tortoiseDB and a MongoDB back-end
  - `db.setConflictWinner(doc: object)` 处理冲突
    - Takes a document that has conflicting versions and deletes all the other versions, making the version passed in the default winner.
- https://github.com/turtle-DB/tortoiseDB /mongodb
  - Enables offline-first applications built with turtleDB to be fully collaborative with automated document versioning, history merging, and synchronization management.
    - Built using Express and Mongo DB Native NodeJS Driver.

- Nano-SQL /773Star/MIT/201911/ts/inactive/未实现同步
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

- debe /35Star/MIT/201907/ts/inactive
  - https://github.com/bkniffler/debe
  - 依赖automerge(delta)
  - offline-first Javascript datastore for browsers, node, electron and react-native with focus on performance and simplicity. 
  - Please note, Debe is currently not supporting relations, and probably never really will.
  - Includes support for concurrent multi-master/client database replication via plugin.
  - Rich querying using SQL-alike syntax
  - Automatic conflict resolution (CRDT)
  - Undo/Redo capabilities
  - PouchDB/RxDB are great and very mature solutions for replicating databases, but being forced to build your services on top of CouchDB can be unfitting for some users. 
  - Debe, and having the whole data flow in Javascript, offers some cool possibilities to control data access and filter & transform incoming/outgoing data according to user permissions. This works through middlewares.
  - https://github.com/bkniffler/workerdb /201901/ts
    - offline-first, syncable Database in WebWorker based on PouchDB/RxDB

- clientdb /506Star/apache2/202207/ts/同步未完成
  - https://github.com/clientdb/clientdb
  - ClientDB is an in-memory database for enabling real-time web apps.
  - The architecture of clientdb is inspired by the Linear app
  - 依赖flexsearch、knex、express、socket.io、lodash
  - [sync-engine work in progress](https://github.com/clientdb/clientdb/pull/10)
  - [differences and advantages compared to RxDB](https://github.com/clientdb/clientdb/issues/12)

- remotestorage.js /2.2kStar/MIT/202211/ts
  - https://github.com/remotestorage/remotestorage.js
  - https://remotestoragejs.readthedocs.io/
  - a JavaScript library for storing user data locally in the browser, as well as connecting to remoteStorage servers and syncing data across devices and applications.
  - It is also capable of connecting and syncing data with a person's Dropbox or Google Drive account (optional).
  - The first prototype of rs.js was written in November 2010. The library is well-tested and actively maintained.
  - for `remoteStorage.local`, a choice is made between `RemoteStorage.IndexedDB`,  `RemoteStorage.LocalStorage` and `RemoteStorage.InMemoryCaching`, depending on what the environment (browser, node.js, Electron, WebView, or other) supports.
  - Data modules make your app and its data interoperable with other apps.

- orbit /2.3kStar/MIT/202209/ts/概念特别多
  - https://github.com/orbitjs/orbit
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is primarily used as a flexible client-side ORM, it can also be used server-side in Node.js.
  - Interact with data from a variety of sources: a REST server, a WebSocket stream, an IndexedDB backup, an in-memory store, etc.
  - Work offline, work online, and seamlessly transition between both modes.
  - Track changes deterministically.
  - Support undo/redo
  - Data in a source can be updated by applying a transform, which consists of one or more operations. 
    - Transforms must be applied atomically—all operations succeed or fail together.
  - Every time a source is transformed, it emits a transform event
    - every change to the in-memory source will be sync'd with the backup IndexedDB source. 

- kinto /4.2kStar/apache2/202210/python
  - https://github.com/Kinto/kinto
  - http://docs.kinto-storage.org/
  - A generic JSON document store with sharing and synchronisation capabilities.
  - Backends: In-memory (development), PostgreSQL 9.5+ (production)
  - 比较了parse、firebase、couchdb、kuzzle、remoteStorage、Hoodie
    - [How does Kinto compare to other solutions?](https://docs.kinto-storage.org/en/stable/faq.html)
  - https://github.com/Kinto/kinto.js
    - An Offline-First JavaScript client for Kinto.

- dagdb /133Star/MIT/202010/js/leveldb/git
  - https://github.com/mikeal/dagdb
  - DagDB is a portable and syncable database for the Web.
  - It can run as a distributed database in Node.js, including using AWS services as a backend.
  - It also runs in the browser. 
    - In fact, there is no "client and server" in DagDB, everything is just a DagDB database replicating from another database. 
    - In this way, it's closer to git than a traditional database workflow.
  - The closest thing to DagDB replication you're familiar with is git. 
    - The way changes are merged from one branch to another and from one remote to another. 
    - We even have a system for keeping track of remote databases that feels a lot like git.
    - if you have two database instances locally you can easily merge one into the other without using the remote system.
# sync-utils
- https://github.com/siliconjungle/tick-network-server
  - An example of a server that sends messages at a regular interval.
  - 依赖express、ws、messagepack
  - https://github.com/siliconjungle/tick-network-client
    - A demo of a client that sends messages at a regular interval.

- https://github.com/NangoHQ/nango /202212/ts
  - https://www.nango.dev/
  - Nango continuously syncs data from any API endpoint (that returns JSON) to your database.
  - Nango has built-in support for OAuth through our sister project Pizzly

- https://github.com/leapfrogtechnology/sync-db
  - Command line utility to synchronize and version control relational database objects across databases.

- https://github.com/urish/firebase-server
  - Firebase Web Socket Protocol Server. Useful for emulating the Firebase server in tests.
  - As of May 2019 there are officially supported emulators for many Firebase services, removing the need for a third-party solution like firebase-server.

- https://github.com/forbesmyester/SyncIt /201409/js
  - SyncIt is a library to enable you to easily add synchronization to your (normal) live or offline (Cordova / Ionic / Phonegap / HTML5 / Other) web Apps. 
  - Tracking versions of data.
  - Knowing which data is on the server.
  - Keeping a list of data which still needs to be sent to the server.
  - Supplying the App with all data required to handle version conflicts when they occur.
# db-collab
- https://github.com/orbitdb/orbit-db /202208/js
  - OrbitDB is a serverless, distributed, peer-to-peer database. 
  - OrbitDB uses IPFS as its data storage and IPFS Pubsub to automatically sync databases with peers. 
  - It's an eventually consistent database that uses CRDTs for conflict-free database merges making OrbitDB an excellent choice for decentralized apps (dApps), blockchain applications and local-first web applications.
- https://github.com/dappkit/aviondb
  - A Distributed, MongoDB-like Database
  - AvionDB uses OrbitDB stores to model MongoDB-like Databases.
# more
- https://github.com/rethinkdb/rethinkdb /202211/cpp/python
  - The open-source database for the realtime web.
  - NoSQL database that stores schemaless JSON documents
- https://github.com/rethinkdb/horizon
  - Horizon is an open-source developer platform for building sophisticated realtime apps. 
  - Horizon is built on top of RethinkDB and consists of four components

- https://github.com/hypercore-protocol/hypercore /202211/js
  - a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data
  - [hypercore and Yjs : how to make them work together](https://github.com/hypercore-protocol/hypercore/issues/296)
    - the y-dat implementation does not actually use the core feature of the hypercore’s append only merkle tree signed log, due to the mutable nature of the Yjs CRDT implementation.

- https://github.com/libp2p/js-libp2p
  - The JavaScript Implementation of libp2p networking stack.

- https://github.com/SyncProxy/sync-client /202012/js/inactive/服务端未开源
  - SyncProxy-client is a javascript client for SyncProxy that enables one-single line of code implementation of synchronization for javascript offline applications using embedded database (IndexedDB, SQLite, SQLJS, WebSQL, LokiJS...).

- https://github.com/malerba118/react-use-database
  - This library is no longer maintained, please consider react-query and apollo-graphql as more robust solutions 
  - react-use-database gives you an opinionated interface, efficient data flow, and concise global state management. 
  - It forces you to think about your client-side data in the context of a queryable database. 
  - It gives you two global data stores: an entity store and a query store.
  - The entity store contains all of your model data. 
    - It’s just a big json blob that is the source of truth for any database entity that you have defined via Normalizr’s notion of schemas 

- https://github.com/digitallyinduced/thin-backend /202211/js/ts/inactive
  - a Blazing Fast, Universal Web App Backend for Making Realtime Single Page Apps
  - Thin Backend has a built-in GUI-based schema designer, helps to quickly build the DDL statements for your database schema
  - Thin Backend is built on top of the production-proven [IHP](https://github.com/digitallyinduced/ihp) architecture & libraries.
