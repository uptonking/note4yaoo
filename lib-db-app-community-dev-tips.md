---
title: lib-db-app-community-dev-tips
tags: [community, database-design]
created: 2023-10-27T09:17:03.711Z
modified: 2023-11-07T16:47:11.499Z
---

# lib-db-app-community-dev-tips

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️🧩 Databases are not intended for storing data but for storing relationships. Relationships are what make Entities worthy.
- https://twitter.com/deisbel/status/1762864820049600840
  - Your main goal in designing databases is to identify Entities and Relationships between them.
  - I show here the types of Relationships and how to store them.
- There are 3 types of relationships in Relational Databases:
  - 1- One to one
  - 2- One to many
  - 3- Many to many
- 1- One to one
  - The way to store this relationship type is by adding the key of one of the Entities into the other.
  - You can store this relationship in any of the table
- 2- One to many
  - The way to store this relationship type is by adding the key of Entities on the side One into the Entity of the side Many. 
  - There is only one possible way.
- 3- Many to many
  - This type of relationship needs to create an extra table for storing it. 
  - You will name the table at your convenience using a meaningful name for the relation. 
  - The table must contain the key from each table.
  - You can also add extra data you want to consider for that relationship, like the maximum number of hours to be used.
  - AssignedComputers(StudentId, ComputerId, MaxHoursToUse)

- Relational databases can model almost everything, but in some cases other kind of databases can fit better.
  - Right, the type and the frequency of the changes are key points in many decisions.

- ## 🔥🔥 [When your data doesn’t fit in memory: the basic techniques | Hacker News_201911](https://news.ycombinator.com/item?id=21508542)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 💡 5 strategies to design a high-performance read-heavy system.
- https://twitter.com/ProgressiveCod2/status/1759845363450859525
  - There's a 91.5% chance you'll work on a read-heavy system.
  - Systems where a majority of requests involve fetching from a data source.

- [1] Database Indexing
  - Create proper indexes for your tables.
  - A good index allows your database to quickly locate rows that match a given query.
- [2] Database Replication (Read Replicas)
  - Create read replicas of your database.
  - These replicas are copies of the primary database that can handle read requests.
  - With more replicas, you can distribute read requests and improve performance.
- [3] Caching
  - Caching is great for read-heavy systems where the data doesn’t change much after creation.
  - A good caching strategy can reduce the load on your database.
  - Look at caching solutions like Redis or Memcached for fast in-memory storage.
- [4] Content Delivery Networks
  - Take caching to the next level by investing in a CDN.
  - With a CDN, you can cache and serve static content closer to the end users and reduce read latency.
- [5] Load Balancing
  - You can spin up multiple replicas, cache instances, or servers to handle the reads.
  - But you also need to ensure fair distribution of traffic between these instances.
  - To do so, implement load balancing.

- ## Tips for going deep on databases:
- https://twitter.com/jorandirkgreef/status/1756165626517709004
  - 1. Pick a conference, like FAST (nice because it’s less DBMS and more focused on the broader hardware/software interactions) and follow the papers/talks from there each year. They might not make sense. Keep chewing the cud.
  - 2. A DBMS at heart is a filesystem with a different interface/workload. Therefore, see what you can learn from filesystems, especially ZFS.

- I like your 2nd point because I was reading the Sqlite implementation book and about halfway through it, it hit me I was reading almost similar ideas to what I read in the Practical File System book.

- ## 数据库表字段命名的时候，请一定要用 snake_case 千万不要用 CamelCase/camelCase。踩了个大坑
- https://twitter.com/mayneyao/status/1749974517123002680
  - [数据库表字段命名踩坑](https://eidos.ink/eidos/185b322fca39472da1e16f9509897003)
  - 只看结论版：数据库表字段命名的时候，请一定要用 snake_case 千万不要用 CamelCase/camelCase

- 我正在构建 Eidos，一个完全运行在浏览器环境的本地版 Notion。
- 在选择工具时候有了很多限制，比如类似 prisma 这种为 nodejs 设计的 ORM 工具，不太方便在浏览器中跑起来。
  - ORM 基本都是给后端准备的，对于 eidos 这种把后端跑在浏览器 worker 里面的场景，估计都没有能适配的
  - 因此最开始技术选型是不使用 ORM，自己写 sql 维护表结构。在 eidos 中，分为 2 种类型的表，eidos__ 开头是 meta 表，就是程序运行的关键，还有一种是用户建立的多维表，tb_ 开头。
- 数据库表很难在一次性就设计完美，经验老道的程序员可以未雨绸缪，但是我显然不在此列。随着业务的发展，添加新字段是在所难免的。
- 基本上每种后端语言都会有对应的 ORM 工具，简化数据库操作和变更。ORM 通常也提供 migration 能力
- eidos 没有使用 ORM，因此这部分依然是自己实现的。
  - 原理也很简单，新建一个 draft 的数据库，把新的 sql schema 重放一遍，然后对比新旧数据库表的差异，做增删和变更。这个方案轻量且实用。
- 一般来说在设计表时，基本都会带上简单的审计字段。created/updated at/by 这种。但是我一开始没有添加这些字段。刚好最近有需求了，于是打算如法炮制，直接加上这些字段。
- 但是这个时候 migrator 工作失败了。 报错如下：Cannot add a column with non-constant default
  - 坑点来了。 pgsql-ast-parser 生成的 sql 会把字段名全部转化为小写。

- ## Ten “false” things you will hear about Databases: (unordered)
- https://twitter.com/thegeeknarrator/status/1740500651233194192
  1) SQL databases don’t scale.
  2) Consistency in ACID == Consistency in CAP
  3) Availability in CAP refers to “High Availability” 
  4) NoSQL databases don’t use B-Trees
  5) All databases use Write Ahead Logging.
  6) Full table scans are always bad. 
  7) Data Modelling is not related to query performance.
  8) Horizontally scalable databases can support unlimited concurrency.
  9) Indexing has no side effects. 
  10) Databases can only run on expensive hardware. 

- I have a question about WAL. Which databases doesn’t use WAL and guarantee consistency of its on-disk data?
  - LMDB does not use a WAL but uses Append only BTrees. 
  - VictoriaMetrics also does not have a WAL but they tradeoff durability in failure scenarios. 
  - Since it is time series data it is ok to lose data worth 1sec in rare scenarios. 
  - I am not entirely sure but I have heard CouchDB also uses Append only Btrees? But please confirm.
- My point is that - there is no way you can guarantee ACID - if you end up doing more than two calls into FS. There is no way. You need to first write your intent (either in separate file or in per-node log of a tree in B-epsilon tree) somewhere.
  - More than one call, I meant to say. One single call to insert a node into B+ Tree can lead to split of a leaf node - which will be more than one call into different logical offsets of that B+ Tree file on the file system. So, you describe your split in WAL first, and then do whatever the number of FS calls to carry out that split. Now without WAL, how do you ensure integrity of your B+Tree structure on disk?
  - Even when we say - LMDB or some other type of DBs don’t use WAL on single file, but they still write their intent somewhere — in nodes. So, in a way, this is still kind of WAL records being distributed, instead of being appended to a single WAL file.

- ## These are the 8 design rules you must learn to break.
- https://twitter.com/deisbel/status/1736437854459273278
  1- You can have some data redundancy and denormalization to make queries faster.
  2- You can have some nullable columns instead of having extra tables and joins.
  3- You can miss some unique keys instead of defining all of them.
  4- You can ignore some indexes instead of defining all of them.
  5- You can have simple String columns containing a list of comma-separated values instead of extra tables, indexes, and relations.
  6- You can use a simple String column to store serialized JSON objects instead of having extra tables and columns.
  7- You can add hard-coded data manually or through a simple script instead of creating a UI to manage them.
  8- You can enforce the business rules at the DB layer instead of doing it on the Business or Application layer.
- Do not get obsessed with the perfect model; start breaking the rules and making smart decisions on demand.

- ## What happens when a database crashes while its in a middle of a transaction sent from a backend server?
- https://twitter.com/hnasr/status/1736064842883342482

- So little context. But typically that transaction is either not committed, it might be rolled back or the transaction is logged and thus will be applied once it's back.
- What if it is logged for later. does back end throws error in this case?
  - Depends. Generally speaking it will return an error, otherwise it will lead to data inconsistencies. This is also where database transactions come in to help you counter these situations.

- I worked with postgres a lot, this is how it plays out on postgres. 
  - postgres tracks transaction numbers based on the latest reported transaction by the threads.. each thread when it gets a query, starts its journey picks up a transaction ID from the transaction manager.. that is its view of the world .. numbers that are greater than itself are ignored.. same with writes - depending on what was committed to the transaction manager and what was written to the WAL you will be able to get that back.. anything that was written but not committed will be lost because the data will exist physically on the disk but no transaction will recognize it because it wasn't committed.. on startup it generally will be able to handle and cleanup some of the transactions that were pending and periodically move the data from the WAL file to the base directories where the data should live..
  - if you were doing some external two phase (to external dbs etc.) transactions..  those will still remain open even after restarting your db and will keep holding that transaction ID as open for that table.. if you dont clean it up, for a long time and your table is very busy.. you'll can reach wrap around - because transaction numbers go in a circle.. there are protections in place for this.. but the risk is if the number that is kept open and the current number running of the current transaction loops all the way, you could lose all your data on the table.. the data will still be there on your disk but because the transaction numbers have wrapped around it will look like the older data is future data and will not be read by the table..

- Database uses wal, so restart time it clear it up. Response to the client would be timeout error. However in distributed database, it would be more interesting because follower node needs to clean up their wal as well.

- Databases have Write Ahead Logs (WALs) which are used in logging transactions. Transactions are ACID, they complete totally or fail. So, I think the transaction will not complete but there will be a WAL entry for it if it's a write to the DB.

- I think
  - Server side: The server will receive a transaction timeout error and then will keep trying to connect to the db until the HTTP request times out.
  - DB side: When the db comes back online it'll read the wal and rollback any uncommitted transactions.

- short answer: When a DB crashes mid-transaction, the DBMS checks the transaction log on restart. It either rolls back uncommitted changes or rolls forward committed ones.

- 2 things - transaction logs which helps undo the changes & rollback segments which stores the previous state of the data. When server restarts it will automatic recovery based on these and undo all the uncommited transactions.

- This can depend on many factors:
  - If high availability is set or not
  - if backend waits for acknowledgement from db if the transaction is committed or not
  - if the sequence of transactions is important or not
  - app architecture

- ## Data Engineering Anti patterns
- https://twitter.com/Ubunta/status/1724771152860741748
  - Overkill: A data warehouse for tiny public datasets.
  - One-offs: Data pipelines for yearly tasks.
  - Misjudged Scale: Treating under 50Gb as big data.
  - Underestimation: Overlooking Postgres/MySQL's capacity
  - Neglecting CSV->strict schema conversion

- ## 🔥🔥 [Show HN: I wrote a free eBook about many lesser-known/secret database tricks | Hacker News_202212](https://news.ycombinator.com/item?id=33833836)
- 
- 
- 

- ## 🔥 [Mistakes Beginners Make When Working with Databases | Hacker News_201606](https://news.ycombinator.com/item?id=11862723)
- 
- 

- ## 🔥 [Database development mistakes made by application developers | Hacker News_201012](https://news.ycombinator.com/item?id=1999874)
- 
- 
- 

- ## 🔥 [Three things you should never put in your database | Hacker News_201205](https://news.ycombinator.com/item?id=3916497)
- 
- 
- 

- ## 🔥 [Two common mistakes when using databases | Hacker News_200910](https://news.ycombinator.com/item?id=865695)
- A well thought-out post and a good read, but both of the author's points about the limitations of relational databases are a little misleading.
  - The first, "Every single element in a relation (aka table) has to be exactly the same type" is true in many relational databases, but isn't necessary: SQLite, for example, is implemented with a nice form of dynamic typing where individual columns can take on multiple data types.
  - Second, "SQL isn't even Turing-complete" is sort of a folk theorem in computer science that isn't necessarily true anymore, especially with all of the proprietary SQL dialects in existence: the original standard, SQL92, is basically equivalent to relational algebra, which has the expressive power of first-order logic - it's so weak it can't even express concepts like graph reachability. But constructs like recursive queries have been added to the SQL standard since SQL92 which may make even standard SQL Turing Complete.
- PL/SQL and T-SQL are certainly Turing complete.
  - Oracle's SQL is by itself Turing complete since the introduction of the "Model" clause 

- For beginners, this is definitely good advice. Particularly the first point - if you're using a relational database, and don't structure your data around its strengths, you'll take a profound performance hit. And sure, don't pass around data structures if you don't know what you're doing, and MySQL is a pretty crummy place to put them.
  - However, once you're doing real work, sometimes translating to XML and back is extraordinarily expensive.
  - The best approach is a hybrid. Use the database to store things relationally if possible, and using defined APIs for sure. 
  - And if your translation stage is expensive, use something like memcached to make sure you do that translation as infrequently as possible. _This_ is the layer that it's appropriate to store serialized data structures at. It's not permanent storage, you can blow it away when you change the internal structures, and nobody external is relying on it. 
  - But you end up, in most programs, with even more speed benefits than if you'd stored it in the database like this to begin with - the initial build can be expensive, but then you're reading basically from memory. (Not all data is well suited to this approach, but if your data is read frequently and written to infrequently - there's few things you can do to increase performance more than this.)
