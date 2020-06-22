---
tags: [electron]
title: log-deving-electron
created: '2020-05-18T09:49:23.005Z'
modified: '2020-06-22T08:11:21.145Z'
---

# log-deving-electron

## faq
- electron vs cef
    - The Chromium Embedded Framework (CEF) is a project that turns Chromium into a library, and provides stable APIs based on Chromium's codebase. Very early versions of Atom editor and NW.js used CEF.
    - To maintain a stable API, **CEF hides all the details of Chromium and wraps Chromium's APIs with its own interface**. 
    - So when we needed to access underlying Chromium APIs, like integrating Node.js into web pages, the advantages of CEF became blockers.
    - So in the end both Electron and NW.js switched to using Chromium's APIs directly.
    - ref
      - https://www.electronjs.org/blog/electron-internals-building-chromium-as-a-library
- electron中可以使用web worker吗？
    - 结论是：可以用，但不推荐
    - It is possible to use Node.js features in Electron's Web Workers, to do so the nodeIntegrationInWorker option should be set to true in webPreferences
    - All built-in modules of Node.js are supported in Web Workers
    - However none of Electron's built-in modules can be used in a multi-threaded environment.
    - Any native Node.js module can be loaded directly in Web Workers, but it is strongly recommended not to do so. 
        - Most existing native modules have been written assuming single-threaded environment, using them in Web Workers will lead to crashes and memory corruptions.
        - Note that even if a native Node.js module is thread-safe it's still not safe to load it in a Web Worker because the process.dlopen function is not thread safe.
        - The only way to load a native module safely for now, is to make sure the app loads no native modules after the Web Workers get started.
    - ref
        - https://www.electronjs.org/docs/tutorial/multithreading

## pieces

- Electron运行package.json中的main脚本中的进程被称为主进程，该进程在应用整个生命周期只会存在唯一一个，负责面窗口的创建、控制、销毁等管理行为，同时也能控制整个应用的生命周期。
    - 主进程本质上是一个 Node.js 进程，该进程充分利用了 Node.js 的跨平台特性，在其 API 的底层，抹掉了不同操作系统中的差异
    - 主进程同时提供一套跨平台的接口，能控制各个操作系统中的原生资源，如：对话框、菜单、文件拖拽等，使得 Electron 的用户体验极大的接近了原生应用。
    - Electron应用的入口是一个js文件（NW.js入口是html文件），运行这个入口文件（通常会是package.json里的main脚本）的进程称作主进程，在主进程使用BrowserWindow模块可以创建并管理web页面，也就是应用的GUI
- 当主进程每创建一个独立 BrowserWindow 实例，Electron都会初始化一个独立的渲染进程，隔离了不同窗口之间的环境
    - 在主进程创建的一个个web页面也都运行着自己的进程，即渲染进程，渲染进程各自独立，各自管理自己的页面，类似浏览器一个的tab
    - 可隐藏窗口，然后让其在背后运行代码
- webview
    - Display external web content in an isolated frame and process.
- preload
    - preload属性能够在webview内所有脚本执行之前，先执行指定的脚本
    - preload环境是一个既能用Node API，又能访问DOM、BOM的特殊环境，我们熟悉的另一个类似环境是renderer
    - preload属性的特点是只在第一次加载页面时执行，后续加载新页不会再执行preload脚本
- Setting `nodeIntegration` to `false` will disable node.js in the renderer process - i.e. your app can only do what a web browser will do.
    - BrowserWindow提供的preload的配置是为了在页面第一次加载文档之前预先加载js脚本文件,preload配置的脚本文件路径，只能为本地文件，其协议必须是file:、asar:二者之一
    - preload脚本仍然有能力去访问所有的 Node APIs, 即使配置`nodeIntegration: false`。但是当这个脚本执行执行完成之后，通过Node 注入的全局对象（global objects）将会被删除



## 进程通信
- 不同于一般的原生应用开发，Electron的渲染进程与主进程分别属于独立的进程中
- Electron官方提供的进程间通讯方式
    - LocalStorage, window.postMessage
        - 一般通过这两种方式进行窗口间的数据通讯
    - 使用ipcMain和ipcRenderer模块
        - 该方式属于Electron特有传输方式，不适用于其他前端开发场景
        - 在渲染进程中使用ipcRender模块向主进程发送消息，主进程中使用ipcMain接收消息进行操作
        - 用ipc传递大量的数据，会有很大的性能问题
    - 直接在渲染进程使用remote模块，不推荐
        - 在渲染进程中能显式调用主进程中的模块代码，类似于Java中的RMI
        - remote底层仍然使用IPC作为进程间通讯的方式，使用不当容易造成内存泄漏
- 渲染进程之间的通信方式
    - 如果数据不需要实时性，只是渲染进程之间数据的共享
        - use HTML5 APIs which are already available in browsers
        - Storage API, localStorage, sessionStorage, and IndexedDB.
    - 如果要求实时性，需要配合前几种方式实现
- 使用remote通信方式，随着主进程逻辑增多，为什么页面开始逐渐出现了卡顿的现象
    - remote模块返回的每个对象 (包括函数) 表示主进程中的一个对象 (我们称它为远程对象或远程函数)。 当调用远程对象的方法时, 调用远程函数, 或者使用远程构造函数 (函数) 创建新对象时, 实际上是在发送同步进程消息。
    - `remote.getGlobal()`内部实现用的是`ipcRendererInternal.sendSync(command, contextId, name)`
    - Electron确保只要渲染进程中的remote远程对象存在（换句话说，没有被垃圾收集），主进程中的相应对象将不会被释放。 当远程对象被垃圾回收后，主进程中的相应对象将被解除引用。
    - 在主进程返回对象后，为什么依然需要保留对象呢？渲染进程在接收到remote模块返回的对象时并不是解析成真实的对象，而是更接近于主进程中对象的镜像对象，所有真正的value都是通过发送rpc消息到主进程中，主进程再将当前真正的值返回到渲染进程中。
    - 当渲染进程中访问其remoteObject中的方法或者属性时，内部都会通过 ipcRendererInternal.sendSync 同步通知主进程中，根据其中的隐藏字段 atomId 在主进程中找到对应的真实对象，获取属性值或者执行其对应方法，然后再通过 event.returnValue 返回数据。其内部实现与remote执行远程方法基本一致。
    - 所以，我们确定了渲染进程长时间卡顿，是因为我们在渲染进程中遍历remote对象中的属性，内部执行大量sendSync方法导致渲染进程一致处于等待状态，从而阻塞了渲染进程其他任务的执行。
- 因为业务代码中直接使用remote模块导致性能收到了严重影响，那我们是否只需要改用IPC方式调用主进程中的逻辑就好了呢？
    - Chromium IPC 在设计上是使用完全异步的方式，理论上不会出现上述所提及的问题
    - 实际测试结果表明，即便不使用remote模块，主进程的卡顿仍可能导致渲染进程无法响应用户的点击
    - 在操作系统设计中，不同的进程理论上是互不影响的，它们各自获取到的资源都是独立的，那么按照正常理解中，Electron的主进程阻塞是不应该影响到渲染进程的运行的。可是渲染进程跟主进程并非真正独立的进程，它们同属于一个Electron应用，那么我们有合理的怀疑，在 Electron 内部，必定存在内部的进程间通讯，而且这些通讯正是导致渲染进程无法响应的罪魁祸首。
    - 通过搜索Electron源码可以发现，Electron内部也存在的很多的模块使用了IPC的sendSync 的方法，而这些方法每一个都可能导致渲染进程无法响应
- 解决方案
    - 在频繁访问的方法中建议使用 ipcRenderer/ipcMain 进行通讯
        - 由于Electron中 ipcRenderer 以及 ipcMain 使用的是 chroumium 中的文件句柄的方式进行跨进程数据传递，该方式在设计上采用的是完全异步的方式，同时性能对比普通的 socket 有明显的优势，因此项目中在主进程以及渲染进程中的大量使用也不会对性能有明显影响
    - 不要在主进程中进行CPU密集型操作
        - 主进程是负责控制应用窗口以及整个应用程序的生命周期，并非处理业务逻辑的。
        - 在项目初期我们曾错误认为主进程是作为程序后台去使用的，因此我们将业务代码统一放到主进程中运行，一旦业务逻辑出现需要CPU长时间处理的，甚至会导致程序处于无响应状态。
        - 因此我们将业务逻辑都转移到了主进程fork出来的子进程进行处理，避免了可能出现卡顿的情况。
    - remote调用的主进程方法尽量声明为async方法
        - 因为remote底层使用的是 sendSync 方法，该方法会让渲染进程一直处于阻塞状态直到主进程方法执行完成并返回数据，因此如果主进程中的方法是IO操作或者是CPU密集型的，则会导致渲染进程一直处于阻塞状态无法处理用户点击事件。
        - 而声明为 async 方法，则会让主进程方法立即返回一个Promise对象，无需等待方法执行完成，极大地减少了渲染进程的等待时间
    - 需要调用remote的主进程方法，不要返回大量数据
        - 在使用remote获取主进程的数据，在渲染进程该对象会处于一种镜像的状态，所有的属性获取、变更同样需要跨进程的访问。这里并不仅限于调用主进程同步的方法，同时包括主进程 async 的方法。
        - remote调用 async 方法虽然能立即返回Promise对象，无需渲染进程等待主进程方法执行完成，可是其执行完的数据仍然会通过 Promise 对象中的 then 方法传递执行后的数据。在该数据中，属性值仍然是使用 remote 的机制。
        - 因此大量数据的获取我们推荐使用 ipcRenderer/ipcMain 进行获取
- 解决方案优化
    - 随着应用规模的增长，主进程最终会承担更多的业务逻辑，而不可避免的会导致在某个场景下出现CPU密集型的操作。这个时候，探讨将CPU密集性任务分散开，是不太现实的。我们开始设想，能否 “架空” 主进程，让它闲下来呢？
    - 在一般的客户端开发中，如果进程任务过于繁重，都会通过多开线程的方式减少进程阻塞的场景，而 node.js 也意识到单线程所带来的局限性，在后面的版本引入了 cluster 的功能模块，为 node.js 带来的负载均衡的子进程特性。而其后甚至在最近的 10.5.0 版本引入 worker_threads 的实验性模块，为 node.js 带来的真正的多线程。
    - worker_threads
        - worker_threads多线程的支持让Electron能更加接近原生应用
    - cluster
        -  cluster，可以让多个子进程使用同一个端口，并且为其提供了负载均衡的特性，使得 node.js 能充分利用多核CPU的特性。但主进程并没有闲下来。
    - child_process
        - child_process模块为node.js提供了原始的子进程方式。通过测试我们发现，在子进程中，即使长时间运行 CPU 密集型的操作，渲染进程以及主进程都不会受到应用。经过一系列的重构，我们将绝大部分业务逻辑转移到子进程中，真正彻底地解决了CPU密集型运算导致的渲染进程卡顿的问题。
- ref 
    - https://www.iguan7u.cn/2019/06/30/Electron-%E8%BF%9B%E7%A8%8B%E9%97%B4%E9%80%9A%E8%AE%AF%E8%AF%A6%E8%A7%A3/

## Electron开发总结
- 主进程任务
    - 窗口管理及生命周期控制
    - 进程间通信
    - 全局通用服务
    - 一些只能或适合在主进程做的事情
        - 例如全局快捷键处理、托盘、session、浏览器下载、截屏、右键菜单
    - 维护一些必要的全局状态
        - 主题、语言、当前用户、用户设置
    - 上面说的通用混合层也跑在这个进程。通过 Node C++ 插件暴露接口。
- 渲染进程任务
    - 负责Web页面的渲染, 具体页面的业务处理
- Service Worker任务
    - 负责静态资源缓存。缓存一些网络图片、音频。保证静态资源的稳定加载
- 避免白屏
    - 使用骨架屏：可以设置背景色或者延迟显示窗口，来避免闪烁
    - 惰性加载：优先加载核心的功能，保证初次加载效率
    - 代码分割 + 预加载
    - 延后加载Node模块：可以选择使用打包工具优化和合并Node模块
    - 划分加载优先级
- 性能优化
    - 静态资源缓存：Service-Worker + Workbox 
    - 预加载机制
        - 渲染隐藏的Tab，延后加载的模块代码，惰性加载的图片，未激活的会话，执行低优先级的任务
        - react requestIdleCallback
    - 避免同步操作
        - Electron可以通过NodeJS进行I/O操作，但是我们一定要尽量避免同步I/O
        - 例如同步的文件操作、同步的进程间通信。它们会阻塞页面的渲染和事件交互
    - 减少主进程负荷
        - Electron的主进程是所有窗口的父进程，它负责调度各种资源。如果主进程被阻塞，将影响整个应用响应性能
        - 所以不要让主进程干脏活累活，能在渲染进程做的，就在渲染进程做。千万避免在主进程中跑计算密集任务和同步I/O
    - 分离CPU密集型操作到单独进程或Worker, 避免阻塞UI
    - 用空间换时间
        - 打开登录页面时先在后台预热
        - 将某些窗口放到了屏幕之外
        - 对于频繁开启/关闭的窗口，也可以使用窗口池来优化。比如 Webview 页面，打开的一个 Webview 页面时，会优先从窗口池中选取，当窗口池为空时才创建新的窗口, 后面页面关闭后会再放回窗口池中，方便后续复用
        - 对于业务无关的、通用的窗口，也可以采用常驻模式，例如通知，图片查看器。这些窗口一旦创建就不会释放，打开效果会更好
- 通信优化
    - 不要滥用remote
        - 其底层基于同步的IPC
        - 属性是动态获取的，为了确保你能够获取到最新的值，remote底层并不会进行缓存，而是每次获取一个属性就动态到主进程中取
    - 封装IPC库
        - 异步
        - 消息合并。合并事件推送，批量传递
        - 序列化。直接传递JSON字符串，Electron内部序列化稍微有点复杂，比如会处理Buffer等特殊类型。
        - 一致化的、简单易用的 API。使用一样在接口支持主进程与渲染进程，以及渲染进程与渲染进程之间双向通信
- 打包体积过大
    - 尝试第三方精简后的electron
- 内存消耗大
    - 由于Chromium采用多进程架构，因此会涉及到进程间通信问题。
        - Browser进程在启动Render进程的过程中会建立一个以 UNIX Socket 为基础的 IPC 通道。
        - 有了 IPC 通道之后，接下来 Browser 进程与 Render 进程就以消息的形式进行通信。
        - 我们将这种消息称为 IPC 消息，以区别于线程消息循环中的消息。
        - 通讯传递数据的过程中，由于不是共享内存（因为 IPC 是基于 Socket 的），导致出现多份数据副本
- ref
    - https://juejin.im/post/5e0010866fb9a015fd69c645

