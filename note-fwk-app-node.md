---
title: note-fwk-app-node
tags: [framework, node]
created: '2020-12-08T18:43:22.473Z'
modified: '2020-12-09T13:51:38.769Z'
---

# note-fwk-app-node

## guide

- node在js体系下标准和新技术发展非常快，框架的周期大多不长
  - 可选框架太多express, koa, nestjs, egg.js, midway, hapi, fastify
  - node的挑战者deno也在快速发展
- java spring成熟稳定，从200210维护至今，适合计划长期运行的企业级项目
  - spring几乎一家独大，不用纠结选择其他框架

## pieces

- node web framework
  - Express, Koa, Hapi, Restify, Fastify, Egg, Midways, Nest, Thinkjs, Sails

- [nest.js和阿里的midway将来谁会更胜一筹呢？](https://www.zhihu.com/question/329910651/answers/updated)
  - 两个框架的方向类似，都是走类似 Spring 那样的依赖注入路线的
  - Midway.js 背后是阿里的团队，而 Nest.js 背后是国外的 Trilon 团队

- nestjs
  - 项目的组织规范官方已经给了，还配套有 CLI，你不用再到处去找 best practice 了
    - passport、config 等一些常用的工具，Nest 有自己的实现
    - 以前用 express 这样传统的 node 框架，总感觉很累，主要工作就是写一个 route，再加个 handler，其它功能东拼西凑弄出来交差了事，总感觉像是在写脚本。。。而 Nest 在 OOP、TS、Decorator 的加持下，编码体验提升成不是一点半点
  - Nest受到Angular的启发，在服务器端提供开箱即用的应用架构，
    - 我自己更深一步的解释：本来Node上是有Express等框架的，为什么说框架没有解决“架构问题”呢？
    - 因为Express是unopinionated，只是一套基于middleware的库，没有规范“代码的结构”。
    - 而Angular是opinionated，定义了Template、Component、Filter(Pipe)、Service、Module这些概念，让代码组织起来更规范。
    - 代码组织规范，就是Nestjs文档中说的“架构”问题。只有代码更规范，开发出的应用才可以易测试、可扩展、松耦合、易维护。
  - nestjs基于nodejs，对前端同学友好，学个spring-boot成本有点高了，还得学java
  - 用过Java Spring 框架和 Angular的同学会发现NEST借鉴了两者很多的特性。
    - NEST属于前端TS大趋势下深度使用注解特性并提供各种增强开发体验的框架。
    - 配合TYPEORM可以在node下拥有不输SPRING的面向切面编程的体验
    - 阿里的egg.js则是在koa的基础上做了一层很好的面向大型企业级应用的框架封装，现在也有了非常好的TS特性支持。
    - egg.js更多的是按照洋葱模型的开发方式，和AOP编程还是有点区别的。
    - 中小型项目推荐egg.js，上手快易懂；大型项目不妨试试NEST.js+typeorm

## ref

- [NestJS is unnecessarily complex](https://www.reddit.com/r/node/comments/bmfvf6/nestjs_is_unnecessarily_complex/)
  - Nest is an opinionated framework, Just like angular
- [Future proof service with Express or Nestjs?](https://www.reddit.com/r/node/comments/cejxyn/future_proof_service_with_express_or_nestjs/)
  - If you're coming from the Java world, Nest will feel very at home with how it uses DI and IoC principles similar to Spring; 
  - after all, Nest was inspired by Angular and Angular was inspired by Java. 
  - Nest uses Express under the hood by default, but it can be set up to use Fastify instead 
  - all Express middleware is compatible with Nest 
  - Nest is just a collection of package (express, passport, typeORM, and others...) tied up with a non standard syntax.
- [nestjs vs plain express performance](https://stackoverflow.com/questions/47733390/nestjs-vs-plain-express-performance)
  - At 20200317, Nest + FastifyAdapter is now almost 2 times faster than express.
- [NestJS - The missing piece to easily develop full-stack TypeScript web applications](https://dev.to/mokkapps/nestjs-the-missing-piece-to-easily-develop-full-stack-typescript-web-applications-34ga)
