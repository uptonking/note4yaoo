---
title: lib-db-postgresql-blog-xp
tags: [blog, dev-xp, postgresql]
created: 2023-10-26T17:28:59.526Z
modified: 2023-10-26T17:29:11.388Z
---

# lib-db-postgresql-blog-xp

# guide

# blogs

## 🤼🏻 [Last Updated Columns With Postgres - Gunnar Morling _202402](https://www.morling.dev/blog/last-updated-columns-with-postgres/)

- 👤
- https://twitter.com/gunnarmorling/status/1759937239235088866
  - A quick write-up on auto-updating an "updated_at" timestamp column in your #Postgres tables. Turns out you don't necessarily need triggers for that
- This is one of the least controversial reasons to use a trigger. Why do you want to avoid it?
  - Just the hassle of defining them all, I guess. But yeah, maybe it's the better solution indeed. Anyways, I was excited to learn that I can refer to `DEFAULT` in updates.

- 🤼🏻 Let me be controversial: `UPDATED_AT` is wrong most of the time:
  - auditing? Use auditing! Why would you need to audit update time and not delete time?
  - replication? Use CDC! This UPDATED_AT doesn't know when the change was made in the DB (commit time)
- No controversies there Frank. in Oracle, the neat one for that is to create your tables with ROWDEPENDENCIES. Last updated (the SCN) is stored on each row automatically with the only cost being 6 bytes per row, and there's a function to convert that to a date.
  - Or store all the SCNs you can and pick the one you prefer. But, yes, ORAROWSCN with ROWDEPENDENCIES is the closest to when the change was visible
- Interesting, I certainly find it useful as an easy means for getting some quick insight in to the freshness of data. Sure, CDC or other approaches will give you way more, but I don't think they have to exclude each other.
- not all tables will have timestamp columns, so even in CDC you may append an 'observed_time' column along with other CDC metadata (e.g. DML type, log sequence number) to the data lake.
- Sure CDC is the best/reliable approach and gives a lot flexibility  too. However if the use case involves a monotonically increasing column (like updated_at), that should also work for replication. However the replication tool needs to be careful of reading rows from a snapshot and wait for inflight transactions to finish.

- [If you have an UPDATED_AT column, I'm curious to know your use cases](https://twitter.com/FranckPachot/status/1760000064355958919)
- Query based CDC
  - If you do CDC by querying WHERE UPDATED_AT > : LAST_TIME_I_CHECKED you will miss some records (those that were updated before : LAST_TIME_I_CHECKED but committed after.
- updated_at is great for cache keys, you can use `:id/:updated_at` as a key to ensure stale cache entries are never served after an update

- Warning: adding non-constant default values can be problematic on large datasets: "Adding a column with a volatile DEFAULT or changing the type of an existing column will require the entire table and its indexes to be rewritten". IdK how pg handles current_timestamp on DEFAULT.
  - Ah, found it: "Another important example is that the current_timestamp family of functions qualify as STABLE, since their values do not change within a transaction." So on PG it seems to be safe. Other DBs might choose other paths!

- It's a nice feature for avoiding stuff like timezone issues, but for "updated_at" I'd go for a trigger, as it guards you from forgetting to update the value and fraudulent manipulations

## [Scaling PostgreSQL read performance by partition /无代码 - DEV Community _202304](https://dev.to/zaf07/scaling-postgresql-read-performance-2pp4)

# more
- [Row Level Security | Tutorials | Crunchy Data](https://www.crunchydata.com/developers/playground/row-level-security)

- [PostgreSQL: No More VACUUM, No More Bloat_202307](https://www.orioledata.com/blog/no-more-vacuum-in-postgresql/)
  - The way InnoDB does this is by effectively doing two writes: the fsync’d-ack-end-user store is a ringbuffer that then gets copied in bulk into the main db file with a whole page-reuse scheme. It is very complicated and took half a decade to get correct and fast.
