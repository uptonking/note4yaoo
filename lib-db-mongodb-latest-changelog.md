---
title: lib-db-mongodb-latest-changelog
tags: [changelog, mongodb]
created: 2023-01-02T08:23:24.229Z
modified: 2023-01-02T08:23:36.399Z
---

# lib-db-mongodb-latest-changelog

# guide

# changelog
- [MongoDB Licensing | MongoDB](https://www.mongodb.com/legal/licensing/community-edition)
  - SSPL 20181016
  - AGPLv3 2018

## v7.0_202307

## v6.0_202207

## v5.0_202107

- time series support
- future-proofs versioned API
- client-side field level encryption
- live resharding

## v4.0_201806

- transactions
- license change effective pr. 4.0.4

## v3.0_201503

- pluggable storage engine API
- WiredTiger storage engine support
- MongoDB Ops Manager

## v2.4_201303

- 支持 text search
  - [Enable Text Search — MongoDB Manual](https://www.mongodb.com/docs/v2.4/tutorial/enable-text-search/)
  - [$text — MongoDB Manual](https://www.mongodb.com/docs/manual/reference/operator/query/text/)
- switch to V8 JavaScript engine

## v2.0_201109

## v1.0_200908

# discuss
- ## [mongoDB 4.0(201806)支持事务了，还有多少人想用MySQL呢？ - 知乎](https://www.zhihu.com/question/279843849)
- mongodb不支持子查询，类似于mysql语句。Select * from orders where orders.sellerid in (select eid from employee where employee.state= 'California'), mongodb做不到。
- 另外联表查询也不友好

- ## [Difference between createIndex() and ensureIndex() in java using mongodb](https://stackoverflow.com/questions/25968592)
- since version > 3.0.0: `db.collection.ensureIndex()` is now an alias for `db.collection.createIndex()` .
