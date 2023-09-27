---
title: lib-db-model-eav-triple
tags: [database-design, entity-attribute-value, triplestore]
created: 2023-09-24T18:20:30.236Z
modified: 2023-09-25T17:52:46.690Z
---

# lib-db-model-eav-triple

# guide

- pros
  - highly flexible for schema
  - no ddl permissions required, 无需在运行时创建新表
  - eav模型与数据库特性无关，需要自己实现查询和join，而json与db特性绑定

- cons
  - 在数据增长时，性能下降很快
  - 和orm结合起来的查询或操作更繁琐
  - complex query，sql冗长
  - complex join

- who is using #eav-db
  - magento

- alternatives-eav
  - jsonb/json: 通常是平台相关的
  - inner platform
  - **property graph**: PG/GPQ
  - more: ms-power-query

- 直接根据具体框架或产品搜索解决方案如airtable-database，不必拘泥于通用方案如event-sourcing/eav/triple
  - 可参考airtable, monday.com, nocodb, apitable

- query
  - 对graph模型的查询，当前主流方案是datalog/cypher，未来标准是gql/pgq
  - property label graph
  - SQL/PGQ: apache-age

- tips
  - eav和schema并不对立，很多cms都会在固定表外提供eva插件，允许用户自定义部分功能
  - EAV performance at large scale is really dreadful
# dev
- [EAV Zero to EAV Hero! - by Magento developer - YouTube_201503](https://www.youtube.com/watch?v=WneHTRZVbec)

- [Triplestore - Wikipedia](https://en.wikipedia.org/wiki/Triplestore)
  - A triplestore or RDF store is a purpose-built database for the storage and retrieval of triples through semantic queries. 
  - A triple is a data entity composed of `subject–predicate–object`, like "Bob is 35" or "Bob knows Fred".
# more
