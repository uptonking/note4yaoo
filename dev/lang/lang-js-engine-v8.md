---
title: lang-js-engine-v8
tags: [js, lang, v8]
created: 2021-01-15T08:30:42.368Z
modified: 2021-08-30T06:55:46.491Z
---

# lang-js-engine-v8

# guide

# js-engines
- https://github.com/GoogleChromeLabs/jsvu
  - jsvu makes it easy to install recent versions of various JavaScript engines without having to compile them from source.
  - 支持v8/spidermonkey/jsc/quickjs/graaljs/hermes

- https://github.com/cashapp/zipline
  - Run Kotlin/JS libraries in Kotlin/JVM and Kotlin/Native programs
  - Zipline works by embedding the QuickJS JavaScript engine in your Kotlin/JVM or Kotlin/Native program. It's a small and fast JavaScript engine that's well-suited to embedding in applications.
# v8

# JavaScriptCore

# SpiderMonkey
- docs
  - [SpiderMonkey JavaScript/WebAssembly Engine](https://spidermonkey.dev/)
  - [SpiderMonkey — Firefox Source Docs documentation](https://firefox-source-docs.mozilla.org/js/index.html)

- [Survey - Where are you embedding SpiderMonkey?](https://discourse.mozilla.org/t/survey-where-are-you-embedding-spidermonkey/77988)

- [mongodb: Code-generating Away the Boilerplate in Our Migration Back to Spidermonkey_201604](https://www.mongodb.com/blog/post/code-generating-away-boilerplate-our-migration-back-spidermonkey)
# quickjs
- [如何评价 Fabrice Bellard 发布 QuickJS JS 引擎? - 知乎](https://www.zhihu.com/question/334509855/answers/updated)

- [使用quickjs替换v8的chromium，终于出demo。新鲜出炉山寨版v8 - 知乎_202205](https://zhuanlan.zhihu.com/p/515105585)
  - quickjs毕竟是个没有jit的东西。性能比起v8差太远了。不过quickjs有个独特的优势，就是启动快，而且对于比较小的js代码（并且不包含大量循环之类的），执行的速度不会比v8差多少

- I quite sceptical about such JS AOT projects.
- https://twitter.com/MaxGraey/status/1454793420501835776
  - They are usually only slightly faster than interprts. 
  - QuickJS is not the fastest interpreter btw. 
  - You can also look at GraalJS which has a much more advanced AOT, but it is still sometimes monstrously slow
# blog

## [Roll your own JavaScript runtime using rust](https://deno.com/blog/roll-your-own-javascript-runtime)

- In this post we’ll walk through creating a custom JavaScript runtime. Let’s call it runjs. 
  - Think of it as building a (much) simplified version of deno itself. 
  - A goal of this post is to create a CLI that can execute local JavaScript files, read a file, write a file, remove a file and has simplified console API.

## [认识 V8 引擎](https://zhuanlan.zhihu.com/p/27628685)

- JavaScript本质上是一种解释型语言，与编译型语言不同的是它需要一遍执行一边解析，而编译型语言在执行时已经完成编译，可直接执行，有更快的执行速度。
- JavaScript代码是在浏览器端解析和执行的，如果需要时间太长，会影响用户体验。那么提高JavaScript的解析速度就是当务之急。
- 现在JavaScript引擎的执行过程大致是：
  - 源代码 -→ 抽象语法树 -→ 字节码 -→ JIT -→ 本地代码(V8引擎没有中间字节码)

- V8更加直接的将抽象语法树通过JIT技术转换成本地代码，放弃了在字节码阶段可以进行的一些性能优化，但保证了执行速度
  - 在V8引擎中，源代码先被解析器转变为抽象语法树(AST)，然后使用JIT编译器的全代码生成器从AST直接生成本地可执行代码。
  - 这个过程不同于JAVA先生成字节码或中间表示，减少了AST到字节码的转换时间，提高了代码的执行速度。
  - 但由于缺少了转换为字节码这一中间过程，也就减少了优化代码的机会。
# discuss
- ## 

- ## 

- ## 

- ## [Making JavaScript run fast on WebAssembly | Hacker News](https://news.ycombinator.com/item?id=27370138)

- One reason to use WASM to run JS, even in a browser, is to allow for interruptible execution of untrusted JS code. I built a library for this (1.2mb) that uses Emscripten to build QuickJS to WASM. I know of a company using my library to implement "plugin"/user-scripting using my library.

- Why not just use an embeddded v8 to sandbox untrusted code? I remember some databases used this v8 approach to let users write untrusted db plugins. Any specific advantages using webassembly instead of a v8 instance?
  - You can't use embedded V8 in a browser.
  - v8 is orders of magnitude more complex than QuickJS. There is no “just” available in a browser.
