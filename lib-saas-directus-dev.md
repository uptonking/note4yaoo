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
    - 数据修改更新的架构采用 `delta` 的设计
    - 提供了用户所有的操作log, activity feed
  - 在admin添加新的data-model时，数据库会创建对应的表，但后端无需生成代码
    - strapi不支持在生产环境中添加model，需要restart
    - ✨ 社区提供了rename/schema-change的方案
  - 🛢️ Works with new or existing SQL databases, no migration required
    - plug-and-play, so you're free to link or remove it anytime, with zero impact on your data
    - 支持postgis 🌍
  - 内置数据库表名有统一前缀
  - 支持集群部署水平scaling
  - rich-fields: block-editor, WYSIWYG, markdown
    - 支持custom field type(基于extension),需要写代码
  - 🪟 rich-views: table, kanban, calendar, card, map
    - 支持custom layouts
  - 强大的权限系统，支持per-field
  - 🔌 Extensions and marketplace
    - marketplace支持自定义地址 MARKETPLACE_REGISTRY
  - Sandboxed Extensions, ✨ 支持在线安装扩展
  - ⛓️ flows
    - 可灵活使用flow的trigger来实现op的暂停和继续
  - 🎛️ insights/dashboard
  - 〰️ 支持realtime data, 包括rest/graphql
    - sdk支持通过参数配置启用websocket
  - 支持i18n, 偏向于简单翻译，提供了translations类型的字段，会自动建立关联表
    - lang/content表需要用户自己创建和配置，自动化程度不高
  - 用户管理
  - 通知系统

- cons 定位不明确 cms vs app
  - license: GPLv3 > BSL
  - auth实现复杂，token包括jwt/session/static三种
  - 👀 不支持rename collection/table和field
  - content的视图无法保存，不能实现类似notion database切换多种视图
  - 开发ext实现热加载比较麻烦
  - versioning的其他版本只能从main创建，不能从其他version再创建version

- 📈 表格不支持拖拽调整row顺序，但支持拖拽调整column顺序
  - 不支持在任意位置插入row, 支持在设置而不是表格中添加列和调整列顺序
  - 不支持分组视图，aggregate接口支持groupBy
  - ✅ 支持拖拽调整列宽度
  - 支持conditional-fields
  - 支持group fields

- features
  - 核心模块: content, user, files, flows, insights/dashboard
  - 表格默认处于只读查看状态，而不是编辑状态
  - built with vue3
  - 📝 block-editor使用editorjs, wysiwyg使用tinymce.v6
  - instant REST+GraphQL API on top of any SQL database
  - Our no-code Vue.js app is intuitive for non-technical users
  - v12 has field-level locking and presence indicators, but not CRDT character-level editing.
  - import JSON or CSV files into your collection as items.
  - export items menu provides granular control over exactly which items and fields are exported: CSV, JSON, XML, or YAML

- who is using #directus
  - ?

- tips
  - ?
# draft
- collections
  - 优化方案，修改schema时数据库层数据操作可能过多，可采用冷热模式，冷模式即目前的方案直接修改schema，热模式会先修改中间表或内存然后等一段时间再持久化同步到db

- 影响范围大的operation如何设计实现，如插入row/column

- relation关系数据的联动显示功能很强大，但意外修改的影响范围也很大，且难以undo
# dev-xp

```shell
# start dev app
pnpm i
pnpm build
pnpm --filter api dev
pnpm --filter app dev
```

- 在admin添加新的data-model时，数据库会创建对应的表， ~~同时后端src/api下面会自动生成对应的schema/router/controller/service~~ 

- 支持i18n, 提供了translations类型的字段，会自动建立关联表
  - 所有内容仍在db的同一张表中，lang/content表需要用户自己创建和配置，自动化程度不高
  - 内容列表显示时同一内容的翻译显示成一篇文章
  - 支持并排显示多语言的内容

- promote其他版本到main版本的过程，像极了github的pr
  - 但没有冲突处理的工具，处理结果是替换，main版本中的新修改会丢失
  - promote后对结果不满意还可以revert

## dev-done

- 登录界面白屏，排查很久未定位到原因，但firefox可正常打开，chrome体系都是白屏
  - [Unable to run Directus locally](https://github.com/directus/directus/issues/17786)
  - You have to set `SERVE_APP=true` in your .env file in order to run the api in dev mode with the build app.
  - 最终发现配置server_app后要访问的是服务端:8055/admin，而不是前端:8080/admin
  - 可能是本地开发时url对应域名的localStorage或cookie存在其他开发的token

## dev-flows

- 可灵活使用flow的trigger来实现op的暂停和继续

## dev-revision-history

- undo可考虑基于revision-history实现

- 更新一行内容时 `PATCH /items/test_version11/0a18dd69-uuid` api
  - 但发送的是字段级的全量内容，不是行级

### 📌 创建内容

```JS
// POST /items/articles
// payload
{
  "title": "post03301824",
  "contents": "# hi, post03301824"
}
// response
{
  "id": "ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643",
  "title": "post03301824",
  "contents": "# hi, post03301824",
  "user_created": "01198d9a-07a0-4f20-b2e2-927d7253d8bd",
  "date_created": "2024-03-30T10:35:04.113Z",
  "user_updated": null,
  "date_updated": null
}

// 📌 更新内容时
// PATCH /items/articles/ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643
// 更新markdown类型字段，基于codemirror
// payload 只包含修改过的字段，title未变化所以没发送
{
  "contents": "# hi, post03301824\n\n- aa"
}
// 更新rich-text类型字段，基于editorjs
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

// 👉🏻 更新rich-text字段时，db directus_revisions表的delta字段的内容
// 创建时的delta
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
// 更新时的delta
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

### 📌 获取revisions

```JS
// GET  /revisions?filter[_and][0][collection][_eq]=articles&filter[_and][1][item][_eq]=ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643&filter[_and][2][version][_null]=true&sort=-id&limit=10&page=0&fields[]=id&fields[]=data&fields[]=delta&fields[]=collection&fields[]=item&fields[]=activity.action&fields[]=activity.timestamp&fields[]=activity.user.id&fields[]=activity.user.email&fields[]=activity.user.first_name&fields[]=activity.user.last_name&fields[]=activity.ip&fields[]=activity.user_agent&fields[]=activity.origin
// response
[{
    "id": 277,
    "data": {
      "id": "ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643",
      "user_created": "01198d9a-07a0-4f20-b2e2-927d7253d8bd",
      "date_created": "2024-03-30T10:35:04.113Z",
      "user_updated": "01198d9a-07a0-4f20-b2e2-927d7253d8bd",
      "date_updated": "2024-03-30T10:38:02.430Z",
      "title": "post03301824",
      "contents": "# hi, post03301824\n\n- aa"
    },
    "delta": {
      "contents": "# hi, post03301824\n\n- aa",
      "user_updated": "01198d9a-07a0-4f20-b2e2-927d7253d8bd",
      "date_updated": "2024-03-30T10:38:02.430Z"
    },
    "collection": "articles",
    "item": "ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643",
    "activity": {
      "action": "update",
      "timestamp": "2024-03-30T10:38:02.432Z",
      "ip": "127.0.0.1",
      "user_agent": "Mozilla/5.0",
      "origin": "http://localhost:8080",
      "user": {}
    }
  },
  {
    "id": 276,
    "data": {
      "title": "post03301824",
      "contents": "# hi, post03301824"
    },
    "delta": {
      "title": "post03301824",
      "contents": "# hi, post03301824"
    },
    "collection": "articles",
    "item": "ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643",
    "activity": {
      "action": "create",
      "timestamp": "2024-03-30T10:35:04.119Z",
      "ip": "127.0.0.1",
      "user_agent": "Mozilla/5.0 ",
      "origin": "http://localhost:8080",
      "user": {}
    }
  }
]

// 📌 revision revert
// 本质是更新 PATCH items/articles/ff52b0e7-56e8-4d27-9ec8-d5cbdcacb643
```

### 📌 创建table-schema

```JS
// POST /collections
// payload
{
  "collection": "test_table11",
  "fields": [{
      "field": "id",
      "type": "uuid",
      "meta": {
        "hidden": true,
        "readonly": true,
        "interface": "input",
        "special": [
          "uuid"
        ]
      },
      "schema": {
        "is_primary_key": true,
        "length": 36,
        "has_auto_increment": false
      }
    },
    {
      "field": "status",
      "type": "string",
      "meta": {
        "width": "full",
        "options": {
          "choices": [{
              "text": "$t:published",
              "value": "published",
              "color": "var(--theme--primary)"
            },
            {
              "text": "$t:draft",
              "value": "draft",
              "color": "var(--theme--foreground)"
            },
            {
              "text": "$t:archived",
              "value": "archived",
              "color": "var(--theme--warning)"
            }
          ]
        },
        "interface": "select-dropdown",
        "display": "labels",
        "display_options": {
          "showAsDot": true,
          "choices": [{
              "text": "$t:published",
              "value": "published",
              "color": "var(--theme--primary)",
              "foreground": "var(--theme--primary)",
              "background": "var(--theme--primary-background)"
            },
            {
              "text": "$t:draft",
              "value": "draft",
              "color": "var(--theme--foreground)",
              "foreground": "var(--theme--foreground)",
              "background": "var(--theme--background-normal)"
            },
            {
              "text": "$t:archived",
              "value": "archived",
              "color": "var(--theme--warning)",
              "foreground": "var(--theme--warning)",
              "background": "var(--theme--warning-background)"
            }
          ]
        }
      },
      "schema": {
        "default_value": "draft",
        "is_nullable": false
      }
    },
    {
      "field": "user_updated",
      "type": "uuid",
      "meta": {
        "special": [
          "user-updated"
        ],
        "interface": "select-dropdown-m2o",
        "options": {
          "template": "{{avatar.$thumbnail}} {{first_name}} {{last_name}}"
        },
        "display": "user",
        "readonly": true,
        "hidden": true,
        "width": "half"
      },
      "schema": {}
    },
    {
      "field": "date_updated",
      "type": "timestamp",
      "meta": {
        "special": [
          "date-updated"
        ],
        "interface": "datetime",
        "readonly": true,
        "hidden": true,
        "width": "half",
        "display": "datetime",
        "display_options": {
          "relative": true
        }
      },
      "schema": {}
    }
  ],
  "schema": {},
  "meta": {
    "archive_field": "status",
    "archive_value": "archived",
    "unarchive_value": "draft",
    "singleton": false
  }
}

// response
{
  "collection": "test_table11",
  "meta": {
    "collection": "test_table11",
    "icon": null,
    "note": null,
    "display_template": null,
    "hidden": false,
    "singleton": false,
    "translations": null,
    "archive_field": "status",
    "archive_app_filter": true,
    "archive_value": "archived",
    "unarchive_value": "draft",
    "sort_field": null,
    "accountability": "all",
    "color": null,
    "item_duplication_fields": null,
    "sort": null,
    "group": null,
    "collapse": "open",
    "preview_url": null,
    "versioning": false
  },
  "schema": {
    "name": "test_table11",
    "sql": "CREATE TABLE `test_table11` (`id` char(36) not null, `status` varchar(255) not null default 'draft', `user_updated` char(36) null, `date_updated` datetime null, primary key (`id`))"
  }
}
// 📌 更新table-schema
```

# more
