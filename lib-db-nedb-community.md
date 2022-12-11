---
title: lib-db-nedb-community
tags: [community, database, nedb]
created: 2022-12-11T22:38:02.682Z
modified: 2022-12-11T22:38:34.694Z
---

# lib-db-nedb-community

# guide

# discuss
- ## 

- ## [Nedb data export to excel/csv formats ?](https://github.com/louischatriot/nedb/issues/518)
- You could simply write a method yourself to load in each obj to memory and pipe it out to JSON.
- By default, a persistent NeDB datafile's format is ndjson (newline-delimited JSON). However, the moment you add a custom afterSerialization and beforeDeserialization hook functions, that default format completely goes out the window at the whim of your hook functions.

- [adds ndjson language support extension by dimitropoulos](https://github.com/Kong/insomnia/pull/4043)

- ## [Could you add the not memory cached datastore option](https://github.com/louischatriot/nedb/issues/63)
  - I'd like to see the not memory cached datastore option, I'd love to store my logs with the same db engine (move them from taffy) without eating all my memory.
- On x86 with gigs of ram you're absolutely right, however I'd like to run in on ARM with only 128 MB of memory where other services run besides node.
- That makes sense then. I didn't think NeDB would be used in that kind of setup, that's cool :)
  - Coding an entire mode where the all DB operations are done from disk would take quite some time
  - However, in your setup where you only want to store logs that you will later query with a full NeDB, you don't need all NeDB functionalities on the ARM so you could use the persistNewState method of the Persistence object which you can find in lib/persistence.js
- I created a small utility that uses nedb's persistence to insert document in NeDB-readable datafiles without putting the database in memory.
- https://github.com/louischatriot/nedb-logger
  - a logger that writes object and JSON messages to a datafile readable by NeDB, with minimal RAM footprint since it doesn't keep a cache of the database in memory.
  - Use it when your application doesn't need to use the database capabilities of NeDB, just the logging ones. You can then use NeDB to query and modify your database

- ## [Added pluggable storage](https://github.com/louischatriot/nedb/pull/427)
- This PR introduces a new option "storage" for Datastore and also for Persistence. 
  - This allows to create a custom storage module (with the same API as the "bundled" storage.js module(s)) and use that as a low-level layer to the file system.
- This makes it possible, for example, to create virtual filesystems for NeDB with very specific properties. 
- For example (taken from a real-world application):
  - in the browser, a custom storage layer for NeDB, that notices changes, can take snapshots and synchronizes with the server at byte level
  - generally, provide a in-memory "file system" for NeDB, for example to temporarily read a datastore that has been received via HTTP, without needing to store it as real files
- This change is also the basis for an experimental two-way, realtime data sync with a server including snapshot capabilities (similar to PouchDB, but with more control over syncing and conflict resolution).

- [Browser version: make storage pluggable](https://github.com/louischatriot/nedb/issues/419)
- The current storage engine already makes use of various storage systems available (via `localforage`), so it is plausible that a user might want to influence the way it works or even implement a completely/different new one.
- The current storage engine is wonderfully simple (something like a virtual file system) and could be replaced by a custom implementation without great effort.

- ## [Is there any way to `close` a datastore? · Issue #244 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/244)
  - So after pending tasks are finished, invoke the close callback and client side can be noticed that the datastore is closed? It's useful when you want to drop or rename the data file without shutting down the server entirely.
- i learned from experience (and confirmed from nedb's author) that multiple nedb instances (running in separate processes) on a single file will corrupt that file.
  - in your password example, if u have a unique constraint for "username" or "email", it will get violated by race-conditions from the multiple nedb instances, @ which point nedb will refuse to load the file and crash

- ## [It looks like we build similar database engine (nedb vs tingodb)_201306](https://github.com/louischatriot/nedb/issues/34)
- tingodb focus on closer compatibility with MongoDB api and its features. One time we already choose wrong solution (it was Alfred DB) and spent significant time to replace it with MongoDB.
- nedb didn't reimplement ObjectID

- I wrote a DB engine(LinvoDB) over NeDB/LevelUP which auto-indexes so that each query can run indexed and avoid scanning.
  - It doesn't load the full datastore in memory, and with large datasets it's faster than NeDB because of full indexing.

- Here is a performance bench comparing NoSQL databases written in pure javascript (finaldb, lowdb, memory, nedb, nosql, pouchdb, tingodb).
  - https://github.com/ezpaarse-project/dbbench /201412/archived
    - A basic benching tool to compare node.js embedded databases

- ## [rxdb: Full Text Search](https://github.com/pubkey/rxdb/issues/259)
- The question is, if it should be baked into rxdb or not. Apart from search-index, there are other really good fuzzy search libraries like fuse.js and lunr.js.
  - https://github.com/doriandrn/rxdb-search
  - They work differently and different use cases. It would be cool, if we have a pluggable interface to write mango queries with the $text operator. This is how mongodb supports fulltext search.

- ## [MongoDB到Nedb的迁移_202106](https://blog.csdn.net/qq_43171049/article/details/117661855)
- 为了实现项目的轻量化，对项目中原本使用的MongoDB进行替换，替换成相似的嵌入式数据库Nedb。
- 由于NeDB没有创建ObjectID的方法，因此引入了bson来实例化ObjectID，且传入数据库中的 _id需转为字符串类型
- nedb 没有全文检索，环境匹配的时候并不能解析原来代码的 $text 操作, 因此在改写成nedb的时候使用普通的查询进行替换
- nedb没有aggregate函数，无法分组，因此需自行编写代码分组，然后通过count进行聚合

- ## [Persist data in BSON on disk · Issue #112 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/112)
- Right now all data persisted on disk is stored in utf8, maybe it can be optional to store it in BSON as this will result in smaller file sizes (but also more computational power to read/write data).
- I'm not sure whether it would make NeDB faster as there is no native BSON codec in the V8 (that I know of). Also, I'm not too worried about file size (storage is cheap and with NeDB's scope it will not be more than ~500 MB) or performance (already plenty fast enough with indexing for the usecases it's designed to handled). 
- I agree with you, introducing BSON will always have a performance overhead. I also agree with you that storage is cheap, however memory is not
  - Though it would be hard to decrease this footprint in memory by using BSON.

- ## [Does NeDB use the disk to do find queries? - Stack Overflow](https://stackoverflow.com/questions/45502484/does-nedb-use-the-disk-to-do-find-queries)
- Depends, if you create indexes on fields, those fields will be held in memory for faster lookup and access. 
- Unindexed field lookups will be hitting disk. 
  - This is true for SQLite, as well as most other persistent databases (e.g PostgreSQL, MySQL, MongoDB, and many more)
- NeDB is an in-memory database, which means that all data will be held in memory (similar to Redis). That being said, you still have to index fields for faster lookup.
- Indexes for NeDB are kept as a Binary Search Tree. At startup, NeDB will load the entire `file.db` into memory, which is why you can still work with the data even if you delete `file.db` .
- NeDB is an in-memory database. It only persist data to disk so that you don't lose it if the process crashes or restarts. That's why it loads the entire `file.db` into memory at startup, and operates purely on the in-memory data structures from then on. 
  - SQLite however only keeps indexes in memory, while the rest of the columns for that row is kept on disk. So if you query for a field that isn't indexed, it will hit the disk.

- ## [Read file as Buffer to mitigate V8's 256MB max string size · Issue #6 · JamesMGreene/nestdb](https://github.com/JamesMGreene/nestdb/issues/6)

- [Over 256Mb datafile throw err upon opening · Issue #389 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/389)

- [how to handle if a db size larger then 256mb? · Issue #363 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/363)
- From what you say switch to MongoDB now. And don't forget to use the 64 bit version of MongoDB, the 32 bit version also comes with memory limitations.

- ## [Multiple node processes support with a single datastore file](https://github.com/louischatriot/nedb/issues/105)
  - I was running two node servers, each on different ports, but both reading and writing to the same persistent datastore file. It looks like each node process is reading its own copy of the doc from the file.
  - For example, node process one creates the first record below, and second node process creates the second record. 
  - The dump of the data file contains both record, but each process can only read one that has been created by itself.
- 👉🏻 One thing you should keep in mind though is that NeDB keeps a copy of the database in RAM, 
  - so is not suited for large applications where you have more than 1M records, If that's your case you should go with mongodb

- Someone else talked about simply copying the updated db file periodically - which would be fine if there were a mechanism to schedule a copy of the db file at a point it's guaranteed to be consistent (e.g. when all updates have been written and none are pending).
  - You'd also need a way to tell the query processes to re-read the file of course - and you'd lose any performance benefits from the query processes working from an in-memory copy - which may be considerable.
  - I'm talking myself into MongoDB here aren't I?
- I think so :) When you arrive at this level of requirements you definitely want a full-blown database solution !
- Yeah - if for no other reason than the moment you start thinking about 'scaling' you really have to consider that you'll probably want your processes to run not just 'multi threaded' but as multiple completely separate processes - perhaps on completely separate machines in different places entirely!!
  - I bit of testing I did using Express did show that using Node Cluster would offer considerable improvement in the load a single server could manage in query terms tho - so I still think there's room to consider a mechanism (if one doesn't already exist) to enable 'safe' copying and updating of the db file any NEDB app is using (e.g. force write and callback - force read and callback)???

- It seems to me that NeDB supports "no concurrency" across multiple processes, since each process gets its own copy of the database and there is no way I could discover to sync the view two processes have of the database.
- Javascript is inherently single-threaded so you're right in that it's "no concurrency" really.
  - Understand, tho, that almost all DBMS's perform CRUD as a single-threaded-task (it's almost impossible to consider any other option) - it's only queries where you have some freedom to multi-thread (with the proviso that maintaining a consistent view of the data can be expensive)
  - Actual cases of people with high-query-traffic databases which are also high-CRUD-traffic are very, very scarce(缺乏的；稀少的) tho - hence my suggesting ways of sharing the db file to enable queries/copy-over updates once the queries are done...
- Recently I struggled with this problem and came up with a solution that is similar to nedb-party but a bit more robust: vangelov/nedb-multi, hope it helps someone.
  - https://github.com/vangelov/nedb-multi

- ## [How is writing and reading at the same time handled?](https://github.com/louischatriot/nedb/issues/99)
- It is not possible. Only workaround is to create dedicated process responsible for database, and talk to it from other processes.
  - NEDB is loading at startup whole dataset from file into memory, and works on this in-memory representation of data. 
  - So if you will load the same data on two different computers, on each computer NEDB will make local copy of that data and both instances couldn't possibly stay in sync with each other.
  - Workaround I was talking about is essentially to make very primitive server. So you have one extra process whose only task is to handle the NEDB, so you have only one dataset to which every other process is writing and reading from. This way your data are always in sync.
  - I can't tell you any further stuff, because I have never done something like this. Just know this is possible.
- there is no built-in method to do it and keeping 2 databases in sync is not an easy problem. Maybe what you would need is to create a simple http server around nedb to have only one central database (reachable by network).
- So, the solution is to build up a network layer on nedb.. just like leveldb.
- My only two comments are that if you're curious about sharing data directly between processes, NeDB is probably not for you. 
  - I'd also add that you shouldn't really be reading the datafile directly, it's meant for NeDB, not for easy access to your data. 
  - As I see it, no one reads MySQL or mongo databases without MySQL or mongo, so why would I to try to read/manipulate and NeDB datafile without an NeDB instance? 
  - I'd say that if you'd like to compare the contents of two NeDB data stores, then load them both into memory using NeDB. Compare them programatically using the NeDB API.
- I assume from your question that you are trying to access the same db from two distinct processes. In that case the only clean way I see of doing so is to set up an http server as a third process and query it from any number of processes you want, read only or not. Pretty much what mongodb does. 

- ## [Two processes sharing datastorefile · Issue #222 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/222)
- If you need to share state between processes I would suggest looking into using something like Redis. 
  - Matt Ranney did a great talk a while back on Voxer's architecture. In it he outlines how they use Redis to bridge processes. Here's a link if you're interested => http://youtube.com/watch?v=pa8utCw7zmY
- Note that you could create an HTTP API over NeDB, much as what MongoDB does, and thus share state without affecting performance, I even begun this work but stopped since it's very easy so I didn't see a point in me doing it. But if you need this you probably want to directly use Mongo Redis or whatever DB that suits your needs.

- ## [can multiple processes write to same db?](https://github.com/louischatriot/nedb/issues/479)
- the answer is no, you should never access the same nedb instance from multiple processes. Typically it would not work, as the first process will get a lock on writing to the data file.

- ## [Batch insert help · Issue #62 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/62)
- I'm trying to insert about 2000+ records(directory listing) at once
  - The following code works for arrays with 20 records or so. 
  - My application crashes at what seems like a threshold.
- If I'm correct, you tried that in a browser environment ? (Node Webkit counts as one). If that's the case, this is a browser limitation, where you can't fire too many functions at once (which is exactly what `async.each` does). You should try to `use async.eachSeries` which does the same thing but sequentially, not in parallel.

- ## [atomic update + insert? · Issue #398 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/398)
- I've been trying to figure out how to orchestrate an atomic update + insert. My situation is that I'm adding a bunch of documents, while also updating a reference in an existing document to include the new documents.

- unfortunately there is no way to guarantee atomicity or use transactions with NeDB, and I am not planning on adding that. 
  - For the vast majority of projects using NeDB this is not an issue but if this is crucial to your project I suggest you use a full-blown DB such as Mongo or Postgres

- ## [Memory usage seems unexpectedly high (RAM usage is 10x disk usage) · Issue #472 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/472)
- We are facing high memory usage when a collection reaches thousands of documents.

- When loaded, the collection is fully kept in memory as "real" JavaScript objects, not strings.
- Indices are holding the entire document in memory rather than a reference to the data on disk. This means no matter what storage driver is being used your entire dataset is going to be in memory the minute you create a single index.

- 👉🏻 By default, a persistent NeDB datafile's format is ndjson (newline-delimited JSON). 
  - However, the moment you add a custom `afterSerialization` and `beforeDeserialization` hook functions, that default format completely goes out the window at the whim of your hook functions.

- ## [boosting nedb performance in big databases](https://github.com/louischatriot/nedb/issues/583)
- with every operation (CRUD), nedb tries to read from the database or write to database file. i think its not necessary, we can do some refines in nedb structure to be super powerful in heavy databases.

- I disagree. NedB is a drop-in replacement for MongoDB, which does and behaves exactly the way you want to convert NedB.
  - NedB is meant to be simple, not only in functionality, but behavior, and it's simplicity is the sole reason I'm using it for as much as I do. 
  - Making NedB memory-based will instantly require and consume more of the server, you make NedB faster, but at the cost of needing more resources (RAM).

- ## [Data persistentance question? · Issue #503 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/503)
- isn't nedb not stored as JSON?  an object per each line
  - AFAIK* it's stored as JSONL
  - http://jsonlines.org/
- Not sure I understand all of this, but do bear in mind the RAM memory implications.
  - NeDB loads the whole opened DB to RAM, so if your DB is 30 MB, it occupies 30 MB of RAM.
  - BUT, If your app opens 30 MB of data (for serialising), then copies the 30 MB of data into NeDB, then just for a moment there you might need 30 (open) + 30 (copy) + 30 (NeDB) = at least 90 MB of RAM for this operation.

- ## [Location of datafile? · Issue #531 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/531)
- I just figured out that when using some bundling tools like webpack, its default target is browser, which means the nedb will use IndexedDB instead (see browser-specific/lib/storage.js below for details).
  - The browser field tells webpack to use browser-specific version of storage.js instead, which will not create any files.
  - The solution is to change the target to, in my case, electron-main in webpack.config.js.

- ## [README misleading when comparing to SQLite · Issue #265 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/265)
- NeDB doesn't support concurrent connections out of the box indeed, but it is crash safe (at least designed to be, still investigating the recent bug report).
- As of v1.4.1, NeDB will always force OS to physically write data to disk whenever a compaction or database load happens, so that you can never lose the whole database in case of a machine crash. 
  - It doesn't flush on every append for performance reasons, but potential data loss in that case is very limited, a few docs at most. That's what major databases do.
  - Note that fsync doesn't work on Windows. Not sure whether that's an issue with my machine or you simply can't fsync on Windows. 
- All major databases sync after each transaction - which, with autocommit, is after each document. 
  - This is the part in SQLite explaining this
  - A similar option is in MySQL/PostgreSQL/CouchDB
- I finished rewriting the crash safe write function, mimicing how Redis AOF basically works
- There is no real consistency in the RDBMS sense as NeDB doesn't implement transactions, foreign keys, constraints and so on ... 
  - Integrity is guaranteed by the append-only, one-line-per-operation format of the datafile. 
  - Any corrupt line is discarded, which can be the case if there is a power loss during an append, but that can only affect the end of the file so that's the same as losing latest data.
  - 👉🏻 Also there cannot indeed be any rollback, since the datafile is replaced only after a successful write.
- Durability is not enforced on every write, only during compaction since a power loss at that moment can result in 100% data loss.
  - For all appends to the datafile durability is the responsibility of the OS, which usually syncs to the disk every 30 seconds so you cannot lose more than 30 seconds of data. That's what most databases do (they do provide an option to force sync on every wrtie though, nedb doesn't).

- ## [It is possibile do operations (find, update, etc..) in synchronous mode?](https://github.com/louischatriot/nedb/issues/445)
- When using memory-only mode, synchronous operations will be very useful, for example, if using NeDB as storage provider for redux. Also, when working in memory-only mode, there is no requirement to perform async operations, due there is not any read I/O
- I would say it is more a result of his design goal to have a consistent API regardless of what backing store is being used (in-memory, localStorage, IndexedDB, Node.js file system, etc.).

- ## [Nedb Encryption & Decryption](https://gist.github.com/bllohar/28ee29b3304d8bf6dbc11d1b16b00130)
- Note that I don't process any JSON because there's really no need to since `afterSerialization` takes a string and `beforeDeserialization` returns a string.
  - [Database encryption with NeDB](https://gist.github.com/jordanbtucker/e9dde26b372048cf2cbe85a6aa9618de)

- ## [Deprecate NeDB in favour of another embedded db(acebase)](https://github.com/Ylianst/MeshCentral/issues/4398)
- Acebase is a current nosql (firebase) compatible embedded database that uses (among other options) sqlite as the backend storage, meaning that (theoretically) the proven performance and reliability of sqlite can be leveraged with mongodb syntax queries.
- In having enabled AceBase and SQLite within the same week, I can tell just how much better and more reliable SQLite is. The airtime is certainly justified.

- ## [nedb: Is this still maintained?](https://github.com/louischatriot/nedb/issues/492)
- TeDB - They're not a 1:1 replacement 
  - but that's actually good because they take a different approach that takes advantage of TypeScript and takes inspiration in other projects like NeDB-core, 
  - for example, they actually require you to use a storage driver, ex. Memory (any), Filesystem (Node. JS), IndexedDB (Browser), AsyncStorage (React Native), etc., 
  - Unfortunately they only provide a storage driver for Electron. 
  - They also have a Filesystem storage driver, but it is labelled as a mock and displaced to the examples folder. 
  - They're probably expecting the community to build the missing drivers, which means you have to pay your share of code before using this project. 
  - This is my preferred choice for new projects if you don't require a 1:1 replacement.
  - Tedb which is mentioned above was made with pure intention to work on electron. Currently using it on Electron 6.0.0 in production. The only storage driver I have written is the tedb electron storage driver. There is also a utils package.
- NestDB - They're missing some of the fixes of NeDB-core but their roadmap shows that they're planning to incorporate them. 
  - This is my preferred choice for new projects if you require a 1:1 replacement.

- PouchDB isn't a self-contained database at all, it's an abstraction layer. 
  - That said, PouchDB can be used on-disk by either embedding a CouchDB instance (super heavyweight solution) or by using a LevelDOWN adapter (default on Node and an acceptable solution)
  - I just think PouchDB is so overly concerned about synchronization/replication across instances and revision control that I feel like their API is much more basic in order to align with the CouchDB protocol vs having their own more expressive API on top of it for the many users who may just want to use it on a single isolated instance like NeDB.

- ## [NeDB, a pure Javascript database for Node.js and Node Webkit_201306](https://news.ycombinator.com/item?id=5912125)
- The trend continues where all things eventually get implemented in Javascript. Waiting for JS.js
- What does this have to do with node-webkit? My understanding is that nodejs is a subset of node-webkit, so by saying "this is for nodejs", you imply "this is for node-webkit".
  - That's true, but I want to stress Node Webkit because NW apps are probably one of the best usecases.
