---
title: lib-db-app-community-etl-dbt
tags: [community, dbt, etl]
created: 2023-05-11T07:31:54.848Z
modified: 2023-12-15T18:03:33.503Z
---

# lib-db-app-community-etl-dbt

# guide

# blogs-dbt
- [How dbt succeeds - by Benn Stancil - benn.substack](https://benn.substack.com/p/how-dbt-succeeds)
# discuss-stars
- ## 

- ## 

- ## Today dbt announced column level lineage... but it's not open source and only available for paying cloud users. _202402
- https://twitter.com/Captaintobs/status/1757601463852023876
  - dbt is using SQLGlot (an open source SQL framework that my company @TobikoData maintains)  to power this newly gated feature.
- But there's an open source alternative to dbt cloud... @SQLMesh , where column level lineage is free and open source for everyone to use.
  - SQLMesh is backwards compatible with existing dbt projects, so you can gain all of its benefits without rewriting your project.

# discuss
- ## 

- ## 

- ## 

- ## 最近在计划一个全新的 #OpenDAL 子项目：oay，OpenDAL Gateway，允许用户使用最熟悉的 API 来访问不同的存储后端。
- https://twitter.com/AFutureD/status/1648685933330599936
- 事实上就是有不少给etcd加zookeeper API，给rocksdb加redis API 之类的项目。我觉得场景不是为了完全获得另一个系统的能力，而是为了不改代码获得一些好处。比如给redis上OSS API可能单纯就是小文件加速，不会去用scan

- 项目自己的定位和用户对项目的使用之间可能还有出入，而且很难说怎么去对齐一下
  - 这就是要贴近用户去思考了，OpenDAL 也过类似的故事。过去 OpenDAL 提供了 Object 的抽象，预期的是用户会重用同一个 Object 去做操作，但是 review 所有用户的代码后发现没人是这样用的，大家每次都在创建新的 Object，于是我直接把这层抽象拆掉了

- ## [A sequel to SQL? An intro to Malloy | Hacker News](https://news.ycombinator.com/item?id=32738874)
- It is the first thing I try to teach CS graduates: DRY ( re-usability) is not applicable in the SQL world. Trying to re-use code, as proposed in Malloy generally results in poor performing queries. Malloy also seems needlessly complex compared to highly successful tools like DBT.
  - One other reason that DBT is successful is the low threshold to migrate your existing codebase.
- DBT shines, not because of the language/templating, but because it handles a lot of the scut work of building out a data warehouse. Write the select statements you want to populate the model, write tests to constrain the model, and build.
