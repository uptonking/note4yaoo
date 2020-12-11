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
  - Midway是一个适用于构建 Serverless 服务，传统应用、微服务，小程序后端的 Node.js 框架。
  - 当前的函数，可以当做一个小容器，原来我们要写一个完整的应用来承载能力，现在只需要写中间的逻辑部分，以及考虑输入和输出的数据。
  - Midway 2.0 集成了 Serverless 能力，同时扩展了 RPC、Socket、微服务等场景，并在其中提供和前端一体化研发的能力
  - 架构设计
    - 和blitz都是在构建时整活，把属于后端的函数从前端剥离出去，用一个http请求代替。
    - 但是后端函数除了前端提供的参数，还需要req res等context参数。
    - blitz通过用useQuery useMutation来包装一层函数，修改函数签名，从而使得后端函数本身具有context参数，而前端调用时不可见这个context参数。
    - midway用了更简洁的办法，没有任何额外包装，context不体现在函数参数里，而是通过类似react hook的方法注入到函数体内。
  - 优点
    - 实现思路比blitz更简单，开发体验更好，实现一体化类型安全也不需要zod这样的东西，plain ts就够了。
    - 而且前端框架无关，react vue都可以。对前端侵入性较小
  - 缺点
    - 不见得一定是缺点吧，个人认为后端没有基于prisma，而是基于egg/midway
    - 大量使用decorator，ioc，还是传统后端味道有点重，审美上觉得不如prisma这样的更加"nodejs"风格的框架。
    - 对接数据库类型的方面，文档里推荐使用的是typeorm，也是一个特别面向对象的、decorator风格的库，写起来有点繁琐。
  - 其他
    - 个人以为，简单地从java等语言把OOP的语法习惯移植到nodejs，搞一堆class和装饰器，很多时候是多此一举的。
    - js本身就提供了原生的object，typescript也提供了很好的对原生object（的各种变形）进行各种typing的能力，
    - 所以实在是没必要在后端和数据库接口的地方搞出一堆数据model的class来。对比一下typeorm，prisma实现自动类型化的方式堪称js典范

- https://github.com/fastify/fastify
  - Fast and low overhead web framework, for Node.js
  - inspired by Hapi and Express

- https://github.com/darukjs/daruk
  - 基于 Koa2，使用 Typescript 开发的轻量级 web 框架
  - 使用 inversifyjs 的IoC容器管理依赖，让开发者享受最佳的OOP和IoC的编程体验。
  - 开启装饰器配置，ts 环境下引入即用

- https://github.com/blitz-js/blitz
  - 依赖react、nextjs、
  - The Fullstack React Framework, built on Next.js, Inspired by Ruby on Rails
  - “Zero-API” data layer lets you import server code directly into your React components instead of having to manually add API endpoints and do client-side fetching and caching.
  - Client-side rendering, Server-side rendering, and fully static pages all in the same app
  - 架构设计
    - 前端next(react)，后端prisma2，没有中间的graphql！！
    - 作者自己实现了两个神奇的 useQuery useMutation函数，作为前后端的桥梁。
    - 构建时，把应该属于后端的代码抽取到后端；
    - 开发时，则视为一个整体，整个app的最终类型定义来源就是prisma的schema，利用prisma自动生成的typscript类型定义，一路从后端代码到前端代码，共享这些类型定义。
  - 优点
    - 不再需要graphql这个麻烦东西了！把http api这个概念也藏起来了！在前后端之间，不仅仅是类型可以共享，整个http请求的过程都隐藏在 useQuery useMutation函数调用过程中了
    - 也提供了一套开箱即用的auth功能，以及自动给你配好了eslint prettier husky jest tsconfig等等这些每个项目都要重复搞一遍的东西。
  - 缺点
    - 一个不能算缺点的缺点，就是它是基于next/react的
  - 结论是，期待大佬，把blitz这个思路放到vue生态里来做个新全栈框架

- https://github.com/redwoodjs/redwood
  - 依赖react、prisma、apollo-graphql、jest、babel、webpack、storybook
  - an opinionated, full-stack, serverless web application framework that will allow you to build and deploy JAMstack applications with ease
  - In the "make it work; make it right; make it fast" paradigm, Redwood is in the later stages of the "make it work" phase. 
  - A Redwood application is split into two parts: a frontend and a backend. 
    - This is represented as two node projects within a single monorepo.
    - The frontend project is called web and the backend project is called api. 
    - They are separate projects because code on the web side will end up running in the user's browser while code on the api side will run on a server somewhere.
  - The api side is an implementation of a GraphQL API.
    - Your business logic is organized into "services"
    - Your services can interact with a database via Prisma's ORM
  - The web side is built with React.
    - Simple but powerful routing (all routes defined in one file) with dynamic (typed) parameters, constraints, and named route functions (to generate correct URLs).
    - Automatic page-based code-splitting.
    - Cells: a declarative way to fetch data from the backend API.
    - Cells allow you to declaratively manage the lifecycle of a component that fetches and displays data. 
  - the web side is called "web" and not "frontend". 
    - This is because Redwood conceives of a world where you may have other sides like "mobile", "desktop", "cli", etc., 
    - all consuming the same GraphQL API and living in the same monorepo.
  - 架构设计
    - 前端react，后端prisma2，中间是apollo graphql。
  - 优点
    - 在此基础上，前端包装了一个cell组件的概念，稍微简化了手写apolloQuery组件的负担；
    - 自己写了个类似react router的东西，包含了简单auth相关的前后端功能。
  - 缺点
    - mutation写法还没有任何简化，
    - 后端从db schema到graphql resolver（或者它叫service）也依然繁琐，没有简化（感觉还不如prisma团队写的nexus简单，可惜nexus framework断更不维护了）。
    - 另外最重要的，目前还没有好的ts支持，前后端自动类型安全上暂时还是白瞎。
  - 结论是：不痛不痒，额外好处不大。

## more-app-framework

- https://github.com/marblejs/marble
  - functional reactive Node.js framework for building server-side applications, based on TypeScript and RxJS.

- https://github.com/reframejs/wildcard-api
  - Wildcard is a JavaScript library to create an API between your Node.js backend and your browser frontend.
  - With Wildcard, creating an API endpoint is as easy as creating a JavaScript function.
  - REST and GraphQL are well-suited tools to create an API that is meant to be used by third-party developers.
  - However, if you want to create a backend API that is meant to be consumed only by your frontend, then you don't need REST nor GraphQL — RPC, such as Wildcard, is enough.
  - In a nuthsell:
    - Is your API meant to be used by third parties? Use REST or GraphQL.
    - Is your API meant to be used by yourself? Use RPC.
    - start with RPC as default and later switch to REST or GraphQL when (and only if!) the need arises.
