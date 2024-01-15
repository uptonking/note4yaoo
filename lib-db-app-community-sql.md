---
title: lib-db-app-community-sql
tags: [community, database, sql]
created: 2023-09-17T17:35:09.069Z
modified: 2023-09-17T17:35:27.024Z
---

# lib-db-app-community-sql

# guide

- sql-pros
  - standardized and stable

- sql-cons
  - not good at recursive query
  - 无法提供excel计算所需要的细粒度缓存和依赖管理 won’t do smart caching and dependency management for the cache
# discuss-stars
- ## 

- ## 

- ## Ever struggled to find if a database supports a particular SQL syntax? 
- https://twitter.com/ohmypy/status/1735275704001196175
  - Or maybe you wanted to compare two DB engines for certain SQL features?
  - Then you might find the SQL Polyglot useful. Write a query and see it run in multiple DBMSs, in your browser!
  - [SQL Polyglot](https://codapi.org/sql/)

- Do you do any translation behind the scenes or is the query ran as-is in all of the selected engines?
  - The query is ran as is, without any kind of preprocessing.

- ## One thing I think a lot: what would replace SQL? 
- https://twitter.com/mengxilu/status/1337968087618834432
  - Not some no-code UX that complies to SQL, but a new paradigm that is still low-level enough to be adopted by the whole ecosystem, what would that look like?

- A supercharged Excel should do it

- I think the future is more a no-code like framework around SQL to auto generate SQL for you, similar to how Looker does this for data visualization.

- If anyone’s ever written Linq in .net I suspect it might be something similar. Abstracted declarative query language.

- You know how initially SQL was meant to be the "language for executives" that was close enough to natural language to make it easy to query for business-related answers. In the end, Excel nailed this vision. Nothing has yet to beat it.
  - Well except people have written excel as an interface into SQL native systems for data larger than classic excel can handle

- Datomic is the model for the future.
  - It's built around datalog, which is strictly more powerful than SQL (basically SQL+recursion, making it esp useful for graph data).
  - It also features pull queries, which are more or less isomorphic to (and predate) graphql (+recursion).
  - It's also more flexible than SQL from a data modeling perspective, as it's based on some of the good parts of the semantic web (RDF; EAV triple store). Practically, this makes it much easier to define polymorphic relationships, and more robust/growable schema.
  - If that's not enough, it has super powers, like time travel (give me a database at time t, and run this query on it) and speculative writes (what would the world look like if I ran this transaction (without actually transacting)).

- ## 🤔 What database has the best query language that’s not sql?
- https://twitter.com/aboodman/status/1607790827996327936
- tinybase > tinyQL
- I think graphQL occupies a pretty useful and pragmatic niche.
  - SQL suffers from cartesianification. Results are a square tabular matrix, which does not effeciently express heirarchical data. Probably graphQL tree shaped results actually fits app data better.
- i’m biased (due to previous employment), but definitely think neo4j and cypher is the answer you’re looking for!  ASCII art ftw!  
- Vertipaq with DAX language
- #datomic's #datalog is very intuitive if all you need are inner joins, which is just unification of variables. The minute you need anything else, things get ugly. Uglier than SQL? Who knows, pick your poison.
- Kusto Query Language (KQL), used by Azure Data Explorer and other Azure products. I'm a skeptic when it comes to query languages and DSLs and yet... KQL is awesome IMO
- Malloy fixes my vote for SQLs biggest flaw — combining entity relationships with querying. Malloy separates them, which is genius, especially for ML
- EdgeDB is an open-source database designed as a spiritual successor to SQL and the relational paradigm
- **My biggest gripe with SQL is the lack of composability**. When writing complex code, I can easily pull out functions. When complex writing SQL, I end up with a giant unmaintainable blob. I hope whatever solution you find addresses this!
- @perplexity_ai ‘s birdsql. Query in natural language (English), GPT figures out the sql. Hot take: natural language is the best query language.

# discuss-sql-against
- ## 

- ## 

- ## 

- ## Some people dislike SQL. But I think there are two completely separate reasons. 
- https://twitter.com/eatonphil/status/1742933165130559602
  - (Ignore a third which is just that "declarative languages are weird".)
  1. It's not static/safe enough for app code.
  2. But it's also not even dynamic (or succinct) enough for interactive querying.
  - Most people I see commenting about SQL are focused on the first point.
  - That said, for interactive queries, being too dynamic can be a problem too. SQLite's syntax is TOO flexible for my liking. Too often it lets me write a nonsense query and returns confusing results.

- Not sure if I understood the second point. I think for me the point that makes me like a lot MongoDB is that Atlas Compass has that interactive Aggregation tab that show  the data that you will receive from the aggregation while you are editing the query. Wish had that for SQL

- I like SQL for one-shot analysis queries but really don't like embedding SQL in whichever language I'm using for app building. 

- As a full language SQL lacks composability.
  - As a syntax, it's hard to generate. What would a JSON or S Expression querying language look like? no more ORMs
  - Still, I think in SQL. I can't conceive of using RDBMS without it. Someone can, not me.

- ## [A Short Story About SQL’s Biggest Rival | Hacker News_202010](https://news.ycombinator.com/item?id=24730713)
- 
- 
- 

- ## [Against SQL | Hacker News_202107](https://news.ycombinator.com/item?id=27791539)
- 
- 

- **GQL makes joins much easier to write than SQL**, which is what you want to be using in your components. But **GQL is not great for offline-support and caching**. You want your frontend to know about how your data relates to each other. Your frontend GQL should query a local SQL db.

- 
- 

# discuss
- ## 

- ## 一直热衷于分布式、程序性能、缓存这些时髦内容，然而往往 SQL 都写不清楚，基本的 SQL 优化常识都没有
- https://twitter.com/im2gua/status/1746688523061920203
- 所以我们一般不允许程序员去碰数据库，涉及到数据存取的都是特定几个人来写，其他人提交申请。
- 现在越来越多的业务逻辑都是在app层面, 数据库就是纯粹存个数据, 非常容易scale up

- ## History of SQL: SQL -> Data Mart -> Materialized View -> OLAP Cube -> dbt tables -> One Big/Wide/Super Table -> Semantic Layer
- https://twitter.com/sspaeti/status/1734610175020167334

- ##  `SELECT *` can have many problems, but by far I think the worst is unpredictability. 
- https://twitter.com/hnasr/status/1726602781815955467
  - However, later the admin decided to add an XML field, JSON, blob and other fields that are populated and used by other apps
  - it will suddenly slow down because it is now picking up all the extra fields that your app didn’t need to begin with.
  - [How Slow is SELECT \* ? (A deep dive) | by Hussein Nasser | Medium](https://medium.com/@hnasr/how-slow-is-select-8d4308ca1f0c)
- TLDR is: You should NEVER use it while coding. Use it only if you want to manually browse a database via the command line and probably in the end of the statement you will want to add a "limit 1" (just in case) 

- ## “ansi sql standard” 
- https://twitter.com/Captaintobs/status/1720881752238166412
- Dialects where 1 / 2 yields 0.5:
  •BigQuery
  •ClickHouse
  •DataBricks / Spark
  •DuckDB
  •Hive
  •MySQL
  •Oracle
  •Snowflake
- Dialects where 1 / 2 yields 0:
  •Drill
  •Postgres
  •Presto/Trino
  •Redshift
  •SQLite
  •Teradata
  •T-SQL
- One of the things that PRQL standarizes, with `/` & `//`
- funny, in substrait 1/2 is 0
  - it’s still very early and I think the output will still depend on how a given consumer (backend) interprets and executed the plan — the intent is a standard IR various SQL dialects, Python dataframe APIs, and other DSLs (PRQL, Malloy, dplyr, etc) can produce

- Do a post about datetime conversion

- ## Sometimes you want to get e.g. the last three orders for *every* customer. 
- https://twitter.com/tobias_petry/status/1719811788441538645
  - Regular joins can't do that. You have to execute n+1 queries in code, which is slow!
  - But with lateral joins, you can do a for-each loop join in SQL
  - [For each loops with LATERAL Joins - Database Tip](https://sqlfordevs.com/for-each-loop-lateral-join)
- Is it possible in SQLite or there’s an alternative?
  - SQLite doesn‘t have lateral joins. But n+1 queries are no performance problem with SQLite as it is running within your app and no network calls are needed.
  - For that specific example I would check Window functions. You can use "partition by" to divide a table by a value, eg. CustomerID. Then it will be easy to retrieve what you need.

- ## I'm considering submitting a talk for @DataCouncilAI (April in Austin, TX) talking about different paradigms for query languages. What would be interesting to cover? 
- https://twitter.com/julianhyde/status/1717283455074259318
  - Paradigms include relational algebra (SQL + Pig); relational calculus (Datalog); deductive & graph; analytic (DAX, MDX); constraint programming; builders (Cascading, Flink, Spark); and data frames.
  - In my work on @morel_lang I've noticed that the algebra, calculus and constraint-programming paradigms fit together quite nicely; and my work on measures is unifying SQL with analytic languages.
- How do you see constraint programming fitting in? In the past, I prototyped a way to convert a SQL schema into constraints
  - In Morel you can iterate over data types, e.g. 'from i, j where i > 0 andalso i < j andalso j < 10'. Even though the extents are infinite, constraints create a finite result.

- ## Never underestimate the power of SQL. We tried everything: more memory, parallel processing, optimized queries, but nothing worked.
- https://twitter.com/RaulJuncoV/status/1712824571202596912
  - SQL `MERGE` was more than a fix; it changed how we handle the data.
- Requirements:
  - Users need to upload the data.
  - Compare and avoid duplications.
  - Delete not matching records.
- We used upsert in Postgres. Now, Postgres 16 introduced Merge
- The biggest change was performance since almost all the processing was moved to the DB. Also, the time taken to INSERT and UPDATE records was reduced significantly as it condensed multiple operations into a single statement.
- I have need to synchronize two tables in two DB many times. The idea is doing like a Merge. The order of the operations is critically important when you do it manually.

- ## SQL 只要涉及计算，要么不好写，要么性能差。
- https://twitter.com/ruanyf/status/1712408004031840521
- 不用这么麻烦，postgres 内嵌python，plsql 也能简单数据处理
- CQRS啊，写入和读取分离。
- 第一反应还是 map + reduce 一把梭
- SQL又臭又长、无法调试，简直反人类。还是map+reduce香，有没有人能把map+reduce编译成存储过程的，那就爽了。
- 以前也讨厌sql，但是自从见识了elasticsearch和databrick的query后发现还是sql容易理解，然后es和databrick都增加了sql query的支持。
  - 后来想了一下，主要是因为sql是很严谨的建立在一套数学理论（关系代数）基础上的。
- 大数据程序员基本操作，各种开窗，session就解决了
- 开发总把db当作黑盒，结果就是一堆垃圾sql

- ## [SQL:2023 is finished: Here is what's new | Hacker News_202304](https://news.ycombinator.com/item?id=35562430)
- I don't believe that adding property graph support to SQL makes much of a difference for SQL and relational databases...
  - However, the PG query additions (I believe they are close to the Cypher language neo4j) being part of the SQL standard will give a boost to marketing and adoption of PG databases. 
  - Vendors can now say "our language follows the SQL standard" instead of referencing cypher and indirectly neo4j. Even if neo4j may have the best intentions, marketing is very important in databases and it is unlikely that vendors could have supported Cypher and thus admit that they are following neo4j rather than leading.
- I think SQL/PGQ have the potential to outright kill the whole field of PG databases (if/once existing databases actually start implementing it).
  - The big marketing claim of Neo4J & friends has always been that they make graph queries possible, with a big portion of that claim being that those queries would be intractable for RDBMs performance-wise.
  - With SQL/PGQ it becomes quite apparent that there is next to no magic sauce in PG databases and that it's all just syntactic sugar on top of node/vertex tables. All the rest of their query plans looks 1:1 what you'll find in a RDBMs. Now that they are on a level playing field query syntax-wise, PG databases will have to compete against RDBMs with a lot more advanced query optimizers, better administrative tooling etc..
- This is my expectation as well. At CIDR this year there was a paper that presented an implementation of SQL/PGQ in DuckDB, and it outperforms Neo4J in a few selected benchmarks

- In relational databases, the property graph queries can be really effective to write authorization queries.

- Cypher has built-in support for traversing relationships between nodes in a graph, which can be more intuitive and efficient than using SQL to join tables.

- Is there a competing query strategy, technology, or approach to compete with SQL? Yes, it gets the job done but it's always felt kludgy.
  - I really like what PRQL is doing. Fixes a lot of the unfortunate SQL syntax.
  - The syntax looks very similar to Microsoft's Kusto Query Language (KQL)
  - There are some ideas based on Datalog
  - I've written quite a bit about a new query language called Malloy

- ## [SQL is 43 years old – Here’s why we still use it today | Hacker News_201705](https://news.ycombinator.com/item?id=14245354&p=2)
- 
- 
- 

- ## [edgedb: We Can Do Better Than SQL | Hacker News_202008](https://news.ycombinator.com/item?id=24106608)
- Yes, SQL has flaws, and the article forgot to mention one of them: you need to build a string to build an SQL query, rather than a more structured object, leading to flaws like SQL injection vulnerabilities, and difficulties adjusting the query.
  - Doing it correctly is not just a matter of using SQL parameters, because column names need to be escaped differently than string literals. Linters can't distinguish between correctly escaped queries and incorrectly escape queries in non-trivial cases. Also, the query will throw a syntax error if the number of filters is zero, since you can't have an empty WHERE clause.

- While Datalog is really cool and my PhD research is based on it, the fixpoint semantics really do not work well with aggregation, grouping, etc.
  - fixpoint定义 f(x) = x 时x的值
