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
- snap-db /58Star/MIT/202001/ts/Nano-SQL
  - https://github.com/only-cliches/snap-db
  - Simple & Robust LSM Powered Javascript key-value store
  - SnapDB is a pure javascript persistent key-value store that provides ordered mapping from keys to string values. 
  - Data is persisted to disk using a Log Structure Merge Tree (LSM Tree) inspired by LevelDB / RocksDB. 
  - SnapDB has 100% API compatibility with LevelDB & RocksDB and also includes additional functionality.

- https://github.com/apple/foundationdb /Apache2/cpp
  - a distributed database designed to handle large volumes of structured data across clusters of commodity servers.
  - It organizes data as an ordered key-value store and employs ACID transactions for all operations. 
  - It is especially well-suited for read/write workloads but also has excellent performance for write-intensive workloads.

- keyv /2kStar/MIT/202211/js
  - https://github.com/jaredwray/keyv
  - Simple key-value storage with support for multiple backends
  - Storage Adapters: etcd, mongodb, redis, sqlite

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

- https://github.com/dicedb/dice /go
  - Re-implementation of Redis in Golang
  - simple Golang-based in-memory KV store that speaks the Redis dialect
  - not production ready
  - started building Dice DB to understand Redis better with [Redis Internals Course](https://arpitbhayani.me/redis-internals/)

- https://github.com/spacejam/sled /rust/bw-tree
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
  - [Sled: Embedded Database Written in Rust | Hacker News](https://news.ycombinator.com/item?id=22375979)
    - LevelDB is a LSM database. 
    - LSM is generally better for write workloads over BTree DBs like LMDB and sled. LMDB also has a single writer restriction.

- https://github.com/JetBrains/xodus /java
  - a transactional schema-less embedded database
  - initially developed for JetBrains YouTrack, also used in JetBrains Hub
  - highly concurrent. Reads are completely non-blocking due to MVCC and true snapshot isolation.
  - written in pure Java and Kotlin.
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

- https://github.com/heineiuo/rippledb /MIT/ts/inactive
  - an embeddable key-value database engine in pure TypeScript, based on LSM-Tree, Inspired by LevelDB.

- https://github.com/belayeng/quadstore /MIT/ts
  - https://belayeng.github.io/quadstore
  - Quadstore is a LevelDB-backed RDF graph database / triplestore for JavaScript runtimes (browsers, Node.js, Deno, Bun, ...) written in TypeScript.
  - Implements the Sink, Source and Store RDF/JS interfaces for maximum interoperability with other RDF libraries
  - Supports SPARQL queries via quadstore-comunica, a tailored configuration and distribution of the Comunica querying framework
  - Natively capable of querying across named graphs

- https://github.com/lotusdblabs/lotusdb /go
  - LotusDB is a fast k/v database compatible with LSM tree and B+ tree, optimization of badger and bbolt.
  - Much lower read and space amplification(倍率，放大率) than typical LSM
  - LotusDB is inspired by a paper named SLM-DB in USENIX FAST ’19, and the Wisckey paper also helps a lot.

- https://github.com/skyzh/mini-lsm /rust
  - https://skyzh.github.io/mini-lsm/
  - Build a simple key-value storage engine in a week!
  - Log-structured merge tree is a data structure to maintain key-value pairs. 
  - This data structure is widely used in distributed database systems like TiDB and CockroachDB as their underlying storage engine. 
  - RocksDB, based on LevelDB, is an implementation of LSM-Tree storage engine.
  - For RB-Tree and B-Tree, all data operations are in-place. That is to say, when you update the value corresponding to the key, the value will be overwritten at its original memory or disk space. 
  - But in an LSM Tree, all write operations, i.e., insertions, updates, deletions, are performed in somewhere else. These operations will be batched into SST (sorted string table) files and be written to the disk. Once written to the disk, the file will not be changed. These operations are applied lazily on disk with a special task called compaction. The compaction job will merge multiple SST files and remove unused data.
- https://github.com/Fullstop000/wickdb
  - Pure Rust LSM-tree based embedded storage engine
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
# kv-based
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
    - Designed to allow partial sync of the data, but not quite implemented yet
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
# more-key-value
- https://github.com/pgte/alfred /201109/js
  - Alfred is a fast in-process key-value store for node.js.
  - atomic operations on one record
  - multiple key-value maps in one database
  - append-only files
