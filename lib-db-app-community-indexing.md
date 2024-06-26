---
title: lib-db-app-community-indexing
tags: [community, database, indexing, query-engine, search]
created: 2023-09-17T17:37:32.457Z
modified: 2023-09-17T17:38:11.187Z
---

# lib-db-app-community-indexing

# guide

# discuss-stars
- ## 

- ## I'm surprised to realize that neither Postgres or SQLite support indexing OVERLAPS/BETWEEN queries for non-numerical ranges. 
- https://twitter.com/ccorcos/status/1736870370140131512
  - The GiST / R*Tree indexes only work on numbers. Dates, I believe, are converted into numerical values
  - Someone, please prove me wrong

# discuss
- ## 

- ## 

- ## 

- ## 🆚️ For an in memory database if you were to design an indexing structure to support both point and range queries, 
- https://x.com/debasishg/status/1803394530571383015
  - is trie the most optimal data structure with respect to query time complexity, space usage and cache line friendliness ?
- in my opinion, a B-tree with a high k-value works pretty well. I have been evaluating the same for @thedicedb and it is serving us well for most of our use cases (point plus range).
  - again, we have not done the stress test yet, but from the initial development, we are inclined towards B-trees.
- This Cassandra memtables paper (https://vldb.org/pvldb/vol15/p3359-lambov.pdf) has some comparisons with comparison-based data structures. But I agree that with a larger k, the height of the tree goes down that will lead to better cache alignment. But as the memtables paper indicates, tries may be easier to cache friendliness than comparison based trees .. The ART paper (https://db.in.tum.de/~leis/papers/ART.pdf) also indicates similar thoughts ..
- I don't know the answer but I'd bet on trie too. The Adaptive Radix Tree: ARTful Indexing for Main-Memory Databases

- ## why you always need a multi-column index
- https://twitter.com/tobias_petry/status/1777985940302032975
  - An index with more columns can check more of a query's conditions. So fewer rows are loaded and the query is faster
- multi-column is an essential feature available with EVERY sql database. 
  - Indexing JSON is a complicated topic. Too much for tweet - and it depends on your database. I wrote an entire chapter on that in my book.
  - For PG just use GIN indexes, with MySQL it is more complicated

- ## SQL Indexing in a Nutshell:
- https://twitter.com/vikasrajputin/status/1773568534737727614
  - 动画示意图

- ## When many database indexes are too many?
- https://twitter.com/deisbel/status/1760322457750085930
- instead of trying to figure out the right number of indexes, let's change our approach to:
  - 1- Define an index only if you have proof you will use it.
  - 2- If you are unsure, refrain(克制；抑制) from creating it.
  - 3- If you need more later, add them.
- If your system mostly makes queries, with not too many concurrent data transactions, then you have more liberty to create more indexes.

- Measure Twice, Index Once. If a particular query is slow, look at whether indexing could help—but also consider other factors like query optimization or schema changes.

- ## Database indexing explained.
- https://twitter.com/ChrisStaud/status/1759958340086767693
  - An index is a key-value pair where the key is used to search for data instead of the corresponding indexed column(s), and the value is a pointer to the relevant row(s) in the table.

- ## 👨🏻‍🏫 How to find redundant indexes
- https://twitter.com/samokhvalov/status/1734467240832201064
  - Redundant indexes refer to multiple indexes on a table that serve the same purpose or where one index could satisfy the queries that all others do. 

- ## 👨🏻‍🏫 How to find unused indexes
- https://twitter.com/samokhvalov/status/1734044926755967163
  - General algorithm of unused indexes cleanup
  - Queries to analyze unused indexes
- Why to clean up unused indexes
  1. They occupy extra space on disk.
  2. They slow down many write operations (INSERTs and non-HOT UPDATEs).
  3. They "spam" caches (OS page cache, Postgres buffer pool) because index blocks are loaded there during write operations mentioned above.
  4. Due to the same reasons, they "spam" WAL (thus, replication and backup systems need to handle more data).
  5. Every index slows down the query planning 
  6. Finally, if there is no plan caching (prepared statements are not used), each extra index increases chances to reach FP_LOCK_SLOTS_PER_BACKEND=16 relations (both tables and indexes) involved in query processing, which, under high QPS, increases chances of having LWLock:LockManager contention 

- unused indexes are problematic in all database platforms, but caution if recursive SQL (eg optimizer, referential integrity, etc) implicitly use them. 

- ## [2 phase indexing · crate/cratedb_202308](https://github.com/crate/crate/pull/14617)
- The way we index documents is not changed, only split into 2 phases.
  - Phase 1: Collect new columns and do a schema update. Don't create a Lucene document with source at this point.
  - Phase 2: Index. Currently target references still might have unassigned OID since this is only a preparation step.

- ## Multi tenancy is paramount for vector indexes
- https://twitter.com/Sirupsen/status/1730356136782549153
  - With b-trees’ log(n) it doesn’t matter too much if you have one big table for all tenants
  - For a vector index, the complexity is higher. Important to use the natural sharding keys when you can

- ## 💡 Database Indexing Explained.
- https://twitter.com/NikkiSiapno/status/1719352895169265797
  - An index is a key-value pair where the key is used to search for data instead of the corresponding indexed column(s), and the value is a pointer to the relevant row(s) in the table.
  - Indexing speeds up queries, but it also takes up storage space and adds overhead to operations
  - B-tree is one of the most commonly used indexing structures where keys are hierarchically sorted. B-tree is most commonly used because of its efficiency in storing and searching through ordered data. Their balanced structure means that all keys can be accessed in the same number of steps, making performance consistent.
  - Hash indexes are best used when you are searching for an exact value match. The key component of a hash index is the hash function. 
  - Bitmap indexing is used for columns with few unique values. 
  - A composite index may be used when multiple columns are often used in a WHERE clause together. 

- ## how bitmap index scans work
- https://twitter.com/hnasr/status/1718592877658538228

- ## 🔥 [Why Can't Database Tables Index Themselves? (2006) | Hacker News_202207](https://news.ycombinator.com/item?id=31990836)
- 
- 
- 

- ## 🔥 [Spending $5k to learn how database indexes work | Hacker News_202111](https://news.ycombinator.com/item?id=29132572)
- 
- 
- 

- ## 🔥 [How does database indexing work? (2008) | Hacker News_202203](https://news.ycombinator.com/item?id=30594233)
- If you want to see a dumb example of how you can implement indexing on top of a SQL database without it, I wrote a tutorial on implementing basic indexes as part of a series on making a SQL database from scratch.
  - [Writing a SQL database from scratch in Go: 3. indexes](https://notes.eatonphil.com/database-basics-indexes.html)

- 
- 
- 

- ## [sql server - Will index be fully loaded into memory_201011](https://stackoverflow.com/questions/4296027/will-index-be-fully-loaded-into-memory)
- No, it's treated like any other data stored on disk. It's loaded into memory disk page by disk page. And a page stays in memory as long as it's regularly accessed.

- The answer to this is in several parts:
  - The size of the index.
  - What parts are accessed.
  - Memory pressure.
- SQL Server cached the index in memory as it was being read.
  - However, if I had put other memory pressure on SQL Server, it would have dropped out those cached index pages by order of lowest reads.

- ## [联合主键和复合主键和联合索引](https://www.cnblogs.com/saoge/p/14431536.html)
- 复合主键 就是指你表的主键含有一个以上的字段组成
- 联合主键 就是多个主键联合形成一个主键组合，联合就在于主键A跟主键B形成的联合主键是唯一的。

- [提问关于 mysql得联合主键和复合主键的问题 - SegmentFault 思否](https://segmentfault.com/q/1010000021884619)
  - 在英文语境中只有 Composite Primary Key（也有叫 Compound Primary Key 的），就是一个表中如果是多个字段组成一个主键，那么这个主键就被称为这玩意儿。
  - 这种概念是中文编程界（或者说是中文编程博客界）人为造出的。
  - 上面的例子看看就得了，根本就是胡编一个 联合主键 的定义出来，你会发现它其实就是一个最简单的自增主键，只不过表的逻辑上 student_id + subject_id 是唯一的，id 就成了所谓的二者的 联合主键。
