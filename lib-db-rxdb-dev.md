---
title: lib-db-rxdb-dev
tags: [database, rxdb]
created: 2022-12-02T11:15:20.076Z
modified: 2022-12-02T11:16:05.028Z
---

# lib-db-rxdb-dev

# guide
- pros
  - RxDB replication protocol支持与自定义后端同步，支持http/websocket/webrtc/CouchDB/Firestore

- cons
  - 付费的插件太多，包括sqlite/indexeddb相关的

- features
  - ?
# faq
- [Questions & Answers · RxDB - JavaScript Database](https://rxdb.info/questions-answers.html)

- Why is the PouchDB RxStorage deprecated?
  - in 2016, there was no client-side database out there that fitted, I created RxDB as a wrapper around PouchDB. 
  - This worked great and all the PouchDB features like the query engine, the adapter system, CouchDB-replication and so on, came for free.
  - 👉🏻 But over the years, it became clear that PouchDB is not suitable for many applications, mostly because of its performance: 
    - To be compliant to CouchDB, PouchDB has to store all revision trees of documents which slows down queries. 
    - Also purging these document revisions is not possible so the database storage size will only increase over time. 
  - Another problem was that many issues in PouchDB have never been fixed, but only closed by the issue-bot
  - The whole PouchDB RxStorage code was full of workarounds and monkey patches to resolve these issues for RxDB users.
- In version 10.0.0 RxDB introduced the RxStorage layer which allows users to swap out the underlying storage engine where RxDB stores and queries documents from. 

- Since v12, RxDB is no longer based on PouchDB but has its own storage layer. Using PouchDB with RxDB is also deprecated. 
# docs

## [crdt plugin](https://github.com/pubkey/rxdb/blob/master/docs-src/crdt.md)

- with crdt, all document writes are represented as CRDT operations in plain JSON. 
- The CRDT **operations are stored together with the document** and each time a conflict arises, the CRDT conflict handler will automatically merge the operations in a deterministic way.
- CRDT operations are stored inside of a special field besides your 'normal' document fields
- When replicating document data with the RxDB replication or the CouchDB replication or even any custom replication, the CRDT operations must be replicated together with the document data as if they would be 'normal' a document property.
- When any instances makes a write to the document, it is required to update the CRDT operations accordingly. 
  - For example if your custom backend updates a document, it must also do that by adding a CRDT operation. 

- 🤔 Why not automerge.js or yjs?
  - Users do not have to learn a new syntax but instead can use the NoSQL operations which they already know.
  - RxDB is often used to replicate data with any custom backend on an already existing infrastructure. Using NoSQL operators instead of binary data in CRDTs, makes it **easy to implement the exact same logic on these backends** so that the backend can also do document writes and still be compliant to the RxDB CRDT plugin.

- When to not use CRDTs
  - CRDT can only be use when your business logic allows to represent document changes via static json operators. 
  - If you can have cases where user interaction is required to correctly merge conflicting document states, you cannot use CRDTs for that.
- Also when CRDTs are used, it is no longer allowed to do non-CRDT writes to the document properties.
# blogs-rxdb
- [Internal of RXDB: Plugins, Storages Adapters - DEV Community_202303](https://dev.to/dhrn/internal-of-rxdb-plugins-storages-adapters-3bi3)
- RXDB follows a modular architecture
  - Core Layer: This layer provides the basic functionality of RXDB, such as document CRUD operations and query execution.
  - Plugin Layer: Plugins are building blocks that helps to extend the functionality of RXDB. They can be used to provide encryption, sync, and validation features, among others. This layer is responsible for the communication between RXDB and the underlying database system. Currently, RXDB supports multiple adapters, including PouchDB, MongoDB, and SQLite.

## [Alternatives for realtime offline-first JavaScript applications](https://rxdb.info/alternatives.html)

- this page contains all known alternatives to RxDB

- RxDB supports using Dexie.js as RxStorage which enhances IndexedDB with RxDB features like MongoDB-like queries etc
# more
