---
title: thread-lang-js-worker-concurrency
tags: [concurrency, js, thread, web-worker]
created: 2021-09-28T04:43:49.453Z
modified: 2022-12-19T01:59:37.634Z
---

# thread-lang-js-worker-concurrency

# guide

- resources
  - [2021 Web Worker 现状 - 知乎](https://zhuanlan.zhihu.com/p/393428948)
# discuss
- ## 

- ## 

- ## 

- ## [为什么web worker可以在前端开多线程，解决单线程卡死页面的问题，但是没有得到广泛使用？ - 知乎](https://www.zhihu.com/question/61125566)

- 计算比较复杂的产品，用 worker 和 wasm 的越来越多了。
  - 比如 pdf 预览、富文本编辑器、多媒体、GIS 等。
  - node 后端用 worker thread 较少，因为大多数 bff 场景其实就是 API gateway 和 orchestration（编排），属于重 IO 轻计算场景，上 worker thread 意义不大。多进程模型更好管理，也更受欢迎，例如 pm2 cluster 。

- 火狐的 pdf.js 在渲染的时候就有用到 web worker。

- 启动耗时、IPC通讯、心智负担三座大山一放，劝退一波人。
  - 对比下可怜的加速比，又劝退一波人。除非万不得已基本不会有人用了。
  - 真要想好好搞并发编程方案，那就引入经典的线程模型呗。然而前端社区偏不，做出来发现没有共享内存不行确实又拿SharedArrayBuffer来打补丁，何必呢？总搞面多了加水水多了加面的把戏

- 我司就是web-worker的重度使用者。我们是做分布式应用的，所以把所有的逻辑全部放到WebWorker中，作为一个“后端”来使用。
  - 要说为什么没有广泛使用，主要看你了解的网页是什么类型的。如果是浏览图文信息，那主线程足够了，但如果是要将大量逻辑跑在前端的“应用”，那绝大多数会有web-worker的需求。

- 关于“弊端”方面的问题。我个人觉得其实没什么弊端，但可以简单地说一些比较有争议的点：
- 没有dom，
  - 这点我个人理解其实不算弊端，相反的，是一个很正确的设计。
  - 为什么这么说？因为worker和window不一样，在window中不能阻塞，但是在worker中可以使用Atomic来做暂停，这就意味着async可以转换成sync。
  - 因此worker中没有dom并不意味着真的就没有dom，它能模拟dom（我们内部已经相关技术方案来验证这个想法，实现路径跟 `ampproject/worker-dom`不一样，就是基于Atomic来做方案，我尽量今年年底将它开源吧）。未来可能还会有ElementWorklet(Worklet技术向可能也会是一个比较直接深挖的点)来优化解决问题的路径长度……
- 没有WebRTC（个人猜测这样的设计点可能和渲染层有关系，WebRTC的一些接口跟canvas有关联，跟dom相关的就很难挪到worker上）。
- SharedArrayBuffer和Atomics支持不够广泛。
  - 这套内存相关的接口其实很早就出来了，但是因为CPU漏洞的问题，导致大家都没有想去好好用它的意愿，这点极大地影响了WebWorker的推广。
  - 现在Chrome90重新用一套更加严格的机制将它带回到移动端。但这也就意味着要比较广泛的使用估计还得有个两三年。
  - 如果有SAB+Atomic，基本就意味着能在WebWorker上构建出一套完善的并发编程方案，这套方案会与WASM会师，估计21~22年，相关提案能到第三阶段，可能golang就会将goroutine带到Web。

- 另外再说一下理论，主线程与worker没有被太多特殊对待。
  - 但差别在于，主线程因为是和UI线程搞在一起，所以真实场景下会少掉很多执行时间；
  - 还有现在越来越多的场景下CPU核心并不完全一致，特别是手机上arm架构很常见的大小核设计，所以worker可能被调度到一些低性能的物理核心上是可能的。

- 因为密集计算在前端使用率没那么高吧。
  - worker和node的child_process.folk类似，都是双向postMessage和onMessage互相通讯，只能传递序列化数据，不支持DOM访问。所以利用worker多线程加载js库是别想了。
  - 而且本身worker的解析建立也是额外开销，worker内的js运行速度也有损失，如果不是需要并行，多次重复调用，对常规场景不会有性能提升。
  - 能用到就是长时间避免密集计算卡死UI，比如上千长度的数组diff等，但是这种需求在前端应该不多。
  - 此外，多线程带来的额外代码不少，全部函数都要改成异步，你要考虑worker崩溃时候的重启，你要考虑同时多次请求的隔绝问题得设计一个类似jsbridge的封装，还是挺烦人的
- 绝大部分场景下，Web Worker没太多用武之地，浏览器性能已经很强了。
- 对于大部分应用60帧一个线程绰绰有余，真正卡顿比如第三方库的渲染，
  - 唯一一个我使用webworker的场景，就是需要做音频处理时，当我在处理一个长达100ms的音频自相关计算时，当启动了4到8个worker时，在手机上才能完成一秒几次的更新。
  - 其实在web里，限制实在太多了，很难把体验做到完美，比如你现在webworker里计算渲染，实际上呢，很多库都是需要dom操作，并不能直接在内存里计算一个位图然后主线程只要把它复制到屏幕上。

- 我做数据可视化的时候有用，启动webworker本身是要耗时间的，经过长期测试大约为14ms。如果一段代码片段耗时没超过20ms就不要用了。
  - 了解一下时间切片、worker中创建worker
  - 另外做一些本地缓存、indexedDB等也可以极大提高速度。
  - 同在可视化用到，做d3大规模图力导引时，把节点位置计算逻辑放在worker中，子主线程通信坐标可以优化，不过在线程通信时，要用array buffer和transfer方式优化一下

- 我司是做教育在线直播的，web端的播放器就是wasm+worker落地的。未来期待着浏览器可以支持wasm更多特性simd，多线程。worker可以实现真正的多线程实现内存共享。那个时候前端真的就要变天了。

- 在视频处理上经常用
  - 比如hls.js这个库里面对worker的使用；
  - 像数据缓存啊，网络请求啊，对很多业务来说不是瓶颈，场景不深刻

- 考虑到线程间通信依然是有损耗的，那么跟起多个进程相比，有可能在某些情况下，效率反而不高，而且最重要的是它增加了编程的复杂度。
  - cluster就是多进程。

- ## [What can service workers do that web workers cannot? - Stack Overflow](https://stackoverflow.com/questions/38632723/what-can-service-workers-do-that-web-workers-cannot)

|              | Web Workers  | Service Workers  |
|--------------|--------------|------------------|
| Instances    | Many per tab | One for all tabs |
| Lifespan     | Same as tab  | Independent      |
| Intended use | Parallelism  | Offline support  |

- So lifecycle is one fundamental difference between the two (a consequence of their intended use).

- ## iframes are a better model than workers for concurrent JS in servers
- https://twitter.com/jarredsumner/status/1532162212613066752
  - half trolling but basically: instead of big app and some underpowered apps, lots of medium-sized apps coordinated externally
- So kinda like micro apps (iframes) which together build up a bigger app?
  - yeah, or maybe browser tabs are a better analogy than iframes

- ## Synchronous communication for DOM operations between main and worker thread has been a fun challenge. 
- https://twitter.com/adamdbradley/status/1442490416062943234
  - But the real dragons lay in marshaling data, and creating functions on one window context, to be accessed by another.
- I have always wondered how node did this with IPC then I saw somebody else pass functions between isolated contexts. completely mind-blowing stuff.
- https://github.com/laverdet/isolated-vm
  - a library for nodejs which gives you access to v8's Isolate interface. 
  - This allows you to create JavaScript environments which are completely isolated from each other. 
  - This can be a powerful tool to run code in a fresh JavaScript environment completely free of extraneous capabilities provided by the nodejs runtime.
