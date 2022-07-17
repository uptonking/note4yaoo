---
title: thread-db-orm-sql-nosql
tags: [database, nosql, orm, sql, thread]
created: 2020-11-22T12:10:09.397Z
modified: 2021-05-23T10:17:05.993Z
---

# thread-db-orm-sql-nosql

# discuss

- ## 

- ## how & why #ScyllaDB engineers moved to B-tree & B+-tree data structures for linear search in their #NoSQL distributed database.
- [The Taming of the B-Trees](https://www.scylladb.com/2021/11/23/the-taming-of-the-b-trees/)

- ## Very common mistake in ActiveRecord: checking for the existence of a belongs_to associated record with `present?` or `blank?` . 
- https://twitter.com/nateberkopec/status/1441406828424822792
  - This is an almost-guaranteed N+1. 
  - You have the foreign key on the record you're looking at - just check if the foreign key is `nil?` .
- If you have a situation where the foreign key might be set but the record doesn't exist: fix that problem before it begins, don't defensively code around it here and shoot yourself in the kneecap.
- ActiveRecord does such a strong job auf abstracting the _id away, so it would awesome if it could do that too in these situations…

- ## I honestly just feel kinda embarrassed for people still arguing about ActiveRecord.
- https://twitter.com/taylorotwell/status/1420402348216786950
  - Friendly reminder that no matter how you feel about this Tweet, all of the code you push to GitHub today will be handled by a platform that uses ActiveRecord.
- Writing code vs arguing on Twitter about the best way to write code. I'll take the former
- When there are multiple ways to solve the same problem, arguments and turf wars always keep happening! 
  - Examples: Vim vs Emacs, Linux vs Windows, Ubuntu vs Fedora, PHP vs Python, etc. etc. ActiveRecord vs DataMapper is just another item on the Yin/Yang pattern

- ## Show HN: FaunaDB, a strongly consistent, globally distributed cloud database__201703
- https://news.ycombinator.com/item?id=13879475
- > It’s relational, but not SQL.
  - Why not? If you already support relational algebra, it seems like a non-brainer to just add SQL. Even if it's only SQL-92 you would be able to support some existing tools/ORMs almost for free.
- This is explained a bit in a blog post[1]. Basically, this is because FaunaDB uses Calvin to do distributed transactions, which makes it hard to support OLAP-style SQL sessions. (If I understand the Calvin paper[2] correctly, this has to do with a combination of how it doesn't support "dependent" transactions, and how it does concurrency control.)

- ## Do not generate database tables on the fly
- https://twitter.com/sseraphini/status/1397888359910055940
- it has some use cases tho, when you don't know which entities and columns you gonna store, and you don't want to use JSON/JSONB for all data
  - Just use nosql
  - in the case of where I'm working we probably use sql because we want to store structured/relational data, we just don't know the tables/columns beforehand.they are user defined (mapped from something else)
  - @MongoDB shine on this. you can use a wildcard to even make optimize queries on user defined data

- ## MikroORM: One ORM to rule them all
- https://www.reddit.com/r/node/comments/nia2i5/one_orm_to_rule_them_all/
- Mikro absolutely thrashes TypeORM with its hands tied behind its back. 
  - It even gives Prisma a run for its money as well (I’ve used all three of these in high load applications at scale). 
  - Unit of work is wonderful and “just works” once you properly connect it to your request context.
  - The only thing that was killing me was lack of type safety when calling toJSON(), but that’s already staged for the next release!
- My question is are you able to do everything using an ORM efficiently? Or do you still write complex SQL’s? For my job, we don’t use an ORM, and have basically a long list of a couple hundred stored procedures in Oracle DB to do every task. What are your views on this?
  - Any ORM will give you a “perfect” query for simple stuff, and I’ve found it’s a perfect fit for 95% of queries. 
  - You absolutely have to drop down to pure sql for the more complex queries.
  - Analytics, multi-joined counts, and extremely large where clauses are usually good candidates.
  - Prepared statements are an awesome choice! I’d say that the only downside is that it generally aces your front end devs out of making tweaks to those endpoints, which really depends on how your company operates.
  - One more thing: make sure you’re always checking the cost of your most used queries (something that’s less intuitive on an orm). I’ve been burned on queries that “felt” fast and then got extremely slow once the table had a few million rows.
- TypeORM died when MikroORM came out. The documentation sucks, it's buggy as hell and the type-safety doesn't even come close to what MikroORM offers, let alone all the issues with getting the CLI to work.
  - I wrote a pretty detailed comment on how MikroORM compares to Prisma, using their own selection of features that Prisma advertises against TypeORM, and think MikroORM absolutely holds its own against Prisma.
  - Prisma's main advantages at this point are type-safety, at the cost of flexibility. Since Prisma returns objects, it can use generics in a completely different way, but that also makes it less of a traditional ORM, meaning you can't leverage after-the-fact loading of relations, computed fields, or any sort of business logic in models.
  - MikroORM on the other hand offers nearly the same level of type-safety with helpers like isInitialized(), load(), while still giving you full access to the underlying query builder (KnexJS), entity manager for hydration, and properly leverages DB transactions the way an ORM should.

- ## One of the biggest limitations of a static site is the inability to host a queryable db with it w/o loading the entire db
- https://twitter.com/privatenumbr/status/1389041601494855685
  - Turns out this is actually possible by segmenting a sqlite db into smaller chunks. Very inspiring!

- ## "Hosting SQLite databases on Github Pages" is absolutely brilliant: it adds a virtual filesystem to SQLite-compiled-to-WebAssembly in order to fetch pages from the database using HTTP range requests 
- https://twitter.com/simonw/status/1388933092216164352
  - [Hosting SQLite databases on Github Pages](https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/)
  - Check out this demo: I run the SQL query `select country_code, long_name from wdi_country order by rowid desc limit 100` and it fetches just 54.2KB of new data (across 49 small HTTP requests) to return 100 results - from a statically hosted database file that's 668.8MB!
  - Looks like the core magic here is only around 300 lines of (devastatingly clever) code
  - https://github.com/phiresky/sql.js-httpvfs
- But it does not support updates, right?
  - Of course it can’t write to this file, but a read-only database is still very useful
- I love SQLite but it has it's limitations and if handled improperly it can be a nightmare and even degrade performance & security issues.
  - e.g. not using block SQL transactions will quickly result in read-writes that take millennial(一千年的).
- It used to take me 15 hrs plus to write 10, 000 records to a sqlite file and block commits using transactions reduced that to a few minutes.
  - I used to do a big transaction in sqlite for this, copy the DB file, # pragma synchronized off, write everything, done.
- Are service workers good enough that we can write full stack apps (possibly with @vercel 's NextJs) with SQL + RestAPI + SPA and deploy the whole thing to a CDN?
- We have some fun experiments going with this and actions
  - the hard part is dealing with concurrent actions (and teaching git to diff/merge sqlite) 
  - but the kludgy(不成熟的，蹩脚的) solution of "if push rejected, reset pull and retry" is surprisingly effective
  - Have you got a prototype of git diffing SQLite? That could be fantastic for a whole bunch of my projects. I have a sqlite-diffable thing I've been playing with
  - https://github.com/simonw/sqlite-diffable
  - it works by dumping the DB to plain text (ndjson)
  - ultimately my use-case was append-only, so I went with the retry-upon-failure strategy (which only really matters in case of concurrent action execution). Not elegant but did the trick!

- ## Made my database access about 20x faster (and smaller!) by removing some tables and storing json in sqlite instead. 
- https://twitter.com/steipete/status/1378633040289792009
  - The JSON1 extensions are compiled into iOS and make queries super easy. 
- Worked with a German car manufacturer during my bachelor‘s thesis. We tried many different things to optimize database performance: schema normalization, in-memory search in the app, etc. What helped most with least effort? Installing a freaking indexing plugin for text fields 
- How did you identify those tables and json -> sqlite to make db faster? Analysing db queries processing time?
  - One table had on average 100x more rows than the others 😬
  - And yeah track time in queries
- For most apps we use json files instead of a database. Not possible for all apps but it is waaay faster when it is possible.
  - We have done it even with large data sets. The large bulk could be referenced by an id (= filename) so not generally applicable, but still.
  - We have another app with read/write data sync’ed with backend, everything in json files. Works great. Again, no generally applicable.
- It's not possible to query on JSON values - or is it?
  - SQLite supports partial indexes and indexes on expressions, as ‘big’ DBMSs do. You can build indexes on generated columns and even turn SQLite into a document database.

- ## Declarative data modelling has been the heart of @KeystoneJS from the start, but mapping it to SQL database structure is proper hard. 
- https://twitter.com/JedWatson/status/1369644213067935745
- The balance @prisma have struck with Migrate - auto gen’d sync, with the escape hatch of real SQL when you need it - is a game changer

- ## This is probably why planetscale.com is using MySQL instead of Postgres 
- https://twitter.com/flybayer/status/1368749877044318214
  - [Why Uber Engineering Switched from Postgres to MySQL_201607](https://eng.uber.com/postgres-to-mysql-migration/)
- It would be interesting to know if Postgres architecture is still the same after 5 years since the article. We are thinking of switching from mysql to postgres for better json management
- They're using MySQL because of Vitess planetscale.com/vitessI
  - The article is very old. Postgresql was and is far superior to MySQL in almost every way. 
  - Quite an amateurish article from uber. Or, if I may , done in the Stackoverflow way, written by a person with not much of an academic background. Hey, everyone can be an engineer after all!

- ## Guilty pleasure: I sort of like writing SQL.
- https://twitter.com/BenLesh/status/1364681180021329922
- I enjoy doing a thing akin to SQL Golfing... 
  - where I try to have any report/export being done 100% in SQL 
  - my code is just making the query and sending the result as json
- Yeah, we definitely can't be friends anymore.
- I like how there's not a lot of ambiguity in SQL, 
  - unlike typeof undefined === "undefined" (true) or typeof undefined === undefined (false)
- SQL is beautiful maths with quirky syntax.
- It's algebraic set theory in concrete terms.

- ## [Geode 和 redis 两个分布式内存数据库的对比，优缺点？](https://www.zhihu.com/question/31699176/answers/updated)
  - Geode是分布式内存数据库，提供了可配置的一致性保证，能够保证数据不丢失，更符合数据库的定位。
  - 而Redis的定位本身就是缓存，采用的最终一致性和周期性持久化策略，在单服务进程模型下，提供了高性能缓存服务
  - Geode是java生态圈，有多种运行模式，可以lib方式运行在client端，其支持的客户端语言有限。
  - Redis引擎是C编写，运行更高效，性能损耗低，由于交互协议简单，支持的客户端语言众多，基本上常用的语言都能够支持。
  - 其实这两者的比较不在一个维度上，

    - 一个是应用场景定位，前者更看重数据安全性、后者作为缓存更看重性能；
    - 一个是上手难度，前者上手比较困难，运维起来也会复杂很多，后者上手简单，集群化方案也比前者简单；
    - 从社区活跃度方面来看，前者社区不怎么活跃，DB-ENGINES在kv存储中排名23， 后者社区活跃，应用广泛，在kv存储中排名第1。

  - 准确的说，Geode不是内存数据库(In-Memory DataBase, IMDB)，而是有数据库功能的内存数据网格（In-Memory Data Grid, IMDG）。

    - 在CAP原理下，Geode可以保证集群内数据的强一致性，注意是真正的强一致性而不是最终一致性，再加上分区可用性，因此是一个CP型的产品，可以提供统一的数据视图，支持高并发下的acid事务。
    - 而Redis是不保证一致性的，因此即使Redis集群，也只能是AP型产品。
    - 另外Geode还有内置的pub/sub，逻辑分组和管理监控等一系列企业级产品功能，因为Geode项目本身就是Pivotal公司把十几年历史的及其成熟的GemFire开源贡献给Apache的顶级项目。

- ## [ObjectiveSQL: 让Java更像SQL](https://www.v2ex.com/t/727939)
- 到底是让Java像SQL一样编程，还是让SQL像Java一样编程，纠结了很久，还是让Java更像SQL，
  - Java的语法表现力不够，只能扩展Javac，实现了算法运算，比较运算，逻辑运算符重载，并封装了常用数据的的函数，抽象了Expression，使Java非常接近SQL，
  - 同时也实现了简单SQL编程的代码生成，基本不需要写代码，也不需要配置就能实现简单SQL的编程
- 我对比过mybatis的 `DynamicSQLBuilder` ，它做的太土了，大都数都是以字符串的形式体现，我的改进有三块：
  1. 动态代码生成：模型中的所有字段都会被动态生成一个Order的内部类Table中的字段。
  2. 算术运算、比较运算符和逻辑运算重载，也就是说Java中的 +, -, * / , >, <, &&, || 都会转换成SQL语句中的表达式，
  3. 我封装了常用数据库的常用函数，例如：count, sum等有上千个的，这样就不会出现字符
  - 上述做法的好处是，最大程度的避免的SQL的语法错误，动态代码提示和单元测试。

- ## Is there an IndexedDB equivalent for Node.js?
- https://www.reddit.com/r/javascript/comments/4ohy5t/is_there_an_indexeddb_equivalent_for_nodejs/
  - IndexedDB is a good thing inside browsers, but I wonder why isn't such a thing not available for Node. JS? 
- https://github.com/bigeasy/indexeddb
  - A pure Node.js implementation of the async W3C Index DB API.
- The reason something like that doesn't exist on the BE is that for size that small you can load it fully into memory, as such it is easier to just use a JSON file for persistence.
  - For larger dataset without a server there are BerkeleyDB, LevelDB, and KyotoCabinet. 
  - However, those are generally designed to be database backends rather than used directly by applications. 
  - For larger data sets, you really should use a database of sort, as they would manage what is kept in memory and what is left on the disk.

# ref
- [OceanBase的一致性协议为什么选择paxos而不是raft?](https://www.zhihu.com/question/52337912/answers/updated)
