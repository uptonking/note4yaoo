---
title: lib-db-sqlite-community-web
tags: [community, indexeddb, sqlite, storage]
created: 2022-11-25T09:47:03.550Z
modified: 2022-11-25T09:47:43.079Z
---

# lib-db-sqlite-community-web

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Existing persistence tech like IndexedDB is hamstrung(妨碍，限制) on iOS by bugs & tricky to program correctly on any platform.
- https://twitter.com/jitl/status/1595887114327314432
  - SQLite/WASM + origin specific file system is promising but not available on iOS (yet?)

- ## Tested around with WASM SQLite + Origin Private File System and got it running in #orclAPEX. 
- https://twitter.com/phartenfeller/status/1594982779653165056
  - Works great and is amazingly fast. 
  - My vision is offline-first Plug-Ins that integrate well with APEXs Low Code approach.
- Basically I dream of 2+ Plug-ins.
  - First does sync. It downloads data from a given query to SQLite in the users browser so we can access it offline (this is the bleeding edge part bc not all browsers can do it yet. + it sends changes on the client back to DB to merge.
  - Secondly I want to modify my Grid Plug-in so it accesses this offline SQLite storage instead of the Oracle DB. Changes are written back to SQLite and later synced by the first plugin.
  - Now we have a offline Grid editing experience by only adding 2 Plug-ins.
- SQLite is cool for this because it is fast with lots of data and I can „mirror“ my source table and add indexes and constraints.
  - Other browser storage options are either nosql, slow or just weird (IndexedDB 😅).
