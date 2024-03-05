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

- ## 

- ## 

- ## 

- ## 
# discuss-compiler-toolchain
- ## 

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
# discuss-gc
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
