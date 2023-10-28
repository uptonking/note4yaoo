---
title: toc-db-postgresql-utils-extensions
tags: [extensions, postgresql, toc, utils]
created: 2023-10-26T15:29:07.458Z
modified: 2023-10-26T15:29:40.053Z
---

# toc-db-postgresql-utils-extensions

# guide

# popular

# plugins

# utils
- https://github.com/pgcentralfoundation/pgrx /202310/rust
  - a framework for developing PostgreSQL extensions in Rust and strives to be as idiomatic and safe as possible.
  - supports Postgres v11-v15
  - [PGX: Write Postgres extensions in Rust instead of C | Hacker News_202007](https://news.ycombinator.com/item?id=23821112)
# query
- https://github.com/tozd/node-reactive-postgres /202204/js/inactive
  - brings reactive (or live) queries to PostgreSQL.
  - I have made something similar trying to match more the concept of a materialized view, but just on the client instead of inside the database
  - You can take an arbitrary SELECT query, using multiple joins, data transformations, and even custom functions, and besides the initial set of results also get real-time updates about any changes to those results. 
  - For every reactive query, a `TEMPORARY TABLE` is created in the database which serves as cache for query results.
  - Triggers are added to all query sources for the query, so that when any of sources change, this package is notified using LISTEN/NOTIFY that a source has changed
  - Because this package uses temporary tables, consider increasing `temp_buffers` PostgreSQL configuration so that there is more space for temporary tables in memory.

- https://github.com/aarroyoc/postgresql-prolog /202310/prolog
  - A Prolog library to connect to PostgreSQL databases
  - [PostgreSQL-Prolog: A Prolog library to connect to PostgreSQL databases | Hacker News_202109](https://news.ycombinator.com/item?id=28660202)
# more
