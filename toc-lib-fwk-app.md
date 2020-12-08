---
title: toc-lib-fwk-app
tags: [framework, lib, toc]
favorited: true
created: '2020-12-08T17:47:09.255Z'
modified: '2020-12-08T17:51:24.195Z'
---

# toc-lib-fwk-app

- 公司里面的技术选型很难由自己决定

## js-ts

- https://github.com/eggjs/egg
  - Egg.js 是一个基于 JavaScript 开发的框架，没有原生提供 TypeScript 的支持
  - 即便是使用了 egg-ts-helper 能够写出 ts 代码，各种三方库的支持也不受控制
  - [从 Egg.js 到 NestJS，爱码客后端选型之路](https://zhuanlan.zhihu.com/p/268159450)

- https://github.com/midwayjs/midway
  - 依赖egg2
  - Midway 是一个适用于构建 Serverless 服务，传统应用、微服务，小程序后端的 Node.js 框架。
  - 当前的函数，可以当做一个小容器，原来我们要写一个完整的应用来承载能力，现在只需要写中间的逻辑部分，以及考虑输入和输出的数据。
  - Midway 2.0 集成了 Serverless 能力，同时扩展了 RPC、Socket、微服务等场景，并在其中提供和前端一体化研发的能力

- https://github.com/cellbang/malagu
  - /116Star/MIT/202012/ts
  - a Serverless First, component-based, platform-independent, progressive application framework based on TypeScript.
  - Spring Boot for TypeScript
    - 借鉴Spring boot的开发思想，可以认为是一个nodejs版本的spring boot
  - Convention over configuration, zero configuration, out of the box
  - Dependency injection
  - Facet-oriented programming (AOP)
  - Integrates with the popular ORM framework for declarative transaction
  - Managing Status with rxjs
  - 它是为了函数计算而生，但并非是一个函数计算的简单应用框架，它可以用来实现一个web服务器，也可以用来写写spa，甚至用来开发一个CLI
- https://github.com/darukjs/daruk
  - 基于 Koa2，使用 Typescript 开发的轻量级 web 框架
  - 使用 inversifyjs 的IoC容器管理依赖，让开发者享受最佳的OOP和IoC的编程体验。
  - 开启装饰器配置，ts 环境下引入即用

## java
