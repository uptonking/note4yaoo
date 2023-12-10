---
title: web-wasm-compiler
tags: [compiler, wasm]
created: 2023-12-10T10:45:43.307Z
modified: 2023-12-10T10:45:52.861Z
---

# web-wasm-compiler

# guide

# Emscripten
- Emscripten is a complete compiler toolchain to WebAssembly, using LLVM, with a special focus on speed, size, and the Web platform.
- The main tool is the Emscripten Compiler Frontend (emcc). This is a drop-in replacement for a standard compiler like gcc or clang.
  - Emcc uses Clang and LLVM to compile to WebAssembly. 
  - Emcc also emits JavaScript that provides API support to the compiled code. That JavaScript can be executed by Node.js, or from within HTML in a browser.
- Emscripten SDK(emsdk)  is used to install the entire toolchain, including emcc and LLVM and so forth.

## [docs](https://emscripten.org/)

- 
- 
- 
- 
- 

# more

# discuss

- ## 

- ## 

- ## [要想实现编程语言，LLVM 和 JVM 哪个更方便？ - 知乎](https://www.zhihu.com/question/429463756)
- 我觉得这个不是谁更方便的问题，而是看你的需求。
  - 如果要重新实现一个编程语言，LLVM和JVM的区别只是CodeGen部分的target不同，也就是LLVM IR和Java Bytecode的区别。
  - 更高层来看，其实是managed runtime（JVM、CLR、V8 Engine等）和unmanaged binary的区别。
- 以我的经验来看，如果只是想做个toy language，二者区别不大。

- jvm-pros
  - 可以选择在Java的AST上修改，可以参考Lombok、JSR 269的实现方式；另外还可以通过JSR 223集成进Java语言；
  - 如果做到和Java的兼容，那么可以瞬间获得世界上最大（可能）的第三方库生态；例如Kotlin、Groovy等；
  - 有很多方便的字节码生成库（asm、ByteBuddy等），毕竟没有其他语言比Java更喜欢动态字节码生成了；
  - 可以方便地使用JVM上的debug、management等规范；
  - 成熟的JIT支持；
  - Write once，Run(Debug) everywhere
- jvm-cons
  - JVM的字节码也是Object-Oriented，所以如果是要设计其他编程范式的语言，在字节码生成方面上会比较麻烦，而且需要比较复杂的Runtime支持；
  - 运行效率、启动速度比不上native。

- llvm-pros
  - 成熟、模块化的框架支持；文档详尽，例如官方就给了一个Kaleidoscope的教程；
  - 不需要优化，交给LLVM的各种优化pass就好了；
  - 可以直接target到多种操作系统、指令集架构上；
  - 也有JIT的支持；
  - 甚至可以直接复用clang的AST
- llvm-cons
  - SSA形式的IR、CFG、phi等编译原理概念，以及其在LLVM中对应的数据结构、实现方式等等，会给心智造成一定的负担；
  - LLVM已经成为了版本号狂魔，有一些API随着版本升级已经不可用了，网上的资源很多已经过时了

- 你不考虑一下graalvm的substrate吗？

- 个人感觉是LLVM方便，因为它被设计出来就是干这个事的，而JVM最初只是java的runtime，只是现在诞生了一些符合java字节码规范的语言。
