---
title: lib-db-postgresql-community-roadmap-changelog
tags: [changelog, community, postgresql, roadmap]
created: 2023-10-28T17:53:02.012Z
modified: 2023-10-28T17:53:23.397Z
---

# lib-db-postgresql-community-roadmap-changelog

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-news-pg
- ## 

- ## 

- ## 

- ## 19 is getting graph queries.
- https://x.com/alxshp/status/2069494262878863772
  - With SQL/PGQ, you can query relationships directly in SQL

- ## PostgreSQL 19 introduces GROUP BY ALL.
- https://x.com/KaraBharat/status/2066419046443258342

- ## PostgreSQL 19 Beta 1 adds ON CONFLICT DO SELECT.
- https://x.com/KaraBharat/status/2064222684813349357
  - Insert a row. If it already exists, return it. 
  - Atomic get-or-create, finally.

- the bigger win is skipping noop updates that bloat wal and fire triggers

- the downstream effect that matters: orms can finally expose get-or-create as one atomic method instead of a retry loop. that eliminates a whole category of phantom-row bugs that are notoriously hard to reproduce in production
# discuss
- ## 

- ## 

- ## 

- ## PostgreSQL 18 Beta is here _202505
- https://x.com/gwenshap/status/1923393474297995662
  - Async I/O (with io_uring) — 2–3x speedups on seq scans, vacuums
  - Skip scan + smarter OR/IN optimizations
  - uuidv7() and virtual generated columns
  - EXPLAIN ANALYZE now shows I/O, CPU, WAL
