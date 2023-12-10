---
title: lib-db-pouchdb-couchdb-dev
tags: [couchdb, database, pouchdb]
created: 2022-12-02T11:12:38.058Z
modified: 2022-12-02T11:15:15.257Z
---

# lib-db-pouchdb-couchdb-dev

# guide

- pros
  - offlineable
  - CouchDB Replication Protocol
  - Custom Conflict Handling

- cons
  - 与couchdb耦合: data-model, database, sync protocol
    - 不必纠结于耦合度过高，sync protocol是公开的，可自行实现相关工具
  - pouchdb适合 one-db-per-user 的场景，跨user/db的搜索没有很好的解决方案
  - doc级别的权限管理没有最佳实践, Read access is on a per-database basis
    - 本地创建用户的问题
  - 数据初始化时可能处理超级大量数据的问题
  - 对二进制数据存储和同步的支持不够好，attachment的设计是针对image/html
  - 不支持transaction
  - js引擎基于firefox的SpiderMonkey
  - 不方便在服务端进行数据处理etl
  - Unlike most other databases, whenever you update a document in PouchDB or CouchDB, you must present the entire document along with its current revision marker.

- features
  - storage adapter: levelup, indexeddb

- who is using #pouchdb
  - ?
- who is using #couchdb
  - npm
  - budibase

- pouchdb-cons
  - no: Multi Tab Support, Observable Queries, Schema Support, Custom Backend
- watermelondb-cons
  - no: Custom Conflict Handling

- collab
  - 为db实现crdt的参考: piratedb, evolu/idbsidesync, triplitdb, indexeddb
  - 不必执着于寻找indexeddb的实现，很多时候只是作为一种持久化的方式

- couchdb vs git
  - git默认保存所有历史版本，couchdb默认会在compact/gc时删除旧版
  - git的冲突处理粒度为doc内的line/行，couchdb冲突处理粒度为doc
  - git的冲突可能需要手动处理，couchdb会自动选择一个作为解决冲突的结果

- tips
  - couchdb fauxton http://127.0.0.1:5984/_utils/

- roadmap
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav
  - alternative-backend: mysql/pg
  - kappa-architecture?
  - attachment/针对图片视频的blob二进制存储数据库: 参考 mongodb-gridfs, pg-lo

- database-features
  - standards: postgresql, sqlite, clickhouse, duckdb
  - persistence
  - indexing
  - query planner
  - query engine: sql or not?
  - replication
  - concurrency
  - conflicts
  - extensions/plugins: 参考sqlite、pg
  - search: fts, fuzzy
  - partial replication
  - auth: 权限控制的粒度，row/doc, column/property
  - arrow

- [CouchDB Best Practices](https://jo.github.io/couchdb-best-practices/)
  - https://github.com/jo/couchdb-best-practices
  - Apache CouchDB™ is a database that uses JSON for documents, JavaScript for MapReduce indexes, and regular HTTP for its API.

- pouchdb的同步协议参考 [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)

- community-pouchdb/couchdb
  - [Apache CouchDB Wiki - Confluence](https://cwiki.apache.org/confluence/display/COUCHDB/)
  - [Couchbase Forums](https://www.couchbase.com/forums/)
  - couchbase discord
  - couchdb(erlang): 使用b+tree
  - [IBM Cloudant](https://www.ibm.com/cloud/cloudant)
# draft
- nonsyncable/local-only tables for config/temporary-data
  - local documents解决了此问题

- auth
  - auth per-doc

- binary-attachment
  - video
  - 方案参考: sqlite-文本 + gridfs-文件
  - 实现类似mongodb-gridfs/pg-large-object/s3的系统，处理TB规模的文件，超大规模的文件建议自研方案
  - fossil受到sqlite对blob支持为最大2G的限制

- continue to rearchitect couchdb on top of foundationdb

- plugins
  - math/statistics
  - gis

- sqlite [Database File Format](https://www.sqlite.org/fileformat2.html)
  - 导出或直接兼容 sqlite格式
# dev

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
# changelog-couchdb
- [Release Notes — Apache CouchDB® Documentation](https://docs.couchdb.org/en/stable/whatsnew/index.html)

- v4.0_202x
- v3.0_202002
  - User-defined partitioned databases for faster querying
  - Live Shard Splitting for incremental scale-out
  - Automatic view index warmer
- v2.0_201609
  - Clustering
  - ✨ New Query Language: mango
  - 2.0 is the unification of BigCouch(Cloudant's work) with the old single node CouchDB
  - New Admin Interface (written in React): fauxton
- v1.0_201007
  - Faster implementation of pread_iolist().
  - Use O_APPEND to save lseeks.
  - Faster default view collation.
- v0.0_2005
  - first released in 2005 and later became an Apache Software Foundation project in 2008.
# more
