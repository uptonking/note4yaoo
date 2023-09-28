---
title: lib-db-sqlite-community
tags: [community, sqlite]
created: 2021-08-30T17:33:26.516Z
modified: 2021-08-30T17:33:46.086Z
---

# lib-db-sqlite-community

# guide

# discuss
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

- ## I used to think forking sqlite (e.g., @libsqlhq ) was crazy but I'm on board now. 
- https://twitter.com/tantaman/status/1684917032096030722
  - While SQLite is great, I just don't think it is ready for the demands of the coming years.
- What do you mean specifically? The weak update hook?
  1. weak update hook / subscriptions 
  2. lack of write concurrency 
  3. lack of pluggable storage engines (eg custom btree rather than vfs or vtab)
  4. limited types
  5. lack of tiered storage
  - Now abandoned SQLite 4 had fixed 3, SQLite hc-tree might fix 2

- Agree about update hook. BEGIN CONCURRENT is not enough write concurrency? I guess not if you want update hook anyway I wonder how long until libsql has a rocksdb backend
- Notion is using SQLite on mobile, correct? How do you guys deal with reacting to mutations?
  - `sqlite3_update_hook` works for us

- Yeah let’s do it and add cell-level reactivity while we are at it.
# discuss
- ## 

- ## 

- ## [Tell HN: SQLite3 does have something like stored procedures | Hacker News](https://news.ycombinator.com/item?id=31913062)
- However, triggers cannot return result rows, and a SELECT query that a view is defined as cannot take parameters (although there is a work-around by using a virtual table which contains a single row whose value is whichever value it is constrained to be). There is also WITH RECURSIVE, which also has many uses.

- ## [Why isn't SQLite more commonly used for save files or for other user-facing application file formats? : programming](https://www.reddit.com/r/programming/comments/h86v81/why_isnt_sqlite_more_commonly_used_for_save_files/)
- What did SQLite gave us? SQL.
  - XML schemas are gnarly, SQL schemas are easy.
  - Primary keys are great. Foreign keys are gorgeous.
  - Constraints on columns are handy.
  - :memory: is awesome for unit-tests.
- A lot of user applications store some or all their state in sqlite, firefox being a prominent example. That is what embeddable databases are designed for. It is not frequently used as an exchange format though, because it is no designed to be a good exchange format.
- Why is it not a good exchange format? Relational tables are an excellent exchange format, and SQLItes is specifically designed to be portable across time and architectures.
  - It's only unportable if you do something like use platform serialization to store your data structures in blobs. Don't do that, or serialize them to JSON/XML/etc before putting them in a blob.




- Also most data in iPhone apps is stored in sqlite files. Rip apart an iphone backup some time and peek at the contents.
- 
- 

- ## ✨ [Show HN: Doculite – Use SQLite as a Document Database | Hacker News_202308](https://news.ycombinator.com/item?id=37040359)
- I'm the core maintainer of the npm sqlite package that your library uses. I recommend that you don't make it a direct dependency, but use dependency injection or an adapter pattern that way your library isn't dependent on a specific package version of sqlite/sqlite3

- Just curious if this is using the JSON functions/operators for SQLite under the covers?
  - Yes – I'm using JSON_extract and generated virtual columns https://www.sqlite.org/json1.html#jex Edit: the database is stored in a sqlite.db file in the cwd

- DocuLite lets you use SQLite like Firebase Firestore.
  - Honestly, that sounds absolutely frightening to my ear. There are redis, there is mongo, orient, and plenty of document-based rapid-development databases which will be a substantially better solution than turning sqlite into Firebase.
  - Yes, you can use data change notification callbacks. It is a cool feature of SQLite, but did you know that their performance is a big concern in a large-scale database (document database grows very quickly by design)? What about COUNTs? Batching operations? Deadlocks? This will go out of hand quickly, because a hammer is used as a shovel here.
- I just did a quick search and struggled to find anything about the performance issues you referred to - can you link something so I can take another look? Thanks for the suggestions.
  - From the code, it s easy to see that you create a WRITE transaction which has the side effect of triggering READ transactions. It is also important to understand that if you mix reads and writes you cannot do it well concurrently with SQLite, so every transaction will be sequential and blocking. Looking at the code further I understand that it will not scale well, since a single write can possibly trigger a waterfall of callbacks creating bottlenecks. The problem in your case is that sqlite_update_hook doesn't transport back data and that it is listening for changes in all tables having ROWID optimisation on. So first things first you only need one such callback and a different approach for integrating it in a document abstraction than table name and rowid predicate in a dozen of registered callbacks.
  - You will unveil more problems with SQLite for this job as you dig deeper. **What you really want is fast writes and dumb querying by document id, whereas SQLite gives you an ultra querying suite that you don't utilize but still have to pay with slower writes**. This is a classic system-design problem. Just try rewriting your collection and document abstractions using proper document data storage and you will see how less complicated it is.

- This is cool. There are a tonne of options for local KV stores that likely outperform this by a large margin, but the obvious benefit here is that SQLite is really simple to configure and operate!

- We currently use Realm for this use case. It’s a local database just like SQLite, but with native support for documents and listeners. Did you try that out?

- ## [Show HN: Squirrelbyte – a SQLite-based JSON document server | Hacker News_202104](https://news.ycombinator.com/item?id=26766557)
- 
- 
- 

- ## [SQLite as a Document Database | Hacker News_202011](https://news.ycombinator.com/item?id=25226260)
- 
- 
- 
- 

- ## Nobody is feasibly going to rewrite Sqlite in Rust.
- https://news.ycombinator.com/item?id=25464846
  - Is making à file based database that hard, compared to creating new programming language for example ?

- If you gave me two year I'm not sure I could implement a filesystem API that correctly did something as simple as "atomically append to a file". See also Dan Luu's writing on the topic of filesystems

- The problem is to write a reliable file database. 
  - Firefox got a lot of bugs related to history file corruption until it was replaced with SQLite. 
  - The same story was with Subversion where they replaced Berkeley key DB due to reliability issues.
  - This reliability comes from a very deep knowledge of OS API and all their corner cases. 
  - Creating a programming language typically involves less corner cases and the bugs in the compiler/runtime are much simple to reproduce (again, typically).

- 
- 

- ## [Xlite: Query Excel and Open Document spreadsheets as SQLite virtual tables | Hacker News](https://news.ycombinator.com/item?id=31874767)
- Sqlite does not allow table valued functions to return results with varying schemas. The schema must be defined once up front and then cannot change.
  - That forum post is a request I made to them to allow dynamic columns but they don't seem interested so far.

- ## Introducing sqlite-xsv - a SQLite extension for quickly querying CSVs!
- https://twitter.com/agarcia_me/status/1613688022079508480
  - Custom delimiters, quotes, column names and types
  - written in Rust, with sqlite-loadable!
- For *non-analytical* queries, I have found sqlite-xsv to be:
  - 1.5-2x faster than other CSV SQLite extensions
  - 1.2-3x faster than @DuckDB, DataFusion, clickhouse-local (!!)
  - 6x faster than pandas
  - 14x faster than sqlite3's .import
  - ~300x faster than dsq, sqlite-utils
- For *analytical* queries 
  - directly on CSVs (ex GROUP BYs and ORDER BYs), both sqlite-xsv and sqlite in general fall short compared to new-age tools like @DuckDB , DataFusion, and clickhouse.

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

- ## [sqlite rowid after deleting rows](https://stackoverflow.com/questions/35876171)
  - I delete rows with id 3 and 4 and run above query again.
  - Now my problem is rowid not getting reset and holes.
  - 在删除某些行后，其他所有行的rowid不变，不受影响，就会形成断断续续的rowid
- rowid is really special. So special that if you have an `INTEGER PRIMARY KEY` , it becomes an alias for the rowid column. 
  - when your primary key is an alias for rowid, it would be terribly inconvenient if this could change. 
  - Since rowid is now aliased to your application data, it would not be acceptable for sqlite to change it.
- If you really really really absolutely need the rowid to change on a VACUUM, you can avoid this aliasing behavior. Note that it will decrease the performance of any table lookups using your primary key.
  - To avoid the aliasing, and degrade your performance, you can use `INT` instead of `INTEGER` when defining your key

- ## [Why Is SQLite Coded in C (2017) | Hacker News](https://news.ycombinator.com/item?id=28278859)

- But it's still a database, a low level, high performance software system. 
  - Even if you write it in rust, some percentage of the code will be unsafe rust or rust that calls a library written in C. 
  - It will be safer, but still not a panacea. 
  - It would be more viable in my opinion to improve the safety of the C code that currently makes up sqlite.

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

- ## [The Design of SQLite4 | Hacker News_202206](https://news.ycombinator.com/item?id=31785170)
- >SQLite4 was an experimental rewrite of SQLite that was active from 2012 through 2014. All development work on SQLite4 has ended. Lessons learned from SQLite4 have been folded into the main SQLite3 product. SQLite4 was never released. There are no plans to revive it. You should be using SQLite3.

- [Work on SQLite4 has concluded | Hacker News_201711](https://news.ycombinator.com/item?id=15648280)
