---
title: toc-db-indexeddb-sync-collab-io
tags: [collab, indexeddb]
created: '2022-06-04T00:39:34.320Z'
modified: '2022-06-04T00:40:09.745Z'
---

# toc-db-indexeddb-sync-collab-io
- 更适合block-editor的数据结构是否是 mongodb ？

- 同步难点
  - 将indexeddb的数据存储转换为mongodb-like结构
  - 如何同步 mongodb-like 的结构，是否用 crdt，还是 http
  - 是否需要中心化服务器
  - 不必过于纠结crdt的集成或三方库，关注于官方同步示例，如block-editor/y-indexeddb/dexie-sync
# popular
- https://github.com/Polarisation/indexeddb-export-import
  - Export/import an IndexedDB database to/from JSON. Can be used to backup and restore.

- nedb /13.1kStar/MIT/2016/js/deprecated
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
  - One datastore is the equivalent of a MongoDB collection
  - Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
  - forks
    - https://github.com/seald/nedb
    - https://github.com/bajankristof/nedb-promises
    - https://github.com/typicode/lowdb

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

- https://github.com/hesselbom/crdtmap-indexeddb
  - https://github.com/hesselbom/crdtmap
  - Inspired by yjs and the CRDT-variant LWW-Element-Set, this is a simple key-value map that can sync between different clients by letting latest timestamp always win.
  - Key is always a string but value could be anything as long as it's just primitive values.
# filesystem-on-indexeddb
- https://github.com/filerjs/filer
  - Filer is a drop-in replacement for node's fs module, a POSIX-like file system for browsers.
  - Filer uses IndexedDB

- https://github.com/fagbokforlaget/simple-fs
  - Handles files on indexeddb like you would do in node.js (promise)

- https://github.com/playerony/indexeddb-fs
  - An "fs" kind of library dedicated to the browser.

- https://github.com/piatkowski/filequeue.js
  - FileQueue in JS - set, store, get, delete, clear Files in IndexedDB. To be used as a upload queue.

- https://github.com/lecepin/file-proxy-indexedDB
  - https://lecepin.github.io/file-proxy-indexedDB/
  - 使用ServiceWorker实现本地图片上传到IndexedDB，并进行 proxy 进行读取操作

- https://github.com/jvilk/BrowserFS
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
# more
- https://github.com/SyncProxy/sync-client
  - SyncProxy javascript client with support for all major embedded databases (IndexedDB, SQLite, WebSQL, LokiJS...)