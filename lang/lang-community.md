---
title: lang-community
tags: [community, lang]
created: '2021-08-30T06:33:01.504Z'
modified: '2021-08-30T06:33:45.293Z'
---

# lang-community

# discuss

- ## 

- ## 

- ## 

- ## 

- ## node.js 对 js 来说就是 runtime， 就像 jre 对于 java 一样
- https://www.zhihu.com/pin/1413223229317775360
  - node.js 不负责 parser 和 vm 的部分，这部分由 v8 负责。
- 任何一门语言只是对操作系统的能力做了抽象，然后提供 api 给 runtime 用，不同 runtime 做的抽象不同，
- node.js 和 jre 就有很多不同的抽象：node.js 里面的 异步+事件、stream、和 posix api 名字一样的 api 等，这都是它的特点，其实做的抽象并不多。。
  - jre 提供的各种包都做了很多抽象，使用各种设计模式，比如 io 包里面的各种 Reader、Writer、InputStream、OutputStream 的层层装饰等不同运行时都是基于操作系统能力做的抽象，
- 理论上来说，编译型语言的能力是最强的，因为可以使用全功能，解释型语言有的时候会遇到没有提供的操作系统能力，这时候只能做扩展了，比如 jre 的 jni，node.js 的 c++ addon。

- 语言和语言之间最大的区别是提供的能力不同，当然，支持的编程范式也不同，抛开语法和编程范式不谈，只谈提供的能力：
- 编译型语言因为是直接在操作系统上跑，所以可以使用操作系统的全部能力，
  - 解释型语言在 vm 上跑，依赖 vm 提供的 api，
  - 这些 api 有不同的抽象，nodejs 和 jre 的抽象都不同，
  - 但提供的能力类似，比如网络、文件系统等 io 能力、进程线程的能力。
  - 对于不够的能力，jvm 和 nodejs 都提供了扩展机制，分别是 jni 和 c++ addon。
- 如果需要的操作系统能力一样，那么不同语言表达同样的逻辑其实没多大差别，
  - 比如 babel 用 js 写转译器、swc 用 rust 写转译器，他们用的能力最多就是用读写文件、线程进程能力，这些 nodejs 和 rust 都提供了，那么表达同样的逻辑，用这语言实现同一种功能其实就没啥差别了，只不过在于编译型和解释型的运行效率上的差别。
  - 所以熟悉了 babel 再去学 swc，只不过是熟悉下 rust 语法就可以了，具体逻辑没啥差别，需要的操作系统能力也一样。同理，go 写的 esbuild 也是。
