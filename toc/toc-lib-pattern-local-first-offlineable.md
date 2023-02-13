---
title: toc-lib-pattern-local-first-offlineable
tags: [lib, local-first, pattern, toc]
created: 2021-08-25T15:50:00.635Z
modified: 2021-09-04T14:03:39.046Z
---

# toc-lib-pattern-local-first-offlineable

# guide

- search: local-first, local first, offline first

- local-first + realtime协作的示例
  - https://github.com/gongojs/project
  - https://github.com/a-type/lo-fi
# popular
- tuple-database /219Star/NALic/202209/ts
  - https://github.com/ccorcos/tuple-database
  - 依赖fs-extra, lodash, fractional-indexing
  - The architecture of this database draws inspiration from a bunch of different places (although, primarily from FoundationDb).
  - 👉🏻 The local-first, "end-user database" database.
  - 👉🏻 All queries are reactive.
  - 👉🏻 ✨ Schemaless — schemas are enforced by the application, not the database.
  - 👉🏻 Asynchronous or Synchronous, Persisted or In-Memory Storage
  - Transactional read/writes written in TypeScript.
  - 👉🏻 Directly read/write indexes with the ability to index graph/relational queries.
    - The logic we've written here for the tuple-database code is exactly what any SQL database is doing under the hood.
  - Suitable for frontend state management.
  - https://github.com/maccman/tuple-playground

- tinybase /1.4kStar/MIT/202212/ts/NoDeps
  - https://github.com/tinyplex/tinybase
  - https://tinybase.org/
  - TinyBase is a smart new way to structure your local app data
  - 基于自定义TinyQL(类似SQL)实现查询
  - 基于checkpoint实现undo
  - 基于hlc crdt实现冲突处理
  - Familiar concepts of tables, rows, and cells, and schematization to model your data domain.
  - Flexibly reactive to reconciled updates, so you only spend cycles on the data that changes.
  - Indexing, metrics, relationships - and even an undo stack for your app state!
  - Easily sync your data to local or remote storage, and use idiomatic bindings to your React UI.
  - Powerful query engine to select, join, filter, group, sort and paginate data - reactively.
    - The Queries object lets you query data across tables, with filtering and aggregation - using a SQL-adjacent syntax called `TinyQL`.
  - A Persister object lets you save and load Store data to and from different locations, or underlying storage types.

- evolu /101Star/GPLv3/202210/ts
  - https://github.com/evoluhq/evolu
  - https://www.evolu.dev/
  - React Hooks library for local-first software with end-to-end encrypted backup and sync using SQLite and CRDT
  - writing local-first software has been challenging because of the lack of libraries and design patterns. I personally failed several times, and that's why I created Evolu.
  - Evolu architecture is almost a clone of James Long CRDT for mortals. Rewritten and improved
  - Evolu uses end-to-end encryption and generates strong and safe passwords for you. 
    - Evolu sync and backup server see only timestamps. Nothing more. 
    - We plan to do at least two security audits.
  - Evolu is not pure P2P software. For syncing and backup, there needs to be a server. 
  - Evolu CRDT has no support for transactions because CRDT transactions are still an unsolved issue. 

- redux-offline /6.1kStar/202012/MIT/js
  - https://github.com/redux-offline/redux-offline
  - https://github.com/redux-offline/offline-side-effects /202101/ts
  - Build Offline-First Apps for Web and React Native
  - Persistent Redux store for Reasonaboutable Offline-First applications, with first-class support for optimistic UI. 
  - Use with React, React Native, or as standalone state container for any web app.
  - 🤔 没必要执着于寻找已有的offline方案，使用 persist + crdt 也可以实现协作，甚至普通的协作同步

- turtleDB /443Star/MIT/201809/js
  - https://github.com/turtle-DB/turtleDB
  - https://turtle-db.github.io/
  - turtleDB is a JavaScript framework and in-browser database for developers to build offline-first, collaborative web applications. 
  - It provides a developer-friendly API to access an in-browser database built on top of IndexedDB.
  - It comes with built in document versioning and automatic server synchronization when paired with our back-end package tortoiseDB
  - https://github.com/turtle-DB/tortoiseDB
    - NodeJS server and mongoDB wrapper for clients to sync to when using turtleDB. 

- SingleFile /9.5kStar/AGPLv3/202211/js
  - https://github.com/gildas-lormeau/SingleFile
  - a Web Extension (and a CLI tool) compatible with Chrome, Firefox to save a complete web page into a single HTML file.
  - 比较了各种格式：singleFile、mhtml、webarchive、html-folder
  - For security reasons, SingleFile is sometimes unable to save the image representation of canvas and snapshots of video elements.
  - [File name doesn't match the page title when saving a page](https://github.com/gildas-lormeau/SingleFile/issues/1106)
    - Please, uncheck "save pages in background" in options (Misc) than you will get the correct title name!
  - https://github.com/gildas-lormeau/SingleFileZ
    - a fork of SingleFile that allows you to save a webpage as a self-extracting HTML file

- https://github.com/aphrodite-sh/aphrodite
  - Aphrodite is a schema layer whose first goal is to make P2P & Local-First software as easy to develop as traditional client-server software.
  - You can think of Aphrodite as an ORM of sorts that is designed for the needs of Local-First applications and P2P data transfer.
  - everything in Aphrodite begins with a schema. This schema encodes the application's data

- local-first /191Star/202104/js/inactive
  - https://github.com/jaredly/local-first
  - This aims to eventually be a fully-featured solution for managing, syncing, and storing application data, in a way that works offline, and collaboratively.
  - Currently implemented
    - a hybrid logical clock (blog post, code)
    - a nested object CRDT (code)
    - a rich-text CRDT (code, example integration with quill, visualization of the data structure)
  - [Local-first database: RxDB + PouchDB](https://jaredforsyth.com/posts/local-first-database-rxdb-pouchdb/)

- IDBSideSync /8Star/MIT/202104/ts
  - https://github.com/clintharris/IDBSideSync
  - https://idbsidesync-todo-demo.vercel.app/
  - IDBSideSync is an experimental JavaScript library that makes it possible to sync browser-based IndexedDB databases using CRDT concepts
  - 基于浏览器的同步方案可参考更成熟的remoteStorage
  - As your app makes CRUD calls to its IndexedDB database, IDBSideSync proxies/intercepts those calls and records the operations to a log (the "oplog").
  - IDBSideSync will upload the client's oplog entries (CRDT state mutation messages) to the remote data store using the registered plugins, and also download other client's oplog entries
  - A hybrid logical clock (i.e., time + counter) is maintained among the clients to help figure out which operations "win" if more than one exists for the same database store/record/property.

- https://github.com/pubkey/broadcast-channel
  - BroadcastChannel allows you to send data between different browser-tabs or nodejs-processes.
  - It works completely client-side and offline, 

- https://github.com/logux/client
  - https://logux.io/
  - Logux is a new way to connect client and server. 
  - Instead of sending HTTP requests (e.g., AJAX and GraphQL) it synchronizes log of operations between client, server, and other clients.
  - Logux and WebSocket client/server framework to make:
    - Logux has features inspired by CRDT to resolve edit conflicts between users. Real-time updates to prevent conflicts
    - Logux combines WebSocket with modern reactive client architecture. It synchronizes Redux actions between clients and servers, and keeps the same order of actions.
    - Offline-first for the next billion users or New York City Subway. Logux saves Redux actions to IndexedDB and has a lot of features to merge changes from different users.
    - Compatible with modern stack: Redux, Vuex and pure JS API, works with any back-end language and any database.

- https://github.com/nornagon/autowiki /automerge
  - Autowiki is a tool for creating networked documents.
  - Autowiki is a local-first app: you own all the data you put into it, and your data never leaves your own machine unless you want it to.
  - Autowiki uses automerge under the hood to resolve edit conflicts automatically.

- https://github.com/hoodiehq/hoodie
  - Hoodie lets you build apps without thinking about the backend and makes sure that they work great independent of connectivity.
  - https://github.com/hoodiehq/hoodie-app-tracker

- https://github.com/local-first-web/state /automerge
  - A Redux-based state container for local-first software, offering seamless synchronization using Automerge CRDTs. (Formerly known as fish Cevitxe).
  - @localfirst/state is an automatically replicated Redux store that gives your app offline capabilities and secure peer-to-peer synchronization superpowers.
  - https://github.com/local-first-web/auth
  - https://github.com/local-first-web/relay

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
# local-first-examples
- hamsterbase /158Star/MIT/202211/ts/仅开源sdk
  - https://github.com/hamsterbase/hamsterbase
  - https://hamsterbase.com/zh/
  - 一个本地优先的网页存档应用。 a self-hosted, local-first web archive application.
  - 本地部署 + 完全离线 + 点对点同步（马上发布了）
  - 储存、管理和预览 HTML, MHTML and Webarchive 格式的文档。
  - 对保存的页面进行高亮、批注。
  - 开源 SDK，目前免费。
  - Full Text Search
  - Open source SDK
  - 推荐使用 SingleFile 保存 html 页面
  - 支持点对点同步，测试时可用本地同步官网，api填写 https://hamsterbase.onrender.com，结尾无/

- https://github.com/unigraph-dev/unigraph-dev
  - A local-first and universal knowledge graph, personal search engine, and workspace for your life.

- https://github.com/digidem/mapeo-desktop
  - An offline map editing application for indigenous territory mapping in remote environments. 
  - It uses mapeo-core for offline peer-to-peer synchronization of an OpenStreetMap database, without any server. 
  - The map editor is based on iDEditor. 
  - The app is built with Electron.
# offline
- https://github.com/localForage/localForage
  - Offline storage, improved. Wraps IndexedDB, WebSQL, or localStorage using a simple but powerful API.

- https://github.com/hoodiehq/hoodie
  - A generic backend with a client API for Offline First applications

- https://github.com/lana-k/sqliteviz
  - Sqliteviz is a single-page offline-first PWA for fully client-side visualisation of SQLite databases or CSV files.
  - Instant offline SQL-powered data visualisation in your browser
  - run SQL queries against a SQLite database and create Plotly charts and pivot tables based on the result sets

- https://github.com/cloudpeers/tlfs  /rust
  - offers a stack to write applications as productively as when using state-of-the-art cloud-based architectures, while providing the Seven Ideals for Local-First Software
# collab
- https://github.com/YousefED/Matrix-CRDT
  - Use Matrix as a backend for local-first applications with the Matrix-CRDT Yjs provider.

- https://github.com/rocicorp/replicache
  - Realtime Sync for Any Backend Stack
# exploring
- https://github.com/drifting-in-space/plane /202212/rust
  - Plane is a container orchestrator for ambitious browser-based applications. 
  - Plane implements an architecture we call session backends.
  - Plane assigns a unique subdomain to each instance, through which it proxies HTTPS/WebSocket connections. When all inbound connections to a container are dropped, Plane shuts it down.
  - [Session Backends](https://driftingin.space/posts/session-lived-application-backends)
# more
- https://github.com/cwise89/react-detect-offline
  - Components that track offline and online state. Render certain content only when online (or only when offline).

- https://github.com/dxxzst/OfflineMap
  - 基于MySQL + Node.js + Leaflet的离线地图展示，支持百度、谷歌、高德、腾讯地图

- https://github.com/madipta/offline-first
  - Sample offline first using Nx monorepo, React, RxDb, NestJs, Prisma, GraphQl, PostgreSql

- https://github.com/rjmackay/offline-db-preso
  - Offline-first data sharing talk for nz.js(con)

- https://docs.amplify.aws/lib/datastore/getting-started/q/platform/js/
  - allows you to start persisting data locally to your device with DataStore, even without an AWS account.
  - Amplify DataStore provides a programming model for leveraging shared and distributed data without writing additional code for offline and online scenarios, which makes working with distributed, cross-user data just as simple as working with local-only data.
