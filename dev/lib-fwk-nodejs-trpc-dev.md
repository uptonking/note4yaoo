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
# dev-log

# dev-xp
- 
- 
- 
- 

- TRPCClientError: No "query"-procedure on path "thread.importRepo"
  - 原因是 useUtils返回的api只能发送GET请求，不能发送POST请求

- [reactjs - All my TRPC queries fail with a 500. What is wrong with my setup? - Stack Overflow](https://stackoverflow.com/questions/75227309/all-my-trpc-queries-fail-with-a-500-what-is-wrong-with-my-setup)
  - using the context you can pretty much do anything from anywhere
  - If your procedure is a mutation, it's trivial, so maybe you can turn your GET into a POST

- [Way to fire requests using `useQuery` with an input `onChange`? · trpc/trpc ](https://github.com/trpc/trpc/discussions/2067)
  - `const value = await utils.namespace.myQueryFunction.fetch();`

- [Allowing prefetch outside of component but still client-side? · trpc/trpc ](https://github.com/trpc/trpc/discussions/3148)

- [TRPCClientError: Unexpected non-whitespace character - NextJS 14 App router · Issue #15 · RJPearson94/terraform-aws-open-next](https://github.com/RJPearson94/terraform-aws-open-next/issues/15)
  - 原因是前端请求的url错误，多了一个斜杠` //workspaces/list`
# more
