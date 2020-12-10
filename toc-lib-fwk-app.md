---
title: toc-lib-fwk-app
tags: [framework, lib, toc]
favorited: true
created: '2020-12-08T17:47:09.255Z'
modified: '2020-12-09T09:35:54.987Z'
---

# toc-lib-fwk-app

- 公司里面的技术选型很难由自己决定

## spring-like

- rester-core /2Star/MIT/202012/ts/commits-700
  - https://github.com/DevinDon/rester-core
  - A TypeScript framework, like Spring Boot.
  - 依赖reflect-metadata、typerom、mongodb、logger
  - 示例服务使用的是node http模块
- node-web-mvc /2Star/MIT/202011/ts/commits-200
  - https://github.com/Beven91/node-web-mvc
  - spring style web mvc framework for node
  - 依赖reflect-metadata、nodejs-hmr
  - node-web-mvc 默认支持三种启动模式
    - node 通过http模块来启动服务
    - express 通过express的中间件来附加服务
    - koa 通过koa的中间件类附加服务
  - 支持Controller 控制器、Route 路由映射、Arguments 参数提取、Response 返回内容、View 视图、Interceptor 拦截器、HttpMessageConverter 内容转换、热更新
- easy-node-ioc /11Star/ISC/202010/ts
  - https://github.com/chenkang084/easy-node-ioc
  - Use Typescript's decorator implement auto injection just like Spring MVC.
  - 用 Typescript 的装饰器实现依赖注入，就像我们使用 Spring MVC 框架一样，web 框架使用的是 Express。
- https://github.com/AsherWang/koa-springboot
  - springboot-like koa
- https://github.com/naoki-tomita/summer
  - A web framework like spring framework.
- https://github.com/loon-project/loon
  - Spring like framework build with Typescript
  - https://github.com/bpcloud/bpframework
  - /1Star/MIT/202011/ts
  - Web framework like java springboot
- https://github.com/t2ee/vader
  - Koa Router in Typescript, Servlet-Like API

- malagu /116Star/MIT/202012/ts
  - https://github.com/cellbang/malagu
  - core依赖reflect-metadata、inversify、rxjs、jexl、traverse
  - a Serverless First, component-based, platform-independent, progressive application framework based on TypeScript.
  - Spring Boot for TypeScript，可以认为是一个nodejs版本的spring boot
  - Convention over configuration, zero configuration, out of the box
  - Dependency injection
  - Facet-oriented programming (AOP)
  - Integrates with the popular ORM framework for declarative transaction
  - Managing Status with rxjs
  - 它是为了函数计算而生，但并非是一个函数计算的简单应用框架，它可以用来实现一个web服务器，也可以用来写写spa，甚至用来开发一个CLI
- https://github.com/Odi-ts/Odi
  - Based on declarative and imperative programming, inspired by ASP. NET / Spring

- https://github.com/singhfulda/loopback4
  - nodejs spring like typescript to do project
- https://github.com/webstyle/express-starter
  - Express.js, TypeScript web application starter Like Spring Boot(Java)

- https://github.com/linweiwei123/spring.js
  - deno framework like spring boot

## popular

- nest /32.4kStar/MIT/202012/ts
  - https://github.com/nestjs/nest
  - A progressive Node.js framework for building efficient and scalable server-side applications.
  - The architecture is heavily inspired by Angular.

- https://github.com/eggjs/egg
  - Egg.js 是一个基于 JavaScript 开发的框架，没有原生提供 TypeScript 的支持
  - 即便是使用了 egg-ts-helper 能够写出 ts 代码，各种三方库的支持也不受控制
  - [从 Egg.js 到 NestJS，爱码客后端选型之路](https://zhuanlan.zhihu.com/p/268159450)
- https://github.com/midwayjs/midway
  - 依赖egg2
  - Midway 是一个适用于构建 Serverless 服务，传统应用、微服务，小程序后端的 Node.js 框架。
  - 当前的函数，可以当做一个小容器，原来我们要写一个完整的应用来承载能力，现在只需要写中间的逻辑部分，以及考虑输入和输出的数据。
  - Midway 2.0 集成了 Serverless 能力，同时扩展了 RPC、Socket、微服务等场景，并在其中提供和前端一体化研发的能力

- https://github.com/fastify/fastify
  - Fast and low overhead web framework, for Node.js
  - inspired by Hapi and Express

- https://github.com/darukjs/daruk
  - 基于 Koa2，使用 Typescript 开发的轻量级 web 框架
  - 使用 inversifyjs 的IoC容器管理依赖，让开发者享受最佳的OOP和IoC的编程体验。
  - 开启装饰器配置，ts 环境下引入即用

## more-app-framework

- https://github.com/reframejs/wildcard-api
  - Wildcard is a JavaScript library to create an API between your Node.js backend and your browser frontend.
  - With Wildcard, creating an API endpoint is as easy as creating a JavaScript function.
  - REST and GraphQL are well-suited tools to create an API that is meant to be used by third-party developers.
  - However, if you want to create a backend API that is meant to be consumed only by your frontend, then you don't need REST nor GraphQL — RPC, such as Wildcard, is enough.
  - In a nuthsell:
    - Is your API meant to be used by third parties? Use REST or GraphQL.
    - Is your API meant to be used by yourself? Use RPC.
    - start with RPC as default and later switch to REST or GraphQL when (and only if!) the need arises.
