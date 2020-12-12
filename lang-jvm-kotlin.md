---
title: lang-jvm-kotlin
tags: [kotlin, lang]
created: '2019-09-07T04:07:36.964Z'
modified: '2020-12-08T13:20:20.680Z'
---

# lang-jvm-kotlin

## basis

- Kotlin是在Java虚拟机（JVM）上运行的静态类型编程语言。
  - 它的开发始于2010年的JetBrains，但是直到2016年，才发布了第一个稳定版本（Kotlin v1.0）
  - JetBrains的负责人Dmitry Jemerov表示Scala接近但编译速度较慢。
- Kotlin旨在像Java一样快地进行编译，但是比Java具有更简洁，更实用的语法

## kotlin-extensions

- Kotlin还可以编译为JavaScript，并且可以创建在启用了JavaScript的浏览器中运行的应用程序。
  - 可以直接在Intellij IDEA中编写JavaScript代码，然后使用Maven或使用命令行进行编译。
  - Kotlinx.html是Kotlin模板引擎，用于在Web应用程序中构建HTML。
  - 可用于Node.js的服务器端编码

- [如何评价 Kotlin Native?](https://www.zhihu.com/question/58044077/answers/updated)
  - kotlin野心很大啊， 底层直通C， 中间层vm，高层脚本。

## kotlin vs java

- [Kotlin会取代java吗？](https://www.zhihu.com/question/299244850/answers/updated)
  - Kotlin编译是在JVM之上执行的字节码，因此Java是运行Kotlin所必需的。
    - Kotlin的大火，来源于Google的官方支持！
    - 对于Java后端来说，基本不会用Kotlin ，因为Java的生态太好了
  - 取代不了，大量的开源jar都是java的，你学了kotlin还要学java
    - 不用这些jar包，开始相当于重头再来，成本非常高。
    - 用这些jar包要看他们的源码，实例什么的，还是要学java。
    - 除非kotlin重新开发一个虚拟机并超过java的jre，否则难，大量的历史代码都是建立在Java上，有大量的历史代码需要维护，java几十年的积累不是白积累的。
    - java刚出来时说要取代c++，结果现在2020年了,c++还是活得好好的，c++累积的大量代码同样不是java能解决的。
    - 搞n多新语言不见得是好事，很多只是语法糖，编译糖，并无实质性创新，未来还是前几种语言垄断。
  - kotlin有个巨大的坑是无法回避的，那就是如果你是公司的库开发者，你的库会被别人调用，那么你就不能用kotlin写库的接口。
    - kotlin调java是无缝的，但是java调kotlin不是无痕的，
    - 在java端，是可以点出kotlin代码结构的。
    - 但作为一个代码洁癖，我又极不情愿用jvm注解，这就导致了所有的类在Java端都会有个Kt尾巴，这是无法忍受的。

- [Kotlin 作为 Android 开发语言相比传统 Java 有什么优势？](https://www.zhihu.com/question/37288009/answers/updated)
  - Google在2019年已经确立了Kotlin在Android开发中的官方地位
  - Android到2020年了还没有彻底支持Java8, 而kotlin支持全系Android

## ref

- [谈编程语言互操作-Java/Kotlin互操作机制](https://zhuanlan.zhihu.com/p/299669161)
  - kotlin语言可以被编译成多种形态，如kotlin-native, kotlin-jvm, kotlin-js
  - Java/Kotlin互操作完全依赖kotlinc编译器产生javac可以识别的统一的字节码*.class文件
  - 尽管Kotlin语言引入了大量简化编程的高级语法（语法糖），最终都会被转为字节码文件，javac可以识别对应的字节码文件，实现编译层面的互相调用
