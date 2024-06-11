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
