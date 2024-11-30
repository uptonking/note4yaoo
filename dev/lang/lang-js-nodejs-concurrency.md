---
title: lang-js-nodejs-concurrency
tags: [concurrency, js, lang, nodejs]
created: 2021-08-30T06:41:24.479Z
modified: 2022-12-19T01:59:01.625Z
---

# lang-js-nodejs-concurrency

# guide

- [说说Nodejs高并发的原理 event-loop](https://zhuanlan.zhihu.com/p/591164293)
# 多线程
- Node.js保持了JavaScript在浏览器中单线程的特点
  - 它的优势是没有线程间数据同步的性能消耗也不会出现死锁的情况
  - 所以它是线程安全并且性能高效的
- 单线程有它的弱点，无法充分利用多核CPU资源，CPU密集型计算可能会导致I/O阻塞，以及出现错误可能会导致应用崩溃。
- 为了解决单线程的缺点，现在提出了很多解决方案
- 浏览器端： HTML5制定了Web Worker标准
  - Web Worker的作用就是为JavaScript创造多线程环境，允许主线程创建Worker线程，将一些任务分配给后者运行 
- Node端：采用了和Web Worker相同的思路来解决单线程中大量计算问题 ，官方提供了child_process模块和cluster模块
  - cluster底层是基于child_process实现
  - child_process、cluster都是用于创建子进程，然后子进程间通过事件消息来传递结果
  - 这个可以很好地保持应用模型的简单和低依赖，从而解决无法利用多核CPU和程序健壮性的问题
  - cluster底层就是child_process，master进程做总控，启动1个agent和n个worker，agent来做任务调度，获取任务，并分配给某个空闲的worker来做。
    - 每个worker进程通过使用 `child_process.fork()` 函数，基于 IPC 实现与master进程间通信
    - fork出的子进程拥有和父进程一致的数据空间、堆、栈等资源，但是是独立的，也就是说二者不能共享这些存储空间。那我们直接用fork自己实现不就行了。
    - 这样的方式仅仅实现了多进程。多进程运行还涉及父子进程通信，子进程管理，以及负载均衡等问题，这些特性cluster帮你实现了
- child_process模块通过它可以开启多个子进程，在多个子进程之间可以共享内存空间，可以通过子进程的互相通信来实现信息的交换
- Node10提供了实验性质的 worker_threads 模块，才让Node拥有了多工作线程，从Node12开始成为正式标准
  - Workers (threads) are useful for performing CPU-intensive JavaScript operations. 
  - They will not help much with I/O-intensive work. 
  - Node.js’s built-in asynchronous I/O operations are more efficient than Workers can be.
- Node.js 通过提供 cluster、child_process API 创建子进程的方式来赋予Node.js “多线程”能力
  - 但是这种创建进程的方式会牺牲共享内存，并且数据通信必须通过json进行传输，有一定的局限性和性能问题
- 基于此，Node.js提供了worker_threads，它比child_process或cluster更轻量
  - 与child_process或cluster不同，worker_threads可以有效地共享内存，通过传输ArrayBuffer实例或共享SharedArrayBuffer实例来实现
  - JavaScript和Node.js没有线程，只有基于Node.js架构的多工作线程
# discuss
- ## 

- ## contrary to popular belief, in Node.js promises (and async/await) would not yield to the event loop. 
- https://x.com/matteocollina/status/1862180654672171418
  - So, if you want the event loop to process I/O in between a long chain of async functions that actually aren’t doing any I/O, you would need to add a setImmediate (promisified) in between.
  - Or.. maybe avoid using so many promises when they are not needed.

- ## 🌰 今天看了下nodejs中线程，立马想到了以前java中学过的线程不安全和synchronized关键字。
- https://twitter.com/wulianwen1/status/1718927142497788299
  - 于是想试试nodejs里面是不是也一样，果然其实语言并不重要
  - [Nodejs Thread Concurrency](https://gist.github.com/childrentime/d4d43672fad2a0bf3dda35fda290dbc1)

- ## [Node.js 并发能力总结 - 知乎](https://zhuanlan.zhihu.com/p/353685224)
- 从逻辑上讲，异步并不是为了并发，而是为了不阻塞主线程。
  - 但是我们却可以同时发起多个异步操作，来起到并发的效果，虽然计算的过程是同步的。
- 当性能的瓶颈是 I/O 操作，比如查询数据库、读取文件或者是访问网络，我们就可以使用异步的方式，来完成并发。
  - 而由于计算量比较小，所以不会过多的限制性能。每当这个时候，你只需要默默担心下游的 QPS 就好了。
  - 以 I/O 操作为主的应用，更适合用 Node.js 来做，比如 Web 服务中同时执行 M 个 SQL，亦或是离线脚本中同时访问发起 N 个 RPC 服务。
  - 所以在代码中使用 async/await 的确很舒服，但是适当的合并请求，使用 Promise.all 才能提高性能。
- 一旦你习惯了 Promise.all，同时了解了 EventLoop 的机制，你会发现 I/O 请求的限制往往在下游。因为对于 Node.js 来说，同时发送 10 个 RPC 请求和同时发送 100 个 RPC 请求的成本差别并不大，都是“发送-等待”的节奏，但是下游的“供应商”是会受不了的，这时你需要限制并发数。
- 常用限制并发数的 Npm 包是 p-limit
  - 通过函数 enqueue、run 和 next，plimit 就产生了一个限制大小但不断消耗的异步函数队列，从而起到限流的作用。

- 在 NodeJS 中，一个异步资源表示为一个关联回调函数的对象。
  - async_hooks module provides an API to track asynchronous resources.

- 异步在 I/O 资源的利用上可以实现并发， 但是异步无法并发的使用 CPU 资源。多进程才能更好地利用多核操作系统的优点。
- Node.js 使用 Cluster 模块来完成多进程，我们可以通过 pm2 的代码来了解多进程
- 进程间的通信使用的是事件监听来通信。
- Cluster 的通信是消息通信，但是没办法共享内存。

- 如果想要共享内存，就需要多线程，Node.js 引入了 worker_threads 模块来完成多线程。
- Worker Threads 更擅长通信，这是线程的优势，不仅是可以消息通信，还可以共享内存。

- 总结
  - 作为 Web 服务，挺高并发数，选择 Cluster 更好；
  - 作为脚本，希望提高并发，选择 Worker Threads 更好；
  - 当计算不是瓶颈，在某个进程或线程中，灵活异步的使用更好。

- ## [Node.js 真的有协程吗？ - 知乎](https://www.zhihu.com/question/305443189/answers/updated)
- “协程是一种用户态的轻量级线程”这是有栈协程或者纤程 (Fiber) 的定义。
  - Node.js中的协程是无栈协程。无栈协程可以看作是回调函数和状态机的语法糖，它不一定要进行调度。

- 有栈协程：用(e)rsp栈寄存器来索引局部变量，上下文是协程私有的栈。 访问上下文数据也就是局部变量的时候，我们无需显式的使用栈寄存器+偏移量来访问，而是直接访问变量名。
- 无栈协程：用this来索引对象的成员变量，上下文就是对象自己。访问上下文数据也就是成员变量的时候，我们无需显式的使用this+成员偏移量（或者变量名）来访问，而是直接访问变量名。
- 两种协程访问的上下文中的数据，生命周期都大于函数的返回：栈的生命周期晚于函数的返回，this对象的生命周期晚于函数的返回。后者更晚而且往往需要手工销毁。

- node的协程是libuv实现的，node上层不可见，协程为node自己去管理和调控，上层只作为启发式的，对work不可见

- https://www.zhihu.com/question/502314022/answer/2247965561
- kotlin nodejs python 的协程都是前面十多年比较流行的无栈协程。
- 协程的核心，所谓协作式，就是碰到等待 io 或者事件的时候，主让出cpu 交给其他任务，（而不是常规代码碰到阻塞的调用，就占着 thread 不放，非要等 os kernel 来协调，把 cpu 让给其他 thread ， aka 抢占式调度。）
- 写过异步或者说事件驱动代码的都懂，凡是需要阻塞的方法调用，都得改成callback风格的api，尽快让出cpu给其他异步任务 ；这不就是协作式。所以协程就是要用提供一种框架化机制，替代这种繁琐又不易读的异步风格的碎片化的代码，比如大家都知道的 callback hell 回调地狱

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
- Node.js 并没有其它支持多线的程语言（如：java），诸如"synchronized"之类的关键字来实现线程同步的概念。
  - Node.js的 worker_threads 区别于它们的多线程。如果添加线程，语言本身的性质将发生变化，所以不能将线程作为一组新的可用类或函数添加。

- ## child_process 是用于创建子进程和父子进程通信的，有4个 api： spawn、exec、execFile、fork
- https://www.zhihu.com/pin/1413231233476685824
- spawn 是用 shell 来跑一段命令，返回一个 stream
- exec 基于 spawn，只是对返回的 stream 做了封装，直接可以拿到 buffer，只不过有上限，可以用  maxBuffer 设置
- execFile 没有跑 shell 环境，可以执行可执行文件，当然也可以跑 shell
- fork 则是用于执行 js 文件的
  - cluster 的 fork 是创建多个子进程以及通信的，会执行到分叉的地方
- 而关于通信：cp 的 api 都支持管道的 pipe，而所有的进程创建方式都支持事件的方式，底层是消息队列

# actor-model
- [[译] 你想知道的关于 actor 模型但可能不敢问的所有信息](https://skyao.io/post/202206-the-actor-model-everything-you-wanted-to-know/)

- [为什么我觉得 Actor 很难用？ - 知乎](https://www.zhihu.com/question/37792465/answers/updated)
