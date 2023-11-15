---
title: lib-db-app-community-devops
tags: [community, database, devops]
created: 2023-10-26T18:47:03.513Z
modified: 2023-10-26T18:47:22.664Z
---

# lib-db-app-community-devops

> about database migration/upgrade

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-migration/upgrade
- ## 

- ## 太久没做数据迁移都忘了要后建索引。
- https://twitter.com/forevertjt/status/1719732968636465590
  - 插入到千万级之后索引就明显影响插入速度了，把索引都干掉就快很多了。

- ## 🔥 [Ask HN: How do you manage direct updates to databases in a production system | Hacker News_202112](https://news.ycombinator.com/item?id=29563226)
- 
- 
- 

- ## 🔥 [Migrating a 40TB SQL Server Database | Hacker News_202007](https://news.ycombinator.com/item?id=23998503)
- 
- 
- 

- ## 🔥 [Ask HN: How does your development team handle database migrations? | Hacker News_201905](https://news.ycombinator.com/item?id=19880334)
- Would be cool to have git for databases.
  - That’s basically the proposition of any event sourcing system. but you’re kinda right, that involves a level of code complication (but then it would be so simple as you described to restore / rebase / etc)

- ## 🔥 [An Unlikely Database Migration | Hacker News_202101](https://news.ycombinator.com/item?id=25767128)
- 
- 
- 

- ## 🔥 [On Uber’s Choice of Databases | Hacker News_201607](https://news.ycombinator.com/item?id=12187797)
- 
- 
- 

- ## 🔥 [Migrating bajillions of database records at Stripe | Hacker News_201509](https://news.ycombinator.com/item?id=10150438)
- 
- 
- 

# discuss-db-docker/k8s
- ## 

- ## 

- ## 🔥 [Running Databases on Kubernetes | Hacker News_202303](https://news.ycombinator.com/item?id=34999039)
- 
- 
- 

- ## 🔥 [Why Databases Are Not for Docker Containers | Hacker News_201702](https://news.ycombinator.com/item?id=13582757)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## Lukewarm(微温的; 不热烈的) take for database products - focus on winning new workloads, don't worry so much about migrations. 
- https://twitter.com/MarkCallaghanDB/status/1724454882785304672
  - RoI on features that win new workloads >>> RoI on features that get migrations.
- One way to “hack” this paradigm is to build based on Postgres, and then contribute/collaborate on open source migration tooling.
- Even more lukewarm take - don’t build a database. Build a data based product within a niche. Then generalize from there if you survive year four.

- ## 🔥 [What we learned after I deleted the main production database by mistake | Hacker News_202209](https://news.ycombinator.com/item?id=32903367)
- 
- 
- 

- ## 🔥 [We deleted the production database by accident | Hacker News_202010](https://news.ycombinator.com/item?id=24813795)
- 
- 
- 

- ## 🔥 [Managing database schema changes without downtime | Hacker News_201803](https://news.ycombinator.com/item?id=16665447)
- 
- 
- 
