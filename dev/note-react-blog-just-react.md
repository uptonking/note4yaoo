---
title: note-react-blog-just-react
tags: [blog, react]
created: 2023-03-03T09:10:33.023Z
modified: 2023-03-03T09:10:48.068Z
---

# note-react-blog-just-react

# guide

- [卡颂 《React技术揭秘》](https://github.com/BetaSu/just-react)
# docs

## [React’s diff algorithm_201312](https://calendar.perfplanet.com/2013/diff/)

- React is a JavaScript library for building user interfaces, designed from the ground up with performance in mind

- vdom
  - It is important to understand that the result of render is not an actual DOM node. 
  - Those are just lightweight JavaScript objects. 
  - We call them the virtual DOM.

- Finding the minimal number of modifications between two arbitrary trees is a O(n^3) problem
  - React uses simple and yet powerful heuristics to find a very good approximation in O(n).
  - React only tries to reconcile trees level by level.
  - You can provide a `key` attribute in order to help React figure out the mapping of list
  - React will match only components with the same class.

- Event Delegation
  - Attaching event listeners to DOM nodes is painfully slow and memory-consuming. 
  - Instead, React implements a popular technique called “event delegation”. 
  - React goes even further and re-implements a W3C compliant event system.
- A single event listener is attached to the root of the document. 
  - When an event is fired, the browser gives us the target DOM node. 
  - In order to propagate the event through the DOM hierarchy, React doesn’t iterate on the virtual DOM hierarchy.
  - Instead we use the fact that every React component has a unique id that encodes the hierarchy. 
  - We can use simple string manipulation to get the id of all the parents. 
  - By storing the event listeners in a hash map, we found that it performed better than attaching them to the virtual DOM.
  - The browser creates a new event object for each event and each listener. 
  - `dispatchEvent('click', 'a.b.c', event) clickCaptureListeners['a'](event); clickCaptureListeners['a.b'](event); clickCaptureListeners['a.b.c'](event); clickBubbleListeners['a.b.c'](event); clickBubbleListeners['a.b'](event); clickBubbleListeners['a'](event);`

- Rendering
  - Whenever you call `setState` on a component, React will mark it as dirty. 
  - **At the end of the event loop, React looks at all the dirty components and re-renders them.**
  - This batching means that during an event loop, there is exactly one time when the DOM is being updated.
- **When `setState` is called, the component rebuilds the virtual DOM for its children.**
  - If you call setState on the root element, then the entire React app is re-rendered. 
  - All the components, even if they didn’t change, will have their render method called
- Finally, you have the possibility to prevent some sub-trees to re-render. 
  - shouldComponentUpdate(object nextProps, object nextState)

- The techniques that make React fast are not new. 
  - We’ve known for a long time that touching the DOM is expensive, you should batch write and read operations, event delegation is faster …
- What makes React stand out is that all those optimizations happen by default. 

## [状态更新](https://react.iamkasong.com/state/prepare.html#%E5%87%A0%E4%B8%AA%E5%85%B3%E9%94%AE%E8%8A%82%E7%82%B9)

- render阶段开始于performSyncWorkOnRoot或performConcurrentWorkOnRoot方法的调用。这取决于本次更新是同步更新还是异步更新。

- 每次状态更新都会创建一个保存更新状态相关内容的对象，我们叫他Update。在render阶段的beginWork中会根据Update计算新的state。
  - 现在触发状态更新的fiber上已经包含Update对象。

- render阶段是从rootFiber开始向下遍历。那么如何从触发状态更新的fiber得到rootFiber呢？
  - 调用markUpdateLaneFromFiberToRoot方法。

- commit阶段开始于commitRoot方法的调用。其中rootFiber会作为传参。

- ClassComponent与HostRoot（即rootFiber.tag对应类型）共用同一种Update结构。
  - lane：优先级相关字段
  - tag：更新的类型，包括UpdateState | ReplaceState | ForceUpdate | CaptureUpdate。
  - next：与其他Update连接形成链表。
- Update存在一个连接其他Update形成链表的字段next
- Fiber节点组成Fiber树，页面中最多同时存在两棵Fiber树：
  - 代表当前页面状态的current Fiber树
  - 代表正在render阶段的workInProgress Fiber树
  - 在commit阶段完成页面渲染后，workInProgress Fiber树变为current Fiber树，workInProgress Fiber树内Fiber节点的updateQueue就变成current updateQueue

- [setState的流程](https://react.iamkasong.com/state/setstate.html)

- [In-depth explanation of state and props update in React - React inDepth](https://indepth.dev/posts/1009/in-depth-explanation-of-state-and-props-update-in-react)
  - [Inside Fiber: in-depth overview of the new reconciliation algorithm in React - React inDepth](https://indepth.dev/posts/1008/inside-fiber-in-depth-overview-of-the-new-reconciliation-algorithm-in-react)

- [didact](https://pomb.us/build-your-own-react/)
  - In Didact, we are walking the whole tree during the render phase. React instead follows some hints and heuristics to skip entire sub-trees where nothing changed.
  - We are also walking the whole tree in the commit phase. React keeps a linked list with just the fibers that have effects and only visit those fibers.

## [双缓存机制](https://github.com/BetaSu/just-react/blob/master/docs/process/doubleBuffer.md)

- 当我们用canvas绘制动画，每一帧绘制前都会调用ctx.clearRect清除上一帧的画面。
  - 如果当前帧画面计算量比较大，导致清除上一帧画面到绘制当前帧画面之间有较长间隙，就会出现白屏。
- 为了解决这个问题，我们可以在内存中绘制当前帧动画，绘制完毕后直接用当前帧替换上一帧画面，由于省去了两帧替换间的计算时间，不会出现从白屏到出现画面的闪烁情况。
  - **这种在内存中构建并直接替换的技术叫做双缓存**。
- **React使用“双缓存”来完成Fiber树的构建与替换——对应着DOM树的创建与更新。**

### [使用双缓存解决 Canvas clearRect 引起的闪屏问题 - 掘金](https://juejin.cn/post/6844903832439242766)

- 经过简单分析，得出闪屏的原因是 clearRect 清除画布后，绘制的时间较长导致出现闪屏的现象。
- 来看一下 microsoft 网站中 双缓冲图形 这篇文章对双缓存的解释：
  - 对图形进行编程时出现闪烁是一个常见问题。
  - 需要多个复杂画图操作的图形操作可导致呈现的图像出现闪烁或具有不可接受的外观。
  - 为解决这些问题，. NET Framework 提供了双缓冲功能。
  - 双缓冲使用内容缓冲来解决与多个画图操作相关的闪烁问题。 
  - 启用双缓冲后，所有画图操作会首先呈现到内存缓冲而不是屏幕上的绘图图面。 
  - 所有画图操作完成后，内存缓冲会直接复制到与之关联的绘图图面。 
  - 由于屏幕上仅执行一个图形操作，因此与复杂画图操作相关的图像闪烁可得以消除

- 解决方法就是新建一个 canvas 作为 缓存 canvas，通过 缓存 canvas 完成绘制过程，绘制完成后，直接将 缓存 canvas 复制到原来的 canvas，这样就可以解决绘制时间过长导致的闪屏问题。
- 这里参考了图形图象处理编程中 双缓存 的概念，将绘制过程交给了 缓存 canvas，这样页面中的 canvas 就省去了绘制过程，而 缓存 canvas 并没有添加到页面，所以我们就看不到绘制过程，也就解决了闪屏的问题。

### [谈谈canvas的性能优化（主要讲缓存问题） - W·Axes - 博客园](https://www.cnblogs.com/axes/p/3567364.html)

- 使用缓存也就是用离屏canvas进行预渲染了，原理很简单，就是先绘制到一个离屏canvas中，然后再通过drawImage把离屏canvas画到主canvas中。可能看到这很多人就会误解，这不是写游戏里面用的很多的双缓冲机制么？

- 其实不然，双缓冲机制是游戏编程中为了防止画面闪烁，因此会有一个显示在用户面前的画布以及一个后台画布，进行绘制时会先将画面内容绘制到后台画布中，再将后台画布里的数据绘制到前台画布中。
- 这就是双缓冲，但是canvas中是没有双缓冲的，因为现代浏览器基本上都是内置了双缓冲机制。所以，使用离屏canvas并不是双缓冲，而是把离屏canvas当成一个缓存区。把需要重复绘制的画面数据进行缓存起来，减少调用canvas的API的消耗。

### [前端“油画设计师”：双缓存绘制与油画分层机制 - 知乎_葡萄城](https://zhuanlan.zhihu.com/p/410295496)

- 重新绘制的过程，实质上是一个不断刮白-重画的过程。
  - 但在屏幕上完成这一系列操作是需要一定时间的，而且屏幕上的图形越复杂，所花的时间就越长，在使用过程中就会让就会直接感觉到屏幕的闪烁。
- 重绘带来的性能负担和闪烁的问题，会给使用者带来较差的使用体验。
  - 为了更好的优化这个两个问题，出现了双缓存画布和油画分层的绘制方法。
- 现在我们有一幅图需要放在Canvas中，使用drawImage()方法，有三种写法：
  - 第一种方法只是把图片原样放到Canvas中，
  - 第二种方法指定宽高就意味着放大或者缩小图片后再放进去，
  - 第三种是将图片裁剪后再放大或者缩小放到canvas中，这三种写法操复杂度作依次增加，性能开销也随之增大。

- 如果使用离屏渲染（即我们所说的双缓存画布），我们可以预先把图片裁剪成想要的尺寸，然后将该内容保存起来，绘制的时候直接使用第一种写法直接将图片放入Canvas中
  - 双缓存画布技术的核心在于系统需要在内存中开辟一块与当前画面等大的“逻辑屏幕“。
  - 我们的画图和动画操作都会先作用于这块”逻辑屏幕“中，当一个操作在这块”逻辑屏幕“上完成之后，再把整块”逻辑屏幕“投放到我们的屏幕上。

- Canvas分层的思想是，动画中每种元素，对渲染和动画的要求是不一样的。
  - 按照分层的逻辑，我们需要频繁更新绘制的只有最上方的猫咪。
  - 这个方法类似油画的绘制，所以也被称为油画分层机制。

- 在该纯前端电子表格中，整个绘制引擎根据油画绘制原理，分为主体图层和装饰图层，
  - 主题图层将会渲染持久的，不会轻易改变的元素，例如背景，单元格，表格线等。
  - 而装饰图层则会渲染常变性元素，例如选择框，拖拽框，悬浮效果等。
  - 在下图中第一层到第四层都是主体图层的内容，第五层是装饰图层。
- 除此之外整个的绘制过程并不是从数据层（Model）直接到视图层（View）的。
  - 而是根据表格内容的特殊性，实现了根据视图层形状，从数据层组合出一层专属视图层的视图数据（ViewModel），再配合前文提到的双缓存画布绘制机制，完成整个表格按需绘制的需求，并缓存绘制结果，进一步提升绘制性能。
- 主体图层不是直接绘制在用户能看到的主画布上，而是绘制在一个看不见的缓存画布上。在需要渲染时，只需要讲缓存画布的内容克隆到主画布上，再附加上装饰图层元素
  - 这样，当表格需要更新时候，比如单元格背景改变，只需要在克隆缓存画布后重绘对应单元格内容即可。
