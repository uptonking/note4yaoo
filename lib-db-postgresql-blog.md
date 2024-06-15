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

## [PostgreSQL: Documentation: 16: VACUUM](https://www.postgresql.org/docs/current/sql-vacuum.html)

- Plain `VACUUM` (without FULL) simply reclaims space and makes it available for re-use. 
  - This form of the command can operate in parallel with normal reading and writing of the table, as an exclusive lock is not obtained. 
  - However, extra space is not returned to the operating system (in most cases); 
  - it's just kept available for re-use within the same table. 
  - It also allows us to leverage multiple CPUs in order to process indexes. This feature is known as parallel vacuum. 
- `VACUUM FULL` rewrites the entire contents of the table into a new disk file with no extra space, allowing unused space to be returned to the operating system. 
  - This form is much slower and requires an ACCESS EXCLUSIVE lock on each table while it is being processed.

### [postgresql - VACUUM returning disk space to operating system - Database Administrators Stack Exchange](https://dba.stackexchange.com/questions/37028/vacuum-returning-disk-space-to-operating-system)

- The standard form of `VACUUM` removes dead row versions in tables and indexes and marks the space available for future reuse. 
  - However, it will not return the space to the operating system, except in the special case where one or more pages at the end of a table become entirely free and an exclusive table lock can be easily obtained. 
  - In contrast,  `VACUUM FULL` actively compacts tables by writing a complete new version of the table file with no dead space. This minimizes the size of the table, but can take a long time. It also requires extra disk space for the new copy of the table, until the operation completes.

## 🗑️⚡️ [Dead Tuples In Focus — Vol II: Enhancing PostgreSQL Performance _202401](https://firattamur.medium.com/dead-tuples-in-focus-vol-ii-enhancing-postgresql-performance-ce7d84f76082)

- When a row in PostgreSQL is updated or deleted, it doesn't disappear. Instead, it evolves into a 'dead tuple' - think of it as the row's ghost, invisible yet present within the database's realm
  - These 'dead tuples' signify the complexity and elegance of PostgreSQL's MVCC, serving as invisible but essential cogs in the database’s lifecycle. 
  - They play a crucial role in maintaining harmony and efficiency, allowing multiple users to coexist and operate without interference.

- VACUUM
  - VACUUM doesn’t shrink your database size. It’s more about housekeeping, making sure the space taken up by dead tuples is now free for new data. 
  - Imagine it as reorganizing your closet to make space without actually getting rid of the closet
  - It does all this without interrupting your database’s daily life. There’s no locking of tables, meaning your database activities continue uninterrupted

- VACUUM FULL
  - It’s more intensive, removing dead tuples and also compacting the database to actually reduce its physical size. 
  - Think of it as not only clearing out your closet but also resizing it to fit your current needs.
  - This command rewrites the table to include only the live tuples, which can significantly shrink the table size.
  - VACUUM FULL requires exclusive access to the table it’s cleaning. This means it locks the table, so no one can read or write to it during the process.

- VACUUM will clean up the dead tuples, making space available for new data. However, it won’t reduce the physical file size of the ‘users’ table.
- VACUUM FULL not only removes dead tuples but also compacts the table, which should reduce its physical size.

## 🆚️ [Is UPDATE the same as DELETE + INSERT in PostgreSQL? _202012](https://www.cybertec-postgresql.com/en/is-update-the-same-as-delete-insert-in-postgresql/)

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

## 🔍 [Postgres Full-Text Search: A Search Engine in a Database _202107](https://www.crunchydata.com/blog/postgres-full-text-search-a-search-engine-in-a-database)

# more
- [StackOverflow的开发者调研 PostgreSQL is the Linux of Database](https://mp.weixin.qq.com/s/xewE87WEaZHp-K5hjuk65A)

- [A Comprehensive Overview of PostgreSQL Query Processing Stages _202401](https://www.highgo.ca/2024/01/26/a-comprehensive-overview-of-postgresql-query-processing-stages/)

- [Overcoming Pitfalls of Postgres Logical Decoding _202406](https://blog.peerdb.io/overcoming-pitfalls-of-postgres-logical-decoding)
