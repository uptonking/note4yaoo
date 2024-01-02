---
title: lang-js-webpack-rewrite
tags: [rewrite, toolchain, webpack]
created: 2023-12-25T19:26:52.486Z
modified: 2024-01-02T07:53:06.355Z
---

# lang-js-webpack-rewrite

# guide

# blogs-webpack-internals
- [手写一个webpack，看看AST怎么用](https://juejin.cn/post/6930877602840182791)
  - webpack最基本的功能其实是将JS的高级模块化语句，import和require之类的转换为浏览器能认识的普通函数调用语句。
  - 要进行语言代码的转换，我们需要对代码进行解析。常用的解析手段是AST，也就是将代码转换为抽象语法树。
  - AST是一个描述代码结构的树形数据结构，代码可以转换为AST，AST也可以转换为代码。
  - babel可以将代码转换为AST，但是webpack官方并没有使用babel，而是基于acorn自己实现了一个JavascriptParser。

- [webpack核心模块tapable源码解析 - 掘金](https://juejin.cn/post/6946094725703139358)
  - tapable的源码的抽象程度比较高，直接扎进去反而会让人云里雾里的，所以本文会从最简单的SyncHook和发布订阅模式入手
  - tapable的各种Hook其实都是基于发布订阅模式。

- [webpack核心模块tapable用法解析 - 掘金](https://juejin.cn/post/6939794845053485093)
  - webpack plugin高度依赖tapable这个库
  - tapable并没有具体的业务逻辑，是一个专门用来实现事件订阅或者他自己称为hook(钩子)的工具库，其根本原理还是发布订阅模式，但是他实现了多种形式的发布订阅模式，还包含了多种形式的流程控制。
  - 这些Hook主要有同步(Sync)和异步(Async)两种，同时还提供了阻断(Bail)，瀑布(Waterfall)，循环(Loop)等流程控制，对于异步流程还提供了并行(Parallel)和串行(Series)两种控制方式。
  - tapable其核心原理还是事件的发布订阅模式，他使用tap来注册事件，使用call来触发事件。
# more
