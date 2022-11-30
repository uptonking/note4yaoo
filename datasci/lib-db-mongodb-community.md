---
title: lib-db-mongodb-community
tags: [community, mongodb]
created: 2022-06-13T02:58:50.821Z
modified: 2022-06-13T02:59:04.350Z
---

# lib-db-mongodb-community

# guide

# discuss
- ## 

- ## 

- ## 

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
