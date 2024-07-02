---
title: lib-db-mysql-community-vitess
tags: [community, distributed, mysql, performance, vitess]
created: 2024-02-17T13:00:57.945Z
modified: 2024-02-17T13:01:44.351Z
---

# lib-db-mysql-community-vitess

# guide

# discuss-stars
- ## 

- ## 

- ## [RFC: Deprecate MariaDB Support in 2022 and Remove in 2023 · vitessio/vitess _202201](https://github.com/vitessio/vitess/issues/9518)
- The reasons for proposing this are as follows:
  - Vitess only officially supports MariaDB 10.0-10.3 today, 10.3 is already nearly 4 years old
  - MariaDB is a hard fork of MySQL and 10. X is a very different database than MySQL 8. X (which is quickly becoming the default with Vitess)
  - Vitess is not well tested on MariaDB today within the project nor the user base

- This issue isn't trying to compare MySQL vs MariaDB, it is just acknowledging that they can't be treated the same anymore. It's fundamentally no different from PostgreSQL compatibility, which is the highest upvoted issue in all of Vitess. It's not technically impossible, just significantly more overhead, that based on the current usage of Vitess would be better spent adding features and improving performance.
# discuss-pg-vitess
- ## 

- ## 

- ## 

- ## Is there a Vitess for Postgres? _202006
- https://news.ycombinator.com/item?id=23642484
- Isn't Citus sort of the same?
  - Yes but I feel Vitess is much more widely used than Citus. MySQL community, last time I check has formed a more mature ecosystem and conscious on HA and Clustering.
  - Postgres still feels more like throwing you a bunch of options and you are on your own.

- ## [PlanetScale – Database for Developers | Hacker News _202105](https://news.ycombinator.com/item?id=27197873)
- Wondering will we see something like this for Postgres? I like the cool things but I can’t migrate to MySQL just because of this.
- I've been following Citus Data
- vitess has postgres compatibility at the bottom of their "Medium Term" roadmap

- ## [Planet Scale for Postgres : r/PostgreSQL _202312](https://www.reddit.com/r/PostgreSQL/comments/18hbrcx/planet_scale_for_postgres/)
- Basically https://neon.tech is the planetscale alternative (with branching etc).
- We just release branching https://supabase.com/blog/supabase-branching
- 
- 
- 

- ## [Postgres compatibility · vitessio/vitess _202011](https://github.com/vitessio/vitess/issues/7003)
- Since this is a non-trivial task, the process is for you to write up a proposal and request comments from the maintainers and community. 

- ## 📡🐘 [RFC: Postgres support · vitessio/vitess _202011](https://github.com/vitessio/vitess/issues/7084)
- Before anyone gets too excited, this work is not yet planned by anyone we know. 
  - The intent behind writing this up is to document the size and scope of the work and a possible blueprint for when someone is ready to take this up. 
  - This RFC is intentionally at a very high-level. Each of the sections will probably need a more detailed RFC of their own.

- Vitess runs with MySQL as the backend DB. 
- This proposal is to allow Vitess to run with PostgreSQL as the backend DB.

- Update on 5/25/2021: The Vitess maintainer team currently has no plans to add Postgres support to Vitess.

- FYI: there is Citus and it is doing something similar to Vitess.
  - I'll probably start with Citus or Yugabyte for now, since even if Postgres support is added it is still far away.

- ## [PostgreSQL support? · vitessio/vitess _201503](https://github.com/vitessio/vitess/issues/479)
- A similar product but support postgreSQL https://github.com/citusdata/citus

# discuss-ha
- ## 

- ## 

- ## [MySQL High Availability at GitHub | Hacker News _201806](https://news.ycombinator.com/item?id=17357319)

- [MySQL High Availability Solutions | by Ganesh Joshi | Medium _202307](https://medium.com/@ganeshchamp39/mysql-high-availability-solutions-ec0f06f455ee)
  - MySQL InnoDB Cluster: An integrated solution offering built-in HA and automatic failover capabilities.
  - Percona XtraDB Cluster: An open-source solution with synchronous replication for enhanced data consistency.

- I feel like this article stabs at a kind of interesting tradeoff in distributed databases: using consensus to store your data, or using consensus to point at the master for the data.
  - A lot of the bleeding-edge DBMS out there (e.g. CockroachDB, TiDB) use the former probably because of the Spanner influence, but maybe the latter is good enough for almost everyone.

- Vitess is another system for horizontally scaling MySQL that they use at YouTube https://vitess.io/
  - Another cool one is ProxySQL. We opted towards that rather than Vitess because it allowed a crawl, walk, run approach. Vitess came across as all or nothing.

- Why not InnoDB Cluster with single primary?
  - That's only practical for a single datacenter. You still really need asyc replication across geographic boundaries with a failover mechanism.

- TiDB is relevant because it is distributed and protocol-compatible with MySQL.
  - protocol-compatible doesn't directly imply API-compatible (I'm thinking of very very subtle differences between things like datatypes or isolation level behavior). I know a bit more about CockroachDB, which consciously does some things differently from Postgres.

- 
- 
- 

# discuss
- ## 

- ## 

- ## 
