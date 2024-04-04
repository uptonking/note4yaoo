---
title: lang-java-concurrency
tags: [concurrency, java, lang]
created: 2020-07-07T08:06:49.253Z
modified: 2022-12-19T01:59:01.628Z
---

# lang-java-concurrency

# guide
- [高并发系统设计 40 问 | JAVA 架构师笔记](https://zq99299.github.io/note-architect/hc/)
# race condition 竞态条件

# discuss-stars

- ## 

- ## 

- ## 

- ## [Alternative for synchronisation in multi threading in JAVA - Stack Overflow](https://stackoverflow.com/questions/51219679/alternative-for-synchronisation-in-multi-threading-in-java)
- TL; DR You have overhead no matter what you do - just select the design and primitives that result in the smallest overhead for your particular use case.
- There are lots of ways of doing asynchronous and parallel operations other than using that type of synchronization:
  - Non-blocking I/O
  - Promise/futures based async
  - Event-driven async
  - Using immutable data structures to minimize the amount of shared resources.
  - There are, of course, a lot of types of locking and synchronization mechanisms available other than just the synchronized keywords, such as counting semaphores, reader-writer locks, etc.
  - There are a lot of other types of concurrency as well, such as the actor model.

# discuss-actor-akka/vertx
- ## 

- ## 

- ## [Akka vs Vert.x vs (any other similar platform) : java _201705](https://www.reddit.com/r/java/comments/6dsd4s/akka_vs_vertx_vs_any_other_similar_platform/)
- what do you need the reactivity for? If you want to add reactivity so you can say "reactive machine learning", then go ahead do do it with whatever you feel comfortable with (I'd go with Akka).
  - In pretty much any other case, I'd say there's a reason for ML algorithms/setups not to be reactive: there are better, easier, faster/more efficient alternatives out there for most of the use cases in which you may need a thing or two from reactivity.

- ## 🤔 [is there any way to implement actors model with vertx? _201807](https://github.com/eclipse-vertx/vert.x/issues/2538)
- are you familiar with verticles? You can think of them as actors. And you can use event bus for sending/receiving messages, so actor model is already implemented.

- how to create signleton verticles in cluster mode? My solution is use unique adress to register verticles, is there any better solutions?
  - vertx provides HA verticle deployment, it's explained in the docs
  - vertx HA deployment deploys a singleton on a cluster, please read the docs
- I have read this doc. but i have another question, how to identity the verticle in vertx HA? deployment id?
  - yes, or you can roll your own registry/identifier

- ## [Opinions on vertx : scala _201911](https://www.reddit.com/r/scala/comments/e0j3za/opinions_on_vertx/)
  - I'm curious to hear opinions from the Scala community on vertx (vertx.io). 
  - As a framework, it has a lot of overlap with akka in building reactive systems. Scala is a supported language for using the toolkit, and in books/documentation they do mention akka on more than one occasion. 
  - vertx doesn't implement the actor model (like akka) and doesn't have an actor supervision hierarchy, but in many other ways the two toolkits are very similar.

- In my experience, always prefer libraries over frameworks. Akka, vert.x, etc will drag you in their world and once you have an unconventional problem that they don’t solve directly you’ll end up having a really hard time. Scala is already an incredibly powerful language with a rich library ecosystem.

- It does not really matter how a library/framework/toolkit markets or calls itself. What matters is, who has the control. Is it vertx or is it me?

- Well I experimented about Scala and Vert.x and posted about it a while ago here. I think Vert.x would be a good web server, as long as it remains stateless. Vert.x verticle is well, a poor man Akka Actor. It doesn't work by memory sharing, you will have to technically pass Json between them. Also as some people here brought up, actor is a bit controversial in the way it breaks "statelessness".

- A large part of the community doesn't like akka or frameworks, so I'd think it's unlikely a lot of people would take a serious look a Java framework that attempts to do something similar.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [如果java虚拟线程稳定了，是不是有一大批框架和工具要重写？ - 知乎](https://www.zhihu.com/question/549661510/answers/updated)
- 大部分程序员能写好多线程的阻塞代码就不错了, 用非阻塞异步框架的JVM 程序员可不多（，心疼一秒自虐的 JS 程序员）
- 目前的大部分阻塞多线程相关的模型， 比如 servlet、以及基于 eventpool， reactor 等等，往往是基于同步阻塞多线程的模式， 在web应用下的高频应用， 正好是虚拟线程的主要发力点， 往往是啥都不用改就享受了这波红利，几乎不用重写。
- 至于那些需要高频异步的场景， 无论是 actor， forkjoin ， reactive-stream，本身就是冲着高效利用物理线程， 对并发任务细节进行抽象的异步框架， 他们和虚拟线程是同质化的，迁移到虚拟线程收益不明确。

- ## 可能是暴论，但我认为高性能并发编程最佳选项始终是Go语言的goroutine和channel。
- https://twitter.com/stephenzhang233/status/1762883684456390874
  - 其他高级语言的并发模型难以实现Go那样接近硬件的控制和精细的任务管理。
  - 比如，Java的并发机制虽然增强了线程安全，却带来了复杂的同步控制、庞大的线程管理负担，以及上下文切换的性能开销。

- ## [Java中synchronized锁和Lock锁在CPU层的实现，或者说在JVM层的实现是否是一致的？ - 知乎](https://www.zhihu.com/question/332327455)
  - 一致指的是都是用CAS指令来判断是否可以获取锁，只不过synchronized底层封装了该指令，Lock锁显示调用了该指令并提供了更为灵便的操作方式？

- 不能完全这么说，因为synchronized锁在jdk1.6之后优化为偏向锁，轻量级锁，重量级锁三种形态，CAS的使用是轻量级锁，重量级锁的实现和CAS还不是一回事。
  - Synchronized是通过对象内部的一个叫做监视器锁（monitor，monitor在这个语境下一般翻译成管程）来实现的。但是监视器锁本质又是依赖于底层的操作系统的Mutex Lock来实现的。
  - 而操作系统实现线程之间的切换这就需要从用户态转换到核心态，这个成本非常高，状态之间的转换需要相对比较长的时间，这就是为什么Synchronized效率低的原因。因此，这种依赖于操作系统Mutex Lock所实现的锁我们称之为“重量级锁”。
  - JDK中对Synchronized做的种种优化，其核心都是为了减少这种重量级锁的使用。
  - JDK1.6以后，为了减少获得锁和释放锁所带来的性能消耗，提高性能，引入了“轻量级锁”和“偏向锁”

- synchronized 会被优化为不同级别的锁，其中的重量级锁会切换到内核态

- synchronized是基于JVM中的Monitor锁实现的，Java1.5之前的synchronized锁性能较低，但是从Java1.6开始，对synchronized锁进行了大量的优化，引入可锁粗话、锁消除、偏向锁、轻量级锁、适应性自旋等技术来提升synchronized的性能。
  - synchronized修饰方法时，不需要JVM编译出的字节码完成加锁操作，是一种隐式的实现方式；
  - synchronized修饰代码块时，是通过编译出的字节码生成的monitorenter和monitorexit指令完成的，在字节码层面是一种显示的实现方式；

- 大部分情况下，被添加synchronized锁的代码不会存在多线程竞争的情况，但是会出现同一个线程多次获取同一个synchronized锁的现象，这样很浪费性能，此时偏向锁应运而生

- synchronized是JVM中提供的内置锁，使用内置锁无法很好地完成一些特定场景下的功能。例如，内置锁不支持响应中断、不支持超时、不支持以非阻塞的方式获取锁。
  - 而lock锁是在JDK层面实现的一种比内置锁更灵活的锁，它能弥补synchronized内置锁的不足，他们都通过Java提供的接口来完成加锁和解锁操作。
  - lock是一种显示锁。JDK提供的显示锁位于java.util.concurrent包下，也叫JUC显示锁。

- ## This is a contrived example tailor made to demonstrate the limitations of synchronization with virtual threads, which have been thoroughly documented, including in JEP 444.
- https://twitter.com/gunnarmorling/status/1736137081611583953
  - This is literally the furthest thing from idiomatic synchronized code.
- Yes, it is contrived, but the point is not that much this particular usage, but rather that this is something to be aware of when adopting virtual threads, in particular with 3rd party libs.

- This one is interesting: this program completes with #Java platform threads, but dead-locks with virtual threads. The reason being that virtual threads are pinned (i.e. not releasing their carrier) in synchronized blocks, thus no carriers are available.

- It isn't widely known but you should never use synchronized ever. The pinning problem using virtual threads is a symptom(症状; 征候，征兆) of this and is still being worked on. There is another cause of VT pinning, native stack pointers. This is even more insidious(隐伏的；潜在的).
  - Interesting, why should one never use synchronized? Ignoring virtual threads, it may not be the most flexible means of thread coordination, but it surely works. 

- Never use synchronized ever? That's way overstated. Synchronized should be used judiciously(有见地的；明智的). There's nothing wrong with the idiomatic use of synchronized in the following code. It's much more concise than using j.u.c primitives.

- I'm reading the code on the monitor-support and jom- * branches of loom, and I found that if synchronized is adapted and a custom scheduler API is provided, this problem still exists in the case of mixing platform threads and virtual threads

- Pinning 🧵 to CPU core is the way to go for low latency systems!

- ## [没有vert.x之前java是如何解决高并发问题的？ - 知乎](https://www.zhihu.com/question/316926737/answers/updated)

- 多得很呀，比如跟vert.x不相上下的undertow呀，裸netty呀。。。

- 前端高并发解决方法有
  - 题主说的烧机器。 http无状态，tomcat用线程池（pool几百个thread)可以hold住大量的client（1000个左右），排队呗；系统瓶颈在中间的事务管理器 和后端数据库的设计上。java ee规范已经考虑cluster了，花钱堆机器横向扩展可以解决，应用开发也要符合可扩展的规范
  - 魔改jvm的线程实现，比如 BEA 的旧版本jrockit jvm （jvm1.3之前的时代）使用“green thread”(jvm实现的虚拟机内部使用的thread)，jrockit jvm管理的线程数 比os 调度的native thread要高2到3个数量级
  - 自己按照servlet规范做服务器。比如有魔改tomcat，把session接口用memcached之类的实现

- 新jdk引入 非阻塞IO 和异步调用，设计风格转erlang。 用惯了jvm线程，这些都学不会了。比如网游类型的系统，需要MOBA，服务器端手撕socket和状态机，和tomcat没啥关系了。

- 最开始，根本没有什么高并发问题，联网的东西没几个，select/poll够够的。
  - 后来互联网兴起了，并发蹭蹭涨，活跃么不一直活跃的，poll也不够用了，开始有epoll。
  - 有了epoll，java开始有nio。可惜java官方api太难用，很多坑。先行者踩完坑，就有了netty/mina。现在应该是netty更流行了。
  - 再后来移动互联网了，并发又涨了点，咋办呢，把事件回调那套应用到curd全流程，充分利用cpu。
  - 可是回调太难写了咋办，有了future，reactive，各种m:n协程，vert的类actor也算。
  - 怎么提升呢？持久性内存，rdma, dpdk 等等现在高大上的技术可能变成标配，内核也开始统一为各种io提供统一高性能异步接口。并发范式上还是csp, actor，到看不到什么突破，不过可能被serverless/streaming隐藏起来。

- nio是利用epoll的吗是调用系统的api吗
  - linux上是的，bsd上是kqueue，win上是iocp

- 之后jboss team在red hat慢慢发展出了netty这些东西，进而发展出了vert.x
  - nio即便有了，还有两个东西没有，一个是java 2011 1.7之后弄的nio 2，future来包装callback，其实更为重要的是1.8之后的lambda，没有lambda之前，你要想写一个callback，乖乖，你需要匿名内部类，所以代码会相对难看
  - 还有什么，我想下，哦，对了，nosql

- ## JVM Virtual Thread，同一套 API 能同时在 Platform Thread 和 Virtual Thread 上工作看上去有点科幻，但好像也确实没啥不行
- https://twitter.com/YangKeao/status/1646590131925839872
- 毕竟 jvm 的并发就是 Job - Worker 模型, 并不管 worker 是啥
- 虽然是同一套 API，不要重新学习了，但不同的是 virtual thread 不再需要使用线程池，可以 vthread-per-job/vthread-per-request 了，要把以前用 Platform Thread 中的经验习惯忘记掉

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

- **异步的四种写法**，
  - callback，future，coroutine（await）和fiber，
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
