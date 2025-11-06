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

- ## gRPC has to be the worst protocol I've ever used.
- https://x.com/davydog187/status/1985780359921885553
  - Want errors? Cool, here's a dozen standard error codes.
  - Want arbitrary data in your errors? Oh, well, you can't do that
  - BUT if you use a Google extension, you can Base64 the error and then write a decoder to extract it 

- got something you like that is better?
  - Still a big fan of ole JSON over HTTP

- Wait of course you get full support for custom and rich typed errors. They're called messages. If your protocol needs rich errors, explicitly encode then in your response schema.
  - The reason there isn't a general purpose error path is that not all protocols require errors. For the protocols that do, it's better to allow the protocol to define its own context specific error schema.

- Oh so base64-ing payload is coming from grpc. I have seen people encoded JSON over HTTP payload to base64 and it let me baffled. Now I know the (stupid) reason.

- https://x.com/_Felipe/status/1985893018482983104
  - I’m a big fan of just passing protobuf objects over HTTP and using the full HTTP protocol functionality instead of using it through the generated RPC interface.
  - One nice aspect of this approach is that you can make it so that when requests have Accept: application/json you can have the server automatically convert the protobuf response to JSON.
- You would need something like gRpc for full duplex streaming and backpressure.
  - You would only need HTTP/2 or HTTP/3 but I agree that using gRPC simplifies the implementation of streaming and back pressure if you can take all the limitations and complexity that gRPC impose on you.

- I do the same using Arrow or Arrow+msgpack instead of protobuf
  - I have blogged about this. You can have a server that allows clients to opt-in to different Arrow compression schemes using standard HTTP constructs.

- Protobuf over HTTP definitely has its perks, especially with flexibility in error handling. Interested to see how Arrow compares for your use cases.
  - Accept: application/vnd.apache.arrow.stream; codecs="lz4, zstd"
  - For tabular data. When your response is a single, potentially deeply nested object, protobuf is a better fit.

- Yeah I've done this in the past returning either binary or json encoded pb data, it's much simpler.

- ## xml-rpc的schema太扯淡，protobuf又不适合手写，所以有了中间产物json-rpc，主要就是讲究个简单方便省时省事。
- https://x.com/geniusvczh/status/1900708477250793559
- 用xml还是json都不应该有区别，因为soap本来就是围绕着代码生成器建立的，你根本不需要亲自去parse中间的protocol

# discuss
- ## 

- ## 

- ## Protobuf is great for explicitness but every API surface it touches become highly verbose. 
- https://x.com/rakyll/status/1985919404471996493
  - In the early days of Go, people used to say that Go looked beautiful until proto generated clients took over the ecosystem.
  - In my opinion, protobuf unwillingly encourages deep nested types and very verbose message names. Oneofs  look verbose/complex from client's perspective. There is a whole ecosystem around annotations which sometimes cause duality.
- plus is a very strong and inflexible coupling point for any API consumer. protobufs become inmutable as soon as they have external clients. they are much better as internal representations, imho.

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
