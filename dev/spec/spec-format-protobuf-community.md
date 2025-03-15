---
title: spec-format-protobuf-community
tags: [community, protobuf]
created: 2024-11-17T10:22:44.639Z
modified: 2024-11-17T10:22:56.761Z
---

# spec-format-protobuf-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️ I was crunching some numbers for JSON vs protobuf and the difference is staggering.
- https://x.com/arpit_bhayani/status/1857840494283468825
  - 2x improvement in data size
  - 2.5x improvement in serialization time
  - 4.5x improvement in deserialization time
  - no wonder protobuf has become a de-facto data format.

- But generally it is suggested to use protobuf only for inter-server communication not directly for clients. Is there any specific reason for it? Like why json is still preferred for browsers not protobuf if it is so advantageous
  - Because you spend a ton of time moving data/req/res over public internet (long distances) and the network latency overpowers the performance again of serialisation and deserialization.

- it's clear how significant network latency can be compared to JSON serialization/deserialization
  - Pinging https://google.com takes ~10 ms, about 1000 times more than the JSON serialisation/deserialisation time mentioned in @arpit_bhayani 's post

- Because browsers don't have native support for protobuf. Protobuf is recommended and designed to use for backend to backend

- If you think that’s fast, check out FastBinaryEncoding

- would be interesting to see benchmarks in comparision with simd json parser

- BJSON would perform much better but yeah not as good as protobuf.
# discuss-grpc
- ## 

- ## 

- ## xml-rpc的schema太扯淡，protobuf又不适合手写，所以有了中间产物json-rpc，主要就是讲究个简单方便省时省事。
- https://x.com/geniusvczh/status/1900708477250793559
- 用xml还是json都不应该有区别，因为soap本来就是围绕着代码生成器建立的，你根本不需要亲自去parse中间的protocol

# discuss
- ## 

- ## 

- ## 

- ## 🌰 Recently, LinkedIn Engineering shared how they used Protocol buffers (ProtoBuf) to improve performances by up to 60% _202403
- https://twitter.com/milan_milanovic/status/1772898221972500759
  - gRPC is a high-performance, open-source, and universal remote procedure call (RPC) framework developed by Google. 
  - It uses Protocol Buffers (protobuf) as its interface definition language.
  - Protocol Buffers are compact binary serialization formats for structured data. 
  - They offer advantages like smaller size and faster processing than traditional JSON or XML.
- Advantages of gRPC:
  1. Speed: Thanks to HTTP/2, gRPC is faster and more efficient than REST over HTTP/1.1.
  2. Polyglot: Provides tools to generate client and server code in many languages.
  3. Streaming: Supports bidirectional streaming, allowing for more interactive real-time communication.
  4. Deadlines/Timeouts: Built-in support ensures requests don't hang.
  5. Ecosystem: Supports authentication, load balancing, retries, etc.
- Drawbacks of gRPC:
  1. Complex: Requires understanding of Protocol Buffers and the gRPC API.
  2. Limited Browser Support: Native browser support is limited due to reliance on HTTP/2.
  3. Tooling: While growing, gRPC tooling is less mature than REST's.
  4. Not human-readable: Because they are binary, they are not easy to debug like text-based formats (such as XML or JSON).
