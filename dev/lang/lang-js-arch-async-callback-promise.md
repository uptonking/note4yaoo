---
title: lang-js-arch-async-callback-promise
tags: [architecture, async, js, lang, promise]
created: 2021-08-30T07:00:06.476Z
modified: 2021-08-30T07:01:09.493Z
---

# lang-js-arch-async-callback-promise

# discuss

- ## 

- ## 


- ## [What are the advantages of async.js over native Promises](https://github.com/caolan/async/issues/1714)
- Promises add a caching layer for results and errors and state machine around your function calls which makes things more stateful and somewhat slower than necessary 
  - and they also allow passing the next point of execution around which breaks encapsulation. 
  - Async/await helps somewhat with the latter but you can get the best of both world with casync along with this library.
- I could do `Promise.all(ratings.map(processRating))` but this would overload my API. With `mapLimit` I can set a max of 25 calls at a time. Rather than 1000's. 

- ## [Node.js 异步api的本质和 libuv](https://zhuanlan.zhihu.com/p/402398815)
- Node.js 是一个 Javascript 的运行时，提供了系统能力的 api，主要是文件、网络相关的 IO api，而 IO api 的实现是在 libuv，提供了同步异步两种形式的 api。
- 本来就来探究下 libuv 的功能和提供的 api 的形式。
- cpu是顺序执行代码的，通过pc寄存器来存储着下一条指令的内存地址。代码的执行流程叫做控制流。
  - 但是对于一些IO操作来说，并不需要cpu做计算，而是在等待硬盘设备、网络设备的数据读取，
  - 这时候 cpu 是空闲的，所以一条控制流不行，会导致cpu利用率太低。
- 所以操作系统又提供了进程、线程的功能，进程是分配资源的单位，而执行代码主要是靠线程，
  - 一个线程就是一条控制流，它是cpu调度的基本单位，也就是说可以在多个控制流之间切换，当一个线程在做IO的时候就释放cpu，让其他线程去跑。
- 一个线程阻塞的等待IO的方式就是同步，会比较浪费 cpu，
  - 而多个线程切换，在做IO的时候让其他线程上 cpu 跑，执行完IO再申请cpu来继续后续处理，这种方式就是异步
- 异步最终是多线程来实现的，但是在 Node.js 里面又进一步通过 event loop 做了封装，
  - 比如执行文件读取、网络访问的时候并不需要开发者去创建线程，而是调用api，指定回调函数就可以了，这是对多线程的进一步封装。
- **异步的底层实现都是通过线程的切换，但是暴露给开发者的形式有两种**：
  - 第一种是开发者控制线程的创建和销毁，指定线程执行的内容，java是这种。
  - 第二种是提供事件循环机制，提供一系列异步api，这些异步api最终是由线程来执行的，但是开发者不需要手动管理线程。javascript是这种。​
- 在Node.js里面，实现 event loop 的就是 libuv，它是一个异步IO库，负责文件和网络的io，提供了事件形式的异步api。
  - libuv里有一个线程池负责维护一些线程用来执行异步api，这个线程池的大小是可以设置的，通过环境变量 UV_THREADPOOL_SIZE 可以设置。
- 就是说libuv是负责IO的 api 的异步实现的，基于更底层的操作系统 api。
  - 这些操作系统api有的是异步的，有的不是，对于不是异步api的那些，就要由libuv的线程池中的线程来执行，变成异步的形式。
- 这些 api 包括：
  - 所有的文件 fs api，除了 watch 的 api
  - 加密 crypto 的异步 api
  - 所有压缩的 zlib api
  - dns.loopup
  - 这些 api 共用一个线程池，那么肯定会相互影响，所以有的时候需要加大线程池的线程数量，默认是 4，当需要的时候可以设置这个环境变量来加大。
- 当面试问到Node.js性能调优的时候，可以答设置libuv的线程池大小，堆大小设置的这两个参数/环境变量。
- 看了文档之后，我们更确认了异步最底层的实现就是线程，只不过是通过libuv的线程池做了封装。

- 再来看下 Node.js 都怎么提供这两种 api 的
- 同步的 api 比较简单，就是调用函数，拿到返回值就行，很多 xxSync 的 api 都是同步的
- 而异步的 api 则分为了两种形式，callback 和 promise
  - 其中 promise 的版本只有两个模块有，fs 和 dns，是在 Node.js 10.x 引入的，方便使用 async、await 来组织代码

- 总结
- 程序在进行IO的时候， cpu是空闲的，为了更好的利用cpu，操作系统提供了进程、线程的功能，一个线程就是一条控制流。
  - 当在IO的时候，切换到别的线程，等IO结束之后再继续执行的方式就是异步，而相应的一个线程阻塞的等待的方式就是同步。
- 异步最终是由线程实现的，但是提供给开发者的有两种形式：
  - 一种是提供线程api，让开发者自己管理线程，
  - 另一种方式就是提供事件循环，对于异步api通过线程来实现。
  - 第二种方式对开发者更透明，不需要关心线程的创建和切换。
- Node.js 里面的 event loop 的实现是在 libuv，它提供了文件和网络的异步 IO 的 api，
  - 从文档中我们可以看到，libuv是基于操作系统的 api 实现的，而其中一些同步的api，则是由 libuv 的线程池来执行，达到异步的目的。
  - 但是线程池的大小默认是 4，有的时候需要加大，可以通过修改 UV_THREADPOOL_SIZE 的方式。
- Node.js 提供的 api 有3种形式，一种是同步的，一种是异步callback、一种是异步promise。
  - 其中异步 promises 的形式是推荐的写法，但是只有在 fs、dns 两个模块可用，并且要在 Node.js 10 以上才行。

- discussion

- 异步底层实现不一定是多线程吧，某些异步任务，如果 IO 任务直接交给硬件，然后等待系统事件通知
  - 是这样，比如 dma 就是，libuv 是通过多线程封装了一些同步系统 api，异步系统 api 的部分不一定是多线程
  - 限定在软件级别的异步就是靠线程了，软件的执行是靠cpu，也就是需要线程。硬件级别的异步是靠电路，就不用线程了。