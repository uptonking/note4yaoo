---
title: lib-db-postgresql-vs-mysql
tags: [comparison, database, mysql, postgresql]
created: 2020-12-18T13:23:08.190Z
modified: 2023-11-01T14:13:41.390Z
---

# lib-db-postgresql-vs-mysql

# guide

- mysql特点
  - 支持修改更新索引

- postgresql特点
  - 支持并行创建索引

- [PostgreSQL vs. MySQL](https://www.postgresqltutorial.com/postgresql-vs-mysql/)
  - PG: MIT-style license; MY: GPL
  - PG-NO && MY-YES
    - Unsigned integer
    - Multiple storage engines e.g., InnoDB and MyISAM
  - PG-YES && MY-NO
    - Identity Column
    - Analytic functions
    - IP address data type
    - Materialized views
    - Table inheritance
    - FULL OUTER JOIN
    - INTERSECT
    - EXCEPT
    - Partial indexes
    - Bitmap indexes
    - Expression indexes
# dev

# blogs-pg-vs-mysql

## 🆚️🐘🐬 [Postgres vs MySQL. The fundamental difference between the… | by Hussein Nasser | Medium _202302](https://medium.com/@hnasr/postgres-vs-mysql-5fa3c588a94e)

- the main difference between the two databases really boils down to the implementation of primary and secondary indexes and how data is stored and updated.
  - An index is a data structure (B+Tree mostly) that allows searching for keys through layers of nodes which databases implement as pages.
  - Leaf nodes or pages contain a list of ordered keys and their values. When a key is found you get its value and the page is cached in the database shared buffers with the hope that future queries may request keys in the same page.
  - Keys in B+Tree indexes are the column(s) on the table the index is created on, and the value is what databases implement differently. 

- Let us explore what value is in Postgres vs MySQL.

- MySQL
- In a primary index, the value is the full row object with all the attributes*. 
  - This is why primary indexes are often referred to as clustered indexes or another term that I prefer index-organized table. This means the primary index is the table.
  - If you do a lookup for a key in the primary index you find the page where the key lives and its value which is the full row of that key, no more I/Os are necessary to get additional columns.
- In a secondary index the key is whatever column(s) you indexed and the value is a pointer to where the full row really live. 
  - The value of secondary index leaf pages are usually primary keys.
- This is the case in MySQL. 
  - In MySQL all tables must have a primary index and all additional secondary index point to the primary keys. 
  - If you don’t create a primary key in a MySQL table, one is created for you.

- Postgres
- In Postgres technically there is no primary index, all indexes are secondary and all point to system managed tuple ids in data pages loaded in the heap. 
- The table data in the heap are unordered, unlike primary index leaf pages which are ordered. 
  - So if you insert rows 1–100 and all of them are in the same page, then later updated rows 1–20, those 20 rows may jump into a different page and become out of order. 
- While in a clustered primary index, insert must go to page that satisfies they key’s order. 
  - That is why Postgres tables are often referred to as “heap organized tables” instead of “index organized tables”.
- It is important to note that updates and deletes in Postgres are actually inserts. Every update or delete creates a new tuple id and the old tuple id is kept for MVCC reasons.

- The truth is the tid by it itself is not enough. Really we need both the tuple id and also the page number, this is referred to as c_tid. 
  - Think about it, it is not enough to just know the tuple id we need to know which page the tuple live. 
  - Something we didn’t have to do for MySQL because we are actually doing a lookup to find the page of the primary key. Where as in Postgres we are simply doing an I/O to fetch the full row.

- In MySQL choosing the primary key data type is critical, as that key will live in all secondary indexes. For example a UUID primary key will bloat all secondary indexes size causing more storage and read I/Os.
  - In Postgres the tuple id is fixed 4 bytes so the secondary indexes won’t have the UUID values but just the tids pointing the heap.

- MySQL uses threads, Postgres uses processes, there are pros and cons for both

- What really matters is breaking down your use cases and queries and understand what each database does and see what works and what doesn’t for you. No wrong or right here.

## [MySQL vs. PostgreSQL — PlanetScale](https://planetscale.com/learn/articles/mysql-vs-postgres)

- MySQL has a simpler and more flexible architecture than PostgreSQL, making it easier to install and configure. 
- On the other hand, Postgres works well when it comes to extensibility and durability.

- Performance is inherently dependent on how indexing is done on the tables that are being queried, irrespective of whether it’s on MySQL or PostgreSQL. 

- it is important to note that materialized views are not natively supported in MySQL. 
  - Materialized views store query results in the database as a physical table, rather than being calculated each time the view is accessed.

- [Migrating from Postgres to MySQL](https://planetscale.com/blog/migrating-from-postgres-to-mysql)

## [对比MariaDB与PostgreSQL，如何选择正确的数据库？ _202405](https://huangz.blog/2024/mariadb-vs-postgresql.html)

- 相似之处
  - MariaDB和PostgreSQL都是强大的数据库系统，因其可靠性和强大的社区支持而广受认可。
  - 两者都支持各种编程语言，比如Python、Java、C/C++和PHP，并提供诸如ACID合规性以确保事务可靠性并支持复杂的查询。

- 不同之处
  - 性能和存储引擎：MariaDB以其速度而著称，它包含多个存储引擎（包括Aria和InnoDB），每个引擎都有它们各自适合的工作负载，并且可以根据特定的性能或数据完整性需求进行微调。与此相反，PostgreSQL使用单一的默认ACID兼容存储引擎，该引擎对并发性和数据完整性进行了优化，这种做法简化了架构，但是也限制了针对特定性能场景进行微调的可能。
  - 复杂性：与MariaDB相比，PostgreSQL提供了更高级的特性，但这些特性也带来了更陡峭的学习曲线。
  - 高级特性：PostgreSQL经常因其特性丰富而受到表扬，比如它强大存储过程、复杂的加锁机制以及对JSON、XML和数组等“NoSQL”数据类型的支持。这些功能使得PostgreSQL成为需要复杂数据集成和强大数据完整性的应用程序的理想选择。
  - 扩展和索引：PostgreSQL还支持更高级的索引类型和非常多的扩展，使其具有极强的可扩展性。比如PostgreSQL的GIN和GIST索引就非常适合实现全文搜索和储存地理空间数据。MariaDB虽然也提供了灵活的插件架构，但它支持的专用索引类型并不多。
# discuss-pg-mysql
- ## 

- ## 

- ## 

- ## The big difference between MySQL's thread model and PostgreSQL's process model is how they handle synchronization. 
- https://x.com/wangbin579/status/1884454988497174716
  - PostgreSQL's process-based sync is pretty clunky and slow under high contention, while MySQL's thread model gives it a significant performance advantage.

- Any notable benefits that Postgres’s process model offers?
  - Yeah, for sure, the multi-process model has its perks too—like being less likely to crash completely.

- I wish Postgres had a separate process for connection pooling and transaction routing. Very annoying to have to run things like pgbouncer as well at scale.

- PostgreSQL's process model may be slower, but it's more stable. MySQL's thread model has its perks too. Each has its place!

- ## Comparing the read-only performance of MySQL and PostgreSQL with the same 128 hash partitions.
- https://x.com/wangbin579/status/1880086759830352341
- Am ai reading this wrong? PG seems much slower at ~1000 req per sec while mysql is around 17k req per sec
  - This is the performance of PostgreSQL hash partitioning, and it doesn't represent the overall performance of PostgreSQL.
- psql is slower because of the optimizations? Or did I misread the results?
  - This is a known issue with PostgreSQL partitions. Even after merging the fast path patch, performance is still not good. The chart above shows the difference between MySQL and PostgreSQL in this test. Of course, the difference can vary in different environments.

- Queries within a single partition's constraints are much faster, right? Is this also the case for RANGE partitions? Can't say I've benchmarked PostgreSQL in this regard.
  - For RANGE partitions, PostgreSQL performs fairly well, as long as not too many partitions need to be accessed.

- This is a well-known issue with PostgreSQL hash partitioning. The official next version is expected to include a fast path patch, which should alleviate some of the issues.

- ## I can't *quickly* think of companies doing massive Postgres deployments (like petabytes or exabytes) 
- https://x.com/iavins/status/1870142918549496283
  - But for MySQL? So many come to my mind easily: YouTube, Facebook, PlanetScale, Uber, etc.
  - Okay, couldn't find a single example of a massive Postgres deployment

- Here are the top three (publicly known) deployments:
  1. Heap - 2PB+
  2. Timescale - 1PB+
  3. Adyen - 100TB

- Ostensibly this is because those companies started in a time where MySQL was dominant and not Postgres (mid 2000s). Check in again 15 years from now and see what the biggest RBDMS deployments are. Also MySQL backed by Oracle which is good for enterprises whereas Postgres is bona fide OSS.
- Postgres became popular much later. MySQL was everyone’s go-to DB in the 2000s. Oracle’s acquisition impacted its popularity to some extent (which also split the community with MariaDB) So we will start reading about massive Postgres deployments in few more years.

- It's easier to migrate from Postgres to MySQL and use the mega-scale tooling in that world than it is to re-create that tooling for Postgres I guess. I also think Postgres' design is better for small-mid systems (MVCC etc) but MySQL eventually wins out when you have to start doing more in the application layer anyway at massive scale.

- I’m pretty sure @zerodhaonline is all in on Postgres and they’re huge!

- Figma. And AWS if you count Aurora

- The number of people demanding compression from Innodb is long, because cost savings are very important due to the scale of many MySQL deployments. I have not heard anybody make the same demands from Postgres. This makes me very suspicious of all the PG fanboi spruiking

- Possibly Notion, but I couldn't find storage numbers in their blog posts
- Figma has a great blog about theirs - but ummm yes there are a TON of massive postgres deployments
- I think PostgreSQL is becoming more enterprise-oriented at larger scales. Azure's acq. of Citus, for example, enables their offering to scale to petabytes as they claim.
- Skype used Postgres. I don't have numbers but it wad quite large back then

- Dropbox metadata is on MySQL and served millions of transactions per second last time I worked on it. Even the multi-exabyte storage system we built used MySQL for indexing. At the time MySQL was much more battle-tested at scale than Postgres.

- If you’re in a situation where you want to store a large number of documents for app retrieval (pdfs, word, etc) I know the S3 or azure storage is the best strategy but how well does Postgres scale in these scenarios?

- ## 🆚️ Postgres and MySQL, the main differences
- https://x.com/hnasr/status/1859366187534254274
  - In a nutshell, the main difference between the two databases really boils down to the implementation of primary and secondary indexes, how data is stored and updated and the MVCC implementation.
  - An index is a data structure (B+Tree mostly) that allows searching for keys through layers of nodes which databases implement as pages

- 🐬 MySQL
  - In a primary index, the value is the full row object with all the attributes*. This is why primary indexes are often referred to as clustered indexes or another term that I prefer index-organized table. This means the primary index is the table.
  - Note that this is true for row-store, databases might use different storage model such as column-store, graphs or documents, fundamentally those could be potential values.
- In a secondary index the key is whatever column(s) you indexed and the value is the primary key for that row. The value of secondary index leaf pages are usually primary keys. 
  - If you do a lookup on a secondary index, you find the secondary key, and the key's value is primary key for that row. To find the full row you need to scan the primary index using the primary key you found to get the full row. 
  - So two index scans.

- 🐘 Postgres
  - Technically in Postgres there is no primary index, all indexes are secondary and all point to system managed tuple ids in data pages loaded in the heap. 
  - The table data in the heap are unordered, unlike the clustered primary index leaf pages which are ordered.
  - Postgres tables are often referred to as “heap organized tables” instead of “index organized tables”.
  - Updates and deletes in Postgres are actually inserts. Every update or delete creates a new tuple id and the old tuple id is kept for MVCC reasons. 
  - The truth is the tid by it itself is not enough. Really we need both the tuple id and also the page number, this is referred to as c_tid. Think about it, it is not enough to just know the tuple id we need to know which page the tuple live. Something we didn’t have to do for MySQL because we are actually doing a lookup to find the page of the primary key. Whereas in Postgres we are simply doing an I/O to fetch the full row.

- That query in MySQL will cost us two B+Tree lookups*.  We need first to lookup x2 using the secondary index to find x2's primary key which is 1, then do another lookup for 1 on the primary index to find the full row so we return all the attributes (hence the *).
  - In Postgres looking up any secondary index will only require one index lookup followed by a constant single I/O to the heap to fetch the page where the full row live. One B+Tree lookup is better than two lookups of course.

- Both MySQL and Postgres require a clean up process that removes dead and unwanted data. MySQL implements a process called “purge, ” while PostgreSQL uses “vacuum”.
  - Purge removes unused undo logs no longer needed either belonging to transactions that already committed or transactions that have rolled back (via a crash) and no longer need the undo log. Too many undo logs can slow down reads.
  - Postgres vacuum process (or really processes), on the other hand, is designed to reclaim storage occupied by “dead tuples”. As we discussed, when a row is updated or deleted in Postgres, the old version of the row is not immediately removed from disk; instead, it’s marked as dead. The vacuum process cleans up these dead tuples, freeing space for new data and preventing table bloat, but not necessary returning this space back to the operating system.

- MySQL uses threads, Postgres uses processes

- MySQL was designed with the flexibility to extend its storage engine, with InnoDB as the default option. This allowed MySQL to support multiple storage engines, for example it could integrate with RocksDB through MyRocks. 
  - However, PostgreSQL operates with a single storage engine (heap storage), and adopting a different one would require forking and significantly rewriting the entire system, making such modifications far more challenging.

- 👥 discussion

- if you don’t define a primary key, MySQL will find a way to create one from existing fields, if it couldn’t it generates a new hidden field and makes it the pk
  - That's not at all the same as a normal PK, it doesn't present externally at all and is only used internally.

- ## I don't think the code bloat for InnoDB in MySQL 8.0 can be undone. 
- https://x.com/MarkCallaghanDB/status/1839429943861887206
  - The workarounds are MyRocks, MariaDB, MySQL 5.7 forever or Postgres.
- I really never understood why people stuck around with MySQL. In my 'bubble' _everyone_ moved over the MariaDB around the MySQL 5.5 era. Although I recently noticed that Geoindexing was better in MySQL 8 compared to MariaDB 10.x. But then again, MariaDB 11 has been out already.
  - We have different bubbles but I started to do tests for MariaDB and was happy to learn it has done much better at avoiding the performance regressions.
- 5.7 is not a reasonable work-around! No one should be using that junk heap anymore.
  - The real cause of the bloat is playing feature catch-up. 5.7, though it releases much later, was still rooted in the 2004-06 era of the platform. Sun lacked resources to advance the product even before Oracle, which had no reason to move it forward. MySQL stagnated for a decade.
  - It got to the point MySQL no longer even qualified as a modern relational database platform. Too much was missing. So the push into 8.0 and later had to do too much, too quickly. Quality will always suffer when that dynamic is in play.

- ## the implementation of btree in PG is also more refined. 
- https://x.com/baotiao/status/1799557033555116035
  - For example, it includes features like suffix compression, blink-tree, and deduplication. 
  - In comparison, up to now, the btree in upstream InnoDB still has a big lock
- InnoDB internal nodes are also linked making them b-link trees. The problem you are referring to is the dict_index_t::lock which tries to solve another problem. Covering the change of the root page.  It’s indeed a bottleneck.
  - I don't think that InnoDB's btree is a blink-tree. In my opinion, it needs to include link pages and support the process where child nodes do not need to link back to parent nodes during structure modification operations (SMO) to be considered a blink-tree.
- Child nodes do not link back to parent nodes. Why do you think that? The nodes at all levels below the root link both ways. To reinforce the point, InnoDB SMO operations are redo logged atomically using the minimal number of latches required on the pages. What is different is that it doesn’t follow the latching protocol of Lehman & Yao (they coined the term B-link tree as part of their latching protocol).
  - NO, I think InnoDB is not doing enough in this area. During SMO, it locks the subtree and does not guarantee locking only two levels. With blink-tree and lock coupling, it can achieve locking only two levels. I have wrote a article about the evolvetion of btree index.
- Sure, it doesn’t follow the L&Y protocol, and could be improved , the point is that it’s physically a B-link tree  

- ## pg可以创建自定义的range类型也可以用内置的daterange类型存储范围类型 然后使用@>, *, +, -等运算符进行范围查询 例如交集 差集 左右开闭区间包含等
- https://twitter.com/changwei1006/status/1769657994030281210
  - pg的GiST索引结合exclude约束可以实现在海量范围数据中快速执行包含以上各种运算符的范围查询
  - MySQL在这些领域就是垃圾
- MySQL也可以between查询两个字符串格式的时间吧

- ## [Supabase or Planetscale? : r/nextjs _202305](https://www.reddit.com/r/nextjs/comments/13owssn/supabase_or_planetscale/)
- If you plan on staying on the free tier planetscale is a lot cheaper. On supabase you get 500mb on the free tier vs 5gb storage on planetscale. supabase has a lot more to offer like auth etc. tho

- They're pretty different services. Planetscale is just for your Database, with features for caching, geodistribution, etc. Supabase is more of an all-in-one platform to build your app on. They give you a Postgres database, and have solutions for authentication, file storage, web hosting, etc.

- ## 🆚️ Old Postgres and old MySQL had similar performance on sysbench. 
- https://twitter.com/MarkCallaghanDB/status/1719500763666452654
  - But modern Postgres is usually faster than modern MySQL because Postgres has avoided CPU perf regressions over time.
  - [Small Datum: Postgres vs MySQL: the impact of CPU overhead on performance](https://smalldatum.blogspot.com/2023/10/postgres-vs-mysql-impact-of-cpu.html)
- Do you mean that new features introduced perf regression in MySQL?
  - Yes. Have seen the same in other DBMS too, just not in Postgres.

- ## 🆚️🔥 [Ask HN: What could a modern database do that PostgreSQL and MySQL can't | Hacker News_202109](https://news.ycombinator.com/item?id=28425379)
- 
- 
- 

- ## [mysql 和 postgresql哪个更适合互联网企业？](https://www.zhihu.com/question/324036100/answers/updated)
- pg除了不能针对单个数据库进行备份恢复，复制，即时点恢复(这给日常维护带来了很大的麻烦)，其它完美。我一个服务器上都有几十上百个数据库。
  - pg开发爽，维护不爽，sql server维护起来真的很方便

- ## [PostgreSQL 与 MySQL 相比，优势何在？](https://www.zhihu.com/question/20010554/answers/updated)
- pg有很多数据库的新特性，很多学术的都会用postgresql

# more
- [postgresql也很强大，为何在中国大陆，mysql成为主流](https://www.zhihu.com/question/31955622/answers/updated)
