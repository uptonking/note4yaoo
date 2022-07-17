---
title: thread-db-sqlite
tags: [database, sqlite]
created: 2021-08-25T14:05:02.158Z
modified: 2021-08-25T14:05:18.280Z
---

# thread-db-sqlite

# discuss

- ## 

- ## 

- ## Bun.js v0.0.83 gets a fast builtin SQLite client
- https://twitter.com/jarredsumner/status/1525105862997442560
- https://github.com/jpwhite3/northwind-SQLite3
  - This is a version of the Microsoft Access 2000 Northwind sample database, re-engineered for SQLite3.
  - The Northwind sample database was provided with Microsoft Access as a tutorial schema for managing small business customers, orders, inventory, purchasing, suppliers, shipping, and employees.
  - All the TABLES and VIEWS from the MSSQL-2000 version have been converted to Sqlite3 and included here.

- This is awesome, I was just looking at using SQLite in an Electron app the other day, there's just no great way to do that. You need either a native module, read/write the whole thing to disk or hacky stuff like this (https://github.com/jlongster/absurd-sql). This would be perfect for Electron.
  - you could also include 3 sqlite3 binaries (win, mac, linux) and call it a day via https://github.com/WebReflection/sqlite-tag-spawned
  - Potentially that's an easier option but I'd rather not have native binaries (other than node/electron) at all. If you look here  https://github.com/JoshuaWise/better-sqlite3/releases/tag/v7.5.1 there are like 6 binaries for linux, different binaries for node/electron (why?), no binaries for arm win/mac 
  - lol I didn’t realize they have to compile separate binaries for every version, arch & platform of electron. Bun wouldn’t really have this problem to begin with because with FFI, you can dynamically link any version of any lib so long as the API hasn’t changed
  - Yeah that's why I don't want to touch this stuff 😂 Bun looks great and it's getting better every day, but I just can't switch to it until it allows opening a webview window or something.
  - I didn't suggest better-sqlite and it's slower than my spawned module for what I could test + it boots slow ...  I was suggesting the pre-compiled shell from the original repo. both node-sqlite and better-sqlite modules have never been a solution to me 
- built-in? Like it'll ship as part of the runtime?
  - Yeah, a “bun:sqlite” builtin module. On macOS it will technically be dynamically linked to system-provided macOS because that’s faster. But on linux it will have a statically linked copy
- What if I wanna link with my custom SQLite on macOS?
  - Fwiw, you probably don’t. It’s a 40%-ish perf loss to not use Apple’s version of SQLite. That being said, would actually be straightforward to make this work - just missing a way to specify a filepath to load sqlite from. It wouldn’t be possible on linux though

- ## the idea of having SQLite as the DB has been in my mind for way too long 
- https://twitter.com/WebReflection/status/1524394134429179904
  - and I have also created a prototype that "just works" and it offers amazing DX ... 
  - I was hoping to release it as SaaS (SQLite as a Service), but I guess I can't really compete here 
  - [Cloudflare: Announcing D1: our first SQL database](https://blog.cloudflare.com/introducing-d1/)

- ## What have you used IndexDB for? Would love to hear some stories / use cases, especially for media
- 

- ## Also SQLite3’s Full Text Search combined with triggers is absolutely mind blowing.
- https://twitter.com/SebastianSzturo/status/1515297367335247877
  - Indexed 50GB of data in 10 lines of SQL and it queries under 20ms…
  - This technology exists literally running on our toasters and we still throw Postgres and Elasticsearch at trivial problems.

- Keeping tabs on some distributed SQLite projects that are up & coming:
  - @litestreamio 
  - rqlite & dqlite.io

- The SQLite problem is the concurrent writes, right now you are only able to write one thread at a time, and each write block your whole database, so if you need to write in your database it could be a big problem. If  your use case is mostly about reading data I do agree.
  - SQLite has WAL mode which allows concurrent writes without blocking.
  - If I understood WAL mode correctly, it only enable you to write and read at the same time, but it does not help you with several writes at the same time right? So if you need concurrent writes you will have the same bottleneck.

- ## 3 projects pushing the boundaries of SQLite
- https://twitter.com/simonw/status/1504604448202518529
  - @litestream , @datasetteproj and Riffle!

- ## Announcing "A future for SQL on the web": absurd-sql
- https://twitter.com/jlongster/status/1425825714788503552
  - [A future for SQL on the web](https://jlongster.com/future-sql-web)
  - https://github.com/jlongster/absurd-sql
- absurd-sql adds a backend to sql.js to allow it to persist data to a storage backend. That means you can use it to write real apps!
- It's blazingly fast compared to IndexedDB.
- You can ditch any of those IndexedDB wrappers. Just use SQLite!
  - The *only* downside is that you have to download a 1MB WASM file. 
  - But remember - browsers parse WASM incredibly fast, and even cache compilation so it's only done once!
- You can run my benchmark demo here
  - https://priceless-keller-d097e5.netlify.app/
- Is IndexedDB's durability a problem? Yes, absolutely. 
  - Browsers do not guarantee that your data will last forever -- they may delete it under certain circumstances which sucks.
  - We *really* need better storage APIs for the web.
  - [High performance storage for your app: the Storage Foundation API__202106](https://web.dev/storage-foundation/)
- There are some major missing pieces though. Locking is crucial. I'm in talks with the authors in hopes that this use case is a good test of the API; supposedly it's built for this.
  - Just imagine; if that API lands you just have to switch your backend with a couple lines of code, and you get an order of magnitude (maybe 2!) better performance.
  - This abstracts away the storage backend -- unlike IndexedDB, you're not locked in
- Another thing I learned: wow Chrome's IndexedDB implementation is bad, which sucks because it's the major browser
  - It's consistently TWICE as slow as Safari or Firefox
- I should also mention another project which is similar
  - https://github.com/rhashimoto/wa-sqlite
  - It allows you to write any custom VFS that you want!
  - It makes different tradeoffs and lacks the same optimizations, but that's ok!
- There's a thread on sql.js talking about all of this
  - [Meta VFS for adding storage options](https://github.com/sql-js/sql.js/issues/447)

- Great work by @jlongster : compile SQLite to WebAssembly, use IndexedDB for persistence, and you get a feature-rich and fast client-side database for the web!

- I enjoyed the write up, though I didn't understand some of the benchmarks. It uses IndexDB for persistence, but is faster than indexDB? Or is it faster for operations when it doesn't need to access IndexDB?
  - **It stores stuff in IDB, but since it's working with blocks of data, the amount of reads/writes is drastically reduced, so the equivalent query is much faster in SQL than IDB**

- Does it lazily read the blocks from the remote server, like in phiresky's approach?
  - There's no remote server, but yes it's similar in that it intercepts read/write requests and performs them against a storage backend (indexeddb right now, could be different in the future)
  - So you need to get the full database in memory? I wonder if an hybrid approach would be doable: store local blocks on writes, and use them on read with a fallback on dynamic lazy fetch via http. This way it would work even with huge dbs (say, wikipedia-size).
  - Definitely don't need the full db in memory, but it does have to exist locally. So you'd need to download the full db once and write it down, from then on it won't load the whole thing. The biggest problem extending it to HTTP is locking. Read the last half of the post
  - It's super **easy to corrupt the database if you don't lock it and apply writes correctly**

- Any plans to use something like litestream to replicate the indexdb entries to s3?
  - No but it would be awesome if someone wanted to do that

- In chrome there is a filesystem api one can use that should be faster than indexedDB. 
  - https://github.com/random-access-storage/random-access-chrome-file
  - Already tried. Can't get it to match IDB's performance with long-lived transactions

- According to the MDN pages, Safari doesn't appear to support the Atomics API. Is that a dealbreaker for absurd-sql?
- If the whole thing is on the client side, is it still web, though?

- One thing I want to point out is that Asyncify is usually _faster_ than Atomics approach.
  - However, it's true that it comes with a size overhead (bad, obviously) as well as requires exported APIs to be async too (actually a good thing IMO).
  - There are some ideas and proposals that would eliminate size overhead in the future, but the async API for exports will stay since... well, it makes sense that if you import async API, your export is async too.
- I don't know how Asyncify could possibly be faster. Isn't it pure overhead? This person found a 1.6x perf hit with it. It's hard to measure `Atomics`, but from what I've seen there's barely any perf hit? Why do you think it's slow?
- As for async API: might be fine for some libs, but it's really bad for sqlite. 
  - If it needs to read 1000 blocks, doing that async is going to be way slower just by nature of waiting on promises.
  - Also, it's a huge feature of SQLite that's it's nice and sync. It's always run in a background thread anyway. 
  - If it's on a worker thread, why should I pay the cost of async? (both speed and ergonomics)
- Sure, for your specific usecase it makes sense, I'm just saying that in general I wouldn't call it a fault of Asyncify that it propagates async imports to async exports. It's just a nature of the coloured functions.

- Would this count as a second implementation of WebSQL for the purposes of getting it implemented in browsers?
