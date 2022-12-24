---
title: lib-db-postgresql-docs
tags: [docs, postgresql]
created: 2022-06-13T03:00:31.773Z
modified: 2022-06-13T03:00:51.734Z
---

# lib-db-postgresql-docs

# guide

# docs

# blogs

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
- 
- 
- 
- 
