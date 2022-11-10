---
title: toc-database-document-mongodb-json
tags: [database, json, mongodb, toc]
created: 2022-06-13T03:56:47.999Z
modified: 2022-11-03T04:14:11.987Z
---

# toc-database-document-mongodb-json

# guide
- 更适合block-editor的数据结构是否是 mongodb？
# mongodb-like
- minimongo /1kStar/LGPLv3/202207/ts
  - https://github.com/mWater/minimongo
  - A client-side MongoDB implementation which supports basic queries, including some geospatial ones.
  - It is either IndexedDb backed (IndexedDb), WebSQL backed (WebSQLDb), Local storage backed (LocalStorageDb) or in memory only (MemoryDb).
  - Uses code from Meteor.js minimongo package, reworked to support more geospatial queries 

- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
  - One datastore is the equivalent of a MongoDB collection
  - Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
  - [Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)
  - forks
    - https://github.com/seald/nedb  /active
      - Embedded persistent or in memory database for Node.js, Electron and browsers, 100% JavaScript, no binary dependency
    - https://github.com/bajankristof/nedb-promises
      - A dead-simple promise wrapper for nedb.
      - As of nedb-promises 5.0.0 nedb package has been replaced with a fork seald/nedb
    - https://github.com/ArcBlock/nedb  /js/no-browser
      - NEDB fork and multi-process support
      - Use @nedb/mongoose-driver as a drop-in replacement for mongoose + mongodb to make apps lightweight
      - if you want to use nedb in browser, please use the original version.
    - https://github.com/GrayHat12/nedb
    - https://github.com/HalleyAssist/nedb
    - https://github.com/Akumzy/nedb-async
      - promise base wrapper methods for Nedb
    - https://github.com/JamesMGreene/nestdb
      - originally forked from NeDB
- https://github.com/Techpire/db
  - 👉🏻 nedb typescript conversion
  - differences
    - Index field with an array value are explicitly not supported.
    - Inserting a duplicate key will overwrite the existing key.
    - Keys must all be the same data type.
- https://github.com/tedb-org/teDB /201908/ts/inactive
  - A structure sane embedded database with pluggable storage and clean concise documentation.
  - TeDB uses an AVL balanced binary tree binary-type-tree to save indexed fields of documents.
  - a storage driver that can either work to persists data to disk or save data to memory. 
- https://github.com/typicode/lowdb /active/ts
  - a small local JSON database powered by Lodash 
  - supports Node, Electron and the browser
  - Change storage, file format (JSON, YAML, ...) or add encryption via adapters
- https://github.com/ivrusson/mockon
  - Mock Server with data persistency based on MockJS and NeDB
- https://github.com/harshgupta97/localhostdb
  - DB server for persistance and in-memory data storage using express and nedb, desktop application built using electron can leverage this to storage data locally.
- https://github.com/marcusjwhelan/nedb-shell
  - A Mongo like shell for NeDB
- https://github.com/mattd-silva22/node-url-shorten-api
  - a url shorten api made if Node.js , Express , TypeScript ans NeDB
- https://github.com/low-teck/vault
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.
- https://github.com/abeegit/bibliothek
  - React and Express + NeDB app that lets you add, edit and display books in the inventory. 
- https://github.com/bi-tm/express-nedb-rest
  - REST API for NeDB database, based on express HTTP server.
- https://github.com/rwl-dev-archive/learn-nedb-json-api
  - Express + NeDB = JSON API
  - https://github.com/gaoliveira21/nedb-crud
  - https://github.com/bluesky50/ts-api-server-express-multi-db
  - https://github.com/caickdias/crud-api-express-nedb-joi

- https://github.com/usmakestwo/githubDB /201811/js
  - A Lightweight Cloud based JSON Database with a MongoDB like API for Node.
  - You will never know that you are interacting with a Github

- https://github.com/arvindr21/diskDB /201712/js
  - A Lightweight Disk based JSON Database with a MongoDB like API for Node
  - You will never know that you are interacting with a File System

- yunodb /246Star/CC0/201704/js/leveldb
  - https://github.com/blahah/yunodb
  - A portable, persistent, electron-embeddable fulltext search + document store database for node.js
  - yuno is a JSON document store with fulltext search. 
  - The document store, which is just the raw JSON objects stored in leveldb/browser-level
  - yuno is being built to serve my use-case of embedding pre-made databases in electron apps
  - forks
    - https://github.com/pdepip/yunodb

- https://github.com/Belphemur/node-json-db
  - A simple "database" that use JSON file for NodeJS
  - Every method are now asynchronous

- picodb /31Star/MIT/202201/js
  - https://github.com/jclo/picodb
  - A tiny in-memory database (MongoDB like) that stores JSON documents
  - It runs both on Node.js and in the ES6 compliant browsers.
  - A document is a Javascript literal object. It is similar to a JSON object. 

- zangodb /1kStar/MIT/201710/js
  - https://github.com/erikolson186/zangodb
  - ZangoDB is a MongoDB-like interface for HTML5 IndexedDB that supports most of the familiar filtering, projection, sorting, updating and aggregation features of MongoDB, for usage in the web browser.

- https://github.com/Ivshti/linvodb3
  - LinvoDB is a Node.js/NW.js/Electron persistent DB with MongoDB/Mongoose-like features and interface.
  - MongoDB-like query language
  - Persistence built on LevelUP - you can pick back-end

- https://github.com/kofrasa/mingo
  - MongoDB query language for in-memory objects
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

- s3rver /471Star/MIT/202110/js
  - https://github.com/jamhall/s3rver
  - A fake S3 server written in NodeJs
  - It is extremely useful for testing S3 in a sandbox environment without actually making calls to Amazon.

- cloudserver /1.4kStar/apache2/202211/js
  - https://github.com/scality/cloudserver
  - Zenko CloudServer, an open-source Node.js implementation of the Amazon S3 protocol on the front-end and backend storage capabilities to multiple clouds, including Azure and Google.
  - CloudServer (formerly S3 Server) is an open-source Amazon S3-compatible object storage server 
  - CloudServer is useful for Developers, either to run as part of a continous integration test environment to emulate the AWS S3 service locally or as an abstraction layer

- https://github.com/sanity-io/groq-store
  - In-memory GROQ store. Streams all available documents from Sanity into an in-memory database and allows you to query them there.

- https://github.com/elmarti/camadb
  - a NoSQL embedded database written in pure TypeScript for Node, Electron and browser
  - SQLite doesn't (by default) return native JS data types (Dates in particular)
  - We use Mingo for aggregation - currently lookup commands aren't supported.
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
# mongodb-render-ui

# more-document-json
