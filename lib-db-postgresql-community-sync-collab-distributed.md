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

- ## TIL Postgres added replication only in 2010
- https://x.com/iavins/status/1870146352052875489
- It's surprising but true. Before that, it was continuous crash recovery via WAL replay, or... Slony trigger-based replication.

- How were people working around this limitation before that?
  - There were several very mature extensions for it - I think Slony was the most popular - https://slony.info - first released over 20 years ago
- Nobody cared that much 🤷‍♂️ And people who cared did schema-level replication with third party extensions like Slony.

- About the same time MySQL added select from a select.

- A major reason why MongoDB become popular in a lot of companies starting in 2010-2015.

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
# discuss-distributed-pg
- ## 

- ## 

- ## Announcing Multigres, a sharding solution for Postgres to take it to the petabyte-scale _20250614
- https://x.com/supabase/status/1933627932972376097
- Powered by the AvgDB storage engine.
  - Definitely going to be interesting to see the scalability factor, along with ensuring query time is lower. 

- needs to be a simple extension you plug and play & it does all the partitioning / sharding / etc. behind the scenes (like fusion drive on macOS) 

- So a custom proxy handler that handles writes and distributes it across shard nodes?
# discuss-ha
- ## 

- ## 

- ## 

- ## [Why PostgreSQL High Availability Matters and How to Achieve It | Hacker News _202306](https://news.ycombinator.com/item?id=36328148)
- It’s amazing that this isn’t a solved problem, but we have all of this crazy language model stuff.
  - Unfortunately Spanner isn’t open source. Yugabyte and Citus are close but have annoying issues. Cockroach isn’t 100% compatible (and has its own issues) and things like FoundationDB which are truly HA and comparable to Spanner in terms of consistency and fault tolerance are not easily plugged into Postgres as the underlying storage engine since sadly it’s only a key value store.
- Citus is not close to Spanner. No global secondary indexes, no cross-shard ACID (the commit status is eventually consistent). No auto-resharding. Yugabyte and Cockroach have a spanner-like architecture, but different open-source model and postgres-compatibility

- one of the solutions which made it pretty simple for us to run postgresql in a ha environment (mostly in k8s, but works standalone as well) is zalandos patroni: https://github.com/zalando/patroni it's really solid and worked for us for a few years already. (it also comes with a haproxy config to have a single leader connection)
- How does patroni can do some self healing after primary db gets down and then up again? Or is manual intervention required? How does it look?
  - manual intervention is not required. Patroni will just use a Standby as the new master. If the old master will be alive again it will be started as a backup. Of course there might be dataloss if it was used with async replication.
  - Patroni has great docs for this here

- I just implemented master with read replica with the bitnami postgres-repmgr image. It's not perfect, but it works and running my own instances in aws instead of rds is going to save me close to 80% when i also add in purchasing a savings plan. By setting this up I've learned more about postgres than i ever ever wanted too. lol

- What's the self-hosted Postgres HA story these days?
  - pg_auto_failover makes it an absolute breeze. I cannot understand how it's not mentioned in the article.
- On self-hosted you can use the same as what cloud vendors are doing. Patroni or pg_auto_failover to manage single-primary + replicas. Maybe Neon to run an Aurora-like. CitusData... Azure did a lot around to get elasticity. Not easy to do the same. YugabyteDB on Kubernetes can be a cloud-native self-hosted solution
# discuss-cdc-pg
- ## 

- ## 

- ## 

- ## [The Ultimate Guide to PostgreSQL Data Change Tracking | Hacker News _202402](https://news.ycombinator.com/item?id=39488719)
- I really like the approach of adding additional context for WAL CDC. I imagine this could be implemented with something like Hasura pretty easily (you can access hasura session data in the db).
  - I use both the trigger + audit table approaches in my sass (for user-facing activity feeds) and subscribe to CDC WAL changes for dealing with callback-like logic (i.e., send registration email, clear cache).
  - I'm not a fan of the pg_notify approach due to requirement of adding triggers (performance penalty) and the 8k character limit per column (you will lose data as it will splice off anything larger than that).
  - Application-level tracking or callbacks makes the stack dependent on the application for data integrity, I'd rather the database be the source of truth on all things data. Especially in the age of microservices.

- Another technique not discussed is to create an md5 hash of each record and to keep track of added and deleted hashes. The d hash would exist as an additional column on each table being tracked.
  - If I understand you right, this seems like a very course-grained way to track changes. You can record that a change was made, but not the specific change. 

- There are also other way, such as bitemporal tables.
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
