---
title: lang-java-community-async
tags: [async, community, java]
created: 2023-08-28T04:41:20.957Z
modified: 2023-08-28T04:41:34.026Z
---

# lang-java-community-async

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Java 8 CompletableFuture 对比 ES6 Promise - 知乎](https://zhuanlan.zhihu.com/p/404601346)
- Java 8 中新增了和 ES6 的 Promise 类似的对象： java.util.concurrent. CompletableFuture 。

- JCU中的Future需要轮询，而netty中提供了更好的Promise相关类。
  - Java其实也支持回调的。不过需要继承FutureTask类，在子类的done方法中写结果处理逻辑。
- netty扩展了jdk的future接口，允许添加监听器。同时Promise接口继承自future接口，拥有设置返回值和异常信息功能，并在设置完成后调用监听器并唤醒阻塞线程。
