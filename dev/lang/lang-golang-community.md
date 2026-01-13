---
title: lang-golang-community
tags: [community, golang]
created: 2023-08-28T06:07:39.658Z
modified: 2023-08-28T06:08:05.348Z
---

# lang-golang-community

# guide

# discuss
- ## 

- ## Go 里面用指针一不留神就会忘记判断 nil 导致 panic，也没有 ?. 可选链运算符
- https://x.com/luoling8192/status/1988877035318509642
  - JS 里面因为对象是引用传递，我不用操心是否需要指针

- 你只是没看到js指针长什么样，但并不代表你没在用指针，你以为是值传递，结果一堆函数改了同一个对象，想 copy 一份对象，还得深拷贝或者结构化 clone，小心各种共享引用。
  - go至少什么时候是值，什么时候是指针，你是一眼能看出来的

- https://x.com/luoling8192/status/1988931433327743304
  - 可能是写少了，我昨天才知道有个东西叫 typed nil
  - 搞了一个可选的 services，初始化的时候可以返回 nil，调用的地方判断了 != nil 之后就直接用了，结果给我直接干 panic 了
- 社区对这玩意普遍是批判为主来着

- ## Go语言其实是一门易学难精的语言
- https://x.com/amehochan/status/1973283775405760689
  - 1、包循环引用问题：Go 语言引入了 init 函数，所以在设计上禁止包之间循环引用，编译时会报错。
  - 2、Goroutine 管理问题：使用 go 方法很简单，但是大量创建的 Goroutine 却很难控制管理。尤其是出现 panic 的情况。
  - 3、“茴香豆”的几种写法：Go 语言引入了多种变量声明方法，import 的几种写法，甚至在方法参数里也支持同类型合并等特性。但每种写法底层都存在着不同的使用场景，有些又很没有必要，初学者往往因为默认的零值而踩坑。
  - 4、接口的鸭子类型：鸭子类型在 TS 等编程语言里面很常见，但它们只服务于数据结构。Go 的鸭子类型是接口定义的范式，但却很容易在定义和使用时不容易找到来源。
  - 5、interface{} 满天飞：any 的使用打破了强类型的约束，而且在很多场景下，没有更好的替代。范型出现的太晚，又过早地 1.0。导致标准库很多只能按照 any 去设计。
  - 6、羸弱的编译器：Go 语言的编译器在设计时相当拘泥于语法格式和细节，一个简单的换行都会导致编译报错。又为了所谓的洁癖原则上要求忽略 ; 这也导致了 Go 语言写出来的代码，必须要通过所谓的 gofmt 或者是 goimports 进行统一格式化后才能一致性。
  - 7、自作聪明的首字母大小写：Go 语言的设定里面首字母大写的各类变量方法等是 public 的，看起来很简单。但却导致了，在序列化反序列化等场景，需要写一堆 Tag 来保证 camelCase 的场景，徒增烦恼。
  - 8、error 和 context 的全局污染：现在 context 是方法的第一个参数，error 是返回值的最后一个参数，基本上成为标准范式。与其这样，Go 还不如引入隐式参数。搞得多值返回很多时候变成为了这碟醋包了这顿饺子的设计。

- 首字母大小写没办法，因为一开始golang就是一个包文件夹下所有的代码，区分啥代码层级？和java相比，弱爆了。

- interface｛｝漫天飞舞实在没办法，谁让它是万物皆可interface，我看中golang、是因为它良好的底层互动能力，以及谷歌这个爹大力的支持。

- ## There are three styles of writing error checking code in Go.
- https://x.com/ohmypy/status/1920393038620184785
- Brief gets eliminated by gofmt and carefree is insane so you're left with conservative.

- ## 我大概从15年开始项目都用Go了。 虽然语法太过简陋，但做项目有两个巨大优势：
- https://x.com/william_bao/status/1800806798460612848
  1. 可以静态编译，不依赖任何环境，直接编译成一个可执行文件扔到服务器就能跑起来。
  2. 可以编译时嵌入其他文件或文件夹。我会把前端项目编译后直接嵌入进来。这样不用单独还弄个前端，一个可执行文件前后端都在里面了
- 这两个优势带来的爽点足以磨平很多简陋带来的问题。而且简陋也不全是坏处，代码多了点，但脑子可以歇着，少死很多脑细胞。
  - 直观可读性，是好代码的第一要义。每个项目初期一般都会是这种风格，等做大了、有钱请高手了，就会搞出设计模式之类能够装逼，但其实误事的东西来，开始抽象化，项目渐渐走向坟墓。代码适当的重复，要好过拼命理解复杂的结构。这也是我最喜欢在初创小团队干活的原因。

- ## 🤔 写了两周 golang 发现 golang 的 defer 用于管理资源释放，避免在多处 return 那里释放资源，貌似很方便；
- https://twitter.com/skywind3000/status/1778094362502787381
  - 但稍微比较下，同样的事情，似乎 python 的 with ，c# 的 using，甚至 java 的 try-with-resource 语句都比 defer 要更加清晰，界限分明，defer 容易写飞，比如 for 循环里放 defer 的错误。
- 还有一个神奇的问题，go 的 defer 和 return 不是原子操作，你 return 语句和 defer 语句如果共享的是指针，容易导致数据混乱。
- 我一开始写golang，这个defer也容易写飞，很大原因是因为C++的raii的习惯，后来会有意识的用golang的闭包结合起来

- golang 里就是 close、unlock、cancel 满天飞，尤其是遇到 loop 真的烦。要么就全包进毫无意义的函数里。
- 对我来说，go最困扰的就是duck type导致源代码很难阅读，如果文档写的不详细有些库连用都不会用。当然我还是菜鸟阶段，指针，协程，基本上不用，所以这些坑还没摸到。
# discuss-news-golang
- ## 

- ## 

- ## 

- ## It's been a year since iterators were added to Go. Do you think it was worth it? _202508
- https://x.com/ohmypy/status/1955228993352855775
- I think it would be better if they improved generics in Go than to add this lol.
  - Honestly I haven't used it and I don't bother much trying to find places to use.

# discuss-compiler-toolchain
- ## 

- ## 

- ## The reason on why Go's syntax is simple is to provide fast compile times. 
- https://x.com/Chikor_Zi/status/1915869480195916246
  - Simpler syntax -> simpler parsing rules -> faster compile times. 
  - It's also why no circular dependencies are allowed and why Go has a rigid package structure. 
  - It's kinda impressive a AOT compiled language faster at compilation than a JIT compiled language like JS.

- The main reason why Go's syntax is simple is to simplify maintaining large codebases written in Go. Simple syntax is easier to read and understand by humans. Fast compilation times is just another core feature of Go, which shortens code-compile-verify feedback loop 

- ## Why do so many Gophers dislike cgo so much? 
- https://twitter.com/penberg/status/1764702044672204806
  - I see people have ported SQLite to Go by machine translating the C code but also wrapping a Wasm build of SQLite in Go. 
  - Why is that better than using SQLite with cgo?

- Biggest thing I've seen: CGO makes compilation really, really slow. 
  - Compiling Go apps that are 100% go is really fast, but the moment you add 1 C dependency, it slows things down a lot. 
  - Also you lose cross-compilation support. You can emulate with zig, but it's not the best
  - Also for perf, sharing data from Go -> C and C -> Go can be really slow. Probably faster that re-writing an entire C app in Go/running it in WASM, but still something to consider

- It’s mostly the performance - CGO perf is so bad that it’s faster in some cases to call a wasm function via Wazero than directly via CGO 
  - Plus there’s the additional compilation complexity

- People dislike what they don't understand. I am a C junkie who likes to use Go. There is nothing wrong with cgo, I'm not writing the software for banks or jet engines. So I use cgo.
# discuss-ide-golang
- ## 

- ## 

- ## 💡 [Import statement deleted on save · Issue · golang/vscode-go _202203](https://github.com/golang/vscode-go/issues/2127)
  - In vscode, it automatically removes any unused imports on save.

- Deleting unused imports is the default behavior to help saved files can compile 
  - 💡 In Go, unused imports are compile-time errors.
  - `"[go]": { "editor.codeActionsOnSave": { "source.organizeImports": false }}`

- [Golang will not let you compile if there’s an import or declared variable that’s unused | Hacker News](https://news.ycombinator.com/item?id=5893748)
  - I think that is the result of an explicit design goal of Go: optimizing for large projects that involve many files and packages developed by many people. 
  - Having extraneous package or variable declarations in parts of a program are not an issue for small, one-off exploratory programs, but can be for large projects. 
  - So they're consciously making it slightly more painful for small projects because they're designing for large projects.

- [Disable removing unused imports in vscode : r/golang _202309](https://www.reddit.com/r/golang/comments/16vpyw1/disable_removing_unused_imports_in_vscode/)
  - You can import the package with an underscore, or use the save without formatting command.
  - Even with save without formatting it still does that
  - In VSCode, you don't need to write the imports first. When you actually want to use something from the package, just start typing, using code completion to select the thing you want to use, and it will add the import for you. 
  - `import ( _ encoding/json _ time )`; 
  - Goland does that too. Just decided to let it insert the imports as and when needed.
# discuss-runtime-stdlib
- ## 

- ## 

- ## 

- ## 

- ## Today I learned that Go's standard library depends on the external packages golang․org/x/crypto and golang․org/x/net.
- https://x.com/ohmypy/status/2010326776967582048
- I think it's safe to treat `http://golang.org/x/*` packages as experimental stdlib
  - I think it's a common misconception. x/* packages aren't experimental, they're production-ready. They just aren't covered by the compatibility guarantee.
  - "x" stands for "extended", not "experimental".

# discuss-gc
- ## 

- ## 

- ## 

- ## [go 的 gc 性能如何？ - 知乎](https://www.zhihu.com/question/583328068)
- go gc目前方向是牺牲垃圾回收效率来换取低延迟，减少stw。
  - 使用内存写屏障方式来避免数据竞争问题，进而实现并发式gc，缩短了stw的时间。

- Go 的 GC（垃圾回收）是其语言设计中重要的一部分，具有高效的性能特征。Go 的 GC 算法是采用的是自适应垃圾回收（Adaptive GC）算法，其可以根据程序的运行情况动态调整回收的频率。Go 的 GC 能够很好的平衡内存使用效率和程序性能，同时也能够有效地防止内存泄漏。因此，Go 的 GC 可以说是非常出色的。

- ## [为什么 Go 在 GC 时 STW 的时间很短？ - 知乎](https://www.zhihu.com/question/326191221)
- 严格来说还是有stw的, 只是极其短, 通常低于1ms级别的, 就是尽量想办法让gc过程分散化, 当然也是利用了go的一些特性而用了些tricks.
- 总的来说, 确实是牺牲了gc吞吐量换来了极短的stw, 这也是故意这样设计的:
  - 一是go的主要应用领域不是CPU敏感的, 而是需要高开发效率甚于高性能的C语言替代品, 通常用于重度IO领域; 
  - 二是go避免了跟jvm和.net这样高吞吐量gc的正面竞争, 发挥出不可替代短stw能力.

- 看Golang自己的proposal。非STW阶段都不打扰执行，WB（write barrier）开启的阶段稍微损失性能，所以直到STW之前都可以认为系统执行的很快，到了STW就停止执行了

- ## [go没有虚拟机怎么运行gc的？ - 知乎](https://www.zhihu.com/question/58863427)
- GC只是内存管理那块的，负责分配和自动回收的。
  - 有的GC算法，例如标记扫描，连编译时插入代码都不需要，就可以用的。
  - Go的GC现在是CMS并行GC，其编译器在编译代码的时候会插入相关的代码进你的程序的，去实现什么时候需要暂停，什么时候启动回收，还有内存中的对象（指针）信息，写屏障检查

- 其实 引用计数 也算是GC的一种的。但是一般我们说的GC，并不包括引用计数的，一般单独说成RC。

- GC统一理论：任何一种GC算法都是跟踪回收和引用计数回收两种思路的组合。

- 虚拟机和gc并没有必然联系，或者你可以认为go虽然没有vm，但是有vee（virtual execute environment，虚拟执行环境）

- 
- 
