---
title: lang-js-node
tags: [js, lang, node]
created: '2019-09-12T02:32:06.774Z'
modified: '2020-07-14T09:26:55.226Z'
---

# lang-js-node

# guide

# 深入浅出Node.js

- Ryan Dahl最初的目标是写一个基于事件驱动、非阻塞I/O的web服务器，以达到更高的性能，提供Apache服务器之外的选择
  - js在后端一直没有市场，引入非阻塞I/O库没有额外阻力
  - js在浏览器中有广泛的事件驱动方面的应用
  - v8在js引擎中性能优秀
- 除了html、webkit和显卡这些ui相关的技术没有支持外，node的架构与浏览器十分相似
  - 都基于事件驱动的异步架构
    - 浏览器通过事件驱动来实现界面交互
    - node通过事件驱动实现I/O
  - 在node中，js能随意访问本地文件，可连接数据库
  - node不处理ui，但用与浏览器相同的机制和原理运行
- node特点
  - 异步I/O
    - node中大多数操作都以异步方式进行调用
  - 事件驱动和回调函数
    - 将前端成熟的事件机制引入后端，配合异步I/O，将事件点暴露给业务
    - 回调函数也许是接受异步调用返回数据最好的方式，但导致代码的编写顺写与执行顺序无关
  - 单线程
    - node保持了js在浏览器中单线程的特点，js与其余线程无法共享状态
    - 单线程的最大好处是不用处处在意状态同步问题，没有切换上下文的性能开销
    - 单线程缺点
      - 无法利用多核cpu
      - 异常会中断整个应用
      - 大量计算占用cpu会导致无法继续调用异步I/O
        - 浏览器的解决方案是web workers，工作线程不阻塞主线程
        - node采用了与web workers相同的思路来解决单线程中大量计算的问题child_process
  - 跨平台
    - 兼容windows和*nix平台主要得益于node在架构层的改动
    - 在操作系统和node上层模块之间构建了一层平台层架构，即libuv
    - libuv封装的功能包括事件循环、文件操作等
    - 目前libuv已成为许多系统实现跨平台的基础组件
    - 第三方c++模块可以记住libuv实现跨平台
- node应用场景
  - i/o密集型计算
  - 胶水层

- 普通扩展模版与内建扩展模块的区别在于无需将源码编译进node，而是通过dlopen()方法动态加载
  - 对于以.node为扩展名的文件，node会调用process.dlopen()去加载
  - uv_dlopen()/uv_dlsym()
- c++扩展模块与js模块的区别在于加载后不需要编译，直接执行后就可以被外部调用了

- 如果采用异步方式，第一个资源的获取不会阻塞第二个资源的请求，有利于分布式i/o
- 多线程的代价在于创建线程和执行期切换线程上下文的开销较大
  - 多线程在多核cpu上能有效提升cpu的利用率
  - 单线程同步的编程模型会因阻塞i/o导致硬件资源得不到更优的利用
  - 多线程的编程模型会因为死锁、状态同步问题让人头疼
  - node在两者间给出了解决方案
    - 利用单线程，远离死锁、状态同步等问题
    - 利用异步i/o，让单线程远离阻塞，更好地利用cpu
    - node还提供了类似浏览器web worker的child_process，可以通过工作进程高效地利用cpu和i/o
- 异步i/o的目标是i/o的调用不阻塞后续运算，将原来等待i/o的这段时间分配给其他需要的业务去执行
- 操作系统内核对于i/o只能两种方式：阻塞和非阻塞
  - 阻塞i/o的特点是调用之后要等到系统内核层面完成操作后，调用才结束
  - 非阻塞i/o是调用之后会立即返回，cpu的时间片可用来处理其他事务
  - 非阻塞i/o也存在问题
    - 为了获取完整数据，应用程序需要重复调用i/o操作来确认是否完成，这种重复调用判断操作是否完成的技术叫做轮询
    - 现存的轮询技术有read、select、poll、epoll、kqueue
- 由于windows和*nix平台的差异，node提供了libuv作为抽象封装层，使得所有平台兼容性的判断都由这一层来完成
  - iocp的异步i/o模型与node的异步调用模型十分近似，在windows下采用iocp实现了异步i/o
  - iocp内部仍然是线程池原理，不同之处在于这些线程池由系统内核接手管理
- 我们时常提到node是单线程的，这里的单线程仅仅是js执行在单线程中罢了
  - 在node中，无论*nix还是windows，内部完成i/o任务的另有线程池
- 在进程启动时，node会创建一个类似`while(true)`的循环，每执行一次循环体的过程我们称为tick
  - 每个tick的过程就是查看是否有事件待处理
    - 如果有，则取出事件及相关回调函数，执行回调函数
    - 如果没有，就退出进程
  - 在每个tick过程中，有一个或多个观察者，判断是否有事件要处理的过程就是向这些观察者询问是否还有事件要处理
  - 在node中，事件主要来源于网络请求、文件i/o等，这些事件对应的观察者有文件i/o观者者、网络i/o观察者等。观察者将事件进行了分类
- 事件循环是一个典型的生产者/消费者模式
  - 网络请求等是事件的生产者，不断为node提供不同类型的事件，这些事件被传递到对应的观察者那里，事件循环则从观察者那里取出事件并处理
  - 在windows下，这个循环基于iocp创建，在*nix下则基于多线程创建
- 对于一般的非异步的函数，函数由我们自行调用，如在for循环体中调用方法
  - 对于node中的异步i/o调用，回调函数却不由开发者来调用
  - 从js发起调用到内核执行完i/o操作的过渡过程中，存在中间产物，叫做请求对象
- 从js调用node核心模块，核心模块调用c++内建模块，内建模块通过libuv进行系统调用，这是node里经典的调用方式
  - js调用立即返回，由js层面发起的异步调用第一阶段就此结束
  - js线程可继续执行当前任务的后续操作，当前的i/o操作在线程池中等待执行，不管它是否阻塞i/o，都不会影响到js线程的后续执行
  - 请求对象是异步i/o过程中的重要中间产物，所有状态都保存在这个对象中，包括送入线程池等待执行以及i/o操作完毕后的回调处理
- 线程池中的i/o操作完毕后，会将获取的结果存储在req->result属性上，然后通知iocp当前操作已完成
- 事件循环、观察者、请求对象、i/o线程池共同构成了node异步i/o模型的基本要素
  - windows下通过iocp来向系统内核发送i/o调用和从内核获取已完成的i/o操作，配以事件循环，以此完成异步i/o的过程
  - 在linux下通过epoll实现这个过程
  - 不同的是线程池在windows下由内核iocp直接提供，*nix下由libuv自行实现
- 前面的介绍基本勾勒出了事件驱动的实质，即通过主循环加事件触发的方式来运行程序
  - node通过事件驱动的方式，无需为每个请求创建额外对应的线程，可以省掉创建线程和销毁线程的开销
  - 同时操作系统在调度任务时因为线程较少，上下文切换代价很低
  - 这使得服务器能够处理大量请求，这是node高性能的原因之一

- 异步编程的主要解决方案
  - 发布订阅模式/事件监听器
    - node自身的events模块
  - promise/deferred模式
    - 使用事件的方式，执行流程需要预先被设定，即使是分支，也需要预先设定，这是由发布订阅的运行机制所决定的
    - 在原始api中一个事件只能处理一个回调，而通过deferred对象，可以对事件加入任意的业务处理逻辑
    - promise/deferred模式在一定程度上缓解了回调函数嵌套过深的问题
    - promise的缺点是需要为不同的场景封装不同的api，没有原生事件灵活
  - 流程控制库
    - async
    - step
    - wind
- 在node中使用的js对象都是通过v8自己的方式来进行分配和管理的
  - 在v8中所有js对象都是通过堆来进行分配的
  - v8为何要限制堆的大小，深层原因是v8的垃圾回收机制的限制
- 在网络流和文件流的操作中，需要处理大量的二进制数据，buffer是像Array的对象，主要用于操作字节
  - buffer性能相关的部分用c++实现，非性能相关的部分用js实现
  - buffer所占用的内存不是通过v8分配的，属于堆外内存
- node和nginx都是基于事件驱动的方式来实现的，采用单线程避免了不必要的内存开销和上下文切换开销
- 基于事件的模型存在的问题是cpu的利用率和进程的健壮性
- 面对单进程单线程对多核使用不足的问题，前人的经验是启动多进程即可
  - 理想状态下每个进程各自利用一个cpu，以此实现多核cpu的利用
  - 弄得提供了child_process模块，fork()方法实现进程的复制
  - 通过fork()复制的进程都是一个独立的进程，这个进程有着独立而全新的v8实例
  - 它需要至少30ms的启动时间和至少10mb的内存
  - 依然要切记fork()进程是昂贵的，好在node通过事件驱动的方式在单线程上解决了大并发的问题，
    - 这里启动多个进程只是为了充分将cpu资源利用起来，而不是为了解决并发问题
- web worker允许创建工作线程在后台运行，不影响主线程上的ui渲染
- node中实现进程间通信IPC的技术是管道pipe
  - 具体细节实现由libuv提供，在win下由命名管道实现，*nix系统采用unix domain socket实现

# faq-not-yet

# faq-repeat

## node environment vs browser environment

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

# faq

## [node.js和前端js有什么区别？](https://www.zhihu.com/question/60164095/answers/updated)

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

# discuss

- ## [Node中的event-loop执行情况可以用microtask和macrotask方式来解释么？](https://www.zhihu.com/question/63684913)
- microtask 相关是V8提供的API，虽然规范里提了同名以及同意义的microtask，这不表示node就用了它，更被别说 macrotask 这种 V8 里没有 API 了。
  - 既然 node 与 libuv 相关没暴露这个，那就跟这俩没关系，俩没关系的事儿咋合一起解释呢。

- ## [浏览器与Node的事件循环(Event Loop)有何区别?](https://zhuanlan.zhihu.com/p/54882306)
- 进程是CPU资源分配的最小单位；线程是CPU调度的最小单位
- 以Chrome浏览器中为例，当你打开一个Tab页时，其实就是创建了一个进程，
  - 一个进程中可以有多个线程，比如渲染线程、JS 引擎线程、HTTP 请求线程等等。
  - 当你发起一个请求时，其实就是创建了一个线程，当请求结束后，该线程可能就会被销毁。
- 浏览器内核是多线程，在内核控制下各线程相互配合以保持同步，一个浏览器通常由以下常驻线程组成：
  - GUI 渲染线程
  - JavaScript 引擎线程
  - 定时触发器线程
  - 事件触发线程
  - 异步 http 请求线程

- ### 浏览器中的 Event Loop
- 事件循环中的异步队列有两种：macro（宏任务）队列和 micro（微任务）队列
- 宏任务队列可以有多个，微任务队列只有一个。
- 常见的 macro-task 
  - 比如：setTimeout、setInterval、 setImmediate、script（整体代码）、 I/O 操作、UI 渲染等。
  - 常见的 micro-task 
  - 比如: process.nextTick、new Promise().then(回调)、MutationObserver(html5 新特性) 等。
- 每一次循环都是一个这样的过程 (随时优先执行micro)
  - 当某个宏任务执行完后, 会查看是否有微任务队列。
    - 如果有，先执行微任务队列中的所有任务，
    - 如果没有，会读取宏任务队列中排在最前的任务，
    - 执行宏任务的过程中，遇到微任务，依次加入微任务队列。
  - 栈空后，再次读取微任务队列里的任务，依次类推。

- ### Node中的 Event Loop
- Node采用V8作为js解析引擎，而I/O处理方面使用了自己设计的 libuv
  - libuv是一个基于事件驱动的跨平台抽象层，封装了不同操作系统一些底层特性，对外提供统一的API，事件循环机制也是它里面的实现
  - libuv库负责Node API的执行。它将不同的任务分配给不同的线程，形成一个 Event Loop（事件循环），以异步的方式将任务的执行结果返回给V8引擎。
- libuv引擎中的事件循环分为6个阶段，它们会按照顺序反复运行。
  - 每当进入某一个阶段的时候，都会从对应的回调队列中取出函数去执行。
  - 当队列为空或者执行的回调函数数量到达系统设定的阈值，就会进入下一阶段。
- node事件循环阶段
  - timers 阶段
    - 会执行 setTimeout 和 setInterval 回调，并且是由 poll 阶段控制的。
    - 在Node中定时器指定的时间也不是准确时间，只能是尽快执行。
  - I/O callbacks 阶段
    - 处理一些上一轮循环中的少数未执行的 I/O 回调
  - idle, prepare 阶段
    - 仅 node 内部使用
  - poll 阶段
    - 获取新的 I/O 事件, 适当的条件下node将阻塞在这里
  - check 阶段
    - 执行 setImmediate() 的回调
  - close callbacks 阶段
    - 执行 socket 的 close 事件回调
- 日常开发中的绝大部分异步任务都是在timers、poll、check这3个阶段处理的
- process.nextTick
  - 这个函数其实是独立于 Event Loop 之外的，它有一个自己的队列，
  - 当每个阶段完成后，如果存在 nextTick 队列，就会清空队列中的所有回调函数，并且优先于其他 microtask 执行

- ### Node与浏览器的 Event Loop 差异
- 浏览器环境下，microtask 的任务队列是每个 macrotask 执行完之后执行。
- 而在Node.js 中，microtask 会在事件循环的各个阶段之间执行，也就是一个阶段执行完毕，就会去执行microtask队列的任务。
- 浏览器和Node环境下，microtask任务队列的执行时机不同
  - Node端，microtask 在事件循环的各个阶段之间执行
  - 浏览器端，microtask 在事件循环的 macrotask 执行完之后执行

- ## [2020年Node.js凉了吗？凉到什么程度了？](https://www.zhihu.com/question/416267787/answers/updated)
- 华为的鸿蒙系统的手环端采用了Javascript开发语言，模拟器使用Node.js
- 技术是由商业利益驱动的，大公司很多技术都应用了node，想要凉先问问大公司愿不愿意花时间和钱去重构项目
- 前公司曾用node做纯后端，后来发现非常非常难招人，最后转java了。
- ref
  - [2019年了，Node.js现在能不能用来做纯后端开发？](https://www.zhihu.com/question/322502957/answers/updated)
  - [现在将node. js作为纯后端的公司多吗？](https://www.zhihu.com/question/431630885/answers/updated)
  - [为什么互联网公司开始用node.js做web服务的中间层？](https://www.zhihu.com/question/264563447/answers/updated)

# pieces

-  ## node-path
- `path.join(path1，path2，path3.......)`
  - 用平台特定的分隔符把全部给定的path片段连接到一起，并规范化生成的路径
  - 先解析相对路径..，再拼接返回，path片段/docs, ./docs, docs三种方式处理无差别
  - path片段前的 `./` 可有可无，只进行路径拼接
  - `path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');`
    - 返回: `/foo/bar/baz/asdf`
- `path.resolve([from...],to)`
  - 按参数从左向右，把路径片段的序列解析为一个**绝对路径**，一定生成绝对路径
  - 先解析路径，再生成绝对路径返回，./docs, docs相同，/docs会作为绝对路径起点
  - `path.resolve('/foo', '/bar', 'baz')` 会返回 `/bar/baz`
  - `path.relative(from,to)`, 可看做resolve的逆运算，返回to目录的相对路径
- `__dirname`
  - Node.js中的文件路径大概有 __dirname, __filename, process.cwd(), ./ 或者 ../
    - 前3者都是绝对路径
  - `__dirname` ：    当前执行文件所在目录的绝对路径
  - `__filename` ：   当前执行文件的带有完整绝对路径文件名的绝对路径
  - `process.cwd()` ：当前执行node命令时候的文件夹目录名，绝对路径 
  - `./` ：跟process.cwd()一样，返回node命令时所在的文件夹的绝对路径
  - `require(./a.js)` ：当node遇到require时，会相对当前执行文件查找
  - 建议：只在require()中才使用相对路径(./, ../)的写法，其他地方一律绝对路径

## events

- Much of the Node.js core API is built around an idiomatic(地道的，符合习惯的，独特的) asynchronous event-driven architecture 
  - in which certain kinds of objects (called "emitters") emit named events that cause Function objects ("listeners") to be called.
  - For instance: 
    - a `net.Server` object emits an event each time a peer connects to it; 
    - a `fs.ReadStream` emits an event when the file is opened; 
    - a `stream` emits an event whenever data is available to be read.
- All objects that emit events are instances of the `EventEmitter` class. 
  - These objects expose an `eventEmitter.on()` function that allows one or more functions to be attached to named events emitted by the object. 
- When the `EventEmitter` object emits an event, all of the functions attached to that specific event are called **synchronously**. 
  - Any values returned by the called listeners are ignored and discarded.
- The `EventEmitter` calls all listeners synchronously in the order in which they were registered. 
  - This ensures the proper sequencing of events and helps avoid race conditions and logic errors. 
  - When appropriate, listener functions can switch to an asynchronous mode of operation using the `setImmediate()` or `process.nextTick()` methods

``` JS
const myEmitter = new MyEmitter();
myEmitter.on('event', (a, b) => {
  setImmediate(() => {
    console.log('this happens asynchronously');
  });
});
myEmitter.emit('event', 'a', 'b');
```

- The `EventEmitter` class is defined and exposed by the `events` module
  - All EventEmitters emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.
  - The `EventEmitter` instance will emit its own '`newListener'` event before a listener is added to its internal array of listeners.

- `emitter.emit(eventName[, ...args])` (v0.1.26)
  - Synchronously calls each of the listeners registered for the event named `eventName`, 
    - in the order they were registered, passing the supplied arguments to each.

- `emitter.addListener(eventName, listener)` (v0.1.26)
  - Alias for `emitter.on(eventName, listener)` (v0.1.101)
  - Adds the `listener` function to the end of the listeners array for the event named `eventName`. 
  - No checks are made to see if the listener has already been added. 
  - Multiple calls passing the same combination of eventName and listener will result in the listener being added, and called, multiple times.
  - By default, event listeners are invoked in the order they are added. 
  - The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

- `emitter.once(eventName, listener)`
  - Adds a one-time `listener` function for the event named `eventName`. 
  - The next time `eventName` is triggered, this listener is removed and then invoked.

- `emitter.off(eventName, listener)` (v10.0.0)
  - Alias for `emitter.removeListener(eventName, listener)` (v0.1.26)
  - Removes the specified `listener` from the listener array for the event named `eventName`.
  - removeListener() will remove, at most, one instance of a listener from the listener array. 
  - If any single listener has been added multiple times to the listener array for the specified eventName, then removeListener() must be called multiple times to remove each instance.
  - Once an event is emitted, all listeners attached to it at the time of emitting are called in order. 
    - This implies that any removeListener() or removeAllListeners() calls after emitting and before the last listener finishes execution will not remove them from emit() in progress. 
    - Subsequent events behave as expected.

``` JS
const myEmitter = new MyEmitter();

const callbackA = () => {
  console.log('A');
  myEmitter.removeListener('event', callbackB);
};
const callbackB = () => {
  console.log('B');
};

myEmitter.on('event', callbackA);
myEmitter.on('event', callbackB);

// callbackA removes listener callbackB but it will still be called.
// Internal listener array at time of emit is[callbackA, callbackB]
myEmitter.emit('event');
// Prints:
//   A
//   B

// callbackB is now removed.
// Internal listener array is [callbackA]
myEmitter.emit('event');
// Prints:
//   A
```

  - Because listeners are managed using an internal array, calling this will change the position indices of any listener registered after the listener being removed. 
  - This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the emitter.listeners() method will need to be recreated.
  - When a single function has been added as a handler multiple times for a single event, removeListener() will remove the most recently added instance. 

- **NodeEventTarget vs. EventEmitter**
- A NodeEventTarget is not an instance of EventEmitter and cannot be used in place of an EventEmitter in most cases.
  - Unlike EventEmitter, any given listener can be registered at most once per event type. Attempts to register a listener multiple times are ignored.
  - The NodeEventTarget does not implement any special default behavior for events with type 'error'.

# 多线程

- Node.js保持了JavaScript在浏览器中单线程的特点
  - 它的优势是没有线程间数据同步的性能消耗也不会出现死锁的情况
  - 所以它是线程安全并且性能高效的
- 单线程有它的弱点，无法充分利用多核CPU资源，CPU密集型计算可能会导致I/O阻塞，以及出现错误可能会导致应用崩溃。
- 为了解决单线程的缺点，现在提出了很多解决方案
- 浏览器端： HTML5制定了Web Worker标准
  - Web Worker的作用就是为JavaScript创造多线程环境，允许主线程创建Worker线程，将一些任务分配给后者运行 
- Node端：采用了和Web Worker相同的思路来解决单线程中大量计算问题 ，官方提供了child_process模块和cluster模块
  - cluster底层是基于child_process实现
  - child_process、cluster都是用于创建子进程，然后子进程间通过事件消息来传递结果
  - 这个可以很好地保持应用模型的简单和低依赖，从而解决无法利用多核CPU和程序健壮性的问题
  - cluster底层就是child_process，master进程做总控，启动1个agent和n个worker，agent来做任务调度，获取任务，并分配给某个空闲的worker来做。
    - 每个worker进程通过使用 `child_process.fork()` 函数，基于 IPC 实现与master进程间通信
    - fork出的子进程拥有和父进程一致的数据空间、堆、栈等资源，但是是独立的，也就是说二者不能共享这些存储空间。那我们直接用fork自己实现不就行了。
    - 这样的方式仅仅实现了多进程。多进程运行还涉及父子进程通信，子进程管理，以及负载均衡等问题，这些特性cluster帮你实现了
- child_process模块通过它可以开启多个子进程，在多个子进程之间可以共享内存空间，可以通过子进程的互相通信来实现信息的交换
- Node10提供了实验性质的 worker_threads 模块，才让Node拥有了多工作线程，从Node12开始成为正式标准
  - Workers (threads) are useful for performing CPU-intensive JavaScript operations. 
  - They will not help much with I/O-intensive work. 
  - Node.js’s built-in asynchronous I/O operations are more efficient than Workers can be.
- Node.js 通过提供 cluster、child_process API 创建子进程的方式来赋予Node.js “多线程”能力
  - 但是这种创建进程的方式会牺牲共享内存，并且数据通信必须通过json进行传输，有一定的局限性和性能问题
- 基于此，Node.js提供了worker_threads，它比child_process或cluster更轻量
  - 与child_process或cluster不同，worker_threads可以有效地共享内存，通过传输ArrayBuffer实例或共享SharedArrayBuffer实例来实现
  - JavaScript和Node.js没有线程，只有基于Node.js架构的多工作线程
