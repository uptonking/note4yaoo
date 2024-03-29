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
  - 在admin添加新的data-model时，数据库会创建对应的表，但后端无需生成代码
    - strapi不支持在生产环境中添加model，需要restart
  - 🛢️ Works with new or existing SQL databases, no migration required
    - plug-and-play, so you're free to link or remove it anytime, with zero impact on your data
    - 支持postgis 🌍
  - 内置数据库表名有统一前缀
  - rich-fields: rich-text
    - 支持custom field type(基于extension),需要写代码
  - rich-views: table, kanban, calendar, card, map
    - 支持custom layouts
  - 强大的权限系统，支持per-field
  - 支持realtime updates
  - 🔌 Extensions and marketplace
    - marketplace支持自定义地址 MARKETPLACE_REGISTRY
  - Sandboxed Extensions, ✨ 支持在线安装扩展
  - 〰️ flows
  - 🎛️ insights/dashboard
  - 用户管理
  - 通知系统
  - 支持i18n, 偏向于简单翻译，提供了translations类型的字段，会自动建立关联表
    - lang/content表需要用户自己创建和配置

- cons 定位不明确 cms vs app
  - license: GPLv3 > BSL
  - auth实现复杂，token包括jwt/session/static三种
  - content的视图无法保存，不能实现类似notion database切换多种视图
  - 开发ext实现热加载比较麻烦
  - 不支持rename collection/table和field
  - versioning的其他版本只能从main创建，不能从其他version再创建version

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

- 支持i18n, 提供了translations类型的字段，会自动建立关联表
  - 所有内容仍在db的同一张表中，lang/content表需要用户自己创建和配置
  - 内容列表显示时同一内容的翻译显示成一篇文章
  - 支持并排显示多语言的内容

- promote其他版本到main版本的过程，像极了github的pr
  - 但没有冲突处理的工具，处理结果是替换，main版本中的新修改会丢失
  - promote后对结果不满意还可以revert

## dev-done

- 登录界面一直白屏，排查了很久未定位到原因，但firefox可正常打开，chrome体系都是白屏
  - [Unable to run Directus locally](https://github.com/directus/directus/issues/17786)
  - You have to set `SERVE_APP=true` in your .env file in order to run the api in dev mode with the build app.
  - 最终发现配置server_app后要访问的是服务端:8055/admin，而不是前端:8080/admin

## dev-revision-history

- 更新一行内容时 `PATCH /items/test_version11/0a18dd69-uuid` api
  - 但发送的是字段级的全量内容，不是行级

```JS
// 更新内容时发送的payload
{
  "details": {
    "time": 1711727969329,
    "blocks": [{
        "id": "njYQrT6OH1",
        "type": "paragraph",
        "data": {
          "text": "- 0329 this is not main version，main11"
        }
      },
      {
        "id": "vMCeybDP_N",
        "type": "paragraph",
        "data": {
          "text": "&gt; main version 变化时， 其他version也会变化, 符合预期吗"
        }
      },
    ],
    "version": "2.28.2"
  }
}

// 用户编辑rich-text字段时，db directus_revisions表的内容，delta字段的内容
// 创建时
{
  "title": "simple-text",
  "details": {
    "time": 1711728688829,
    "blocks": [{
      "id": "ld4zbGf7AA",
      "type": "paragraph",
      "data": {
        "text": "hello"
      }
    }],
    "version": "2.28.2"
  }
}
// 更新时
{
  "details": {
    "time": 1711728704077,
    "blocks": [{
      "id": "ld4zbGf7AA",
      "type": "paragraph",
      "data": {
        "text": "hello, 20240330"
      }
    }],
    "version": "2.28.2"
  },
  "user_updated": "b24c015b-10b2-4d37-b38a-29410b3deb3d",
  "date_updated": "2024-03-29T16:11:45.556Z"
}
```

# more
- [Advanced Filtering: Dates, Aggregation & Grouping, and Combining Filters | Directus Docs](https://docs.directus.io/blog/advanced-filtering-dates-aggregation-and-grouping-and-combining-filters.html)
