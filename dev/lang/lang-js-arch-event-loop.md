---
title: lang-js-arch-event-loop
tags: [architecture, event-loop, js, lang]
created: 2021-08-30T06:49:37.481Z
modified: 2021-08-30T06:52:33.680Z
---

# lang-js-arch-event-loop

# discuss

- ## 

- ## [is requestAnimationFrame belong to microtask or macrotask in main thread task management?](https://stackoverflow.com/questions/70995372/is-requestanimationframe-belong-to-microtask-or-macrotask-in-main-thread-task-ma)
- Technically... neither. 
  - requestAnimationFrame (rAF)'s callbacks are ... callbacks.
- Only one of macrotasks will get executed per event-loop iteration, selected at the first step
  - Finally there are callbacks. These may be called from a task (e.g when the task is to fire an event), or in some particular event-loop iterations, called "painting frames".
- Indeed the step labelled update the rendering is to be called once in a while (generally when the monitor sent its V-Sync update), and will run a series of operations, calling callbacks, among which our dear rAF's callbacks.
- rAF (and the other callbacks in the "painting frame"), have a special place in the event-loop where they may seem to be called with the highest priority. 
  - Actually they don't participate in the task prioritization system per se (which happens in the first step of the event loop), they may indeed be called from the same event-loop iteration as even the task that did queue them.

- ## [Node中的event-loop执行情况可以用microtask和macrotask方式来解释么？](https://www.zhihu.com/question/63684913)
- microtask 相关是V8提供的API，虽然规范里提了同名以及同意义的microtask，这不表示node就用了它，更被别说 macrotask 这种 V8 里没有 API 了。
  - 既然 node 与 libuv 相关没暴露这个，那就跟这俩没关系，俩没关系的事儿咋合一起解释呢。

- ## [浏览器与Node的事件循环(Event Loop)有何区别?](https://zhuanlan.zhihu.com/p/54882306)
- 进程是CPU资源分配的最小单位；线程是CPU调度的最小单位
- 以Chrome浏览器中为例，当你打开一个Tab页时，其实就是创建了一个进程，
  - 一个进程中可以有多个线程，比如渲染线程、JS 引擎线程、HTTP 请求线程等等。
  - 当你发起一个请求时，其实就是创建了一个线程，当请求结束后，该线程可能就会被销毁。
- 浏览器内核是多线程，在内核控制下各线程相互配合以保持同步，一个浏览器通常由以下常驻线程组成：
  - GUI渲染线程
  - JavaScript引擎线程
  - 定时触发器线程
  - 事件触发线程
  - 异步http请求线程

- ### 浏览器中的 Event Loop
- 事件循环中的异步队列有两种：macro（宏任务）队列和 micro（微任务）队列
- 宏任务队列可以有多个，微任务队列只有一个。
- 常见的 macro-task 
  - 比如：setTimeout、setInterval、 setImmediate、script（整体代码）、 I/O 操作、UI 渲染等。
- 常见的 micro-task 
  - 比如: process.nextTick、new Promise().then(回调)、MutationObserver(html5 新特性) 等。
- 每一次循环都是一个这样的过程 (随时优先执行micro)
  - 当某个宏任务执行完后, 会查看是否有微任务队列。
    - 如果有，先执行微任务队列中的所有任务，
    - 如果没有，会读取宏任务队列中排在最前的任务，
    - 执行宏任务的过程中，遇到微任务，依次加入微任务队列。
  - 栈空后，再次读取微任务队列里的任务，依次类推。

- ### Node中的 Event Loop
- Node采用V8作为js解析引擎，而I/O处理方面使用了自己设计的 libuv
  - libuv是一个基于事件驱动的跨平台抽象层，封装了不同操作系统一些底层特性，对外提供统一的API，事件循环机制也是它里面的实现
  - libuv库负责Node API的执行。它将不同的任务分配给不同的线程，形成一个 Event Loop（事件循环），以异步的方式将任务的执行结果返回给V8引擎。
- libuv引擎中的事件循环分为6个阶段，它们会按照顺序反复运行。
  - 每当进入某一个阶段的时候，都会从对应的回调队列中取出函数去执行。
  - 当队列为空或者执行的回调函数数量到达系统设定的阈值，就会进入下一阶段。
- node事件循环阶段
  - timers 阶段
    - 会执行 setTimeout 和 setInterval 回调，并且是由 poll 阶段控制的。
    - 在Node中定时器指定的时间也不是准确时间，只能是尽快执行。
  - I/O callbacks 阶段
    - 处理一些上一轮循环中的少数未执行的 I/O 回调
  - idle, prepare 阶段
    - 仅 node 内部使用
  - poll 阶段
    - 获取新的 I/O 事件, 适当的条件下node将阻塞在这里
  - check 阶段
    - 执行 setImmediate() 的回调
  - close callbacks 阶段
    - 执行 socket 的 close 事件回调
- 日常开发中的绝大部分异步任务都是在timers、poll、check这3个阶段处理的
- process.nextTick
  - 这个函数其实是独立于 Event Loop 之外的，它有一个自己的队列，
  - 当每个阶段完成后，如果存在 nextTick 队列，就会清空队列中的所有回调函数，并且优先于其他 microtask 执行

- ### Node与浏览器的 Event Loop 差异
- 浏览器环境下，microtask 的任务队列是每个 macrotask 执行完之后执行。
- 而在Node.js 中，microtask 会在事件循环的各个阶段之间执行，也就是一个阶段执行完毕，就会去执行microtask队列的任务。
- 浏览器和Node环境下，microtask任务队列的执行时机不同
  - Node端，microtask 在事件循环的各个阶段之间执行
  - 浏览器端，microtask 在事件循环的 macrotask 执行完之后执行

- ## [2020年Node.js凉了吗？凉到什么程度了？](https://www.zhihu.com/question/416267787/answers/updated)
- 华为的鸿蒙系统的手环端采用了Javascript开发语言，模拟器使用Node.js
- 技术是由商业利益驱动的，大公司很多技术都应用了node，想要凉先问问大公司愿不愿意花时间和钱去重构项目
- 前公司曾用node做纯后端，后来发现非常非常难招人，最后转java了。

- ref
  - [2019年了，Node.js现在能不能用来做纯后端开发？](https://www.zhihu.com/question/322502957/answers/updated)
  - [现在将node. js作为纯后端的公司多吗？](https://www.zhihu.com/question/431630885/answers/updated)
  - [为什么互联网公司开始用node.js做web服务的中间层？](https://www.zhihu.com/question/264563447/answers/updated)
# discuss-java-event-loop
- [事件调度层：为什么 EventLoop 是 Netty 的精髓？.md](https://learn.lianglianglee.com/%E4%B8%93%E6%A0%8F/Netty%20%E6%A0%B8%E5%BF%83%E5%8E%9F%E7%90%86%E5%89%96%E6%9E%90%E4%B8%8E%20RPC%20%E5%AE%9E%E8%B7%B5-%E5%AE%8C/04%20%E4%BA%8B%E4%BB%B6%E8%B0%83%E5%BA%A6%E5%B1%82%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%20EventLoop%20%E6%98%AF%20Netty%20%E7%9A%84%E7%B2%BE%E9%AB%93%EF%BC%9F.md)
  - Netty 高性能的奥秘在于其 Reactor 线程模型。 
  - EventLoop 是 Netty Reactor 线程模型的核心处理引擎
  - 单线程模型结构，在 Reactor 单线程模型中，所有 I/O 操作（包括连接建立、数据读写、事件分发等），都是由一个线程完成的。单线程模型逻辑简单，缺陷也十分明显
  - 多线程模型将业务逻辑交给多个线程进行处理。除此之外，多线程模型其他的操作与单线程模型是类似的，例如读取数据依然保留了串行化的设计。
  - 主从多线程模型由多个 Reactor 线程组成，每个 Reactor 线程都有独立的 Selector 对象。MainReactor 仅负责处理客户端连接的 Accept 事件，连接建立成功后将新创建的连接对象注册至 SubReactor。再由 SubReactor 分配线程池中的 I/O 线程与其连接绑定，它将负责连接生命周期内所有的 I/O 事件。
  - Netty 推荐使用主从多线程模型，这样就可以轻松达到成千上万规模的客户端连接。
  - 大致总结出 Reactor 线程模型运行机制的四个步骤，分别为连接注册、事件轮询、事件分发、任务处理

### [Event Loop 事件循环 - 知乎](https://zhuanlan.zhihu.com/p/343643559)

- HTTP 服务器是常见的服务器类型，往往需要同时处理大量的请求。

- Serialization 单线程串行顺序处理
  - 单线程串行，一个个请求顺序处理：处理请求1 -> 处理请求2 -> 处理请求 X。
  - 简单，资源消耗少。但是资源利用率不高，效率低。如果阻塞会导致等待，并发能力低。

- Parallellism 多线程并发处理
  - 一个线程处理一个请求：A 线程处理请求 1，B 线程处理请求 2，N 线程处理请求 X。
  - 复杂，并发性高，但是消耗大量资源，还有线程切换成本。这个是 Java Web 常用的模式。

- Concurrency 单线程并发处理
  - 一个线程同时处理多个请求
  - 略复杂，并发性高，资源消耗低，效率高，但是一个线程的处理能力有限。
  - 通过 I/O Multiplexing 实现，比如 Select、Epoll 等。这个 Nginx 和 Node.js 用的模式。

- 对于 CPU 来说，CPU 的计算能力也是一定的，也就是每个时间段可以做的事情也是有限的，所以如何高效的利用 CPU 尤为重要。
  - CPU 时间片分给线程，目的是为了可以同时处理多任务。但是多线程带来了线程资源的消耗以及线程切换带来的时间片损耗。
  - 如果我们可以在一个线程同时处理多个任务，那么就可以避免这个问题，并且保持 CPU 的高效利用。
  - I/O 多路复用让单线程可以同时处理多网络请求，同时 CPU 的速度远远大于网络速度，明显的时间差，所以使用 EL 模型处理多网络请求是一种比较高效的的方式。
  - 我们熟知的高性能网络应用 Nginx 和 Redis 都使用了 EL。

- Node 为服务端开发设计，不止是网络功能，还需要支持定时器、文件管理、加解密等。
  - 对于阻塞和 CPU 密集型操作，我们可以在 EL 主线程开一个线程完成这些任务，EL 继续处理其他事件。等其他线程把耗时任务完成，通过事件通知 EL，EL 根据优先级处理这些事件，这样 EL 就可以应对阻塞和 CPU 密集型的耗时任务了。

- ## [event-loop异步模型为什么比多线程模型在IO密集场景中更高效？](https://www.zhihu.com/question/67751355)
- 为什么说 event-loop 在IO密集型场景中比线程模型更高效？
  - 常见说法是，因为线程切换上下文开销很大，但 event-loop模型中不也需要不断的在主线程和IO线程之间切换吗？
- HotSpot JVM 为什么放弃 green thread 而改为 native thread？
  - 如果线程模型的劣势在于切换开销，那一个自然的想法就是用更轻量的用户级线程替换OS线程，然而根据资料，JVM最初就是LWT，但后来却改为了OS线程，据说是因为并行瓶颈问题，具体指的是什么呢？
- 如果说LWT方案有难以解决的缺陷，那 go、akka 等以高并发为卖点的语言或库，是否存在同样的问题？

- 不知道题主之前见到的 event-loop 模型的程序是怎么组织的。
  - 最著名的 event-loop 的程序莫过于 redis 和 nginx，而两个恰好都是 single-threaded，一个进程占满一个核。
  - 有些应用中请求处理可能需要一定的CPU时间，那么可能会分到另外的线程去计算，为的也是保证 I/O 这一个线程能够不被阻塞。
- 用户线程的问题主要在于操作系统无法提供足够的支持，因为从操作系统的角度来看，一个时间只有一个线程在运行而已。
  - Linux以线程为调度单位，不管多少个用户线程都在这一个核上运行；
  - 一旦这个OS线程被抢占或挂起了（比如 blocking syscall），所有的用户线程都被一起挂起。
  - 这也回到了为什么在处理 I/O 的时候，用 event-loop + non-blocking I/O 要好过 multi-threading + blocking I/O 的原因：防止OS线程被 blocking I/O 强制挂起。

- 因为event loop模型可以不使用IO线程，而是使用操作系统提供的IO复用/异步IO/事件驱动IO。
  - 就比如ngx，在linux上，ngx用的是边沿触发的epoll，这是典型的IO复用，ngx是没有专门的IO线程的。
  - 所以并不是event loop模型更高效，而是异步IO复用比多线程同步IO额外开销更低。
- event loop模型的优点是，
  - 一，event loop更贴近异步IO复用的模型，因此开发效率更高。
  - 二，单线程模型能够避免多线程带来的同步问题，既提高了开发效率，又避免了同步开销。
