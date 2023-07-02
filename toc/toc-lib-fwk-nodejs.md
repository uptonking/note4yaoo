---
title: toc-lib-fwk-nodejs
tags: [framework, lib, nodejs, toc]
created: 2020-12-08T17:47:09.255Z
modified: 2022-12-19T01:49:01.371Z
---

# toc-lib-fwk-nodejs

# guide

- 团队协作时统一且易理解的架构抽象、功能隔离、插件设计更重要
- 国内有很多快速开发框架如jeesite/jeecg，国外对应的是cms框架
  - https://github.com/n370/awesome-headless-cms

- ref
  - keyword: backend-for-frontend, spring-like, restful-api, node-framework
  - [下一代前端框架会去解决什么问题？ blitz、redwood](https://www.zhihu.com/question/433673833/answer/1616521720)
    - 个人认为，前端~api~后端~数据库，这个链条上的类型安全，是个发展方向。
    - 现在的graphql，apollo，next，prisma这些感觉还是繁琐，未成简洁体系。
  - [@nestjs/core vs koa vs fastify vs restify vs loopback](https://www.npmtrends.com/@nestjs/core-vs-koa-vs-fastify-vs-restify-vs-loopback)
# popular-node-framework
- trpc /14.9kStar/MIT/202211/ts
  - https://github.com/trpc/trpc
  - https://trpc.io/
  - tRPC allows you to easily build & consume fully typesafe APIs, without schemas or code generation.
  - The client above is not importing any code from the server, only its type declarations.

- feathers /14.3kStar/MIT/202301/ts
  - https://github.com/feathersjs/feathers
  - A framework for real-time applications and REST APIs with JavaScript and TypeScript
  - Feathers can interact with any backend technology, supports over a dozen databases and works with any frontend technology like React, VueJS, Angular, React Native, Android or iOS.
  - v5_202211使用typescript重写，不使用orm而用基于knex(js)的schema+resolver

- nestjs /32.4kStar/MIT/202012/ts
  - https://github.com/nestjs/nest
  - core依赖reflect-metadata、rxjs6、websockets、express、axios
  - A progressive Node.js framework for building efficient and scalable server-side applications.
  - The architecture is heavily inspired by Angular.
  - Under the hood, Nest makes use of Express, but also, provides compatibility with a wide range of other libraries, like e.g. Fastify, 

- loopback.v4 /3.7kStar/MIT/202106/ts
  - https://github.com/strongloop/loopback-next
  - https://loopback.io/doc/en/lb4/index.html
  - api多用class和@get等装饰器
  - extensible Node.js and TypeScript framework for building APIs and microservices.
  - OpenAPI Spec Driven REST API
  - A new, improved programming model with Dependency Injection and new concepts such as Components, Mixins, Repositories, etc. make this the most extensible version yet.
  - loopback是三个功能的集合
    - 基于Express的web架构
    - 结合Express提供便捷的RESTFul接入
    - 提供一套ORM解决方案
  - 优点
    - 集成了 swagger，ORM，auth验证
    - 接口自动生成。可以定制。
  - 缺点
    - 缺乏灵活性。针对性的业务逻辑难以改动。

- blitz
  - https://github.com/blitz-js/blitz
  - 依赖react、nextjs、prisma、passport、react-query、jsonwebtoken
  - 代码风格是functional，很少用class、this；依赖注入也少
  - 特色是 no api，带来的问题是很难在mobile app中使用blitz query
  - The Fullstack React Framework, built on Next.js, Inspired by Ruby on Rails
  - “Zero-API” data layer lets you import server code directly into your React components instead of having to manually add API endpoints and do client-side fetching and caching.
  - Client-side rendering, Server-side rendering, and fully static pages all in the same app
  - Database/ORM agnostic, but Prisma 2 is default
  - 架构设计
    - 前端nextjs(react)，后端prisma2，没有中间的graphql！！
    - 作者自己实现了两个神奇的useQuery useMutation函数，作为前后端的桥梁
    - 构建时，把应该属于后端的代码抽取到后端；
    - 开发时，则视为一个整体，整个app的最终类型定义来源就是prisma的schema，利用prisma自动生成的typscript类型定义，一路从后端代码到前端代码，共享这些类型定义。
  - 优点
    - 不再需要graphql这个麻烦东西了！把http api这个概念也藏起来了！在前后端之间，不仅仅是类型可以共享，整个http请求的过程都隐藏在 useQuery useMutation函数调用过程中了
    - 也提供了一套开箱即用的auth功能，以及自动给你配好了eslint prettier husky jest tsconfig等等这些每个项目都要重复搞一遍的东西。
  - 缺点
    - 一个不能算缺点的缺点，就是它是基于next/react的
    - 后端api不方便扩展到其他端，如android、ios
  - 结论是，期待大佬，把blitz这个思路放到vue生态里来做个新全栈框架
  - Introducing Blitz, a Ruby on Rails equivalent for monolithic fullstack React apps!
    - https://twitter.com/flybayer/status/1229425878481793024
    - At build time we swap out that import with a API call. The server code stays on the server. 
    - This is a huge DX boost since you don’t have to muck with all the API stuff yourself.
  - Adonis uses SSR templates instead of React, so it's in its own category, imo
    - That leaves Redwood & Blitz. We have a core difference at our data layer, but I could see a future where we merge together.
    - For now, we are both testing our hypothesis to see what people really want 
  - Blitz/Redwood are providing an all-in-one Rails-like DX with CLI, code scaffolding, etc, 
    - where Remix is just the react framework part.
    - You could totally build a Blitz/Redwood type thing on top of Remix.

- https://github.com/ts-rest/ts-rest
  - https://ts-rest.com/
  - RPC-like client, contract, and server implementation for a pure REST API
  - ts-rest offers a simple way to define a contract for your API, giving you end to end type safety without the hassle or code generation.
  - No Code Generation
  - Full optional OpenAPI integration

- egg /16.5kStar/MIT/202011/js
  - https://github.com/eggjs/egg
  - https://github.com/eggjs/egg-core
  - 是一个基于JavaScript开发的框架，没有原生提供 TypeScript 的支持
  - 即便是使用了 egg-ts-helper 能够写出 ts 代码，各种三方库的支持也不受控制
  - [从 Egg.js 到 NestJS，爱码客后端选型之路](https://zhuanlan.zhihu.com/p/268159450)

- midway /3.4kStar/MIT/202012/ts
  - https://github.com/midwayjs/midway
  - 依赖egg2
  - Midway是一个适用于构建 Serverless 服务，传统应用、微服务，小程序后端的 Node.js 框架。
  - 当前的函数，可以当做一个小容器，原来我们要写一个完整的应用来承载能力，现在只需要写中间的逻辑部分，以及考虑输入和输出的数据。
  - Midway 2.0集成了 Serverless 能力，同时扩展了 RPC、Socket、微服务等场景，并在其中提供和前端一体化研发的能力
  - 架构设计
    - midway和blitz都是在构建时整活，把属于后端的函数从前端剥离出去，用一个http请求代替。
    - 但是后端函数除了前端提供的参数，还需要req res等context参数。
    - blitz通过用useQuery useMutation来包装一层函数，修改函数签名，从而使得后端函数本身具有context参数，而前端调用时不可见这个context参数。
    - midway用了更简洁的办法，没有任何额外包装，context不体现在函数参数里，而是通过类似react hook的方法注入到函数体内。
  - 优点
    - 实现思路比blitz更简单，开发体验更好，实现一体化类型安全也不需要zod这样的东西，plain ts就够了。
    - 而且前端框架无关，react vue都可以。对前端侵入性较小
  - 缺点
    - 不见得一定是缺点吧，个人认为后端没有基于prisma，而是基于egg/midway
    - 大量使用decorator、ioc，还是传统后端味道有点重，审美上觉得不如prisma这样的更加"nodejs"风格的框架。
    - 对接数据库类型的方面，文档里推荐使用的是typeorm，也是一个特别面向对象的、decorator风格的库，写起来有点繁琐。
  - 其他
    - 个人以为，简单地从java等语言把OOP的语法习惯移植到nodejs，搞一堆class和装饰器，很多时候是多此一举的。
    - js本身就提供了原生的object，typescript也提供了很好的对原生object（的各种变形）进行各种typing的能力，
    - 所以实在是没必要在后端和数据库接口的地方搞出一堆数据model的class来。对比一下typeorm，prisma实现自动类型化的方式堪称js典范
   - https://github.com/ykfe/ssr
    - fullstack framework based on midway-faas that implemented serverless-side render specification for faas.
    - ssr is serverless-side render specification implementation.
    - Serverless让端开发者更好地开发各种端上应用，不需要投入太多精力关注于后端服务的实现
    - 此框架脱胎于 egg-react-ssr 项目和 ssr v4版本（midway-faas + react ssr）

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
    - 后端从db schema到graphql resolver（或者它叫service）也依然繁琐，没有简化。
    - 另外最重要的，目前还没有好的ts支持，前后端自动类型安全上暂时还是白瞎。
  - 结论是：不痛不痒，额外好处不大。

- https://github.com/adonisjs/core
  - Fullstack MVC framework for Node.js
  - It takes care of much of the Web development hassles, offering you a clean and stable API to build Web apps and micro services.
  - node版本的laravel，laravel中让人喜欢的orm的Eloquent，在adonisjs中叫lucid，比laravel的代码量还少
  - adonisjs是后端框架，和vue，angular等前端框架没有冲突，就是说，使用adonisjs做数据api，把json格式的数据发送给vue、angular等前端框架，或者小程序等，非常便捷。
  - adonisjs默认返回json格式，使用视图模版就是ssr的方式
  - 非常opinionated，rest api和orm都是自己实现，不支持typeorm和prisma
  - 使用ace自定义cli，而不是npm scripts
- https://github.com/varaljs/varal
  - 在node上实现Laravel的编程思想与代码风格

- https://github.com/xiongwilee/Gracejs
  - A Nodejs BFF framework, build with koa2（基于koa2的标准前后端分离框架）

- https://github.com/marblejs/marble
  - functional reactive Node.js framework for building server-side applications, based on TypeScript and RxJS.
  - Marble wraps native HTTP server with the RxJS, giving a pretty straightforward way to treat incoming requests like streams, in a very reactive manner. 
  - It won't bring any value to Nestjs though since we completely encapsulate server behind provided architecture's building blocks. What sits underneath doesn't matter

- https://github.com/FoalTS/foal
  - a Node.js framework for building HTTP APIs and Web applications with a rich interface(Angular/React/Vue).
  - The authorization system, database migrations, development tools or even hashing of passwords are just the tip of the iceberg. 
  - But FoalTS does not pretend to be a closed framework. 
  - You can still import and use your favorite libraries from the rich ecosystem of Node.js.
- https://github.com/TypedProject/tsed
  - a framework on top of Express/Koa to write your application with TypeScript
  - It provides a lot of decorators and guideline to make your code more readable and less error-prone.
- https://github.com/socketio/socket.io
  - Realtime application framework (Node. JS server)
- https://github.com/fastify/fastify
  - Fast and low overhead web framework, for Node.js
  - inspired by Hapi and Express
- https://github.com/darukjs/daruk
  - 基于Koa2，使用Typescript开发的轻量级web框架
  - 使用 inversifyjs 的IoC容器管理依赖，让开发者享受最佳的OOP和IoC的编程体验。
  - 开启装饰器配置，ts环境下引入即用

- https://github.com/nodosjs/nodos
  - https://nodosjs.github.io/
  - Node.js framework for humans (inspired by rails, phoenix, django)
# rust
- https://github.com/patr0nus/rust-nodejs
  - Embedding Node.js in Rust.
# loopback-examples
- https://github.com/loopbackio/loopback4-example-shopping
  - LoopBack 4 Example: Online Shopping APIs
  - [e-commerce demo scenario](https://github.com/loopbackio/loopback-next/issues/1476)

- https://github.com/tomasggarcia/Loopback-my-sql-react-challenge
  - http://18.229.137.95/
  - 简单crud项目，依赖少

- more-loopback
  - https://github.com/NguyenVanDo51/base_project_react_loopback
# more-app-framework
- https://github.com/ladjs/lad
  - Lad is the best Node.js framework. 可替代express或koa
  - Made by a former Express TC and Koa team member.

- https://github.com/reframejs/wildcard-api
  - Wildcard is a JavaScript library to create an API between your Node.js backend and your browser frontend.
  - With Wildcard, creating an API endpoint is as easy as creating a JavaScript function.
  - REST and GraphQL are well-suited tools to create an API that is meant to be used by third-party developers.
  - However, if you want to create a backend API that is meant to be consumed only by your frontend, then you don't need REST nor GraphQL — RPC, such as Wildcard, is enough.
  - In a nuthsell:
    - Is your API meant to be used by third parties? Use REST or GraphQL.
    - Is your API meant to be used by yourself? Use RPC.
    - start with RPC as default and later switch to REST or GraphQL when (and only if!) the need arises.
