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
- https://github.com/Polarisation/indexeddb-export-import
  - Export/import an IndexedDB database to/from JSON. Can be used to backup and restore.
# sync
- remotestorage.js /2.2kStar/MIT/202211/ts
  - https://github.com/remotestorage/remotestorage.js
  - https://remotestoragejs.readthedocs.io/
  - a JavaScript library for storing user data locally in the browser, as well as connecting to remoteStorage servers and syncing data across devices and applications.
  - It is also capable of connecting and syncing data with a person's Dropbox or Google Drive account (optional).
  - The first prototype of rs.js was written in November 2010. The library is well-tested and actively maintained.
  - rs.js optionally supports Dropbox and Google Drive as storage backends which users can connect.
  - Data modules make your app and its data interoperable with other apps. 

- https://github.com/madmoizo/backinfront  /1Star/ISC/202206/js
  - Backinfront is both the manager of your browser database and a router which handles requests locally. 
  - If you are building an offline first web app which needs sync capabilities, Backinfront is probably the tool your are looking for.
  - Backinfront is designed to work inside a Service Worker make sure to NOT use it in a window context
  - 依赖idb

- https://github.com/azer/indexeddb /202005/ts/inactive
  - Well-tested, low-level wrapper around the IndexedDB API. It can sync locally and remotely.

- https://github.com/logux/core
  - https://logux.io/
  - Logux is a new way to connect client and server. Instead of sending HTTP requests (e.g., AJAX and GraphQL) it synchronizes log of operations between client, server, and other clients.
  - when multiple users work with the same document. Logux has features inspired by CRDT to resolve edit conflicts between users. 
  - Time travel to keep actions order the same on every client. A distributed timer to detect the latest changes.
  - offline first: Logux saves Redux actions to IndexedDB and has a lot of features to merge changes from different users.
  - Logux combines WebSocket with modern reactive client architecture. It synchronizes Redux actions between clients and servers, and keeps the same order of actions.
  - Optimistic UI to improve UI performance by updating UI without waiting for an answer from the server. Time travel will revert changes later if the server refuses them.
  - Compatible with modern stack: Redux, Vuex and pure JS API, works with any back-end language and any database.
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
  - As your app makes CRUD calls to its IndexedDB database, IDBSideSync proxies/intercepts those calls and records the operations to a log (the "oplog").
  - IDBSideSync will upload the client's oplog entries (CRDT state mutation messages) to the remote data store using the registered plugins, and also download other client's oplog entries
  - A hybrid logical clock (i.e., time + counter) is maintained among the clients to help figure out which operations "win" if more than one exists for the same database store/record/property.

- https://github.com/hesselbom/crdtmap-indexeddb
  - https://github.com/hesselbom/crdtmap
  - Inspired by yjs and the CRDT-variant LWW-Element-Set, this is a simple key-value map that can sync between different clients by letting latest timestamp always win.
  - Key is always a string but value could be anything as long as it's just primitive values.
# more
- https://github.com/SyncProxy/sync-client /202012/js/inactive
  - SyncProxy-client is a javascript client for SyncProxy that enables one-single line of code implementation of synchronization for javascript offline applications using embedded database (IndexedDB, SQLite, SQLJS, WebSQL, LokiJS...).
