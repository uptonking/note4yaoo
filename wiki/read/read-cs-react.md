---
title: read-cs-react
tags: [cs, react, read]
created: 2021-09-22T13:14:22.482Z
modified: 2021-09-22T13:14:36.958Z
---

# read-cs-react

# [React技术揭秘__卡颂](https://react.iamkasong.com/)

## react理念

- 从官网看React的理念
  - A JavaScript library for building user interfaces
- 关键是实现快速响应。那么制约快速响应的因素是什么呢？
  - 当遇到大计算量的操作或者设备性能不足使页面掉帧，导致卡顿。
  - 发送网络请求后，由于需要等待数据返回才能进一步操作导致不能快速响应。
- 这两类场景可以概括为：CPU的瓶颈、IO的瓶颈

- 当项目变得庞大、组件数量繁多时，就容易遇到CPU的瓶颈。
  - JS可以操作DOM，GUI渲染线程与JS线程是互斥的。所以JS脚本执行和浏览器布局、绘制不能同时执行。
  - 在浏览器每一帧的时间中，预留一些时间给JS线程，React利用这部分时间更新组件（可以看到，在源码中，预留的初始时间是5ms）
  - 当预留的时间不够用时，React将线程控制权交还给浏览器使其有时间渲染UI，React则等待下一帧时间到来继续被中断的工作。
  - 这种将长任务分拆到每一帧中，一次执行一小段任务的操作，被称为时间切片（time slice）
  - 解决CPU瓶颈的关键是实现时间切片，而时间切片的关键是：将同步的更新变为可中断的异步更新。

- IO的瓶颈
  - 网络延迟是前端开发者无法解决的。如何在网络延迟客观存在的情况下，减少用户对网络延迟的感知？
  - React给出的答案是将人机交互研究的结果整合到真实的 UI 中
  - 当“这一小段时间”足够短时，用户是无感知的。如果请求时间超过一个范围，再显示loading的效果
  - 为此，React实现了Suspense功能及配套的hook——useDeferredValue
  - 而在源码内部，为了支持这些特性，同样需要将同步的更新变为可中断的异步更新

## react v15 架构

- 分为两层
  - Reconciler（协调器）—— 负责找出变化的组件
  - Renderer（渲染器）—— 负责将变化的组件渲染到页面上
- Reconciler。每当有更新发生时，Reconciler会
  - 调用函数组件、或class组件的render方法，将返回的JSX转化为虚拟DOM
  - 将虚拟DOM和上次更新时的虚拟DOM对比
  - 通过对比找出本次更新中变化的虚拟DOM
  - 通知Renderer将变化的虚拟DOM渲染到页面上

- Renderer。浏览器环境ReactDOM
  - 在每次更新发生时，Renderer接到Reconciler通知，将变化的组件渲染在当前宿主环境。

- v15架构缺点
  - 在Reconciler中，mount的组件会调用mountComponent，update的组件会调用updateComponent (opens new window)。这两个方法都会递归更新子组件
- 递归更新的缺点
  - 由于递归执行，所以更新一旦开始，中途就无法中断。
  - 当层级很深时，递归更新时间超过了16ms，用户交互就会卡顿。

## react v16 架构

- 分为三层
  - Scheduler（调度器）—— 调度任务的优先级，高优任务优先进入Reconciler
  - Reconciler（协调器）—— 负责找出变化的组件
  - Renderer（渲染器）—— 负责将变化的组件渲染到页面上

- Scheduler
  - 既然我们以浏览器是否有剩余时间作为任务中断的标准，那么我们需要一种机制，当浏览器有剩余时间时通知我们。
  - 其实部分浏览器已经实现了这个API，这就是requestIdleCallback
  - 但是由于以下因素，React放弃使用：
    - 浏览器兼容性不够高，safari、ie不支持
    - 触发频率不稳定，受很多因素影响。比如当我们的浏览器切换tab后，之前tab注册的requestIdleCallback触发的频率会变得很低
  - 基于以上原因，React实现了功能更完备的requestIdleCallback polyfill，这就是Scheduler。

- Reconciler
  - v15中Reconciler是递归处理虚拟DOM的
  - v16更新工作从递归变成了可以中断的循环过程。每次循环都会调用shouldYield判断当前是否有剩余时间。
  - 在React16中，Reconciler与Renderer不再是交替工作。
  - 当Scheduler将任务交给Reconciler后，Reconciler会为变化的虚拟DOM打上代表增/删/更新的标记
  - 整个Scheduler与Reconciler的工作都在内存中进行。只有当所有组件都完成Reconciler的工作，才会统一交给Renderer。

- Renderer
  - Renderer根据Reconciler为虚拟DOM打的标记，同步执行对应的DOM操作。

- 由于Scheduler和Reconciler都是平台无关的，所以React为他们单独发了一个包react-Reconciler。你可以用这个包自己实现一个ReactDOM

## fiber起源

- 在React中做的就是践行代数效应（Algebraic Effects）
  - 代数效应是函数式编程中的一个概念，用于将副作用从函数调用中分离。
- async await是有传染性的 —— 当一个函数变为async后，这意味着调用他的函数也需要是async
- 代数效应与React有什么关系呢？最明显的例子就是Hooks
  - 对于类似useState、useReducer、useRef这样的Hook，我们不需要关注FunctionComponent的state在Hook中是如何保存的，React会为我们处理
  - 如果这个例子还不够明显，可以看看官方的Suspense Demo，Demo中完全是同步的写法
- 异步可中断更新可以理解为：更新在执行过程中可能会被打断（浏览器时间分片用尽或有更高优任务插队），当可以继续执行时恢复之前执行的中间状态。
  - 这就是代数效应中try...handle的作用。
  - 其实，浏览器原生就支持类似的实现，这就是Generator。

- 但是Generator的一些缺陷使React团队放弃了他：
  - 类似async，Generator也是传染性的，使用了Generator则上下文的其他函数也需要作出改变。这样心智负担比较重。
  - Generator执行的中间状态是上下文关联的，所以计算y时无法复用之前已经计算出的x，需要重新计算。如果通过全局变量保存之前执行的中间状态，又会引入新的复杂度。
  - 基于这些原因，React没有采用Generator实现协调器。

- Fiber并不是计算机术语中的新名词，他的中文翻译叫做纤程，与进程（Process）、线程（Thread）、协程（Coroutine）同为程序执行过程。
  - 在很多文章中将纤程理解为协程的一种实现。在JS中，协程的实现便是Generator。
- 可以将纤程(Fiber)、协程(Generator)理解为代数效应思想在JS中的体现。
- React Fiber可以理解为：
  - React内部实现的一套状态更新机制。支持任务不同优先级，可中断与恢复，并且恢复后可以复用之前的中间状态。
  - 其中每个任务更新单元为React Element对应的Fiber节点。

## fiber原理

- 虚拟DOM在React中有个正式的称呼——Fiber，用Fiber来取代React16虚拟DOM这一称呼。
- Fiber的含义
  - 作为架构来说，之前React15的Reconciler采用递归的方式执行，数据保存在递归调用栈中，所以被称为stack Reconciler。React16的Reconciler基于Fiber节点实现，被称为Fiber Reconciler。
  - 作为静态的数据结构来说，每个Fiber节点对应一个React element，保存了该组件的类型（函数组件/类组件/原生组件...）、对应的DOM节点等信息。
  - 作为动态的工作单元来说，每个Fiber节点保存了本次更新中该组件改变的状态、要执行的工作（需要被删除/被插入页面中/被更新...）。
- 每个Fiber节点有个对应的React element，多个Fiber节点是如何连接形成树呢？
  - fiber.child/sibling/return(parent)
- 为什么父级指针叫做return而不是parent或者father呢？
  - 因为作为一个工作单元，return指节点执行完completeWork后会返回的下一个节点。
  - 子Fiber节点及其兄弟节点完成工作后会返回其父级节点，所以用return指代父级节点

- 在内存中构建并直接替换的技术叫做双缓存
  - 当我们用canvas绘制动画，每一帧绘制前都会调用ctx.clearRect清除上一帧的画面。如果当前帧画面计算量比较大，导致清除上一帧画面到绘制当前帧画面之间有较长间隙，就会出现白屏。为了解决这个问题，我们可以在内存中绘制当前帧动画，绘制完毕后直接用当前帧替换上一帧画面，由于省去了两帧替换间的计算时间，不会出现从白屏到出现画面的闪烁情况。
  - React使用“双缓存”来完成Fiber树的构建与替换——对应着DOM树的创建与更新。

- 在React中最多会同时存在两棵Fiber树。当前屏幕上显示内容对应的Fiber树称为current Fiber树，正在内存中构建的Fiber树称为workInProgress Fiber树。
  - current Fiber树中的Fiber节点被称为current fiber，workInProgress Fiber树中的Fiber节点被称为workInProgress fiber，他们通过`alternate`属性连接。
- React应用的根节点通过使current指针在不同Fiber树的rootFiber间切换来完成current Fiber树指向的切换。
  - 即当workInProgress Fiber树构建完成交给Renderer渲染在页面上后，应用根节点的current指针指向workInProgress Fiber树，此时workInProgress Fiber树就变为current Fiber树。
  - 每次状态更新都会产生新的workInProgress Fiber树，通过current与workInProgress的替换，完成DOM更新。
- mount时
  - 首次执行ReactDOM.render会创建fiberRootNode（源码中叫fiberRoot）和rootFiber。
  - 其中fiberRootNode是整个应用的根节点，rootFiber是`<App/>`所在组件树的根节点。
  - 之所以要区分fiberRootNode与rootFiber，是因为在应用中我们可以多次调用ReactDOM.render渲染不同的组件树，他们会拥有不同的rootFiber。但是整个应用的根节点只有一个，那就是fiberRootNode。
  - 接下来进入render阶段，根据组件返回的JSX在内存中依次创建Fiber节点并连接在一起构建Fiber树，被称为workInProgress Fiber树
  - 在构建workInProgress Fiber树时会尝试复用current Fiber树中已有的Fiber节点内的属性
  - 已构建完的workInProgress Fiber树在commit阶段渲染到页面
- update时
  - 触发状态改变，这会开启一次新的render阶段并构建一棵新的workInProgress Fiber 树。
  - 和mount时一样，workInProgress fiber的创建可以复用current Fiber树对应的节点数据。
  - 这个决定是否复用的过程就是Diff算法
  - workInProgress Fiber 树在render阶段完成构建后进入commit阶段渲染到页面上
  - 渲染完毕后，workInProgress Fiber 树变为current Fiber 树。
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
  - 

## 深入理解jsx

- JSX在编译时会被Babel编译为`React.createElement`方法
  - JSX并不是只能被编译为`React.createElement`方法，你可以通过`@babel/plugin-transform-react-jsx` 插件显式告诉Babel编译时需要将JSX编译为什么函数的调用（默认为`React.createElement`）。
- JSX是一种描述当前组件内容的数据结构，他不包含组件schedule、reconcile、render所需的相关信息
- 比如如下信息就不包括在JSX中：
  - 组件在更新中的优先级
  - 组件的state
  - 组件被打上的用于Renderer的标记
  - 这些内容都包含在Fiber节点中。

- 所以，在组件mount时，Reconciler根据JSX描述的组件内容生成组件对应的Fiber节点。
- 在update时，Reconciler将JSX与Fiber节点保存的数据对比，生成组件对应的Fiber节点，并根据对比结果为Fiber节点打上标记

## render phase

- render阶段开始于`performSyncWorkOnRoot`或`performConcurrentWorkOnRoot`方法的调用。这取决于本次更新是同步更新还是异步更新。
- workLoopSync/workLoopConcurrent唯一的区别是是否调用shouldYield
  - 如果当前浏览器帧没有剩余时间，shouldYield会中止循环，直到浏览器有空闲时间后再继续遍历。
- performUnitOfWork方法会创建下一个Fiber节点并赋值给workInProgress，并将workInProgress与已创建的Fiber节点连接起来构成Fiber树。
- Fiber Reconciler是从Stack Reconciler重构而来，通过遍历的方式实现可中断的递归，所以performUnitOfWork的工作可以分为两部分
- 首先从rootFiber开始向下深度优先遍历。为遍历到的每个Fiber节点调用beginWork方法
  - 该方法会根据传入的Fiber节点创建子Fiber节点，并将这两个Fiber节点连接起来。
  - 当遍历到叶子节点（即没有子组件的组件）时就会进入下一阶段。
- 调用completeWork 处理Fiber节点
  - 当某个Fiber节点执行完completeWork，如果其存在兄弟Fiber节点（即fiber.sibling !== null），会进入其兄弟Fiber的“递”阶段。
  - 如果不存在兄弟Fiber，会进入父级Fiber的“归”阶段

## commit phase

- commitRoot方法是commit阶段工作的起点。
- 在rootFiber.firstEffect上保存了一条需要执行副作用的Fiber节点的单向链表effectList，这些Fiber节点的updateQueue中保存了变化的props。
  - 这些副作用对应的DOM操作在commit阶段执行。
  - 除此之外，一些生命周期钩子（比如componentDidXXX）、hook（比如useEffect）需要在commit阶段执行。
- commit阶段的主要工作（即Renderer的工作流程）分为三部分：
  - before mutation阶段（执行DOM操作前）
  - mutation阶段（执行DOM操作）, 根据effectTag调用不同的处理函数处理Fiber。
  - layout阶段（执行DOM操作后
- 在before mutation阶段之前和layout阶段之后还有一些额外工作，涉及到比如useEffect的触发、优先级相关的重置、ref的绑定/解绑。

## diff算法

- React文档中提到，即使在最前沿的算法中，将前后两棵树完全比对的算法的复杂程度为 O(n 3 )，其中n是树中元素的数量
- 为了降低算法复杂度，React的diff会预设三个限制：
  - 只对同级元素进行Diff。如果一个DOM节点在前后两次更新中跨越了层级，那么React不会尝试复用
  - 两个不同类型的元素会产生出不同的树。如果元素由div变为p，React会销毁
  - 开发者可以通过 key prop来提示哪些子元素在不同的渲染下能保持稳定
- React团队发现，在日常开发中，相较于新增和删除，更新组件发生的频率更高。所以Diff会优先判断当前节点是否属于更新

> 在我们做数组相关的算法题时，经常使用双指针从数组头和尾同时遍历以提高效率，但是这里却不行。

- 虽然本次更新的JSX对象newChildren为数组形式，但是和newChildren中每个组件进行比较的是current fiber，同级的Fiber节点是由sibling指针链接形成的单链表，即不支持双指针遍历。
  - 即newChildren[0]与fiber比较，newChildren[1]与fiber.sibling比较。 所以无法使用双指针优化。
- Diff算法的整体逻辑会经历两轮遍历：
  - 第一轮遍历：处理更新的节点。
  - 第二轮遍历：处理剩下的不属于更新的节点

## 状态更新

- 在React中，有如下方法可以触发状态更新（排除SSR相关）：
  - ReactDOM.render
  - this.setState
  - this.forceUpdate
  - useState
  - useReducer
- 这些方法调用的场景各不相同，他们是如何接入同一套状态更新机制呢？
  - 每次状态更新都会创建一个保存更新状态相关内容的对象，我们叫他Update。
  - 在render阶段的beginWork中会根据Update计算新的state。
- render阶段是从rootFiber开始向下遍历。那么如何从触发状态更新的fiber得到rootFiber呢？
  - 调用markUpdateLaneFromFiberToRoot方法。
  - 该方法做的工作可以概括为：从触发状态更新的fiber一直向上遍历到rootFiber，并返回rootFiber。
  - 由于不同更新优先级不尽相同，所以过程中还会更新遍历到的fiber的优先级。
- 梳理下状态更新的整个调用路径的关键节点
  - 触发状态更新（根据场景调用不同方法）
  - 创建Update对象
  - 从fiber到root（`markUpdateLaneFromFiberToRoot`）
  - 调度更新（`ensureRootIsScheduled`）
  - render阶段（`performSyncWorkOnRoot` 或 `performConcurrentWorkOnRoot`）
  - commit阶段（`commitRoot`）
- 状态更新流程开始后首先会创建Update对象
  - 由于不同类型组件工作方式不同，所以存在两种不同结构的Update，其中ClassComponent与HostRoot共用一套Update结构，FunctionComponent单独使用一种Update结构。
  - 虽然他们的结构不同，但是他们工作机制与工作流程大体相同
- ClassComponent与HostRoot（即rootFiber.tag对应类型）共用同一种Update结构。
  - 类似于Fiber节点组成Fiber树，Fiber节点上的多个Update会组成链表并被包含在fiber.updateQueue中。

- React通过Scheduler调度任务。
  - 具体到代码，每当需要调度任务时，React会调用Scheduler提供的方法runWithPriority。
  - 该方法接收一个优先级常量与一个回调函数作为参数。回调函数会以优先级高低为顺序排列在一个定时器中并在合适的时间触发。
- 优先级最终会反映到update.lane变量上。当前我们只需要知道这个变量能够区分Update的优先级。

- ReactDOM.render的流程
  - 创建fiberRootNode、rootFiber、updateQueue（`legacyCreateRootFromDOMContainer`）
  - 创建Update对象（`updateContainer`）
  - 从fiber到root（`markUpdateLaneFromFiberToRoot`）
  - 调度更新（`ensureRootIsScheduled`）
  - render阶段（`performSyncWorkOnRoot` 或 `performConcurrentWorkOnRoot`）
  - commit阶段（`commitRoot`）

## hooks理念

- React的架构遵循schedule - render - commit的运行流程，这个流程是React世界最底层的运行规律
  - ClassComponent作为React世界的原子，他的生命周期（componentWillXXX/componentDidXXX）是为了介入React的运行流程而实现的更上层抽象，这么做是为了方便框架使用者更容易上手
  - 相比于ClassComponent的更上层抽象，Hooks则更贴近React内部运行的各种概念（state | context | life-cycle）。

## 极简hooks实现

- 这些update是如何组合在一起呢？
  - 他们会形成环状单向链表。
  - 调用updateNum实际调用的是dispatchAction.bind(null, hook.queue)
  - 你可以照着这个例子模拟插入多个update的情况，会发现queue.pending始终指向最后一个插入的update。
  - 这样做的好处是，当我们要遍历update时，queue.pending.next指向第一个插入的update。
- 更新产生的update对象会保存在queue中
- 不同于ClassComponent的实例可以存储数据，对于FunctionComponent，queue存储在哪里呢？
  - FunctionComponent对应的fiber中。fiber.memoizedState中保存的Hook的数据结构
- Hook与update类似，都通过链表连接。不过Hook是无环的单向链表。
  - 每个useState对应一个hook对象。
- 在组件render时，每当遇到下一个useState，我们移动workInProgressHook的指针。
  - 这样，只要每次组件render时useState的调用顺序及数量保持一致，那么始终可以通过workInProgressHook找到当前useState对应的hook对象。

- React Hooks没有使用isMount变量，而是在不同时机使用不同的dispatcher。
  - 换言之，mount时的useState与update时的useState不是同一个函数。
- React Hooks有中途跳过更新的优化手段。
- React Hooks有batchedUpdates，当在click中触发三次updateNum，精简React会触发三次更新，而React只会触发一次。
- React Hooks的update有优先级概念，可以跳过不高优先的update。

## hooks数据结构

- 在真实的Hooks中，组件mount时的hook与update时的hook来源于不同的对象，这类对象在源码中被称为dispatcher。
- hook与FunctionComponent fiber都存在memoizedState属性，不要混淆他们的概念。
  - fiber.memoizedState：FunctionComponent对应fiber保存的Hooks链表。
  - hook.memoizedState：Hooks链表中保存的单一hook对应的数据。

- useState只是预置了reducer的useReducer。

## useEffect

- 在flushPassiveEffects方法内部会从全局变量rootWithPendingPassiveEffects获取effectList。
- flushPassiveEffects内部会设置优先级，并执行flushPassiveEffectsImpl
- flushPassiveEffectsImpl主要做三件事：
  - 调用该useEffect在上一次render时的销毁函数
  - 调用该useEffect在本次render时的回调函数
  - 如果存在同步任务，不需要等待下次事件循环的宏任务，提前执行他

- useEffect的执行需要保证所有组件useEffect的销毁函数必须都执行完后才能执行任意一个组件的useEffect的回调函数。这是因为多个组件间可能共用同一个ref。
- 阶段二：回调函数的执行
  - 其中向pendingPassiveHookEffectsMount中push数据的操作同样发生在schedulePassiveEffects中。

## useRef

- HostComponent在commit阶段的mutation阶段执行DOM操作。
  - 所以，对应ref的更新也是发生在mutation阶段。
  - 再进一步，mutation阶段执行DOM操作的依据为effectTag。
- ref的工作流程可以分为两部分：
  - render阶段为含有ref属性的fiber添加Ref effectTag
  - commit阶段为包含Ref effectTag的fiber执行对应操作
- 在render阶段的beginWork与completeWork中有个同名方法markRef用于为含有ref属性的fiber增加Ref effectTag。
- 在commit阶段的mutation阶段中，对于ref属性改变的情况，需要先移除之前的ref。
- 在mutation阶段，对于Deletion effectTag的fiber（对应需要删除的DOM节点），需要递归他的子树，对子孙fiber的ref执行类似commitDetachRef的操作。

## Concurrent

- 要实现Concurrent Mode，最关键的一点是：实现异步可中断的更新。
  - 如果我们同步运行Fiber架构（通过ReactDOM.render），则Fiber架构与重构前并无区别。
- 要实现Concurrent Mode，最关键的一点是：实现异步可中断的更新。
  - 基于当前的架构，当一次更新在运行过程中被中断，过段时间再继续运行，这就是“异步可中断的更新”。
  - 当一次更新在运行过程中被中断，转而重新开始一次新的更新，我们可以说：后一次更新打断了前一次更新
- 多个优先级之间如何互相打断？优先级能否升降？本次更新应该赋予什么优先级？
  - 这就需要一个模型控制不同优先级之间的关系与行为，于是lane模型诞生了。
- batchedUpdates在很早的版本就存在了，不过之前的实现局限很多（脱离当前上下文环境的更新不会被合并）。
  - 在Concurrent Mode中，是以优先级为依据对更新进行合并的，使用范围更广。
  - Suspense内的组件子树比组件树的其他部分拥有更低的优先级

## Scheduler的原理与实现

- 时间切片的本质是模拟实现requestIdleCallback
  - requestIdleCallback是在“浏览器重排/重绘”后如果当前帧还有空余时间时被调用的。
- Scheduler的时间切片功能是通过task（宏任务）实现的
  - 最常见的task当属setTimeout了。但是有个task比setTimeout执行时机更靠前，那就是MessageChannel
  - 所以Scheduler将需要被执行的回调函数作为MessageChannel的回调执行。如果当前宿主环境不支持MessageChannel，则使用setTimeout。
- 在React的render阶段，开启Concurrent Mode时，每次遍历前，都会通过Scheduler提供的shouldYield方法判断是否需要中断遍历，使浏览器有时间渲染
- 是否中断的依据，最重要的一点便是每个任务的剩余时间是否用完。在Scheduler中，为任务分配的初始剩余时间为5ms。
- 在React内部凡是涉及到优先级调度的地方，都会使用unstable_runWithPriority。
- commit阶段是同步执行的。可以看到，commit阶段的起点commitRoot方法的优先级为ImmediateSchedulerPriority。

## lane模型

- Scheduler与React是两套优先级机制。在React中，存在多种使用不同优先级的情况
- React需要设计一套满足如下需要的优先级机制：
  - 可以表示优先级的不同
  - 可能同时存在几个同优先级的更新，所以还得能表示批的概念
  - 方便进行优先级相关计算
- 为了满足如上需求，React设计了lane模型。
- lane模型借鉴了同样的概念，使用31位的二进制表示31条赛道，位数越小的赛道优先级越高，某些相邻的赛道拥有相同优先级
