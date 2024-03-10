---
title: lib-fwk-orm-sequelize-dev
tags: [orm, sequelize]
created: 2023-02-05T18:48:56.739Z
modified: 2023-02-05T18:49:11.444Z
---

# lib-fwk-orm-sequelize-dev

# guide
- pros
  - solid transaction support
  - read replication
  - 维护了框架无关的迁移工具 umzug

- cons
  - ?

- features
  - relations
  - eager and lazy loading
  - jsonb: 支持pg, 不支持sqlite

- who is using #sequelize-orm
  - cms: outline-wiki
  - app: nocobase
# dev
- model
  - MyModel.init部分的schema定义才会被同步到db，model class自身可包含额外属性和方法
# more
