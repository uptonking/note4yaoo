---
title: lang-cpp
tags: [cpp, lang]
created: 2019-06-09T05:36:54.368Z
modified: 2020-07-14T09:26:25.358Z
---

# lang-cpp

# guide

- classic-examples-cpp
  - onlyoffice-core(server是c#)
  - crdt
  - db, git-like
  - more: json-parser
# dev
- make用来执行Makefile
  - make工具可以看成是一个智能的批处理工具，它本身并没有编译和链接的功能，而是用类似于批处理的方式，通过调用makefile文件中用户指定的命令来进行编译和链接的
  - makefile命令中就包含了调用gcc（也可以是别的编译器）去编译某个源文件的命令
  - makefile对简单工程可以手写，对大工程手写makefile很麻烦，若换平台则要重新修改
- cmake用来执行CMakeLists.txt
- qmake用来处理*.pro工程文件
- Makefile的抽象层次最低，cmake和qmake在Linux等环境下最后还是会生成一个Makefile
- cmake和qmake支持跨平台，cmake的做法是生成指定编译器的工程文件，而qmake完全自成体系
- cmake也能生成针对qt 程序的那种特殊makefile，只是cmake的CMakeLists.txt写起来相对与qmake的pro文件复杂点
- c++开源项目源码阅读推荐：STL, Boost， leveldb
- c语言头文件 .h 
- c语言源文件 .c
- c++头文件 .h/.hpp/.hxx
- c++源文件 .cpp/.cc/ `.C` /.c++/.cxx
- VC里用cpp作后缀名, 在GCC里默认采用C、cc、cxx作为后缀名
- 对Win来说"test.c"和"TEST. C"是完全相同的文件名，但在Linux/Unix平台上就不同了
- GCC相关文件后缀
  - .c为后缀的文件，C语言源代码文件； 
  - .a为后缀的文件，是由目标文件构成的档案库文件； 
  - `.C` ，.cc或.cxx 为后缀的文件，是C++源代码文件； 
  - .h为后缀的文件，是程序所包含的头文件； 
  - .i 为后缀的文件，是已经预处理过的C源代码文件； 
  - .ii为后缀的文件，是已经预处理过的C++源代码文件； 
  - .m为后缀的文件，是Objective-C源代码文件； 
  - .o为后缀的文件，是编译后的目标文件； 
  - .s为后缀的文件，是汇编语言源代码文件； 
  - `.S` 为后缀的文件，是经过预编译的汇编语言源代码文件。
- TCMalloc是Google开发的内存分配器
  - 在不少项目中都有使用，例如在Golang中就使用了类似的算法进行内存分配
  - 它具有现代化内存分配器的基本特征：对抗内存碎片、在多核处理器能够scale
  - 据称，它的内存分配速度是glibc2.3中实现的malloc的数倍
# C

# C++

## STL

## Boost

- boost就是STL以后的样子

## compiler 编译器

- 传统编译器的工作原理基本上都是三段式的，可以分为
  - 前端（Frontend）：前端负责解析源代码，检查语法错误，并将其翻译为抽象的语法树（Abstract Syntax Tree）
  - 优化器（Optimizer）：优化器对这一中间代码进行优化，试图使代码更高效
  - 后端（Backend）：后端则负责将优化器优化后的中间代码转换为目标机器的代码，这一过程后端会最大化的利用目标机器的特殊指令，以提高代码的性能

### LLVM - Apache 2.0

- The LLVM Project is a collection of modular and reusable compiler and toolchain technologies.
- 从字面上来讲，LLVM(Low Level Virtual Machine)是一个底层虚拟机，LLVM曾经有一部分功能对虚拟机有所帮助。但现在，LLVM所代表的基本和虚拟机没有关系了，而是直接作为一个项目名字使用
- LLVM可以被看作是一系列的编译器和工具链技术的集合，而且它们是模块化，并且是可重用的
- LLVM是一个C++实现的开源软件；
- LLVM本身并不是编译器，只是一套用于开发编译器、解释器等程序语言相关工具的库，主要聚焦于编译器后端功能，如代码生成、代码优化、JIT等
- llvm目前它支援了包括ActionScript、Ada、D语言、Fortran、GLSL、Haskell、Java bytecode、Objective-C、Swift、Python、Ruby、Rust、Scala以及C#
- 应用场景
  - 用它来做静态编译器后端，没问题；
  - 做动态编译器后端，也能行。
  - 单独拿出LLVM的一个或多个pass来做IR到IR的转换也不在话下。
  - 基于LLVM来做调试器，也没问题。
  - 拿LLVM IR当跨平台汇编用也很有趣

### GCC - GPL

- The GNU Compiler Collection includes front ends for C, C++, Objective-C, Fortran, Ada, Go, and D, as well as libraries for these languages (libstdc++, ...).
- GCC was originally written as the compiler for the GNU operating system
- G++则是专门用来处理C++语言的，G++是GCC编译器集合的一个前端
- gcc编译程序主要经过四个过程
  - 预处理（Pre-Processing）
  - 编译 （Compiling）
  - 汇编 （Assembling）
  - 链接 （Linking）

### Clang - Apache 2.0

- Clang 是一个 C++编写、基于LLVM、发布的 C/C++/Objective C/Objective C++ 编译器，其目标（之一）就是超越GCC。
- Clang只支持C，C++和Objective-C三种C家族语言
- 相比于GCC，Clang具有如下优点
  - 编译速度快: 在某些平台上，Clang的编译速度显著快过GCC(Debug模式下编译OC速度比GGC快3倍)
  - 占用内存小: Clang生成的AST所占用的内存是GCC的1/5左右
  - 模块化设计: Clang采用基于库的模块化设计，易于IDE集成及其他用途的重用
  - 诊断信息可读性强: 在编译过程中，Clang创建并保留了大量详细的元数据，利于调试和错误报告
  - 设计清晰简单，容易理解，易于扩展增强
# discuss-toolchain
- ## 

- ## CMake is the standard way to build C and C++ software portably. 
- https://twitter.com/lemire/status/1711801773042630665
  - It is currently challenging but we can make it easier by documenting best practices.

- There is actually no standard nor consensus for C/C++. 
  - There is no consensus, that’s for sure, but it is as close to a standard as it gets.

- CMake's problem is not just the documentation, it's its constant changing APIs, the growing amount of code required to just get something seemingly simple going on, over-complicating the build process, the syntax, and so on! CMake is too big to be too good!

- CMake needs to be decomposed: config | make | cache
# discuss
- ## 

- ## 

- ## 

- ## 
