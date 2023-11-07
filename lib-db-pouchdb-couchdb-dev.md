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

- features
  - storage adapter: levelup, indexeddb

- who is using #pouchdb
  - ?
- who is using #couchdb
  - npm
  - budibase

- alternatives
  - pouchdb server    /inactive
  - couchdb(erlang): 使用b+tree
  - [IBM Cloudant](https://www.ibm.com/cloud/cloudant)

- collab
  - 为db实现crdt的参考: piratedb, evolu/idbsidesync, triplitdb, indexeddb
  - 不必执着于寻找indexeddb的实现，很多时候只是作为一种持久化的方式

- tips
  - couchdb fauxton http://127.0.0.1:5984/_utils/

- roadmap
  - pouchdb + kappa-crdt +eav => pouchdb-crdt-eav
  - alternative-backend: mysql/pg
  - kappa-architecture?
  - 针对图片、视频的blob二进制存储数据库: 参考 mongodb-gridfs, pg-lo

- database-features
  - standards: postgresql, sqlite, clickhouse, duckdb
  - persistence
  - indexing
  - query planner
  - query engine: sql or not?
  - concurrency
  - replication
  - conflicts
  - search: fts, fuzzy
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
  - [pouchdb blog](https://pouchdb.com/blog/)
  - [couchdb blog](https://blog.couchdb.org/)
# draft
- nonsyncable/local-only tables for config/temporary-data
# dev

# changelog-pouchdb

- [Secondary indexes have landed in PouchDB_201405](https://pouchdb.com/2014/05/01/secondary-indexes-have-landed-in-pouchdb.html)
  - With the release of PouchDB 2.2.0, we're happy to introduce a feature that's been cooking on the slow simmer for some time: secondary indexes, a.k.a. persistent map/reduce.
  - it allows you to index anything in your JSON documents – not just the doc IDs.
  - the new API is modeled after CouchDB's
# changelog-couchdb
- [Release Notes — Apache CouchDB® Documentation](https://docs.couchdb.org/en/stable/whatsnew/index.html)

- v4.0_202x
- v3.0_202002
  - User-defined partitioned databases for faster querying
  - Live Shard Splitting for incremental scale-out
  - Automatic view index warmer
- v2.0_201609
  - Clustering
  - New Query Language: mango
  - 2.0 is the unification of BigCouch(Cloudant's work) with the old single node CouchDB
  - New Admin Interface (written in React): fauxton
- v1.0_201007
# more
