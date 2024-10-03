---
title: lib-db-sqlite-community
tags: [community, sqlite]
created: 2021-08-30T17:33:26.516Z
modified: 2021-08-30T17:33:46.086Z
---

# lib-db-sqlite-community

# guide

# discuss-stars
- ## 

- ## 

- ## imagine there was a sqlite extension for making KV virtual tables. What features would you expect? 
- https://twitter.com/agarcia_me/status/1690474942285103104
  - ttl/expiry for entries? Multiple keys? Keys besides strings? Subscriptions?

- aren't you describing redis. Basically any feature of redis say yeah sure all the way until you have a pub sub model with channels.

- I’d model it after Redis - both relative TTLs and absolute Unix seconds. 
  - But with SQL, you could also potentially query all (e.g) “keys expiring in the next 5 minutes” + similar table-wide ops that Redis can’t.

- We used to build relational databases on top of kv stores e.g. MySQL using BerkeleyDB and some engines let you specify you want non-key values stored in the index so you don't need to read other files eg Postgres exposing this layer of sqlite could be cool to make smaller files

- why this need “extension”?????
  - How do you guarantee that this cache will stay within a certain memory limit? Redis can guarantee it.
  - SQLite can already provide database level heap limits so with some hacking that could plausibly be extended for a use case like this, I think.
- I'm thinking of table-level size-on-disk or row count limits. Like "make a new KV table that's a max 50MB" or "this KV table has a max 5K rows" or something. enforced with virtual table logic on INSERT/UPDATEs
  - For notions cache we have a row count limit, but need to carefully schedule our delete & LRU time stamp update transactions for low read & update IO times to avoid degrading app performance
- SQLite doesn’t have this kind of hard limit. You can limit max pages, but you’ll need at most 2x the page limit of the DB to VACUUM, and WAL things may go over too
- Yup, mostly to enforce the ttl so you don't have to do it manually. Otherwise `CREATE TABLE kv (key TEXT PRIMARY KEY, value ANY)` is just fine
# discuss-performance
- ## 

- ## 

- ## SQLite is unfortunately too slow in the browser to be used as a reactive database.
- https://twitter.com/swyx/status/1743857432206643589
  - [In-Memory SQLite Perf / Matt | Observable](https://observablehq.com/@tantaman/in-memory-sqlite-perf)
  - Without adding a complicated layer on top which essentially becomes a second database itself. After pat leave I’ll turn this draft into something presentable

# discuss-search
- ## 

- ## 

- ## 

- ## How to do "Hybrid search" with SQLite FTS5 and sqlite-vec
- https://x.com/agarcia_me/status/1841522698373247065
  - Reciprocal rank fusion, FTS-first, re-order by semantics, and more
  - Featuring the great snowflake-arctic-embed-m-v1.5 model and sqlite-lembed, using pure SQL examples.
  - Sample of what this looks like, using RRF: A single SQL SELECT statement, with CTEs performing vector + fts searches, combining the results in the last step.

- Last Sunday, I was trying to make one with llama 3.2 1b  and Duckdb
# discuss
- ## 

- ## 

- ## 

- ## 

- ## fun fact: SQLite is the most deployed and most used database. There are over one trillion (1e12) SQLite databases in active use.
- https://twitter.com/iavins/status/1774464622067679738
  - It is maintained by three people. They don't allow outside contributions.
  - Open-Source, not Open-Contribution
- LibSQL is an interesting fork of SQLite that is both open-source and open-contributions.

- It's part of Chromium as well, used for WebSQL, you can open the corresponding file on disk directly with Sqlite, I use that feature to pass some data from extension to local program

- ## 🔥 [Joining CSV and JSON data with an in-memory SQLite database | Hacker News_202106](https://news.ycombinator.com/item?id=27565482)
- 
- 
- 

- ## 🔥 [There are over one trillion SQLite databases in active use | Hacker News_202112](https://news.ycombinator.com/item?id=29461127)
- 
- 
- 

- ## 🔥 [How to Corrupt a SQLite Database File | Hacker News_202204](https://news.ycombinator.com/item?id=31214131)
- 
- 
- 

- ## 🔥🔥 [How to Corrupt a SQLite Database File | Hacker News_202001](https://news.ycombinator.com/item?id=22098832)
- 
- 
- 

- ## 🔥 [How to Corrupt an SQLite Database File | Hacker News_201310](https://news.ycombinator.com/item?id=6502229)
- 
- 
- 

- ## [Tell HN: SQLite3 does have something like stored procedures | Hacker News](https://news.ycombinator.com/item?id=31913062)
- However, triggers cannot return result rows, and a SELECT query that a view is defined as cannot take parameters (although there is a work-around by using a virtual table which contains a single row whose value is whichever value it is constrained to be). There is also WITH RECURSIVE, which also has many uses.

- ## [ What is the SQLite of nosql databases? | Hacker News](https://news.ycombinator.com/item?id=27490361)
- As others have mentioned you have lots of options: LMDB, LevelDB/RocksDB, BerkeleyDB. 
  - For what it's worth, I spent a long time looking for an embedded key-value store for my current native project since I didn't need the full complexity of SQL. In the end I chose... SQLite.
  - All of these embedded NoSQL databases seem to be missing critical features. 
  - One such feature for my use case is database compaction. 
  - Last I checked, an LMDB database file can never shrink. 
  - Full compaction of LevelDB is slow and complicated (as I understand it essentially breaks the levels optimization which is the whole point of the thing.) 
  - SQLite meanwhile supports fast incremental vacuum(清洁；真空), and it can be triggered manually or automatically.
  - SQLite just has everything. Plus the reliability is unmatched. 
  - Even if you just need a single table that maps blob keys to blob values, I would still recommend SQLite over any NoSQL database today.

- The SQLite of NoSQL is still SQLite: https://www.sqlite.org/json1.html

- Filesystem. Linux has VFS cache which is very robust and efficient.
  - Remember that it is typical for programs to read /etc/nsswitch.conf, /etc/resolve.conf and tons of others at startup time - the filesystem is the datasource in Unix tradition, so the machinery is very well optimized.
- SQLite has a backend which is well suited as a key-value store.
  - Here is a NoSql database based on the SQLite backend
  - https://github.com/symisc/unqlite /202205/clang
    - UnQLite is an embedded NoSQL (Key/Value store and Document-store) database engine.

- ## Is there a good way to use SQLite with serverless?
- https://twitter.com/makon_dev/status/1630635156716306443
- Depends on what you mean by "serverless." 😅 @flydotio could be called serverless in the sense that you don't have to manage servers. In any case, to use SQLite you need a persistent volume, or you could use a service like @ChiselStrike :)
- Chiselstrike is SQLite over WASM with HTTP client (so you don’t need a TCP pipe or access to process aka Node; works in edge /serverless/workers)
  - LolaDB is an HTTP client that pulls all your db clients on a centralized server infra & wraps the calls into a unified interface 
  - Prisma Data Proxy gives you a prisma:// protocol connection. Should work on serverless HTTP as well … haven’t tested it

- ## [SQLite: QEMU All over Again? | Hacker News_202210](https://news.ycombinator.com/item?id=33081159)
- Just a note that LiteFS isn't a distributed filesystem; despite the name, it's not a filesystem at all, but rather just a filesystem proxy. 
  - It does essentially the same thing that the VFS layer in SQLite itself does, but it does it with a FUSE filesystem, so you don't have to change SQLite's configuration in your application.
  - As for the "distributed" part of it: LiteFS has a single-writer multi-reader architecture; it's the same strategy you'd use to scale out Postgres.
- I'm curious about how such a strategy deals with applications that update a value and then read the updated value back to the user, since there might be a replication delay between the write (that goes to the master) and the read (that comes from the closest replica). Do you make optimistic updates on the client or do you club (write-then-read) operations into a transaction?
  - LiteFS author here. It depends on the application. You can check the replication position on the replicas and simply wait until the replica catches up. That requires maintaining that position on the client though.
  - An easier approach that works for a lot of apps is to simply have the client read from the primary for a period of time (e.g. 5 seconds) after they issue a write. That's easy to implement with a cookie and it's typically "good enough" consistency for many read-heavy applications.
  - This is an application (and frequently data type) dependent decision. Some data is safe to return on acceptance, others need to wait for acknowledged writes. The most naive solution is to just make all writes slow but acknowledged.

- Note that SQLite transactions are also fundamentally single writer, multiple reader (isolation level serializized with snapshot isolation and no work-forking).
  - So if you want to make SQLite distributed you will have to end up with not just a single writable replicate but a global write log on transaction level. Which is very very bad for performance for many use cases. (E.g. in PostgreSQL if you use serialized & snapshot transaction isolation it's "forking the world" for parallel write transactions and if multiple transactions have no overlap they can complete in parallel without a problem (in parallel but on the same single write enabled replica). This is good enough for quite a bunch of applications and can still have a decent throughput).
  - As far as I can tell many use-cases which could profit from a distributed SQLite would not really like a per-transaction global lock but would be okay with something like what Postgres does. Through there are always some exceptions.
