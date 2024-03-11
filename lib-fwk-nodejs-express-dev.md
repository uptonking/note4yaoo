---
title: lib-fwk-nodejs-express-dev
tags: [express, nodejs]
created: 2023-02-05T18:55:13.937Z
modified: 2023-02-05T18:55:27.887Z
---

# lib-fwk-nodejs-express-dev

# guide

- pros
  - almost feature-complete

- cons
  - 功能特性的集成缺少类似nestjs的最佳实践，特别是缓存、消息队列，导致代码易混乱
  - 对最新标准的支持不好，如http2/tls
  - No support of async error handling, async middlewares.

- who is using #express
  - fwk: strapi, eggjs
  - app: outline
# dev

# orm-同时支持rdbms和nosql的方案(sqlite+mongodb)

- 考虑因素
  - 数据库特性及插件的支持
  - 空值处理

## [Payload CMS - Database](https://payloadcms.com/docs/database/overview)

- Payload interacts with your database via the database adapter that you choose. 
  - Right now, Payload officially supports two database adapters:
  - MongoDB w/ `Mongoose`; Postgres w/ `Drizzle`; 
  - We will be adding support for SQLite and MySQL in the near future using Drizzle ORM.

- You should prefer MongoDB if:
  - You don't want to deal with keeping production/staging databases in sync via DDL changes
  - You leverage a lot of array fields, block fields, or hasMany select fields and similar
  - Most (or everything) in your project is localized

- You should prefer a relational DB like Postgres if:
  - You are comfortable with migration workflows
  - You require enforced data consistency at the database level
  - You have a lot of relationships between collections and require relationships to be enforced

- It's important to note that almost everything Payload does is available in all of our officially supported database adapters, including localization, arrays, blocks, etc.
  - The only thing that is not supported in Postgres yet is the `Point` field, but that should be added soon.

## [feathers Services](https://feathersjs.com/guides/basics/services.html)

- In Feathers, a service is an object or instance of a class that implements certain methods. 
  - Services provide a way for Feathers to interact with different kinds of data sources in a uniform, protocol-independent way.
- Writing all that code yourself for every service is pretty repetitive and cumbersome, which is why Feathers has a collection of pre-built services for different databases.
  - Feathers database adapters support a common usage API, pagination and querying syntax for many popular databases
- The following database adapters are maintained as part of Feathers core:
  - sql(sqlite, pg, mysql, mssql), 基于`knex`实现
  - mongodb，基于mongo-driver实现，不依赖mongoose
  - memory

- [FAQ | feathers](https://feathersjs.com/help/faq.html)
  - When making a request using REST (HTTP) query string values don't have any type information and will always be strings. 
  - Some database adapters that have a schema (like `feathers-mongoose` or `feathers-sequelize`) will try to convert values to the correct type but others (like `feathers-mongodb`) can't. 
  - Additionally,  `null` will always be a string and always has to be converted if you want to query for `null`. This can be done in a `before` hook

- [Migrating to v5 | feathers](https://feathersjs.com/guides/migrating.html)
  - The new schemas and resolvers cover most use cases previously provided by higher level ORMs like Sequelize or Mongoose in a more flexible and Feathers friendly way. 
  - This allows for a better database integration into Feathers without the overhead of a full ORM which is why the more low level `MongoDB` and `Knex` (SQL) database adapters have been moved into Feathers core for first-class SQL and MongoDB database support.

## [MikroORM - Usage with MongoDB](https://mikro-orm.io/docs/usage-with-mongo)

- rdbms基于`knex`实现
- nosql基于mongo-driver实现，不依赖mongoose
- To access driver specific methods like `em.aggregate()` we need to specify the driver type when calling `MikroORM.init<D>()`. 
- 使用示例是装饰器风格, typeorm也是装饰器风格

- Starting with v3.4, MongoDB driver supports transactions.
  - implicit transactions are disabled by default
  - you need to explicitly create all collections before working with them

- If you want to use database that is not currently supported, you can implement your own driver. 

- SQLite extensions like sqlean can add many useful features that are notably missing by default (e.g. regexp).
# more
- [重读Express框架 - 掘金](https://juejin.cn/post/7100571058234720287)
