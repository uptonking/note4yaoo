---
title: toc-lib-nestjs
tags: [lib, nestjs, toc]
created: 2020-12-13T13:14:12.113Z
modified: 2020-12-13T13:14:40.141Z
---

# toc-lib-nestjs

# guide
- 不必执着于查找模版，但选择主流框架可以参考很多已有问题的解决方案
  - 一般都可以将项目分解为前端ui、后台api，然后再细分模块
  - 比如论坛/电商/控制台admin前端ui、rest-api
  - 只有主流框架才会有丰富的集成方案和示例
  - 具体业务场景千变万化，若修改模版成本高，则不如自己实现
  - 实际开发者 MERN 技术栈用的人也很多
  - 集中精力到管理后台的业务
# nestjs-popular
- awesome-nestjs
  - 使用nestjs的代表：nodepress, leaa-cms, nestjsx/crud, realworld-eg
  - https://github.com/juliandavidmr/awesome-nestjs
  - https://github.com/dzzzzzy/Nestjs-Learning (多个例子)

- https://github.com/brocoders/nestjs-boilerplate
  - NestJS boilerplate. Auth, TypeORM, Postgres, Mailing, I18N, Docker.
  - Database (typeorm).
  - Sign in and sign up via email.

- https://github.com/rayman1104/ra-data-nestjsx-crud
  - a data-provider for react-admin
  - backend application built via nestjs framework with nestjsx/crud plugin.
  - https://github.com/marmelab/react-admin

- https://github.com/lujakob/nestjs-realworld-example-app
  - real world backend API built with NestJS + TypeORM/Prisma
  - The branch master implements TypeORM with a mySQL database.

- https://github.com/nestjsx/crud
  - RESTful APIs built with NestJs
- https://github.com/topfullstack/nestjs-mongoose-crud
  - Nest.js crud module for mongoose models without nestjsx/crud
- https://github.com/ablestack/nestjs-bff
  - A full-stack TypeScript solution, and starter project. 
  - Includes an API, CLI, and example client webapp.
  - The frontend example is in Angular, although any client-side Javascript framework can easily be used, including React, or Vue js.
- https://github.com/kyle-mccarthy/nest-next
  - it allows the rendering of next.js pages via nestjs controllers and providing initial props to the page as well.
- https://github.com/nerfdev/nest-rest-framework
  - toolkit for creating full-featured APIs using Nest framework. 
  - Inspired by Django REST Framework.
- https://github.com/notadd/notadd /201901
  - 基于Nest.js的微服务开发架构

- https://github.com/surmon-china/nodepress
  - RESTful API service for Blog/CMS, powered by @nestjs
  - 适用于 surmon.me 博客 的 RESTful API 服务；
  - v3.x 使用 nestjs 进行重构，之前的 nodejs 版本在nodejs分支。
  - 基于 nestjs； 需安装 mongoDB 和 Redis 方可完整运行。
- https://github.com/ZhiXiao-Lin/nestify /2019
  - An enterprise web fullstack framework based on Nest.js

- https://github.com/mx-space/core
  - Mix Space 核心服务；基于 nestjs (nodejs)，需安装 mongoDB 和 Redis 方可完整运行
  - https://github.com/mx-space/kami
  - https://github.com/mx-space/mx-web-yun

- https://github.com/JHyeok/nestjs-api-example
  - NestJS REST API Boilerplate
# nestjs-examples
- https://github.com/BlueRexPY/TSMusic
  - https://ts-music.vercel.app/
  - Spotify clone online application
  - 前端依赖 react, mobx, nextjs
  - 后端依赖 nestjs, mongodb

- https://github.com/kentayamada-dev/instagram-clone
  - Instagram Clone
  - https://app.instagram-clone.net/
  - 分前后端2个文件夹
  - 前端依赖 nextjs, chakra-ui, swr

- https://github.com/mk026/kanban-board
  - (WIP) Fullstack React (MUI, MobX) / NestJS (TypeORM, PostgreSQL) App
  - 分前后端2个文件夹

- https://github.com/alvytsk/nestjs-react-gallery-app
  - Server Nestjs Database MongoDB File Storage MinIO Client based on my boilerplate for Webpack/React/Redux app

- https://github.com/juvpengele/nestjs-react-file-sharing-app
  - This is a file sharing application with features like authentication, uploading images, create sharable links for your images, upgrading your plan using stripe
  - 依赖 tailwindcss, vite, react-query

- https://github.com/chenc041/react-nestjs-full-stack
  - A react and nestjs full stack template
- https://github.com/alexKudryavtsev-web/template-nestjs-react
  - Template app by NestJs and React
  - Authorization by JWT

- https://github.com/NiGhTTraX/ts-monorepo
  - Template project for setting up a TypeScript monorepo

- https://github.com/coderinblack08/presage
  - https://www.joinpresage.com/
  - A Medium alternative built for referral podcasts and blogs

- https://github.com/nathanielhall/mern-starter-app
  - Fullstack starter app using React, NestJS, PostgreSQL (not MERN)
  - NestJSTypeScriptPrisma

- https://github.com/ehawk61/CountryViewer
  - Viewing Countries loaded into a MongoDB and having basic CRUD operations to it.

- https://github.com/alshiryaev/autoportal
  - An example fullstack web app. NestJS + React + Docker-Compose.
  - typeorm

## blog/forum

- https://github.com/fantasticit/wipi /202107
  - https://blog.codingit.cn/
  - A blog system written by React.js, Nest.js and MySQL.
  - Wipi是一个面向个人的开源的集成文章发表、页面创建、知识小册等功能的 CMS 系统
  - MySQL：数据存储; next.js：前端页面框架; nest.js：服务端框架; AliyunOSS：对象存储
  - 分为client + server + admin 三部分
  - client前端依赖antd4、highlight.js、next10、react-spring、viewerjs(image)
  - admin控制台依赖antd4、echarts4、monaco-editor、next10、showdown
  - server依赖nestjs6、typeorm、marked、mysql、rxjs6、passport

- https://github.com/bs32g1038/node-blog
  - https://www.lizc.net/
  - react blog project base on nodejs, nestjs, mongoose, typescript, react, ant-design, nextjs

- https://github.com/starryskystar/blog-c
  - 博客重构，后端服务基于nestjs；界面重度模仿知乎
  - 依赖antd4、umijs、marked、prismjs、braft-editor
- https://github.com/hys1440248234/Developer-Forum
  - 仿掘金的开发者论坛，前后端，仅用于学习目的。
  - 使用 Vue.js3+Typescript+Nest.js

- Surmon.me 个人网站
  - https://github.com/surmon-china/nodepress /202106
    - RESTful API service | 博客服务端
    - 给出了部分文档说明，包括数据库
  - https://github.com/surmon-china/surmon.me
    - 使用 Vue (3) 构建的个人网站。
  - https://github.com/surmon-china/veact-admin
    - 适用于 surmon.me 博客的管理员后台应用，使用 React 和 veactjs(Mutable state enhancer lib for @react by @vuejs) 进行开发。以react为主。
    - https://github.com/surmon-china/surmon.me.native
      - My blog app, powered by react-native

- https://github.com/caiocampos/blog-posts
  - Página de postagens usando React, NestJS, Mongoose e MongoDB
  - 界面偏向博客管理后台

- https://github.com/mavhungu/nestjs-blog
  - 分前后端2个文件夹

- https://github.com/shen100/mili /202003
  - 开源的社区系统, nestjs+vue

- https://github.com/JekEugene/nestjs-forum
  - client + server

- https://github.com/hojas/nest-blog
  - A simple blog server system build with Nest.
  - 没有实现前端
- https://github.com/joffarex/nodorum
  - Fully featured, reddit-like forum API, with advanced RBAC system, built with NestJS, DDD, CQRS and much more...
  - 没有实现前端

- https://github.com/sygeman/dream
  - 类似slack/discord的界面，部分聊天需要会员身份

## admin (很多blog/cms自身也会提供admin管理界面)

- https://github.com/SolidZORO/leaa /202008
  - a monorepo CMS (Content Management System) built with Nest.js, Next.js, and Ant Design.
  - leaa-api/backend(Nest.js + @nestjsx/crud + MySQL + Docker Compose)
  - leaa-dashboard(demo)/dashboard (React.js + Antd + MobX)

## ecommerce/saas

- https://github.com/TencentCloudBase/cloudbase-extension-cms
  - https://docs.cloudbase.net/cms/intro.html
  - 依赖 Node.js + Nest.js + CloudBase
  - CloudBase CMS 是由腾讯云开发推出的，基于 Node.js 的 Headless 内容管理平台
  - 基于模板配置生成内容管理界面，无须编写代码
  - 支持 Webhook 触发，可以方便的与外部系统集成

- https://github.com/michalmarchewczyk/ecommerce-platform-nestjs-api
  - REST API for the E-commerce Platform project

- https://github.com/staart/api /202103
  - SaaS backend & API framework powered by @nestjs

- https://github.com/ibrahimjelliti/BookStore
  - 简单服务器，无数据库，使用json对象模拟crud

- https://github.com/kelvin-mai/nest-commerce /201905
  - E-Commerce Web App built with NestJS

## starter

- https://github.com/shalahinovilya/nestjs-react-store
  - 前端js
- https://github.com/celestialsonya/burger-app-nestjs
  - express-react-postgress fullstack app with nestjs

- https://github.com/Clarence161095/reactjs-nestjs-typeorm-template
  - 分前端和后端2个文件夹

- https://github.com/Yasai-T/Nexra
  - nextjs chakra-UI nestJS prisma monorepo

- https://github.com/appcket/appcket-org
  - Appcket is a starter kit to build your next great app idea
- https://github.com/alexdevero/docker-nestjs-react-postgres
  - Starter app build with Nest.js, React, PostgreSQL and Docker

## more-examples

- https://github.com/nphivu414/game-store-monorepo-app
  - A full-stack web app built with NestJS and ReactJS that helps you find and discover over 500, 000+ video games on your device. Powered by RAWG API.

- https://github.com/benediktms/hive-mind
  - Monorepo for the hive-mind nest api and next web app
- https://github.com/kshipra-jadav/Pizza-Ordering-App
  - Full Stack Pizza Ordering App - Made With React(TS), NestJS and Postgres :)

- https://github.com/omerta-web-master/Socialdive
  - Social media full stack application. React JS + Nest JS

- https://github.com/Vivify-Ideas/nestjs-boilerplate
  - Authentication, TypeORM, Configuration, Swagger
- https://github.com/bradtraversy/nestjs_rest_api
  - A CRUD REST API using the NestJS framework and MongoDB/Mongoose.
- https://github.com/kuangshp/nestjs-mysql-api
  - nestjs+mysql+typeorm+jwt+swagger企业项目中的RBAC权限管理
  - 采用java的MVC的经典开发模型(在nestjs开发中也可以使用基于angular方式的模块化开发模式, 看个人喜好), 来构建项目结构
  - 使用jwt的方式进行登录鉴权(颗粒度仅到菜单权限)
- https://github.com/NarHakobyan/awesome-nest-boilerplate
  - nestjs, Typescript, Postgres, TypeORM
- https://github.com/squareboat/nestjs-boilerplate
  - A production ready scalable NestJS boilerplate with batteries included. 
  - Objection.js is a SQL-friendly ORM for Node.js
- https://github.com/fivethree-team/nestjs-prisma-starter
  - GraphQL with Prisma Client, Passport-JWT authentication, Swagger Api and Docker
- https://github.com/WonderPanda/nestjs-microservice-architecture
  - A reference architecture for building microservices with Nest
- https://github.com/kentloog/nestjs-sequelize-typescript
  - Nest + sequelize-typescript + JWT + Jest + Swagger
  - [Weekly Discussion: Prisma/Typeorm/Sequelize](https://www.reddit.com/r/graphql/comments/auas6a/weekly_discussion_prismatypeormsequelize/)

- https://github.com/kelvin-mai/nest-ideas-api
  - A reddit/twitter style app to keep track of posted App Ideas. 
  - This is the companion source code for the YouTube tutorial Ideas App - NestJS API series.

- https://github.com/rucken/core-nestjs
  - A simple application demonstrating the basic usage of permissions with NestJS (JWT, Passport, Facebook)
- https://github.com/Javen205/TNWX
  - 微信系开发脚手架，支持微信公众号、微信支付、微信小游戏、微信小程序、企业微信/企业号
  - 能快速的集成至任何 Node.js 框架(Express、Nest、Egg、Koa 等)

- https://github.com/pietrzakadrian/bank
  - Full Stack Web Application similar to financial software that is used in banking institutions | React.js and Node.js
  - client/frontend
    - React.js, Redux, Redux-Saga, Reselect, immer, Ant Design and styled-components
  - server/backend
    - TypeScript, Node.js, Nest.js, REST API, PostgreSQL and Swagger Documentation
# nestjs-extensions
- https://github.com/sergey-telpuk/nestjs-rbac
  - rbac module for Nest.

- https://github.com/nest-cloud/nestcloud
  - A NodeJS micro-service solution, writing by Typescript language and NestJS framework.
  - Consul module. Etcd module. Kubernetes client module.

- https://github.com/Theodo-UK/nestjs-admin
  - A generic administration interface for TypeORM entities

- https://github.com/cristiangonsevi/auth_backend
  - Backend of auth application built with NestJs 8
# nestjs-repos
- https://github.com/Discoin/api-v3
  - The rewritten Discoin API

- https://github.com/Passion-fruits/passionfruits-backend-node
  - https://github.com/Passion-fruits/passionfruit_frontend_V2

- https://github.com/bulolo/nestjs-admin
  - nestjs+mysql+typeorm+jwt+swagger搭建企业项目中的RBAC权限管理
  - 基于Nestjs的权限管理系统。提供了丰富的中间件支持（用户认证、跨域、访问日志、追踪ID等）
  - 没有实现前端
