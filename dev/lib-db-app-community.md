---
title: lib-db-app-community
tags: [community, database]
created: 2021-08-30T15:50:29.925Z
modified: 2023-09-16T17:54:11.257Z
---

# lib-db-app-community

# guide

# discuss
- ## 

- ## 🔥 [Searchable and sortable H1B salary database | Hacker News_202306](https://news.ycombinator.com/item?id=36277706)
- 
- 
- 

- ## 🔥 [If All You Have Is a Database, Everything Looks Like a Nail(钉子) | Hacker News_202012](https://news.ycombinator.com/item?id=25330223)
- I like the idea the author mentions of message queues in the database. It also sounds like it would be easier to separate if need be. I also like the idea of keeping everything in a single database as long as possible. Even if it turns out not to scale, it is a lot easier to figure out your business logic in that environment. Anything which avoids microservice madness and Kubernetes keenness as long as possible is very attractive to me.

- Why do blobs cause transactional problems? Create the blob. GIve it an ID. Give it a path/URL. Do all that before going anywhere near the database, at which point the blob is all settled an immutable. Then, stick the tiny record into the database which identifies the blob. Done; the blob is now live, from the POV of the database consumers.

- ## [Ask HN: Why are we so fragmented in databases options? | Hacker News_202210](https://news.ycombinator.com/item?id=33345464)
- Relational databases have dominated since the 1980s. 

- ## this is an excellent lecture on the history of DB, 
- https://twitter.com/mim_djo/status/1632318627142852610
  - although Google Map reduce system was a bad idea, all new shared disk DWH ( BigQuery, Snowflake, Dremio, Databricks etc ) stole the best part from it, which is separating Storage from Compute
- relational DB system are just too good in stealing other people innovations.
  - Separating compute from storage
  - Json
  - Graph
  - Open table format (Iceberg, delta)

- ## [Things I learned after getting users | Hacker News_202303](https://news.ycombinator.com/item?id=35132223)
- i relied on a SQL ORM which in short is a tool that makes writing SQL easier to pick up and faster to develop. the biggest downside is that it might execute 50 queries to your database to get a list of information, when it probably only needs 1, which will cause slowdown
  - I appreciate this honesty. Listen to this old man's advise: learn SQL properly. It's not that hard. Focus on it for a few weeks intensely and you've mastered it for life. Then just write SQL directly.
