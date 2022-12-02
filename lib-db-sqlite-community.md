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

- ## 

- ## 

- ## 

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
  - https://github.com/symisc/unqlite
    - UnQLite is an embedded NoSQL (Key/Value store and Document-store) database engine.

- ## [sqlite rowid after deleting rows](https://stackoverflow.com/questions/35876171)
  - I delete rows with id 3 and 4 and run above query again.
  - Now my problem is rowid not getting reset and holes.
  - 在删除某些行后，其他所有行的rowid不变，不受影响，就会形成断断续续的rowid
- rowid is really special. So special that if you have an `INTEGER PRIMARY KEY` , it becomes an alias for the rowid column. 
  - when your primary key is an alias for rowid, it would be terribly inconvenient if this could change. 
  - Since rowid is now aliased to your application data, it would not be acceptable for sqlite to change it.
- If you really really really absolutely need the rowid to change on a VACUUM, you can avoid this aliasing behavior. Note that it will decrease the performance of any table lookups using your primary key.
  - To avoid the aliasing, and degrade your performance, you can use `INT` instead of `INTEGER` when defining your key
