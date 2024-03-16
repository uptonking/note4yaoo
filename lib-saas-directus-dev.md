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
  - 在admin添加新的data-model时，数据库会创建对应的表，但后端无需生成代码，支持动态访问，相比之下，strapi不支持在生产环境中添加model需要restart
  - Works with new or existing SQL databases, no migration required
  - plug-and-play, so you're free to link or remove it anytime, with zero impact on your data
  - 强大的权限系统，支持per-field和conditional
  - 内置数据库表名有统一前缀
  - 支持realtime updates
  - Extensions provide a way to modify or expand Directus' functionality
  - 支持postgis
  - flows

- cons
  - license: GPLv3 > BSL
  - built with vue3

- features
  - 核心模块: content, user, files, flows, insights/dashboard
  - instant REST+GraphQL API on top of any SQL database
  - Our no-code Vue.js app is intuitive for non-technical users
# dev-xp
- 在admin添加新的data-model时，数据库会创建对应的表，~~同时后端src/api下面会自动生成对应的schema/router/controller/service~~

## dev-done

- 登录界面一直白屏，排查了很久未定位到原因，但firefox可正常打开，chrome体系都是白屏
  - [Unable to run Directus locally](https://github.com/directus/directus/issues/17786)
  - You have to set `SERVE_APP=true` in your .env file in order to run the api in dev mode with the build app.
  - 最终发现配置server_app后要访问的是服务端:8055/admin，而不是前端:8080/admin
# codebase
- flows
  - 基于vuedraggable实现，未使用其他外部依赖

- graphql用的不多
  - 前端app主要是insights部分
  - 后端包括controller/**service**/middleware, 移除需要一定的工作量
# more
