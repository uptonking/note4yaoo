---
title: lib-db-nedb-roadmap
tags: [nedb, roadmap]
created: 2022-12-16T15:40:46.028Z
modified: 2022-12-16T15:40:56.278Z
---

# lib-db-nedb-roadmap

# guide

- 基于idb的数据存取不使用字符串，使用arraybuffer

- 参考sqlite是如何解决并发读写的问题的
# nedb-roadmap
- compound-index
  - [Compound indexes](https://github.com/louischatriot/nedb/issues/93)
  - [Compound by rmanibus](https://github.com/louischatriot/nedb/pull/660)
  - [Added compound index](https://github.com/louischatriot/nedb/pull/208)

- query-operators
  - [added $first, $last, $before and $after query parameters](https://github.com/louischatriot/nedb/pull/148)
  - [Added .group() function](https://github.com/louischatriot/nedb/pull/153)

- [wrap a cursor in a readable stream](https://github.com/louischatriot/nedb/issues/465)

- persistence-adapter 要支持浏览器和nodejs环境
  - bson
  - [Added pluggable storage](https://github.com/louischatriot/nedb/pull/427)
  - [Persistence in Browser (localStorage)](https://github.com/louischatriot/nedb/pull/168)
  - [indexeddb backend](https://github.com/louischatriot/nedb/pull/223)
  - [indexedDB backend with localStorage fallback](https://github.com/louischatriot/nedb/pull/322)
  - [added support for Buffers (BLOB)](https://github.com/louischatriot/nedb/pull/167)

- 将所有数据放在内存改为可选
  - tingodb
  - nedb-logger

- [Listen to database changes](https://github.com/louischatriot/nedb/issues/175)

- 不支持同步

- 不支持全文搜索 full text search
  - 可参考 indexeddb, dexie, rxdb, pouchdb, ydn-db-fulltext
  - 类似mongodb的 $text 
  - [IndexedDB Full Text Search (Proof of Concept)](https://gist.github.com/inexorabletash/a279f03ab5610817c0540c83857e4295)

- undo/redo
  - [This page demonstrates how to use triggers to implement undo/redo logic for an application that uses SQLite](https://www.sqlite.org/undoredo.html)

- 不支持多线程访问，但有第三方扩展支持
  - [can multiple processes write to same db?](https://github.com/louischatriot/nedb/issues/479)

- 读取数据超过256mb时会抛出异常
  - [Stream files line by line when parsing to avoid memory limits](https://github.com/louischatriot/nedb/pull/463)

- 不支持以 read-only 的方式打开数据库

- 不支持事务 transaction
  - [atomic update + insert?](https://github.com/louischatriot/nedb/issues/398)

- 批量插入超大量数据会受浏览器限制
  - [Batch insert help](https://github.com/louischatriot/nedb/issues/62)
