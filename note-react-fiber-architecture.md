---
title: note-react-fiber-architecture
tags: [react]
created: 2020-06-27T05:10:19.958Z
modified: 2020-07-14T11:58:47.593Z
---

# note-react-fiber-architecture

# guide

- 司徒正美分析fiber
  - [React Fiber架构](https://zhuanlan.zhihu.com/p/37095662)
  - [React Fiber在并发模式下的运行机制](https://zhuanlan.zhihu.com/p/54042084)
  - [React Fiber的优先级调度机制与事件系统](https://zhuanlan.zhihu.com/p/95443185)
- ref
  - [react fiber 主流程及功能模块梳理](https://juejin.im/post/6844903781805752328)
# blog

## [Fiber架构的心智模型](https://react.iamkasong.com/process/fiber-mental.html)

- 代数效应能够将副作用（例子中为请求图片数量）从函数逻辑中分离，使函数关注点保持纯粹。
- 从React15到React16，协调器（Reconciler）重构的一大目的是：将老的同步更新的架构变为异步可中断更新。
- 异步可中断更新可以理解为：更新在执行过程中可能会被打断（浏览器时间分片用尽或有更高优任务插队），当可以继续执行时恢复之前执行的中间状态。

- 其实，浏览器原生就支持类似的实现，这就是Generator。
- 但是**Generator的一些缺陷使React团队放弃了他**：
  - 类似async，Generator也是传染性的，使用了Generator则上下文的其他函数也需要作出改变。这样心智负担比较重。
  - Generator执行的中间状态是上下文关联的。
- 只考虑“单一优先级任务的中断与继续”情况下Generator可以很好的实现异步可中断更新。

- 但是当我们考虑“高优先级任务插队”的情况，如果此时已经完成doExpensiveWorkA与doExpensiveWorkB计算出x与y。
  - 如果通过全局变量保存之前执行的中间状态，又会引入新的复杂度。
- 基于这些原因，React没有采用Generator实现协调器。

- 每个任务更新单元为React Element对应的Fiber节点。

- A Fiber is essentially an incremental unit for rendering purposes. 
  - By breaking down what needs to be rendered and updated to the DOM, React is able to update the most important things first.
  - A fiber is a javascript object that contains data about the component as well as data about that component’s input and output. 
  - A fiber is both an instance of a component as well as frame in the call stack.
  - Fibers have both types and keys(for reconciliation), just like React elements. 

## [Fiber架构的工作原理](https://react.iamkasong.com/process/doublebuffer.html)

- 当我们用canvas绘制动画，每一帧绘制前都会调用ctx.clearRect清除上一帧的画面。
  - 如果当前帧画面计算量比较大，导致清除上一帧画面到绘制当前帧画面之间有较长间隙，就会出现白屏。
  - 为了解决这个问题，我们可以在内存中绘制当前帧动画，绘制完毕后直接用当前帧替换上一帧画面，由于省去了两帧替换间的计算时间，不会出现从白屏到出现画面的闪烁情况。
  - 这种在内存中构建并直接替换的技术叫做双缓存 (opens new window)。

- React使用“双缓存”来完成Fiber树的构建与替换——对应着DOM树的创建与更新。
- 在React中最多会同时存在两棵Fiber树。当前屏幕上显示内容对应的Fiber树称为current Fiber树，正在内存中构建的Fiber树称为workInProgress Fiber树。
- current Fiber树中的Fiber节点被称为current fiber，workInProgress Fiber树中的Fiber节点被称为workInProgress fiber，他们通过alternate属性连接。
- 当workInProgress Fiber树构建完成交给Renderer渲染在页面上后，应用根节点的current指针指向workInProgress Fiber树，此时workInProgress Fiber树就变为current Fiber树。

- Fiber节点组成Fiber树，页面中最多同时存在两棵Fiber树：
  - 代表当前页面状态的current Fiber树
  - 代表正在render阶段的workInProgress Fiber树
  - 在commit阶段完成页面渲染后，workInProgress Fiber树变为current Fiber树，workInProgress Fiber树内Fiber节点的updateQueue就变成current updateQueue

- https://twitter.com/acdlite/status/978696799757086720
  - So much of React's architecture is based on stuff game developers figured out decades ago.
  - Like double buffering. React has a current tree and a work-in-progress tree. When the WIP tree is finished rendering, we swap. The WIP becomes current.
  - Is it true that the entire WIP tree is rebuilt on every component render call?
    - No, we reuse the parts that don’t change
  - Interesting. The caveat about having two buffers, could structural sharing help with that on low memory devices or would that strategy itself use too much memory?
    - Yeah, we use structural sharing. The parts of the tree that don't change are reused.
    - We also swap back and forth between the same two fibers, so there are only two fiber allocations at most per component.
    - Nice. Reminds me of frame re-use in TCO recursion.

## [源码解析一 Fiber and FiberRoot](https://github.com/LuSuguru/fake-react/blob/master/doc/fiber-and-fiberRoot.md)

- 在v15的stack reconciler中，如果某个节点setState，会从当前节点开始，一直递归到整个dom树的最底层，找到需要修改的信息，并传递给renderer进行渲染。
  - 这整个过程在react中是通过递归实现，一气呵成，连续不可中断。
  - 如果需要渲染的组件树过于庞大，js执行占据主线程时间较长，导致页面响应度变差，就会很明显造成卡顿现象

- 为了解决这个问题，React重构了整个调和架构，称为新的fiber reconciler，它支持：
  - 能够把任务切片处理，拆分任务并能调度的能力
  - 对每个任务划分优先级，优先级通过事件判定，根据优先级不同分配到不同的 Task 中处理
  - 能够调整优先级，重置或者复用任务

- 每一个ReactElement，都会生成相应的工作单元（我们把每个工作单元称为Fiber），根据这些节点的层级关系，会生成整个Fiber树。
- FiberRoot是整个Fiber树的根节点，无论是更新还是渲染，都是从根节点开始的
- 在fiber reconciler中，在全局维护着一条关于FiberRoot的队列，如下图，每次在更新渲染时，都会更新当前 fiberRoot的优先级，并塞到任务队列的末尾
- Fiber是一个工作单元，由于一切的调度更新渲染都是围绕着它展开，在fiber reconciler下，操作是可以分成很多小部分，并且可以被中断的，所以同步操作DOM可能会导致Fiber树与实际DOM的不同步。对于每个节点，不光需要存储了对应元素节点的基本信息，还要保存一些用于任务调度的信息，以及跟周围节点的关系信息
- WorkInProgress 是Fiber进行调度时生成的一个副本，与Fiber通过alternate相互连接，
  - 由于现在的任务都是可中断的，如果直接在原树上操作，若此时需要中断，归还控制权，那么更新到一半的Fiber树该怎么办，保留，回滚? 为了解决这个问题，在Fiber reconciler中，Mount或者Update时，都会基于当前 Fiber树生成一棵新的WorkInProgress树（副本树），调度完成后用整个WorkInProgress树替代当前的Fiber树，成为当前的Fiber树

## [React Hooks(三): concurrency](https://zhuanlan.zhihu.com/p/99977314)

- Javascript 虽然是单线程语言，但是其仍然可以进行并发，比如 node.js 里日常使用的各种异步 api，都能帮我们编写并发的代码。
- 除了宿主环境提供的异步 IO，Javascript 还提供了一个另一个常被忽略的并发原语： 协程(Coroutine)
- 简单定义一下上下文相关的术语
  - 上下文：程序运行中的一个状态
  - 上下文切换：从一个上下文切换到另一个上下文的技术
  - 调度：决定哪个上下文可以获得cpu时间片的方法
- 进程是最传统的上下文系统
  - 每个进程都有独立的地址空间和资源句柄，每次新建进程时都需要分配新的地址空间和资源句柄（可以通过写时赋值进行节省），
  - 其好处是进程间相互隔离，一个进程 crash 通常不会影响另一个进程，坏处是开销太大
- 进程主要分为三个状态： 就绪态、运行态、睡眠态
  - 就绪和运行状态切换就是通过调度来实现，
  - 就绪态获取时间片则切换到运行态，运行态时间片到期或者主动让出时间片(sched_yield)就会切换到就绪态，
  - 当运行态等待某系条件（典型的就是 IO 或者锁）就会陷入睡眠态，条件达成就切换到就绪态。
- 线程是一种轻量级别的进程（linux 里甚至不区分进程和线程），
  - 和进程的区别主要在于，线程不会创建新的地址空间和资源描述符表，
  - 这样带来的好处就是开销明显减小，
  - 但是坏处就是因为公用了地址空间，可能会造成一个线程会污染另一个线程的地址空间，即一个线程 crash 掉，很可能造成同一进程下其他线程也 crash 掉
- 并发并不等于并行，并行需要多核的支持，并发却不需要。
  - 线程和进程既支持并发也支持并行
  - 并行强调的是充分发挥多核的计算优势，
  - 而并发更加强调的是任务间的协作，如 webpack 里的 uglify 操作是明显的 CPU 密集任务，在多核场景下使用并行有巨大的优势，而 n 个不同的生产者和 n 个不同消费者之间的协作，更强调的是并发。
  - 实际上我们绝大部分都是把线程和进程当做并发原语而非并行原语使用。
- 在 Python 没引入 asycio 支持前，绝大部分 python 应用编写网络应用都是使用多线程|多进程模型
  - 虽然使用了多线程，但是这里的多线程更多的是用于并发而非并行，
  - 其实我们的任务绝大部分时间都是耗在了 IO 等待上面，这时候你是单核还是多核对系统的吞吐率影响其实不大。
  - 由于多进程内存开销较大，在 C10k 的时候，其创建和关闭的内存开销已基本不可接受，
  - 而多线程虽然内存开销较多进程小了不少，但是却存在另一个性能瓶颈：调度
  - linux 在使用 CFS 调度器的情况下，其调度开销大约为 O(logm), 其中 m 为活跃上下文数，其大约等同于活跃的客户端数，
  - 因此每次线程遇到 IO 阻塞时，都会进行调度从而产生 O(logm)的开销。这在 QPS 较大的情况下是一笔不小的开销。
- 上面多线程网络模型的开销是由两个原因导致的：
  - IO 阻塞读写 socket 导致触发调度：调度频繁
  - 活跃上下文数目较大导致调度开销较大：调度效率低
- 使用事件驱动编程时碰到的一个问题是，我们的业务逻辑被拆散为一个个的 callback 上下文，且借助于闭包的性质，我们可以方便的在各个 callback 之间传递状态，然后由 runtime(比如 node.js 或者 nginx 等）根据事件的触发来执行上下文切换。
- 假如我们的函数支持多个入口，这样就可以将上次回调的记过自然的保存在函数闭包里，从下个入口进入这个函数可以自然的通过闭包访问上次回调执行的状态，即我们需要一个可唤醒可中断的对象，这个可唤醒可中断的对象就是 coroutine。
- coroutine 具有如下两个重要性质
  - 可唤醒可中断的函数
  - 不可抢占
- Generator 和 Async/Await 就是 coroutine 的一种实现。
  - Generator 刚开始只是作为简化 Iterableiterator 的实现，后来渐渐的在此之上加上了 coroutine 的功能。
  - 虽然我们的 callee 可以主动的让出时间片，但是下一个调度的对象并不是随机选择的，下一个调度的对象必然是 caller，这是一个很大的局限
- 上面讲到 Generator 的最大限制在于 coroutine 只能 yield 给 caller，这在实际应用中存在较大的局限，
  - 例如一般的调度器是根据优先级进行调度，这个优先级可能是任务的触发顺序也有可能是任务本身手动指定的优先级，
  - 考虑到大部分的 web|server 应用，绝大部分场景都是处理异步任务，所以如果能内置异步任务的自动调度，那么基本上可以满足大部分的需求。
- 虽然 async/await 异常方便，但是仍然存在诸多限制
  - 必须在 async 函数里才能使用 yield(await), async 函数存在向上的传染性，导致自顶向上都需要改成 async 函数
  - 不支持优先级调度：其调度规则是内置的按照事件触发顺序进行调度，实际应用中可能需要根据优先级进行调度
- React Fiber： 框架层控制的支持同步任务和优先级的协程
  - 事实上 React Fiber 是另一种协程的实现方式
  - fiber大部分情况下和coroutine的功能相同均支持cooperative multitasking，
  - 主要的区别在于 fiber 更多的是系统级别的，而 coroutine 则更多的是 userland 级别的
  - 由于 React 并没有直接暴露操作 suspend 和 resume 的操作，更多的是在框架级别进行 coroutine 的调度，因此叫 fiber 可能更为合理

## [React Fiber架构如何从JS引擎手中“夺回”调度权](https://segmentfault.com/a/1190000020110045)

- React 16采用新的Fiber架构对React进行完全重写，同时保持向后兼容。
- concurrent rendering 又叫 async rendering，主要包含2个特性
  - time slicing（分片）
    - 为了让浏览器保持60fps，渲染一帧需要在16.67ms内完成，否则会造成“卡顿”
    - time slicing将渲染工作切分，保证JavaScript的执行不会造成卡顿
    - 如果当前帧的时间片已经用完，React就将控制权交还给浏览器，剩下的工作等到下一帧再做
    - 另一个作用是，将渲染工作按重要性来排序，提高时间敏感（time-sensitive）渲染的优先级（比如text input）
  - suspense
    - 让任何一个组件能够暂停渲染，等待数据的获取（比如懒加载组件、比如网络请求数据）
  - 这两个特性的关键前提是：React的渲染能够被中止（interrupt）、恢复。

- 背景：JavaScript的执行模型：call stack
- 首先，我们先解释，为什么过去的架构无法支持渲染中止。
- JavaScript原生的执行模型：通过调用栈来管理函数执行状态。
  - 其中每个栈帧表示一个工作单元（a unit of work），存储了函数调用的返回指针、当前函数、调用参数、局部变量等信息。
  - 因为JavaScript的执行栈是由引擎管理的，执行栈一旦开始，就会一直执行，直到执行栈清空。无法按需中止。
- React将视图看做函数调用的结果：`View = Component(Data)`
  - Component会递归调用其他的Component，若页面复杂的话，这个调用栈会很深，导致UI变卡。
  - 在React Fiber之前，React的渲染就是使用原生执行栈来管理组件树的递归渲染。
  - 这意味着，整颗组件树的渲染必须一次性完成，工作无法被分片。
- React Fiber架构就是用JavaScript来实现的执行模型。
  - 可以将它比作由react管理的“调用栈”，一个fiber与一个函数栈帧非常类似，它们都表示一个工作单元（a unit of work）。
  - 一个组件实例对应一个Fiber。
  - React Fiber是使用JavaScript实现的，这意味着它的底层依然是JavaScript调用栈。
- React Fiber与调用栈的区别：
  - React Fiber是链表结构，过去的递归调用变成了对fiber的链表遍历。
    - fiber不仅有return指针，还有child、sibling指针，有这三个指针的链表就能够实现深度优先遍历。
  - 另一个区别是，栈帧在函数返回以后就销毁了，而fiber会在渲染结束以后继续存在，保存组件实例的信息（比如state）
- Fiber的英文含义就是“纤维”，意指比Thread更细的线，寓意它是比线程(Thread)控制得更精密的执行模型
  - 一个fiber执行完自己的工作以后，会主动让出控制权，不会主宰（dominate）整个程序的执行。
- 协程（Coroutines）基本是相同的概念，它们的区别微乎其微。
  - 说白了，React Fiber就是用JavaScript实现的一种协程模型。
- React Fiber就是React自己实现的底层执行模型。
  - 得益于自主掌控的底层执行模型，React能够在这个执行模型之上实现更多的编程模式，而不必受到过多来自JavaScript语言的约束
  - 随时暂停、恢复渲染
  - 进行并发渲染：一个渲染还没有完成就开始另一个渲染，并控制各个渲染的优先级
  - componentDidCatch
  - Suspense
  - Algebraic Effects，以及基于它的React hooks编程模式，Algebraic Effects为一个组件（一个纯函数）提供了一个运行时的上下文：组件树中的一个组件实例
- 与Fiber相反，JS原生调用栈则不可控、不协作（non-cooperative）
  - 如果函数不断地递归调用，那么它就会主宰整个程序，后续的工作（比如浏览器paint）必须等待它执行完成。
- 为什么不使用generator来实现协作式调度
  - generator函数也能够主动让出程序控制权（generator函数本质就是协程），理论上用它也能够实现concurrent rendering。
  - 那为什么react不使用generator函数而是自己实现Fiber呢？
  - 如果React全面使用generator，那么React内部的调度逻辑、用户编写的所有组件都是generator，这会给用户增加心智负担，
  - 并且大量使用generator会有不小的性能开销，过于依赖执行引擎的优化；
  - Fiber架构能够更加灵活地让React从任意一个Fiber恢复执行（不只是从上次中断的地方恢复，而且能够从更早的Fiber恢复），
  - 而generator函数只能回到之前的yield状态，不能回到更早的执行状态。
- React Fiber的更新过程被分为两个阶段(Phase)：第一阶段Render Phase；第二阶段Commit Phase。
  - 在第一阶段Render Phase，React Fiber会找出需要更新哪些DOM，这个阶段是可以被打断的，甚至可以中途放弃
  - 但是到了第二阶段Commit Phase，就必须一鼓作气把DOM更新完，绝不会被打断。

- React，它掌控调度权的方式是：
  - 一方面，用链表的方式来遍历组件树，避免使用原生调用栈（原生的函数递归无法被打断）；
  - 另一方面，允许组件通过throw Promise的方式来将控制权交还调度器。
- React掌控了调度权以后，也自己设计了一些异步原语，让用户用同步的方式编写异步代码，而不需要依赖js本身的generator机制
  - 一个React异步原语是React.lazy，通过它来定义的异步数据（即代码）也能像同步数据一样被消费，就好像LazyComponent从一开始就存在一样
- 既然generator是js原生提供的协程模型，支持控制权的交出与恢复，那么它理论上也能用来实现React Fiber架构
  - redux-saga就是利用调度权来实现异步编程范式的一个先例，它通过强迫用户使用generator函数来掌控调度权
- React团队当然考虑过这个方案，但是最终因为以下原因放弃：
  - 语法负担重、心智负担重，看看大家是怎么吐槽redux-saga的。
  - 目前typescript对于generator函数的类型推导能力很弱。
    - const result = yield value result的类型总是any。
    - 这个缺陷在过去就对redux-saga造成了很大影响。 
  - 性能负担重，过于依赖于执行引擎的优化。
    - generator function就像异步函数一样，是有传染性的，所有的React组件、hooks都必须使用generator来实现。
    - 一个中小型应用运行时就可能同时存在就成百上千个generator实例，这对于执行引擎提出了巨大的优化挑战。
  - generator只能从上次yield的地方恢复，而fiber还能从过去的某个状态恢复。

- 确实 fiber 等优化可以在 js 引擎层面做，但主流的 js 引擎不会去做，因为它们也要恰饭的，首先考虑的往往是标准

- Generator主要的问题不就是没法记录多个断点。。
  - Iterator返回一次，断点就会变更为下一个，这样的话等你渲染完，还怎么返回hook断点来异步更新。
  - 而Fiber是链表上的节点，组件可以记录当前执行位置用于后续返回。
  - React保持组件纯度和副作用隔离一部分原因是为了SSR。
# dev
- The Fiber architecture can solve blocking (and a host of other problems) because Fiber made it possible to split reconciliation and rendering to the DOM into two separate phases.
  - Phase 1 is called Render/Reconciliation.
  - Phase 2 is called Commit.
- In phase 1, React is called to render new and/or updated components
  - React will schedule the work to be done (changes to be rendered) by creating a list of changes (called an effect list) that will be executed in the Commit phase. 
  - React will fully compute this list of changes before the second phase is executed.
  - After collecting the render output from the entire component tree, React will diff the new tree (the virtual DOM) with the current DOM tree and collect the list of changes that need to be made to the DOM to produce the desired UI structure. 
- In phase 2, React actually tells the DOM to render the effect list created in phase one.
- The Reconciliation/Render phase can be interrupted, but the Commit phase cannot, and it's only in the Commit phase that React will actually render to the DOM.
- ref
  - https://dev.to/afairlie/to-understand-react-fiber-you-need-to-know-about-threads-3dof
  - https://kentcdodds.com/blog/fix-the-slow-render-before-you-fix-the-re-render
