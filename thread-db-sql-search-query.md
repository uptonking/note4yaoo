---
title: thread-db-sql-search-query
tags: [search, sql, thread]
created: 2022-06-11T20:34:39.918Z
modified: 2022-06-11T20:35:11.775Z
---

# thread-db-sql-search-query

# guide

- datomic-alternative
  - clojure: datascript, xtdb, datahike, datalevin
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## SQL 使用带大小写的字段查询时，带上双引号即可。 select * from [table] where “pId” = “123”
- https://twitter.com/EryouHao/status/1535541208910483457
  - 之前不知道，还由于这个把数据库中的字段都命名为 snake_case 格式。
  - 于是陷入了在 TypeScript、lint、前端字段转换的痛苦之中。

- 不同数据库的引号处理机制是有差异的，对未来可能的数据库选型迁移不太友好，所以还是**更建议以 snake case 来命名字段**
