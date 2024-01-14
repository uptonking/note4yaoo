---
title: toc-db-indexeddb-lib-dexie
tags: [dexie, indexeddb, lib, toc]
created: 2022-11-06T03:18:08.698Z
modified: 2022-11-25T17:19:08.656Z
---

# toc-db-indexeddb-lib-dexie

# guide

- [Dexie Best Practices](https://dexie.org/docs/Tutorial/Best-Practices)

- [Dexie 4.0 Road Map](https://github.com/dexie/Dexie.js/discussions/1455)
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
- https://dexie.org/docs/Syncable/Dexie.syncable.js
  - Enables two-way synchronization with a remote server of any kind.
  - https://github.com/nponiros/sync_server
    - A small node server which uses NeDB to write data to the disk. 
    - The server can be used with a client for example SyncClient to save change sets which can later be synchronized with other devices. 
    - The server was made to work with the ISyncProtocol and Dexie.Syncable. 
    - It supports the poll pattern using AJAX and the react pattern using nodejs-websocket.
  - [Offline use with Sync to Server](https://github.com/only-cliches/Nano-SQL/issues/18)
    - Dexie.Syncable the Sync Server just uses Nedb as a quick way to get a sample running. You would replace that with MongoDB or whatever backend DB you wanted so you con isn't relevant here.

- https://github.com/tykoth/ra-data-dexie /js
  - Experimental React-Admin data provider using Dexie (IndexedDB)
  - 依赖react-admin
  - 更好的参考 ra-data-localForage

- https://gitlab.com/onezoomin/bygonz/bygonz /AGPLv3/202207/ts
  - Client-First Change Synchronisation, History Aggregation, and Conflict Management
  - Extends Dexie with modification History
  - Synchronizes modifications via Dgraph, Syncronizes state via modification log
  - [bygonz is a local-first library that implements CRDT atomic attribute logs via Dexie middleware_202211](https://talk.fission.codes/t/onezoomin-ztax-bygonz-fundability-exploration/3640)
    - i have successful proof of concept implementations using, dgraph, git, wnfs, and most recently ipfs as “backends”.
    - @boris started calling bygonz a db that uses wnfs, but i actually prefer to think of it as a lib that facilitates a local-first data synchronization pattern

- https://github.com/subshell/data-repositories
  - This is a wrapper around Dexie, which itself is already a wrapper around IndexedDB. 
  - This wrapper allows to create repository classes, similar as you might be used to from Java and Spring Data.
  - It is recommended to have separate Dexie databases for every repository (due to some issues with Dexie and the versioning across multiple repositories). 
  - The repositories naturally work with RxJS and Observables. If you want to use JavaScript Promises instead you can just call .toPromise() on every returned Observable. 
  - **Due to the nature of IndexedDB, there is no synchronous way to read or write any data**.

- https://github.com/riapacheco/indexedDB_dexie
  - Architecture testing app for utilizing IndexedDB with Dexie.

- https://github.com/amjadbouhouch/markup
  - https://mark-up.netlify.app/
  - The mobile first markdow editor for web & desktop with tiptap plugins and more
  - 依赖pouchdb、dexie、daisyui、tiptap、react-query
# examples
- https://github.com/deechris27/browserStorage /js
  - https://deechris27.github.io/browserStorage/
  - Reactjs file upload, Dexie-indexeddb browser storage

- https://github.com/saypa95/NotesApp
  - https://saypa95.github.io/NotesApp/
  - Notes App (React, Dexie.js)
  - https://github.com/jrgrimshaw/notes-app-tutorial

- https://github.com/sgkandale/TypNote
  - https://typnote.netlify.app/
  - TypNote is an offline note taking app
  - Dexie is used to store notes inside IndexedDB of browser.

- https://github.com/DarthAmun/pnptome
  - https://darthamun.github.io/pnptome/
  - project written in react/typescript for managing once collection of homebrew. 

- https://github.com/TBosak/notomato /ts
  - Pomodoro notes app built in Ionic & Angular frameworks, using Dexie.js to persist tasks/notes in IndexedDB.

- https://github.com/agilworld/reactjs-redux-form-builder-indexedDB-dexie /201904/js
  - Form Builder under React JS + Redux + Dexie Indexed DB

- https://github.com/AldoHub/React-Dexie /201907/js
  - React implementation using Hooks, IndexedDb with Dexiejs and file uploading

- https://github.com/bignerdranch/dexie-fulltextsearch  /201704/js
  - Full text search for IndexedDB databases, powered by Dexie.
  - 依赖lunr
  - [IndexedDB+Dexie+Lunr MTG full-text search demo](https://gist.github.com/nolanlawson/6f69f4a573c1da862e92)

- https://github.com/ebenezerdon/market-list-app
  - A market-list application built with React.js, IndexedDB and Dexie.js for offline storage.

- https://github.com/ttessarolo/useDexie
  - React Hooks to use Dexie.js IndexDB library with ease
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

- https://github.com/nponiros/sync_client
  - This module can be used to write data to IndexedDB using Dexie and to synchronize the data in IndexedDB with a server. 
  - Dexie. Syncable is used for the synchronization. This module contains an implementation of the ISyncProtocol. 
  - It was primarily written to work with sync-server but should work with other servers which offer the same API.
# more-dexie
- https://github.com/stutrek/dexie-hooks
  - There is now an official replacement for this!
  - See Dexie's official docs on useLiveQuery

- https://github.com/helgasoft/leaflet.dexie
  - A Leaflet plugin for offline maps storage using library Dexie.js.
  - The source code is based on leaflet.offline

- https://github.com/Vissie2/dexie-2d-geospatial-index
  - A playground to test the performance of H3 geospatial indexing using Dexie.

- https://gist.github.com/JamesMessinger/a0d6389a5d0e3a24814b
  - Very Simple IndexedDB Example
  - I would not recommend coding against the raw indexedDB API unless you really have to. 
  - Performance is also a reason to use a wrapper library like dexie that can do multiple operations in a single transaction without sacrificing code readability and error handling.
  - [IndexedDB: When to close a connection](https://stackoverflow.com/questions/34915581)
