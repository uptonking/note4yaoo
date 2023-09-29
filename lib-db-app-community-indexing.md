---
title: lib-db-app-community-indexing
tags: [community, database, indexing, query-engine, search]
created: 2023-09-17T17:37:32.457Z
modified: 2023-09-17T17:38:11.187Z
---

# lib-db-app-community-indexing

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [How does database indexing work? (2008) | Hacker News_202203](https://news.ycombinator.com/item?id=30594233)
- If you want to see a dumb example of how you can implement indexing on top of a SQL database without it, I wrote a tutorial on implementing basic indexes as part of a series on making a SQL database from scratch.
  - [Writing a SQL database from scratch in Go: 3. indexes](https://notes.eatonphil.com/database-basics-indexes.html)

- 
- 
- 

- ## [sql server - Will index be fully loaded into memory_201011](https://stackoverflow.com/questions/4296027/will-index-be-fully-loaded-into-memory)
- No, it's treated like any other data stored on disk. It's loaded into memory disk page by disk page. And a page stays in memory as long as it's regularly accessed.

- The answer to this is in several parts:
  - The size of the index.
  - What parts are accessed.
  - Memory pressure.
- SQL Server cached the index in memory as it was being read.
  - However, if I had put other memory pressure on SQL Server, it would have dropped out those cached index pages by order of lowest reads.

- ## [联合主键和复合主键和联合索引](https://www.cnblogs.com/saoge/p/14431536.html)
- 复合主键 就是指你表的主键含有一个以上的字段组成
- 联合主键 就是多个主键联合形成一个主键组合，联合就在于主键A跟主键B形成的联合主键是唯一的。

- [提问关于 mysql得联合主键和复合主键的问题 - SegmentFault 思否](https://segmentfault.com/q/1010000021884619)
  - 在英文语境中只有 Composite Primary Key（也有叫 Compound Primary Key 的），就是一个表中如果是多个字段组成一个主键，那么这个主键就被称为这玩意儿。
  - 这种概念是中文编程界（或者说是中文编程博客界）人为造出的。
  - 上面的例子看看就得了，根本就是胡编一个 联合主键 的定义出来，你会发现它其实就是一个最简单的自增主键，只不过表的逻辑上 student_id + subject_id 是唯一的，id 就成了所谓的二者的 联合主键。
