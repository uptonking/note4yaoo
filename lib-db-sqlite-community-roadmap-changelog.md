---
title: lib-db-sqlite-community-roadmap-changelog
tags: [changelog, community, roadmap, sqlite]
created: 2023-10-28T17:44:09.976Z
modified: 2023-10-28T17:44:35.356Z
---

# lib-db-sqlite-community-roadmap-changelog

# guide

# discuss-stars
- ## 

- ## 

- ## aws really needs a sqlite option
- https://twitter.com/thdxr/status/1771728366774669430
- There’s an option to mount SQLite on EFS. You can still get the benefits of SQLite but it’s a horrible solution for prod applications
- yeah even with the guarantees EFS provides i don’t think sqlite likes being on a network drive
  - Yes the latency will be poor. I read somewhere it takes around 64ms to retrieve 10 records from an SQLite db mounted on Efs
- Working well enough for me. I can load 15k records over http to my db.

- https://sqlite.org/cloudsqlite/doc/trunk/www/index.wiki on Lambda with concurrency=1 ...
  - yeah the problem is then your reads are single threaded also
- Right! And your writers are slow or without durability guarantees. So you’d have to go for Fargate. And at that point you might as well go for RDS…

- ## 🎯 [The Design of SQLite4 | Hacker News_202206](https://news.ycombinator.com/item?id=31785170)
- >SQLite4 was an experimental rewrite of SQLite that was active from 2012 through 2014. All development work on SQLite4 has ended. Lessons learned from SQLite4 have been folded into the main SQLite3 product. SQLite4 was never released. There are no plans to revive it. You should be using SQLite3.

- [Work on SQLite4 has concluded | Hacker News_201711](https://news.ycombinator.com/item?id=15648280)
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🎯 [SQLite: Past, Present, and Future | Hacker News_202209](https://news.ycombinator.com/item?id=32675861)
- 
- 
- 
