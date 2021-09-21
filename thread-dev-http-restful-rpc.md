---
title: thread-dev-http-restful-rpc
tags: [graphql, http, restful, rpc, thread]
created: '2021-09-20T18:37:02.986Z'
modified: '2021-09-20T18:38:00.319Z'
---

# thread-dev-http-restful-rpc

# discuss

- ## What is tRPC?
- https://twitter.com/t3dotgg/status/1438434802839945220
  - tRPC is a genius abuse of Typescript to create a typesafe API on server and client with strong inference and validation.
  - defining server queries and mutations has never been easier.
  - By using TS type defs generated "from the server code", the client is able to AUTO COMPLETE EVERY ENDPOINT AND INFER TYPES CORRECTLY.
- Why should I care?
  - Sharing type definitions in a statically typed system between client and server is incredibly hard to beat.
  - I can change a field's name in DB and get errors where it's used on frontend. The 'surface area' from data -> user is tiny. Debugging is so easy.
- Why not GraphQL?
  - it's heavy.
  - React Query already got me 70% of what I wanted from gql (caching, query invalidation, etc). tRPC gets me the last 30% (and makes backend more fun too)
- Why not Blitz.js?
  - If I was starting up a new web-only project with a team, I'd likely use Blitz. 
  - Main reasons I didn't for this:
    - Only wanted the type validation
    - Bought into NextAuth.js
    - tRPC can be added to existing Next.js app, Blitz would be full replacement
