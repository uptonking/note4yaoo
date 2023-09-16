---
title: lib-db-datalog-blog
tags: [blog, database, datalog]
created: 2023-09-16T17:27:45.505Z
modified: 2023-09-16T17:27:59.262Z
---

# lib-db-datalog-blog

# guide

# blog

## [Datalog in Javascript](https://www.instantdb.com/essays/datalogjs)

- Datalog is a logic-based query language that’s as powerful as SQL. 
- SQL databases store data in different tables
- In Datalog databases, there are no tables. Or really everything is just stored in one table, the **triple table**
- A `triple` is a row with an `id`/`attribute`/`value`. 
  - Triples have a curious property; with just these three columns, they can describe any kind of information!

- SQL has roots in relational algebra. You give the query engine a combination of clauses and statements
- Datalog databases rely on pattern matching. We create “patterns” that match against triples. 
- In Datalog, we still rely on pattern matching for join. 
  - The trick is to match multiple patterns
# more
