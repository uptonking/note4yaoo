---
title: thread-fwk-nodejs
tags: [framework, nodejs, thread]
created: 2021-04-23T18:10:44.275Z
modified: 2022-12-19T01:48:53.761Z
---

# thread-fwk-nodejs

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🏘️ [代码结构中Dao，Service，Controller，Util，Model是什么意思，为什么划分？ - 知乎](https://www.zhihu.com/question/58410621/answers/updated)

- 简单点，不用长篇大论。你只要记住一个核心两个要点就可以了。
  - 核心就是封装，也就是我入口小，里面大，你别管我用了几千几百行代码实现了什么功能，我一封装，就是一行API给你，你调我，我给你我说好的功能，这就是封装。
  - 两个要点：1分层，2传递。 
  - 分层就是我把一组同样功能的封装放一起。和数据库打交道的放一起，这层就是DAO，database access object。 把提供业务功能的分一层，就是service，有的地方叫做domain service，把控场的分一层，controller。 
  - 传递就是我要在各个东西之间传递参数，是的函数有调用参数？这个是面向过程的思想传下来的，面向对象我们传递的是实体，对象，并不是你给我四个数，

- Controller：控制层，负责接收前端的请求，根据不同的请求调用不同的Service进行处理，并将处理结果返回给前端，实现了用户请求与业务逻辑之间的关联。
  - 负责请求转发，接受页面过来的参数，传给Service处理，接到返回值，再传给页面。
  - 针对具体的业务流程，会有不同的控制器
  - 更多的是将 Service 层的结果加以处理返回给 View，也可能会处理一些简单的参数检验工作。
- Service：业务逻辑层，主要负责处理具体的业务逻辑，协调不同的Dao完成数据的操作，提供给上层Controller进行调用。
  - 主要负责业务模块的逻辑应用设计，更面向业务。比如用户登录的校验等。
  - Service层的业务实现，具体要调用到已定义的DAO层的接口，封装Service层的业务逻辑有利于通用的业务逻辑的独立性和重复利用性，程序显得非常简洁。
- Dao(Data Access Object)：数据访问层，主要负责和数据库进行交互，包括数据的增删改查、数据连接、事务控制等，封装了对数据库的访问，提供了一组操作数据库的接口。
  - 具体到对于某个表的增删改查，也就是说某个DAO一定是和数据库的某一张表一一对应的。
  - DAO层的数据源配置，以及有关数据库连接的参数
- Model：模型层，用于描述应用程序中的数据对象，包括数据结构和数据访问方法。在MVC架构中，Model通常和数据库中的表对应，负责从数据库中读取数据并封装成实体对象，提供给Service层和Controller层使用。

- controller 就是个mvc历史遗留下来的“坏”名字，应该叫 protocol/api，接口/协议层。作用是将 http/rpc请求转化为编程语言中的 object/struct。 然后调用service层的方法。
- service是业务逻辑层，里面编写业务逻辑，不要出现 sql 等数据读写，数据读写应当调用dao。（数据的必填长度等格式验证应当在业务逻辑层） service衍生出了biz，在这里就不展开了。
- dao 里面写 sql redis mq 等数据存储读写代码 dao是数据访问对象的缩写。在go里面我更喜欢叫 data store
- 实践指南：
  - 开发一个功能时先不要管http/rpc。在java/go 的世界先定义好 interface ，然后实现自己interface。
  - 实现的过程中将数据读写都放在dao里面。
  - 在动态类型后端语言不要搞严格的分层，会很累。导致最终分了个寂寞，此处不展开。
# discuss-architecture/pattern
- ## 

- ## 

- ## 

- ## 

- ## [After 2 years of solo Node.js in production, here are the patterns I swear by and the ones I abandoned. : r/node](https://www.reddit.com/r/node/comments/1riuksx/after_2_years_of_solo_nodejs_in_production_here/)
- Running a Node.js monolith in production for 2+ years as the only developer. 15K+ users, ~200 req/s at peak. Here's what actually matters:

Patterns I swear by:

1. Centralized error handling middleware Every Express route wraps async handlers with a single error catcher. No try/catch in every route. One place to log, one place to format error responses.

2. Request validation at the edge Joi/Zod validation on every incoming request before it touches any business logic. The number of bugs this prevents is insane.

3. Structured logging from day 1 Winston with JSON format, correlation IDs on every request. When something breaks at 3 AM, structured logs are the difference between debugging in 5 minutes vs 2 hours.

4. Database connection pooling with health checks Mongoose with proper poolSize, heartbeat interval, and reconnection logic. Had a 4-hour outage early on because I used default connection settings.

5. Rate limiting per endpoint, not just globally Some endpoints (auth, payments) get strict limits. Others (reads) are more permissive. One global rate limit is too blunt.

6. Graceful shutdown handling SIGTERM handler that stops accepting new connections, finishes in-flight requests, closes DB connections, then exits. Prevents data corruption during deploys.

Patterns I abandoned:

1. Microservices Built 4 separate services for 50 users. Debugging was a nightmare. Consolidated back to a monolith. Night and day difference in velocity.

2. GraphQL For my use case (mostly CRUD with simple relationships), REST was simpler and faster to develop. GraphQL added complexity with no real benefit at my scale.

3. Event-driven architecture with message queues Used RabbitMQ for async processing. Replaced it with simple cron jobs on Lambda. 90% of "async processing" needs are just scheduled tasks.

4. Clustering with PM2 Switched to a single process behind an ALB. Node handles concurrent requests fine with async I/O. PM2 clustering added complexity for minimal benefit at my traffic level.

5. ORM-heavy patterns Started with Sequelize, moved to raw MongoDB queries. For simple CRUD, native drivers are faster and easier to debug.

- The biggest insight: complexity is the real enemy when you're solo. Every abstraction layer you add is another thing to debug at 3 AM when things break.

- Microservices for 50 users ??
  - You'd be surprised how many companies do that
- Microservices for a solo dev ??

- What are the odds there are two "life-hack" style of posts in a single day and both of them list graceful shutdown handling with SIGTERM. Thanks, ChatGPT. What are you trying to accomplish?

- One thing I've found is a good (micro?)services pattern to reduce complexity. We have a single codebase, that has an entry point pattern to build several different lambdas that we deploy with IaC (pulumi, but terraform also works). This allows us to write simple code, in a single project, that refers to other parts of the system. So the parts of our system that need to scale can, and the ones that don't, don't.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Skip - The Reactive Framework. I’ve always wanted something like React for the backend 
- https://x.com/Vjeux/status/1872353619800199366
- i remember skip wasn’t maintained for a long time.. is it back on track now?
  - Shipping a brand new programming language is hard. They changed the strategy, they build the core library using skip but have people write code in javascript instead. Much lower adoption barrier but still the same wins.

- A summary of the architecture:
  - Low level: The runtime (written in Skiplang), compiles to native or wasm.
  - Medium level: The JS bindings, use native code when available (node), otherwise wasm.
  - High level: The framework, bindings + helper functions to write reactive systems

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
