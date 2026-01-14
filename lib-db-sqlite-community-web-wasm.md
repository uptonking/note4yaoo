---
title: lib-db-sqlite-community-web-wasm
tags: [community, indexeddb, sqlite, storage, wasm]
created: 2022-11-25T09:47:03.550Z
modified: 2023-12-09T10:03:55.375Z
---

# lib-db-sqlite-community-web-wasm

# guide

- [The Current State of SQLite Persistence on the Web_202307](https://www.powersync.com/blog/sqlite-persistence-on-the-web)
# discuss-stars
- ## 

- ## 

- ## 

- ## Didn’t expect that using SQLite on the browser’s OPFS would turn into a distributed problem too
- https://x.com/zx_loro/status/2009565910999392518
- The fact that doing anything cross tab inside a browser becomes a distributed systems problem, despite it not only being local, but also *in the same process* is absolutely absurd. The APIs we deserve don't exist.

- And it sucks that crossing those boundaries has such a perf hit too

- ## I wonder if instead of SQLite to WASM if it'd be easier to embed DuckDB as WASM for local first 
- https://x.com/RogersKonnor/status/1841881976971698669
- +1 on DuckDB embed story. That and the query language is identical Postgres SQL if I'm not mistaken

- ## 🌰 What if PGlite could lazily load database files over HTTP with range requests?
- https://x.com/samwillis/status/1841816489877286970
  - https://pglite-httpfs-demo.netlify.app/
  - This demo shows how to use PGlite, a WASM build of Postgres running entirely in the browser, with the WIP HttpFs to connect to a remote PGlite database. 
  - It's using HTTP range requests to fetch database file pages from the remote server on demand.

- ## 🆚️ SQLite WASM is much slower than the in-memory better-sqlite3, but still, the new Evolu CRDT algorithm can handle approximately 1666 mutations per second
- https://x.com/evoluhq/status/1836518784539980248
  - I developed and tuned it with the in-memory better-sqlite3, where you can get around 25k mutations per second
  - Note: Don't expect that one mutation will be exactly 1 / 1666; that's not how Just in Time (JIT) compilation works. 
  - The start is always slower before it picks up speed 

- ## 💡 Would anyone believe me if I said I can get IndexedDB to read and write faster than a fully in-memory SQLite DB in the browser?
- https://twitter.com/tantaman/status/1743031911092564338
- that is pretty hard to believe... Are you treating IDB entries like nodes in a btree or something like that?
  - Yeah. Each value is a page and key the range of keys in that page.
- That's cool. Does it make writes faster too?

- cause SQLite is a wasm port with Structured Cloning right? IndexedDB is butt slow tho, have to do major custom batch/throttling and cache/buffering to hide it.
  - Yeah the wasm bridge is hell expensive. For idb, I ended up reading and writing pages of objects to a given key and that key represents the range of keys in the page.
  - This is way faster than any option provided by the idb api. Of course it creates a bunch of complexity.
- Similar to how @FireproofStorge uses it
- Yeah, I do the same, 😫=why can't we just have good native APis

- ## 🌰 eidos 用 sqlite-wasm 做存储，到目前为止丢了两次数据，
- https://twitter.com/mayneyao/status/1720141066240991347
  - 最后发现 OPFS 需要请求数据持久化权限，否则数据可能被浏览器清理掉。
  - API 比较新，相关的文章比较少，记录下。希望你不要丢数据
  - 📝 [Web OPFS 数据持久化](https://gine.me/posts/70f8e931bc17426fb54127948bcf4a0e)
  - 跑去 sqlite 论坛发帖问了下，终于找到问题所在。因为我没有向用户请求数据持久化权限。如果你没有向用户请求持久化权限。数据还是会给你存储，但是浏览器可能会把数据清理掉。 
  - 这一点很隐晦，MDN只给了代码，在代码里面提了下，但是文档里面没怎么说。
  - 如何获取数据持久化权限呢？ `navigator.storage.persist()`

- ## Feature table of all the possible ways of using a sqlite database in a JavaScript environment
- https://twitter.com/fabiospampinato/status/1693379882409922788
- better-sqlite3: it's good, but it's a native dependency, and those can be painful to work with (Electron, C++), and it only works with Node.
- Binaries: nice simple trick, but mainly the serialization overhead for binary blobs is too large, and notarization is painful.
- FFI: amazing if you don't need to use neither custom builds nor Node/Browser.
- JS: mainly sql.js requires reading/writing the entire database at once, which should be a deal breaker.
- WASM: amazing, but without memory-mapping WAL is not supported, and file locking is tricky.

# discuss-against-sqlite
- ## 

- ## 

- ## 

- ## Solid explanation of why web applications using SQLite shouldn't use the default, bare BEGIN TRANSACTION syntax. 
- https://twitter.com/fractaledmind/status/1754903412548800805
  - If you are using a framework that automatically wraps write operations in transactions, that framework should ensure those transactions are EXCLUSIVE or IMMEDIATE
- SQLite transactions are lazy by default -- they only take a write lock when necessary.
  - If your transactions start readonly and then upgrade to writes, it may be better to just declare it a write transaction from the start
  - If you expect the contention(争夺；竞争) to be high -- lots of transactions trying to write at the same time -- `BEGIN EXCLUSIVE` is your friend.
- With `BEGIN EXCLUSIVE` , the flow is:
  1. Transaction A takes a write lock first
  2. Transaction A commits, transaction B takes its write lock
  3. Transaction B commits
- What about WAL mode (write-ahead log journaling)?
  - Well, it gets subtly worse. WAL journaling mode gives you a great concurrency boost, because instead of allowing one writer or N readers, it allows one writer and N readers to execute concurrently.
  - There's a consistency price here though. WAL guarantees you snapshot isolation, which means that each transaction will see some consistent state of the database, and will only commit if there isn't going to be any conflict.
  - That's optimistic concurrency -- we assume everything is going to be alright and proceed, and worst case we get an error and need to roll back.
- Again, `BEGIN EXCLUSIVE` lets you opt-out of optimistic concurrency, if you know your workload has high contention.
- There's also another flavor of transactions in SQLite - `BEGIN IMMEDIATE` , almost identical to `EXCLUSIVE` , and in fact totally identical in WAL mode. 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🆚 Your SQLite bindings really matter.
- https://x.com/tantaman/status/1956151559110451499
  - hermes vs better-sqlite3 vs rust

- ## How Notion uses Sqlite WASM.
- https://x.com/evoluhq/status/1813874658619601205
  - Evolu do that without Shared Workers which are not supported on Android.

- ## [Cloud Backed SQLite | Hacker News_202307](https://news.ycombinator.com/item?id=36610595)
- I've just been exploring serving large SQLite databases in chunks and querying them with http range requests to prevent downloading the entire database. It's pretty awesome! I found a really interesting library called sql.js-httpvfs that does pretty much all the work. I chunked up my 350Mb sqlite db into 43 x 8Mb pieces with the included script and uploaded them with my static files to GitHub, which gets deployed via GitHub Pages

- 
- 
- 
- 

- ## [SQLite WASM: Something subtle in the browser | Hacker News_202302](https://news.ycombinator.com/item?id=34774357)
- 
- 
- 

- ## 🤔🔥 [Why SQLite is so great for the edge | Hacker News_202306](https://news.ycombinator.com/item?id=36208568)
- 
- 
- 

- ## SQLite is just corruption-prone under Windows?
- https://twitter.com/fabiospampinato/status/1693284873581060429
  - SQLite is very clear that you can corrupt a database if file locking APIs are not working correctly.
  - By the way POSIX advisory lock APIs that only work on linux/mac are still pretty valuable for server-only use cases, nobody sane uses Windows there anyway. 

- SQLite CLI on Windows works without any special warning though … not sure if that’s due specific Windows code or just a “no need to warn users here stuff easily breaks” but I’m also sure SQLite is used in many Windows only projects too

- ## Thinking about local-first apps with SQLite for apps without auth.
- https://twitter.com/ralex1993/status/1679877455308283907
  - Run a single server with a SQLite database.
  - Backup that database to file storage like S3
  - Every browser client downloads the database to OPFS
  - Hacked browser-based ORM so writes are HTTP proxied to server
- OBFS = Origin Private File System, a way to store big files in browser-based apps.
  - This would depend on a realtime sync engine to get origin DB updates to connected browsers.
  - And I still have no idea how to do auth and gated content in local-first apps. It's a tough problem.
  - So so so many other caveats with this approach. It's a seriously idle thought, and I've considered exactly 0 implementation details or edge cases. But it could be a fun experiment.

- I've had requests for something similar with Litestream. People wanted to stream up to S3 and then have replicas stream down. The latency is not great but the bigger problem is usually egress cost ($0.09/GB).

- ## I'm looking for feedback on an idea I have for massively scaling @Cosmos infra costs by serving just the node's DB over the internet and running the node in the browser.
- https://twitter.com/assafmo/status/1681659436329488384
- 💡 How it works:
  - Run a regular node with a PostgreSQL/SQLite DB backend
  - Compile a version of the node to Wasm. We just need the query & simulation logic, no need to keep up with blocks or p2p.
  - Run that node in the browser, connecting to the remote DB
  - Profit
- This would massively reduce the infrastructure costs of running @CosmosSDK nodes just to serve queries, as this delegates the heavy computations to the client, while the backend only serves the DB.
- However, there are some technical challenges that would need to be addressed in order to implement this idea. Namely, compiling just the relevant parts to Wasm, but also how to run that node in the browser in a way that it would still be compatible with current client libraries.

- ## vlcn: One of the things I'm most excited for is partnering with the LibSQL folks to create a custom syntax for defining tables which are backed by CRDTs!
- https://twitter.com/tantaman/status/1643588081067384834

- ## Spent a week optimizing `useQuery` to get hundreds of concurrent SQLite queries to return in a single frame in the browser.
- https://twitter.com/tantaman/status/1634579771404288002
  - And now realizing that implementing a fully reactive SQL layer actually isn't that far out of reach.

- 🤔 What was the challenge?
- On reactive sql (in progress), the main insight is its an inverted database. You index the queries via ranges then see if an insert/update/delete overlaps a query’s range.
- React specific -- react is "call happy" when invoking `useSyncExternalStore` so.. intelligently caching there, and "folding" many invocations to `useSyncExternalStore` into a single call
- A simple, and dumb one, is just making sure `useQuery` always uses prepared statements. Preparing a statement can take up ~75% of the time of a query.
- Implicit read transaction actually have quite an overhead (esp when indexeddb is backing sqlite). Putting all calls to `useQuery` in a given render pass together in one read transaction was a huge win.
- These are also interesting as a baseline of what SQLite can do in the browser:  
  - [wa-sqlite benchmarks](https://rhashimoto.github.io/wa-sqlite/demo/benchmarks.html)
- Curious to know how tuppledb helped you
  - Just reading through their approaches to reactivity. So for the second half of the tweet, unrelated to the first.

- [Many Small Queries Are Efficient In SQLite](https://www.sqlite.org/np1queryprob.html)
  - with SQLite, 200 or more SQL statement per webpage is not a problem.

- ## What are the limitations of sql.js? As far as I read on their site, it is also SQLite compiled to wasm.
- https://twitter.com/visheratin/status/1623068001112059921
- For us @fleetctl the key limitation is lack of support for virtual tables (a really interesting feature of SQLite if you haven't checked it out!)
- I haven't worked with SQLite in a browser yet, but do I understand right that wa-sqlite, as well as sql.js, reads the whole DB in memory to start working with it?
  - My understanding is that is the case with sql.js and it's not with wa-sqlite. I'm much less familiar with the storage side of SQLite, but their VFS concept looks quite interesting
- It seems like wa-sqlite really performs partial reads/writes over the pages. But my concern is that this logic might be slower than keeping everything in memory.
- in the in-memory case, what happens if the user leaves the page, it crashes, browser exits, etc? Do you have to persist after every operation?
  - Yes. sql.js maintainer in this issue said that exporting is a rather fast operation even for large databases.

- ## [Anyway to save SQL DB to IndexedDB without calling export() for persistence? · Issue #302 · sql-js/sql.js](https://github.com/sql-js/sql.js/issues/302)
- I am currently having to call export every time I need to save to indexedDB for persistence. The problem is export greatly increases the save time taken and I cannot save just the SQLJS object due to the new SQL.database constructor not being able to handle that? Is there any way around this or could this be a possible enhancement.
- Also @jlongster has forked SQL.js to add the supported hooks to allow for custom filesystems. Would be great to see these incorporated into SQL.js mainline.
- Unfortunately the suitability of the File System Access API for SQLite seems to be going nowhere, despite its recent support in Safari. First of all, Firefox seems pretty strongly opposed to it.
  - In addition, it looks like Chrome's implementation for writes copies the file, writes to the copy, scans the copy for malware, and renames the copy over the original. So changing 1 block of a 1GB SQLite database might cost over 2GB of I/O (1 for the copy, 1 for the scan) unless your filesystem has some kind of block-level deduplication. That's probably worse than export(). Not sure what Safari does.

- ## Funny how I tend to overcomplicate things. Working on a project that processes lots of data in the browser (~12M records).
- https://twitter.com/mgechev/status/1608266730765422594
- First I tried to find an efficient multidimensional index implemented in C++/Rust to compile to WASM and query in a Web Worker.
  - Didn't work great because of missing SIMD instructions in WASM that the C++ data structure depends on.
- Decided to switch to a simpler data structure that doesn't use SIMD...and is slower.
  - The pointers for this PHTree created too big of a memory overhead so the browser wouldn't execute the script before running out of memory.
- I was thinking...let me use SQLite compiled to WASM and create an index over the columns I run queries.
  - The database grew to 800MB, but the gzipped version it was still manageable.
- Funny thing, it was performing *almost* just as well as the database without an index, that was almost half the size...
  - Still querying the database in a Web Worker to offload from the main thread.
- Decided to compare the performance of SQLite to simple for loops over an array...
  - Guess what...the for loop was close to twice faster.
- Ended up using just a simple for loop over ~200MB data file in a Web Worker and the performance is decent. The complexity is also way lower.
- Turned out SQLite is >25% faster. Glad I went that route :)
  - I ran in the same browser and did a proper benchmark the second time.

- ## Two reasons to use the Notion desktop app(202212):
- https://twitter.com/NotionHQ/status/1606002597579538432 
  - 50% faster performance than web
  - a more focused writing experience
- We use IndexedDB, but not for caching content (and we fight it all the time as it is 😱). Unsure if we've ever tried throwing blocks in there.
  - We’ve had good experience caching all your calendar and contacts data with @Cron in IDB, to a less voluminous degree, but essentially also just JSON blobs. That said, SQLite has been rock-solid for other projects I’ve worked on.

- If IDB was less finicky(难以令人满意的，挑剔的) for Notion’s use case and we used it for blocks, could we get the same 50% for the web app?!
- 👉🏻 IndexedDB struggles with block-level granularity. We'd need to build a batched cache strategy instead of caching each block individually. We've also seen a lot of IDB flake(怪人); at a certain scale, problems that affect 0.1% of users start to result in a lot of bug reports.
- 👉🏻 You have to do your own paging to get good performance with idb. It’s best thought of as a block store not a kv store.
  - Replicache aggregates data into blocks of roughly 4kb and we found that to be the best tradeoff.
- Yep, that was my conclusion too. Instead of doing all the paging work, we're gonna wait for SQLite + OPFS for web to mature.
- 👉🏻 As someone casually building with IDB, could you explain what you mean by doing your own paging?
  - Make the records you store in IndexedDB big & chunky. @aboodman suggested 4kb per record. So, treat records more like “pages” in a DB, not rows like in a SQL-style DB.
  - That makes sense. It's a little disappointing. I think maybe I could chunk operation data by document, since it's already generally accessed by range. But I'd prefer not to re-implement stuff like querying hybridized in-memory and in-store. Maybe I'll keep an eye on sqlite too...
  - Once you read rows out of SQLite or IndexedDB where do they go? Straight into the DOM never to be looked at again??? You’ll want a cache either way. OTOH whenever you get advice from Randoms Online, ignore the advice and do the Simplest Thing That Could Possibly Work first
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
  - Other browser storage options are either nosql, slow or just weird (IndexedDB).

- ## [SQLite in the browser with WASM/JS_202210](https://news.ycombinator.com/item?id=33374402)
- You may have seen “Absurd SQL” which was a proof of concept for building a SQLite Virtual FS backend using IndexedDB. It provided full ACID compliment transactions. Incredible work but a hack at best.
  - The OPFS supersedes all that and makes it possible to have proper consistent and resilient transactions.
  - WASM SQLite with the OPFS is the future of offline first web app development. The concept of a single codebase web/mobile/desktop app with proper offline storage is here.
- I previously experimented with combining Yjs (CRDT toolkit) with Pouch/CouchDB to create an eventually consistent db, but decided that CouchDB was the wrong backend.

- ## 👉🏻 A long, tragic history of SQLite, the web, and my career.
- https://twitter.com/aboodman/status/1633351945464475648
  - 2020: Chrome implements cache partioning, killing the ability to share large wasm objects like SQLite across web pages.
  - So what's the takeaway? I guess for me some concrete ones are:
  - API design is very difficult. IDB had universal vendor support, but just turned out to not be what devs wanted.
- The arc of software history bends toward the right solution, independent of roadblocks. Nowadays because of OSS the arc bends a lot faster. It's very difficult/impossible for vendors to *mandate* something that isn't good.
- If we want to preserve the zero-install experience of the web *and* enable rich web pages, we need *some* way to share objects across sites. We can't and shouldn't rely on browsers to implement the majority of APIs. There has to be some way for developers to do this. 
