---
title: lib-collab-crdt-community-hlc
tags: [collaboration, community, crdt, hybrid-logical-clock]
created: 2023-02-07T09:12:11.909Z
modified: 2023-02-07T09:12:37.761Z
---

# lib-collab-crdt-community-hlc

# guide

# discuss-evolu
- ## 

- ## 

- ## 

- ## evolu Switch to the official sqlite3 WASM client with a friendly MIT license
- https://twitter.com/evoluhq/status/1622708143670042625
  - Evolu no longer uses IndexedDB for persisting sqlite3 files. Instead, it uses modern Origin-Private FileSystem (OPFS) in Chrome and good old LocalStorage in other browsers.
- The LocalStorage implementation leverages VFS, so it doesn't load and save whole files. In other words, it's fast enough. The only limit is LocalStorage max size (5MB), which is sufficient unless a lot of data are stored.
- The Origin-Private FileSystem (OPFS) is currently supported only in Chrome, but both Safari and Firefox are finishing their support. Meanwhile, Evolu is using LocalStorage.

# discuss
- ## 

- ## 

- ## 

- ## 
