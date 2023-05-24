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

## [Why Is SQLite Coded in C (2017) | Hacker News](https://news.ycombinator.com/item?id=28278859)

- But it's still a database, a low level, high performance software system. 
  - Even if you write it in rust, some percentage of the code will be unsafe rust or rust that calls a library written in C. 
  - It will be safer, but still not a panacea. 
  - It would be more viable in my opinion to improve the safety of the C code that currently makes up sqlite.
