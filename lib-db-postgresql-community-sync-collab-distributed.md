---
title: lib-db-postgresql-community-sync-collab-distributed
tags: [collaboration, community, distributed, postgresql, synchronization]
created: 2023-10-28T17:52:29.661Z
modified: 2023-10-28T17:52:51.915Z
---

# lib-db-postgresql-community-sync-collab-distributed

# guide

# discuss-stars
- ## 

- ## 

- ## For CDC users, one of the most exciting features in #Postgres version 16 is the support for logical replication from stand-by servers (a.k.a. read replicas). 
- https://twitter.com/gunnarmorling/status/1737158441611796623
- I remember having to watch replication lag like a hawk to make sure prod disk never blew up. We're huge postgres fans at work, and having the option to CDC from a replica only opens possibilities for our customers to safely move those tuples to an analytic store.
  - Yeah, alluding to that in the post too. You still can run into WAL growth issues also when using logical replication from a stand-by, if you have hot standby feedback on. Which you should, as otherwise the slot may become invalid after schema changes.
  - As of Postgres 13, you can limit the maximum WAL size to keep (only that you then may have to recreate replication slots if they fall too much behind, similar to how things work with binlog clients for MySQL).

# discuss-replication
- ## 

- ## 

- ## What do you think about logical replication in @PostgreSQL ?
- https://twitter.com/samokhvalov/status/1777337304325279765
- Very powerful to enable a wide-variety of use-cases incl. HA/DR (ex: Cloud to on-prem), migrations, online upgrades, cloning data to non-pg targets for other use-cases etc. But a lot of gotchas that need to handled with care: slot growth, lack of DDL support, perf (both initial snapshot and incremental sync), failover slots etc.
- How is there no DDL support. What do people do when they're running extensions?
  - As long as the custom data-types introduced by the extension are WAL backed, I think logical replication should just work. Otherwise, I’d need to check. Im not sure how it can work. During my days at Citus, I remember us adding WAL support to the columnar extension to support HA/backups. If logical replication doesn’t work in those scenarios, other modes of replication such as using a watermark column are a good alternative.

- I think once logical failover slots are available in-core and there's some built-in solution for sequences, it'll be much more viable. I know people who have avoided it simply because losing track of state kinda defeats the purpose.
  - We've done some work on sequences: https://docs.omnigres.org/omni_seq/id/
- Yeah, failover slots are definitely needed. Slots on stand-bys get you halfway there, though, it just requires a bit of manual work. 

- Its missing sequences not getting replicated. Had that not been the case, the last major version upgrade we did would have been a almost zero downtime major version upgrade.
  - We did some initial work on sequences https://docs.omnigres.org/omni_seq/id/
- Why you need to replicate sequences? 2-way replication?

- It’s pretty great once it’s going. One issue I’ve had is for large tables, the initial copy never finishes. We’ve worked around this using the RDS snapshot technique described by Instacart

- Useful for usecases like data warehousing, provenance, integration, time travel debugging and so on. However beware of those replication slots ... running out of space.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🔥 [Citus 6.1 Released – Horizontally scale your Postgres database | Hacker News_201702](https://news.ycombinator.com/item?id=13662166)
- 
- 
- 

- ## 🔥 [PgSync: Sync Postgres data between databases | Hacker News_202003](https://news.ycombinator.com/item?id=22676112)
- 
- 
- 
