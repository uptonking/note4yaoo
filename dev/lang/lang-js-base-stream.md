---
title: lang-js-base-stream
tags: [lang-js, stream]
created: 2023-04-11T13:29:37.727Z
modified: 2023-04-11T13:29:56.273Z
---

# lang-js-base-stream

# guide

- [Node Stream流核心机制理解 - 掘金](https://juejin.cn/post/7115043225944981535)
# more

# discuss-stars

- ## 

- ## 

- ## [Show HN: Durable Streams – Kafka-style semantics for client streaming over HTTP | Hacker News _202512](https://news.ycombinator.com/item?id=46209189)
- what's the relationship between Durable Stream and CRDT, are they replacements for one another, or can they work well together?
  - Durable Streams are a lightweight network protocol on top of standard HTTP. When you are building a synchronisation layer for let's say a local-first app, you need to not only exchange data over some lower-level protocol (i.e. HTTP / SSE / WS), but you also have to define a higher-level protocol on how the client & server are going to communicate - i.e. how to resume data fetching once the client reconnects, based on the last data that the client received (~offset). Since the reconnect & offset should be automatically handled by the Durable Stream, you could just build your domain logic on top of it.
  - CRDTs are primarily meant to resolve data conflicts, usually client-side, based on a defined conflict resolution strategy (i.e. last-writer-wins). Some of the CRDT libraries, like automerge, loro or yjs, also implement a networking layer to exchange the data between nodes (could be even P2P), meaning they already have a built-in mechanism for reconnection and offset (~send me data since X). However, nobody forces you to use their networking layer, meaning that with Durable Streams, you would have a good starting point to build your own.
- Great answer! I was always confused about how CRDTs were transferred. Like you said, existing implementations often come with their own in-house networking solutions. Now it's totally clear, since CRDTs are only about data, it's no wonder their transfer methods differ. That makes Durable Stream a very good companion to work with CRDTs—the boundaries are clear, and they complement each other perfectly.
  - I also feel that I could give Durable Stream's protocol spec to a coding agent, and it could blend into the best suited implementation for my current project (say, a Go repo). The simple yet sophisticated spec is more valuable than a bunch of SDKs.

- ## 🚀 Today we're open-sourcing Durable Streams: a persistent stream primitive and HTTP protocol for reliable, resumable, real-time data streaming to clients. _20251210
- https://x.com/ElectricSQL/status/1998456703793471916
  - [Announcing Durable Streams | ElectricSQL _20251209](https://electric-sql.com/blog/2025/12/09/announcing-durable-streams)
  - We built it inside Electric. Now we're standardizing it as a standalone protocol.
  - The problem: Server-to-server messaging is solved. Kafka, RabbitMQ, NATS—battle-tested, boring infrastructure.
  - Client streaming? Still broken.
  - WebSockets and SSE connections are fragile. Tabs suspend. Networks flap. Pages refresh. When connections break, you lose data or build bespoke resume logic.
  - The fix: streams become a first-class primitive with their own URL.
  - Each stream is an addressable, append-only log. 
  - Clients read from any position using opaque, monotonic offsets.
  - No server-side session state. Progress tracked client-side.
- Why HTTP matters:
  - Works everywhere: browsers, mobile, native, IoT
  - Offset-based URLs = CDN-cacheable historical reads
  - Fan out to millions of clients without origin bottleneck
  - Fits behind standard API gateways
  - No WebSocket complexity. No sticky sessions.
- How it works:
  - PUT to create, POST to append (returns next offset)
  - GET to read/resume from any offset Long-poll or SSE for live tail JSON mode preserves message boundaries
  - Plain HTTP. Resumable. Replayable.
- This is the foundation of Electric 2.0's composable architecture:
  - Foundation: Durable Streams (today)
- Coming soon:
  - State Protocol (insert/update/delete semantics)
  - Database adapters (Postgres, MySQL, SQLite)
  - AI transport plugins (Vercel AI SDK, TanStack AI)
- In the repo:
  - ✓ Reference Node.js server
  - ✓ TypeScript clients
  - ✓ CLI for testing
  - ✓ Conformance test suite
  - We want many implementations—Python, Go, Rust, Swift, Kotlin—and different storage backends. The test suite ensures compatibility.

- This is very interesting, does it solve for various enterprise proxies buffering streams? We had to previously implement websockets fallback to SSE because ent proxies buffered the whole response and returned it as one chunk.
  - yeah SSE falls back to long-polling — which is very fast too, just a bit choppier than SSE for very fast updates because of the RTT every time there's an update (e.g. for token streaming SSE is noticeably smoother).

- I think a comparison with @s2_streamstore would be useful.(s2 基于 slatedb/rust)

- Low latency (long polling) and high concurrency (CDN) seem at odds. For request collapsing to work, clients would have to re-poll in near lockstep on the same cursor/offset. With global jitter + lag, polls de-sync fast—so you still hit origin w/ tons of requests.
  - we've tested to millions of connected clients so it seems fine? And yes, the higher the concurrency, the less likelihood that people would hit the same offsets but still there'll be plenty of overlap.
  - We've explored ways to ensure clients are more likely to overlap but it's not been an issue to date so haven't gone further.

- Very cool. Also, the server side storing of the messages per stream seems to be an exercise left for the reader (makes sense as this is a protocol). Any guidance on that part?
  - each stream is an immutable log — so file per stream works great (which is how the ref implementation does it) but anything really would work at many scales — dbs, redis, etc. for huge scale (what we're doing on electric cloud) you ned object storage.
  - we're hoping to kickstart some implementations with other groups that have production-ready pluggable storage options

- https://x.com/cramforce/status/1998798451681919377
  - resumeable-stream obviously a massive reference point and the primary way of solving reliability and resumeability with the Vercel AI SDK atm.

- https://x.com/kylemathews/status/1998461754712441038
  - Electric Cloud delivers millions of state changes a day over our durable streams protocol — so we're splitting it out so it can be used for any transport/sync use case. 
  - It's a really unique and scalable plain-http protocol that solves a lot of problems we see in AI/real-time.

- https://x.com/joelhooks/status/1999886451270676956
  - I've been struggling with agent mail (as mcp versus cli) and want a more "native" approach so building out a typescript variant using pglite and the Durable Streams spec to facilitate agent coordination in swarm
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Your API needs to process huge JSON payloads (5–20 MB) from clients. How do you design it so parsing alone doesn’t choke your CPU?
- https://x.com/SumitM_X/status/1999107796131094714
- Offer NDJSON (newline-delimited JSON) + client-side chunking so the server can stream-parse record by record and ack/checkpoint offsets for resumable ingest.

- Use streaming JSON parsing so you process chunks as they arrive instead of loading the whole payload into memory. Offload heavy processing and consider compression or binary formats for efficiency.

- Use a streaming JSON parser (like JSONStream in Node.js or Jackson Streaming in Java) to process the data in chunks instead of loading the full object into memory. This prevents blocking the main thread and keeps your memory footprint low.

- Stream parsing with something like streaming JSON libraries, async processing, and maybe request size limits. Also consider gzipping payloads before sending. What's your current bottleneck?

- ## Writing Node Stream + Web Stream compatible code is really really annoying.
- https://x.com/tannerlinsley/status/1882171811137528008
- If you can, rely on web streams as both are supported everywhere. 
  - If you can't, use the .fromWeb()/.toWeb() methods on Node's Readable and Writable. They do what you think they do.
- Node streams are more performant, but you are the best judge of the performance/compatibility balance.
  -  there are use cases for both, but standard-first is certainly the default. 

- Neither Node streams nor `readable-stream` can run in the browser, which defeats compatibility. I get it that the spec isn't perfect and, perhaps, even flawed. But compatibility goes a long way
  - readable-stream should work in browsers

- We rely on web streams in MSW across the board for compatibility reasons, which is a top priority for an environment-agnostic tool.

- ## People don't understand how many optimizations are lost by exposing Request.body/Response.body
- https://x.com/KhafraDev/status/1882825305200763280
- But this is a standard, no? 
  - They were added a significant amount of time after Request, Response, and the body mixins. Exposing `.body` causes a cascade of webstreams (similar to `async` ): you cannot selectively choose when to use webstreams once it is exposed.

- ## Reading a response body in chunks and stopping the readable stream the moment I got the needed info feels like superpowers.  
- https://x.com/kettanaito/status/1824029571630412272
- What is the difference between this and ArrayBuffer?
  - Those `value` chunks are ArrayBuffer! Just chunked, which means they are streamed in pieces as the response body is being read. Using something like `await response.arrayBuffer()` will do something similar to what I showed above but will read the entire body at once.
  - In fact, all the convenience body reading methods like `.arrayBuffer(), .json(), .formData()` , etc. are wrappers around consuming the `ReadableStream` , which is `response.body` .
- That's how some high-frequency trading code works. You don't parse a JSON response because it takes time; you go directly to the offset where the number you're looking for will likely be
- In Node, reading the whole body is important to avoid memory leaks.
- Does the reader not implement async iterator? Then you could replace the `while(true)` with `for await (...)`
