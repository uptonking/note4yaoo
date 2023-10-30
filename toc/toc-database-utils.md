---
title: toc-database-utils
tags: [database, lib, utils]
created: 2023-08-23T17:15:09.363Z
modified: 2023-08-23T17:15:46.484Z
---

# toc-database-utils

# guide

- log-based-db
  - flume/ssb/hyperbee
  - event-sourcing
# hypercore
- https://github.com/holepunchto/hypercore /MIT/js
  - https://docs.holepunch.to/building-blocks/hypercore
  - Hypercore is a secure, distributed append-only log.
  - **Built for sharing large datasets and streams of real time data**
  - 依赖streamx、protomux、big-sparse-array、compact-encoding、events、flat-tree、fast-fifo、random-access-file
  - Modular. Hypercore aims to do one thing and one thing well - distributing a stream of data.
  - Sparse replication. Only download the data you are interested in.
  - Realtime. Get the latest updates to the log fast and securely.
  - Performant. Uses a simple flat file structure to maximize I/O performance.
  - Secure. Uses signed merkle trees to verify log integrity in real time.
  - Version 10 is not compatible with earlier versions (9 and earlier), but is considered LTS
    - v10 adds support for truncate and many other things
  - [Proposal integrate Query able append only log](https://github.com/holepunchto/hypercore/issues/312)
    - this data structure is called fleece, allows you to exchange less data and keep it query able while streaming 
    - it's the core of couchbase the fastest most complet database implementation that exists by the way using a lot of nice stuff. 
  - [Add custom storage](https://github.com/holepunchto/hypercore/pull/294)
    - This is a proof-of-concept to see whether Hypercore could support alternative storage to random-access-storage.
    - In 10, we have intermediaries for everything (ie a BlockStore stores the blocks), so can be abstracted easily now, if RAF is too low level for the usecase.
  - https://github.com/gmaclennan/hypercore-storage-level
    - Levelup storage for Hypercore

- https://github.com/datrs/hypercore-protocol-rs /rust
  - https://github.com/datrs/hypercore /rust
  - https://docs.rs/hypercore/latest/hypercore/
  - Rust implementation of Hypercore protocol
  - This crate provides a low-level streaming API to hypercore-protocol and exposes an interface that should make it easy to implement actual protocol logic on top. 
  - This crate targets Hypercore 9 (Dat 2) only.
    - For ongoing work to support the latest version 10 of hypercore see the v10 branch.
  - It uses `async-std` for async IO, and `snow` for the Noise handshake.

- https://github.com/holepunchto/hyperbee /js
  - https://docs.holepunch.to/building-blocks/hyperbee
  - An append-only B-tree running on a Hypercore. 
  - It provides a key/value-store API, atomic batch insertions, and creating sorted iterators.
  - 依赖streamx、mutexify
  - Hyperbee is a key-value database that's built on top of hypercore. It works basically like leveldb but it's networked with a hyper:// address, so reads work remotely
  - It uses a single Hypercore for storage, using a technique called embedded indexing.
  - It provides features like cache warmup extension, efficient diffing, version control, sorted iteration, and sparse downloading.
  - As with the Hypercore, a Hyperbee can only have a single writer on a single machine
  - https://github.com/geut/hyperbee-live-stream
    - Creates a ReadableStream but keep watching for changes in the range defined

- https://github.com/holepunchto/hyperdrive /js
  - https://docs.holepunch.to/building-blocks/hyperdrive
  - a secure, real-time distributed file system designed for easy P2P file sharing.

- https://github.com/Telios-org/nebula /js
  - Real-time distributed storage for files and key value databases built on top of Hypercore Protocol
  - A lot of inspiration was taken from Hyperdrive, but Hyperdrive didn't have options for fine-grain access control, multiple writers, and the ability to delete files from disk once added to the drives.

- https://github.com/genderev/assassin /202009/js/inactive
  - Assassin is a decentralized database that uses background threads to kill slow JavaScript.
  - I ended up creating this database partly because IndexedDB is disabled in private browsing, which means none of these databases work for me.
  - Assassin is a key/value store that supports mapping a key to its corresponding value.
  - System Architecture: The DAT protocol distributes and hosts data between many computers, so there is no one location where data is stored. Assassin relies on the the DAT protocol for data persistence. The metadata of the key-value pairs are stored in a distributed `trie` structure.
  - Storage Model: Assassin sends data to the server, which then stores the metadata in the distributed file system Hyperdrive, which is built on the DAT protocol

- https://github.com/holepunchto/hyperblobs /js
  - A simple blob store for Hypercore.
  - Each blob is identified by its unique bounds within the Hypercore, which makes them easy to save and retrieve

- https://github.com/RangerMauve/hypercore-fetch /js
  - Implementation of Fetch that uses the Hyper SDK for loading p2p content

- https://github.com/tradle/multi-hyperbee /js
  - A LevelUP compatible leaderless multi-master database with eventual consistency, **using hyperbee + CRDT + HLC**. 
  - Similarly CockroachDB achieves replication on top of RocksDB, but here it is a pure P2P **streaming** database, with zero central management.
  - like all other low-level components of hypercore ecosystem it is a single-writer data structure. Multi-writer is a higher-level abstraction, hence the name multi-hyperbee.

- https://github.com/holepunchto/autobase
  - Autobase lets you write concise multiwriter data structures with Hypercore
  - https://github.com/lejeunerenard/autobase-event-bus

- https://github.com/dxos/feed-level-indexer
  - Index messages into a leveldb through multiple hypercore feeds.

- https://github.com/digidem/multi-core-indexer /js
  - You can use this module to index one or more hypercores
  - This module is useful if you want to create an index of items in multiple Hypercores. 
  - There is no guarantee of ordering, so the indexer needs to be able to index unordered data. 
  - Sparse hypercores are supported, and undownloaded entries in the hypercore will be indexed when they are downloaded.

- https://github.com/digidem/websocket-hypercore-replicator
  - Replicate a hypercore over a websocket

- https://github.com/rafapaezbas/hypercore-speed-tests
  - Test with Hypercore and Hyperbee

## examples-hypercore

- https://github.com/Ruulul/automerge_hypercore_demos /js
  - local_sync_textareas

- https://github.com/CodelyTV/p2p-editor /js/inactive
  - P2P Editor is a code editor that works in the browser which lets you share live coding sessions.
  - Code editor: Ace
  - Database: append only log (hypercore)
  - Communication: WebRTC RTCDataChannel (webrtc-swarm)
  - Peer discovery: WebRTC signaling server (signalhub)
  - Storage: RAM

- https://github.com/LuKks/hyperfind
  - Explore hypercores (quick demo)
  - https://github.com/LuKks/use-hyper
    - React hooks for the hypercore-protocol stack

## utils-hypercore

- https://github.com/RangerMauve/hyper-sdk /js
  - A Software Development Kit for the hypercore-protocol
  - Hypercore-protocol and it's ecosystem consists of a bunch of low level building blocks for working with data in distributed applications. Although this modularity makes it easy to mix and match pieces, it adds complexity when it comes to actually building something.
  - The Hyper SDK combines the lower level pieces of the Hyper stack into high level APIs that you can use across platforms 

- https://github.com/extendedmind/peermerge /rust
  - Peer protocol (hypercore or p2panda) + Automerge in Rust

- https://github.com/HDegroote/hypercore-rehost-server /js
  - Simple server to keep hypercores available.
  - A CLI to interact with this server is provided at hypercore-rehost-cli.

- https://github.com/fsteff/hyperobjects /ts
  - Simple object store with transaction support, built on hypercore.
  - concurrent, atomic transactions
  - internally uses an octree to store object-ID > hypercore index mappings

- https://github.com/emilbayes/hypercore-dag /js/inactive
  - DAGs on top of hypercore, allowing verified random-access to graph nodes

## dat-ecosystem

- refs-dat
  - [Dat Ecosystem](https://dat-ecosystem.org/)
  - https://dat-ecosystem-archive.github.io/how-dat-works/

- https://github.com/dat-ecosystem/dat /js
  - https://dat.foundation/
  - peer-to-peer sharing & live synchronization of files via command line
  - Use dat command line to share files with version control, back up data to servers, browse remote files on demand, and automate long-term data preservation
  - dat is the first application based upon the Hypercore Protocol, and drove the architectural design through iterative development between 2014 and 2017. T

- https://github.com/garbados/pouchdb-hypercore /js
  - Synchronize PouchDB or CouchDB with P2P Hypercores
  - A PouchDB plugin that maps records in hypercores, a P2P append-only datastructure, to a PouchDB or CouchDB instance. 
  - The plugin allows you to follow changes in hypercores locally and remotely.
# kappa-db
- https://github.com/kappa-db/kappa-core /ISC/202011/js/inactive
  - kappa-core is a minimal peer-to-peer database, based on append-only logs and materialized views.
  - kappa-core is built atop two major building blocks:
    - hypercore, which is used for (append-only) log storage; parts of logs can be selectively sync'd between peers
    - materialized views, which are built by traversing logs in potentially out-of-order sequence
  - kappa-core is built on an abstraction called a kappa architecture, or "event sourcing". 
    - This differs from the traditional approach to databases, which is centered on storing the latest value for each key in the database.
    - In contrast, **kappa architecture centers on a primitive called the "append-only log"** as its single source of truth.
    - Each entry in a log is addressable by its "sequence number" (starting at 0, then 1, 2, 3, ...). In the case of kappa-core, which uses hypercore underneath
  - kappa-core still uses tables like the above, though. 
    - However, instead of being the source of truth, these **tables are generated (or materialized) from the log data**, providing a view of the log data in a new or optimized context. 
    - These are called materialized views.
  - [Running kappa in the browser?](https://github.com/kappa-db/kappa-core/issues/25)
    - For regular Node use, people tend to use level and random-access-file for storage, and then maybe hyperswarm for network discovery.
    - check out random-access-storage/random-access-web and RangerMauve/hyperswarm-web. Level/browser-level supports browser use.
  - https://github.com/Frando/kappa-core /用于kappa-record-db
    - https://www.npmjs.com/package/@frando/kappa-core /v6

- https://github.com/kappa-db/workshop /js
  - https://kappa-db.github.io/workshop/build/01.html
  - let's learn how to write peer-to-peer applications in javascript!
  - A small series of workshops to introduce kappa architecture and how to build p2p programs with modules like hypercore, multifeed, and kappa-core.
  - https://github.com/aral/kappa-architecture-workshop-work-files
  - https://github.com/dwyl/learn-kappa-architecture
  - https://github.com/tradle/hypercore-workshop
    - we forked it to update to new materials and shift focus to core Hypercore modules.
  - https://github.com/hypercore-protocol/p2p-multiwriter-with-autobase
    - For this workshop we'll be focusing almost entirely on our newest feature: support for multiwriter collaboration.

- https://github.com/arso-project/kappa-record-db /202005/js/inactive
  - A peer-to-peer database built on hypercores and kappa-core@experimental.
  - Index a set of hypercores efficiently into materialized-view style secondary indexes
  - Is developed for Sonar which adds full-text search, binary assets, an HTTP API, a CLI and a UI.
  - Internally, the database uses unordered-materialized-kv to have a shared notion of the latest versions of a record.

- https://github.com/arso-project/sonar /GPLv3/js/ts
  - https://sonar.arso.xyz/
  - A p2p content database and search engine
  - Each collection has a kappa-record-db that's plugged into a search index through tantivy. 
  - Each collection has also a list of associated Hyperblobs to store raw file contents.
  - [Introducing Sonar_201912](https://arso.xyz/blog/2019-12-17-introducing-sonar)
  - [Full text search in Sonar](https://arso.xyz/blog/2020-04-24-full-text-search)

- https://github.com/arso-project/hyper-content-db /201912/js/inactive
  - A Kappa-style peer-to-peer content database, on top of hyperdrives.

- https://github.com/mafintosh/hyperdb /201901/js/inactive
  - HyperDB is a scalable peer-to-peer key-value database.
  - A HyperDB is fundamentally a set of hypercores.
  - The combination of all operations performed on a HyperDB by all of its members forms a DAG (directed acyclic graph). 
  - HyperDB builds an incremental index with every new key/value pairs ("nodes") written

- https://github.com/peermaps/kappa-sparse-query /js/inactive
  - architecture for sparse data flows over kappa-core driven by peer queries
  - eplicate feeds for kappa-core@experimental views using sparse queries

- https://github.com/kappa-db/multifeed /js
  - multi-writer hypercore
  - It solves the problem of hypercore only allowing one writer by making it easy to manage and sync a set of hypercores -- by a variety of authors -- across peers.
  - Replication works by extending the regular hypercore exchange mechanism to include a meta-exchange, where peers share information about the feeds they have locally, and choose which of the remote feeds they'd like to download in exchange. 
    - Right now, the replication mechanism defaults to sharing all local feeds and downloading all remote feeds.

- https://github.com/kappa-db/kappa-view-level /js
  - make kappa-core views over leveldb
  - This module handles view lifecycle logic for you: normally a kappa view needs to manage storing and fetching the state of the indexer ("up to what log sequence numbers have I processed?"), as well as purging the view's LevelDB database when the version of the view gets bumped.
  - inspired by https://github.com/flumedb/flumeview-level

- https://github.com/ssbc/ssb-server /js
  - https://ssbc.github.io/ssb-server/
  - ssb-server is an open source peer-to-peer log store used as a database, identity provider, and messaging system. 
  - ssb-server **behaves just like a Kappa Architecture DB**. 
  - ssb-servers comprise(包含；构成) a global gossip-protocol mesh without any host dependencies.

- https://github.com/okdistribute/peerfs /js
  - multiwriter peer-to-peer filesystem, built on kappa-core and hyperdrive

- https://gitlab.com/coboxcoop/kappa-drive
  - a peer-to-peer multiwriter filesystem.
  - Supports Hyperdrive V10. Originally known as 'peerfs'.
- https://gitlab.com/coboxcoop/drive
  - a wrapper for kappa-drive

- https://github.com/eliquious/kappa /go/inactive
  - an implementation of the Kappa Architecture written in Go.
  - https://github.com/blacklabeldata/kappa

- https://github.com/ouyi/kafka-flink-demo /java
  - A demo application implementing the Kappa architecture, based on Kafka, Flink, and ELK.

- https://github.com/hkwi/osara /python
  - micro-framework on top of kafka / kappa architecture

- [Kappa Architecture - Where Everything Is A Stream · java-design-patterns](https://github.com/iluwatar/java-design-patterns/issues/892)

- [kappa architecture vs event sourcing](https://github.com/tschudin/ssb-icn2019-paper/issues/6)

- [Kappa Architecture - A big data engineering approach](https://pradeepl.com/blog/kappa-architecture/)
# append-only-log
- resources
  - [History Data Structures](https://gist.github.com/CMCDragonkai/d266a3055735545447439f0fa662a0e1)

- https://github.com/ssbc/async-append-only-log /js
  - A new append-only-log for SSB purposes
  - This module is heavily inspired by flumelog-aligned-offset. It is an attempt to implement the same concept but in a simpler fashion
  - A log consists of a number of blocks, that contain a number of records. A record is simply it's length, as a 16-bit unsigned integer, followed by the data bytes. 
  - This module is not compatible with flume without a wrapper around stream as it uses the same terminology as JITDB and ssb-db2 of using offset for the byte position of a record instead of seq.
- https://github.com/ssbc/jitdb /js
  - A database on top of `async-append-only-log` with automatic index generation and maintenance.
  - Async append only log takes care of persistance of the main log. It is expected to use bipf to encode data.
  - JITDB lazily creates and maintains indexes based on the way the data is queried.
    - JITDB lazily creates and maintains indexes based on the way the data is queried.
    - Specific indexes will only updated when it is queried again. These indexes are tiny compared to normal flume indexes.
  - For this to be feasible it must be really fast to do a full log scan. 
    - It turns out that the combination of push streams and bipf makes streaming the full log not much slower than reading the file.

- https://github.com/ssbc/ssb-db2 /42Star/LGPLv3/202305/js
  - a new database for secure-scuttlebutt, it is meant as a replacement for ssb-db
  - 依赖async-append-only-log、bipf、jitdb、level6、flumecodec、jitdb、pull-stream、pull-stream、typedarray-to-buffer
  - Run in the browser via ssb-browser-core
  - the database stores data in bipf
  - Replace flume with jitdb and specialized indexes
  - Run in the browser via ssb-browser-core
  - Work well with partial replication
  - The log used underneath ssb-db2 is different than that one in ssb-db, this means we need to scan over the old log and copy all messages onto the new log
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

- https://github.com/orbitdb/ipfs-log /js
  - an immutable, operation-based CRDT for distributed systems. 
  - It's an append-only log that can be used to model a mutable, shared state between peers in p2p applications.
  - Every entry in the log is saved in IPFS and each points to a hash of previous entry(ies) forming a graph. Logs can be forked and joined back together.
  - originally created for, and currently used in, orbit-db 
  - https://github.com/berty/go-ipfs-log /go
    - provide a fully compatible port of the JavaScript version in Go.
    - Go version of append-only log CRDT on IPFS
  - https://github.com/eqlabs/ipfs-log-rs
    - Rust implementation of ipfs-log by Haja Networks: an append-only log on IPFS.
  - https://github.com/orbitdb/orbit-db-eventstore /js
    - An append-only log with traversable history. 
    - Useful for "latest N" use cases or as a message queue.
  - https://github.com/orbitdb/orbit-db-feedstore /js
    - A log database with traversable history. 
    - Entries can be added and removed. 
    - Useful for "shopping cart" type of use cases, or for example as a feed of blog posts or "tweets".

- https://github.com/digidem/unordered-materialized-kv /js/inactive/搜索依赖和示例
  - materialized view key/id store based on unordered log messages
  - This library presents a familiar key/value materialized view for append-only log data which can be inserted in any order. 
  - This library implements a **multi-register conflict strategy**, so each key may map to more than one value. 
    - To merge multiple values into a single value, point at more than one ancestor id.
  - This library is useful for kappa architectures with missing or out of order log entries, or where calculating a topological ordering would be expensive
  - This library does not store values itself, only the IDs to look up values. This way you can use an append-only log to store your primary values without duplicating data.
  - https://github.com/peermaps/unordered-materialized-kv-pubsub
    - extends the unordered-materialized-kv api with independent sessions that can open() and close() sets of keys
  - https://github.com/peermaps/unordered-materialized-kv-live

- https://github.com/flumedb/flumedb /MIT/202006/js/inactive
  - A modular database made for moving logs with streams.
  - ✨ Flume is a modular database comprised of an Append Only Log and Streaming Views on that log. 
  - This makes a star shaped pipeline - or rather, there is a pipeline from the log to each view, but the log is part of every pipeline.
  - https://github.com/sunrise-choir/flumedb-rs
    - a re-write of the JavaScript flumedb into Rust with a new architecture for better performance and flexibility.
    - main source of truth is an append-only write-only log: which provides durable storage
    - secondary derived truths are views on the log: which focus on answering queries about the data
    - In flume, each view remembers a version number, and if the version number changes, it just rebuilds the view. This means view code can be easily updated, or new views added. It just rebuilds the view on startup.

- https://github.com/Shaance/rust-simple-log-append-db /rust
  - Simple db using append only log file. 
  - This runs in a single thread
  - Implemented for learning purpose
  - When log file exceeds a certain size (1 MB in the main.rs file usage of the db), compaction process will kick-in.

- https://github.com/rozbb/ct-merkle /rust
  - an implementation of the append-only log described in the Certificate Transparency specification (RFC 6962). 
  - The log is a Merkle tree, and its leaves are the items it contains.

- https://github.com/ssbc/margaret /go
  - a flume-like persisted append-only log implementation
  - Margaret outputs data according to the offset2 format, which is inspired by (but significantly differs from) flumelog-offset

- https://github.com/embano1/memlog /apache2/go
  - A Kafka log inspired in-memory and append-only data structure
  - lightweight, thread-safe and append-only in-memory data structure modeled as a Log.

## oplog

- https://github.com/eugeneware/abstract-log /js/inactive
  - An abstract interface to build data processing applications on a log-based architecture
  - The idea would be to have implementations that would allow reading/writing to files, databases, kafka, redis, etc.
  - This is basically abstract-blob-store for append-only logs.
  - https://github.com/eugeneware/fs-log

- https://github.com/hackergrrl/append-only-log /js/inactive
  - Abstract interface for an append-only log.
  - Like abstract-blob-store, but for append-only logs.

- https://github.com/bigeasy/transcript /js/go/rust
  - Append-only log that supports JSON or binary formats.
- https://github.com/adzialocha/append-only-log /rust
  - Experiment with append-only logs

- https://github.com/felixge/node-dirty /js/inactive
  - fast key value store with append-only disk log. Ideal for apps with < 1 million records.
  - The file format is newline separated JSON
  - Your database lives in the same process as your application, they share memory
  - There is no query language, you just `forEach` through all records

- https://github.com/arindas/riakv /rust
  - Log structured, append only, key value store implementation from Rust In Action with some enhancements.
  - Persistent key value store with a hash table index
  - Optionally, persistent index for fast loading
  - The underlying storage used by the key value store is completely generic. It is subject to Read + Write + Seek trait bounds.
- https://github.com/ollej/akvdb /rust
  - A simple key-value store with a log-structured, append-only storage architecture where data is encrypted with AES GCM.
  - Modified from the actionkv example in the book Rust in Action
  - https://github.com/rust-in-action/code
  - https://github.com/RottingHorse/actionkv
  - https://github.com/tony-go/fdb

- https://github.com/pietgeursen/bamboo-rs 
  - Rust implementation of bamboo.
  - https://github.com/AljoschaMeyer/bamboo
    - A cryptographically secure, distributed, single-writer append-only log that supports transitive partial replication and local deletion of data.
    - this log format can serve as a more efficient alternative to secure-scuttlebutt's linked lists or hypercore's merkle forests.

- https://github.com/pfrazee/queryable-log /js/inactive
  - A structured append-only log which can be queried. 
  - Stores as ndjson and applies a log-size limit.

- https://github.com/montyanderson/kog /ts
  - An append-only log database with replication and high availability
- https://github.com/marcelsud/snapdb /ts
  - An append-only log DB just for fun and profit
- https://github.com/oak-database/oak-lite /js
  - https://github.com/oak-database/oak-lite

- https://github.com/fasiha/isomorphic-gatty /ts
  - Append-only log for isomorphic-git, expected to be used as remote sync for local-first web app
  - Gatty saves a stream of events to a git repo and synchronizes it with a remote git server (e.g., GitHub, Gitlab, Gogs, Azure Repos, etc.). The “events” are just plain strings that your app generates and understands: Gatty doesn’t know anything about them.

- https://github.com/mafintosh/append-tree /js/hypercore/inactive
  - Model a tree structure on top of an append-only log.
  - stores a small index for every entry in the log, meaning no external indexing is required to model the tree. 
  - Also means that you can perform fast lookups on sparsely replicated logs.

- https://github.com/stelar-labs/neutrondb-rs /rust
  - a log-structured merge-tree key-value store for any implemented data type.

- https://github.com/abcum/syncr /go
  - a library for storage of append-only log data on local or remote storage.
  - Thread safe, for use by multiple goroutines
  - Ability to buffer writes, or sync writes immediately
  - Support for append-only files locally, and in S3, GCS, RiakCS, CephFS, SeaweedFS

- https://github.com/rosedblabs/wal /go
  - Write Ahead Log for LSM or bitcask storage, with block cache.

- https://github.com/tomfran/LSM-Tree /java
  - Log-Structured Merge Tree Java implementation
  - Sorted String Table (SSTable) is a collection of files modelling key-value pairs in sorted order by key. It is used as a persistent storage for the LSM tree.
- https://github.com/ingaleniranjan365/lsmdb /java
  - Implementation of log-structured merge-trees to create a key-value store
  - Implement a generic key-value database in Java that fulfills /element/:id/timestamp/:timestamp
  - https://github.com/vardhan/lsmdb

## log-database

- https://github.com/mvayngrib/logbase /js/inactive
  - Append-only log and log-based database

- https://codeberg.org/small-tech/jsdb /js
  - A zero-dependency, transparent, in-memory, streaming write-on-update JavaScript database for the Small Web that persists to a JavaScript transaction log.
  - A small and simple data layer for basic persistence and querying.
  - For Node.js: will not work in the browser
  - all data is kept in memory and, without tweaks, cannot exceed 1.4GB in size
  - Streaming writes on update: writes are streamed to disk to an append-only transaction log as JavaScript statements and are both quick (in the single-digit milliseconds region on a development laptop with an SSD drive) and as safe as we can make them (synchronous at the kernel level).
  - No schema, no migrations: again, this is meant to be a very simple persistence, query, and observation layer for local server-side data
  - JSDB tables are written into JavaScript Data Format (JSDF) files. 
  - A JSDF file is just es6 module 
  - When you load in a JSDB table, JSDB will, by default, compact the JSDF file.

- https://github.com/khonsulabs/nebari /rust
  - A pure Rust database implementation using an append-only B-Tree file format.
  - This crate provides the Roots type, which is the transactional storage layer for BonsaiDb. 
  - It is loosely inspired by Couchstore.
  - A TreeFile is a key-value store that uses an append-only file format for its implementation.
  - The major downside of append-only formats is that deleted data isn't cleaned up until a maintenance process occurs: compaction

- https://github.com/lockbook/db-rs /rust
  - embedded, single-threaded database for Rustaceans.
  - All table mutations are persisted to an append only log using the fast & compact bincode representation of your types.
  - Each table has an in-memory representation and a corresponding log entry format. 
  - Presently there is no way to abort a transaction. TXs are also a mechanism for batch writing, log entries are kept in memory until the transaction completes and written once to disk.
  - https://github.com/Parth/hmdb /legacy
- https://github.com/qoollo/pearl /rust
  - Append only key-value blob storage on disk
- https://github.com/GlenDC/alumdb /rust
  - an embeddable append-log written in Rust that can optionally be used via a server as well.

- https://github.com/ruuda/noblit /rust
  - Noblit is an embeddable append-only database. 
  - The database records a history of immutable (entity, attribute, value) tuples. 
  - Tuples can be asserted and retracted. A retraction is recorded as a new fact; it is not a delete. 
  - Any historical state of the database can be reproduced, and the history is first-class and queryable.

- https://github.com/wasmerio/ate /rust
  - a distributed immutable data store and built in memory based materialized view with strong encryption and authentication.
  - data is persisted to a distributed commit log.
  - strong authentication and authorized is by design built into the data model.

- https://github.com/nrw/pouchdb-commit-log /js/inactive
  - cluster-friendly append-only topic-based commit log + materialized view implementation for pouchdb (inspired by apache kafka and samza)

- https://github.com/delta-db/deltadb /201602/js/inactive
  - DeltaDB is an offline-first database designed to talk directly to clients and works great offline and online.
  - Stores all data as a series of deltas, which allows for smooth collaborative experiences even in frequently offline scenarios.
  - https://github.com/delta-db/deltadb-server

- https://github.com/barrucadu/logdb /go/inactive
  - An efficient log-structured database supporting efficient insertion of new entries and removal from either end of the log.
  - a Go library for efficient log-structured databases. 
  - A log-structured database is a very simple data store where writes are only ever appended to the database, there are no random-access writes at all.
  - To prevent the database from growing indefinitely, a contiguous chunk of entries can be removed from either the beginning or the end.
- https://github.com/healeycodes/bitcask-lite /go
  - A log-structured hash table database. 
  - Speedy K/V store for datasets larger than memory.
- https://github.com/arriqaaq/flashdb /go
  - simple, in-memory, key/value store in pure Go. 
  - It persists to disk, is ACID compliant, and uses locking for multiple readers and a single writer. 
  - It supports redis like operations for data structures like SET, SORTED SET, HASH and STRING.
  - ACID semantics with locking transactions that support rollbacks
- https://github.com/justinethier/keyva /go
  - distributed key-value store using the log-structured merge tree (LSM tree), a popular alternative to B-trees for persistently storing data.
  - Data is always added to an LSM tree using sequential writes. That is, data is only written to storage using append operations.
  - The MemTable, a data structure stored entirely in memory, is initially used to store new data.
  - In order to recover data across restarts, the same data is also appended to a Write Ahead Log (WAL). The WAL is a simple append-only log that contains a single record for each operation made to the LSM tree.
  - Eventually the MemTable will become too large to efficiently hold in memory and the data is flushed to a Sorted String Table (SST) file on disk.
  - SST files can efficiently serve large data sets
- https://github.com/dgraph-io/badger /go
  - embeddable, persistent and fast key-value (KV) database written in pure Go. 
  - It is the underlying database for Dgraph, a fast, distributed graph database. 
  - It's meant to be a performant alternative to non-Go-based key-value stores like RocksDB.
  - [Using Badger for storing immutable, append-only logs, FIFO compaction strategy?](https://github.com/dgraph-io/badger/issues/1165)
    - Badger supports only leveled compaction for now. By default, we keep only a single version of a key. Older versions are dropped by compactions automatically. This means old stale data will be cleaned up eventually.

- https://github.com/google/trillian /go
  - A transparent, highly scalable and cryptographically verifiable data store.
  - Trillian implements a Merkle tree whose contents are served from a data storage layer, to allow scalability to extremely large trees. 
  - On top of this Merkle tree, Trillian provides an append-only Log mode, analogous to the original Certificate Transparency logs. In this mode, the Merkle tree is effectively filled up from the left, giving a dense Merkle tree.
  - Certificate Transparency (CT) is the most well-known and widely deployed transparency application

- https://github.com/yahoo/HaloDB /apache2/java
  - simple embedded key-value store written in Java. 
  - HaloDB is suitable for IO bound workloads, and is capable of handling high throughput reads and writes at submillisecond latencies.
  - written for a high-throughput, low latency distributed key-value database that powers multiple ad platforms at Yahoo, therefore all its design choices and optimizations were primarily for this use case.
  - HaloDB comprises of two main components: 
    - an **index in memory** which stores all the keys, and append-only log files on the persistent layer which stores all the data. 
    - To reduce Java garbage collection pressure the index is allocated in native memory, outside the Java heap.

- https://github.com/upserve/uppend /java
  - an append-only, key-multivalue store which is suitable for streaming aggregation of immutable event data. 
  - It is designed to handle both wide (large number of unique keys) and deep (large number of elements in a particular key) data. 
  - a multithreaded embedded java database. 
  - New keys are not durably written immediately, they are added to a temporary cache. The write cache is periodically flushed to disk. 
  - heavily utilizes the mmap, and the linux page cache.

- https://github.com/pravega/pravega /java
  - open source storage system implementing Streams as first-class primitive for storing/serving continuous and unbounded data.
  - A Pravega Stream is similar to but more flexible than a "topic" in popular message oriented middleware such as RabbitMQ or Apache Kafka.
  - Pravega Streams are based on an append-only log data structure. By using append-only logs, Pravega rapidly ingests data into durable storage. 

## log-state

- https://github.com/fiatjaf/journalstate /js
  - turn a log of sequential, handwritten facts, into a state

- https://github.com/chinedufn/dipa /rust
  - designed to generate very tiny diffs by default
  - does not know anything about networks and has no networking code

## log-utils

- https://github.com/y-scope/clp /cpp
  - https://yscope.com/
  - Compressed Log Processor (CLP) is a free tool capable of compressing text logs and searching the compressed logs without decompression.
# materialized-view
- resources
  - [ppt: Materialized Views with MongoDB](https://daniloab.github.io/mongodb-materialized-view-talk/)

- https://github.com/Svjard/nepata /ts
  - A rapid report framework around MongoDB allowing for the generation of materialized views in MongoDB against collections without an in-depth understanding of Mongo queries.
- https://github.com/ilinieja/node-mongoose-materialized-views-example /ts
  - [How to create and manage Mongo DB Materialized Views using triggers.](https://bonigopalan.medium.com/how-to-create-and-manage-mongo-db-materialized-views-using-triggers-a2fb58a4d1a0)
- https://github.com/janez89/mongoose-materialized /js/inactive
  - A mongoose plugin for the materialized paths.

- https://github.com/viaacode/pulsar2db /rust
  - Subscribe to Pulsar topics and build final state (or a materialized view) for a certain object or key.

- https://github.com/ilikepi63/turnip-rs /rust
  - Leaderless, streaming platform based on materialized views
# more
