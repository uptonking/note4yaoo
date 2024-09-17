---
title: lib-db-mongodb-community
tags: [community, mongodb]
created: 2022-06-13T02:58:50.821Z
modified: 2022-06-13T02:59:04.350Z
---

# lib-db-mongodb-community

# guide

- resources
  - [Feature Comparison of MongoDB GUI tools (Jan 2024) | Top MongoDB GUI Tools](https://www.mongodb-gui-tools.com/)
# discuss-stars
- ## 

- ## 

- ## 
# discuss-news-mongo
- ## 

- ## 

- ## 🗑️ [MongoDB deprecates Atlas Device sync | Hacker News _202409](https://news.ycombinator.com/item?id=41489636)
- Really devastating. I think the rename from Realm is why people haven't noticed this, but I guess also its popularity really has dwindled. Even though I only use local RealmSwift, I don't trust that the community will be able to keep it going even in maintenance mode.

- Adam (CEO of Ditto) here, Mongo is transitioning to a partner-first strategy for mobile and edge applications. We are working closely with Mongo to create a cohesive product experience between Ditto and Mongo Atlas. High-level that is a supported bidirectional connector between Atlas and Ditto's Edge Sync platform.
  - Furthermore, we are working with customers of Atlas Device Sync to help and support them in the transition. There are aspects of Ditto different than Realm - most prominent is that we are schema-less. This will mean some client-side code transition, but longer-term a tighter alignment with Mongo Atlas. We are excited as well to introduce more to Ditto's unique capability of P2P device sync.
# discuss-usecase-xp
- ## 

- ## 

- ## 🔥 [HSBC moves from 65 relational databases into one global MongoDB database | Hacker News_202006](https://news.ycombinator.com/item?id=23507197)
- Jepsen's latest analysis of MongoDB -- https://jepsen.io/analyses/mongodb-4.2.6 -- finds that it doesn't even preserve snapshot isolation when set at the highest consistency level. This seems like a pretty terrible decision.

- There’s been a lot of talk about the Jepsen-Mongo affair on HN lately, but the problem I have with Mongo and NoSQL in general is much more basic - it’s modeling relationships, which always end up appearing in every data model I’ve ever designed. I’m aware you can keep references from one doc to another but it always ends up being a messy affair even at smallish scales, and it feels as if the cognitive burden of managing these relationships ends up falling on the dev, instead of being managed by the DB.
- Mongodb now supports effectively "Joins" in its aggregation framework, so it can do some relational style data representation. The latest versions also support transactions.
  - Yeah but they do not recommend using that. I think the one nosql afficianado in my team spoke with mongo support and they recommended reassessing our document structure for it
  - We’re still concerned that $lookup can be misused to treat MongoDB like a relational database

- Mongodbs newer versions support schema validation by allowing you to register a JSON-Schema description against a collection and validate writes against It.
# discuss
- ## 

- ## MongoDB finds most users stick to defaults when it comes to consistency settings  
- https://twitter.com/PeterZaitsev/status/1756688542502474001
  - [Tunable Consistency in MongoDB _202402](https://muratbuffalo.blogspot.com/2024/02/tunable-consistency-in-mongodb.html)

- ## [MongoDB Compass looks great and is free, is there any reason to use Robo 3T or Studio 3T anymore? : mongodb _202103](https://www.reddit.com/r/mongodb/comments/m1sr4z/mongodb_compass_looks_great_and_is_free_is_there/)
- I have used compass, studio 3T, and noSqlBooster and noSqlBooster is by far the best if you are good with JavaScript IMO. 
  - It has the easiest way to write complex 1 off scripts and incorporates lodash and moment globally for scripts which is incredibly useful. It has mongoose like syntax built in. 
  - The product is very well maintained and they have some very big name customers.
  - [Compare Editions - NoSQLBooster for MongoDB](https://nosqlbooster.com/compareEditions)

- ## [To denormalize the TPC-H benchmark dataset_202202](https://www.mongodb.com/community/forums/t/to-denormalize-the-tpc-h-benchmark-dataset/147309)
  - I want to denormalize the TPC-H dataset having 8 relational tables and 22 relational queries. I want to migrate the relational database into MongoDB
- I don’t think there is enough clarity to provide a recommendation. 
  - There will be not the one and only answer. 
  - Your schema highly depends on how data is accessed. 
  - 👉🏻 One rule of thumb is: that data that is accessed together should be stored together. 
  - Bases on this you will first need to evaluate your access pattern, define the most important queries, find relationships, define patterns to use. 
  - We need to take into account data durability and staleness at this point as well as cost of maintaining duplicated data / indices vs. fast access.

- ## [MongoDB 的表上怎么做 JOIN？ - 知乎](https://www.zhihu.com/question/486997525/answers/updated)
- mongodb的aggregate功能很强大。连表可用$lookup。
- 我在去年也问过这个问题，现在我可以回答你，如果你问这个问题，说明你需要切换成postgres或者mysql

- [详解MongoDB中的多表关联查询（$lookup） - 东山絮柳仔 - 博客园](https://www.cnblogs.com/xuliuzai/p/10055535.html)

- ## [国内有没有成功使用MongoDB作为主存数据库的案例？ - 知乎](https://www.zhihu.com/question/35635370/answers/updated)
- 我们公司，Bmob后端云，http://www.bmobapp.com。 
  - 从13年云上线，客户的数据就一直用的MongoDB，使用快10年了。 
  - 内存使用高、并发高的时候响应慢这些都是跟你请求量有关，也跟你查询索引优化有关
  - 我们遇到目前最大一个坑就是数据库的实时状态，库表命名空间当大于16MB使用不了mongotop命令，这个坑。
  - 这个命令很重要，并且没有可以替换的方案
- 当前mongodb在我司拥有5000个实例，数万亿级数据量。QPS历史峰值也近千万级别，集群中单表最大千亿级别。
  - 以当前我司业务使用mongodb过程为例，以下场景不适合选择mongodb，也不适合选择mysql：
  - 8字段以上的随机组合查询，由于mongodb、mysql等数据库都需要自己手动创建索引，8字段以上的组合情况太大，因此索引不容易建
  - 非前缀匹配的模糊查询
  - 全文检索
- 网易游戏几乎全部MongoDB
  - 做游戏用mongo绝对是爽，需求变化太快了，

- ## 🔥 [Show HN: AvionDB: A Decentralised Database with MongoDB-like Developer Interface | Hacker News_202005](https://news.ycombinator.com/item?id=23058070)
- 
- 
- 
