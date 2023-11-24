---
title: thread-fwk-nodejs
tags: [framework, nodejs, thread]
created: 2021-04-23T18:10:44.275Z
modified: 2022-12-19T01:48:53.761Z
---

# thread-fwk-nodejs

# guide

# discuss
- ## 

- ## 

- ## 在Node环境中跑起了PHP框架Laravel。
- https://twitter.com/TooooooBug/status/1727896108591178194
  - 去年7月左右 WordPress被成功在WASM PHP环境中跑起来 https://wasmlabs.dev/articles/wordpress-in-the-browser/
  - PHP-WASM项目地址 https://github.com/seanmorris/php-wasm
  - @php-wasm/node包https://npmjs.com/package/@php-wasm/node
  - 基于php-wasm的Laravel环境
- 意义在于用serverless 环境来跑Laravel？
  - 项目README中写得很直白：解决PHP开发环境搭建的问题。
  - 但这类项目确实可以有更深远的意义，相当于编程语言/环境有大一统的可能性了，无论是serverless环境还是浏览器环境还是什么其他的环境，都更容易支持。也许也还能带来其它新的特性和玩法或者性能上的提升之类之类的。

- ## 🆚️ Web server 'hello world' benchmark : Go vs Node.js vs Nim vs Bun
- https://twitter.com/lemire/status/1710538462460256437
  - There are many popular frameworks for writing little web applications. Go and JavaScript (Node.js) are among the most popular choices. 
  - Reportedly, Netflix runs on Node.js; Uber moved from Node.js to Go for better performance. There are also less popular options such as nim.
  - I just write a little toy web application. A minimalist application tells you the best possible speed since any more complex application has to run slower.
  - [Web server ‘hello world’ benchmark : Go vs Node.js vs Nim vs Bun – Daniel Lemire's blog](https://lemire.me/blog/2023/10/07/web-server-hello-world-benchmark-go-vs-node-js-vs-nim-vs-bun/)
  - [I have updated my benchmark with new dedicated Bun code and a tweaked Go version.](https://twitter.com/lemire/status/1710684542103642374)

- tell me you haven't read anything Jarred's ever wrote about fastify, express, Bun.serve and node:http

- Not really useful hello work benchmark.
  - The rationale(全部理由, 根本原因) is that it gives you a reference.

- ## One of my favorite things about using Node for APIs: I can reuse code on the client and the server.
- https://twitter.com/housecor/status/1422976765274824709
- How? I create a monorepo with 3 folders: 
  1. ui
  2. api
  3. shared (code used by both UI and API)
  - Result: I can reuse validation, formatting, etc. on client & server.
- I like to organize code the same way. I'll also use dependency-cruiser to make sure nothing in shared/ can import from outside the shared/ folder

- ## WebContainers: Run Node.js natively in the browser
- https://news.ycombinator.com/item?id=27223012
- Everyone thought WASM would enable developers to write code in any language they wanted (with type checking and higher performance) and deploy it on the web.
  - the demo is very impressive (except for the "only works in Chromium-based browser" message on the next.js demo, where the preview should be - despite Mozilla being one of the main WASM backers and Firefox having arguably the best WASM engine).
- WASM is a math coprocessor for JS. 💡 **WASM can't even talk to the DOM API directly** (which is the API you use to build web pages in JS); you have to write JavaScript glue code for any/all I/O in WASM.
  - WASM can't even talk to the DOM API directly. For now. It's planned.
  - For existing code bases that don’t already do DOM manipulation (so, all of them) other parts of the Web API might be more useful, like the canvas, the video API, the RTC API etc.
- It's the "File System Access API, " the one that allows the browser to read/write files on your actual computer. It's an I/O feature, impossible to polyfill.
  - The similarly named "FileSystem API" gives you access to a sandboxed "virtual drive" in the browser. Firefox has supported that for years, and polyfills are possible, but it's irrelevant in this case.
- We'll be open sourcing core parts of WebContainer as we move towards GA. 
  - We have some additional technical info in our core WG repo
  - https://github.com/stackblitz/webcontainer-core
- Faster than your local environment. Builds complete up to 20% faster. How? Isn't this using npm?
  - It's using a custom npm client we've built called Turbo. We haven't released any more info on Turbo v2 yet but will soon.

- what is the difference between running javascript on the browser and running node.js on the browser?
  - This is going full inception(开端、开始) mode. Nodejs is compiled to wasm (like assembly for your browser), and then loaded inside the browser, which can then run javascript.
  - So a full JS engine is loaded, completely separate from the built-in one.
  - wasm can't access the file system, but it could implement an API that emulates a file system inside the browser sandbox. Presumably that's what they're doing here.
  - But you can do that same API emulation in regular browser JavaScript, too. What's the WASM intermediate buying here?
  - I think it is more complicated to emulate those api in normal browser environment compared to emulating some OS api for running node.js.
  - Because many node.js api are written in C/C++, it might be easier to implements OS features instead of rewriting in JS. This is just my assumption.

- ## At StackBlitz, we’re excited to bring Node.js back to its roots - the browser!
- https://twitter.com/stackblitz/status/1395409316270772224
  - [Introducing WebContainers: Run Node.js natively in your browser](https://blog.stackblitz.com/posts/introducing-webcontainers/)
- Will it work in Brave and other Chromium based browsers?
  - Yes! It even runs in Firefox and (soon) Safari once they full ship WASM Threads
- How many cross-browser compatibility issues will I have resulting from this being based on the Chrome V8 JS engine?  How much stub-code will I need to include to attain similar behavior across diverse devices, screen sizes and resolutions, and browser JS implementations?
  - I appreciate your response. The thing is, I can't make business decisions based on "ideally" and "hopefully"
- Do you intend to support the browser DOM as a target, or only jsdom?
  - We'd love to support browser DOM
