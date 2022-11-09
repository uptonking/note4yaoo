---
title: toc-db-indexeddb-utils-extensions
tags: [indexeddb, toc, utils]
created: 2022-06-04T00:43:13.971Z
modified: 2022-11-04T14:22:17.373Z
---

# toc-db-indexeddb-utils-extensions

# popular

- https://github.com/fkworld/indexeddb-benchmark
  - simple indexeddb benchmark website
  - 测试内容
    - 在主线程中读写数据。
    - 在 worker 中读写数据。
    - 在 worker 中读写数据，并使用 transfer。
  - indexeddb 虽然是异步读写，但是依然会阻塞主线程。原因是其涉及到数据的结构化克隆。所以在读写大量数据时，需要使用 worker。
  - 在 worker 中 indexeddb 的读写速度比在主线程中慢很多。原因未知，可能与 cpu 占用有关。
  - worker transfer 能大大增加主线程与 worker 间的数据传输速度。但要注意交出控制权后，处理逻辑会有相应变化。

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

- https://github.com/KayleePop/idb-kv
  - A tiny and simple API for indexeddb with automatic batching for out of the box performance.
  - https://github.com/KayleePop/idbkv-chunk-store
    - Abstract chunk store built on idb-kv: the lightweight and simple API for indexeddb with automatic batching
- https://github.com/simplifyjs/indexeddb-crud
  - Comparison between native IndexedDB API and using IDB library in operating CRUD workaround

- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.

- https://github.com/stoxy-js/stoxy
  - Stoxy is a state management API for all modern Web Technologies.
  - Stoxy stores the data in a in-browser Database called IndexedDB, only keeping the latest 5 accessed objects in-memory for faster access.
  - Stoxy utilizes a promise-based use flow making it really easy to asynchronously read and write from the storage.
  - If your browser doesn't support IndexedDB, there's no need to worry. Stoxy recognizes these cases automatically, and opts out of using it and utilizes a in-memory system only.
- https://github.com/phanhuyanh/choxy
  - reactive state management system and wrapper for IndexedDB.
  - Choxy allows you to easily handle, save data to IndexedDB

- https://github.com/falsandtru/clientchannel
  - Persist objects and sync them between tabs via IndexedDB or LocalStorage.
# filesystem-on-indexeddb
- https://github.com/filerjs/filer
  - Filer is a drop-in replacement for node's fs module, a POSIX-like file system for browsers.
  - Filer uses IndexedDB

- https://github.com/fagbokforlaget/simple-fs  /js
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
# indexeddb-cache
- https://github.com/akirarika/kurimudb /202202/ts
  - 一款渐进式的 Web 端本地存储库，可将数据保存到 LocalStorage、IndexedDB、Cookie 等地方，和订阅值的变更。
  - 除了持久化数据之外，若你愿意，Kurimudb 还能成为你应用的 Model 层抽象，接任你应用中状态管理库的职责 (如 Vuex、Redux、Mobx)，使你应用真正拥有单一数据来源。

- https://github.com/piotr-cz/swr-idb-cache
  - IndexedDB Cache Provider for SWR
  - Synchronize SWR Cache with IndexedDB to get offline cache.
  - Library reads current state of cache stored in IndexedDB into memory using idb during initialization. Then it resolves into Cache Provider which should be passed to SWR.

- https://github.com/yishiashia/indexeddb-image-cache
  - A example of images cached with indexedDB.

- https://github.com/baiyukey/headLoader
  - 使用indexedDB管理页面缓存，减少不必要的网络请求，加速页面装载速度。
  - headLoader的主要功能有：资源加载、预加载、热加载、多页面缓存共享、代码隐藏等。
  - 主要作用是使网站快速响应及反编译

- https://github.com/StudentOfJS/query-plus
  - fetch and process data in web worker, store in indexedDB.

- https://github.com/zmkwjx/baikbingo-cache
  - 基于indexedDB的缓存解决

- https://github.com/piotr-cz/swr-idb-cache
  - IndexedDB Cache Provider for SWR

- https://github.com/knadh/indexed-cache
  - library for sideloading static assets on pages and caching them in the browser's IndexedDB 
# storage-uniform-interface
- https://github.com/idleberg/web-porridge /ts
  - Feature-enhanced wrapper for both, Storage API and IndexedDB API, sharing a common, familiar interface.
  - automatic (de)serialization
  - Object-level read & write access

- https://github.com/beforesemicolon/client-web-storage
  - Browser storage interface for IndexedDB, WebSQL, LocalStorage, and in memory data with Schema and data validator.

- https://github.com/badbatch/cachemap
  - An extensible, isomorphic cache with modules to interface with Redis, LocalStorage, IndexedDB and an in-memory Map.
# indexeddb-utils
- https://github.com/NullixAT/browstorjs  /ts
  - Persistent key/value data storage for your Browser and/or PWA, promisified, including file support and service worker support, all with IndexedDB.

- https://github.com/dabblewriter/browserbase
  - IndexedDB wrapper providing promises, easy versioning, and events, including change events across tabs

- https://github.com/dumbmatter/fakeIndexedDB
  - A pure JS in-memory implementation of the IndexedDB API
- https://github.com/bigeasy/indexeddb
  - A pure-JavaScript, persistent implementation of IndexedDB.

- https://github.com/YeloPartyHat/LocalDatabase
  - simple queryable embedded database designed for front-end that wraps IndexedDB.

- https://github.com/kennygomdori/AsyncIndexedDB
  - asynchronous wrapper around Javascript IndexedDB. 
- https://github.com/westhide/async-idb
  - async, easy to use, fully typed indexedDB library

- https://github.com/Doxor-js/doxor.js
  - Offline database in Front-End library for interacting with IndexedDB

- https://github.com/toba/db
  - An IndexedDB API intentionally modeled after Firestore with the expectation it will often be used alongside Firestore.
- https://github.com/tangshuang/indb
  - Maybe the best way to understand and use indexedDB.

- https://github.com/NetsydeMiro/typeddb
  - A TypeScript wrapper for the IndexedDB browser API, enabling strongly typed ORM style querying.

- https://github.com/unadlib/origin-storage
  - A same-origin storage for cross-domain access, it is based on localForage and supports IndexedDB, WebSQL and localStorage
  - origin-storage uses localStorage in browsers with no IndexedDB or WebSQL support. And Safari is not supported.

- https://github.com/ipfs/js-idb-pull-blob-store
  - IndexedDB implementation for interface-pull-blob-store

- https://github.com/WebReflection/indexed-values
  - An ever growing Set based utility to optimize JSON, IndexedDB, or postMessage.

- https://github.com/kevinfarrugia/redux-persist-indexeddb-worker-storage
  - Redux Persist storage engine using IndexedDB and web workers.

- https://github.com/lr0pb/IDB.js
  - a lightweight high-level promise-based wrapper for fast access to IndexedDB API

- https://github.com/codeart1st/idb-rbush
  - IDB-RBush is a high-performance JavaScript library for 2D spatial indexing of points and rectangles in an IndexedDB object store. 
  - It's based on an optimized R-tree data structure with bulk insertion support.
  - Spatial index is a special data structure for points and rectangles that allows you to perform queries like "all items within this bounding box" very efficiently (e.g. hundreds of times faster than looping over all items). It's most commonly used in maps and data visualizations.

- https://github.com/Vissie2/dexie-2d-geospatial-index
  - A playground to test the performance of H3 geospatial indexing using Dexie.
# json-key-value
- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.

- minimongo /1kStar/LGPLv3/202207/ts
  - https://github.com/mWater/minimongo
  - A client-side MongoDB implementation which supports basic queries, including some geospatial ones.
  - It is either IndexedDb backed (IndexedDb), WebSQL backed (WebSQLDb), Local storage backed (LocalStorageDb) or in memory only (MemoryDb).

- ZangoDB /1kStar/MIT/201710/js
  - https://github.com/erikolson186/zangodb
  - ZangoDB is a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.
# encryption-security
- https://github.com/willgm/web-crypto-storage
  - tiny promise-based crypto keyval storage using IndexedDB and the native Web Crypto API
- https://github.com/AKASHAorg/secure-webstore
  - A secure IndexedDB store with built-in encryption
- https://github.com/desiic/enindex
  - Encrypted IndexedDB - Designed for convenience of use, using Promise instead of callback 
# more-utils
- https://github.com/jurca/indexed-db.es6
  - The indexed-db.es6 is ES2015-style wrapper of the native IndexedDB HTML5 document-oriented database.
  - declarative schema with data-migration support

- https://github.com/JayPuff/browser-file-storage
  - Abstracts the complexity of indexed DB so that a user can easily save files/blobs by key/filename on the browser
  - Browser must support the IndexedDB API as it cannot be polyfilled
