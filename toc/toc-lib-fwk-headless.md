---
title: toc-lib-fwk-headless
tags: [fwk, headless, toc]
created: 2021-05-24T16:55:24.630Z
modified: 2021-05-24T16:55:40.481Z
---

# toc-lib-fwk-headless

# guide

- rest api本身就是headless的设计
- 国内有很多快速开发框架如jeesite/jeecg，国外对应的是headless/cms框架
  - https://github.com/n370/awesome-headless-cms
# popular
- strapi /36.7kStar/MIT+EE/202105/js
  - https://github.com/strapi/strapi
  - 核心功能是提供了通过ui操作实现rest api的功能
    - 系统内容通过ui操作编写
    - 系统前端strapi没有限制，strapi只提供了api
  - Open source Node.js Headless CMS to easily 
  - The original purpose of the project was to help Bootstrap your API
  - Now, Strapi is an open-source headless CMS that gives developers the freedom to choose their favorite tools and frameworks and allows editors to manage and distribute their content using their application's admin panel.

- refine /2.6kStar/MIT/202208/ts
  - https://github.com/pankod/refine
  - https://refine.dev/
  - refine is a React-based headless framework for building data-intensive applications 
  - t ships with Ant Design System and Material UI
  - refine is a headless React framework, 
    - which means all out-of-the-box features such as Routing, Networking, Authentication, Authorization, State Management, Realtime, i18n, etc. can be used without being tied to any UI element or framework. 
    - Also, Ant Design as out-of-the-box is supported.
  - refine makes extensive use of hooks as a default way for interacting with your components. 
  - refine relies heavily to React Query for data handling, caching and state management. 
  - Backend Agnostic : Connects to any custom backend. Built-in support for REST API, GraphQL

- https://github.com/kontenbase/kontenbase /202209/ts/inactive
  - https://kontenbase.com/
  - no code backend API platform/Backend as a Service (BaaS)
  - 依赖 centrifuge
  - https://github.com/centrifugal/centrifugo /202212/go
    - Scalable real-time messaging server in a language-agnostic way
    - [Centrifugo vs RabitMQ · Issue #126 · centrifugal/centrifugo](https://github.com/centrifugal/centrifugo/issues/126)
    - Centrifugo's goal is delivering real-time messages to end users of your application with at most once delivery model (fire and forget in general). 
    - Centrifugo is just a PUB/SUB server designed for client applications, it's not suitable for usage on backend side - for example to coordinate microservices. 
    - Rabbit can be used as queue, PUB/SUB broker etc.
# headless-platfrom
- https://github.com/TencentCloudBase/cloudbase-extension-cms
  - https://docs.cloudbase.net/cms/intro.html
  - 依赖 Node.js + Nest.js + CloudBase
  - CloudBase CMS 是由腾讯云开发推出的，基于 Node.js 的 Headless 内容管理平台
  - 基于模板配置生成内容管理界面，无须编写代码
  - 支持 Webhook 触发，可以方便的与外部系统集成
# more-headless
