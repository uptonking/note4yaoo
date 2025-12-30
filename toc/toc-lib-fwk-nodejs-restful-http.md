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

- https://github.com/microsoft/typespec /MIT/202409/java/ts
  - https://typespec.io/
  - TypeSpec is a language for defining cloud service APIs and shapes. 
  - TypeSpec is a highly extensible language with primitives that can describe API shapes common among REST, OpenAPI, gRPC, and other protocols.
  - TypeSpec to OpenAPI 3.0 Example

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

- https://github.com/typicode/json-server /75.2kStar/MIT > FSL/202509/js
  - Get a full fake REST API with zero coding in less than 30 seconds (seriously)
  - [V1 by typicode · Pull Request · typicode/json-server _202401](https://github.com/typicode/json-server/pull/1468/files#diff-c693279643b8cd5d248172d9c22cb7cf4ed163a3c98c8a3f69c2717edd3eacb7)
    - license: MIT > FSL

- https://github.com/thiagobustamante/typescript-rest /202106/ts
  - annotation-based expressjs extension for typescript.
  - typescript-rest、typescript-ioc、typescript-rest-ioc

- https://github.com/PostgREST/postgrest /26.3kStar/MIT/202512/haskell
  - https://postgrest.org/
  - PostgREST serves a fully RESTful API from any existing PostgreSQL database. 
  - It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.
  - 可直接将 PostgreSQL 数据库发布成 REST API，甚至有基于此库的 SaaS 服务如 supabase 可提供类 Google Firebase 的功能。
  - TLDR; subsecond response times for up to 2000 requests/sec on Heroku free tier.
    - Three factors contribute to the speed. First the server is written in Haskell using the Warp HTTP server (aka a compiled language with lightweight threads). Next it delegates as much calculation as possible to the database. Finally it uses the database efficiently with the `Hasql`(Haskell) library

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

- https://github.com/jbreckmckye/node-typescript-architecture /202307/ts/inactive
  - Hexagonal architecture / ports-and-adapters for Node.js using simple functional programming
  - 依赖newtype-ts、monocle-ts、fp-ts、express
# admin/crud
- api-server-nodejs /239Star/MIT/202211/ts/inactive
  - https://github.com/app-generator/api-server-nodejs
  - Express Starter with JWT authentication, and SQLite persistance - Provided by AppSeed App Generator. 
  - 依赖Express, SQLite, TypeORM, passport-jwt
  - 产品技术栈包含js/python，不包含golang
  - Authentication Flow uses json web tokens via Passport library - passport-jwt strategy.
  - TypeScript, Joy for validation
  - https://github.com/app-generator/api-server-nodejs-demo
  - https://github.com/app-generator/api-server-nestjs
  - https://github.com/app-generator/api-server-fastapi
  - https://github.com/app-generator/api-server-django
  - https://github.com/app-generator/api-server-flask
- api-server-nodejs-mongo /11Star/MIT/202212/ts/代码简单
  - https://github.com/app-generator/api-server-nodejs-mongo
  - 典型的dashboard的后端示例
  - 依赖express、mongoose、passport-jwt
  - Can be used with other React Starters for a complete Full-Stack experience
- https://github.com/app-generator/sample-docker-nodejs-react
  - docker compose up --build 

- https://github.com/sunburst89757/react-admin /202302/ts/inactive
  - https://github.com/sunburst89757/react-admin-backend
  - http://47.98.204.143:3000/login
  - 使用vite+ts+redux-toolkit为模板 创建的 react 后台管理模板
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

- fast-crud /1.1kStar/MIT/202510/ts/vue
  - https://github.com/fast-crud/fast-crud
  - http://fast-crud.docmirror.cn/
  - 面向配置的crud开发框架，快速开发crud功能，可作为低代码平台的基础框架
  - 可以直接使用示例中的fs-admin，特点是简单
  - 也可以采用其他的admin开源项目，然后集成fast-crud
  - 基于目前市面上开源的高星admin项目fork，集成fast-crud，ant-design-vue、Element-Plus 、NaiveUI
    - https://github.com/fast-crud/fs-admin-antdv /vue

- https://github.com/duxweb/dvha /176Star/MIT/202512/ts/vue
  - https://duxweb.github.io/dvha/
  - 一个基于 Vue 3 的无头（Headless）中后台框架，vue 版的 refine
  - 通过将业务逻辑与 UI 表现层解耦，专注于前端的多管理端、认证、权限、CRUD、I18n等业务逻辑处理，可以搭配任何 Vue 生态的 UI 框架
  - 可与任何 Vue 生态 UI 框架集成（Element Plus、Ant Design Vue、Naive UI 等）
  - 内置多管理端支持，支持主后台、子应用后台、商户后台等多租户架构
  - 完整的认证流程和权限管理，支持多种认证方式和细粒度权限控制

- https://github.com/thomas4019/expressa /MIT/202401/js/vue
  - API creation middleware with an admin interface
  - makes it easy to create basic APIs by using JSON schema
  - django-like admin interface for creating collection-REST endpoints and managing permissions
  - 依赖express、mongo-query、sift
  - it's just middleware, not a framework
  - per-collection database storage: MongoDB, PostgreSQL, or JSON-files (useful for version control)
  - Expressa is not primarily built for simple blog websites or mostly static content websites.

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

- https://github.com/go-admin-team/go-admin /12.3kStar/MIT/202509/go/ts/inactive
  - https://www.go-admin.pro/
  - 基于Gin + Vue + Element UI & Arco Design & Ant Design 的前后端分离权限管理系统脚手架（包含了：多租户的支持，基础用户管理功能，jwt鉴权，代码生成器，RBAC资源控制，表单构建，定时任务等）3分钟构建自己的中后台项目
    - 不依赖wire-di
  - 基于Casbin的 RBAC 访问控制模型
  - 基于 GORM 的数据库存储，可扩展多种类型数据库
  - 多租户：系统默认支持多租户，按库分离，一个库一个租户。
  - Element UI vue demo：https://vue2.go-admin.dev
  - Arco Design vue3 demo：https://vue3.go-admin.dev
  - antd demo：https://antd.go-admin.pro
  - [可以公开下Antd beta的前端代码吗？ _202210](https://github.com/go-admin-team/go-admin/issues/663)
    - antd是go-admin的订阅版, 一年88元
  - [这个项目连个维护的人都没有吗XD _202507](https://github.com/go-admin-team/go-admin/issues/841)
    - 应该是教程年久失修，还有几个前情提要没写上。 我用的mysql5.7，原配置文件用的utf8，我按要求建立数据库用的utf8，应该是后来数据库更新了，但是配置和说明都没有变更，直接跑，直接挂了，
    - 把数据库改成utf8mb4, 连接也改了utf8mb4 立马就可以运行了

- https://github.com/flipped-aurora/gin-vue-admin /23.8kStar/apache2+logo/202510/go/ts/vue
  - http://demo.gin-vue-admin.com/
  - Vite+Vue3+Gin拥有AI辅助的基础开发平台，企业级业务AI+开发解决方案，支持TS和JS混用。
  - 它集成了JWT鉴权、权限管理、动态路由、显隐可控组件、分页封装、多点登录拦截、资源权限、上传下载、代码生成器、表单生成器和可配置的导入导出等开发必备功能
  - 依赖gin、gorm、casbin、fsnotify、jwt、minio、excelize
    - 不依赖wire-di
  - 💰 如果您将此项目用于商业用途，请遵守Apache2.0协议并保留作者技术支持声明。您需保留如下版权声明信息，以及日志和代码中所包含的版权声明信息。所需保留信息均为文案性质，不会影响任何业务内容，如决定商用【产生收益的商业行为均在商用行列】或者必须剔除请购买授权
  - 采用MySql > (5.7) 版本 数据库引擎 InnoDB，使用 gorm 实现对数据库的基本操作。
  - 缓存：使用Redis实现记录当前活跃用户的jwt令牌并实现多点登录限制。
  - 配置文件：使用 fsnotify 和 viper 实现yaml格式的配置文件。

- https://github.com/GoAdminGroup/go-admin /8.7kStar/apache2/202506/go/inactive
  - https://www.go-admin.com/
  - http://doc.go-admin.cn/zh/quick_start/
  - 基于 golang 面向生产的数据可视化管理平台搭建框架
  - 一般开发一套管理后台需要至少一个后台工程师，一个前端工程师，花费至少一周时间才能搭建完成，搭建完成后我们需要分别去部署前端代码和后端代码。 而利用 GoAdmin，只需要一名golang后端工程师。在先花一点点时间了解掌握GoAdmin后，即可开发好一个面向生产环境的管理后台。而且所有的框架代码（包括前端文件）都将编译成一个二进制文件，直接部署到正式服务器即可运行，测试分发和部署十分便捷
  - 内置支持对主流SQL数据库（mysql/postgresql/sqlite/mssql）增删改查的管理插件，更多的功能插件如：服务器文件管理，数据监控系统等等会陆续开发并开放。
  - 内置完善的rbac权限系统
  - 支持多个web框架接入
  - GoAdmin通过各种适配器使得你在各个web框架中使用都十分的方便。目前支持的web框架有： gin / beego / fasthttp / buffalo / echo / gorilla/mux / iris / chi / gf
  - 框架的插件内容包括：控制器，路由以及视图

- https://github.com/LyricTian/gin-admin /2.8kStar/apache2/202506/go
  - 基于 Golang + Gin + GORM 2.0 + Casbin 2.0 + Wire DI 的轻量级、灵活、优雅且功能齐全的 RBAC 脚手架。

- https://github.com/mikestefanello/pagoda /2.8kStar/MIT/202508/go/ent
  - easy full-stack web development starter kit and admin panel in Go
  - Pagoda is not a framework but rather a base starter-kit for rapid, easy full-stack web development in Go
  - This project aims to highlight that Go alone can be powerful and easy to work with as a full-stack solution and ssr html
  - Echo: High performance, extensible, minimalist Go web framework.
  - HTML components written in pure Go. They render to HTML 5
# web-framework
- https://github.com/mjackson/remix-the-web/tree/main/packages/node-fetch-server /MIT/202409/ts/单文件
  - node-fetch-server allows you to build servers for Node.js that use the web Fetch API primitives (namely `Request` and `Response`) instead of the traditional `req/res` API used in libraries like Express.
  - This web standard API is already used in many places across the JavaScript ecosystem: Bun.serve, Cloudflare Workers, Deno.serve, Fastly Compute
  - When you write servers using the Request and Response APIs, you maximize the chances that your code will be portable across these different JavaScript runtimes.
  - https://x.com/mjackson/status/1831746987517264056
    - The main API is a createRequestListener() function you can use to create a http.RequestListener that seamlessly integrates with http.createServer() and https.createServer().
    - You can use this to power your Remix app *today* if you aren’t using any special features of Express
    - This is how the web evolves. The people who wrote the spec weren't thinking about server applications for it, but it happened. And now that it has (and we're not going back) it'll improve and adapt.
    - I have been saying this for years, this needs to be added to nodejs itself. Looks promising really nice job !
      - There's an effort in the Node.js committee to redesign the http module. I believe that will include the way servers are created. Fingers crossed!

- https://github.com/plantain-00/protocol-first-design-demo
  - API 协议优先，相关数据只需要相对集中地、相对方便地定义一次，其它信息由此派生或生成出来
  - graphql 的一个特点是，用户可以控制需要返回哪些字段，而 RESTful API 一般默认不会实现这个。
  - 这里的实现，不像 graphql 那样需要列出所有需要的字段，而是默认返回所有字段，根据参数中的 ignoredFields，把不需要的字段排除掉。
- https://github.com/plantain-00/protocol-based-web-framework
  - A protocol and code generation based web framework.
  - db支持sqlite、postgres、mongodb

- https://github.com/senchalabs/Connect /MIT/201905/js/inactive
  - Connect is an extensible HTTP server framework for node using "plugins" known as middleware.
  - The core of Connect is "using" middleware. Middleware are added as a "stack" where incoming requests will execute each middleware one-by-one until a middleware does not call `next()` within it.
  - These middleware and libraries are officially supported by the Connect/Express team
# rest-starter
- https://github.com/vagnercardosoweb/nodejs-structure-with-typescript /202401/ts/inactive
  - Structure already configured to start any API in NODE with Typescript
  - 未使用orm
  - https://github.com/vcwebnetworks/nodejs-skeleton

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

- https://github.com/edwinhern/express-typescript-2024 /202503/ts/函数式风格
  - Modular Structure: Organized by feature for easy navigation and scalability
  - Rapid TypeScript execution with `tsx` and type checking with `tsc`.
  - Efficient logging with `pino-http`.
  - Testing: Setup with Vitest and Supertest
  - Code Style: Biomejs for consistent coding standards
  - Docker Support: Ready for containerization and deployment
  - Strongly typed request validation using Zod
  - Swagger UI: Interactive API documentation generated from Zod schemas

- https://github.com/javieraviles/node-typescript-koa-rest /202105/ts/inactive
  - REST API boilerplate using NodeJS and KOA2, typescript. 
  - Logging and JWT as middlewares.
  - TypeORM with class-validator, SQL CRUD. 
  - Docker included. Swagger docs, actions CI and valuable README

- https://github.com/w3tecch/express-typescript-boilerplate /MIT/201911/ts/inactive
  - RESTful API with NodeJs & TypeScript
  - Inspired by the awesome framework laravel in PHP and of the repositories from pleerock

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
  - 作者是Developer Advocate @cloudflare，前端网红宣传多，待观望
  - The router RegExpRouter is really fast. Not using linear loops. 
  - Hono has zero dependencies and uses only the Web Standard API.
  - Hono has built-in middleware, custom middleware, and third-party middleware. 
  - https://github.com/honojs/honox /MIT/202403/ts
    - meta framework for creating full-stack websites or Web APIs - (formerly Sonik)
    - built on Hono, Vite, and UI libraries.
    - File-based routing - You can create a large application like Next.js.
    - You can bring your own renderer, not only one using hono/jsx.
    - Islands hydration - If you want interactions, create an island. JavaScript is hydrated only for it.

- https://github.com/oakserver/oak /MIT/202501/ts
  - https://oakserver.org/
  - oak is a middleware framework for handling HTTP requests across Deno, Node.js, Bun and Cloudflare Workers.
  - It also includes a middleware router
  - This middleware framework is inspired by Koa and middleware router inspired by @koa/router.
  - oak was inspired by Express.js and koa and originally written for the Deno runtime.

- https://github.com/Actionhero/Actionhero /apache2/202406/ts
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

- https://github.com/unjs/nitro /MIT/202403/ts
  - https://nitro.unjs.io/
  - Create web servers that run anywhere. 
  - The open engine powering Nuxt and open to everyone.
  - Nitro provides a built-in storage layer that can abstract filesystem or database or any other data source.
  - Nitro is a framework to build web servers with a lot more features than H3 and a larger scope. 
  - it's build on top of H3

- https://github.com/nksaraf/vinxi /MIT/202409/ts
  - https://vinxi.vercel.app/
  - The JavaScript toolkit to build full stack apps and frameworks with your own opinions
  - Compose full stack applications (and frameworks) using Vite, the versatile bundler and dev server, and Nitro, the universal production server. The core primitive in vinxi is a router.
  - There are currently two frameworks actively being developed on vinxi: SolidStart, TanstackStart
# py-fastapi
- https://github.com/yezz123/DogeAPI /MIT/202405/python/inactive
  - API with high performance built with FastAPI & SQLAlchemy, help to improve connection with your Backend Side to create a simple blog and Cruds with OAuth2PasswordBearer
  - uvicorn main:app --reload
  - [Build and Secure an API in Python with FastAPI – Blog _202105](https://blog.yezz.me/blog/Build-and-Secure-an-API-in-Python-with-FastAPI)
# more
