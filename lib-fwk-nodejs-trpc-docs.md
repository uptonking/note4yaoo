---
title: lib-fwk-nodejs-trpc-docs
tags: [backend, docs, trpc]
created: 2022-11-03T09:46:36.127Z
modified: 2022-12-19T01:49:50.959Z
---

# lib-fwk-nodejs-trpc-docs

# guide
- trpc /14.8kStar/MIT/202211/ts
  - https://github.com/trpc/trpc
  - https://trpc.io/
  - tRPC allows you to easily build & consume fully typesafe APIs, without schemas or code generation.
  - tRPC has zero deps and a tiny client-side footprint.
  - Batteries included - React.js/Next.js/Express.js/Fastify adapters. (But tRPC is not tied)
# blogs

## [Building an end-to-end typesafe API — without GraphQL, poc_202106](https://colinhacks.com/essays/painless-typesafety)

- With a REST APIs, you use different URLs (/users, /user/:id) and HTTP request types (e.g GET, POST, etc) to access different functionality. For instance GET /users will fetch all users, GET /user/abc123 will fetch a single user, and POST /user will create a new user.
- RPC strips all of that away. Endpoints are just named functions that accept some arguments and return a value. The RPC ethos is to make API calls look and feel like calling a function (albeit one that's defined on a remote server).
- GraphQL is an RPC protocol that's been augmented with a schema language and a mechanism for client-side field selection.
# more
- [A Brief History of API: RPC, REST, GraphQL, tRPC](https://dev.to/zenstack/a-brief-history-of-api-rpc-rest-graphql-trpc-fme)
  - REST. So the most advantage it has is simple and intuitive. It uses a standard HTTP method and resource centralized way to define API 
  - Although it is called RPC, it only inherits the concept to call the remote function locally but in a more pure way that doesn’t have the IDL file and the code generation process.
