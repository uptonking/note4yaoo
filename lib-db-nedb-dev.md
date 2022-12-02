---
title: lib-db-nedb-dev
tags: [database, nedb]
created: 2022-11-27T19:20:09.883Z
modified: 2022-11-27T19:20:24.273Z
---

# lib-db-nedb-dev

# guide

# discuss
- ## [boosting nedb performance in big databases](https://github.com/louischatriot/nedb/issues/583)
  - I disagree. NedB is a drop-in replacement for MongoDB, which does and behaves exactly the way you want to convert NedB.
    - NedB is meant to be simple, not only in functionality, but behavior, and it's simplicity is the sole reason I'm using it for as much as I do. 
    - Making NedB memory-based will instantly require and consume more of the server, you make NedB faster, but at the cost of needing more resources (RAM).

- ## [It is possibile do operations (find, update, etc..) in synchronous mode?](https://github.com/louischatriot/nedb/issues/445)
  - When using memory-only mode, synchronous operations will be very useful, for example, if using NeDB as storage provider for redux. Also, when working in memory-only mode, there is no requirement to perform async operations, due there is not any read I/O
  - I would say it is more a result of his design goal to have a consistent API regardless of what backing store is being used (in-memory, localStorage, IndexedDB, Node.js file system, etc.).

- ## [Deprecate NeDB in favour of another embedded db(acebase)](https://github.com/Ylianst/MeshCentral/issues/4398)
- Acebase is a current nosql (firebase) compatible embedded database that uses (among other options) sqlite as the backend storage, meaning that (theoretically) the proven performance and reliability of sqlite can be leveraged with mongodb syntax queries.
- In having enabled AceBase and SQLite within the same week, I can tell just how much better and more reliable SQLite is. The airtime is certainly justified.

- ## [nedb: Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)
- TeDB - They're not a 1:1 replacement 
  - but that's actually good because they take a different approach that takes advantage of TypeScript and takes inspiration in other projects like NeDB-core, 
  - for example, they actually require you to use a storage driver, ex. Memory (any), Filesystem (Node. JS), IndexedDB (Browser), AsyncStorage (React Native), etc., 
  - Unfortunately they only provide a storage driver for Electron. 
  - They also have a Filesystem storage driver, but it is labelled as a mock and displaced to the examples folder. 
  - They're probably expecting the community to build the missing drivers, which means you have to pay your share of code before using this project. 
  - This is my preferred choice for new projects if you don't require a 1:1 replacement.
  - Tedb which is mentioned above was made with pure intention to work on electron. Currently using it on Electron 6.0.0 in production. The only storage driver I have written is the tedb electron storage driver. There is also a utils package.
- NestDB - They're missing some of the fixes of NeDB-core but their roadmap shows that they're planning to incorporate them. 
  - This is my preferred choice for new projects if you require a 1:1 replacement.

- PouchDB isn't a self-contained database at all, it's an abstraction layer. 
  - That said, PouchDB can be used on-disk by either embedding a CouchDB instance (super heavyweight solution) or by using a LevelDOWN adapter (default on Node and an acceptable solution)
  - I just think PouchDB is so overly concerned about synchronization/replication across instances and revision control that I feel like their API is much more basic in order to align with the CouchDB protocol vs having their own more expressive API on top of it for the many users who may just want to use it on a single isolated instance like NeDB.
- 
- 
- 
