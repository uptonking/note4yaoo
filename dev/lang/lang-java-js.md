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
# graaljs
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
# nashorn (jdk 8-10)
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
# rhino (jdk 6-7)
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
# discuss
- ## 

- ## 

- ## 

- ## [Javascript异步任务(如promise)操作全局变量是否需要加锁？ - 知乎](https://www.zhihu.com/question/523481325)

- 通常不需要，因为js里 worker(和线程宏观上差不多)和主线程之间的数据是structured clone 基本上都是副本（现在node的structuredClone貌似能clone不外泄的循环引用了，但是依然是副本）。
  - 但是有些个别例外，像 贺老 说的 使用share dArrayBuffer (不过sharedArrayBuffer比较原始，需要自己写数据结构化/反结构化，用的并不多，多任务一起解帧时候会用到，其他地方用的不多见)。这时候有写/修改操作的话，是有可能需要加锁的。
  - js 里atomic就类似锁机制，比较傻瓜，API已经给你做好了。
  - promise其实也能当“锁”用来占住共享资源的写权限，比如一个任务await, 另一个任务操作 resolve 和reject。await 的语意有点像acquire, 而fullfill就像release.

- Promise是個垃圾。沒有取消，沒有continue

- 锁一般只在多线程情况下才需要引入的，由于Javascript是单线程的，原则上是不需要常规意义上的锁的，因为根本不存在会有多条指令会同时访问同一个全局变量的这种情况的，因此就不需要有锁的概念。
  - 但是在应用层面会有时会需要对某个全局变量进行管理，避免不同函数访问和修改而导致全局变量的不可预测，这种不可预测是应用层面的，而不是常规意义的锁。
- 为解决应用层的全局变量的可预测，本质上就是一个竞态问题，是设计模式的问题，解决这些问题可以有两个方式：
  - 引入类似Redux/Vuex这类的状态管理，不是直接定义全局变量，而是将全局变量定义在Store里面，然后通过Redux/Vuex约定的方式按可预测的方式来修改全局变量。本实质上是Flux设计模式的实现。
  - 还有一个方式引入一些有限状态机，通过有限状态机来统筹应用的状态切换，确保对全局变量的修改在可预测的范围内进行，避免一些不可预测的状态修改。

- JS除了SharedArrayBuffer类型的对象之外没有可以多线程访问的对象。
  - 对SharedArrayBuffer对象的访问默认是 Unordered ，如果需要更强的内存序，要使用 Atomic（保证Sequential Consistent）。

- JavaScript的异步编步机制
  - 自定义任务队列（Task Queue）
  - 宏任务和微任务
  - requestAnimationFrame由系统来决定回调函数的执行时机。视浏览器的实现而定，但一般来说，它在宏任务执行完，渲染之前，这使得其可以获取到最新的布局和样式信息
  - Promise
  - 

- ## [JavaScript的功能是不是都是靠C或者C++这种编译语言提供的？](https://www.zhihu.com/question/49176184)
- JavaScript在语言层面并没有暴露任何操作系统层面的功能。它的本意是要嵌在某种宿主环境里，由宿主注入它希望暴露出来的功能。
  - 例如说V8自身并没有读写文件的能力，而Node.js作为一个宿主环境注入操作文件的API给V8，在Node.js里写JavaScript就可以操作文件了。
  - 浏览器是最常见的宿主环境，确实大多数浏览器都是C或者C++实现的，但也有用Java、C#、Rust等语言实现的；
  - 而其它类型的宿主环境也有很多，例如说用Java实现的好几种服务器端环境（Node.jar/Avatar.js、Vert.x/Nodyn）。
