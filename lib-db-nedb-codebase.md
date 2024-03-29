---
title: lib-db-nedb-codebase
tags: [codebase, nedb]
created: 2022-12-16T15:40:30.768Z
modified: 2022-12-16T15:40:42.527Z
---

# lib-db-nedb-codebase

# guide

## not-yet

- Executor 支持buffer和main两个执行队列，为什么buffer队列也是立即执行？

- bst, l398 if (!this.compareKeys(key, this.key) === 0) return; 这个写法很奇怪
  - 测试表明，可删掉
# 浏览器版
- 基于localforage实现nedb的web版
  - 一个Datastore/collection对应indexeddb中的一个objectStore，key是文件名，value是对应的node版文件内容(数据+索引)
  - 但nedb浏览器版的一个Datastore的内容只有一个value，而不是一个文档对象对应一行
  - minimongo的示例对应idb中的单张表+多行数据
# api

## Datastore/crud-api

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
  - 1. _getRawCandidates: basic/$in/compare
  - 2. remove all expired documents

## Index

- index
  - new Index()
  - this.indexes[fieldName].insert(this.getAllData()); 
  - 操作大多通过 this.tree

## query

- findAsync(query, projection = {})
  - 直接通过游标实现 new Cursor()

- count/operators

## Cursor

- 在索引上查找并返回

- 使用cursor的api
  - countAsync
  - findAsync、findOneAsync
  - _updateAsync

## Persistence/Storage

- persistence
  - serialize > afterSerialization > appendFileAsync

- persistCachedDatabaseAsync
  - 数据+索引序列化 > afterSerialize > crashSafeWriteFileLinesAsync
  - 全量覆盖

- ensureIndex时，会appendFile

## more-nedb-src
