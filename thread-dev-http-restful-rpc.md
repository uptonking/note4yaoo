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
# discuss-protobuf
- ## 

- ## Unpopular opinion: use Protocol Buffers, not because the format is that great (it isn't), but because the range of supported languages for codegen can't be beat.
- https://x.com/JustDeezGuy/status/1917589307113537664
  - Further unpopular opinion: Protocol Buffers plus named pipes (Windows) or UNIX-domain sockets (everything else) are a great IPC mechanism for isolated processes on single hosts.

- Protobuf supports twice as many languages as ASN.1 out of the box, with another five times as many languages covered by third parties.

- 1M$ idea: protocol buffers, but with off-heap memory IO bypassing and RDMA

- The one thing protobufs do really badly is having a bunch of optional fields.  At some point of complexity, sending protobufs directly over the wire gets worse than using a dedicated streaming bus with a schema registry.

- Convince me to use protocol buffers over raw binary blobs.
  - You’ll need to come up with a mapping from those binary blobs to data structures in your code, provide some means of managing the evolution of those structures, account for the possibility of different versions interacting at the same time, etc. The point isn’t Protobuf per se, 

- Protobuf alone *could* be fine, but these technologies come with strings attached as they were designed for server apps and utterly suck for local user apps.

- ## 遇到一个 Protocol Buffers in JS 的坑：.proto float 会导致 JS number 精度丢失。
- https://twitter.com/ThaddeusJiang/status/1749662021535289653
- 类型系统：
  - DB: Float
  - JS: number
  - proto: float
- 两种解决方案：
  1. proto: float -> string 以字符串作为交换格式
  2. proto: float -> double 依然以浮点数为交换格式，只是增加浮点数精度

- ## 🆚️ Is there anyone here who is using Protocol Buffers as the format of their Kafka records? 
- https://twitter.com/gunnarmorling/status/1747197582244200913
  - How has your experience been, and what made you pick protobuf over Avro?
- Protobuf is VERY popular in my experience, likely exceeding avro. Personally, I'm all for Avro and msgpack. Both provide better runtime adaptability without as much code generation.

- Avro without schema registry is terrible in terms of backwards compatibility. Protobuf is much better/easier in this. Also, with protobuf, one can easily employ nice partial deserialization tricks 

- Avro needs the encoding schema to deserialise, so with Kafka that implies the use of a schema registry. I’m sure it’s better now, but CSR used to be a massive point of friction. +1 for protobuf and @bufbuild

- We use pb for its compatibility guarantee and multiple language support."Everyone uses schema registry" is simply not true for us because we hesitate to adopt it to avoid introducing another point of failure. (also it brings local testability issue IMO)
- How do you exchange schemas between producers and consumers?
  - Just git

- We use Protobuf for sending app events to Kafka and on the downstream use Spark 3.4 which now has support for parsing protobuf messages using descriptor files. We also keep the protobuf schema on Confluent schema registry. Upwards of 500M+ events per day.

- We use protobufs for Kafka (we didn't use Avro in this project). We don't share schema, instead we use protos in a way that respects its clear rules to backward compat. We also have lots of gRPC around so it's natural/easier to use the same serialization (some shared serdes etc)

- ## 🤼🏻 protobuf's strength lies in its interface definition language, which makes communication between components owned by different teams easy, but it wasn't designed for performance
- https://twitter.com/eatonphil/status/1740057705124139069
- I'm working on a Go package, which will provide simple building blocks for fast zero-alloc marshaling and unmarshaling of protobuf messages with arbitrary nesting and complexity. This package will be used in @VictoriaMetrics source code initially.
- Protobuf is jack-of-all-trades. It doesn't have to be the fastest. Also one place where it really shines is schema evolution and how tolerant it is for backward-/forward-compatibility.
- At Google they use arenas for allocating protobufs to avoid overhead, but this isn't in any of the gRPC libraries. I do prefer the pb IDL to flatbuffers/capnp, but the overhead from allocations is like 99.99% of our profiles, and we even use better codegen: vtprotobuf
- This is where https://capnproto.org shines

# discuss-graphql
- ## 

- ## 

- ## 

- ## 除非你有很特别的需求，100% 确定 GraphQL 非常适合，否则 RESTful API 足够你使用
- https://twitter.com/beihuo/status/1775960603858960630
  - 因为 GraphQL 会引入大量的复杂性，比如如何做缓存，如何做 rate limit。
  - 最后你会发现你可能还需要引入 federation，事情一下子变了。各个语言和框架的实现，又是一个坑。
- 还有细粒度数据安全的问题（不知道是不是你说的federation包括了这个）

- https://twitter.com/zhdsuperman/status/1776301948914090407
  - fb 没给 db 抽象实现，社区的实现各个语言质量差异太大了，版本化、鉴权、限流、安全、参数校验、测试，gateway 到 db 都要大改，就为了客户端请求调用方便一点，收益太小了。
# discuss
- ## 

- ## 

- ## 

- ## 🆚️ REST APIs are outdated. GraphQL is overrated. Just send JSON over WebSockets and be done with it
- https://x.com/_trish_07/status/1901695896745914395
- Real devs just send raw binary over UDP and pray it reaches

- I’m guessing you don’t waste time with databases either, just flat file your data and when a user needs something push it over the web socket

- The real solution is managing events on a pub/sub broker. You can still use JSON for the payload.

- ## 🪧 REST API Cheatsheet
- https://twitter.com/sahnlam/status/1768159055229723063
  - six fundamental principles of REST API design
  - Key components like HTTP methods, protocols, and versioning
  - Practical tips on pagination, filtering, and endpoint design

- ## gRPC is gaining popularity for service-to-service communication. Here's why:
- https://twitter.com/sahnlam/status/1738787868414550072
  - Speed - gRPC is built on HTTP/2 and Protobufs for maximum throughput and minimal latency. Much faster than JSON over HTTP.
  - Efficiency - The compact Protobuf binary format means smaller payloads than JSON. Less data sent = better performance.
  - Type Safety - Protobufs are strongly typed, eliminating many bugs.
  - Polyglot - Write services in many popular languages, the IDL works across them all.
  - Streaming - gRPC supports bidirectional streaming for real-time data transmission.
  - Great Ecosystem - Tons of tools exist for code gen, load balancing, monitoring, and more.
- gRPC has some drawbacks:
  - More Complex - Defining Protobuf schemas and setting up gRPC can have a learning curve.
  - Not Human Readable - Protobufs are binary, so not as easy to troubleshoot as JSON. Tools like grpcurl a little bit.
  - Limited Browser Support - gRPC works best for backend microservices, not front-end apps.
- For most backend use cases, gRPC delivers an efficient, robust and high-performance communication framework perfect for modern microservices.

- Another drawback: Scaling requires proxy servers to support grpc as well

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
