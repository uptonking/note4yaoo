---
title: lib-db-pouchdb-examples-couchdb
tags: [couchdb, database, examples, pouchdb, toc]
created: 2022-11-30T18:55:16.304Z
modified: 2023-09-28T20:35:56.153Z
---

# lib-db-pouchdb-examples-couchdb

# guide

- pouchdb适合开发无需服务端的应用
  - 可参考admin模版项目，将状态管理操作替换为pouchdb操作
  - 可参考mongodb的案例如cms，然后将crud替换为pouchdb操作

- fans-p/couchdb
  - https://github.com/daleharvey/pouchbase
  - https://github.com/nolanlawson/pouchdb-find
    - https://news.ycombinator.com/threads?id=nolanl
  - https://github.com/redgeoff/delta-pouch
  - https://github.com/janl/couchdb-test-couchjs
  - https://github.com/jo/couchdb-best-practices
  - https://github.com/glynnbird/couchimport
  - https://github.com/gr2m/couchdb-excel-import

- resources
  - [Pouchdb Plugins and External Projects](https://pouchdb.com/external.html)
  - [Couchbase Open Source Projects](https://developer.couchbase.com/open-source-projects/)
# popular
- https://github.com/pubkey/client-side-databases
  - https://pubkey.github.io/client-side-databases/database-comparison/index.html
  - I have implemented the exact same chat application with different database technologies.
  - The chat app is a web based angular application, with functionality similar to Whatsapp Web.
  - PouchDB with IndexedDB adapter & CouchDB replication
  - RxDB PouchDB with PouchDB Storage & GraphQL replication
  - RxDB LokiJS with LokiJS Storage & GraphQL replication
  - RxDB Dexie.js with Dexie.js Storage & GraphQL replication
  - WatermelonDB with LokiJS adapter (no backend sync atm)
  - This is a fork of Nolan Lawsons Database Comparison. This fork behaves equally, but it uses a new transaction for each database write
  - https://github.com/nolanlawson/database-comparison
  - https://github.com/nolanlawson/database-comparison-worker-pouch

- https://github.com/ezpaarse-project/dbbench /201412/archived
  - A basic benching tool to compare node.js embedded databases
  - It inserts randomly generated objects with string identifiers, then queries random identifiers for a given period of time.

- https://github.com/AugurProject/pouchdb-perf /201911/ts
  - https://augurproject.github.io/pouchdb-perf/
  - PouchDB Perf Test

- couchdb /5.5kStar/apache2/202211/erlang
  - https://github.com/apache/couchdb
  - https://couchdb.apache.org/
  - Seamless multi-master syncing database with an intuitive HTTP/JSON API, designed for reliability
  - CouchDB is a database that completely embraces the web. 
    - Store your data with JSON documents. 
    - Access your documents with your web browser, via HTTP. 
    - Query, combine, and transform your documents with JavaScript. 
    - You can distribute your data, efficiently using CouchDB’s incremental replication.
    - CouchDB comes with a suite of features, such as on-the-fly document transformation and real-time change notifications
  - [CouchDB Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html)
    - Couch Replication Protocol is implemented in a variety of projects and products that span every imaginable computing environment from globally distributed server-clusters, over mobile phones to web browsers.
  - https://github.com/apache/couchdb-nano
    - The official Apache CouchDB library for Node.js
  - https://github.com/couchbase/couchdb

- pouchdb /16kStar/apache2/202310/js/core代码量不大
  - https://github.com/pouchdb/pouchdb
  - https://pouchdb.com/
  - PouchDB is an open-source JavaScript database inspired by Apache CouchDB that is designed to run well within the browser.
  - It enables applications to store data locally while offline, then synchronize it with CouchDB and compatible servers when the application is back online
  - PouchDB is not a self-contained database; 
    - it is a CouchDB-style abstraction layer over other databases. 
    - PouchDB supports all modern browsers, using IndexedDB under the hood
    - In Node.js, PouchDB uses LevelDB under the hood, and also supports many other backends via the LevelUP ecosystem.
  - The main benefit is to be able to replicate data with any CouchDB compatible endpoint. 
    - Because of the CouchDB compatibility, PouchDB has to do a lot of overhead in handling the revision tree of document, which is why it can show bad performance for bigger datasets.
    - RxDB was originally build around PouchDB until the storage layer was abstracted out in version 10.0.0(202107)
    - PouchDB has some performance issues because of how it has to store the document revision tree to stay compatible with the CouchDB API.
  - [how to to do partial (descending)l sync? F.e. chat messages](https://github.com/pouchdb/pouchdb/issues/8221)
    - You can use filtered replication
  - forks
  - https://github.com/emtee40/pouchdb-js
  - https://github.com/Passionate-Solver-Technologies/pouchdb-with-attachment /202310

- pouchdb-server /894Star/apache2/201907/js/内存/sqlite
  - https://github.com/pouchdb/pouchdb-server
  - PouchDB Server is a drop-in replacement for CouchDB, using PouchDB and Node.js.
  - 依赖pouchdb、bluebird、couchdb-render、express、xhr2
  - PouchDB Server can run fully in-memory (no changes are saved)
    - Or it can run using SQLite rather than LevelDB
  - 🧐 It is modeled after the single-node design of CouchDB 1.x, although it contains some CouchDB 2.x features such as Mango queries.
  - PouchDB Server is much less battle-tested than CouchDB, but it does pass the full PouchDB test suite.
  - PouchDB Server is a standalone REST server that implements the CouchDB API, while using a LevelDB-based PouchDB under the hood. It also supports an --in-memory mode and any LevelDOWN adapter
  - [Replication stream endpoint](https://github.com/pouchdb/pouchdb-server/issues/175)
    - The goal is to replace the existing replication algorithm with a less chatty protocol. Thoughts?
    - We have discussed this at CouchDB Dev Summit and for now our hypothesis is that Http/2 solves most of these issues
  - forks
  - https://github.com/VislaLabs/pouchdb-server /202308
    - Move dependencies to express-pouchdb package, sqlite3.v5
  - https://github.com/qiaogaojian/contribute_pouchdb-server /202209
    - upgrade to sqlite5
  - https://github.com/mitchmyburgh/pouchdb-server /202111
    - remove pouch-promise
  - https://github.com/grengojbo/pouchdb-server /201809
    - express-pouchdb began to rewrite code in the style of es6
    - Added minimal JWT auth
  - https://github.com/the-t-in-rtf/pouchdb-server /201909
    - forked for the purposes of publishing a scoped version of express-pouchdb and pouchdb-auth.
  - https://github.com/cognition-app/pouchdb-server /202003/js
    - Use lerna for monorepo management
- https://github.com/gr2m/spawn-pouchdb-server /202103/js
  - Configurable per-app pouchdb-server as a drop-in replacement for CouchDB
  - Simplify development setup. Having a built-in PouchDB-Server in our apps will make CouchDB optional.
  - Isolated CouchDB configurations
  - https://github.com/gr2m/pouchdb-security
    - fork of pouchdb-security package, fixes pouchdb-server#97
- https://github.com/demon24ru/PouchDB-server-test /202112/js
  - pouchdb-adapter-websql-core + SQLite
  - https://github.com/demon24ru/PouchDB-websql-SQLite-server
  - https://github.com/demon24ru/PouchDB-server-test-proxy
    - pouchdb proxy with JWT authentication

- https://github.com/mmalecki/crdt-couchdb /MIT/201308/js
  - A subclass of `crdt` lib which sources data from CouchDB and updates them in real-time. 
  - It supports pre-fetching of views and filtering of changes with CouchDB filters (using changes).
  - https://github.com/dominictarr/crdt /MIT/201403/js
    - Commutative Replicated Data Types for easy collaborative/distributed systems.
    - 提供了简单和复杂多个示例

- delta-pouch /184Star/apache2/201706/js
  - https://github.com/redgeoff/delta-pouch
  - Conflict-free collaborative editing for PouchDB
  - A PouchDB plugin for partial updates that uses the **every-doc-is-a-delta** storage pattern. 
  - You can use delta pouch to enable conflict-free collaborative editing of the same docs.
  - Delta pouch stores every change as a doc.
  - [Question: a helpful link describing the "every-doc-is-a-delta storage pattern"?](https://github.com/redgeoff/delta-pouch/issues/53)
    - Sounds like "every-doc-is-a-delta" is another way of saying "log database". Is that right?
    - I would look up anything related to "Event Sourcing" which perhaps is a superset of this idea. Basically, the idea is that you save the events that happen in your system and then compile those into views.
  - forks
  - https://github.com/Brainsway-Cloud/delta-pouch /201802
  - [Doesn't play nice with Pouch Find](https://github.com/redgeoff/delta-pouch/issues/175)
    - https://github.com/funblaster22/delta-pouch-find/tree/bulkGet

- https://github.com/couchapp/couchapp /201808/python2
  - https://couchapp.readthedocs.io/en/latest/intro/what-is-couchapp.html
  - Utilities to make standalone CouchDB application development simple
  - CouchApp is a set of scripts and a jQuery plugin designed to bring clarity and order to the freedom of CouchDB's document-based approach.
  - Also, be sure to checkout our Erlang-based sibling, erica.
  - A CouchApp is just a JavaScript and HTML5 app that can be served directly to the browser from CouchDB, without any other software in the stack
  - CouchDB is an HTTP server, capable of serving HTML directly to the browser. It is also a database designed from the ground up for horizontal scalability. 

- https://github.com/perfood/couch-auth /63Star/MIT/202311/ts
  - CouchAuth is a full-featured NodeJS/Express user authentication solution for APIs and Single Page Apps (SPA) using CouchDB or Cloudant.
  - This is a heavily modified SuperLogin, re-written in TypeScript and developed with Node 14/16 & CouchDB 3.
  - compatible with Cloudant when using the CouchDB-style authentication, adapted for current OWASP best practises and can be used on CloudFoundry.
  - Authentication solution for APIs, sPAs and Offline-First CouchDB powered Apps
  - Supports local login with username/email and password using best security practices
  - I'm only actively working on / testing the local email/PW authentication strategy, not for the OAuth part. 

- https://github.com/cheminfo/rest-on-couch /202309/js
  - Interface to CouchDB that allows the control of permissions on the documents.
  - https://github.com/cheminfo/rest-on-couch-client

- https://github.com/IconCMO/pouch-datalog /js/inactive
  - Datomic-like Datalog queries for PouchDB
  - The query engine is a fork from Datascript.
  - 依赖datascript
  - https://github.com/IconCMO/datascript
    - An immutable in-memory database and Datalog query engine in ClojureScript.
  - https://github.com/dahjelle/dataquery
    - Forked the query language from Datascript, and changed to only utilize external indexes in an asynchronous manner.

- hoodie /4.3kStar/apache2/202101/js/inactive
  - https://github.com/hoodiehq/hoodie
  - [How Hoodie Works](https://github.com/hoodiehq/hoodie/blob/master/docs/about/how-hoodie-works.rst)
  - The Offline First JavaScript Backend
  - hoodie can be used standalone or as a hapi plugin. 
  - Hoodie is using `PouchDB` for its in-browser storage.
  - Hoodie uses PouchDB for storing data locally. Hoodie saves all data here first, before doing anything else.
  - Hoodie relies on CouchDB. We use it to sync data back and forth between the server and the clients
  - So Hoodie does `client ↔ database ↔ server` instead of the traditional `client ↔ server ↔ database`, and this is where many of its superpowers come from.
  - [Project status?](https://github.com/hoodiehq/hoodie/issues/900)
    - not actively maintained, sorry.
  - [any plan for php port of the backend ?](https://github.com/hoodiehq/hoodie/issues/899)
    - A Store API which is compatible with CouchDB's database-level APIs
    - An Account API 
  - https://github.com/hoodiehq/pouchdb-users
    - PouchDB plugin to simulate CouchDB’s _users database behavior

- https://github.com/cloudless-hq/atreyu /apache2/202311/js/svelte
  - https://atreyu.dev/docs/
  - an edge- and serviceworker first metaframework for personal, data centric web applications. 
  - 依赖pouchdb
  - It supports real time data sync, offline usage and values minimal boilerplate with opt in to most features.
  - Falcor is used for state management, caching, batching and data sharing.
  - Svelte views are bound to a virtual data object with a js proxy based store implementation
  - ipfs as a local asset server and content addressable storage system, ipfs is not required for production sites and is not required to run in a p2p mode

- https://github.com/olafura/PouchFlux /201508/js
  - Flux with PouchDB

- https://github.com/serby/save /143Star/ISC/202209/js
  - A simple CRUD based persistence abstraction for storing objects to any backend data store. eg. Memory, MongoDB, Redis, CouchDB, Postgres, Punch Card etc.

- https://github.com/paperhive/octonom /201802/ts
  - General-purpose models and collections with multi-database support, written in TypeScript
  - Collections are specific to the database you use (e.g. MongoCollection, CouchCollection)
- https://github.com/genbliz/mocody /202303/ts/wip
  - Implementation of single table design, and unified query access for MongoDB, CouchDB, and dynamoDB
  - https://github.com/genbliz/mocody/tree/add-pouchdb

- https://github.com/Agrejus/db-framework-plugin-pouchdb /202311/ts
  - https://github.com/Agrejus/db-framework /202311/ts
  - Db Framework is a TypeScript first ORM designed to wrap existing database frameworks such as PouchDB to augment its functionality.
  - Inspired by . NET's Entity Framework, Db Framework operates the same way and tries to keep method names as close as possible.
  - Install a db provider: pouchdb, memory, localStorage.
  - https://github.com/Agrejus/db-framework-plugin-memory
  - https://github.com/Agrejus/pouchdb-entity-fabric /202209/ts
    - PouchDB ORM modeled after .net's Entity Framework

- https://github.com/KorbinianKuhn/pouchoose /202101/ts
  - Mongoose-like API for PouchDB.
  - Heavily work in progress
  - Powerful queries based on PouchDB-Find
- https://github.com/kidrecursive/mongoose-couch /201303/js
  - Mongoose ODM for CouchDB
- https://github.com/jfelsinger/couch-cushion /201506/js
  - A Node.js ODM for Couchbase
  - Documents in couch-cushion are represented as an instance of a model. Models are defined via a schema. The schema setup is loosely based off of that in mongoose.

- https://github.com/thaibault/couchdb-web-node-plugin /202311/ts
  - A database server, model instance conflict handler, rest api, authentication, session management, schema validator and model relation guarantee for webNode.
  - PouchDB with model specification/checking, user authentication and right management as web-node plugin.
  - https://github.com/thaibault/web-node /ts
    - A generic web backend configuration and plugin management.
    - a high level javaScript backend plugin system and configuration merger.
  - https://github.com/thaibault/clientnode /ts
    - The main goal of this plugin is providing an generic interface logic like controller for calling instance methods or getting property values of an object orientated designed plugin. 
    - A set of reusable logic elements for building gui components is integrated as well.

- https://github.com/hyper63/hyper-adapter-pouchdb /202311/js
  - A Data port adapter that uses PouchDB in the hyper service framework
  - https://github.com/hyper63/hyper-adapter-couchdb
    - A Data port adapter that uses CouchDB in the hyper service framework
  - https://github.com/hyper63/hyper-adapter-queue
    - in memory queue for local usage
    - This adapter uses an in-memory queue and is designed to work with local hyper services or services with small workloads.
  - https://github.com/hyper63/hyper-adapter-sqlite
  - https://github.com/hyper63/hyper-adapter-fs
  - https://github.com/hyper63/hyper-adapter-minisearch

- https://github.com/NoteSelf/NoteSelf.github.io /119Star/BSD/202005/js/inactive
  - https://noteself.org/
  - https://NoteSelf.github.io
  - built on top of TiddlyWiki, a powerful, free, highly customizable and open-source personal wiki.
  - 依赖tiddlywiki5、tw-pouchdb
  - We took the best of it, it's powerful customization system, and mixed it with one of the best embedded databases available, PouchDb, to bring in the synchronization capabilities you need.
  - This TiddlyWiki-variant stores documents in the browser (pouchdb) and can sync to a couchdb-server.
# couch-like
- microcouch-js /3Star/apache2/202209/js
  - https://github.com/jo/microcouch-js
  - A minimal Pouch-like implementation of a CouchDB compatible in-browser couch, for educational purpose.
  - Data model is the same as PouchDBs new `indexeddb` adapter.
  - Microcouch uses PouchDBs `pouchdb-merge` module.
  - Microcouch is quiet small, currently less than 30kB minified. It is about five times smaller and replicates almost ten times faster than PouchDB, depending on the document structure.
- https://github.com/jo/microcouch-rs /202302/rust/wip
  - A minimal Pouch-like implementation of a CouchDB compatible embeddable couch.
  - The design was worked out in the JavaScript microcouch and this Rust version will follow it.
  - https://github.com/jo/rouchdb /202204/rust
    - Minimal CouchDB compatible database written in Rust.
    - Very basic replication between two HTTP dbs works
- https://github.com/jo/minip /201805/js
  - a simple database that can replicate with CouchDB.
  - MemoryP - in memory store
  - HttpP - talks to a real CouchDB. only works with CouchDB 2 (relies on _bulk_get).
  - No changes feed. No views. Almost no error handling. No deletes. No checkpointing.

- https://github.com/DrGomi/OuchDB /202006/ts
  - shameless copy of the most basic PouchDB functionality

- https://github.com/mikeal/couchup /201307/js
  - A CouchDB implementation on top of levelup.
  - The goal is to build a data model well suited for mobile applications that may need to work offline and sync later on and maintain smart client side caches. 
  - The goal is to build a data model well suited for mobile applications that may need to work offline and sync later on and maintain smart client side caches. 
  - This data model is inspired by CouchDB but diverges greatly in the way it handles and resolves the revision history and conflicts. 
  - couchup implements a "most writes wins" conflict resolution scheme and does not require or even allow user specific conflict resolution.
  - modular. This repository only implements the base document storage layer. Indexes, attachments and replicators are implemented as additional modules
  - The tradeoffs couchup has made in revision tree storage along with some other simple optimizations mean that couchup already has better write performance than CouchDB and the same consistency guarantees.

- https://github.com/janl/jscouch /159Star/apache2/201202/js/作者团队
  - An interactive CouchDB tutorial based on a partial re-implementation of CouchDB in JavaScript

- https://github.com/garrensmith/couch_hack_week /202005/rust/foundationdb/inactive
  - An implementation of CouchDB using Rust and FoundationDB for Cloudant's hackweek.
  - The aim was to be able to read `/{db}/_all_docs`.
  - [MiniCouchDB in Rust_202006](https://www.garrensmith.com/minicouchdb-in-rust/)

- https://github.com/arve0/build-your-own-couchdb /202311/rust
  - https://arve0.github.io/build-your-own-couchdb/
  - Build your own modern CouchDB with Rust
  - Bindings for SQLite is available through the rusqlite crate
  - I want "real time" replication to IndexedDB, which is unpleasant with regular CouchDB. The unpleasantness is mainly due to the revision mechanism, which is fairly Erlang specific. Revisions hashes are calculated using Erlang data structures and md5, both which are not native in browsers. Of course it is possible to achieve the revision calculation with some extra libraries. Still, I think it will be a fun challenge to implement a modern CouchDB variant
  - Non goals: Compatibility with CouchDB; Writing low level code; Extensive server side logic, like index lookup and design documents

- https://github.com/jrawsthorne/couchbase-rs /1Star/NALic/202309/rust/提交多
  - Unofficial Reimplementation of Couchbase Server in Rust
  - https://github.com/jrawsthorne/libcouchbase-rs /202106/rust
    - Play around with the Couchbase protocol in Rust
    - Currently, every second, this inserts a document, gets that document, asserts it is equal, deletes it, gets again and asserts it's None
  - https://github.com/krsanty02/couchbase /java/1commit

- https://github.com/khonsulabs/bonsaidb /918Star/MIT/202311/rust
  - https://bonsaidb.io/
  - A programmable document database inspired by `CouchDB` written in Rust.
  - ACID-compliant, transactional storage of Collections
  - Role-Based Access Control (RBAC)
  - Local-only access, networked access via QUIC, or networked access via WebSockets
  - [Introducing PliantDb](https://ecton.dev/introducing-pliantdb/)
  - [Renamed from PliantDb to BonsaiDb_202107](https://github.com/khonsulabs/bonsaidb/commit/aa4e236ce4e527077b1842921fa98cc2a9f126af)
  - [Branch support](https://github.com/khonsulabs/nebari/issues/29)
    - For BonsaiDb we plan on supporting the replication logic at the BonsaiDb level, and we are hoping to support bi-directional replication with customizable conflict resolution. 
    - This is a form of branching, because you can clone a database using replication, modify it, and then eventually replicate again in either direction.
  - [Project Status_202301](https://github.com/khonsulabs/bonsaidb/issues/262)
    - July 2022: I wrote an overview of my goals of Sediment, a storage layer I am planning on sitting below Nebari, which BonsaiDb uses for the underlying database implementation
    - August 2022: I get Sediment to the point of benchmarking, I went and did the same benchmark against PostgreSQL and discovered that PostgreSQL outperformed them all. Why? It turns out Write-ahead logging is the fastest way to get incoming writes to disk.
    - December 2022: I've begun a rewrite of Sediment due to changing some of my goals now that there is a WAL in front of the storage layer. It's still early in development.
    - One serious thought I still have is whether Nebari should exist, or whether BonsaiDb should just use another database format.
  - [Refactor Views to utilize Nebari's B-Tree_202110](https://github.com/khonsulabs/bonsaidb/issues/76)
    - With our approach to storage in Sled, there was no actual tree to latch onto for the reduce/re-reduce functionality. 
    - The net effect of this change for the histogram example is that the internal tree would be responsible for reducing the samples, allowing for fewer calculations for any given query.
  - https://github.com/khonsulabs/nebari /MIT/rust
    - A pure Rust database implementation using an append-only B-Tree file format.
    - This crate provides the Roots type, which is the transactional storage layer for BonsaiDb. It is loosely inspired by `Couchstore`.
    - The major downside of append-only formats is that deleted data isn't cleaned up until a maintenance process occurs: compaction.

- https://github.com/nlfiedler/mokuroku /apache2/202309/rust/rocksdb
  - Secondary indices for RocksDB in Rust.
  - designed to provide a secondary index on top of the RocksDB key/value store, similar to what PouchDB does for LevelDB.
  - Your application will provide implementations of the `Document` trait to suit the various types of data to be stored in the database, and this library will invoke the mapping function on those Document instances to produce index key/value pairs.
  - The behavior of this library is similar to PouchDB, albeit(虽然；尽管) with an API suitable for the language. 
  - Unlike PouchDB, this library does not put any constraints on the format of the database records.
  - You may see the term `view` used here and there. This is what CouchDB and PouchDB call the indices in their documentation. 
    - The function name `emit` also comes from the `map/reduce` API of CouchDB, and makes as much sense as anything else.
  - What this library does exactly: the indices managed by this library are "stand-alone", meaning they are not embedded within the database files (e.g. zone maps or bloom filters). Additionally, the index is updated in a lazy fashion

- https://github.com/glynnbird/postdblite /202303/js
  - PostDB is proof-of-concept database that exposes a Apache CouchDB-like API but which is backed by a SQLite database. 
  - It does not implement CouchDB's MVCC, Design Documents, attachments, MapReduce, "Mango" search or any other CouchDB feature.
- https://github.com/glynnbird/postdb /apache2/202011/js/pg/inactive
  - A CouchDB-like database that uses PostgreSQL as the storage engine.
  - PostDB is proof-of-concept database that exposes a Apache CouchDB-like API but which is backed by a PostgreSQL database.
  - It does not implement CouchDB's MVCC, Design Documents, attachments, MapReduce, "Mango" search or any other CouchDB feature.
  - It does however provide a "consistent" data store where the documents and secondary indexes are in lock-step. Documents are limited to 100KB in size.
  - Optionally, PostDB nodes can be run in readonly mode and configured to read data from PostgreSQL read replicas to scale out read performance.
- https://github.com/glynnbird/postfdb /201908/js
  - proof-of-concept database that exposes a Apache CouchDB-like API but which is backed by a FoundationDB database
  - It does not implement CouchDB's MVCC, Design Documents, attachments, MapReduce, "Mango" search or any other CouchDB feature.

- https://github.com/kowsik/memcouchd /201103/js
  - a pure JavaScript in-memory implementation of some aspects of CouchDB with a nodejs/connect Web front-end.

- https://github.com/demsking/fakecouch /202101/ts/inactive
  - A fake CouchDB server for testing.
  - a fake CouchDB server which implements endpoints used in common applications.
  - It does not claim to be use as a regular CouchDB server. 
  - It uses some static data as result for some database requests.

- https://github.com/chris-l/mock-couch /201807/js
  - http://chris-l.github.io/mock-couch/
  - A node.js module designed to mock a CouchDB server, mostly for unit testing purposes.

- https://github.com/AndyA/shootingstick /1Star/apache2/202210/ts
  - A CouchDB clone
  - 依赖sqlite、express、lodash

- https://github.com/pgte/dribbledb /201112/js/inactive
  - MVCC database written in javascript
  - a browser local store capable of remote syncing.
  - It supports several storage strategies and remote pushing and pulling strategies.
  - It works with CouchDB-style APIs and a lot more to come.

- https://github.com/jacwright/restdb /201211/js
  - A RESTful database: inspired by CouchDB, built with JavaScript, on Node.js, backed by leveldb

- https://github.com/marten-de-vries/chairdb /python/inactive
  - A small CouchDB-compatible database with sync support

- https://github.com/fiatjaf/summadb /go/inactive
  - A hierarchical database that stores computed values.
  - For more fine-grained permissions and other features I'm also developing a small Go database compatible with PouchDB
  - https://github.com/fiatjaf/summuladb
    - A SummaDB that runs in the browser.

- https://github.com/ondra-novak/sofadb /201903/cpp
  - CouchDB inspired document database written in C++. In planning state
- https://github.com/RipcordSoftware/AvanceDB /201810/cpp
  - An in-memory database based on the CouchDB REST API and containing the CouchDB Futon and Fauxton web sites
  - If you are currently using CouchDB and struggle with view build times, then AvanceDB should be a seamless replacement for your view workload.
  - AvanceDB is not designed to replace CouchDB for document storage. 
  - The core is written in C++ 11 with Boost and map/reduce executed by an embedded SpiderMonkey JSAPI instance

- https://github.com/jchris/booth /201003/ruby/js
  - Booth is an implementation of CouchDB in Ruby. It's meant as an illustration of CouchDB as a protocol.
  - CouchDB uses a robust append only B-Tree implementation for storage

- https://github.com/delta-db/deltadb /201602/js/inactive
  - DeltaDB is an offline-first database designed to talk directly to clients and works great offline and online.
  - Stores all data as a series of deltas, which allows for smooth collaborative experiences even in frequently offline scenarios.
  - I have decided to suspend development of DeltaDB for the following reasons:
    - last-write-wins policy is nice when starting a new project as it is automatic, but other conflict resolution policies that force the user to manually resolve the conflict, like CouchDB’s revision protocol, have become more of the standard in the offline-first world.
    - Building a DB that scales and is Building a DB that scales and is distributed over many nodes, takes a lot of work.

- https://github.com/couchbase/couchstore /BSL/202312/c/cpp
  - couchbase storage file library
  - Couchstore is a low-level KV library that has a couple of unique features that we needed when building couchbase.
  - append-only (doesn't change stuff from the past).
  - indexed by change (and allows iteration since a particular change).
  - The file format is relatively simple 
  - Currently this library can only be built as part of Couchbase Server due to dependencies on the Couchbase Platform Library and Couchbase Server CMake project

- https://github.com/couchbase/couchbase-lite-core /202310/cpp/c
  - Cross-platform C++ core library for Couchbase Lite
# sync/collab
- resources
  - [(Alpha) PouchDB integration for Yjs](https://gist.github.com/samwillis/1465da23194d1ad480a5548458864077)
    - [Distributed offline editing with couch/pouchdb - Yjs Community_202101](https://discuss.yjs.dev/t/distributed-offline-editing-with-couch-pouchdb/340)
  - [Inline attachment Blob ignored during deterministic _rev generation resulting in _rev hash collision](https://github.com/pouchdb/pouchdb/issues/8257)

- https://github.com/alxndrsn/pouch-replication-exploration /201601/js
  - https://alxndrsn.github.io/pouch-replication-exploration/
  - Exploration of pouchdb replication

- pouchdb-sync-to-anything /43Star/MIT/201807/js
  - https://github.com/karlwestin/pouchdb-sync-to-anything
  - This is a plugin that lets you use CouchDBs replication algorithm with checkpointing, resuming, etc, but provide your own function to write the documents. 
  - This can be used to sequentially write updates to a REST API, 
  - 👉🏻 This is a partial implementation of the CouchDB replication protocol. 
    - It allows you to use PouchDB's tools to save replication checkpoints for syncing with your API. 
    - Using those checkpoints, we can start the next replication from the last good checkpoint.
  - Using this works best for one way data-flows only. If you're interested in a 2-way data flow, consider syncing data from the server to a different PouchDB instance, and write changes that are to be sent to the server separately.

- https://github.com/eigenfunctor/doc-sync /201912/ts
  - https://www.eigenfunctor.io/doc-sync/
  - a library that leverages Typescript and Pouchdb/CouchDB to enforce a synchronized document model between the browser and Node.js

- https://github.com/WoelkiM/AutoCouch /MIT/202004/ts/inactive/automerge
  - AutoCouch is a TypeScript framework to create object-oriented CRDTs that supports a simple way of distribution.
  - Database is a simplified wrapper of a PouchDB that allows getting and putting documents.
  - 📕 [AutoCouch: a JSON CRDT framework_202004](https://www.researchgate.net/publication/340954717_AutoCouch_a_JSON_CRDT_framework)
    - AutoCouch is a JSON framework combining the benefits of the Automerge CRDT library and CouchDB
  - [AutoCouch: A JSON CRDT Framework — Pascal Grosch - YouTube_202004](https://www.youtube.com/watch?v=D2_irGwRpjc)
  - https://github.com/WoelkiM/Polly_React_Example_AutoCouch
    - an example for a React app using AutoMerge
  - https://github.com/automerge/hypermerge /201911/ts/基于log实现crdt的思路

- https://github.com/jo/pouch-resolve-conflicts /201803/js
  - plugin to assist in PouchDB conflict resolving.

- https://github.com/garbados/pouchdb-hypercore /apache2/202007/js
  - Synchronize PouchDB or CouchDB with P2P Hypercores
  - A PouchDB plugin that maps records in hypercores, a P2P append-only datastructure, to a PouchDB or CouchDB instance. 
  - The plugin allows you to follow changes in hypercores locally and remotely.
  - https://github.com/calvinmetcalf/pouch-dat

- https://github.com/RangerMauve/pouchdb-adapter-hyperbee /202103/js
  - https://github.com/RangerMauve/pouchdb-hyperbee-example
  - Adapter for PouchDB to load p2p data from Hyperbee

- https://github.com/garbados/pouchdb-orbit /201802/js
  - An OrbitDB plugin for PouchDB that adds some methods for P2P replication

- https://github.com/garbados/pouchdb-cabal /js
  - Interact with Cabal using PouchDB
  - Comparable to cabal-core

- https://github.com/CoMfUcIoS/socket.io-pouch /201811/js
  - PouchDB and CouchDB over WebSockets, using Socket.io
- https://github.com/redgeoff/couchdb-howler /201803/js
  - Use web sockets to subscribe to CouchDB global changes

- https://github.com/yldio/pouch-websocket-sync /201606/js
  - PouchDB live sync through websockets
  - Sync several PouchDBs through websockets.
  - Supports reconnection, negotiation and authentication.
  - https://github.com/yldio/pouch-websocket-sync-example
    - Example "Todo-MVC" application of using pouch-websocket-sync together with React and Redux, keeping local database in sync with remote.

- https://github.com/pgte/pouch-stream-server /201511/js
  - PouchDB stream server. Serves generic PouchDB object streams.
  - Tested against PouchDB version 5.
  - https://github.com/yldio/pouch-remote-stream
    - Consume a remote PouchDB stream.
  - https://github.com/yldio/pouch-stream-multi-sync
    - Sync several PouchDBs through a stream.
  - https://github.com/calvinmetcalf/PouchStream
    - use some streams with your pouches
  - https://github.com/conor-mac-aoidh/express-pouchdb-replication-stream
    - An express endpoint for streaming bulk couchdb changes to pouchdb.

- https://github.com/yldio/pouch-clerk /201607/js
  - PouchDB worker reacting to document changes.
  - A clerk listens to changes in one or more PouchDB databases and react to document state changes.
  - https://github.com/yldio/pouch-clerk-example-app

- https://github.com/redgeoff/spiegel /MIT/202303/js
  - Scalable replication and change listening for CouchDB
  - Spiegel was designed to provide scalable replication and change listening for Quizster, a photo-based feedback and submission system.

- https://github.com/pouchdb-community/pouchdb-replication-stream /202307/js
  - Replicate PouchDB/CouchDB databases with Node.js-style streams
  - you can replicate two databases by just attaching the streams together
- https://github.com/pouchdb-community/pouchdb-load /201607/js
  - Load documents into CouchDB/PouchDB from a dumpfile
  - This method is typically much faster than standard replication, because it uses fewer HTTP requests. So it's a great way to quickly load an initial state for your database.

- https://github.com/pietervandereems/PeerPouch /201501/js/webrtc
  - A plugin for PouchDB which allows a remote PouchDB instance to be used locally. 
  - It transfers data over WebRTC, for simple lower-latency remote access and even particularly peer-to-peer replication!
  - fork of https://github.com/natevw/PeerPouch /201311/js/inactive
- https://github.com/scottmtp/pouch-replicate-webrtc /201510/js
  - Replicate a PouchDB over a WebRTC DataChannel, for NodeJS and the Browser.

- https://github.com/pouchdb/pouchbase /201604/js
  - PouchBase is a service that lets your PouchDB applications easily provide login and online sync functionality.
- https://github.com/daleharvey/pouchbase /201605/js
  - a test server for PouchDB, it provides open online databases that you can use to test PouchDB sync with.
  - Data stored here is publically available and is pediodically deleted, please do not use for anything other than testing.

- https://github.com/pouchdb-community/pouchdb-full-sync /201607/js
  - Fully replicate two PouchDB or CouchDB databases, while preserving absolutely all document history and conflicts.
  - Useful for: Implementing infinite undo/redo in your app
  - Normally, the CouchDB replication protocol only replicates the leafs between two databases. 
    - This preserves conflicts (which is awesome!), but it discards non-leafs for performance reasons.
  - Notice that all the revisions are kept, even the non-leafs. 

- https://github.com/sagarb3/Sync-Service-Pouch /201901/js
  - Sync Service Implemented on Top Of Pouch Db , (Mongo->Pouch->Indexeddb)

- https://github.com/redgeoff/replicate-couchdb-cluster /201803/js
  - A fault-tolerant way to replicate an entire CouchDB cluster

- https://github.com/IBM/couchbackup /202311/js
  - a command-line utility that allows a Cloudant or CouchDB database to be backed up to a text file. 
  - couchbackup does not do CouchDB replication as such, it simply streams through a database's _changes feed
  - couchbackup does not support backing up or restoring databases containing documents with attachments. It is recommended to store attachments directly in an object store. 

- https://github.com/vrtmrz/self-hosted-livesync-server /shell
  - CouchDB Server which configured about CORS for Obsidian and Self-hosted LiveSync.
  - Automatically set up SSL Certificates by Let's Encrypt (With Caddy).

- https://github.com/couchbase/sync_gateway /BSL/202312/go
  - https://www.couchbase.com/products/sync-gateway
  - Manages access and synchronization between Couchbase Lite and Couchbase Server

- https://github.com/neoandray/pouchsync /202307/js
  - Sync local pouch database with remote Mongo server and React snapshots

- https://github.com/redgeoff/pouchdb-persist /201410/js
  - pouchdb-persist was created when there were no similar options in pouchdb. 
  - Instead, use the live replication settings in pouchdb.

- https://github.com/Stwissel/couchdb-replication-graph /202312/js
  - Visualizing replication of CouchDB

- https://github.com/iriscouch/follow /apache2/201709/js
  - Very stable, very reliable, NodeJS CouchDB _changes follower
  - This looks much like the request API

- https://github.com/dominictarr/level-couch-sync /201509/js
  - Replicate couchdb data into leveldb in real time with follow. Must be used with sublevel.

- https://github.com/dominictarr/couch-sync /201111/js
  - this is like following a view
  - couch-sync requests a view, then listens on the _changes feed, pipeing the results through the map function so that you have always upto date view data, in memory

- https://github.com/Aam-Digital/replication-backend /GPLv3/202310/ts
  - This backend service can be used to filter the replication between a PouchDB and a CouchDB instance based on permission rules. 
  - It does this by overriding some of CouchDB's endpoints where permissions are checked on the transmitted entities. 
  - The permission rules are defined through CASL.
  - This system is Node.js application built with the NestJS framework.
# client-mobile-pc
- https://github.com/craftzdog/react-native-sqlite-2 /202211/ts
  - SQLite3 Native Plugin for React Native for Android, iOS, Windows and macOS.
  - It works pretty well with PouchDB on React Native app.
  - The reason for this plugin is that react-native-sqlite-storage has some problems when used with PouchDB
- https://github.com/craftzdog/pouchdb-adapter-react-native-sqlite /202108/js
  - PouchDB adapter using ReactNative SQLite as its backing store
  - SQLite storage performs much faster than AsyncStorage, especially with secondary index.
  - https://github.com/craftzdog/pouchdb-react-native-demo /202108/js
    - A working demo for PouchDB on React Native with SQLite3 storage
  - https://github.com/craftzdog/pouchdb-react-native /202204/inactive
    - A performant fork of PouchDB for React Native.
    - The attachment support has been dropped since I no longer store binary data in PouchDB.

- https://github.com/seigel/pouchdb-react-native /472Star/MIT/202010/js
  - PouchDB, the React Native-only edition. A preset representing the PouchDB code that runs in React Native.
  - preset contains the version of PouchDB that is designed for React Native. In particular, it ships with the AsyncStorage adapter as its default adapter. 

- https://github.com/demon24ru/pouchdb-adapter-sqlite-node /202108/js
  - pouchdb-adapter-sqlite for Node.js

- https://github.com/cozy-labs/cozy-desktop
  - File Synchronisation for Cozy on Desktop and Laptop

- https://github.com/duytq94/react-native-note-with-pouchdb /201910/js
  - Making a simple note app with PouchDB in React Native

- https://github.com/RyanLarge13/My-Recipes-Android /202310/js
  - fullstack recipe mobile Android application made with React Native and PouchDB for offline first data persistence
# pouchdb-event
- https://github.com/stockulus/pouchdb-event-store /201708/js
  - mimimal eventStore on top of pouchdb

- https://github.com/EternalDeiwos/panmnesia /201712/js
  - An action registry and redux-based aggregate store for a PouchDB-based event stream.

- https://github.com/thomastoye/field-journal /202112/ts/pouchdb
  - https://field-journal.pages.dev/
  - An experimental browser-based, offline-first, event-sourced dispatching, messaging, and incident tracking application.

- https://github.com/patrickpang/perpetual /201809/js
  - A WIP Life Management System = Todos + Calendar + Notes Implemented as a Progressive Web App
  - Offline editing
  - PouchDB
  - Workbox

- https://github.com/twilson63/vflow-pouchdb /201502/js
  - an abstraction around pouchDB's changes feed and it creates a simple api for interacting with the write stream system. 
  - It basically breaks it down into an event emitter.
# starter
- https://github.com/eingress/docker-pouchdb-server
  - a drop-in replacement for CouchDB, using PouchDB and Node.js
- https://github.com/CliffCrerar/poucdb-server-docker-image /js
  - Create a couchdb like pouchdb server docker image with a fauxton console

- https://github.com/MalyanaSkyrim/docker-mern-app /201911/js
  - Dockerize mern app, implement flux and implement offline-first pattern using pouchdb with couchdb

- https://github.com/mobiusdickus/nodejs-couchdb /202305/js
  - Dockerized template for a Node.js API and CouchDB database, served through Node.js.

- https://github.com/chaosprinz/webapp-boilerplate /201911/js
  - Boilerplate for developing webapps based on react with express/socket.io-backend using couchdb

- https://github.com/wandonye/openapi-express-couchdb /201909/js
  - openapi express couchdb boilerplate

- https://github.com/enfrte/couchdb-rest-api /201909/js
  - example of a NodeJS ReST API connecting to a CouchDB database

- https://github.com/EranGrin/couchDB-Node-Passport-Login /202003/js
  - A user login and registration app using Node.js, Express, Passport, CouchDB

- https://github.com/IvanAprea/react-client-couchdb 202206/ts
  - sudo docker-compose -f docker-compose.dev.yml

- https://github.com/robertohuertasm/couchdb
  - This example deploys a self-hosted version of CouchDB. Railway Template

- https://github.com/jelastic-jps/couchbase /js
  - Auto-Scalable Couchbase Cluster in Docker Containers
  - Prepackaged clustered NoSQL Couchbase DB solution with out-of-box automatic scaling and embedded data rebalancing for one-click deployment into Docker containers.

- https://github.com/BrianARuff/-SSE-Demo-App-RTC /202302/js
  - SSE (server send events) BE (back end) - using pouchDB - connected to two different clients (one regular html/js and one react app) sending data from DB via SSE to client in near real time
  - You can see the event sources in the browser dev tools by going to the network tab, finding the network request, and clicking event sources, and every 4ms a new request is made, but the database only updates every 1 second, so you only see a change in the value every 1 second.
  - https://github.com/BrianARuff/SSE_CRA_Client /js
# examples
- https://github.com/nolanlawson/pouchdb-getting-started-todo /201408/js
  - A complete version of the "Getting Started" PouchDB todo app
  - https://github.com/daleharvey/pouchdb-getting-started-todo /201307/js
  - https://github.com/phongtattuan/pouchdb-todos /201512/js
    - https://phongtattuan.github.io/pouchdb-todos/
  - https://github.com/larrymiami/pouchdb-tutorial /202201/js
  - https://github.com/Fishbite/pouchdb-todo /202108/js

- https://github.com/JaxonRailey/js-todolist-with-pouchdb-and-couchdb /202207/js
  - Another todolist to explain how to use couchdb synchronized pouchdb
  - 问题: 其他设备的更新不会自动通知当前设备的ui

- https://github.com/ronnix/pouchdb-couchdb-sync-example /201805/js
  - PouchDB + CouchDB syncing example

- https://gitlab.com/emergence-engineering/blog/-/tree/master/articles/prosemirror-sync-1 /ts
  - [Collaborative text editor with ProseMirror and a syncing database_202007](https://emergence-engineering.com/blog/prosemirror-sync-1)

- https://github.com/shellyln/kanban-board-app /202101/ts/redux/inactive
  - https://shellyln.github.io/knbn
  - Kanban style task management board app
  - 依赖redux、material-ui.v4、pouchdb-find、codemirror5
  - Calendar view
  - Synchronize multiple device boards with CouchDB remote server
  - Write kanban in Markdown syntax

- https://github.com/roldaojr/ra-data-pouchdb /LGPLv3/202204/js/inactive
  - PouchDB/CouchDB data provider for [react-admin](https://github.com/marmelab/react-admin)
  - This data provider takes a PouchDB object as input, then creates a client-side data provider around it.
  - Requires PouchDB-find plugin.
  - working: pagination, sorting(requires secondary indexes)
  - not working： filtering by column，full text search

- https://github.com/jed1976/prototype_cms /202208/js
  - Fun prototype CMS built with Node, CouchDB/PouchDB, RE: DOM and Tachyons.

- https://github.com/ibm-watson-data-lab/shopping-list-vanillajs-pouchdb /201802/js
  - https://github.com/ibm-watson-data-lab/shopping-list-react-pouchdb /202004/js
  - an Offline First demo Progressive Web App built using React and PouchDB
  - PouchDB syncs its data with a remote IBM Cloudant database.
  - PouchDB can synchronize with CouchDB and compatible servers.
- https://github.com/ibm-watson-data-lab/shopping-list-preact-pouchdb /201808/js
  - a reference implementation of an Offline First shopping list app, built as a Progressive Web App using Preact and PouchDB.

- https://github.com/couchbaselabs/todolite-electron-pouchdb /201612/ts
  - Example to demonstrate Couchbase in an Electron desktop application with PouchDB
  - https://github.com/ibm-watson-data-lab/shopping-list-electron-pouchdb /201710/js
  - https://github.com/krevindev/To-Do-List-Desktop /202309/js
  - https://github.com/JamesTheHacker/Neuron /201608/js/react

- https://github.com/marmelab/reactive-beers /201910/js
  - an example application using CouchDB and PouchDB
  - [CouchDB, The Open-Source Cloud Firestore Alternative? - DEV Community_201909](https://dev.to/juliendemangeon/couchdb-the-open-source-cloud-firestore-alternative-2gc0)
    - There is no per-document rights, only per-DB. A common recommendation around this is to use many (think thousands) of DBs, i.e. DB-per-user, and set up filtered replications to maintain each user's access. Unfortunately this has very poor performance
    - Couchbase, does a much better job of security and rights, though has its own quirks. It requires a secondary layer (called Sync Gateway) to give it a Couch-like API which can connect to PouchDB

- https://github.com/Tunetown/Notes /GPLv3/202210/js
  - https://notes.webertom.net/
  - This is a Notes Taking App based purely on CouchDB and JavaScript
  - 无需build可直接运行的项目, 依赖tinymce5.7、codemirror5、luckysheet、pouchdb7、jquery

- https://github.com/YuJiaHao/pouch-note-app /202206/js
  - a practice with react pouchdb and couchdb

- https://github.com/danobot/notorious /GPLv3/202102/ts/友好
  - https://danobot.github.io/notorious-landing
  - Offline-first note taking application for desktop and the web
  - 依赖redux-pouchdb、blueprintjs、material-ui.v4、antd.v3、codemirror.v5、flexsearch、turndown
  - Notorious backend is a CouchDB database and an optional web interface for accessing Notorious through a web browser.

- https://github.com/stanlemon/javascript/tree/main/apps/react-pouchdb-example /202309/ts
  - A react app using pouchdb written in typescript.
- https://github.com/hvaoc/react-pouchdb /202005/js/todomvc
  - https://arnosaine.github.io/react-pouchdb/
  - React wrapper for PouchDB that also subscribes to changes.
- https://github.com/cerebralideas/todomvc-universal-react-pouchdb /201908/ts
  - TodoMVC app written as a universal app in TypeScript with persistence server-side data
  - this is over-engineered for a todo app, but this is exactly what we needed to build super resilient, high availability, Web platforms to handle millions of requests a day.
  - 依赖redux、rxjs、superagent

- https://github.com/LauSam09/switch /202012/js
  - an application for managing house recipes and shopping. 
  - It is a progressive web application (PWA) application written using React, and is intended to function entirely offline if necessary.

- https://github.com/mehtaarn000/reactdrive /MIT/202105/js
  - File storage system built with Reactjs, Expressjs, Nodejs, and CouchDB

- https://github.com/dtinth/tmp /202101/ts
  - a web-based local file storage application. 
  - Basically, you can put files into it, and you can get files out of it.
  - 依赖pouchdb、react-query、nextjs10

- https://github.com/terichadbourne/offline-first-project-manager /201802/js
  - Offline First project management tool, built as a Progressive Web App with PouchDB, CouchDB, and service workers
  - This project is featured in my talk, Offline First: Making Your App Awesome When the Network Isn't.

- https://github.com/mradultiw/Wassup /202105/js
  - client-server based desktop chat application written in Javascript
  - It has a central server and database which is used to connect clients together.
  - Each client has it's own local database. 

- https://github.com/ShabanGomaa/Chat /201803/js
  - a simple chat application using react

- https://github.com/hadrysmateusz/writing-app /202202/ts/inactive
  - Rich-text editor with full offline support and cloud-syncing as well as local file editing functionality. 
  - Built with electron, react, couchdb, aws-amplify.v3, plate.v9

- https://github.com/starikan/pouchdb-viewer /202104/js
  - Standalone PouchDB viewer powered by Electron and pouchdb-server

- https://github.com/kbrisso/file-base /202309/js/ts
  - A database for managing your files using Electron and React.
  - You can tag, add notes, organize, categorize, filter, search and quickly find your needed files with an easy-to-use application
  - Filebase does not modify your existing files or directories 
  - uses PouchDB to store file and directory structure using a tree type structure, each of these nodes in the tree can have metadata added to it that will be searchable

- https://github.com/zyzmoz/SubscriptionManager /201907/js
  - User Subscription Manager created w React and PouchDB

- https://github.com/ErikVerheul/OneBacklog /202310/js
  - A Vue SPA for maintaining multi team product backlogs using CouchDB

- https://github.com/weiying-chen/vue-pouch-example /202312/js/vue
  - Vue Pouch Example

- https://github.com/okode/offline-todo-app /201909/ts
  - Ionic Shared List stored on PouchDB/CouchDB
  - https://github.com/xoxefdp/ionic-offline-todo
  - https://github.com/saty932/ionic3-pouchdb-Todoapp /201710/ts
  - https://github.com/GLCChaves/ClouDO /201905/ts/Ionic4
  - https://github.com/jarodms/ionic4-pouchdb /201912/ts/Ionic4

- https://github.com/pik-gane/vodle /202311/js/angular
  - Vodle will help groups make better decisions
  - Its underlying algorithm is based on thorough science and makes sure that all participants get the exact same influence on the decision
  - Built With Ionic Angular Typescript CouchDB Weblate

- https://github.com/1-Platform/idea-hub /202201/ts
  - a place to share ideas and innovations
  - Load remote couchdb with design documents and default tag
  - This repository is part of One Platform.

- https://github.com/FoxUSA/StoreDown /202207/js/vue
  - An inventory system that is hopefully simple enough 
  - If you want to sync between multiple devices, you need to setup a CouchDB server.
  - CouchDB Sync via PouchDB

- https://github.com/vrtmrz/obsidian-livesync /202311/ts
  - Self-hosted LiveSync is a community-implemented synchronization plugin.
  - A self-hosted or purchased CouchDB acts as the intermediate server
  - You can use CouchDB or its compatibles like IBM Cloudant.
  - Note: It has no compatibility with the official "Obsidian Sync".

- https://github.com/oglimmer/linky /202104/js
  - A link management system - or maybe just a playground for reactjs, node 
  - react-redux-form
  - CouchDB backend via nano

- https://github.com/genglefr/my-gallery /201804/js
  - Image gallery, in sync thx to PouchDB and Couchbase Sync Gateway websocket
  - a proof of concept for synching pouchdb - couchdb databases, using base64 images as documents. 
  - Since 19/02/2018, the sync is done over websocket of sync gateway.

- https://github.com/wonderwhy-er/offline-first-seed /201603/js
  - Minimalistic JavaScript offline first application seed using PouchDB and ServiceWorker
  - Uses Express/Node for server. Runs PouchDB both on server and client to allow working offline and sync when online Uses ServiceWorker to allow running page/app while offline Uses MaterializeCSS for styling

- https://github.com/couchbase-examples/couchbase-tutorials /202312/js
  - This repository contains the content for the Couchbase Developer Tutorials

- https://github.com/mohammadnazari110/pwa_offline_video_download /201905/js
  - this is a sample PWA app for download video and store to indexedDB with pouchDB

- https://github.com/ayastreb/money-tracker /202211/js
  - https://moneytracker.cc/
  - an open-source progressive web app that allows you to track your income and expenses.
  - Data is stored locally on device in PouchDB database and can be synced to the cloud.

- https://github.com/medic/cht-core /AGPLv3/202312/ts/js
  - https://communityhealthtoolkit.org/
  - The CHT Core Framework makes it faster to build responsive, offline-first digital health apps that equip health workers to provide better care in their communities.
  - [Why the CHT uses CouchDB - Product - Community Health Toolkit_202208](https://forum.communityhealthtoolkit.org/t/why-the-cht-uses-couchdb/2113)
  - https://github.com/medic/cht-sync /ts
    - CHT Sync is a bundled solution consisting of Logstash, CouchDB, PostgREST, DBT, and Superset. 
    - Its purpose is to synchronize data from CouchDB to PostgreSQL, facilitating analytics on a Superset dashboard. 
  - https://github.com/medic/cht-pipeline
    - a tool used to define data models for transforming the raw data we get from Couch DB into models that can then be queried to build dashboards.
    - contains transformation models for DBT.

- https://github.com/salgum1114/react-3d-editor
  - A-Frame based 3D visualization editing tool.

- https://github.com/Mo0812/MKNote /201905/js/vue
  - a note web app, which uses Markdown to render your notes.
  - verything works totally offline, all the data is stored on your browser and on your machine - no fancy backend
  - Even if its offline you can sync your notes over multi instances by running your own CouchDB backend

- https://github.com/xu4wang/markgraph /202207/js
  - http://awis.me/diagram/
  - Markdown Graph Notes App
  - Mermaid to draw diagrams
  - 依赖codemirror5、mermaid9、highlight

- https://github.com/patgoddard/codeMate /201404/js
  - A code editor for online or offline use using the chromium or chrome browser. 
  - It uses AceEditor, Pouchdb and an optional remote couchdb.
  - https://github.com/Profnird/codemate /202108/js

- https://github.com/steve-1820/memex /MIT/202009/ts/inactive
  - This a POC on how a memex could potentially work.
  - [Show HN: Open-Source Memex – Alternative Approach to Roam/Obsidian | Hacker News_202009](https://news.ycombinator.com/item?id=24572449)
    - This blog is a summary of a fun 1 month adventure I had with Knowledge Management Systems and building a POC
    - The Electron app receives this data through an API and saves it down locally using PouchDB 

- https://cherrypc.com/textapp.zip
  - [Show HN: TinyMCE and PouchDB Text App | Hacker News_202302](https://news.ycombinator.com/item?id=34860605)
  - This simple text app uses an older version of TinyMCE and one of their older demos.
  - I also use Bootstrap, jQuery
  - It lets you create "Folders" (PouchDBs) to store and manage documents. You can CRUD and search for documents.
  - You don't need a webserver to use it. Just load the index.html file from the textapp folder.

- https://github.com/samundrak/interactive-image-viewer /201908/js
  - https://affectionate-mestorf-34e48b.netlify.com/
  - Interactive Image viewer to select a position in image and tag/comment
  - FabricJS, ReactJS, IndexedDB

- https://github.com/ajhenry/searchable-car-database /202009/js
  - https://ajhenry.github.io/searchable-car-database/
  - This is a searchable car dataset with 40, 000+ entries 
  - There is a link to a react app that utilizes the data along with PouchDb to create a browser based database with indexing.

- https://github.com/evrom/plop /201402/js
  - A Blog CMS that uses PouchDB locally or remotely for storage.

- https://github.com/flysteur-dev/pager /202104/js
  - Minimalist serverless RSS reader (PWA, React, CouchDB, Web worker, Offline persistance, Docker)

- https://github.com/FieldDB/FieldDB /202112/js/inactive
  - app written in 100% Javascript which runs entirely client side, backed by a NoSQL database 
  - we are currently using CouchDB and its offline browser wrapper PouchDB alpha

- https://github.com/seb835/proptodo-multi /201707/ts
  - A multi-user to-do list, using couchdb, pouchdb, ionic, and superlogin
# examples-couch
- https://github.com/koostudios/couchpress /83Star/MIT/201205/CoffeeScript
  - lightweight and modular CMS built on NodeJS, Express and CouchDB

- https://github.com/homerjam/ace-cms /201912/js
  - Flexible, multi-site, headless CMS. 
  - ACE takes it's name from the key parts of the stack - Angular, CouchDB and Express.

- https://github.com/HusseinTaha/couchdb-node-cms /201506/js
  - A micro CMS for couchdb and nodejs 
  - This project use nodejs and couchdb to manage data from database using html templates.

- https://github.com/BigBlueHat/BlueInk /201612/js
  - BlueInk is being rewritten into an Open Source CMS built on Apache CouchDB and Cloudant mostly as a CouchApp.
- https://github.com/markuso/kleks /201511/CoffeeScript
  - http://markuso.github.io/kleks
  - pure CouchDB based CMS written as a CouchApp using Kanso, Spine.js, CoffeeScript and Stylus. 
  - Supports multi-site setup and Markdown authoring

- https://github.com/luisgerhorst/ccms /201310/js
  - Backend-free, client-side JavaScript and CouchDB based CMS.
  - it doesn't require any custom backend (such as PHP, Ruby on Rails or node.js). This is possible by using CouchDB's HTTP API
  - Another important feature is that the site dynamically loads required contents from the database using JavaScript

- budibase /19.5kStar/GPLv3/202312/ts/svelte
  - https://github.com/Budibase/budibase
  - https://budibase.com/
  - Low code platform for creating internal tools, workflows, and admin panels in minutes.
  - 后端依赖koa、knex、pouchdb
  - 前端依赖svelte
  - unlike other platforms, with Budibase you can start from scratch and create business apps with no datasources
  - Budibase integrates with a number of popular tools allowing you to build apps
  - the Budibase API enables Budibase as a backend
  - At Budibase we use CouchDB as the underlying technology of our internal Budibase DB.

- https://github.com/bterkuile/cmtool /202209/ruby/js
  - A rails 3.2+ CMS as engine for a CouchDB backend

- https://github.com/bryopsida/network-scanner /202307/ts
  - An api for configuring scheduled scans and persisting results to couchdb

- https://github.com/kdoran/lookout /202008/js
  - https://kdoran.github.io/lookout/
  - Web admin dashboard for CouchDBs

- https://github.com/makoni/ReleaseInformerBot /201704/js
  - Telegram Bot that will inform you about updates in App Store

- https://github.com/glynnbird/datamakerapp /201909/js/vue
  - An Electron App that generates sample data for Cloudant/CouchDB databases.

- https://github.com/NinjaGrandpa/nodejs-couchdb-demo /202307/js
  - A simple customer database built with CouchDB and NodeJs
# server
- https://github.com/infinity-arc/ts-express-pouchdb-server /202003/js
  - powerful API that can be run as a micro service to power progressive web applications.

- https://github.com/pouchdb/pouchdb-express-router /201911/js
  - an expressjs routing module that provides the minimal API to allow PouchDB instance to replicate over HTTP, 
  - it is designed to be mounted into expressjs web application to prove the an endpoint for PouchDB applications to sync with.

- https://github.com/acailly/easy-pouchdb-server /202105/js
  - Deploy a PouchDB server easily
  - running pouchdb server is perfect for small hobby projects or proof of concepts.

- https://github.com/fasiha/gotanda-pouchdb-server /202011/ts
  - A centralized Node.js server for your PouchDB-wielding local-first apps to sync to. Multiple users ok, multiple apps ok. Login with GitHub.
  - This repo is intended to service apps that use PouchDB to store their data locally—web apps or mobile apps or wherever PouchDB is supported.

- https://github.com/twilson63/express-pouchdb-jwt /201603/js
  - This is an express server that can point to a pouch or couch database and provide a jwt verification for authentication to a couch or pouch database.
  - this project creates a simple gateway to your pouchdb or couchdb servers. 
  - For the first iteration, the strategy is to use a pouchdb in memory server to sync with a couchdb database and expose the in memory pouchdb server as an endpoint.
  - The purpose for this microservice is to enable jwt user authentication for couchdb and pouchdb databases from client or native applications.
- https://github.com/dhavaln/auth0-pouchdb-syncgateway /js
  - PouchDB to Sync Gateway communication using Auth0
  - The demo AngularJS app is using authentication from Auth0, and then connects PouchDB to Sync Gateway using NodeJS Proxy server.

- https://github.com/BeneathTheInk/couchdb-jwt-auth-server /201706/js
  - A Node.js server for managing CouchDB authentication through JSON Web Tokens.
  - This service requires couch_jwt_auth to be installed on the CouchDB server.
- https://github.com/ronnieroyston/couch-behind-node
  - JSON Web Token Authentication & Node.js Authorization for Couch Database, Framework Free, Library Free

- https://github.com/CoMfUcIoS/session-pouchdb-store /js
  - PouchDB express session store. Can do realtime session data synchronization via PouchDB server
  - Default in-memory PouchDB instance.

- https://github.com/DEEJ4Y/pouchdb-services /ts
  - A set of PouchDB service functions and a class version of them, with `mongodb` style `ObjectID` id's for all your documents.

- https://github.com/npm/seq-file /js
  - A module for storing the ever-increasing sequence files when following couchdb _changes feeds.

- https://github.com/solzimer/session-pouchdb-store /js
  - A PouchDB session store for express.js.
  - Can do realtime session data synchronization via PouchDB server
  - Default in-memory PouchDB instance.
  - Scavenge and purge invalid/expired sessions.

- https://github.com/BigBlueHat/anno-proto-coucho /201610/js
  - Web Annotation Protocol Server built on Apache CouchDB
  - Apache CouchDB's HTTP API is quite similar to the Web Annotation Protocol except the later is specific to Annotation.
# pouchdb-utils
- https://github.com/i-mizzle/electron-react-pouchdb-boilerplate /202309/js
  - Boilerplate template for an electron application. with react and pouchDB
- https://github.com/quepas/electron-leveldown-pouchdb-webpack /202211/js
  - example

- https://github.com/nicolas-albert/prebuilt-pouchdb
  - Experiment the duration of a prebuilt PouchDB database, including replication and index computing to allow a fast client initialization.

- https://github.com/pouchdb/upsert /201703/js
  - PouchDB plugin for upsert() and putIfNotExists() functions
  - https://github.com/snowyu/pouchdb-upsertex /ts
    - Modified from pouchdb-upsert

- https://github.com/pouchdb-community/relational-pouch /202211/ts
  - a plugin for PouchDB that allows you to interact with PouchDB/CouchDB like a relational data store, with types and relations.
  - The main goal of this is to provide an API that is as similar to Ember Data and jsonapi as possible, while still being performant and Pouch-like.
  - This plugin is largely what powers Ember Pouch.
- https://github.com/egtoney/rcdb /ts
  - This library allows you to make and manage relational data in a CouchDB instance using nano
  - Features are implemented using CouchDB design documents to do type checking and some basic security to maintain consistency.
- https://github.com/iyobo/pouchorm /202205/ts
  - The definitive ORM for working with PouchDB.
  - Introduces the concept of Collections to pouchdb
  - Supports web, electron, react-native, and anything else
- https://github.com/compactd/slothdb /201808/ts
  - A typescript ORM that uses annotation and classes to describe the database
- https://github.com/ldavidsp/pouchdb-sql /202108/js
  - plugin that allows SQL queries to be performed against PouchDB databases
  - It requires the pouchdb-find plugin.

- https://github.com/marten-de-vries/pouchdb-seamless-auth /201706/js
  - Seamless switching between online (CouchDB) and offline (PouchDB) authentication.
  - This plug-in stores password hashes in a local PouchDB, not a smart thing
- https://github.com/pouchdb-community/pouchdb-authentication
  - User authentication plugin for PouchDB and CouchDB.
- https://github.com/dscsa/pouch /js
  - Library to add validation and syncing to PouchDB
- https://github.com/chorpler/pouchdb-auth-utils /202209/ts
  - PouchDB Authentication plugin, revised for PouchDB >=7.0.0 and requiring promises
  - install CouchDB, throw in a little SSL, and you've got everything you need for your site's authentication.
  - This plugin uses vanilla CouchDB.

- https://github.com/pouchdb-community/pouchdb-quick-search /370Star/apache2/201702/js/lunr/inactive
  - efficient and accurate full-text search engine built on top of PouchDB
  - The underlying tokenization/stemming/stopword engine is Lunr, which is optimized for English text, using a variant of the Porter stemmer. 
  - This is a local plugin, so it is not designed to work against CouchDB/Cloudant/etc. 
  - If you'd like to search against the server, use the CouchDB Lucene plugin, Cloudant's search indexes, or something similar.
  - https://github.com/mochi-cards/pouchdb-quick-search

- https://github.com/onyxcodes/dbmanager-ui /202208/ts
  - UI for managing PouchDB databases through DBManager interface layer
  - 依赖redux-toolkit

- https://github.com/jo/docuri /201701/js
  - Rich document ids for CouchDB
  - DocURIs can tell a lot about the document

- https://github.com/garbados/pouchdb-jsonviews /202311/js
  - A plugin that adds a JSON-based map/reduce view interface to PouchDB and CouchDB.

- https://github.com/curo-open/pouchdb-view-rebuild /202105/js
  - Fast PouchDB view index rebuild

- https://github.com/garbados/pouchdb-paginators /202311/js
  - A plugin that adds to PouchDB methods like .paginateAllDocs() which return paginators over results. 
  - Paginators can be iterated over without loading all results into memory
  - Pagination in PouchDB and CouchDB is rather unintuitive, especially for map/reduce views. This plugin intends to make it easy and reliable.
- https://github.com/tripott/paginate /201804/js
  - React/Redux pagination. Performant express/couch api pagination strategies with allDocs and mango queries.

- https://github.com/raviraju/CRUD_Videos /201606/js
  - CRUD operations for video attachments in pouchDb-couchDb NoSQL databases

- https://github.com/puncoz-official/redux-pouchdb-middleware /202001/ts
  - redux middleware to sync data between redux with pouchdb and vice-versa.
  - https://github.com/yldio/pouch-redux-middleware /201710/js
- https://github.com/vicentedealencar/redux-pouchdb /201912/js
  - sync store state to pouchdb
  - The PouchDB database persists the state of chosen parts of the Redux store every time it changes.
- https://github.com/medihack/redux-pouchdb-plus /201806/js
  - Synchronize Redux store with PouchDB to have a persistent store.
- https://github.com/jurassix/redux-pouchdb-store-enhancer /201611/js
  - to store actions locally, sync with remote CouchDB, and time travel by applying remote actions locally and then compute distributed nextState.
  - Every action that a single client emits as part of the regular Redux architecture will be intercepted and pushed into a local PouchDB database.
  - All local PouchDB actions are sync'd to a remote CouchDB database. 
  - All actions are added to the DB in accountant style, where every record is additive, and conflicts are almost guaranteed to be nonexistent.
  - Actions ordering is guaranteed to be deterministic by using a PouchDB `_id` that is a composite of `TIMESTAMP-UUIDv4`.
  - [Performance with large number of stored events](https://github.com/jurassix/redux-pouchdb-store-enhancer/issues/2)
    - I love idea of automatic state syncing, and generating new state based on saved events. 
    - However, I've made some benchmarks and find out that the most time-consuming part of loading state is getting all stored actions from local PouchDB instance.
    - this test shows main bottleneck of loading all store events from PouchDB. We need to figure out some way to efficiently load inital state
    - My plan to prevent this issue was to consolidate actions into a single action given a threshold. When to do this is the hard part
    - Maybe if we chunked the batching we could mitigate some of the time traveling conflicts. So instead of condensing all actions at a threshold we could just condense partitions of the actions.
    - I have thought about moving the reducer to the server too. 
- https://github.com/alexcorvi/PouchX /mobx
  - Seamless synchronization between PouchDB and MobX

- https://github.com/Terreii/use-pouchdb /apache2/202304/ts
  - a collection of React Hooks to access data in a PouchDB database from React components.
- https://github.com/davidmartinez10/use-pouchdb-collection /202204/ts
  - simple React hook for PouchDB. 
  - Designed to be as simple and easy to use as React.useState().
- https://github.com/stanlemon/react-pouchdb /202205/ts
  - https://github.com/stanlemon/javascript/tree/main/packages/react-pouchdb
  - React components for interacting with PouchDB documents. 
  - These components can be used to wrap parts of an application and both load and save state to a document. 
  - These components can be used both with React and React Native.
- https://github.com/ArnoSaine/react-pouchdb /202009/js
  - React wrapper for PouchDB that also subscribes to changes.
- https://github.com/atrauzzi/protoculture-react-pouchdb /202003/ts
  - a collection of React data components which allow you to obtain live data from PouchDB instances. 
  - It supports multiple database connections which can be selected by well known strings.

- https://github.com/osxi/react-pouch-redux-starter-kit
  - Quickly get started with React + PouchDB + Redux
  - https://github.com/whitphx/react-redux-pouch-example

- https://github.com/NotWoods/csv-to-pouch /202204/js
  - Parse CSV files and save their data to a PouchDB database.

- https://github.com/eFishery/pouchy-store /202011/js
  - a library to help developer create Offline First apps out of the box with synchronizing capabilities locally-remotely. 
  - https://github.com/eFishery/pouchy-store-example

- https://github.com/snowyu/pouchdb-transform.js /202210/ts
  - PouchDB Advanced Transform Library
  - This plugin is modified from transform-pouch to enhance it's ability
- https://github.com/pouchdb-community/transform-pouch /202108/js
  - PouchDB plugin for modifying documents before and after storage in the database.
  - Apply a transform function to documents before and after they are stored in the database. 

- https://github.com/dpmcmlxxvi/pouchdb-geospatial /202211/js
  - PouchDB geospatial query plugin.
  - provides spatial querying of GeoJSON objects. 
  - Any GeoJSON object inserted into the database via the the plugin API is spatially indexed using an `R-Tree`.
  - GeoJSON objects within a PouchDB database can be queried against an input GeoJSON object to test if they satisfy one of the DE-9IM spatial predicates

- https://github.com/pouchdb/geopouch /201703/js
  - Spatial plugin from PouchDB extracted and supporting N dimensional coordinates.
  - https://github.com/couchbase/geocouch /erlang

- https://github.com/hermanho/react-leaflet-pouchdb-tilelayer /202309/ts
  - React version of Leaflet. TileLayer. PouchDBCached
- https://github.com/MazeMap/Leaflet.TileLayer.PouchDBCached /202203/js
  - A Leaflet tile layer which caches into PouchDB for offline use

- https://github.com/cdaringe/pouchy /201908/ts
  - Pouchy wraps & extends PouchDB and provides various sorely needed sugar methods.
  - most methods provided are very simple PouchDB-native method modifiers, but are targeted to save you frequent boilerplate re-typing!

- https://github.com/Zardoz89/filestore-pouchdb /201912/js
  - Handles a simple file storage over PouchDB. 
  - Mimics some functionality of a virtual file system like directories and file hierarchy, but avoids to try to be a full virtual file system.
  - Store files on the browser, with the optional capacity of synchronize with a remote CouchDb database. 

- https://github.com/neojski/visualizeRevTree /201606/js
  - Visualize couchdb/pouchdb revision tree right in your browser

- https://github.com/garbados/comdb /202205/js
  - A PouchDB plugin that transparently encrypts and decrypts its data
- https://github.com/calvinmetcalf/crypto-pouch /202110/js
  - plugin for encrypted pouchdb/couchdb databases
  - This only encrypts the contents of documents, not the `_id` or `_rev`, nor view keys and values
  - encrypts documents using TweetNaCl.js, an audited encryption library. It uses the xsalsa20-poly1305 algorithm.
- https://github.com/jo/pouch-box /201505/js
  - Asymmetric encrypted PouchDB, powered by NaCl's curve25519-xsalsa20-poly1305.
  - uses TweetNaCl.js, a port of TweetNaCl / NaCl to JavaScript for modern browsers and Node.js by Dmitry Chestnykh

- https://github.com/pouchdb-community/worker-pouch /201802/js
  - Adapter plugin to use PouchDB over Web Workers and Service Workers. 
  - Transparently proxies all PouchDB API requests to the worker, so that the most expensive database operations are run in a separate thread.

- https://github.com/bkniffler/workerdb /201901/ts/rxdb8/rxjs6
  - Performant, Reactive, offline-first, syncable Database in WebWorker based on PouchDB/RxDB, great for electronJS and web-applications
  - vanilla: The database can be used with or without any framework

- https://github.com/genbliz/mocody /202303/ts
  - Implementation of single table design, and unified query access for MongoDB, CouchDB, and dynamoDB.

- https://github.com/sudzy-group/pouchable /ts
  - PouchDB simplified by TypeScript Decorators

- https://github.com/cloudant/meteor-couchdb
  - Meteor database driver for CouchDB and Cloudant
  - an efficient Livequery implementation providing real-time updates from the database by consuming the CouchDB _changes feed
  - Distributed Data Protocol (DDP) RPC end-points for updating the data from clients connected over the wire

- https://github.com/dungeonfog/pouchdb-rs /202010/Rust
  - Rust wrapper around PouchDB, using wasm-bindgen

- https://github.com/neoskop/bouch /201911/ts
  - CouchDB/PouchDB Backup/Restore Tool with Attachments Support
  - an CLI Tool to backup and restore CouchDB and PouchDB databases.

- https://github.com/Squarespace/pouchdb-lru-cache /201803/js
  - An LRU (least recently used) cache designed for storing binary data in PouchDB. 
  - Runs in modern browsers and Node.js.
  - this could be used for caching images so that you don't have to re-load them every time.
- https://github.com/HitomiTenshi/pouchdb-binary-utils /201907/js
  - PouchDB utilities for operating on binary strings and Buffers/Blobs.

- https://github.com/DamonOehlman/attachmate /201706/js
  - An experiment in using @isaacs useful fstream project to stream files in and out of CouchDB as attachments to documents.
- https://github.com/KlausTrainer/couch_image_resizer /201209/js
  - a simple web service that can serve CouchDB document attachments and, if the attachment is an image, is able to resize it using the convert program that is part of the ImageMagick tool suite. 
  - Resized images are held in an in-memory LRU cache, whose configurable size is 128 megabytes by default.
# couchdb-utils
- https://github.com/oreilly/couchdb-guide
  - https://guide.couchdb.org/
  - Three of CouchDB’s creators show you how to use this document-oriented database as a standalone application framework
  - The contents of this guide are out of date. All relevant info has been updated and integrated into the official CouchDB documentation

- https://github.com/dianabarsan/couchdb-perf /js
  - CouchDb 2 vs CouchDb 3 superficial performance bench

- https://github.com/jo/couchdb-bootstrap /202103/js
  - Bootstrap CouchDB projects: configure, setup security, deploy ddocs and create users.

- https://github.com/apache/couchdb-fauxton /js
  - the new Web UI for CouchDB

- https://github.com/ermouth/couch-photon /json
  - an alternative CouchDB admin panel
  - Photon is a single CouchDB design document with attachments, so it can be installed on any running CouchDB without rebuilding or reconfiguring.
  - Photon never existed as source files, its sources are CouchDB docs. 

- https://github.com/antal0x11/express-couchdb /js
  - A simple CRUD application with ExpressJS and CouchDB.
  - https://github.com/irfanullah2/CouchdbCrud
- https://github.com/NinjaGrandpa/nodejs-couchdb-demo /js
  - A simple customer database built with CouchDB and NodeJs

- https://github.com/garrensmith/fortuna-rs /202103/js/rust
  - A javascript view engine for CouchDB 4.x written in Rust using Google V8.
  - Install FoundationDB Install CouchDB dependencies Setup CouchDB
  - [Building a faster CouchDB View Server in Rust](https://www.garrensmith.com/building-a-faster-couchdb-view-server-in-rust/)

- https://github.com/couchbaselabs/node-ottoman /202310/ts
  - https://ottomanjs.com/
  - ODM built for Couchbase and Node.js.
  - 依赖Ottoman, Couchbase SDK, Couchbase Server
  - https://github.com/stoqey/sofa
    - [I am working on an ORM based of couchbase and node-ottoman - Node.js SDK - Couchbase Forums](https://www.couchbase.com/forums/t/i-am-working-on-an-orm-based-of-couchbase-and-node-ottoman/31636)

- https://github.com/minni-im/tape-recorder /202105/js
  - Thin ORM for CouchDB on top of Nano
- https://github.com/Wemotive-POC/couchdb-orm /202201/js
  - 提供了example
- https://github.com/jimpo/couch-monster /2012/js
  - CouchDB ORM for Node.js
- https://github.com/EternalDeiwos/model /201711/js
  - PouchDB adapter for the json-document modelling framework
  - https://github.com/anvilresearch/json-document /201705/js
    - Model and manipulate data with ES6 classes, JSON Schema initialization and validation, JSON Patch, JSON Pointer, and JSON Mappings.

- https://github.com/ermouth/covercouch /108Star/MIT/201902/js
  - 💡 CoverCouch implements per-document r/w/d ACL for CouchDB. 
  - CoverCouch acts as proxy – original CouchDB REST API kept untouched, but all requests to Couch – r/w/d, _changes feed, _view, _update, _list or other fn call, replication – everything is filtered.

- https://github.com/janl/per-doc-auth-for-couchdb /201706/js
  - Docs have new property $access: ['user', 'role', …]
  - R/W access to docs is matched against the http user & roles and the $access field
  - Tech Demo: Do Not Use

- https://github.com/gr2m/couchdb-user-management-app /201411/js
  - https://gr2m.github.io/couchdb-user-management-app/
  - Web app to manage CouchDB users and database security settings

- https://github.com/etrepum/couchperuser /201412/erlang
  - a CouchDB plugin daemon that creates per-user databases
  - Obsolete as of CouchDB 2.1.1: You can now enable this in CouchDB using the built-in `couch_peruser` option.

- https://github.com/twilson63/express-couchUser /201504/js
  - A express module for CouchDb based User Authentication Module
  - The optional `validateUser` allows you to specify extra validation other than username/password. 

- https://github.com/MustafaHi/auth-couchdb /202206/js
  - Node.js server authentication application for Couchdb
  - Using the latest and fastest API's for Node.js including fastify web framework and undici HTTP client
  - Using fastify's auto directory scan for auto page addition
  - Account creation, activation, modification and deletion.

- https://github.com/ermouth/cloudwall /201903/js
  - A platform for developing, testing, building, deploying and running CouchDB hosted apps.

- https://github.com/glynnbird/couchwarehouse /js
  - a command-line tool that turns your Apache CouchDB database(s) into a local data warehouse. 
  - The target database can be either be SQLite, PostgreSQL, MySQL or Elasticsearch.
  - creating a new SQLite, PostgreSQL or MySQL table to match the couchdb schema
  - downloading all the documents (except design documents) and inserting one row per document into the target database.
  - continuously monitoring CouchDB for new documents, updates to existing documents and deletions.

- https://github.com/ICTatRTI/couchdb-conflict-manager /202202/js
  - A pluggable UI (web component) for managing conflicts in a CouchDB Database.

- https://github.com/glynnbird/couchmigrate
  - CouchDB command-line design document migration tool
  - https://github.com/glynnbird/couchimport
  - https://github.com/glynnbird/couchsnap
  - https://github.com/glynnbird/couchsnapshot
  - https://github.com/glynnbird/couchfirehose /202311/js
    - A proof-of-concept tool that allows Cloudant/CouchDB data to be transferred quickly between a source database and a target database. 
    - This is not replication.It doesn't transfer attachments.
    - It is faster than replication but gets its speed by assuming that the source database is static and the the target database is empty.
    - The source database's changes feed is consumed in batches and a queue of bulk writes is built up in the app.

- https://github.com/felixge/node-couchdb /201906/js
  - A thin node.js idiom based module for CouchDB's REST API that tries to stay close to the metal.

- https://github.com/medic/couch2pg /202209/js
  - Library and app to replicate a CouchDB database to PostgreSQL
- https://github.com/sysadminmike/couch-to-postgres /201710/js
  - Node libary to stream CouchDB changes into PostgreSQL

- https://github.com/1999/node-couchdb /202208/js
  - provides an easy way to interact with CouchDB using preferred cache layer: memory/memcached

- https://github.com/iriscouch/couchjs
  - Drop-in replacement JavaScript engine for Apache CouchDB
  - By using CouchJS, you will get 100% CouchDB compatibility (the test suite completely passes) but your JavaScript environment is V8, or Node.js.

- https://github.com/obscure-com/couchdb-dbperuser-provisioning /201508/js
  - Many developers choose to store user-specific data in CouchDB by creating a separate database for each user. This approach can provide better security and performance than storing all user data in a single, monolithic database. 
  - This repo contains a CouchDB OS daemon that can be used to provision(供应, 提供) per-user databases for most use cases.

- https://github.com/jcrugzz/changes-stream
  - A fault tolerant changes stream with builtin retry HEAVILY inspired by follow.
- https://github.com/jo/couchdb-global-changes-stream
  - Multiplexed persisted global couchdb changes stream across all databases.

- https://github.com/jo/grunt-couch /202302/js
  - Build and publish Couchapps and CouchDB design documents with grunt. Simple.
  - Compile CouchDB design documents from Couchapp like directory tree.

- https://github.com/pekrau/webapp-flask-couchdb-template /202310/python
  - A template for a web app based on Flask and CouchDB with user account handling.

- https://github.com/MatteoGuadrini/PSCouchDB /powershell
  - https://matteoguadrini.github.io/PSCouchDB/
  - Advanced CLI for CouchDB server

- https://github.com/crkn-rcdr/kivik /202108/ts
  - An opinionated library and command-line utility for configuration CouchDB endpoints, databases, and design documents.
  - Kivik's opinionated nature lies in its expectation of a directory structure where it will find all of the CouchDB configuration you'd like to test and deploy
- https://github.com/go-kivik/kivik /202312/go
  - Common interface to CouchDB or CouchDB-like databases for Go and GopherJS
  - The kivik package must be used in conjunction with a database driver.

- https://github.com/maxlath/blue-cot /202208/js
  - CouchDB library with a simple, functional-programing-friendly API, returning promises
  - Class-less, thus a different initialization, but the rest of the API stays the same
  - Uses Cookie Authentication instead of Basic Auth for better performance

- https://github.com/maxlath/couch-init2 /202304/js
  - An opinionated CouchDB databases initializer

- https://github.com/cliffano/couchtato /201811/js
  - a CouchDB database iterator tool.
  - This is handy when you want to apply a set of JavaScript functions against all documents in a CouchDB database or view, or only some of them by specifying a start and/or an end key(s). 

- https://github.com/glynnbird/changesreader /js
  - CouchDB changes reader
- https://github.com/DamonOehlman/changemate /js
  - Changemate is a change notification service and framework. 
  - At present it only supports responding to the _changes feed of a couch database, but will be expanded in time to support other change notification formats.

- https://github.com/rnewson/couchdb-lucene /java
  - Enables full-text searching of CouchDB documents using Lucene

- https://github.com/MalekovAzat/CouchDbStressTesting /python/ts
  - CouchDb synchronization stress testing

- https://github.com/mgp/iron-cushion /201309/java
  - A benchmark and load test for CouchDB

- https://github.com/janl/couchdb-test-couchjs /201402/js
  - A test suite for CouchDB’s query server. 
  - Replaces test/query_server/query_server_spec.rb

- https://github.com/OldSneerJaw/couchster /201908/js
  - utility to aid in the process of designing well-structured document validation functions for Apache CouchDB.
  - https://github.com/OldSneerJaw/couchster-test-examples

- https://github.com/stanlemon/couchdb-userdb /201907/js
  - A tool for managing user specific databases in an Apache CouchDB
  - This tool will look at the `_users` database and monitor for documents and cross reference them against user specific databases 
  - In the event that a document exists in `_users` but has no corresponding database, this tool will create it. 

- https://github.com/node-casbin/couchdb-adapter /202307/ts
  - CouchDB policy storage, implemented as an adapter for node-casbin.

- https://github.com/maxlath/couchdb-view-by-keys /202005/js
  - A command-line tool to query CouchDB views, focused on easing queries with complex JSON keys

- https://github.com/jmarca/couchdb_get_views /201903/js
  - This is a module to simplify getting view output from CouchDB. 

- https://github.com/timo-reymann/poc-couchdb-view-reduce /202211/shell
  - Proof of Concept to utilize CouchDB view reduce
  - reduce is not used in Fauxton, but by default in API calls

- https://github.com/dominictarr/pull-couch /201601/js
  - Parse the rows out of a couchdb views query without parsing it as one large json object. 
  - instead split based on the format couchdb happens to use (delimited by \r) and then parse each line with JSON.parse. 
  - This is much faster than parsing everything with a streaming parser (if implemented in js), such as JSONStream

- https://github.com/mikerhodes/couchdbgin /202311/js
  - (Incomplete) Exercise in creating an inverted index using JSON paths and values within CouchDB
  - This proof of concept shows how CouchDB could index every field in a document into the same index and enable general querying across all the fields in a Mango-like way

- https://github.com/notnotse/ol-couchdb-source /202004/js
  - OpenLayers source for fetching and displaying GeoJSON documents from a CouchDB server.

- https://github.com/altcmdio/couchdb-with-cors
  - Identical to the official CouchDB image (3.3.2), with permissive CORS pre-configured

- https://github.com/SPINEProject/ManagerCouchdb /202206/js
  - a javascript library for managing CouchDB servers and databases

- https://github.com/dianabarsan/couchdb-seq-tests
  - CouchDb sequence comparison when pushing docs again after restoring from backup

- https://github.com/onur1/couchilla /js
  - Use couchilla to bundle a CouchDB design document from a directory of JavaScript files.
  - [Bundle your CouchDB map/reduce functions with ease](https://ogu.nz/couchilla.html)

- https://github.com/mhausenblas/ld-in-couch /201211/python
  - This project enables you to store, process and query RDF-based Linked Data in Apache CouchDB.

- https://github.com/zetavg/Inventory/tree/main/packages/couchdb-public-server /js
  - A simple HTTP server to serve content in CouchDB databases publicly

- https://github.com/rajcrk/couchdb-query-helper /202206/js
  - library that can help you build query, schema, and control your database more easier.

- https://github.com/glynnbird/sqltomango /202206/js
  - converts Structured Query Language (SQL) into CouchDB Mango / Cloudant Query JSON objects
  - This tool converts SQL strings into Mango objects, to allow users to interact with CouchDB/Cloudant database with SQL queries.
  - https://github.com/glynnbird/mangogrep
    - A command-line tool for "grepping" streams of JSON with CouchDB Mango selectors, or SQL

- https://github.com/onur1/tango /202301/js
  - textual syntax for the mango query language.
  - tango expressions are based on the C syntax. Currently it supports basic comparison operators (==, >, >=, <, <=, ||, &&) and parentheses for explicit operator precedence.

- https://github.com/garrensmith/mango_smoothie /201702/rust
  - A CouchDB Mango/Cloudant query client for rust.
  - It supports creating indexes, listing indexes and querying indexes

- https://github.com/glynnbird/couchdiff /202211/js
  - command-line utility to calculate the difference between two Cloudant/CouchDB datbases.
  - https://github.com/glynnbird/couchdeconflict
    - Command-line utility to remove conflicts from CouchDB/Cloudant documents

- https://github.com/gr2m/couchdb-excel-import /201501/js
  - imports Excel files (*.xls, *.xlsx) into CouchDB documents, and transforms the sheets into JSON.

- https://github.com/maxlath/couchdb-bulk2 /202111/js
  - Pipe newline-delimited JSON into CouchDB
  - command line tool meant to eat newline-delimited JSON (CouchDB documents) on stdin and POSTing them to the _bulk_docs endpoint of a CouchDB server.

- https://github.com/nfriedly/couchdb-backup-restore /202102/js
  - Creates backups of couchdb databases (.tar.gz files containing one .json file per database) and restores from those backups.
  - Also plays nice with Cloudant (hosted CouchDB service).
  - the official backup methods are recommended for most users. However, this tool will remain avaliable for those who need it.
  - This library does not support attachments

- https://github.com/ilfrich/couchdb-to-mongodb /201907/js
  - migrate CouchDB databases to MongoDB collections
  - Since CouchDB and MongoDB are structured slightly different, the convention is to migrate each CouchDB database to a separate collection within a separate database.
  - The migration tool will not migrate `_design` documents.
  - https://github.com/jimishio/couchdb-to-mongodb /201704/shell
- https://github.com/simagix/couch-to-mongo /202103/java
  - Migrate data from CouchDB to MongoDB. 
  - The algorithm is based on the fact that in CouchDB, documents are sorted by the document ID. 
  - The application uses a thread to read data off CouchDB and kicks off multiple threads to save data to MongoDB.
- https://github.com/Firkintun/slouch /201411/js
  - A lazy, pull-only, continuous replication server from CouchDB to MongoDB

- https://github.com/tchlyah/couchmove /202308/java
  - open-source Java migration tool for Couchbase
  - Couchmove can help you track, manage and apply changes in your Couchbase buckets. The concept is very similar to other database migration tools such as Liquibase, Flyway, mongeez, mongobee
  - Couchmove is widely inspired from Flyway : it strongly favors simplicity and convention over configuration

- [mongo2couch.py](https://gist.github.com/Kailashcj/8b24b90356ccfcf2d1cc6558b785b9c5)
  - /201906/python
  - migrate documents from mongodb to apache couchdb database
  - does not support the use case for 'documents with attachments'
# test
- https://github.com/ViduusEntertainment/pouchdb-seed-database /202202/ts
  - seed-database with admins/members/roles

- https://github.com/chxyang/couchdb-demo-app
  - The source repository for the getting started tutorial for PouchDB

- https://github.com/gr2m/pouchdb-attachments-sync-test /js
  - https://gr2m.github.io/pouchdb-attachments-sync-test/
  - Current PouchDB downloads all attachments from all revisions when replicating from a remote repository, instead of smartly checking what attachments already exist locally

- https://github.com/cozy/pouchdb-playground /202104/js
  - Make queries with PouchDB and measure performances.
  - Hacking the Cozy Pouchdb playground app requires you to setup a dev environment.
  - Hacking the Cozy Pouchdb playground app requires you to setup a dev environment for cozy-client
# more
- https://github.com/KouchDB/replication-source-poc /202211/java
  - Demonstrates how to stand-up a Java Springboot service as a source for CouchDB replication
  - CouchDB mock replication source Proof Of Concept.

- https://github.com/oknosoft/metadata.js /201903/js/inactive
  - Library for building offline-first browser-based applications 
  - To manage data on the browser side, Pouchdb and AlaSQL are used
  - Couchdb was chosen as the main server data storage
  - Supported the ability to connect data adapters to 1C and other ORM, SQL and NoSQL servers
  - For developers of mobile and browser applications who are cramped(受限制) within the 1C platform

- https://github.com/kristopolous/db.js /202109/js/inactive
  - portable Javascript document store event-driven database
  - It's been feature-complete and stable for years

- https://github.com/hexojs/warehouse /188Star/MIT/202309/ts/hexo
  - https://hexojs.github.io/warehouse/
  - A JSON database with Models, Schemas, and a flexible querying interface. 
  - It powers the wildly successful static site generator Hexo.
