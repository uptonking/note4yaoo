---
title: lib-db-datalog-examples
tags: [database, datalog, examples]
created: 2023-09-16T17:28:07.511Z
modified: 2023-09-16T17:28:29.873Z
---

# lib-db-datalog-examples

# guide

- resources
  - [OSS Clojure-Datalog Databases](https://clojurelog.github.io/)
  - https://github.com/simongray/clojure-graph-resources
    - a curated list of mostly mature and/or actively developed Clojure resources relevant for dealing with graph-like data
# popular
- https://github.com/fireproof-storage/fireproof /MIT/ts
  - https://use-fireproof.com/
  - Live database for the web
  - Simplify your application state with a live database. Automatically update your UI based on local or remote changes, and optionally integrate with any cloud for replication and sharing.
  - Fireproof is an embedded JavaScript document database designed to streamline app development. 
  - Data resides locally, with optional encrypted cloud storage and realtime collaboration. 
  - Features like live queries, database branches and snapshots, and file attachments make Fireproof ideal for browser-based apps big or small.
  - Fireproof has a unique take on distributed data integrity, rooted in immutable data and cryptographically verifiable protocols. 
  - The core Merkle hash-tree clock is based on Alan's Pail
  - Mikeal wrote the prolly trees implementation.
# datalog-db
- https://github.com/cozodb/cozo /MPLv2/rust
  - https://cozodb.org/
  - A transactional, relational-graph-vector database that uses Datalog for query.
  - a general-purpose, transactional, relational database that uses Datalog for query, is embeddable but can also handle huge amounts of data and concurrency, and focuses on graph data and algorithms. 
  - It supports time travel and it is performant!
  - you can run a complete CozoDB instance in your browser with wasm

- https://github.com/KnowledgeGarden/java-unidu-pire /apache2/java
  - [PIRE: An extensible IR engine based on probabilistic Datalog](https://www.researchgate.net/publication/225246464_PIRE_An_extensible_IR_engine_based_on_probabilistic_Datalog)
  - In terms of Datomic alternatives, the Pire Project was a well researched Distributed Datalog project written in Java by a German professor; the project had a few PubMed research papers using it. 
  - The project terminated when the professor was killed in a vehicular accident. I asked for and got permission to bring it to github [1]; 
  - we updated it to jdk 1.8 and tweaked the code a bit to move tests out of the core code. 
  - It is functional. 
  - Runs on several RDBMS platforms (not postgres) using config files.

- https://github.com/tonsky/datascript /EPLv1/clojure
  - An immutable in-memory database and Datalog query engine in Clojure and ClojureScript.
  - DataScript is meant to run inside the browser.
  - DataScript databases are immutable and based on persistent data structures. In fact, they’re more like data structures than databases (think Hashmap)

- https://github.com/replikativ/datahike /clojure
  - a durable Datalog database powered by an efficient Datalog query engine
  - This project started as a port of DataScript to the hitchhiker-tree.

- https://github.com/juji-io/datalevin /EPLv1/clojure
  - A simple, fast and versatile Datalog database
  - It is our observation that many developers prefer the flavor of Datalog popularized by Datomic® over any flavor of SQL, once they get to use it. 
  - Perhaps it is because Datalog is more declarative and composable than SQL, e.g. the **automatic implicit joins** seem to be its killer feature.
  - To keep things simple and familiar, Datalevin does not store transaction ids along with the datoms, and behaves the same way as most other databases: when data are deleted, they are gone.
  - Datalevin started out as a port of Datascript in-memory Datalog database to Lightning Memory-Mapped Database (LMDB). 
  - Independent from Datalog, Datalevin can be used as a fast key-value store for EDN data, with support for range queries, predicate filtering and more. 
    - Datalevin packages the underlying LMDB database as a convenient key-value store for EDN data.
  - Datalevin can also run in an event-driven networked client/server mode 

- https://github.com/xtdb/xtdb /MIT/clojure
  - Bitemporal and dynamic relational database for SQL and Datalog
  - a general purpose database with graph-oriented bitemporal indexes. 
  - Datalog, SQL & EQL queries are supported, and Java, HTTP & Clojure APIs are provided.
  - In addition to SQL, XTDB supplies a Datalog query interface that can be used to express complex joins and recursive graph traversals.
  - Crux is now XTDB

- https://github.com/quoll/asami /clojure
  - A graph database, for Clojure and ClojureScript.

- https://github.com/ribelo/doxa /clojure
  - a simple in-memory database, trying to copy the best solutions from datascript, xtdb, fulcro, autonormal and especially shadow-grove.

- https://github.com/mhuebert/re-db /clojure
  - a fast, reactive client-side triple-store for handling global state in ClojureScript apps. 
  - It is inspired by Datomic and DataScript and works in conjunction with Reagent.
# examples

# utils

# more
