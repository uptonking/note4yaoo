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
# sync
- https://github.com/Polarisation/indexeddb-export-import
  - Export/import an IndexedDB database to/from JSON. Can be used to backup and restore.

- nedb /13.1kStar/MIT/201602/js/deprecated
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
  - One datastore is the equivalent of a MongoDB collection
  - Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
  - [Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)
  - forks
    - https://github.com/seald/nedb
    - https://github.com/HalleyAssist/nedb
    - https://github.com/bajankristof/nedb-promises
- https://github.com/tedb-org/teDB /ts
  - A structure sane embedded database with pluggable storage and clean concise documentation.
  - TeDB uses an AVL balanced binary tree binary-type-tree to save indexed fields of documents.
  - a storage driver that can either work to persists data to disk or save data to memory. 
- https://github.com/typicode/lowdb /ts
  - a small local JSON database powered by Lodash 
  - supports Node, Electron and the browser

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
- https://github.com/SyncProxy/sync-client
  - SyncProxy javascript client with support for all major embedded databases (IndexedDB, SQLite, WebSQL, LokiJS...)
