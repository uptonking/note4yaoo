---
title: lang-js-base-arraybuffer-blob
tags: [arraybuffer, blob, ECMAScript, js, lang]
created: 2022-11-23T17:50:41.004Z
modified: 2022-11-23T17:51:08.635Z
---

# lang-js-base-arraybuffer-blob

# guide

# examples
- https://github.com/zandaqo/structurae
  - A collection of data structures for high-performance JavaScript applications 
  - simple binary protocol based on DataView and defined with JSONSchema
  - making web apps using an objects backed by TypedArrays for much less memory allocation.
# discuss
- ## 

- ## 

- ## 

- ## Has anyone written anything in depth outlining the mental model you should use when passing things between node and napi-rs, 
- https://twitter.com/adamwathan/status/1615500615236616192
  - and how to have a good sense for what’s fast/efficient and what’s a bad idea?
  - Like when to do one call with lots of data vs many calls with little data.
- 👉🏻 Use buffers instead of strings. Strings have to be copied to and from the JS heap, buffers can be accessed directly with no copies.
  - Try to avoid creating lots of objects if you can. It's like 25x slower to create objects from native than in JS.
  - Function calls between JS and native can also be expensive in napi, in either direction. So don't be too chatty - send a bunch of stuff to Rust in one call and do as much as you can without calling back to JS.
  - Along with buffers, you can also use numbers instead of strings in a lot of cases. Like if you have a property that takes string enum, convert to a number on the JS side before passing to native to avoid a string copy (and vice versa).
- So function signature in rust accepts `napi::Buffer` and node uses `TextEncoder.encode()` to create the buffer before passing it in? Is that the fast path?
  - Ideally you'd never create a string in the first place. For example, if you read content from a file, you can read it directly to a Buffer rather than a string.
- And if possible, don't just *use* buffers, but *reuse* buffers. Creating new buffer instances (both in JS and in NAPI) is quite expensive, so if you can reuse a single (or set of) buffer to transfer data between rust & JS, that can be extremely fast.
- What is it exactly that makes the function calls expensive, like what variables about the call affect how expensive it is? And when you say object, do you mean creating something in Rust that will be returned to node as a JS object? What’s a better way to return structured data?
  - For the small-size structs, just return the #[napi(object)] decorated struct. For large-size structs, I’ll suggest serializing it into a JSON buffer using serde_json::to_vec and deserializing it in JavaScript using JSON.parse

- 👉🏻 Always do one call with zero copied big data. There is significant overhead on the Node-API call and it will prevent the engine from optimizing the JavaScript codes that contain the Node-API call

- Blind shot here but I would likely go for big data, little calls. I would say that the overhead of calling a FFI function (Node -> Rust) is higher than the buffer speed.
