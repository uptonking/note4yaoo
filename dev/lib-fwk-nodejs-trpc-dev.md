---
title: lib-fwk-nodejs-trpc-dev
tags: [backend, nodejs, trpc]
created: 2022-11-03T09:43:13.833Z
modified: 2022-12-19T01:49:43.776Z
---

# lib-fwk-nodejs-trpc-dev

# guide

- features
  - Full static typesafety & autocompletion
  - No code generation, run-time bloat, or build pipeline.
  - Framework agnostic with adapters
  - Subscriptions support - Add typesafe observability to your application.
  - Request batching - Requests made at the same time can be automatically combined into one.

- pros
  - 前后端复用类型

- cons
  - 前端代码和后端代码部分耦合，难以拆分
  - 框架对代码的侵入性非常高
  - designed for monorepos，分离的仓库暂未提供复用方案
  - rpc的风格，基于json-rpc，不如rest主流

- tips
  - 简单验证poc原型可直接express+orm，计划长期时选择trpc框架
