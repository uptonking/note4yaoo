---
title: lib-db-postgresql-community-devops
tags: [community, devops, postgresql]
created: 2023-10-26T19:18:00.650Z
modified: 2023-10-26T19:18:19.584Z
---

# lib-db-postgresql-community-devops

# guide

# discuss-stars
- ## 

- ## 《云RDS阉掉了PostgreSQL的灵魂》—— 用户无法在云数据库 RDS 上自由加装扩展，一些强力扩展也不可能出现在 RDS 中。
- https://twitter.com/GobeUncleWang/status/1768815151300706686
  - 使用 RDS 无法发挥出 PostgreSQL 真正的实力，而这是一个对云厂商来说无法解决的缺陷。（不过使用本地优先的RDS Pigsty则无此问题

- 🤔 确实难理解为啥云不给装插件
  - 性能不行，增加运维成本，而且云上基本上都是魔改版的pg，插件不一定兼不兼容呢
- 先给你一个普遍支持的插件列表，然后往里装，想要多的就加钱 想要自定义就是安全风险，加钱-安全 两手抓
# discuss-perf
- ## 

- ## 

- ## 🔥 [Lessons learned scaling a PostgreSQL database to 1.2bn records/month | Hacker News_201901](https://news.ycombinator.com/item?id=19024872)
- 
- 
- 

- ## 🔥 [Simple script to analyse your PostgreSQL database config, give tuning advice | Hacker News_201903](https://news.ycombinator.com/item?id=19423036)
- 
- 
- 

# discuss-migration/upgrade
- ## 

- ## 🔥 [Migrating 1200 databases from MySQL to Postgres | Hacker News_201708](https://news.ycombinator.com/item?id=15026887)
- 
- 
- 

- ## 🔥 [Better Database Migrations in Postgres | Hacker News_201709](https://news.ycombinator.com/item?id=15235221)
- 
- 
- 

# discuss-docker
- ## 

- ## 

- ## 🔥 [A PostgreSQL Docker container that automatically upgrades your database | Hacker News_202307](https://news.ycombinator.com/item?id=36746274)
- 
- 
- 

# discuss
- ## 

- ## Manning 的 PostgreSQL 新书，介绍了一些使用 PostgreSQL 的注意事项以及常见问题，属于运维方面的内容吧。
- https://twitter.com/huangzworks/status/1757410451107754118

- ## TIL, as a Postgres superuser, you can run: `SET ROLE other_user;` Then, start working as that user.
- https://twitter.com/winsletts/status/1745504268973695371
- You can also use `\c user=other_user`

- `psql -U your_username -t -c "SELECT datname FROM pg_database WHERE datname NOT IN ($EXCLUDEDBS)"`

- ## 🔥 [Recovering a PostgreSQL database after a hard drive failure | Hacker News_202112](https://news.ycombinator.com/item?id=29744815)
- 
- 
- 

- ## 🔥 [Cleaning Up Your Postgres Database | Hacker News_202103](https://news.ycombinator.com/item?id=26367080)
- 
- 
- 

- ## 🔥 [Updating a 50 terabyte PostgreSQL database (2018) | Hacker News_202201](https://news.ycombinator.com/item?id=29923303)
- 
- 
- 

- ## 🔥 [Updating a 50 terabyte PostgreSQL database (2018) | Hacker News_202103](https://news.ycombinator.com/item?id=26535357)
- 
- 
- 

- ## 🔥 [Securing a Postgres Database | Hacker News_202104](https://news.ycombinator.com/item?id=26674756)
- 
- 
- 
