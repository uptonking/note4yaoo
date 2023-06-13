---
title: lang-js-arch-event-loop
tags: [architecture, event-loop, js, lang]
created: 2021-08-30T06:49:37.481Z
modified: 2021-08-30T06:52:33.680Z
---

# lang-js-arch-event-loop

# guide

- tips
  - [面试必问的异步顺序问题，用 Performance devtools 轻松理清 - 知乎](https://zhuanlan.zhihu.com/p/603691968)

- micoroTask
  - [Tasks, microtasks, queues and schedules - JakeArchibald.com](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)
# blogs

## [Explainer: queueMicrotask | docs](https://fergald.github.io/docs/explainers/queueMicrotask.html)

- There are several existing ways to queue a microtask (introduction to microtasks):
  - Promise.resolve().then(callback)
  - Register a mutation observer and trigger it with a mutation
- The library asap uses these tricks to provide a cross-browser way of queueing a microtask.
  - Developers and frameworks are already using these methods to queue microtasks. 
- The platform should support queueing microtasks directly as a primitive operation.

- This proposal would add an API to directly queue a microtask without the need for any tricks.
  - `queueMicrotask(callback);`

- A microtask posted with queueMicrotask may itself post another microtask so of course buggy websites can create infinite loops using this API. 

## [💡 requestIdleCallback和requestAnimationFrame详解](https://www.cnblogs.com/cangqinglang/p/13877078.html)

- 页面是一帧一帧绘制出来的，当每秒绘制的帧数（FPS）达到 60 时，页面是流畅的
  - 每一帧分到的时间是 1000/60 ≈ 16 ms。所以我们书写代码时力求不让一帧的工作量超过 16ms。

- 浏览器每一帧都需要完成哪些工作？ life of a frame
1. input events 处理用户的交互
  - blocking input events: touch, wheel
  - non-blocking input events: click, keypress
2. timers JS执行
  - 如事件处理函数
3. frame begin 帧开始。窗口尺寸变更，页面滚动等的处理
  - window resize
  - scroll
  - mediaquery changed
  - animation events
4. requestAnimationFrame(rAF)/IntersectionObserver callbacks
5. Layout
  - recalc style
  - update layout
  - ResizeObserver callbacks
6. Paint
  - compositing update
  - patint invalidation
  - record
- 上面六个步骤完成后没超过 16 ms，说明时间有富余，此时就会执行 `requestIdleCallback` 里注册的任务。
  - requestAnimationFrame 每一帧必定会执行，requestIdleCallback 是捡浏览器空闲来执行任务。
  - requestIdleCallback 可能不会执行

- 👉🏻 layout > `useLayoutEffect` > `requestAnimationFrame` > Update layer tree > paint > `useEffect`
  - [What's useEffect execution order and its internal clean-up logic when requestAnimationFrame and cancelAnimationFrame are used? - Stack Overflow](https://stackoverflow.com/questions/53781632)

- [浏览器渲染详细过程：重绘、重排和 composite 只是冰山一角 - 掘金](https://juejin.cn/post/6844903476506394638)
  - html5官方规范： [html5 event loop processing model](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)
1. 判断当前的document是否需要渲染，用官方规范的说法就是浏览器会判断这个document是否会从UI Render中获益，因为只需要保持60Hz的刷新率即可，而每轮event loop都是非常快的，所以没必要每轮loop都Render UI，而是差不多16ms的时候再Render
2. 触发resize事件
3. 触发scroll事件
4. 计算是否触发media query
5. 执行css animation和触发‘animationstart’等animation相关事件. run the fullscreen rendering steps：
6. 执行requestAnimationFrame的回调
7. 执行IntersectionObserver的回调，也许你在图片懒加载的逻辑里用过这个api。
8. 更新、渲染用户界面

- resize和scroll事件是在渲染流程里触发的
  - 这意味着如果你想在scroll事件上绑回调去执行动画，那么根本不需要用requestAnimationFrame去节流，scroll事件本身就是在每帧真正渲染前执行，自带节流效果！
  - 当然，滚动图片懒加载、滚动内容无限加载等业务逻辑而非动画逻辑还是需要throttle的。

- 一些低优先级的任务可使用 requestIdleCallback 等浏览器不忙的时候来执行，同时因为时间有限，它所执行的任务应该尽量是能够量化，细分的微任务（micro task）。
  - 因为它发生在一帧的最后，此时页面布局已经完成，所以不建议在 requestIdleCallback 里再操作 DOM，这样会导致页面再次重绘。DOM 操作建议在 rAF 中进行。
- Promise也不建议在这里面进行，因为 Promise 的回调属性 Event loop 中优先级较高的一种微任务，会在 requestIdleCallback 结束时立即执行，不管此时是否还有富余的时间，这样有很大可能会让一帧超过 16 ms。

- requestAnimationFrame(callback) 会在浏览器每次重绘前执行 callback 回调, 每次 callback 执行的时机都是浏览器刷新下一帧渲染周期的起点上。

- requestAnimationFrame 方法不同与 setTimeout 或 setInterval，它是由系统来决定回调函数的执行时机的，会请求浏览器在下一次重新渲染之前执行回调函数。
  - 无论设备的刷新率是多少，requestAnimationFrame 的时间间隔都会紧跟屏幕刷新一次所需要的时间
  - 需要注意的是这个方法虽然能够保证回调函数在每一帧内只渲染一次，但是如果这一帧有太多任务执行，还是会造成卡顿的；因此它只能保证重新渲染的时间间隔最短是屏幕的刷新时间。

- https://groups.google.com/a/chromium.org/g/blink-dev/c/j7YQtj0Yyxs?pli=1
  - Update Layer Tree is currently measuring two things:
    - Blink compositing update (decides which PaintLayers should be composited, allocates or clears their CompositedLayerMapping, creates and sets geometry and other properties of GraphicsLayers)
    - prepaint tree walk (issues paint invalidations on the layout objects, and builds paint property trees)
  - Update Layer is measuring some of the bookkeeping that occurs in between paint and commit (PictureLayer:: Update).  I think the main thing this is doing is copying paint ops out of the DrawingDisplayItem (which was created during paint) and into the PictureLayer's RecordingSource (so that the commit can transfer them into the PictureLayerImpl's RasterSource).
  - Composite Layers is actually the time that the main thread spends waiting for the commit to finish on the compositor thread.  I agree it should instead be named "Commit Layers".

- [When exactly are use(Layout)Effect hooks called? : reactjs](https://www.reddit.com/r/reactjs/comments/ms8qk5/when_exactly_are_uselayouteffect_hooks_called/)
  - useLayoutEffect is called on the requestAnimationFrame loop. Because requestAnimationFrame is synced with the browsers own refresh rate you can enter a state where the DOM has been committed but not painted.
# discuss-react-effect
- ## 💡 What will be logged in the console when this component is mounted?
- https://twitter.com/diegohaz/status/1662671157978447872
  - Note the usage of both layout and non-layout effects. StrictMode should be ignored.

- 测试表明
  - 事件函数如onClick中的microtask，会在effect前执行，且state值是setState前的值
  - layoutEffect中的microtask，会在effect后执行

```JS
// https://codepen.io/uptonking/pen/wvYZYam

function App() {
  const [on, setOn] = useState(false);

  useLayoutEffect(() => {
    console.log('a');
    queueMicrotask(() => console.log('b'));
    requestAnimationFrame(() => console.log('c'));

    setOn(true);
  }, [])

  useEffect(() => {
    // effect的执行时机在 queueMicrotask 和 requestAnimationFrame 前
    console.log(on);
  }, [on]);

  return (
    <button
        onClick={() => {
          console.log("click");
          queueMicrotask(() => console.log("b"));
          requestAnimationFrame(() => console.log("c"));

          setOn((v) => !v);
        }}
      >
        {`${on} `} click to setState
      </button>
  );
}

// a false true b c
// when click 
// click b false c 
```

- ## [New in 18: useEffect fires synchronously when it's the result of a discrete(离散的) input · reactwg/react-18](https://github.com/reactwg/react-18/discussions/128)
  - A discrete input is a type of event where the result of one event can affect the behavior of the next, like clicks or presses. Multiple discrete events cannot be batched or throttled without affecting program behavior.
    - A practical example where this matters is a counter. If the user increments a counter multiple times in quick succession, we must process each one individually so that the final count is correct.
    - In React 17 and below, the function passed to `useEffect` typically fires asynchronously after the browser has painted. The idea is to defer as much work as possible until paint so that the user experience is not delayed. This includes things like setting up subscriptions.
  - For example, if useEffect attaches an event listener, the listener is guaranteed to be added before the next input.
  - The same behavior applies to flushSync: the results of the effect are applied immediately, before the flushSync call exits.
  - The behavior for non-discrete events is unchanged: in most cases, React will defer the effect until after paint (though not always, if there's remaining time in the frame).
  - Note that this only affects the timing of when useEffect functions are called. It does not affect the priority of updates that are triggered inside a useEffect. They still get the default priority. (This is in contrast to useLayoutEffect, which not only calls the effect callback synchronously but also gives synchronous priority to its updates.)
# discuss
- ## 

- ## 

- ## 

- ## [How does the event loop in the browser deal with the event queue, job queue, render queue at the same time? - Stack Overflow](https://stackoverflow.com/questions/65456485/how-does-the-event-loop-in-the-browser-deal-with-the-event-queue-job-queue-ren)
- messages from other processes and previous tasks will queue new tasks in various task-sources, themselves ending in fewer task-queues. (This feeds the left loop of Jake's diagram).
- at each iteration, the first step of the event-loop is to pick the first task from one of these task-queues (chosen as they wish, this allows task prioritization).
- after this main task is completed (step 7 in the specs), the event loop will look at the microtask queue in what is called a microtask-checkpoint.
- only for the Documents where the active display monitor did emit its SYNC pulse since the last iteration (once every 16.67ms on a 60Hz monitor), it **updates the rendering** (right loop in Jake's diagram, steps 11.6~11.15 in the specs).
- During these steps it will execute a few tasks like firing UI events, updating animations and run the animation frame callbacks. Every time one of these algorithm invokes a callback, the user-agent has to perform a new microtask-checkpoint as per the clean up after running algorithm, so for instance every animation frame callback will get interleaved with such a checkpoint, and some of these algorithms even perform the microtask-checkpoint directly.

- So this means that the **microtask-checkpoint is not just executed in a single point** in the event loop, **it is executed once after the main task, and many times after each callback execution in the update the rendering steps**.

- The user-agent can not just delay the microtask, it has to execute it right after the task that queued it did complete, i.e, from the event loop perspective, microtasks are executed synchronously.

- In the same way, the "render queue" is not a task-queue either, it has to run when the browser has a "rendering opportunity", it can't be part of the task prioritization mechanism 

- ## [When will requestAnimationFrame be executed? - Stack Overflow](https://stackoverflow.com/questions/43050448/when-will-requestanimationframe-be-executed)
- The spec now says when this happens in the Event Loop Processing Model section. The shortened version with a lot of detail removed is:
- Do the oldest (macro) task
- Do microtasks
- If this is a good time to render:
  - Do some prep work
  - Run `requestAnimationFrame` callbacks
  - Render

- ## [Does requestAnimationFrame run between microstasks? - Stack Overflow](https://stackoverflow.com/questions/73477611/does-requestanimationframe-run-between-microstasks)
- microtask-queue is not a task queue.
- there is a priority system in the event-loop, the first step of the event-loop is to choose a task among all the possible task-queues. That's where the priority is set. We'll even soon be able to have control over it in the near future. 
  - However rAF has a special place in the event loop, it's not a task per se and thus doesn't participate in the prioritization system, it will get called as part of the event loop processing when the monitor sends its VSync signal. So it will slip in even a flow of highest priority tasks.
  - However, microtask aren't tasks, and the microtask queue doesn't work like a task queue. It will get emptied entirely before it comes back to the event loop, and **new microtask queued during the microtask-checkpoint will also get executed in that same checkpoint**. (To be noted, after each rAF callbacks you have a microtask-checkpoint, so you could even rewrite below example with one rAF callback firing before the blocking loop, and another firing after, both would participate in the same "rendering frame"). 

- ## queueMicrotask: executes synchronously after all layout effects have been executed
- https://twitter.com/sebastienlorber/status/1650829494209466373
  - I find this pattern useful in some very specific situations.

```JS
useLayoutEffect(
  () => {
    queueMicrotask(
      () => doSomething()
    )
  }
)
```

- 👀 Shh. You shouldn't have told people because now when someone else uses it to setState, they'll be after you in the queue. Only works well if you're the only one doing it.
  - is there a good use-case for queueMicrotask(setState) that someone uses?
- I use it to focus inputs after animating them in
- I feel like most developers don't know about queueMicrotask.
  - That's exactly how react batches all state updates. I just learned about this recently.
  - Probably i would make a thread or a blog post explaining about queueMicrotask (there are not so much of them out there)

- ## Did you know about queueMicrotask() in JavaScript? It's pretty handy.
- https://twitter.com/diegohaz/status/1530662445240426496
  - element.focus() may fire in the wrong order before finishing bubbling
  - queueMicrotask( ()=> element.focus())
- A microtask is essentially sync code that's pushed to the end of the current work (as if you've written it at the end of the script).
  - It's different from `setTimeout` (runs async after paint) and `requestAnimationFrame` (runs async right before paint).
- 👉🏻 Just a note: this is true for synthetic events like the ones in React. Native event bubbling runs after microtasks, so you would instead use something like this
- A promise that resolves immediately is the same as queueMicrotask:
  - Promise.resolve().then(callback)
  - setTimeout is totally different. It will happen after the browser paint.

- The update for forceUpdate is scheduled in a microtask between 1 and 3 in the microtask queue. When that update is processed, we see that it's from a discrete user event (click), and in that case we synchronously fire the effects.
  - If you're interested, the code that you linked to is where we schedule the update for the setState in a microtask. 
  - The place where we flush the effects synchronously if it's in a discrete update is here
- We use queueMicrotask in React to schedule sync updates at the end of the current event, such as updates inside clicks which you want to batch within the same event but process synchronously at the end before anything observes it

- queueMicrotask is not part of JavaScript but the HTML DOM API.

- Worth mentioning that it's essentially the same as Promise.resolve().then(...)
  - And you should not have infinite loops of microtasks or your app will hang, which is not the case with macrotasks because event loop

- Does async IIFE with early await has the same effect as queueMicrotask?

```JS
// State updates inside event handlers are now sync in React 18. So this will log 1, 2, 3
// I mean, as "sync" as microtasks are. Not the same as ReactDOM.flushSync().
// I'm not sure if this is guaranteed, though.

// - https://twitter.com/daniguardio_la/status/1531309444721692674
// effects (more like updates as a whole) do execute in microtasks, so it makes sense that they're executed between 1 and 3.

useEffect(() => log(2))

function onClick() {
  queueMicrotask(() => log(1))
  forceUpdate()
  queueMicrotask(() => log(3))
}
```

- ## [is requestAnimationFrame belong to microtask or macrotask in main thread task management?](https://stackoverflow.com/questions/70995372/is-requestanimationframe-belong-to-microtask-or-macrotask-in-main-thread-task-ma)
- Technically... neither. 
  - requestAnimationFrame (rAF)'s callbacks are ... callbacks.
- Only one of macrotasks will get executed per event-loop iteration, selected at the first step
  - Finally there are callbacks. These may be called from a task (e.g when the task is to fire an event), or in some particular event-loop iterations, called "painting frames".
- Indeed the step labelled update the rendering is to be called once in a while (generally when the monitor sent its V-Sync update), and will run a series of operations, calling callbacks, among which our dear rAF's callbacks.
- **rAF (and the other callbacks in the "painting frame"), have a special place in the event-loop where they may seem to be called with the highest priority**. 
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
