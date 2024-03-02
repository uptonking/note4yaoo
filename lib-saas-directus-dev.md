---
title: lib-saas-directus-dev
tags: [cms, directus]
created: 2024-02-16T14:55:26.345Z
modified: 2024-02-16T14:55:58.271Z
---

# lib-saas-directus-dev

# guide
- pros
  - 支持 content versioning
  - 数据修改更新的架构采用delta的设计
  - 在admin添加新的data-model时，数据库会创建对应的表，但后端无需生成代码，
    - 支持动态访问，相比之下，strapi不支持在生产环境中添加model
  - Works with new or existing SQL databases, no migration required.
  - Extensions provide a way to modify or expand Directus' functionality

- cons
  - license: GPLv3 > BSL

- features
  - instant REST+GraphQL API on top of any SQL database
  - Our no-code Vue.js app is intuitive for non-technical users
# dev
- 在admin添加新的data-model时，数据库会创建对应的表，~~同时后端src/api下面会自动生成对应的schema/router/controller/service~~
# more
