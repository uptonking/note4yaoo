---
title: toc-db-indexeddb-uitls
tags: [indexeddb, toc, utils]
created: '2022-06-04T00:43:13.971Z'
modified: '2022-06-04T00:43:59.348Z'
---

# toc-db-indexeddb-uitls

# popular
- https://github.com/dexie/Dexie.js
  - A Minimalistic Wrapper for IndexedDB
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
# indexeddb-react-vue
- https://github.com/assuncaocharles/react-indexed-db
  - wraps IndexedDB database in an Declarative way. 
  - It exposes very simple promises API to enable the usage of IndexedDB 

- https://github.com/hc-oss/use-indexeddb
  - hook w/ promises for easy IndexedDB access in React

- https://github.com/eldomagan/vuex-orm-localforage
  - VuexORMLocalforage is a plugin for the amazing VuexORM that let you sync your Vuex Store with an IndexedDB database using LocalForage.
# more-indexeddb-repos
