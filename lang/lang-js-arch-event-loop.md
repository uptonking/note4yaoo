---
title: lang-js-arch-event-loop
tags: [architecture, event-loop, js, lang]
created: '2021-08-30T06:49:37.481Z'
modified: '2021-08-30T06:52:33.680Z'
---

# lang-js-arch-event-loop

# discuss

- ## 

- ## 

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
