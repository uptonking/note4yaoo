---
title: lib-db-postgresql-community-tips
tags: [community, devops, postgresql]
created: 2023-10-28T17:51:55.607Z
modified: 2023-10-28T17:52:17.942Z
---

# lib-db-postgresql-community-tips

# guide

# discuss-stars
- ## 

- ## 

- ## PostgreSQL is a fascinating database and if you want to explore something super interesting in it, I would highly recommend reading about these five niche concepts
- https://x.com/arpit_bhayani/status/1865012459423305841
  1. Transaction Wraparound Problem
  2. Transaction ID Freezing
  3. Integration of Freezing Logic in VACUUM
  4. Aggressive Freezing vs. Lazy Freezing
  5. Multi-page Freezing and Freeze Map Maintenance

- ## I was today years old when I learned about the "\watch" option of psql for repeatedly running a query and examining its changing output.
- https://twitter.com/gunnarmorling/status/1693868171931914288
  - `SELECT * from foo; \watch 1`

- In PG16 you will have a count option to stop it after n runs. Even better

- ## 🔥 [Tips for a healthier Postgres database (2021) | Hacker News_202302](https://news.ycombinator.com/item?id=34734021)
- 
- 
- 

- ## 🔥 [Tips for a Healthier Postgres Database | Hacker News_202201](https://news.ycombinator.com/item?id=29858083)
- 
- 
- 

# discuss-pg-rust
- ## 

- ## 

- ## [PL/Rust 1.0: now a trusted language for Postgres | Hacker News_202304](https://news.ycombinator.com/item?id=35501065)
- why would anyone want to use PL/Rust over PL/PQSL? what is the use case?
  - > PL/Rust is a loadable procedural language that enables writing PostgreSQL functions in the Rust programming language
  - Use to write PostgreSQL functions in Rust. Also
  - > The top advantages of PL/Rust include writing natively-compiled functions to achieve the absolute best performance, access to Rust's large development ecosystem, and Rust's compile-time safety guarantees.

- A crucial facet of optimization for computational triggers in PostgreSQL pertains to the implementation of event triggers, which enable operations to be executed in bulk (per DML statement) rather than on a per-row basis. It appears that, at present, PL/Rust has not incorporated support for event triggers. According to the documentation
  - Event Triggers and DO blocks are not (yet) supported by PL/Rust.

- ## [RustgreSQL | Hacker News_201701](https://news.ycombinator.com/item?id=13354099)
- I would suggest that the author creates a clone of a "simpler" DB like SQLite or Redis. Those have, as far as I understand, good C codebases, so understanding the system should be much easier.

# discuss-cons-pg
- ## 

- ## 

- ## PostgreSQL has some limits on the number of partitions. 
- https://twitter.com/FranckPachot/status/1772630850854670729
  - YugabyteDB scales out with the automatic distribution of rows and index entries and uses partitions for lifecycle management or geo-partitioning, where the number is low
  - [Solve PostgreSQL Indexes, Partitioning, LockManager Limitations _202403](https://www.yugabyte.com/blog/postgresql-indexes-partitioning-lockmanager-limitations/)
- Interesting article. I feel that partitioning by hash is a different use case to partitioning by range of time (which I feel is the more common use in PG). Are you looking to cover that partitioning case sometime?
  - Yes I used hash here because it is easy to distribute without thinking of values. Will be the same on time: partition by range in postgres, or declaring the key as ASC or DESC in YugabyteDB. Can additionally partition by range on YB for lifecycle management, with few partitions)

- To me this seems applicable to hash partitioning but not when partitioning by range on time (e.g. monthly) though right?
  - It can. An index on the date will be: `CREATE INDEX on payments (created desc, payment_id)`

  - range sharded, split automatically when growing (you can pre-split if you know the values) 
  - Or, if the date is in the key, PK can be: `primary key (created desc, payment_id)`

- https://twitter.com/FranckPachot/status/1772895989394710668
  - Sharding by HASH is nice to immediately distribute, is the default on first key column
  - RANGE sharding is better for range queries
# discuss-pg-utils/crud
- ## 

- ## 

- ## 

- ## 作为个人开发者，效率至上。我现在使用 PostgreSQL + PostgREST，可以省去 99% 的后端编写工作。
- https://x.com/austinit/status/1892222113366286606
- 夸大宣传吧。后端又不只是数据库操作。
- 如果涉及联表查询，多个表数据的同步更新呢？

# discuss
- ## 

- ## 

- ## 

- ## 

- ## How many people use window functions in Postgres
- https://x.com/craigkerstiens/status/1907464058695229598
- I like to describe them as functions that take many rows as input and don’t change the grain of the output, in comparison with aggregate functions.

- Window and Aggregation functions are both amazing, but the learning curve is steep like you suggest. That said, I have delegated a lot of this query writing now to ChatGPT, which given the specific schema and sample data; makes short work of both.

- ## Five hard problems in @PostgreSQL :
- https://x.com/samokhvalov/status/1910512378376224989
  1. LWLock contention of various kinds when various buffers overflow / thresholds exceeded
  2. no simple path to sharding for OLTP
  3. single-threaded processes (eg replication bottlenecks)
  4. partitioning requires a lot of effort
  5. upgrades too

- 2 + 4 is a large part of why we built @niledatabase, Lots of B2B companies are struggling with these.
  - The other was that if you go with DB-per-tenant, there's basically no good ecosystem tools for managing a large herd of DBs across all the operational tasks.

- ## use an underscore to write long numbers for queries. 
- https://x.com/crunchydata/status/1913249228257702329
  - `select * where orders > 1_000_000` ; 
  - This only works for query input though. To get query results with zero separators , use to_char for formatting. 

```sql
SELECT 
   id, 
   customer_name,
   to_char(total_sales, 'FM999,999,999') AS formatted_sales
FROM
  sales
WHERE
  total_sales > 1_000_000;
```

- ## Postgres' ENUM type is a trap.
- https://x.com/gwenshap/status/1918091482898268302 
  - You can’t remove, rename or reorder values. Only way is to drop and recreate the type... which you can’t do if any table is using it.
  - Adding a new value takes a lock.
  - ✅ Better: use a CHECK constraint or a small reference table. You get validation and flexibility without all these gotchas.

- The problem with Postgres Enums is that it’s so limited that there’s really no safe way to use it (unless you are really sure they set of values will never change). The alternatives are more flexible.

- To me domains sit at the proper level of encapsulation of what the constraints of a given field are.

- ## Adding partitions to a Postgres table is a great way to bulk-load data. But you want to add partitions efficiently:
- https://x.com/gwenshap/status/1919465937641865285
  - In Postgres, the right DDL path can make or break your uptime.

- ❌ CREATE TABLE new_partition (...) PARTITION OF parent FOR VALUES (...)
  - Blocks the entire partitioned table with an exclusive lock
  - Not safe for high-write systems
- ✅ ALTER TABLE parent ATTACH PARTITION new_partition FOR VALUES (...)
  - Safe for concurrent inserts and backfills

- Why use ATTACH/DETACH?
  - No downtime
  - Safe data backfill
  - Easy archival and rollbacks
  - Same outcome, smoother ops

- ## [What I Wish Someone Told Me About Postgres _202411](https://challahscript.com/what_i_wish_someone_told_me_about_postgres)

- Normalize your data unless you have a good reason not to
Follow all the advice from the folks that make Postgres
Note some general SQL eccentricities
Saving your pinkies: you don’t have to write SQL in all caps
NULL is weird
You can make psql more useful
Fix your unreadable output
Clarify ambiguous nulls
Use auto-completion
Lean on backslash shortcuts
Copy to a CSV
Use column shorthands and aliases

- It’s possible that adding an index will do nothing (particularly if it’s misconfigured)
What is an index?
An index isn’t much use for a table with barely any rows in it
When indexing multiple columns, the order matters
If doing prefix matches, use text_pattern_ops

- Long-held locks can break your app (even ACCESS SHARE)
What is a lock?
How locks work in Postgres
How this can cause problems
Long-running transactions can be just as bad

- JSONB is a sharp knife
JSONB can be slower than normal columns
JSONB is not as self-documenting as a standard table schema
JSONB Postgres types are a bit awkward to work with

- ## TIL there was an attempt to bring async I/O to PostgreSQL, but unfortunately it didn't pan out
- https://x.com/iavins/status/1869008971551350981

- ## [Common mistakes in PostgreSQL | Hacker News _201905](https://news.ycombinator.com/item?id=19817531)
- There are two ways to built abstractions: 
  - either by defining an interface that represents the lowest-common-denominator of functionality such that all the underlying implementations already implement it; 
  - or by defining the interface that you want to have, where some implementations can implement it directly, and others require a shim/polyfill implementation, 
  - or where the implementation “adapter” will just plain throw a NotImplementedError at your attempt to use the advanced features of the interface.
  - Personally, I prefer the latter. But it seems like in the ORM space the latter approach is nowhere to be found.

- ORMs are great for quickly standing up a database, but if you need advanced features you should probably just use raw SQL. Most ORMs even make this very simple and safe.

- 
- 
- 

- ## 🧐 Each Postgres server can host multiple databases, but be careful! An important note is all databases on the same server share the Write-Ahead Log (WAL)
- https://x.com/qianl_cs/status/1826314526431871476
  - This means if you perform a point-in-time recovery or rollback, it must be done for all databases on the server. So you cannot selectively restore a single database. 
  - Therefore, if you have multiple loosely coupled services each connecting to a separate database, it's better to put them on different Postgres database servers.

- If you have such loosely coupled services that you want them each to have their own Postgres server, it's also worth considering if you even need that infrastructure. Maybe your services would be fine with SQLite or DuckDB.

- ## 最近两天优化了下线上的数据库查询，成功把 pg 的 cpu 利用率从接近 100% 降到 30% 上下，pg 的磁盘 iops 从 1500 上下优化到 30 左右，慢查询也少了很多。
- https://twitter.com/kk1984_/status/1787774865443057748
  - 我之前没做过这方面的优化，只是对数据库有些基本的认识，所以这一路上对我来说还是挺有趣的，分享一些我学到的经验抛砖引玉
  - 如果之前对怎么优化 pg 的查询性能没有经验的话，官方的 Examining Index Usage 跟 Performance Tips 文档值得一读
  - `EXPLAIN (ANALYZE, VERBOSE) <statement>` 对于理解 pg 怎么执行 SQL 很有用，不过设置了 ANALYZE 后，语句会真的执行
  - pg 不支持在查询的时候手动指定用什么索引，只能交给 optimizer 去选择。因此如果想知道在生产环境下 pg 会怎么查询，就得提供同等或相似规模的数据。目前我的做法是利用 AWS RDS 的 restore to point-in-time 功能 ，把当前的数据复制到另一个实例上，然后在这个新实例上做实验。
  - 怎么优化索引得根据 EXPLAIN 给出的 query plan 来。

- ## How much has everyone's favorite open source query optimizer, PostgreSQL, improved over the last 10 years? Turns out, quite a lot!
- https://twitter.com/RyanMarcus/status/1778835012927774732
- i love this! though my unfounded inclination would be that it's more likely the execution engine improved than the optimizer (because it's often easier to find pareto-efficient changes there). would definitely be curious to see this done controlling for various factors

- How much of this improvement do you think come from the more algorithmic side of things? Like better join algorithms etc.
  - I don't think V8 - V16 has any new join algorithms (hash, merge, and loop are in all 3). If I had to guess, I'd say the gains are coming from improved cardinality estimation (better stats, better models) and engine improvements (JIT, parallel workers).

- ## Postgres doesn’t support hints
- https://twitter.com/denismagda/status/1768411154651718087
  - but there is one mighty extension- `pg_hint_plan` - that brings the feature to the database 

- ## i wonder when "PostgresLite" will become a thing
- https://twitter.com/jarredsumner/status/1751967157884432652
  - SQLite's single-file embedded no-server model makes getting started easy, but backends often need a database like Postgres
  - A reasonable alternative is to use SQLite in development and Postgres in production, but that often causes subtle issues. Some queries only work in Postgres. Some queries run very slowly in tests/development. The differences between the two is big enough to matter

- There would be a number of significant technical challenges in adapting Postgres to be single-file, embedded, no-server.
  - The biggest is probably that it currently has a 1:1 relationship between connection and processes. And requests within a request are processed serially. There has been a long standing debate about moving to multi-threaded but they always settle in staying multi-process onto.
  - Last time I scanned the mailing list it sounded like they were pretty determined to give it another go but I don't know how that developed after that.
  - Even if that got working it would almost certainly be more resource heavy than SQLite but that might be a good tradeoff for many use cases.
  - I have thought about what it would take to lift just like the SQL handling stuff, the query planner, on disk record format etc and then bolting that onto something like LMDB but I never got that far with it.

- This is why I think @deno_land created the KV abstraction. Would love to see something similar in Bun.

- Have you seen @tursodatabase ?  They created a fork of SQLite that contains a server mode and replication protocol to help you serve a SQLite database.

- ## How to use subtransactions in Postgres
- https://twitter.com/samokhvalov/status/1719228501658882268
  - TL; DR Don't use subtransactions, unless absolutely necessary.
  - A subtransaction, also known as "nested transaction", is a transaction started by instruction within the scope of an already started transaction 
- As a bottom line:
  - 1. If you can, don't use subtransactions
  - 2. Keep an eye on pgsql-hackers threads related to them and if you can, participate (help test and improve)
  - 3. If absolutely necessary, use them in lower-TPS systems only
  - avoid deep nesting

- ## [Things I hate about PostgreSQL (2020) | Hacker News_202104](https://news.ycombinator.com/item?id=26709019)
- 
- 
- 

- ## [Common mistakes in PostgreSQL | Hacker News_201905](https://news.ycombinator.com/item?id=19817531)
- 
- 
- 
