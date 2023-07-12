---
title: lang-java-jvm-graal
tags: [graal, jvm, lang]
created: 2021-01-15T04:08:52.762Z
modified: 2021-01-15T04:09:25.198Z
---

# lang-java-jvm-graal

# guide

- tips
  - 正在快速发展的方向是wasm，而不是字节码转换
  - WASM 满足了与 Graal 相同的大部分需求，并且由于它嵌入在每个主要浏览器中，因此也满足了一些需求。
# dev
- 本来就该推翻重来造一遍轮子，在编译时生成代码如micronaut，或者编译后修改字节码如quarkus。

- GraalVM is a universal virtual machine 
  - for running applications written in JavaScript, Python, Ruby, R, JVM-based languages like Java, Scala, Groovy, Kotlin, Clojure, and LLVM-based languages such as C and C++.
- GraalVM CE is available for free for development and production use.

- Oracle于20180417发布
- 支持多语言编程的通用虚拟机
- 项目的各组件大多以GPLv2的协议发布
- 目前支持Linux和Mac，不支持Windows
- GraalVM开发了「跨语言互操作协议」，它是一种特殊的接口协议，每种运行在GraalVM之上的语言都要实现这种协议，这样就能保证跨语言的互操作性。 
  - 语言和语言之间无须了解对方就可以高效传值。
  - 该协议还在不断改进中，未来会支持更多特性。

- 主要组件
  - Graal：一个由Java语言编写的JIT编译器
  - SubstrateVM：一个对执行容器抽象层的轻量级封装
  - Truffle：一个用于构建语言解析器的工具集和API

- The Java architects worked to support multilingualism starting in Java 7 by conversions to Java bytecode by adding `invokedynamic` to the JVM specification. 
- The GraalVM team felt that since Java bytecode had too much Java semantics built into it, a longer term effort could be much more efficient and a 100% compatible implementation at that.
# graal-js/node
- https://github.com/oracle/graaljs /UPL/java/cpp/clang
  - A ECMAScript 2022 compliant JavaScript implementation built on GraalVM. 
  - With polyglot language interoperability support. 
  - Running Node.js applications!

- [Node.js vs Graal.js Performance](https://github.com/oracle/graaljs/issues/74)
  - [GraalJS is around 70X slower than NodeJS 14_202010](https://github.com/oracle/graaljs/issues/360)
    - Revisit that in 6 Month and you will get much better results

- [Node.js Runtime](https://www.graalvm.org/latest/reference-manual/js/NodeJS/)
  - GraalVM’s Node.js runtime is based on a recent version of Node.js, and runs the GraalVM JavaScript engine instead of Google V8. 
  - Thus, some internal features (e.g., VM-internal statistics, configuration, profiling, debugging, etc.) are unsupported, or supported with potentially different behavior.

- [Using JavaScript Modules and Packages in GraalVM JavaScript](https://www.graalvm.org/22.0/reference-manual/js/Modules/)
  - GraalVM ships with a specific Node.js version that it is compatible with. Applications can therefore freely import and use NPM packages compatible with the supported Node.js version, including CommonJS, ES modules, and modules that use native bindings.
  - When **embedded** in a Java application (using the Context API), GraalVM JavaScript can execute JavaScript applications and modules that do not depend on Node.js’ built-in modules such as 'fs', 'events', or 'http' or Node.js-specific functions such as setTimeout() or setInterval(). 
  - On the other hand, modules that depend on such Node.js builtins cannot be loaded in a GraalVM polyglot Context.
  - By default, a Java Context does not support loading modules using the CommonJS `require()` function.
    - Experimental support for CommonJS modules can be enabled through the `js.commonjs-require` option as described below.
  - GraalVM JavaScript supports the full ES modules specification, including `import` statements, dynamic import of modules using `import()`, and advanced features such as top-level `await`. 
    - ECMAScript modules can be loaded in a Context simply by evaluating the module sources.
  - By default, GraalVM JavaScript uses the built-in FileSystem of the polyglot Context to load and resolve ES modules.

- [👉🏻 Is GraalJS a fork of Node.js? | Hacker News_202209](https://news.ycombinator.com/item?id=32713344)
  - No, not really a fork. **GraalJS is a new independent from-scratch implementation of JavaScript**. 
  - It uses a pair of radically different execution and optimisation techniques known as self-specialising-ASTs, and partial evaluation, and runs on the JVM.
  - But a sibling project, [Graal-Node.js](https://github.com/oracle/graaljs/tree/master/graal-nodejs), does include vendored code from Node.js in order to be compatible with Node.js applications. That's where the commits come from I'd guess.

- [Graal.js API for other languages?](https://github.com/oracle/graaljs/issues/542)
  - GraalJS (like any Java application) can be used from the native code using JNI (Java Native Interface). 
  - JNI Invocation API allows you to spawn and use JVM in the same process. Note that you can use JNI even if you don't want to use JVM but the native image (containing GraalJS) instead because native image supports JNI as well. 
  - If you plan to use the native image then you can also use its C API.
  - Graal.js' main API is via `org.graalvm.polyglot.Context` from Java. Or if you prefer and can accept some downsides, via our compatibility layer to `javax.script.ScriptEngine`.
# graal-wasm
- https://gitee.com/mirrors/GraalWasm
  - GraalWasm, an engine for running WebAssembly programs on GraalVM

- ## [昨天看了一个很有意思的视频，讲的是 WEB 后台开发， WASM 一统天下的故事。 - V2EX](https://v2ex.com/t/829706)
- 所说的任何一点，JVM 都具备。

- WASM 太底层了，就真的是一个虚拟机，在里面跑虚拟机语言就都是虚拟机套虚拟机 
  - 准确地说，这里的所有虚拟机（我要把 JVM 都拉上）全部都应该叫模拟器。究其原因，它并非采用虚拟化技术进行隔离，而是采用模拟器技术逐指令翻译，从而使得字节码平台无关。
  - 对照地说，GBA 模拟器也是一样的操作。 —— 反而，Qemu 有时是个虚拟机。因此倒也不用唯名论地逐字推敲。

- 现在有些 docker 不就是用 qemu 驱动的，但发布体积大，CPU 转译效率又低，有些时候没必要杀鸡用牛刀。 
  - WASM 可以做到体积极度轻量，几乎无重型依赖包。 
  - 你说 JVM 也可以，但 JVM 是一种特定语言。
  - WASM 代表着十几种语言，这点上 WASM 完胜。

- docker 的开发者说过，如果早年有 wasm ，就可以不用开发 docker 了。
  - 两个看似不相关的技术，本质上都是把代码装进黑盒后，便捷发布。
  - WASM 对运行环境依赖很低，这样平台移植性就非常高。有时候 docker 还要用 qemu 包一层，就是因为 x86 和 arm64 指令不兼容，WASM 把这个问题，从根本上给解决掉。
- docker 是二进制级别的打包，不需要源代码适配，兼容性不是一个需要重写+编译的东西能比的
  - docker 是二进制级别的打包，不能二次平台适配了。
  - 而 WASM 是中间字节码打包，加载后可以二次适配到任意 CPU 和可运行平台。 真正意义上的 write once, run everywhere.
- 至于上云的话，还是慎重，现在各个云平台并没有什么统一标准，真就是上云一时爽，下云火葬场。换个平台就脱一层皮。

- WASM 和 GraalVM 有什么区别？
  1. GraalVM 完全支持热加载。
  2. GraalVM 完全支持跨平台，甚至可以嵌入到 MySQL 和 Oracle 中作为执行引擎。
  3. GraalVM 支持 jvm 语言，如果 java 、kotlin 、Scala 等 jvm 语言，也支持 js 、Python 、ruby 等动态语言，还支持 C 、C++等基于 LLVM 的语言，跨语言调用无性能损失
  4. GraalVM 性能非常优秀，可以高性能通用编译后端
  5. GraalVM 同时支持 AOT 和 JIT ，任何语言只要编译到 GraalVM 字节码，就能进行 AOT 编译，获得最快的启动速度，也可以进行 JIT 编译，获得最高的性能峰值

- GraalVM 只是一个公司的产品吧，由一个商业公司来维护。
  - 而 WASM 是一种开源标准，社区都在帮着写代码，肯定差距很大的。

- wasm 已经有不少应用，pyodide ，以及 figma 等
# discuss-js-graal

> 更推荐的方案是wasm

- ## 

- ## [既然 GraalVM 支持多语言且能 AOT 编译 Java，它能否用来 AOT 编译 TS？ - 知乎](https://www.zhihu.com/question/423945328/answers/updated)
- 现在 graal.js 如果做成 native image，是相当于把 Java 写的 JS 解释器编译到 native，然后解释执行 JS 吗？还是说像 Dart 那样把 JS 源码本身给 AOT 了（这时候弱类型感觉没法做啊）？
  - 恩，AOT的是解释(编译)器本身，js代码还是要到运行时被这个AOT了的JIT编译器JIT编译。
  - 弱类型动态类型只是提高优化难度，完全aot肯定是能做的，就是性能不好说。

- ## [javascript为什么不像java一样直接事先编译成字节码然后跑在v8上？ - 知乎](https://www.zhihu.com/question/429597199)

- https://github.com/tc39/proposal-binary-ast
  - Binary AST proposal for ECMAScript
  - [What is the current status of this proposal?](https://github.com/tc39/proposal-binary-ast/issues/79)
    - No one is working on it for the last several years
  - [Solved by W3C EXI?](https://github.com/tc39/proposal-binary-ast/issues/80)
    - A huge part of this proposal is about parsing JS on demand and not at the start, Which that proposal has nothing to do with. But I think it can be used in binary serialization part.

- 因为现阶段，网络加载时间远超解析JS文件的时间。

- JS 其实就是先编译成字节码然后跑在 v8 上的，只不过这个过程是对程序员完全透明的。
  - 至于为什么不预先编译成字节码，**因为 JS 没有统一的字节码规范，而解释器不止 v8 一个**，早期各个浏览器都有自己的解释器，v8 的字节码只能由 v8 解析，换个解释器就不灵了。
  - 于是，JS 在过去以及未来的很长一段时间之内，都是事实上的中间代码。这非常像某个历史时期，各大编程语言把 C 当成中间代码一样。
- js engine是browser的一部分，不同的browser有不同的engine，不同的engine采用了不同的优化，使用的指令集不一样，也就是bytecode不统一，不像jvm具有一致性。

- 你如果想手动执行这个过程，可以用下面这个代码：

```JS
var vm = require('vm');
var fs = require('fs');

//读取源文件（JS源码）
var jsCode = fs.readFileSync(__dirname + "/test.js").toString();

//生成字节码
var script = new vm.Script(jsCode, { produceCachedData: true });
var byteCode = script.cachedData;

//将字节码写入文件
fs.writeFileSync(__dirname + "/test.jsb", byteCode);
```

- TC39已经有了相关的提案，这份提案叫做 Binary AST，也就是二进制的 AST 语法树格式。
  - 注意所谓「二进制 AST」和字节码的区别：前者只相当于把 Babel 获得的 JSON 解析结果存储到对机器友好的字节流里，后者则是一种需要定义出 VM 规范的新格式（比如基于栈或基于寄存器）。
  - 不难发现，Binary AST 既与目前的 ECMAScript 标准严格对应，并且也规避了与各大 JS 引擎内部结构相重叠的问题，因此有更好的落地可能性。

- 引入 Binary AST 的动机，和题主的想法非常相似：现代 Web 应用的性能和动态加载的 JS 包体积密切相关，虽然我们已有各种缓存机制，但 Web 这种天生动态的特性，决定了应用经常需要「冷启动」式地加载 JS 包，这时缓存只是治标不治本。
  - 为此，我们需要更好的手段来减少包体积并提升解析速度，从而优化首屏时间，提升用户体验。
  - 对这些大体积 JS 文件进行解析的开销，甚至会超过 JS 引擎生成字节码和初始化 JIT 的开销。
- Binary AST 能发挥用武之地的地方——既能省去词法分析语法分析直接拿到 AST 结构，又能更省空间更快完成加载
- Binary AST 提案是怎么设计的呢？这是一种新的替代性表层语法编码，与文本表示有相当接近的双向映射。
- 怎样保证 Binary AST 的语法能向后兼容呢？提案中为此设计了一个 header 表，其中会列出原始 JS 代码会用到哪些节点和哪些属性。比如 FunctionExpression 节点就可能包含 isAsync 属性。如果某个文件中用到了 async 函数，它的 header 列表中就会列出 isAsync 这个字段。如果 header 中列出的节点或属性不被当前版本的引擎所支持，就会抛出一个异常（类似于 ES7 代码不能在 ES5 环境下执行）

- 目前提案倡导者已经实现了早期原型，并在 SpiderMonkey 引擎上针对 Facebook 官网，进行了将其 Binary AST 化的测试。
  - 根据测试数据，基于 Binary AST，创建完整 AST 所需的时间能减少约 70% 到 90%。
  - 因为 SpiderMonkey 原本这部分时间需要耗费 500-800 毫秒，因此对于前端长期追求的「页面秒开」来说，这无疑是一个很不错的结果。
- 类似 Binary AST 的能力，其实在 Dart VM 中已经落地了。
  - 自从 Dart 2.0 开始，Dart 引擎已经不支持直接解释执行文本，而是会把 Dart 源码编译成名为 Kernel Binary 的 .dill 格式二进制文件。
  - 但由于 Dart 和 Flutter 绑定的封闭性，它直接禁止两个不同版本的 Kernel Binary 互相兼容。

- java也需要通过虚拟机把java代码转化成机器码。你可以把 V8 看成是一个虚构机，从宏观的结果导向角度上讲它跟java虚拟机没什么不同。
  - 但我想说 V8 并没有采用某种单一的技术，而是混合编译执行和解释执行这两种手段，这种混合使用编译器和解释器的技术称为 JIT（Just In Time）技术。
  - 解释执行的启动速度快，但是执行时的速度慢，而编译执行的启动速度慢，但是执行时的速度快。

- ## [为什么基于graal.js的es4x可以实现4倍多于node.js的性能提升？ - 知乎](https://www.zhihu.com/question/432339801/answers/updated)
- vert.x区别于node.js一个最大特点就是多条eventloop，node一个实例缺省只有一条 
  - vert.x启动就按照available cores * 2的数量，启动多条eventloops
- 一个vert.x进程，有多条eventloop线程，而node是一个进程，只有一条eventloop线程
  - vert.x除此之外，还提供了eventloop之间的通信方式，也就是eventbus，这个跟最初原作者tim fox最早是做message bus消息总线的有关系

- ## [如何评价基于GraalVM/Truffle的Graal.js？](https://www.zhihu.com/question/54878770)
  - 打算是用graal.js替换掉openjdk现在里面的nashorn

- GraalVM 提供了两种运行 Java 应用程序的方法：在 HotSpot JVM 上使用 Graal 即时 （JIT） 编译器或作为提前 （AOT） 编译的本机可执行文件。

- 使用GraalVM Truffle，Java和其他支持的语言可以直接相互互操作，并在同一内存空间中来回传递数据。
  - **Java on Truffle是Java虚拟机规范的实现，使用Truffle语言实现框架构建**。
  - 它是一个完整的Java VM，包含所有核心组件，实现与Java运行时环境库相同的API，并重用GraalVM中的所有JAR和本机库。

- Native Image是一项创新技术，可将 Java 代码编译为独立的本机可执行文件或本机共享库。 
  - 在构建本机可执行文件期间处理的 Java 字节码包括所有应用程序类、依赖项、第三方依赖库以及所需的任何 JDK 类。 
  - 生成的自包含本机可执行文件特定于不需要 JVM 的每个操作系统和机器体系结构。

- GraalVM 有 GraalVM Enterprise 和 GraalVM Community 版本，包括对 Java 11 和 Java 17 的支持。 GraalVM Enterprise基于Oracle JDK，而GraalVM Community基于OpenJDK。

- ## [为什么没人推动用 JS 实现 JVM 这件事，为什么浏览器不内置 JVM？](https://www.zhihu.com/question/333230233)
  - 为什么没人推动用js实现一个工程化的jvm，不是个人玩具类的，从而使浏览器可以运行java程序

- 👉🏻 有 WebAssembly 了。
  - JVM 只是 Java 一家用的，WebAssembly 是一套二进制标准给所有语言用，到时候就不只是 Java 了，还有 C#、Rust、C++，等等等等。

- applet就是java在浏览器的执行环境，但是对比JS没有优势，被淘汰了。
  - jvm 是 c++实现的，js在浏览器上运行也是基于 V8 引擎的，所以不可能用 js 实现一个 JVM （没啥意义）
  - wasm 并不是编译为 js，而是直接编译成了浏览器可以运行的二进制模块

- 想用java写js的人有很多很多，可参考vaadin, gwt, jsweet, Java2Script等项目，都在致力于用java写浏览器程序
- 曾经的浏览器是可以用object或embed标签跑java程序的，但并没有多好用，而且有安全性问题，所以早就 ban 了。

- ## [JavaScript on GraalVM](https://dev.to/pmlopes/javascript-on-graalvm-120f)
- discussion
- I am wondering which part make es4x so fast comparing to node.js because as you mentioned in the video that GraalJS run as fast or almost fast as v8.
  - Does the performance gain from replacing libuv or run on GraalVM ?

    - Or it is because you seem to wrap the node.js api by java implementation?
    - I'm really curious about that.

  - There are a couple of things that make it faster. 

    - The usage of netty provides faster IO than libuv, 
    - then vertx implements a different eventloop that uses all computing resources and gives better handling of async tasks, 
    - finally graalvm (in contrast to V8) can optimize the full application (not just the js script), it optimizes netty, vertx and the js code (graaljs + es4x) 
    - so in the end the JIT gives an extra boost to everything and you get that performance. 
    - The cost isn't free, you will see that this has the side effect that only works as expected for long running processes (short cli apps won't benefit from this).

  - ES4X is a new JavaScript runtime that is supposed to replace the official vertx js. 

    - The official vertx js is using nashorn so it only supports ES5.1, it's not high performance and has a development workflow based on java tools such as maven and not npm.
    - The goal is that with version 4 vertx will drop that js runtime and adopt ES4X.
    - This brings to the following question, ES4X is based on vertx, not libuv so express will not work out of the box but writing an API shim could be doable but it's not on my plans atm.

  - Finally regarding the multiple event loops, they never block each other, what is guaranteed is that if a request is started on event loop A then all handlers for that request are handled on event loop A to avoid context switching and improve performance.
- I really doubt that single vertx instance (vertice) is faster than single instance of libuv. 
  - Libuv is written in pure C and talks directly to system kernel (file descriptors). 

    - The main reason that vertx is faster is the multi-reactor pattern. 
    - Most of frameworks based on libuv (node, asyncio) are single threaded. 
    - Vertx can create event loop on each thread by default.

  - You will see that the node implementations are scaling to all cores using the cluster module. 

    - Also others had the same question and also provided a implementation using 0http which claims to be fast, results however show the opposite.
# discuss
- ## 

- ## 

- ## 

- ## [如何看待 Java11 即将弃用 Nashorn 引擎？ - 知乎](https://www.zhihu.com/question/282928698/answers/updated)
- nashorn其实做得一般般，js这个社区已经接近是v8一家撑着了，
  - 换言之，**如果不能兼容node，光支持js没有太大意义**，所以为了全面兼容node.js和ecmascript，所以将来会用graal.js替换之，从这一个角度上看，graal前途光明，vert.x已经在积极做es4+（是es 4+，不是仅仅es4）也就是ecmascript的语言支持了

- ## [为什么现在java几乎所有的工具/类库，都在尝试往graal上搬？用graal做aot？ - 知乎](https://www.zhihu.com/question/486452665/answers/updated)
- 本质上还是GraalVM开始逐渐流行了。
  - GraalVM能将Java应用的启动时间减少到1/50
  - GraalVM基本上不会省CPU，但是在内存上的节省是非常可观的。GraalVM能够减少将近4/5的内存。
- 在GraalVM/Truffle的基础上，GraalVM不仅可以运行Java，还可以运行js、ruby、python等多种语言，而且可以用统一的语言来进行调试、headdump分析等。
  - 给开发者带来的好处就是，Java代码可以几乎无缝的调用其他语言的功能和三方库。甚至java的库，也可以通过GraalVM编译成C语言的动态库，供其他语言调用。
- GraalVM还有很多缺点
  - 动态反射、资源获取都需要手动标记。
  - 目前的执行效率还有提升空间。

- 现在native-image的性能提升真的很有限，更多的是负优化，从官方自己的介绍就能看到aot极限吞吐是没jit高的。
- 启动时间不多扯了，aot完了可以从5秒降低到1秒，但是绝对不可能从50秒降低到10秒，它减少的是JVM本身的启动时间和预热时间，不是你应用的加载时间。
- 大多数应用（例如spring）在目前这个时间点想上native-image是比较难的。
  - 能上native-image并且没有明显的功能缺失的话，说明代码依赖清晰，也没有用什么特别离谱的奇淫巧技。
  - 开发者可能因自己的喜好倾向，**不往代码里加反射等代码**，而采用代码生成器等，但是在以前，这种做法是没有什么明显的好处的，因为反射+字节码生成比代码生成器显然更加简单方便
  - 现在有了native-image，这种开发者自己的倾向就变成了优势：你纯反射native了配置麻烦而且性能差、字节码也根本无从加载，我代码生成不用额外加配置、性能也无损。
- 主要优化就是启动速度和内存占用，因为编译成原生程序二进制了，只有很轻很轻的jre了，所以内存占用降低了很多，启动速度真的是几十秒到几秒的提升，不信自己可以随便用支持graal的框架测试

- 主要是受了go的刺激。 
  - 云时代的到来导致容器大行其道，而go就是为容器而生的语言。 go的快速启动，占用内存底非常适合容器。 
  - Java正好相反，所以Spring native（快速启动，占用内存底）e出来了，就是应对go的这种场景。

- 我觉得吧主要是因为时代不同了，技术在不断发展，K8s都成了基础设施，以后服务端的程序都是要运行在k8s上的。这使得Java当年大杀四方的绝招: 一次编写到处运行不香了。其他原生编程语言在k8s的加持下毫不费力的拥有了这个能力

- ❓ 赶时髦蹭热度，我大胆预言最多2年这类需要手写反射配置的aot工具统统完蛋，java语言一直都依靠方便而又强大的反射来弥补其抽象能力不足的缺陷，为了aot放弃反射根本得不偿失。

- ## [如何评价 GraalVM 这个项目？](https://www.zhihu.com/question/274042223/answers/updated)
- 结论是GraalVM想成为一统天下的“最终”虚拟机。
  - 大部分脚本语言或者有动态特效的语言都需要一个语言虚拟机运行，比如CPython，Lua，Erlang，Java，Ruby，R，JS，PHP，Perl，APL等等，
  - 但是这些语言的虚拟机具体的实现，差距很大，比如CPython的VM就不忍直视，JVM的HotSpotVM，C#的CLR和JS的v8却是state of the art级别
- 那么能不能付出较小努力，用一个state of the art的虚拟机，来运行这些语言，让它们享受该虚拟机的一些工匠特性，比如gc，锁，jit等？
  - 答案基本上是肯定的
  - 首先，对于Java，Scala，Groovy这些本来就是JVM-based的语言，那没有什么压力，直接上JVM即可。
  - 对于CPython，R，Ruby，PHP乃至自己写的一门新的语言，回顾一下我们的一般做法：

    - 首先解析源代码到AST，然后写一个AST解释器->
    - 当有些人用这个语言的时候，语言设计者可能继续迭代，实现一个虚拟机，包括GC，运行时等，代码执行仍然是AST解释器->
    - 用的人多了，继续迭代，将AST转换为字节码，使用字节码解释器->
    - 用的人特别多，性能也很关键，如果这个语言社区有足够资金和人力，那么可以写JIT编译器，提升GC性能等，大部分语言都到不了这一步。

  - 我们希望一门语言在AST解释器节点性能就足够好了，不用花那么多精力和财力做性能优化等，这就是Truffle语言框架的动机，

    - Truffle是一个Java框架，自然跑在JVM上，
    - 在这个框架下，用户只需要实现具体语言的AST解释器，付出的努力比较小，性能也足够好。
    - 因为基于Truffle框架，AST树在解释过程中可以根据type feedback变形
    - Truffle还可以在AST解释过程中使用编译器将这个AST树的一部分节点编译为机器代码，后面不解释执行AST节点，直接执行机器代码，这个过程也叫做部分求值（Partial Evaluation）

  - Truffle将AST节点编译为机器代码使用的编译器是Graal，这是一个Java写的即时编译器

    - JVM是C++写的，它内置了两个C++写的即时编译器，C1和C2。
    - 一般频繁的代码先用C1编译，这些代码即热点，如果热点继续，那么会使用C2编译。
    - JVMCI相当于把本该交给C2编译的代码交给Graal编译，然后使用编译后的代码（其实也可以替代C1）
      - graal就是java写的编译器，他要想插入到jvm上面使能就需要jvmci
    - CPython，R，Ruby，JS通过Truffle框架写个AST解释器也可以在JVM上运行了。
    - 那么如果是静态语言，像C/C++，Go，Fortran，解决方案是将C/C++这些语言用一些工具（如clang）转换为LLVM IR，然后使用基于Truffle的AST解释LLVM IR，这个解释LLVM IR的东西就是Sulong。

  - 到这里大部分语言都可以在JVM上运行了，上面提到的所有技术放到一张图里面，这个整体就叫做GraalVM

    - 其实并不真正存在GraalVM这个语言虚拟机，
    - GraalVM是指以Java虚拟机为基础，以Graal即时编译器为核心，以能运行多种语言为目标，包含一系列框架和技术的大杂烩

  - 所有语言最终都是运行在JVM上，需要机器提前安装JDK环境，而且JVM由于自身原因，启动速度比较慢，内存负载较高。

    - 能不能把程序直接打包成平台相关的可执行文件，后面直接执行这个可执行文件，不依赖JVM？
    - 答案是jaotc，哦不是，是吊打它几十条街的SubstrateVM。
    - SVM借助Graal编译器，可以将Java程序AOT编译为可执行程序（没错，Graal编译器既可以JIT又可以AOT）

- 现在jdk里面的jit compiler c2太老了 
  - 晦涩难懂 已经很久没有更新了 在当前基础上 已经不可能有重大更新 都是加一些手动的intrinsic
  - graal是用java写的compiler 加上hotspot vm 就是graalvm 现在的结构更加模块化 更容易实现强大的优化 比如多语言支持 aot
# discuss-usecase
- ## 

- ## 

- ## [怎么看apache solr通过简单将openjdk替换成graalvm就将响应时间提升了15%？ - 知乎](https://www.zhihu.com/question/496976187)
- 有什么是openjdk能做，graal不能做的？
  - graal可以看成是openjdk的超集，提供了更多的功能，比如native image/aot，polyglot多语言集成，工具嘛，功能越多是不是越好，只要硬盘上的体积能够接受
  - openjdk目前啊，提供了更为丰富的gc策略，比如zgc和shenandoah，目前只有openjdk才有，而graal只看到红帽在做，但是什么时候做出来，那就不知道了
  - 除此之外，其他领域，graal基本上是完美替代openjdk
  - 那graal本身就可以通过jvmci替换openjdk里面的c2编译器

- 讲讲我个人使用的问题吧
  - 实际上graalvm占用会高一些
  - libgraal需要额外空间加载jit编译器替换掉c2，想要恢复rss占用请用企业版
# more
- [graalvm license分析 | mjblog_202009](https://mjblog.github.io/2020/09/25/graal_license/)
  - graalvm社区版本使整体是GPLv2 with classpath exception
  - 目前关心的组件主要有GPLv2(compiler/vm)、UPL(truffle/js)和BSD(sulong)三种协议
  - UPL是非常开放友好的开源协议。不仅允许任意重用代码(包括商业使用)，而且明确提供了专利授权和保护，法律风险非常低
