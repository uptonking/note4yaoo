---
title: toc-db-indexeddb-dexie
tags: [dexie, indexeddb, lib, toc]
created: 2022-11-06T03:18:08.698Z
modified: 2022-11-06T03:18:26.506Z
---

# toc-db-indexeddb-dexie

# guide

# popular
- Dexie.js /8kStar/Apache2/202206/ts
  - https://github.com/dexie/Dexie.js
  - https://dexie.org/
  - https://dexie.org/docs/Tutorial/Hello-World
  - A Minimalistic Wrapper for IndexedDB
  - Dexie solves three main issues with the native IndexedDB API:
    - Poor queries
    - Code complexity
    - Ambiguous error handling
  - Reactive (since v3.2)
    - Query the db without boilerplate and let your components mirror the database in real time.

- https://dexie.org/docs/Syncable/Dexie. Syncable.js
  - Enables two-way synchronization with a remote server of any kind.
  - https://github.com/nponiros/sync_server
    - A small node server which uses NeDB to write data to the disk. 
    - The server can be used with a client for example SyncClient to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the ISyncProtocol and Dexie.Syncable. 
    - It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
  - [Offline use with Sync to Server](https://github.com/only-cliches/Nano-SQL/issues/18)
    - Dexie.Syncable the Sync Server just uses Nedb as a quick way to get a sample running. You would replace that with MongoDB or whatever backend DB you wanted so you con isn't relevant here.

- https://github.com/subshell/data-repositories
  - This is a wrapper around Dexie, which itself is already a wrapper around IndexedDB. 
  - This wrapper allows to create repository classes, similar as you might be used to from Java and Spring Data.
  - It is recommended to have separate Dexie databases for every repository (due to some issues with Dexie and the versioning across multiple repositories). 
  - The repositories naturally work with RxJS and Observables. If you want to use JavaScript Promises instead you can just call .toPromise() on every returned Observable. 
  - **Due to the nature of IndexedDB, there is no synchronous way to read or write any data**.

- https://github.com/riapacheco/indexedDB_dexie
  - Architecture testing app for utilizing IndexedDB with Dexie. 
# utils
- https://github.com/ignasbernotas/dexie-relationships
  - provides an API to ease the loading of relational data from foreign tables

- https://github.com/YurySolovyov/dexie-mongoify
  - Dexie.js plugin with MongoDB-like API

- https://github.com/jaetask/dexie-easy-encrypt
  - Easy, unopinionated, table encryption middleware for Dexie

- https://github.com/mark43/dexie-encrypted
  - encrypt an IndexedDB database using Dexie.js. 
  - By default it uses tweetnacl.js, but you may use any encryption method you desire. 
  - Note that Dexie-encrypted cannot encrypt indices as doing this would make the database unsearchable.

- https://github.com/dfahlander/poc-dexie-cloud-encryption
  - POC dexie-cloud with dexie-encrypted
# examples
- https://github.com/AldoHub/React-Dexie
  - React implementation using Hooks, IndexedDb with Dexiejs and file uploading

- https://github.com/agilworld/reactjs-redux-form-builder-indexedDB-dexie
  - Form Builder under React JS + Redux + Dexie Indexed DB

- https://github.com/ebenezerdon/market-list-app
  - A market-list application built with React.js, IndexedDB and Dexie.js for offline storage.

- https://github.com/bignerdranch/dexie-fulltextsearch
  - Full text search for IndexedDB databases, powered by Dexie.

- https://github.com/tykoth/ra-data-dexie
  - Experimental React-Admin data provider using Dexie (IndexedDB)
  - 依赖react-admin

- https://github.com/ttessarolo/useDexie
  - React Hooks to use Dexie.js IndexDB library with ease
# more-dexie
- https://github.com/stutrek/dexie-hooks
  - There is now an official replacement for this!
  - See Dexie's official docs on useLiveQuery

- https://github.com/helgasoft/leaflet.dexie
  - A Leaflet plugin for offline maps storage using library Dexie.js.
  - The source code is based on leaflet.offline
