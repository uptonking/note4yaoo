---
title: job-cs-pattern-design
tags: [cs, design-pattern, job]
created: 2021-09-23T18:31:09.718Z
modified: 2021-09-23T18:31:42.015Z
---

# job-cs-pattern-design

# guide

- 6大原则
  - 开放封闭原则
  - 单一职责原则
  - 接口隔离原则
  - 迪米特法则（也称为最小知识原则）
  - 依赖反转原则
  - 里氏代换原则

- 框架中常用的设计模式
- 创建型 5
  - 工厂方法
  - 抽象工厂
  - 建造者
  - 原型模式
  - 单例模式
- 结构型 7
  - 适配器
  - 装饰器
  - 桥接
  - 组合
  - 门面/外观
  - 代理模式
  - 享元
- 行为型 12
  - 发布订阅、观察者
  - 迭代器 Symbol.iterator
  - 访问者
  - 中介者
  - 策略模式
  - 模版方法
  - 命令模式
  - 状态模式
  - 职责链
  - 解释器
  - 备忘录

- 框架中常用的数据结构
  - tree树: dom树、js生成ast、react vdom树
  - stack栈: JS执行栈、react stack reconciler
  - queue队列: 异步任务队列
  - 哈希表: vue diff算法key作用
  - 图: GC标记清除算法在标记过程中维护可达图、webpack在编译过程中维护可达图

- resources
  - [JavaScript设计模式与开发实践 | 汪图南](https://wangtunan.github.io/blog/designPattern/)
  - [JavaScript设计模式es6（23种) - 掘金](https://juejin.cn/post/6844904032826294286)
  - [JavaScript中常见的十五种设计模式 - -渔人码头- - 博客园](https://www.cnblogs.com/imwtr/p/9451129.html)
  - [Hooks Pattern](https://www.patterns.dev/posts/hooks-pattern)
  - [JavaScript 设计模式](https://www.freecodecamp.org/chinese/news/javascript-design-patterns-explained/)
    - [JavaScript Design Patterns – Explained with Examples](https://www.freecodecamp.org/news/javascript-design-patterns-explained/)
# 创建型

## 建造者

- usecase
  - redux createReducer ActionReducerMapBuilder

- Use the Builder pattern to clean up code in situations where you have a constructor with too many parameters.

- 通过定义一个类来简化复杂对象的创建，该类的目的是构建另一个类的实例。
  - 构建器模式还允许实现Fluent接口。

- [Java 解决构造方法参数过多-builder模式（effect java 学习笔记2） - 掘金](https://juejin.cn/post/6844903917365493768)
  - builder 对构造方法的一个微小的优势是，builder 可以有多个可变参数，因为每个参数都是在它自己的方法中指 定的

## 原型模式

- 使得类的实例能够生成自身的拷贝。
  - 如果创建一个对象的实例非常复杂且耗时时，就可以使用这种模式，而不重新创建一个新的实例，你可以拷贝一个对象并直接修改它。

## 单例模式

- usecase
  - 全局缓存
  - 线程池
  - 浏览器中的window对象
  - 网页登录浮窗

- 用来确保类只有一个实例。Joshua Bloch在Effective Java中建议到，还有一种方法就是使用枚举。
# 结构型

## 适配器

- usecase
  - redux-persist
  - remotestorage.js
  - LokiDB
  - react-admin DataProvider
  - tanstack adapter for frameworks
  - more
    - localForage,StreamSaver.js
    - 整合多个第三方SDK的任务就交由适配器来做

- Adapter，将一个类（对象）的接口（方法或者属性）转化为另一个接口，以满足用户需求，使类（对象）之间接口的不兼容问题通过适配器得以解决

- 适配数据源的时候，比如有些场景，既要适配mysql数据源，又要适配oracle数据源，也是适配器模式； 
- 在我们业务代码中经常有新旧接口适配需求，可以采用该模式。

- [适配器模式 - 知食记](https://mind.ricky.moe/other/she-ji-mo-shi-1/kuo-pei-qi-mo-shi)
- [适配器在JavaScript中的体现 - 掘金](https://juejin.cn/post/6844903683210084366)

## 装饰器

- 动态的给一个对象附加额外的功能，因此它也是子类化的一种替代方法。
- 我们常用的AOP，既有动态代理，也有装饰者的味道。

## 组合模式

- 让客户端看起来在处理单个对象和对象的组合是平等的，换句话说，某个类型的方法同时也接受自身类型作为参数。（So in other words methods on a type accepting the same type）
- 凡是有级联操作的，你都可以尝试这个设计模式。

## 桥接

- 其实我们每天都在用到，但是你可能却浑然不知。只要你用到面向接口编程，其实都是在用桥接模式。

## 门面/外观

- 为一组组件，接口，抽象或子系统提供简化的接口。
- 我们每天使用的SLFJ日志就是门面日志，比如我们使用Dubbo，向外提供的服务就尽量采用门面模式，然后服务在调用各种service做聚合。

## 享元

- 使用缓存来减少对小对象的访问时间
- 只要用到了缓存，基本都是在使用享元模式。很多同学都说自己的项目太low了，都没有用到什么设计模式，这不是开玩笑吗，你用个map缓存几个对象，基本上都运用了享元的思想。

## 代理

- usecase
  - vue 3
# 行为型

## 发布订阅模式

- usecase
  - redux
  - vue2.x依赖收集与通知
  - nodejs eventemitter

- 意义：在软件架构中，发布订阅是一种消息范式，消息的发送者（称为发布者）不会将消息直接发送给特定的接收者（称为订阅者）。而是将发布的消息分为不同的类别，无需了解哪些订阅者可能存在。同样的，订阅者可以表达对一个或多个类别的兴趣，只接收感兴趣的消息，无需了解哪些发布者存在

- [发布-订阅模式 - 知食记](https://mind.ricky.moe/other/she-ji-mo-shi-1/guan-cha-zhe-mo-shi)
- [观察者模式 - 知食记](https://mind.ricky.moe/other/she-ji-mo-shi-1/guan-cha-zhe-mo-shi-1)
- [观察者模式与发布-订阅模式的区别是什么？ - 知食记](https://mind.ricky.moe/other/she-ji-mo-shi-1/guan-cha-zhe-mo-shi-yu-fa-bu-ding-yue-mo-shi-de-qu-bie-shi-shen-me)
  - 区别在于是否存在第三方、发布者能否直接感知订阅者
  - 发布-订阅模式下，实现了完全地解耦。

### 观察者模式

- usecase
  - DOM模型可以视为观察者模式，DOM元素作为被观察者，事件处理程序作为观察者，当事件发生时，这种变化会被观察者捕获到，做出响应反应。

- 意义：一个被称作被观察者的对象，维护一组被称为观察者的对象，这些对象依赖于被观察者，被观察者自动将自身的状态的任何变化直接通知给它们

## 中介者

- 通过使用一个中间对象来进行消息分发以及减少类之间的直接依赖。
  - 业务代码使用的场景太多了。比如你们用MQ，其实就是在用中介者模式

## 访问者

- 提供一个方便的可维护的方式来操作一组对象。它使得你在不改变操作的对象前提下，可以修改或者扩展对象的行为。

## 策略模式

- 定义一系列算法，把他们一个一个封装起来，并且使他们可以相互替换。

- 常用于优化大量的if-else

## 模版方法

- 让子类可以重写方法的一部分，而不是整个重写，你可以控制子类需要重写那些操作。

## 命令模式

- 将命令包装在对象中，以便可以将其存储，传递到方法中，并像任何其他对象一样返回。

## 状态模式

- 允许您在运行时根据内部状态轻松更改对象的行为。

## 职责链

- 通过把请求从一个对象传递到链条中下一个对象的方式来解除对象之间的耦合，直到请求被处理完毕。
  - 链中的对象是同一接口或抽象类的不同实现。
- 凡是带有Filter关键词的，基本都在用这个设计模式。
  - 在业务代码使用的场景实在是太多了，用到拦截器的地方基本都在用这个设计模式。

## 解释器

- 为该语言定义语法并使用该语法来解释该格式的语句。

## 备忘录

- 生成对象状态的一个快照，以便对象可以恢复原始状态而不用暴露自身的内容。
  - 比如Date对象通过自身内部的一个long值来实现备忘录模式。

- 一种场景是，你要把数据丢到MQ，但是MQ暂时不可用，那么你把数据暂存到DB，后面再轮询丢到MQ。
# more
- [24种设计模式的通俗理解](https://www.cnblogs.com/shoshana-kong/p/10787629.html)
