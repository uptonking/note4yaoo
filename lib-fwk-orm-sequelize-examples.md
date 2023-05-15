---
title: lib-fwk-orm-sequelize-examples
tags: [examples, sequelize]
created: 2023-02-05T18:50:23.632Z
modified: 2023-02-05T18:50:32.900Z
---

# lib-fwk-orm-sequelize-examples

# guide
- orm技术选型
  - issues数量
    - typeorm 1800+
    - knex 700+
    - sequelize 700+

- tips
  - 模版参考: react-admin
# popular
- https://github.com/masb0ymas/expresso-sequelize /提交多/功能丰富
  - Sequelize ORM v6.x + Sequelize TypeScript v2.x
  - Handlebars for templating HTML
  - Using Module Alias for simplify the require/import paths
  - Documentation with Swagger，但测试create user失败
  - 还提供了typeorm、mongoose版本
  - v5_20230404: improve apps with service pattern
  - https://github.com/masb0ymas/koala-sequelize-typescript /202103/ts/inactive
  - https://github.com/masb0ymas/expresso-gateway
    - Api Gateway with Express TypeScript

- https://github.com/bissbr01/Command-project-management /ts
  - A Scrum Management App for teams
  - 依赖reduxjs-toolkit、mantine、dnd-kit、formik
  - 提供了project、team等基础功能，还支持看板
  - https://github.com/bissbr01/Command-backend /js
    - 依赖sequelize6
    - A containerized REST API for the Command project managment app.

- https://github.com/ruyd/automated-express-backend
  - NodeJS Express Starter for backends and microservices
  - Auto CRUD API Routes for Models
  - Auto SwaggerUI Admin
  - Non-invasive, allows regular/custom backend work
  - Database Migrations with umzug
  - JWT Security RS256
  - 数据库依赖docker
  - https://github.com/ruyd/fullstack-monorepo
    - Fullstack Canvas Drawing App and TypeScript Starter Template
    - React, Redux, React Query,Material UI
    - Sequelize,Postgres,auth0

- https://github.com/lalalilo/express-crud-router /113Star/MIT/202201/ts/无db
  - Expose resource CRUD routes for Express & Sequelize. 
  - Compatible with React Admin Simple Rest Data Provider. 
  - The lib is ORM agnostic
  - https://github.com/lalalilo/express-crud-router-sequelize-v6-connector

- https://github.com/nmanikiran/rest-api-node-typescript /202106/ts/inactive
  - simple REST API with node and express with typescript
  - 架构典型，可通过api访问数据 http://localhost:3009/api/lessons
  - 不支持jwt

- https://github.com/sequelize/umzug
  - Framework agnostic migration tool for Node.js
  - It provides a clean API for running and rolling back tasks.
  - Database agnostic

- https://github.com/feathersjs-ecosystem/feathers-sequelize
  - A Feathers service adapter for the Sequelize ORM. 
  - Supporting MySQL, MariaDB, Postgres, SQLite, and SQL Server

- https://github.com/sequelize/express-example /js
  - A proposal for the usage of Sequelize within an Express. JS application.

- https://github.com/overlookmotel/sequelize-hierarchy /js/201906/inactive
  - Relational databases aren't very good at dealing with nested hierarchies like folders/categories/Tree
  - To store a hierarchy in a database, the usual method is to give each record a `ParentID` field which says which is the record one level above it.
  - if you want to retrieve an entire tree/hierarchy structure from the database, it requires multiple queries, recursively getting each level of the hierarchy. 
    - For a big tree structure, this is a lengthy process, and annoying to code.
    - This plugin for Sequelize solves this problem.
  - Requires Sequelize v2.x.x, v3.x.x, v4.x.x or v5.x.x.
  - [Add initial support for Sequelize V6](https://github.com/overlookmotel/sequelize-hierarchy/pull/223)
  - [Sequelize V6](https://github.com/overlookmotel/sequelize-hierarchy/issues/174)
  - https://github.com/astrosoftpro/sequelize-hierarchy-next
  - https://github.com/SecurityESys/sequelize-hierarchy
  - https://github.com/fizure/sequelize-hierarchy
# server-sent event
- https://github.com/dexterio200/chat-app-server
  - Server side of a chat room app - built with Node.js, Express, Sequelize & Server-sent events.

- https://github.com/nataliaev/game-server
  - https://github.com/nataliaev/game-client
  - using Node.js, Express, Sequelize and server-sent events.

- https://github.com/mvillarrealb/sequelize-event-stream
  - Event publishing capabilities for your sequelize's models using hooks
- https://github.com/joeybaker/sequelize-stream
  - Create a stream of Sequelize create, update, and destroy events. 
  - This is useful if you want to build a real-time stream of events in your database.
# v7
- https://github.com/tapiwakundi/movies-api /js
  - simple example
# apps-v7
- https://github.com/dez126/team-git-saved-backend-main
  - HomeTasktick App Backend

- https://github.com/GuilhermeSantos001/grupomavedigital
  - nestjs + seq@v7

- https://github.com/haandev/eaystate-backend /wip未完成
  - headless real estate cms backend
  - 后端依赖express、2版sequelize、minimist
  - https://github.com/haandev/easystate-dashboard

- https://github.com/fdc1010/cffi-admin-dashboard
  - CFFI Admin Dashboard powered by Argon Dashboard 2 MUI 

- https://github.com/Hemocione/competitions-backend
  - https://github.com/Hemocione/competitions-frontend /js

- https://github.com/craftycodie/Sunrise-Halo3-WebServices
  - A NestJS, Domain-Driven Design reimplementation of Halo 3's web services.
# v6
- https://github.com/Kaltsoon/sequelize-cursor-pagination
  - Cursor-based pagination queries for Sequelize models

- https://github.com/tomjschuster/sequelize-ui
  - https://sequelizeui.app/
  - a Sequelize ORM code generator, which generates a full Node.js TypeScript project, entirely in the browser
  - Use the schema editor to design your database tables, fields and associations, then preview the Sequelize models and migrations in the code viewer before downloading the project as a zip file or copying code from individual files.
  - Sequelize UI currenly only generates TypeScript Sequelize code, not js

- https://github.com/andyforever/sequelizer
  - A GUI Desktop App for export sequelize models from database automatically.

## apps-v6

- https://github.com/juravlevdima/PERN-chat
  - Chat made with PERN Stack & Socket. IO
  - React | React Router | Redux Toolkit
  - Real-time chat using web-sockets

- https://github.com/raphaelalmeidamartins/fullstack-bank
  - Digital wallet full stack application developed with Next.js and Node.js

- https://github.com/thedenisnikulin/chattitude-app-backend
  - a well structured Typescript version of old Chattitude

- https://github.com/xcfstudio/woodfish-server
  - 多用户电子木鱼系统，基于Koa2
  - https://github.com/xcfstudio/woodfish-app /vue

- https://github.com/nban38/NFT_API_Typescript
  - Node Js ( Typescript )

- https://github.com/viclafouch/meme-studio
  - creating and sharing "internet memes"
# starter
- https://github.com/boxpositron/typescript-webpack-sequelize-template
  - NodeJS Server Template with support for sequelize and webpack
  - 过于简单

- https://github.com/CuaMcCarsaree44/typescript-expressjs
  - Turns out I made a boilerplate code through this repository.

- https://github.com/StefanNedelchev/express-sequelize-ts-example
  - A basic example of using express with sessions, sequelize and typescript.
  - basic NodeJS application for web API microservices that uses express with express-session, sequelize-typescript to connect to a SQL database and authenticate users.
  - The app is written following the proper OOP approach using TypeScript classes with decorators
  - 过于简单

- https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate /typedi
  - ExpressJS Boilerplate with Typescrip+Docker+Sequelize integration

- https://github.com/ljlm0402/typescript-express-starter /202301/ts
  - Express RESTful API Boilerplate Using TypeScript，模版项目的模版
  - 支持mongoose、多种orm、graphql

- https://github.com/weareopensource/Typescript
  - TypeScript - Boilerplate Back : Express, Jwt, Mongo, Sequelize (Draft)

- https://github.com/HUNTER9881/Sqlite_Express_Typescript
  - [Node.js + TypeScript + MongoDB: JWT Authentication 2023](https://codevoweb.com/node-typescript-mongodb-jwt-authentication/)

- https://github.com/ImRLopezAG/Ts-Api-Template
  - This is an API template made with express and typescript, to speed up your development, it contains repositories and generic services for the typical CRUD actions, based on a Sequelize model, we use it for data persistence

- https://github.com/SystangoTechnologies/koach-typescript
  - Production ready boilerplate for building APIs in Typescript(3.4) with koa2, and using SQL database and http/2 as the communication protocol.

- https://github.com/teo-garcia/fastify-template-sequelize
  - using Fastify with Sequelize.
# utils
- https://github.com/rfink/sequelize-redis-cache /js
  - Small fluent interface for caching sequelize database query results in redis more easily

- https://github.com/nealwp/smodg
  - Generate Sequelize models from TypeScript type definitions
# more
- https://github.com/PIYoung/node-express-boilerplate-multitenant
  - node express postgres boilerplate for multitenant(saas)

- https://github.com/metacollective9/sequelize-serverless-poc
  - Sequelize ORM (using typescript) with lambda function using the serverless framework.
  - https://github.com/dherault/serverless-offline
    - Emulate AWS λ and API Gateway locally when developing your Serverless project
