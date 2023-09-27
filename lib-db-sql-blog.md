---
title: lib-db-sql-blog
tags: [blog, sql]
created: 2023-03-12T14:41:59.976Z
modified: 2023-03-12T14:42:08.788Z
---

# lib-db-sql-blog

# guide

# query-non-sql

# N+1

## [数据库查询的N+1问题](https://blog.icehoney.me/posts/2021-02-20-sql-n-1/)

- 举一个简单的例子，数据库中有一张 cars 表存储汽车的相关信息，还有一张 wheels 表存储汽车的轮胎信息。
  - SELECT * FROM cars; 
  - SELECT * FROM wheels WHERE car_id = ${car_id}; 
- 这里的 N 就是汽车的数量，如果需要知道每个汽车的轮胎信息那就正好需要**查询 N+1 次**。

- 如果汽车和轮胎是一对一的关系可以通过使用 `join` 语句来减少数据库查询次数
  - SELECT cars.*, wheels.* FROM cars INNER JOIN wheels ON wheels.car_id = cars.id
  - 把**查询降为1次**。

- 如果汽车和轮胎是一对多的关系可以通过使用 `IN`：
  - SELECT * FROM cars; 
  - SELECT * FROM wheels WHERE wheels.car_id IN (1, 2, 3)
  - 把**查询降为2次**。

- Django 可以使用select-related(opens new window) 和 prefetch-related(opens new window)来解决这个问题。
  - select-related 主要用于一对一的关系，而 prefetch-related 主要用于多对多或者多对一的关系。
- Ruby on Rails 使用 includes(opens new window) 来解决 N+1 问题。

- 后端开发需要时刻注意 N+1 问题， 在开发模式下，日志会输出 SQL 查询语句，需要多加注意。也可以使用一些工具来检测这个问题。

## [[科普文]什么是ORM中的N+1 - 知乎](https://zhuanlan.zhihu.com/p/27323883)

- User和Post是一对多的关系，也就是User是Post的外键。
  - 有一个需求，展示一个文章列表页：文章标题，文章作者名称。就这两个字段，也不需要分页。
- 这个问题并不难，但对于新手而言，可能常常会犯的一个错误就是在循环中进行查询。
- 这样做是非常糟糕的，数据量小还少，在数据量较大的情况下，是非常消耗数据库性能的。
- N+1问题就是这样产生的：查询主表是一次，查询出N 条记录，根据这N 条记录，查询关联的副（从）表，共需要N 次。所以，应该叫1+N 问题更合适一些。

- 其实，如果稍微了解一点SQL，根本不用这么麻烦，直接使用 `IN` 一次就搞定了。

- 对于这类问题，ORM 其实为我们提供了相应的方案，那就是使用『预加载功能』。
  - 使用with()方法指定想要预加载的关联
# more
