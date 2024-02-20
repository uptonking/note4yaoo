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
  - [Multitenancy using multiple databases using knex](https://vincit.github.io/objection.js/recipes/multitenancy-using-multiple-databases.html)
# popular
- https://github.com/masb0ymas/expresso-sequelize /MIT/202310/ts/提交多/功能丰富
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
  - 仅支持第3方登录，未提供注册
  - https://github.com/bissbr01/Command-backend /js
    - 依赖sequelize6
    - A containerized REST API for the Command project managment app.

- https://github.com/ruyd/automated-express-backend /202306/ts
  - NodeJS Express Starter for backends and microservices
  - Auto CRUD API Routes for Models
  - Auto SwaggerUI Admin
  - Non-invasive, allows regular/custom backend work
  - Database Migrations with umzug
  - JWT Security RS256
  - 数据库依赖docker
  - https://github.com/ruyd/fullstack-monorepo /202306/ts/提交多
    - Fullstack Canvas Drawing App and TypeScript Starter Template
    - React, Redux, React Query, Material UI
    - Sequelize, Postgres, auth0
    - 支持注册新用户、admin界面
    - http://localhost:3000/admin/settings

- https://github.com/lalalilo/express-crud-router /113Star/MIT/202201/ts/无db
  - https://github.com/nicgirault/express-crud-router /202309/ts
  - Expose resource CRUD routes for Express & Sequelize. 
  - Compatible with React Admin Simple Rest Data Provider. 
  - The lib is ORM agnostic
  - https://github.com/lalalilo/express-crud-router-sequelize-v6-connector

- https://github.com/MyungWanPark/shopping-mall-backend /202401/ts
  - https://github.com/MyungWanPark/shopping-mall-frontend
  - https://shoppingmall-myungwan.netlify.app/
  - 后端express、sequelize、mysql、jwt
  - 前端依赖react、mui、ApexCharts、axios
  - State Management: Context API
  - 支持注册登录jwt、购物车、简单销售仪表板、搜索

- https://github.com/tiagospeckart/geekscript-backend
  - https://github.com/GabrielGameDev/geek-script-front
  - This repository is the final project for the Gama Academy Web Development course
  - 实现了登录，未实现注册

- https://github.com/nmanikiran/rest-api-node-typescript /202106/ts/inactive
  - simple REST API with node and express with typescript
  - 架构典型，可通过api访问数据 http://localhost:3009/api/lessons
  - 不支持jwt

- https://github.com/feathersjs-ecosystem/feathers-sequelize /202306/ts
  - A Feathers service adapter for the Sequelize ORM. 
  - Supporting MySQL, MariaDB, Postgres, SQLite, and SQL Server

- https://github.com/sequelize/express-example /js
  - A proposal for the usage of Sequelize within an Express. JS application.

- https://github.com/overlookmotel/sequelize-hierarchy /js/201906/inactive
  - Relational databases aren't very good at dealing with nested hierarchies like **folders/categories/Tree**
  - To store a hierarchy in a database, the usual method is to give each record a `ParentID` field which says which is the record one level above it.
  - if you want to retrieve an entire tree/hierarchy structure from the database, it requires multiple queries, recursively getting each level of the hierarchy. 
    - For a big tree structure, this is a lengthy process, and annoying to code.
    - This plugin for Sequelize solves this problem.
  - Requires Sequelize v2.x.x, v3.x.x, v4.x.x or v5.x.x.
  - [Add initial support for Sequelize V6](https://github.com/overlookmotel/sequelize-hierarchy/pull/223)
  - [Sequelize V6](https://github.com/overlookmotel/sequelize-hierarchy/issues/174)
  - https://github.com/fizure/sequelize-hierarchy
  - https://github.com/astrosoftpro/sequelize-hierarchy-next
  - https://github.com/SecurityESys/sequelize-hierarchy

- https://github.com/grantcarthew/node-mppg /js/inactive
  - The Materialized Paths pattern is a simple method to store tree or hierarchical data into a flat data store. 
  - It stores each tree node as a row in a table. 
  - Each row stores the identifiers of the node’s ancestors or path as a string.
  - The pattern also provides more flexibility in working with the path, such as finding nodes by partial paths.

- https://github.com/sequelize/sequelize-sscce /202402/ts
  - Base repository for creating and sharing Sequelize SSCCEs
  - Use this repository to create an SSCCE for your issue
  - Short, Self Contained, Correct (Compilable), Example

- ddd-forum /1.8kStar/ISC/202306/ts/hacker-news
  - https://github.com/stemmlerjs/ddd-forum
  - https://dddforum.com/
  - Hacker news-inspired forum app built with TypeScript using DDD practices from solidbook.io.
  - 后端依赖 express、sequelize、redis
  - 前端依赖 react、redux、react-quill
  - https://github.com/dyarleniber/typescript-ddd-forum

- MBBS /52Star/MIT/202207/ts/功能全
  - https://github.com/linfaxin/MBBS
  - http://mbbs.cc/
  - [论坛等级和功能对比](http://bbs.mbbs.cc/#/thread/detail/5)
  - 轻量级全功能论坛、移动/PC双端适配、无依赖一键启动、技术栈 express + sqlite + react
  - 后端依赖express、sequelize、sqlite3、svg-captcha
  - 前端依赖mui、ahooks、umi3
  - 全功能论坛：板块/楼中楼/角色权限/审核/富文本编辑/个性化配置/邮件通知 等
  - 自带授权登录：免开发支持 QQ/微信/支付宝 授权登录

- https://github.com/PelagicCreatures/marlin /202204/js/inactive
  - An ExpressJS CMS for sites with Sequelize db backends
  - Data model driven database (sequelize)
  - Admin data editing UI suite automatically built from data model
  - ACL access control on tables by user role (superuser, admin, etc.)
  - 前端依赖pug，未找到prosemirror
  - https://github.com/PelagicCreatures/marlin-app
    - a boilerplate app that includes many common functions of a web site/app featuring registered users. 
    - we use HIJAX to load pages after the initial load. 
    - 【DOM编程艺术】 Hijax---渐进增强地使用Ajax 
    - 按照老传统，让表单把整个页面都提交到服务器，然后服务器再发回来一个包含反馈的新页面，所有处理操作都在服务器上完成
    - 为了给这个登录表单添加AJAX功能，就需要拦截提交表单的请求,让XMLHttpRequest请求来代为发送

- https://github.com/FujiBilly/partition-sequelize-ts /201909/js
  - 改进 sequelize-typescript 库使其支持 Postgresql 10/11版本的分区表
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

- https://github.com/tomjschuster/sequelize-ui /BSD/202402/ts
  - https://sequelizeui.app/
  - a Sequelize ORM code generator, which generates a full Node.js TypeScript project, entirely in the browser
  - Use the schema editor to design your database tables, fields and associations, then preview the Sequelize models and migrations in the code viewer before downloading the project as a zip file or copying code from individual files.
  - Sequelize UI currently only generates TypeScript Sequelize code, not js

- https://github.com/andyforever/sequelizer
  - A GUI Desktop App for export sequelize models from database automatically.
# apps-v6
- https://github.com/demamano/File-Import /202306/ts
  - file import with reatTS , NodeTS, and express , sequelize , mysql

- https://github.com/juravlevdima/PERN-chat
  - Chat made with PERN Stack & Socket. IO
  - React | React Router | Redux Toolkit
  - Real-time chat using web-sockets

- https://github.com/khaled-badenjki/cilo /202307/js
  - Cilo simplifies the build of multi tenant applications by providing a wrapper around sequelize that handles the multi-tenancy for you.
  - The code will bahave the same as if you were building a single tenant application.

- https://github.com/Wind213/sequelize-multi-tenant /201901/js
  - An example of shared database schema isolated multi-tenant implementation with express, nodejs and sequelize.

- https://github.com/AnishLushte07/multi-tenant-application /201909/js
  - Multi tenant application using NodeJs, express, sequelize, mysql.

- https://github.com/ali-husnain/expressjs-multi-tenant-rest-graphql-api-boilerplate /js
  - This is a proof-of-concept (POC), multi-tenant RESTful Web Services application built on top of NodeJS.

- https://github.com/PIYoung/node-express-boilerplate-multitenant /MIT/202302/ts
  - node express postgres boilerplate for multitenant(saas)

- https://github.com/rreeves1996/team-manager /202309/ts
  - a MERN app (MySQL database) that functions as a team management app

- https://github.com/kanban-org/kanban-board /202402/js
  - https://www.kanban.live/
  - full-stack Kanban task management app
  - 依赖Sequelize

- https://github.com/fnfacun/Koa_trello /202005/ts
  - 后端 - trello 团队协作工具
  - 模仿 trello 团队协作工具 首页是用户面板
  - koa-static-cache, sequelize-typescript

- https://github.com/lukasbals/scrumboard /202305/ts
  - The simplest task tracking tool for dev teams.
  - Next.js, Socket.io, React-DnD, MobX, Sequelize

- https://github.com/yuedun/issue-tracking-system /202005/ts/inactive
  - 基于Koa框架，layui，Sequelize.js5.x版本，使用TypeScript开发的事务跟踪系统

- https://github.com/raphaelalmeidamartins/fullstack-bank /202309/ts
  - Digital wallet full stack application developed with Next.js and Node.js

- https://github.com/thedenisnikulin/chattitude-app-backend /202206/ts/inactive
  - a well structured Typescript version of old Chattitude
  - https://github.com/thedenisnikulin/chattitude-app-frontend

- https://github.com/muttaqin1/CipherConvo /MIT/202311/ts
  - MERN stack chat app built with TypeScript, ReactJS, NodeJS, ExpressJS, Inversify, Sequelize, Websocket, and JWT.
  - This chat app is End-to-End encrypted. 
  - The project is fully coded using OOP with inversion of control and dependency injection

- https://github.com/srujan-nalam/Link-chat-application /202304/ts
  - a full stack chat application. You can chat privately or in a group and send images if you wish.
- https://github.com/ahmedsemih/Fullstack-Chat-App /202304/ts
  - Full Stack Realtime Chat App. Built with React, Nest.js and Socket.io.

- https://github.com/FitseTLT/social-media-app /202309/ts
  - social media web app developed with Node (Express), React, and MySQL DB with sequelize.js for ORM. 
  - It uses Web socket for live chat and WebRTC for audio and video calls.

- https://github.com/liadber/together /202401/ts/angular
  - a basic social network designed for entrepreneurs. 
  - Users can create profiles, share projects, 

- https://github.com/attila-huszar/fox-ticket /202402/ts
  - Fox Ticket Full Stack Project

- https://github.com/nirav-v/hardpost /202402/ts
  - https://www.hardpost-shop.com/
  - Developing an e-commerce marketplace for skateboarders to sell and purchase skate-related items.

- https://github.com/TULENp/ExpReader /202402/ts
  - Online bookstore and reading app with a gaming motivation system

- https://github.com/kunalkeshan/Social-Sphere /MPLv2/202310/ts
  - Web app that allows users to create their own personal page to share their social media links and other personalized links
  - The backend handles the data storage and retrieval using MongoDB, while the frontend is responsible for rendering the user interface and making API calls to the backend.

- https://github.com/xcfstudio/woodfish-server
  - 多用户电子木鱼系统，基于Koa2
  - https://github.com/xcfstudio/woodfish-app /vue

- https://github.com/nban38/NFT_API_Typescript
  - Node Js ( Typescript )

- https://github.com/viclafouch/meme-studio
  - creating and sharing "internet memes"

- https://github.com/Kshitiz1403/Collaborative-IDE /202401/ts/yjs
  - a full stack system supporting collaborative code editing, compiling & shared shell.
  - Monaco editor is the internal implementation of VSCode's editor. I am using the React port of it Monaco for React.
  - I am using Yjs for providing CRDT & conflict free collaborative editing

- https://github.com/kamilmuzyka/reviseus /202312/ts
  - a single page application created as a place for peer reviews and revisions
  - The server runs as a Node/Express application that uses PostgreSQL as a database.

- https://github.com/YamanSD/Dexter /202312/ts
  - an online compiler that leverages Node.js and Docker to execute user-provided programs. 
  - It offers dynamic Docker image creation, ability to add and remove programming languages, and maintains a database to log user execution statistics.
  - Dexter utilizes MySQL to store user execution statistics. 
  - The editor provides syntax highlighting, suggestions, & many more features that are provided by the Monaco editor.

- https://github.com/idea2app/iWebLog /202312/ts
  - Light-weight Personal Web App (PWA) based on Next.js, MobX & Sequelize

- https://github.com/affan-ch/Linko /MIT/202311/ts
  - open-source Link Management platform designed to simplify URL handling with an array of features, including a URL shortener, tracking capabilities, QR code generator, Bio pages, and more.

- https://github.com/Slash-Go/SlashGoServer /MIT/202211/ts
  - The most seamless way to manage intra-organization knowledge through memorable shortlinks

- https://github.com/Maxinum/WareHouseBot /202308/ts
  - Telegram bot for keeping records of deliveries and sales

- https://github.com/danirod/djs-tagbag /202304/ts
  - A simple key-value storage for persisting tags into your Discord.js bots.

- https://github.com/jihunhong/VanillaChart /202210/ts
  - CherryChart BACK-END (express, typescript)
  - https://github.com/jihunhong/CherryChart-Client /202210/js
# starter
- https://github.com/cirosantilli/node-express-sequelize-nextjs-realworld-example-app /202208/ts/be+fe
  - Node.js + Express.js + Sequelize + SQLite/PostgreSQL + Next.js fullstack static/SSG/ISG Example Realworld App
  - https://github.com/cirosantilli/node-express-sequelize-realworld-example-app /202106/js

- https://github.com/TonyMckes/conduit-realworld-example-app /202303/js/be+fe
  - created to demonstrate a fully fledged fullstack application built with React / Express.js / Sequelize / PostgreSQL including CRUD operations, authentication, routing, pagination, and more.
- https://github.com/chojs23/realword-express-sequelize /202303/js
  - sequelize ^6.26.0
- https://github.com/Varun-Hegde/Conduit_NodeJS /202105/js
  - Express and NodeJS based backend implementation of the RealWorld API Spec.
  - MySQL + Sequelize

- https://github.com/boxpositron/typescript-webpack-sequelize-template
  - NodeJS Server Template with support for sequelize and webpack
  - 过于简单

- https://github.com/CuaMcCarsaree44/typescript-expressjs
  - Turns out I made a boilerplate code through this repository.

- https://github.com/StefanNedelchev/express-sequelize-ts-example /202401/ts
  - A basic example of using express with sessions, sequelize and typescript.
  - basic NodeJS application for web API microservices that uses express with express-session, sequelize-typescript to connect to a SQL database and authenticate users.
  - The app is written following the proper OOP approach using TypeScript classes with decorators
  - 过于简单
  - If the registration/login was successful, the user should be instantly logged in with a session. 

- https://github.com/felipecal/Api-Sequelize /MIT/202402/ts
  - This is a simple CRUD api in TypeScript, sequelize, aws rds or docker database.
  - 依赖express、sequelize、swagger-ui-express、bcrypt
  - AWS RDS or Docker Database
  - Swagger - Documentation

- https://github.com/mcaligares/express-typescript /202310/ts
  - Express project with Typescript support ready to start coding

- https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate /MIT/202205/ts/typedi/inactive
  - ExpressJS Boilerplate with Typescrip+Docker+Sequelize integration

- https://github.com/kushalshit27/nodejs-sequelize-typeScript /202402/ts
  - build your own API with Node.js + Express+ Sequelize + TypeScript

- https://github.com/ljlm0402/typescript-express-starter /202301/ts
  - Express RESTful API Boilerplate Using TypeScript，可选参数的模版项目
  - 支持mongoose、多种orm、graphql
- https://github.com/SamuelMarks/restify-orm-scaffold /202402/ts
  - Simple baseline scaffold to get you started using TypeORM and/or Sequelize and/or Waterline on restify with TypeScript.

- https://github.com/Thre4dripper/NodeTs-Express-Service-Based-Template /MIT/202401/ts
  - configurable Node.js, Express, and TypeScript server template with a service-based architecture 
  - Database Compatibility: Interact with MySQL, PostgreSQL, MariaDB, Sqlite, MSSql, MongoDB.

- https://github.com/codespede/pwoli /202311/ts
  - Pwoli is a NodeJS/TypeScript framework written in TypeScript which can work independantly on a raw NodeJS/TypeScript environement OR, in co-ordination with any other frameworks or libraries like Express.js.
  - Pwoli can connect to any kind of ORMs by implementing thier corresponding ORM Adapters and works with Sequelize and Mongoose 

- https://github.com/Thre4dripper/node-server-init /202401/ts
  - initializing Node.js server projects with customizable configurations.
  - npx node-server-init my-server
  - Sequelize & Mongoose: Integrations with Sequelize for SQL database operations and Mongoose for MongoDB.

- https://github.com/weareopensource/Typescript /202110/ts/inactive
  - TypeScript - Boilerplate Back : Express, Jwt, Mongo, Sequelize (Draft)
- https://github.com/faid-terence/SequelizePostgresExpressMagic /202402/ts
  - Sequelize + pg
  - Utilizes JWT for secure authentication.

- https://github.com/kazi-naimul/typescript-express-mysql-boilerplate /202312/ts
  - A boilerplate for any enterprise rest api or service with Node.js -Typescript, Express and Sequelize ORM for mysql, postgresql or others.

- https://github.com/HUNTER9881/Sqlite_Express_Typescript
  - [Node.js + TypeScript + MongoDB: JWT Authentication 2023](https://codevoweb.com/node-typescript-mongodb-jwt-authentication/)

- https://github.com/salino3/node-typescript /202402/ts
  - front + back

- https://github.com/ImRLopezAG/Ts-Api-Template /202311/ts
  - This is an API template made with express and typescript, to speed up your development, it contains repositories and generic services for the typical CRUD actions, based on a Sequelize model, we use it for data persistence

- https://github.com/Murilo-MRS/nodejs-ts-boilerplate /202401/ts
  - Boilerplate NODEJS TYPESCRIPT SEQUELIZE MYSQL
  - https://github.com/juananmuxed/template-ts-api /202312/ts
  - https://github.com/nabadeep25/typescript-node-sequelize-boilerplate /202310/ts
  - https://github.com/SourceSprint/ts-webpack-sequelize-template /202308/ts

- https://github.com/SystangoTechnologies/koach-typescript /202203/ts/inactive
  - Production ready boilerplate for building APIs in Typescript(3.4) with koa2, and using SQL database and http/2 as the communication protocol.

- https://github.com/teo-garcia/fastify-template-sequelize
  - using Fastify with Sequelize.

- https://github.com/designly1/nextjs14-auth-sequelize-starter /202402/ts
  - starter app with Sequelze ORM and JWT authentication

- https://github.com/saulotarsobc/electronjs-with-nextjs /202401/ts
  - ElectronJS application with NextJS and TypeScript
# auth
- https://github.com/diegomottadev/auth-base-app /202402/ts
  - This repository contain a REST API project for creating users, user roles, and user authentication using Node.js, Express.js, and Sequelize with TypeScript.

- https://github.com/rahulthackkar/nodejs-mysql-jwt-sequelize /js
  - Node JS + Express + User authentication using JWT + Sequelize + Jest + Docker

- https://github.com/PROTEK-ID/mern-auth-template /202309/ts
  - MERN Stack Authentication using Sequelize (MySQL as dialect) for backend template.

- https://github.com/bezkoder/node-js-express-login-example /js
  - Express Login example (with Registration) using JWT, Cookies, MySQL database
  - 流程图很清晰
  - [Node.js Express: Login and Registration example with JWT - BezKoder](https://www.bezkoder.com/node-js-express-login-example/)

- https://github.com/kylewhittemore/react-sequelize-template /js
  - Full-stack react with passport js local strategy for authentication
# utils
- https://github.com/tylerjpeterson/sequelize-history /js
  - This module will setup automatic revision tracking for any Sequelize model. 
  - This is effectively a re-write of sequelize-temporal
- https://github.com/nielsgl/sequelize-paper-trail /js
  - Sequelize plugin for tracking revision history of model instances.

- https://github.com/sequelize/sequelize-auto /202112/ts
  - Automatically generate models for SequelizeJS via the command line.
- https://github.com/spinlud/sequelize-typescript-generator /202310/ts
  - Automatically generates typescript models compatible with sequelize-typescript library directly from your source database.
- https://github.com/zcong1993/auto-sequelize-typescript /202111/ts
  - auto generate model files from exists db schemas

- https://github.com/TeamMaestro/sequelize-common /202308/ts
  - A common set of models and functions that we use throughout most of our Sequelize projects

- https://github.com/sequelize/sequelize-typescript
  - Decorators and some other features for sequelize (v6).

- https://github.com/doralteres/express-sequelize-autocrud /MIT/202402/ts
  - library designed to simplify the creation of CRUD (Create, Read, Update, Delete) routes for your Sequelize models in an Express.js
  - Middleware Support: Integrate custom middleware functions with generated routes to extend functionality.
  - Transaction Support: Create, Update and Delete routes runs inside sequelize transaction 

- https://github.com/bitovi/hatchify /202402/ts
  - a web application framework designed to accelerate the development of CRUD applications
  - provide you with a fully functional system straight from a datatype schema. 
  - Our frontend will use React and MUI, and our backend will be using Koa.

- https://github.com/Kaltsoon/sequelize-cursor-pagination /202211/ts
  - Cursor-based pagination queries for Sequelize models
- https://github.com/ephys/sequelize-cursor-pagination /202110/ts
  - GraphQL-ready cursor pagination for Sequelize.
  - This library has been designed with the GraphQL Cursor Connections Specification in mind, but can likely be used for any cursor pagination (including REST).
- https://github.com/unthread-io/sequelize-cursor-pagination /202303/ts
  - Cursor (aka keyset) pagination for Sequelize.

- https://github.com/rfink/sequelize-redis-cache /js
  - Small fluent interface for caching sequelize database query results in redis more easily

- https://github.com/nealwp/smodg
  - Generate Sequelize models from TypeScript type definitions

- https://github.com/blankstar85/sequelize-central-log
  - Maintain Sequelize Model change history in a central table. 
  - This is highly configurable and supports composite primary keys ( up to 3 for now). 
  - Written in Typescript and provides typing.

- https://github.com/westmark/sequelize-multi-tenant-enhancer /201702/js
  - A Proxy based enhancer function which enables schema based multi tenancy in Sequelize.

- https://github.com/pilagod/uow-sequelize /ts/inactive
  - Unit of Work pattern implementation for Sequelize, based on uow-template.

- https://github.com/easygrating/sequelize-query-parser /202401/ts
  - Query string parser to sequelize query object
  - designed to simplify the process of parsing client requests and creating Sequelize-compatible queries effortlessly.

- https://github.com/alexsanteenodev/nodemailer-sequelize-queue /202402/ts
  - This package allows to queue email and process it later by schedule using Nodemailer for sending mails, Sequelize for save queue to database and Node cron for scheduling.

- https://github.com/actionhero/ah-sequelize-plugin /202309/ts
  - This plugin connects Sequelize and Actionhero
  - It handles running migrations and connecting your models.
  - Under the hood, we use sequelize-typescript and Umzug

- https://github.com/FaetterP/opensearch-sequelize /202311/ts
  - Sequelize-like promise-based Node.js ORM tool for OpenSearch.

- https://github.com/BleeveNL/apistart /202311/ts
  - A NodeJS Framework that is build to create single purpose microservices lightning fast.
  - The goal is to generate a strictly typed NodeJS framework 

- https://github.com/momentohq/momento-sequelize-cache /apache2/202310/ts
  - This project provides a Momento-backed read-aside caching implementation for sequelize. 
  - The goal is to provide an interface for caching sequelize queries.
  - You can use Momento as your caching engine for any relational databases that are a part of sequelize's dialects.
  - To use this library, you will need a Momento API key. 
# ddd/cqrs
- https://github.com/Judahh/flexiblePersistence /ts
  - A CQRS and Event Sourcing platform
  - It's possible to use different databases or services implementing IPersistence interface, like MongoDB does (MongoPersistence).
  - Other implementations: DAO, Sequelize, Service
  - https://github.com/Judahh/sequelizePersistence

- https://github.com/sugarandmagic/sequelize-mv-support /MIT/ts
  - This package adds support for Views and Materialized Views in Sequelize.
  - We're heavy users of views and materialized views, but we use Sequelize a lot for bootstrapping and testing database schema. 
  - this module adds support for both views and materialized views to Sequelize, as well as properly exporting typescript declarations.
  - All the original Sequelize methods and options still work with this module

- https://github.com/s4nt14go/white-label /202312/ts
  - Serverless Domain-Driven Design (DDD) with unit tests
  - This project exemplifies a CreateUser use case and how we can trigger an event, signaling we have a new user onboard.
  - DBs: PostgreSQL CockroachDB Serverless and DynamoDB
  - ORM: Sequelize
  - AWS services: Lambda, AppSync, Systems Manager Parameter Store
  - I started this project using Khalil Stemmler's white-label users module and applied some concepts based on Vladimir Khorikov courses where he tackles DDD in a great way.

- https://github.com/QuaNode/beamjs /js
  - Enterprise full stack web development framework (Backend-JS - ExpressJS - AngularJS - MongoDB)
  - BeamJS is built above Backend-JS to provide data controllers for SQL and No-SQL databases. It also includes file system controllers that work on a local file system or cloud storage.
  - These data controllers are abstract adapters above ODM/ORM patterns of MongooseJS and SequelizeJS. These data controllers are abstract adapters above ODM/ORM patterns of MongooseJS and SequelizeJS.
  - supports CQRS architecture through mixed model definitions over different DBs.
  - supports Horizontal/DB multi-tenancy by automatically handling multi-DB connection mapping.
  - https://github.com/quaNode/Backend-JS /js
    - a layer built above expressjs and socket.io to enable behaviours framework for nodejs applications.

- https://github.com/luizcalaca/ddd-typescript-sequelize-node-api /ts
  - Domain Drive Design + Clean Architecture + Node.js + Typescript + Sequelize

- https://github.com/joshuaalpuerto/node-ddd-boilerplate /js/inactive
  - Node DDD Boilerplate
  - Sequelize is used to define mappings between models and database tables

- https://github.com/rezeus/kernel /js/inactive
  - Kernel for event-driven applications.
  - Asynchronous event is a regular event whose listener returns a Promise.

- https://github.com/flux-capacitor/flux-capacitor /MIT/js/inactive
  - Flux architecture for the backend. Realtime data and time travel capabilities included.
  - Works like Redux. Dispatch events to change database data
  - Events are persisted, thus tracking the database's history
  - Pushing realtime data becomes trivial, since you can subscribe to the store for updates
  - **Isomorphic reducers - Share code between back end and front end**
  - Middleware concept, compatible with Redux middleware
  - No lock-in: Ability to opt-out any time and just use the underlying database directly
  - Finer-grained access control - Control write access by event type, not only by table
  - Works with PostgreSQL, MySQL, SQLite & MSSQL using Sequelize right now
  - It is related to CQRS, but no traditional CQRS. Rather something between common CRUD and traditional CQRS.
  - Differences to Redux
    - Reducer's signature is `(collection, event) => changeset` instead of `(state, action) => state`. The `action` and the `event` are just synonyms.The real difference is that the flux capacitor reducers take a database collection and return a changeset (a set of database operations).
    - This is necessary, since we usually cannot hold the complete database in memory as opposed to Redux' state.
  - Differences to traditional CQRS
    - No distributed system by default, but just one data storage service (can be easily turned into a cluster, though)
    - No aggregates, just one read model to check business rules when handling an event
    - Depends on database transactions to ensure data consistency
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
# search
- https://github.com/mujz/pg-search-sequelize /js/inactive
  - Postgres full-text search in Node.js and Sequelize.
  - https://github.com/mujz/pg-search-sequelize-example /js/inactive
    - An example use case of pg-search-sequelize
# cms
- https://github.com/apstanisic/zmaj /ts
  - https://zmaj.vercel.app/
  - a headless CMS with RESTful API for your database and admin panel to easily manage your data
  - Built on top of React and React Admin for admin panel, and NestJS and Sequelize for API.
  - 依赖nestjs-passport、knex、sequelize
# testing
- https://github.com/omvmike/fake-entity-service /202401/ts
  - Library to simplify database data generation for testing purposes
  - aim is simplify database data generation for integration and end-to-end tests.
  - the main goal is to make it ORM agnostic. At the moment the library supports Sequelize ORM and TypeORM.
  - Target framework is NestJs but the code is framework agnostic 
  - The library was tested with Jest but it should work with any other test runner.
  - This library is inspired by Laravel's factory so you can find some similarities. But since it's a TypeScript library, it has quite different syntax.

- https://github.com/NielsSteensma/sequelize-typescript-mock-examples /201911/ts
  - Examples of mocking sequelize-typescript models with Jest.
# devops
- https://github.com/sequelize/umzug /MIT/202402/ts
  - Framework agnostic migration tool for Node.js
  - It provides a clean API for running and rolling back tasks.
  - Database agnostic

- https://github.com/mosano-eu/abmt /MIT/202310/ts
  - framework-agnostic migration to handle database maintainability needs, such as executing schema migrations, data seeding, and other type of time-based versioning operations.
# more
- https://github.com/metacollective9/sequelize-serverless-poc
  - Sequelize ORM (using typescript) with lambda function using the serverless framework.
  - https://github.com/dherault/serverless-offline
    - Emulate AWS λ and API Gateway locally when developing your Serverless project
