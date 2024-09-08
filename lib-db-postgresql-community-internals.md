---
title: lib-db-postgresql-community-internals
tags: [codebase, community, database, internals, postgresql]
created: 2023-10-28T13:45:28.278Z
modified: 2023-10-28T13:46:14.957Z
---

# lib-db-postgresql-community-internals

# guide

# discuss-stars
- ## 

- ## 

- ## How does Postgres decide when to use an index? Depends.
- https://twitter.com/denismagda/status/1778445306662723747

- ## Postgres is an amazing database. It’s only significant weakness now is in Materialized views, with their lack of incremental refresh._202207
- https://news.ycombinator.com/item?id=32097663
  - Was disappointing to see there was no progress towards this in v15.
- That work towards incrementally updated views is happening and progressing. 
  - For now, it's a separate extension, though: https://github.com/sraoss/pg_ivm
- I wanted incremental refresh in Postgres as well and found that you can manage your own table to get something close.
  - Basically you create a regular table in place of a materialised one, only aggregate data newer than what's currently in the table then store the new aggregates in table. Repeat this an interval.
- Interestingly, DBT does not support creating materialized views.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Like most databases, Postgres work with fixed size pages. 
- https://x.com/hnasr/status/1832071246051446991
  - Those pages are 8K in size, each page will have the rows, or index tuples and a fixed header. The pages are just bytes in files and they are read and cached in the buffer pool.
  - If a table has 100 pages, to do a full table scan, we would be making close to 100 system read calls, taking kernel read-ahead in to consideration. 
  - Postgres 17 now combines I/Os to retrieve multiple pages at once. This leads to fewer system calls and lower read latency.

- ## Postgres code has this habit of making some code 1-based indexed and some 0-based indexed.
- https://twitter.com/eatonphil/status/1725572175292158096
  - For example, in a query: to find the relation (table, in simple cases) being referred to, you get a 1-based index. To look up that relation in the list of relations it's 0-based.
- I'm still not used to Postgres arrays being 1-based.

- ## [Unexpected downsides of UUID keys in PostgreSQL | Hacker News_202306](https://news.ycombinator.com/item?id=36429986)
- CouchDB uses sequential UUID by default
  - the choice of UUID has a significant impact on the layout of the B-tree, prior to compaction.

- 
- 
- 

- ## 🔥 [Get PostgreSQL Database Structure as a Detailed JavaScript Object | Hacker News_201912](https://news.ycombinator.com/item?id=21714500)
- 
- 
- 
