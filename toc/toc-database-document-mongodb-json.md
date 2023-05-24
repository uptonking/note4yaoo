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

- tingodb /1.1kStar/MIT/201901/js
  - https://github.com/sergeyksv/tingodb
  - http://www.tingodb.com/
  - an embedded JavaScript in-process filesystem or in-memory database upwards compatible with MongoDB at the v1.4 API level.
  - Upwards compatible means that if you build an app that uses functionality implemented by TingoDB you can switch to MongoDB almost without code changes. 
  - https://github.com/sergeyksv/tungus
    - Mongoose driver for TingoDB

- ZangoDB /1kStar/MIT/201710/js
  - https://github.com/erikolson186/zangodb
  - https://erikolson186.github.io/zangodb/
  - ZangoDB is a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.
  - an implementation of IndexedDB is required. 
    - For environments without a native implementation of IndexedDB, https://github.com/dumbmatter/fakeIndexedDB can be used
  - forks
    - https://github.com/allwi290/zangodb
      - cjs to es

- ForerunnerDB /707Star/MIT/202006/js/v2+v3
  - https://github.com/Irrelon/ForerunnerDB
  - ForerunnerDB is a NoSQL JavaScript JSON database with a query language based on MongoDB (with some differences) and runs on browsers and Node.js.
  - ForerunnerDB supports data persistence on both the client (via LocalForage) and in Node.js (by saving and loading JSON data files).
  - ForerunnerDB is an in-memory store but you choose how often (if at all) data is loaded and saved with underlying storage engines.
  - https://github.com/Irrelon/forerunnerdb-core /202110/js/v3/inactive
    - This project contains the core query/match/update functionality of ForerunnerDB 3.x
    - forerunnerdb-core provides the core of ForerunnerDB 3.0 which is a complete rewrite of ForerunnerDB in ES6
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
  - forks
    - https://github.com/pdepip/yunodb

- https://github.com/usmakestwo/githubDB /201811/js
  - A Lightweight Cloud based JSON Database with a MongoDB like API for Node.
  - You will never know that you are interacting with a Github

- https://github.com/arvindr21/diskDB /201712/js
  - A Lightweight Disk based JSON Database with a MongoDB like API for Node
  - You will never know that you are interacting with a File System

- https://github.com/Belphemur/node-json-db
  - A simple "database" that use JSON file for NodeJS
  - Every method are now asynchronous

- https://github.com/anywhichway/joqular /201902/js
  - JavaScript Object Query Language Representation - Funny it's mostly JSON.
  - JOQULAR is a query language specification. 
  - Like SQL, JOQULAR allows you to mutate the returned records to meet you needs.
  - 不如json patch
# db-document-json
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
# mongodb-utils
- https://github.com/kofrasa/mingo /202211/ts
  - MongoDB query language for in-memory objects

- https://github.com/Ligengxin96/sql-in-mongodb /3Star/GPLv3/202108/ts
  - This tools can convert common sql query to mongodb query
- https://github.com/orgoldfus/sql2mongo /202012/js
  - Use SQL syntax to query MongoDB
  - Parses an SQL WHERE clause to a mongo query object.

- https://github.com/nodkz/mongodb-memory-server /202211/ts
  - This package spins up an actual/real MongoDB server programmatically from within nodejs, for testing or mocking during development. 
  - By default it holds the data in memory. 

- https://github.com/tkssharma/nodejs-db-orm-world /202003/ts
  - Node JS with different ORM like Typeorm, Knex, Prisma and Sequelize with Node JS API Development Node JS with without any ORM (MYSQL raw queries)

- https://github.com/slacy/minimongo /202001/python
  - a lightweight, schemaless, Pythonic Object-Oriented interface to MongoDB

- https://github.com/scottrogowski/mongita /202210/python
  - Mongita is a lightweight embedded document database that implements a commonly-used subset of the MongoDB/PyMongo interface
  - instead of being a server, Mongita is a self-contained Python library. 
  - Mongita can be configured to store its documents either on disk or in memory.
# non-js-json-db
- https://github.com/Softmotions/ejdb
  - Embeddable JSON Database engine C library. 
  - Simple XPath like query language (JQL).

- https://github.com/FerretDB/FerretDB /5kStar/apache2/202212/go
  - FerretDB (previously MangoDB) was founded to become the de-facto open-source substitute to MongoDB
  - 直接在PostgreSQL上对外提供 MongoDB 的 API
  - FerretDB is an open-source proxy, converting the MongoDB 6.0+ wire protocol queries to SQL - using PostgreSQL as a database engine.
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
