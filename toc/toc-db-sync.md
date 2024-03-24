---
title: toc-db-sync
tags: [db, synchronization, toc]
created: 2022-11-25T15:41:22.619Z
modified: 2022-11-25T15:41:47.534Z
---

# toc-db-sync

# guide
- 协作需要考虑 同步 + 冲突处理

- 支持offline的架构
  - 还可以考虑使用多级缓存，不一定全量数据库，类似react-query + indexeddb
  - 参考sqlite+http-range的部分下载示例(sql.js-httpvfs)

- sync-protocols
  - sync/collab/local-first
  - 是否支持切换存储层
  - 是否支持冲突处理
  - database realtime
  - minimongo/meteor 的replication协议参考 [meteor: Distributed Data Protocol (DDP)](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)
  - pouchdb的同步协议参考 [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)
  - [remoteStorage Protocol](https://remotestorage.io/protocol/): defines a simple key/value store for apps to save and retrieve data
  - [Watermelon sync protocol](https://nozbe.github.io/WatermelonDB/Advanced/Sync.html)
  - firebase-like: supabase
  - [rxdb alternatives](https://rxdb.info/alternatives.html)
  - [Automerge CRDT Sync Protocol](https://automerge.org/docs/how-it-works/sync/)

- [Comparison of Offline Sync Protocols and Implementations](https://offlinefirst.org/sync/)
  - couchdb/realm/firebase
# collab/distributed
- https://github.com/okdistribute/piratedb /js/inactive
  - A multiwriter peer-to-peer database with a last-writer-wins CRDT.
  - 依赖subleveldown、unordered-materialized-kv、randombytes
  - 测试用例使用kappa-core、memdb、random-access-memory

- orbit-db /7.4kStar/MIT/202301/js
  - https://github.com/orbitdb/orbit-db
  - OrbitDB is a serverless, distributed, peer-to-peer database. 
  - OrbitDB uses IPFS as its data storage and IPFS Pubsub to automatically sync databases with peers. 
  - It's an eventually consistent database that uses CRDTs for conflict-free database merges making OrbitDB an excellent choice for decentralized apps (dApps), blockchain applications and local-first web applications.
- https://github.com/dappkit/aviondb /MIT/202010/ts
  - A Distributed, MongoDB-like Database
  - AvionDB uses OrbitDB stores to model MongoDB-like Databases.

- dagdb /133Star/MIT/202010/js/leveldb/git/inactive
  - https://github.com/mikeal/dagdb
  - DagDB is a portable and syncable database for the Web.
  - It can run as a distributed database in Node.js, including using AWS services as a backend.
  - It also runs in the browser. 
  - 依赖@ipld/block、@ipld/fbl、datastore-car、levelup4
  - In fact, there is no "client and server" in DagDB, everything is just a DagDB database replicating from another database. 
    - In this way, it's closer to git than a traditional database workflow.
  - The closest thing to DagDB replication you're familiar with is git. 
    - The way changes are merged from one branch to another and from one remote to another. 
    - We even have a system for keeping track of remote databases that feels a lot like git.
    - if you have two database instances locally you can easily merge one into the other without using the remote system.
  - DagDB's primary storage system is a simple key-value store. 
    - Keys can be any string, and values can be almost anything.
  - DagDB uses a technique called "content addressing" that links data by hashing the value. 
    - This means that, even if you create the link again with the same data, the link will be the same and the data will be deduplicated.
  - Since it is often problematic to store large amounts of binary as a single value, DagDB also natively supports storing streams of binary data.
    - DagDB treats any async generator as a binary stream. 
    - Node.js Streams are valid async generators so they work right away.

- https://github.com/unmeshjoshi/replicate /java
  - This is a basic framework for quickly building and testing replication algorithms. 
  - It doesn't require any additional setup (e.g., Docker) for setting up a cluster and allows writing simple JUnit tests for testing replication mechanisms. 
  - The framework was created to learn and teach various distributed system techniques, enabling the testing of working code while exploring distributed systems concepts

- https://github.com/superfly/corrosion /apache2/202310/rust
  - https://superfly.github.io/corrosion/
  - Gossip-based service discovery (and more) for large distributed systems.
  - We built Corrosion specifically for service discovery across a large global network, replacing Consul’s central state database with eventually consistent state distributed across our hosts.
  - Maintains a SQLite database on each node
  - Gossips local changes throughout the cluster
  - Uses CR-SQLite for conflict resolution with CRDTs
  - Uses Foca to manage cluster membership using a SWIM protocol
  - Periodically synchronizes with a subset of other cluster nodes, to ensure consistency

- https://github.com/drifting-in-space/driftdb /ts/rust
  - https://driftdb.com/
  - A real-time data backend for browser-based applications.
  - core Rust driftdb implementation.

- debe /35Star/MIT/201907/ts/inactive
  - https://github.com/bkniffler/debe
  - 依赖automerge(delta)
  - offline-first Javascript datastore for browsers, node, electron and react-native with focus on performance and simplicity. 
  - Debe is currently not supporting relations, and probably never really will.
  - Includes support for concurrent multi-master/client database replication via plugin.
  - Rich querying using SQL-alike syntax
  - Automatic conflict resolution (CRDT)
  - Undo/Redo capabilities
  - PouchDB/RxDB are great and very mature solutions for replicating databases, but being forced to build your services on top of CouchDB can be unfitting for some users. 
  - Debe, and having the whole data flow in Javascript, offers some cool possibilities to control data access and filter & transform incoming/outgoing data according to user permissions. This works through middlewares.
  - https://github.com/bkniffler/workerdb /201901/ts
    - offline-first, syncable Database in WebWorker based on PouchDB/RxDB
# db-sync
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
  - 🤔 [What makes synceddb a good offline-first database?_201801](https://github.com/paldepind/synceddb/issues/47)
    - One of the distinguishing features of SyncedDB is that it attempts to be a very lightweight wrapper around IndexedDB. 
    - It's essentially IndexedDB + migrations + promises + syncing.

- sync_server-nedb /33Star/MIT/201807/js/nedb
  - https://github.com/nponiros/sync_server
  - A simple server which can be used to synchronize data from multiple devices
  - A small node server which uses NeDB to write data to the disk. 
    - The database used to store the data. Currently only NeDB is supported
  - The server can be used with a client for example `SyncClient` to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the `ISyncProtocol` and `Dexie.Syncable`. 
    - 👉🏻 It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
  - The server supports 4 different protocols: http, https, ws and wss
  - [Syncable: possible collaboration · dexie/Dexie.js](https://github.com/dexie/Dexie.js/issues/397)
- sync_client-dexie /29Star/MIT/201804/js
  - https://github.com/nponiros/sync_client
  - This module can be used to write data to IndexedDB using `Dexie` and to synchronize the data in IndexedDB with a server.
  - `Dexie.Syncable` is used for the synchronization. This module contains an implementation of the `ISyncProtocol`. 
  - It was primarily written to work with `sync-server` but should work with other servers which offer the same API.

- https://github.com/leapfrogtechnology/sync-db /MIT/202306/ts/inactive
  - Command line utility to synchronize and version control relational database objects across databases.
  - This utility uses Knex under the hood

- turtleDB-indexeddb /443Star/MIT/201809/js/代码量少
  - https://github.com/turtle-DB/turtleDB
  - https://turtle-db.github.io/
  - turtleDB is a JavaScript framework and in-browser database for developers to build offline-first, collaborative web applications. 
  - It provides a developer-friendly API to access an in-browser database built on top of IndexedDB.
  - It comes with built in document versioning and automatic server synchronization when paired with our back-end package tortoiseDB
  - Document versioning and developer-controlled conflict resolution
  - Synchronization with tortoiseDB and a MongoDB back-end
  - `db.setConflictWinner(doc: object)` 处理冲突
    - Takes a document that has conflicting versions and deletes all the other versions, making the version passed in the default winner.
- https://github.com/turtle-DB/tortoiseDB /mongodb
  - Enables offline-first applications built with turtleDB to be fully collaborative with automated document versioning, history merging, and synchronization management.
  - Built using Express and Mongo DB Native NodeJS Driver.

- Nano-SQL /773Star/MIT/201911/ts/inactive/未实现同步
  - https://github.com/only-cliches/Nano-SQL
  - https://nanosql.io/
  - 依赖snap-db(kv)
  - Universal database layer for the client, server & mobile devices. It's like Lego for databases.
  - Graph, Join, Filter, Select and Order your data in dozens of ways.
  - NanoSQL supports a wide range of ways to save your data in the browser, on the phone, and on the server.
    - Memory (Browser/NodeJS/Electron) 
    - Snap DB (NodeJS/Electron; LSM Powered Javascript key-value store) 
    - Indexed DB (Browser) 
    - Local Storage (Browser)
  - [Offline use with Sync to Server](https://github.com/only-cliches/Nano-SQL/issues/18)
  - [Is this project still maintained?](https://github.com/only-cliches/Nano-SQL/issues/217)
    - https://github.com/only-cliches/snap-db  /inactive

- clientdb /506Star/apache2/202207/ts/同步未完成
  - https://github.com/clientdb/clientdb
  - ClientDB is an in-memory database for enabling real-time web apps.
  - The architecture of clientdb is inspired by the Linear app
  - 依赖flexsearch、knex、express、socket.io、lodash
  - [sync-engine work in progress](https://github.com/clientdb/clientdb/pull/10)
  - [differences and advantages compared to RxDB](https://github.com/clientdb/clientdb/issues/12)

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
  - https://twitter.com/JFriedensreich/status/1596884820352798725
    - the problem with @remotestorage_ is that the storage model fits 
      - neither the couchdb/json document well where you want a flat bucket with arbitrary sorted indexes 
      - nor the file/blob where you want a DAG of content addressed storage like ipfs.

- orbit /2.3kStar/MIT/202209/ts/概念特别多
  - https://github.com/orbitjs/orbit
  - Orbit is a composable data framework for managing the complex needs of today's web applications.
  - Although Orbit is primarily used as a flexible client-side ORM, it can also be used server-side in Node.js.
  - Interact with data from a variety of sources: a REST server, a WebSocket stream, an IndexedDB backup, an in-memory store, etc.
  - Work offline, work online, and seamlessly transition between both modes.
  - Track changes deterministically.
  - Support undo/redo
  - Data in a source can be updated by applying a transform, which consists of one or more operations. 
    - Transforms must be applied atomically—all operations succeed or fail together.
  - Every time a source is transformed, it emits a transform event
    - every change to the in-memory source will be sync'd with the backup IndexedDB source. 

- kinto /4.2kStar/apache2/202210/python
  - https://github.com/Kinto/kinto
  - http://docs.kinto-storage.org/
  - A generic JSON document store with sharing and synchronisation capabilities.
  - Backends: In-memory (development), PostgreSQL 9.5+ (production)
  - [How does Kinto compare to other solutions?](https://docs.kinto-storage.org/en/stable/faq.html)
    - 比较了parse、firebase、couchdb、kuzzle、remoteStorage、Hoodie
  - https://github.com/Kinto/kinto.js
    - An Offline-First JavaScript client for Kinto.

- https://github.com/endpointservices/mps3 /202311/ts
  - Vendorless Multiplayer Database over any s3-compatible storage API
  - MPS3 is a key-value document store. A manifest lists all keys in the DB as references to files hosted on s3.
  - Setting a key first writes the content to storage, then updates the manifest. 
  - To enable subscriptions, the client polls the manifest for changes. 
  - To enable causally consistent concurrent writes, the manifest is represented as a time indexed log of patches and checkpoints which is resolved on read.
  - sync protocol is causally consistent under concurrent writes.
  - Offline-first, fast page loads and no lost writes.
  - Tested with S3, Backblaze, R2 and self-hosted solutions like Minio.
  - [sync protocol of MPS3](https://github.com/endpointservices/mps3/blob/main/docs/sync_protocol.md)
    - MPS3 is a Key-Value store. The values are stored in versioned storage locations on S3. There is a layer of indirection that maps DB logical keys to storage locations hosted in a manifest
    - To enable consistent atomic updates of multiple keys, first the client writes the new values, and then it updates the manifest, not dissimilar to write-ahead-logging. Other clients use the manifest to access the DB
    - client sends the operation as a JSON_merge_patch. 
    - it is inefficient for a client to replay the entire DB history.
    - A client only needs to read an imperfect guess of the latest state, then replay all patches within a lag window to correct an estimate of the final state
    - Large clock skew is detected by MPS3 by comparing the manifest key timestamp against the server-provided `LastModified` time.
    - The algorithm is deceptively(欺骗性的；造成假象的) simple in implementation but leans heavily on the algebraic property of JSON-merge-patch and wiggle(扭动; 摆动) room in causal consistency to accommodate client-side clock_skew. 
    - The same algorithm is used also to synchronize state transfer between tabs in the local-first setting. 
# sync-utils
- https://github.com/sueddeutsche/json-sync /201803/js
  - Enables real-time collaborative editing of arbitrary JSON objects
  - Client and Server are syncing with the Differential Synchronization algorithm
  - The client fetches the initial state of the data and enters a sync-room via WebSockets
  - Every change of this state is synced via the sync method
  - Clients receive events about changes from the server which are automatically applied to a shared object (in-place)
  - The server takes care of syncing the state of all connected clients
  - https://github.com/janmonschke/diffsync /MIT/201505/js

- https://github.com/syncthing/syncthing /MPLv2/202312/go
  - https://forum.syncthing.net/
  - Open Source Continuous File Synchronization. It synchronizes files between two or more computers. 
  - We take every reasonable precaution to avoid corrupting the user's files.
  - [Partially sync · syncthing/syncthing](https://github.com/syncthing/syncthing/issues/7349)
    - There's ignore patterns: docs.syncthing.net/users/ignoring.html
    - IMO there's a fundamental disagreement on how "partial sync" (or "selective sync") should work. for me, it should work exactly how you outlined it. 
    - I guess better said: for anybody that has used dropbox selective sync OR resilio selective sync, I would dare say is really obvious that ignore patterns is NOT the solution to this problem

- https://github.com/abrarsheikhsony/SFDC-change-data-capture
  - explains specifically for Change Data Capture (CDC)
  - https://github.com/abrarsheikhsony/SFDC-streaming-api-events

- https://github.com/debezium/debezium /java
  - https://debezium.io/
  - provides a low latency data streaming platform for change data capture (CDC). 
  - You set up and configure Debezium to monitor your databases, and then your applications consume events for each row-level change made to the database. 
  - Only committed changes are visible
  - since Debezium records the history of data changes in durable, replicated logs, your application can be stopped and restarted at any time, and it will be able to consume all of the events it missed while it was not running
  - Monitoring databases and being notified when data changes has always been complicated. 
    - Relational database triggers can be useful, but are specific to each database
    - Debezium provides modules that do this work for you. 
    - Some modules are generic and work with multiple database management systems
    - Other modules are tailored for specific database management systems

- https://github.com/linkedin/databus /java/inactive
  - https://github.com/linkedin/databus

- https://github.com/speculare-cloud/speculare-pgcdc /rust
  -  allows you to listen to changes in your PostgreSQL database via logical replication and then broadcast those changes over websockets.

- https://github.com/canertosuner/postgresql-change-data-capture-using-debezium
  - PostgreSQL Change Data Capture (CDC) Using Debezium

- https://github.com/siliconjungle/tick-network-server
  - An example of a server that sends messages at a regular interval.
  - 依赖express、ws、messagepack
  - https://github.com/siliconjungle/tick-network-client
    - A demo of a client that sends messages at a regular interval.

- https://github.com/NangoHQ/nango /202212/ts
  - https://www.nango.dev/
  - Nango continuously syncs data from any API endpoint (that returns JSON) to your database.
  - Nango has built-in support for OAuth through our sister project Pizzly

- https://github.com/urish/firebase-server /201910/ts/archived
  - Firebase Web Socket Protocol Server. Useful for emulating the Firebase server in tests.
  - As of May 2019 there are officially supported emulators for many Firebase services, removing the need for a third-party solution like firebase-server.

- https://github.com/forbesmyester/SyncIt /201409/js
  - SyncIt is a library to enable you to easily add synchronization to your (normal) live or offline (Cordova / Ionic / Phonegap / HTML5 / Other) web Apps. 
  - Tracking versions of data.
  - Knowing which data is on the server.
  - Keeping a list of data which still needs to be sent to the server.
  - Supplying the App with all data required to handle version conflicts when they occur.

- https://github.com/ankane/pgsync /202312/ruby
  - Sync data from one Postgres database to another (like pg_dump/pg_restore).
  - tables are transferred in parallel
  - sync partial tables, groups of tables, and related records

- https://github.com/powersync-ja/powersync-web-sdk /ts
  - This monorepo contains the packages for PowerSync's Web SDK.
  - [I saw some mentions that the powersync is going to become fully open-source solution with self-hosting option. Do you have any ETA for that?_20231123](https://discord.com/channels/1138230179878154300/1138230180813479968/1177079452426051614)
    - It will happen next year though.What I can say is that we are busy working on figuring it out, so if you ask me again in 1 month

- https://github.com/vmware/node-replication /MIT/202212/rust/inactive
  - An operation-log based approach for data replication.
  - implement concurrent and replicated versions of (single-threaded) data structures by combining ap set of different concurrency techniques: flat combining, operation logging, readers-writer locks, and partitioning.
# partial-sync/replication
- https://github.com/pietgeursen/bamboo-rs /202108/rust
  - Rust implementation of bamboo
  - bamboo-rs aspires to be portable, fast and correct.
  - Bamboo supports partial replication of logs, it is possible to request only a subset of a log while still being able to verify the data.
  - this log format can serve as a more efficient alternative to secure-scuttlebutt's linked lists or hypercore's merkle forests.
  - https://github.com/AljoschaMeyer/bamboo /blog
    - A cryptographically secure, distributed, single-writer append-only log that supports transitive partial replication and local deletion of data.

- https://github.com/arj03/ssb-partial-replication /202003/js
  - A collection of functions useful for replicating a part of the log instead of everything. 
  - This is superseeded by SSB secure partial replication.
  - https://github.com/arj03/ssb-secure-partial-feed

- https://github.com/ssbc/ssb-replication-scheduler /LGPLv3/202305/js
  - Plugin to trigger replication of feeds identified as friendly in the social graph
  - 依赖ssb-db2
  - [RequestManager for partial replication 已实现并合并](https://github.com/ssbc/ssb-replication-scheduler/pull/5)

- https://github.com/nichoth/eventual-gram-ssb-old /202102/js/inactive
  - A social app designed for sharing photographs. Heavily influenced by patchwork, but with a UI designed for photos
  - uses preact as the view layer
  - The only thing left for easier onboarding was partial replication so I implemented the current version to see two browsers syncing like this
  - I'm currently working on a better design for partial replication so this is mostly a tech demo.

- https://github.com/ryanpbrewster/jump-sync /202102/ts
  - Partial incremental sync with "jump-ahead" support

- https://github.com/PeerDB-io/peerdb /1.3kStar/Elastic/202312/rust/go/ts
  - https://peerdb.io/
  - Postgres first ETL/ELT, enabling 10x faster data movement in and out of Postgres
  - [Launch HN: PeerDB (YC S23) – Fast, Native ETL/ELT for Postgres | Hacker News_202307](https://news.ycombinator.com/item?id=36895220)
    - support multiple features including log-based (CDC) / query based streaming, efficient syncing of tables with large (TOAST) columns, configurable batching and parallelism to prevent OOMs and crashes etc

- https://github.com/itzdarsh/prepl /202209/python
  - MongoDB partial replication with selective database/collection with the help of change stream.
  - [MongoDB & Partial Replication_202209](https://www.linkedin.com/pulse/mongodb-partial-replication-darshan-jayarama)
    - MongoDB change stream allows you to replicate part of your data with the very minimal coding.
    - it uses the change stream to replicate the data from source cluster to target cluster. If you’re using MongoDB 3.6 or later, change streams are already built in
    - Apart from partial replication, change stream can also be used to create the triggers in which when a specified action is performed we can trigger the counter action as desired.

- https://github.com/cosmoss-jigu/hydralist /202011/cpp
  - A Scalable In-Memory Index Using Asynchronous Updates and Partial Replication
- https://github.com/epfl-labos/paris /202007/cpp/inactive
  - Causally Consistent Transactions with Non-blocking Reads and Partial Replication
  - PaRiS(Partially Replicated System) is the first transactional causally consistent system that supports partial replication and implements non-blocking parallel read operations. 

- https://github.com/earthstar-project/earthstar /LGPLv3/ts
  - Storage for private, distributed, offline-first applications.
  - Earthstar is an offline-first key-value database which supports author versions.
  - Earthstar is a key-value database. It has fewer guarantees than Kappa-db and more flexibility. You can hold any subset of the documents, sync them in any order, do partial sync, drop ones you don't want.
  - [Comparison to GUN?](https://github.com/earthstar-project/earthstar/discussions/230)
    - Designed to allow partial sync of the data, but not quite implemented yet_202101

- https://github.com/willyrgf/pg-syncer /202011/go/inactive
  - a query-based syncer between PostgreSQL databases.
  - partialsync have not yet been implemented

- https://github.com/viant/dbsync /202210/go/inactive
  - SQL based cross database cost effective synchronization
  - data synchronization between various database and cloud vendor becomes more and more frequent task. 
  - This project provides SQL based cross database vendor data synchronization for small and large(billions+ records) tables/views in a cost effective way.
  - This is achieved by both determining the smallest changed dataset and by dividing transferable dataset in the partitioned/chunked segments. Both read and writes can be easily parallelized.
  - Chunk synchronization uses ID based range to divide a dataset into a smaller segments. 
  - Query based synchronization: In some cases view or actual SQL can be source for data sync, in that scenario SQL can be used as source.
  - Query based sync: In some cases view or actual SQL can be source for data sync, in that scenario SQL can be used as source.
# raft
- https://github.com/pgte/skiff-algorithm /201410/js
  - Raft implementation in Node.js
  - Persists to LevelDB (or any database exposing a LevelDown interface).
  - Exposes the cluster as a Levelup or Leveldown-compatible interface, with which you can extend using the Levelup plugins.
  - Encodes messages using Msgpack

- https://github.com/datafuselabs/openraft /MIT/rust
  - rust raft with improvements

- https://github.com/eatonphil/raft-rs /202312/rust
  - Another minimal Raft implementation in Rust.
  - you don't learn a concept well until you've implemented it a few times
- https://github.com/eatonphil/goraft /202305/go
  - A basic Raft implementation in Go.
  - [Implementing the Raft distributed consensus protocol in Go](https://notes.eatonphil.com/2023-05-25-raft.html)

- https://github.com/vaibhawvipul/minimal-raft /rust
  - a minimalistic implementation of RAFT algorithm

- https://github.com/andreev-io/little-raft /MIT/202209/rust/inactive
  - The lightest distributed consensus library. Run your own replicated state machine

- https://github.com/hashicorp/raft /MPLv2/202401/go
  - Golang implementation of the Raft consensus protocol
  - a Go library that manages a replicated log and can be used with an FSM to manage replicated state machines. It is a library for providing consensus.

- https://github.com/drmingdrmer/one_file_raft /202401/rust/单文件
  - This is a concise, demonstrative implementation of the Raft consensus algorithm contained within a single Rust file, approximately 300 lines in length.
  - 288行了, 要实现joint有点不够了

- https://github.com/noghartt/paxos-from-scratch /202402/rust
  - An implementation of simple Paxos consensus algorithm written from scratch with Rust.
  - Single-decree(判决，裁定) Paxos Consensus Algorithm written from scratch
# more
- https://github.com/rethinkdb/rethinkdb /202211/cpp/python
  - The open-source database for the realtime web.
  - NoSQL database that stores schemaless JSON documents
- https://github.com/rethinkdb/horizon
  - Horizon is an open-source developer platform for building sophisticated realtime apps. 
  - Horizon is built on top of RethinkDB and consists of four components

- https://github.com/hypercore-protocol/hypercore /202211/js
  - a secure, distributed append-only log.
  - Built for sharing large datasets and streams of real time data
  - [hypercore and Yjs : how to make them work together](https://github.com/hypercore-protocol/hypercore/issues/296)
    - the y-dat implementation does not actually use the core feature of the hypercore’s append only merkle tree signed log, due to the mutable nature of the Yjs CRDT implementation.

- https://github.com/libp2p/js-libp2p
  - The JavaScript Implementation of libp2p networking stack.

- https://github.com/SyncProxy/sync-client /202012/js/inactive/服务端未开源
  - SyncProxy-client is a javascript client for SyncProxy that enables one-single line of code implementation of synchronization for javascript offline applications using embedded database (IndexedDB, SQLite, SQLJS, WebSQL, LokiJS...).

- https://github.com/malerba118/react-use-database
  - This library is no longer maintained, please consider react-query and apollo-graphql as more robust solutions 
  - react-use-database gives you an opinionated interface, efficient data flow, and concise global state management. 
  - It forces you to think about your client-side data in the context of a queryable database. 
  - It gives you two global data stores: an entity store and a query store.
  - The entity store contains all of your model data. 
    - It’s just a big json blob that is the source of truth for any database entity that you have defined via Normalizr’s notion of schemas 

- https://github.com/digitallyinduced/thin-backend /202211/js/ts/inactive
  - a Blazing Fast, Universal Web App Backend for Making Realtime Single Page Apps
  - Thin Backend has a built-in GUI-based schema designer, helps to quickly build the DDL statements for your database schema
  - Thin Backend is built on top of the production-proven [IHP](https://github.com/digitallyinduced/ihp) architecture & libraries.
