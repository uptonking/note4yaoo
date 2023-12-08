---
title: lib-db-sql-community
tags: [community, sql]
created: 2023-07-19T10:48:09.951Z
modified: 2023-07-19T10:48:24.003Z
---

# lib-db-sql-community

# guide

# discuss
- ## 

- ## 

- ## TIL: In SQL, looking for "all rows without a specific value" will not include rows containing NULL 
- https://twitter.com/damienalexandre/status/1732391868132913226
  - That's really unexpected behavior on all engines: #mysql, #postgresql...

- The SQL Standard clearly states that 
  1. that the WHERE clause returns all rows for which its predicate evaluates to TRUE. 
  2. that any comparison with NULL evaluates to UNKNOWN, and
  3. that UNKNOWN and TRUE are not the same thing.

- So do you need to use `val != 'crazy' OR val IS NULL` ?
  - Yes, absolutely
- What about NOT IN?
  - Same behavior
- PostgreSQL offers IS DISTINCT FROM

- ## When you are writing SQL queries, remember that the precedence of `OR` operator is different from `AND` operator, just as most programming languages do. 
- https://twitter.com/leiysky/status/1681597163946807296
  - Care of it, or you will be suffered
