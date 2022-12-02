---
title: toc-database-document-minimongo
tags: [minimongo, mongodb, toc]
created: 2022-11-30T18:57:06.925Z
modified: 2022-11-30T18:57:26.459Z
---

# toc-database-document-minimongo

# guide

- faq
  - 是否同步的是全量数据，如何只同步用户相关的

- minimongo/meteor 的replication协议参考 [Distributed Data Protocol (DDP)](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md)

- meteor
  - a whole framework with its own package manager, database management and replication protocol.
  - hard to integrate it with other modern JavaScript frameworks like angular, vue.js or svelte
  - Meteor uses MongoDB in the backend and can replicate with a Minimongo database in the frontend
  - to make a meteor app offline first capable. There are some projects that might do this, but all are unmaintained.
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
# utils
- https://github.com/frozeman/meteor-persistent-minimongo2 /201805/js
  - client-side observer class that provides persistence for Meteor Collections using browser storage via localforage.
  - package based on meteor-local-persist by Jeff Mitchel
  - https://github.com/jeffmitchel/meteor-local-persist /201510/js
    - Persistent client (browser) collections for Meteor, using localStorage. Collections are reactive across browser tabs.

- https://github.com/serby/save /202209/js
  - A simple CRUD based persistence abstraction for storing objects to any backend data store. eg. Memory, MongoDB, Redis, CouchDB, Postgres, Punch Card etc.
  - save comes with a fully featured in memory engine which is super handy for testing your models. 
  - https://github.com/serby/save-mongodb

- https://github.com/radekmie/MiniMongoExplorer
  - Chrome extension for reviewing MiniMongo.
# examples
- https://github.com/john-guerra/reactHooksMiniMongo /202204/js
  - a simple example created in my class to demonstrate functional programming with React and Minimongo

- https://github.com/Dev1an/Quill-Operational-Transform /201706/js
  - A demo on how to transform Deltas obtained from the Quill text editor to resolve conflicts in text documents. 
  - The demonstration uses meteor's minimongo database: an in-browser version of the popular MongoDB database.
# more
- https://github.com/ajaybhatia/minimongo-cache /201908/coffeescript
  - A forked version of Minimongo designed for a synchronous local cache for React apps. 
  - This is designed to replace Flux.
  - since we treat the local database like a cache, we can use the same read-through caching techniques for data fetching that we use on the server

- https://github.com/leonardoventurini/meteor-devtools-evolved
  - The Meteor framework development tool belt, evolved.
  - Distributed Data Protocol (DDP): filter and search for any DDP message, being able to handle thousands and thousands of messages without a hiccup.
