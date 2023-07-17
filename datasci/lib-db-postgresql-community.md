---
title: lib-db-postgresql-community
tags: [community, postgresql]
created: 2022-06-13T03:00:54.134Z
modified: 2022-06-13T03:01:05.956Z
---

# lib-db-postgresql-community

# guide

# discuss
- ## 

- ## 骂PG 社区, 我只服姜老师, 哈哈哈哈哈  "中国的公有云数据库市场中，PG 的营收仅有 MySQL 的 0.1-0.3%
- https://twitter.com/baotiao/status/1680804553942515712

- ## [pg_jieba postgres14 分词和预期结果不一致](https://github.com/jaiminpan/pg_jieba/issues/54)

- ## [PostgreSQL中三种自增列sequence，serial，identity区别](https://www.cnblogs.com/wy123/p/13367486.html)
- 对于自增字段，无特殊需求的情况下，sequence不适合作为“自增列”，作为最最次选。
  - sequence在所有数据库中的性质都一样，它是跟具体的字段不是强绑定的，其特点是支持多个对个对象之间共享。
  - sequence类型的字段表，在使用CREATE TABLE new_table LIKE old_table的时候，新表的自增字段会已久指向原始表的sequence
  - sequence作为自增字段值的时候，对表的写入需要另外单独授权sequence
- identity是serial的“增强版”，更适合作为“自增列”使用。
  - identity本质是为了兼容标准sql中的语法而新加的，
  - 修复了serial的缺陷，如无法通过alter table的方式实现增加或者删除serial字段
- sequence，serial，identity共同的缺点
  - 是在显式插入之后，无法将自增值更新为表中的最大Id，这一点再显式插入的情况下是潜在自增字段Id冲突的
  - 自增列在显式插入之后，一定要手动重置为表的最大Id
