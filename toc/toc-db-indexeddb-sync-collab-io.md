---
title: toc-db-indexeddb-sync-collab-io
tags: [collaboration, indexeddb]
created: 2022-06-04T00:39:34.320Z
modified: 2022-10-22T18:47:16.228Z
---

# toc-db-indexeddb-sync-collab-io
- 更适合block-editor的数据结构是否是 mongodb ？

- 同步难点
  - 将indexeddb的数据存储转换为mongodb-like结构
  - 如何同步 mongodb-like 的结构，是否用 crdt，还是 http
  - 是否需要中心化服务器
  - 不必过于纠结crdt的集成或三方库，关注于官方同步示例，如block-editor/y-indexeddb/dexie-sync
# export/import
- https://github.com/Polarisation/indexeddb-export-import /202210/js
  - Export/import an IndexedDB database to/from JSON. Can be used to backup and restore.
# sync
- remotestorage.js /2.2kStar/MIT/202211/ts
  - https://github.com/remotestorage/remotestorage.js
  - https://remotestoragejs.readthedocs.io/
  - a JavaScript library for storing user data locally in the browser, as well as connecting to remoteStorage servers and syncing data across devices and applications.
  - It is also capable of connecting and syncing data with a person's Dropbox or Google Drive account (optional).
  - The first prototype of rs.js was written in November 2010. The library is well-tested and actively maintained.
  - Although remoteStorage.js was initially written for being used in browsers, we do support using it in Node.js 
  - IndexedDB is not fast enough to access from a button click. Make sure to put an in-memory caching layer in the module, and return control to the app immediately
  - for `remoteStorage.local`, a choice is made between `RemoteStorage.IndexedDB`,  `RemoteStorage.LocalStorage` and `RemoteStorage.InMemoryCaching`, depending on what the environment (browser, node.js, Electron, WebView, or other) supports.
  - Data modules make your app and its data interoperable with other apps.
  - Conflicts are resolved by calling storeObject() or storeFile() on the device where the conflict surfaced. 

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

- synceddb-idb /7Star/ISC/202203/ts/idb
  - https://github.com/darrachequesne/synceddb
  - a fork of the awesome idb library, which adds the ability to sync an IndexedDB database with a remote REST API.
  - 后端api，fetchChanges, pushChanges
  - Every change is tracked in a store. 
    - The `SyncManager` then sync these changes with the remote REST API when the connection is available, making it easier to build offline-first applications.
    - The `LiveQuery` provides a way to run a query every time the underlying stores are updated
  - Entities without `keyPath` are not currently supported.
  - Only the last version of each entity is kept on the client side.
  - 🔀 conflict: The last write wins (though you can customize the behavior in the `onpusherror` handler).
  - Inspired from Dexie.js liveQuery.
  - https://github.com/darrachequesne/synceddb-todo-example /js/express-server

- https://github.com/azer/indexeddb /202005/ts/inactive
  - Well-tested wrapper around the IndexedDB API. It can sync locally and remotely.
  - You can use the `sync` method to keep multiple local indexeddb database instances easily.
  - You can sync your IndexedDB remotely. To accomplish this, you'll need to customize `Push` and `Pull` classes. 
  - Well-tested, low-level wrapper around the IndexedDB API. 

- https://github.com/madmoizo/backinfront  /1Star/ISC/202206/js
  - Backinfront is both the manager of your browser database and a router which handles requests locally. 
  - If you are building an offline first web app which needs sync capabilities, Backinfront is probably the tool your are looking for.
  - Backinfront is designed to work inside a Service Worker make sure to NOT use it in a window context
  - 依赖idb

- https://github.com/theShagod/indexeddb-mysql-sync-testing
  - Playing with service workers, indexeddb and background sync.
  - https://www.jawsdb.com/
    - Database as a service
# collab
- https://github.com/yjs/y-indexeddb
  - IndexedDB database adapter for Yjs
  - Use the IndexedDB database adapter to store your shared data persistently in the browser. 
  - The next time you join the session, your changes will still be there.
  - Minimizes the amount of data exchanged between server and client
  - Makes offline editing possible

- IDBSideSync /8Star/MIT/202104/ts
  - https://github.com/clintharris/IDBSideSync
  - https://idbsidesync-todo-demo.vercel.app/
  - IDBSideSync is an experimental JavaScript library that makes it possible to sync browser-based IndexedDB databases using CRDT concepts
  - 基于浏览器的同步方案可参考更成熟的remoteStorage
  - As your app makes CRUD calls to its IndexedDB database, IDBSideSync proxies/intercepts those calls and records the operations to a log (the "oplog").
  - IDBSideSync will upload the client's oplog entries (CRDT state mutation messages) to the remote data store using the registered plugins, and also download other client's oplog entries
  - A hybrid logical clock (i.e., time + counter) is maintained among the clients to help figure out which operations "win" if more than one exists for the same database store/record/property.

- https://github.com/hesselbom/crdtmap-indexeddb
  - https://github.com/hesselbom/crdtmap
  - Inspired by yjs and the CRDT-variant LWW-Element-Set, this is a simple key-value map that can sync between different clients by letting latest timestamp always win.
# more
- https://github.com/SyncProxy/sync-client /202012/js/inactive/服务端未开源
  - SyncProxy-client is a javascript client for SyncProxy that enables one-single line of code implementation of synchronization for javascript offline applications using embedded database (IndexedDB, SQLite, SQLJS, WebSQL, LokiJS...).
