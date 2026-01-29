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

- [Explain Plan Visualizer by Datadog](https://explain.datadoghq.com/)
  - Currently for PostgreSQL, MySQL, MSSQL and MongoDB
# discuss-stars
- ## 

- ## 

- ## 

- ## 3-valued logic in SQL was a mistake. 
- https://x.com/julianhyde/status/1928103685059448936
  - Users prefer 2VL, 2VL plans are faster, and most queries give the same results anyway. 
- I decided early on that @morel_lang would use 2VL, and I don’t miss 3VL at all. Not as a user writing queries, and especially not when optimizing queries like NOT IN and converting INTERSECT to a join.

- ## A quick reminder that LIMIT without ORDER BY can produce unpredictable results 
- https://x.com/FranckPachot/status/1881281403528343815
  - it's not a bug but a brilliant @PostgreSQL feature
- what's the default "order by" column? The table's ID column?
  - There's no default. Without ORDER BY, you get rows as they come from the storage, depending on the execution plan, scan optimizations, parallel query, and luck (Relational tables are sets of rows and have no order - ORDER BY is an SQL addition to fetch them sorted)

- Even more funny: use limit with offset. What do you expect to get

- Same as for clickhouse, due to its multi threaded nature if you don't use `ORDER BY` before `LIMIT` you get also  same unpredictable results.

- The same could be said for non-deterministic ordering when no unique column is an element in the order by clause. It’s a cold world.

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

# discuss-sql-favor
- ## 

- ## 

- ## True, but SQL became the universal data access language for apps, with ORMs hiding the complexity. 
- https://x.com/penberg/status/1917594823416242450
  - It’s like POSIX — far from perfect but unlikely to ever get replaced
- You can clearly do better than stitching together bunch of strings to express a query, right? However, that does not matter very much because (1) ORMs generate the strings for you and (2) the string gets compiled into efficient code at statement prepare time.
  - sql over ORM any day. Just adding overhead

- It's like we invented various languages that transpile to JavaScript
  - This doesn’t mean it’s a good idea OR that it should continue though. Just like Rust/C++
# discuss-sql-against
- ## 

- ## 

- ## 

- ## Some people dislike SQL. But I think there are two completely separate reasons. 
- https://twitter.com/eatonphil/status/1742933165130559602
  - (Ignore a third which is just that "declarative languages are weird".)
  01. It's not static/safe enough for app code.
  02. But it's also not even dynamic (or succinct) enough for interactive querying.
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
# discuss-cte(Common Table Expression)
- ## 

- ## 🆚️ CTE vs. Temporal Table: Would temporal tables be faster? 
- https://twitter.com/RaulJuncoV/status/1751286514045092338
  - Use CTEs to make queries easy to read and maintain in non-large datasets.
  - Use Temp Tables for performance optimization with large datasets; they reduce computations.

- CTEs (Common Table Expressions) 
  - CTEs can make complex queries more readable and easier to maintain. 
  - They are excellent for breaking down complex logic into simpler, more manageable parts.
  - CTEs are most efficient for organizing query logic but don't store their results.
  - They act as temporary views executed every time they are referenced.

- Temporal Tables
  - Temp tables come with Performance through Persistence.
  - Temp tables store data in the database's temporary storage (e.g., the tempdb in SQL Server).
  - On Temp tables, you can also define indexes
  - This physical storage and the indexes will make the reads or joins X times faster.

- I love CTEs because of their readability, but the performance on Temp Tables is hard to ignore in large datasets.
# discuss-lang-morel
- ## 

- ## 

- ## 

- ## Data in @morel_lang isn’t always tabular (lists or bags of records) but it often is. So I think it’s time to add a mode so that tables look like tables.
- https://x.com/julianhyde/status/1917030983062458690
- Does @ultorg have a text mode?
  - Ultorg has JSON output or "flattened" CSV for export purposes, though UI interactions are always driven from the graphical nested table layout. I think @jonathoda has a more terminal-like UI for nested relations, though!

# discuss-sql-formats
- ## 

- ## 

- ## [Transpile Any SQL to PostgreSQL Dialect | Hacker News _202403](https://news.ycombinator.com/item?id=39741956)
- 
- 

- Is there any standardized AST for SQL?
  - The SQL standard nominally defines one (I don't know if it hands it to you on a silver platter as some sort of grammar but it certainly defines one one way or another), but if you just implement that and then send your code out into the world, you're going to be disappointed with the results. 
  - All the database have deviations and extensions of their own and people use them frequently.

- 
- 
- 

# discuss
- ## 

- ## 

- ## One major prop to SQL systems is they'll answer any query no matter how complex. NoSQL is like "unless it's a index scan, get lost". 
- https://x.com/matthew_linkous/status/1919743619365265508
  - I much prefer a system that just works from the beginning that you can then optimize than one where you have to come up with query plan first

- ## Top 20 SQL query optimization techniques
- https://x.com/milan_milanovic/status/1808141926907920502
01.  Create an index on huge tables (>1.000.000) rows
02.  Use EXIST() instead of COUNT() to find an element in the table
03.  SELECT fields instead of using SELECT *
04.  Avoid Subqueries in WHERE Clause
05.  Avoid SELECT DISTINCT where possible
06.  Use WHERE Clause instead of HAVING
07.  Create joins with INNER JOIN (not WHERE)
08.  Use LIMIT to sample query results
09.  Use UNION ALL instead of UNION wherever possible
10. Use UNION where instead of WHERE ... or ... query.
11. Run your query during off-peak hours
12. Avoid using OR in join queries
13. Choose GROUP BY over window functions
14. Use derived and temporary tables
15. Drop the index before loading bulk data
16. Use materialized views instead of views
17. Avoid != or <> (not equal) operator
18. Minimize the number of subqueries
19. Use INNER join as little as possible when you can get the same output using LEFT/RIGHT join.
20. Frequently try to use temporary sources to retrieve the same dataset.

- ## Neumann把SQL批判一顿，说SQL语法顺序和语义顺序不一致不利于初学者学习，CTE的抽象不好用不利于数据分析人士使用，SQL越来越复杂要累死数据库开发者了。
- https://twitter.com/DylanGalois/status/1776906328348217387
  - 既然学SQL前要学关系代数，干脆直接写关系代数得了，所有人都开心，于是有了SaneQL。最后出来的东西真像DataFrame API
- SQL 就是上个世纪的东西，浓浓的 COBOL 味, DataFrame API 才是现代编程语言的该有的 style
- 殊途同归嘛，但是 SQL 的功能太丰富了，还是没法被完全替代
- 光批判SQL有啥用，要批判就把数据库一起批判，每个数据库都想着扩充一把SQL，同样一句SQL这个数据库能跑那个数据库没法跑，多数据库并存混用的时候，还得请教多个dba帮着矫正SQL

- ## 👨🏻‍🏫 How Databases Execute SQL Statements?
- https://twitter.com/sahnlam/status/1771407763517898825
  - The process of SQL execution in a database involves several components interacting together. 
  - While the specific architecture can vary between different database systems, the following steps describe a common sequence of operations.

- ## There is currently some fuzz about the performance of  subqueries vs with clause.
- https://twitter.com/SQLPerfTips/status/1770139458265850351

- ## 🐛 SQL does this weird thing too. I wonder what ancient language this comes from
- https://twitter.com/lukaseder/status/1764218716156305624
  - python print(['a', 'b' 'c', 'd']) => ['a', 'bc', 'd']

- ## 💡 dengTIL PRQL - Pipelined Relational Query Language, pronounced “Prequel”. 
- https://twitter.com/iavins/status/1763244325981331782
  - It compiles to SQL and claims that it makes writing complex SQL queries simple and in
- Also worth taking a look at Kusto (kql) from @Microsoft , ES|QL from @elastic and SPL from @splunk
- This is generally a good idea. See this tweet. It's a powerful augment to SQL, without taking away the Recursive expression+value based nature of SQL

- ## 🔍⚡️ Are there any DBs that have an interface to send query plans over the wire rather than SQL? 
- https://twitter.com/criccomini/status/1754198831577841918
  - What I'm thinking is essentially a protobuf of something like a substrait plan.
  - I think everyone agree's it's kind of silly for an app to go from ORM -> SQL text -> wire -> parse SQL -> IR. If the ORM library could just construct an IR from the ORM and send that over, it'd be much more efficient (and more type safe!).
  - This would also open up the ability for LLMs to send IRs instead of SQL
- Vox is below the IR and optimizer. What I’m talking about is farther up the stack—eliminating the parser from the equation and going straight to IR.
- This is similar to our reasoning in TB for zero deserialization. SQL (as a data format) is not the most efficient for massive write ingest.
- You need to access the catalog to interpret the SQL and compile it. It must know the schema, views, access rights, row level security. And these can change. More efficient to do it in the DB. To be typesafe, just use bind variables. To not send SQL text, use stored procedures
- Arrow Flight SQL defines methods for Substrait querying. It is fairly straightforward to implement something like this with DataFusion. I hope others follow. Somewhat related

- Vox is below the IR and optimizer. What I’m talking about is farther up the stack—eliminating the parser from the equation and going straight to IR.

- i think spark connect works that way, it just send unresolved query plan, it does not matter if it is sql or dataframe API, if I understood correctly
- That's essentially what Spark Connect does

- Not exactly the same as what you said.. but for Postgres there is a pg_hint_plan extension which lets you tweak plans by sending comments over the wire…

- Back in the day, we solved this at @SingleStoreDB by using SQL to communicate between nodes in a cluster, which forced us to build all of the internal optimizer controls with good enough UX that users could access them (as query hints).

- We did this to Kudu - which provides a great storage engine, but no query planner or query language. This project: https://github.com/twilio/calcite-kudu was designed to create the query plan and tell kudu to execute it.

- You can usually send hints to the RDBMS, but I don't know of any that let you send a full execution plan. But why would you need that? For most modern RDBMSs it's highly unlikely that you could out perform them, beyond hints and fresh cardinality

- ## [The Unreasonable Effectiveness of SQL - The Couchbase Blog_201904](https://www.couchbase.com/blog/unreasonable-effectiveness-of-sql/)
- SQL has inspired query language design for non-relational databases: SQL for object databases, SQL for object-relational, SQL for XML, SQL for spatial, SQL for search, SQL for JSON, SQL for timeseries, SQL for streams and so on.  Every BI tool interacts with the data using variety of SQL.
- every popular NoSQL databases have a variation of SQL: N1QL in Couchbase, CQL in Cassandra, ElasticSearch SQL in Elastic.
- Now, there are more SQL projects in NOSQL databases than SQL databases.

- ## Exploring the history of SQL 
- https://twitter.com/sspaeti/status/1749447691946340677
  - SQL's journey has been groundbreaking since its 1970s inception as SEQUEL to today's advanced Natural Language Queries.
  - What's your favorite SQL evolution with all these different SQL flavors today?

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
