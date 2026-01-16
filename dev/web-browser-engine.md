---
title: web-browser-engine
tags: [browser, web, webkit]
created: 2020-06-27T08:19:22.900Z
modified: 2020-12-21T07:44:53.873Z
---

# web-browser-engine

# guide
- resources
  - [Web Browser Engineering book](https://browser.engineering/)
  - [Let's build a browser engine! Part 1: Getting started _201408](https://limpet.net/mbrubeck/2014/08/08/toy-layout-engine-1.html)
# discuss-stars
- ## 准备把《手写简易的浏览器》掏出来。
- https://www.zhihu.com/pin/1382344579656626176
- 其实浏览器或者跨端引擎也好都主要完成两件事情：渲染和逻辑（包括交互逻辑），两者之间不能相互阻塞，需要一个 event loop。
- 整体思路是：
  - 实现一个html parser，把html字符串 parse 成 dom tree，实现一个css parser，把css字符串 parse 成 css tree，然后实现渲染引擎，也就是把两者合并成 render tree，计算出坐标，之后通过 canvas 来渲染。这是渲染的部分。
  - js字符串的解释执行，首先需要一个js parser，这个就不自己实现了，用 acron 就行，之后自己做解释执行。这是逻辑部分。
- 渲染和逻辑执行需要不能相互阻塞，渲染要保证 16ms 渲染一次，自己实现一个 event loop，每次取一个任务来执行，之后执行所有微任务，然后检查下是否要渲染。
  - 这个 event loop 要不断的用 setTimeout 来异步递归（同步的死循环会卡死）。
  - 这样就能不断的进行新的帧的渲染和js逻辑的执行。
  - 上面跑通了之后要实现网络下载的功能，从一个 url 来下载 html，解析出其中的 css 和 js 单独下载。这部分相对简单。
- 之后要实现一个静态（或者动态）服务器来下发这些资源。
- 最后在浏览器里面做一个浏览器的界面，有地址栏，有内容区等等。
# browser-engine-overview
- 苹果曾经使用Gecko，嫌弃Gecko曾经有段时间太臃肿，就把KDE的HTML引擎KHTML、JavaScript引擎KJS加工过来，发布了WebCore+JavaScriptCore的WebKit并开源。
- 后来Google加入使用WebCore引擎，再后来Chromium又分支出去Blink引擎，JavaScript引擎是Google开源的V8。

- 浏览器的主要结构
  - 用户界面
    - 包括地址栏、前进/后退按钮、书签菜单等。
    - 除浏览器主窗口显示的您请求的页面外，其他显示的各个部分都属于用户界面
  - 浏览器引擎 
    - 在用户界面和呈现引擎之间传送指令。
  - 呈现引擎 
    - 负责显示请求的内容。
    - 如果请求的内容是HTML，它就负责解析HTML和CSS内容，并将解析后的内容显示在屏幕上。
    - 与其他浏览器不同的是：chrome浏览器中每个tab页对应一个呈现引擎实例，每个tab页都是一个单独的进程
  - 网络 
    - 用于网络调用，比如HTTP请求。其接口与平台无关，并为所有平台提供底层实现。
  - 用户界面后端 
    - 用于绘制基本的窗口小部件，比如组合框和窗口。
    - 其公开了与平台无关的通用接口，而在底层使用操作系统的用户界面方法。
  - JavaScript解释器
    - 用于解析和执行JavaScript代码。
  - 数据存储
    - 这是持久层。浏览器需要在硬盘上保存各种数据，例如Cookie。
    - HTML5定义了网络数据库，这是一个完整但轻便的浏览器内数据库

- 浏览器的基本组成是GUI和html解析引擎，后来js引擎也被独立出来。
- Chrome的html解析引擎是WebKit fork出来的Blink，js引擎是v8。而GUI框架它是在哪个操作系统上就用那个操作系统的主流框架，比如在mac上就是Cocoa，在linux上就是gtk，windows它基于win32 API开发了一个自己的框架
- 目前的edge，这三样大概就是edgeHTML, chakra，和win32 API包括mfc wpf这一套东西
- Firefox的html引擎是gecko，js是spidermonkey，GUI是XUL, XUL是一个基于各平台得底层api开发的一个高层的跨平台的图形界面框架，所以还有好些软件是用XUL来做自己的界面。而且XUL和gecko spidermonkey耦合的挺深，要用基本上就都要用。

- Firefox
  - HTML引擎：Mariner -> Raptor -> NGLayout -> Gecko
  - JavaScript引擎：Mocha -> SpiderMonkey
  - JIT即时编译器: TraceMonkey -> JaegerMonkey -> IonMonkey+OdinMonkey
# JavaScriptCore 

## JavaScriptCore wiki

- https://trac.webkit.org/wiki/JavaScriptCore

- JavaScriptCore is the built-in JavaScript engine for WebKit. 
  - It currently implements ​ECMAScript as in ​ECMA-262 specification.
- JavaScriptCore is often referred with different names, such as ​SquirrelFish and ​SquirrelFish Extreme. 
  - Within the context of Safari, Nitro and Nitro Extreme (the marketing terms from Apple) are also commonly used. 
  - However, the name of the project and the library is always JavaScriptCore.
# blog

## [Chrome浏览器架构](https://www.cnblogs.com/suihang/p/12718528.html)

- 早在2016年，Chrome官方团队使用“面向服务的架构”（简称SOA）的思想设计了新的Chrome架构。
  - 原来的各种模块会被重构成独立的服务（Service），访问服务必须使用定义好的接口，通过IPC来通信，
  - 每个服务都可以在独立的进程中运行，并且可以轻松拆分为不同的进程或聚合为一个进程。
  - 当Chrome在功能强大的硬件上运行时，它可能会将每个服务拆分为不同的进程以提供更高的稳定性，但是如果是在资源受限的设备上，Chrome会将服务整合到一个进程中以节省内存。
- 浏览器进程
  - 主要负责界面显示、用户交互、子进程管理，同时提供存储等功能。
  - 控制应用程序的“chrome”部分，包括地址栏，书签，后退和前进按钮, 还处理Web浏览器的隐形，特权部分，例如网络请求和文件访问。
- 渲染进程
  - 核心任务是将HTML、CSS 和JavaScript转换为用户可以与之交互的网页，排版引擎Blink和JavaScript引擎V8都是运行在该进程中，
  - 默认情况下，Chrome会为每个Tab标签创建一个渲染进程。
  - 出于安全考虑，渲染进程都是运行在沙箱模式下。
- GPU进程
  - 其实，Chrome刚开始发布的时候是没有GPU进程的。
  - 而GPU的使用初衷是为了实现 3D CSS 的效果
  - 随后网页、Chrome的UI界面都选择采用GPU来绘制，这使得GPU成为浏览器普遍的需求。
  - 最后，Chrome在其多进程架构上也引入了GPU进程。
- 网络进程
  - 主要负责页面的网络资源加载，之前是作为一个模块运行在浏览器进程里面的，直至最近才独立出来，成为一个单独的进程。
- 插件进程
  - 主要是负责插件的运行，因插件易崩溃，所以需要通过插件进程来隔离，以保证插件进程崩溃不会对浏览器和页面造成影响。
- utility进程
  - 有时候浏览器主进程需要做一些“危险”的事情，比如图片解码、文件解压缩。
  - 如果这些“危险”的操作发生了失败，会导致整个主进程发生异常崩溃，这是我们不愿意看到的。
  - 因此Chromium设计出了一个utility进程的机制。
  - 主进程临时需要做一些不方便的任务的情况下，可以启动一个utility进程来代替主进程执行，主进程与utility进程之间通过IPC消息来通信。
- 如果当前在资源充足的环境下还会有如下其他进程
  - UI进程、存储进程、设备进程、Audio进程、Video进程、Profile进程...
- 当前最新Chrome浏览器已经在面向服务的架构上了，可以打开Chrome的任务管理器看一下

## [深入理解浏览器工作原理](https://www.cnblogs.com/xiaohuochai/p/9174471.html)

- 浏览器主要组件包括：
  1. 用户界面 － 包括地址栏、后退/前进按钮、书签目录等，也就是所看到的除了用来显示所请求页面的主窗口之外的其他部分
  2. 浏览器引擎 － 用来查询及操作渲染引擎的接口
  3. 渲染引擎 － 用来显示请求的内容，例如，如果请求内容为html，它负责解析html及css，并将解析后的结果显示出来。
  4. 网络 － 用来完成网络调用，例如http请求，它具有平台无关的接口，可以在不同平台上工作。
  5. UI后端 － 用来绘制类似组合选择框及对话框等基本组件，具有不特定于某个平台的通用接口，底层使用操作系统的用户接口。
  6. JS解释器 － 用来解释执行JS代码。
  7. 数据存储 － 属于持久层，浏览器需要在硬盘中保存类似cookie的各种数据，HTML5定义了web database技术，这是一种轻量级完整的客户端存储技术
- 浏览器内核分成两部分：渲染引擎和js引擎
  - 由于js引擎越来越独立，内核就倾向于只指渲染引擎，负责请求网络页面资源加以解析排版并呈现给用户
  - 默认情况下，渲染引擎可以显示html、xml文档及图片，它也可以借助插件显示其他类型数据，例如使用PDF阅读器插件，可以显示PDF格式
- 主流渲染引擎
  - firefox使用gecko引擎
  - IE使用Trident引擎，2015年微软推出自己新的浏览器，原名叫斯巴达，后改名edge，使用edge引擎
  - opera最早使用Presto引擎，后来弃用
  - chrome\safari\opera使用webkit引擎，13年chrome和opera开始使用Blink引擎
  - UC使用U3引擎
  - QQ浏览器和微信内核使用X5引擎，16年开始使用Blink引擎
- 主流js引擎
  - 老版本IE使用JScript引擎，IE9之后用Chakra，edge浏览器早期使用Chakra
  - firefox使用spidermonkey系列引擎
  - safari使用的JavaScriptCore(aka. SquirrelFish)系列引擎
  - Opera使用Carakan引擎
  - chrome使用V8引擎，node封装了V8引擎
# ref
- [一文看懂Chrome浏览器工作原理 google4篇系列总结](https://juejin.cn/post/6844904046411644941)
- [五大主流浏览器及四大内核](https://zhuanlan.zhihu.com/p/99777087)
- [浏览器引擎列表](https://pic1.zhimg.com/80/v2-782b4462528d0ef134c71f3c216c6836_720w.jpg)
- [浏览器内核版本检测](https://ie.icoa.cn/)
- [Google图解：Chrome快是有原因的，科普浏览器架构_201809](https://toutiao.io/posts/uozd28/preview)
# discuss
- ## 

- ## 

- ## 

- ## 

- ## We built a browser with GPT-5.2 in Cursor. It ran uninterrupted for one week.
- https://x.com/its_bvisness/status/2011585317070127430
  - It's 3M+ lines of code across thousands of files. The rendering engine is from-scratch in Rust with HTML parsing, CSS cascade, layout, text shaping, paint, and a custom JS VM.
  - It still has issues and is of course very far from Webkit/Chromium parity, but we were astonished that simple websites render quickly and largely correctly.

- 3M+ lines of "from-scratch" code, yet it depends on:
  - Servo's HTML parser
  - Servo's CSS parser
  - QuickJS for JS
  - selectors for CSS selector matching
  - resvg for SVG rendering
  - egui, wgpu, and tiny-skia for rendering
  - tungstenite for WebSocket support
  - there are indeed over 3M lines of Rust before even considering dependencies. With dependencies there are over 9M lines of Rust. (So says cargo-loc, which I fear may be missing some dependencies due to workspace things.)
  - Also it clearly uses other libraries for layout and text shaping, etc. Not that I begrudge them that (everyone uses Harfbuzz) but it’s absolutely not from scratch.
- it also read Servo's code to "inform" itself

- Do you know how many dependencies chromium has?

- A smarter AI would have just forked Chromium and rebranded it...

- ## [Google Chromium 为什么要从 WebKit 中抽离，新建一个 Blink 分支？](https://www.zhihu.com/question/20920823/answers/updated)
- 因为历史原因，WebCore本身一开始就没有多线程或者多进程的概念，
  - 现有的架构对并行处理的支持非常困难，Google也认为必须对WebCore进行整体架构上的大改才能更好的支持并行处理，更充分利用多核CPU的能力，避免主线程过度拥挤
  - 为了避免单项任务长时间阻塞主线程，WebCore目前是用延时Timer的方式将一个复杂任务分解成多段来顺序执行，这种方式即不优雅，更无法充分利用多核的能力
- WebCore为了可以同时支持不同的JS虚拟机（如JSC和V8）导致了额外的性能开销和妨碍了对JS性能更多的改进
