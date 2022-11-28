---
title: toc-database-document-nedb
tags: [database, json, nedb, toc]
created: 2022-11-26T17:34:59.095Z
modified: 2022-11-26T17:35:24.870Z
---

# toc-database-document-nedb

# guide

# nedb-like
- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
  - One datastore is the equivalent of a MongoDB collection
  - Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
    - For a Node.js/Node Webkit database it's the file system
    - For a browser-side database it's localforage, which uses the best backend available (IndexedDB then WebSQL then localStorage)
  - I consider NeDB to be feature-complete, i.e. it does everything I think it should and nothing more. As a general rule I will not accept pull requests anymore
  - [Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)

- nedb-forks
  - https://github.com/seald/nedb  /202209/js/active
    - forked it and maintain it for the needs of Seald.
    - Since version 3.0.0, NeDB provides a Promise-based equivalent for each function which is suffixed with Async
  - https://github.com/bajankristof/nedb-promises /202209/js
    - A dead-simple promise wrapper for nedb.
    - As of nedb-promises 5.0.0 nedb package has been replaced with a fork seald/nedb
  - https://github.com/ArcBlock/nedb  /202210/MIT/js/no-browser/多线程
    - a NEDB fork used by ArcBlock products.
    - Use @nedb/multi to read and write to the same database in different node.js processes
    - Use @nedb/mongoose-driver as a drop-in replacement for mongoose + mongodb to make apps lightweight
    - if you want to use nedb in browser, please use the original version.
  - https://github.com/HalleyAssist/nedb /202211/js
    - Embedded datastore for node.js
  - https://github.com/Akumzy/nedb-async
    - a simply promise base wrapper methods for Nedb
  - https://github.com/JamesMGreene/nestdb /201903/js
    - originally forked from NeDB

- https://github.com/Techpire/db /1Star/MIT/202203/ts
  - 👉🏻 nedb typescript conversion
  - differences
    - Index field with an array value are explicitly not supported.
    - Inserting a duplicate key will overwrite the existing key.
    - Keys must all be the same data type.
- https://github.com/tedb-org/teDB /201908/ts/inactive
  - A structure sane embedded database with pluggable storage and clean concise documentation.
  - TeDB uses an AVL balanced binary tree `binary-type-tree` to save indexed fields of documents.
  - a storage driver that can either work to persists data to disk or save data to memory. 
  - It is not exactly like nedb. It should be able to handle very large collections.
  - https://github.com/marcusjwhelan/binary-type-tree
    - AVL Tree for Node and the browser with TypeScript
    - I forked the binary tree written in nedb and rewrote most of it and added some extra restrictions and capabilities
- https://github.com/scottwrobinson/camo /202108/js/inactive
  - A class-based ES6 ODM for Mongo-like databases.
  - Camo was created for two reasons: to bring traditional-style classes to MongoDB JavaScript, and to support NeDB as a backend
  - Camo was designed and built with multiple Mongo-like backends in mind, like NeDB, LokiJS*, and TaffyDB*.

- lowdb /18.7Star/MIT/202211/ts
  - https://github.com/typicode/lowdb
  - Simple to use local JSON database.
  - supports Node, Electron and the browser
  - adapters: JSONFile/Memory/LocalStorage/TextFile
    - Change storage, file format (JSON, YAML,XML,remote-storage ...) or add encryption via adapters
    - An adapter is a simple class that just needs to expose two methods: read/write
  - Lowdb doesn't support Node's cluster module.
  - If you have large JavaScript objects (~10-100MB) you may hit some performance issues. 
    - This is because whenever you call `db.write`, the whole `db.data` is serialized using `JSON.stringify` and written to storage.
    - If you plan to scale, it's highly recommended to use databases like PostgreSQL or MongoDB instead.
  - who is using
    - json-server

- https://github.com/ivrusson/mockon
  - Mock Server with data persistency based on MockJS and NeDB
- https://github.com/harshgupta97/localhostdb
  - DB server for persistance and in-memory data storage using express and nedb, desktop application built using electron can leverage this to storage data locally.
- https://github.com/marcusjwhelan/nedb-shell
  - A Mongo like shell for NeDB
# examples
- https://github.com/mattd-silva22/node-url-shorten-api
  - a url shorten api made if Node.js , Express , TypeScript ans NeDB
- https://github.com/wheresvic/shorty
  - A simple self-hostable private url shortener using Node.js & Nedb (a file-based Mongodb API compatible db).
  - The idea behind shorty was to have a simple url shortening service that could be hosted on a cheap VPS with less than 1Gb RAM. Therefore, shorty uses only file-based storage to keep dependencies to a minimum.
- https://github.com/elunico/URL-Shortener
  - A simple URL shortener in using Node, Express, and Nedb
  - Regardless of whether you use the API directly or the client-side interface, you are limited to creating 50 short URLs an hour 

- https://github.com/low-teck/vault
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.
- https://github.com/abeegit/bibliothek
  - React and Express + NeDB app that lets you add, edit and display books in the inventory. 
# nedb-crud
- https://github.com/bi-tm/express-nedb-rest
  - REST API for NeDB database, based on express HTTP server.
- https://github.com/rwl-dev-archive/learn-nedb-json-api
  - Express + NeDB = JSON API
  - https://github.com/gaoliveira21/nedb-crud
  - https://github.com/bluesky50/ts-api-server-express-multi-db
  - https://github.com/caickdias/crud-api-express-nedb-joi
# more-nedb
