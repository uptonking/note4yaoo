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

- ## 

- ## 

- ## Reading a response body in chunks and stopping the readable stream the moment I got the needed info feels like superpowers.  
- https://x.com/kettanaito/status/1824029571630412272
- What is the difference between this and ArrayBuffer?
  - Those `value` chunks are ArrayBuffer! Just chunked, which means they are streamed in pieces as the response body is being read. Using something like `await response.arrayBuffer()` will do something similar to what I showed above but will read the entire body at once.
  - In fact, all the convenience body reading methods like `.arrayBuffer(), .json(), .formData()` , etc. are wrappers around consuming the `ReadableStream` , which is `response.body` .
- That's how some high-frequency trading code works. You don't parse a JSON response because it takes time; you go directly to the offset where the number you're looking for will likely be
- In Node, reading the whole body is important to avoid memory leaks.
- Does the reader not implement async iterator? Then you could replace the `while(true)` with `for await (...)`
