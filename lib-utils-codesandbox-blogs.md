---
title: lib-utils-codesandbox-blogs
tags: [blog, codesandbox]
created: 2024-01-25T13:28:59.741Z
modified: 2024-01-25T13:29:10.054Z
---

# lib-utils-codesandbox-blogs

# guide

# blogs

## [Building a Next-Level Code Playground/Sandbox/REPL with Sandpack _202402](https://www.joshwcomeau.com/react/next-level-playground/)

- I recently rebuilt this blog's playground, using Sandpack, a modern playground framework built by the folks at CodeSandbox
- The "secret sauce" for CodeSandbox has been the in-browser bundler. It can fetch dependencies from NPM, transpile your JSX, and even supports modern quality-of-life features like hot module reloading. It does this all in-browser

- Something interesting about the way Sandpack is architected: the bundler isn't running locally.
  - When we render a `<SandpackPreview>` component, it produces an iframe. 
  - This iframe is hosted by CodeSandbox, and all of the bundling happens on their external domain.
  - Essentially, when the user makes a change to the code in the editor, the new code is dispatched over to the site in the iframe. That page will re-bundle the code and display the new result.
- The good thing about this approach is that it's secure. 
  - If the user writes some JS that attempts to read cookies/localStorage, for example, they'll be accessing the stuff on CodeSandbox's domain, not your own.
- That said, I was a bit wary of having such a hard dependency on an external service. If CodeSandbox ever goes down, I don't want it to affect my playgrounds!
- we can build + deploy the bundler code ourselves, to whatever domain we'd like.
  - You can learn how to self-host the bundler in their docs.
# blogs-js-sandbox 🧊

## [浅析 JavaScript 沙箱 - 掘金](https://juejin.cn/post/7148335784431468551)

- [浅析 JavaScript 沙箱机制 - 知乎](https://zhuanlan.zhihu.com/p/428039764)
  - 沙箱（Sandbox）是一种用于隔离正在运行程序的安全机制，通常用于执行未经测试或不受信任的程序或代码，它会为待执行的程序创建一个独立的执行环境，内部程序的执行不会影响到外部程序的运行。
  - 最直接的想法就是程序中访问的所有变量均来自可靠或自主实现的上下文环境而不会从全局的执行环境中取值
  - 非常简陋的沙箱（with）
    - with 会在作用域链的顶端添加一个新的作用域，该作用域的变量对象会加入 with 传入的对象
    - 问题来了，在提供的上下文对象中没有找到某个变量时，代码仍会沿着作用域链一层一层向上查找，这样的一个沙箱仍然无法控制内部代码的执行
  - 没那么简陋的沙箱（With + Proxy）
    - Proxy 中的 get 和 set 方法只能拦截已存在于代理对象中的属性，对于代理对象中不存在的属性这两个钩子是无感知的。
    - 因此这里我们使用 Proxy.has() 来拦截 with 代码块中的任意变量的访问，并设置一个白名单，在白名单内的变量可以正常走作用域链的访问方式，不在白名单内的变量会继续判断是否存在沙箱自行维护的上下文对象中，存在则正常访问，不存在则直接报错
    - 较为简单的场景就可以覆盖了, eg: Vue 的模板字符串
  - 天然的优质沙箱（iframe）
    - iframe 标签可以创造一个独立的浏览器原生级别的运行环境，这个环境由浏览器实现了与主环境的隔离。
    - 在 iframe 中运行的脚本程序访问到的全局对象均是当前 iframe 执行上下文提供的，不会影响其父页面的主体功能，因此使用 iframe 来实现一个沙箱是目前最方便、简单、安全的方法。
    - 虽然浏览器为主页面和 iframe 之间提供了 postMessage 等方式进行通信，但单单使用 iframe 来实现多沙箱通信这个场景是比较困难且不易维护的。
  - 应该能用的沙箱（With + Proxy + iframe）
    - 利用 iframe 对全局对象的天然隔离性，将 iframe.contentWindow 取出作为当前沙箱执行的全局对象
    - 将上述沙箱全局对象作为 with 的参数限制内部执行程序的访问，同时使用 Proxy 监听程序内部的访问。
    - 维护一个共享状态列表，列出需要与外部共享的全局状态，在 Proxy 内部实现访问控制。
  - 沙箱逃逸（Sandbox Escape）
    - 访问沙箱执行上下文中某个对象内部属性时，Proxy无法捕获到这个属性的访问操作。
    - 通过访问原型链实现逃逸，JS 可以直接声明一个字面量，沿着该字面量的原型链向上查找原型对象即可访问到外层的全局对象，这种行为亦是无法感知的
  - “无瑕疵”的沙箱（Customize Interpreter）
    - 有不少开源库已经在做这样一件事情，也就是分析源程序结构从而手动控制每一条语句的执行逻辑，通过这样一种方式无论是指定程序运行时的上下文环境还是捕获妄想逃脱沙箱控制的操作都是在掌控范围内的。
    - 实现这样一个沙箱本质上就是实现一个自定义的解释器。
    - myInterpreter(code, ctx, illegalOperations) // 自定义解释器

## [【微前端】JS沙箱的基本实现 - 知乎](https://zhuanlan.zhihu.com/p/450103808)

- 微前端中，为了保证应用之间js环境（主要是window全局变量）的独立，需要使用JS沙箱来对各应用的执行环境进行隔离。
- qiankun中使用了两种方案来实现这一隔离，分别是：快照沙箱、代理沙箱Proxy
- 对于支持Proxy的浏览器使用代理沙箱，不支持的浏览器降级使用快照沙箱。
- 快照沙箱的基本思路是记录差异并存储。
  - 沙箱激活前，当前window对象一定为纯粹的window对象；沙箱激活后至沙箱失活前，当前的window对象一定为当前应用使用的window（即纯粹的window对象+当前应用对window对象做出的修改）
  - 快照沙箱即对两个状态的window对象进行一次快照，然后比对两次快照的不同，存储不同内容和原始内容，达到差异重置的目的。
- 代理沙箱运用了proxy，保证了window对象的纯净，不被污染。
  - 代理沙箱运用了proxy，保证了window对象的纯净，不被污染。
  - 每个 ProxySandbox 都拥有其独立的代理对象，并不会污染真正的window对象，而快照沙箱会污染真正的window对象，所以需要在激活失活时去进行恢复/重置操作

## [30 行代码实现 JS 沙箱 - 知乎](https://zhuanlan.zhihu.com/p/589341143)

- 在 JavaScript 中，动态执行代码的方法有 Function 和 eval

```JS
eval('console.log("aaa:", aaa)');

Function('str', 'console.log(str, aaa)')('aaa:');
```

- `eval` 是在**当前作用域**直接执行代码，代码可以直接访问当前作用域。
  - 而 `Function` 创建的函数只会在**全局作用域**中运行（除主动修改作用域：bind，call 等），所以 Function 相对安全。
- 因为使用 `Function` 相当于定义一个函数，会进行分词和解析等编译工作，如果 Funcion 中执行的内容有语法错误，还是会报错 Uncaught SyntaxError 语法错误。
  - 但 `eval` 是直接对执行代码进行机器码的转译，缺少引擎编译带来的性能优化。所以 Function 比 eval 性能更优。
- 选择 Function 函数来动态执行代码后，我们可以 const createSandbox = () => code => Function(code)()
- 可以使用 Object.create() 来创建一个全局对象的副本，然后使用 with 让沙箱代码访问这个副本对象，从而达到隔离的效果。
  - with 语句可以将某个对象添加到作用域链的顶部。
  - 使用 with 的方式还存在一个问题，就是当访问全局对象不存在的字段时，还是能够访问到全局对象，比如新增字段。
- 避免沙箱代码中使用 this 访问全局对象，使用 bind 方法修改作用域。

## [使用 WebAssembly 打造定制 JS Runtime - 掘金](https://juejin.cn/post/7146939939786063885)

- 起因是在 lightdm-webkit2-greeter 这个 lightdm 插件中看到了自定义 JS Runtime的魔力，它支持在显示管理器中使用 web 技术去自定义登录界面，与操作系统的交互是通过 Runtime 中的一组 JS API来实现登录、关机、睡眠等功能

- 把 webkit 搬过来渲染系统界面，然后通过定制的 JS Runtime 与操作系统交互，相当于对浏览器本身进行了改造，关键的实现点是把系统调用封装成了Native函数，并在JS Runtime中进行绑定，以实现浏览器界面控制操作系统。

- 这种方式和 Electron 的本质区别在于，无需让浏览器与另外一个进程通信，它直接拓展了 JS 的运行时环境，与 Node 的做法十分相像，不过这次我们越过中间商赚差价，自己实现 Runtime ，可以做的更小巧和定制化。

- 这里选择了 Figma 曾经的方案 - Duktape
  - Duktape是一个嵌入式Javascript引擎，专注于可移植性和低空间占用。
  - 易于集成到C/C++项目中：将duktape.c, duktape.h，和duk_config.h添加到的构建项目中，然后使用Duktape API实现 C 代码与 Ecmascript 函数的双向调用。
# blogs-iframe

## [初探富文本之React实时预览](https://github.com/WindrunnerMax/EveryDay/blob/master/Plugin/%E5%88%9D%E6%8E%A2%E5%AF%8C%E6%96%87%E6%9C%AC%E4%B9%8BReact%E5%AE%9E%E6%97%B6%E9%A2%84%E8%A7%88.md)

- 在上文中我们一直是使用限制用户访问全局变量或者是隔离当前环境的方式来实现沙箱，
  - 但是实际上我们还可以换个思路，我们可以将用户的代码放置于一个iframe中来执行，这样我们就可以将用户的代码隔离在一个独立的环境中，从而实现沙箱的效果，
  - 这种方式也是比较常见的，例如CodeSandbox就是使用这种方式来实现的
  - 还可以通过iframe的sandbox属性来限制用户的行为，例如限制allow-forms表单提交、allow-popups弹窗、allow-top-navigation导航修改等，这样就可以做到更加安全的沙箱了

- 
- 
- 

# blogs-codesandbox

## [Hosting the Bundler – Sandpack](https://sandpack.codesandbox.io/docs/guides/hosting-the-bundler)

- You can also host the bundler by yourself
  - The bundler is part of the codesandbox-client codebase
  - create your instance of sandpack with `yarn build:sandpack`.
- We use Service Workers to download all transpilers in the background, so the next time a user visits your website they don't have to download the bundler anymore and it can be used offline. This is possible because we host the service worker externally.

## 🎯 [Announcing Sandpack 2.0 and a Node.js runtime for any browser_202302](https://codesandbox.io/blog/announcing-sandpack-2)

- One year ago, we introduced Sandpack, an open-source in-browser bundler that allows you to run live running code examples on your website.
- But in version 1, the big caveat to “any JavaScript application” was that it only worked for client runtime execution. And we wanted to change that.
- Nodebox allows running server-side examples. 

- 💡 Nodebox under the hood
- Nodebox is a high-level abstraction of Node.js. 
  - That means it doesn’t implement some of the small details of Node.js, but we made various tweaks to make it compatible with every browser. 
  - So, Nodebox aims for application compatibility, not Node.js feature parity.
- Performance was also one of our top priorities while developing Nodebox. 
  - 👉🏻 We completely rewrote the Sandpack transpiler using Rust, tweaked our caching and made several other optimizations. 
  - The result? It’s really fast! Our Vite templates, for example, have a hot start time of 500ms.
- We’re shipping Nodebox with out-of-the-box support for Next.js, Vite and Astro, but we’re growing to support just about any server-side framework you can imagine. 
  - However, bear in mind it can’t run napi or any other low-level C++/Rust package you can use in Node.js—only WebAssembly and JavaScript modules. 
  - Postgres, MongoDB and MySQL are also currently not supported because of the lack of raw socket support in browsers.
- Plus, we're currently working on some missing APIs, such as async_hooks, vm, worker_threads, automatic process exiting (users now need to manually call process.exit before the process is exited) and synchronous exec/spawn. 
  - Nodebox works in iOS Safari, but it’s still on beta support due to a browser memory leak. 

- 🆚️ Difference with WebContainers
- WebContainers is a technology that also allows you to run Node.js in the browser. 
  - However, it uses modern browser technologies like `SharedArrayBuffer`, which makes it impossible to run in Safari and requires the user to set additional `Cross-Origin-Isolation` headers on the server to run any code.

- Instead, we implemented Nodebox without modern browser technologies, to make it run in any browser (like iOS and Safari) with minimal setup. 
  - The disadvantage of this is that Nodebox will use more memory when you spawn more threads, and we cannot get full Node API compatibility (for example, we cannot use synchronous fork). 
  - This is okay for Nodebox because it was built to run small projects and examples, which it does really well. 
  - If you want to do full development in the browser, we recommend using our microVM technology instead.

## 🎯 [Introducing Sandpack - A Toolkit for Creating In-Browser Live Coding_202112](https://codesandbox.io/blog/sandpack-announcement)

- Sandpack, the in-browser bundler that powers CodeSandbox, has been open-sourced for everyone to use
  - you can build your own CodeSandbox
- When CodeSandbox started, it ran all projects in the browser using a primitive bundler that runs in an iframe. 
  - We’re now at the point that the bundler supports npm dependencies, hot module reloading, caching, and a whole lot more.

## [What's Unique About CodeSandbox _201810](https://codesandbox.io/blog/whats-unique-about-codesandbox)

- The frontend and the microservices of CodeSandbox are open source! This is the place where you can find out how CodeSandbox works
# more
