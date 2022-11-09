---
title: toc-database-key-value-leveldb
tags: [database, key-value, leveldb, toc]
created: 2022-11-03T04:09:01.455Z
modified: 2022-11-03T04:14:00.563Z
---

# toc-database-key-value-leveldb

# guide

# db-key-value
- https://github.com/apple/foundationdb /Apache2/c++
  - a distributed database designed to handle large volumes of structured data across clusters of commodity servers.
  - It organizes data as an ordered key-value store and employs ACID transactions for all operations. 
  - It is especially well-suited for read/write workloads but also has excellent performance for write-intensive workloads.

- keyv /2kStar/MIT/202211/js
  - https://github.com/jaredwray/keyv
  - Simple key-value storage with support for multiple backends
  - Storage Adapters: etcd, mongodb, redis, sqlite
# leveldb-like
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
  - Many alternatives are available. For example, memory-level is an in-memory database backed by a red-black tree
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
# more-key-value
