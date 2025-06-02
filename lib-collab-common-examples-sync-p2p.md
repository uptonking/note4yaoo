---
title: lib-collab-common-examples-sync-p2p
tags: [collaboration, data-sync, examples, p2p, synchronization]
created: 2023-01-17T19:10:10.160Z
modified: 2023-01-17T19:13:01.845Z
---

# lib-collab-common-examples-sync-p2p

# guide

- tips
  - collab/sync/realtime
  - 主流框架或cms大多支持websocket通信

- 考虑客户端升级的问题
  - 同步前一定要检查一个version，参考indexeddb upgrade
  - 参考sqlite+http-range的部分下载示例(sql.js-httpvfs)
# sync-solutions
- https://github.com/rocicorp/mono /apache2/202412/ts
  - https://mono-replicache-trunk-docs.vercel.app/
  - This is the mono repo for Rocicorp's two main products (as of 2024).
  - packages/zero-client: The main client library. It use replicache under the hood.
  - packages/zero-cache: The server side code.
  - packages/zql: The IVM (incremental view maintenance) engine as well as the query language/API.
  - apps/zbugs: The bug tracker app.
  - packages/replicache: The replicache client library.
  - Reflect is no longer under development.
  - https://github.com/cbnsndwch/zero-sources
    - A collection of utilities and custom change sources for @rocicorp/zero

- https://github.com/powersync-ja/powersync-service /FSL-1.1-Apache-2.0(2y)/202406/ts
  - https://www.powersync.com/
  - The backend PowerSync Service responsible for data replication.
  - PowerSync is a Postgres-SQLite sync layer, which helps developers to create local-first real-time reactive apps that work seamlessly both online and offline.
  - https://github.com/powersync-ja/powersync-js /apache2/202501/ts
    - SDK that enables local-first and real-time reactive apps with embedded SQLite for JavaScript clients, including React Native and Web

- https://github.com/get-convex/convex-backend /2.5kStar/FSL-1.1-Apache-2.0/202502/rust/ts
  - https://docs.convex.dev/
  - The open-source reactive database for app developers
  - The self-hosted product includes most features of the cloud product, including the dashboard and CLI. 
    - Self-hosted Convex works well with a variety of tools including Neon, Fly.io, Vercel, Netlify, RDS, Sqlite, Postgres, and more.
  - https://x.com/jamesacowling/status/1890088514806772032
    - We just launched self-hosted @convex_dev _20250214
    - When people say they want open source they rarely mean they just want to read the source code. They mean they want unrestricted access, an active community, ease of use, and yes, often something for free.

- https://github.com/typeonce-dev/sync-engine-web /ISC/202503/ts
  - https://typeonce.dev/
  - A Sync Engine for the web: React (TanStack Router), Web Workers, Effect, Loro
  - A local-first, offline-capable web sync engine implementation with CRDT-based synchronization. The project provides a complete solution for data synchronization between multiple devices while maintaining data consistency and offline capabilities.
  - Local-First Architecture: Data is primarily stored and managed locally, with server acting as sync + backup
  - CRDT-Based Sync: Uses loro-crdt for conflict-free data synchronization
  - Secure Authentication: JWT-based auth with master/access token system
  - This is a functional implementation of a web sync engine, optimized for single-user scenarios (not real-time collaboration). 
    - The focus is on providing reliable data synchronization while maintaining offline capabilities.

- https://github.com/anyproto/any-sync /MIT/202506/go
  - Any-Sync is an open-source protocol that enables local first communication and collaboration based on CRDTs.
  - It is focused on bringing high-performance communication and collaboration at scale
  - Any-Sync allows users to sync data via local WiFi networks. 
  - Any-Sync uses end-to-end encryption so that backup nodes store encrypted data that they cannot read. Creators control encryption keys; there is no central registry of users
  - Simultaneous support of p2p and remote communication

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

- https://github.com/drifting-in-space/driftdb /MIT/rust/ts
  - https://driftdb.com/
  - A real-time data backend for browser-based applications.
  - core Rust driftdb implementation.

- https://github.com/gardencmp/jazz /MIT/202311/ts
  - https://jazz.tools/
  - open-source toolkit for building apps with secure sync.
  - File upload and real-time media streaming
  - Set fine-grained, role-based permissions in Groups that are synced along with your data
  - Permissions verifiably enforced everywhere, using encryption & signatures under the hood.
  - Change roles dynamically for evolving teams, expiring invite links and more.

- https://github.com/serenity-kit/secsync /ts
  - https://www.secsync.com/
  - Is an architecture to relay end-to-end encrypted CRDTs over a central service.
  - eg: End-to-end encrypted document using Yjs incl. Cursor Awareness
  - eg: End-to-end encrypted todo list using Automerge
  - Why use a central relay service?
    - The main reason is to exchange data asynchronously.

- https://github.com/deepstreamIO/deepstream.io /MIT/202403/ts
  - https://deepstreamio.github.io/
  - open source server inspired by concepts behind financial trading technology. 
  - It allows clients and backend services to sync data, send messages and make rpcs at very high speed and scale.
  - Deepstream and Socket.io actually both use engine.io for browser communication
  - The server itself is configurable and uses permission files to validate incoming messages, but doesn’t hold any custom logic other than that. 
  - It is not an HTTP server, so won’t be able to serve images, HTML or CSS files. 
  - [Show HN: Deepstream.io – open-source real-time server with pub/sub and data sync | Hacker News_201602](https://news.ycombinator.com/item?id=11071916)
  - What is the algorithm used for JSON synchronization? Operational Transformation, CRDT, diff/patch?
    - Currently if a conflict occurs it’s reported back to the client that triggered it and its up to it to resolve it. We are currently working on configurable merge strategies on a per record level
    - for most use cases, newest update wins is sufficient if it can be done on a fine granular basis (one property of an object/document). It's what web applications have been doing for forever and being a 'realtime' framework doesn't change this if your use case isn't something like google docs.
  - Is this similar to firebase
    - Yes, but there are a number of core differences
    - Deepstream.io is a free open source server, not a PaaS offering
    - Deepstream offers pub-sub, request-response and web-rtc call management in addition to data-sync
    - Firebase’s data-sync approach is based on one large chunk of JSON data that allows you to observe and manipulate sub-paths. Deepstream does the same, but breaks the data down into individual units, called records
    - Deepstream uses a functional permissioning model, allowing you to interface with other systems (data-bases / active directory) for user-management, as opposed to firebase’ configuration based permissioning approach

- https://github.com/peers/peerjs /202303/ts
  - PeerJS provides a complete, configurable, and easy-to-use peer-to-peer API built on top of WebRTC, supporting both data channels and media streams.

- https://github.com/holochain/holochain /CAL/202212/rust
  - https://developer.holochain.org/
  - Holochain is a framework for building peer-to-peer distributed applications, also known as hApps. 
  - It emphasizes agent-centric architecture, intrinsic data integrity, and scalability. 
  - Holochain enables developers to build applications that run on just the devices of the participants without relying on centralized servers or blockchain tokens and it provides a robust and efficient means of managing data.
  - This repository contains the Holochain core libraries, not the runtime intended for end-users of Holochain applications.

- https://github.com/saarw/flushout /201910/ts
  - 💡 a distributed data model based on event sourcing. 
  - Collaborative applications use it for clients that need responsive interaction without network delay, or need to function offline.
  - Clients interact with a local proxy of a remote master model without accessing the network. They can then periodically flush changes from the proxy to the master in the background when the network is available.
  - [Building a collaborative React app with Flushout_202003](https://saarw.github.io/dev/2020/03/02/building-a-collaborative-react-app-with-flushout.html)

- https://github.com/ar-nelson/osmosis-js /202103/ts
  - An in-process JSON database with automatic peer-to-peer background synchronization between devices on a local network. Keep your apps in sync without a cloud!
  - 传输层使用jsonrpc
  - Osmosis synchronization is automatic, encrypted, and relatively safe from conflicts. 
  - Updates are modeled with a JSON CRDT.
  - Osmosis uses two kinds of sockets: broadcast UDP sockets that send heartbeat packets, and unicast TCP sockets that send Monocypher-encrypted, zstandard-compressed JSON-RPC messages.

- https://github.com/JacobJaffe/event-system-prototype
  - Prototype of a syncing game state between a p2p, host switching network through an action system & event history.

- https://github.com/spreadjs/spread /js
  - a local JavaScript datastructure, that is instantly synced across devices/nodes/instances
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

- https://github.com/primus/primus /MIT/202311/js
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

- https://github.com/hyperhyperspace/hyperhyperspace-core /MIT/ts
  - https://www.hyperhyperspace.org/
  - A library to create p2p applications, using the browser as a full peer.
  - An offline-first shared data library for creating p2p apps that work in the browser (and now also NodeJs).
  - HHS uses an immutable typed-objects local storage model. 
    - Objects are both retrieved and cross-referenced using a structural hash of their contents as their id (a form of content-based addressing).
  - Mutability is implemented using CRDTs. Identities and data authentication are cryptographic.
  - Objects and their references form an immutable DAG, a fact that is used for data replication in HHS p2p mesh.

- https://github.com/karyons/karyon /GPLv3/202312/rust
  - An infrastructure for peer-to-peer, decentralized, and collaborative software.
  - karyon jsonrpc: A fast and small async JSONRPC2.0 implementation.
  - karyon crdt: A CRDT implementation for building collaborative software.
  - karyon base: A lightweight, extensible database that operates with karyon crdt.
  - Big thanks to Ink & Switch team, smol async runtime, and zmq.rs for the inspiration!.

- https://github.com/feathersjs-ecosystem/feathers-sync /MIT/202305/js/inactive
  - Synchronize service events between Feathers application instances
  - When running multiple instances of your Feathers application (e.g. on several Heroku Dynos), service events (created, updated, patched, removed and any custom defined events) do not get propagated to other instances.
  - feathers-sync uses a messaging mechanism to propagate all events to all application instances. 
  - It currently supports redis, amqp/RabbitMQ
  - This allows to scale real-time websocket connections to any number of clients.

- https://github.com/yomorun/presencejs
  - a JavaScript library that allows you to build real-time web applications . 
  - The server is built on top of YoMo(go)
  - Fallback to WebSocket if WebTransport connection cannot be established

- https://github.com/CoCreate-app/CoCreate-cursors
  - https://cocreate.app/docs/cursors
  - Collaborative user cursor position for inputs, textarea's and contenteditable elements.

- https://github.com/ssbc/secret-stack /js
  - create secure peer to peer networks using secret-handshakes.
  - This provides a framework to make building secure, decentralized systems easier. such as ssb-server which this was refactored out of
  - https://github.com/ssbc/ssb-db2 /js
    - a new database for secure-scuttlebutt, it is meant as a replacement for ssb-db
    - Run in the browser via ssb-browser-core
  - https://github.com/ssbc/ssb-db /js/flumedb团队
    - ssb-db provides tools for dealing with unforgeable append-only message feeds.
    - secret-stack plugin which provides storing of valid secure-scuttlebutt messages in an append-only log.
  - https://github.com/staltz/ppppp-db /js
    - It's a secret-stack plugin much like ssb-db2. 
    - Other than that, you can also use the feed format
  - https://github.com/arj03/ssb-browser-core
    - Run Secure Scuttlebutt (similar to ssb-server) in a browser
    - SSB browser core is a full implementation of SSB running in the browser only (but not limited to, of course). 
    - Your feed key is stored in the browser together with the log, indexes and smaller images. 
    - Wasm is used for crypto and is around 90% the speed of the C implementation. 
    - A WebSocket is used to connect to pubs or rooms

- https://github.com/BetterTyped/hyper-fetch /apache2/202310/ts
  - https://hyperfetch.bettertyped.com/
  - fetching and realtime data-exchange framework meticulously crafted to prioritize simplicity and efficiency.
  - Next-generation features streamlines architecture creation, grants access to the request lifecycle

- https://github.com/cefjoeii/mern-crud /MIT/202311/js
  - A simple records system using MongoDB, Express.js, React.js, and Node.js with real-time Create, Read, Update, and Delete operations using Socket.io.
  - Semantic UI React was used for the UI in the front-end.

- https://github.com/realtimecms/realtime-cms /BSD/202001/js
  - Core project for realtime cms - server-side framework for real-time applications
  - https://github.com/realtimecms/users-service

- https://github.com/peer/db /apache2/202311/go
  - https://gitlab.com/peerdb/peerdb
  - A collaborative database
  - PeerDB requires an ElasticSearch instance. ElasticSearch instance needs to have an index with documents in PeerDB schema and configured with PeerDB mapping.
  - Power of PeerDB Search comes from having data in ElasticSearch index organized into documents in PeerDB schema.

- https://github.com/dmotz/trystero /MIT/202404/js/WebRTC
  - https://oxism.com/trystero
  - Build instant multiplayer webapps, no server required — Magic WebRTC matchmaking over BitTorrent, Nostr, MQTT, IPFS, and Firebase
  - Trystero manages a clandestine courier network that lets your application's users talk directly with one another, encrypted and without a server middleman.
  - Peers can connect via BitTorrent, Nostr, MQTT, Firebase, or IPFS – all using the same API.
  - Besides making peer matching automatic, Trystero offers some nice abstractions on top of WebRTC:
    - Rooms / broadcasting
    - Automatic chunking and throttling of large data
    - Session data encryption
  - To establish a direct peer-to-peer connection with WebRTC, a signalling channel is needed to exchange peer information (SDP). 
    - Typically this involves running your own matchmaking server but Trystero abstracts this away for you and offers multiple "serverless" strategies for connecting peers (currently BitTorrent, Nostr, MQTT, Firebase, and IPFS).
    - Beyond peer discovery, your app's data never touches the strategy medium and is sent directly peer-to-peer and end-to-end encrypted between users.
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

- https://github.com/frameable/pigeon /MIT/202212/js/inactive
  - https://github.com/frameable/pigeon/wiki/Benchmarks
  - Diff, patch, merge, and synchronize JSON documents with an Automerge-compatible interface
  - While Automerge optimizes for working offline and merging changes periodically, Pigeon is optimized for online real-time collaboration.
  - Change sets use JSON-Patch-esque paths, and so are more easily introspectable using existing tools
  - By default, history will grow only to 1000 items in length, after which oldest entries will be jettisoned(抛扔, 扔弃)
  - Changes are computed across entire data structures, rather than tracing via proxies
  - Changes may be made in-place for situations where performance is critical
  - Documents need not have a direct common ancestor for patches from one to apply to another
  - Unix timestamps and client ids are used instead of vector clocks to ensure order and determinism
  - https://news.ycombinator.com/item?id=33865672
    - We have used Automerge a bunch, but found that there is a threshold where beyond a given document size, performance gets exponentially worse, until even trivial updates take many seconds' worth of CPU. That is often how it works when the document end state is exclusively the sum of all the edits that have ever happened
    - Our answer was to reimplement the Automerge API with different mechanics underneath that allows for a "snapshots + recent changes" paradigm, instead of "the doc is the sum of all changes". That way performance doesn't have to degrade over time as changes accumulate.

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

# decentralized/p2p

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
