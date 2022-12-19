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


# api-spec
- https://github.com/json-api/json-api
  - https://jsonapi.org/
  - a specification for APIs that use JSON. 

- https://github.com/OData/odata.net
  - OData . NET Libraries project includes the implementation of core functionalities of OData protocol on the . NET platform, including URI parsing, request and response reading and writing, Entity Data Model (EDM) building
  - [OData简介 - 知乎](https://zhuanlan.zhihu.com/p/56639241)
  - [Why not OData? | Documentation](https://docs.servicestack.net/why-not-odata)
  - [olingo - Why is ODATA not widely adopted by the developers for RESTful development? - Stack Overflow](https://stackoverflow.com/questions/55266573/why-is-odata-not-widely-adopted-by-the-developers-for-restful-development)
  - https://github.com/zackyang000/node-odata
# rest-api
- api-server-nodejs /178Star/MIT/202212/ts
  - https://github.com/app-generator/api-server-nodejs
  - Express Starter with JWT authentication, and SQLite persistance - Provided by AppSeed App Generator. 
  - 依赖Express, SQLite, TypeORM, passport-jwt
  - Authentication Flow uses json web tokens via Passport library - passport-jwt strategy.
  - TypeScript, Joy for validation
- api-server-nodejs-mongo /11Star/MIT/202212/ts/代码简单
  - https://github.com/app-generator/api-server-nodejs-mongo
  - 典型的dashboard的后端示例
  - 依赖express、mongoose、passport-jwt
  - Can be used with other React Starters for a complete Full-Stack experience

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
- https://github.com/defunkt/jquery-pjax
  - pjax = pushState + ajax
  - pjax works by fetching HTML from your server via ajax and replacing the content of a container element on your page with the loaded HTML. 
    - It then updates the current URL in the browser using pushState. 
    - No page resources (JS, CSS) get re-executed or re-applied;

- https://github.com/falsandtru/pjax-api
  - https://falsandtru.github.io/pjax-api/
  - The pjax-api provides almost complete original web experience. 
  - Most SPA frameworks and pjax libraries lack many essential functions to keep the original web experience such as follows.
# more-rest-examples
- https://github.com/taniarascia/node-api-postgres
  - https://blog.logrocket.com/setting-up-a-restful-api-with-node-js-and-postgresql-d96d6fc892d8/
  - Create, read, update, delete in a Node.js app with an Express server and Postgres database.

- https://github.com/andregardi/jwt-express-typeorm
  - use TypeScript, Express.js and TypeORM to create an enterprise level Rest API with JWT authentication and role based authorization. 

- https://github.com/javieraviles/node-typescript-koa-rest
  - REST API boilerplate using NodeJS and KOA2, typescript. 
  - Logging and JWT as middlewares.

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
