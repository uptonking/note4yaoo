---
title: lib-collab-common-examples-sync-p2p
tags: [collaboration, data-sync, examples, p2p, synchronization]
created: 2023-01-17T19:10:10.160Z
modified: 2023-01-17T19:13:01.845Z
---

# lib-collab-common-examples-sync-p2p

# guide
- 考虑到客户端升级的问题
  - 同步前一定要检查一个version，参考indexeddb upgrade
# sync-examples
- verdant/lo-fi /7Star/MIT/202211/ts
  - https://github.com/a-type/verdant
  - https://github.com/a-type/lo-fi
  - https://verdant.dev/
  - An IndexedDB-powered database and data sync solution for lightweight, local-first web apps.
  - server依赖sqlite、jwt、ws
  - 基于hybrid-logical-clock
  - Undo and redo changes
  - it includes an optional server which unlocks the power of sync and realtime
  - the goal of lo-fi is to be simple and recognizable.
    - One small, generic syncing server is all you need
    - NO. Infinitely growing storage usage
    - NO. Having to deeply understand CRDTs
    - NO. Peer to peer networking
    - NO. WASM-compiled databases in your browser
  - [Investigate: move off dependency on sync SQLite (and multi-node scaling)](https://github.com/a-type/verdant/issues/263)
    - Using better-sqlite3 for synchronous writes also meant that writes block reads for the whole server, which is convenient from an abstract standpoint but also bad from a scaling and adaptability standpoint.
    - Another thing that would block multi-node scaling is server order (unless I did something like LiteStream and only allowed one writer node, but that kind of feels too rigid when I've already got CRDTs in use...).

- https://github.com/drifting-in-space/driftdb /ts/rust
  - https://driftdb.com/
  - A real-time data backend for browser-based applications.
  - core Rust driftdb implementation.

- https://github.com/webstudio-is/immerhin /ts
  - Send patches around to keep the system in sync.
  - The core idea is to use immer-patches to keep the UI in sync between client and server, multiple clients, or multiple windows.
  - 依赖 immer-patches
  - It uses Immer as an interface for state mutations and provides a convenient way to group mutations into a single transaction, and enables undo/redo out of the box.
  - Get undo/redo for free
  - Server agnostic
  - State management libraries agnostic (a container interface)
  - **Resolve conflicts (not implemented yet)**
  - [Patches | Immer](https://immerjs.github.io/immer/patches/)
    - The generated patches are similar (but not the same) to the RFC-6902 JSON patch standard, except that the path property is an array, rather than a string. 

- https://github.com/Rolands-Laucis/Socio
  - A WebSocket based realtime duplex Front-End and Back-End syncing API paradigm framework

- https://github.com/serenity-kit/secsync
  - Is an architecture to relay end-to-end encrypted CRDTs over a central service.
  - eg: End-to-end encrypted document using Yjs incl. Cursor Awareness
  - eg: End-to-end encrypted todo list using Automerge
  - Why use a central relay service?
    - The main reason is to exchange data asynchronously.

- https://github.com/peers/peerjs /202303/ts
  - PeerJS provides a complete, configurable, and easy-to-use peer-to-peer API built on top of WebRTC, supporting both data channels and media streams.

- https://github.com/ar-nelson/osmosis-js /202103/ts
  - An in-process JSON database with automatic peer-to-peer background synchronization between devices on a local network. Keep your apps in sync without a cloud!
  - 传输层使用jsonrpc
  - Osmosis synchronization is automatic, encrypted, and relatively safe from conflicts. Updates are modeled with a JSON CRDT.
  - Osmosis uses two kinds of sockets: broadcast UDP sockets that send heartbeat packets, and unicast TCP sockets that send Monocypher-encrypted, zstandard-compressed JSON-RPC messages.

- https://github.com/JacobJaffe/event-system-prototype
  - Prototype of a syncing game state between a p2p, host switching network through an action system & event history.

- https://github.com/spreadjs/spread /js
  - Spread.js is a local JavaScript datastructure, that is instantly synced across devices/nodes/instances
  - It can be used, when building distributed applications, that need local in-memory data for fast access.
  - Use Plain JavaScript Objects
  - Technically the process is pretty simple. 
    - The Storage object is being monitored using a JS Proxy. 
    - Every change will instantly be emitted to the server, where is gets broadcasted to all connected instances. 
    - On each instance, the incoming operation is applied, keeping the storage object in sync.
  - Wen a new instance joins the group, it automatically requests the current state of the storage object. 
    - Any other instance will then send a copy of the data object to the new instance.

- https://github.com/derhuerst/files-sync-stream
  - Sync files (or any blobs of data) between two peers, in both directions, over any transport. 
  - You decide where and how to store the files. 
  - files-sync-stream accepts a generic file read function and emits data events when receiving data.

- https://github.com/kettle11/tangle /ts/rust/wasm
  - https://tanglesync.com/
  - Tangle is a library that aims to make multiplayer apps and games far easier to build.
  - Tangle 'magically' wraps WebAssembly so you can write programs without worrying about message passing, serialization, or consensus.
  - Under the hood Tangle uses peer to peer WebRTC connections. This may change!

- https://github.com/RamonGal/Distributed-Systems /lamport+redis-redlock
  - This view is to be managed by a django rest backend that serves the views json response, which will be a serialized disposition of data from a postgres database.
  - For a perfectly in sync view for different users, we use an implementation of a `Lamport` timestamp.
  - An algorithm for mutual exclusion using a `redis Redlock` was made and the above mentioned timestamp helps determines the pace with which we can apply changes to the shared state.
  - [Redis Redlock](https://redis.com/redis-best-practices/communication-patterns/redlock/) is canonical implementations of locking

- https://github.com/NangoHQ/nango /202212/ts
  - https://www.nango.dev/
  - Nango continuously syncs data from any API endpoint (that returns JSON) to your database.
  - Nango has built-in support for OAuth through our sister project Pizzly

- https://github.com/primus/primus /202301/js
  - Primus, the creator god of the transformers & an abstraction layer for real-time to prevent module lock-in.
  - There are a lot of real-time frameworks available for Node.js and they all have different opinions on how real-time should be done. 
  - Primus provides a common low level interface to communicate in real-time using various real-time frameworks.
  - Built-in reconnect, it just works. 
  - Offline detection, Primus is smart enough to detect when users drop their internet connection (switching WIFI points/cell towers for example) and reconnects when they are back online.
  - Automatically encodes and decodes messages using custom parsers. Can be easily switched for binary encoding for example.
  - A clean, stream-compatible interface for the client and server.
  - Comes with an amazing plugin interface to keep the core library as fast and lean as possible while still allowing the server and the client to be extended
  - Primus doesn't ship with real-time frameworks as dependencies, it assumes that you as user add them yourself as a dependency. This is done to keep the module as lightweight as possible

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

- https://github.com/hyperhyperspace/hyperhyperspace-core
  - HHS uses an immutable typed-objects local storage model. Objects are both retreived and cross-referenced using a structural hash of their contents as their id (a form of content-based addressing).
  - Mutability is implemented using CRDTs. Identities and data authentication are cryptographic.
  - Objects and their references form an immutable DAG, a fact that is used for data replication in HHS p2p mesh.

- https://github.com/feathersjs-ecosystem/feathers-sync
  - Synchronize service events between Feathers application instances
  - When running multiple instances of your Feathers application (e.g. on several Heroku Dynos), service events (created, updated, patched, removed and any custom defined events) do not get propagated to other instances.
  - feathers-sync uses a messaging mechanism to propagate all events to all application instances. 
  - It currently supports redis, amqp/RabbitMQ

- https://github.com/yomorun/presencejs
  - a JavaScript library that allows you to build real-time web applications . 
  - The server is built on top of YoMo(go)
  - Fallback to WebSocket if WebTransport connection cannot be established

- https://github.com/CoCreate-app/CoCreate-cursors
  - https://cocreate.app/docs/cursors
  - Collaborative user cursor position for inputs, textarea's and contenteditable elements.

- https://github.com/ssbc/secret-stack /js
  - create secure peer to peer networks using secret-handshakes.
  - This provides a framework to make building secure, decentralized systems easier. (such as ssb-server which this was refactored out of ;)
  - https://github.com/ssbc/ssb-db
    - secret-stack plugin which provides storing of valid secure-scuttlebutt messages in an append-only log.


# sync-json
- https://github.com/zettant/realtime-object-sync
  - server and client libraries for realtime JSON object synchronization.

- https://github.com/jsebrech/minisync /基于deltaState
  - A library for P2P synchronization of JSON data objects, enabling a set of peers to synchronize changes to a JSON object without relying on a central server.
  - Clients can merge in any and all directions, they just need to have a shared ancestry by initially creating an object from the result of getChanges of any other client.
  - Minisync encodes the changes to send between parties as a JSON structure.
  - Lock-free algorithm, many clients can edit the same object in parallel
  - Eventually consistent state between all clients
  - limitations: This is experimental code and therefore likely to break between versions, causing data loss across all clients when a new minisync version is deployed!

- https://github.com/frameable/pigeon /js
  - Diff, patch, merge, and synchronize JSON documents with an Automerge-compatible interface
  - While Automerge optimizes for working offline and merging changes periodically, Pigeon is optimized for online real-time collaboration.
  - Change sets use JSON-Patch-esque paths, and so are more easily introspectable using existing tools

- https://github.com/privatenumber/reactive-json-file
  - Reactively sync JSON mutations to disk

- https://github.com/JoshMerlino/filestore-json
  - Easily sync JSON objects of any shape with the filesystem.
  - Read & write to JSON files on a storage device without the need to interact with the filesystem.
  - Persistent data between process restarts.
  - Automatically updates internal value when JSON file is modified.

- https://github.com/MagicCube/hybrid-storage
  - 一种可以在本地离线与云端同步 JSON 对象的存储方案。
  - 用本地的 LocalStorage 和云端的 OSS 文件同时存储 JSON 键值对数据
  - 读操作默认走本地的 LocalStorage，写操作则是先写本地，然后再以异步操作队列（AsyncQueue 类）同步至服务端

- https://github.com/ken107/push-model
  - This Node module implements a WebSocket JSON-RPC server with object synchronization capabilities based on the JSON-Pointer and JSON-Patch standards.
  - Harmony Proxy is used to detect subsequent changes to the data, which are published incrementally as JSON Patches.

- https://github.com/codePlaceOfficial/virtualFileServer
  - keep local files and JSON objects in sync

- https://github.com/lloydeverett/json-sync-server
  - Simple ExpressJS HTTP server that allows all clients to sync (read or update) a single JSON object. 
# sync-state

# more
- https://github.com/owojcikiewicz/realtime-sync
  - enables collaborative editing of HTML inputs in real-time across multiple websites and clients.
  - built using WebSockets

- https://github.com/flmeHashira/Clip-Sync
  - Realtime Clipboard Sync based on Electron and Realm
  - frontend + backend

- https://github.com/damrbaby/pathsync
  - firebase-like realtime sync powered by Redis and WebSockets.
  - In-memory syncing of paths using Node.js, Redis, and WebSockets that live streams to observables.
  - Redis needs to be running. Requires ioredis, faye, and express.

- https://github.com/JailBreakC/distributed-json-ot /未实现
  - distributed json ot demo project, shows how to sync data with version control
