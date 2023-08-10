---
title: lib-fwk-orm-knex-examples
tags: [examples, knex, orm]
created: 2023-01-22T19:52:48.582Z
modified: 2023-01-22T19:52:59.120Z
---

# lib-fwk-orm-knex-examples

# guide
- orm技术选型
  - issues数量
    - typeorm 1800+
    - knex 700+
    - sequelize 700+

- 后端常用场景
  - headless CMS, page builder, form builder, file manager, admin-area
  - admin/dashboard
  - forum/community
  - content内容或文档系统
  - lowcode integration
  - 流程自动化

- tips
  - [Multitenancy using multiple databases using knex](https://vincit.github.io/objection.js/recipes/multitenancy-using-multiple-databases.html)

- ref
# popular
- https://github.com/shalior/express-ts-template /结构合理
  - Express.js template using TypeScript, Knex and Docker to head-start development.
  - fork of https://github.com/cdellacqua/express-knex-typescript-template

- https://github.com/kurierjs/kurier
  - A TypeScript framework to create APIs following the 1.1 Spec of JSONAPI + the Operations proposal spec.
  - Baked into Kurier, there is an operation processor which takes care of basic CRUD actions by using Knex.
  - JSONAPI is transport-layer independent, so it can be used for HTTP, WebSockets or any transport protocol of your choice.
  - The framework supports JSONAPI operations via WebSockets, and it includes middlewares for Koa, Express and Vercel to automatically add HTTP endpoints for each declared resource and processor.
  - The framework uses JSON Web Tokens as a way of verifying if a user is valid for a given operation.

- https://github.com/waitingsong/kmore
  - SQL query builder based on Knex with powerful TypeScript type support.
  - Intergrated Tracing of OpenTelemetry. Declarative Transaction via decorator @Transactional

- https://github.com/victor-vieira21/knex-mongoose-sequelize-lucid
  - 4个orm示例
# starter-boilerplate
- https://github.com/gabsrethink/nodejs-knex-authentication
  - Authentication API using NodeJS with TypeScript and Knex
  - 提供了jest测试

- https://github.com/ttuom1nen/knex-test
  - Express, Knex, Postgresql, Typescript
  - minimal test for Migrations/Seeds

- https://github.com/spinningideas/knex-poc /无jwt
  - this repo demonstrates use of knexjs as an ORM using two tables with geography data sets (continents and countries).
- https://github.com/apotox/knex-pg-express
  - unit tests + mocks
  - vitest setup inMemory pg database

- https://github.com/fransaycon/fastify-esbuild-postgres-boilerplate
  - fastify boilerplate with built in setup for esbuild, knex+postgres

- https://github.com/vipinkavlar/node-express-typescript-mysql-knex-swagger
  - Node-express-typescript with Mysql integrated with Knex querybuilder
  - 依赖awilix(IoC)
- https://github.com/mstickel/jokes-system
  - TypeDI, Actuator

- https://github.com/bilalsha/api-skelton
  - Skelton for creating api using express, typescript, eslint, prettier, jest, knex, objection, sqlite
- https://github.com/zayniddindev/nodejs-typescript
  - objection + knex
- objection
  - https://github.com/eliranlevi/node-ts-boilerplate
  - https://github.com/Nawaytes/koa-boilerplate

- https://github.com/ljlm0402/typescript-express-starter /202301/ts
  - Express RESTful API Boilerplate Using TypeScript，模版项目
  - 支持切换不同orm
  - 支持mongoose、orm、graphql

- https://github.com/agencyenterprise/aeboilerplate /202001/inactive
  - full-stack React/Node/Typescript web project starter that focuses primarily on ease-of-use and simplicity.

- https://github.com/eliranlevi/node-ts-boilerplate
  - Preconfigured boilerplate for building Node.js applications using Express & TypeScript, MySQL with Objection (ORM) and Knex. 
  - Start building REST APIs in seconds.
# apps
- https://github.com/Team-PlanOut/planout-backend
  - Planout Knex backend

- https://github.com/HannesOberreiter/btree_server
  - Backend API for b.tree Beekeeping Webapplication
  - Written in typescript build with nodejs, express, knex.js and objections.js.

- https://github.com/dgadelha/knex-playground
  - https://dgadelha.github.io/knex-playground/
# utils
- https://github.com/felixmosh/knex-mock-client
  - A mock client for Knex which allows you to write tests with DB interactions with a breeze.

- https://github.com/knex/knex-repositories
  - Parametrized CRUD repository abstraction for Knex.js

- https://github.com/acro5piano/knex-with-relations
  - A Knex plugin for batch loading table relations.

- https://github.com/alarner/perk
  - A well documented set of tools for building node web applications.
  - [Database](http://perkframework.com/v1/api/database.html)
  - Perk uses knex as a query builder. Knex allows you to easily write database queries that are compatible with multiple RDBMS

- https://github.com/wwwouter/typed-knex
  - A TypeScript wrapper for Knex.js
  - This module is deprecated. I recommend you to use one of these:
    - Knex.js with types.
    - TypeORM
# more
- https://github.com/nire0510/jsoq
  - Query and manipulate JSON arrays easily. 
  - Powered by lodash, inspired by knex and SQL in general.
