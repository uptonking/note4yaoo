---
title: lib-fwk-nodejs-trpc-community-stars
tags: [community, nodejs, trpc]
created: 2022-11-03T09:47:18.670Z
modified: 2022-12-19T01:51:13.255Z
---

# lib-fwk-nodejs-trpc-community-stars

# guide

# discuss
- ## 

- ## 

- ## TRPC: End-to-end typesafe APIs made easy (trpc.io)_202202
- https://news.ycombinator.com/item?id=31285827
- a brief explanation
  - It's designed specifically for a full-stack TypeScript app. Your API is implemented as strongly typed server-side functions.
  - The input type is specified using a schema library like Zod or io-ts.
  - TypeScript infers the return type of these functions.
  - You can then import the type signatures of your functions into your client. Just types, no runtime code! This is safe in typescript with the `import type` syntax.
- You can do this with GraphQL but it relies on code-generation, requires complete buy-in, and (IMO) doesn't provide a great developer experience. 
  - Without tRPC, it's common to manually provide type definitions for the results of API calls. 
  - But those definitions can easily get out of sync with your actual server code. 

- Does this work with NestJS?
  - It can be made to work with any framework with a proper adapter. NestJS is quite opinionated though so I suspect the two will not work well together.

- ## Using with Nest. Js_202202
- https://github.com/trpc/trpc/discussions/1504
- None of the maintainers of tRPC are users of nestjs. Therefore, we have no plans on putting in more unpaid work to support nestjs
