---
title: thread-lang-rust
tags: [lang, rust, thread]
created: 2023-10-06T16:26:26.532Z
modified: 2023-10-06T16:26:57.557Z
---

# thread-lang-rust

# guide

# discuss-stars
- ## 

- ## 

- ## Sounds like there was an effort to rewrite React Compiler in Rust, but JavaScript won out in the end.
- https://x.com/birch_js/status/1901454090552709542
  - Interestingly, it's eventually planned to compile it with Static Hermes. Which implies we may get a headless Static Hermes-based runtime in future?

- ## 🤔 Prisma rewrite in TypeScript _202412
- https://x.com/localhost_5173/status/1863873604229972068
- [Prisma ORM Manifesto: Clarity and Collaboration _202412](https://www.prisma.io/blog/prisma-orm-manifesto)
  - Prisma’s architecture has historically limited community contributions. Core functionality—such as query parsing, validation, and execution—has been managed by our Rust engine, which has been opaque to our TypeScript-focused community. Expanding capabilities or fixing core issues often fell solely to our team.

- https://x.com/jarredsumner/status/1863837970471784924
  - I bet moving from Rust to TypeScript will make Prisma faster. NAPI overhead & event loop scheduling overhead is significant for DB drivers.
  - The APIs we use to make bun:sqlite & Bun.sql’s native implementations fast don’t have an equivalent for napi because they rely on JSC internals that don’t really exist in V8
- Is the overhead of transitioning between JavaScript and WebAssembly smaller? Prisma’s approach make sense, but I do wonder if embedded databases such as SQLite are better off linked to the runtime or will Wasm be a good long term solution 
  - The overhead between js and wasm is large. You end up with tons of copies back and forth across the barrier.
- Right, but is there anything we can do at the runtime level? Perhaps embedded databases are the only use case here, but it’s hard for me to see them being special purpose built just for JavaScript
  - I'm not sure what the solution is. I actually planned to go the other way – Zero is current implemented in TS for performance and convenience in the web ecosystem, but when we get to mobile my assumption is we will go back to native. I was hoping by that time the wasm folks have figured this marshaling stuff out.
-  the whole situation is a bit absurd: both JavaScript and Wasm code runs on the same runtime (V8 or JavaScriptCore), but we don't do that because the overhead is too high. However, the overhead of native calls via NAPI is high too. And from packaging perspective, the way I do with Limbo is JavaScript + Wasm and it's so much simpler compared to SQLite and libSQL having to build for every native target out there...
   - Interesting. I assumed you’d want every drop of native perf possible (wasm still has significant overhead). Also I assumed if you were in native land you’d have access somehow to full js api with goodies like v8’s ExternalString, which can prevent copies. But we haven’t tried any of this.

- Rust adds overhead in all situations. C is better for certain tasks, and JavaScript/TypeScript works best for the rest.

- NAPI is a glaringly inefficient FFI. It's worse than JNI.
- And NAPI-RS just adds even more overhead. It's all about the algorithms, not the language.
- and system design in this case. The cost of having extra rust process running side by side is not worth it.

- If struct comes part of the language. How much difference do you think it would make for JS tooling being in JS

- ## I learned Rust by typing out examples, making mistakes, and fixing them
- https://x.com/penberg/status/1862209708301386124
  - The problems tend to be localized enough for you to solve them as a beginner.
  - So i bought two Rust books, typed out all the examples, made mistakes, and eventually learned how to write Rust!

# discuss
- ## 

- ## 

- ## 

- ## still, you think Rust is “too new” to learn?
- https://x.com/0xlelouch_/status/2001602140436058112

> Linux kernel is gaining Rust
> Windows kernel has Rust components
> Android has Rust in system services
> Firefox uses Rust (Servo, Stylo, parts of Gecko)
> Chrome uses Rust (security-critical components)
> AWS is writing core infra in Rust
> Cloudflare rewrote hot paths in Rust
> Discord backend uses Rust
> Dropbox uses Rust for sync engine
> Figma uses Rust for performance-critical code
> Meta uses Rust in production tooling
> Microsoft recommends Rust for new systems code
> Linux drivers are being written in Rust
> PostgreSQL extensions are being written in Rust
> Wasm runtimes (Wasmtime, Wasmer) are Rust
> Blockchain clients (Solana, Polkadot, Near) are Rust
> Game engines (Bevy) are Rust
> Databases (TiKV, Redpanda parts) are Rust
> Observability tools (Vector) are Rust
> CLI tools you use daily (ripgrep, fd, bat) are Rust

> Ripgrep is Rust
> Alacritty is Rust
> Tokio (Discord backend) is Rust
> Cloudflare edge is Rust
> Firefox Quantum CSS is Rust
> Deno is Rust
> SWC is Rust
> 1Password core is Rust
> Signal protocol is Rust
> Android Bluetooth is Rust
> Linux kernel (6.1+) accepts Rust
> npm (parts) is Rust
> Windows (parts) is Rust

- still, you are not convinced to learn C and C++

> Linux is C
> Git is C
> Python interpreter (CPython) is C
> Ruby interpreter (MRI) is C
> PostgreSQL is C
> SQLite is C
> Redis is C
> MySQL is C++
> MongoDB is C++
> Unreal Engine is C++
> Chrome is C++
> Firefox is C++
> Windows kernel is C
> macOS kernel (XNU) is C
> Photoshop is C++
> VMware is C++
> TensorFlow (Core) is C++

- https://x.com/0xlelouch_/status/2001603136180592647
  - still, you think Go is “just a simple language”?

Kubernetes is written in Go
Docker (engine) is written in Go
containerd is written in Go
etcd is written in Go
Prometheus is written in Go
Grafana backend is written in Go
Helm is written in Go
Terraform is written in Go
Consul is written in Go
Vault is written in Go
Istio control plane is written in Go
Linkerd is written in Go
Caddy web server is written in Go
CockroachDB is written in Go
InfluxDB is written in Go
Loki is written in Go
OTel collectors are written in Go
Cloudflare systems heavily use Go
Uber’s internal platforms use Go

- ## Rust exists because C++ refused to admit it has problems.
- https://x.com/davepl1968/status/1904324609232736542
- No, Rust exists because people treat C++ as "C with Classes" and continue to abuse it. If you stick to unique_ptr and shared_ptr and so on, you can write entirely memory-safe code trivially.

- https://x.com/penberg/status/1904441622802145352
  - Rust exists for many reasons, but one of them is because there are as many variants of C++ as there are developers. C++ has a lot of features and it’s hard to ”stick to” a specific subset in larger projects…
  - So, you're saying Rust is simply a coding style guideline of C++? 

- ## 用 rust 实现一些偏底层的数据结构真的是太痛苦了，比如实现一个高性能的 lrucache，你不用 unsafe 基本不可能（至少我没这能力）。
- https://x.com/minibobo/status/1904193920684486748
- 此事早已有定论，LinkedList这种数据结构在rust都是噩梦

- ## 🤔 [Four Years of Rust | Hacker News _201905](https://news.ycombinator.com/item?id=19919561)
- 
- 
- 

- ## Someone said that even after 5 years of Rust and they still end up in situations when I need to spend over an hour to wrestle with borrow checker. 
- https://x.com/ifesdjeen/status/1870481296386077176
- You need not run into lifetimes, until you need absolute raw peformance. Just clone away until you get things working, then measure the sections in hot loop, and introduce lifetimes there incrementally.
  - Make it work, make it better, make it faster. In that order.

- ## 看来 PingCAP Talent Plan 是彻底抛弃 Rust 了 _202411
- https://x.com/blackanger/status/1858467762202607932
- 公司很久之前就 Go 上 Rust 下了。因为不那么核心的部分没那么需要memory safety之类的，快速出原型推向市场看客户反映更关键。
- 正确选择，Rust对绝大部分创业公司而言都不适合。学习成本偏高

- ## This post on rewriting Rust is very interesting, but I kept thinking: "and where's the stuff you would remove? you would remove stuff, right? not just add stuff?"
- https://x.com/thorstenball/status/1839202375568892361
- if we're talking rewrites, just off the top of my head:
  - remove proc macros
  - remove implicit into_iter
  - remove Drop
  - remove half of capabilities of module system (why http://mod.rs or http://foo.rs? Just one)
- It seems like Rust is running into the cpp problem. The features will continue until morale improves.

- ## In Rust when you see `let y = x.clone();` You don’t know if it’s a cheap reference count increment or an expensive allocation and memcopy.
- https://x.com/fredine/status/1808654410660393457
  - You can do this instead: `let y = Arc::clone(x)` ; 
  - And enforce it with a clippy lint: #![deny(clippy::clone_on_ref_ptr)]

- ## io_uring是不是可以看成kernel和user space通过两个channel完成同步？
- https://x.com/JXQNHZr1yUAj5Be/status/1807001570258845819
- 可以，而且还可以用 provided buffer 做一个 spsc ringbuffer 用 atomic 同步
- aio 是不是也是

- ## Do you still use .env files in your #rustlang project?
- https://x.com/5422m4n/status/1801362925141246118
  - TIL: the `env` section in your workspace `.cargo/config.toml` can be a drop-in replacement

- At first I thought "cool", but I'm not a big fan of asymmetry. cargo run and running the binary directly should both do the same. I guess it's more for build scripts and rustc variables.
- Yeah. This is awesome but I want to commit my config while I wouldn’t want to commit my secrets.

- ## Rust really makes it hard to move out. You get:
- https://x.com/Horusiath/status/1800411588660502855
  - docs with compile-verified snippets
  - test & benchmark tools
  - code formatter
  - good abstractions at stdlib level
  - solid compile-time safety mechanisms
- You try other PL and realise, these things are not to be taken for granted.

- ## 🔢 tldr: JSON 中的数字类型长度为 53bit，所以存入一个 `u64` 会产生神秘 bug
- https://twitter.com/roifex/status/1779879331378118918
  - 群友：Rust 应该立马整一个 u53 类型
- 不是 53 位整数，而是 double-precision 64-bit binary format IEEE 754 value，这是标准规定了的。
  - 如果你有一个 64 位数，如果它的用途是 ID 或 hash 而非数值，在 JSON 和 JavaScript 当中你应该用字符串存储。
- js 的 number 应该对应到 f64, 它恰好有 53 位二进制有效数字(小数部分 52bit + normal value 默认整数部分为 1)（其实比 u53 多个可以表示正负

- 因为这个锅，本来准备用json的structure HTTP header改了别的形式
- JSON 本身应该只规定了数字长啥样，没有规定它怎么存/怎么用。这个限制应该来自 js？ 
  - 不过 lsp 最重要的客户端 vscode 是 js 实现，那也就只能去兼容它。
  - 如果 lsp 的两端都能够正确处理 u64 大小的 JSON，它应该没有问题的。

- 这个东西在写 go grpc gateway 的时候有痛到， 一开始我写了一堆 Unmarshaler 后来意识到可以用 第三方的 json 库比官方机灵多了

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

- ## The thing I appreciate the most from @rustlang is its mentality that it explicitly shows all possible problems and race conditions in your code. 
- https://twitter.com/CompuIves/status/1387830838792970243
  - You have to decide how to handle it, and you can decide to ignore it, but then you made that as a conscious decision.
- An example of this is parsing a string. 
  - Many languages would implicitly handle invalid strings by throwing an error, or worse, by returning something unexpected.
  - In Rust, the return type specifies that this can go wrong, and you can decide to handle the error or to let it panic.

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

- ## 

- ## 

- ## 📌 rust usage
- https://x.com/adahstwt/status/2053672160053567569
Rust + Tokio → Async Systems
Rust + Actix → High-Performance APIs
Rust + Axum → Modern Backend

Rust + Diesel → ORM / DB Access
Rust + SQLx → Async Database

Rust + WebAssembly → Browser Apps
Rust + Yew → Frontend (WASM)

Rust + Tauri → Desktop Apps
Rust + egui → Native GUIs

Rust + Bevy → Game Development
Rust + wgpu → Graphics

Rust + Embedded Rust → Firmware / IoT
Rust + Linux Kernel → Systems

Rust + Polars → Data Processing
Rust + Arrow → Analytics

one language

> performance
> safety
> systems
> full-stack (yes)

and people still say
“rust is too hard” 

- Every language has this ecosystem, long before Rust existed. So being hard is something else & having a rich ecosystem is something else.

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
# discuss-axum-actix 🆚
- ## 

- ## [Axum or Actix in 2024 : r/rust _202403](https://www.reddit.com/r/rust/comments/1bj9rc3/axum_or_actix_in_2024/)
- They're both very similar now, it doesn't matter much for most things. The only thing is that Actix Web has its own ecosystem for middleware and such while Axum uses the Tower ecosystem.
- it's based on the tokio + hyper ecosystem, which is definitely production-ready. axum is also macro-less, which is a plus for me
  - Actix Web can also be used without macros similarly to Axum and others, just so you know.

- I have a slight preference for actix because of better OpenAPI integration.

- ## [Axum vs Actix : r/rust _202402](https://www.reddit.com/r/rust/comments/1b216bf/axum_vs_actix/)
- actix uses a pool of single thread tokio runtimes and axum just uses the multithread runtime. The multithread runtime does add a litte big overhead but in situations where the endpoints in the backend do generate not even loads when executing that can be better then a bunch of single thread runtimes.

- Go with axum, i's a lot easier to get into and the performance difference is negligible. Most Benchmarks are gamed because you can skip a lot of checks you want in a real life scenario. The main factor is that actix is essentially single threading tasks so it gains a bit on that front.

- If you're just looking for performance, , there's a fork of Actix you should look into named ntex. It currently sets on the throne of synthetic benchmarks.
- Actix docs are way better.
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

- ## 🆚️ rust vs js toolchain
- https://twitter.com/kiyov09/status/1712126491402645878
- Now we need to ship a 'Make' with rules that that implicitly detect the language and based on the folder structure and call the appropriate commands
