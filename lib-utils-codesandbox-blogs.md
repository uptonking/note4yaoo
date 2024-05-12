---
title: lib-utils-codesandbox-blogs
tags: [blog, codesandbox]
created: 2024-01-25T13:28:59.741Z
modified: 2024-01-25T13:29:10.054Z
---

# lib-utils-codesandbox-blogs

# guide

# blogs-dev-xp

## [Building a Next-Level Code Playground/Sandbox/REPL with Sandpack _202402](https://www.joshwcomeau.com/react/next-level-playground/)

- I recently rebuilt this blog's playground, using Sandpack, a modern playground framework built by the folks at CodeSandbox
- The "secret sauce" for CodeSandbox has been the in-browser bundler. It can fetch dependencies from NPM, transpile your JSX, and even supports modern quality-of-life features like hot module reloading. It does this all in-browser
- By default, Sandpack uses CodeMirror as its code editor.
  - This is a bit surprising; CodeSandbox uses VSCode as its editor, and so I thought for sure Sandpack would use Monaco, the editor that powers VSCode.
  - After experimenting with it, however, I've discovered I quite like CodeMirror. It's not as fully-featured as Monaco, but then it doesn't need to be; most web-based playgrounds are meant to demonstrate a concept, not serve as a daily-driver editor.

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

# blogs-csb-internals

## [CodeSandbox是如何让npm上的模块直接在浏览器端运行的 _202011](https://www.yuque.com/wangxiangzhong/aob8up/uf99c5)

- [CodeSandbox - 从入门到实现原理解析](https://www.yuque.com/wangxiangzhong/aob8up)

- [技术夹](https://www.yuque.com/wangxiangzhong/mvugau)
  - [一文彻底搞懂前端沙箱](https://www.yuque.com/wangxiangzhong/mvugau/bgs3po)

## [搭建一个属于自己的在线 IDE - 网易云音乐技术团队 _202010](https://juejin.cn/post/6882541950205952013)

- [云音乐低代码：基于 CodeSandbox 的沙箱性能优化 - 掘金 _202205](https://juejin.cn/post/7102243774985666596)
  - 距离发布如何私有化部署 CodeSandbox 沙箱的文章《搭建一个属于自己的在线 IDE》 已经过了一年多的时间，最开始是为了在区块复用平台上能够实时构建前端代码并预览效果。
  - 不过在去年云音乐内部启动的基于源码的低代码平台项目中，同样有在线实时构建前端应用的需求，最初是采用从零开发沙箱的方式，不过自研沙箱存在以下几点问题：
    - 灵活性较差
    - 兼容性较差
    - 未实现与平台的隔离
  - 当然如果继续在这个自研沙箱上继续开发，上面提到的问题还是可以逐步被解决的，只是需要投入更多的人力。
  - 而 CodeSandbox 作为目最主流且成熟度较高的在线构建沙箱，不存在上面列出的问题。而且实现代码全部开源，也不存在安全问题。于是便决定采用私有化部署的 CodeSandbox 来替换低代码平台的自研沙箱

- 笔者主要研究的是 Codesandbox 以及 Stackblitz 。这两个都是商业化的项目，其中 Stackblitz 的核心部分并没有开源出来，而 CodeSandbox 绝大部分的功能都已经开源出来了，所以最终选择了 CodeSandbox。
- CodeSandbox 最大的特点是采用在浏览器端做项目构建，也就是说打包和运行不依赖服务器。由于浏览器端并没有 Node 环境，所以 CodeSandbox 自己实现了一个可以跑在浏览器端的简化版 webpack。
- CodeSandbox 主要包含了三个部分：
  - Editor 编辑器：主要用于编辑代码，代码变动后会通知 Sandbox 进行转译
  - Packager npm 在线打包器：给 Sandbox 提供 npm 包中的文件内容
  - Sandbox 代码运行沙盒：在一个单独的 iframe 中运行，负责代码的编译 Transpiler 和运行 Evalation
- 构建过程主要包括了三个步骤：
  - Packager--npm 包打包阶段：下载 npm 包并递归查找所有引用到的文件，然后提供给下个阶段进行编译
    - Packager 阶段的代码实现是在 CodeSandbox 托管在 GitHub 上的仓库 dependency-packager 里，这是一个基于 express 框架提供的服务，并且部署采用了 Serverless(基于 AWS Lambda) 方式，让 Packager 服务更具伸缩性，可以灵活地应付高并发的场景。
    - （注：在私有化部署中如果没有 Serverless 环境，可以将源码中有关 AWS Lambda 部分全部注释掉即可 ）
  - Transpilation--编译阶段：编译所有代码, 构建模块依赖图
    - 当 Sandbox 从 Editor 接收到前端项目的源代码、npm 依赖以及构建模板 Preset。Sandbox 会初始化配置，然后从 Packager 服务下载 npm 依赖包对应的 manifest 文件，接着从前端项目的入口文件开始对项目进行编译，并解析 AST 递归编译被 require 的文件，形成依赖图（注：和 webpack 原理基本一致）。
    - CodeSandbox 支持外部预定义项目的构建模板 Preset。Preset 规定了针对某一类型的文件，采用哪些 Transpiler（相当于 Webpack 的 Loader）对文件进行编译。目前可供选择的 Preset 选项有： vue-cli 、 create-react-app、create-react-app-typescript、 parcel、angular-cli、preact-cli。但是不支持修改某个 Preset 中的具体配置
  - Evaluation--执行阶段：使用 eval 运行编译后的代码，实现项目预览
    - 从项目入口文件对应的编译后的模块开始，递归调用 eval 执行所有被引用到的模块。
- 如何私有化部署 CodeSandbox。
  - 首先是 npm 在线打包服务 dependency-packager。笔者是通过镜像部署到自己的服务器上的。
  - react-sandpack 项目，就是 CodeSandbox 提供的基于 react 实现的的编辑器项目
  - 子组件 FileExplorer、CodeMirror、BrowserPreview 分别是左侧的文件目录树、中间的代码编辑区和右侧的项目构建后的页面预览区。
  - SandpackProvider 还会再插入一个 iframe 标签，主要用于显示项目构建后的页面，而右侧预览区组件 BrowserPreview 中的 Preview 组件会将这个 ifame 插入到自己的节点，这样就实现了将项目构建的页面实时显示出来的目的。
  - iframe 加载的 bundlerUrl 默认是官方提供的地址 http://sandpack-${version}.codesandbox.io ，其中这个域名对应的服务其实就是 CodeSandbox 的核心--在浏览器端构建前端项目的服务
- 代码运行沙盒 SandBox
  - CodeSandbox 前端构建的核心部分的目录在 CodeSandbox-client 工程中 packages/app 项目，其中的原理已经在上面阐述过了，这里只需要将该项目构建出来的 www 文件夹部署到服务器即可
  - 注意这里采用了分阶段构建镜像，即先构建 CodeSandbox 项目，再构建镜像。但在实践中发现 CodeSandbox 项目放在服务器上构建不是很顺利，所以最终还是选择在本地构建该项目，然后将构建产物一并上传到远程 git 仓库，这样在打包机上只需要构建镜像并运行即可。
- 为什么直接使用 CodeSandbox 提供的默认构建服务？其实就是为了对 CodeSandbox 的构建流程进行定制
  - 替换组件样式自动引入的 babel 插件功能
  - 添加预览区域截图功能
  - create-react-app 模板中添加对 less 文件编译的支持
  - 修改 CodeSandbox 请求的 npm 打包服务地址

- 👥 

- 文章如今看来有点过时了。基本原理是正确的，但是 csb 进化的太快了

- 为什么不用theia、vscode网页版呢？这些都可以直接打包，而且可以配置私域的源呀
  - 主要是应用场景吧，文章提到的浏览器构建的方式对于组件/区块级别已经足够了。目前的确在尝试服务端构建方式来实现实际的前端项目在 web 上开发的目的，不过这种方式如果要真正可以在实际工作中应用的话，对服务器的各方面要求比较高。 总结来说做这个方案选择主要考虑到应用场景，以及实现成本、投入产出比等等。

- 可以使用 code-server 搭建一个浏览器中运行基于 HTTP 或者 SSH 协议的 VSCode
  - 嗯 不错的思路
# blogs-csb

## [Hosting the Bundler – Sandpack](https://sandpack.codesandbox.io/docs/guides/hosting-the-bundler)

- You can also host the bundler by yourself
  - The bundler is part of the codesandbox-client codebase
  - create your instance of sandpack with `yarn build:sandpack`.
- We use Service Workers to download all transpilers in the background, so the next time a user visits your website they don't have to download the bundler anymore and it can be used offline. This is possible because we host the service worker externally.

## 🎯 [Announcing Sandpack 2.0 and a Node.js runtime for any browser _202302](https://codesandbox.io/blog/announcing-sandpack-2)

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

## 🎯 [Introducing Sandpack - A Toolkit for Creating In-Browser Live Coding _202112](https://codesandbox.io/blog/sandpack-announcement)

- Sandpack, the in-browser bundler that powers CodeSandbox, has been open-sourced for everyone to use
  - you can build your own CodeSandbox
- When CodeSandbox started, it ran all projects in the browser using a primitive bundler that runs in an iframe. 
  - We’re now at the point that the bundler supports npm dependencies, hot module reloading, caching, and a whole lot more.

## ✨ [What's Unique about CodeSandbox CDEs _202404](https://codesandbox.io/blog/whats-unique-about-codesandbox-cde)

- Recently, we released CodeSandbox CDE, a collaborative cloud development environment (CDE) that allows you to run your full development flow in Firecracker microVMs. 
- No Cold Starts
  - what if you're coding in the cloud? It would be a waste to keep a server running while you're not working; 
  - That's why all cloud solutions have an inactivity timer. After x minutes of inactivity, the server shuts down and you won't have to pay for running it.
  - But now, when you come back, you have to wait for that server and your development environment to boot up again. It's slower than your laptop, because now you have to wait.
  - Any time you stop coding for a while, the inactivity timer kicks in.
  - That's why we've developed VM snapshotting for our CDE solution. Instead of shutting down the VM, we hibernate it (like your laptop!). We save all memory to disk, and the next time you come back, we'll resume that environment exactly like you left it, within 2 seconds. No need to wait for booting things up.
  - Memory snapshots do not just save time, it also enables new workflows and experiences. We can actually snapshot many CDE environments, and they will all seem to be running 24/7 when you open them.
- Instant Context Switching
  - We don't only create a memory snapshot of your running environment. We create memory snapshots for every branch and PR. 
  - Every time a new PR is opened, we spin up a development environment, check out the branch, run the dev server, and create a snapshot.
  - If you need to switch between a branch, or even a repository, you can spin up a new environment just for that branch. Since everything is snapshotted, this only takes 2 seconds and you can instantly start coding.
  - New environments are cloned from the snapshot of your default branch (e.g. main), or from a snapshot of the branch itself. This enables some new cool functionality like brancheable databases. 
  - You can even run multiple branches at the same time and quickly switch between them without losing context.
- Preview Development Environments
  - Did you ever have to run a Pull Request locally on your laptop to review it? It's a time sink, because you need to check out the branch, install dependencies and restart the dev server.
  - This “deployment preview” works for full-stack applications too. You can run a database, backend and frontend all at the same time by defining a docker-compose file in the .devcontainer folder.
- Collaborative Branches
  - On CodeSandbox, every environment is collaborative by default. When working on a branch, you can share the link with others and they will be able to see what you're working on.
  - We implement this collaboration by giving every user their own rootless container to run their code in.

- Conclusion
  - When building CodeSandbox, we've focused on creating a product that unlocks all the values that dev environment in the cloud can give. 
  - It resulted in a more opinionated environment, but it saves us a lot of time in our day-to-day development flows.

## ✨ [What's Unique About CodeSandbox _201810](https://codesandbox.io/blog/whats-unique-about-codesandbox)

- The frontend and the microservices of CodeSandbox are open source! This is the place where you can find out how CodeSandbox works

- [What’s Unique About CodeSandbox ](https://medium.com/@compuives/whats-unique-about-codesandbox-f1791d867e48)

- Live Collaboration
  - When working on a sandbox you can open up a Live Session. This generates a unique URL which you can give to others to join your sandbox and collaborate live (google docs style) together with you. 
  - you can also enable ‘Classroom Mode’, this mode allows you to specify who can edit the sandbox and who can only view.
- GitHub Committing/Forking/PRing
- VSCode Integration
- Container Sandboxes
  - Previously we would run a sandbox in the browser. This works great for many sandboxes, but imposes a limitation on what you can run. 
  - With Container Sandboxes we actually run the code on a server, this makes it possible to eg. create a Node/GraphQL server on CodeSandbox. It also opens up the possibility to create Next/Gatsby/Nuxt projects inside CodeSandbox. 
- Dashboard & Teams
  - Everyone has a dashboard that they can organize their sandboxes in. In this dashboard you can create directories (like Google Docs) to categorize your sandboxes.
- Beginner Friendly Tricks
- Deploy Sandboxes
- Smaller Factors
  - Private/Unlisted Sandboxes
  - Jest Support
# more
