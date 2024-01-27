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

- https://github.com/worldbrain/storex /MIT/202205/ts/Memex/inactive
  - A modular and portable database abstraction ecosystem for JavaScript
  - Storex is a minimal storage layer as a foundation for easing common problems around storing and moving data around.
  - current officially supported back-ends are: dexie/sequelize/firestore
  - This project started as the storage layer for Memex, a tool to organize your web-research for yourself and collaboratively.
  - This has been powering Memex in production for over 3 years, facilitating our experiments with peer-to-peer sync 

- https://github.com/levelgraph/levelgraph /MIT/202108/js/inactive
  - LevelGraph is a Graph Database, built on the uber-fast key-value store LevelDB through the powerful LevelUp library. 
  - You can use it inside your node.js application or in any IndexedDB-powered Browser.
  - LevelGraph loosely follows the Hexastore approach, uses six indices for every triple

- https://github.com/fortunejs/fortune /202108/js
  - non-native graph database abstraction layer that implements graph-like features on the application-level for Node.js and web browsers. 
  - It provides a common interface for databases, as well as relationships, inverse updates, referential integrity, which are built upon assumptions in the data model.
  - By default, the data is persisted in memory (and IndexedDB for the browser). There are adapters for databases such as MongoDB, Postgres, and NeDB.
  - No object-relational mapping (ORM) or active record pattern, just plain data objects.
  - No coupling with network protocol, handle requests from anywhere.

- https://github.com/usegraffy/graffy /apache2/202310/js
  - https://graffy.org/
  - Live queries for graph-shaped data
  - Graffy supports complex, expressive live queries - with multiple levels of resource expansion and pagination - based on a novel application of set theory and CRDTs.
  - Graffy was inspired by (and borrows from) Facebook's GraphQL and Netflix's Falcor. Compared to GraphQL, Graffy offers a more familiar data model, true live queries and more efficient caching. Compared to Falcor, it provides cursor-based pagination and real-time subscriptions.

- https://github.com/apache/incubator-hugegraph /java
  - A graph database that supports more than 100+ billion data, high performance and scalability (Include OLTP Engine & REST-API & Backends)
  - Billions of vertices and edges can be easily stored into and queried from HugeGraph due to its excellent OLTP ability. 

- https://github.com/pegurnee/db4o /java/inactive
  - This is a repo for the java Versant Object-Oriented Database db4o.
  - Somebody please look at Actian's Versant Object Database (now called "Actian NoSQL") and just clone it. You'll make very big money.
  - [It's a shame that almost no one knows or uses Versant OODBMS | Hacker News](https://news.ycombinator.com/item?id=23784578)
    - As the name suggest it's object oriented and queries return graphs of objects.
    - It's heavily multi-threaded and has been around since 1989 (iirc).
    - The only big downside (besides being proprietary) is that it's almost impossible to scale out (horizontally). But it scales enormously well vertically (throw resources at it and it will happily use it in a very efficient manner).
  - [Ask HN: Which project does not have any good open-source alternatives? | Hacker News](https://news.ycombinator.com/item?id=21884828)
    - P.S. It fell out of favor because the systems that used it tended to be monoliths that did too much to scale well. 
    - The "right way to do it," IMHO is to build a central stateful brain with it, kick all asynchronous work out to stateless worker microservices and read from active secondaries. 
    - If the brain's only job is to mutate state by applying business logic, you can scale quite far.

- https://github.com/indradb/indradb /2kStar/MPLv2/202307/rust
  - A graph database written in rust.
  - IndraDB's original design was heavily inspired by TAO, facebook's graph datastore
  - JSON-based properties tied to vertices and edges.
  - Cross-language support via gRPC, or direct embedding as a library.
  - Pluggable underlying datastores, with several built-in datastores. Postgresql and sled are available separately.
# triplestore/rdf
- https://github.com/enterlab/simplegraph /java
  - Simple in-memory Graph Database/Cache (Triplestore): learn how a Graph DB works (educational, learner)
  - The SimpleGraph is implemented as a TripleStore, containing tuples (well, actually triples) of Subject, Object and Predicate.

- https://github.com/blazegraph/database /java
  - https://blazegraph.com/
  - a ultra high-performance graph database supporting Blueprints and RDF/SPARQL APIs
  - It supports up to 50 Billion edges on a single machine. 
  - It powers the Wikimedia Foundation's Wikidata Query Service.

- https://github.com/atomicdata-dev/atomic-server /587Star/MIT/202401/rust/ts
  - https://atomicserver.eu/
  - a lightweight, yet powerful CMS / Graph Database
  - powered by actix-web and sled database
  - Documents, collaborative, rich text, similar to Google Docs / Notion.
  - Tables, with strict schema validation, keyboard support, copy / paste support. Similar to Airtable.
  - Event-sourced versioning / history powered by Atomic Commits
  - Synchronization using websockets
  - Full-text search with fuzzy search and various operators, often <3ms responses. Powered by tantivy.
# graph-utils
- https://github.com/unum-cloud/networkxum /python
  - https://unum.am/storage
  - NetworkXum is NetworkX-like interface for large persistent graphs stored inside DBMS. 
  - This lets you upscale from Megabyte-Gigabyte graphs to Terabyte-Petabyte graphs (that won't fit into RAM), without changing your code. 
  - We provide wrappers for following DBs: mongodb/neo4j/sqlite/mysql/pg

- https://github.com/unum-cloud/ustore /cpp
  - Multi-Modal Database replacing MongoDB, Neo4J, and Elastic with 1 faster ACID solution, with NetworkX and Pandas interfaces, and bindings for C 99, C++ 17, Python 3, Java, GoLang

- https://github.com/kuzudb/kuzu /cpp
  - Embeddable property graph database management system built for query speed and scalability. 
  - Flexible Property Graph Data Model and Cypher query language
# more
- https://github.com/dpapathanasiou/simple-graph /sql
  - This is a simple graph database in SQLite, inspired by "SQLite as a document database"
  - The schema consists of just two structures: Nodes(json) and Edges({id:json})
  - There are also traversal function templates as native SQLite Common Table Expressions which produce lists of identifiers or return all objects along the path.
  - [SQLite as a document database_202006](https://dgl.cx/2020/06/sqlite-json-support)
