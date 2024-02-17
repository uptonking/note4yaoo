---
title: lib-db-sql-blog
tags: [blog, sql]
created: 2023-03-12T14:41:59.976Z
modified: 2023-03-12T14:42:08.788Z
---

# lib-db-sql-blog

# guide

# blogs

## [DQL、DML、DDL、DCL的概念与区别](https://blog.csdn.net/tomatofly/article/details/5949070)

1974年-----由Boyce和Chamberlin提出，当时称SEQUEL。
1976年-----IBM公司的Sanjase研究所在研制RDBMS SYSTEM R时改为SQL。
1979年-----ORACLE公司发表第一个基于SQL的商业化RDBMS产品。
1982年-----IBM公司出版第一个RDBMS语言SQL/DS。
1985年-----IBM公司出版第一个RDBMS语言DB2。
1986年-----美国国家标准化组织ANSI宣布SQL作为数据库工业标准。

- SQL是一个标准的数据库语言，是面向集合的描述性非过程化语言，简单易学易维护
  - 它是非过程性语言，即大多数语句都是独立执行的，与上下文无关，
  - 而绝大部分应用都是一个完整的过程，显然用SQL完全实现这些功能是很困难的。
  - 所以大多数数据库公司为了解决此问题，作了如下两方面的工作：
  - (1)扩充SQL，在SQL中引入过程性结构；
  - (2)把SQL嵌入到高级语言中，以便一起完成一个完整的应用。

- SQL语言共分为四大类：数据查询语言DQL，数据操纵语言DML，数据定义语言DDL，数据控制语言DCL。

1. 数据查询语言DQL
数据查询语言DQL基本结构是由SELECT子句，FROM子句，WHERE子句组成的查询块：
SELECT <字段名表>
FROM <表或视图名>
WHERE <查询条件>

2. 数据操纵语言DML
数据操纵语言DML主要有三种形式：
1) 插入：INSERT
2) 更新：UPDATE
3) 删除：DELETE

3. 数据定义语言DDL
数据定义语言DDL用来创建数据库中的各种对象-----表、视图、索引、同义词、聚簇等如：
CREATE TABLE/VIEW/INDEX/SYN/CLUSTER
DDL操作是隐性提交的！不能rollback

4. 数据控制语言DCL
数据控制语言DCL用来授予或回收访问数据库的某种特权，并控制数据库操纵事务发生的时间及效果，对数据库实行监视等。如：
1) GRANT：授权。
2) ROLLBACK [WORK] TO [SAVEPOINT]：回退到某一点。
回滚命令使数据库状态回到上次最后提交的状态。其格式为：
SQL>ROLLBACK; 
3) COMMIT [WORK]：提交。
在数据库的插入、删除和修改操作时，只有当事务在提交到数据库时才算完成。
在事务提交前，只有操作数据库的这个人才能有权看到所做的事情，别人只有在最后提交完成后才可以看到。
提交数据有三种类型：显式提交、隐式提交及自动提交。
(1) 显式提交
用COMMIT命令直接完成的提交为显式提交。其格式为：
SQL>COMMIT；

(2) 隐式提交
用SQL命令间接完成的提交为隐式提交。这些命令是：
ALTER，AUDIT，COMMENT，CONNECT，CREATE，DISCONNECT，DROP，
EXIT，GRANT，NOAUDIT，QUIT，REVOKE，RENAME。

(3) 自动提交
若把AUTOCOMMIT设置为ON，则在插入、修改、删除语句执行后，
系统将自动进行提交，这就是自动提交。其格式为：
SQL>SET AUTOCOMMIT ON；

## 🧩 [What Is the `WITH` Clause in SQL?](https://learnsql.com/blog/what-is-with-clause-sql/)

- The WITH clause in SQL was introduced in standard SQL to simplify complex long queries, especially those with JOINs and subqueries. 
  - Often interchangeably called CTE or subquery refactoring, a WITH clause defines a temporary data set whose output is available to be referenced in subsequent queries.
- The WITH clause is considered “temporary” because the result is not permanently stored anywhere in the database schema. 
  - It acts as a temporary view that only exists for the duration of the query
  - It is only valid in the query to which it belongs
- the key advantage of the WITH clause is that it helps organize and simplify long and complex hierarchical queries by breaking them down into smaller, more readable chunks.

- Some common applications of SQL CTE include:
  - Referencing a temporary table multiple times in a single query.
  - Using it as an alternative to creating a view in the database.
  - Performing multi-level aggregations, such as finding the average of maximums.
  - Performing an identical calculation multiple times over within the context of a larger query.
# blogs-query-engine

## 📖 [How Query Engines Work](https://howqueryengineswork.com/)

- [How Query Engines Work by Andy Grove [Leanpub PDF/iPad/Kindle]](https://leanpub.com/how-query-engines-work)

- This book provides an introduction to the high-level concepts behind query engines and walks through all aspects of **building a fully working SQL query engine in `Kotlin`**.
  - 本书的重点是查询引擎设计，它通常与编程语言无关。
  - 本书选择 Kotlin 是因为它简洁易懂。它还与 Java 100% 兼容，这意味着您可以从 Java 和其他基于 Java 的语言（例如 Scala）调用 Kotlin 代码。
  - Apache Arrow项目中的 DataFusion 查询引擎也主要基于本书的设计

### [How Query Engines Work 学习记录](https://frankma.me/posts/database/how-query-engines-work/)

- 可以作为0基础的查询引擎的入门资料，尤其是从RecordBatch定义，到DataSource构建，再到logical plan和physical plan实现，会对查询引擎的基本概念有一定的了解。
  - 但是从SQL Support开始，后面章节的内容过于太generial了，只能做简单了解。
  - 总体来说，还是很适合从0入门的，可以使用自己擅长的语言实现一遍，比如我的golang port
  - https://github.com/Fedomn/how-query-engine-work /go

- 构建查询引擎第一步是，选择一个type system，去代表查询引擎处理的数据类型。
- 查询引擎 需要考虑处理数据的方式：row-by-row 还是 columnar format。
- 现代大多数查询引擎都是基于Volcano Query Planner，它的每个step本质是一个iterator去访问rows。 
  - 它是可以简单实现的模型，但如果处理billions级别的数据时，它的per-row overheads就会体现出来(大量虚函数调用)。
- 减轻overhead的方式，通过iterator over batches of data 来批量处理数据。
- 进一步，如果batch操作的是columnar data而不是rows，就可以利用vectorized processing，即利用SIMD去处理一个column里的多个值，在a single CPU instruction里。
- 这里使用Apache Arrow作为基础的类型系统
- 我们基于arrow的array类型，即用一批columnar的数据，来构造一批rows。减少了per-row overheads(虚函数调用)，利用SIMD提高CPU一个cycle的处理数据量。

- 一个逻辑计划(logical plan) 代表 data transformation or action，它返回一些行数据(a set of tuples)。
  - 每个logical plan都可以有 其它的logical plans作为inputs。
  - 一个逻辑表达式(logical expression) 代表 将要对input logical plan执行的expression，它最后会返回一个具体的数据类型。它是logical plan的基础构建块，在runtime时被执行。

- 将logical和physical plans明显区分开来的原因是：一个logical plan可以存在 多种physical plan去执行operation。
  - 一个physical expression会将input的RecordBatch 进行evaluate，并产生一列数据。
  - physical expression有了后，就可以组装起physical plans。

- distributed query execution介绍如何利用multi-core CPU 和 multi-servers。内容主要都是high level层介绍。

## 👥 [How Query Engines Work | Hacker News_202309](https://news.ycombinator.com/item?id=37415494)

- Apache Arrow could (and hopefully will) really shake up the database industry in the years ahead. Whatever eventually supplants(取代, 代替) Postgres is quite likely going to be based on Arrow - polyglot zero-copy vector processing is the future.
- I don't see the connection. Apache Arrow isn't going to make a b-tree or LSM faster or more efficient. It's not going to make a point look-up query faster against columnar storage, or a range scan faster against row-based storage. It doesn't make distributed quorum faster, or otherwise impact consistency and fault tolerance.
  - Removing or reducing SerDe overhead is great, and for analytical workloads where SerDe can be 30-50% of clock time then something like Apache Arrow is pure magic. For the remaining 9X% of use cases it's not adding any more value then you'd see from protobuf.
- 👉🏻 **I agree Arrow by itself doesn't address any novel/fundamental OLTP challenges**, but I'm not arguing that the thing which eventually supplants Postgres will succeed because of best-in-class OLTP performance - anyone needing that today is not choosing Postgres anyway (same as ever).
  - The real proposition is having a modern, general purpose workhorse underpinned by an ecosystem with strong network effects and polyglot APIs. Assuming analytical systems continue to gravitate towards Arrow I believe the OLTP world will be dragged along also.
# blogs-usecase-N+1

## [数据库查询的N+1问题](https://blog.icehoney.me/posts/2021-02-20-sql-n-1/)

- 举一个简单的例子，数据库中有一张 cars 表存储汽车的相关信息，还有一张 wheels 表存储汽车的轮胎信息。
  - SELECT * FROM cars; 
  - SELECT * FROM wheels WHERE car_id = ${car_id}; 
- 这里的 N 就是汽车的数量，如果需要知道每个汽车的轮胎信息那就正好需要**查询 N+1 次**。

- 如果汽车和轮胎是一对一的关系可以通过使用 `join` 语句来减少数据库查询次数
  - SELECT cars.*, wheels.* FROM cars INNER JOIN wheels ON wheels.car_id = cars.id
  - 把**查询降为1次**。

- 如果汽车和轮胎是一对多的关系可以通过使用 `IN`：
  - SELECT * FROM cars; 
  - SELECT * FROM wheels WHERE wheels.car_id IN (1, 2, 3)
  - 把**查询降为2次**。

- Django 可以使用select-related(opens new window) 和 prefetch-related(opens new window)来解决这个问题。
  - select-related 主要用于一对一的关系，而 prefetch-related 主要用于多对多或者多对一的关系。
- Ruby on Rails 使用 includes(opens new window) 来解决 N+1 问题。

- 后端开发需要时刻注意 N+1 问题， 在开发模式下，日志会输出 SQL 查询语句，需要多加注意。也可以使用一些工具来检测这个问题。

## [[科普文]什么是ORM中的N+1 - 知乎](https://zhuanlan.zhihu.com/p/27323883)

- User和Post是一对多的关系，也就是User是Post的外键。
  - 有一个需求，展示一个文章列表页：文章标题，文章作者名称。就这两个字段，也不需要分页。
- 这个问题并不难，但对于新手而言，可能常常会犯的一个错误就是在循环中进行查询。
- 这样做是非常糟糕的，数据量小还少，在数据量较大的情况下，是非常消耗数据库性能的。
- N+1问题就是这样产生的：查询主表是一次，查询出N 条记录，根据这N 条记录，查询关联的副（从）表，共需要N 次。所以，应该叫1+N 问题更合适一些。

- 其实，如果稍微了解一点SQL，根本不用这么麻烦，直接使用 `IN` 一次就搞定了。

- 对于这类问题，ORM 其实为我们提供了相应的方案，那就是使用『预加载功能』。
  - 使用with()方法指定想要预加载的关联
# more
