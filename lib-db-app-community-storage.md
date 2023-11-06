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

- ## 

- ## 🤔 How do major SQL databases store data? (not indexes)
- https://twitter.com/eatonphil/status/1721536449881796685
  - Postgres: only unorganized heap files
  - SQLite & MySQL: only organized btrees
  - SQL Server & Oracle: unorganized heap files or organized btrees

# discuss-filesystem
- ## 

- ## [Ash HN: What if we use file system as database? | Hacker News](https://news.ycombinator.com/item?id=37777463)
- The main reason is that I can use a variety of tools to view and manipulate files.
  - But other software can also mess with your "database", including the operating system itself. For example, Syncthing was breaking my static site by changing the unicode normalisation of file names. MacOS being case insensitive brought issues. Illegal filename characters brought issues.
  - This approach works well if you want to make data accessible to humans, but it's wildly inefficient if you expect machines to operate on that data, and comes with a few caveats(告诫，警告).

- This chapter from "Database design" by Adrienne Watt has a very good explanation why this approach didn't stick

- For simple apps and app components, it's very convenient and manageable.
  - It becomes a problem when you: (1) scale up (2) have to deal with multiple relationships between objects. 
  - The "Database design" by Adrienne Watt posted in another comment covers the scale concerns well, but another scale problem she doesn't mention is hitting inode limit, at least if you're on a single machine. 
  - You can of course use a distributed filesystem as database, but at that point, you might want to use a database proper.

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
