---
title: lang-js-base-arraybuffer-blob
tags: [arraybuffer, blob, ECMAScript, js, lang]
created: 2022-11-23T17:50:41.004Z
modified: 2022-11-23T17:51:08.635Z
---

# lang-js-base-arraybuffer-blob

# guide

# blogs

## [SharedArrayBuffer以及跨域隔离 - 掘金](https://juejin.cn/post/7184319485107503159)

- SharedArrayBuffer 对象用来表示一个通用的、固定长度的原始二进制数据缓冲区，
  - 类似于 ArrayBuffer 对象，它们都可以用来在共享内存（shared memory）上创建视图。
  - 与 ArrayBuffer 不同的是，SharedArrayBuffer 不能被转移

- SharedArrayBuffer这个对象可以用来在网站的线程之间共享内存数据，
  - 由于JavaScript是单线程的，为了让浏览器能够更好地利用CPU的性能，让代码的编译以及运行效率更好，H5引入了web workers这个API，提供了多线程的使用方式。
  - 在默认情况下多个线程之间的数据是隔离的，如果要是用其他线程的数据，就必须将其复制过来，通过postMessage发送数据，
  - 为了解决这个问题，就出现了SharedArrayBuffer这个对象，这就让线程之间的通信效率变得更高

- 为了应对幽灵漏洞(2018年发现的电脑漏洞，对CPU产生危害)，从2018年开始所有主流浏览器禁用SharedArrayBuffer，在2020年，通过标准化的方法重启SharedArrayBuffer。
  - 而使用对象的前提是，当前页面要**处于安全上下文中，并且跨域隔离的环境中**

- 安全上下文是 Window 与 Worker 中满足了最低标准的身份验证和机密性的概念。
  - 许多 Web API 仅能在安全上下文中访问。
  - 安全上下文的主要目标是防止中间人攻击者访问强大的接口，从而导致更加严重的破坏。
- 怎样的环境才是安全的呢？
- 本地资源
  - 带有 http://127.0.0.1、http://localhost和http://*.localhost 的网址和 file:// 网址的资源
- 非本地资源
  - 必须通过 https:// 或 wss:// URL 提供服务
  - 用于传送资源的网络信道的安全属性不能是废弃的

- 什么是跨域隔离
- 某些漏洞可能会通过一些web API攻击电脑，为了应对这些API带来的风险，浏览器提供了一个隔离环境，也就是跨域隔离，可以通过设置让页面进入跨域隔离环境
- 要进入跨域隔离，就需要在顶层文档的响应头上添加以下两个响应头
  - Cross-Origin-Opener-Policy: same-origin
  - Cross-Origin-Embedder-Policy: require-corp
- Cross-Origin-Opener-Policy简称COOP，它会对当前的文档进行进程隔离，确保顶层文档不会与跨源文档共享同一个上下文它一共有三个值
- Cross-Origin-Embedder-Policy简称COEP，防止文档加载未明确授予文档权限，它有两个值
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
