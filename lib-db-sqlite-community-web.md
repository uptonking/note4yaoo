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

- ## Two reasons to use the Notion desktop app(202212):
- https://twitter.com/NotionHQ/status/1606002597579538432 
  - 50% faster performance than web
  - a more focused writing experience
- We use IndexedDB, but not for caching content (and we fight it all the time as it is 😱). Unsure if we've ever tried throwing blocks in there.
  - We’ve had good experience caching all your calendar and contacts data with @Cron in IDB, to a less voluminous degree, but essentially also just JSON blobs. That said, SQLite has been rock-solid for other projects I’ve worked on.

- If IDB was less finicky(难以令人满意的，挑剔的) for Notion’s use case and we used it for blocks, could we get the same 50% for the web app?!
- IndexedDB struggles with block-level granularity. We'd need to build a batched cache strategy instead of caching each block individually. We've also seen a lot of IDB flake(怪人); at a certain scale, problems that affect 0.1% of users start to result in a lot of bug reports.
- 👉🏻 You have to do your own paging to get good performance with idb. It’s best thought of as a block store not a kv store.
  - Replicache aggregates data into blocks of roughly 4kb and we found that to be the best tradeoff.
- Yep, that was my conclusion too. Instead of doing all the paging work, we're gonna wait for SQLite + OPFS for web to mature.
- My only concern is how it’s going to work across tabs. We had to do a lot of pretty clever work in Replicache to make it fast and support schema changes across tabs. Hard to make it fast when access blocks on cross-process locks.
- I was thinking we’d funnel all access through a ServiceWorker or SharedWorker. No locks needed. We already negotiate schema updates for SQLite/IndexedDB in a simple way - tabs that are out of date switch to memory and/or refresh.
- That will work but you’ll still have the latency to service worker, which will cause you to want to run mutations against the per tab cache locally, not against the service worker. This means there can be conflicts when two tabs mutate their local cache in conflicting ways.
  - Basically you end up having to sync the store with tabs in the same way you sync with server today. Because no matter what you’ll want in memory perf in the tabs. It ends up being kind of a two level sync: tabs to storage, storage to server.
  - This can all totally work (we have it working). It’s just not as simple as “just  read/write direct to sqlite” which is what I think a lot of people are hoping.
- We already have a SQLite in a separate process we talk to via JSON (& the tab in memory cache, write operation queue, etc etc etc), hopefully a SQLite in a Worker we talk to with structured clone will perform even better
- Firebase coordinates the primary tab by acquiring a lease via IndexDB. A good explanation on how that pivots to using broadcast channel is in the comments
  - That kind of strategy also works. My point is only that “just use sqlite” I don’t think magically addresses performance, because there is cross process synchronization that is fundamental to running in a web browser.


- ## What’s the advantage of using WASM SQLite over IndexedDB for a web application?
- https://twitter.com/frankdilo/status/1600579551771377674
- IndexedDB can never be as fast, plus SQLite is just way more advanced to use...
- Indexeddb has an awful api, is way less performant, and you cant use it on other platforms (desktop/mobile apps) if you're sharing persistence code!
- Are you using it for Reader?
  - Both, sadly. Would love to only use wasm sqlite but it doesnt support persistence to disk yet!
  - That’s what I was wondering about. Does it use IndexedDB under the hood to save data?
  - We only use the wasm sqlite for full-text-search right now, and we just dump the whole db to disk periodically. 
  - Everything else (storing document data, syncing, etc) is on indexeddb still yes 😢 it's too critical to trust with wasm sqlite

- ## I’ve been playing with SQLite in the browser via WASM the past few days. 
- https://twitter.com/devongovett/status/1600679294833156097
  - I have to say, it’s really nice to have a full database available locally. 
  - Once you’ve downloaded the data, you can sort, filter, join, etc basically instantly with no network requests. And it works offline!
- Is the reason to use SQL lite vs index db a preference for the API? Or is there some reason why indexeddb doesn't work in some use cases?
  - It’s much easier to do complex queries and joins with SQL in a high level, declarative way. 
- I guess what I’m missing is why you’d want to send a large amount of data to each user. I’ve always found using SQL on the server side to be plenty fast, and you still have to send incremental updates and incorporate them into the local copy of the database.
  - Depends how much data you’re expected to have! But even then, you can load it incrementally in some cases too. This architecture is super common with native mobile apps. Won’t work for everything but could make subsequent updates much faster in many cases.
- @meteorjs has had this for 10+ years with #minimongo.
- I've worked on a kiosk app developed as a PWA that used IndexedDB to permanently store a SQLite database on the client and load it when the app started. There was a service worker that periodically checked if the database had a new version and would download it in background.
- I've seen this done well in AWS amplify stack with the data store library. Client has the db synced. Mutations happen locally and sync when back online. Tradeoff of course is initial sync being large depending on use case, but UI is fast after the sync since the data is local.

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
