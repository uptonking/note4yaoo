---
title: lib-fwk-orm-knex-examples
tags: [examples, knex, orm]
created: 2023-01-22T19:52:48.582Z
modified: 2023-01-22T19:52:59.120Z
---

# lib-fwk-orm-knex-examples

# guide

- 后端常用场景
  - cms, page/form builder, file manager
  - admin/dashboard
  - wiki/knowledge-base
  - forum/community
  - workflow automation
  - lowcode integrations

- tips
  - 很少存在替换orm的场景，通常orm都会支持主流rdbms
  - 同时支持knex和mongoose需要架构层的抽象
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

- https://github.com/kysely-org/kysely /MIT/202403/ts
  - https://kysely.dev/
  - a type-safe and autocompletion-friendly typescript SQL query builder. 
  - Inspired by knex. 

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

- https://github.com/louislam/redbean-node /MIT/202311/ts
  - http://redbean-node.whatsticker.online/
  - an easy to use ORM tool for Node.js, strongly inspired by RedBeanPHP.
  - Ported RedBeanPHP's main features and api design
  - Automatically creates tables and columns
  - Build on top of knex.js
  - async/await or promise friendly

- https://github.com/sutandojs/sutando /MIT/202402/js
  - https://sutando.org/
  - a modern Node.js ORM, like Laravel Eloquent

- https://github.com/dgadelha/knex-playground /202310/ts
  - https://dgadelha.github.io/knex-playground/
  - 在类似vscode的浏览器界面中查看sql 
- https://github.com/michaelavila/knex-querylab /MIT/202104/ts/inactive
  - https://michaelavila.com/knex-querylab/
  - easily experiment with the knex.js syntax and see the generated SQL
- https://github.com/bostrom/knex-sandbox /EPLv1/201602/js
  - in browser sandbox for playing around with Knex.js
  - https://github.com/shuta13/knex-sandbox /202103/ts

- https://github.com/r48n34/db-erd-gen /MIT/202401/ts/自动生成sql-ddl
  - https://db-erd-gen.vercel.app/
  - Free DrawSQL like website
  - 依赖@devbookhq/splitter、mantine5、reactflow、zustand、zod
  - Save SQL in various DB format
  - support output: Postgres MySQL SQLite knex.js kysely ts types

- https://github.com/kurierjs/kurier /MIT/202312/ts
  - https://kurier.readthedocs.io/en/latest/
  - TypeScript framework to create JSON: API compliant APIs
  - A TypeScript framework to create APIs following the 1.1 Spec of JSONAPI + the Operations proposal spec.
  - there is an operation processor which takes care of basic CRUD actions by using Knex.
  - ✨ JSONAPI is transport-layer independent, so it can be used for HTTP, WebSockets or any transport protocol of your choice.
  - The framework supports JSONAPI operations via WebSockets, and it includes middlewares for Koa, Express and Vercel to automatically add HTTP endpoints for each declared resource and processor.
  - The framework uses JSON Web Tokens as a way of verifying if a user is valid for a given operation.
  - https://github.com/carlbennettnz/json-api-knex-adapter /202006/ts
    - Serve resources from your SQL database using json-api@3

- https://github.com/thetutlage/knex-dynamic-connection /MIT/202310/ts
  - This module is meant to patch knex and add support for defining dynamic connection configuration.
  - Adds support for dynamically returning connection config for knex queries. 
  - ✨ Helpful when you want to deal with write/read replicas
  - Knex.js doesn't have inbuilt support for read/write connections. One can create two separate instances of knex for read and write, but that still doesn't completely solve the problem.
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
  - This app uses: React Redux Apollo GraphQL graphql-server ReactRouter ReduxForm SVG Knex/SQL CTE (Common Table Expression)

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
- https://github.com/gothinkster/koa-knex-realworld-example /201910/js/archived
  - Example (Koa.js + Knex) containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the RealWorld spec and API
  - 在controller中直接用knex构建并执行sql
  - 提供了建表的knex脚本
  - 🍴 forks
  - https://github.com/EJIqpEP/koa-knex-realworld-example /202205/js
    - Updated sqlite3, Fixed bcrypt
  - https://github.com/mlaccetti/koa-knex-realworld-heroku-example /201905/js
    - Add in the in-memory caching, require('memory-cache')

- https://github.com/kenyipp/realworld-nodejs-example-app /202304/ts/inactive
  - scalable RealWorld app implemented with TypeScript, Node.js, AWS Lambda, and tested with high-quality unit and integration tests
  - Express + Knex
  - Refactor project to implement a microservice architecture using TypeScript
  - Implement GraphQL endpoint for retrieving articles
  - https://github.com/kenyipp/realworld-nodejs-example-app/tree/eef7b22eff24e3249dba5f7eedebea3d865de967 /202207/js
    - 早期版本基于express、knex2实现
    - 采用controller/model两层架构, model实际上是dao因为封装了knex方法
    - 提供了建表的sql

- https://github.com/LimarenkoDenis/typescript-node-koa-realworld-example-app /201710/ts
  - fullstack application built with Koa.js + Knex including CRUD operations, authentication, routing, pagination, and more.
  - https://github.com/LimarenkoDenis/angular-ngxs-nx-realworld-example-app

- https://github.com/avanelli/fastify-realworld-example-app /202303/js
  - Fastify + Knex.js - Realworld Example App
  - [提供了建表的knex脚本](https://github.com/avanelli/fastify-realworld-example-app/blob/main/knex/migrations/20220919145459_create.js)
  - https://github.com/Z-Ferguson/Fastify-Knex-PostgreSQL-Conduit /202305/js/未完成/只做了user和article

- https://github.com/PedroPadilhaPortella/Medium_Clone_NgRx /202208/be-js/fe-ts/inactive
  - Medium_Clone_NgRx, koa2 + knex.v0.21

- https://github.com/victor-vieira21/knex-mongoose-sequelize-lucid
  - 4个orm示例，弱架构，仅参考

- https://github.com/ljlm0402/typescript-express-starter /202311/ts/typedi
  - Express RESTful API Boilerplate Using TypeScript, 可选的多模版项目
  - ✨ 支持Mongoose/Sequelize/TypeORM/Prisma/Knex/MikroORM/GraphQL
  - 采用controller/service/model三层架构，class风格，依赖注入，少量使用装饰器
  - 使用objection

- https://github.com/dyshaev-working/nodejs-express-typescript-knex-psql-crud-example /202012/ts
  - Example CRUD application Express/Knex/PostgreSql
  - 采用controller/service/dao三层架构，函数式风格
  - 实现简单，仅1个route，无jwt

- https://github.com/icapps/nodejs-silverback /ISC/201902/ts
  - NodeJS boilerplate project
  - 采用controller/service/repository/model四层架构，函数式风格，经典架构
  - repository层使用knex，model层仅定义schema类型及crud方法参数类型
  - 依赖express、redis、tree-house-authentication
  - 功能丰富，包括auth/mail; 团队转向nestjs
  - redis用于测试和auth-session
  - router使用handleAsyncFn
  - https://github.com/icapps/react-silverback /201807/js
    - 依赖react-redux、bootstrap4
  - https://github.com/icapps/tree-house /202107/ts
    - NodeJS utilities and handy helpers extending ExpressJS functionalities
    - setBasicSecurity,setBodyParser,getRateLimiter
  - https://github.com/icapps/tree-house-authentication /202301/ts
    - authentication utilities and JWT methods; Two-factor auth
  - https://github.com/icapps/tree-house-storage /202207/ts
    - multipartUpload, Local filesystem, S3
  - https://github.com/icapps/nodejs_boilerplate /202111/ts/单文件
  - https://github.com/icapps/nodejs-express-template /201711/ts
    - 依赖sequelize4
    - 采用controller/service/model三层架构, class风格

- https://github.com/Zarkus13/pizza-pasta-api /202211/ts/inactive
  - Pizza & Pasta API using Node.js, Express, TypeScript, Knex, Zod
  - 采用controller/service/dao/model四层架构，函数式风格+class，按业务modules划分架构
  - 依赖express、jsonwebtoken、multer、zod

- https://github.com/dhruvsaxena1998/node-typescript-starter /202110/ts/inactive
  - Node.js express template written with typescript.
  - ✨ 采用controller/service/repository三层架构，class风格，经典架构
  - 依赖express、jsonwebtoken、swagger-ui-express

- https://github.com/VladShevchenko9/ts-api /MIT/202403/ts
  - Simple ts-node api endpoints
  - 依赖express、knex、jsonwebtoken、mysql
  - 采用controller/service/repository三层架构, class风格
  - AbstractModelService抽象出了通用crud工具方法

- https://github.com/santoshshinde2012/node-ts-knex-boilerplate /202402/ts
  - Node-Typescript-Knex-Boilerplate
  - 采用controller/service/entity三层架构，class风格, 可按业务modules划分架构
  - service层操作db，entity层定义schema和配置
  - 未实现jwt

- https://github.com/disney-parent-pass/back-end /202212/ts/inactive
  - Gain more experience building out an API server with user authentication
  - 依赖jsonwebtoken、knex、sqlite3
  - 采用controller/service/entity三层架构，class风格, 可按业务modules划分架构

- https://github.com/cdellacqua/express-knex-typescript-template /202311/ts/ssr-pug
  - Express.js template using TypeScript, Knex and Docker to head-start development.
  - 采用route/service两层架构
  - ✨ service层部分crud方法通过公共工具方法实现，如findOneGenerator/createMultiGenerator
  - view层pug，功能丰富, 代码精简
  - 依赖knex-transact、bcryptjs、jsonwebtoken、pg-query-stream、pug、winston、express-validator
  - router使用asyncWrapper
  - 🍴 fork https://github.com/shalior/express-ts-template
  - https://github.com/shalior/express-mongo-ts /202301/ts/inactive

- https://github.com/agencyenterprise/aeboilerplate /202001/ts/inactive
  - a full-stack React/Node Typescript project
  - 采用controller/service两层架构，函数式风格
  - router使用了asyncHandler
  - 依赖passport、knex，未使用jwt
  - an opinionated boilerplate that includes independent client and API
  - The client application is generated using `create-react-app`.
  - https://github.com/agencyenterprise/ae-bootstrap
  - https://github.com/agencyenterprise/hack-2023-ae-faucet

- https://github.com/jasogwa/typescript-api /202209/ts
  - CRUD API Using NODE JS, Typescript, Knex, and SQL
  - 采用controller/service两层架构
  - 数据库采用连接池pool

- https://github.com/whyboris/express-knex-api /202001/js/inactive/单文件示例
  - A RESTful API that interacts with business data

- https://github.com/antonkalik/knex-postgres-boilerplate /202307/ts/弱架构
  - knex-postgres-boilerplate
  - https://github.com/MatthewAraujo/api-rest /202307/ts/弱架构
  - https://github.com/mxro/knex-typescript-starter-project /202002/ts/弱架构

- https://github.com/apotox/knex-pg-express /202212/ts/弱架构
  - unit tests + mocks
  - vitest setup inMemory pg database

- https://github.com/jvcjunior/node_express_functional /202012/ts
  - Node/Express API using some functional approach
  - 采用controller/service/repository/model四层架构，函数式风格
  - 依赖express、jsonwebtoken、knex、objection、sqlite3

- https://github.com/yosua-kristianto/typescript-expressjs /202212/ts
  - I made a boilerplate; java风格; knex几乎没用，主要用sequelize
  - 采用controller/repository/model三层架构，class风格

- https://github.com/kasvith/typescript-express-jwt-knex-boilerplate /MIT/202107/ts
  - Typescript Express JWT Knex Boilerplate
  - 实现了自定义decorator，如@ApiVersion('1.0')
  - 实现了自定义依赖注入

- https://github.com/gabsrethink/nodejs-knex-authentication /202210/ts/inactive
  - Authentication API using NodeJS with TypeScript and Knex
  - 提供了jest测试

- https://github.com/travishorn/koa-sqlite-jwt-server /201810/js/弱架构
  - API server with JWT-authenticated routes. Uses Koa and Knex.

- https://github.com/orphandeity/express-authorization-server /202312/js
  - offers secure user authentication for web applications. 
  - Built on Express, it includes JWT session management, Redis for token storage, and SQLite for user data. 

- https://github.com/ErikBahena/Express-Knex-Postgres-JWT-Auth-Template /202203/js
  - boilerplate code for when you're starting a new postgres backend project

- https://github.com/luk3skyw4lker/refresh-token-strategy-nodejs /202103/ts
  - The implementation of the refresh token strategy in Node.js with Typescript, Knex, Express and JWT.

- https://github.com/the-complete-todo-application/back-end /201911/ts
  - The back-end application. Node, Express, Knex, SQLite, PostgreSQL.
  - https://github.com/the-complete-todo-application/front-end
    - Front-end application. React, Redux, TypeScript, Material-UI.

- https://github.com/vitorlinsbinski/api-rest-nodejs /202402/ts
  - RESTful API developed in NodeJS with Fastify

- https://github.com/fransaycon/fastify-esbuild-postgres-boilerplate /202302/ts
  - fastify boilerplate with built in setup for esbuild, knex+postgres

- https://github.com/DanielAraldi/Proffy /MIT/202402/ts
  - Proffy is an online study platform
  - Proffy is an application that connects students with teachers.
  - 采用controller/repository/model三层架构，class风格

- https://github.com/RafaelGoulartB/proffy /MIT/202202/ts
  - Project made to connect teachers to students, made in Next Level Week #2
  - 依赖express、knex、sqlite3、react

- https://github.com/osvaldokalvaitir/nodejs-proffy /202008/ts/弱架构
  - Proffy Application using Node.js, Express, knex.js, TypeScript, CORS, SQLite and Insomnia
  - Project built during Rocketseat's Next Level Week #2
  - https://github.com/higorsnt/proffy /202008

- https://github.com/tdubs42/tdubs-fullstack-framework /202108/js
  - Uses express, CORS, helmet, and knex for the backend. 
  - Uses react and axios for the frontend.
- https://github.com/rednil/express-passport-knex-lit /202301/js
  - A fullstack starter for little projects requiring authentication and user management.
  - Based on express, passport, knex and lit, automatically packed into a docker container using a github action.
- https://github.com/alexeagleson/nextjs-fullstack-app-template /202301/ts
  - A fullstack template for a NextJs App
  - This tutorial is available as a video on youtube

- https://github.com/cham11ng/typescript-api-starter /MIT/202210/ts/inactive
  - Starter for Node.js Express API in Typescript with jsonwebtoken, joi, Knex, Objection.js and many other popular tools.
  - 依赖objection3、knex2、pg、express
  - https://github.com/Nawaytes/koa-boilerplate /202306/ts/多占位符文件
    - Objection + Koa
  - https://github.com/resitdc/express-knex-pg-boilerplate /202305/ts
    - 采用controller/model两层架构，class Users extends objection.Model
- https://github.com/bilalsha/api-skelton /202301/ts
  - Skelton for creating api using express, typescript, eslint, prettier, jest, knex, objection, sqlite

- https://github.com/restuwahyu13/express-book-store /202111/ts/inactive
  - Example book store api using Express + Typescript and Knex ORM + Objection

- https://github.com/nickygb/clean-api /202204/ts
  - Clean API using Typescript + Express + Tsoa + Inversify + Knex
  - https://github.com/oMatheusmol/api-knex-clean-architecture /202112/ts
  - https://github.com/MatheusWill/CRUD-Clean-Architecture /202112/ts
  - https://github.com/matheussantiago12/typescript-clean-api /202104/ts

- https://github.com/bkonkle/node-knex-typescript-example /201901/ts
  - An example API application using Node, Knex, and TypeScript
  - 提供了PostgresProvider、RedisProvider

- https://github.com/githiago-f/customers-api /202105/ts
  - Monorepo using express on the back-end and react on front-end
  - 采用controller/repository两层架构，函数式风格

- https://github.com/benjamin-chavez/node-pg-knex-passport-template /202309/ts/inactive
  - Backend Express API Template using Knex, PostgreSQL, Passport, and Typescript.
  - 依赖passport-local，不依赖jwt

- https://github.com/otedesco/apart-services /202307/ts/inactive
  - Microservices architecture backend, built with Node.js and Typescript using Turborepo.

- https://github.com/benjamin-chavez/express-api-auth0 /MIT/202309/ts/inactive
  - Backend Express API Template using Knex, PostgreSQL, Passport, and Typescript.

- https://github.com/sombriks/simple-knex-koa-example /MIT/202312/js/inactive
  - http://example.sombriks.org/books
  - sample application touring API, tests, continuous integration, continuous deployments, image publishing and so on
  - Kubernetes is how people put things in production nowadays and sometimes it can be tricky to test because it's heavy. By using kind as kubernetes runtime, part of this issue is solved and the developer can be more confident on how the application will behave inside the belly of the beast.
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

- https://github.com/ganeshmani/node_bookmark_manager_app /202002/js
  - BookMark Manager Built using Nodejs, Express, Knex and MySQL

- https://github.com/onosendi/product-feedback /202202/ts/样式友好/inactive
  - https://product-feedback.dlindegren.com/
  - Product feedback hobby project
  - Community product feedback that moves through a life cycle: suggestion -> planned -> in-progress -> live.
  - 依赖Redux-Toolkit, Fastify, pg, knex, react-final-form

- https://github.com/sumanthyedoti/indirect /202209/ts/inactive
  - Communication platform for organisations and communities
  - 依赖express-session、ajv、knex、passport、socket.io、@headlessui/react、react-query、slate-react、zustand

- https://github.com/hieunc229/tracie /202102/ts
  - A minimal, self-hosted event tracking service with SQLite (Knex) and NodeJS
  - This is a client library, used to create events and send them to your hosted server.
  - https://github.com/hieunc229/tracie-server

- https://github.com/Himmeltala/chatroom-serve /202304/ts/inactive
  - 【练习项目】基于 Node.js + Socket.io + knex + mysql2 实现的聊天室服务器

- https://github.com/HannesOberreiter/btree_server /AGPLv3/202402/ts
  - API Server for b.tree Beekeeping Application. Node.js and Objections.js
  - Written in typescript build with nodejs, express, knex.js and objections.js.
  - https://github.com/HannesOberreiter/btree_database
    - The maria folder will be our local volume for the database
    - The redis folder will be our local volume for the redis database dumps

- https://github.com/bot-ts/framework /202310/ts
  - a framework for discord.js designed in TypeScript 
  - discord.js is a powerful Node.js  module that allows you to interact with the Discord API  very easily. It takes a much more object-oriented approach

- https://github.com/YappyBots/YappyGitHub /202403/js
  - A github monitor bot for Discord
  - Monitor your github repos by adding this bot to your server, set up a channel for it, and don't miss any events!

- https://github.com/jplsilva/Palebot /202107/ts
  - A Discord bot made with Discordjs, Typescript, Node.js and Knex

- https://github.com/gabrielmaialva33/wpp-ai /MIT/202311/ts
  - chatbot for WhatsApp using Node.js, Typescript and following general best practices.

- https://github.com/anthonymunene/reservation-apps /202312/ts
  - A reservation airbnb clone API built with feathersjs knex ORM and PostgreSQL

- https://github.com/vymalo/api-watcher-backend /202304/ts
  - https://blog.ssegning.com/
  - https://github.com/vymalo/api-watcher-ui
    - UI App for the SMS API Watcher, a Stub server for APIs

- https://github.com/mux-mux/findface /202402/js
  - https://jsgo.pro/findface/
  - Find the face in the image
  - ClarifAI Face Area Detect, PostresSQL, Bcrypt
  - https://github.com/SKorchinskiy/Face-Detector /202401/ts
- https://github.com/KenTandrian/smart-face-detector-api /202402/js
  - A backend server for Smart Face Detector project using Node JS, Express JS, and PostgreSQL. 
  - a capstone project for Zero to Mastery Academy: Web Developer 2022

- https://github.com/Team-PlanOut/planout-backend /202210/ts/inactive
  - https://planout-one.vercel.app/
  - Task Manager Application for Casual Event Planning
  - https://github.com/Team-PlanOut/planout-frontend
    - Plan events and get notifications when tasks are completed.

- https://github.com/robgietema/nick /MIT/202401/js
  - Nick is a (nearly) headless CMS written in Node.js which provides a RESTful hypermedia API. 
  - The API is compatible with the REST API of the Plone CMS and can be used together with the web frontend Volto.

- https://github.com/thedevs-network/kutt /MIT/202211/ts/inactive
  - a modern URL shortener with support for custom domains. 
  - Shorten URLs, manage your links and view the click rate statistics.
  - 依赖Express、Passport、Next、EasyPeasy-State、Recharts、PostgreSQL、Redis
  - Admin account to view, delete and ban links.
  - Set password for links.
  - Expiration time for links.
  - https://github.com/recaptime-dev/rtappdotio /202204/ts/inactive
    - Source code for the Kutt instance at rtapp.tk, in-sync with the upstream
  - https://github.com/OldSergo/kutt /202401/ts

- https://github.com/lungers/wastebin /AGPLv3/202307/ts/inactive
  - yet another pastebin and url shortener

- https://github.com/colic-nevena/docsy /202306/ts/inactive
  - Document sharing PWA using React, Express and OneSignal
# utils
- https://github.com/justsml/knex-full-text-search /202308/ts
  - A Knex plugin for easy Full-text Search queries in Postgres.

- https://github.com/ArturAralin/knex-elephant /MIT/202009/ts
  - PostgreSQL special sql functions for Knex library

- https://github.com/butopen/pg2ts /202203/ts
  - Convert Postgres Tables to Typescript constants to be used in your SQL queries with a single command

- https://github.com/mrdulin/nodejs-pg-knex-samples /MIT/202001/ts
  - Learning PostgreSQL, knex.js by examples.

- https://github.com/jadbox/mongoose-sql /201702/js
  - Mongoose compatible interface for PostgreSQL
  - uses Knex to interface with PostgreSQL

- https://github.com/baethon/kex /MIT/202111/js
  - Kex is a query extension for Knex. 
  - It uses the concept of "model" from ORMs like Lucid, or Laravel Eloquent restricted only to make queries. It has support for scopes, plugins, relations, and many more.

- https://github.com/felixmosh/knex-paginate /MIT/202303/js
  - Extension of Knex's query builder with `paginate` method that will help with your pagination tasks.
  - This lib got inspiration from knex-paginator.
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

- https://github.com/wholebuzz/db-json-column /202111/ts
  - JSON column support for Knex and TypeORM
  - If you need to query JSON columns with your Query Builder and Connection Pool without writing raw SQL, this package is for you.

- https://github.com/FleekHQ/knex-flex-filter /201907/js
  - a no-dependency package that adds dynamic filter functionality to Knex.
  - you can send the server side a `{'price_gt', 100}` param that can be directly interpreted by Knex Flex Filter 

- https://github.com/kibertoad/knex-tablecleaner /202109/js
  - Simple library for deleting all rows from a given list of DB tables. 
  - Tables are cleaned sequentially in a given order, to avoid foreign key constraint violations.

- https://github.com/acro5piano/knex-with-relations /MIT/202310/ts
  - A Knex plugin for batch loading table relations.
  - Provides convenient method to fetch both n-1 relation and 1-1 relation

- https://github.com/danielgindi/knex-schema-builder /MIT/202009/js
  - A schema builder module for knex.js, handles schema initialization and migration
  - I built this little helper so I can have a way of easily describing a database schema and automate the process of database initialization for an installation of a project - or migration of the database to newer versions.

- https://github.com/kriasoft/knex-types /MIT/202212/ts/inactive
  - An utility module for Knex.js that generates TypeScript definitions (types) from a PostgreSQL database schema.

- https://github.com/TRUEPIC/queryql /MIT/202401/js
  - QueryQL makes it easy to add filtering, sorting, and pagination to your Node.js REST API through your old friend: the query string
  - QueryQL works with any Node.js web framework (be it Express, Koa, etc.), supports any query builder / ORM through adapters, and allows for custom validators so you can define validation in a familiar way.
  - QueryQL supports knex/joi
  - QueryQL takes a parsed query string (like Express' req.query) and translates it into the appropriate function calls that your query builder / ORM understands to filter, sort, and paginate the records.

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

- https://github.com/plinioduartt/ts-transaction-manager /202303/ts
  - Abstracted transaction control for Typescript decorators, to facilitate transaction management and make the code cleaner.
  - Supported: Knex/Typeorm
  - you can use the `@Transactional` decorator at usecases/services/adapters layer without the fear of coupling the layers of your application with the ORM specific syntax.

- https://github.com/waitingsong/kmore /MIT/202402/ts
  - SQL query builder based on Knex with powerful TypeScript type support.
  - Declarative Transaction via decorator `@Transactional`.
  - Type-safe join table easily

- https://github.com/smooth-code/knex-scripts /202211/js
  - Knex utilities to interact with Postgres database.

- https://github.com/knex/knex-utils /202303/ts
  - Useful utilities for Knex.js
  - checkHeartbeat
  - DB relation difference operations

- https://github.com/KarmaBlackshaw/knex-meta /202306/ts
  - Useful extensions for knex query builder

- https://github.com/StreetStrider/knexed /202007/js
  - Utilities for tables, joins, transactions and other.

- https://github.com/justsml/knex-spatial /202309/ts
  - Knex plugin for Postgis w/ geospatial helper methods

- https://github.com/knex/knex-repositories /MIT/202303/ts
  - Parametrized CRUD repository abstraction for Knex.js
  - https://github.com/cubos/knex-repository /202207/ts
- https://github.com/cornflowerblu/knex-repository /202207/ts
  - a simple repository pattern using native PG & Knex as a light wrapper for serialization.
  - https://github.com/allie-wake-up/birchtree /201805/ts
    - a repository library built on knex

- https://github.com/js-items/foundation /201910/ts/inactive
  - Provides set of interfaces, utils and tests for concrete implementations of js-items repositories.
  - implementing the Repository Pattern for JavaScript Entities
  - https://github.com/js-items/knex
    - Concrete implementation of js-items for knex.js

- https://github.com/dialexa/knex-plus /201810/ts
  - A lightweight repository library powered by KnexJS
  - an extremely lightweight layer on top of Knex
  - It's not meant to be extensive, support associations (belongs to, has many), etc

- https://github.com/day1co/fastdao /MIT/202402/ts
  - fast and simple dao using knex
# testing
- https://github.com/felixmosh/knex-mock-client /MIT/202310/ts
  - A mock client for knex which allows you to write unit tests with DB interactions
  - Each db request that your app makes throughout knex will be registered in a scoped (by query method) history call list. 
- https://github.com/jbrumwell/mock-knex /MIT/202312/js
  - A mock knex adapter for simulating a database during testing, especially useful when used in combination with fixture-factory.
# devops
- https://github.com/ozum/knex-migrate-sql-file /MIT/202303/ts
  - Use sql files instead of (or in addition to) `knex.schema` methods.
  - Exports getMigrators, upSQL and downSQL functions which executes knex.raw() method on SQL files having same file name appended .up.sql and .down.sql.

- https://github.com/jfollmann/knex-migrations-ts /202108/ts
  - Sample to use knex migrations with PostgreSQL and Typescript support.

- https://github.com/TryGhost/knex-migrator /MIT/202312/js
  - A database migration tool for knex.js, which supports MySQL and SQlite3.
  - Replicas are unsupported, because Knex.js doesn't support them.
  - Sqlite does not support read locks by default.

- https://github.com/flodlc/pg-mate /202303/ts/inactive
  - a migration management tool for PostgreSQL 
  - Customizable client injection for migrations (native pg driver, zapatos, or any other client you want)
  - First-class CLI and programmatic usage

- https://github.com/asteinarson/knemm /202106/ts
  - a tool and library intended for DB schema administration, manipulation and inspection, for relational (SQL) databases
  - It can be used both as a standalone CLI tool and as a Node.js dependency
  - It relies largely on the Knex.js library for connecting with and executing generated queries.

- https://github.com/wgrisa/knex-migration-with-schema /202110/ts
  - Simplifies the execution of database migrations across different schemas with Knex
  - This library offers two functions, one to create new schemas, and one to execute migrations on a schema

- https://github.com/why2pac/knex-automigrate /MIT/202206/js
  - Table schema based database migration tool, built on top of the knex.js
  - Migration schema file name must be started with table_.

- https://github.com/sheerun/knex-migrate /MIT/201909/js
  - Modern database migration toolkit for knex.js
  - 100% compatible with knex.js migrations cli

- https://github.com/niradler/rve-knex-migration /201711/js
  - reverse engineer db to knex migration file

- https://github.com/marcbachmann/knex-umzug /202304/js
  - A storage adapter for umzug, a database migration library.
  - It supports namespacing and custom database table names. 
  - This storage adapter not only shows you the current state of a migration but also shows all the migration paths and tracks hostname and system user which executed a migration.
  - This library only makes knex work with umzug. Please check out the umzug api for more details

- https://github.com/maxcnunes/mongo-to-knex /201702/js
  - Applies mongo standard query to knex query builder.

- https://github.com/Vincit/knex-db-manager /ISC/202008/js
  - Utility for create, drop, truncate etc. administrative database operations.
  - Library uses knex connection for non administrative queries, but also creates privileged connection directly with driver with superuser privileges for creating and dropping databases / roles.

- https://github.com/leapfrogtechnology/sync-db /MIT/202306/ts/inactive
  - Command line utility to synchronize and version control relational database objects across databases.
  - This utility uses Knex under the hood
# more
- https://github.com/nire0510/jsoq /GPLv3/202310/ts
  - Query and manipulate JSON arrays easily. 
  - Powered by lodash, inspired by knex and SQL in general.
