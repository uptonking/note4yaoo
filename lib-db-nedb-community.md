---
title: lib-db-nedb-community
tags: [community, database, nedb]
created: 2022-12-11T22:38:02.682Z
modified: 2022-12-11T22:38:34.694Z
---

# lib-db-nedb-community

# guide
- [node database comparisons](https://github.com/only-cliches/Nano-SQL/issues/48)
  - 比较db: nanoSQL, nedb, lokijs, LoveField, pouchdb, alaSQL
  - 比较项目: node/browser, dbms, undo/redo, events, indexeddb, orm, typescript

- 参考sqlite是如何解决并发读写的问题的
# discuss
- ## 

- ## 

- ## 

- ## [Confusing about option upsert when update](https://github.com/louischatriot/nedb/issues/495)
- db.insert will generate unique _id for each item, but when use db.update with upsert option, all _id is the same, So, next time when you open database file, only one record will left. 
  - 👉🏻 each update request is added a new line with an identical id, when the database is reloaded, it will purge itself by removing all old arrays (Keeping the last one). This is done for performance reasons.

- ## [Listen to database changes](https://github.com/louischatriot/nedb/issues/175)
- You could manually couple your database operations with custom events, e.g.:

```JS
db.insert([{ a: 5 }, { b: 42 }], function(err, newDocs) {
  eventEmitter.emit('insert', newDocs);
});
```

- here is my idea for such an API, loosely based on Meteor's `Mongo.Cursor#observe` callbacks... because I really hate the PouchDB API for it. 

- [Inserted, updated and removed events](https://github.com/louischatriot/nedb/pull/156)

- ## [Case insensitive sorting?](https://github.com/louischatriot/nedb/issues/580)
- i just ran into this need as well--i think a sort callback would be a great way to solve this 
  - but since i don't think that's going to happen i'm going to solve for my project by denormalizing a document property just for sorting, e.g. saving the `toLowerCase()` version in a separate property
- there is also the `compareStrings` option to Datastore, but it's global to the Datastore (that may be fine for your use case, though!)
  - compareStrings: (a, b) => { return a.toLowerCase().localeCompare(b.toLowerCase()); }, 
  - NeDB seems to not use `compareStrings` when comparison operators such as `$lt` and `$gt` are used.

- ## [Unicode support for .sort and .find · Issue #150](https://github.com/louischatriot/nedb/issues/150)
- It's not really an issue of internationalization, rather than the way strings are compared in JS. 
- Thinking about it I think the best and simplest way is to do as MongoDB did, i.e. not code any special locale-aware sorting and let the user create his own sorting key. 

- ## [how well would this work with 10M documents?](https://github.com/louischatriot/nedb/issues/476)
- This is not the right project. When you `ensureIndex` a field on a datastore you are going to store the entire dataset in memory. 
  - This means you'll likely end up using more RAM than you would diskspace for your datastore. 
  - Unless you just don't index your data or manage your own indices and hold a reference to the _id. 
  - But really this project does some funny things with the way it indexes document.

- ## [High memory usage, because indices hold entire document](https://github.com/louischatriot/nedb/issues/506)
  - I noticed that you are storing the entire document in the index rather than referencing to the data on the disk(or other storage APIs). 
  - This seems incredibly memory expensive, because one would assume the index would just hold the value being indexed(as the key) and a reference to the document(as the value), rather than the value being the entire document.
  - This limits your database size by the amount of memory you have(or are willing to dedicate to your database).
- Why not just have the storage driver be a KV store, and use the key as a reference to the document which would be stored as the value(as JSON)? 
  - I don't see this being a huge performance impact, as the OS should be caching the file.

- We've replaced NeDB with our own fork of LinvoDB3
  - LinvoDB3: We're using Google's LevelDB as a backend.
  - The DB is not fully in memory, and we've acceptable performances. We've also added support for mongoose via a driver

- ## [Loading time is too long](https://github.com/louischatriot/nedb/issues/600)
- Are you using any indexes? If so that is why. NeDB has to re-index every collection on load.

- ## [added support for Buffers (BLOB)](https://github.com/louischatriot/nedb/pull/167)
- Thanks for the PR, unfortunately I'll not merge it as I think buffers don't have their place in nedb. 
  - There is already a quite simple way to store a BLOB, and that is to serialize it (as your code does in hex format). 
  - Also, buffers are Node only and don't work in node webkit or the browser, so code would need hard to maintain internal forks for something ze already have a good workaround for.

- ## [fixing races in 2 test cases](https://github.com/louischatriot/nedb/pull/610)
- I noticed that the function ensureIndex is not sync (as stated in the comment) and some operations may races with the assertions. 

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

- ## [foundryvtt: Database architecture upgrades](https://github.com/foundryvtt/foundryvtt/issues/5065)

### NeDB

> The nedb package provides a pure JS file-system storage with a variety of convenience operations for performing certain queries and updates.

#### Pros

- Writes human readable data that can be parsed by JSON (almost)
- Pure JavaScript with minimal dependencies
- Fast read operations because `_id` field is designed to use a BST
- Supports a query syntax for operating on records conditional on their current values

#### Cons

- No longer maintained, some security issues.
- 👉🏻 Current design of embedded documents is inefficient for large parent documents (like Scenes).
- API is outdated and callback-based without support for Promises.
- Write operations are not as fast as they could be with other options
- Human readable `.db` files may encourage dangerous behavior by users who attempt to edit them directly

### LevelDB

> LevelDB is a Google-developed key-value storage database written in C++. Node.js and Electron bindings are available via `classic-level` which builds upon `abstract-level` to implement the LevelDB bindings. [Level/classic-level](https://github.com/Level/classic-level)
>  

#### Pros

- Fast write operations using low-level C++ bindings
- Simple and easy API which natively supports async Promises
- Well maintained by a group of multiple active contributors ([opencollective.com/level](https://opencollective.com/level))
- Potential to be very well suited for our parent/child document format using the built-in concept of sublevels

>  

#### Cons

- Data written in binary format that is not human readable
- Can only look up records in the database by ID. To find records containing a certain value iteration will be required.

>  

### TeDB

> A package designed as something of a `nedb` successor, this DB engine written in TypeScript has many of the same methods and interfaces that NEDB did. It does not, however, provide file-system storage as a built-in feature and would require development of a custom storage driver to optimally write and read data to and from disk.
>  

#### Pros

- Potentially most directly compatible with existing NEDB approach

>  

#### Cons

- Does not provide a file-system storage driver which means this option cannot be readily tested.

>  

### LowDB

> A simple local JSON database. Use native JavaScript API to query. Written in TypeScript. ([typicode/lowdb](https://github.com/typicode/lowdb))
>  

#### Pros

- Very lightweight in terms of dependencies
- Simple API which natively supports async Promises.

>  

#### Cons

- Too simple, lacks an indexed approach for fast data retrieval
- Very poor performance compared to other options
- Frequent issues with permission failures
- No guarantee of atomic transactions or other form of concurrency control

- ## [It looks like we build similar database engine (nedb vs tingodb)_201306](https://github.com/louischatriot/nedb/issues/34)
- tingodb: we focus on closer compatibility with MongoDB api and its features. One time we already choose wrong solution (it was Alfred DB) and spent significant time to replace it with MongoDB.

- nedb didn't reimplement ObjectID

- tingodb: We do not keep all data in memory because we want to process relatively big datasets. The cost for this is that full table scan (non indexed query) known to be slow. But with real database you should already learn that full scan is always slow and you should avoid it.
  - MongoDB uses memory mapping and fully rely to OS chaching. We can't, our work around it is partial cache. It is useful to at least to avoid double data load when doing query and getting actual data. The problem with partial cache is keeping it within allowed size. Best known solution is LRU and we tried corresponding module, but found it SLOW due to complex expiration logic. We choose the simple but fastest option which is direct mapped cache though it is not 100% effective (if you allow it max size to 1000 it doesn't mean that it will fit real 1000 elements.
- You can quickly mimics nedb behaviour in tingodb by making simple unlimited cache by replacing `tcache.js` content
  - Probably we can provide option to choose not only size but cache strategy as well. Different apps might have different demands.
- What we know on practice that we can replace mongodb to tingodb on middle level apps almost without performance penalty. We don't shut for more. I'd rather more concerned on better functionality level compatibility.
- tingodb: Our goal is to mimic MongoDB in its behaviour, this is challenging. 
  - This not only more complex queries that should work the same way, but another very interesting behaviours.
  - For example cursor provided by mongo db is "final", i.e. it contains data available on time when you did query. 
  - 👉🏻 Nothing special except that we not want to bind full data copy to cursor and there is some architectural that forces us to use different indexes approach and some other stuff.
- In short NedDB is in memory db first but with optional filesystem persistance. 
  - TingoDB is file system first but with memory cache
- As a quick proof just run benchmark test on nedb with "-m" key (memory only) and without. Results will be the same
- NeDB is fast because it keeps ALL data in memory, which means that DB can't be larger than physical memory 
  - Also, benchmark is TOO simplistic, it uses document with single field with sequential access, this is mostly JOKE

- I wrote a DB engine(LinvoDB) over NeDB/LevelUP which auto-indexes so that each query can run indexed and avoid scanning.
  - It doesn't load the full datastore in memory, and with large datasets it's faster than NeDB because of full indexing.
  - Finally, we also did some benchmarking during implementation, and found that it has a tendency to degrade fast. For example, lets assume objects scan and search for attribute in nested object.

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

- ## [error on loading data in NeDB](https://github.com/louischatriot/nedb/issues/540)
- Although NeDB does do its updates in append mode, it also does a full datafile rewrite at the end of the initial loading process and during every compaction operation. If your total record size, when represented as a string, exceeds 256MB, then it will fail as Node.js/V8/JS does not support that large of a string.

- [Stream files line by line when parsing to avoid memory limits](https://github.com/louischatriot/nedb/pull/463)

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

- ## [Unable to load, when the database file is too large](https://github.com/louischatriot/nedb/issues/457)
- Auto-compaction every once in a while or, if the data set is actually above 256Mb, use another DB. 
  - NeDB use `Buffer` to load file from disk to memory and its limit for most systems is 256Mb.

- ## [Read file as Buffer to mitigate V8's 256MB max string size · Issue #6 · JamesMGreene/nestdb](https://github.com/JamesMGreene/nestdb/issues/6)

- ## [Over 256Mb datafile throw err upon opening · Issue #389 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/389)
- As I can see (but I am pretty much newbie in Node) there is a problem in Buffer.js during DB loading and trying to convert all file from Buffer to String in one go. Since one String can't be longer than kMaxLength in V8.
- As I understood from googling, there is no way to open over256Mb JSON file in node in one go: only streaming by line and parsing into JSON.

- [how to handle if a db size larger then 256mb? · Issue #363 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/363)
- From what you say switch to MongoDB now. And don't forget to use the 64 bit version of MongoDB, the 32 bit version also comes with memory limitations.

- ## [Multiple node processes support with a single datastore file](https://github.com/louischatriot/nedb/issues/105)
  - I was running two node servers, each on different ports, but both reading and writing to the same persistent datastore file. It looks like each node process is reading its own copy of the doc from the file.
  - For example, node process one creates the first record below, and second node process creates the second record. 
  - The dump of the data file contains both record, but each process can only read one that has been created by itself.

- I began working on this louischatriot/nedb-server which basically an Express server around a single NeDB instance, allowing concurrent access by different processes. Didn't have the time to finish and not sure when I will find it but this is pretty simple, just a REST wrapper. If anyone wants to take the project and finish it I'll be happy to review a PR !
- I'm new to Express (and, indeed, Node as a server thing - I use it in bundled WebAPPs mostly) but isn't that approach still 'single threaded' for all requests made the the Express 'server'?
  - You could multi-thread it using something like Cluster Node but then you'd run the risk of conflicting CRUD requests (one thread deletes a record whilst another is updating it - leaving it undeleted and updated or updated and then deleted at-random).
  - When I think about it - the best solution would be to have 2 separate DB files - a read-only one which is accessed by a multi-threaded query 'server' and the writable one which is access by a single-threaded CRUD server - but I've no idea how practical that is - how we'd tell NEDB to write the file/copy the file and re-read the file on-demand!?
- Did you think about combining http://elasticsearch.org and MongoDB? Using that together would give you extremely fast queries on a large amount of data via ElasticSearch while MongoDB keeps responsible for concurrent CRUD ops.

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

- I don't think you'd ever consider multiple CRUD processes but the concept of having a process to perform updates and a separate process returning queries would be quite useful I think?
  - I have a Node game backend where I really need separate CRUD and Query processes because a single-threaded CRUD process is fine (and indeed has considerable integrity benefits) but a single-threaded query process couldn't cope with the likely demand...

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

- So, the solution is to build up a network layer on nedb.. just like leveldb.

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

- ## [atomic update + insert?](https://github.com/louischatriot/nedb/issues/398)
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

- ## [Alternative backends/persistence layers](https://github.com/louischatriot/nedb/issues/179)
- Do you think it is possible to fully separate persistence and "query engine"? If yes how?
  - I was thinking about this issue as well, but couldn't find any sensible solution. The only thing I could think of is to have query engine + cache, and in case of cache-miss enumerate through all stored documents and test the query on them. Then indeed you can have storage engine abstracted into separate layer. It only has to feed you with the stream of documents to test your queries against.

- 👉🏻 It is possible assuming each query is indexed. Basically what I propose is that indexes are built for every query on demand by iterating through all docs in storage and adding them to the indexes.
  - Then, on each query, we only have to get the Ids of the matched documents only via the indexes and then retrieve the docs with those Ids from the storage engine.

- I'm still not fully comfortable with the idea of indexes, but aren't both of us talking about something like this?
  - Yes, essentially we are talking about the same thing. However, if the query is not entirely indexed, you'll have to iterate through all documents in the persistence layer on every query, which would introduce a great overhead compared to doing the same operation on documents in memory.

- Right now persistence and query are indeed separated in NeDB, and in theory you could switch persistence layers (almost) easily. That's what is used to create the browser version which doesn't have persistence (I never had the time to create the persistence engine for it).
  - Now if you want to persist to disk and not load the entire DB in memory, I think you'll need to tie query and persistence together, or as @lvshti says use entirely indexed queries.
- IMO, if you want to use levelDB as a backend, you'll be better off using MongoDB since the use case was to have a pure JS DB. If you want to code persistence and on disk DB using JS I'd very happy about it, I've been meaning to do it for a long time :) But that seems like a lot of work.

- May I present my understanding of how the whole design should look like and please tell me why this is naive or sub-optimal?
- Database engine with replaceable persistence layer should consist of 3 separate parts:
  - query engine - you just give to it pattern and the document, and it returns true/false
  - indexes - binary trees which are storing only key for the document, not a whole document
  - persistence - key-value store of any kind you like (in-memory, on-disk + in-memory cache, or fully on-disk)
- In action it would look something like this:
Startup:
- Iterate through all documents in persistence and create indexes which have been specified
Find:
- check if any index apply, and if so get narrowed list of keys from it
- get from persistence documents corresponding to all those keys (or go through all keys if no index apply)
- run query engine on each document from step 2 to get the final list of documents

- ## [Data persistence question?](https://github.com/louischatriot/nedb/issues/503)
- isn't nedb not stored as JSON?  an object per each line
  - AFAIK* it's stored as JSONL
  - http://jsonlines.org/
- Not sure I understand all of this, but do bear in mind the RAM memory implications.
  - NeDB loads the whole opened DB to RAM, so if your DB is 30 MB, it occupies 30 MB of RAM.
  - BUT, If your app opens 30 MB of data (for serialising), then copies the 30 MB of data into NeDB, then just for a moment there you might need 30 (open) + 30 (copy) + 30 (NeDB) = at least 90 MB of RAM for this operation.

- ## [Location of datafile?](https://github.com/louischatriot/nedb/issues/531)
- I just figured out that when using some bundling tools like webpack, its default target is browser, which means the nedb will use IndexedDB instead (see browser-specific/lib/storage.js below for details).
  - The browser field tells webpack to use browser-specific version of storage.js instead, which will not create any files.
  - The solution is to change the target to, in my case, electron-main in webpack.config.js.

- Nedb let's you create a new auto-loading Datastore using this call: `db = new Datastore({ filename: 'path/to/datafile', autoload: true });`
  - It appears, however, that this command is only accurate when performed from the main process (for new Electron developers, this is usually your main.ts or main.js file).
  - If you perform the Datastore creation command from a class which is executed in the renderer process (any class which is executed in the BrowserWindow), nedb ignores the datafile you provided and creates your database in IndexedDB instead. 
  - You'll find your database in your application's "userData" directory in a subdirectory \IndexedDB\http....leveldb. 
  - In my case it was (on Linux):`\home\myUser\.config\myAppName\IndexedDB\http_localhost_4200.indexeddb.leveldb`
  - ~/.config/google-chrome/Default/IndexedDB/
- If you really want nedb to create and use the database file that you provide during Datastore creation, you must create AND access the data file (add, remove, ... documents) from the main process
  - Creating the data file from the main process (in main.ts)
  - Putting the db variable in a global variable in the main process (in main.ts)
  - Accessing the global db variable from the renderer process by calling the global db variable
  - `db = remote.getGlobal('collectionDb');`

- ## [README misleading when comparing to SQLite · Issue #265 · louischatriot/nedb](https://github.com/louischatriot/nedb/issues/265)
- NeDB doesn't support concurrent connections out of the box indeed, but it is crash safe (at least designed to be, still investigating the recent bug report).
- As of v1.4.1, NeDB will always force OS to physically write data to disk whenever a compaction or database load happens, so that you can never lose the whole database in case of a machine crash. 
  - It doesn't flush on every append for performance reasons, but potential data loss in that case is very limited, a few docs at most. That's what major databases do.
  - Note that fsync doesn't work on Windows. Not sure whether that's an issue with my machine or you simply can't fsync on Windows. 
- 👉🏻 All major databases sync after each transaction - which, with autocommit, is after each document. 
  - This is the part in SQLite explaining this
  - A similar option is in MySQL/PostgreSQL/CouchDB
- I finished rewriting the crash safe write function, mimicing how Redis AOF basically works
- upon reload, always use the contents of the datafile except in the (pathological) case where datafile doesn't exist but temp datafile does, which cannot be done by nedb (the user needs to do it manually, at which point we can assume he's trying to crash nedb on purpose !).
- 👉🏻 There is no real consistency in the RDBMS sense as NeDB doesn't implement transactions, foreign keys, constraints and so on ... 
  - Integrity is guaranteed by the append-only, one-line-per-operation format of the datafile. 
  - Any corrupt line is discarded, which can be the case if there is a power loss during an append, but that can only affect the end of the file so that's the same as losing latest data.
  - 👉🏻 Also there cannot indeed be any rollback, since the datafile is replaced only after a successful write.
- Durability is not enforced on every write, only during compaction since a power loss at that moment can result in 100% data loss.
  - For all appends to the datafile durability is the responsibility of the OS, which usually syncs to the disk every 30 seconds so you cannot lose more than 30 seconds of data. 
  - That's what most databases do (they do provide an option to force sync on every write though, nedb doesn't).

- this code doesn't work on Windows, as it seems that Windows's counterpart to `fsync` , `FlushFileBuffers` cannot be called on directories. 
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
