---
title: lib-db-pouchdb-dev-couch
tags: [couchdb, database, pouchdb]
created: 2022-12-02T11:12:38.058Z
modified: 2024-01-04T06:53:04.003Z
---

# lib-db-pouchdb-dev-couch

# guide

- pros
  - offlineable
  - CouchDB Replication Protocol
  - Custom Conflict Handling

- cons
  - 与couchdb耦合: data-model, sync protocol, database-features
    - 不必纠结于耦合度过高，sync protocol是公开的，可自行实现相关工具
  - pouchdb适合 one-db-per-user 的场景，跨user/db的搜索没有很好的解决方案
  - doc级别的权限管理没有最佳实践, Read access is on a per-database basis
  - 同步协议非常chatty，不适合实时协作，改进方案可参考bonsaidb
  - filtered replication待改进, 过滤计算scale困难
  - 不支持与非couchdb的数据库同步，但可参考event-sourcing自己实现
  - pouchdb擅长同步，但对实时协作的支持不如websocket，不支持awareness
  - 本地创建用户时如何同步/合并数据
  - 初始化时处理超级大量数据很慢的问题
  - 对二进制数据存储和同步的支持不够好，attachment的设计是针对image/html
  - 不支持transaction
  - js引擎基于firefox的SpiderMonkey
  - 不方便在服务端进行数据处理etl
  - Unlike most other databases, whenever you update a document in PouchDB or CouchDB, you must present the entire document along with its current revision marker.
  - The problem with couchdb is that it does one request per document which makes the protocol slow for browser based applications also it has no http2 support
  - 针对大量数据的查询或全文搜索很难在client实现，需要一种在client选择计算发生在客户端还是服务端的逻辑

- features
  - sync between db
  - http and rest
  - storage adapter: levelup, indexeddb
  - pouchdb擅长离线编辑再同步的场景，而不是高性能的实时协作

- who is using #pouchdb
  - CHT/Community Health Toolkit
- who is using #couchdb
  - npm
  - budibase

- watermelondb-cons
  - no: Custom Conflict Handling
- pouchdb-cons
  - no: Multi Tab Support, Observable Queries, Schema Support, Custom Backend

- collab
  - couchdb和crdt集成的思路，couchdb作为event-sourcing的数据源，基于此计算数据视图
  - 为db实现crdt的参考: piratedb, evolu/idbsidesync, triplitdb, indexeddb
  - 不必执着于寻找indexeddb的实现，很多时候只是作为一种持久化的方式

- couchdb vs git
  - git默认保存所有历史版本，couchdb默认会在compact/gc时删除旧版
  - git的冲突处理粒度为doc内的line/行，couchdb冲突处理粒度为doc
  - git的冲突可能需要手动处理，couchdb会自动选择一个作为解决冲突的结果

- tips
  - couchdb fauxton http://127.0.0.1:5984/_utils/
  - couchdb(erlang): 使用b+tree
  - couchdb更专注于tp，对于重分析类查询可参考主流olap解决方法，传统关系型数据库也是这么做的，将数据导入ap数据库再分析

- local-first-db的案例
  - 常用chat作为示例: scuttlebutt > manyverse/MPLv2, hypercore > keet/NonOpen, triplitdb > beeper, kappa > cabal/AGPLv3

- roadmap
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav: 参考triplitdb
  - kappa-architecture?
  - partial-replication: 参考hypercore
  - sync: couchbase sync gateway; 与minimongo+mongodb的方案比较; 可参考event-sourcing自己实现
  - attachment/针对图片视频的blob二进制存储数据库: 参考couchbase, mongodb-gridfs, pg-lo
  - alternative-backend: mysql/pg

- database-features
  - standards: postgresql, sqlite, clickhouse, duckdb
  - crdt for conflicts resolution
  - version-history: undo/redo
  - partial-replication/selective-sync
  - ivm: incremental view maintenance
  - reactive-query: dexie, tinybase
  - db-per-user: pouchdb, sqlite
  - sync-protocol: websocket
  - auth/permission: 权限控制的粒度，row/doc, column/property
  - offline persistence
  - integrations/apps: excel, notes
  - indexing
  - query planner
  - query engine: sql or not?
  - replication
  - concurrency
  - conflicts
  - extensions/plugins: 参考sqlite、pg
  - search: fts, fuzzy
  - arrow
  - end-to-end encryption

- community-pouchdb/couchdb
  - [Apache CouchDB Wiki - Confluence](https://cwiki.apache.org/confluence/display/COUCHDB/)
  - [Couchbase Forums](https://www.couchbase.com/forums/)
  - couchbase discord
  - [IBM Cloudant](https://www.ibm.com/cloud/cloudant)
  - [couchdb-user-archive - Google Groups](https://groups.google.com/g/couchdb-user-archive)
# draft
- nonsyncable/local-only tables for config/temporary-data
  - local documents解决了此问题

- auth
  - auth per-doc

- binary-attachment
  - 方案参考: sqlite-文本 + gridfs-文件
  - 实现类似mongodb-gridfs/pg-large-object/s3的系统，处理TB规模的文件，超大规模的文件建议自研方案
  - video
  - fossil受到sqlite对blob支持为最大2G的限制

- continue to rearchitect couchdb on top of foundationdb

- plugins
  - math/statistics
  - gis

- usecase
  - bookmark/tags

- sqlite [Database File Format](https://www.sqlite.org/fileformat2.html)
  - 导出或直接兼容 sqlite格式

- couchapp
  - reimplement with wasm
# dev
- > By design, CouchDB and PouchDB do not support transactions. A document is the smallest unit of operations.
# changelog-pouchdb
- [v8.0.0_202212](https://pouchdb.com/2022/12/14/pouchdb-8.0.0.html)
  - ✨ Embracing modern ES6 + JS syntax
  - PouchDB now has `activeTasks` like couchdb
  - Add `purge` to the indexeddb adapter
- [v7.0.0_201806](https://pouchdb.com/2018/06/21/pouchdb-7.0.0.html)
  - drop WebSQL from our default builds
  - Removed Promise Polyfill
  - Switch to fetch
  - use the documents contents to determine its revision
- [v6.0.0_201609](https://pouchdb.com/2016/09/05/pouchdb-6.0.0.html)
  - Remove new PouchDB(dbName).then
  - Remove extras API, extracted out into separate packages
  - Remove SQLite Plugin support
- [v5.0.0_201510](https://pouchdb.com/2015/10/06/pouchdb-5.0.0-five-years-of-pouchdb.html)
  - Implement `bulkGet()`.
- [v4.0.0_201508](https://pouchdb.com/2015/08/03/pouchdb-4.0.0-ballast-overboard.html)
  - Return Blobs (or Buffers) in get() + allDocs() + changes() + query() with {binary: true}. 
  - Remove `onChange` and `complete` callbacks; use the EventEmitter-style `changes()`,  `replicate()` and `sync()`.
  - Allow chaining of plugin registration
- [v3.0.0_201408](https://pouchdb.com/2014/08/12/pouchdb-3.0.0.html)
  - `_local` documents are now unversioned in the underlying backend for better map/reduce performance
  - MD5 hashes are now calculated incrementally in a way that won't freeze the DOM
  - You can no longer rely on errors to have an identifying name. Instead, rely on CouchDB-centric errors to have a status
- [v2.2.0_201405](https://pouchdb.com/2014/05/01/pouchdb-2.2.0.html)
  - ✨ secondary indexes, a.k.a. persistent map/reduce
  - `.changes()` API switched to an EventEmitter
- v0.0_201006
# more
