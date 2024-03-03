---
title: lib-db-app-community-storage
tags: [community, database, storage]
created: 2023-09-17T17:35:57.181Z
modified: 2023-09-17T17:36:36.118Z
---

# lib-db-app-community-storage

# guide

# discuss-stars
- ## 

- ## 

- ## Databases have tables and indexes stored in files. 
- https://twitter.com/hnasr/status/1725905694111498532
  - As you create rows, the database system writes to data pages in memory which is then written to data files on disk. 
  - But what happens when the db crashes while writing to the file?
  - [What happens when databases crash?](https://medium.com/@hnasr/what-happens-when-databases-crash-74540fd97ea9)

- ## 🤔 How do major SQL databases store data? (not indexes)
- https://twitter.com/eatonphil/status/1721536449881796685
  - Postgres: only unorganized heap files
  - SQLite & MySQL: only organized btrees
  - SQL Server & Oracle: unorganized heap files or organized btrees

# discuss-filesystem
- ## 

- ## 

- ## [What "filetype" is a database? : learnprogramming_202209](https://www.reddit.com/r/learnprogramming/comments/xhqlk7/what_filetype_is_a_database/)
- the important thing to note is that a database isn't a file, it's a program. Now obviously the program will write the contents to disk somehow so that the data isn't lost when the computer restarts, but that's an implementation detail of the database and should never be interacted with directly. For example, you would never try to read/write a .doc file but instead always use Microsoft Word to interact with it since that is their special format and not intended for direct consumption.

- A database doesn't have a filetype, because it's not a file. It's a program that stores records, and can fetch and update them faster than writing anything to a file. 

- ## [Ash HN: What if we use file system as database? | Hacker News](https://news.ycombinator.com/item?id=37777463)
- The main reason is that I can use a variety of tools to view and manipulate files.
  - But other software can also mess with your "database", including the operating system itself. For example, Syncthing was breaking my static site by changing the unicode normalisation of file names. MacOS being case insensitive brought issues. Illegal filename characters brought issues.
  - This approach works well if you want to make data accessible to humans, but it's wildly inefficient if you expect machines to operate on that data, and comes with a few caveats(告诫，警告).

- This chapter from "Database design" by Adrienne Watt has a very good explanation why this approach didn't stick

- For simple apps and app components, it's very convenient and manageable.
  - It becomes a problem when you: (1) scale up (2) have to deal with multiple relationships between objects. 
  - The "Database design" by Adrienne Watt posted in another comment covers the scale concerns well, but another scale problem she doesn't mention is hitting inode limit, at least if you're on a single machine. 
  - You can of course use a distributed filesystem as database, but at that point, you might want to use a database proper.

- Why not, is because you want ACID guarantees (ie, what if two people are editing a file at once), ability to scale, or a query language.
  - That all can be achieved by using file system as database. Not even complicated to implement. 
  - See couchDB for how to handle "what if two people are editing a file at once".
- You're not getting that just from the file system though. Depending on the performance requirements and use case it may or may not be complicated. You are going down the rabbit hole of creating your own foundation for a database at that point.

- ## 🔥 [Database as Filesystem [video] | Hacker News_201907](https://news.ycombinator.com/item?id=20394088)
- 
- 

- ## 🔥 [Ask HN: Is Hackernews still using the file system as database? | Hacker News_201705](https://news.ycombinator.com/item?id=14371189)
- 
- 

- ## 🤔🔥 [Why use a database instead of just saving your data to disk? | Hacker News_201305](https://news.ycombinator.com/item?id=5733935)
- here's some good reasons, your OS doesn't want you to store tons of small pieces of data in many different files.
  1. Your FS has a minimum blocksize, often somewhere around 4k, you'll waste disk space with small files
  2. Your FS has a minimum blocksize, often somewhere around 4k, you'll waste disk space with small files
  3. Reading/writing data from files directly requires syscalls, a DB can cache a lot in memory and minimize syscalls.
  4. Atomic transactions are hard, even with a database. Are you actually sure you know how fsync works? 
  5. Distributed operation is hard, take a look at a databases like couchbase, elasticsearch or S3, where data is replicated across machines and datacenters in a highly reliable way
  6. Consistent backups on a live app are hard. Using postgres or another MVCC DB? Just perform a dump, it will be a true snapshot.
  7. Do you need to coordinate writes across multiple app instances (E.G. every web-app ever), you'll have to figure out your own record locking system. 

- Well here's one good reason: If your data cannot all fit in memory at once, you cannot simply serialize and deserialize it from disk. You will have to create some kind of indexed solution involving reading and writing to files piecemeal and by doing so you'll have created an impromptu database by default.

- I recently did experiments with storing documents (blobs) with UUIDs as files. I stored documents within a hierarchy of a few levels of directories to avoid having too many files in a single directory (UUID abcdefg was stored as a/b/c/d/abcdefg). Performance was surprisingly low. Reading documents resulted in a lot of disk seeks. Also it seems that directory entries lookup is a O(n) operation in a standard ext4. 
  - I also did experiments with simple databases like GDBM. The effect was also disappointing. 
  - In the end I started to really appreciate RDBMSes design and all theory that is behind them. 
  - Creating a highly performant system using I/O operations is HARD.

- 👉🏻 Depends entirely on what you're doing. 
  - If you're just saving large sets of data to the disk, and doing nothing else with them, then yeah, don't use a DB. 
  - If you're running lots of random queries on piece-mail parts of several dozen sets of those files, then use a DB.
  - There's a reason it's called SQL: Structured Query Language. If you're interrogating the data, you want SQL (or something like it). If you're just loading stuff / saving stuff to disk, like a Word file, and not performing any sort of random search or query on it, then yeah, using a DB doesn't make sense.
- This was my first reaction, as well. This goes especially for large datasets. If you are making linear passes over very large databases, I don't think I see much advantage in using a DB beyond possible benefits of shared storage.

- The same reason you divide your programs into functions, classes, etc. A well-designed database can change as the data you store needs to change. You also get a nice abstraction for accessing/querying data (e.g. relational algebra/SQL) that is well-studied and widely applicable.

- 🧐 Worth noting that Hacker News is a "store it all in files" design.
  - Files on disk mean you can use all your great UNIX tooling to do all sorts of complex operations that would take you many many hours of skilled development to do with a database. Then there are all the possible things you could do with Git or (imagine!) ZFS! Versioning everything for free? Keep an activity log within a hierarchy. 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## I deleted a few TBs of data from s3, cost me $270 to **delete** data
- https://twitter.com/boristane/status/1764018341327286549
  - according to cost explorer it's the DeleteObject operation
- Oh it’s probably cause you’re using glacier and doing early deletes. From S3 standard they’re always free.
  - That's probably it "Objects that are archived to S3 Glacier (...) are charged for a minimum storage duration of 90 days(...)Objects deleted prior to the minimum storage duration incur a pro-rated charge equal to the storage charge for the remaining days."
  - Same for "S3 Standard-IA" but 30 days. It's a bit of a scam they leave this in a finer print while recommending to use "Intelligent-Tiering" everywhere.

- Many people dont realize S3 is paid by API call. Also the sane reason opening your S3 up to public access is crazy. Put CloudFront infront of it and save 70%.
  - And glacier has a 90 day minimum

- ## 🛢️🌰 How Cassandra handles writes?
- https://twitter.com/thegeeknarrator/status/1763903178393694467
- Accept write requests
- save it to an in-memory write-back cache called memtable. 
  - Serve reads faster, no disk access required. 
- Append to a Commitlog (WAL)
  - Durability. 
  - If Cassandra crashes before flushing the memtable to disk, it restores acked writes by replaying the Commitlog.
- When the memtable is flushed to disk as an SSTable (an immutable file), Commitlog entries that have been persisted can be eliminated. 

- ## ⌛️ What was life like with PostgreSQL prior to the 7.1 release in 2001 which added a WAL?
- https://twitter.com/MarkCallaghanDB/status/1761086709859864849
  - Was it like life with MyISAM, as in crashes often meant restore from backup and/or loss of recent commits?
  - For MyISAM I heard stories too -- run myisamchk each night after crashes. 
  - Did PG even have pgchk back then (pre 7.1) to do the same? But I already am snarky about MyISAM. I am just trying to figure out if I can also be snarky about early PG.

- I remember hearing how ALTER TABLE needed 24 hrs to complete

- I don't remember the times per node. I do remember the estimated time to roll out a change over the tier for popular tables. Online Schema Change (OSC) was a game changer.

- it seems Postgres really took off after 9.5/9.6 and the transition to the annual numbering system from 10 onwards. I don’t have much experience before that, and it’s quite shocking to find people still happily running 9.6 because 10 looked like a brand new version and they got cold feet about upgrading

- Having started out a Full-History database may have helped here a little. Up to v 6.2 PostgreSQL had tmin and tmax system fields and SQL syntax for each table to specify at which point in time you wanted to see it. So everything was still there, which probably helped a lot

- > "To maintain database consistency in case of an operating system crash, previous releases of PostgreSQL have forced all data modifications to disk before each transaction commit." /v7.1-docs
- If you have M pages to write back and a crash occurs after N pages were written (N < M) then what happens? I am still trying to figure out whether it was a problem.
  - SQLite has a solution for that, but it comes at a cost (write pages elsewhere first, fsync, then update pages in place). 
  - InnoDB has doublewrite buffer which is similar, but exists for a different reason (torn page protection). 
  - What did old PG do?
- PostgreSQL didn't have autovacuum back then (introduced in v7.4) so most transaction operations were write-only. And I assume transactions were marked committed only after syncing all other data. Crashed transactions would presumably be nothing more than dead tuples in the table.

- f a transaction made 5 heap pages dirty and a crash happens after the first 3 were written to disk, what was done on recovery? There are more complicated scenarios, but I want to start with an easy one.
  - Postgres doesn’t overwrite data ) except in some catalog cases) so the unfinished transaction would appear to have rolled back.
- My comments above are about overwriting disk pages which is required to make a transaction durable -- and which should be all or nothing. I am asking whether PG was crash safe WRT that prior to 7.1.
  - Hmm. The heap table AM was essentially write-only except tuple header metadata fields, so that should be consistent. I'm not 100% sure about indexes though; I suspect that would've had some additional special handling to flush btree pages around splits, so that no data is lost.
- I think the answer is that if it wrote N < M whole pages, that's fine, because the CLOG doesn't say that the relevant transaction committed yet (see my other answer about two flushes).  But if it wrote half a page you could get in trouble (CF InnoDB's double writes, and PG's FPW)
  - That is the detail I needed. I still have much to learn about PG and clearly I don't know much about the CLOG.

- FYI, the `clog` was renamed to `pg_xact` in version 10.

- I'm sure I remember Postgres 6.4 was very solid, but it was pretty slow. That's why MySQL got traction on the web, it was fast as long as you didn't mind a bit of data loss.

- ## 看 OrioleDB 的博客，早些年磁盘 IOPS 是瓶颈，数据库的算法和数据结构都是围绕降低 IOPS 设计的，不太考虑 CPU，
- https://twitter.com/liumengxinfly/status/1747577046883287331
  - 现在 IOPS 上来了之前的很多设计就不合理了，又要回来优化 CPU 的利用率，降低各种锁的开销
  - [Rethinking buffer mapping for modern hardware architectures_202301](https://www.orioledata.com/blog/buffer-management/)

- ## Direct IO can easily be misunderstood: Is it required for database durability?
- https://twitter.com/jorandirkgreef/status/1724950847035941074
  - The crux of the problem is that DBMS's do need to distinguish between volatile data (kernel page cache) and durable data when they externalize transaction commitments to users.
  - It's hard to do that (at least correctly) if the DBMS is only able to read from the kernel page cache, i.e. if the DBMS has no way to read directly from the disk itself.
  - Granted, there's still the disk's own cache to consider, which Direct IO alone doesn't address (you can fsync the fd when you call open to address this—a FoundationDB trick, which inspired the same for @TigerBeetleDB )... but Direct IO is a vital(极重要的，必不可少的) building block in designing a DBMS for durability.
  - To be clear, the non-intuitive thing about DBMS durability is that it’s often surprisingly as much as how you read() from the disk, for example, when recovering from the WAL at startup, as how you write() to the disk and call fsync.

- looks like `fsync` flushes both the kernel page cache and the disk cache from the man page doc
  - Yes, exactly. Direct IO bypasses the kernel page cache, but you still need `fsync` to flush writes from the disk cache all the way to durable disk.
- It also ensures that the write is flushed from the various queues. Queues at the OS level like the staging queue and the hardware dispatch queue. And the submission queue between OS and the SSD.
- Enterprise grade SSDs have Power Loss Protection (PLP). Effectively a bunch of capacitors having sufficient charge for tens of milliseconds to flush the content from the cache (DRAM) to the NAND based flash. The fsync to the drive can effectively be a noop.

- ## [Soft deletion probably isn't worth it | Hacker News_202207](https://news.ycombinator.com/item?id=32156009)
- I've been a software dev since the 90s and at this point, I've learned to basically do things like audit trails and soft deletion by default, unless there's some reason not to.
  - Somebody always wants to undelete something, or examine it to see why it was deleted, or see who changed something, or blah blah blah. It helps the business, it helps you as developer by giving you debug information as well as helping you to cover your ass when you are blamed for some data loss bug that was really user error.
  - **Soft deletion has obvious drawbacks but is usually far less work than implementing equivalent functionality out-of-stream**, with verbose logging or some such.
  - Retrofitting your app and adding soft deletion and audit trails after the fact is usually an order of magnitude more work. Can always add it pre-launch and leave it turned off.
- If performance is a concern, this is usually something that can be mitigated. You can e.g. have a reaper(收割者；收获者) job that runs daily and hard-deletes everything that was soft-deleted more than n days ago, or whatever.

- Views are a simple solution to this problem. Pretty much all moderns RDBMSs support **updatable views**, so creating views over your tables with a simple WHERE deleted_at IS NULL solves the majority of the author's problems, including (IIRC) foreign key issues, assuming the deletes are done appropriately.
  - I feel like a lot of developers underutilize the capabilities of the massively advanced database engines they code against. Sure, concerns about splitting logic between the DB and app layers are valid, but there are fairly well developed techniques for keeping DB and app states, logic and schemas aligned via migrations and partitioning and whatnot.

- Cascaded deletes scare me anyway. It only takes one idiot to implement UPSERT as DELETE+INSERT because it seems easier, and child data is lost. You could always use triggers to cascade you soft-delete flags as an alternative method, though that would be less efficient (and more likely to be buggy) than the built-in solution that cascaded deletes are.
- If you look at how system-versioned (or “temporal”) tables are implemented in some DBMSs, that is a good compromise. The history table is your audit, containing all old versions of rows even deleted ones, and the base table can be really deleted from, so you don't need views or other abstractions away from the base data to avoid accidentally resurrecting data. You

- 
- 
- 
- 
- 
- 
