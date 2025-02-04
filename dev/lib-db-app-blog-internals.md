---
title: lib-db-app-blog-internals
tags: [blog, database, internals]
created: 2023-12-13T06:58:33.523Z
modified: 2023-12-13T06:58:52.302Z
---

# lib-db-app-blog-internals

# guide

# blogs

## [How Databases Store and Retrieve Data_202108](https://siemens.blog/posts/how-databases-store-and-retrieve-data/)

## [Why Databases Should Bypass the Linux Page Cache - The New Stack _202403](https://thenewstack.io/why-databases-should-bypass-the-linux-page-cache/)

- The Linux page cache, also called disk cache, is a general-purpose type of cache. 
  - Although it can be tuned to better serve database kind of workloads, it’s fundamentally inefficient for database implementations.
- The page cache lacks the context over key database-specific needs that’s needed for optimal performance and control. 
  - Given the page cache’s inefficient memory use, poor negative caching, redundant buffers, high CPU overheads for reads and premature cache eviction (among other challenges), it makes sense for a performance-oriented database to take a different approach.
- Let’s look at why ScyllaDB, a database for latency-sensitive apps, completely bypasses the Linux cache during reads and uses its own highly efficient row-based integrated internal cache instead.

- 
- 
- 

# blogs-mvcc
- [Isolation Levels and MVCC in SQL Databases: A Technical Comparative Study _202402](https://fosdem.org/2024/schedule/event/fosdem-2024-3600-isolation-levels-and-mvcc-in-sql-databases-a-technical-comparative-study/)
# more
