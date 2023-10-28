---
title: lib-db-app-community-design
tags: [community, database, design]
created: 2023-09-17T17:50:30.020Z
modified: 2023-09-17T17:50:49.932Z
---

# lib-db-app-community-design

# guide

> about database schema design and examples

# discuss-stars
- ## 

- ## 

- ## 🔥 [Use singular nouns for database table names | Hacker News_202304](https://news.ycombinator.com/item?id=35762682)
- 
- 
- 

- ## 🔥 [A one-size-fits-all database doesn't fit anyone | Hacker News_201806](https://news.ycombinator.com/item?id=17404517)
- 
- 
- 

- ## 📄🔥 [Xata File Attachments: Databases can now store files and images | Hacker News_202308](https://news.ycombinator.com/item?id=37324370)
- 
- 
- 

- ## 💡🔥🔥 [A humble guide to database schema design | Hacker News_202004](https://news.ycombinator.com/item?id=22806142)
- 
- 
- 

# discuss-schema
- ## 

- ## 

- ## 

- ## 🔥 [Databases always have a schema (2018) | Hacker News_201902](https://news.ycombinator.com/item?id=19244080)

- ## 🔥 [Database schema changes are hard (2017) | Hacker News_201903](https://news.ycombinator.com/item?id=19286885)
- 
- 
- 

# discuss
- ## 

- ## 

- ## 🔥 [How to build a IP geolocation database from scratch? | Hacker News_202309](https://news.ycombinator.com/item?id=37507355)
- 
- 
- 

- ## 🔥 [Why you might want a domain-specific database like TigerBeetleDB | Hacker News_202209](https://news.ycombinator.com/item?id=32779851)
- 
- 
- 

- ## 🔥 [A table that should exist in all projects with a database | Hacker News_201012](https://news.ycombinator.com/item?id=1984325)
- 
- 
- 

- ## 🔥 [The Database Inside Your Codebase | Hacker News_202102](https://news.ycombinator.com/item?id=26160186)
- 
- 
- 

- ## 🔥 [Ask HN: Do you self-host your database? | Hacker News_202106](https://news.ycombinator.com/item?id=27671376)
- 
- 
- 

- ## 🛢️🔥 [The database I wish I had | Hacker News_202009](https://news.ycombinator.com/item?id=24337244)
- 
- 
- 

- ## 🤔 [Ask HN: How to handle 50GB of transaction data each day? (200GB during peak) | Hacker News_201602](https://news.ycombinator.com/item?id=11157829)
- Can confirm, don't use mongo. We're stuck with it now, and I really wish we had used Postgres for biz data and Cassandra for the high volume non-relational data. They're just materialized views on-top of your event stream anyway.

- Check out LinkedIn's posts about log processing and Apache Kafka. Handling data as streams of events lets you avoid spikey query-based processing, and helps you scale out horizontally. Partitioning lets you do joins, and you can still add databases as "materialized views" for query-ability. Add Secor to automatically write logs to S3 so you can feel secure in the face of data loss, and use replication of at least 3 in your Kafka topics.

- ## 🔥 [We put a distributed database in the browser and made a game of it | Hacker News_202307](https://news.ycombinator.com/item?id=36680535)
- Is this something similar to couch/pouchdb?
  - TigerBeetle is more domain-specific, i.e. focused on financial transactions and high-performance, high-availability. There are just two entity types in the database: accounts and transfers between accounts. 
- > In comparison to {C, P}ouchDB, I think the question is around offline-first availability.
  - Got it, thanks! Yeah that is indeed not how TigerBeetle works. If you ever cannot connect to the cluster, you keep retry messages (idempotently) until you connect and the message succeeds.

- ## 和ChatGPT聊DB设计获得新知，Nested Set Model：
- https://twitter.com/TooooooBug/status/1659041013800001536
  - 将父子关系映射到数轴上变为数字范围的包含关系，然后通过数字范围大小就能计算出各条记录的父子关系，避免反复递归。
