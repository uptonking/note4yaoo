---
title: lib-fwk-nodejs-feathers-dev
tags: [backend, feathers, lib, nodejs]
created: 2023-01-12T16:33:14.483Z
modified: 2023-01-12T16:33:34.413Z
---

# lib-fwk-nodejs-feathers-dev

> a full-stack web-framework for creating APIs and real-time applications with TypeScript or JavaScript.

# guide
- pros
  - websocket优先, 支持多种provider如socketio/primus
  - 支持horizontal scaling
  - a unified approach for HTTP and real-time APIs
  - node-server支持切换express/koa

- cons
  - ?

- features
  - No decorators, no modules or DI for small or medium project
    - 函数式风格
  - Fast: Leveraging a unique architecture, Feathers lets you focus on building your APIs and real-time applications quickly. 
    - You automatically get scalable HTTP and real-time APIs
  - Universal: Feathers can be used with NodeJS, in the browser, with React Native or with any other API client. 
    - You can use any database with many supported out of the box
  - Flexible: a large ecosystem of plugins 
- [Feathers vs Nest | feathers](https://feathersjs.com/feathers-vs-nest.html)
  - Nest uses dependency injection system and a module based architecture, 
    - Feathers uses service based architecture with a more functional approach.
  - Feathers can generate client code for its server, Nest can't.
  - Nest uses RxJS for running interceptors, guards, filters or validation pipes. 
    - Feathers uses before, after and around hooks.
  - Nest can only be written in TypeScript whereas Feathers supports JavaScript and TypeScript.

- usecase
  - 实时协作的编辑器

- 后端常用场景
  - headless CMS, page builder, form builder, file manager, admin-area
  - admin/dashboard
  - forum/community
  - content内容或文档系统
  - lowcode integration
  - 流程自动化

- 技术选型
  - 后端框架很多(loopback/adonis)都实现了orm和mongoose的集成，此时可参考成熟模版的选择

- ecosystem
  - feathers-authentication-management
  - feathers-lowdb
# dev

# changelog

## [v5.0.0-pre33_202211](https://github.com/feathersjs/feathers/blob/dove/CHANGELOG.md#500-pre33-2022-11-08)

- [What's New in v5 | feathers](https://feathersjs.com/guides/whats-new.html)
  - We've completely rewritten all of Feathers in TypeScript
  - In 2016, we realized that we could decouple Feathers from the underlying HTTP transport, resulting in our first framework-agnostic, 支持express/koa
  - Radix Trie router: the algorithm behind Fastify's speed is now built into Feathers
  - new, official tools for data validation and mutation in the new core package, @feathersjs/schema

- [Migrating to v5 | feathers](https://feathersjs.com/guides/migrating.html)
- 👀 The new schemas and resolvers cover most use cases previously provided by higher level ORMs like Sequelize or Mongoose in a more flexible and Feathers friendly way.
  - low level MongoDB and Knex (SQL) database adapters have been moved into Feathers core for first-class SQL and MongoDB database support.

## v5.0.0-pre.0_202005

- 🚨 BREAKING
- configuration: Falls back to node-config instead of adding additional functionality like path replacements and automatic environment variable insertion.
- transport-commons: Removes the old message format and client service timeout

- core: Migrate @feathersjs/feathers to TypeScript
- core: use @feathers/hooks and add async type
