---
title: lib-xplat-kotlin-compose-community
tags: [community, compose, cross-platform, kotlin]
created: 2021-05-13T07:52:19.930Z
modified: 2021-05-13T07:52:46.653Z
---

# lib-xplat-kotlin-compose-community

# discuss

- ## 

- ## 

- ## 

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
