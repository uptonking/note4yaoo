---
title: lib-db-app-community-event-oplog
tags: [append-only-log, community, database, events, oplog]
created: 2023-09-17T18:16:50.624Z
modified: 2023-11-01T10:08:09.232Z
---

# lib-db-app-community-event-oplog

# guide

# discuss-stars
- ## 

- ## Don’t stack your Log on my Log
- https://twitter.com/eatonphil/status/1762920320585879627
- Related: LSM without WHL (2022)
  - Interesting as an LSM trees uses ... a log; the WHL required for recovery requires... a log. Can we just drop one ? It seems that the answer is yes. Just Looking into it.
- You build a replicated database for MySQL (or postgres) on top of RocksDB on top of Raft on top of a filesystem on top of ssds How many logs do you have?
  - Physiological Log describes metadata operations carried out at that layer. And the definition of metadata changes at each layer - dbms, fs and flash.
- I'm struggling to see how realize that uni-log - these pieces of software are perched on top of one another - application(user-space) <- DBMS(user) <- FS (kernel) <- Device Driver (kernel) .

- Doesn’t this put a lot of questions on time series databases and their long term performance on SSDs?

- ## Learnt the hard way, append everything and deduplicate later is substantially cheaper than merge
- https://twitter.com/mim_djo/status/1754364525003055380
- ClickHouse has that approach. Append then reorganise asynchronously.
- If that were the case why doesn’t a merge just do this under the hood?
  - Not all data has a natural timestamp order
- in my current universe, 98% of the data is from vendor APIs with no timestamps. some do. but with most, don't have any other option but snapshot and dedupe
- Also importantly, deduping can be done during downtime.

- ## 🆚️ [Damn Cool Algorithms: Log structured storage (2009) | Hacker News_201705](https://news.ycombinator.com/item?id=14447727)
- In the 8 years since this was written, Log-Structured Merge Trees have basically "won". 
  - BigTable, AppEngine, LevelDB, Cassandra, HBase, MongoDB, and several others are all built around them.
- There's a powerful hardware trend driving this, namely that disk capacities and write bandwidth are still increasing rapidly, but **seek times have basically plateaued(达到稳定时期；进入停滞状态)**. 
  - 👉🏻 That means that data structures that rely on append-only operations can continue to scale to take advantage of bigger disks, 
  - but **data structures that rely on disk seeks (eg. B-trees) have hit a bottleneck**. 
  - Also, as number of cores continues to increase, playback & processing from a sequential log can often be parallelized, but updating your on-disk indexes blocks on I/O.
- what will replace this once enterprise SSDs start replacing spinning disks?
  - SSDs have even more unique access patterns - they give you (relatively) fast seek times, there's no particular penalty for random-access vs. sequential usage, but you really want to avoid writes, both to preserve the lifetime of the drive and because mixing reads & writes with a SSD lowers performance.
  - I don't see SSDs replacing mechanical disks. Rather, they're being used for different functions. Disks are becoming a data warehouse; they're the new tape(磁带)
  - Operational serving is moving toward SSDs and RAM, with a periodic processing step that pulls data off disks and builds a pre-made shard that gets written all at once to the SSD. 
  - LSM trees are well-adapted to the data-warehousing part of this, which is why you continue to see big uptake of BigTable/Cassandra/Mongo.
- random access has a penalty compared to sequential access. the unique characteristic would be that SSDs have more channels*banks than e.g. RAM, which has similar characteristics regarding access patterns.
- SSDs don't have seek times at all as there is no actuator arm and read/write head to "seek" into place in order to read/write data.
  - the fact that SSDs do not have seek times is an important distinction when discussing storage engines. You might want to read the following by Jay Kreps one of the authors of Kafka, Voldermort and Samza

- there is already a lot of thought that goes into LSM trees on flash storage - check out RocksDB for example, which goes to great lengths to allow the user to deal with Read/Write amplification(放大或增强), a problem specific to flash storage. So I don't think that more SSD adoption will fundamentally change anything.
- 🆚️ The tradeoff from LSM tree to B-tree, very generally speaking, is more about access patterns: 
  - LSM trees lend themselves to insert-heavy workloads because the structure is conceptually just a big array that you very quickly append stuff to the end of without checking the rest of the array. 
  - That's the magic of why it's so fast for insertions - there's no overhead. 
  - You just ignore the older key/values. 
  - When doing a read, you read backwards from the end, reading only the newest values. 
  - When you fill your memory budget, you flush your array to a lower layer, removing the duplicate old values. 
- Another point is that oftentimes these data structures span storage layers (or the "cache hierarchy" as database systems people like calling it) - e.g. you could have an LSM tree that has a top layer fitting in L3, then a bunch more in memory, then the majority of it spilling over to disk. 
  - Another example is the Bw-Tree, which introduces a mapping table that is a storage-agnostic lookup table that tells you wherever a record is, disk or memory or otherwise, and is smart about paging stuff in and out of memory based on hotness.

- My layman's guess is something that combines the two. larger immutable storage using B-Tree's (or similar), and more live data using log structured stuff. With semi-regular promotion of data from log to b-tree and eventual clean-up of data no longer referencable in the b-tree.

- event sourcing seems like a very powerful pattern that I haven't seen wide adoption. The best documentation seems to be some MS dev library notes and a discussion from M Fowler.
- 🤔 Are there any open source implementations of a database that uses event sourcing?
- I built https://github.com/amark/gun after I was using MongoDB to event source data. The key piece for me was wanting to have Firebase-like realtime sync for my event sourcing.
- I've become a bit of a CouchDB zealot of late for this exact reason... Native support for incrementally updating map-reduce combined with change-feeds makes implementing event sourcing straightforward. 
  - If you wanted to reimplement event sourcing in couch, it can be implemented as a versioned merge in a map-reduce view that takes a sequential ordered events (e.g. ui-event:0000025) and maps those changes into a "versioned" JSON. 
  - This versioned JSON changes leaf values into versioned objects like "fieldValue": { "_val": 34.00, "_ver": 25 } which I call property fields. 
  - This is necessary because CouchDB is a B+Tree implementation and reduce operations are sequential but not contiguous. 
  - The reduce phase merges all events sequentially by choosing property fields with the latest event – making it a CRDT type – and resulting in a single JSON document with the latest fields with "_ver" info for each. 
  - This scheme has a drawback that each event needs to have a unique serially ordered ID to work. Not sure how time stamps would work. I chose the ID based scheme to allow the UI be able to know when a user interaction conflicts (a vector clock between) and let it display the conflict to the user or decide how to merge the knew state.
  - It's not the most efficient but for most moderate sized UI's with a single state tree, it performs fine.
- In addition to the other solutions mentioned, Apache Samza lands somewhere in that neighborhood.
# discuss
- ## 

- ## 

- ## If you like logs and databases and event sourcing stuff, definitely check out this article from @PatHelland .
- https://twitter.com/LewisCTech/status/1762034969243943107
  - This is a really intuitive model of Eventual Consistency
- > From this perspective, the contents of the database hold a caching of the latest record values in the logs. The truth is the log. The database is a cache of a subset of the log. /@PatHelland

- I love the concept of logs as a first class distributed database (or at least the write model)
  - Tbh, this was eye-opening for me and since then influenced how I think about systems and design - and everything else causally related to it 

- https://twitter.com/ifesdjeen/status/1762012801847960047
- Performance retrieval seems like a fundamental need to me.
- if performance is not a concern, then Event Sourcing is fine. Problem is, in real world, performance is a major concern. Don’t get me wrong, I think Event Sourcing is a great concept, but only in theory.
- Goog luck replaying 5 years of events when your new server boots.
  - Not sure if you have worked with event sourcing before, but not every time you have to read all messages. You have consumers that store the position to read from it when server reboots. Also sometimes you have snapshot mechanism to not read the whole stream again.
- Snapshots + log is not just the log.

- You mean the actual WAL vs the b-trees?

- ## I'm looking for a durable (storage-backed) data structure that is a time-indexed log, 
- https://twitter.com/dustingetz/status/1734337596115886146
  - 20 transactions per second, the key is a time bucket and the value is a record. 
  - The log must support efficient lookup by time-bucket as well as O(1) relative scan forward/backward for playback. 
  - File system storage is fine as is rotating files every day if needed. Suggestions?
- what you’re looking for is exactly what time series database does
  - most popular is timescale db and influx db. if you’re familiar with running postgres, i’d say timescale since it runs on top of postgres.

- Apache KvRocks, Or just RocksDb if you don’t need replication

- ## 💡 It's eye opening to me how appending to a log file is seen is basically free, compared to other database operations. 
- https://twitter.com/LewisCTech/status/1733576104773026192
  - At least that's the impression I get reading papers and materials on the subject.
- Appending is the most fundamental file operation.
- There is definitely some "synergy"(协作, 相互作用) here between that being a fundamental file OP and event sourcing.
  - That’s the original append-only @CouchDB architecture, with interleaved(交错) indexes etc.
- I always figured that's what the Changes feed was.
  - Changes is a view over the sparse sequence index. The actual append only file also included ID index, binary doc bodies, and  streamed attachment chunks.
- Inserts are easy, updates are hard. It's the same problem with microservices and workflows. They point to inserts being viable and hand-wave away the problems with modifications
  - But this is roughly why I designed my platform the way I did. To keep the advantages of append-only logs for modifications, you need deterministic consumers. This means no clocks and no race-conditions. The rest followed

- ## What should you do after publishing an event?
- https://twitter.com/ProgressiveCod2/status/1733024610437009741
  - There were two main angles to the discussion:
  - Should we just forget about the event after sending it to the broker and continue processing other events?
  - Or should we worry about getting a confirmation that the event reached its destination?
  - The answer, of course, is a game of trade-offs.
  - By the way, we were using Kafka for that project.
- Kafka provided 3 options we could choose from:
- [1] Fire and Forget
  - we send a message to the broker and forget about it.
  - Kafka is highly-available so there's a pretty solid chance that the messages would be delivered.
  - But you can’t completely rule out lost messages.
- [2] Synchronous Send
  - Kafka does let you send messages synchronously. The Producer basically waits for an acknowledgment in the form of a Future object.
  - If there is an issue, the Producer throws an exception.
- [3] Asynchronous Send
  - Producer sends a message to the broker and registers a callback function. It doesn’t wait and continues processing.
  - The callback gets triggered when the Kafka Broker acknowledges the message or there's an error.
- We evaluated what we wanted for a particular type of event based on the business scenario.
- Asynchronous send is a mix of high performance and handling exceptions.
  - It was ideal for business-critical events in a production scenario.
- Synchronous Send sounds safe, but results in poor performance because it creates a blocking thread.
  - We avoided this approach completely.
- Fire and Forget is best for performance and throughput.
  - This makes it suitable for cases where message delivery is not critical.
  - We used it only for logging and some user-tracking events that weren’t super-important.

- Fire and forget is a special case of asynchronous send approach where the producer doesn't care about the acknowledgment or error.

- For a queue based message broadcasting system(say DB to client stream) fire and forget is how things work (For instance firestore) Any reason for that? Correct me if I’m wrong
  - You are correct. There are lot of good reasons for using fire and forget:
  - it's best for low latency and throughput
  - loosely coupled
  - generally more resilient

- If messages aren't being consumed, you'll see lag and should have an alert on your Kafka lag

- ## ❌ One JSON file per application log event. 
- https://twitter.com/gunnarmorling/status/1727586416413077924
  - It's this kind of inefficiencies which make me think that our industry probably could do with 1/10th of the compute resources, when designing systems just a bit more carefully.
- You or I would see these JSON docs as records in a (streaming) database, or as (remote) method arguments in (persistent) memory. But when all you have is a hammer… and that hammer is a (pretty good) distributed file system., this is what happens.

- Seen this a few times. Kafka sink to S3, IoT, event sourcing, etc as a raw backup.

- Easy to see how you end up with this design. It makes the producer side very simple, just a stateless call to the AWS API per event. And it scales well for large message sizes.

- Me, I would process and ingest all those within AWS in any convenient database. Then, even reexport in a more suitable format . Sure it will take time, but a few speeding tricks and some patience should do it especially since the bulk of the work is only done once.

- ## 今日 Rust 小震撼: 把 logstash 换成 vector 之后内存用量从 7G 降至不到 200M
- https://twitter.com/electroniclunar/status/1722457277305950556
- logstash是ruby+java，内存大也正常。不过logstash的管道过滤和fanout 还是挺好用的。
- 用 loggie（golang）也是 200M

- 以前写过中心日志处理器，绝大部分内存都用来保障 at-least-once 的缓存。而且因为一些特殊原因不能用 MQ，只能靠服务器硬抗。 如果有 MQ，内存要多小都行。

- ## [Is ORM still an anti-pattern? | Hacker News_202306](https://news.ycombinator.com/item?id=36497613)
- Materialized views are almost criminally underused. I feel most people don't know about or understand them. 
  - They can be a very effective "caching layer" for one thing. 
  - I have used them to great effect.
  - A lot of times I see people pulling things out of the database and caching them in Redis. 
  - When in fact a materialized view would accomplish the same thing with less effort.
- They are great if the frequency of changes isn't very high and the underlying tables are read-heavy and running it directly against the tables would be expensive (e.g. complex joins).
- Typically Redis is used in medium to high volume of many smallish but repetitive queries where you want to store some key bits of information (not entire records at which point going to database might be simpler) that are sought often and you don't want to hit the database again and again for them - a bit different from the materialized view scenario.

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

- ## 🛋️ [The database I wish I had | Lobsters_202008](https://lobste.rs/s/m9vkg4/database_i_wish_i_had)
- Well, I took the author at their word: “Being immutable means that only new information is added, no in-place update ever happens, and nothing is ever deleted.”
  - What you’re describing is what I’d call append-only or log-based. That’s how CouchDB’s and Couchbase Server’s databases work. It has the downside of lots of write amplification, since all the live data gets rewritten every time you compact.
  - On devices with limited storage, append-only has the worse problem that you can’t free up any storage unless you have enough free space to copy all the live data first. Which basically means it’s dangerous to fill up more than half of your storage, unless you carefully keep track of how much live data you have. 
- In fact, git itself implements this internally with “packfiles”, which is an internal binary format to represent diffs efficiently regarding storage. However every bit of data is still there, the “compaction” is transparent to the user.
  - Having snapshots is an possibility, but this would be better if left to the application to do, if the database could expose the snapshot and build more data on top of it, and let the application delete old data when convenient.

- The sync protocol, and conflict handling, are IMHO a lot more interesting problems than the implementation of the local DB. 
  - Take a look at Dat and Scuttlebutt … neither is perfect, but they have interesting designs. (And they make good use of append-only data structures at the sharing/protocol level.)
  - For a lower level approach to syncing, the CouchDB replication protocol, at a very high level, is a decent design. We still use the same architecture in Couchbase Lite, although the details of the protocol are completely different because sending zillions of HTTP requests is too expensive.

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
