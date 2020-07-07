---
tags: [blog, react, concurrent]
title: page-blog-react-concurrent
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-03T09:36:59.280Z'
---

# page-blog-react-concurrent

## pieces

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

## Building Great User Experiences with Concurrent Mode and Suspense

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

``` JS
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

## guide

- ref
  - [精读《Suspense 改变开发方式》](https://zhuanlan.zhihu.com/p/113463166)
  - [理解 React Fiber & Concurrent Mode](https://zhuanlan.zhihu.com/p/109971435)
