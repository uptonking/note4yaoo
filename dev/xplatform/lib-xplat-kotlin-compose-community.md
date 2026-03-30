---
title: lib-xplat-kotlin-compose-community
tags: [community, compose, cross-platform, kotlin]
created: 2021-05-13T07:52:19.930Z
modified: 2021-05-13T07:52:46.653Z
---

# lib-xplat-kotlin-compose-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-swift
- ## 

- ## 

- ## 

- ## Swift 6.3 发布，正式支持 Android  _202603
- https://x.com/jaywcjlove/status/2038520042241810496
  - 现在可以用 Swift 构建 Android 应用，还能跨平台共享逻辑。

- 那是用Android Studio还是Xcode开发？
  - Android Studio 和 xcode 都需要安装

- 看了一下预览，感觉安卓那边变成iOS风格了，不像是安卓原生的应用。

- 有的选谁会用swift？底层用native+业务层用前端语言才是未来。

- UI 沒法跨平台的話依舊沒競爭力，只是對 iOS 開發者想雙棲帶來便利性

- Swift 怎么好意思说要支持安卓平台的，一个连模块化都不完整的蹩脚语言，连不同目录文件同名都不允许，成员没有 public private机制，非要用 extension 分隔，这种现代语言中的“怪物”，跨平台 工程化，不如先把自身的反人类非现代特性做到 ts、C#、rust、go一样好用的级别再谈别的
  - kotlin又好到哪里去呢 更别提那个android studio了…. 那个gradle更是重量级 如果说语言是设计问题 有点难改，gradle是为何 ai时代 不必太纠结语言问题，生态才是关键 很显然 安卓这边差苹果太远了（体验）
- 怎么被你说的这么不堪，你确认成员没有public private机制么

- 好像不是Apple官方搞的哈。Skip是什么来头？
- 这个skip没出swift 6.3之前也能用吧
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 💡 Jetpack Compose was essentially a Kotlin clone of Flutter, literally to the point of translating large chunks of code.
- https://twitter.com/timsneath/status/1727853284684386404
  - That all happened, and set a bar that others had to invest heavily to compete with. 

- https://twitter.com/JimSproch/status/1728081821114466785
  - It's true. If you look hard enough, you'll still find some ktdocs that were copy-pasted from flutter. That said, we also made many different design choices, like our usage of an optimizing compiler, and positional memoization, and widgets as functions.

- ## Compose for iOS is officially in Alpha!_202304
- https://twitter.com/JimSproch/status/1646488217519288321
- Does it render natively on iOS also?
  - Yes, it is entirely native on iOS.

- ## 如何看待Kotlin 桌面 UI Jetpack Compose for Desktop？
- https://www.zhihu.com/question/430328747/answers/updated
- JetBrains在Kotlin生态的推进上，经常东一榔头西一棒子。Kotlin for JVM, Javascript, Native 四面开花，很多开源项目做个demo或alpha版，就渐渐搁置了。
  - compose-jb 还是 Kotlin/JVM + JNI Skia C++，感觉跟JavaFX的角色相同。IntelliJ IDEA 自身的UI绘制渲染实现是用JavaFX？还是Swing？（我不了解）
  - 所以我等着看JetBrains先在自家核心产品中使用的效果。

- ## flutter为什么不使用kotlin作为开发语言？
- https://www.zhihu.com/question/378389226/answers/updated
- dartvm在设计时候就没想过做成一个通用的虚拟机
  - 这个跟jvm不一样，jvm从一开始就设计成兼容性比较强的虚拟机，所以jvm上有很多语言，甚至还有脚本引擎，dartvm那个更像是一个语言引擎
  - 安卓的dalvik就是hotspot改嘛，所以兼容kotlin简单，dartvm就要困难许多，一开始就没这么设计，谷歌也没空去做那个兼容

- [Dart: Why Not a Bytecode VM?](https://fartlang.org/articles/dart-vm/why-not-bytecode.html)
  - The biggest advantage of a bytecode VM is that it is not restricted to one input language. (JVM)
  - Scala and F# show that a new language can be developed for an existing VM, 
  - but it’s possible to do that without bytecode: you can compile to source. (like CoffeeScript)
  - [Inaccuracies in "bytecode VM" article](https://groups.google.com/a/dartlang.org/g/misc/c/u_jk0906sYg)
  - [Why not a bytecode VM in the browser?](https://www.reddit.com/r/programming/comments/nkkcm/why_not_a_bytecode_vm_in_the_browser/)
