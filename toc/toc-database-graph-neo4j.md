---
title: toc-database-graph-neo4j
tags: [database, graph, toc]
created: 2022-11-03T04:12:00.024Z
modified: 2022-11-03T04:49:42.587Z
---

# toc-database-graph-neo4j

# guide

- blogs
  - [一文了解各大图数据库查询语言（Gremlin vs Cypher vs nGQL）| 操作入门篇 - 知乎](https://zhuanlan.zhihu.com/p/110995885)
# db-graph
- https://github.com/neo4j/neo4j  /java
  - the world’s leading Graph Database
  - Neo4j offers orders of magnitude performance benefits compared to relational DBs.

- https://github.com/belayeng/quadstore /MIT/ts
  - https://belayeng.github.io/quadstore
  - Quadstore is a LevelDB-backed RDF graph database / triplestore for JavaScript runtimes (browsers, Node.js, Deno, Bun, ...) written in TypeScript.
  - Implements the Sink, Source and Store RDF/JS interfaces for maximum interoperability with other RDF libraries
  - Supports SPARQL queries via quadstore-comunica, a tailored configuration and distribution of the Comunica querying framework
  - Natively capable of querying across named graphs

- https://github.com/worldbrain/storex /MIT/202205/ts/inactive
  - A modular and portable database abstraction ecosystem for JavaScript
  - Storex is a minimal storage layer as a foundation for easing common problems around storing and moving data around.
  - This project started as the storage layer for Memex, a tool to organize your web-research for yourself and collaboratively.
  - current officially supported back-ends are: dexie/sequelize/firestore

- https://github.com/levelgraph/levelgraph /202108/js
  - LevelGraph is a Graph Database, built on the uber-fast key-value store LevelDB through the powerful LevelUp library. 
  - You can use it inside your node.js application or in any IndexedDB-powered Browser.
  - LevelGraph loosely follows the Hexastore approach, uses six indices for every triple

- https://github.com/fortunejs/fortune /202108/js
  - non-native graph database abstraction layer that implements graph-like features on the application-level for Node.js and web browsers. 
  - It provides a common interface for databases, as well as relationships, inverse updates, referential integrity, which are built upon assumptions in the data model.
  - By default, the data is persisted in memory (and IndexedDB for the browser). There are adapters for databases such as MongoDB, Postgres, and NeDB.
  - No object-relational mapping (ORM) or active record pattern, just plain data objects.
  - No coupling with network protocol, handle requests from anywhere.

- https://github.com/apache/incubator-hugegraph /java
  - A graph database that supports more than 100+ billion data, high performance and scalability (Include OLTP Engine & REST-API & Backends)
  - Billions of vertices and edges can be easily stored into and queried from HugeGraph due to its excellent OLTP ability. 
