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
# discuss-stars
- ## 

- ## 
# discuss-concurrency-languages
- ## 

- ## 

- ## My memory tells me there are two papers. First one that talks about how event-based concurrency is better than thread-based concurrency and a second one that makes tries to make the opposite claim. But I can't find them anymore! Did my mind hallucinate them?
- https://x.com/penberg/status/1856605191002329461
  - "why X is a bad idea" was the pattern of the paper titles

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Napa.js: A multi-threaded JavaScript runtime | Hacker News _201710](https://news.ycombinator.com/item?id=15498219)
- Multi-threading does well for some problems, but often, multi-machining or multi-processing is sufficient, which is why so many runtimes don't really do multi-threading: Node. JS, Python, Ruby.
  - Very true, and we've seen better performance from multi-process than multi-threading in some high-traffic (10Gbps) systems (those were C++ however, not node). It was puzzling, but I put it down to the OS scheduler; I imagine that a single multi-threaded process would be pre-empted in the typical fashion, but that multiple single-threaded processes would, in aggregate, spend less time in a pre-empted state.
- The benefit to programs that don't use threading and use event loop and shared nothing multi-process is that they don't have the overhead when things are maxed out.
  - This is why virtually every high performance server (nginx, redis, memcached, etc) is written this way and things like varnish (thread per request) are multiples or orders of magnitude slower.
  - Funny people criticizing nodejs for using the same architecture that all the best-in-class products use.

- Context switching is expensive and very tempting to forget about in multi-threaded development. You eliminate that overhead constraining the execution code to a single thread context.

- Node.JS, Python, and Ruby are in C/C++ so you can do multithreading in all three, if you are willing to write native modules.



- 
- 
- 
- 

- ## Apparently since Node v20 and Chrome v111 it's possible to perfectly* pass a synchronous function to a worker and for that worker to just call it synchronously, thanks to ` SharedArrayBuffer.prototype.grow` .
- https://twitter.com/fabiospampinato/status/1751590274873077860
  - Previously this wasn't possible because the worker needs to create a SharedArrayBuffer, pass it to the other thread, and then the other thread writes the result onto the buffer, basically. Problem is you can't pre-allocate a SAB of the right size, now you can grow it though.
  - Unfortunately there's still the ~problem where it could get into a deadlock situation, where worker A passes a sync function to worker B, and worker B passes a sync function on worker A that depends on the function it received, so both of them can wait on the other part forever.

- grow is nice but not widely available ... Atomics + SAB already make that possible anyway 
- How do you not need to be able to grow the SAB if you don't know how much space you are going to need to encode the value to return back to the worker?
  - 2 SAB ... the first one is to ask how many bytes are needed and waited sync to then pass the right SAB to fill with data ... still sync.
  - With Atomics you can make anything look sync, even multiple Atomics operations batched in a single one.

- ## 🆚️ What's the difference between a Binary Mutex and a Semaphore?
- https://twitter.com/RaulJuncoV/status/1745817381358747810
- A mutex (short for mutual exclusion) is like a lock that safeguards shared resources.
  - It ensures that only one thread or process can access the resource at any given time.
  - A mutex is typically binary, with two states: locked or unlocked. It's a simple on-off switch.

- A semaphore doesn't enforce mutual exclusion by itself.
  - But allows us to limit the number of threads/processes accessing the resource at the same time.
  - A semaphore has a non-negative count, representing the number of available units or resources.

- ##  what if JS had a simple way to share structured data across Worker (without postMessage)?
- https://twitter.com/jarredsumner/status/1719259259840684417
  - Shared structs proposal is a better approach for the “objects” but a Map is useful for concurrency

- ## What if you could use web workers directly from JSX?
- https://twitter.com/manucorporat/status/1657419808336486400

- Last year, did research for how to do filtering, sorting, grouping, etc. in a web worker for TanStack Table, but had no idea how it could be bundled. Maybe it's actually possible?
  - https://twitter.com/KevinVanCott/status/1657603580386242561
- This has massive implications for the table API. Essentially everything needs to become async/lazy.
- Big if true. I just don't understand how it could work and bundle yet. Maybe a qwik adapter for table could explore this?

- ## [Webworker support · konvajs/react-konva](https://github.com/konvajs/react-konva/issues/474)
- i dont think react-konva is slow. I am using it to create grids, around 1 million rows x 1 million columns. I find it really fast, comparable to native canvas, with marginal difference.
- first you need to find where the slowness comes from. From React (it is slow in many cases), from Konva rendering?
  - 💡 Using a Webworker is not a magic way to solve the performance. It can make the UI more responsive, but rendering itself may be still slow.
  - For now, I have no idea how we can synchronize react in the main thread with nodes three in the web worker. As I know, there are some attempts to run full react in the Webwork, but it is too complex.
- The best I could think of is to relocate my state manager in a web worker and all the huge computation in webassembly, and use an offscreen canvas to render from another thread. But this would be in an ideal and deadlineless dev project ...

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

- ## What's something you know should be done in a Worker, but ended up running on the main thread due to feasibility/time/complexity reasons?
- https://twitter.com/_developit/status/1428731551794278402
- All my state management. React depends heavily on stable references and I would have to use some complex patch set method to keep things stable. @dai_shi has some done some cool redux stuff on that but... I still have to keep all of my app state on the main thread
  - my recent experimental project is to render react components in worker
  - https://github.com/dai-shi/react-worker-components
- This is a tricky one IMO - moving UI update calculation into a Worker; this way also means **moving input handling to the Worker**, which means your best-case input response times are 2 x postMessage cost (base of around 5ms IIRC). Not unworkable, but tricky to scale.
  - Yeah, 5ms is big. We have control which components to offload. The question is if developers can predict whether a component takes more than 5ms to render... Sounds impossible. The main use case in my mind is async stuff like data fetching from server.
- Isn’t data fetching off the main thread anyway?
  - Yeah, I mean data fetching + rendering with the fetched data. My motivation is to realize "React Suspense for Data Fetching". While React Server Components seems the way forward, it would be nice to have a solution without server.
- An ideal solution might **serialize input responders and send them to the main thread** so they can execute immediately instead of calling handlers in the worker. The Worker still handles large updates (change screens, etc), but the **UI thread handles most interactions**.
  - An ideal solution is proper shared memory primitives which are available on worker and main thread
  - Maybe, though there'd still be a cost. Shared Memory is really difficult to spec in browsers because of the security implications.
  - Record and tuples may be shared without any security (races) problem.
  - True! Now you have a locking problem
- Procedural Generation. I would love to do it in a worker but **Off Screen Canvas isn't widely supported** and I spend more time trying to think about the typed array transfer protocol than having fun making art.
- A huge performance boost for HTML-over-the-wire libs (like Hotwire, @htmx_org or @unpoly ) would be the ability to parse HTML in a separate thread.
- Charting library calculations. Animation tween calculations
- Text parsing to build an ast, for syntax highlighting and validation.
- Aggregate stats on Geospatial data to fit it into a fixed tile, aka give me the average temperature in this tile based on a bunch of points from GeoJSON. Can be done using an R-tree, but would be even smoother in a worker.
- We test between sending images blur url or image blur hash and decoding it on client(by getting url from canvas). 
  - second solution had better performance because no extra connection to server needed after getting hashes. 
  - Next require string for blur url but we can get it onmessage
- not really in topic but merging 2 big immutable objects is always a pain specially if you wanna try to keep the same reference to avoid rerenders
  - https://github.com/developit/object-diff-patch
- Re-rendering needs low latency, doesn't the cost of round-trip IO op (serialize via msg, db, network) + worker compute outweigh the cost of thread blocking? Sure this is just one task example, worker is better for multiple tasks.
  - I depends. I once faced a problem where I was dealing with multiple images uploading so I had to show the upload progress for each image. Meanwhile, the user could add more images from another local folder and start a new bulk upload. That would hit the backend and then do a big state update with all the images. All of this while the upload indicator shows for each image (not really ideal i know, **we switched to a global progress bar later**) and the user still needs to be able to scroll the image grid, move the images around to reorder and rename
  - The state update would be the main thing to move off-thread there. Anything else would be pretty directly UI-related, which is main thread territory.
- All of it! We should only listen to events on the main thread, and pass them into a worker. If the worker isn't loaded, enqueue them until it is.
  - This gets tricky for things like responding to text input. It can be done with a worker roundtrip, but it's hard.
- Webcrypto encrypting ANY file
  - The browser uses a dedicated thread for webcrypto already, so you likely won’t see much of a difference putting this into a web worker.
  - The only downside is that you can't really run multiple webcrypto's in parallel; the browser will schedule them to run sequentially in the same WebCrypto thread (the browser only has one of these...). But yes, it's good in that the main thread is never blocked by WebCrypto...
- Image manipulation via canvas (scale, crop, rotate, hue/bright/contrast etc)
- client-side image downsizing
  - Yup. Nearly instant on a desktop but 5+ seconds on a mobile device. But changing the code to a worker has lots of risk for a .001% of the application feature.
- Heavy numeric data transformations prior to plotting (eg smoothing, grouping/mean, etc, done client side for interactivity). Ideally should also be ported to WASM.
- Mostly audio stuff, like encoding. But it matters mostly for external projects, sometimes worker overhead isn't worth it.
- pdf generation - QR code reading
  - counter-question: what do you think of using indexedDB as a communication channel/ cache for data heavy communication between main thread and worker thread
  - **IndexedDB is pretty slow**. I'd sooner use a basic in-memory sync setup, or postMessage with a cache on the Worker side if you can afford the 5ms 2-hop cost.
