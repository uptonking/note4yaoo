---
title: toc-db-postgres-examples
tags: [db, examples, postgresql, toc]
created: 2023-10-11T20:33:41.839Z
modified: 2023-10-11T20:34:10.999Z
---

# toc-db-postgres-examples

# guide

# popular

# apps

# utils
- https://github.com/pgcentralfoundation/pgrx /rust
  - a framework for developing PostgreSQL extensions in Rust and strives to be as idiomatic and safe as possible.
  - supports Postgres v11-v15
# query
- https://github.com/tozd/node-reactive-postgres /202204/js/inactive
  - brings reactive (or live) queries to PostgreSQL.
  - I have made something similar trying to match more the concept of a materialized view, but just on the client instead of inside the database
  - You can take an arbitrary SELECT query, using multiple joins, data transformations, and even custom functions, and besides the initial set of results also get real-time updates about any changes to those results. 
  - For every reactive query, a `TEMPORARY TABLE` is created in the database which serves as cache for query results.
  - Triggers are added to all query sources for the query, so that when any of sources change, this package is notified using LISTEN/NOTIFY that a source has changed
  - Because this package uses temporary tables, consider increasing `temp_buffers` PostgreSQL configuration so that there is more space for temporary tables in memory.
# more
