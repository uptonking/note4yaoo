---
title: lib-db-indexeddb-blog
tags: [blog, indexeddb]
created: 2022-06-13T02:56:54.717Z
modified: 2022-06-13T02:57:07.648Z
---

# lib-db-indexeddb-blog

# guide

# [rxdb: Why IndexedDB is slow and what to use instead](https://rxdb.info/slow-indexeddb.html)
- [Why IndexedDB is slow and what to use instead](https://github.com/pubkey/rxdb/blob/master/docs-src/slow-indexeddb.md)

- For in-browser data storage, you have some options:
- **Cookies** are sent with each HTTP request, <= 4kb.
- **LocalStorage** is a synchronous API over asynchronous IO-access. 
  - Storing and reading data can fully block the JavaScript process 
  - <=5mb. you cannot use LocalStorage for more then few simple key-value pairs.
- **IndexedDB** is an indexed key-object database. 
  - It can store json data and iterate over its indexes. 
  - It is [widely supported](https://caniuse.com/indexeddb) and stable.
- The **FileSystem API** could be used to store plain binary files, 
  - but it is [only supported in chrome](https://caniuse.com/filesystem) for now.
- **WebSQL** [is deprecated](https://hacks.mozilla.org/2010/06/beyond-html5-database-apis-and-the-road-to-indexeddb/)
  - because it never was a real standard and turning it into a standard would have been too difficult.

- IndexedDB is slow. 
  - Inserting a few hundred documents can take up several seconds. 
  - Even sending data over the internet to the backend can be faster then storing it inside of an IndexedDB database.

- the key point here is that all these documents get written in a single transaction.
- 👉🏻 I forked the comparison tool here and changed it to use one transaction per document write. 
  - And there we have it. Inserting 1k documents with one transaction per write, takes about 2 seconds.
  - Interestingly if we increase the document size to be 100x bigger, it still takes about the same time to store them. 
  - This makes clear that the limiting factor to IndexedDB performance is the transaction handling, not the data throughput.

- To fix your IndexedDB performance problems you have to make sure to use as less data transfers/transactions as possible. 
- But most of the time is not so easy. 
  - Your user clicks around, data gets replicated from the backend, another browser tab writes data. 
  - All these things can happen at random time and you cannot crunch all that data in a single transaction.
- Another solution is to just not care about performance at all. 
  - In a few releases the browser vendors will have optimized IndexedDB and everything is fast again. 
  - The chromium devs made a statement to focus on optimizing read performance, not write performance.

- In the following I lay out some performance optimizations than can be made to have faster reads and writes in IndexedDB.

## Batched Cursor

- With the `getAll()` method, a faster alternative to the old `openCursor()` can be created which improves performance when reading data from the IndexedDB store.
- Interestingly choosing a high batch size is important. 
  - When you known that all results of a given `IDBKeyRange` are needed, you should not set a batch size at all and just directly query all documents via `getAll()`.

## IndexedDB Sharding

- Sharding is a technique, normally used in server side databases, where the database is partitioned horizontally. 
  - Instead of storing all documents at one table/collection, the documents are split into so called shards and each shard is stored on one table/collection. 
  - This is done in server side architectures to spread the load between multiple physical servers which increases scalability.

- When you use IndexedDB in a browser, there is of course no way to split the load between the client and other servers. 
- Partitioning the documents horizontally into multiple IndexedDB stores, has shown to have a big performance improvement in write- and read operations while only increasing initial pageload slightly.
  - sharding should always be done by `IDBObjectStore` and not by database. 
  - 👉🏻 Running a batched cursor over the whole dataset with 10 store shards in parallel is about 28% faster then running it over a single store.
- As downside, getting 10k documents by their id is slower when it has to run over the shards.

## Custom Indexes

- Indexes improve the query performance of IndexedDB significant. 
  - Instead of fetching all data from the storage when you search for a subset of it, you can iterate over the index and stop iterating when all relevant data has been found.

- As shown, using a custom index can further improve the performance of running a batched cursor by about 10%.
- Another big benefit of using custom indexes, is that you can also encode `boolean` values in them, which cannot be done with normal IndexedDB indexes.

## Relaxed durability

- Chromium based browsers allow to set durability to `relaxed` when creating an IndexedDB transaction. 
  - Which runs the transaction in a less secure durability mode, which can improve the performance.
  - The user agent may consider that the transaction has successfully committed as soon as all outstanding changes have been written to the operating system, without subsequent verification.

## Explicit transaction commits

- By explicitly committing a transaction, another slight performance improvement can be achieved. 
  - Instead of waiting for the browser to commit an open transaction, we call the `commit()` method to explicitly close it.
  - The improvement of this technique is minimal, but observable as these tests show.

## In-Memory on top of IndexedDB

- 👉🏻 To prevent transaction handling and to fix the performance problems, we need to stop using IndexedDB as a database. 
- Instead all data is loaded into the memory on the initial page load. 
  - Here all reads and writes happen in memory which is about 100x faster. 
  - Only some time after a write occurred, the memory state is persisted into IndexedDB with a single write transaction. 
  - In this scenario IndexedDB is used as a filesystem, not as a database.
- There are some libraries that already do that:
  - LokiJS with the [IndexedDB Adapter](https://techfort.github.io/LokiJS/LokiIndexedAdapter.html)
  - [Absurd-SQL](https://github.com/jlongster/absurd-sql)
  - SQL.js with the [empscripten Filesystem API](https://emscripten.org/docs/api_reference/Filesystem-API.html#filesystem-api-idbfs). This is provided to overcome the limitation that browsers do not offer synchronous APIs for persistent storage, and so (by default) all writes exist only temporarily in-memory.
  - [DuckDB Wasm](https://duckdb.org/2021/10/29/duckdb-wasm.html)

### In-Memory: Persistence

- One downside of not directly using IndexedDB, is that your data is not persistent all the time. 
  - And when the JavaScript process exists without having persisted to IndexedDB, data can be lost. 
- One point is make persisting as fast as possible. 
  - LokiJS for example has the incremental-indexeddb-adapter which only saves new writes to the disc instead of persisting the whole state. 
- Another point is to run the persisting at the correct point in time
  - When the database is idle and no write or query is running.
  - When the window fires the beforeunload event we can assume that the JavaScript process is exited any moment and we have to persist the state. After beforeunload there are several seconds time which are sufficient to store all new changes. This has shown to work quite reliable.
- The only missing event that can happen is when the browser exists unexpectedly like when it crashes or when the power of the computer is shut of.

### In-Memory: Multi Tab Support

- when you have all database state in memory and only periodically write it to disc, multiple browser tabs could overwrite each other and you would loose data. 
  - This might not be a problem when you rely on a client-server replication, because the lost data might already be replicated with the backend and therefore with the other tabs. 
  - But this would not work when the client is offline.
- The ideal way to solve that problem, is to use a SharedWorker. 
  - A SharedWorker is like a WebWorker that runs its own JavaScript process only that the SharedWorker is shared between multiple contexts. 
  - You could create the database in the SharedWorker and then all browser tabs could request the Worker for data instead of having their own database. 
- But unfortunately the SharedWorker API does not work in all browsers. 
  - Safari dropped its support and InternetExplorer or Android Chrome, never adopted it. 
  - Also it cannot be polyfilled. 
- Instead, we could use the `BroadcastChannel` API to communicate between tabs and then apply a leader election between them. 
  - The leader election ensures that, no matter how many tabs are open, always one tab is the Leader.
- The disadvantage is that the leader election process takes some time on the initial page load (about 150 milliseconds). 
  - Also the leader election can break when a JavaScript process is fully blocked for a longer time. 
  - When this happens, a good way is to just reload the browser tab to restart the election process.
# [re: Why IndexedDB is slow and what to use instead - RavenDB NoSQL Database_202112](https://ravendb.net/articles/re-why-indexeddb-is-slow-and-what-to-use-instead)
- I don’t actually know anything about IndexedDB, but I have been working with databases for a sufficiently long time to understand what the root problem here is.
- the trouble is not with the number of documents that are being saved, but the number of transactions.
- I dug a bit and found that IndexedDB is based on LevelDB (and I do know that one quite a bit). The underlying issue is that each transaction commit needs to issue an fsync(), and fsync is slow!
- Pretty much all database engines have to deal with that, the usual answer is to allow transaction merging of some sort. Many relational databases will write to the log and commit multiple transactions in a single fsync(), RavenDB will do explicit transaction merging in order to batch writes to disk.
- However, for pretty much every database out there with durability guarantees, the worst thing you can do is write a lot of data one transaction at a time. Server databases still benefit from being able to amortize multiple operations across different requests, but a client side database is effectively forced to do serial work with no chance for optimization.
- From the client perspective, the only viable option here is to batch writes to get better performance. Then again, if you are working on the client side, you are either responding to a user action (in which case you have plenty of time to commit) or running in the background, which means that you have the ability to batch.
# [The pain and anguish of using IndexedDB: problems, bugs and oddities_202211](https://gist.github.com/pesterhazy/4de96193af89a6dd5ce682ce2adff49a)
- This gist lists challenges you run into when building offline-first applications based on IndexedDB, including open-source libraries like Firebase, pouchdb and AWS amplify 

- State deleted after 7 days of inactivity (Safari)
  - After 7 days of inactivity, Safari deletes all browser storage, including cookies, localstorage, websql and indexeddb. Other browsers don't do this.
  - The feature, called Intelligent Tracking Prevention (ITP), is meant to prevent advertisers from abusing indexeddb as a way to track users.

- Is IndexedDB ACID compliant?
  - IndexedDB does not provide transaction isolation. As far as I know, concurrent transactions (in multiple tabs or even in a single tab) are never rolled back because they touch the same object stores. The only exception, as far as I can tell, is exceptions thrown when a primary key constraint is violated. This can be used to achieve some level of transaction isolation. However, the guarantees are nowhere near as extensive as those provided by SQL databases.

- No locking primitives (Safari, Firefox)
  - The Web Platform lacks a standardized way - or any proper way, really - to lock a resource across multiple tabs of the same browser. Multiple tabs of an app using IndexedDB will invariably write to the same IndexedDb database. Without cross-tab locking, database corruption is hard to avoid.

- Private Browsing Mode (Firefox)
  - Firefox is the only major browser without support for IndexedDB in Private Browsing mode. 
  - Because there is no API to tell if Private Browsing is active, the only workaround is to try to open a test database and to regard the API as unavailable if this fails.

- Web SQL - the database that could have been
  - Before IndexedDB there was Web SQL, a thin wrapper around the legendary SQLite embedded database. Web SQL is more powerful (a proper superset of IndexedDB) and arguably better designed than IndexedDB.
  - Mozilla objected to the Web SQL interface as having no alternative implementation available. 
  - Ironically, IndexedDB is internally implemented based on SQLite in Firefox (Chrome uses the simpler LevelDB instead).

- [Notion's page load and navigation times just got faster_202104](https://www.notion.so/blog/faster-page-load-navigation)
  - We decided to migrate our desktop apps to SQLite because it's a hardened storage solution that's shown marked performance improvements on our mobile applications for the past year.
  - Before SQLite, we relied on IndexedDB for client-side storage. 
  - But we encountered storage quotas, a number of bugs, and performance concerns on Windows machines in particular, which meant IndexedDB wouldn’t scale with Notion’s growing user base.

- Bugs, bugs, bugs (Safari)
  - The Webkit team keeps shipping critical storage-related bugs into production, again and again
# [Best Practices for Using IndexedDB_201706](https://web.dev/indexeddb-best-practices/)

> Learn best practices for syncing application state between IndexedDB and (in-memory) popular state management libraries.

- When a user first loads a website or application, there's often a fair amount of work involved in constructing the initial application state that's used to render the UI.
  - For example, sometimes the app needs to authenticate the user client-side and then make several API requests before it has all the data it needs to display on the page.
- Storing the application state in IndexedDB can be a great way to speed up the load time for repeat visits. 
  - The app can then sync up with any API services in the background and update the UI with new data lazily, employing a stale-while- revalidate strategy.
- Another good use for IndexedDB is to store user-generated content, either as a temporary store before it is uploaded to the server or as a client-side cache of remote data - or, of course, both.

- Keeping your app predictable
- A lot of the complexities around IndexedDB stem from the fact that there are so many factors you (the developer) have no control over.
- Not everything can be stored in IndexedDB on all platforms
  - If you are storing large, user-generated files such as images or videos, then you may try to store them as `File` or `Blob` objects. 
    - This will work on some platforms but fail on others. 
    - Safari on iOS, in particular, cannot store Blobs in IndexedDB.
    - Storing ArrayBuffers in IndexedDB is very well supported.
    - a Blob has a MIME type while an ArrayBuffer does not. You will need to store the type alongside the buffer in order to do the conversion correctly.
- Writing to storage may fail 
  - Errors when writing to IndexedDB can happen for a variety of reasons, and in some cases these reasons are outside of your control as a developer.
  - For example, some browsers currently don't allow writing to IndexedDB when in private browsing mode.
  - There's also the possibility that a user is on a device that's almost out of disk space, and the browser will restrict you from storing anything at all.
  - This also means it's generally a good idea to keep application state in memory (in addition to storing it), so the UI doesn't break when running in private browsing mode or when storage space isn't available 
- Stored data may have been modified or deleted by the user
  - Unlike server-side databases where you can restrict unauthorized access, client-side databases are accessible to browser extensions and developer tools, and they can be cleared by the user.
- Stored data may be out of date 
  - IndexedDB has built-in support for schema versions and upgrading via its `IDBOpenDBRequest.onupgradeneeded()`
  - you still need to write your upgrade code in such a way that it can handle the user coming from a previous version (including a version with a bug).
  - Unit tests can be very helpful here

- Keeping your app performant
  - As a general rule, reads and writes to IndexedDB should not be larger than required for the data being accessed.
  - While IndexedDB makes is possible to store large, nested objects as a single record, this practice should be avoided. 
    - 👀 The reason is because when IndexedDB stores an object, it must first create a structured clone of that object, and the structured cloning process happens on the main thread. 
    - The larger the object, the longer the blocking time will be.
  - while simply storing the entire state tree as a single record in IndexedDB may be tempting and convenient, doing this after every change (even if throttled/debounced) will result in unnecessary blocking of the main thread, it will increase the likelihood of write errors, and in some cases it will even cause the browser tab to crash or become unresponsive.
  - 👉🏻 Instead of storing the entire state tree in a single record, you should break it up into individual records and only update the records that actually change.
    - In cases where it's not feasible to break up a state object and just write the minimal change-set, breaking up the data into sub-trees and only writing those is still preferable to always writing the entire state tree. 
  - The same is true if you store large items like images, music, or video in IndexedDB.
- Lastly, you should always be measuring the performance impact of the code you write.
# firefox: indexeddb
- mozilla-firefox-indexeddb - sqlite
  - https://hg.mozilla.org/mozilla-central/file/default/dom/indexedDB

- Mozilla objected to the Web SQL interface as having no alternative implementation available. 
  - So IndexedDB, an API with less surface, was chosen instead. Ironically, IndexedDB is internally implemented based on SQLite in Firefox (Chrome uses the simpler LevelDB instead).

- [Firefox uses SQLite to implement IDB, while Chrome uses leveldb. SQLite wins again.](https://twitter.com/jlongster/status/1425833031068180481)
# safari-webkit: indexeddb
- webkit的indexeddb基于sqlite实现
  - 提供了 SQLiteIDBBackingStore.cpp、MemoryIDBBackingStore.cpp
  - https://github.com/WebKit/WebKit/blob/main/Source/WebCore/Modules/indexeddb/server/SQLiteIDBBackingStore.cpp
# chrome: indexeddb
- chromium/blink - backendStore没找到leveldb
  - https://chromium.googlesource.com/chromium/blink/+/refs/heads/main/Source/modules/indexeddb/

- linux位置

## [IndexedDB](https://chromium.googlesource.com/chromium/src/+/master/content/browser/indexed_db/docs/README.md)

- (IndexedDB) Backing Store
  - The backing store represents all IndexedDB data for an origin. 
  - This includes all IndexedDB databases for that origin. 
- 👉🏻 A backing store has a dedicated leveldb database where all data for that origin is stored.
- A leveldb database represents a leveldatabase database. Each backing store has a unique leveldb database, located at: `IndexedDB/<serialized_origin>.leveldb/`.

- An IndexedDB database represents a database in the IndexedDB API. 
  - The backing store can contain many IndexedDB databases. 
  - 👉🏻 So a single LevelDB database has multiple IndexedDB databases.
  - IndexedDB databases are identified by a unique auto-incrementing int64_t database_id.

- Blob Storage
  - Blob are supported in IndexedDB to allow large values to be stored in IndexedDB without needing to save them directly into leveldb (which doesn't work well with large values). 
  - Blobs are a special type of “External Object”, i.e. objects where some other subsystem in chrome is involved in managing them.

## [chrome: IndexedDB Data Path](https://chromium.googlesource.com/chromium/src/+/a77a9a172b05957ad025104fc62979d5e2b87323/third_party/blink/renderer/modules/indexeddb/docs/idb_data_path.md)

- This document is a quick overview of the Blink implementation of IndexedDB read/write requests.
- Chrome's IndexedDB implementation is logically split into two components.
- The Blink side, also called the frontend in older code, implements the interfaces in the IndexedDB specification, translates requests from Web applications into lower-level requests for the IndexedDB backing stores, and performs a fair amount of error checking.
- The browser side, also called the backend in older code, implements the IndexedDB backing store, which executes the low-level requests coming from the Blink side.
- The two components are currently (Q4 2017) hosted in separate processes and bridged by a couple of glue layers. As part of the OnionSoup 2.0 effort, we hope to most of the backing store implementation in Blink, and remove the glue layers.
- The backing store implementation is built on top of two storage systems:
  - Blobs, managed by the Blob system, are stored as individual files in a per-origin directory. Blobs are specifically designed for storing large amounts of data.
  - LevelDB is a key-value store optimized for small keys (10s-100s of bytes) and fairly small values (10s-1000s of bytes). Chrome creates a per-origin LevelDB database that holds the data for all the origin's IndexedDB databases. The LevelDB database also holds references to the Blobs stored in the Blob system.
# [How the browsers store IndexedDB data_201210](https://www.aaron-powell.com/posts/2012-10-05-indexeddb-storage/)
- At the time of writing the IndexedDB implementation of WebKit, and by extension Chrome, is still prefixed
  - leveldb

- firefox is using SQLite as IndexedDB replaced the WebSQL proposal which was based on SQLite 
  - `%AppData%\Roaming\Mozilla\Firefox\Profiles\your profile id\indexedDB\domain`

- Internet Explorer 10 uses the Extensible Storage Engine as its underlying storage model. 
  - This is the same database format that many of Windows features use including the Desktop Search (very common in Windows 8), Active Directory on Windows Servers and even Exchange.
  - `%AppData%\Local\Microsoft\Internet Explorer\Indexed DB\Internet.edb`
# rxdb

## [Alternatives for realtime offline-first JavaScript applications](https://rxdb.info/alternatives.html)

- this page contains all known alternatives to RxDB

- RxDB supports using Dexie.js as RxStorage which enhances IndexedDB with RxDB features like MongoDB-like queries etc

## more rxdb

- https://news.ycombinator.com/from?site=rxdb.info
# more
- [local-first tech](https://jaredforsyth.com/posts/)
