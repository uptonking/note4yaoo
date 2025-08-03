---
title: lang-js-nodejs-community
tags: [community, js, lang, nodejs]
created: 2021-08-30T06:47:48.554Z
modified: 2022-12-19T01:49:06.760Z
---

# lang-js-nodejs-community

# guide

# discuss-file-io
- ## 

- ## 

- ## [Find home directory in platform agnostic way - Stack Overflow](https://stackoverflow.com/questions/9080085/node-js-find-home-directory-in-platform-agnostic-way)
- `os.homedir()` was added by this PR and is part of the public 4.0.0 release of nodejs.

- ## [Check synchronously if file/directory exists in Node.js - Stack Overflow](https://stackoverflow.com/questions/4482686/check-synchronously-if-file-directory-exists-in-node-js)
- Update December 2016: `fs.exists()` is still deprecated but `fs.existsSync()` is no longer deprecated. So you can safely use it now.

- The answer to this question has changed over the years.
  - You can use `fs.existsSync()` ; 
  - You've specifically asked for a synchronous check, but if you can use an asynchronous check instead (usually best with I/O), use `fs.promises.access` if you're using async functions or `fs.access` (since exists is deprecated) if not
# discuss-network
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [I finally escaped Node | Hacker News_202103](https://news.ycombinator.com/item?id=26561847)
- We went away from node as a backend technology for a bunch of reasons. Here's a list of the biggest pain points:
  - Lack of a good standard API; compared to environments like Java, C# or Go, node's standard library is significantly sparse.
  - The tendency for small libraries/frameworks leads to a very high number of third party code with all the problems attached; bigger attack surface, licensing challenges, it's economically impossible to vet and review dependencies
  - There's a tendency in the ecosystem to abandon projects rather soon (~1-2 years) and to keep changing things. Further, we have had several situations where maintainers did not respect semver. The state of documentation of a lot of projects is non-existent.
  - Lack of multi threading. We have used all the options, including RPC implementations, but that doesn't even come close to approaches like Java threads or go routines. Neither in performance, nor in maintainability.
  - Lack of typing. That's probably the biggest one. Yes, we use TypeScript, quite extensively even. But TypeScript brings its own problems. First, it's only declarative. If you have a `something: number` , there's no guarantee that it's actually a number upon execution, so if you have a bug in a layer interacting with another system, that might fail a couple levels deep. You hence end up with type checks at some places and you cannot really trust it anyway. Second, TypeScript's tooling is slow and has some annoying quirks (e.g. aliases not being resolved upon compilation). Having aliases allowing to shorten import paths is a big, big win, though. Third, the typing, given the complexity of JavaScript, can be confusing, sometimes even seemingly impossible to get right.

- ## [node.js和前端js有什么区别？](https://www.zhihu.com/question/60164095/answers/updated)

- 虽然都是用的js的语法，但编程的方向却不太一样，
  - 如果用Node.js来做服务端开发，更多的时候是面相API编程，与请求打交道，
  - 而前端js则更多的面相DOM编程
- 一个是基于浏览器端的javascript ，个是基于服务端的javascript
  - 语法一样，组成不一样
  - JavaScript：
    - ECMAScript（语言基础，如：语法、数据类型结构以及一些内置对象）
    - DOM（一些操作页面元素的方法）
    - BOM（一些操作浏览器的方法）
  - Node.js：
    - ECMAScript（语言基础，如：语法、数据类型结构以及一些内置对象）
    - OS（操作系统）
    - file（文件系统）
    - net（网络系统）
    - database（数据库）
- node.js就是把js作为编程语言工具的一种，进行了扩展，来实现各种后端操作。
  - 所谓后端，更多的关注各种数据结构，运算逻辑，如果非要用前端的方式去理解，学学用js画canvas吧，画个绽放的烟花，后端的算法也就感受一二了。
# node environment vs browser environment
- ### [Differences between Node.js and the Browser](https://nodejs.dev/learn/differences-between-nodejs-and-the-browser)
- In the browser, most of the time what you are doing is interacting with the DOM, or other Web Platform APIs like Cookies. 
  - Those do not exist in Node.js, of course. 
  - You don't have the document, window and all the other objects that are provided by the browser.
  - And in the browser, we don't have all the nice APIs that Node.js provides through its modules, like the filesystem access functionality.
- Another big difference is that in Node.js you control the environment. 
  - you know which version of Node.js you will run the application on
- Another difference is that Node.js uses the CommonJS module system, while in the browser we are starting to see the ES Modules standard being implemented.

- ### [Differences between Node environment and browser javascript environment](https://stackoverflow.com/questions/23959868/differences-between-node-environment-and-browser-javascript-environment)
- Code that runs on the client usually have very different goals from the code that runs on the server. 
  - However when it makes sense to use some library's features in both environments, there are a lot of them that are defined using a universal AMD form which makes them platform independent
- The major difference between both environments is that one is subject to rigorous security policies and restrictions (browser) while the other isn't. 
  - The browser is also an untrustworthy environment for security-related operations such as enforcing security permissions.
- The biggest practical difference is that you have to design a browser application to work in an installed base of existing browsers including older versions (lowest common denominator). 
  - When deploying a node application, you get to select the ONE version of node that you want to develop for and deploy with. 
  - This allows node developers to use the latest greatest features in node which won't be available across the general browser population for years.
  - Libraries should be designed for the environment in which they are truly useful.

- ### [Differences between Node and the Browser_201808](https://flaviocopes.com/node-difference-browser/)
- In the browser, most of the time what you are doing is interacting with the DOM, or other Web Platform APIs like Cookies. 
  - Those do not exist in Node, of course. 
  - You don’t have the `document, window` and all the other objects that are provided by the browser.
  - And in the browser, we don’t have all the nice APIs that Node.js provides through its modules, like the filesystem access functionality.
- Another big difference is that in Node.js you control the environment. 
  - Unless you are building an open source application that anyone can deploy anywhere, you know which version of Node you will run the application on. 
  - Compared to the browser environment, where you don’t get the luxury to choose what browser your visitors will use, this is very convenient.
  - This means that you can write all the modern ES6-7-8-9 JavaScript that your Node version supports.
- Another difference is that Node uses the CommonJS module system, 
  - while in the browser we are starting to see the ES Modules standard being implemented.

- ### [What is Node.js and how does it differ from a browser_201908](https://medium.com/swlh/what-is-node-js-and-how-does-it-differ-from-a-browser-ddebef00cbd9)
- First and foremost, node.js is a javascript runtime based on chrome’s javascript engine called V8
  - In simple terms, people extracted the javascript engine from chrome and made it able to run standalone. 
  - there is no DOM, no UI, there are some runtime differences
- Very much like javascript running in a browser, node.js is has a single thread for running javascript and it uses the event queue. 
  - Blocking the main thread does not freeze any UI 
  - but it is still bad practice because it prevents async tasks like web requests from ever being handled. 
  - Exceptions, flow, scoping all works identical to javascript modules. 
  - But there are many significant differences. 
- **CommonJS**
  - Node.js has a module system that predates the modern import statement. 
  - While node.js has recently started supporting `import`, almost all code in the wild still uses common.js. 
  - In common.js you will use `require` to load a javascript module.
- **Full user-level system access**
  - Unlike the browser where Javascript is sandboxed for your safety, node.js has full access to the system like any other native application. 
  - This means you can read and write directly to/from the file system, have unrestricted access to the network, can execute software and more. 
  - This means writing full desktop software is possible with node.js even including a UI through modules like electron. 
  - This means that javascript ran through node.js needs to be treated with the same level of caution as running C++, java, or any other language directly on your system. 
  - Never run untrusted javascript in node.js.
- **Global instead of Window**
  - A lot of the APIs of the browser are missing like anything related to DOM and CSS, Performance, Document, APIs related to window. 
  - So for logic’s sake, the global object was renamed to global, since it does not refer to a window and has no window like properties
- **The Async IO threadpool**
  - Browsers do have multiple threads to support the execution of javascript but in node.js the threadpool is used for super fast IO. 
  - When you use native modules they can tap into the threadpool, usually to do things like read from disk or send/receive data over the network in the background without wasting precious main thread CPU cycles that are reserved to your javascript code. 
  - This means that as long as you use the async versions of IO operation methods, the IO is basically zero cost for the javascript thread because the load is handled by another thread in the background. 
  - This is part of what makes it possible to have high-performance js based servers even though javascript itself only runs on one thread.
- Node.js is primarily used to make web servers and CLI tools, however, node.js can do so much more. 
  - Use the Vulkan API to create a window and create your game
  - PC application is done with node.js through electron
  - vscode was made in node.js through electron and it performs great.
  - You can even extend what node.js can do using C++ if the library for what you want does not yet exist. 
- there is one major reason why node.js exists and why it is so popular. 
  - That reason is: It runs javascript like we are used to. 
  - it even allows sharing of code between back and front end. 
  - The whole serverless concept couldn’t have been born without this fact.
