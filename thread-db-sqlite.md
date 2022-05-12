---
title: thread-db-sqlite
tags: [database, sqlite]
created: '2021-08-25T14:05:02.158Z'
modified: '2021-08-25T14:05:18.280Z'
---

# thread-db-sqlite

# discuss

- ## 

- ## 

- ## 

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
