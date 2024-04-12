---
title: lib-saas-strapi-dev
tags: [strapi]
created: 2023-11-28T19:04:34.803Z
modified: 2023-12-15T16:51:56.101Z
---

# lib-saas-strapi-dev

# guide

- pros 支持扩展api和ui
  - MIT; features-rich; good documentation/community
  - 🔌 plugin-system and marketplace, 插件架构很彻底, 如ctb/cm
    - 但不支持类似directus的在线安装plugin
  - 📣 draft & publish, 不支持多个draft-version(directus支持)
  - free Custom Roles & Permissions since v4.8, 权限功能强大
  - media library and providers
  - i18n, 在架构层支持多语言，支持多语言的内容自动建立关联
  - future flags
  - Data Import & Export
  - rich fields: rich-text-blocks/markdown, media
    - 支持custom filed, 但需要写代码不能通过ui创建
    - 不支持dropdown,但有第三方插件支持
  - built with typescript
  - 提供了很多集成示例，如redis/search
  - 👀 支持rename field(需要restart)，不支持rename table
  - 开发plugins时支持热加载
  - 支持graphql

- cons
  - paid: Review workflow, Audit Logs, version-history
    - Shared Projects
    - ~~不支持version-history，但audit日志记录可作为类似功能~~
  - ui不支持: Conditional fields, nested component, nestable menu
  - rich views not supported
  - v4不支持mongodb
  - 🐛 与现有数据库集成不方便
  - 🚨 At this time and in the future there is no plan to allow model creating or updating while in a production environment, and
    - there is currently no plans to move model settings into the database. 
    - There are no known nor recommended workarounds for this.
  - It doesn't namespace its admin table
  - cannot store Content Manager layout configurations in the model settings. 因为未来移动版的layout可能不同，保存后如何恢复
  - 不支持undo, undo可考虑基于revision-history实现， v4支持unpublish
  - 不支持多种第三方登录
    - ❓ 如何与现有系统集成，可参考sso单点登录
  - rbac功能默认需要内置的10张表，复杂度高，难以迁移离开
  - 大版本的breaking-changes很多
  - media-lib可能存在大量未被使用的media，如何清理
  - user用户管理功能弱，不支持分组, 类似multi-tenancy
  - 前端旧版本的依赖难以升级，如react-router
  - 编辑内容点击save后，插件中的组件不会rerender更新，需要 location.reload
  - plugins
    - 🚨 plugin disable后再启动，plugin的db表数据、配置、自定义api会被删除，如builder
    - 纯前端的plugin不方便直接预览
    - 开发插件时server和admin无法共享工具方法，因为tsc的编译target分别是cjs/es5

- 📈 表格不支持拖拽调整row顺序和column顺序，但支持设置调整列顺序
  - 不支持在任意位置插入row, 支持在设置而不是表格中添加列和调整列顺序
  - 不支持拖拽调整列宽度
  - ✅ 支持group fields: components/dynamic-zone

- features
  - 核心模块: content-mgr, content-type-builder, media-lib, roles-permissions
  - 通过plugin支持 realtime data/notifications
  - Self-hosted or Cloud
  - compose fields: component/dynamic-zone
  - Modern Admin Pane
  - Multi-database support: PostgreSQL, MySQL, SQLite
  - Customizable: fully customizing APIs, routes, or plugins
  - Front-end Agnostic: any front-end framework, mobile apps or even IoT
  - Secure by default: Reusable policies, CORS, CSP, P3P, Xframe, XSS
  - flexible Content Types Builder: fields, components and Dynamic Zones
  - Media Library: Upload your images, videos, audio or documents 
  - i18n: create, manage and distribute localized content in different languages, called "locales"
  - Role Based Access Control: Create an unlimited number of custom roles and permissions for admin and end users.
  - GraphQL or REST: Consume the API using REST or GraphQL
  - 支持openapi doc
  - [Internationalization - Strapi Features](https://strapi.io/features/internationalization)

- features-enterprise
  - The only restrictions on the free version is that audit-logs and Review Workflows are not available

- who is using #strapi
  - luban-h5
  - VirtusLab

- cms vs framework
  - ?

- tips
  - 💡🤔 notion database 的设计思路是先填写数据再设置类型，而不是大多数cms的先设置类型再填写数据
  - 动态修改数据类型、修改schema

- resources
  - [Strapi Community Forum](https://forum.strapi.io/)
  - [Directus vs. Strapi – Comparison Headless CMS — Restack](https://www.restack.io/docs/directus-vs-strapi)
# draft/migrate-to-v5
- 📡 roadmap - lts: editor, excel-table, local-db
  - ~~掌握strapi-够用~~ > 模仿directus-config/delta > undb-fe-be > 模仿directus-flow > collab
  - migrate plugins to v5: versioning, media
  - editor: slate, quill, craftjs
  - i18n-cn: 多语言优化、版本控制
  - examples: realworld
- app-builder
  - 针对 移动端 短视频/小程序 的nocode更符合国内市场需求
  - build: admin, h5, mini-app, themes, cloud-component

- 基于ast实现lowcode的方案
  - craft/reka
  - tango, sparrow

- ⌛️ version/history
  - 参考官方实现来做开源版本，参考官方文档说明和代码
    - `packages/core/content-manager/server/src/history` 源码
    - `packages/core/admin/admin/src/content-manager/history/pages/History.tsx` 源码

- media
  - 🍴 fork media-lib/upload 实现文件管理、资源管理
  - files: docx/ppt
  - usage-references
  - ♻️ 支持回收站，默认删除到回收站, soft-delete

- frontend-admin
  - 🤔 将 content-type-builder 隐藏后是否就是普通网站的界面了
  - 参考curator实现自定义admin
  - 多层次的菜单 collapsible/nestable menu

- backend
  - api-rate-limit
  - open register

- plugins
  - 如何实现在线安装plugins
  - plugins settings page

- content-types
  - 🔒 让content-type-builder中的models在prod或默认环境下readonly，admin可开启edit
  - 让invisible状态的models处于折叠且只读的状态，而不是隐藏

- rich-fields
  - password

- flow
  - 🤔 考虑基于flow实现conditional fields

- gis
  - plugin-location: filter by coordinate, using postgis

- 流式输出 stream response

- more toC features

- 启动时自动切换到可用端口

- 单元格级别、卡片级别的权限控制，如隐藏部分看板卡片
# 🔌 plugins
- dev-xp
  - 🚨 plugin disable后再启动，plugin的db表数据、配置、自定义api会被删除，如builder

- export
  - ☑️ 不支持选择指定字段导出

- media
  - ☑️ media-preview 只生成缩略图却没有使用

- upload
  - 支持在不用建表或配置字段的情况下，导入导出excel/csv
  - 处理大文件的上传

- navigation
  - ☑️ 跳转到content item的路由失效

- 
- 

# 🖇️ integrations
- ❓ 如何与现有系统集成，可参考sso单点登录

- 集成react-admin
- 如何集成页面编辑器，如craft，可参考内置编辑器
# dev-v5
- v5插件的热加载问题很大，基于vite实现
  - 不能检测到新创建的文件，需要重启
# dev-xp
- 在admin添加新的content-type时，数据库会创建对应的表，同时后端src/api下面会自动生成对应的schema/router/controller/service，prod生产环境下不支持动态添加新的content-type

- 删除media-lib中的文件时，文件也会删除(待确认是否在回收站)

- 默认的role权限
  - author只能输入数据，不能查看其他人的数据，数据处于draft状态但不能publish
  - editor可以查看其他人的数据，可以publish

- ❓ 不支持查询所有现有的content-types; 似乎有折中方案
  - 待确认，因为content-type-builder可显示所有collection-types，需要分析请求的接口

- i18n支持admin配置界面语言和cm内容语言，提供了表级别的内容过滤显示
  - 所有内容仍在db的同一张表中，系统自动添加了`locale`字段
  - Content can only be managed one locale at the time. 
  - It is not possible to edit or publish content for several locales at the same time 
- 支持不同语言的entry~~共享部分字段~~，通过fill-in快速填充同名字段的内容
  - 同一文章会自动建立关联，支持切换语言时立即显示
  - 🧐 删除文章时会同时删除其他语言的内容
  - 支持将表的部分字段禁止多语言，即共享部分字段
  - ☑️ 不支持并排显示多语言的内容

- 不要直接在afterCreate/afterUpdate中修改response，这样admin界面不会显示修改
  - ❓ 通过route middleware可以更新admin界面的显示

- 支持的fields
  - rich-blocks: 基于slate
  - rich-markdown: 基于codemirror5

- 
- 

## dev-done

- ~~draft/publish的实现似乎只在api层面，admin界面的显示状态有问题~~, v5已解决

## dev-version-history

- features
  - switch versions
  - time-travel
  - multiple draft

- 要点
  - 更新内容时保存历史数据 /post/put
  - 返回数据时返回历史版本 /get

- 
- 
- 

## dev-content-versioning

- 在admin前端使用了非公开api `addMiddlewares`

### 📌 在ctb创建类型时，后端会创建schema.json文件

```JS
// payload POST /content-type-builder/content-types
{
  "components": [],
  "contentType": {
    "draftAndPublish": true,
    "pluginOptions": {
      "versions": {
        "versioned": true // 👈🏻
      }
    },
    "displayName": "test-version1",
    "singularName": "test-version1",
    "pluralName": "test-version1s",
    "kind": "collectionType",
    "attributes": {
      "body11": {
        "pluginOptions": {
          "versions": {
            "versioned": true // 👈🏻 
          }
        },
        "type": "string"
      }
    }
  }
}
// response
{
  "data": {
    "uid": "api::test-version1.test-version1"
  }
}
// 服务端自动生成的 schema.json
"attributes": {
  "body": {
    "pluginOptions": {
      "versions": {
        "versioned": true
      }
    },
    "type": "string"
  }
}
```

### 📌 在cm创建内容时，发送用户输入内容，返回带版本的完整内容

```js
// POST /content-manager/collection-types/api::test-version11.test-version11
// payload
{
  "title11": "hi11"
}
// response v4
{
  "id": 5,
  "title11": "hi11",
  "createdAt": "2024-03-28T04:10:11.152Z",
  "updatedAt": "2024-03-28T04:10:11.152Z",
  "publishedAt": null,
  "vuid": "24b728b9-878b-4c00-b70f-e262ab3bb8db",
  "versionNumber": 1,
  "versionComment": null,
  "isVisibleInListView": true,
  "createdBy": {
    "id": 1,
    "firstname": "admin",
    "lastname": "super",
    "username": null
  },
  "updatedBy": {
    "id": 1,
    "firstname": "admin",
    "lastname": "super",
    "username": null
  },
  "versions": []
}
// response v5
{
  "id": 3,
  "documentId": "xvvoa31x94xacp6anfp5ace0",
  "title11": "hi",
  "createdAt": "2024-03-28T04:27:30.940Z",
  "updatedAt": "2024-03-28T04:27:30.940Z",
  "publishedAt": null,
  "locale": null,
  "vuid": null,
  "versionNumber": 1,
  "versionComment": null,
  "isVisibleInListView": true,
  "createdBy": {
    "id": 1,
    "firstname": "admin",
    "lastname": "super",
    "username": null
  },
  "updatedBy": {
    "id": 1,
    "firstname": "admin",
    "lastname": "super",
    "username": null
  },
  "versions": [],
  "status": "draft"
}

// 📌 在cm更新内容时, url包含当前ver，返回的内容包含ver+1及所有旧version
// 后端会create创建新的row而不是update当前row，实现细节参考了i18n插件
// v4 PUT /content-manager/collection-types/api::test-version1.test-version1/2
// v5 PUT /content-manager/collection-types/api::test-version12.test-version12/xvvoa31x94xacp6anfp5ace0
// payload
{
  "id": 3,
  "body": "content123====",
  "createdAt": "2024-03-26T05:59:50.397Z",
  "updatedAt": "2024-03-26T05:59:50.397Z",
  "publishedAt": null,
  "vuid": "d8f65e57-1ec8-4069-9f9d-01ae56514213",
  "versionNumber": 3,
  "versionComment": null,
  "isVisibleInListView": true,
  "versions": [
    1,
    2
  ]
} {
  "title11": "hi11"
}
// response v4 会返回所有历史版本
{
  "id": 4,
  "body": "content123====",
  "createdAt": "2024-03-26T06:03:09.631Z",
  "updatedAt": "2024-03-26T06:03:09.631Z",
  "publishedAt": null,
  "vuid": "d8f65e57-1ec8-4069-9f9d-01ae56514213",
  "versionNumber": 4, // 👈🏻 最新版本
  "versionComment": null,
  "isVisibleInListView": true,
  "createdBy": {
    "id": 1,
    "firstname": "admin",
    "lastname": "super",
    "username": null
  },
  "updatedBy": {
    "id": 1,
    "firstname": "admin",
    "lastname": "super",
    "username": null
  },
  "versions": [{ // 👈🏻 所有历史版本，不包含最新版
      "id": 1,
      "body": "content",
      "createdAt": "2024-03-26T05:58:47.799Z",
      "updatedAt": "2024-03-26T05:58:47.799Z",
      "publishedAt": null,
      "vuid": "d8f65e57-1ec8-4069-9f9d-01ae56514213",
      "versionNumber": 1,
      "versionComment": null,
      "isVisibleInListView": false
    },
    {
      "id": 2,
      "body": "content1",
    },
    {
      "id": 3,
      "body": "content123",
      "createdAt": "2024-03-26T05:59:50.397Z",
      "updatedAt": "2024-03-26T05:59:50.397Z",
      "publishedAt": null,
      "vuid": "d8f65e57-1ec8-4069-9f9d-01ae56514213",
      "versionNumber": 3,
      "versionComment": null,
      "isVisibleInListView": false
    }
  ]
}
// response v5
{
  "data": {
    "id": 3,
    "documentId": "xvvoa31x94xacp6anfp5ace0",
    "title11": "hi11",
    "createdAt": "2024-03-28T04:27:30.940Z",
    "updatedAt": "2024-03-28T04:30:56.360Z",
    "publishedAt": null,
    "locale": null,
    "vuid": null,
    "versionNumber": 1,
    "versionComment": null,
    "isVisibleInListView": true,
    "createdBy": {
      "id": 1,
      "firstname": "admin",
      "lastname": "super",
      "username": null
    },
    "updatedBy": {
      "id": 1,
      "firstname": "admin",
      "lastname": "super",
      "username": null
    },
    "versions": [],
    "status": "draft"
  },
  "meta": {
    "availableLocales": [],
    "availableStatus": []
  }
}
```

- 
- 
- 
- 

# more
