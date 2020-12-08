---
title: note-fwk-app-express-vs-koa
tags: [express, framework, koa]
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

## ref

- [What's the Node framework landscape like?](https://dev.to/ben/what-s-the-node-framework-landscape-like-5d5f/comments)
