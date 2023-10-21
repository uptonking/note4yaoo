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

- cons
  - 与couchdb耦合: data-model, database, sync protocol
  - pouchdb适合 one-db-per-user 的场景，跨user/db的搜索没有很好的解决方案
  - doc级别的权限管理没有最佳实践
  - 数据初始化时可能处理超级大量数据的问题
  - 本地创建用户的问题
  - 对二进制数据存储和同步的支持

- features
  - storage adapter: levelup, indexeddb

- alternatives
  - pouchdb server    /inactive
  - couchdb(erlang)
  - [IBM Cloudant](https://www.ibm.com/cloud/cloudant)

- collab
  - 为db实现crdt的参考: piratedb, evolu/idbsidesync, triplitdb, indexeddb
  - 不必执着于寻找indexeddb的实现，很多时候只是作为一种持久化的方式

- roadmap
  - alternative-backend: mysql/pg
  - kappa-architecture?

- pouchdb的同步协议参考 [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)
# dev

# more
