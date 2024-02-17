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

- ## 📡 [RFC: Postgres support · vitessio/vitess _202011](https://github.com/vitessio/vitess/issues/7084)
- Before anyone gets too excited, this work is not yet planned by anyone we know. 
  - The intent behind writing this up is to document the size and scope of the work and a possible blueprint for when someone is ready to take this up. 
  - This RFC is intentionally at a very high-level. Each of the sections will probably need a more detailed RFC of their own.

- Vitess runs with MySQL as the backend DB. 
- This proposal is to allow Vitess to run with PostgreSQL as the backend DB.

- Update on 5/25/2021: The Vitess maintainer team currently has no plans to add Postgres support to Vitess.

- ## [PostgreSQL support? · vitessio/vitess _201503](https://github.com/vitessio/vitess/issues/479)
- A similar product but support postgreSQL https://github.com/citusdata/citus

# discuss
- ## 

- ## 

- ## 
