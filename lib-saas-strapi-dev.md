---
title: lib-saas-strapi-dev
tags: [strapi]
created: 2023-11-28T19:04:34.803Z
modified: 2023-12-15T16:51:56.101Z
---

# lib-saas-strapi-dev

# guide

- pros
  - MIT and features-rich
  - plugin system and marketplace
  - media library and providers
  - rbac is free
  - 支持audit日志记录
  - Data Import & Export
  - future flags
  - draft & publish
  - built with typescript
  - 提供了很多集成示例，如 redis/search

- cons
  - paid: Review workflow, Audit Logs, version-history, Shared Projects
    - ~~不支持version-history，但audit日志记录可作为类似功能~~
  - ui不支持: Conditional fields, nested component
  - 与已有数据库集成不方便
  - v4不支持mongodb
  - 🐛 At this time and in the future there is no plan to allow model creating or updating while in a production environment, and
    - there is currently no plans to move model settings into the database. 
    - There are no known nor recommended workarounds for this.
  - It doesn't namespace its admin table
  - 不支持多种第三方登录
  - rbac功能默认需要内置的10张表，复杂度高，难以迁移离开
  - 纯前端的plugin不方便直接预览
  - 大版本的breaking-changes很多
  - media-lib可能存在大量未被使用的media，如何清理

- features
  - 核心模块: content-mgr, content-type-builder, media-lib, roles-permissions
  - Self-hosted or Cloud
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

- roadmap
  - lts: editor, excel-table, local-db
  - ~~掌握strapi-够用~~ > 模仿directus-config/delta > undb-fe-be > 模仿directus-flow > collab

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
# draft
- ⌛️ version/history
  - 参考官方实现来做开源版本，参考 
    - `packages/core/content-manager/server/src/history` 源码
    - `packages/core/admin/admin/src/content-manager/history/pages/History.tsx` 源码

- media
  - files: docx/ppt
  - usage-references

- frontend-admin
  - 🤔 将 content-type-builder 隐藏后是否就是普通网站的界面了
  - 参考curator实现自定义admin

- backend
  - api-rate-limit

- 流式输出 stream response

- more toC features
# 🖇️ integrations
- 集成react-admin
- 如何集成页面编辑器，如craft，可参考内置编辑器
# dev
- 在admin添加新的content-type时，数据库会创建对应的表，同时后端src/api下面会自动生成对应的schema/router/controller/service，prod生产环境下不支持动态添加新的content-type

- 
- 
- 
- 

## done

- ~~draft/publish的实现似乎只在api层面，admin界面的显示状态有问题~~, v5已解决
# more
