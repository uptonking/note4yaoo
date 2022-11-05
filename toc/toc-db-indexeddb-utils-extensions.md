---
title: toc-db-indexeddb-utils-extensions
tags: [indexeddb, toc, utils]
created: 2022-06-04T00:43:13.971Z
modified: 2022-11-04T14:22:17.373Z
---

# toc-db-indexeddb-utils-extensions

# popular

- https://github.com/jakearchibald/idb
  - IndexedDB, but with promises
- https://github.com/darrachequesne/synceddb
  - a fork of the awesome idb library, which adds the ability to sync an IndexedDB database with a remote REST API.
- https://github.com/sylvia1106/idb-managed
  - Easy IndexedDB API, using DB manager to manage local database. Based on idb.
- https://github.com/jakearchibald/idb-keyval
  - a super-simple promise-based keyval store implemented with IndexedDB, originally based on async-storage by Mozilla.
- https://github.com/haixiangyan/my-idb-keyval
  - 最近用到了 idb-keyval 这个库，阅读了一下源码后终于是有点感觉了
  - 手把手带你造一个 idb-keyval 轮子
- https://github.com/azu/kvs
  - Key Value storage for Browser, Node.js, and In-Memory.
  - I want to get universal storage library that works on Browser and Node.js.
  - Previously, I've created localstorage-ponyfill for this purpose. However,  `Window.localStorage` does not work on Web Workers or Service Worker
  - @kvs/* packages provide async storage API using IndexedDB etc and resolve this issue.
- https://github.com/KayleePop/idb-kv
  - A tiny and simple API for indexeddb with automatic batching for out of the box performance.
  - https://github.com/KayleePop/idbkv-chunk-store
    - Abstract chunk store built on idb-kv: the lightweight and simple API for indexeddb with automatic batching
- https://github.com/simplifyjs/indexeddb-crud
  - Comparison between native IndexedDB API and using IDB library in operating CRUD workaround
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

- https://github.com/BrianHung/filesystem /2019/inactive
  - https://brianhung.info/filesystem/demo
  - a FileSystem built on IndexedDB

- https://github.com/lecepin/file-proxy-indexedDB
  - https://lecepin.github.io/file-proxy-indexedDB/
  - 使用ServiceWorker实现本地图片上传到IndexedDB，并进行 proxy 进行读取操作

- https://github.com/jvilk/BrowserFS
  - BrowserFS is an in-browser filesystem that emulates the Node JS filesystem API and supports storing and retrieving files from various backends.
# indexeddb-utils
- https://github.com/dabblewriter/browserbase
  - IndexedDB wrapper providing promises, easy versioning, and events, including change events across tabs

- https://github.com/dumbmatter/fakeIndexedDB
  - A pure JS in-memory implementation of the IndexedDB API
- https://github.com/bigeasy/indexeddb
  - A pure-JavaScript, persistent implementation of IndexedDB.

- https://github.com/baiyukey/headLoader
  - 使用indexedDB管理页面缓存，减少不必要的网络请求，加速页面装载速度。
  - headLoader的主要功能有：资源加载、预加载、热加载、多页面缓存共享、代码隐藏等。
  - 主要作用是使网站快速响应及反编译

- https://github.com/zmkwjx/baikbingo-cache
  - Baikbingo 基于indexedDB的缓存解决

- https://github.com/kennygomdori/AsyncIndexedDB
  - asynchronous wrapper around Javascript IndexedDB. 

- https://github.com/badbatch/cachemap
  - An extensible, isomorphic cache with modules to interface with Redis, LocalStorage, IndexedDB and an in-memory Map.

- https://github.com/toba/db
  - An IndexedDB API intentionally modeled after Firestore with the expectation it will often be used alongside Firestore.

- https://github.com/NetsydeMiro/typeddb
  - A TypeScript wrapper for the IndexedDB browser API, enabling strongly typed ORM style querying.

- https://github.com/unadlib/origin-storage
  - A same-origin storage for cross-domain access, it is based on localForage and supports IndexedDB, WebSQL and localStorage
  - origin-storage uses localStorage in browsers with no IndexedDB or WebSQL support. And Safari is not supported.

- https://github.com/WebReflection/indexed-values
  - An ever growing Set based utility to optimize JSON, IndexedDB, or postMessage.
# json-key-value
- minimongo /1kStar/LGPLv3/202207/ts
  - https://github.com/mWater/minimongo
  - A client-side MongoDB implementation which supports basic queries, including some geospatial ones.
  - It is either IndexedDb backed (IndexedDb), WebSQL backed (WebSQLDb), Local storage backed (LocalStorageDb) or in memory only (MemoryDb).
  - Uses code from Meteor.js minimongo package, reworked to support more geospatial queries 

- zangodb /1kStar/MIT/201710/js
  - https://github.com/erikolson186/zangodb
  - ZangoDB is a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.
# more-utils
- https://github.com/jurca/indexed-db.es6
  - The indexed-db.es6 is ES2015-style wrapper of the native IndexedDB HTML5 document-oriented database.
  - declarative schema with data-migration support

- https://github.com/JayPuff/browser-file-storage
  - Abstracts the complexity of indexed DB so that a user can easily save files/blobs by key/filename on the browser
  - Browser must support the IndexedDB API as it cannot be polyfilled
