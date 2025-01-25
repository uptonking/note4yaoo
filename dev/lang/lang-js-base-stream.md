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

# discuss

- ## 

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
