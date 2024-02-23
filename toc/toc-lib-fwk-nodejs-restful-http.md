---
title: toc-lib-fwk-nodejs-restful-http
tags: [ajax, framework, http, restful, toc]
created: 2020-12-13T09:14:01.137Z
modified: 2022-12-19T01:51:01.389Z
---

# toc-lib-fwk-nodejs-restful-http

# guide

- mock-api
  - [fetch-mock vs json-server vs nock](https://www.npmtrends.com/fetch-mock-vs-json-server-vs-nock)

- solutions
  - [Arrow Flight RPC — Apache Arrow](https://arrow.apache.org/docs/format/Flight.html)
# api-spec
- https://github.com/json-api/json-api
  - https://jsonapi.org/
  - A SPECIFICATION FOR BUILDING APIS IN JSON
  - [OpenAPI 3.0 spec that conforms to JSON: API - JSON API](https://discuss.jsonapi.org/t/openapi-3-0-spec-that-conforms-to-json-api/1803)

- https://github.com/osu-mist/jsonapi-openapi-generator
  - A script for generating an OpenAPI document adhering to the JSON: API specification.

- https://github.com/OData/odata.net
  - OData . NET Libraries project includes the implementation of core functionalities of OData protocol on the . NET platform, including URI parsing, request and response reading and writing, Entity Data Model (EDM) building
  - [OData简介 - 知乎](https://zhuanlan.zhihu.com/p/56639241)
  - [Why not OData? | Documentation](https://docs.servicestack.net/why-not-odata)
  - [Choosing OData or REST ? Detailed Analysis - Stack Overflow](https://stackoverflow.com/questions/59967080/choosing-odata-or-rest-detailed-analysis)
    - OData is great when there is a single or highly coupled data source where there are very clear relationships between the resources.
  - https://github.com/zackyang000/node-odata

- https://github.com/dxc-technology/halstack-client
  - Our Javascript SDK for abstracting the consumption and creation of hypermedia API resources expressed in **HAL**
  - Halstack Client for JavaScript enables developers to easily work with hypermedia-based APIs in a declarative manner. 
# rest-api
- https://github.com/heerey525/express_mongoDB /202203/js
  - https://heerey525.github.io/express_mongoDB/apidoc/
  - express+mongoDB的一套后台管理系统
  - 功能点：邮箱验证、注册、登录、jwt验证、用户管理、权限列表、角色列表、商品的增删改查、国际化管理（增删改查、批量添加、excel导入导出、导出js文件）、图片上传等
  - 依赖mongoose
  - https://github.com/heerey525/express_mongodb_web /202012/js/vue

- https://github.com/restify/node-restify /202211/js
  - 依赖mime、qs、http-signature、send(for streaming files)
  - restify is a framework, utilizing connect style middleware for building REST APIs.
  - There are actually three separate clients shipped in restify: JsonClient, StringClient, HttpClient
  - One of the coolest features of restify is that it automatically creates DTrace probes for you whenever you add a new route/handler.

- https://github.com/typicode/json-server /202211/js
  - Get a full fake REST API with zero coding in less than 30 seconds (seriously)

- https://github.com/thiagobustamante/typescript-rest /202106/ts
  - annotation-based expressjs extension for typescript.
  - typescript-rest、typescript-ioc、typescript-rest-ioc

- https://github.com/PostgREST/postgrest
  - https://postgrest.org/
  - PostgREST serves a fully RESTful API from any existing PostgreSQL database. 
  - It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.
  - 可直接将 PostgreSQL 数据库发布成 REST API，甚至有基于此库的 SaaS 服务如 supabase 可提供类 Google Firebase 的功能。

- https://github.com/developit/express-es6-rest-api
  - boilerplate for building REST APIs with ES6 and Express.

- https://github.com/albingroen/typescript-express-server
  - express server template with Typescript

- https://github.com/dalenguyen/rest-api-node-typescript
  - Building RESTful Web APIs with Node.js, Express, MongoDB and TypeScript
- https://github.com/nerdeveloper/hackathon-starter-kit
  - A Node-Typescript/Express Boilerplate with Authentication(Local, Github, Facebook, Twitter, Google, LinkedIn, Dropbox, Slack, Discord), Authorization, and CRUD functionality + PWA Support!

- https://github.com/aichbauer/express-rest-api-boilerplate
  - Express REST API with JWT Authentication and support for sqlite, mysql, and postgresql
  - routes mapping via express-routes-mapper

- https://github.com/talyssonoc/node-api-boilerplate /ts
  - DDD/Clean Architecture inspired boilerplate for Node web APIs
  - Modules are the building pieces of an application built with this boilerplate. You can either encapsulate an integration or a feature using a module 
  - Both the boot and stopping processes are defined as a sequence of lifecycle events.

- https://github.com/hiteshchoudhary/apihub /MIT/202401/js
  - https://freeapi.app/
  - Your own API Hub to learn and master API interaction.
  - We are trying to build a single source API hub that can be used to learn api handling in any programming language.
  - our API hub offers custom endpoints that provide a hands-on experience in handling API responses.
  - our API hub also provides advanced APIs to challenge and stretch your skills.
  - Our open-source project is currently hosted on a remote server, where we are forced to reset the entire server, including the file system and MongoDB database, every 2 hours to avoid incurring additional costs.
# crud/admin
- api-server-nodejs /178Star/MIT/202212/ts
  - https://github.com/app-generator/api-server-nodejs
  - Express Starter with JWT authentication, and SQLite persistance - Provided by AppSeed App Generator. 
  - 依赖Express, SQLite, TypeORM, passport-jwt
  - Authentication Flow uses json web tokens via Passport library - passport-jwt strategy.
  - TypeScript, Joy for validation
  - https://github.com/app-generator/api-server-nodejs-demo
- api-server-nodejs-mongo /11Star/MIT/202212/ts/代码简单
  - https://github.com/app-generator/api-server-nodejs-mongo
  - 典型的dashboard的后端示例
  - 依赖express、mongoose、passport-jwt
  - Can be used with other React Starters for a complete Full-Stack experience
- https://github.com/app-generator/sample-docker-nodejs-react
  - docker compose up --build 

- https://github.com/sunburst89757/react-admin
  - https://github.com/sunburst89757/react-admin-backend
  - http://47.98.204.143:3000/login
  - 后端项目，使用的模板是koa-ts-template
  - redux-toolkit: 全局状态管理工具
  - 使用 access_token refresh_token 进行无感刷新
  - Antd 组件库
- https://github.com/heerey525/express_mongoDB /202203/js
  - https://heerey525.github.io/express_mongoDB/apidoc/
  - express+mongoDB的一套后台管理系统
  - 功能点：邮箱验证、注册、登录、jwt验证、用户管理、权限列表、角色列表、商品的增删改查、国际化管理（增删改查、批量添加、excel导入导出、导出js文件）、图片上传等
  - 依赖mongoose
  - https://github.com/heerey525/express_mongodb_web /202012/js/vue

- fast-crud /512Star/MIT/202311/ts/vue
  - https://github.com/fast-crud/fast-crud
  - http://fast-crud.docmirror.cn/
  - 面向配置的crud开发框架，快速开发crud功能，可作为低代码平台的基础框架
  - 可以直接使用示例中的fs-admin，特点是简单
  - 也可以采用其他的admin开源项目，然后集成fast-crud
  - 基于目前市面上开源的高星admin项目fork，集成fast-crud，Antdv 3x 、Element-Plus 、NaiveUI 三选一
    - https://github.com/fast-crud/fs-admin-antdv /vue

- https://github.com/idurar/mern-admin /MIT/202311/js
  - https://www.idurarapp.com/demo-mern-admin/
  - MERN Stack Antd Admin Dashboard CRUD Auth
  - App Built on top of this Starter project IDURAR ERP/CRM
  - https://github.com/idurar/idurar-erp-crm /FairCode/202401/js
    - ERP / CRM | Node.js React.js
    - Alternative to SalesForce | Node Js React AntD MERN

- adminjs /6.2kStar/MIT/202211/ts/仅参考db设计
  - https://github.com/SoftwareBrothers/adminjs
  - https://adminjs-demo.herokuapp.com/
  - AdminJS is an automatic admin interface that can be plugged into your application. 
  - 亮点是可切换数据库(mongo/pg/mysql)、后端框架(express/hapi/nest)
  - 自动生成简单的crud界面，前后端打包被自动化了，不利于自定义打包
  - You, as a developer, provide database models (like posts, comments, stores, products or whatever else your application uses), and AdminJS generates UI which allows you (or other trusted users) to manage content.
  - It uses (for example) Hapi.js+mongoose for rendering a couple of REST routes and mongoose as the connector to the database.
  - Inspired by: django admin, rails admin and active admin.
  - By default, AdminJS is equipped with a powerful `quill` editor, which makes it a perfect tool as a Content Management System
  - https://github.com/SoftwareBrothers/adminjs-example-app
    - Example application using adminjs
  - https://github.com/SoftwareBrothers/adminjs-dev
  - https://github.com/SoftwareBrothers/adminjs-design-system

- https://github.com/creativetimofficial/argon-dashboard-react-nodejs /202101/js
  - 开源了dashboard的react前端和后端
  - https://github.com/creativetimofficial/argon-dashboard-nodejs
  - https://github.com/creativetimofficial/material-dashboard-react-nodejs

- https://github.com/thomas4019/expressa /202210/js/vue
  - makes it easy to create basic APIs by using JSON schema
  - django-like admin interface for creating collection-REST endpoints and managing permissions

- https://github.com/AndhikaBukh/Storify /202208/ts/starter
  - http://storify-six.vercel.app/
  - a social media app built with React. 
  - We are building a platform for users to share their stories and connect with others.
  - 前端依赖react-router、react  /ts
  - 后端依赖express、mongoose    /js

- https://github.com/simov/express-admin /201409/js
  - https://simov.github.io/express-admin/
  - a NodeJS tool for easy creation of user friendly administrative interface for MySQL, MariaDB, SQLite and PostgreSQL databases.
  - It's built with: Hogan.js (mustache.js), Express, mysql and Bootstrap.
  - https://github.com/simov/express-admin-examples /201407/js

- https://github.com/pratiksh404/adminetic /202309/php/js
  - https://pratikdai404.gitbook.io/adminetic/
  - Admin starter kit with user, role and permission, activity, settings and preference management along with CRUD, ACL, BREAD Permission, Repo Pattern, SuperAdmin Generator
# web-framework
- https://github.com/plantain-00/protocol-first-design-demo
  - API 协议优先，相关数据只需要相对集中地、相对方便地定义一次，其它信息由此派生或生成出来
  - graphql 的一个特点是，用户可以控制需要返回哪些字段，而 RESTful API 一般默认不会实现这个。
  - 这里的实现，不像 graphql 那样需要列出所有需要的字段，而是默认返回所有字段，根据参数中的 ignoredFields，把不需要的字段排除掉。
- https://github.com/plantain-00/protocol-based-web-framework
  - A protocol and code generation based web framework.
  - db支持sqlite、postgres、mongodb
# rest-starter
- https://github.com/criscunas/todo-server
  - Backend API for Todo App built with Node & Express.
  - Data is stored in an empty JSON file.
  - https://github.com/criscunas/todo-client
    - Built with Vue3 and Tailwind CSS
# mock-fetch
- https://github.com/izelnakri/memoria
  - Single JS/TS ORM for frontend, backend & in-memory testing
  - It is a very flexible typeorm-like entity definition API that just use JS classes and decorators to define or generate the schema. 
  - You can choose different adapters and use the same CRUD interface: MemoryAdapter, RESTAdapter or SQLAdapter.
  - The http mock server(@memoria/server) can be run in-browser and node environments, thus allows for running your in-memory test suite in SSR(server-side rendering) environment if it is needed.
# ajax/pjax
- https://github.com/falsandtru/pjax-api
  - https://falsandtru.github.io/pjax-api/
  - The pjax-api provides almost complete original web experience. 
  - Most SPA frameworks and pjax libraries lack many essential functions to keep the original web experience such as follows.

- https://github.com/hydecorp/push-state /ts
  - hy-push-state is a web component that lets you turn web pages into web apps. 
  - The component dynamically loads new content (formerly known as "ajax") and inserts it into the current page, without causing Flash of White, Flash of Unstyled Content, etc.
  - hy-push-state is similar to pjax and smoothState, but offers a more advanced pre-fetching logic and gives you more control over its internals to enable advanced page transition animations.

- https://github.com/defunkt/jquery-pjax
- pjax = pushState + ajax
  - pjax works by fetching HTML from your server via ajax and replacing the content of a container element on your page with the loaded HTML. 
    - It then updates the current URL in the browser using pushState. 
    - No page resources (JS, CSS) get re-executed or re-applied;
# rest-examples
- https://github.com/taniarascia/node-api-postgres
  - https://blog.logrocket.com/setting-up-a-restful-api-with-node-js-and-postgresql-d96d6fc892d8/
- Create, read, update, delete in a Node.js app with an Express server and Postgres database.

- https://github.com/javieraviles/node-typescript-koa-rest /202105/ts/inactive
  - REST API boilerplate using NodeJS and KOA2, typescript. 
  - Logging and JWT as middlewares.
  - TypeORM with class-validator, SQL CRUD. 
  - Docker included. Swagger docs, actions CI and valuable README

- https://github.com/w3tecch/express-typescript-boilerplate
  - RESTful API with NodeJs & TypeScript 
- https://github.com/contiamo/restful-react
  - declarative way of interacting with RESTful backends, featuring code-generation from Swagger and OpenAPI spec
- https://github.com/kunalkapadia/express-mongoose-es6-rest-api
  - A boilerplate application for building RESTful APIs Microservice in Node.js using express and mongoose
  - ES6 with code coverage and JsonWebToken Authentication

- https://github.com/Melzar/onion-architecture-boilerplate
  - a real life example of Onion Architecture with use of Node.js, Express and Typescript

- https://github.com/parse-community/parse-server
  - API server module for Node/Express
  - an open source backend that can be deployed to any infrastructure that can run Node.js.
- https://github.com/r-spacex/SpaceX-API
  - Open Source REST API for rocket, core, capsule, pad, and launch data
# express-like
- https://github.com/tinyhttp/tinyhttp /ts
  - a modern Express-like web framework 
  - Async middleware support

- https://github.com/hattipjs/hattip /MIT/202402/ts
  - Like Express, but for the future
  - HatTip is a set of JavaScript packages for building HTTP server applications.
  - Modern: Based on current and future web standards (Fetch API & WinterCG).
  - Runs anywhere (Node.js, the Edge, Deno, ...).
  - Modular: Use as much or as little as you need.
  - compose function from the @hattip/compose package can be used to compose multiple handlers into a single one, creating a simple but powerful middleware system.

- https://github.com/honojs/hono /ts/NoDeps
  - https://hono.dev/
  - a small, simple, and ultrafast web framework for the Edges. 
  - It works on any JavaScript runtime: Cloudflare Workers, Fastly Compute@Edge, Deno, Bun, Vercel, Lagon, AWS Lambda, Lambda@Edge, and Node.js.
  - The router RegExpRouter is really fast. Not using linear loops. 
  - Hono has zero dependencies and uses only the Web Standard API.
  - Hono has built-in middleware, custom middleware, and third-party middleware. 

- https://github.com/Actionhero/Actionhero /apache2/202401/ts
  - https://www.actionherojs.com/
  - a realtime multi-transport nodejs API Server with integrated cluster capabilities and delayed tasks
  - The reusable, scalable, and quick node.js API server for stateless and stateful applications
  - The goal of actionhero is to create an easy-to-use toolkit for making reusable & scalable APIs for HTTP, WebSockets

- https://github.com/unjs/h3 /MIT/202312/ts
  - minimal h(ttp) framework built for high performance and portability.
  - Works perfectly in Serverless, Workers, and Node.js
  - Native promise support
  - Super fast route matching using unjs/radix3
  - Compatibility layer with node/connect/express middleware

- https://github.com/unjs/nitro /ts
  - https://nitro.unjs.io/
  - Create web servers that run anywhere. 
  - The open engine powering Nuxt and open to everyone.
  - Nitro provides a built-in storage layer that can abstract filesystem or database or any other data source.
# more
