---
title: lib-fwk-orm-sequelize-examples
tags: [examples, sequelize]
created: 2023-02-05T18:50:23.632Z
modified: 2023-02-05T18:50:32.900Z
---

# lib-fwk-orm-sequelize-examples

# guide

- tips
  - examples: starter, realworld, fullstack
  - 模版参考: react-admin
  - 数据库典型示例: 商品-货架， 电影-演员

- 后端架构总结
  - 通常三层架构就能满足开发需求且不繁琐，需要支持nosql时再添加dao或定制开发
  - controller: 请求接收，参数校验，权限校验，异常状态码，尽量没有业务逻辑，尽量只用一个service，
    - 若需要多个service则考虑创建新service包含所需业务流程
    - createX/newX, getX, updateX/saveX, removeX, register
  - service: 梳理业务流程，数据模型转换，使用所需的(多个)dao/repo进行计算与持久化返回结果dto
    - 返回的可以不是db中的model，可返回业务对象do/vo/dto
    - addX/insertX, findX/selectX, setX/updateByX, deleteX
  - dao: 只包含db的crud，尽量没有业务逻辑
    - dao的实现依赖orm，可能需要model，也可能不需要model
  - model: 对应db表schema
  - ioc的缺点: 调试时跳转到方法调用的定义不方便
  - [What is the best practice for service-dao pattern? - Stack Overflow](https://stackoverflow.com/questions/17639731/what-is-the-best-practice-for-service-dao-pattern)

- 动态添加route和建表
  - 多数模版项目的api route是固定的，动态添加api需要定制开发
  - 动态添加model需定制开发

- resources
# popular
- https://github.com/masb0ymas/expresso-sequelize /MIT/202402/ts/提交多/功能丰富
  - https://expresso.masb0ymas.com/
  - expresso with Sequelize
  - 采用controller/service/entity三层架构，class风格
  - 依赖axios、express-rate-limit、i18next-fs-backend、multer、node-cron、pg-hstore、sequelize-typescript2、zod
  - router使用了asyncHandler
  - Sequelize ORM v6.x + Sequelize TypeScript v2.x
  - Handlebars for templating HTML
  - Documentation with Swagger，但测试create user失败
  - 还提供了typeorm、mongoose版本
  - v5_20230404: improve apps with service pattern, 将工具lib拆分到了单独仓库
  - 运维使用docker，未使用k8s
  - https://github.com/masb0ymas/expresso
    - Library for expresso Template: core, hooks, query, provider
    - 💡📡 可参考实现knex版
    - Storage Provider ( Aws S3, Google Cloud Storage, and MinIO )
    - Memory Cache ( ioredis )
    - Permission Access per Endpoint API
  - https://github.com/masb0ymas/expresso-typeorm /MIT/202401/ts
  - https://github.com/masb0ymas/expresso-mongoose /202210/ts/inactive
  - https://github.com/masb0ymas/koala-sequelize-typescript /202103/ts/inactive
    - Just Boilerplate Koa, Sequelize and TypeScript 
  - https://github.com/masb0ymas/expresso-gateway
    - Api Gateway with Express TypeScript

- https://github.com/bissbr01/Command-project-management /202301/ts-fe/inactive
  - https://scrum-management-frontend.onrender.com/
  - A Scrum Management App for teams
  - 依赖reduxjs-toolkit、mantine、dnd-kit、formik
  - 提供了project、team等基础功能，还支持看板
  - 仅支持第3方登录，未提供注册
  - https://github.com/bissbr01/Command-backend /202303/js-be
    - A containerized REST API for the Command project management app.
    - 依赖sequelize6

- https://github.com/ruyd/automated-express-backend /202306/ts
  - NodeJS Express Starter for backends and microservices
  - 依赖express-jwt、firebase-admin、sequelize6、socket.io、swagger-ui-express、umzug
  - 采用controller/model两层架构，函数式风格
  - 按业务modules划分架构
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

- https://github.com/nicgirault/express-crud-router /113Star/MIT/202309/ts/无db
  - Expose resource CRUD routes for Express & Sequelize. 
  - Compatible with React Admin Simple Rest Data Provider. 
  - The lib is ORM agnostic
  - https://github.com/lalalilo/express-crud-router-sequelize-v6-connector /202308/ts
  - https://github.com/nicgirault/ra-toolkit /202309/ts
    - Additional react-admin components & hooks

- https://github.com/MyungWanPark/shopping-mall-backend /202303/ts/inactive
  - https://github.com/MyungWanPark/shopping-mall-frontend /202303/ts/inactive
  - https://shoppingmall-myungwan.netlify.app/
  - 后端express、sequelize、mysql、jwt
  - 前端依赖react、mui、ApexCharts、axios
  - State Management: Context API
  - 支持注册登录jwt、购物车、简单销售仪表板、搜索

- https://github.com/feathersjs-ecosystem/feathers-sequelize /202306/ts
  - A Feathers service adapter for the Sequelize ORM. 
  - Supporting MySQL, MariaDB, Postgres, SQLite, and SQL Server

- https://github.com/tomjschuster/sequelize-ui /BSD/202402/ts
  - https://sequelizeui.app/
  - a Sequelize ORM code generator, which generates a full Node.js TypeScript project, entirely in the browser
  - Use the schema editor to design your database tables, fields and associations, then preview the Sequelize models and migrations in the code viewer before downloading the project as a zip file or copying code from individual files.
  - Sequelize UI currently only generates TypeScript Sequelize code, not js

- https://github.com/overlookmotel/sequelize-hierarchy /js/201906/inactive
  - Relational databases aren't very good at dealing with nested hierarchies like **folders/categories/Tree**
  - To store a hierarchy in a database, the usual method is to give each record a `ParentID` field which says which is the record one level above it.
  - if you want to retrieve an entire tree/hierarchy structure from the database, it requires multiple queries, recursively getting each level of the hierarchy. 
    - For a big tree structure, this is a lengthy process, and annoying to code.
    - This plugin for Sequelize solves this problem.
  - Requires Sequelize v2.x.x, v3.x.x, v4.x.x or v5.x.x.
  - [Add initial support for Sequelize V6](https://github.com/overlookmotel/sequelize-hierarchy/pull/223)
  - [Sequelize V6](https://github.com/overlookmotel/sequelize-hierarchy/issues/174)
  - 🍴 forks
  - https://github.com/fizure/sequelize-hierarchy /202204/js
    - Add Hierarchy model; support v6
  - https://github.com/astrosoftpro/sequelize-hierarchy-next /202301/js
    - rework: coroutine->await, support sequelize 6
  - https://github.com/SecurityESys/sequelize-hierarchy /202302/js
    - Merge patches for v6 support
  - https://github.com/wizspark/sequelize-hierarchy /202202/js

- https://github.com/grantcarthew/node-mppg /MIT/202112/js/单文件/inactive
  - The Materialized Paths pattern is a simple method to store tree or hierarchical data into a flat data store. 
  - It stores each tree node as a row in a table. 
  - Each row stores the identifiers of the node’s ancestors or path as a string.
  - The pattern also provides more flexibility in working with the path, such as finding nodes by partial paths.

- ddd-forum /1.8kStar/ISC/202306/ts
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

- https://github.com/FujiBilly/partition-sequelize-ts /201909/js
  - 改进 sequelize-typescript 库使其支持 Postgresql 10/11版本的分区表
- https://github.com/sequelize/sequelize-typescript /MIT/202311/ts
  - Decorators and some other features for sequelize (v6).
  - [Any plan to support sequelize 7? _202301](https://github.com/sequelize/sequelize-typescript/issues/1564)
    - Decorators are being implemented directly into the sequelize package as of v7 with same/similar API for compatibility. I think some of the functionality might already been ported in early alpha versions.
  - [Is this repo still maintained? _202210](https://github.com/sequelize/sequelize-typescript/issues/1452)
    - Development on sequelize-typescript is indeed slowing down. 
    - Luckily sequelize-typescript will be merged with sequelize for the next major release (v7) under the NPM package @sequelize/core
    - sequelize-typescript is being sunsetted because we're merging it into core.
  - [Question: Any blog post explaining why someone should use this package instead of just using sequelize? _202304](https://github.com/sequelize/sequelize-typescript/issues/1628)
    - In sequelize v7 these features are part of sequelize itself so there is no need to use sequelize-typescript anymore.

- https://github.com/aidinrs/sql-puzzle /MIT/202306/ts/wip
  - a type-safe, highly composable, and functional query builder for Sequelize, written in TypeScript
  - built around the idea of composing functionalities and code reuse. This is achieved by defining SQL constructs at the lowest possible level and building upon those.
# v7
- https://github.com/bitovi/bitscaffold /202305/ts
  - Scaffold is a web application framework designed to accelerate the development of new, or enhancement of existing, CRUD applications.
  - Create a new Koa + Scaffold 

- https://github.com/tapiwakundi/movies-api /js
  - simple example

- https://github.com/dez126/team-git-saved-backend-main
  - HomeTasktick App Backend

- https://github.com/GuilhermeSantos001/grupomavedigital
  - nestjs + seq@v7

- https://github.com/haandev/eaystate-backend /wip未完成
  - headless real estate cms backend
  - 后端依赖express、2版sequelize、minimist
  - https://github.com/haandev/easystate-dashboard

- https://github.com/fdc1010/cffi-admin-dashboard /202211/js/inactive
  - CFFI Admin Dashboard powered by Argon Dashboard 2 MUI 

- https://github.com/Hemocione/competitions-backend
  - https://github.com/Hemocione/competitions-frontend /js

- https://github.com/craftycodie/Sunrise-Halo3-WebServices
  - A NestJS, Domain-Driven Design reimplementation of Halo 3's web services.
# examples
- https://github.com/demamano/File-Import /202306/ts
  - file import with reactTS , NodeTS, and express , sequelize , mysql
  - upload and view excel sheets
  - 依赖express、sequelize、exceljs、xlsx、mysql2、antd、react-dropzone

- https://github.com/bitovi/hatchify /202403/ts
  - A medium-code React, MUI, and Sequelize, koa
  - Hatchify is a web application framework designed to accelerate the development of CRUD applications. 
  - Hatchify can provide you with a fully functional system straight from a datatype schema.
  - Hatchify’s schemas define your data structure fields and relationships. We share these schemas across our backend and frontend to create database tables, generate REST endpoints, and create React components and data fetchers.

- https://github.com/khaled-badenjki/cilo /202307/js
  - simplifies the build of multi tenant applications by providing a wrapper around sequelize that handles the multi-tenancy for you.
  - The code will bahave the same as if you were building a single tenant application.

- https://github.com/Wind213/sequelize-multi-tenant /201901/js
  - An example of shared database schema isolated multi-tenant implementation with express, nodejs and sequelize.

- https://github.com/AnishLushte07/multi-tenant-application /201909/js
  - Multi tenant application using NodeJs, express, sequelize, mysql.

- https://github.com/PIYoung/node-express-boilerplate-multitenant /MIT/202302/ts
  - node express postgres boilerplate for multitenant(saas)

- https://github.com/westmark/sequelize-multi-tenant-enhancer /201702/js
  - A Proxy based enhancer function which enables schema based multi tenancy in Sequelize.

- https://github.com/rreeves1996/team-manager /202309/ts
  - a MERN app (MySQL database) that functions as a team management app

- https://github.com/kanban-org/kanban-board /202402/js
  - https://www.kanban.live/
  - full-stack Kanban task management app
  - 依赖express、sequelize、pg、react-redux、formik、react-beautiful-dnd

- https://github.com/fnfacun/Koa_trello /202005/ts
  - 后端 - trello 团队协作工具
  - 模仿 trello 团队协作工具 首页是用户面板
  - koa-static-cache, sequelize-typescript

- https://github.com/lukasbals/scrumboard /202305/ts
  - The simplest task tracking tool for dev teams.
  - Next.js, Socket.io, React-DnD, MobX, Sequelize

- https://github.com/yuedun/issue-tracking-system /202005/ts/inactive
  - 基于Koa框架，layui，Sequelize.js5.x版本，使用TypeScript开发的事务跟踪系统

- https://github.com/pawelmalak/flame /MIT/202307/ts/inactive
  - Flame is self-hosted startpage for your server. inspired (heavily) by SUI.
  - Easily manage your apps and bookmarks with built-in editors.
  - Sequelize ORM + SQLite
  - Redux + react

- https://github.com/raphaelalmeidamartins/fullstack-bank /202309/ts
  - Digital wallet full stack application developed with Next.js and Node.js

- https://github.com/juravlevdima/PERN-chat /202212/ts/inactive
  - https://pern-chat.onrender.com/
  - Chat made with PERN Stack & Socket. IO
  - React | React Router | Redux Toolkit
  - Real-time chat using web-sockets

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

- https://github.com/adarshaacharya/CsOverflow /MIT/202106/ts
  - Q/A forum for Computer Science and Engineering students
  - Token based secured authentication system
  - Feature enriched Quill Text Editor
  - Frontend : Typescript, React.js, Redux
  - Backend : Express, Sequelize

- https://github.com/liadber/together /202401/ts/angular
  - a basic social network designed for entrepreneurs. 
  - Users can create profiles, share projects, 

- https://github.com/GeneralBots/BotServer /AGPLv3/202503/ts
  - https://gb.pragmatismo.com.br/
  - Bot Server accelerates the process of developing a bot. It provisions all code base, resources and deployment to the cloud, and gives you templates you can choose from whenever you need a new bot. 
  - The server has a database and service backend allowing you to further modify your bot package directly by downloading a zip file, editing and uploading it back to the server (deploying process) with no code

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

- https://github.com/viclafouch/meme-studio /202401/ts
  - https://www.meme-studio.io/
  - creating and sharing "internet memes"
  - I do not save your meme in our database, so make sure you export your work.

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

- https://github.com/marcobiedermann/url-shortener /202205/ts
  - Simple URL Shortener
  - 依赖express、sequelize6
  - 未实现认证

- https://github.com/Maxinum/WareHouseBot /202308/ts
  - Telegram bot for keeping records of deliveries and sales

- https://github.com/danirod/djs-tagbag /202304/ts
  - A simple key-value storage for persisting tags into your Discord.js bots.

- https://github.com/jihunhong/VanillaChart /202210/ts
  - CherryChart BACK-END (express, typescript)
  - https://github.com/jihunhong/CherryChart-Client /202210/js
# starter
- https://github.com/sequelize/sequelize-sscce /202402/ts
  - Base repository for creating and sharing Sequelize SSCCEs
  - Use this repository to create an SSCCE for your issue
  - Short, Self Contained, Correct (Compilable), Example

- https://github.com/anthonybudd/Express-ts-API-Template /MIT/202407/ts
  - Production-ready minimal REST API boilerplate using Express.js, Sequelize and MySQL.
  - Auth using JWT's with Passport.js
  - production-ready OpenApiSpec.yml & Kubernetes files
  - designed to work with AnthonyBudd/Vuetify-SPA-Template
  - https://github.com/anthonybudd/express-api-boilerplate /js旧版
  - https://github.com/anthonybudd/Vuetify3-SaaS-Template /202406/vue3/js

- https://github.com/TonyMckes/conduit-realworld-example-app /MIT/202303/js/inactive/be+fe/依赖少
  - https://conduit-realworld-example-app.fly.dev/
  - created to demonstrate a fully fledged fullstack application 
  - built with React, Express.js, Sequelize, PostgreSQL
  - 前端依赖axios、react-paginate、markdown-to-jsx，不依赖第三方状态管理
  - 后端依赖express、jsonwebtoken、jsonwebtoken

- https://github.com/cirosantilli/node-express-sequelize-nextjs-realworld-example-app /202208/ts
  - Node.js + Express.js + Sequelize + SQLite/PostgreSQL + Next.js fullstack static/SSG/ISG Example Realworld App
  - https://github.com/cirosantilli/node-express-sequelize-realworld-example-app /202106/js

- https://github.com/chojs23/realword-express-sequelize /202303/js
  - sequelize ^6.26.0
- https://github.com/Varun-Hegde/Conduit_NodeJS /202105/js
  - Express and NodeJS based backend implementation of the RealWorld API Spec.
  - MySQL + Sequelize

- https://github.com/joovitor12/northwind-node /202210/ts/js
  - northwind-node, northwind-react

- https://github.com/MrsLecter/Traders /202210/ts/ejs
  - Creating a database from existing tables, queries to the database
  - Express + PostgreSQL + Sequelize + Bootstrap

- https://github.com/ljlm0402/typescript-express-starter /202311/ts/typedi
  - Express RESTful API Boilerplate Using TypeScript, 可选的多模版项目
  - ✨ 支持Mongoose/Sequelize/TypeORM/Prisma/Knex/MikroORM/GraphQL
  - 采用controller/service/model三层架构，class风格，依赖注入，少量使用装饰器

- https://github.com/Thre4dripper/NodeTs-Express-Service-Based-Template /MIT/202401/ts
  - configurable Node.js, Express, and TypeScript server template with a service-based architecture 
  - 采用controller/service/repository/model四层架构，class风格，可按业务modules划分架构
  - Sequelize/Mongoose
  - 依赖axios、express、jsonwebtoken、swagger-ui-express
  - Database Compatibility: Interact with MySQL, PostgreSQL, MariaDB, Sqlite, MSSql, MongoDB

- https://github.com/sharafdin/yonode /MIT/202403/ts/js
  - https://docs.yonode.org/
  - The Node.js Toolkit for Rapid Development
  - Yonode templates are available for both JavaScript and TypeScript

- https://github.com/Thre4dripper/node-server-init /202401/ts/偏向cli
  - initialize Node.js server projects with customizable configurations
  - 采用controller/service/repository/model四层架构，可按业务modules划分架构
  - Sequelize & Mongoose: Integrations with Sequelize for SQL database operations and Mongoose for MongoDB.
  - Built-in validations for incoming request payloads.

- https://github.com/owliehq/neatsio /MIT/202210/ts
  - Generate REST API from your Sequelize/Mongoose models
  - NOT ALL METHODS ARE YET IMPLEMENTED WITH MONGOOSE
  - To use Neatsio, you have to create Models using Sequelize or Mongoose. Planned for the next project iterations, Neatsio will be interoperable with TypeORM, Bookshelf or Objection.js
  - Focus on models and business logic, the lib generate automatically endpoints based on mongoose/sequelize schemas. 
  - This lib is opinionated, some features or development orientation are due to personal choices
  - Support of query paramaters to handle filtering, pagination, sorting, and sub-populating
  - https://github.com/owliehq/buboJS /202303/ts/inactive
    - a library to build quickly and efficiently a Rest API
    - Integrated role management tools, For the rights, the library `role-acl` is used
    - Middlewares Sequelize: @SequelizeAttributes
  - https://github.com/owliehq/models /MIT/202002/ts
    - Organize & share your business logic ressources onto ODM style objects

- https://github.com/codespede/pwoli /BSD/202303/ts
  - https://codespede.github.io/pwoli/rest-api
  - https://codespede.github.io/pwoli/input-forms
  - a NodeJS/TypeScript framework written in TypeScript which can work independently on a raw NodeJS/TypeScript environment OR, in co-ordination with any other frameworks or libraries like Express.js.
  - 依赖ejs、fs-extra、typedoc
  - 类似ssr全栈框架，不是orm
  - 示例是直接调用model的方法
  - Pwoli can connect to any kind of ORMs by implementing their corresponding ORM Adapters and works with Sequelize and Mongoose 
  - For any other DB/ORM support, an ORM Adapter implementing `IORMAdapter` has to be implemented. 
  - Fully flexible and extensible - thanks to the OOP based architecture
  - Frontend widgets like ActiveForm, GridView, ListView for SSR(Server Side HTML Rendering) applications.
  - Works on both raw NodeJS and TypeScript applications.
  - 💡 Pwoli is inspired from PHP's Yii framework.
  - https://github.com/codespede/pwoli-express-typescript-sample /202211/ts/mongo
  - https://github.com/codespede/pwoli-nodejs-typescript-sample /202211/ts/sequelize

- https://github.com/mikemajesty/node-generic-repositories /202402/ts
  - TypeORM | Sequelize Typescript | Mongoose
  - 简单示例，代码混乱

- https://github.com/SamuelMarks/restify-orm-scaffold /MIT/202402/ts
  - Simple baseline scaffold to get you started using TypeORM and/or Sequelize and/or Waterline on restify with TypeScript.
  - 无架构，仅实现了user/auth api
  - 🐳 支持 Docker / Podman， k8s

- https://github.com/felipecal/Api-Sequelize /MIT/202402/ts/提交多
  - This is a simple CRUD api in TypeScript, sequelize, aws rds or docker database.
  - 采用controller/service/model三层架构，class风格
  - 依赖express、jsonwebtoken、sequelize、swagger-ui-express、bcrypt

- https://github.com/kazi-naimul/typescript-express-mysql-boilerplate /202312/ts
  - A boilerplate for any enterprise rest api or service with Node.js -Typescript, Express and Sequelize ORM for mysql, postgresql or others.
  - 采用controller/service/dao/model四层架构，class风格，无装饰器
  - service/dao/model都采用interface+impl的实现
  - 实现了associate
  - 依赖express、jsonwebtoken、passport-jwt、redis
  - Authentication and authorization: using passport
  - Job scheduler: with Node-cron

- https://github.com/weareopensource/Typescript /202110/ts/inactive
  - https://node.weareopensource.me/api/tasks
  - https://vue.weareopensource.me/
  - TypeScript - Boilerplate Back: Express, Jwt, Mongo, Sequelize (Draft)
  - 采用controller/service/repository/model四层架构，函数式风格，按业务modules划分架构
  - routes/policies无需手动定义，server init时会自动读取目录并注册routes
  - 支持mongoose/sequelize, model使用joi校验
  - 依赖express、jsonwebtoken、passport-jwt
  - https://github.com/weareopensource/Node /202401/js
    - Repository and Services Pattern
  - https://github.com/weareopensource/Vue /202401/js/vue
    - Boilerplate Front : Vue 3, Vuex, Vuetify 3, JWT, Jest

- https://github.com/mcaligares/express-typescript /202310/ts
  - Express project with Typescript support ready to start coding
  - 采用controller/service/repository/model四层架构，函数式风格
  - model基于接口实现
  - 依赖express、jsonwebtoken、sequelize-typescript、crypto-js

- https://github.com/nabadeep25/typescript-node-sequelize-boilerplate /202310/ts
  - ✨ 采用controller/service/model三层架构, 函数式风格
  - 依赖express、jsonwebtoken、joi、swagger-ui-express

- https://github.com/Haniismail/sequelize-starter /MIT/202306/ts/较乱
  - A starter for a node.js and sequelize app that includes an MVC architecture 
  - 采用controller/repository/model三层架构, 函数式风格
  - 实现了associate
  - 依赖express、jsonwebtoken、swagger-ui-express

- https://github.com/osamaAbdullah/express_template /202402/ts/结构合理
  - 依赖sequelize7、express-session、passport-local、vinejs(validate)
  - 采用controller/model两层架构，函数式风格
  - 未实现jwt

- https://github.com/mksglu/sequelize-ts /201905/ts
  - Starter Kit: Node JS, PostgreSQL, Express JS, TypeScript, Sequelize, TDD, Docker
  - 采用service/model两层架构，函数式风格
  - 实现了associate

- https://github.com/Oivlisfriend/sequelize_typescript_nodejs_mysql /202310/ts/过于简单
  - 采用controller/model两层架构，函数式风格

- https://github.com/nmanikiran/rest-api-node-typescript /202106/ts/inactive
  - simple REST API with node and express with typescript
  - 采用controller/repository/model三层架构，class风格
  - 架构典型，可通过api访问数据 http://localhost:3009/api/lessons
  - 未实现jwt

- https://github.com/richLpf/express-ts-swagger-service /202308/ts
  - 基于Typescript + Express + Sequelize + Swagger + PM2 + Docker 搭建的后端服务
  - 采用controller/repository/model三层架构，class风格
  - 依赖express、jsonwebtoken、swagger-ui-express
- https://github.com/mrdulin/node-sequelize-examples /202106/ts
  - Template based on Node.js, Express, TypeScript
  - 采用controller/repository/model三层架构，class风格
  - 依赖express、bcrypt、jsonwebtoken、swagger-ui-express

- https://github.com/albinojunior/node-crudapi-ts /202012/ts/inactive
  - CRUD boilerplate for create Node Restful API's with Express Framework and Sequelize ORM 
  - 采用controller/service/model三层架构，class风格, 按业务modules划分架构
  - 抽象出了通用的CrudService，不与model绑定
  - class UserService extends CrudService
  - 依赖express、jsonwebtoken、sequelize

- https://github.com/lhenriquegomescamilo/template-server-nodejs /202004/ts
  - a base template for Node.js Rest API applications
  - 采用controller/service/model三层架构, class风格, 按业务modules划分架构
  - 依赖express、jwt-simple、passport-jwt、sequelize
- https://github.com/sudhakar-jonnakuti/express-sequelize /202312/ts
  - express + typescript + sequelize
  - 采用controller/service/model三层架构, class风格, 按业务modules划分架构

- https://github.com/sonbyungjun/cucu /202008/ts/typedi
  - TypeScript Express Starter With CRUD Generator
  - 采用controller/service/model三层架构, class风格, 装饰器, 按业务modules划分架构

- https://github.com/yosua-kristianto/typescript-expressjs /202212/ts
  - Turns out I made a boilerplate code through this repository.
  - 采用controller/repository/model三层架构，class风格
  - repository采用接口+impl

- https://github.com/kushalshit27/nodejs-sequelize-typeScript /202108/ts
  - build your own API with Node.js + Express+ Sequelize + TypeScript
  - 两层架构, class风格

- https://github.com/Mohammad-Faisal/professional-express-sequelize-docker-boilerplate /MIT/202205/ts/typedi/inactive
  - ExpressJS Boilerplate with Typescrip+Docker+Sequelize integration
  - 采用controller/service/repository/model四层架构，class风格，多装饰器

- https://github.com/faid-terence/SequelizePostgresExpressMagic /202402/ts
  - Sequelize + pg
  - Utilizes JWT for secure authentication.

- https://github.com/HUNTER9881/Sqlite_Express_Typescript /202301/ts
  - [Node.js + TypeScript + MongoDB: JWT Authentication](https://codevoweb.com/node-typescript-mongodb-jwt-authentication/)

- https://github.com/salino3/node-typescript /202402/ts
  - front + back

- https://github.com/ImRLopezAG/Ts-Api-Template /202311/ts/tsyringe
  - This is an API template made with express and typescript, to speed up your development, it contains repositories and generic services for the typical CRUD actions, based on a Sequelize model, we use it for data persistence
  - 采用controller/service/model三层架构，依赖注入，多装饰器
  - 依赖tsyringe、express、jsonwebtoken、sequelize6、swagger-ui-express

- https://github.com/Murilo-MRS/nodejs-ts-boilerplate /202401/ts
  - Boilerplate NODEJS TYPESCRIPT SEQUELIZE MYSQL
  - 采用controller/service/model三层架构, 多占位符文件，跑不起来
- https://github.com/juananmuxed/template-ts-api /202312/ts
  - 采用controller/model两层架构，class风格

- https://github.com/Faeshal/nodets-layered-architecture-sequelize /202311/ts/inactive
  - Typescript Node REST API boilerplate using service layered architecture + sequelize
  - 3 main layers: Controller, Service, Repository
  - 依赖express-paginate、sequelize6
  - 未使用jwt，未实现认证

- https://github.com/SystangoTechnologies/koach-typescript /202203/ts/inactive
  - Production ready boilerplate for building APIs in Typescript(3.4) with koa2, and using SQL database and http/2 as the communication protocol.
  - 采用controller/service/entity/model四层架构, class风格

- https://github.com/SourceSprint/ts-webpack-sequelize-template /202308/ts/过于简单
  - NodeJS Server Template with support for sequelize and webpack

- https://github.com/StefanNedelchev/express-sequelize-ts-example /202401/ts/过于简单
  - A basic example of using express with sessions, sequelize and typescript.
  - basic NodeJS application for web API microservices that uses express with express-session, sequelize-typescript to connect to a SQL database and authenticate users.
  - 🧐 The app is written following the proper OOP approach using TypeScript classes with decorators
  - If the registration/login was successful, the user should be instantly logged in with a session. 

- https://github.com/teo-garcia/fastify-template-sequelize
  - using Fastify with Sequelize.

- https://github.com/designly1/nextjs14-auth-sequelize-starter /202402/ts
  - starter app with Sequelize ORM and JWT authentication

- https://github.com/saulotarsobc/electronjs-with-nextjs /202401/ts
  - ElectronJS application with NextJS and TypeScript

- https://github.com/sequelize/express-example /202203/js/inactive
  - A proposal for the usage of Sequelize within an Express. JS application.

- https://github.com/saumya04/Nodular /201904/js/inactive
  - A Node JS structure following some of the most best practices from other top frameworks - Built on the top of Express JS
  - 依赖sequelize5、jsonwebtoken、express

- https://github.com/tiagospeckart/geekscript-backend /202305/ts/inactive
  - https://github.com/GabrielGameDev/geek-script-front
  - This repository is the final project for the Gama Academy Web Development course
  - 实现了登录，未实现注册

- https://github.com/Billeclipse/Supercharging-Node.js-Applications-with-Sequelize-Project /202311/js
  - My version of a learning project on an educational course/book from Packt named "Supercharging Node.js Applications with Sequelize"

- https://github.com/bruzt/exemplo-ecommerce /202112/ts/inactive
  - 函数式风格
  - 业务代码比较乱
# auth
- resources
  - [@auth/sequelize-adapter | Auth.js](https://authjs.dev/reference/adapter/sequelize)

- https://github.com/diegomottadev/auth-base-app /202402/ts
  - https://documenter.getpostman.com/view/21594008/2s93z873e9
  - This repository contain a REST API project for creating users, user roles, and user authentication using Node.js, Express.js, and Sequelize with TypeScript.
  - To access protected endpoints, you need to include an authentication token in the request headers. 
  - https://github.com/diegomottadev/auth-base-view /202402/js
    - Frontend utilizing React with JavaScript that incorporates user, role, and permission logic crucial for orchestrating flow within any application interface.

- https://github.com/rahulthackkar/nodejs-mysql-jwt-sequelize /202207/js/ejs
  - Node JS + Express + User authentication using JWT + Sequelize + Jest + Docker

- https://github.com/PROTEK-ID/mern-auth-template /202309/ts/fe+be
  - MERN Stack Authentication using Sequelize (MySQL as dialect) for backend template.

- https://github.com/bezkoder/node-js-express-login-example /202402/js/流程图很清晰
  - Express Login example (with Registration) using JWT, Cookies, MySQL database
  - [Node.js Express: Login and Registration example with JWT](https://www.bezkoder.com/node-js-express-login-example/)

- https://github.com/cornflourblue/node-mysql-registration-login-api /MIT/202008/js
  - Node.js + MySQL API for User Management, Authentication and Registration
  - 依赖sequelize6、express-jwt、express-jwt、bcryptjs
  - https://github.com/cornflourblue/react-redux-registration-login-example /202008/js
  - https://github.com/cornflourblue/react-redux-jwt-authentication-example /202006/js

- https://github.com/kylewhittemore/react-sequelize-template /202105/js
  - Full-stack react with passport js local strategy for authentication
# utils
- https://github.com/mujz/pg-search-sequelize /201711/js/inactive
  - Postgres full-text search in Node.js and Sequelize.
  - This library makes use of Postgres full-text search and Materialized Views to run fast, powerful, and simple search queries
  - https://github.com/mujz/pg-search-sequelize-example /js/inactive
    - An example use case of pg-search-sequelize

- https://github.com/tylerjpeterson/sequelize-history /201912/js
  - This module will setup automatic revision tracking for any Sequelize model. 
  - This is effectively a re-write of sequelize-temporal
- https://github.com/nielsgl/sequelize-paper-trail /201909/js
  - Sequelize plugin for tracking revision history of model instances.

- https://github.com/andyforever/sequelizer /202211/js
  - A GUI Desktop App for export sequelize models from database automatically.

- https://github.com/sequelize/sequelize-auto /202112/ts
  - Automatically generate models for SequelizeJS via the command line.
- https://github.com/spinlud/sequelize-typescript-generator /202310/ts
  - Automatically generates typescript models compatible with sequelize-typescript library directly from your source database.
- https://github.com/zcong1993/auto-sequelize-typescript /202111/ts
  - auto generate model files from exists db schemas

- https://github.com/TeamMaestro/sequelize-common /202308/ts
  - A common set of models and functions that we use throughout most of our Sequelize projects

- https://github.com/doralteres/express-sequelize-autocrud /MIT/202402/ts
  - library designed to simplify the creation of CRUD (Create, Read, Update, Delete) routes for your Sequelize models in an Express.js
  - Middleware Support: Integrate custom middleware functions with generated routes to extend functionality.
  - Transaction Support: Create, Update and Delete routes runs inside sequelize transaction 

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

- https://github.com/blankstar85/sequelize-central-log /MIT/202309/ts
  - Maintain Sequelize Model change history in a central table. 
  - This is highly configurable and supports composite primary keys ( up to 3 for now). 
  - Written in Typescript and provides typing.

- https://github.com/BibbyChung/sequelize-adapter /202107/ts
  - Use Unit Of Wrok pattern to wrap sequelize up and make sequelize easy to use.
  - use the singleton pattern to design
  - use the unit of work pattern to wrap sequelize
  - use transaction feature to create, update, delete by default

- https://github.com/pilagod/uow-sequelize /MIT/201811/ts/inactive
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

- https://github.com/sugarandmagic/sequelize-mv-support /MIT/202211/ts/inactive
  - This package adds support for Views and Materialized Views in Sequelize.
  - NOTE: Currently it's only supported in PostgreSQL.
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

- https://github.com/QuaNode/beamjs /MIT/202401/js
  - Enterprise full stack web development framework (Backend-JS - ExpressJS - AngularJS - MongoDB)
  - BeamJS is built above Backend-JS to provide data controllers for SQL and No-SQL databases. It also includes file system controllers that work on a local file system or cloud storage.
  - These data controllers are abstract adapters above ODM/ORM patterns of MongooseJS and SequelizeJS. These data controllers are abstract adapters above ODM/ORM patterns of MongooseJS and SequelizeJS.
  - supports CQRS architecture through mixed model definitions over different DBs.
  - supports Horizontal/DB multi-tenancy by automatically handling multi-DB connection mapping.
  - https://github.com/quaNode/Backend-JS /js
    - a layer built above expressjs and socket.io to enable behaviours framework for nodejs applications.

- https://github.com/luizcalaca/ddd-typescript-sequelize-node-api /202209/ts/inactive
  - Domain Drive Design + Clean Architecture + Node.js + Typescript + Sequelize

- https://github.com/joshuaalpuerto/node-ddd-boilerplate /201905/js/inactive
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
# cms
- https://github.com/PelagicCreatures/marlin /202204/js/pug/inactive
  - An ExpressJS CMS for sites with Sequelize db backends
  - Data model driven database (sequelize)
  - Admin data editing UI suite automatically built from data model
  - ACL access control on tables by user role (superuser, admin, etc.)
  - https://github.com/PelagicCreatures/marlin-app /202109/js/pug
    - a boilerplate app that includes many common functions of a web site/app featuring registered users. 
    - we use HIJAX to load pages after the initial load. 
    - 【DOM编程艺术】 Hijax---渐进增强地使用Ajax 
    - 按照老传统，让表单把整个页面都提交到服务器，然后服务器再发回来一个包含反馈的新页面，所有处理操作都在服务器上完成
    - 为了给这个登录表单添加AJAX功能，就需要拦截提交表单的请求,让XMLHttpRequest请求来代为发送

- https://github.com/duhdugg/preaction-cms /MIT/202303/js/inactive
  - https://duhdugg.github.io/preaction-cms/
  - a barebones, extensible Content Management System built on top of simple JavaScript libraries. 
  - When starting the server, lib/ext scans the `ext` directory for other directories containing an `index.js` file
  - By default, Preaction CMS only supports 5 block types: Carousel, Content, Iframe, Navigation, and Spacer. You can add more block types by putting them in the `blockExtensions` object in `src/ext/index.js`.
  - You should run Preaction CMS behind a reverse-proxy such as Nginx.

- https://github.com/ezy/seedpress-cms /201807/js
  - A headless CMS built in Express for PostgresQL using Sequelize. 
  - Generally follows the Wordpress post and term schema.

- https://github.com/TaleLin/lin-cms-koa /202111/js
  - 使用Node. JS KOA构建的CMS开发框架
  - 是林间有风团队经过大量项目实践所提炼出的一套内容管理系统框架。
  - https://github.com/TaleLin/lin-cms-vue /202401/js/vue

- https://github.com/apstanisic/zmaj /202310/ts
  - https://zmaj.vercel.app/
  - a headless CMS with RESTful API for your database and admin panel to easily manage your data
  - Built on top of React and React Admin for admin panel, and NestJS and Sequelize for API.
  - 依赖nestjs-passport、knex、sequelize
# testing
- https://github.com/causalhq/sequelize-interview
  - Make sure to complete the entire setup process below, and can run the final test command

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

- https://github.com/hasinoorit/sequelizemm /202311/ts
  - a command-line interface tool that simplifies the creation and management of migrations for your Sequelize project. 
  - This tool utilizes the Query Interface provided by Sequelize to create migration files that can be used to modify your database schema.
# more
- https://github.com/metacollective9/sequelize-serverless-poc
  - Sequelize ORM (using typescript) with lambda function using the serverless framework.
  - https://github.com/dherault/serverless-offline
    - Emulate AWS λ and API Gateway locally when developing your Serverless project
