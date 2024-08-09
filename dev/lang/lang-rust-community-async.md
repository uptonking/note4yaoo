---
title: lang-rust-community-async
tags: [async, community, rust]
created: 2023-08-28T04:42:35.252Z
modified: 2023-08-28T04:43:22.738Z
---

# lang-rust-community-async

# guide

# discuss-stars
- ## 

- ## 

- ## [为什么tokio能成为rust异步标准？ - 知乎](https://www.zhihu.com/question/586107884)
- tokio 能成为目前 Rust 异步运行时的事实标准，最主要的原因应该是马太效应——用的人最多。
  - tokio 出得早，2018年发布，而 async-std 2019年发布。（async/await 语法稳定于 2019 年底）
  - tokio 背后有亚马逊这样的大客户支持和应用。
  - hyper 默认支持 tokio。作为 Rust 中最完整的 http 服务端和客户端，这位更是重量级。
- tokio 是 M: N 协程运行时，IO 风格是reactor。
  - 与之相对的还有结合 thread-per-core 和 io-uring 的协程运行时，每个协程不会跨线程运行，IO 风格是 proactor。例如字节跳动的 monoio，Datadog 的 glommio。

- 按我理解 reactor 就是来数据了通知你读，proactor 就是来数据了给你读好

- 有个异步标准就不错了. 我scala连IOMonad都好几家, 谁也不服谁倒不是啥大事儿, 天天还给你掐来掐去

- 简单。性能不成可以优化，语法复杂比较难提高。
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Async is the final boss in Rust. _202408
- https://x.com/fredine/status/1821048270711615936
- Mutex, Macros, Traits and multithread stuff are also mini bosses

- ## So http://tokio.rs is Spring? 
- https://twitter.com/criccomini/status/1775277749537792059
- it is netty and its associated projects. 
  - there are alternatives to its components. if you are looking for something basic it works. 
  - tikv has its own alternatives to parts of it e.g., https://github.com/tikv/yatp instead of tokio::task for tasks. 
  - There are other async runtimes too
  - on the other hand Tonic/Hyper is pretty common ways of doing protobuf based RPC servers. 
  - This is what I meant by async being a mess in some ways :) (See also crossbeam, mio, parking lot which do both sync and async. Then again, Java didn’t get NIO until 1.4 etc…)

- there is support for atomics, basic/sync blocking multi-threading and channels already in stdlib, tokio does have a good channel implementation that can work as both async and sync. crossbeam has concurrent skip lists, additional channels and locks? and other neat things. 
  - note that my opinions on these matters (parallelism and concurrency) are excessively grumpy(脾气暴躁的) as i deal with it day to day. (i also happen to think java.util.concurrent is the gold standard for concurrency and i refused to use anything else in the JVM land, including when using Scala, where I just ignored its own Futures…)

- ## I have decided All IN async fn and stopping implementing poll based futures any more (although I spent a lot of time to make them works correctly)
- https://twitter.com/OnlyXuanwo/status/1770122232146305162
- The first problem: rustfmt won't format `stream!` macro

- ## Does https://github.com/cloudflare/pingora has potential to be the killer application of tokio?
- https://twitter.com/leiysky/status/1763203777543479473
- It's not raw tokio it's Pingora tokio runtime
  - By default it will use the stealing runtime, which is tokio runtime. And the no stealing runtime is backed by multiple tokio single-threaded runtime. Thus it's a typical tokio application
- No stealing runtime seems interesting. Is it becoming thread per core?
  - Not sure. Good to read the internal doc here

- ## How do you track memory usage in Rust async? 
- https://twitter.com/BohuTANG/status/1762675998997577928
  - For a data warehouse developed in Rust, like Databend, tracking and controlling memory usage is very challenging and has consumed a lot of our effort.

- Write your own runtime or drop the async ecosystem ... A Data INFRA System always ends with its own runtime.

- ## [rust 的异步为什么要把网络库重新写一遍？ - 知乎](https://www.zhihu.com/question/556880425)
- go 的异步是有栈协程，无传染性，任意函数调用里都可以切换控制权。底层网络库可以选择切换，也可以选择阻塞，不一定需要提供两套 API。 go runtime 本身就是异步运行时，标准库自然都是异步的。
- rust 的异步是无栈协程，有传染性，只有在await 点才能切换控制权。必须整个应用都异步化，才能最大程度发挥异步的优势。所以形成了一套异步生态系统。
- rust 有实现有栈协程的能力，但由于原子性和安全性的冲突、空间利用率、堆分配等问题，最后胜出的是无栈协程。

- async/await的传染性问题，不光是rust，连async/await的鼻祖C#，都是两套API。这是async/await这一套实现协程的通病。
  - 某些语言走了有栈这一条路，如Java21的虚拟线程实现，就是线程和协程一套API。
- 有栈的主要问题是栈内存消耗比较大。
- java的线程和协程是一套API，根据运行上下文自动适应是阻塞还是非阻塞。因为Java的有栈协程不是语法糖，而是JVM支持的，并且Java语言层面重写了bio，juc，socket，以及synchronized除外的所有lock实现等。除了synchronized关键字不支持一套API阻塞和非阻塞都支持。但是synchronized改成lock的API调用并不是难事。
- java的虚拟线程是残缺的，因为缺乏go channel那样的数据结构，并且很多底层操作还不支持，要用好很难。此外，有栈协程性能上是有缺陷的。

- 任何语言的同步和异步生态都是割裂开来的，又不只有Rust是这样。但是Rust未来有可能将两者统一统一，这就得看“关键字泛型”的进度和效果。

- ## I suppose that Async Rust may properly separate four concepts:
- https://twitter.com/brabalawuka/status/1751100101312094607
1. Libs that are runtime agnostic, e.g. combinators, channels.
2. Libs that bind to a runtime, e.g., timers, IO structs.
3. Runtime that schedules runtime-agnostic future.
4. Runtime that schedules certain tasks.

- > Runtime that schedules certain tasks.
  - More certainly, runtime that drives (IO) tasks. A runtime scheduling common futures cannot move forward such tasks itself. Just like async-executor cannot drive tokio IO tasks.

- ## 大致搞懂了 #Rust Async Runtime 的实现路线。可以先直接拉到最后读结语部分：
- https://twitter.com/tison1096/status/1721354360922546275
  - 目前只有 Future 和 Waker 接口是 Stable 接口，其他的 block_on 和 spawn 也好，async io 和 timer 的实现也好，都是一些最佳实践。这也能看出来目前 Async Rust 不稳定的状态。
  - [Async Rust 的实现 | 夜天之书](https://www.tisonkun.org/2023/11/05/async-rust/)
- 我四年前开始写 Rust 就是这个状态，现在还是
