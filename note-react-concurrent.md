---
title: note-react-concurrent
tags: [concurrent, react]
created: 1970-01-01T00:00:00.000Z
modified: 2020-07-14T10:50:30.695Z
---

# note-react-concurrent

> react v18 introduces concurrent rendering, rather than concurrent mode.
> contents in this page may be obsolete.

# summary 
- react-concurrent-mode新特性
  - Suspense/SuspenseList
    - 指定组件的loading状态/loading组件出现顺序
  - useTransition
    - 更新时先pending，展示现有信息不变部分，loading变化部分
  - useDeferredValue
    - 让占性能的组件先使用旧值
  - Priority-based Rendering 策略
    - 优先执行需要立刻响应的状态更新，延迟占性能的更新，先看旧内容
- Priority-based Rendering
  - 将需要立刻渲染的 `setState` 放在 `startTransition` 外，将占性能的操作及计算放在 `startTransition` 内
  - [Splitting High and Low Priority State](https://reactjs.org/docs/concurrent-mode-patterns.html#splitting-high-and-low-priority-state)
# pieces
- concurrent mode重点关注的是UX，之前的feature如hooks大多关注的的是DX
  - 国内对于使用concurrent mode并不热情，因为用户体验难以量化

- **SWR与前端数据依赖请求**
- 数据依赖关系其实是一个 DAG（有向无环图）。有些数据依赖于其他，有的则无依赖性，对数据的请求则是对这个有向无环图的遍历。
- 最高效的请求方式一定是在拓扑序上尽可能地并行（每当一个数据的依赖都就绪时，立即发起请求）
- 大部分时候（请求并不复杂时），我们用 `Promise.all` 来描述这个 DAG
- `Promise.all([fetchA(), fetchB()]).then([a, b] => fetchC(a, b))`
- swr只需要描述 DAG 中，每一个点的被指向边即可（数据依赖）。
- 每次渲染的时候，SWR会试着执行取数函数（例如 `()=> '/api/c?a=' + A.id` )
  - 如果这个函数抛出异常，那么就意味着它的依赖还没有就绪（A === undefined），SWR将暂停这个数据的请求。
  - 在任一数据完成加载时，由于 `setState` 触发重渲染，上述Hooks会被重选执行一遍（再次检查数据依赖是否就绪），然后对就绪的数据发起新的一轮请求。
  - SWR allows you to fetch data that depends on other data. It ensures the maximum possible parallelism (avoiding waterfalls), as well as serial fetching when a piece of dynamic data is required for the next data fetch to happen.

- **stale-while-revalidate**
- ref
  - [深入浅出 useSWR 原理](https://zhuanlan.zhihu.com/p/93824106)
- **waterfall图展示的请求时间过长的问题**
  - an unintentional request sequence that should have been parallelized
  - 本可以并行执行的并行执行的请求却串行执行了
  - chrome的Waterfall列列出了每个网络请求对应的开始时间和结束时间
    - 从图中可以看出，这一系列请求有明显的先后关系。除了个别请求的时间范围（色块）存在重叠，大部分的都是前后相连的。这就说明它们之间有串行关系
    - 假如所有的网络请求都能改成并行的话，我们能将网络IO需要的时间降低至原来的1/10左右。
    - 首先，将被诊断页面的网络请求按照数据依赖关系分成几个组。如请求B的参数来自于请求A的结果，则B必须在A之后的组中。然后，组内并行请求，组间串行请求。

```JS
// 这是串行写法
async fetchData1() {
  // 执行完一个再执行下一个
  await fetchStudent()
  await fetchTeacher()
  await fetchSchool()
}

// 这是并行写法
async fetchData2() {
  await Promise.all([
    // 互相之间无等待关系
    fetchStudent(),
    fetchTeacher(),
    fetchSchool()
  ])
}

// 当不易一次全部处理时，可以将arr的定义和Promise.all操作分开
async fetchData3() {
  let arr = []
  // something
  arr.push(fetchStudent())
  //other things
  arr.push(fetchTeacher())
  //...
  arr.push(fetchSchool())
  await Promise.all(arr)
}
```

  - 浏览器根据html中外连资源出现的顺序，依次放入队列Queue, 然后根据优先级确定向服务器获取资源的顺序。同优先级的资源根据html中出现的先后顺序来向服务器获取资源
  - Queueing: 出现下面的情况时，浏览器会把当前请求放入队列中进行排队
    - 有更高优先级的请求时.
    - 和目标服务器已经建立了6个TCP连接（最多6个，适用于HTTP/1.0和HTTP/1.1）
    - 浏览器正在硬盘缓存上简单的分配空间
  - 提高性能方法
    - 首先, 减少所有资源的加载时间. 亦即减小瀑布图的宽度. 
    - 其次, 减少请求数量，也就是降低瀑布图的高度. 瀑布图越矮越好.
    - 最后, 通过优化资源请求顺序来加快渲染时间. 
  - ref
    - [Chrome的Waterfall](https://www.cnblogs.com/shengulong/p/7449927.html)
    - [优化前端应用性能 — 网络篇](https://medium.com/@banyudu/%E4%BC%98%E5%8C%96%E5%89%8D%E7%AB%AF%E5%BA%94%E7%94%A8%E6%80%A7%E8%83%BD-%E7%BD%91%E7%BB%9C%E7%AF%87-b94feefeb8b0)

---

- race conditions问题
  - Race conditions are bugs that happen due to incorrect assumptions about the order in which our code may run
  - Race Condition是开发中经常遇到的问题，比如查询天气的时候，先输入“北京”，再输入“深圳”，这时将发起 2 个请求。很可第一个请求花的时间比第二个请求长，如果不做处理，最终看到的是北京的天气，而不是深圳
  - 即前面请求的响应结果，在靠后的时机返回，后面请求结果先返回
  - 竞态条件出现的原因是无法保证异步操作的完成会按照他们开始时同样的顺序
  - 解决方式很简单，在useEffect返回的cleanup函数中清理数据或设置失效标记，然后在更新数据前根据标记判断其有效性
  - 上面这种方案虽然解决了问题，但体验并不好。
    - 在输入数据的过程中，并不能看到输入过程中返回的结果，只能看到最终的结果。我们期望的效果是输入过程中能实时展示有效的结果
    - 可以引入2个全局变量，一个变量用来标识当前请求的序号，另一个记录上一个有效请求的序号。只有序号比上一个有效序号大的时候，才展示数据。这样就保证了旧的请求不会覆盖新的请求
  - 还可以将setState的第一个参数设为函数来解决 
  - ref
    - [React Hooks 搞定 Race Condition](https://segmentfault.com/a/1190000019893237)
    - [Race conditions in React and beyond](https://wanago.io/2020/03/02/race-conditions-in-react-and-beyond-a-race-condition-guard-with-typescript/)
    - [化解使用 Promise 时的竞态条件](https://efe.baidu.com/blog/defusing-race-conditions-when-using-promises/)
    - [How to fetch data with React Hooks?](https://www.robinwieruch.de/react-hooks-fetch-data)
  - [race condition with Promise](https://twitter.com/LaraNerdsom/status/1219825132702785537)

---

- React目前主要的问题有两个
  - 页面在大量DOM节点同时更新的情况下，会出现延迟很严重的现象，具体表现为交互/渲染的卡顿现象
    - 第一个问题会在设备计算能力差（比如 mobile device）的情况下被放大，我们可以把这个问题和 CPU 绑在一起（CPU-bound）
  - 异步操作（比如 data fetch）需要在组件mount之后进行，导致子组件的fetch有可能被父组件的fetch阻塞
    - 第二个问题会在设备网络情况差（比如slow network）的情况下被放大，我们可以把这个问题和 IO 绑在一起（IO-bound）
- 第一个问题并不是一个performance问题，而是一个调度 (scheduling) 问题，所以提高处理速度并不能完全解决这个问题，就像提高网速并不能解决 HTTP/1.1 协议的线头阻塞 (Head-of-line blocking) 问题。
- 这个问题的本质是，浏览器的 main thread 是单线程的，短时间大量 CPU consuming 的 task 被加到了 call stack，导致 event loop 在好几个周期都没有空闲去处理 queue 里面的用户交互 (click, scroll, etc.)，从而用户感知到了卡顿。
- 比如第一个问题在Table搜索的时候很常见，如果数据特别多，搜索的时候的卡顿是一定的。解决方法也很简单，使用 `debounce` 函数在用户连续输入的时候，不进行操作，等用户输入暂停再搜索
- 解决这个问题的原理其实很简单，HTTP/2 采用分帧 (Frame) 的方式解决的 HTTP/1.1 的线头阻塞问题，我们也可以将大量的更新任务 (Batch update task) 拆分成一个个小的 task，从而让 event loop 有机会处理用户交互的 callback。
- React Fiber就是React Team一直在持续开发用来解决上面问题的新 algorithm 或者叫 reconciler。
- 旧的Reconciler (又叫 Stack Reconciler)，React 会维护一个 Virtual DOM tree 用来 mapping 真正的 DOM tree。state update 会创建一个新的 Virtual DOM tree，然后对两个 Virtual DOM tree 使用 diffing 算法，从而得到需要修改的队列，然后会一口气将所有的修改 apply to DOM。
- 为什么要叫Stack Reconciler？
  - 因为这里的 Diffing 过程是递归 (recursive) 的。
  - 我们使用递归都需要注意的一个风险 - 栈溢出 (stack overflow) 。
  - 为什么会发生栈溢出，因为递归调用，外层的栈是不会弹出的（尾递归除外）。
  - 当然这里的问题其实跟栈溢出没什么关系，重点在于栈被一直占用了。
  - JavaScript运行环境只有一个call stack，因此就造成了我们上面提到的用户感知到卡顿的问题。
- 新的Fiber Reconciler是怎么解决这个问题的呢？
  - 递归改成循环 (while loop)，同时在每次循环结束做过期（expire) 判断，如果过期就标记下当前的位置，break出来，让 main thread 有机会完成高优先级的work
  - React会维护两个Fiber tree，一个称之为 current tree 与当前DOM对应，另一个叫做 workingProgress tree 与期望更新后的DO 对应。我们上面提到的修改会直接 apply 在 workingProgress tree，然后会将 current 指针和 workingProgress 指针对调，从而实现更新。这种技巧我们称之为 Double Buffering
- Suspense可以用来解决请求阻塞的问题
- Fiber的update机制，有个细节问题就是，render phase 可以被打断的，那如果打断的work要怎么处理呢？
- 这里其实因为用户交互的优先级更高，因此需要先进行加粗的工作，进行到一半的修改颜色工作就会被丢弃，等到完成了字体加粗的工作再回过头来重启。
- 会带来一个问题，有些生命周期函数可能会被多次调用，比如上图的 componentWillUpdate。
- componentDidMount(), componentDidUpdate(), componentWillUnmount() 这三个生命周期函数 (lifecycle method) 运行在commit阶段，其余的生命周期函数都可以简单理解为运行在render阶段
- 生命周期函数有可能被执行多次的解决方式有两种：
  - 把在这些生命周期执行的逻辑放到commit phase执行，如果能完全做到，这里可以直接将组件改成React hook的形式。
  - 保证render phase执行的逻辑是幂等的 (idempotent)
# Building Great User Experiences with Concurrent Mode and Suspense
- This post will be most relevant to people working on data fetching libraries for React.
- It shows how to best integrate them with Concurrent Mode and Suspense. 
- Suspense is a powerful tool for carefully orchestrating an elegant loading sequence with a few, well-defined states that progressively reveal content. 
- The traditional approach to loading data in React apps involves what we refer to as **fetch-on-render**. 
  - First we render a component with a spinner, then fetch data on mount (componentDidMount or useEffect), and finally update to render the resulting data. 
  - It’s certainly possible to use this pattern with Suspense: instead of initially rendering a placeholder itself, a component can “suspend” — indicate to React that it isn’t ready yet. 
  - This will tell React to find the nearest ancestor `<Suspense fallback={<Placeholder/>}>` , and render its fallback instead. 
  - If you watched earlier Suspense demos, this example may feel familiar — it’s how we originally imagined using Suspense for data-fetching.
- It turns out that this approach has some limitations.
- Using the fetch-on-render approach described above to implement this could cause sequential round trips (sometimes referred to as a “waterfall”). 
  - First the data for the `<Post>` component would be fetched and then the data for `<CommentList>` would be fetched, increasing the time it takes to show the full page.
- There’s also another often-overlooked downside to this approach. 
  - If `<Post>` eagerly requires (or imports) the `<CommentList>` component, our app will have to wait to show the post body while the code for the comments is downloading. 
  - We could lazily load `<CommentList>` , but then that would delay fetching comments data and increase the time to show the full page. 
- The fetch-on-render approach is widely used by React apps today and can certainly be used to create great apps.

- **Parallel Data and View Trees**
- One of the most appealing things about the fetch-on-render pattern is that it colocates what data a component needs with how to render that data
- All the issues we saw above were due to when we fetch data in this approach: upon rendering. 
- We need to be able to fetch data before we’ve rendered the component. 
- The only way to achieve that is by extracting the data dependencies into parallel data and view trees.
- Other frameworks could achieve a similar effect by allowing developers to define data-fetching logic in a sibling file (maybe Post.data.js), or perhaps integrate with a bundler to allow defining data dependencies with UI code and automatically extracting it, similar to Relay Compiler.
- The key is that regardless of the technology we’re using to load our data — GraphQL, REST, etc — we can separate what data to load from how and when to actually load it. 

- **Fetch in Event Handlers**
- The key is to start fetching code and data for a new view in the same event handler that triggers showing that view. 
- We can either fetch the data within our router — if our router supports preloading data for routes — or in the click event on the link that triggered the navigation. 
- It turns out that the React Router folks are already hard at work on building APIs to support preloading data for routes. But other routing frameworks can implement this idea too.
- Conceptually, we want every route definition to include two things: what component to render and what data to preload, as a function of the route/url params.
- This approach can be generalized to other data-fetching solutions. An app that uses REST might define a route like this

```JS
function Post(props) {
  const postData = useFragment(graphql `
    fragment PostData on Post {
      author
      title

      # fetch data for the comments, but don't block on it being ready
      ...CommentList @defer
    }
  `, props.post);

  return (
    <div>
      <h1>{postData.title}</h1>
      <h2>by {postData.author}</h2>
      {/* @defer pairs naturally with <Suspense> to make the UI non-blocking too */}
      <Suspense fallback={<Spinner/>}>
        <CommentList post={postData} />
      </Suspense>
    </div>
  );
}
```

- This same approach can be employed not just for routing, but in other places where we show content lazily or based on user interaction. 
  - For example, a tab component could eagerly load the first tab’s code and data, and then use the same pattern as above to load the code and data for other tabs in the tab-change event handler. 
  - A component that displays a modal could preload the code and data for the modal in the click handler that triggers opening the modal, and so on.
- Once we’ve implemented the ability to start loading code and data for a view independently, we have the option to go one step further. 
  - If we can load code and data for a view after the user clicks, we can also start that work before they click, getting a head start on preparing the view.
- Best of all, we can centralize that logic in a few key places — a router or core UI components — and get any performance benefits automatically throughout our app. 

- **Load Data Incrementally**
- The above patterns — parallel data/view trees and fetching in event handlers — let us start loading all the data for a view earlier. 
- But we still want to be able to show more important parts of the view without waiting for all of our data.
- At Facebook we’ve implemented support for this in GraphQL and Relay in the form of some new GraphQL directives (annotations that affect how/when data is delivered, but not what data). 
- This same pattern can be applied to other frameworks as well. 
- For example, apps that call a REST API might make parallel requests to fetch the body and comments data for a post to avoid blocking on all the data being ready.

- **Treat Code Like Data**
- `React.lazy` is, as the name implies, lazy. 
  - It won’t start downloading code until the lazy component is actually rendered   
  - it’s “fetch-on-render” for code!
- To solve this, the React team is considering APIs that would allow bundle splitting and eager preloading for code as well. 
- That would allow a user to pass some form of lazy component to a router, and for the router to trigger loading the code alongside its data as early as possible.

- To recap, achieving a great loading experience means that we need to start loading code and data as early as possible, but without waiting for all of it to be ready. 
  - Parallel data and view trees allow us to load the data for a view in parallel with loading the view (code) itself. 
  - Fetching in an event handler means we can start loading data as early as possible, and even optimistically preload a view when we have enough confidence that a user will navigate to it.
  - Loading data incrementally allows us to load important data earlier without delaying the fetching of less important data. 
  - And treating code as data — and preloading it with similar APIs — allows us to load it earlier too.
# guide
- ref
  - [精读《Suspense 改变开发方式》](https://zhuanlan.zhihu.com/p/113463166)
  - [理解 React Fiber & Concurrent Mode](https://zhuanlan.zhihu.com/p/109971435)
