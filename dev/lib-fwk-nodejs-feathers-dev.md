---
title: lib-fwk-nodejs-feathers-dev
tags: [feathers, lib, nodejs]
created: 2023-01-12T16:33:14.483Z
modified: 2023-01-12T16:33:34.413Z
---

# lib-fwk-nodejs-feathers-dev

# guide

# dev

# changelog

## v5.0.0-_202211

- [What's New in v5 | feathers](https://feathersjs.com/guides/whats-new.html)
  - We've completely rewritten all of Feathers in TypeScript
  - In 2016, we realized that we could decouple Feathers from the underlying HTTP transport, resulting in our first framework-agnostic, 支持express/koa
  - Radix Trie router: the algorithm behind Fastify's speed is now built into Feathers
  - new, official tools for data validation and mutation in the new core package, @feathersjs/schema

- [Migrating to v5 | feathers](https://feathersjs.com/guides/migrating.html)
- 👀 The new schemas and resolvers cover most use cases previously provided by higher level ORMs like Sequelize or Mongoose in a more flexible and Feathers friendly way.
  - low level MongoDB and Knex (SQL) database adapters have been moved into Feathers core for first-class SQL and MongoDB database support.
