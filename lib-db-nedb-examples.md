---
title: lib-db-nedb-examples
tags: [database, examples, json, nedb, toc]
created: 2022-11-26T17:34:59.095Z
modified: 2023-09-28T20:33:44.333Z
---

# lib-db-nedb-examples

# guide
- 不支持同步

- 参考替代方案如何解决全量数据载入内存的问题
# nedb-like
- nedb /13.1kStar/MIT/201602/js
  - https://github.com/louischatriot/nedb
  - Embedded persistent or in memory database for Node.js, nw.js, Electron and browsers, 100% JavaScript, no binary dependency. 
  - API is a subset of MongoDB's and it's plenty fast.
    - One datastore is the equivalent of a MongoDB collection
  - A copy of the whole database is kept in memory. This is not much on the expected kind of datasets (20MB for 10000 2KB documents).
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
    - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
    - For a Node.js/Node Webkit database it's the file system
    - For a browser-side database it's `localforage`, which uses the best backend available (IndexedDB then localStorage)
    - Under the hood, NeDB's **persistence uses an append-only format**, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - I consider NeDB to be feature-complete, i.e. it does everything I think it should and nothing more. As a general rule I will not accept pull requests anymore
  - 依赖 https://github.com/louischatriot/node-binary-search-tree
  - [Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)

- https://github.com/seald/nedb /202209/js/active
  - forked it and maintain it for the needs of Seald.
  - Since version 3.0.0, NeDB provides a Promise-based equivalent for each function which is suffixed with `Async`.
  - https://github.com/bajankristof/nedb-promises /202209/js
    - A dead-simple promise wrapper for nedb.
    - As of nedb-promises 5.0.0 nedb package has been replaced with a fork seald/nedb
  - https://github.com/levg34/typescript-nedb-orm
    - ORM for @seald-io/nedb written in TypeScript
- https://github.com/rmanibus/nedb
  - [Implement Compound Indexes ](https://github.com/seald/nedb/pull/27)
- https://github.com/ArcBlock/nedb  /202210/MIT/js/no-browser/多线程
  - a NEDB fork used by ArcBlock products.
  - Use @nedb/multi to read and write to the same database in different node.js processes
  - Use @nedb/mongoose-driver as a drop-in replacement for mongoose + mongodb to make apps lightweight
  - if you want to use nedb in browser, please use the original version.
  - https://github.com/vangelov/nedb-multi /201705/js
    - A proxy for NeDB which allows for multi-process access
    - I decided to try a similar, but lock-free approach, using the axon framework
    - There's still only one master process that the others connect to, but there are no locks. 
    - Also, both callback- and cursor-based methods are supported. 
    - https://github.com/tj/axon
      - message-oriented socket library for node.js heavily inspired by zeromq
    - https://github.com/thelarz/nedb-multi
      - Allow host listen ip arg so I can run on machine without internet access
  - https://github.com/allain/nedb-party /201703/js
    - A library for making nedb multi-process capable.
    - Basically, it'll check to see if another process has the db locked, if it does, it'll send requests to that process, through rpc, to perform change operations.
    - it does not support methods that return cursors. 
    - It also relies on each process starting a http server on the same port and whichever manages to start listening becomes the master and the others connect to it.
- https://github.com/salmanff/nedb-asyncfs /202203/js
  - This fork allows you to store the database files on async storage mediums like aws or dropbox. 
  - You should not use nedb-asyncfs for in-browser functionality.
- https://github.com/OneBitAhead/nedb-x /202203/js/很多小功能
  - Functional extension to NeDB
  - Group by with aggregates
 Substructure database with model attribute
 - Joining (left join) model data
 - Tree data (with open/closed nodes)

- mani /12Star/MIT/201606/js/lunr
  - https://github.com/glennjones/mani
  - Mani provides a document based search tool in javascript, for browser and node.js 
  - 依赖nedb、localForage、lunr.js、geolib
  - It merges together free text search, mongodb type queries, geo search and facets from other projects into one library.
  - Serialize data and indexes to and from a JSON file

- feathers-nedb-fuzzy-search /11Str/MIT/202012/js
  - https://github.com/FossPrime/feathers-nedb-fuzzy-search
  - NeDB adapter for fuzzy search, api compatible with the MongoDB version
  - Add fuzzy `$search` to NeDB `service.find` queries.
  - 依赖 @seald-io/nedb
  - https://github.com/trinly01/feathers-nedb-puzzy-search

- https://github.com/ivanvaladares/Node-Suggestive-Search
  - built to help type-ahead and dropdown search boxes and also correct misspelled searches (did you mean?).
  - This module is compatible with: nedb v1.8, mongodb v2.2, redis 2.8

- nedb-forks
  - https://github.com/HalleyAssist/nedb /202211/js
    - Embedded datastore for node.js
  - https://github.com/Akumzy/nedb-async
    - a simply promise base wrapper methods for Nedb
  - https://github.com/JamesMGreene/nestdb /201903/js
    - originally forked from NeDB
    - support inserted, updated and removed events
  - https://github.com/Techpire/db /1Star/MIT/202203/ts/half-baked
    - nedb typescript conversion
    - differences
      - Index field with an array value are explicitly not supported.
      - Inserting a duplicate key will overwrite the existing key.
      - Keys must all be the same data type.

- LinvoDB3 /746Star/MIT/202008/js/leveldb
  - https://github.com/Ivshti/linvodb3
  - LinvoDB is a Node.js/NW.js/Electron persistent DB with MongoDB/Mongoose-like features and interface.
  - MongoDB-like query language
  - Persistence built on LevelUP
  - NW.js/Electron friendly - JS-only backend is level-js or Medea(kv)
  - 👉🏻 LinvoDB is based on NeDB, the most significant core change is that it uses LevelUP as a back-end, meaning it doesn't have to keep the whole dataset in memory. 
  - LinvoDB also can do a query entirely by indexes, meaning it doesn't have to scan the full database on a query.
    - LinvoDB does the entire query through the indexes, NeDB scans the DB
  - [It looks like we build similar database engine(tingodb)](https://github.com/louischatriot/nedb/issues/34)
    - I wrote a DB engine over NeDB/LevelUP which auto-indexes so that each query can run indexed and avoid scanning.
    - It doesn't load the full datastore in memory, and with large datasets it's faster than NeDB because of full indexing.
  - forks
  - https://github.com/aerys/linvodb3
  - https://github.com/aerys/mongoose-linvodb3 /升级leveldown
  - https://github.com/wittyPuneet/linvodb3
  - https://github.com/Absio/linvodb3-with-serialization-options
    - LinvoDB fork for adding extension option into Model.
    - beforeDeserialization, afterSerialization
- https://github.com/Ivshti/linvodb-fts
  - full text search in memory - linvodb-fts - trie/metaphone; using natural
- https://github.com/Ivshti/linvo-p2p-sync
  - Syncing between a key-value store and the Linvo API
- https://github.com/Ivshti/linvodb-slides
  - Slides for talk at bulgariawebsummit
- https://github.com/mohammedahmed18/electron-app /202210/ts
  - 依赖linvodb3、realm10、reduxjs-toolkit
- https://github.com/dmfarcas/clipboard-manager
  - A simple cross platform clipboard manager.
- https://github.com/ZorrillosDev/watchit-app /202209/js
  - Watchit is a movie playback system, in its most basic form it allows you to filter, search, play movies
  - 依赖orbit-db、linvodb3
- https://github.com/martpie/museeks /202209/ts
  - cross-platform music player
- https://github.com/jullinator/electron
  - npm install npm start
- https://github.com/kidando/json_data_manager
  - An Electron desktop app that allows you to perform CRUD operations on tables/collections that are stored as json files. 
- https://github.com/fullstackio/realtime-news
  - real-time news server with current events, twitter, websocket support
  - Combining the speed of NeDB with the live query capabilities of leveldb, LinvoDB is a good choice for speed and single-node database requirements.

- tingodb /1.1kStar/MIT/201901/js/不直接支持浏览器环境
  - https://github.com/sergeyksv/tingodb
  - http://www.tingodb.com/
  - an embedded JavaScript in-process filesystem or in-memory database upwards compatible with MongoDB at the v1.4 API level.
  - all tests are designed to work on both MongoDB using its native driver and TingoDB
  - Full set of MongoDB search operators is supported.
  - 内存中默认不存放全量数据，放的是索引
    - TingoDB uses memory only for indexes and optional cache. 
    - It loads collection documents using file access operations. 
    - We estimated memory consumption vs data-set size ratio as 1:100. 
    - This of course depends on amount of indexes that database uses.
    - all indexes are all in memory, by default only `_id:1` index is maintained.
  - TingoDB supports B-tree indexes that stored in memory. 
    - Indexes are used for search query optimizations and mimics MongoDB indexes (spare, unique and so on). 
    - Compound indexes are not supported yet.
  - Database stored as a folder where each file represent single collection. 
    - Collection files used in append only mode which ensures safe access to data but can cause space overuse as you update your data. 
    - As workaround for this database will make automatic compactization
  - Documents itself serialized using JSON
    - We did some benchmarks using BSON, MessagePack ans some others. The winner was JSON.
    - Every document represented by 3 objects in data file. First is constant size header, second is variable size header and the last is document itself. This approach allows to increase initial file load speed and give us some freedom for future changes.
  - [does tingodb can use on browser](https://github.com/sergeyksv/tingodb/issues/112)
    - no. code itself has no any dependencies that will not work in browser except persistence layer. There was no plans to make it work in browser as I see no much purpose for this.
  - [[FR] write indexes in a separated file](https://github.com/sergeyksv/tingodb/issues/151)
    - One great way to improve it, i think, would be to write indexes and actual data in separated files.
  - https://github.com/sergeyksv/tungus
    - Mongoose driver for TingoDB
  - forks
    - https://github.com/alancnet/tingodb
      - Return promises if callback is not specified
- https://github.com/turinglabsorg/nodejs-express-starter
  - Personal NodeJS starter with TingoDB, TypeScript, BodyParser and CORS
  - https://github.com/lean-stack/node.tingo-rest
- https://github.com/akil-io/storage-tingodb
  - The simplest ever MongoDB object relation mapper and data access library
- https://github.com/zahiruldu/change-track
  - Web content change tracker
- https://github.com/alanning/mongodb-in-memory
  - MongoDB compatible in-memory database for unit testing using TingoDB.
  - It converts TingoDb's API to Promise API
  - https://github.com/TheBrainFamily/tingodb-promise
- https://github.com/RobertoMalatesta/tingo-db-gui-manager
  - GUI manager for TingoDB/MongoDB built using React & Tungus itself.

- teDB /83Star/MIT/201802/ts/inactive
  - https://github.com/tedb-org/teDB
  - A structure sane embedded database with pluggable storage
  - TeDB uses an AVL balanced binary tree `binary-type-tree` to save indexed fields of documents.
  - a storage driver that can either work to persists data to disk or save data to memory. 
  - It is not exactly like nedb. It should be able to handle very large collections.
  - TeDB was made with pure intention to work on electron. The only storage driver I have written is the TeDB electron storage driver.
  - The binary tree only saves the value and `_id` to memory allowing for larger data sets to be indexed.
  - Almost all operations use a method of the storage driver to save, delete, or search, for documents. 
    - When creating a storage driver that persists to a filesystem for FAT32, NTFS, ext2, ext3, and ext4, most directories use a binary tree store the location of the file. 
    - So utilizing this it is faster to query the file instead of having to create another binary tree to hold the location of a document in a file. 
  - https://github.com/marcusjwhelan/binary-type-tree
    - AVL Tree for Node and the browser with TypeScript
    - I forked the binary tree written in nedb and rewrote most of it and added some extra restrictions and capabilities

- blinkdb /59Star/MIT/202211/ts/不支持sync
  - https://github.com/blinkdb-js/blinkdb
  - https://blinkdb.io/
  - 依赖sorted-btree
  - An in-memory JS database optimized for large scale storage on the frontend.
    - With database features such as **indexes**, **query optimization** and support for both relational & non-relational data, BlinkDB allows you to query your data with filters, sort and paginate in one go - just like a real database, and just as performant
  - stores like Redux or MobX - are not optimized for performance with large quantities of entities.
  - Keep your UI reactive by watching for changes on your database.
    - it’s a bad idea to query the database everytime you want to render its items in your components
    - watch() will observe a table and call the provided callback every time an item is inserted, updated, or deleted
  - Filter, sort, and implement pagination directly within BlinkDB.
  - [BlinkDB has a powerful query system and can filter, sort & limit your data](https://blinkdb.io/docs/filters/)
    - in order to prevent loading all items at once
    - in the backend, this is most often solved by offset-based pagination or cursor-based pagination - both of which BlinkDB supports.

- camo /202108/js/inactive/odm(object document mapper)
  - https://github.com/scottwrobinson/camo
  - A class-based ES6 ODM for Mongo-like databases.
  - Camo was created for two reasons: to bring traditional-style classes to MongoDB JavaScript, and to support NeDB as a backend
  - Camo was designed and built with multiple Mongo-like backends in mind, like NeDB, LokiJS*, and TaffyDB*.
- https://github.com/jaykukadiya99/neDB-with-nodeJs
  - 依赖camo
  - Nodejs simple application with NeDB (camo package like mongoose for mongodb and NeDB)
- https://github.com/seald/follicle
  - a fork of camo made for the needs of Seald
  - A class-based ES6 ODM for Mongo-like databases
- https://github.com/4strid/nekodb /201910/js
  - Tiny ODM for MongoDB/NeDB
  - NekoDB comes with NeDB built in
  - [Nekodb A tiny ODM for Nedb and Mongodb](https://aghae.github.io/post/Nekodb%20A%20tiny%20ODM%20for%20Nedb%20and%20Mongodb/)
- https://github.com/bengl/mongosmash
  - simple ODM for MongoDB and NeDB on Node.js (using JS Harmony).

- [Nedb Encryption & Decryption](https://gist.github.com/bllohar/28ee29b3304d8bf6dbc11d1b16b00130)
  - Note that I don't process any JSON because there's really no need to since `afterSerialization` takes a string and `beforeDeserialization` returns a string.
  - [Database encryption with NeDB](https://gist.github.com/jordanbtucker/e9dde26b372048cf2cbe85a6aa9618de)

- qbase /1Star/Unlicensed/202012/ts/sift
  - https://github.com/abhishiv/qbase
  - lightweight and fast in-memory data store with support for lazy queries, watchable queries, transactions, H1/HM/MTM/BT relationships, and MongoDB styled selectors.
  - 依赖sift
  - Written to be an lightweight functional alternative to `@apollo/client`

- lowdb /20.2kStar/MIT/202310/ts/代码少
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
  - [data not sync from two instance for pm2 ( exec_mode cluster)](https://github.com/typicode/lowdb/issues/344)
    - Sorry, lowdb doesn't support concurrency/clusters, instead it's supposed to be run in one instance.
    - You can force a re-read by calling db.read() though, but you'll probably have issues so I wouldn't recommend that
  - [Whether to support cluster](https://github.com/typicode/lowdb/issues/100)
    - When using lowdb, you should always have a single Node instance running.
    - If you have 2 instances of Node, each will have a different version of your database but both will write to one file and one of the instance data will be lost.
  - [Can you use more than one instance of lowdb?](https://github.com/typicode/lowdb/issues/296)
    - Yes, it's possible. Simply create 2 adapters/db instance
  - used-by
    - json-server

- sync_server-nedb /33Star/MIT/201807/js
  - https://github.com/nponiros/sync_server
  - A simple server which can be used to synchronize data from multiple devices
  - A small node server which uses NeDB to write data to the disk. 
    - The database used to store the data. Currently only NeDB is supported
  - The server can be used with a client for example `SyncClient` to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the `ISyncProtocol` and `Dexie.Syncable`. 
    - 👉🏻 It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
- sync_client-dexie /29Star/MIT/201804/js
  - https://github.com/nponiros/sync_client
  - This module can be used to write data to IndexedDB using `Dexie` and to synchronize the data in IndexedDB with a server.
  - `Dexie.Syncable` is used for the synchronization. This module contains an implementation of the `ISyncProtocol`. 
  - It was primarily written to work with `sync-server` but should work with other servers which offer the same API.

- https://github.com/Ligengxin96/sql-in-mongodb /3Star/GPLv3/202108/ts
  - This tools can convert common sql query to mongodb query
# examples
- rhaego(blog starter) /29Star/ISC/202204/js
  - https://github.com/youknowznm/rhaego
  - 基于 react + koa, 开箱即用的 Material Design 风格博客系统
  - 依赖 koa、nedb、marked、react-router5、highlight.js
  - 基于嵌入式数据库 NeDB, 即插即用
  - 未使用任何组件库/样式库/动画库
  - 访客无需注册即可对文章点赞和评论
  - 编辑文章时, 实时预览 markdown
  - 根据配置展示 GitHub 仓库, 社交资料和个人简历
  - 根据真实客户端 IP 限制访客的有效请求次数
  - https://github.com/youknowznm/mini-express
    - 尝试实现一个极简的 express 风格服务器, 实现路由池, 中间件和对请求及响应的部分增强. 

- https://github.com/low-teck/vault /202202/ts
  - A react-electron app that secures user data locally using AES algorithm with the help of nedb and crypto-js ans styled with chakra-ui.

- https://github.com/abeegit/bibliothek /202101/ts/client+server
  - React and Express + NeDB app that lets you add, edit and display books in the inventory. 

- https://github.com/RodgerLai/nodejs-nedb-excel /201703/js
  - 基于nodejs+webpack, 以nosql轻量级嵌入式数据库nedb作为存储，页面渲染采用react+redux, 样式框架为ant design, 实现了excel表格上传导出以及可视化
  - 依赖 https://github.com/jiangxy/react-antd-admin

- openKB /636Star/MIT/202205/js/inactive/view层handlebars/nedb
  - https://github.com/mrvautin/openKB
  - https://openkb.markmoffat.com/
  - 体验和helpkb基本一致
  - 依赖nedb、express、jquery、lunr、markdown-it
  - openKB is a Markdown Knowledge base application (FAQ) built with Nodejs and ExpressJS. 
  - The application uses an embedded database (nedb) by default but can also use a MongoDB server by changing the config
  - openKB is a search based Knowledge base (FAQ) backed by Lunr.js indexing 
  - openKB uses the pure Javascript nedb embedded database by default or a MongoDB server.
  - openKB uses Markdown-it

- https://github.com/leonardporteria/weight-recording-app
  - https://weight-recording-app.herokuapp.com/
  - A web application to keep track of your weight.
  - HTML5/SCSS/JavaScript/NodeJS/Express/NeDB

- https://github.com/mattd-silva22/node-url-shorten-api /202109/ts
  - a url shorten api made if Node.js , Express , TypeScript ans NeDB
- https://github.com/wheresvic/shorty
  - A simple self-hostable private url shortener using Node.js & Nedb (a file-based Mongodb API compatible db).
  - The idea behind shorty was to have a simple url shortening service that could be hosted on a cheap VPS with less than 1Gb RAM. Therefore, shorty uses only file-based storage to keep dependencies to a minimum.
- https://github.com/elunico/URL-Shortener
  - A simple URL shortener in using Node, Express, and Nedb
  - Regardless of whether you use the API directly or the client-side interface, you are limited to creating 50 short URLs an hour 

- https://github.com/harshgupta97/localhostdb
  - DB server for persistance and in-memory data storage using express and nedb, desktop application built using electron can leverage this to storage data locally.

- https://github.com/bdTechies/book-manager /201901/js/redux
  - https://book-manager.bdtechies.com/
  - cross-platform desktop app to manage personal library.

- https://github.com/Hunlongyu/ReadMe /202110/ts/vue
  - Github star manager, 支持 star 管理，收藏和取消收藏
  - 全平台支持. Windows, Mac, Linux
  - 支持快速在线编辑代码和本地编辑器编辑代码

- https://github.com/kavinda-ravishan/Web_Chat_App /202205/js
  - https://chat-application-nodejs-io.herokuapp.com/
  - real-time browser base chat application

- https://github.com/hutia/pwd-mgr /202203/ts/antd
  - personal infomation and password management.

- https://github.com/jasonbrandoo/react-express-nedb
  - Simple react auth with express

- https://github.com/sibite/social-app
  - Post, share, comment, upload photos and chat

- https://github.com/massCodeIO/massCode
  - code snippets manager for developers
  - Built with Electron, Vue 3 & Codemirror.
  - The new version will have a database based on plain JSON. In v1 it was used for this purpose library NeDB, which is no longer supported by the author
# nedb-starter-crud
- ts-api-server-express-multi-db /1Star/NALic/201804/ts/nedb/多种db/inactive
  - https://github.com/bluesky50/ts-api-server-express-multi-db
  - a rest API server built with Express. 
    - The server has API endpoints for Posts and Users. 
  - It aims to demonstrate the ability to provide rest services. 
  - 依赖express、mongoose、sequelize
  - Also, it aims to highlight the ability for the server to have modular controllers that can connect and query data from a variety of databases. 
    - The Server can connect with a variety of database types: mongo, nedb, and sqlite.
  - https://github.com/bluesky50/ts-api-server-koa-postgres /201805/ts
  - https://github.com/bluesky50/ts-api-server-express-mongo /201804/ts

- https://github.com/hojinahn4234/electron-typescript-react-nedb /202209/ts
  - work-in-progress scaffold for an Electron app in TypeScript, integrating React and NeDB.
  - Built with create-react-app, electron, and electron-builder.
- https://github.com/codegiik/electron-react-nedb-boilerplate
  - a fork of https://github.com/electron-react-boilerplate/electron-react-boilerplate

- https://github.com/AshutoshSinghai-InvizAI-DataEngg/node-backend-nedb /202206/js
  - a sample implementation of an authentication system that uses JSON Web Token to manage users' login data in Node.js web server.
- https://github.com/rcoder/nanocrud /202004/ts
  - tiny, dumb HTTP CRUD APIs backed by NeDB databases + automatic Git snapshots
  - insert a new document into the database; if the demo server is running, this should echo back the inserted document and update the test database in /tmp/nanocrud-demo

- https://github.com/okHadi/mern-starter-template /202208/js/client+server
  - A template project using NeDB (lightweight alternative to MongoDB), ExpressJS, React and NodeJs
  - a starting point for any type of a MERN application. 
  - You can easily change NeDB to MongoDB as well. 

- https://github.com/FilkCH/todo-app /202206/js/client+server
  - A lightweight vanilla JS based ToDo app with basic CRUD and sorting operations. 
  - Runs on express and neDB with a REST API.

- https://github.com/bi-tm/express-nedb-rest /202012/js
  - REST API for NeDB database, based on express HTTP server.

- https://github.com/rwl-dev-archive/learn-nedb-json-api /202009/ts
  - Express + NeDB = JSON API

- https://github.com/felixle236/backend-seed /201807/ts
  - backend-seed - Backend environment
  - Integrating user permission & good transmission in large numbers of users.
  - Cache data in memory & share them between processes (if using the cluster module) 
  - Multi-layer Architecture Pattern
  - Singleton Pattern，依赖 typedi
  - Generic Repository Pattern
  - https://github.com/felixle236/frontend-seed

- https://github.com/uppalasaikumar/node-express-mvc-ejs-start /201711/js
  - Node Express MVC EJS Bootstrap Starter app
  - Mongoose MongoDB object modeling
  - nedb In-memory database
  - jQuery library for DOM manipulation
# nedb-utils
- https://github.com/czwbig/nedb-mongoose-driver /202206/js
  - A Mongoose driver for NeDB, most APIs are compatible.
  - fork from https://github.com/ArcBlock/nedb
- https://github.com/aerys/mongoose-nedb /201612/js
  - A Mongoose driver for NeDB.
  - 依赖nedb、mongoose、bson
  - [extend nedb to support mongoose like schema](https://gist.github.com/dhigginbotham/5922171)
- mongoose
  - https://github.com/aerys/mongoose-nedb
  - https://github.com/ishantiw/crud-api
    - This API works on data stored in In-Memory for which we are using NeDB database
    - We are using modli as an API to define the schema and the crud operation. 
  - https://github.com/danibram/ffra
    - Tiny layer over Koa/fastify to make easier create Rest APIs

- https://github.com/Mido22/sqlite-to-nedb /201611
  - Util for converting a sqlite database into a nedb database

- https://github.com/ivrusson/mockon /202111/ts
  - Mock Server with data persistency based on MockJS and NeDB

- https://github.com/louischatriot/nedb-to-mongodb /201510/js
  - Utility to transfer all your data in a nedb database in a MongoDB collection

- https://github.com/bajankristof/nedb-models
  - a simple and extensible model wrapper for nedb using nedb-promises.

- https://github.com/nikolvs/nedb-repl
  - The command-line tool for NeDB
- https://github.com/marcusjwhelan/nedb-shell
  - A Mongo like shell for NeDB

- https://github.com/louischatriot/nedb-server
  - HTTP interface for a NeDB database
# more-nedb
- https://github.com/xiyuan-fengyu/ppspider
  - 基于puppeteer的web爬虫框架，提供灵活的任务队列管理调度方案，提供便捷的数据保存方案（nedb/mongodb），提供数据可视化和用户交互的实现方案

- https://github.com/sius/fakerdb /202005/js
  - Generate an unlimited stream of JSON schema instances using json-schema-faker, faker, chance and insert the data into a supported database, e.g.: nedb, mongodb, postgres, mssql.

- https://github.com/Jianxff/NEDB /cpp/B+Tree
  - NEDB 是基于 C++ 的简单数据库. 项目参考 SQLite 底层原理与 InnoDB 引擎, 实现数据库[增-删-查-改]的基本操作, 并提供控制台界面与外部接口.

- https://github.com/seppevs/migrate-mongo
  - A database migration tool for MongoDB in Node
