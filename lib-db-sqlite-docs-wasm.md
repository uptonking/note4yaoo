---
title: lib-db-sqlite-docs-wasm
tags: [docs, sqlite, wasm]
created: 2022-11-27T15:36:01.309Z
modified: 2022-11-27T15:36:13.148Z
---

# lib-db-sqlite-docs-wasm

# guide

- resources
  - [sqlite3 WebAssembly & JavaScript Documentation](https://sqlite.org/wasm/doc/trunk/index.md)
# blogs
- [From Web SQL to SQLite Wasm: the database migration guide - Chrome Developers](https://developer.chrome.com/blog/from-web-sql-to-sqlite-wasm/)
# persistence
- [Browser Persistence - vlcn.io](https://vlcn.io/docs/guide-persistence)

- The official SQLite WASM port
- pros:
  - Maintained and supported by the SQLite team
  - Aggressively focused on performance
  - Permissive license (public domain)
- cons
  - OPFS has coarse grained locking and doesn't behave well when many tabs interact with the same persisted database. This could be solved by using WebLocks the VFS implementation. Something yet to be explored.
  - The official SQLite build can only use OPFS or session/localStorage for persistence. Session & local storage aren't great options given they're capped at 5MB, really leaving us only with OPFS.

- An unofficial WASM port called wa-sqlite
- pros
  - ability to use indexeddb for persistence rather than OPFS. indexeddb has been around a long time and is well supported by all major browsers.
  - Can run SQLite + Persistence in the UI thread
  - Can be used in a shared worker to share the same db instance across multiple tabs

- cons
  - GPLv3 license
  - May not be as fast as the official port
# docs

## [sqlite3 wasm docs: Persistent Storage Options](https://sqlite.org/wasm/doc/trunk/persistence.md)

- Web apps have traditionally not had many options for storing persistent state on a client. 
  - First came cookies, then localStorage and sessionStorage, plus IndexedDB and the aborted WebSQL effort. 
  - WebSQL was dropped before it was standardized and IndexedDB has a poor reputation as having an awkward interface and cross-browser incompatibilities.
- As of 2021, browsers started implementing filesystem-style storage, namely Google's Origin-Private FileSystem.

### Key-Value VFS (kvvfs)

- kvvfs is an `sqlite3_vfs` implementation conceived and created to store a whole sqlite3 database in the localStorage or sessionStorage objects. 
  - 👉🏻 Those objects are only available in the main UI thread, not Worker threads, so this feature only works in the main thread. 
  - kvvfs stores each page of the database into a separate entry of the storage object, encoding each page into an ASCII form so that it's JS-friendly.
- This VFS supports only a single database per storage object. 
  - That is, there can be, at most, one localStorage database and one sessionStorage database.

- The encoding of the database into a format JS can make use of is slow and consumes a good deal of space, so these storage options are not recommended for any "serious work." 
  - Rather, they were added primarily so that clients who do not have OPFS support can have at least some form of persistence.
  - When the storage is full, database operations which modify the db will fail. 
- Because of the inherent inefficiency of storing a database in persistent JS objects, which requires encoding them in text form, database in kvvfs are larger than their on-disk counterparts and likely considerably slower.

- JsStorageDb: kvvfs the Easy Way

### OPFS via sqlite3_vfs

- The Origin-Private FileSystem, OPFS, is an API providing browser-side persistent storage which, not coincidentally, sqlite3 can use for storing databases.
- As of late 2022, only bleeding-edge versions of Chromium-derived browsers have the necessary APIs. 
  - Support from other browsers is expected to follow as soon as their developers see all of 2023's web apps targeting Chrome specifically for the persistent sqlite3 support 😉.
- This support comes in two flavors:
  - An `sqlite3_vfs` implementation which exposes OPFS only to the sqlite3-internal VFS API (and not directly to the clients).
  - Emscripten's WASMFS provides OPFS via client-transparent virtual filesystem emulation.

- Both approaches have their benefits and drawbacks and have essentially identical performance. 
- They are not mutally exclusive but it is illegal to open any given database via both approaches at the same time because OPFS exclusively locks files when they are opened.

- JavaScript's `SharedArrayBuffer` type is required for both variants of OPFS support

- OPFS via sqlite3_vfs
  - 👉🏻 This support is only available when sqlite3.js is loaded from a Worker thread. 
  - This OPFS wrapper implements an sqlite3_vfs wrapper entirely in JavaScript.

- concurrent access to OPFS-hosted files is a pain point for this VFS. Client applications will not be able to achieve desktop-app-grade concurrency in this environment.

- OPFS offers a handful of synchronous APIs which are required by this API. 
  - A file can be opened in asynchronous mode without any sort of locking, but acquiring access to the synchronous APIs requires what OPFS calls a "sync access handle, " which exclusively locks the file. 
  - So long as an OPFS file is locked, it may not be opened by any other service running in that same HTTP origin. e.g. code running in one browser tab cannot access that file so long as it is locked by another tab running from that same origin.
  - In essence, that means that no two database handles can have the same OPFS-hosted database open at one time. 
  - If the same page is opened in two tabs, the second tab will hit a locking error the second it tries to open the same OPFS-hosted database!

- Sometimes sqlite3 will call into a VFS without explicitly acquiring a lock on the storage in advance (on journal files, for example). 
  - Such locks are internally called implicit locks or auto-locks. 
  - They are locks which are not required by the sqlite3 VFS but are required by OPFS. 

### OPFS via WASMFS

- 👉🏻 Unlike the sqlite3_vfs OPFS wrapper, this one works in the main UI thread and does not require that databases saved in OPFS use an OPFS-aware sqlite3_vfs.
  - Instead, it "mounts" a specific directory in the virtual filesystem, under which all files are hosted in OPFS storage. 
  - Any C code which uses the file I/O APIs defined by C89 or POSIX gets transparently proxied by the Emscripten-provided virtual filesystem, so may also make use of the OPFS storage.
- This support is, as of this writing, currently only available in the main JS thread due to an Emscripten Worker-loading issue. 
- OPFS support via WASMFS has to be explicitly activated. 
  - The first time that is called it will, if needed, try to activate the WASMFS OPFS backend and "mount" it on a specific virtual directory. 
  - Calls after the first one simply return the directory name returned by the first call, without trying to (re)initialize the OPFS support.
- Though the mount point name is intended to stay stable, client code should avoid hard-coding it anywhere and always use this function to fetch it. 
  - It will not change in the lifetime of a single session, so it may be saved for reuse, but it should not be hard-coded.
- OPFS's file locking support is, as of this writing (late 2022), a moving target but WASMFS currently locks OPFS-hosted files when write operations start on a file and release the lock when the last handle to the file is closed. 
  - (Noting that WASMFS has its own higher-level abstraction of file handles so that it can support multiple filesystems.)

### Cross-thread Communication via OPFS

- sqlite3 over OPFS opens up a possibility in JS which does not otherwise readily exist: communication between arbitrary threads.
- There are no mechanisms in JS to share state between two threads except `postMessage()`,        `SharedArrayBuffer`, and (to a very limited extent) `Atomics`. 
  - localStorage, sessionStorage, and the long-defunc (but still extant) WebSQL, are main-thread only. 
  - Presumably WebSQL was not permitted in Workers for the very reason that it would open up a communication channel between arbitrary threads.
- However, if a client loads the sqlite3 module from multiple threads, they can communicate freely via an OPFS-hosted database. 
  - Mostly. Such usage would introduce file-locking contention between the threads. 
  - So long as each thread uses only very brief transactions, the automatic lock-retry mechanism will transparently account for the locking, 
  - but as soon as one thread holds a transaction open for any significant amount of time, or too many threads are contending for access, locking-related exceptions would result and would be translated as I/O errors to the C API.

- Whether the capability of communicating across threads via a database is a feature or a bug is left for the client to decide.

## Building JS/WASM Bundles

- sqlite3.js and sqlite3.wasm are the "standard builds"
  - built for wide deployment on a number of browsers, with optional support for persistent storage usage OPFS.

## Related Works

- https://github.com/rhashimoto/wa-sqlite
  - the first known implementation of OPFS storage of sqlite databases.
- https://github.com/jlongster/absurd-sql
  - demonstrates storing sqlite3 databases inside IndexedDB databases.
- https://github.com/snaplet/postgres-wasm
  - runs a Postgres database server in a browser.
- https://github.com/sagemathinc/cowasm
  - Collaborative WebAssembly for Servers and Browsers. Built using Zig.
# more
