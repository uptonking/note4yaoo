---
title: thread-lang-rust
tags: [lang, rust, thread]
created: 2023-10-06T16:26:26.532Z
modified: 2023-10-06T16:26:57.557Z
---

# thread-lang-rust

# guide

# discuss
- ## 

- ## 

- ## 

- ## 还是 Rust 高级，测试默认是并行跑的。
- https://twitter.com/yfractal/status/1776906689549082843
  - 我在测试结束的时候，清空了 redis。一个测试好好的，两个测试稳定报错。我开始以为 Rust 给我指令重新排了序，后来发现测试原来是并行跑的。

- ## 依我看，rust 并不适合大部分项目。rust优点是内存安全，缺点是表达能力太差。
- https://twitter.com/geniusvczh/status/1773593794199384320
  - 需要内存安全的项目少之又少，而表达能力差直接影响到写不出用起来舒适的库（看看隔壁Jvav ）。
  - 内存安全也不是免费的，你得加一堆东西来让编译器证明，结果大家学不会就只能unsafe，退化成了好看一点的C语言，脱裤子放屁

- ## 写多了 JSON.stringify / JSON.parse，现在发现用 rust 生成个 JSON 都好费劲，JS 太灵活了
- https://twitter.com/zoomdong2/status/1770085465955369054
- 静态语言是这样的。
  - 没有对象字面量的动态语言在这方面体验是最差的.

- ## The US government explicitly recommends 6 memory safe languages:
- https://twitter.com/samuel_colvin/status/1763339372361814187
  - C# - created by Microsoft
  - Go - created by Google
  - Java - created by Sun, bought by Oracle
  - Rust - create bor Mozilla
  - Swift - created by Apple
  - Python - create by one fucking genius on his own in his Christmas holidays 

- For those saying "but Python is written in C" please think for a minute. All these languages are implemented using tools which are not themselves memory safe - it's precisely the language which provides a way for developers to construct assembly instructions in a memory safe way.
  - E.g. Rust generates llvm code. Llvm is not memory safe - it's the borrow checker etc. that make Rust memory safe.

- ## [Rust语言已有哪些成功的（被看好的）应用、实践？ - 知乎](https://www.zhihu.com/question/314665060)
- Rust 入驻 Linux 内核，同时又入驻 Windows 内核，世上两大操作系统都青睐 Rust
  - 安卓21年的时候就引入了，比linux和win还早

- ## 想问问大家写 Rust 都用什么 IDE。 最近体验了一下，感觉 RustRover 也不是很好用啊。经常卡住+代码补全提示不出来。
- https://twitter.com/jihuayu123/status/1755454756448014441
- 随便找个编辑器搭配 rust-analyzer 都很好用

- ## 🤼🏻 Haskell proves you don't need null at a high-level. Rust proves you don't need null at a low-level.
- https://twitter.com/jdegoes/status/1754938879017140680
  - Why are you still using null, again??

- Haskell actually has 2 versions of null; ⟂ and None.

- on Web `null` is inevitable 
  - document.body.getAttribute('null') === null; // true
  - most APIs (note *most*, not all) don't understand `undefined` or `void`, they just deal with `null` instead to indicate absence of something that although *might* be not-null in the future.
  - I tend, at least in JS, to follow the same concept
  - one is a *maybe-null* well known field of the window object (or any DOM element, really) the other one is the complete absence of meaning/API.

- Strong disagree.  Both prove you can manage null or undefined memory at the language level. They both have null/undefined memory. It's how computers/os work. They just deal with it for you. Some use lifetimes and some gc. It's the tools they give you we should focus on!

- Unsafe rust does have null.

- ## Specific types like `Result` and `Option` in Rust offer  methods like `map` and `and_then` that enable a monadic interface, 
- https://twitter.com/debasishg/status/1753790041812558282
  - but Rust does not provide means to abstract over monads, which is an important difference with languages like Haskell. 
  - While having a common interface for `Option` , `Result` , and `Future` would be good, I don't miss monads in Rust where I can write imperative loops without worrying about shared mutable state.

- ## 🧮 graphs are quite hard to model with Rust, mainly because of the complex interaction between  ownership rules and managing mutable cyclic data structures. 
- https://twitter.com/debasishg/status/1752737782815195253
  - Was looking for options and found that arena based modeling (region-based memory management) is possibly the way to go. 
- Writing a linked list in C/C++ is trivial. In Rust it requires intermediate (almost advanced)  level of knowledge. When I first ended up using PhantomData, I thought to myself this is surely a hack.
- I don't think this is true. It's just that modeling graphs as nodes that have pointers to other nodes, as you might do on the JVM, does not work. But even on the JVM it is often better to model graphs with edges and node ids.

- What’s wrong with adjacency lists modelled as hashes? Check out cleora graph embedding or mine
  - petgraph, a widely used Rust graph crate, also uses adjacency list rep for it's main Graph type

- ## we delve into the challenges of building Zed's GPUI framework in Rust, navigating its unique ownership system to shape user interfaces.
- https://twitter.com/zeddotdev/status/1751003887706751229

- https://twitter.com/leiysky/status/1752680618767581563
  - 写 Rust 的一个好处是，大家各自被编译器折腾后都会最终设计出几乎一样的解法，大大降低了交流成本……

- ## I wonder if someone has written a "Rust for C programmers" blog post to highlight the semantic differences between the two languages...
- https://twitter.com/penberg/status/1746107695533281535

- [Rust for Embedded C Programmers - OpenTitan Documentation](https://opentitan.org/book/doc/rust_for_c_devs.html)

- For example, it took me a really long time to adjust to the fact that in Rust objects move in memory by default and you need to use Pin to keep them put. 
  - This is still sometimes counterintuitive to me when integrating with lower level things like `io_uring`. 
  - With C, once you `malloc()` an object, it's going to be at a fixed location allowing you to just pass a pointer to it. 
  - However, in Rust, the default behavior is the opposite, which leads to interesting bugs if you're not careful.
- Another thing that keeps biting me is mutability. 
  - In C, everything is mutable by default but in Rust you really are building with immutability by default. 
  - And usually, the way to make something mutable is to use interior mutability with something like `RefCell`.
  - I often make the mistake of passing a mut reference around only to eventually discover that it's pretty much impossible to evolve the code because the borrow checker starts to complain as soon as there's a possibility of multiple code paths mutating the same thing.
- Zig is certainly more natural language to integrate with the OS and libc interfaces. But Zig also has many of the same issues as C with memory safety and resource leaks, which makes Rust so attractive. 

- ## My 5 year prediction: we'll realize it was a mistake to write all of our high-level tools in a language built around systems-level memory safety (Rust)
- https://twitter.com/jlongster/status/1745094749717954705
  - The language itself is good but the entire semantics are built around something we don’t need and slow down development

- ## DWARF and frame pointers. It's a must-read if you're puzzled by perf, DWARF, frame pointers, profiling, or sampling.
- https://twitter.com/OnlyXuanwo/status/1735526268261847490
  - [feat: Enable `rustflags = "-C force-frame-pointers=yes"` default for opendal release process · apache/incubator-opendal](https://github.com/apache/incubator-opendal/issues/3756)

- ## Nowadays I have doubts about using Rust primarily for building cross-language bindings. 
- https://twitter.com/Horusiath/status/1734385412800745686
  - It's great language, but once you need to pass Rust-idiomatic API to C FFI (or WASM) things are no longer so smooth.
  - The major advantage of Rust was that past alternatives were way worse.
- Any good alternatives? 
  - Recently Zig gets some attention and it seems to target this space. But I have too little experience to confirm yet.
- I was really hoping for F# to take that space. But the only space F# is taking is in C# features.

- Cross-language is by definition not smooth, but I tend to agree that C-like APIs are easier to integrate with. That said, the ecosystem for cross-language bindings with Rust is fairly extensive. I douby Zig would do much better here because you anyway need to build some wrappers.

- Swift really shines in mixed native language projects
  - Swift is a tri force! (imperative, functional, concurrent)

- ## Rust is mostly an uglier OCaml. Fight me.
- https://twitter.com/basus/status/1730321811773014186
- Rust uses typeclasses, ocaml uses higher order modules. They feel completely different IMO.

- ## The three registers of Rust
- https://twitter.com/greg_johnston/status/1727817195093209356
1. `.clone()` everywhere because let’s be honest I’m parsing a CSV file and will only run this once a year
2. `Vec<Box<dyn SomeTrait>>` will be good enough for now
3. `macro_rules` to derive SomeTrait on n-ary tuples up to 16 so you never allocate

- ## 刚刚搜索Rust怎么实现双链表。Rust的某reddit社区坚持认为，Rust不需要双链表，因为XX性能原因，所以你写不出双链表也不是大问题，Rust把这个弄得很难写，不是大问题。
- https://twitter.com/JXQNHZr1yUAj5Be/status/1710474773954768987
  - 但这问题是在双链表上吗？人家是抛砖引玉，问有cyclic引用的数据结构在Rust怎么处理的一般问题。
- 所有循环引用结构在 Rust 都难写，目前我体验最好的 safe 的方案还是 index arena 的形式（需要依赖 unsafe 的 dep）

- 问题是rust连做一棵有环的树，都是天方夜谭啊……链表本身也是树，rust在数据结构方面的局限性不应该被无视
  - 没办法，rust 用了所有权这种东西，循环引用确实很难实现
- 生命周期/所有权要求的偏序结构，和环状数据结构的固有矛盾。

- 我觉得这是对 rust 有点苛求了，难写应该是只考虑使用 safe rust 的部分。如果能在 unsafe 实现的基础上封装出 safe 的 public API ，就够了
- 每次看到这种牺牲自由度，换取安全性的编程语言，我都忍不住想到点别的东西

- 不是bug, 是feature。 双向链表用 `LinkedList<T>` 就好。
# discuss-usecase 🌰
- ## 

- ## 

- ## Starting next week, @meilisearch will switch its core engine from Rust to C++. 
- https://twitter.com/Kerollmops/status/1774917166350868893
  - After years of struggling with segfaults, out-of-bounds issues, and a complex package manager, the team decided that the Rust language still needed to reach its promise of being the successor of C++.

- ## 为啥现在写本地模型更流行的是 c++ 和 python, 而不是近些年比较火的 Rust 和 go?
- https://twitter.com/holegots/status/1767428017960423484
- 之前研究过这个问题, 感觉的主要原因是 CUDA 和 CPP  耦合到一起了, 而 Python 和 CUDA/CPP 的交互已经有一整套生态和轮子, 
  - 反观其他语言(Rust/Go) 只能走 C 再调用 CPP 来调用 CUDA , 这点劣势太大了, 而且算法老哥们也大部分不太会这两个语言.

- 生态打不过，而且我个人理解主要计算是在 gpu 上面跑，这一块基本上都是 Python 胶水 + C++ 实现。 Rust 这边做 model serving 什么还挺好的。如果写 ml/dl 模型的话 binding C++ (流行度差很多数量级) 或者 Pure Rust (gpu 不支持) 的一些也有。其实目前不太看得到替换 Python 的必要。

- cpp底层+python应用+各种库=既灵活又高效还通用，go和rust我粗浅的感觉还是偏专长

- 我司也在搞端上（安卓，ios和pc）的模型，业务流程分为三块，云上的数据召回，端上动态数据召回以及端上模型（数据embedding和nn），云上的数据用go什么都可以，但是端上几乎不可能使用c++以外的语言，因为go，rust在机器学习库上非常少。c++有caffe和mnn。python是由于pytorch等，但也只用于训练

- 训练的package是python的，部署lib是cpp的。rust和go也能做，不是主流。甚至R, matlab, julia, perl, lisp, java都可以。

- C++ 和 Python 已经有了很成熟的生态和库。许多机器学习框架（例如 TensorFlow、PyTorch、Scikit-learn）都在这两种语言中得到了广泛的应用和支持。另外，C++ 语言所提供的内存管理能力可以支持更加高效的本地模型开发，Python 语言则具有更加方便易用的特点。Rust 和 Go 不如 C++ 和 Python 成熟

- 首先所有实验除了很早期之外都是利用py的各种库做。而且py上手落地都快，科学计算库非常成熟，利于快速实现算法，性能大家都是本质调cuda，那点卖点根本没意义。你从算法开发角度想就理解了。c++和cuda更不用说。

- ## [Complete Rewrite of ESLint | Hacker News _202211](https://news.ycombinator.com/item?id=33772530)
- also note that both Deno and Sveltekit moved from TypeScript to JSDoc

- Cloudflare made Pingora (Rust) to use instead of NGINX (C) though idk if that meets the rewrite criteria.
# discuss-rs-js
- ## 

- ## 

- ## 

- ## [Is there a transpiler or something that converts Rust code to JavaScript? _202112](https://users.rust-lang.org/t/is-there-a-transpiler-or-something-that-converts-rust-code-to-javascript/69324)
- WASM does not support threads, but in the browser it can be done using web workers if I understand correctly.
  - You won't be able to do anything that requires network access and so on. At least not in the browser.

- ## [Compiling Rust to JS? - community - The Rust Programming Language Forum _202001](https://users.rust-lang.org/t/compiling-rust-to-js/37480)
- It depends what you mean by compiling to "JS". Rust has an asm.js target too, so it's technically JavaScript. But asm.js back-end is not as reliable and fast as the WASM one.
  - TypeScript, CoffeeScript, and partially Dart can be compiled to code that looks like JavaScript source code, with the same higher-level constructs. But this is because semantics of these languages is very similar to JavaScript's, and these languages have intentionally chosen to avoid behaving in ways that are impossible to express in JS.
  - Rust does lots of things that high-level JavaScript code can't do, or does differently. Even simplest things like addition of two numbers has different semantics, so you can't translate Rust's a+b to a+b in JS.

- ## [Compile to javascript : r/rust _201902](https://www.reddit.com/r/rust/comments/am2qoc/compile_to_javascript/)
  - Is there a pathway to compiling Rust to JS? Like Scala.js or Gopher.js? 

- There is the asmjs-unknown-emscripten compile target, which compiles to asm.js (subset of JS) via emscripten.

- You can use the asmjs target, which produces perfectly fine JavaScript libs. 
  - Alternatively you could try to use the wasm-unknown target and use the wasm2js tool to convert the wasm file to JS
  - Unfortunately the latter case produces > 300 MiB JS files for me that break uglifyjs 

- ## [I rewrote 10k lines of JS into Rust over the last month. Here'a write up about i : rust_202010](https://www.reddit.com/r/rust/comments/k3jy5g/i_rewrote_10k_lines_of_js_into_rust_over_the_last/)
- Overall I've been brainstorming this change for a couple years. So I'd already shifted from a classical OOP mess with Shield/Weapon/Pillar inheriting from Permanent to one where everything is a Thing.
- I'd also moved towards having everything be referenced with integer ids which seems to be something Rust likes. This was originally so that a clone wouldn't need to update any references
- Rewriting let me come across a couple small bugs.

- ## I’m kinda fascinated by how Rust was the harbinger of next-gen JS tooling
- https://twitter.com/DasSurma/status/1712005157611774056
- One that hasn’t been mentioned is that it borrows some ideas from functional languages (sum types, monads, etc.) which makes it more elegant for AST manipulation. Same reason compiler devs love OCaml.

- I think it actually wasn’t Rust. It was esbuild showing the way. SWC existed years before but didn’t really catch on until later. It wasn’t end to end (no bundler). ESBuild showed how fast native tools could be and others had to follow to keep up.
