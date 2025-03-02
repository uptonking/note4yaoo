---
title: toc-database-document-mongodb-json
tags: [database, json, mongodb, toc]
created: 2022-06-13T03:56:47.999Z
modified: 2022-11-03T04:14:11.987Z
---

# toc-database-document-mongodb-json

# guide
- alternatives
  - minimongo
  - nedb

- 偏向crud而不是查询的场景，考虑json patch

- 更适合block-editor的数据结构是否是 mongodb？
# mongodb-like
- popular
  - nedb
  - minimongo

- sift.js /1.6kStar/MIT/202211/ts
  - https://github.com/crcn/sift.js
  - Use Mongodb queries in JavaScript
  - Supports node.js, and web

- https://github.com/kofrasa/mingo /MIT/202309/ts
  - MongoDB query language for in-memory objects
  - Supports dot notation for both `<array>.<index>` and `<document>.<field>` selectors.
  - Query and Projection Operators
  - Aggregation Framework Operators
  - Update Operators
  - Filtering and aggregation using streaming.
- https://github.com/flex-development/mango /ts/inactive
  - MongoDB-like API for in-memory object collections

- tingodb /1.1kStar/MIT/201901/js
  - https://github.com/sergeyksv/tingodb
  - http://www.tingodb.com/
  - an embedded JavaScript in-process filesystem or in-memory database upwards compatible with MongoDB at the v1.4 API level.
  - Upwards compatible means that if you build an app that uses functionality implemented by TingoDB you can switch to MongoDB almost without code changes. 
  - https://github.com/sergeyksv/tungus
    - Mongoose driver for TingoDB

- https://github.com/maxnowack/signaldb /73Star/MIT/202312/ts
  - https://signaldb.js.org/
  - a local JavaScript database with a MongoDB-like interface and TypeScript support, enabling optimistic UI with signal-based reactivity across multiple frameworks.
  - It enables the storage of data through a JSON interface in various storage providers, including the widely-used localStorage.
  - In theory, every signal library is supported. SignalDB currently have pre-build reactivity ✨ adapters for preact-singals/mobx/solidjs
  - At the heart of SignalDB lies its advanced handling of collections and queries. Our in-memory data storage approach ensures blazing-fast query performance
  - SignalDB plans to implement a cutting-edge data replication engine, drawing inspiration from established protocols like the RxDB replication protocol 
  - [Show HN: SignalDB – Reactive Local JavaScript Database | Hacker News _202310](https://news.ycombinator.com/item?id=37959470)
    - Looks exactly like what Meteor did in 2011 (called minimongo)
    - The design is heavily inspired by Minimongo. 

- ZangoDB /1kStar/MIT/201710/js
  - https://github.com/erikolson186/zangodb
  - https://erikolson186.github.io/zangodb/
  - ZangoDB is a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.
  - an implementation of IndexedDB is required. 
    - For environments without a native implementation of IndexedDB, https://github.com/dumbmatter/fakeIndexedDB can be used
  - 🍴 forks
  - https://github.com/allwi290/zangodb
    - cjs to es

- https://github.com/rain1017/memdb /201511/js/inactive
  - 全球首个支持分布式事务的MongoDB
  - Distributed Transactional In-Memory Database
  - MongoDB and Mongoose Compatible
  - It's just a 'MongoDB' with a cache layer which support distributed transaction.

- ForerunnerDB /707Star/MIT/202006/js/v2/inactive
  - https://github.com/Irrelon/ForerunnerDB
  - http://www.irrelon.com/
  - ForerunnerDB is a NoSQL JavaScript JSON database with a query language based on MongoDB (with some differences) and runs on browsers and Node.js.
  - ForerunnerDB supports data persistence on both the client (via LocalForage) and in Node.js (by saving and loading JSON data files).
  - ForerunnerDB is an in-memory store but you choose how often (if at all) data is loaded and saved with underlying storage engines.
  - https://github.com/Irrelon/forerunnerdb-core /202110/js/v3/inactive
    - This project contains the core query/match/update functionality of ForerunnerDB 3.x
    - provides the core of ForerunnerDB 3.0 which is a complete rewrite of ForerunnerDB in ES6
    - 3.0 is being built in a completely modular fashion with extensibility at heart.
    - queries in ForerunnerDB 3.x use MongoDB query language by default.
  - [How does load work?](https://github.com/Irrelon/ForerunnerDB/issues/247)
    - The load() method does indeed load everything into memory 
    - ForerunnerDB's initial use case was the manipulation and complex querying of JSON data in memory. 
  - [Stream subset of data from disk while querying](https://github.com/Irrelon/ForerunnerDB/issues/56)
    - ForerunnerDB was originally intended as a browser-based DB with in-memory access and then grew to include Node.js support and persistent storage.
    - It would be relatively slow and difficult to query the data in a persisted state as the current storage system allows LocalStorage which doesn't provide for row-by-row access (although we could engineer one with a slower read/write to storage as a side effect).

- https://github.com/elmarti/camadb /202110/ts
  - a NoSQL embedded database written in pure TypeScript for Node, Electron and browser
  - SQLite doesn't (by default) return native JS data types (Dates in particular)
  - CamaDB uses a MongoDB style **query** language, powered by SiftJS.
  - we use a MongoDB style language for data **updates**, for this we use obop
  - We use Mingo for **aggregation** - currently lookup commands aren't supported.

- PicoDB /31Star/MIT/202201/js
  - https://github.com/jclo/picodb
  - A tiny in-memory database (MongoDB like) that stores JSON documents
  - It runs both on Node.js and in the ES6 compliant browsers.
  - A document is a Javascript literal object. It is similar to a JSON object. 

- yunodb /246Star/CC0/201704/js/levelup
  - https://github.com/blahah/yunodb
  - A portable, persistent, electron-embeddable fulltext search + document store database for node.js
  - yuno is a JSON document store with fulltext search. 
  - The document store, which is just the raw JSON objects stored in leveldb/levelup/browser-level
  - The inverted search index, powered by search-index
  - yuno is being built to serve my use-case of embedding pre-made databases in electron apps
  - 🍴 forks
    - https://github.com/pdepip/yunodb

- https://github.com/FoundationDB/fdb-document-layer /apache2/201909/cpp/python
  - [Known Differences | FoundationDB Document Layer](https://foundationdb.github.io/fdb-document-layer/known-differences.html)
  - A document data model on FoundationDB, implementing MongoDB® wire protocol
  - implements a subset of the MongoDB® API (v 3.0.0) with some differences. 
  - allow the use of the MongoDB® API via existing MongoDB® client bindings. 
  - All persistent data are stored in the FoundationDB Key-Value Store.
  - The Problem with Document Layer it implements MongoDB API v 3.0.0 and has not been significantly updated for years.

- https://github.com/usmakestwo/githubDB /201811/js
  - A Lightweight Cloud based JSON Database with a MongoDB like API for Node.
  - You will never know that you are interacting with a Github

- https://github.com/arvindr21/diskDB /201712/js
  - A Lightweight Disk based JSON Database with a MongoDB like API for Node
  - You will never know that you are interacting with a File System

- https://github.com/Belphemur/node-json-db /MIT/202401/ts
  - A simple "database" that use JSON file for NodeJS
  - Every method are now asynchronous

- https://github.com/anywhichway/joqular /201902/js
  - JavaScript Object Query Language Representation - Funny it's mostly JSON.
  - JOQULAR is a query language specification. 
  - Like SQL, JOQULAR allows you to mutate the returned records to meet you needs.
  - 不如json patch

- https://github.com/JerrySievert/mongolike /201408/js
  - A proof of concept MongoDB clone built on Postgres

- https://github.com/go-kivik/mango /go/inactive
  - Go implementation of the Mango query language used by CouchDB and PouchDB

- https://github.com/at30in/lucene-mongo-query /202304/js
  - Lucene-inspired string-based mongodb query language for humans (and ferrets).

- https://github.com/onur1/tango /202301/js
  - textual syntax for the mango query language.
  - tango expressions are based on the C syntax. Currently it supports basic comparison operators (==, >, >=, <, <=, ||, &&) and parentheses for explicit operator precedence.

- https://github.com/glynnbird/sqltomango /202206/js
  - converts Structured Query Language (SQL) into CouchDB Mango / Cloudant Query JSON objects
  - This tool converts SQL strings into Mango objects, to allow users to interact with CouchDB/Cloudant database with SQL queries.
  - https://github.com/glynnbird/mangogrep
    - A command-line tool for "grepping" streams of JSON with CouchDB Mango selectors, or SQL

- https://github.com/thomas4019/pgmongo /ISC/201812/js/inactive
  - Replace MongoDB with PostgreSQL using jsonb fields
  - Drop-in replacement Applications do not need code changes
  - pgmongo rewrites queries and proxies them to a Postgres database.
  - This implements the MongoDB wire protocol and adapts queries to work with a PostgreSQL database using jsonb fields. 

- https://github.com/torodb/server /201707/java
  - open source NoSQL database that runs on top of a RDBMS. 
  - turns your RDBMS into a MongoDB-compatible server, supporting the MongoDB query API and MongoDB's replication, but storing your data into a reliable and trusted ACID database. 
  - ToroDB currently supports PostgreSQL as a backend, but others will be added in the future.

- https://github.com/renebigot/reactive-db-js /MIT/202012/js
  - in memory reactive database with a MongoDB like query syntax.
  - reactive: You can subscribe/unsubscribe to any collection, so if documents are created, updated, or removed, you'll be notified.
  - reactive-db-js is not performance optimised. It's goal is to provide an easy way to store and query with a notification mecanism. It may be slow with lots of datas stored

- https://github.com/kanryu/puremongo /201401/ts
  - a pure JavaScript clone for MongoDB
  - API is similar to at https://github.com/mongodb/node-mongodb-native .
  - You can run the DB on node.js, on Common.js, even on web browsers.
# db-doc-json
- https://github.com/Alex-Werner/SBTree /MIT/202310/js
  - https://alex-werner.github.io/SBTree/
  - Fast document store using B+ Tree for fields. 
  - Adapters support for In-Memory and FileSystem
  - This library's goal is to provide a way to quickly store document-based data in-memory or on the filesystem.
  - It uses a field-specific indexing system relying on B+Tree structure.
  - This allow to handle a lot of data, and have them indexed without the need to keep the whole dataset in-memory.
  - Most of the databases uses B-Tree (MongoDB) or B+Tree (CouchDB, InnoDB, MariaDB, MySQL).
  - By default. Everything except specifically excluded field are indexed. Nested object are also indexed. Optional support for uniques key provided.

- https://github.com/losfair/RefineDB /202109/rust/inactive
  - A strongly-typed document database that runs on any transactional key-value store.
  - Currently supported backends are:
    - FoundationDB for distributed deployment.
    - SQLite for single-machine deployment.
    - A simple in-memory key-value store for the web playground.

- redux-database /18Star/MIT/202005/ts/NoDeps
  - https://github.com/nerdgeschoss/redux-database
  - https://nerdgeschoss.github.io/redux-database
  - Simple reducer based in-memory database with strong typings and immutable documents, with plugins for redux and react.
  - Client side data normalization is hard. This library helps you to organize your state in a relational way, with queries and joins as you would expect from an SQL based database. 
  - There is a storage adaper for redux or you can use it as a standalone library (redux-database has no dependencies!).

- redux-db /25Star/MIT/201902/ts
  - https://github.com/msolvaag/redux-db
  - redux-db provides a normalized redux store and easy object management.
  - Having a normalized state is a good strategy if your data is nested in different ways.

- kinto /4.2kStar/apache2/202210/python
  - https://github.com/Kinto/kinto
  - http://docs.kinto-storage.org/
  - A generic JSON document store with sharing and synchronisation capabilities.
  - Backends: In-memory (development), PostgreSQL 9.5+ (production)
  - [How does Kinto compare to other solutions?](https://docs.kinto-storage.org/en/stable/faq.html)
    - 比较了parse、firebase、couchdb、kuzzle、remoteStorage、Hoodie
  - https://github.com/Kinto/kinto.js
    - An Offline-First JavaScript client for Kinto.

- https://github.com/mkrd/DictDataBase /202310/python
  - A python NoSQL dictionary database, with concurrent access and ACID compliance
  - a fast document-based database that uses json files or compressed json files for storage.
  - [I made DictDataBase, it‘s like SQLite but for JSON! : Python_202210](https://www.reddit.com/r/Python/comments/yemdn4/i_made_dictdatabase_its_like_sqlite_but_for_json/)

- https://github.com/nire0510/jsoq /GPLv3/202310/ts
  - Query and manipulate JSON arrays easily. 
  - Powered by lodash, inspired by knex and SQL in general.

- https://github.com/microsoft/documentdb /MIT/202502/c
  - DocumentDB offers a native implementation of document-oriented NoSQL database, enabling seamless CRUD operations on BSON data types within a PostgreSQL framework. 
  - Powering vCore-based Azure Cosmos DB for MongoDB.
  - https://x.com/marcoslot/status/1883264982110064952
    - I helped create the first version of this while at Microsoft and it has a lot of neat tricks. It takes a Mongo query expressed as BSON, and then rewires things in planner/executor hooks to ultimately run an elaborate SQL query with joins and custom operators that use RUM indexes
# object-storage/s3
- minio /36.1kStar/AGPLv3/202211/go
  - https://github.com/minio/minio
  - https://min.io/download
  - MinIO is a High Performance Object Storage
  - It is API compatible with Amazon S3 cloud storage service.

- Zenko CloudServer /1.5kStar/apache2/202302/js
  - https://github.com/scality/cloudserver
  - https://www.zenko.io/cloudserver
  - CloudServer (formerly S3 Server) is an open-source Amazon S3-compatible object storage server 
  - CloudServer provides a single AWS S3 API interface to access multiple backend data storage both on-premise or public in the cloud.
  - 支持的存储backend: file, in-memory, multiple
  - [Getting Started](https://s3-server.readthedocs.io/en/latest/GETTING_STARTED.html)
  - [Add S3 SELECT functionality · Issue](https://github.com/scality/cloudserver/issues/3247)
    - Current behavior: Entire file must be pulled back to process one column
    - [Amazon S3 Select supports only the SELECT SQL command.](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-glacier-select-sql-reference-select.html)
  - CloudServer is useful for Developers, either to run as part of a continuos integration test environment to emulate the AWS S3 service locally or as an abstraction layer

- s3rver /471Star/MIT/202110/js/inactive
  - https://github.com/jamhall/s3rver
  - A fake S3 server written in NodeJs
  - It is extremely useful for testing S3 in a sandbox environment without actually making calls to Amazon.

- https://github.com/slatedb/slatedb /apache2/202409/rust
  - https://slatedb.io/
  - A cloud native embedded storage engine built on object storage
  - SlateDB is an embedded storage engine built as a log-structured merge-tree. 
  - Unlike traditional LSM-tree storage engines, SlateDB writes data to object storage (S3, GCS, ABS, MinIO, Tigris, and so on). 
    - Leveraging object storage allows SlateDB to provide bottomless storage capacity, high durability, and easy replication. 
  - 🆚️ The trade-off is that object storage has a higher latency and higher API cost than local disk.
    - To mitigate high write API costs (PUTs), SlateDB batches writes. 
    - To mitigate write latency, SlateDB provides an async put method.
    - To mitigate write latency, SlateDB provides an async put method.

- https://github.com/sanity-io/groq-store
  - In-memory GROQ store. Streams all available documents from Sanity into an in-memory database and allows you to query them there.
# tree-like/nested
- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.
  - Limitations
    - It is assumed that you have children of each node in a single array object
    - Self referencing objects at any point in the tree are not supported
    - An id field is required to perform better change detection (using idKey option).

- https://github.com/Voronenko/Storing_TreeView_Structures_WithMongoDB
  - Educational repository demonstrating approaches for storing tree structures with NoSQL database MongoDB
  - using five typical approaches plus one combination of operating with hierarchy data on example of the MongoDB database.

- https://github.com/jlxw/static-json-db
  - A NoSQL key-value database stored as a directory tree of small JSON files which can be deployed as part of a static website and queried from client browsers in an efficient manner. 
  - Data is stored in JSON files which are branched into smaller JSON files as size tresholds are met. 
  - static-json-db can be a lower-cost alternative to traditional databases that do not need to be updated frequently. 

- https://github.com/epochtalk/treedb
  - Database for tree structured data
  - LevelDB backend for hierarchical data.
# sql on mongodb
- https://github.com/synatic/sql-to-mongo /18Star/MIT/202212/js
  - Converts M-SQL Queries to Mongo find statements or aggregation pipelines.
  - M-SQL is a specific way to use MySQL style queries tailored to MongoDB functions 
  - Parses the given SQL statement to an aggregate or query depending on if a straight query is possible.

- https://github.com/Ligengxin96/sql-in-mongodb /202108/ts/inactive
  - convert common sql query to mongodb query

- https://github.com/orgoldfus/sql2mongo /202012/js/inactive
  - Parses an SQL WHERE clause to a mongo query object.

- https://github.com/gordonBusyman/mongo-to-sql-converter
  - convert MongoDB query (find()) to SQL
  - takes string as input and gives string as output. It supports only db.find method

- https://github.com/fabianTMC/mongoToSQL /202204/js
  - Convert MongoDB aggregation pipelines to their SQL equivalent
# mongo-gui
- https://github.com/mongodb-js/compass /SSPL/202401/ts
  - https://mongodb.com/compass
  - the source code and build tooling used in MongoDB Compass.
  - 提供了很多Plugins

- https://github.com/mongo-express/mongo-express /MIT/202312/js/传统bootstrap风格
  - A web-based MongoDB admin interface written with Node.js, Express, and Bootstrap3
  - Connect to multiple databases
  - GridFS support - add/get/delete incredibly large files
  - https://github.com/mrvautin/adminMongo /201906/js/inactive

- https://github.com/arunbandari/mongo-gui /MIT/202311/ts
  - http://20.169.156.177:4321/
  - A web-based MongoDB graphical user interface.
  - 前端依赖angular.v8、ng-zorro-antd、zone.js
  - 后端依赖express、mongodb、bson
  - Connect to local/remote mongodb instances
  - View/add/delete databases
  - Import CSV or JSON files
  - Export collection to CSV or JSON files
# mongo-utils
- https://github.com/Ligengxin96/sql-in-mongodb /3Star/GPLv3/202108/ts
  - This tools can convert common sql query to mongodb query
- https://github.com/orgoldfus/sql2mongo /202012/js
  - Use SQL syntax to query MongoDB
  - Parses an SQL WHERE clause to a mongo query object.

- https://github.com/nodkz/mongodb-memory-server /MIT/202401/ts
  - This package spins up an actual/real MongoDB server programmatically from within nodejs, for testing or mocking during development. 
  - By default it holds the data in memory. 
  - On install, this package downloads the latest MongoDB binaries and saves them to a cache folder.
  - Every `MongoMemoryServer` instance creates and starts a fresh MongoDB server on some free port. You may start up several `mongod` simultaneously.

- https://github.com/tkssharma/nodejs-db-orm-world /202003/ts
  - Node JS with different ORM like Typeorm, Knex, Prisma and Sequelize with Node JS API Development Node JS with without any ORM (MYSQL raw queries)

- https://github.com/slacy/minimongo /202001/python
  - a lightweight, schemaless, Pythonic Object-Oriented interface to MongoDB

- https://github.com/scottrogowski/mongita /BSD/202304/python/inactive
  - a lightweight embedded document database that implements a commonly-used subset of the MongoDB/PyMongo interface
  - instead of being a server, Mongita is a self-contained Python library. 
  - Mongita can be configured to store its documents either on disk or in memory.

- https://github.com/danstocker-legacy/jorder /201507/js/inactive
  - Jorder makes working with in-memory table data fast and simple. 
  - Based on Sntls, it allows you to re-interpret table and index data structures as collections, trees, etc. and thus formulate very expressive and effective data queries.
  - Smarter indexes: Jorder allows multi-field full-text indexes.
  - [Benchmarks](https://github.com/danstocker-legacy/jorder/wiki/Benchmarks)

- https://github.com/mongodb-js/mongodb-language-model /202004/js/inactive
  - Parses MongoDB query language and creates hierarchical Ampersand.js models to interact with the query tree
  - Parses a MongoDB query and creates an abstract syntax tree (AST) with part of speech tagging. 
  - Currently, only strict extended json syntax is supported
- https://github.com/fcoury/mongodb-language-model-rust 
  - ported from Node.js and PEGjs to Rust and pest.rs

- https://github.com/MyIsaak/sqlitemongo /202212/ts/inactive
  - Migrate your sqlite3 database to mongodb.
  - It copies all tables from sqlite3 into mongo collections under a specified database. 
- https://github.com/J-F-Liu/sqlite2mongo /202203/rust/inactive
  - Import sqlite database to mongodb.
  - Differences to sqlitemongo
    - DateTime, Boolean field types are reserved.
    - Supports dry-run and convert field name to mixed case.

- https://github.com/thomas4019/mongo-query-to-postgres-jsonb /MIT/202312/js
  - Converts MongoDB queries to postgresql queries for jsonb fields.
  - This tool converts a Mongo query to a PostgreSQL where clause for data stored in a jsonb field.
  - This tool is used by `pgmongo` which intends to provide a drop-in replacement for MongoDB.
# mongo-sync/collab
- https://github.com/share/sharedb-milestone-mongo /202309/js
  - A Mongo implementation of the ShareDB Milestone Database API

- https://github.com/capaj/Moonridge /MIT/201703/js
  - http://capaj.github.io/Moonridge
  - Mongo live query framework bootstrapped on socket.io-rpc and mongoose
  - isomorphic client side library and server framework, which brings Mongoose model to the browser(or over the network to other node process). 
  - the coolest feature is live queries. These are performance hungry, but Moonridge is caching live queries in memory
  - why not just port mongoosejs to the client side and let clients talk to mongo directly. While this would surely be an interesting project, Moonridge has features which would not be possible without a server instance(live querying, custom authorization/authentication). I think these features are worth it introducing a new framework to the backend.
# nosql
- https://github.com/petersirka/nosql /201907/js/inactive
  - NoSQL embedded database for small node.js projects
  - Supports views
  - Supports simple filtering
  - Total.js framework uses NoSQL embedded database

- https://github.com/zelaxo/lazlodb /apache2/201902/js
  - http://lazlo.yenvo.io/
  - a portable, compact & serverless NoSql database built using Node JS & MessagePack
  - Data is stored in .laz files in MessagePack encoded form. As MessagePack is smaller than JSON, it takes less space & hence the files are compact.
  - Each .laz file represents a document (or a table in sql).
  - All documents exist in a database, which is essentially a folder being tracked by lazlo.
  - https://github.com/zelaxo/lazlo-node

- https://github.com/finalclass/finaldb /201402/js
  - Database system using streams and file system. NoSql way
  - Final DB is a NoSQl database that uses file system as a storage.
  - It's totally asynchronous. No synchronous function is called in it's code.
  - It uses `when` library for async calls. Every async function returns a `Promise`.
  - Uses `final-fs` library for file system manipulation.

- https://github.com/Softmotions/ejdb /c
  - Embeddable JSON Database engine C library. 
  - Simple XPath like query language (JQL).

- https://github.com/event-driven-io/Pongo /MIT/202407/ts
  - https://event-driven-io.github.io/Pongo/
  - Mongo but on Postgres and with strong consistency benefits
  - How does it work?
    - Pongo treats PostgreSQL as a Document Database benefiting from JSONB support
    - Pongo takes MongoDB api and translates it to the native PostgreSQL queries
  - How is it different than FerretDB?
    - FerretDB plugs into the native MongoDB protocol, which allows it to be used as MongoDB and connect to tools like Mongo UI, etc
    - Pongo operates on a different layer, translating the MongoDB API directly into SQL in the library code

- https://github.com/FerretDB/FerretDB /8.2kStar/apache2/202402/go
  - https://www.ferretdb.io/
  - FerretDB (previously MangoDB) was founded to become the de-facto open-source substitute to MongoDB
  - 直接在PostgreSQL上对外提供 MongoDB 的 API
  - FerretDB is an open-source proxy, converting the MongoDB 6.0+ wire protocol queries to SQL - using PostgreSQL or SQLite as a database engine
  - It functions as a drop-in replacement for MongoDB 6.0+ in many cases. 
  - [FerretDB: open-source MongoDB alternative | Hacker News_202304](https://news.ycombinator.com/item?id=35539464)
  - [FerretDB v1.2.0_20230522](https://blog.ferretdb.io/ferretdb-v-1-2-0-minor-release/)
    - support SQLite database backend. 
# more-document-json
- https://github.com/ashleydavis/sql-to-mongodb
  - A Node.js script to convert an SQL database to a MongoDB database.

- https://github.com/RonnyChen/MongoSql /201601/java
  - 直接将部分SQL转换成mongodb的语句访问mongodb

- https://github.com/huggingface/Mongoku
  - MongoDB client for the web. Query your data directly from your browser
  - Built on TypeScript/Node.js/Angular.
