---
title: toc-database-utils
tags: [database, lib, utils]
created: 2023-08-23T17:15:09.363Z
modified: 2023-08-23T17:15:46.484Z
---

# toc-database-utils

# guide

# utils

# distributed

# db-protocols/spec

## hypercore

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
  - This crate provides a low-level streaming API to hypercore-protocol and exposes an interface that should make it easy to implement actual protocol logic on top. This crate targets Hypercore 9 (Dat 2) only.
  - It uses `async-std` for async IO, and `snow` for the Noise handshake.

- https://github.com/RangerMauve/hyper-sdk /js
  - A Software Development Kit for the hypercore-protocol
  - Hypercore-protocol and it's ecosystem consists of a bunch of low level building blocks for working with data in distributed applications. Although this modularity makes it easy to mix and match pieces, it adds complexity when it comes to actually building something.

- https://github.com/holepunchto/hyperbee /js
  - https://docs.holepunch.to/building-blocks/hyperbee
  - An append-only B-tree running on a Hypercore. 
  - It provides a key/value-store API, atomic batch insertions, and creating sorted iterators.
  - 依赖streamx、mutexify
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

- https://github.com/fsteff/hyperobjects
  - Simple object store with transaction support, built on hypercore.
  - concurrent, atomic transactions

- https://github.com/rafapaezbas/hypercore-speed-tests
  - Test with Hypercore and Hyperbee

### dat-ecosystem

- refs-dat
  - [Dat Ecosystem](https://dat-ecosystem.org/)
  - https://dat-ecosystem-archive.github.io/how-dat-works/

- https://github.com/dat-ecosystem/dat /js
  - https://dat.foundation/
  - peer-to-peer sharing & live synchronization of files via command line
  - Use dat command line to share files with version control, back up data to servers, browse remote files on demand, and automate long-term data preservation
  - dat is the first application based upon the Hypercore Protocol, and drove the architectural design through iterative development between 2014 and 2017. T

## kappa-db

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

- https://github.com/arso-project/kappa-record-db /202005/js/inactive
  - A peer-to-peer database built on hypercores and kappa-core@experimental.
  - Index a set of hypercores efficiently into materialized-view style secondary indexes
  - Is developed for Sonar which adds full-text search, binary assets, an HTTP API, a CLI and a UI.
  - Internally, the database uses unordered-materialized-kv to have a shared notion of the latest versions of a record.
- https://github.com/arso-project/sonar /js/ts
  - https://sonar.arso.xyz/
  - A p2p content database and search engine

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
  - inspired by https://github.com/flumedb/flumeview-level

- https://github.com/ssbc/ssb-server /js
  - https://ssbc.github.io/ssb-server/
  - ssb-server is an open source peer-to-peer log store used as a database, identity provider, and messaging system. 
  - ssb-server **behaves just like a Kappa Architecture DB**. 
  - ssb-servers comprise(包含；构成) a global gossip-protocol mesh without any host dependencies.

- https://github.com/okdistribute/peerfs /js
  - multiwriter peer-to-peer filesystem, built on kappa-core and hyperdrive

- https://github.com/arso-project/hyper-content-db /201912/js/inactive
  - A Kappa-style peer-to-peer content database, on top of hyperdrives.

- https://gitlab.com/coboxcoop/kappa-drive
  - a peer-to-peer multiwriter filesystem.
  - Supports Hyperdrive V10. Originally known as 'peerfs'.
- https://gitlab.com/coboxcoop/drive
  - a wrapper for kappa-drive

- https://github.com/eliquious/kappa /go
  - an implementation of the Kappa Architecture written in Go.
  - https://github.com/blacklabeldata/kappa

- https://github.com/ouyi/kafka-flink-demo /java
  - A demo application implementing the Kappa architecture, based on Kafka, Flink, and ELK.

- https://github.com/hkwi/osara /python
  - micro-framework on top of kafka / kappa architecture

- [Kappa Architecture - Where Everything Is A Stream · java-design-patterns](https://github.com/iluwatar/java-design-patterns/issues/892)

- [kappa architecture vs event sourcing](https://github.com/tschudin/ssb-icn2019-paper/issues/6)

- [Kappa Architecture - A big data engineering approach](https://pradeepl.com/blog/kappa-architecture/)

## append-only-log

- https://github.com/ssbc/async-append-only-log /js
  - A new append-only-log for SSB purposes
  - This module is heavily inspired by flumelog-aligned-offset. It is an attempt to implement the same concept but in a simpler fashion
  - A log consists of a number of blocks, that contain a number of records. A record is simply it's length, as a 16-bit unsigned integer, followed by the data bytes. 
  - This module is not compatible with flume without a wrapper around stream as it uses the same terminology as JITDB and ssb-db2 of using offset for the byte position of a record instead of seq.
- https://github.com/ssbc/jitdb /js
  - A database on top of async-append-only-log with automatic index generation and maintenance.
  - Async append only log takes care of persistance of the main log. It is expected to use bipf to encode data.
  - JITDB lazily creates and maintains indexes based on the way the data is queried.
    - JITDB lazily creates and maintains indexes based on the way the data is queried.
    - Specific indexes will only updated when it is queried again. These indexes are tiny compared to normal flume indexes.
  - For this to be feasible it must be really fast to do a full log scan. 
    - It turns out that the combination of push streams and bipf makes streaming the full log not much slower than reading the file.

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

- https://github.com/digidem/unordered-materialized-kv /js/inactive
  - materialized view key/id store based on unordered log messages
  - This library presents a familiar key/value materialized view for append-only log data which can be inserted in any order. 
  - This library implements a multi-register conflict strategy, so each key may map to more than one value. To merge multiple values into a single value, point at more than one ancestor id.
  - This library is useful for kappa architectures with missing or out of order log entries, or where calculating a topological ordering would be expensive
  - This library does not store values itself, only the IDs to look up values. This way you can use an append-only log to store your primary values without duplicating data.

- https://github.com/flumedb/flumedb /MIT/202006/js/inactive
  - A modular database made for moving logs with streams.
  - Flume is a modular database comprised of an Append Only Log and Streaming Views on that log. 
  - This makes a star shaped pipeline - or rather, there is a pipeline from the log to each view, but the log is part of every pipeline.
# more
