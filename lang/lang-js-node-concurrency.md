---
title: lang-js-node-concurrency
tags: [concurrent, js, lang, node]
created: 2021-08-30T06:41:24.479Z
modified: 2021-08-30T06:41:48.713Z
---

# lang-js-node-concurrency

# discuss

- ## 

- ## 

- ## [既然 Node.js 是单线程，又是怎么做到支持异步函数调用的？ - 知乎](https://www.zhihu.com/question/19914053)
- nodejs js执行代码是单线程
  - 但是他的宿主环境是多线程，libuv分配线程池
  - nodejs使用事件驱动，从libuv中获取结果，并且加入主线程
- 除了你的代码是单线程，其余都是多线程（线程池），nodejs本身是事件驱动，一个io事件完成会被放到一个事件队列中，
  - 主线程负责轮训这个队列，然后执行相应的回调函数。
- 在node.js里面只有你写的代码是单线程的，其内部并不是单线程的，只是它实现了这个机制，让用户写的代码都是单线程的。
- 单线程指的是主线程是“单线程”的，所有阻塞的部分交给一个线程池处理，然后这个主线程通过一个队列跟线程池协作，于是对我们写到的js代码部分，不再关心线程问题，代码也主要由一堆callback回调构成，然后主线程在不停的循环过程中，适时调用这些代码。

- [node.js - 既然nodejs是单线程的，那么它怎么处理并发，难道要排队么 - SegmentFault 思否](https://segmentfault.com/q/1010000000190024)

- [Node.js内部是不是多线程？ - 知乎](https://www.zhihu.com/question/22295607)
- Node.js 的 Event Loop 是单线程的，也就是说，执行你的程序逻辑的时候是单线程。
  - 但是 Node.js 处理 IO 和网络事件的 libuv 库却是多线程的。libuv 有自己的线程池管理。

- [nodeJs的多线程和一般erlang, java, c++等后端语言的区别? - 知乎](https://www.zhihu.com/question/551224239)
- Node.js的cluster是用来做负载均衡的，跟多线程没有任何关系，它实际上是启动多个node进程，每个进程之间相互隔离，从而可能达到更高的QPS，以及确实的集群稳定性。
- 至于多线程，有两种模型，一种是基于共享内存的多线程模型，一种是基于消息队列的多线程模型。
  - 像java这种，它是通过创建多个线程来分别执行你的java代码，从而实现并发，但是多个线程却会共享同一份内存数据，这也就导致java多线程在使用时需要特别注意脏数据的问题，要加各种读写锁。
  - 而像nodejs，它也可以并发，但是它不是创建多个线程去执行你的js代码，而是创建多个IO任务到事件循环的队列里，然后node会自动帮你创建多个线程分别处理这些IO任务，当这些任务完毕后，再通知你去执行相应的回调函数。但不管是那些普通的js代码，还是这些IO任务的回调函数，它们都是js代码，都是在唯一的一个主线程中执行的，也就不会有脏数据的问题。
  - 所以，java对并发有更好的编程性，你可以直接编写要并发执行的java代码。而nodejs有更简单的并发模型，你不需要亲自编写并发代码，不需要关注共享内存问题，只需要发起IO任务，并在主线程里接收IO任务完成的消息(回调)就行了。
- child_process是创建进程，不存在共享内存问题

- ## [理解Node.js中的"多线程" - 知乎](https://zhuanlan.zhihu.com/p/74879045)
- Node.js 通过提供 cluster、child_process API 创建子进程的方式来赋予Node.js “多线程”能力。
  - 但是这种创建进程的方式会牺牲共享内存，并且数据通信必须通过json进行传输。（有一定的局限性和性能问题）
- 基于此 Node.js V10.5.0 提供了 worker_threads，它比 child_process 或 cluster更轻量级。 
  - 与child_process 或 cluster 不同，worker_threads 可以共享内存，通过传输 ArrayBuffer 实例或共享 SharedArrayBuffer 实例来实现。
- Node.js 并没有其它支持多线的程语言（如：java），诸如"synchronized"之类的关键字来实现线程同步的概念。Node.js的 worker_threads 区别于它们的多线程。如果添加线程，语言本身的性质将发生变化，所以不能将线程作为一组新的可用类或函数添加。

- ## child_process 是用于创建子进程和父子进程通信的，有4个 api： spawn、exec、execFile、fork
- https://www.zhihu.com/pin/1413231233476685824
- spawn 是用 shell 来跑一段命令，返回一个 stream
- exec 基于 spawn，只是对返回的 stream 做了封装，直接可以拿到 buffer，只不过有上限，可以用  maxBuffer 设置
- execFile 没有跑 shell 环境，可以执行可执行文件，当然也可以跑 shell
- fork 则是用于执行 js 文件的
  - cluster 的 fork 是创建多个子进程以及通信的，会执行到分叉的地方
- 而关于通信：cp 的 api 都支持管道的 pipe，而所有的进程创建方式都支持事件的方式，底层是消息队列
