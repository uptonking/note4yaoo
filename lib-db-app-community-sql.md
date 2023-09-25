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
- My biggest gripe with SQL is the lack of composability. When writing complex code, I can easily pull out functions. When complex writing SQL, I end up with a giant unmaintainable blob. I hope whatever solution you find addresses this!
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

- GQL makes joins much easier to write than SQL, which is what you want to be using in your components. But GQL is not great for offline-support and caching. You want your frontend to know about how your data relates to each other. Your frontend GQL should query a local SQL db.

- 
- 

# discuss
- ## 

- ## 

- ## [SQL is 43 years old – Here’s why we still use it today | Hacker News_201705](https://news.ycombinator.com/item?id=14245354&p=2)
- 
- 
- 

- ## [edgedb: We Can Do Better Than SQL | Hacker News_202008](https://news.ycombinator.com/item?id=24106608)
- 
- 

- [Show HN: EdgeDB 1.0 | Hacker News_202202](https://news.ycombinator.com/item?id=30290225)
  - EdgeQL is designed to replace SQL, not graph query languages. 
  - Think of it as SQL getting a proper type system and GraphQL capabilities of reaching into deep relationships in an ergonomic way.

- SC32 WG3 is developing two related standards to support property graphs:
  1. SQL/PGQ (ISO/IEC JTC1 9075 part 16) -- This adds language to create property graph views on top of existing SQL tables and write property graph queries in a GRAPH_TABLE function in an SQL FROM statement.
  2. GQL (ISO/IEC JTC1 39075 Database Language GQL) -- This is a full declarative property graph database language to create, maintain, and query graphs. This includes support for both descriptive and prescriptive schemas.
  - **The Graph Pattern Matching language is identical between the two standards.**
