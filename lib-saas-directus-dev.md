---
title: lib-saas-directus-dev
tags: [cms, directus]
created: 2024-02-16T14:55:26.345Z
modified: 2024-02-16T14:55:58.271Z
---

# lib-saas-directus-dev

# guide
- pros 支持扩展api和ui
  - ⌛️ 支持content versioning
    - 数据修改更新的架构采用delta的设计
    - 提供了用户所有的操作log, activity feed
  - 在admin添加新的data-model时，数据库会创建对应的表，但后端无需生成代码，支持动态访问，相比之下，strapi不支持在生产环境中添加model需要restart
  - 🛢️ Works with new or existing SQL databases, no migration required
    - plug-and-play, so you're free to link or remove it anytime, with zero impact on your data
  - 内置数据库表名有统一前缀
  - rich-fields: rich-text
    - 支持custom field type(基于extension),需要写代码
  - rich-views: table, kanban, calendar, card, map
    - 支持custom layouts
  - 强大的权限系统，支持per-field
  - 支持realtime updates
  - 🔌 Extensions provide a way to modify or expand Directus' functionality
  - Sandboxed Extensions
  - 支持postgis
  - 〰️ flows
  - 🎛️ insights/dashboard
  - 用户管理
  - 通知系统

- cons 定位不明确 cms vs app
  - license: GPLv3 > BSL
  - auth实现复杂，token包括jwt/session/static三种
  - content的视图无法保存，不能实现类似notion database切换多种视图
  - 开发ext实现热加载比较麻烦

- 📈 表格不支持拖拽调整row顺序，但支持拖拽调整column顺序
  - 不支持在任意位置插入row, 支持在设置而不是表格中添加列和调整列顺序
  - 不支持分组视图，aggregate接口支持groupBy
  - ✅ 支持拖拽调整列宽度
  - 支持conditional-fields
  - 支持group fields

- features
  - 核心模块: content, user, files, flows, insights/dashboard
  - 表格默认处于查看状态
  - built with vue3
  - instant REST+GraphQL API on top of any SQL database
  - Our no-code Vue.js app is intuitive for non-technical users
# draft
- collections
  - 优化方案，修改schema时数据库层数据操作可能过多，可采用冷热模式，冷模式即目前的方案直接修改schema，热模式会先修改中间表或内存然后等一段时间再持久化同步到db
# dev-xp

```shell
# start dev app
pnpm --filter api dev
pnpm --filter app dev
```

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
- [Advanced Filtering: Dates, Aggregation & Grouping, and Combining Filters | Directus Docs](https://docs.directus.io/blog/advanced-filtering-dates-aggregation-and-grouping-and-combining-filters.html)
