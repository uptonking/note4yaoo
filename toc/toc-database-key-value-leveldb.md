---
title: toc-database-key-value-leveldb
tags: [database, key-value, leveldb, toc]
created: 2022-11-03T04:09:01.455Z
modified: 2022-11-03T04:14:00.563Z
---

# toc-database-key-value-leveldb

# guide

- not-yet
  - browser-level的持久化为何是二进制？

- resources
  - leveldb vs redis
  - https://github.com/Level/awesome
  - [LSM-Tree 论文的中文翻译](https://github.com/tangwz/LSM-Tree-CN/blob/main/LSM-Tree-CN.md)
# db-key-value
- denokv /320Star/MIT/202312/rust/ts/sqlite
  - https://github.com/denoland/denokv
  - https://deno.com/kv
  - A self-hosted backend for Deno KV, the JavaScript first key-value database
  - Deno KV can be used with the built-in single instance database in the CLI, useful for testing and development, with a hosted and scalable backend on Deno Deploy, or with this self-hostable Deno KV backend.
  - built on top of the robust SQLite database, and uses non-blocking IO to ensure excellent performance even in the face of hundreds of concurrent connections.

- snap-db /58Star/MIT/202001/ts/NoDeps/Nano-SQL
  - https://github.com/only-cliches/snap-db
  - Simple & Robust LSM Powered Javascript key-value store
  - SnapDB is a pure javascript persistent key-value store that provides ordered mapping from keys to string values. 
  - Data is persisted to disk using a Log Structure Merge Tree (LSM Tree) inspired by LevelDB/RocksDB. 
  - SnapDB has 100% API compatibility with LevelDB & RocksDB and also includes additional functionality.
  - Uses synchronous filesystem methods to exclusively perform append writes to disk, this puts the performance of SnapDB near the theoretical maximum write performance for ACID compliant javascript databases.

- https://github.com/heineiuo/rippledb /MIT/202010/ts/lsm/inactive
  - https://rippledb.github.io/
  - an embeddable key-value database engine in pure TypeScript, based on LSM-Tree, Inspired by LevelDB.

- https://github.com/apple/foundationdb /Apache2/cpp
  - a distributed database designed to handle large volumes of structured data across clusters of commodity servers.
  - It organizes data as an ordered key-value store and employs ACID transactions for all operations. 
  - It is especially well-suited for read/write workloads but also has excellent performance for write-intensive workloads.

- keyv /2.4kStar/MIT/202402/ts
  - https://github.com/jaredwray/keyv
  - https://keyv.org/
  - Simple key-value storage with support for multiple backends
  - Storage Adapters: etcd, mongodb, redis, sqlite, pg, mysql
  - https://github.com/roccomuso/keyv-leveldb /201803/js
    - LevelDB storage adapter for Keyv.
  - https://github.com/zaaack/keyv-file /202402/ts
    - File storage adapter for Keyv, using json to serialize data fast and small
    - TTL functionality is handled internally by interval scan, don't need to panic about expired data take too much space.

- https://github.com/engula/engula /apache2/rust/inactive/selectdb成员项目
  - https://engula.io/
  - a distributed key-value store, used as a cache, database, and storage engine.
  - [Engula Development Guide](https://github.com/engula/engula/discussions/244)
    - API: inspired by Redis, and some programming languages like Rust, Python, etc.
    - Architecture: inspired by Socrates, Aurora, Spanner, BigTable, TAO.
    - Transaction: inspired by hybrid-logical-clocks (HLC)
    - Stream engine: inspired by LogDevice, Delos
    - Object engine: inspired by RocksDB, GFS, and DeltaLake.
  - https://github.com/w41ter/sekas /rust
    - a distributed key-value store, used as cache, database, and storage engine for other distributed system.

- https://github.com/mozilla/rkv /rust
  - typed key-value storage solution. 
  - It supports multiple backend engines with varying guarantees, such as LMDB for performance, or "SafeMode" for reliability.
  - The "SafeMode" backend performs well, with two caveats: the entire database is stored in memory, and write transactions are synchronously written to disk (only on commit).

- https://github.com/surrealdb/echodb /rust
  - An embedded, in-memory, immutable, copy-on-write, key-value database engine
  - Multi-version concurrency control
  - Rich transaction support with rollbacks

- https://github.com/spacejam/sled /MIT/202308/rust/bw-tree
  - https://docs.rs/sled
  - http://sled.rs/
  - a high-performance embedded database with an API that is similar to a `BTreeMap<[u8], [u8]>`.
  - fully thread-safe, and all operations are atomic.
  - subscribe to changes on key prefixes
  - flash-optimized log-structured storage
  - uses modern b-tree techniques such as prefix encoding and suffix truncation for reducing the storage costs of long keys with shared prefixes.
  - lock-free tree on a lock-free pagecache on a lock-free log
  - Sled uses a hybrid architecture of B+ Trees and LSM Tree (Bw Trees)
  - https://github.com/panicfarm/sltest
    - Demonstrates potential memory leak in SLED.
  - [Subscriptions and the Pit of Success](https://github.com/spacejam/sled/issues/1162)
  - [An embedded database written in Rust | Hacker News_201805](https://news.ycombinator.com/item?id=17170733)
  - [Sled: Embedded Database Written in Rust | Hacker News_202002](https://news.ycombinator.com/item?id=22375979)
    - LevelDB is a LSM database. 
    - LSM is generally better for write workloads over BTree DBs like LMDB and sled. LMDB also has a single writer restriction.

- https://github.com/WyattJia/Pomegranate /rust/archived
  - A tiny skiplist based log-structured merge-tree written in Rust.

- https://github.com/JetBrains/xodus /apache2/java
  - a transactional schema-less embedded database
  - initially developed for JetBrains YouTrack, also used in JetBrains Hub
  - highly concurrent. Reads are completely non-blocking due to MVCC and true snapshot isolation.
  - written in pure Java and Kotlin.

- https://github.com/lmdbjava/lmdbjava /java
  - Lightning Memory Database (LMDB) for Java: a low latency, transactional, sorted, embedded, key-value store
  - LmdbJava adds Java-specific features to LMDB
  - https://github.com/lmdbjava/benchmarks
    - Benchmark of open source, embedded, memory-mapped, key-value stores available from Java (JMH)
  - https://github.com/LMDB/lmdb /c
    - https://www.symas.com/lmdb
    - fast, memory-efficient database we developed for the OpenLDAP Project. 
    - With memory-mapped files, LMDB has the read performance of a pure in-memory database while retaining the persistence of standard disk-based databases.

- https://github.com/alanshaw/pail /MIT/202309/js
  - DAG based key value store.
  - Sharded DAG that minimises traversals and work to build shards.
  - 依赖@ipld/car~dag-cbor, sade, archy

- https://github.com/mikeal/dkv /js/inactive
  - Decentralized key-value store running on IPFS
  - DKV offers a simple interface for storing key/value pairs. Values can include links to other values recursively, giving you the ability to create complex graphs that de-duplicate commonly linked data.

- https://github.com/cberner/redb /2.3kStar/MIT/202311/rust/lmdb
  - https://www.redb.org/
  - simple, portable, high-performance, ACID, embedded key-value store.
  - written in pure Rust and is loosely inspired by lmdb. 
  - Data is stored in a collection of copy-on-write B-trees. 
  - Zero-copy, thread-safe,  `BTreeMap` based API
  - Fully ACID-compliant transactions
  - MVCC support for concurrent readers & writer, without blocking
  - Crash-safe by default
  - Savepoints and rollbacks

- https://github.com/ether/ueberDB /apache2/202401/ts
  - UeberDB turns every database into a simple key value store by providing a layer of abstraction between your software and your database.
  - UeberDB does bulk writing ergo reduces the overhead of database transactions.
  - Reads are cached and writes are done in a bulk. This can be turned off.
  - 支持 couchdb/Mongo/Elasticsearch/MySQL/pg/sqlite/redis

- https://github.com/huan/flash-store /apache2/202203/ts/inactive
  - FlashStore is Key-Value persistent storage with easy to use ES6 Map-like API(both Async and Sync support), powered by LevelDB and TypeScript.
  - Supported Backend: LevelDB, LevelDB, SnapDB, RocksDB

- https://github.com/web3-storage/pail /MIT/202402/js/ts
  - DAG based key value store. 
  - Sharded DAG that minimises traversals and work to build shards.
  - 依赖@ipld/car、@ipld/dag-cbor、cborg、sade

- https://github.com/cockroachdb/pebble /BSD/202402/go
  - RocksDB/LevelDB inspired key-value database in Go
  - a LevelDB/RocksDB inspired key-value store focused on performance and internal usage by CockroachDB.
  - Pebble inherits the RocksDB file formats and a few extensions such as range deletion tombstones, table-level bloom filters, and updates to the MANIFEST format.
  - Pebble intentionally does not aspire to include every feature in RocksDB and specifically targets the use case and feature set needed by CockroachDB:
    - Block-based tables
    - Checkpoints
    - Indexed batches
    - Level-based compaction
  - RocksDB has a large number of features that are not implemented in Pebble
  - WARNING: Pebble may silently corrupt data or behave incorrectly if used with a RocksDB database that uses a feature Pebble doesn't support
  - Pebble was introduced as an alternative storage engine to RocksDB in CockroachDB v20.1 (released May 2020) and was used in production successfully at that time. Pebble was made the default storage engine in CockroachDB v20.2 (released Nov 2020). 
# leveldb-like
- https://github.com/Level/bench
  - Benchmark `abstract-level` databases. 
  - Currently only suitable for use in Node.js.

- https://github.com/google/leveldb /BSD/c++
  - LevelDB is a fast key-value storage library written at Google that provides an ordered mapping from string keys to string values.
  - Data is stored sorted by key.
  - This is not a SQL database. 
    - It does not have a relational data model, 
    - it does not support SQL queries, 
    - and it has no support for indexes.
  - Only a single process (possibly multi-threaded) can access a particular database at a time.
  - no client-server support builtin to the library
  - https://github.com/facebook/rocksdb /Apache2|GPLv2/c++
    - built on earlier work on LevelDB
    - 功能丰富

- https://github.com/Level/community
  - Level is a collection of Node.js modules for creating transparent databases. 
    - A solid set of primitives enable powerful databases to be built in userland.
  - At the heart of Level are key-value databases that follow the characteristics of LevelDB. 
    - They support binary keys and values, batched atomic writes and bi-directional iterators that read from a snapshot in time. 
    - Entries are sorted lexicographically by keys 
  - Level combines idiomatic JavaScript interfaces like async iterators with Node.js interfaces like streams, events and buffers. 
    - It offers a rich set of data types through encodings 
    - and can split a database into evented sections called sublevels.
  - The underlying storage can be easily swapped by selecting a different database implementation, all sharing a common API and the same characteristics.
- https://github.com/Level/level
  - Universal abstract-level database for Node.js and browsers.
  - Bundle for leveldown/classic-level and level-js/browser-level
  - It offers a persistent database that works in both Node.js and browsers, backed by LevelDB and IndexedDB respectively. 
  - Many alternatives are available. 
- https://github.com/Level/abstract-level
  - Abstract class for a lexicographically sorted key-value database. 
  - The successor to abstract-leveldown
  - abstract-level is the new core of Level on top of which several databases are (or will be) implemented.
  - An abstract-level database is at its core a key-value database. A key-value pair is referred to as an entry here
- https://github.com/Level/classic-level
  - An abstract-level database backed by LevelDB. 
  - The successor to leveldown with builtin encodings, sublevels, events, promises and support of Uint8Array. 
- https://github.com/Level/browser-level
  - An abstract-level database for browsers, backed by IndexedDB. 
  - The successor to level-js
  - browser-level has first-class support of binary keys and values, using either Uint8Array or Buffer.
- https://github.com/Level/memory-level
  - In-memory abstract-level database for Node.js and browsers, backed by a fully persistent red-black tree.
  - The successor to memdown and level-mem.
- https://github.com/Level/levelup
  - A wrapper for abstract-leveldown compliant stores, for Node.js and browsers.
  - deprecated, because it is superseded by abstract-level.

- https://github.com/jed/sheet-down
  - This library uses abstract-leveldown to turn a worksheet within a Google Spreadsheet into a leveldown-compatible store for use with levelup.

- https://github.com/tancehao/reimplement-leveldb-in-rust /202304/rust/inactive
  - reimplement leveldb in rust, with some new features.
  - Search tired levels(L0 currently) in parellel; 
  - MVCC enabled.

- https://github.com/belayeng/quadstore /MIT/ts
  - https://belayeng.github.io/quadstore
  - Quadstore is a LevelDB-backed RDF graph database / triplestore for JavaScript runtimes (browsers, Node.js, Deno, Bun, ...) written in TypeScript.
  - Implements the Sink, Source and Store RDF/JS interfaces for maximum interoperability with other RDF libraries
  - Supports SPARQL queries via quadstore-comunica, a tailored configuration and distribution of the Comunica querying framework
  - Natively capable of querying across named graphs

- https://github.com/lotusdblabs/lotusdb /go/lsm
  - LotusDB is a fast k/v database compatible with LSM tree and B+ tree, optimization of badger and bbolt.
  - Much lower read and space amplification(倍率，放大率) than typical LSM
  - LotusDB is inspired by a paper named SLM-DB in USENIX FAST ’19, and the Wisckey paper also helps a lot.

- https://github.com/skyzh/mini-lsm /rust
  - https://skyzh.github.io/mini-lsm/
  - Build a simple key-value storage engine in a week!
  - Week 1: Mini-LSM
  - Week 2: Compaction and Persistence
  - Week 3: Multi-Version Concurrency Control
  - Log-structured merge tree is a data structure to maintain key-value pairs. 
  - This data structure is widely used in distributed database systems like TiDB and CockroachDB as their underlying storage engine. 
  - RocksDB, based on LevelDB, is an implementation of LSM-Tree storage engine.
  - For RB-Tree and B-Tree, all data operations are in-place. That is to say, when you update the value corresponding to the key, the value will be overwritten at its original memory or disk space. 
  - But in an LSM Tree, all write operations, i.e., insertions, updates, deletions, are performed in somewhere else. These operations will be batched into SST (sorted string table) files and be written to the disk. Once written to the disk, the file will not be changed. These operations are applied lazily on disk with a special task called compaction. The compaction job will merge multiple SST files and remove unused data.

- https://github.com/adambcomer/database-engine /rust
  - LSM-Tree Key-Value Store based on RocksDB
  - [Build a Database Pt. 1: Motivation & Design | Adam Comer](https://adambcomer.com/blog/simple-database/motivation-design/)
    - In this series, we will design and build a simple Log Structured Merge(LSM) tree storage engine similar to RocksDB
    - A LSM-Tree storage pattern is very efficient for writes

- https://github.com/KipData/KipDB /apache2/rust/lsm
  - 轻量级键值存储引擎, 整体设计参考LevelDB，旨在作为NewSQL分布式数据库的存储引擎
  - 支持嵌入式/单机存储/远程调用等多应用场景
  - 实现MVCC以支持ACID
  - 高性能，BenchMark写入吞吐量约为Sled的两倍，且大数据量下的顺序读取平均延迟为1μs左右
  - 远程连接使用ProtoBuf实现，支持多语言通信
  - https://github.com/KipData/KipSQL
    - Lightweight SQL calculation engine, as the SQL layer of KipDB, implemented with TalentPlan's TinySQL as the reference standard

- https://github.com/Fullstop000/wickdb /bsd/202108/rust/inactive
  - Pure Rust LSM-tree based embedded storage engine

- https://github.com/burhanxz/Distributed-KV /java
  - 根据LSM论文，并结合CPP已有的实现，利用Java实现了LSM架构；
  - 综合Dubbo等框架的特点，实现了简洁的RPC框架。
# rocksdb-like
- https://github.com/speedb-io/speedb /apache2/202401/cpp
  - https://www.speedb.io/
  - A RocksDB compliant high performance scalable embedded key-value store
  - Speedb is a 100% RocksDB compatible, drop-in library, focused on high performance, optimized for modern storage hardware and scale, on-premise and in the cloud. 
# foundationdb-powered
- https://github.com/FoundationDB/fdb-record-layer /apache2/202401/java
  - The Record Layer is a Java API providing a record-oriented store on top of FoundationDB, (very) roughly equivalent to a simple relational database
  - Records are defined and stored in terms of protobuf messages.
  - The Record Layer supports a variety of different index types including value indexes (the kind provided by most databases), rank indexes, and aggregate indexes.
  - Queries - The Record Layer does not provide a query language, however it provides query APIs with the ability to scan, filter, and sort across one or more record types, and a query planner capable of automatic selection of indexes.
  - The Record Layer provides the ability to support many discrete record store instances, all with a shared (and evolving) schema. 
    - For example, rather than modeling a single database in which to store all users' data, each user can be given their own record store, perhaps sharded across different FDB cluster instances.
# redis-like
- https://github.com/seppo0010/rsedis /1.7kStar/bsd/202011/rust
  - Redis re-implemented in Rust. To learn Rust.
  - rsedis does not rely on UNIX-specific features. Windows users can run it as a replacement of Redis.
  - uses multiple threads which may be more useful in machines with multiple cores.

- https://github.com/dicedb/dice /go
  - Re-implementation of Redis in Golang
  - simple Golang-based in-memory KV store that speaks the Redis dialect
  - not production ready
  - started building Dice DB to understand Redis better with [Redis Internals Course](https://arpitbhayani.me/redis-internals/)

- https://github.com/alicebob/miniredis /go
  - Miniredis implements (parts of) the Redis server, to be used in unittests. 
  - It enables a simple, cheap, in-memory, Redis replacement, with a real TCP interface. 
  - Think of it as the Redis version of net/http/httptest.
  - There are no dependencies on external binaries, so you can easily integrate it in automated build processes.
# level-search
- search-index /1.3kStar/MIT/202207/js
  - https://github.com/fergiemcdowall/search-index
  - A persistent, network resilient, full text search library for the browser and Node.js
  - built on top of levelup, its possible to use another backend by passing the appropriate `abstract-leveldown`

- levi /374Star/MIT/201901/js
  - https://github.com/cshum/levi
  - Stream based full-text search for Node.js and browsers. Using LevelDB as storage backend.
  - 依赖levelup、cosine-similarity、stemmer
  - Full-text search using TF-IDF and cosine similarity plus query-time field boost options. 
  - Levi is built on LevelUP. By default, it uses LevelDB on Node.js and IndexedDB on browser. 
  - Using stream based query mechanism with Highland.js, Levi is designed to be memory efficient

- https://github.com/eugeneware/levels /45Star/MIT/201309/js
  - a light-weight LevelDB full text search for node.js. 
  - This is a port of the redis search reds by TJ Holowaychuk to use LevelDb.

- https://github.com/juliangruber/level-trie /31Star/MIT/201608/js
  - The TRIE data structure and search algorithm, on top of leveldb.

- https://github.com/dominictarr/level-inverted-index /201602/js
  - Inverted Index for levelup.

- https://github.com/eugeneware/level-queryengine /63Star/BSD/201405/js
  - A generic pluggable query-engine system (that supports indexes) for levelup/leveldb databases.
  - Using this architecture you can query your levelup database using your own query langauge with full index support.
- https://github.com/eugeneware/fulltext-engine /32Star/BSD/201405/js
  - Query your levelup/leveldb engine using full text search phrases with INDEXES.
  - This is a plugin for level-queryengine.
- https://github.com/eugeneware/subindex /201506/js
  - Generic pluggable indexing system for leveldb/levelup.
  - Designed to be used with level-queryengine to create efficient searches on levelup with pluggable query languages/systems
- https://github.com/eugeneware/jsonquery-engine /201504/js
  - A full MongoDB query language implementation with INDEXES for querying your levelup/leveldb database.
  - This is a plugin for level-queryengine.
# level-query
- https://github.com/Raynos/level-livefeed /MIT/201409/js
  - Live query a range in leveldb
  - You query a range in the database. It will load the range from disk and then also add on anything else you put or del from it.
# level-multi
- https://github.com/tradle/multi-hyperbee /js
  - A LevelUP compatible leaderless multi-master database with eventual consistency, **using hyperbee + CRDT + HLC**. 
  - Similarly CockroachDB achieves replication on top of RocksDB, but here it is a pure P2P **streaming** database, with zero central management.
  - like all other low-level components of hypercore ecosystem it is a single-writer data structure. Multi-writer is a higher-level abstraction, hence the name multi-hyperbee.
  - batch is not yet supported
  - In this version we only add multi-writer to Hyperbee. But we can extend it to Trie and Drive

- https://github.com/juliangruber/multilevel /201802/js
  - Expose a LevelDB over the network

- https://github.com/mafintosh/multi-master-merge /201511/js
  - A database with multi master replication and merge support based on leveldb, fwdb and scuttleup
# level-utils
- https://github.com/fergiemcdowall/pumbledb /201308/js
  - a Node.js key-value server that uses LevelDB

- https://github.com/laixintao/iredis /python
  - Interactive Redis: A Cli for Redis with AutoCompletion and Syntax Highlighting

- https://github.com/kesla/mysqldown /201307/js
  - An drop-in replacement for LevelDOWN that works in mysql
# kv-based
- https://github.com/nlfiedler/mokuroku /apache2/rust/202309
  - Secondary indices for RocksDB in Rust.
  - designed to provide a secondary index on top of the RocksDB key/value store, similar to what PouchDB does for LevelDB.
  - Your application will provide implementations of the `Document` trait to suit the various types of data to be stored in the database, and this library will invoke the mapping function on those Document instances to produce index key/value pairs.
  - The behavior of this library is similar to PouchDB, albeit(虽然；尽管) with an API suitable for the language. 
  - Unlike PouchDB, this library does not put any constraints on the format of the database records.
  - You may see the term `view` used here and there. This is what CouchDB and PouchDB call the indices in their documentation. 
    - The function name `emit` also comes from the `map/reduce` API of CouchDB, and makes as much sense as anything else.
  - What this library does exactly: the indices managed by this library are "stand-alone", meaning they are not embedded within the database files (e.g. zone maps or bloom filters). Additionally, the index is updated in a lazy fashion

- https://github.com/earthstar-project/earthstar /LGPLv3/ts
  - Storage for private, distributed, offline-first applications.
  - Earthstar is an offline-first key-value database which supports author versions.
  - This is a reference implementation written in Typescript. You can use it to add Earthstar functionality to applications running on servers, browsers, the command line, or anywhere else JavaScript can be run.
  - [What Earthstar is and is not](https://github.com/earthstar-project/earthstar-docs/blob/main/docs/intro/rules-of-earthstar.md)
    - It's a delta-state based CRDT that works in adversarial conditions.
  - can store arbitrary data, keyed by two pieces of information: a free-form `path` and a public `key` identifying the author. So a single path like /wiki/flowers may hold revisions by multiple authors.
  - A share's data is stored on its users' devices using replicas.
    - A replica is a concrete copy of the data in a share, stored on a user's device.
    - When two replicas are configured to use the same share address, they can synchronise their data with each other
  - Data stored in a replica are persisted as separate Documents.
    - Documents describe and contain your share's data.
    - Every document has a path like /my-story.txt.
  - [Comparison to GUN?](https://github.com/earthstar-project/earthstar/discussions/230)
    - Designed to allow partial sync of the data, but not quite implemented yet_202101
  - [Comparison to Kappa-db?](https://github.com/earthstar-project/earthstar/discussions/228)
    - Kappa-db is a bundle of append-only logs (hypercores), one per author per device. It builds indexes by processing messages from the logs, in order, to build up a reduced state. The logs grow forever.
    - Earthstar is a key-value database.You can hold any subset of the documents, sync them in any order, do partial sync, drop ones you don't want.
    - Kappa-db uses hyperswarm to find peers and the hypercore protocol to sync data, with some custom stuff to handle multiple hypercores.
    - Earthstar is not well developed here. It can connect to cloud peers over HTTP for syncing, in the style of SSB pubs. I'm planning to add hyperswarm also for direct p2p connections.
    - Kappa-db relies on "logs that sync" as the underlying abstraction. 
    - Earthstar relies on a specification for "signed versioned documents".

- https://github.com/digidem/unordered-materialized-kv /js/inactive
  - materialized view key/id store based on unordered log messages
  - This library presents a familiar key/value materialized view for append-only log data which can be inserted in any order. 
  - This library implements a multi-register conflict strategy, so each key may map to more than one value. To merge multiple values into a single value, point at more than one ancestor id.
  - This library is useful for **kappa architectures** with missing or out of order log entries, or where calculating a topological ordering would be expensive
  - This library does not store values itself, only the IDs to look up values. This way you can use an append-only log to store your primary values without duplicating data.
# key-value-benchmark
- https://github.com/couchbaselabs/ForestDB-Benchmark /201706/cpp
  - a benchmark program for embedded key-value storage engines, based on a sophisticated workload generation which is more realistic than performing a bunch of read/write operations. 
  - It generates key-value store operations using the APIs of Couchstore, which is the current storage engine of Couchbase Server. 
  - We currently provide API-wrappers for ForestDB, LevelDB, RocksDB, and WiredTiger.
# more-key-value
- https://github.com/pgte/alfred /201109/js
  - Alfred is a fast in-process key-value store for node.js.
  - atomic operations on one record
  - multiple key-value maps in one database
  - append-only files
