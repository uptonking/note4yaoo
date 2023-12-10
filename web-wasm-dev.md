---
title: web-wasm-dev
tags: [dev, wasm]
created: 2020-12-31T19:17:26.544Z
modified: 2021-01-01T20:10:51.125Z
---

# web-wasm-dev

# guide

- tips
  - 前端开发后端化(Nodejs)，后端开发前端化(WebAssembly)都是比较明确的趋势，未来前后端开发将进一步融合。
  - cpp性能好但开发复杂，rust取代web还要看发展
# faq

## [Why WASM is not the future of Babylon.js__202108](https://babylonjs.medium.com/why-wasm-is-not-the-future-of-babylon-js-5832b09c9b10)

- [recently a question about WebAssembly (WASM) being the future](https://twitter.com/jpmolla/status/1420704185478156288)
  - @threejs: NO
  - @babylonjs: NO

- I wanted to use this blog to get more into details about why we do not think WASM is the future of JavaScript frameworks.

### WASM is a target not a user facing language

- WASM is meant to be a way for native developers (mostly C/C++) to compile their project into something that a browser can understand and execute.
- You can still read and maybe manually write WASM code as it is text based (the same way you can write byte code instead of writing C# or Java code).
- It is just **terribly inefficient** to use it that way. 
- Furthermore to reduce the size most of the time the WASM module are stored in a binary format.
- Memory management is on you, math functions are on you, string management is on you, etc.
  - Thanks to that, the performance of WebAssembly is supposed to execute faster than the JavaScript equivalent.
  - But unfortunately this is not something we can build a web framework on.
  - The main reason is that it is not easy (to say the least) to write WASM as it is not really meant to be written by humans.
- We had a long discussion about it on our repo where we were evaluating the option to use AssemblyScript
  - **The conclusion is that for now we see no good reason to port the entire engine to C++** (immense amount of work, killing all contributions we could get from the community, harder to maintain, etc.) to get the potential performance boost of WASM.

### WASM should not be called for small chunk of work

- We could argue that some parts of the engine should be written with WASM. Maybe the more compute intensive (like the math library).
- But there is a catch: Communication between JavaScript environment and WASM environment takes time. There is a bit of marshalling involved and that marshalling is expensive.

### WASM is hard to debug

- Because WASM is not easy to read, it it not easy to debug. 
- Chrome recently released some tools to help
- But in a nutshell you have to compile your native code with debug symbols to get some debugging support. 

### WASM could be fat

- Because WASM modules needs to provide everything (from memory management to math support) they can quickly become big assets that need to be loaded every time you start your page.
- As an example, we are currently working on supporting WebGPU. To do so we need to compile our shaders (written in GLSL) to WGSL and this requires us to load a 3MB WASM module (just remember that the entire babylonjs library is 3MB).

### But we still love WASM

- That being said we are not haters of WASM. 
- On the contrary we are using it in several areas of Babylon.js (mostly when we want to use existing native code that will do some atomic functions)
  - Draco decompression
  - KTX2 decoders
  - GLSL to WGSL compilation
  - Ammo physics engine
  - Navmesh and crowd agents
- Maybe in the future we will revisit our position if the situation changes but we will always make sure that the experience for web developers is top notch!

### discussion

- [Why WASM is not (for now) the future of Babylon.js](https://twitter.com/deltakosh/status/1423657621010087947)
- [Why WASM is not the future of Babylon.js](https://babylonjs.medium.com/why-wasm-is-not-the-future-of-babylon-js-5832b09c9b10)
- What about WebGPU?
  - Webgpu can be seen like webgl3 so no difference
- Nice writeup, yeah it’ll be hard to integrate WASM in unless we figure out a way to let WASM do its own thing for longer without too much communication with the JS side.
- Great read. Could not agree more!
People should not try to turn WASM into a cult. Tech is meant to be used and leveraged as required by the use cases. Do not try to turn something as great as WASM into an alleged silver bullet that will fit all problems. Be pragmatic engineers!

# dev
- 典型应用场景
  - 扩展浏览器端视音频处理能力
  - 游戏计算
- 90%的应用场景都不需要WebAssembly
  - https://www.infoq.cn/article/ytxfUWloi2wi00cQY-8a
  - js问题
    - 语法太灵活导致开发大型项目困难
    - 性能不能满足一些场景的需要
  - TypeScript是JavaScript的一个严格超集，并添加了可选的静态类型和使用看起来像基于类的面向对象编程语法操作Prototype，TypeScript最终仍然是被编译成JavaScript在浏览器中执行
  - 在2008年，Google推出了JavaScript引擎V8，首次通过JIT技术提升JavaScript的执行速度，并且它真的做到了
    - Web应用中，性能瓶颈大部分的原因已经不在JavaScript，而在于DOM。浏览器中通常会把DOM 和JavaScript独立实现，这两个模块相互访问的时候，都是通过接口访问。由于JavaScript单线程的特性，这种访问只能是单工的
    - 为了减少js访问dom的次数，可以使用Virtual Dom，Web Worker 
    - JIT执行时，可以根据代码编译进行优化，代码运行时，不需要每次都翻译成二进制汇编代码，V8就是这样优化JavaScript性能的
  - 为了进一步提升JIT优化效率，Mozilla 推出了asm.js。asm.js也是强类型的JavaScript，但是他的语法则是JavaScript的子集，是为了JIT性能优化而专门打造的，其他大厂都觉得asm.js的思路不错，于是联合起来共建WebAssembly生态
  - WebAssembly是一份字节码标准，以字节码的形式依赖虚拟机在浏览器中运行，可以依赖Emscripten等编译器将C++/Golang/Rust/Kotlin等强类型语言编译成为WebAssembly字节码.wasm 文件。
    - WebAssembly并不是Assembly（汇编），它只是看起来像汇编
  - 鉴于V8的强大性能，90%的应用场景下你不需要WebAssembly
  - 如何提高JS代码性能
    - 声明变量时提供默认类型，加快JIT介入
    - 不要轻易改变变量的类型
    - Node.js像Java一样也存在JIT预热？
# blogs

## [Compiling Javascript to wasm - Wasm Builders](https://www.wasm.builders/gunjan_0307/compiling-javascript-to-wasm-34lk)

- Are there any good reason to use this approach? Because if you want to run JavaScript without a browser, you can just use NodeJS.
  - So one key reason would be security. Since WebAssembly uses a sandbox model, you can prevent a malicious or buggy JavaScript application from compromising the host. 
  - Other reasons might be performance and portability. Depending on the application, it might be faster to run the WebAssembly code directly (no Nodejs overhead). 
  - As for portability, you might run this same application anywhere without recompilation (server, client, edge, IoT, whatever).
- For me, it was simply getting byte code off my JavaScript files, it's like dream comes true.

## [WebAssembly入门 - 知乎](https://zhuanlan.zhihu.com/p/278028242)

- ASM.js 是 Mozilla 在 2013 年推出的，是 javaScript 的一个严格子集，可以作为C/C++等其他语言编译的目标语言，从而使得 js 引擎可以采用 AOT(Ahead Of Time) 的编译策略，也就是在运行前直接编译成机器码，因此运行速度会有一定的提升。
  - ASM.js 标准中还规定了很多类似的标记规则，用于告诉 js 引擎变量的类型，便于进行 AOT 优化。

- WebAssembly 于 2019 年 12 月 5 日成为万维网联盟（W3C）的推荐标准，与 HTML，CSS 和 JavaScript 一起成为 Web 的第四种语言。

- 从 .wasm 源文件到实例化的对象主要有三个步骤，加载 -> 编译 -> 实例化 -> 调用。
  - 加载：读取 .wasm 字节码到本地中，一般是通过 fetch 从网络中取得。
  - 编译：在 Worker 线程进行，编译成平台相关的代码。
  - 实例化：将宿主环境的一些对象、方法导入到 wasm 模块中，比如导入操作 dom 的方法。
  - 调用：通过上一步已经实例化的对象，来调用 wasm 模块中的方法。

### [javascript为什么不像java一样直接事先编译成字节码然后跑在v8上？ - 知乎](https://www.zhihu.com/question/429597199)

- javascript 一段程序， 翻译到机器码， 体积可能就大个好几倍。 好几倍的体积， 在弱网情况下可就伤了神了。 
  - v8： 要不你给我源码吧。 我现编译还快。 
  - 这也是大文件先 zip 再传输。 传输到目标机器上再 unzip 的道理。
- wasm， 一个浏览器支持的 汇编语言。wasm 编译很快。 因为本身就做了比较严格的要求。 但是传输快不快还得看各个语言编译器的实现。 有的语言要打一个 runtime 包到目标文件里。

- 
- 
- 
- 
- 
- 
- 

## [A step-by-step tutorial on Compiling mkbitmap to WebAssembly](https://web.dev/compiling-mkbitmap-to-webassembly/)

## [From Web SQL to SQLite Wasm: the database migration guide - Chrome Developers](https://developer.chrome.com/blog/from-web-sql-to-sqlite-wasm/)

# more
- [Node.js大家是用什么方式链接C++代码的](https://www.v2ex.com/t/568399)
- 打算用 electron 做 UI，CPP 做内核。但是在选择使用什么方式在 C++和 electron 之间搭桥的时候遇到了困难。
- 目前看到的只有两个选择，一个是 node-ffi 直接链接 C++编译的 dll，
  - 第一个选择 node-ffi 看上去不错但是一方面调用的时候开销大，另一方面似乎不太稳定而且缺乏维护（在 Github 上面最近一次 commit 还是在 1 月份） 
- 另一个是使用 node-addon 的方法，用 node-gyp 编译 C++然后再链接。
  - 第二个选择用 node-gyp 编译 C++似乎是个官方方案，但是运行例子 node-gyp 一直报错，看了 issue list 才知道问题已经存在很久没人修了，继续深入还得花一点时间。

- 仅供参考
  1. C++起个服务器，nodejs 与服务器交互。
  2. C++编译成 web asm，nodejs 直接调用
  3. FFI(这个坑目测更多，没具体研究过)
  4. 类似于 1，socket
  - 首推 web asm，稳，快，简单，更新快，和 js 天然
- WASM确实是好东西，可惜我的C++部分涉及到了标准库之外的东西，port 到 wasm 上面还是有点麻烦。
  - 看来用 socket 做 Electron 和 C++程序之间的 ipc 可能是最方便的方案。
- 现在楼主想用一个 Electron，即压根不考虑运行在浏览器，而是运行到桌面客户端上，
  - 因此没必要搞这一层，用 N-API 是最好的选择，用 IPC 只限于传输的数据比较有限，或者输入参数固定的场景
  - 如果对于需要传递 C 结构体指针，频繁互相调用，N-API 能直接对应到 JS object 对象，调用起来是最原生的
- 如果产品规模较大的话， 最好还是Native框架 + cef 来做，
  - 系统 API 和库的使用就会方便的多，Node 对 Native 的支持很有限，
  - 功能实现会有限制，比如窗口控制、并行下载等。

- [Is WebAssembly magic performance pixie dust?](https://surma.dev/things/js-to-asc/)
  - The incredibly unsatisfying answer is: It depends. It depends on oh-so-many factors, and I’ll be touching on some of them here.
  - V8 is really good at executing JavaScript.
  - While WebAssembly can run faster than JavaScript, it is likely that you will have to hand-optimize your code to achieve that. 
