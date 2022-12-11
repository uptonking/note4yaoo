---
title: lib-db-nedb-dev
tags: [database, nedb]
created: 2022-11-27T19:20:09.883Z
modified: 2022-11-27T19:20:24.273Z
---

# lib-db-nedb-dev

# guide

- [node database comparisons](https://github.com/only-cliches/Nano-SQL/issues/48)
  - 比较db: nanoSQL, nedb, lokijs, LoveField, pouchdb, alaSQL
  - 比较项目: node/browser, dbms, undo/redo, events, indexeddb, orm, typescript
# nedb-roadmap
- 要支持浏览器和nodejs环境
  - indexeddb-fs

- persistence-adapter
  - bson
  - [Added pluggable storage](https://github.com/louischatriot/nedb/pull/427)

- 将所有数据放在内存改为可选
  - tingodb
  - nedb-logger

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

- 不支持事务 transaction
  - [atomic update + insert?](https://github.com/louischatriot/nedb/issues/398)

- 批量插入超大量数据会受浏览器限制
  - [Batch insert help](https://github.com/louischatriot/nedb/issues/62)
# codebase
- not-yet
  - bst, l398 if (!this.compareKeys(key, this.key) === 0) return; 这个写法很奇怪

- create database
  - new Datastore()，保存在内存中，内存数据模型就是Datastore
- add/update/remove
  - db.insertAsync([{ a: 5 }, { a: 42 }])
    - _addToIndexes
  - db.updateAsync(query, update, options)
    - modifiedDoc = model.modify(candidate, update);
    - 修改内存中数据 this._updateIndexes(modifications);
    - 修改持久化数据 this.persistence.persistNewStateAsync(newDocs);
  - db.removeAsync(query, options)
    - 更新内存 this._removeFromIndexes
    - 更新本地 this.persistence.persistNewStateAsync(removedDocs);
  - update和remove都依赖 _getCandidatesAsync
- index
  - new Index()
  - this.indexes[fieldName].insert(this.getAllData()); 
- find
  - findAsync(query, projection = {})
- count/operators
- persist

## Datastore/crud-api

## Index/Cursor

## Persistence/Storage

## more-nedb-src

- Executor 支持buffer和main两个执行队列
