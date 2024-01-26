---
title: toc-lib-fwk-saas
tags: [fwk, lib, saas, toc]
created: 2021-03-31T06:23:17.868Z
modified: 2021-05-25T09:41:29.066Z
---

# toc-lib-fwk-saas

# software-as-a-service

- https://github.com/TencentCloudBase/cloudbase-extension-cms
  - https://docs.cloudbase.net/cms/intro.html
  - 依赖 Node.js + Nest.js + CloudBase
  - CloudBase CMS 是由腾讯云开发推出的，基于 Node.js 的 Headless 内容管理平台
  - 基于模板配置生成内容管理界面，无须编写代码
  - 支持 Webhook 触发，可以方便的与外部系统集成
# saas-multi-tenant
- [How To Build A Multi-Tenant App With Payload](https://payloadcms.com/blog/how-to-build-a-multi-tenant-app-with-payload)

- [现在主流的saas软件所有租户共用一个数据库吗？ - 知乎](https://www.zhihu.com/question/43650948)
  - 现在主流的saas类软件，比如： 金蝶云ERP， 管家婆云进销存， 纷享销客，阿里丁丁等等， 他们是每个租户有独立的数据库还是共用一个数据库？

- 3种方案
  - separate database
    - 1 db per tenant
  - Shared Database, Separate Schemas
    - 1 table per tenant
  - Shared Database, Shared Schema
    - 1 table all tenants

- 我们采用多数据库 + schema（Postgresql）隔离方案，一个数据库存储多个用户的数据，同时兼容成本及性能扩容需求。
  - 支持多个数据库，用户增长时仅需新增数据库即可扩容

- 只有多租户的架构，才有可能实现所有客户共享基础设施，分摊运维成本。
  - 所以，从老美的视角：SaaS能够取代安装版，最根本的原因是成本Cost。而多租户是实现这种成本降低的关键。
  - 2012年在美国也有这种方式，将一个安装版软件打扮成SaaS模式，到现在，都在市场上消失，大家改变不了这种成本模型，其实是把自己硬往坑里塞啊。
  - 所以，结论是就是：主流SaaS是多租户架构，所有租户共享一个、或者多个数据库。
- 现在大一些的企业级的SaaS会采用混合模式，一部分共享资源，一部分隔离。现在比较前沿的就是用Serverless来做隔离。
- 看一下多租户的开源框架，大概就能看出来。
  - 小客户一般是通过租户Id来控制访问权限的。
  - 大客户可以单独给他开一个数据库。
  - 这种操作完全可以在数据访问层做控制。

- https://github.com/daniccan/multi-tenant-node-app /202209/js
  - POC of Multi-Tenant REST Application Built on top of NodeJS
  - npx sequelize-cli db:migrate
- https://github.com/larbisahli/multi-tenant-application-architecture-with-node.js /202207/ts/共享db
  - Multi-tenant application architecture with Node.js - Express, and PostgreSQL
  - In the Table-based multi-tenancy model, every row in every table is associated with a partitioning key (usually the tenant identifier) and restricts data access using Row Level Security (RLS for short), consequently, we don't need to worry about which schema or database it is connecting to.

- https://github.com/PIYoung/node-express-boilerplate-multitenant
  - node express postgres boilerplate for multitenant(saas)

- nextacular /454Star/MIT/202209/js
  - https://github.com/nextacular/nextacular
  - https://nextacular.co/
  - starter kit that will help you build full-stack multi-tenant SaaS platforms efficiently and help you focus on developing your core SaaS features. 
  - 依赖nextjs、swr、headlessui、prisma
  - Features packaged out-of-the-box: Authentication, Billing & Payment, Database, Email, Custom Domains, Multi-tenancy, Workspaces, and Teams

- https://github.com/raymondkneipp/multi-tenant-via-subdomain /202210/ts
  - Demo app I built to display information from a mock database depending on the subdomain. 
  - This basic concept can be used to implement multi-tenant architecture into any app.

- https://github.com/BeameryHQ/ddd-ts /202201/ts
  - Build (multi-tenanted) NodeJS apps with DDD and Typescript with ease.

- https://github.com/micheleriva/krabs /202108/ts/inactive
  - Krabs is an enterprise-ready Express.js/Fastify middleware for serving thousands of different websites from a single Next.js instance.

- https://github.com/craftup/node-mongo-tenant /22009/js
  - A multi-tenancy plugin for mongoose with tenant separation on document level.
  - There are 3 ways of implementing multi-tenancy in mongoDB:
    - on document level (cheap and easy to administer but only secured by app logic)
    - on collection level (not recommended, due to breaking mongoDB concepts)
    - on database level (very flexible and secure but expensive)

- https://github.com/calvo-jp/fe-hybrid-setup /202210/ts
  - micro FE, monorepo, multi-tenant, etc... (exploration)
- https://github.com/devpies/saas-client /202211/ts
  - Multi-tenant SaaS app built on AWS
- https://github.com/kevinmmartins/node-multi-tenant-application /201910/js
  - Multi-tenant application example
- https://github.com/horacioh/multi-tenancy-react-example /201902/ts
  - React Multi tenant Architecture example

- https://github.com/tux86/nestjs-serverless-boilerplate /202205/ts
  - Serverless Multi-tenant NestJS backend "Boilerplate" + Fastify + Serverless Framework 3 + Graphql + Modules for AWS Serverless
- https://github.com/marcoesposito/nestjs-typeorm-multi-tenant /202005/ts
  - NestJS and TypeORM application that handles multi tenants with multi database
- https://github.com/deye9/node-multi-tenant /201905/js
  - Multi-tenant Application with Node.js
  - https://laravel-tenancy.com/ served as an inspiration for this project.
# netlify/vercel/self-hostable
- https://github.com/coollabsio/coolify
  - https://coollabs.io/coolify
  - 前端依赖svelte
  - An open-source, hassle-free, self-hostable Heroku & Netlify alternative
# micro-frontend
- https://github.com/microsoft/redux-micro-frontend /202202/ts/inactive
  - This library can be used for using Redux in a Micro Frontend based architecture.
  - Micro Frontends is an architectural pattern for breaking up a monolith Frontend application into manageable, decoupled and smaller applications.
# auth
- https://github.com/nextauthjs/next-auth /ISC/ts
  - https://authjs.dev/
  - a set of open-source packages that are built on Web Standard APIs for authentication in modern applications with any framework on any platform in any JS runtime.
  - [database adapters](https://authjs.dev/reference/adapters)
    - 支持sequelize、prisma、drizzle
  - [NextAuth.js is becoming Auth.js_20221215](https://twitter.com/balazsorban44/status/1603082914362986496)
    - Runtime/framework agnostic
  - https://github.com/nextauthjs/next-auth-example
    - Example showing how to use NextAuth.js with Next.js

- https://github.com/logto-io/logto /MPL/ts
  - https://logto.io/
  - a modern Auth0 alternative for building identity infrastructure with minimal effort
  - offers a comprehensive identity solution covering both the front and backend, complete with pre-built infrastructure
  - OIDC-based authentication and RBAC authorization.
  - Flexible connectors, scalable with community contributions, customizable with SAML, OAuth, and OIDC protocols.
  - Various sign-in options, such as social, email, phone number, and username, including passwordless authentication
  - User management and audit logs help you understand user identity-related information and keep your security on track.

- https://github.com/pilcrowOnPaper/lucia /MIT/ts
  - https://lucia-auth.com/
  - a simple and flexible user and session management library that provides an abstraction layer between your app and your database. 
  - Middleware allows Lucia to read the request and response since these are different across frameworks and runtime
    - 支持express、fastify、nextjs、astro
  - uses adapters to connect to your database
    - 支持mongoose、sqlite、pg、redis、prisma、drizzle-orm、kysely

- https://github.com/keycloak/keycloak /18.4kStar/apache2/202312/java
  - https://www.keycloak.org/
  - Open Source Identity and Access Management solution for modern Applications and Services.
  - This repository contains the source code for the Keycloak Server, Java adapters and the JavaScript adapter.

- https://github.com/casbin/node-casbin /ts
  - https://casbin.org/
  - An authorization library that supports access control models like ACL, RBAC, ABAC in Node.js and Browser

- https://github.com/stalniy/casl /5.4kStar/MIT/202401/ts
  - https://casl.js.org/
  - CASL is an isomorphic authorization JavaScript library which restricts what resources a given user is allowed to access
  - designed to be incrementally adoptable and can easily scale between a simple claim based and fully featured subject and attribute based authorization.
  - Heavily inspired by cancan(from ruby-on-rails).
  - ⚖️ CASL implements Attribute Based Access Control
  - https://github.com/fratzinger/feathers-casl /ts
    - a convenient layer to use CASL in feathers.js.
    - Fully powered by Feathers 5 & CASL 6

## auth-jwt

- https://github.com/rajeshpillai/node-jwt-step-by-step /202005/js
  - A simple express jwt server with vanilla javascript client for testing
  - backend + frontend
# ide-like
- https://github.com/labring/laf /ts
  - https://laf.dev/
  - laf 是开源的云开发平台，提供云函数、云数据库、云存储等开箱即用的应用资源。
  - 让开发者专注于业务开发，无需折腾服务器，快速释放创意。
  - 云函数
  - 云数据库
  - 云存储
  - WebIDE，像写博客一样写代码
  - 网站托管
  - WebSocket 支持
# sass-examples

# more

- https://github.com/yazz/yazz /js
  - Yazz is a both an IDE for building small web applications and a decentralised app store. 
  - Yazz allows you to build Web apps visually. Yazz runs on the web, PC/Mac/Linux (desktop application or NodeJS) or as a container (Docker, Kubernetes).

- https://github.com/stacksjs/stacks /202311/ts
  - https://stacksjs.dev/
  - Type-safe full-stack framework for Artisans
  - The goal of the framework is to help you create & maintain frontends, backends, and clouds
  - Stacks UI: Powered by Bun, Nitro, Tauri, UnoCSS, Vite & Vue
  - Stacks Functions: Develop serverless (or server) functions with countless helpers 
