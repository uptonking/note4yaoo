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
- https://github.com/datalogui/datalog /110Star/MIT/202206/ts/inactive
  - https://datalogui.dev/
  - An implementation of Datalog with a focus on managing UIs & UI state.
  - Differential updates. Only run queries on the differences in data. Don't run the query on everything every time.
  - Run queries on the results of your queries. It's queries all the way down.
  - Works with React.

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

- https://github.com/dpapathanasiou/simple-graph /sql
  - This is a simple graph database in SQLite, inspired by "SQLite as a document database"
  - The schema consists of just two structures: Nodes(json) and Edges({id:json})
  - There are also traversal function templates as native SQLite Common Table Expressions which produce lists of identifiers or return all objects along the path.
  - [SQLite as a document database_202006](https://dgl.cx/2020/06/sqlite-json-support)
# query-datalog
- datomic-alternative
  - clojure: datascript, xtdb, datahike, datalevin

- https://github.com/d4hines/datalog-ts
  - A tiny (<100 LOC), toy implementation of Datalog in Typescript
  - https://github.com/stopachka/datalogJS /js

- https://github.com/smallhelm/level-fact-base /js
  - Store immutable "facts" in level and query them with datalog.
  - level-fact-base is inspired by Datomic. Also check out datascript.

- https://github.com/ccorcos/datalog-prototype /ts
  - This is a full-stack prototype of collaborate web application backed by a Datalog-inspired database.

- https://github.com/alexwarth/roomdb /js
  - a Datalog-style database inspired by the implementation of the Dynamicland project. 
  - It enables programmers to represent facts using natural language, with a syntax adapted from my `NL-Datalog` project.

- https://github.com/rust-lang/datafrog /rust
  - a lightweight Datalog engine intended to be embedded in other Rust programs.
  - https://github.com/frankmcsherry/datafrog
    - [A relatively simple Datalog engine in Rust](https://github.com/frankmcsherry/blog/blob/master/posts/2018-05-19.md)
    - In this post we will build up a relatively concise Datalog engine: DataFrog.
    - One of the design goals is that simple or not, there should be little enough in the way of someone coming to understand how it all works
    - [A relatively simple Datalog engine | Hacker News_201805](https://news.ycombinator.com/item?id=17107527)

- https://github.com/vilterp/datalog-ts /ts
  - a datalog interpreter in typescript

- https://github.com/the-kenny/hellschreiber /rust
  - Experiments in writing a SQLite backed database similar to Datomic.

- https://github.com/knowsys/nemo /rust
  - a datalog-based rule engine for fast and scalable analytic data processing in memory.
  - Nemo's data model aims at compatibility with RDF/SPARQL while preserving established logic programming conventions and features.
  - Rules: datalog dialect with support for existential rules (tuple-generating dependencies), stratified negation, and datatypes (including numeric comparison and arithmetic functions)

- https://github.com/ekzhang/crepe /rust
  - Datalog compiler embedded in Rust as a procedural macro
  - a library that allows you to write declarative logic programs in Rust, with a Datalog-like syntax. 
  - It provides a procedural macro that generates efficient, safe code and interoperates seamlessly with Rust programs.

- https://github.com/wernsey/Jatalog /java
  - a Datalog implementation in Java. 
  - It provides a parser for the language and an evaluation engine to execute queries that can be embedded into larger applications.
  - The engine implements semi-naive, bottom-up evaluation.
  - It implements stratified negation; Technically, it implements the Stratified Datalog¬ language[ceri].
  - It can parse and evaluate Datalog programs from files and Strings (actually anything that implements java.io. Reader).
  - It implements "=", "<>" (alternatively "!="), "<", "<=", ">" and ">=" as built-in predicates.
  - It avoids third party dependencies.
  - The class Shell implements a REPL command-line interface.
  - I remember that doing the stratified negation was quite complex and I won't be able to explain it of the top of my head anymore.
# datalog-db
- https://github.com/cozodb/cozo /MPLv2/rust
  - https://cozodb.org/
  - A transactional, relational-graph-vector database that uses Datalog for query.
  - a general-purpose, transactional, relational database that uses Datalog for query, is embeddable but can also handle huge amounts of data and concurrency, and focuses on graph data and algorithms. 
  - It supports time travel and it is performant!
  - you can run a complete CozoDB instance in your browser with wasm
  - [Show HN: Cozo – new Graph DB with Datalog, embedded like SQLite | Hacker News_202211](https://news.ycombinator.com/item?id=33518320)

- https://github.com/KnowledgeGarden/java-unidu-pire /apache2/java
  - [PIRE: An extensible IR engine based on probabilistic Datalog](https://www.researchgate.net/publication/225246464_PIRE_An_extensible_IR_engine_based_on_probabilistic_Datalog)
  - In terms of Datomic alternatives, the Pire Project was a well researched Distributed Datalog project written in Java by a German professor; the project had a few PubMed research papers using it. 
  - The project terminated when the professor was killed in a vehicular accident. I asked for and got permission to bring it to github [1]; 
  - we updated it to jdk 1.8 and tweaked the code a bit to move tests out of the core code. 
  - It is functional. 
  - Runs on several RDBMS platforms (not postgres) using config files.

- https://github.com/sqwishy/owoof /rust
  - A program for querying and modifying information in a datalog-like format backed by SQLite.
  - A glorified query-builder inspired by Datomic that uses a datalog-like format for querying and modifying information around a SQLite database.
  - This is a pet project and probably shouldn't be used for anything serious.

- https://github.com/mozilla/mentat /rust/inactive
  - https://mozilla.github.io/mentat/
  - A persistent, relational store inspired by Datomic and DataScript
  - Mentat is intended to be a flexible relational (not key-value, not document-oriented) store that makes it easy to describe, grow, and reuse your domain schema.
  - Just like DataScript, Mentat speaks Datalog for querying and takes additions and retractions as input to a transaction.
  - Unlike DataScript, Mentat exposes free-text indexing, **thanks to SQLite**.
  - Mentat was designed for embedding, initially in an experimental Electron app 
  - Mentat uses partial indices, which are available in SQLite 3.8.0 and higher
  - forks
  - https://github.com/qpdb/mentat

- https://github.com/leostera/pachadb /rust
  - an embeddable, immutable, graph, edge database.
  - edge database means you can run it on edge providers like Cloudflare
  - graph database means that the data in Pacha is stored as tiny little facts that form a huge graph of knowledge(entity-relation-values)
  - Pacha uses Datalog instead of SQL for queries. Since the data in Pacha forms a Graph, Datalog is a much easier way to query for it.

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
  - [Datalevin is good, but its more useful in the same realm as sqlite | Hacker News](https://news.ycombinator.com/item?id=31127793)
    - Not exactly. My goal of developing Datalevin is to replace our use of both Datomic and Postgres, so we have a single DB. 
    - The aim is to provide a versatile(多用途的，多功能的) database that meets data needs of most use cases.

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
- https://github.com/ekzhang/percival /MIT/rust/ts/svelte
  - https://percival.ink/
  - Percival is a declarative data query and visualization language. 
  - It provides a reactive, web-based notebook environment for exploring complex datasets, producing interactive graphics, and sharing results.
  - Percival combines the flexibility of Datalog as a query language for relational data with the beauty of exploratory visualization grammars.
# utils
- https://github.com/austinbirch/reactive-entity /clojure
  - A reactive version of DataScript’s d/entity API for your Reagent components.
  - This library allows you to use a reactive version of DataScript entities directly in your Reagent components, re-rendering those components only when the exact attributes they depend on are updated.

- https://github.com/wotbrew/relic /clojure
  - a Clojure(Script) data structure that provides the functional relational programming model described by the tar pit paper.
## rules

- https://github.com/cerner/clara-rules /clojure
  - a forward-chaining rules engine written in Clojure(Script) with Java interoperability. 
  - It aims to simplify code with a developer-centric approach to expert systems. 

- https://github.com/oakes/odoyle-rules /clojure
  - A rules engine for Clojure(Script)
  - O'Doyle stores data in id-attribute-value tuples like [::player ::health 10] whereas Clara (by default) uses Clojure records
# more
