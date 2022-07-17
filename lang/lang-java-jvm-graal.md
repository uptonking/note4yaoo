---
title: lang-java-jvm-graal
tags: [graal, jvm, lang]
created: 2021-01-15T04:08:52.762Z
modified: 2021-01-15T04:09:25.198Z
---

# lang-java-jvm-graal

# guide

# pieces

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

# discuss

- ## [为什么没人推动用 JS 实现 JVM 这件事，为什么浏览器不内置 JVM？](https://www.zhihu.com/question/333230233)
  - 为什么没人推动用js实现一个工程化的jvm，不是个人玩具类的，从而使浏览器可以运行java程序

- applet就是java在浏览器的执行环境，但是对比JS没有优势，被淘汰了。
  - jvm 是 c++实现的，js在浏览器上运行也是基于 V8 引擎的，所以不可能用 js 实现一个 JVM （没啥意义）
  - wasm 并不是编译为 js，而是直接编译成了浏览器可以运行的二进制模块

- 想用java写js的人有很多很多，可参考vaadin, gwt, jsweet, Java2Script等项目，都在致力于用java写浏览器程序
- 曾经的浏览器是可以用object或embed标签跑java程序的，但并没有多好用，而且有安全性问题，所以早就 ban 了。
- 有 WebAssembly 了。
  - JVM 只是 Java 一家用的，WebAssembly 是一套二进制标准给所有语言用，到时候就不只是 Java 了，还有 C#、Rust、C++，等等等等。

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

# ref
