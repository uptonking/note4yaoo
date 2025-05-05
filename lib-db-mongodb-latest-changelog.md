---
title: lib-db-mongodb-latest-changelog
tags: [changelog, mongodb]
created: 2023-01-02T08:23:24.229Z
modified: 2023-01-02T08:23:36.399Z
---

# lib-db-mongodb-latest-changelog

# guide

# changelog
- resources
  - [MongoDB - Wikipedia](https://en.wikipedia.org/wiki/MongoDB)
  - [MongoDB Evolved – Version History | MongoDB](https://www.mongodb.com/resources/products/mongodb-version-history)
  - [MongoDB Licensing | MongoDB](https://www.mongodb.com/legal/licensing/community-edition)
    - SSPL 20181016
    - AGPLv3 2018

## v8.0_202410

- With a design emphasis on enterprise-grade security, resilience, availability, and performance—including more than 45 architectural improvements and new features

- significantly improves performance by allowing applications to more quickly and efficiently query and transform data with up to 32% better throughput. 
  - Architectural optimizations in MongoDB 8.0 have reduced memory usage and query times.
- MongoDB Queryable Encryption is an industry-first innovation developed by MongoDB’s Cryptography Research Group that allows customers to encrypt sensitive application data, store it securely as fully randomized encrypted data in the MongoDB database, and run expressive queries on the encrypted data for processing.
- horizontal scaling is now faster and easier at a lower cost. 

- 
- 

## v7.0_202308

- major improvements across four key areas: Migrations, security, performance and developer experience.
- Migration operations are streamlined with updates to Cluster-to-Cluster Sync (mongosync)
- Security is reinforced with the general availability of Queryable Encryption
- Performance improvements include an advanced query execution strategy becoming the default for find() and prefix of aggregate() queries. 
- Updates to the Query API introduce bitwise operators, percentile operators, and user role variables in the Aggregation Framework

- 
- 

## v6.0_202207

- optimizations for time series collections; 
- improved support for event-driven architectures; 
- full support for sharded joins and graph traversal; 
- improvements to operational resilience and sharding; 
- and the ability to run expressive queries on fully randomized encrypted data.

- 
- 

## v5.0_202107

- native time series collections optimized for IoT and financial apps
- future-proofs versioned API: The MongoDB Stable API 
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
