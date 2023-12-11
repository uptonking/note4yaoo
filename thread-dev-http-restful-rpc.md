---
title: thread-dev-http-restful-rpc
tags: [graphql, http, restful, rpc, thread]
created: 2021-09-20T18:37:02.986Z
modified: 2021-09-20T18:38:00.319Z
---

# thread-dev-http-restful-rpc

# guide

- solutions
  - [Arrow Flight RPC — Apache Arrow](https://arrow.apache.org/docs/format/Flight.html)
# discuss
- ## 

- ## 

- ## gRPC 竟然擅自把空数组变成了 undefined，减少数据传递，提供性能
- https://twitter.com/ThaddeusJiang/status/1734034431285886990
  - 实际上，为了节省 2 个字符增加了很多黑盒，造成 server 和 client 看到的数据不一样，极易产生 bug。
- 这算feature，但感觉array的默认配置最好是true，但现在默认是false了

- ## Forward Proxy vs Reverse Proxy
- https://twitter.com/hackinarticles/status/1710756805037445619

- ## A big optimization that could be added to @trpcio
- https://twitter.com/fabiospampinato/status/1692653720306151712
  - To send a file to the server today you need to read the entire file in memory, encode it as base64, encode that as json, then parse the json, parse the base64, and have it all in memory. All of that is wasted time basically.

- Instead, I think it could work like this:
  - Make a stream for the file.
  - Check if the RPC call contains a single stream or buffer, if so special-case this RPC call.
  - Everything except that is put in a special http header.
  - Send the stream/buffer as the body of the request

- That should be like arbitrarily faster, the bigger the file the greater the improvement.
  - No base64 encoding.
  - Much smaller encoded json payload.
  - Much smaller decoded json payload.
  - No base64 decoding.
  - No need to put the entire thing in memory at once either.

- Actually maybe something like this can even be generalized to an arbitrary number of streams/buffers per call. Like each of those could be replaced with a special token that says "I'm going to send this to you with the followup call with id [...]" or something like that 

- It already can do something like this for the experimental `FormData` support, there’s just more work to be done on supporting non-json content types before it will be production ready - probably from v11 due to a breaking change we discussed needing
  - For now the best way to transfer a file is to use a signed URL for uploads and downloads to a separate storage service. Base64 is a really bad idea for scalability

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
