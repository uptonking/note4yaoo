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

- ## guests say that they don't need CRDTs b/c they're "too complex" but then go on to explain their custom solution which is... a CRDT
- https://twitter.com/tantaman/status/1691083925060227075
- I've been guilty of similar things in the past. "That paper looks long. I'll just implement my idea." Some time later: "Oh.. I just implemented a worse version of what was in that paper"
- I've seen data synchronization code in a real app that looked exactly like a CRDT merge function, but the authors never heard or know anything about the CRDT literature and lattice algebra. It was much more complex than it should have been though.
