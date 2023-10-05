---
title: lib-db-app-community-oplog
tags: [append-only-log, community, database, oplog]
created: 2023-09-17T18:16:50.624Z
modified: 2023-09-17T18:17:13.008Z
---

# lib-db-app-community-oplog

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Is ORM still an anti-pattern? | Hacker News_202306](https://news.ycombinator.com/item?id=36497613)
- Materialized views are almost criminally underused. I feel most people don't know about or understand them. 
  - They can be a very effective "caching layer" for one thing. 
  - I have used them to great effect.
  - A lot of times I see people pulling things out of the database and caching them in Redis. 
  - When in fact a materialized view would accomplish the same thing with less effort.
- They are great if the frequency of changes isn't very high and the underlying tables are read-heavy and running it directly against the tables would be expensive (e.g. complex joins).
- Typically Redis is used in medium to high volume of many smallish but repetitive queries where you want to store some key bits of information (not entire records at which point going to database might be simpler) that are sought often and you don't want to hit the database again and again for them - a bit different from the materialized view scenario.

- ## [Damn Cool Algorithms: Log structured storage (2009) | Hacker News_201705](https://news.ycombinator.com/item?id=14447727)
- In the 8 years since this was written, Log-Structured Merge Trees have basically "won". 
  - BigTable, AppEngine, LevelDB, Cassandra, HBase, MongoDB, and several others are all built around them.
- There's a powerful hardware trend driving this, namely that disk capacities and write bandwidth are still increasing rapidly, but **seek times have basically plateaued(达到稳定时期；进入停滞状态)**. 
  - 👉🏻 That means that data structures that rely on append-only operations can continue to scale to take advantage of bigger disks, 
  - but **data structures that rely on disk seeks (eg. B-trees) have hit a bottleneck**. 
  - Also, as number of cores continues to increase, playback & processing from a sequential log can often be parallelized, but updating your on-disk indexes blocks on I/O.

- there is already a lot of thought that goes into LSM trees on flash storage - check out RocksDB for example, which goes to great lengths to allow the user to deal with Read / Write amplification, a problem specific to flash storage. 

- The tradeoff from LSM tree to B-tree, very generally speaking, is more about access patterns: 
  - LSM trees lend themselves to insert-heavy workloads because the structure is conceptually just a big array that you very quickly append stuff to the end of without checking the rest of the array. 
  - That's the magic of why it's so fast for insertions - there's no overhead. 
  - You just ignore the older key/values. 
  - When doing a read, you read backwards from the end, reading only the newest values. When you fill your memory budget, you flush your array to a lower layer, removing the duplicate old values. 

- Another point is that oftentimes these data structures span storage layers (or the "cache hierarchy" as database systems people like calling it) - e.g. you could have an LSM tree that has a top layer fitting in L3, then a bunch more in memory, then the majority of it spilling over to disk. 
  - Another example is the Bw-Tree, which introduces a mapping table that is a storage-agnostic lookup table that tells you wherever a record is, disk or memory or otherwise, and is smart about paging stuff in and out of memory based on hotness.

- Slightly related perhaps and something I have been curious about for a while... event sourcing seems like a very powerful pattern that I haven't seen wide adoption. The best documentation seems to be some MS dev library notes and a discussion from M Fowler.
- 🤔 Are there any open source implementations of a database that uses event sourcing?
- I built https://github.com/amark/gun after I was using MongoDB to event source data. The key piece for me was wanting to have Firebase-like realtime sync for my event sourcing.
- I've become a bit of a CouchDB zealot of late for this exact reason... Native support for incrementally updating map-reduce combined with change-feeds makes implementing event sourcing straightforward. 
  - If you wanted to reimplement event sourcing in couch, it can be implemented as a versioned merge in a map-reduce view that takes a sequential ordered events (e.g. ui-event:0000025) and maps those changes into a "versioned" JSON. This versioned JSON changes leaf values into versioned objects like "fieldValue": { "_val": 34.00, "_ver": 25 } which I call property fields. This is necessary because CouchDB is a B+Tree implementation and reduce operations are sequential but not contiguous. The reduce phase merges all events sequentially by choosing property fields with the latest event – making it a CRDT type – and resulting in a single JSON document with the latest fields with "_ver" info for each. This scheme has a drawback that each event needs to have a unique serially ordered ID to work. Not sure how time stamps would work. I chose the ID based scheme to allow the UI be able to know when a user interaction conflicts (a vector clock between) and let it display the conflict to the user or decide how to merge the knew state.

- ## Write-ahead logging is a standard way to ensure data integrity and reliability. 
- https://twitter.com/arpit_bhayani/status/1508665078929047552
  - Any changes made on the database are first logged in an append-only file called write-ahead Log or Commit Log. 
  - Then the actual blocks having the data (row, document) on the disk are updated
  - An operation like Update Query, Delete Query is logged in the commit log and not the actual changes making the write lightning-fast.
  - WAL also takes care of its data integrity by writing a CRC-32 before logging the operation. This CRC is checked during reading and replicating

- Advantages of using WAL
  - we can skip flushing the data to the disk on every update
  - significantly reduce the number of disk writes
  - we can recover the data in case of a data loss
  - we can have point-in-time snapshots

- A write-ahead log is the append-only source of truth in a database; each transaction appends events to it before table files are updated. Change data capture (which Marta is referring to) lets you retrieve and consume changes from that log. 

- ## [I've been developing high performance databases for the last five years | Hacker News](https://news.ycombinator.com/item?id=8979043)
- It's tough to beat MVCC for a database that wants isolated concurrent transactions. 
  - **Append only designs seem attractive, but they don't actually help much with write throughput on SSDs** (but avoiding in-place updates does, due to erase blocks.) 
  - And they often require writing much more information. E.g. writing 100 bytes in LMDB, which is an append only btree, requires copying all pages from the root to the leaf and writing them all out, typically 64k or more. 
  - Writing 100 bytes to a transaction log or WAL costs about 100 bytes. There's a huge write amplification going on.

- ## [A way to do atomic writes | Hacker News](https://news.ycombinator.com/item?id=20040779)
- Appending log based file system has a lot of appeals. A lot of hard problems, like atomic write, become trivial. A log based FS shares similar properties as the transaction log in RDBMS, making consistency and recovery easy. Write performance is fantastic. With enough cache memory, read performance should be good, too. The only down-size is the performance hit when doing garbage collection. 
  - Totally agree. Log based file system makes things much easier, such as atomic write, data consistency and failure recovery. Along with COW semantics, transaction isolation also becomes easier. By its append-only writing nature, file versioning is trivial as well. Garbage collection is performance downside indeed, but it can be mitigated by COW switching and delayed bulk collection IMHO. Overall, the cost is worthwhile and that is what I am currently doing in ZboxFS

- I think elements of that generationality are the foundations of the Log Structured Merge Trees used by KV Stores like LevelDB and RocksDB. Atleast I think that's the same concept, I'm not well read on filesystems.
- Yes, LSMT is a good example of pushing the idea of a hybrid append log and in memory data structure further.
- However, LSMT is for relatively smaller data set, i.e. ordered key-value. It has worse write amplification than a simple append log. There're 2~3 writes per change.
  - Also it doesn't offer help to address the frequent update block problem. All versions of a data change are written to disk. A merge is needed to get rid of the old versions.
  - But it has a number of good implementation ideas that can be borrowed.

- ## 🤔 [Immutable Data (2015) | Hacker News](https://news.ycombinator.com/item?id=36470739)
- Author here, 8 years on. Although the advantages are real, I can't say I have had much opportunity to implement schemas like this. The extra complexity is usually what gets in the way, and it can add difficulty to migrations.
  - I think it would be useful in certain scenarios, for specific parts of an application. Usually where the history is relevant to the user. I think using it more generally could be helped by some theoretical tooling for common patterns and data migrations.
- You can use Datomic for instance or SirixDB on which I'm working in my spare time.
  - The idea is an indexed append-only log-structure and to use a functional tree structure (sharing unchanged nodes between revisions) plus a novel algorithm to balance incremental and full dumps of database pages using a sliding window instead.

- 👉🏻 I agree this is **more of an application level concern than a database thing**. If you need to maintain a history for the user requirement then you will naturally land on a scheme like this.
- We also have help from other quarters nowadays.
- Databases often provide a time travel feature where we can query `AS OF` a certain date.
- Some people went down the whole event sourcing/CQRS/Kafka route where there is an immutable audit log of updates.
- Data warehousing has moved on such that we can implement “slowly changing data” there.
- All in all, complicating our application logic, migrations and GDPR in order to maintain history in line of business applications might not be worthwhile.

- Suppose that instead of a typical User table, you have a User_Revision table like suggested. If this information gets leaked, the user is exposed to more vectors of attack.
  - GDPR and the right to having your personal data deleted certainly puts a bit of a stopper on using an immutable database for anything personally identifying.

- I'll argue that this is bad design. It works as long as the amount of data is small, but even then taking a low-data scenario and building lots of views or triggers just seems a bit weird. 

- ## [Speaking of B-trees, I find CouchDB's implementation really interesting | Hacker News](https://news.ycombinator.com/item?id=7522724)
- Speaking of B-trees, I find CouchDB's implementation really interesting: the backing file is append-only, meaning that modifying the tree implies appending the modified nodes at the end of the file (for example, if I change a leaf, than I rewrite it at the end of the file, and rewrite its parent so that it points to the leaf's new position, and so on until we reach the root node).
  - Sounds like a waste of space, but it solves a bunch of problems, like being crash-proof (since we never overwrite anything, it's always possible to just find the last root) and allowing reads concurrent with a write without any synchronizing necessary. Plus, it's actually optimized for SSD's due to its log-like structure!

- Massive waste of space though. LMDB is also copy-on-write and crash-proof but doesn't require compaction like CouchDB does

- ## [Building a Distributed Log from Scratch, Part 1: Storage Mechanics | Hacker News](https://news.ycombinator.com/item?id=15983185)
- [Building a Distributed Log from Scratch, Part 1: Storage Mechanics – Brave New Geek](https://bravenewgeek.com/building-a-distributed-log-from-scratch-part-1-storage-mechanics/)

- I have to admit that I only recently got familiar with logs. 
  - I was designing a B+Tree in Python for fun and was struggling to make it survive crashes: a single insertion in a tree often results in multiple page writes which is not atomic.
  - The solution to this problem is simple and elegant with a **Write-Ahead Log**. Every page write is appended to the log and only merged back into the tree file when it's sure that the log is safely written to storage.

- If you're interested in those, there are at least two other designs you should have a look at:
  - couchdb uses a single file for each db, which means the write ahead log _is_ the storage. The atomicity is guaranteed by saying that the latest root is the valid root. If writes are interrupted, everything since the last root is invalid and discarded upon restart. A simple design that just works, although it tends to be wasteful and requires frequent compactions
  - lmdb uses copy on write to make sure space is properly used, and atomicity is provided by sharing only the strict minimal pieces of information, so small in fact atomicity is guaranteed by the os.

- ## [The database I wish I had](https://www.reddit.com/r/programming/comments/ijwz5b/the_database_i_wish_i_had/)
- technically PouchDB is also append-only, but its history tracking isn't as elaborate as git.
  - PouchDB's _rev field is a common pitfall for new people when starting with it.
  - I was trying to use those _revs for revision control myself, and I had to watch her say it a few times in order to convince myself to stop doing it

- ## The real-time syncing immutable, append-only log that hypercore provides can also be accessed randomly, 
- https://news.ycombinator.com/item?id=15468295
  - allowing for lots of cool parallel/distributed log processing architectures (**Kappa architecture**), similar to Kafka (which is also based on immutable, append-only logs). 
  - We have just focused on syncing a filesystem at first because we had a strong use case there, but **you could totally build a CRDT on top of an append only log**.

- ## I need a general term for a data structure that contains all its past revisions. Examples:
- https://twitter.com/gritzko/status/1156782170041700352
  - Immutable tree (like in git)
  - Weave (like in SCCS.. BitKeeper)
  - Append-only log (like everywhere)

- ## When explaining @apachekafka , most articles first discuss topics, then partitions. 
- https://twitter.com/gunnarmorling/status/1413401342840819714
  - I feel it's more intuitive to do it the other way around: first introduce partitions as the implementation of the append-only log concept, then topics as logical groups of partitions.
- I think it depends. From an RDBMS background, I found topics a much more natural parallel to ~= tables, and then getting into it from there. I agree about partitions being the natural entry point from the purely append-only log concept though
- Partitions are the building blocks that developers write code to, how Kafka scale, how it provides durability (hello replicas), and how it is administered. This became so clear to me when I was writing the bucket priority pattern

- ## Reflecting on the fact that I've built some flavor of the "immutable, append-only log + materialized views" pattern into every non-trivial software project I've built since 2006.
- https://twitter.com/neil_conway/status/994717227621347329
- Similar here, but not the same: My projects have always involved materialized views, not always append-only, and always with transparent rewrite.
- This is exactly what we do with our IoT commit logs. Let’s face it, once something is digitised, the world needs to accept that it can never be removed; it can only really become inaccessible.
