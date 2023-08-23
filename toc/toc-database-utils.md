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

- https://github.com/holepunchto/hypercore /js
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

- https://github.com/holepunchto/hyperbee /js
  - https://docs.holepunch.to/building-blocks/hyperbee
  - An append-only B-tree running on a Hypercore. 
  - It provides a key/value-store API, atomic batch insertions, and creating sorted iterators.
  - 依赖streamx、mutexify
  - It uses a single Hypercore for storage, using a technique called embedded indexing.
  - It provides features like cache warmup extension, efficient diffing, version control, sorted iteration, and sparse downloading.
  - As with the Hypercore, a Hyperbee can only have a single writer on a single machine

- https://github.com/holepunchto/hyperdrive /js
  - https://docs.holepunch.to/building-blocks/hyperdrive
  - a secure, real-time distributed file system designed for easy P2P file sharing. 

- https://github.com/tradle/multi-hyperbee /js
  - A LevelUP compatible leaderless multi-master database with eventual consistency, **using hyperbee + CRDT + HLC**. 
  - Similarly CockroachDB achieves replication on top of RocksDB, but here it is a pure P2P **streaming** database, with zero central management.
  - like all other low-level components of hypercore ecosystem it is a single-writer data structure. Multi-writer is a higher-level abstraction, hence the name multi-hyperbee.

### dat-ecosystem

- https://github.com/dat-ecosystem/dat
  - https://dat.foundation/
  - peer-to-peer sharing & live synchronization of files via command line
  - Use dat command line to share files with version control, back up data to servers, browse remote files on demand, and automate long-term data preservation
  - dat is the first application based upon the Hypercore Protocol, and drove the architectural design through iterative development between 2014 and 2017. T

## kappa-db

- https://github.com/kappa-db/kappa-core /ISC/202011/js/inactive
  - Minimal peer-to-peer database, based on kappa architecture.
  - kappa-core is built on an abstraction called a kappa architecture, or "event sourcing". 
    - This differs from the traditional approach to databases, which is centered on storing the latest value for each key in the database.
    - In contrast, **kappa architecture centers on a primitive called the "append-only log"** as its single source of truth.
    - Each entry in a log is addressable by its "sequence number" (starting at 0, then 1, 2, 3, ...). In the case of kappa-core, which uses hypercore underneath
  - kappa-core still uses tables like the above, though. 
    - However, instead of being the source of truth, these **tables are generated (or materialized) from the log data**, providing a view of the log data in a new or optimized context. 
    - These are called materialized views.
  - https://github.com/Frando/kappa-core

- https://github.com/arso-project/kappa-record-db /202005/js/inactive
  - A peer-to-peer database built on hypercores and kappa-core@experimental.
  - Index a set of hypercores efficiently into materialized-view style secondary indexes
  - Is developed for Sonar which adds full-text search, binary assets, an HTTP API, a CLI and a UI.
  - Internally, the database uses unordered-materialized-kv to have a shared notion of the latest versions of a record.
- https://github.com/arso-project/sonar /js/ts
  - https://sonar.arso.xyz/
  - A p2p content database and search engine

- https://github.com/kappa-db/multifeed /js
  - multi-writer hypercore
  - It solves the problem of hypercore only allowing one writer by making it easy to manage and sync a set of hypercores -- by a variety of authors -- across peers.
  - Replication works by extending the regular hypercore exchange mechanism to include a meta-exchange, where peers share information about the feeds they have locally, and choose which of the remote feeds they'd like to download in exchange. 
    - Right now, the replication mechanism defaults to sharing all local feeds and downloading all remote feeds.

- https://github.com/kappa-db/kappa-view-level /js
  - make kappa-core views over leveldb
  - inspired by https://github.com/flumedb/flumeview-level

- https://github.com/okdistribute/peerfs /js
  - multiwriter peer-to-peer filesystem, built on kappa-core and hyperdrive

- https://github.com/arso-project/hyper-content-db /201912/js/inactive
  - A Kappa-style peer-to-peer content database, on top of hyperdrives.

- https://gitlab.com/coboxcoop/kappa-drive
  - a peer-to-peer multiwriter filesystem.
  - Supports Hyperdrive V10. Originally known as 'peerfs'.
- https://gitlab.com/coboxcoop/drive
  - a wrapper for kappa-drive

## append-only-log

- https://github.com/flumedb/flumedb /MIT/202006/js/inactive
  - A modular database made for moving logs with streams.
  - Flume is a modular database comprised of an Append Only Log and Streaming Views on that log. 
  - This makes a star shaped pipeline - or rather, there is a pipeline from the log to each view, but the log is part of every pipeline.
# more
