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
    - One datastore is the equivalent of a MongoDB collection
  - A copy of the whole database is kept in memory. This is not much on the expected kind of datasets (20MB for 10, 000 2KB documents).
  - You can use NeDB as an in-memory only datastore or as a persistent datastore. 
    - If you specify a filename, the database will be persistent, and automatically select the best storage method available (IndexedDB, WebSQL or localStorage) depending on the browser.
    - For a Node.js/Node Webkit database it's the file system
    - For a browser-side database it's `localforage`, which uses the best backend available (IndexedDB then WebSQL then localStorage)
    - Under the hood, NeDB's persistence uses an append-only format, meaning that all updates and deletes actually result in lines added at the end of the datafile, for performance reasons.
  - I consider NeDB to be feature-complete, i.e. it does everything I think it should and nothing more. As a general rule I will not accept pull requests anymore
  - [Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)

- https://github.com/seald/nedb  /202209/js/active
  - forked it and maintain it for the needs of Seald.
  - Since version 3.0.0, NeDB provides a Promise-based equivalent for each function which is suffixed with `Async`.
  - https://github.com/bajankristof/nedb-promises /202209/js
    - A dead-simple promise wrapper for nedb.
    - As of nedb-promises 5.0.0 nedb package has been replaced with a fork seald/nedb

- nedb-forks
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
  - https://github.com/Techpire/db /1Star/MIT/202203/ts/half-baked
    - nedb typescript conversion
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

- camo /202108/js/inactive/odm(object document mapper)
  - https://github.com/scottwrobinson/camo
  - A class-based ES6 ODM for Mongo-like databases.
  - Camo was created for two reasons: to bring traditional-style classes to MongoDB JavaScript, and to support NeDB as a backend
  - Camo was designed and built with multiple Mongo-like backends in mind, like NeDB, LokiJS*, and TaffyDB*.
- https://github.com/seald/follicle
  - a fork of camo made for the needs of Seald
  - A class-based ES6 ODM for Mongo-like databases
- https://github.com/4strid/nekodb /201910/js
  - Tiny ODM for MongoDB/NeDB
- https://github.com/bengl/mongosmash
  - simple ODM for MongoDB and NeDB on Node.js (using JS Harmony).

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
# nedb-starter-crud
- ts-api-server-express-multi-db /1Star/NALic/201804/ts/nedb/多种db/inactive
  - https://github.com/bluesky50/ts-api-server-express-multi-db
  - a rest API server built with Express. 
    - The server has API endpoints for Posts and Users. 
  - It aims to demonstrate the ability to provide rest services. 
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
# nedb-utils
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

- https://github.com/sius/fakerdb /202209/js
  - Generate an unlimited stream of JSON schema instances using json-schema-faker, faker, chance and insert the data into a supported database, e.g.: nedb, mongodb, postgres, mssql.

- https://github.com/Jianxff/NEDB /cpp/B+Tree
  - NEDB 是基于 C++ 的简单数据库. 项目参考 SQLite 底层原理与 InnoDB 引擎, 实现数据库[增-删-查-改]的基本操作, 并提供控制台界面与外部接口.
