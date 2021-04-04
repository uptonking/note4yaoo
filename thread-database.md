---
title: thread-database
tags: [database, thread]
created: '2020-11-22T12:10:09.397Z'
modified: '2021-01-06T14:39:56.358Z'
---

# thread-database

# pieces

- ## 

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

# ref

- [OceanBase的一致性协议为什么选择paxos而不是raft?](https://www.zhihu.com/question/52337912/answers/updated)
