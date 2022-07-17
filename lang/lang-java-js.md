---
title: lang-java-js
tags: [java, js, lang]
created: 2021-01-15T04:08:33.542Z
modified: 2021-01-15T04:08:46.423Z
---

# lang-java-js

# guide

# pieces

- rhino
  - jdk6/7中支持执行js
- nashorn
  - jdk8正式发布
  - jdk 15删除了Nashorn JavaScript 引擎、相关 API 和jjs工具
- graaljs
  - 在新项目中推荐使用

# Graal.js

- graaljs /933Star/UPL/202101/cpp
  - https://github.com/oracle/graaljs
  - https://www.graalvm.org/reference-manual/js/
  - A ECMAScript 2020 compliant Javascript implementation built on GraalVM. 
  - With polyglot language interoperability support.

- The goals of GraalVM JavaScript are:
  - Execute JavaScript code with best possible performance
  - Full compatibility with the latest ECMAScript specification
  - Support Node.js applications, including native packages
  - Allow simple upgrading from Nashorn or Rhino based applications
  - Fast interoperability with Java, Scala, or Kotlin, or with other GraalVM languages like Ruby, Python, or R
  - Be embeddable in systems like Oracle RDBMS or MySQL

- The preferred way to run GraalVM JavaScript is from a GraalVM. 
  - If you prefer running it on a stock JVM, please have a look at the documentation in RunOnJDK.md.
  - The core JavaScript engine is a Java application and is thus in principle compatible with every operating system that provides a compatible JVM, see RunOnJDK.md.
  - New features, e.g. ECMAScript proposals scheduled to land in future editions, are added frequently and are accessible behind a flag.
- GraalVM JavaScript can execute Node.js applications. 
  - It provides high compatibility with existing npm packages, 
  - This includes npm packages with native implementations. 
  - Note that some npm modules will require to be re-compiled from source with GraalVM JavaScript if they ship with binaries that have been compiled for Node.js based on V8. 
  - Node.js support is only available in full GraalVM releases, but not in the standalone GraalVM JavaScript distribution.

## discuss

- [如何评价基于GraalVM/Truffle的Graal.js？](https://www.zhihu.com/question/54878770)
  - 打算是用graal.js替换掉openjdk现在里面的nashorn

- [JavaScript on GraalVM](https://dev.to/pmlopes/javascript-on-graalvm-120f)
- discussion
- I am wondering which part make es4x so fast comparing to node.js because as you mentioned in the video that GraalJS run as fast or almost fast as v8.
  - Does the performance gain from replacing libuv or run on GraalVM ?
    - Or it is because you seem to wrap the node.js api by java implementation?
    - I'm really curious about that.
  - There are a couple of things that make it faster. 
    - The usage of netty provides faster IO than libuv, 
    - then vertx implements a different eventloop that uses all computing resources and gives better handling of async tasks, 
    - finally graalvm (in contrast to V8) can optimize the full application (not just the js script), it optimizes netty, vertx and the js code (graaljs + es4x) 
    - so in the end the JIT gives an extra boost to everything and you get that performance. 
    - The cost isn't free, you will see that this has the side effect that only works as expected for long running processes (short cli apps won't benefit from this).
  - ES4X is a new JavaScript runtime that is supposed to replace the official vertx js. 
    - The official vertx js is using nashorn so it only supports ES5.1, it's not high performance and has a development workflow based on java tools such as maven and not npm.
    - The goal is that with version 4 vertx will drop that js runtime and adopt ES4X.
    - This brings to the following question, ES4X is based on vertx, not libuv so express will not work out of the box but writing an API shim could be doable but it's not on my plans atm.
  - Finally regarding the multiple event loops, they never block each other, what is guaranteed is that if a request is started on event loop A then all handlers for that request are handled on event loop A to avoid context switching and improve performance.
- I really doubt that single vertx instance (vertice) is faster than single instance of libuv. 
  - Libuv is written in pure C and talks directly to system kernel (file descriptors). 
    - The main reason that vertx is faster is the multi-reactor pattern. 
    - Most of frameworks based on libuv (node, asyncio) are single threaded. 
    - Vertx can create event loop on each thread by default.
  - You will see that the node implementations are scaling to all cores using the cluster module. 
    - Also others had the same question and also provided a implementation using 0http which claims to be fast, results however show the opposite.

# nashorn

- nashorn /55Star/GPLv2+ClasspathExp/202101/java
  - https://github.com/openjdk/nashorn
  - http://openjdk.java.net/projects/nashorn/
  - Nashorn engine is an open source implementation of the ECMAScript Edition 5.1 Language Specification. 
    - It also implements many new features introduced in ECMAScript 6 including template strings; let, const, and block scope
  - It is written in Java and runs on the Java Virtual Machine.
  - Nashorn used to be part of the JDK until Java 14. 
    - This project provides a standalone version of Nashorn suitable for use with Java 15 and later.
  - Nashorn is licensed under GPL v2 with the Classpath exception, just like the JDK.

- [如何看待 Java11 即将弃用 Nashorn 引擎？](https://www.zhihu.com/question/282928698/answers/updated)
  - 如果不能兼容node，光支持js没有太大意义

# rhino

- rhino /2.8kStar/MPL2/202101/cpp
  - https://github.com/mozilla/rhino
  - https://www.mozilla.org/rhino/
  - Rhino is an open-source implementation of JavaScript written entirely in Java

- [Rhino 和 Nashorn 到底怎么运行？](https://www.zhihu.com/question/27631001)
  - Rhino和Nashorn都是用Java实现的JavaScript引擎。它们自身都是普通的Java程序，运行在JVM上
  - Rhino有解释和编译两种执行模式，可以通过设置Rhino的优化级别（optimization level）来改变。
  - 当优化级别为-1时，Rhino使用一个用Java写的字节码解释器来解释执行JavaScript。
  - 当优化级别为0～9时，Rhino使用一个用Java写的编译器将JavaScript编译为Java字节码
    - 生成出来的Java字节码交由JVM直接执行
  - Sun/Oracle JDK6/OpenJDK6中自带的Rhino是经过裁剪的，去掉了Mozilla Rhino中的部分功能。其中一个被去掉的功能就是Rhino的编译模式。
    - 这意味着JDK6自带的Rhino只能用解释模式运行。
  - 而Oracle JDK7/OpenJDK7放宽了这一限制，当有SecurityManager时只能用解释模式，否则可以配置"rhino.opt.level"系统属性来设置Rhino的优化级别；
    - 默认仍然是用解释模式（优化级别默认为-1）。
  - Nashorn是一个纯编译的JavaScript引擎。
    - 它没有用Java实现的JavaScript解释器，而只有把JavaScript编译为Java字节码再交由JVM执行这一种流程，跟Rhino的编译流程类似。

# ref

- [JavaScript的功能是不是都是靠C或者C++这种编译语言提供的？](https://www.zhihu.com/question/49176184)
  - JavaScript在语言层面并没有暴露任何操作系统层面的功能。它的本意是要嵌在某种宿主环境里，由宿主注入它希望暴露出来的功能。
  - 例如说V8自身并没有读写文件的能力，而Node.js作为一个宿主环境注入操作文件的API给V8，在Node.js里写JavaScript就可以操作文件了。
  - 浏览器是最常见的宿主环境，确实大多数浏览器都是C或者C++实现的，但也有用Java、C#、Rust等语言实现的；
  - 而其它类型的宿主环境也有很多，例如说用Java实现的好几种服务器端环境（Node.jar/Avatar.js、Vert.x/Nodyn）。
