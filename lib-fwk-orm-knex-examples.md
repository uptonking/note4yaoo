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

- resources
  - [knex/ECOSYSTEM.md](https://github.com/knex/knex/blob/master/ECOSYSTEM.md)
# popular
- knex /18.5kStar/MIT/202401/js
  - https://github.com/knex/knex
  - http://knexjs.org/
  - A query builder for MSSQL, MySQL, PostgreSQL, SQLite3, Oracle
  - 依赖lodash、commander、tarn(db-pool)
  - feathers.v5抽象出schema+resolver，通过knex+mongoose支持rdbms和nosql
  - knex-based orm: mikro-orm, bookshelf, objection.js
  - https://github.com/tgriesser/knex-next /201810/ts
    - a future version of knex (TypeScript + internal rewrite), just putting it here for anyone interested
    - Better dialect feature separation

- bookshelf /6.3kStar/MIT/202007/js/inactive/同作者
  - https://github.com/bookshelf/bookshelf
  - Bookshelf is a JavaScript ORM for Node.js, built on the Knex SQL query builder. 
  - It features both Promise-based and traditional callback interfaces, 
  - It is designed to work with PostgreSQL, MySQL, and SQLite3.
  - Bookshelf aims to provide a simple library for common tasks when querying databases in JavaScript, and forming relations between these objects, taking a lot of ideas from the Data Mapper Pattern.
  - https://github.com/seegno/bookshelf-json-columns
    - Parse JSON columns with Bookshelf.js
  - https://github.com/tanem/express-bookshelf-realworld-example-app /202210/js/inactive
    - An Express and Bookshelf based backend implementation of the RealWorld API Spec.

- mikro-orm /5.5kStar/MIT/202301/ts/开发者主程只有1个
  - https://github.com/mikro-orm/mikro-orm
  - https://mikro-orm.io/
  - TypeScript ORM for Node.js based on Data Mapper, Unit of Work and Identity Map patterns.
  - 依赖esprima、dataloader、acorn-loose、fs-extra、reflect-metadata、knex
  - 使用示例是装饰器风格
  - Supports MongoDB, MySQL, MariaDB, PostgreSQL and SQLite databases.
  - Heavily inspired by Doctrine and Nextras Orm. (两者都为PHP设计)
  - Unit of Work maintains a list of objects (entities) affected by a business transaction and coordinates the writing out of changes. 
  - [Read Replica Connections | MikroORM](https://mikro-orm.io/docs/read-connections)
    - When resolving read connections, the default strategy is to assign random read replicas for all read operations (SELECT, COUNT) that are not running inside a transaction.
    - By default, select queries will use random read connection if not inside transaction. 

- https://github.com/adonisjs/lucid /MIT/202402/ts
  - https://lucid.adonisjs.com/
  - SQL ORM for AdonisJS built on top of Knex. 
  - Comes with a db query builder, Active record ORM, migrations, seeders and model factories.
  - A fluent query builder built on top of Knex.
  - Support for read-write replicas and multiple connection management.
  - Class-based models that adhere to the active record pattern.

- https://github.com/dgadelha/knex-playground /202310/ts
  - https://dgadelha.github.io/knex-playground/
  - 在类似vscode的浏览器界面中查看sql 
- https://github.com/michaelavila/knex-querylab /MIT/202104/ts/inactive
  - https://michaelavila.com/knex-querylab/
  - easily experiment with the knex.js syntax and see the generated SQL
- https://github.com/bostrom/knex-sandbox /EPLv1/201602/js
  - in browser sandbox for playing around with Knex.js
  - https://github.com/shuta13/knex-sandbox /202103/ts

- https://github.com/shalior/express-ts-template /结构合理
  - 🌰 Express.js template using TypeScript, Knex and Docker to head-start development.
  - fork of https://github.com/cdellacqua/express-knex-typescript-template /202311/ts
  - https://github.com/shalior/express-mongo-ts

- https://github.com/kurierjs/kurier /MIT/202312/ts
  - https://kurier.readthedocs.io/en/latest/
  - TypeScript framework to create JSON: API compliant APIs
  - A TypeScript framework to create APIs following the 1.1 Spec of JSONAPI + the Operations proposal spec.
  - Baked into Kurier, there is an operation processor which takes care of basic CRUD actions by using Knex.
  - JSONAPI is transport-layer independent, so it can be used for HTTP, WebSockets or any transport protocol of your choice.
  - The framework supports JSONAPI operations via WebSockets, and it includes middlewares for Koa, Express and Vercel to automatically add HTTP endpoints for each declared resource and processor.
  - The framework uses JSON Web Tokens as a way of verifying if a user is valid for a given operation.

- https://github.com/waitingsong/kmore /MIT/202402/ts
  - SQL query builder based on Knex with powerful TypeScript type support.
  - Declarative Transaction via decorator `@Transactional`.
  - Type-safe join table easily

- https://github.com/victor-vieira21/knex-mongoose-sequelize-lucid
  - 4个orm示例

- https://github.com/thetutlage/knex-dynamic-connection /MIT/202310/ts
  - This module is meant to patch knex and add support for defining dynamic connection configuration.
  - Adds support for dynamically returning connection config for knex queries. 
  - Helpful when you want to deal with write/read replicas
  - Knex.js doesn't have inbuilt support for read/write connections. One can create two seperate instances of knex for read and write, but that still doesn't completely solve the problem.
  - if you want to use multiple servers for read operations, you cannot do that, since knex.js allows only one connection server and will pool connections within that server.
  - With the help of this module, you can make knex create a connection using the dynamic config for every query.
  - [Ready for production use? _202209](https://github.com/thetutlage/knex-dynamic-connection/issues/17)
    - Used by AdonisJS and is actively maintained
  - https://www.npmjs.com/package/knex-pg-rr /201704/js
    - With Read-replica support for PG only
    - https://www.npmjs.com/package/knex-pg-read-replica /201611

- https://github.com/dolthub/dolt-knexjs-example /apache2/202309/js
  - https://github.com/dolthub/dolt-knexjs-example/tree/use-replica
  - [Getting Started with Dolt and Knex.js | DoltHub Blog _202309](https://www.dolthub.com/blog/2023-09-27-dolt-and-knexjs/)
  - Hosted Dolt now supports read replicas, a read-only server you can run queries against. Every write to the primary server is replicated to the read replicas. This allows you to scale your read traffic horizontally.
  - Some SQL query builders and ORMs (such as Sequelize) support specifying one or more read replicas and will automatically route read traffic to the replicas. 
  - Knex.js does not have this feature yet. To accomplish something similar, we create two Knex instances - one for the primary and one for the read replica - and explicitly send read queries to the read replica.

- https://github.com/a179346/knex-tree /MIT/202109/ts
  - Query hierarchical data structures in sql with knex

- https://github.com/devboell/family-tree /201709/js
  - An example app that lets you create a family tree, in this case a historical royal dynasty
  - The main theme of this app is recursion. The SQL model is hierarchical, and a CTE is used to query family tree data. 
  - The family tree graph is displayed by (vanilla) SVG elements wrapped in nested (recursive) React components.

- https://github.com/RisingStack/mysql-large-data-handling /MIT/201706/js
  - Handling large amount of data with MySQL and Node.js
  - 依赖knex.v0.13、mysql、moment
  - 🌰 [Node.js + MySQL Example: Handling 100's of GigaBytes of Data - RisingStack Engineering _202306](https://blog.risingstack.com/node-js-mysql-example-handling-hundred-gigabytes-of-data/)
    - take a look at how you can efficiently handle billions of rows that take up hundreds of gigabytes of storage space.
    - Creating tables for each user clearly adds complexity, but it may be a big win when it comes to removing users or similar entities with huge amount of associated data.
    - With MySQL, a partitioned table will work as if it was multiple tables, but you can use the same interface you got used to
    - In MySQL, you can partition by RANGE, LIST, COLUMN, HASH and KEY
    - When you use partitioning, MySQL will keep that data on separate parts of the disk as if they were separate tables and organizes your data automatically based on the partitioning key
# starter
- https://github.com/knex/knex-repositories /MIT/202303/ts
  - Parametrized CRUD repository abstraction for Knex.js

- https://github.com/gothinkster/koa-knex-realworld-example /201910/js
  - Example Node. Js (Koa.js + Knex) codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API.
- https://github.com/avanelli/fastify-realworld-example-app /202303/js
  - Fastify + Knex.js - Realworld Example App

- https://github.com/dhruvsaxena1998/node-typescript-starter /202110/ts
  - Node.js express template written with typescript.
  - https://github.com/yosua-kristianto/typescript-expressjs /202212/ts
  - https://github.com/alonavns/Yerevan /201907/ts
  - https://github.com/mxro/knex-typescript-starter-project /202002/ts
  - https://github.com/antonkalik/knex-postgres-boilerplate /202307/ts
  - https://github.com/eliranlevi/node-ts-boilerplate /201904/ts

- https://github.com/travishorn/koa-sqlite-jwt-server /201810/js
  - API server with JWT-authenticated routes. Uses Koa and Knex.

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

- https://github.com/kenyipp/realworld-nodejs-example-app /202304/ts
  - scalable RealWorld app implemented with TypeScript, Node.js, AWS Lambda, and tested with high-quality unit and integration tests
  - Express + Knex

- https://github.com/bilalsha/api-skelton
  - Skelton for creating api using express, typescript, eslint, prettier, jest, knex, objection, sqlite
- https://github.com/zayniddindev/nodejs-typescript
  - objection + knex
- objection
  - https://github.com/Nawaytes/koa-boilerplate

- https://github.com/ljlm0402/typescript-express-starter /202311/ts
  - Express RESTful API Boilerplate Using TypeScript，模版项目
  - 支持切换不同orm
  - 支持mongoose、orm、graphql、knex

- https://github.com/agencyenterprise/aeboilerplate /201907/ts/inactive
  - full-stack React/Node/Typescript web project starter that focuses primarily on ease-of-use and simplicity.
  - an opinionated boilerplate that includes independent client and API applications packaged into one repository.

- https://github.com/eliranlevi/node-ts-boilerplate
  - Preconfigured boilerplate for building Node.js applications using Express & TypeScript, MySQL with Objection (ORM) and Knex. 
  - Start building REST APIs in seconds.

- https://github.com/ErikBahena/Express-Knex-Postgres-JWT-Auth-Template /202203/js
  - boilerplate code for when you're starting a new postgres backend project

- https://github.com/santoshshinde2012/node-ts-knex-boilerplate /202402/tsconfig
  - Node-Typescript-Knex-Boilerplate

- https://github.com/cham11ng/typescript-api-starter /MIT/202210/ts
  - Starter for Node.js Express API in Typescript with jsonwebtoken, joi, Knex, Objection.js and many other popular tools.
  - 依赖objection3、knex2、pg、express
# examples
- https://github.com/franzon/postgres-rls-example /202006/js
  - This application is an example of how RLS can be used in an express app, using a middleware for getting the correct connection for each tenant.
  - A good way to make this checking less error-prone, e.g., forgetting a `where tenant_id = ?` clause, is by centralizing the isolation policies at the database level, removing the responsibility from the developers. 
  - One way to achieve this on Postgres is to use a feature called Row Level Security, which allows to making restrictions on which rows are returned when selecting or affected when inserting, updating, and deleting.

- https://github.com/bravi-software/knextancy /MIT/201710/js
  - Small library that provides a way of implementing multi-tenancy using table prefixes.
  - Its tenant method expects a knex instance and a tenantId and returns Promise for a special tenantKnex instance that scopes every queries to the particular tenant.
  - https://github.com/bravi-software/knextancy-example /201608/js
    - a simple example of how to build a multi tenant REST API. 
    - Using knextancy with express and PostgreSQL database.

- https://github.com/Team-PlanOut/planout-backend
  - Planout Knex backend

- https://github.com/HannesOberreiter/btree_server /AGPLv3/202402/ts
  - API Server for b.tree Beekeeping Application. Node.js and Objections.js
  - Written in typescript build with nodejs, express, knex.js and objections.js.
  - https://github.com/HannesOberreiter/btree_database
    - The maria folder will be our local volume for the database
    - The redis folder will be our local volume for the redis database dumps

- https://github.com/ganeshmani/node_bookmark_manager_app /202002/js
  - BookMark Manager Built using Nodejs, Express, Knex and MySQL

- https://github.com/osvaldokalvaitir/nodejs-proffy /202008/ts
  - Proffy Application using Node.js, Express, knex.js, TypeScript, CORS, SQLite and Insomnia

- https://github.com/bot-ts/framework /202310/ts
  - a framework for discord.js designed in TypeScript 
  - discord.js is a powerful Node.js  module that allows you to interact with the Discord API  very easily. It takes a much more object-oriented approach
# utils
- https://github.com/felixmosh/knex-mock-client /MIT/202310/ts
  - A mock client for knex which allows you to write unit tests with DB interactions
  - Each db request that your app makes throughout knex will be registered in a scoped (by query method) history call list. 
- https://github.com/jbrumwell/mock-knex /MIT/202312/js
  - A mock knex adapter for simulating a database during testing, especially useful when used in combination with fixture-factory.

- https://github.com/felixmosh/knex-paginate /MIT/202303/js
  - Extension of Knex's query builder with `paginate` method that will help with your pagination tasks.
  - https://github.com/cannblw/knex-paginator /201912/js

- https://github.com/jpalumickas/knex-cursor-pagination /MIT/202206/ts
  - Add stable cursor pagination to Knex query builder. 
  - This package also supports relay connection result.

- https://github.com/johnazre/knex-populate /202308/js
  - allows you to populate foreign key fields in the JSON response
  - Mimics the structure of responses from Mongoose/MongoDB and SailsJS/Waterline.

- https://github.com/harish2704/knex-json-query /202107/js
  - A high-level utility which will will generate Knex query from a single JSON object.

- https://github.com/ricardocrescenti/knex-json-where /202004/ts
  - Add filters on Knex query through a JSON object.

- https://github.com/ozum/knex-migrate-sql-file /MIT/202303/ts
  - Use sql files instead of (or in addition to) `knex.schema` methods.
  - Exports getMigrators, upSQL and downSQL functions which executes knex.raw() method on SQL files having same file name appended .up.sql and .down.sql.

- https://github.com/maxcnunes/mongo-to-knex /201702/js
  - Applies mongo standard query to knex query builder.

- https://github.com/FleekHQ/knex-flex-filter /201907/js
  - a no-dependency package that adds dynamic filter functionality to Knex.

- https://github.com/kibertoad/knex-tablecleaner /202109/js
  - Simple library for deleting all rows from a given list of DB tables. 
  - Tables are cleaned sequentially in a given order, to avoid foreign key constraint violations.

- https://github.com/acro5piano/knex-with-relations /MIT/202310/ts
  - A Knex plugin for batch loading table relations.
  - Provides convenient method to fetch both n-1 relation and 1-1 relation

- https://github.com/danielgindi/knex-schema-builder /MIT/202009/js
  - A schema builder module for knex.js, handles schema initialization and migration
  - I built this little helper so I can have a way of easily describing a database schema and automate the process of database initialization for an installation of a project - or migration of the database to newer versions.

- https://github.com/TRUEPIC/queryql /MIT/202401/js
  - QueryQL makes it easy to add filtering, sorting, and pagination to your Node.js REST API through your old friend: the query string
  - QueryQL makes it easy to add filtering, sorting, and pagination to your Node.js REST API through your old friend: the query string

- https://github.com/alarner/perk /202301/ts/inactive
  - A well documented set of tools for building node web applications.
  - [Database](http://perkframework.com/v1/api/database.html)
  - Perk uses knex as a query builder. Knex allows you to easily write database queries that are compatible with multiple RDBMS

- https://github.com/gravity-ui/postgreskit /MIT/202401/ts
  - a package for connecting to PostgreSQL. 
  - It includes the pg, Knex, and Objection libraries, as well as a multi-host connection module.
  - Under the hood, this module creates N instances of knex (N is the number of hosts passed in connectionString). 
    - From these instances, it polls the database hosts every healthcheckInterval milliseconds, requesting if they are primary hosts or replica hosts
  - Both `db.primary` and `db.replica` point to regular knex instances that can do everything described in the knex documentation.

- https://github.com/haltcase/trilogy /MIT/202205/ts/inactive
  - https://trilogy.js.org/
  - a simple Promise-based wrapper for SQLite databases. 
  - It supports both the native C++ sqlite3 driver and the pure JavaScript sql.js backend
  - It's not an ORM and isn't intended to be one — it doesn't have any relationship features.
  - Instead it focuses on providing a simple, clear API that's influenced more by Mongoose than by SQL.
  - trilogy uses knex internally to build its queries, but it's also exposed so you can use it to build your own. 
  - supports multiple swappable backends ( plus in-memory storage )
    - Both the native sqlite3 module and sql.js (pure JavaScript!) are supported. There is also memory-only storage for fast, unpersisted data handling

- https://github.com/d-band/sk2 /202011/js
  - sk2 is used for extend sequelize with knex

- https://github.com/alekbarszczewski/knex-hooks /202005/js
  - Allows to easily add before/after insert/update/delete/select hooks to knex.

- https://github.com/felixmosh/knex-on-duplicate-update /202204/js
  - Simple patcher for Knex. It adds the .onDuplicateUpdate() function to knex's query builder in order to add support MySQL's on duplicate key update columnName=Values(columnName).
  - Knex (v0.21.10) added an official upsert functionality with similar capabilities which supports MySQL, Postgress & SQLite.

- https://github.com/libsql/knex-libsql /202306/js
  - A Knex dialect for libSQL/sqld, using the @libsql/sqlite3 package that emulates sqlite3.

- https://github.com/travishorn/authjs-knexjs-adapter /202401/ts
  - An adapter for Auth.js/NextAuth.js to allow you to connect to any database service via Knex.js.

- https://github.com/smooth-code/knex-scripts /202211/js
  - Knex utilities to interact with Postgres database.

- https://github.com/StreetStrider/knexed /202007/js
  - Adds some neatness to Knex library. 
  - Utilities for tables, joins, transactions and other.

- https://github.com/knex/knex-utils /202303/ts
  - Useful utilities for Knex.js
# devops
- https://github.com/jfollmann/knex-migrations-ts /202108/ts
  - Sample to use knex migrations with PostgreSQL and Typescript support.

- https://github.com/TryGhost/knex-migrator /MIT/202312/js
  - A database migration tool for knex.js, which supports MySQL and SQlite3.
  - Replicas are unsupported, because Knex.js doesn't support them.
  - Sqlite does not support read locks by default.

- https://github.com/why2pac/knex-automigrate /MIT/202206/js
  - Table schema based database migration tool, built on top of the knex.js
  - Migration schema file name must be started with table_.

- https://github.com/sheerun/knex-migrate /MIT/201909/js
  - Modern database migration toolkit for knex.js
  - 100% compatible with knex.js migrations cli

- https://github.com/niradler/rve-knex-migration /201711/js
  - reverse engineer db to knex migration file

- https://github.com/flodlc/pg-mate /202303/ts
  - a migration management tool for PostgreSQL 
  - Customizable client injection for migrations (native pg driver, zapatos, or any other client you want)
  - First-class CLI and programmatic usage

- https://github.com/marcbachmann/knex-umzug /202304/js
  - A storage adapter for umzug, a database migration library.
  - It supports namespacing and custom database table names. 
  - This storage adapter not only shows you the current state of a migration but also shows all the migration paths and tracks hostname and system user which executed a migration.
  - This library only makes knex work with umzug. Please check out the umzug api for more details

- https://github.com/Vincit/knex-db-manager /ISC/202008/js
  - Utility for create, drop, truncate etc. administrative database operations.
  - Library uses knex connection for non administrative queries, but also creates priviliged connection directly with driver with superuser privileges for creating and dropping databases / roles.
# more
- https://github.com/nire0510/jsoq /GPLv3/202310/ts
  - Query and manipulate JSON arrays easily. 
  - Powered by lodash, inspired by knex and SQL in general.

- https://github.com/mrdulin/nodejs-pg-knex-samples /MIT/202001/ts
  - Learning PostgreSQL, knex.js by examples.
