---
title: toc-db-benchmark
tags: [benchmark, db, toc]
created: 2022-11-25T16:16:25.906Z
modified: 2022-11-25T16:16:52.713Z
---

# toc-db-benchmark

# guide

- common
  - oltp
    - tpc-c
  - olap
    - tpc-h
# benchmarks
- https://github.com/nolanlawson/database-comparison
  - http://nolanlawson.github.io/database-comparison/
  - Compare DOM-blocking in browser databases
  - Demo app to test different browser databases (memory, LocalStorage, IndexedDB, WebSQL) and in particular see whether or not they block the DOM.

- https://github.com/pubkey/client-side-databases
  - https://pubkey.github.io/client-side-databases/database-comparison/index.html
  - I have implemented the exact same chat application with different database technologies.
  - PouchDB with IndexedDB adapter & CouchDB replication
  - RxDB PouchDB with PouchDB Storage & GraphQL replication
  - RxDB LokiJS with LokiJS Storage & GraphQL replication
  - RxDB Dexie.js with Dexie.js Storage & GraphQL replication
  - WatermelonDB with LokiJS adapter (no backend sync atm)
