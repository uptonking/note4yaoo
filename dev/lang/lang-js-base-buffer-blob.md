---
title: lang-js-base-buffer-blob
tags: [arraybuffer, blob, ECMAScript, js, lang]
created: 2022-11-23T17:50:41.004Z
modified: 2023-11-10T07:30:17.500Z
---

# lang-js-base-buffer-blob

# guide

- tips
  - [Sparse arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#sparse_arrays)
# blogs

## [一文带你学会 Blob（含 7 个使用场景）](https://xie.infoq.cn/article/9974df9a229e5c28679c77773)

- Blob（Binary Large Object）表示二进制类型的大对象。在数据库管理系统中，将二进制数据存储为一个单一个体的集合。
  - Blob 通常是影像、声音或多媒体文件。
- 在 JavaScript 中 Blob 类型的对象表示不可变的类似文件对象的原始数据。 

- Blob使用场景
  1. 图片本地预览
  2. 图片本地预览 + 分片上传
  3. 图片本地预览 + 分片上传 + 暂停 + 续传
  4. 从互联网下载数据
  5. 下载文件
  6. 图片压缩
  7. 生成 PDF 文档

- [Blob对象](https://github.com/pfan123/Articles/issues/10)
  - 在使用 preloadJS处理加载问题时，我们可以绕过其他方式跨域
  - 隐藏视频源路径
  - Web Worker 串行加载优化
  - 使用 createObjectURL(blob) 输出页面，移动端长按保存，转发

- Blob 与 ArrayBuffer 的区别
- ArrayBuffer 对象用于表示通用的，固定长度的原始二进制数据缓冲区。
  - 你不能直接操纵 ArrayBuffer 的内容，而是需要创建一个类型化数组对象或 DataView 对象，该对象以特定格式表示缓冲区，并使用该对象读取和写入缓冲区的内容。
- Blob类型的对象表示不可变的类似文件对象的原始数据。
  - Blob 表示的不一定是 JavaScript 原生格式的数据。
  - File 接口基于 Blob，继承了Blob 功能并将其扩展为支持用户系统上的文件。

- Blob对象是不可变的，而 ArrayBuffer 是可以通过 TypedArrays 或 DataView 来操作。
- 除非你需要使用 ArrayBuffer 提供的写入/编辑的能力，否则 Blob 格式可能是最好的。
- ArrayBuffer 是存在内存中的，可以直接操作。
  - 而 Blob 可以位于磁盘、高速缓存内存和其他不可用的位置。
- 虽然 Blob 可以直接作为参数传递给其他函数，比如 window. URL.createObjectURL()。但是，你可能仍需要 FileReader 之类的 File API 才能与 Blob 一起使用。

- Blob 与 ArrayBuffer 对象之间是可以相互转化的：
  - 使用 FileReader 的 readAsArrayBuffer() 方法，可以把 Blob 对象转换为 ArrayBuffer 对象；
  - 使用 Blob 构造函数，如 new Blob([new Uint8Array(data]); ，可以把 ArrayBuffer 对象转换为 Blob 对象。

- Blob URL 和 Data URL 区别
  - Blob URL 格式如 `blob:域名/uuid` ， Data URL 格式如： `data:[<mediatype>][;base64],<data>`  。

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

## more-blogs

- [谈谈JS二进制：File、Blob、FileReader、ArrayBuffer、Base64 - 李昆博客](https://onelk.cn/article/9OQ30JW7QNPY6ER5)
# discuss
- ## 

- ## 

- ## 💡 Fast Buffer-to-String conversion in JavaScript with a Lookup Table
- https://twitter.com/lemire/status/1732999134280314978
  - When programming in a JavaScript environment such as Node.js, you might recover raw data from the network and need to convert the bytes into strings. In a system such as Node.js, you may represent such raw bytes using a Buffer instance.
  - You can conveniently convert a Buffer instance into a JavaScript (mybuffer.toString()). But, maybe surprisingly, creating new strings can be a bottleneck. Thus a worthwhile optimization might be to try to recognize that your incoming bytes are one out of a list of known strings.
  - [Fast Buffer-to-String conversion in JavaScript with a Lookup Table – Daniel Lemire's blog](https://lemire.me/blog/2023/12/08/fast-buffer-to-string-conversion-in-javascript-with-a-lookup-table/)

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
