---
tags: [lang/java/jvm]
title: lang-java-jvm
created: '2019-07-03T05:33:54.419Z'
modified: '2020-07-07T08:09:54.436Z'
---

# lang-java-jvm

## classloader

## gc

## GraalVM

- GraalVM is a universal virtual machine for running applications written in JavaScript, Python, Ruby, R, JVM-based languages like Java, Scala, Groovy, Kotlin, Clojure, and LLVM-based languages such as C and C++.
- 支持多语言编程的通用虚拟机
- 项目的各组件大多以GPLv2的协议发布
- GraalVM CE is available for free for development and production use.
- 目前支持Linux和Mac，不支持Windows
- GraalVM开发了「跨语言互操作协议」，它是一种特殊的接口协议，每种运行在GraalVM之上的语言都要实现这种协议，这样就能保证跨语言的互操作性。 语言和语言之间无须了解对方就可以高效传值。该协议还在不断改进中，未来会支持更多特性。
- Oracle于20180417发布
- 主要组件
  - Graal：一个由Java语言编写的JIT编译器
  - SubstrateVM：一个对执行容器抽象层的轻量级封装
  - Truffle：一个用于构建语言解析器的工具集和API
- The Java architects worked to support multilingualism starting in Java 7 by conversions to Java bytecode by adding `invokedynamic` to the JVM specification. 
- The GraalVM team felt that since Java bytecode had too much Java semantics built into it, a longer term effort could be much more efficient and a 100% compatible implementation at that.
