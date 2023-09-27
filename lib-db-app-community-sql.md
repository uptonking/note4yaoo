---
title: lib-db-app-community-sql
tags: [community, database, sql]
created: 2023-09-17T17:35:09.069Z
modified: 2023-09-17T17:35:27.024Z
---

# lib-db-app-community-sql

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

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

# discuss-sql-cons
- ## 

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

- ## 

- ## 

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

