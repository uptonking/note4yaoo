---
title: lang-java-concurrency
tags: [concurrency, java, lang]
created: 2020-07-07T08:06:49.253Z
modified: 2022-12-19T01:59:01.628Z
---

# lang-java-concurrency

# pieces

# race condition 竞态条件

# discuss

- ## 

- ## 

- ## 

- ## [为什么Java坚持多线程不选择协程？](https://www.zhihu.com/question/332042250)
- 先说结论：协程是非常值得学习的概念，它是多任务编程的未来。但是Java全力推进这个事情的动力并不大。
- 可以直接改用netty去处理这类问题。你可以理解为NIO + woker thread大致就是一套“协程”，只不过没有实现在语法层面，写起来不优雅而已。
- 再说创建/销毁线程的开销。这个问题在Java里通过线程池得到了很好的解决。
  - 你会发现即便你用vert.x或者kotlin的协程，归根到底也是要靠线程池工作的。
  - goroutine相当于设置一个全局的“线程池”，GOMAXPROCS就是线程池的最大数量；
  - 而Java可以自由设置多个不同的线程池（比如处理请求一套，异步任务另外一套等）。
  - kotlin利用这个机制来构建多个不同的协程scope。这看起来似乎会更灵活一点。
- 线程的切换开销。线程的切换实际上只会发生在那些“活跃”的线程上。
  - 对于类似于Web的场景，大量的线程实际上因为IO（发请求/读DB）而挂起，根本不会参与OS的线程切换。
  - 现实当中一个最大200线程的服务器可能同一时刻的“活跃线程”总数只有数十而已。其开销没有想象的那么大。
  - 为了避免过大的线程切换开销，真正要防范的是同时有大量“活跃线程”。
- 此外说说与NIO的配合。在Java这个生态里Java NIO/Netty/Vert. X/rxJava/Akka可以任意选择。
  - 一般来讲，Netty可以解决绝大部分因为IO的等待造成资源浪费的问题。
  - Vert. X/rxJava可以让程序写的更加“优雅”一点（见仁见智）。
  - Akka就是Java世界里对“原教旨OO“的实现，很有特色。
  - 的确，用NIO + completedFuture/handler/lambda不如async+await写起来舒服，但起码是可以干活的。
- 如果真的要较真Java的NIO用于业务的问题，其核心痛点应该是JDBC。
  - 这是个诞生了几十年的，必须使用Blocking IO的DB交互协议。其上承载了Java庞大的生态和业务逻辑。
  - Java要改自己的编程方式，必须得重新设计和实现JDBC，就像vert-x3/vertx-mysql-postgresql-client 那样做。
  - 问题是，社区里这种“异步JDBC”还没有支持oracle、sql server等传统DB。对mysql和postgres的支持还需要继续趟坑～
- 如果认真阅读上面这些需要“协程”解决的问题，就会发现基本上都可以以各种方式解决。
  - 觉得线程耗资源，可以控制线程总数，可以减少线程stack的大小，可以用线程池配置max和min idle等等。
  - 想要go的channel，可以上disruptor。
- 可以说，Java这个生态里尽管没有“协程”这个第一级别的概念，但是要解决问题的工具并不缺。
  - Java仅仅是没有解决”协程“在Java中的定义，以及“写得优雅“这个问题。
- 其他新的语言历史包袱少，比较容易重新思考“什么是现代的multi-task编程的方式“这个大主题。
  - kotlin的协程、go的goroutine、javascript的async await、python的asyncio、swift的GCD都给了各自的答案。
- 最后说一句，多线程容易出bug主要因为：
  - “抢占式”的线程切换 —— 你无法确定两个线程访问数据的顺序，一切都很随机
  - “同步”不可组装 —— 同步的代码组装起来也不同步，必须加个更大的同步块
- 协程能不能避免容易出bug的缺陷，主要看能不能避免上面两个问题。
  - 如果协程底层用的还是线程池，两个协程还是通过共享内存通讯，那么多线程该出什么bug，多协程照样出。
  - javascript里不出这种bug是因为其用户线程就一个，不会出现线程切换，也不用同步；
  - go是建议用channel做goroutine的通讯。如果go routine不用channel，而是用共享变量，并且没有用Sync包控制一下，还是会出bug。

- 基本上java的技术栈都是基于线程提供出来的，servlet，jdbc，jms底层都是封装了线程提供出来，做web开发的90%的时间不需要考虑线程的问题
  - 应该说都是j2ee的东西，j2ee自己都凉了，从长远看这些东西会慢慢变成legacy code&system

- 异步的四种写法，callback，future，coroutine（await）和fiber，
  - fiber是完全模拟线程，所以thread local可以变成fiber local，@Trasactional并不需要改动一样能用，
  - 但是本质上说，如果短连接的一问一答式的流程没有变，异步开发和同步开发不会有太大差异也是真的，所以还是思维和需求要摆脱出http那种一问一答式的企业级开发应用的小天地才是王道
  - 最后go应该是走错路了，上面说的四种方式，其实go只用了一种，强行替用户做了选择，所以吸引了大量脚本程序员进入这个语言，
  - 但其实kotlin是一个好的开始，java的loom实际上是在学习kotlin，而kotlin的coroutine在正式发布之后，也变得跟java将来的loom很接近了

- 同意，核心就是CPU和内存没人工值钱。
- 在Java类库极大丰富的今天，能解决异步编程复杂的手段非常多，协程可能是最后才会被想起的手段。所以大家对协程的诉求并没有那么高。

- 协程改善了并发代码的书写问题，但在共享内存这个大前提下，线程安全的问题绕不过去的。

- tomcat上的worker线程池的最大线程数一般会配置为50～500之间，为什么不配多一点呢
  - 因为配多了，在内存瓶颈达到之前会先遇到IO瓶颈。那时候你要优先处理的更可能是优化cache和分库分表。
  - IO瓶颈就是指的数据库IO吧
  - 也不一定，比如调用底层服务接口。但web这个业务的特性决定了大部分压力最终会落到存储上。
  - io有很多，像网络通信也是io的一种，内网的分布式系统，像分布式文件存储，像数据库，像内存计算，像消息队列，像缓存，不在同进程中获取外部资源都是io。现在硬盘速度太慢了，导致io特别卡。

- ## [Why event loop uses more than one thread?](https://stackoverflow.com/questions/54133054)
- usual multi-threaded server spends a thread per connection. 
  - This sets a natural limit about 10000 simultaneous connections. 
  - Netty is asynchronous and can keep much more. 