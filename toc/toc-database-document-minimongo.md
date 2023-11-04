---
title: toc-database-document-minimongo
tags: [minimongo, mongodb, toc]
created: 2022-11-30T18:57:06.925Z
modified: 2022-11-30T18:57:26.459Z
---

# toc-database-document-minimongo

# guide

- faq
  - minimongo的示例对应idb中的单张表+多行数据
  - 是否同步的是全量数据，如何只同步用户相关的

- minimongo/meteor 的replication协议参考 [Distributed Data Protocol (DDP)](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)

- [Meteor的工作原理及优势与不足](https://cloud.tencent.com/developer/article/1643568)
  - 优势：易学、偏向客户端、实时响应、生态
  - 不足：nodejs单线程不适合计算密集型、约束少、NoSQL、非静态、首次加载时间长
# minimongo-like
- minimongo /1kStar/LGPLv3/202207/ts
  - https://github.com/mWater/minimongo
  - Client-side in-memory mongodb backed by localstorage with server sync over http
    - A client-side MongoDB implementation which supports basic queries, including some geospatial ones.
    - Uses code from Meteor.js minimongo package(2014), reworked to support more geospatial queries 
  - It is either IndexedDb backed (IndexedDb), Local storage backed (LocalStorageDb) or in memory only (MemoryDb).
  - sqlite plugin is also supported when available
  - ReplicatingDb: Keeps two local databases in sync. Finds go only to master.
  - Minimongo is designed to work with a server that performs three-way merging of documents that are being upserted by multiple users.
  - Compared to RxDB, Minimongo has no concept of revisions or conflict handling, which might lead to undefined behavior when used with replication or in multiple browser tabs. Minimongo has no observable queries or changestream.
- https://github.com/petehunt/minimongo-cache /201703/coffeescript
  - A forked version of Minimongo designed for a synchronous local cache for React apps. 
  - This is designed to replace Flux.
  - since we treat the local database like a cache, we can use the same read-through caching techniques for data fetching that we use on the server
  - forks
  - https://github.com/xvonabur/minimongo-cache
    - `for (collectionName in changeRecords) { }` 描述变更
- https://github.com/meteorrn/minimongo-cache /202211/js
  - A fork of the minimongo-cache package maintained for the purpose of supporting the @meteorrn/core package
  - https://github.com/AstonBraham/minimongo-cache
    - refactor-to-es6

- https://github.com/oortcloud/ddp-ejson /201405/js
  - Extended JSON library; used in Meteor's Distributed Data Protocol.
  - 支持 `$date/$binary`
- https://github.com/lgandecki/modifyjs /201803/js
  - Modify your objects with a mongo like syntax. 
  - This is based on a modify function of Meteor's brilliant minimongo package, cleaned up, rewritten to es6, changed to work without Meteor context
  - rxdb crdt使用
- https://github.com/crcn/sift.js
  - Use Mongodb queries in JavaScript

- gongojs-project: v1-js-websocket，v2-ts-轮询
  - https://github.com/gongojs/project
  - Reactive, realtime, offline queries with a ok_hand developer experience.
  - Client-side mongo-like database makes CRUD operations a joy
  - Works with any server-side database (currently MongoDB supported, FaunDB planned)
  - Queries are reactive and realtime* (live), with optimistic updates for free
    - Client-side queries are realtime, but depend on your subscription transports. 
    - 👉🏻 Due to feedback, we have refocused attention to serverless polling ("near-realtime") vs the original websocket server (true realtime).
    - 旧版v1采用websocket，新版采用polling
  - Works offline, syncs on reconnect, persists with IndexedDB
  - the concept and data flow is very similar to Meteor.
    - I spent years working with Meteor and have a lot of love for the team
  - https://github.com/gongojs/gongo-client
    - WIP: DX focused in-browser database with offline and realtime.
    - 依赖idb、modifyjs、arson(encoder and decoder)、bson、ejson
  - https://github.com/gongojs/gongo-client-react
    - React hooks for gongo-client
    - 依赖 gongo-client
  - https://github.com/gongojs/gongo-server
    - Server(less) components for GongoJS fullstack data and auth
    - 依赖express，不依赖websocket
  - https://github.com/gongojs/gongo-server-db-mongo
    - MongoDB DatabaseAdapter for GongoJS server
    - 依赖 jsonpatch-to-mongodb
  - https://github.com/gongojs/old-v1
    - Backup of original v1 code

- ddp /1Star/MIT/202207/ts
  - https://github.com/Jantje19/ddp
  - a library version of the DDP features that Meteor offers. 
  - This library allows you to use the Meteor features without having to install the framework and without being tied into the NodeJS
  - https://github.com/Jantje19/ddp-react
    - React hooks for the custom DDP project, however these hooks should work with any DDP server (even Meteor).
    - 依赖simpleddp

- https://github.com/Gregivy/simpleddp /202007/js
  - simplify the process of working with Meteor.js server over DDP protocol using external JS environments (like Node.js, Cordova, Ionic, ReactNative, etc).
  - It is battle tested in production and ready to use
  - written in ES6 and uses modern features like promises. 

- https://github.com/mondora/ddp.js /201710/js
  - javascript isomorphic/universal ddp client.
  - to give the developer a clear, consistent API to communicate with the ddp server

- https://github.com/stubailo/meteor-rest /201605/js
  - makes it easy to make your Meteor app's data accessible over HTTP.

- https://github.com/c58/marsdb /201609/js/未实现索引
  - MarsDB is a lightweight client-side database. 
  - It's based on a Meteor's minimongo matching/modifying implementation. 
  - written on ES6, have a Promise based interface and may be backed with any storage implementation
  - 支持内存、localStorage、localForage、levelup
  - It's also supports observable cursors.
  - [Added simple indexes with String, Number and Date types support](https://github.com/c58/marsdb/pull/8)
  - [linvodb: Any plans to rewrite on ES6? Check my work in c58/marsdb_201509](https://github.com/Ivshti/linvodb3/issues/24)
  - https://github.com/c58/marsdb-sync-client
    - It's a Meteor compatible DDP client, based on MarsDB. 
    - It supports methods, pub/sub and collection operations. 
    - It is very similar to Meteor
  - https://github.com/c58/marsdb-sync-server
    - It's a Meteor compatible DDP server, based on MarsDB

- https://github.com/pubkey/event-reduce /202212/ts
  - https://pubkey.github.io/event-reduce/
  - An algorithm to optimize database queries that run multiple times
  - 提供了使用示例，包括minimongo、nedb、pouchdb
  - EventReduce only works with queries that have a predictable sort-order for any given documents. (you can make any query predicable by adding the primary key as last sort parameter)
  - At the moment there is only the JavaScript implementation
  - Is this something like materialized views?
    - Yes and no. Materialized views solve a similar problem but in a different way with different trade-offs.
  - Is this something like event sourcing or CQRS?
    - No, event sourcing is mostly used to calculate a current state by attaching the full event stream to the starting state. This allows for stuff like time travel and so on. EventReduce solves a completely different (performance-) problem and only shares some common keywords like event.
# utils
- https://github.com/serby/save /143Star/ISC/202209/js
  - A simple CRUD based persistence abstraction for storing objects to any backend data store. eg. Memory, MongoDB, Redis, CouchDB, Postgres, Punch Card etc.
  - save comes with a fully featured in memory engine which is super handy for testing your models. 
  - https://github.com/serby/save-mongodb

- https://github.com/radekmie/MiniMongoExplorer
  - Chrome extension for reviewing MiniMongo.

- https://github.com/NickStefan/minimongoose /201602/js
  - mongoose in the browser
# examples
- https://github.com/ezzatisawesome/ChromeStorageSync /202112/js
  - completed MVP of syncing db using minimongo

- https://github.com/kasivisu4/d3-gallery
  - https://kasivisu4.github.io/d3-gallery/
  - user can search the d3 graph 
  - Used the Minimongo IndexDB to store the data in the Browser Storage.

- https://github.com/yianchen0131/Preorder-Marketplace /202207/js
  - http://giantpreorderplace.surge.sh/
  - Preorder website is an ecommerce platform for users to place preorders on products listed. 
  - This project uses Minimongo IndexDB to store items data and member data upon member signing up in "Join" from the navbar of the website. Items are already imported to items database
- https://github.com/yianan261/taskmaster-app
  - functional programming with react hooks
- https://github.com/kasivisu4/pdp_homework_3_fp
  - https://kasivisu4.github.io/pdp_homework_3_fp/
  - Shopping Cart Functionality using React Function Programming Paradigm
  - minimongo中的数据持久化在idb的多张表的多个行

- https://github.com/john-guerra/reactHooksMiniMongo /202204/js
  - a simple example created in my class to demonstrate functional programming with React and Minimongo
- https://github.com/yianan261/Shopping-Cart
  - Hooks implementation of a shopping cart where users can add product items to cart

- https://github.com/Dev1an/Quill-Operational-Transform /201706/js
  - A demo on how to transform Deltas obtained from the Quill text editor to resolve conflicts in text documents. 
  - The demonstration uses meteor's minimongo database: an in-browser version of the popular MongoDB database.
# meteor-ddp
- https://github.com/Hydrawisk793/kaphein-js-ddp-client /202107/js
  - An implementation of meteor DDP client.

- https://github.com/Tarang/DDP-Server /201601/js
  - DDP-Server is a nodejs based DDP Server.
  - You can then connect to it using a ddp client such as ddp.

- https://github.com/Streemo/react-ddp /201609/js
  - A lightweight ddp-client for react-native.
  - This library is meant to include minimally necessary set of functions which are implemented on traditional Meteor clients
  - You may use redux, minimongo, or a custom object to store data; 
  - With react-ddp and minimongo-cache, we can achieve a front-end on react-native which is eerily similar to a traditional Meteor front end, with little work on your end, whilst being modular
  - The coupling between the data-store and react-ddp is as easy as writing custom added, changed, and remove callbacks. For minimongo, this is trivial because the ddp messages are already in "mongo" form.
  - https://github.com/Streemo/lojic
    - Reactive DDP observer for the client. WIP.

- https://github.com/looshi/redux-ddp /201607/js/client+server/依赖meteor
  - redux app demonstrating use of DDP messages to populate a Redux store.
  - 依赖ddp.js、redux
  - This project is using Meteor 1.3 beta.
  - When DDP messages arrive, a Redux action is called and the Redux Store will be updated accordingly.
  - Minimongo is not used to store the remote database driven state.
  - The Store contains a players collection which is a key value store ( very similar to minimongo )
  - I find that using key value objects for a collection inside a Store is much easier to deal with than using an Array.
  - the UI is updated optimistically.

- https://github.com/rclai/redux-ddp /201602/js/client+server
  - Getting Meteor DDP collection data to get synced straight into a Redux store instead of minimongo and figuring out how to apply optimistic updates.

- https://github.com/apendua/ddp-redux /201806/js
  - fetch resources from your ddp server in a completely declarative way. 
  - Subscriptions/ methods (queries) parameters are evaluated by selectors and all you need to do is to extract collection data from the redux store. 
  - Most typical DDP "commands" are accessible by simply dispatching a redux action

- https://github.com/veliovgroup/Meteor-Files
  - Upload files via DDP or HTTP to Meteor server FS, AWS, GridFS, DropBox or Google Drive.
  - well-maintained Meteor.js package for files management using MongoDB Collection API.
  - Upload via HTTP and DDP transports
  - Compatible with all front-end frameworks from Blaze to React
  - 比较了 websockets-ddp/http/webrtc-udp: [About upload Transports](https://github.com/veliovgroup/Meteor-Files/blob/master/docs/about-transports.md)

- https://github.com/oortcloud/node-ddp-client /201612/js
  - A callback style DDP (Meteor's Distributed Data Protocol) node client

- https://github.com/vnnvanhuong/ws-ddp-client /201907/js/使用meteor的示例
  - A demo for DDP Client using Websockets API
  - Using WebSocket APIs for communicating with a DDP Server.
  - Implemention in pure JS, no extra libraries needed.
  - For this demo, I used Rocket. Chat which contains a DDP Server. I created a user wdc/secret for authentication.

- https://github.com/tanejasomi/DDP_Implementation_meteor /201803/js
  - Distributed Data Protocol is Client-Server Protocol based on WebSockets for queuing and updating a Server-Side database and for synchronizing such updates among clients. 
  - Project implemented to show Latency Compensation and transparent reconnection
# meteor-minimongo
- https://github.com/harryadel/blastjs /202202/js
  - The aim of this project is to extract Blaze and all of its associated packages to NPM so it can be used outside of Meteor.

- https://github.com/GroundMeteor/db /201711/js
  - thin layer providing Meteor offline database
- https://github.com/CaptainN/npdev-collections /202012/js
  - I like Mongo and MiniMongo for it's low bar for entry, and it's simple iteration
  - Use offline storage client side by default. ground:db is a great solution.
  - for SSR, we have a number of tricky parts to choreograph(设计，编舞)
  - Use methods for data transfer by default, instead of reactive pub/sub (on the list of TODOs is to allow pub/sub instead of methods).
  - [Moving to Meteor Community · Issue #212 · GroundMeteor/db](https://github.com/GroundMeteor/db/issues/212)

- https://github.com/stumps-dev/meteor-persist-collection /201801/js
  - persist a collection in the browser storage
  - runs A LOT faster than GroundDB.

- https://github.com/frozeman/meteor-persistent-minimongo2 /201805/js
  - client-side observer class that provides persistence for Meteor Collections using browser storage via localforage.
  - package based on meteor-local-persist by Jeff Mitchel
  - https://github.com/jeffmitchel/meteor-local-persist /201510/js
    - Persistent client (browser) collections for Meteor, using localStorage. Collections are reactive across browser tabs.
# more
- https://github.com/leonardoventurini/meteor-devtools-evolved
  - The Meteor framework development tool belt, evolved.
  - Distributed Data Protocol (DDP): filter and search for any DDP message, being able to handle thousands and thousands of messages without a hiccup.
