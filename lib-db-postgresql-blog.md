---
title: lib-db-postgresql-blog
tags: [blog, postgresql]
created: 2023-10-26T17:28:21.438Z
modified: 2023-10-26T17:28:41.701Z
---

# lib-db-postgresql-blog

# guide

- https://github.com/Vonng/pg
  - 关于PostgreSQL应用开发，监控管理 与 内核架构 的 文章与 笔记
  - [PostgreSQL指南：内幕探索](https://pg-internal.vonng.com/)

- https://github.com/Vonng/ddia
  - 《Designing Data-Intensive Application》DDIA中文翻译
# blogs

## 🎯✨ [Thoughts on PostgreSQL in 2024 | Jonathan Katz_202401](https://jkatz05.com/post/postgres/postgresql-2024/)

- The new year is a great opportunity to ask “where is PostgreSQL going?”
- Based on many conversation and observations, I proposed three broad feature buckets to look at:
  - Availability; Performance; Developer features (优化方向是CAP)

- For existing PostgreSQL users and users looking to migrate to PostgreSQL, features around availability are the biggest ask. 
  - Typically, this centers around high availability, or the ability to continue to have access to the database (especially read/write access) during a planned (update) or unplanned (outage) disruption. 
- A key feature for PostgreSQL that will continue to improve availability is logical replication. 
  - One advantage this has over physical (or binary) replication is that you can use logical replication to stream changes from a PostgreSQL 15 to a PostgreSQL 16 system as part of a major version upgrade. This can help reduce the amount of downtime it takes to perform a major version upgrade 
- Another area of availability to consider is around schema maintenance operations (i.e. DDL statements), such an ALTER TABLE that takes an ACCESS EXCLUSIVE lock on the table that blocks all other write operations on that table
  - There are various utilities and extensions that let you run nonblocking schema updates, but it would be more convenient, and likely performant, to support more nonblocking schema changes natively in PostgreSQL

- PostgreSQL has a reputation of vertically scaling, or being able to scale as you provide more hardware resources to a single instance. 
- One of the biggest efforts, and one that’s been an ongoing multi-year project, is to support direct IO (DIO) and asynchronous IO (AIO) in PostgreSQL.
- Another effort I’m intrigued by is parallel recovery. PostgreSQL users with heavy write workloads tend to postpone checkpoints to defer I/O workload. This can be problematic on a busy system if PostgreSQL crashes and a checkpoint has not occurred for awhile.
  - One way to help overcome this limitation is to support “parallel recovery, ” or being able to replay changes in parallel.
  - This would apply not only to crash recovery, but how PostgreSQL can replay any WAL changes (e.g. point-in-time-recovery). 

- I view “developer features” as a fairly broad category around how users can architect and build their apps around PostgreSQL. 
  - This includes SQL syntax, functions, procedural language support, and other features that help users both build apps
- Currently, a lot of innovation on PostgreSQL developer features is occurring in extensions, which is an advantage of PostgreSQL’s extensible model.
- we should be investing in adding developer features in PostgreSQL that are not possible to add in extensions, such as SQL standard features. 

- Finally, we need to see how we can continue to support the emergent workload coming from AI/ML data, specifically vector storage and search

- PostgreSQL was designed to be extensible: you can add functionality to PostgreSQL without having to fork it. 
  - This includes new data types, indexing methods, ways to work with other database systems, utilities that make it easier to manage PostgreSQL features, additional programming languages, and even extensions that let you write your own extensions.

## [Is UPDATE the same as DELETE + INSERT in PostgreSQL?_202012](https://www.cybertec-postgresql.com/en/is-update-the-same-as-delete-insert-in-postgresql/)

- PostgreSQL does not update a table row in place. 
  - Rather, it writes a new version of the row (the PostgreSQL term for a row version is “tuple”) and leaves the old row version in place to serve concurrent read requests. 
  - VACUUM later removes these “dead tuples”.
- Conclusion
  - To understand the difference between UPDATE and DELETE+INSERT, we had a closer look at the tuple headers. We saw infomask, infomask2 and t_ctid, where the latter provides the link between the old and the new version of a row.
  - PostgreSQL’s row header occupies 23 bytes, which is more storage overhead than in other databases, but is required for PostgreSQL’s special multiversioning and tuple visibility implementation.

- ref: [PostgreSQL: Documentation: 15: 25.1. Routine Vacuuming](https://www.postgresql.org/docs/current/routine-vacuuming.html#VACUUM-FOR-SPACE-RECOVERY)
  - In PostgreSQL, an UPDATE or DELETE of a row does not immediately remove the old version of the row. 
  - This approach is necessary to gain the benefits of multiversion concurrency control (MVCC)
  - the row version must not be deleted while it is still potentially visible to other transactions. 
  - But eventually, an outdated or deleted row version is no longer of interest to any transaction. 
  - The space it occupies must then be reclaimed for reuse by new rows, to avoid unbounded growth of disk space requirements. 
  - This is done by running VACUUM.
# more
- [StackOverflow的开发者调研 PostgreSQL is the Linux of Database](https://mp.weixin.qq.com/s/xewE87WEaZHp-K5hjuk65A)
