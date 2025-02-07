---
title: lang-java-extensions
tags: [engineering, extensions, java, lang]
created: 2020-12-14T13:18:38.355Z
modified: 2021-01-04T15:51:00.214Z
---

# lang-java-extensions

# debug-test

# compiler-babel-like
- [TeaVM](https://github.com/konsoletyper/teavm) 
  - /Apache2
  - Compiler of Java bytecode to JavaScript
  - TeaVM is an ahead-of-time compiler for Java bytecode that emits JavaScript and WebAssembly that runs in a browser.
    - Its close relative is the well-known GWT. 
    - The main difference is that TeaVM does not require source code, only compiled class files.
    - TeaVM successfully compiles Kotlin and Scala.

- [Retrolambda](https://github.com/luontola/retrolambda)
  - Backport of Java 8's lambda expressions to Java 7, 6 and 5
# discuss-osgi/module
- ## 

- ## 

- ## [为什么我感觉java的模块化很鸡肋？ - 知乎](https://www.zhihu.com/question/608644195)
- 如果类的访问修饰符不是public的，则意味着这个类只被在它所在的包访问，项目中其他包也想访问怎么办？
  - Java 9 的模块化，在很大程度上可以解决这个问题，类的访问边界不但有包内和包外的区别，还增加了模块内和模块外的区别。
- 然而Java每个项目只能有一个模块，必须放在项目更目录下。这也是他鸡肋的地方，和Maven等包管理工具定位重叠了。哪怕一个Maven项目里可以创建多个Java module，那都有他存在的价值。而且模块外也可以通过加编译选项访问到模块内的东西，隔离了个寂寞

- 模块化服务的主要是类库（尤其是标准库），你开发应用的话那当然不怎么用得上。
  - 在 Java 9 之前没有模块系统的时代，Java 控制访问权限的唯一方式就是 public/private 这些关键字，对于各种库里在某个叫 internal/impl 包中的实现类是没办法保护的，而 private 的保护也可以通过反射轻易绕过。

- 阿里还折腾了两年后来转微服务了
  - 都微服务了，还搞什么module。
