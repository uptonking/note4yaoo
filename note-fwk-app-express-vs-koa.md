---
title: note-fwk-app-express-vs-koa
tags: [comparison, express, framework, koa]
created: '2020-12-08T09:38:21.479Z'
modified: '2020-12-08T13:29:27.651Z'
---

# note-fwk-app-express-vs-koa

## faq

- Why isn't Koa just Express 4.0?
  - Koa is a pretty large departure from what people know about Express, the design is fundamentally much different, 
  - so the migration from Express 3.0 to this Express 4.0 would effectively mean rewriting the entire application, so we thought it would be more appropriate to create a new library.

## guide

## koa vs express

- [多维度分析 Express、Koa 之间的区别](https://zhuanlan.zhihu.com/p/115339314)
  - 本文从 Handler 处理方式、中间件执行机制的实现、响应机制三个维度来对 Express、Koa 做了比较，
    - 通常都会说 Koa 是洋葱模型，这重点在于中间件的设计。
    - 但是按照上面的分析，会发现 Express 也是类似的，
    - 不同的是Express 中间件机制使用了 Callback 实现，这样如果出现异步则可能会使你在执行顺序上感到困惑，因此如果我们想做接口耗时统计、错误处理 Koa 的这种中间件模式处理起来更方便些。
  - 最后一点响应机制也很重要，Koa 不是立即响应，是整个中间件处理完成在最外层进行了响应，而 Express 则是立即响应。

- [Express和Koa2的区别](https://segmentfault.com/a/1190000022536921)
- 用法的区别
  - Express是基于回调，也是node中最常见的Error-First的模式（第一个参数是error对象）
  - Koa是使用的号称异步终极解决方案的Async/Await，也就是基于Promise，使用Try-Catch来捕获错误
- 中间件的区别
  - Express的中间件是线性模型
  - Koa的中间件是洋葱模型（聊一聊KOA的洋葱模型）
- 集成度
  - Express自带了Router和Static的中间件
  - Koa需要自行安装Router和Static的中间件

- koa-pros
  - Generator Support
    - This makes the code more manageable
  - Lightweight
    - It has just 550 lines of code
  - Beyond Generator Functions
    - team has shifted towards async/await style programming

- koa-cons
  - Small Community
    - This offers lesser room for discussion and creative input
  - Incompatible middleware with express style
    - Koa isn’t compatible with express style middleware
  - Incompatible Generators
    - Koa uses generators which aren’t compatible with any other type of Node.js framework middleware

- express-pros
  - Rapid App Development
    - It facilitates rapid application development as so many things in Express are done by default.
  - Middleware
    - It allows you to set up middleware to respond to HTTP requests.
  - Routing
    - Routing is much easier with Express when you have a number of web pages.
  - Dynamic Web Pages
    - It also helps in rendering web pages dynamically.

- express-cons
  - API is not stable
    - The Application Programming Interface keeps on changing at frequent intervals and does not remain stable.
  - No strong library support
    - With no strong library support system, it makes it difficult for programmers to even implement simple task

- How is Koa different than Connect/Express?
  - Promises-based control flow
    - No callback hell.
  - Koa is barebones
    - Unlike both Connect and Express, Koa does not include any middleware.
    - Koa is more modular.
    - Koa does not provides functionalities like Routing, Templating, Sending files and JSONP while the express does.
  - Koa relies less on middleware
    - For example, instead of a "body parsing" middleware, you would instead use a body parsing function.
  - Koa abstracts node's request/response
    - Proper stream handling.

- 光看在前端工具中的应用比如webpack等，express就占了压倒性优势
  - webpack-dev-server功能中的dev和hot的确可以改成koa版本的，
    - 不过在实际的使用中，有可能用到的不止这两个中间件，
    - 比如有的团队会配合使用一些mock中间件或者http请求转发中间件等，
    - 就我看到的目前大部分还都是express，如果要替换，是这些一整套都要进行替换，成本还是比较大的~
    - 而且作为前端工具来讲，在express生态比较成熟的情况下，硬要替换成koa感觉也没啥收益~
  - 知道callback的人async await的人多多了
  - express有着比koa2更多的中间件、社区资源

- [Koa vs Express](https://github.com/koajs/koa/blob/master/docs/koa-vs-express.md)
  - Philosophically, Koa aims to "fix and replace node", whereas Express "augments node".
  - Koa uses promises and async functions to rid apps of callback hell and simplify error handling. 
    - It exposes its own ctx.request and ctx.response objects instead of node's req and res objects.
  - Express, on the other hand, augments node's req and res objects with additional properties and methods 
    - and includes many other "framework" features, such as routing, templating, jsonp, sending files, which Koa does not.
  - Thus, Koa can be viewed as an abstraction of node.js's http modules, where as Express is an application framework for node.js.
    - Thus, if you'd like to be closer to node.js and traditional node.js-style coding, you probably want to stick to Connect/Express or similar frameworks. 
    - If you want to get rid of callbacks, use Koa.
    - As result of this different philosophy is that traditional node.js "middleware", i.e. functions of the form (req, res, next), are incompatible with Koa. 
  - a lot of the Express goodies were moved to the middleware level in Koa to help form a stronger foundation
    - This makes middleware more enjoyable and less error-prone to write, for the entire stack, not just the end application code.

- [Should I be using Koa over express?](https://www.reddit.com/r/node/comments/8iz642/should_i_be_using_koa_over_express/)
  - The main reason that Koa got any real traction was during a period when Express wasn't receiving regular updates, and there were some ownership issues. 
    - Express has since been donated to the Node.js Foundation and it's leaps and bounds more popular than any other framework (4.7M weekly downloads for Express vs 123k for Koa, 227k for Hapi). 
    - You will find more documentation, training, support, and plugins for Express than other frameworks
    - if you plan on working with other developers,
    -  it's more likely that they'll have experience with Express compared to other frameworks

 - Either is fine. Express is still more popular. 
   - Use koa if you like writing “onion” style middleware

- [reddit: Koa vs Express](https://www.reddit.com/r/node/comments/f7da6o/koa_vs_express_without_the_bs/)
- I use Koa on a side projects and I ran into issues in three areas:
  - Piping binary content through a response (generated PDF created by an external process, got it working just was a bit complicated and way more examples for Express).
  - Using existing admin modules that plug into Express but are not easy or but possible to get working on Koa. Example is say Arena queue admin UI (**). Ended up spinning up a separate admin Express instance on another port as a quick workaround.
  - Not really Koa but made a choice on one of the router modules for it and got burned for a while (had to lock version) when that project changed their implantation breaking the way many had been hooking up routes. And that change was not on a major version bump 

## thread-express-koa

- What's your favourite framework for creating APIs in Node
  - https://twitter.com/mrflamez_/status/1299852011513565186
  - for JS it has to be adonis or nest. for setting up a quick POC though it's always express or koa

- Which is the Optimal Node Framework: Express.js, Koa.js or Sails.js?
  - https://twitter.com/JavaScriptDaily/status/908639055163912192
  - I love KoaJs, but I admit I lack experience with any of the others

- why are you still using express instead of Koa?(201911)
  - https://twitter.com/sseraphini/status/1200161578701803520
  - Express has a larger ecosystem
    - Many libs build on top of express (graphql-yoga, apollo-server, etc)
  - i use both, sometimes i only need a sequential middleware stack, sometimes i need to crawl back up the stack. I’d say express is simpler especially for new devs
  - I recently migrated all my services from Koa back to express.js. 
    - As others have pointed out: community size. 
    - Koa itself might be maintained, but there are a lot of poorly supported packages at the edges of the dependency tree/ plugins.

## ref

- [Bulletproof node.js project architecture ](https://dev.to/santypk4/bulletproof-node-js-project-architecture-4epf)
  - https://github.com/santiq/bulletproof-nodejs
  - Express.js is great frameworks for making a node.js REST APIs however it doesn't give you any clue on how to organizing your node.js project.
  - 3 Layer architecture: controller, service, dao
- [What's the Node framework landscape like?](https://dev.to/ben/what-s-the-node-framework-landscape-like-5d5f/comments)
- [Hapi vs Koa vs Express](https://www.section.io/engineering-education/hapi-vs-koa-vs-express/)
