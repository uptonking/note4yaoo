---
title: lib-collab-common-examples-sync-p2p
tags: [collaboration, data-sync, examples, p2p, synchronization]
created: 2023-01-17T19:10:10.160Z
modified: 2023-01-17T19:13:01.845Z
---

# lib-collab-common-examples-sync-p2p

# guide

# sync-examples
- lo-fi /7Star/MIT/202211/ts
  - https://github.com/a-type/lo-fi
  - https://lo-fi.gfor.rest/
  - An IndexedDB-powered database and data sync solution for lightweight, local-first web apps.
  - server依赖sqlite、jwt、ws
  - Undo and redo changes
  - it includes an optional server which unlocks the power of sync and realtime
  - the goal of lo-fi is to be simple and recognizable.
    - One small, generic syncing server is all you need
    - NO. Infinitely growing storage usage
    - NO. Having to deeply understand CRDTs
    - NO. Peer to peer networking
    - NO. WASM-compiled databases in your browser

- https://github.com/Rolands-Laucis/Socio
  - A WebSocket based realtime duplex Front-End and Back-End syncing API paradigm framework

- https://github.com/ar-nelson/osmosis-js /202103/ts
  - An in-process JSON database with automatic peer-to-peer background synchronization between devices on a local network. Keep your apps in sync without a cloud!
  - JS reference implementation of Osmosis, a JSON data store with peer-to-peer background sync

- https://github.com/JacobJaffe/event-system-prototype
  - Prototype of a syncing game state between a p2p, host switching network through an action system & event history.

- https://github.com/derhuerst/files-sync-stream
  - Sync files (or any blobs of data) between two peers, in both directions, over any transport. 
  - You decide where and how to store the files. 
  - files-sync-stream accepts a generic file read function and emits data events when receiving data.

- https://github.com/RamonGal/Distributed-Systems /lamport+redis-redlock
  - This view is to be managed by a django rest backend that serves the views json response, which will be a serialized disposition of data from a postgres database.
  - For a perfectly in sync view for different users, we use an implementation of a `Lamport` timestamp.
  - An algorithm for mutual exclusion using a `redis Redlock` was made and the above mentioned timestamp helps determines the pace with which we can apply changes to the shared state.
  - [Redis Redlock](https://redis.com/redis-best-practices/communication-patterns/redlock/) is canonical implementations of locking

- https://github.com/NangoHQ/nango /202212/ts
  - https://www.nango.dev/
  - Nango continuously syncs data from any API endpoint (that returns JSON) to your database.
  - Nango has built-in support for OAuth through our sister project Pizzly
# sync-json
- https://github.com/zettant/realtime-object-sync
  - server and client libraries for realtime JSON object synchronization.

- https://github.com/privatenumber/reactive-json-file
  - Reactively sync JSON mutations to disk

- https://github.com/JoshMerlino/filestore-json
  - Easily sync JSON objects of any shape with the filesystem.
  - Read & write to JSON files on a storage device without the need to interact with the filesystem.
  - Persistent data between process restarts.
  - Automatically updates internal value when JSON file is modified.

- https://github.com/codePlaceOfficial/virtualFileServer
  - keep local files and JSON objects in sync

- https://github.com/lloydeverett/json-sync-server
  - Simple ExpressJS HTTP server that allows all clients to sync (read or update) a single JSON object. 
# more
- https://github.com/owojcikiewicz/realtime-sync
  - enables collaborative editing of HTML inputs in real-time across multiple websites and clients.
  - built using WebSockets

- https://github.com/flmeHashira/Clip-Sync
  - Realtime Clipboard Sync based on Electron and Realm
  - frontend + backend

- https://github.com/damrbaby/pathsync
  - firebase-like realtime sync powered by Redis and WebSockets.
  - In-memory syncing of paths using Node.js, Redis, and WebSockets that live streams to observables.
  - Redis needs to be running. Requires ioredis, faye, and express.

- https://github.com/JailBreakC/distributed-json-ot /未实现
  - distributed json ot demo project, shows how to sync data with version control
