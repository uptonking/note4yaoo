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

- ## Now that SQLite can be run in a browser as a 296KB (compressed) WASM file, 
- https://twitter.com/quolpr/status/1563502562531086337
  - I think it's time we all forgave W3C/Mozilla for rejecting it as a core browser component in Web SQL
- But the downside is that wasm SQLite still don’t give such persistency as WebSql. 
  - You can use absurd-sql on top of idb, but the performance still will not be the same
  - And file system api + SQLite wasm is still not as performant as WebSQL
- What web standards really miss — performant file system api OR storage API that can read and write blocks of data fast. You can do it with IDB, but it will be still not performant as raw OS read and write to file

- ## CRDT extension successfully compiled and running in the new official SQLite WASM.
- https://twitter.com/tantaman/status/1587624390518251520
  - Adios(再见) absurd-sql and sql.js
- the official sqlite wasm apis are a bit tricky to use and load correctly. 
  - @schickling has been working on a vite compatible package to ease this.
  - the official build uses `origin private filesystem` (并不和操作系统的文件系统一一对应) rather than indexeddb for persistence, so a big + there.
- crsqlite is a run time loadable extension 
  - For WASM, however, it seems you are required to statically link it to SQLite at compile time.
  - Does rusqlite have docs on adding extensions to its wasm bundle? If so I can put together a guide from those.

- ## I've migrated to the new, official SQLite WASM build in favour of absurd-sql.
- https://twitter.com/schickling/status/1595877724870123521
- Does this support permanent storage in IndexedDB and does it run in a service worker?
  - I'm using the OPFS storage variant and mostly use it from a web worker - not a service worker.

- ## The #SQLite based Wasm library to replace Web SQL won't be backed by IndexedDB, 
- https://twitter.com/ChromiumDev/status/1565306838224175104
  - but by the origin private file system, and specifically access handles optimized for performant read/write access
- Yes, the plan is to eventually remove Web SQL, but our intention is to empower developers to create their own solutions for structured storage, and we're therefore working with the #SQLite team to create a SQLite implementation over Wasm. This solution will replace Web SQL
- The origin private file system is supported by Chrome 🛞, Safari 🧭 , and support for it is in development for Firefox 🦊_202209
- Is it planned to support saving FileSystemHandle's in there? Currently the only way to save them I know, is the indexedDB and that gets pretty slow with larger amounts of data.
  - Hopefully. `FileSystemHandle` is serializable, so it should work in theory if SQLite can deal with serializable objects (which I don’t know). To be found out once the library gets reality.

- ## Big news in web app persistence: SQLite + Chrome are collaborating to create an official SQLite WASM build, backed by performant filesystem APIs!
- https://twitter.com/geoffreylitt/status/1573693207640244229
  - Currently in Riffle we use absurd-sql for persistence to IndexedDB.
  - It's a fantastic project but hits some perf limits due to IDB, and of course no 1st-party support by Sqlite team
  - I'm hoping that this new FS-backed SQLite build will be faster in some cases than IDB. 
- This SQLite build will be backed by the "origin private file system" (OPFS) which means these "files" aren't visible to the user.
  - This is because the performant FS APIs are only available inside OPFS
  - My tentative takeaway is that extending this to user-visible files is hard because exclusive write locks on files is a major part of the design for these fast random access file APIs
- Both absurd-sql and sql.js were instrumental in helping us (sqlite team) understand how to take on the OPFS task. We experimented with absurd-sql-like IDB storage but it's simply too easy to corrupt sqlite dbs stored there.

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
