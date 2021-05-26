---
title: web-wasm-dev
tags: [dev, wasm]
created: '2020-12-31T19:17:26.544Z'
modified: '2021-01-01T20:10:51.125Z'
---

# web-wasm-dev

# guide

- tips
  - 前端开发后端化(Nodejs)，后端开发前端化(WebAssembly)都是比较明确的趋势，未来前后端开发将进一步融合。
# faq

# pieces
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
# discuss
- ## [如何看待 WebAssembly 这门技术？](https://www.zhihu.com/question/362649730/answers/updated)
- 我不太认为 WASM 是值得前端 all in 的技术，概括地说几点问题：
  - WASM运行时性能在原理上就是受限的，跑不到真正的汇编级别。
    - Rust 编译到 WASM 后有不小的性能损失，极致优化后的 JS 不会输它多少
    - 所以真实世界 benchmark 里，WASM 往往并没有压倒性的优势。
    - 不要以为这是因为它不够成熟，而是原理上就决定了。
  - WASM不是计算密集型应用的唯一救星。
    - 对于真正高度并行且精度要求不高的算法，**用WebGL做GPU加速往往更快**，然后才是WASM这种CPU上运行的字节码。
  - 嵌入 WASM 函数到 JS，未必就能提高性能。
    - JS 自身的 JIT 已经内置了机器码级的优化，你手动把算法重写成 C，未必比 Happy Path 上的 JIT 更快。
  - JS 与 WASM 的双向调用并不像 Python 嵌入 C 那么简单，
    - 你不能随便把 JS 里的对象直接交给 WASM，至于喊着打通一切运行时类型的 WASM Interface Types 才刚有了个影子。
  - 主流前端UI框架未必值得用 WASM 重写，
    - 它们的场景是 IO 密集的，换语言彻底重写的投入产出比很难说。
    - 按相同逻辑，既然 JVM 比 V8 快，你愿意用 Java 重写 Node 服务吗？
  - WASM生态跟前端工具链基本无关，
    - 它的 Emscripten 工具链搞的完全就是 C++ 系语言交叉编译，从编译器到依赖库都完全跟 JS 这一套无关。
  - [一个白学家眼里的WebAssembly](https://zhuanlan.zhihu.com/p/102692865)
  - 我不是说WASM不好，它非常适合把原生应用搬到Web上 
    - 编译出一个C++应用的Web版就像把它编译到安卓一样，换一套工具链就行。
    - 但是，不要把 WASM 当作一切前端性能问题的灵丹妙药，更不要觉得把你的 JS 随便用 Rust 重写一下就能快几倍。
    - 还是那句老话，没有银弹
- 我们认为WebAssembly的潜力在服务端。
  - 与Java 和 JavaScript 引擎相比，WASM 通过LLVM 工具链支持20多种编程语言，从而让开发人员有选择语言工具的自由
  - 同时，WASM 可以轻松支持CPU、GPU、 AI 优化芯片和FPGA 等硬件功能。
  - 与Docker之类的容器相比，它为开发人员提供了更抽象的代码执行环境，从而提高了开发效率。
    - 它可以直接部署代码和应用程序，而不必启动操作系统。
    - Wasm 程序不需修改，就可以在不同的操作系统上运行。
    - 这与当今的云原生微服务架构配合得很好。
  - WASM 消耗的内存和资源比操作系统级别的容器少得多。
- 我认为wasm的价值非常大
  1. 首先wasm得到了很多大厂的支持，无论是typescript还是c/c++还是go语言都能编译到wasm；
  2. 然后wasm虚拟的实现代码只要几千行，可以根据不同的需求快速定制虚拟机；所以wasm做嵌入式是非常方便的；
  3. 其次wasm可以反编译到很多其他语言，加强了语言的互通。
  4. 至于在浏览器上跑wasm，他绝对不是用来操作dom和css的，wasm最早的demo就是启动一个虚幻场景，在曾经页游盛行的时代，wasm的价值非常明显。只不过在移动互联网的浪潮下没落了。
  5. 当前wasm已经实现了aot编译，性能以及和c相当，从而所以语言编译到wasm在静态化成为更好的方案。
  6. 我预言下一步wasm将成为全平台的中间语言，各种新旧语言都能在wasm字节码上执行，成为手机游戏热更新的新宿主（取代当下的lua和js）。甚至很多app都将其编译到 wasm 字节码执行，实现真正一切代码的跨一切跨平台包括web。
- wasm当前现状
  1. 当前wasm在浏览器上通过浏览器jit执行。性能和js的jit差不多。
  2. wasm在非web环境可以解释执行，jit执行，aot编译执行。性能是aot大于 jit 大于 解释。
  3. 在iOS只能解释或aot，不能jit，iOS系统不允许执行动态生成的代码页。
- 没什么好说的，目前我只想告诉你wasm性能不高。。。。
  - 仅有的价值就是方便js复用其他代码现有的算法，没有平台api依赖那种
- WASM意义重大。
  - 原本只有JavaScript是跨所有平台的，C++/C#差一个浏览器，现在这个问题没有了。老旧代码可以继续拿来用。
- 在我的Wasm的实践来说，Wasm对于前端开发来说是解放了一些特殊能力，使得一些边缘计算成为了可能。
  - Web前端的算法能力和数据处理能力在对于C++是比较薄弱的，wasm使得很多C++实现的算法很方便的移植到了浏览器中，
    - 使得JS只需要调用调用方法就可能实现以前JS很难实现的功能，比如我前段时间做的扣脸功能。
- 而对后端来说，Wasm主要是解决了后端开发C++库的一些心智负担。
  - 对于后端来说，如果要使用一个C++库则需要安装这个C++库的依赖到线上环境，
  - 其次再使用node-gyp来构建的库，这样就很可能C++库版本依赖发生变化导致的各种各样的问题，无疑是加大了后端开发者的心智负担，
  - 而如果使用Wasm则只需要一次构建，不再需要安装C++依赖库
  - 其实不管是nan还是napi或多或少都会因为V8代码的结构调整收到影响或导致不可用，可以说有可能你node10能使用的C++扩展到node12居然就不可用了
  - 那么无疑Wasm是更好的解决方案，可以使nodejs后端开发不再关注于V8或C++库的一些变化，而更关注于JS相关的东西
- WebAssembly 是让其他编译型语言进入前端的重要技术，前端不只有JS了！
  - 我正在开发的 Ant Design WebAssembly组件库
  - 我用Blazor这个框架，实现Ant Design，运行在 WebAssembly 环境

- ## [WebAssembly 的出现是否会取代 JavaScript？](https://www.zhihu.com/question/322007706/answers/updated)
- 这个说法不准确，wasm只是一个字节码标准，人们可以基于这个标准开发高级语言。
  - 类似jvm一样，很多语言可以编译成jvm字节码，从而使用jvm平台。
  - wasm出现的意义是使用其他语言开发web app成为可能。
  - 之前也有其他语言，比如typescript开发，但是都是把代码编译成JavaScript运行，本质上还是使用的JavaScript. 个人认为JavaScript以后会作为浏览器默认支持的高级语言一直存在下去，
  - 但是wasm出现可以使基于web的开发工具出现百花齐放的状态，web端可能出现类似Java这样适合大型项目的静态类型语言。
- 不论是短期还是长期，我都坚定地认为JS不会被替代。
  - 短期上WASM显然无法替代JS
  - 工具链调试困难、包体积庞大冗余、调 OpenGL 都要走回 JS 到 WebGL，性能未必有保证等
- 感觉不会
  - 从企业来看，不会。增加人员薪资成本，开发效率低
  - 从开发者个人来看，在这个卷的不能再卷的行业，大家也不想放弃之前的技术生态圈，去干费劲不讨好的事
  - 在历史进程来看，个体强不如群体强，js生态会繁荣发展下去的
- 我认为WASM不会取代JS，相反会更丰富JS的生态圈。
  - 不说长期，但现在短期现在已经开始取代很多node.js的C++扩展了。
  - 包括本人也是极力推荐只要非强依赖V8引擎的C++扩展都用WASM来做。这样的好处有很多。
  - 不会因为V8的升级和Node版本导致扩展不可用。
  - 摆脱对node.js的依赖，浏览器直接就可以跑。即使以后升级到deno一样可用。
  - 不需要在不同环境编译，开发过C++扩展的就知道，经常性导致不同环境（尤其是不同Linux发行版）缺少依赖以至于编译失败。
  - 兼容性好不会因为win和Linux的方法不同而和CPU指令集（ARM和x86之争）不同无法运行。
  - 所以目前短期来看都是在丰富JS语言能力。
    - 而且使用其它语言包括rust，golang，java，c++你会发现编译WASM给JS写方法很方便，而全部用非js语言来开法非常麻烦。
    - 而这些都是在丰富JS库，以及方便移植的其它语言代码。
    - 所以后续难保不会出现clickhouse.js,docker.js，k8s.js。
  - 长期来说开发估计还是少不了JS，只不过上线可能会全部转换为WASM了。
- 后面JavaScript会被编译为webAssembly提速。这叫取代了吗？

- ## [Reason, ClojureScript, AssemblyScript 你更看好哪门语言的未来？](https://www.zhihu.com/question/347763134/answers/updated)
- 目前完全没有想清楚它的抽象高度到底在哪
  - 是想做一门高级语言，还是Wasm的一个带糖语法？
  - 现在这种不上不下的时候就号称它是 TS 的严格子集完全自己打自己脸，而且即使他加了更多高级的语言结构，我也担心它会掉入「恐怖谷理论」（即越像时越发现不像）与 leaky abstraction 的问题里。
- WebAssembly 的 GC proposal 还没定下来，现在自己直接带 GC 到 Wasm 的 linear memory 上只是暂时的解决方案，在 GC 的实现和与 JS 的互交互上有不少问题。
  - 也就是说managed语言（不包括 C/C++/Rust）编译到 WebAssembly 的这场仗根本就还没开始
  - 正式玩家都还没上线呢，AssemblyScript 现在玩的就是个内测
- 我认为所有能弄成wasm的非JS(非带GC的)语言目前都是有潜力的。
  - 最后谁更胜一筹，估计会取决于一些随机的市场因素。
  - 事实证明，一门语言是否成功，跟这门语言是否先进，根本一点关系都没有。
  - 勉强能说得上有关系的，就是爹要有钱。

- ## [有哪些效果拔群的 WebAssembly 应用？](https://www.zhihu.com/question/265700379/answers/updated)
- 计算机视觉方面
  - 基于Web端的图像检测与跟踪
  - 基于Web端的人脸关键点检测与跟踪
- 视频解码方面
- AutoCad web版本
- 作为 tensorflow.js 的可选后端之一，默认实现为 WebGL
  - 另外 WebGPU 很值得关注！
  - 这种大量的并行计算，还是gpu加速来吧。
- 我来举用和不用 WASM 的两个【复杂前端应用】的例子，它们都有大量的活跃用户。
  - Figma 大有取代 Sketch 之势，它就重度使用了 WASM
  - 虽然 Figma 的外围控件 UI 是 HTML + CSS 的，但核心的交互界面则在一个 Canvas 内承载，不难发现这个 Canvas 是使用 WebGL 的
  - 中间这整个 Canvas 的交互明显是 WASM 控制的。外围控件平台独立 UI + 核心编辑区域 WASM，这种架构设计是值得借鉴的。
  - 推荐一个在浏览器里运行的全功能 Photoshop，亦即稿定PS
    - Photopea 所有的代码都是 JavaScript，没有任何 WASM 成分
    - 我就此专门问过 Ivan 的想法，按他的说法，用 JS 重写那些 C++ 的底层代码，对他来说往往比费力把这些库接进来更方便
    - Photopea 从字体二进制解析、算法处理、渲染到图像编码导出，几乎都是他自己 JavaScript 徒手撸的。
    - 另外，一些 AI 抠图等需要训练模型的地方，未来也可能引入 WASM。
  - 所以基本上，效果拔群的 Web 应用，关键倒不是选 JavaScript 还是 WASM，而是**掌握对渲染的极致控制**。
    - 当你有了这个水平之后，是否使用 WASM 也只是一种选择而已

- ## [c++项目转成wasm全过程_202007](https://zhuanlan.zhihu.com/p/158586853)
- 本项目是一个类似RN|Weex的一个跨端项目，
  - 其上层DSL为小程序，通过编译工具(node cli)将小程序编写的代码编译(encode)为一段binary代码(其包含了首屏的vdom和style信息以及业务的js代码)，
  - 并将其动态下发给客户端，客户端将下发的binary代码进行decode，并进行native渲染，并与业务的js代码进行动态绑定。
  - 由于encode和decode存在大量的代码复用(内嵌了一个mini的js引擎实现)，所以encode和decode的代码均通过c++编写
  - 客户端(ios|android)SDK源码依赖c++代码，而node cli则是需要先将C++代码编译为动态库(linux为so，mac下为dylib，windows下为dll)，然后node层通过node-ffi进行跨语言调用动态库代码
- 虽然通过node-ffi我们能够成功的实现在node层调用c++的代码，这仍然面临着一些问题
  - 早期的node-ffi存在node的版本限制，不支持node12以上的版本（后来切换到ref-napi解决兼容性问题）
  - c++代码的crash会导致node进程奔溃，影响node在服务端侧的使用和稳定性
  - 多平台的发布问题，如果我们想自己发布的node cli能够在多个平台正常运行基本上有两种方式
  - 通过node-gyp交给用户侧完成so的编译过程，但是由于c++代码里对标准库和语言版本都有一些要求，在用户侧编译对用户的环境有一定的要求
  - 发布cli的时候，完成各个平台的动态库编译，
    - 这就要求每次发布cli的时候都要现在三个平台完成动态库的编译，这实际上要求我们在三个系统上搭建好自己的gitlab-runner，
    - 然而公司的内部的gitlab-runner默认只支持linux，这就要求我们自己搭建好一套成熟的gitlab多平台的CICD流程，这并不简单，而且这也难以解决开发者自己在本地发版的需求
  - 动态库虽然能完美的支持node、android和ios，但是在web端却无法去加载执行动态库，这阻止了我们将编译流程迁移到web的尝试。
  - 虽然我们发布了动态库，使得用户无需自己本地编译动态库，
    - 动态库的调用仍然依赖于ref-napi这个库去完成c++到js的binding，该库需要在用户本地进行编译(依赖了node-gyp进而依赖了xcode),
    - 而wasm不依赖xcode等c++环境，避免了用户对c++编译环境的依赖。
- 出于上述的一些限制，我们尝试将c++代码编译为wasm，wasm除了其出色的执行性能，其还具有出色的跨平台特性
  - wasm是与操作系统和node版本无关的，因此我们一次编译，即可运行在linux|mac|window等多个操作系统上，再也不需要为各个系统分别编译动态库产物， 
  - 在node 8以上即支持了wasm，也无需担心node版本的兼容问题。
  - wasm也可同时运行在web，使得我们后期可以探索web上的编译方案。
  - wasm的运行在一个沙盒环境中，并不会因为其执行异常导致进程奔溃。
- 我们将c++代码编译为wasm碰到的第一个问题就是如何处理系统调用，
  - 实际上述编译结果难以跨平台的一大原因就在于不同操作系统的系统调用实现是不同的，我们必须要为不同的操作系统生成不同的代码来适配不同的系统调用实现。 
  - 这时候一个自然的处理方式就是将上述的系统调用结果编译到一个已经支持跨平台的runtime的系统调用上。
  - 幸运的是已经存在了多种上述的runtime: browser, node, wasi
- 以浏览器为例，浏览器里js的`console.log`是一个天然的跨平台的系统调用，其可以平稳的运行在不同的操作系统上。 
  - 因此我们只需要将上述c++代码编译为wasm+ js glue代码即可，js glue代码负责将系统调用适配到浏览器提供的js api上
- wasm制定了标准的api接口(WASI)，
  - 这时候wasm并不需要依赖js glue代码才能正常运行，任何实现了WASI的接口的runtime都能够正常加载该wasm。 
  - 其实wasm本质上和js是无关的，其可以完全运行在独立的沙箱环境里，通过WASI和系统API进行交互，
  - 这实际上促使了wasm runtime的发展，此时已经并不局限在可以将多种语言编译为wasm，更进一步的我们可以用各种语言实现wasm 的runtime，
  - wasm此时可以运行在除了browser和node之外的其他runtime里，甚至可以被内嵌入移动端的sdk里。
- discussion
- 这个真的什么都好，摆脱了对V8的依赖也不用因为不同平台次次编译。
  - 但是找内存泄露非常不好解决，你虽然可以打印内存快照数据找出是哪个变量泄露的，但是emscripten为了模拟c的malloc全部挂载到了一个全局变量中，所以即使你定位到那个全局变量泄露也无法针对根源解决。
  - 最后我是使用了require-vm才终于解决这个问题
- 飞书这边，我用 wasm 编译zlib 提供给js接口做压缩和解压，没有用emcc 工具链，自己手动编译其实也不复杂。
  - 出于包体积敏感的原因，没有生成is glue，互相调用过程，数据传输等手动封装一下问题也不大的。
  - 不过对于复杂的cpp还是更推荐emcc
# ref
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
