---
title: note-dev-state-redux
tags: [redux, state]
created: '2020-11-02T06:05:20.019Z'
modified: '2020-11-02T06:05:38.780Z'
---

# note-dev-state-redux

- Redux is a predictable state container for JavaScript apps.
- redux vs pub sub

## faq

- 为什么很多人将fetch请求和redux绑定在一起使用
  - 因为不管是改全局state还是fetch什么的，在我的组件内部都是副作用，副作用的东西之后，它还要改一层全局状态，如果你的场景是请求了改这个组件，那没啥问题，但如果你请求了数据，这个数据在多层次都要用到，你得放全局，这个fetch得副作用你觉得放哪能解决你的问题？既然redux那块有一层改全局state的功能划分，再加一层副作用异步改全局state的能力，redux-thunk提供了，所以effects这种副作用理应靠在redux那边。这个你用一下dva+umi的方式可能更好理解。

- ### [redux有什么缺点？](https://www.zhihu.com/question/263928256)
  - 需要写大量的 Action Creator 代码
  - 需要写大量 switch case 分支判断
  - Action 和 Reducer 分开书写，维护起来麻烦
  - 模板代码太多，使用不方便，属性要一个一个 pick，对 ts 也不友好
  - 触发更新的效率也比较差，connect 的组件的 listener 必须一个一个遍历，再靠浅比较去拦截不必要的更新
  - 异步操作，通常可以使用 thunk 中间件来做异步
  - store里面的数据必须都是可以序列化的，比如普通文本，数组，不支持Map，Set等数据结构
  - store 的推荐数据结构是 json object
    - 这对于我们的业务来说也不太合适，我们的数据结构是图状，互相有复杂的关联关系
    - 适合用面向对象来描述模型，描述切面，需要多实例隔离，显然用 json 或者 normalizr 强行做只会增加复杂度，和已有的代码也完全无法小成本适配
  - 基于 snapshot 的 time travel 内存占用高，性能差，并且没有配套的暂停、重启、切换、清空、事务等机制
  - 无法做关联更新，每一次的所有变更必须由用户触发，既是优点又是缺点
  - 非class的设计在ts下得主动写interface并在调用方声明，而 class 的好处是在于本身就能作为 type，并且可以利用 IDE做反向依赖查找
    - 在复杂业务中，函数式很难落地，包括类似游戏开发中的ECS架构，其实都很难实践，那一点点利用分级缓存提升的性能远远不如面向对象带来的优势更多，还是看业务场景和团队成员的。
  - 对于自定义的class实例、引用类型、各个不同命名空间属性之间的互相引用似乎是不支持的，仍然需要设计成扁平化，通过 id 来关联，查找的时候显然是不如链式结构快的，并且很难用

- ### [Redux vs Simple Pub Sub](https://spectrum.chat/react/general/redux-vs-simple-pub-sub~818edeff-0616-4462-9743-71c2678795a5)
  - I developed a project which is using redux to send messages to a component that is residing in another parent component 
    - but the same problem was resolved using a simple ES6 pub sub library. 
    - This raised my curiosity whether to use Redux or a simple Pub Sub would be enough?
  - It probably depends on the long term roadmap for this project.
    - For example, if you expect to store system wide internal state that's shared by many components in many routes, then Redux store should help avoid refetching the same resources over and over again.
    - But if you don't see the project to grow too much in complexity, then keeping the app light and simple seems perfect!
  - **one thing that Pub/Sub doesn't solve** is 
    - if components rendered later require the same resources, you'd need to fetch again, 
    - since a basic Pub/Sub is stateless in the sense that it doesn't store messages. 
    - React Context and Redux are stateful, which solves the problem
  - I use react context for small light weight stuff. Works great.
  - A redux action triggers the change in the store (computed via reducer), 
    - and then each component [subscribed to the store via connect/useSelector] can read the store values and re-render. 
    - This is idiomatic in react-redux world.
  - If your problem is solved with pubsub lib, great for you. 
    - But if you keep on adding features the following might happen: 
      - (a) you need to access the data from a new component on the page, 
      - (b) you need to access the data from another page in the app or 
      - (c) you need to save the data across app reloads (as with redux-persist). 
    - And now, since you're using a custom solution, you'll need to find or invent a solution that fits, whereas in redux these problems are already taken care of.
  - The idea of pub/sub and listeners caching data reminds me of FLUX pattern with multiple stores, 
    - which lead to the creation of Redux with one store, 
    - because people were struggling with syncing data across multiple stores and not having a single source of truth
    - Personally my take on React Context is that it could be used for storing local app state that doesn't need to live in a global store and also prevent prop drilling. 
    - So, sort of a complement to Redux IF you expect to build a large app. 
    - Otherwise we could also possibly just use React Context as a global store instead of Redux for smaller apps?

## pieces

- Redux is not supposed to "replace the initial idea of react.js", 
  - think of it more like a library to manage shared state between components and to coordinate state mutations. 
  - Redux does use a pub/sub pattern indeed

- redux适合管理全局app状态，局部component的状态无需额外状态管理或过重的状态管理
- redux自身的300行代码只处理简单的同步数据流，把脏活、累活比如异步数据流全扔给各种适配和插件处理了。

- Redux is global state, which is fine as long as only genuinely global stuff goes in there, 
  - like current user profile or basket contents. 
  - Where redux becomes a problem is when people try to use it for everything instead of just using React state
  - Some of that advice could be outdated - before Context, 
    - redux was one of very few ways to avoid heavy prop drilling. 
    - Now that context is here as a non-global option, I'd recommend keeping redux to pure globals
  - But to add to that, now that context is here you don't really need to use redux at all. 
    - However, I like it because as well as being a global store it's also pub/sub
  - You can use redux for everything but that's often overkill. 
    - Sometimes local component state is all you need. 
    - If you're making async calls to a backend definitely use redux.
  - I use react state all the time with backend calls, 
    - but I you mean really long-running tasks where app receives status messages over web sockets right? 
    - In which case yeah redux would be nice. 
    - Could wire the socket handler to redux actions, and present progress anywhere in the UI
  - I was going to say that I would do all calls async off the bat(off the bat, 立即，立刻) anyway wherever possible.
    - Same idea with the websockets as server-sent events which are very easy to work with. 
    - I can see a global being useful there as it literally is global - anywhere in the SPA.

- The drawbacks of using 1 context wrapping a useReducer is your components will re-render each time any property changes. 
  - Redux implements a pub/sub pattern, where you retrieve the part of the store you want outside of your component, so only re-render for that part.

- Pub/sub implementations such as redux exist largely to decouple publishers and subscribers. 
  - Thus we should not name actions in a way that describes how the reducer will handle them. 
  - Action names should indicate what happened, not what needs to happen

## redux-toolkit

- The official, opinionated, batteries-included toolset for efficient Redux development

- three common concerns about Redux:
  - "Redux requires too much boilerplate code"
  - "Configuring a Redux store is too complicated"
  - "I have to add a lot of packages to get Redux to do anything useful"
- redux-toolkit does not address concepts like "reusable encapsulated Redux modules", data caching, file structures, managing entity relationships in the store, and so on.

- toolkit-api
  - configureStore()
    - wraps createStore to provide simplified configuration options and good defaults.
  - createReducer()
    - lets you supply a lookup table of action types to case reducer functions, rather than writing switch statements.
  - createAction()
    - generates an action creator function for the given action type string. 
  - createSlice()
    - automatically generates a slice reducer with corresponding action creators and action types.
  - createAsyncThunk()
    - accepts an action type string and a function that returns a promise
  - createEntityAdapter()
    - generates a set of reusable reducers and selectors to manage normalized data in the store
  - createSelector()
    - utility from the Reselect library, re-exported for ease of use.

- toolkit优点
  - 它默认配置好了 redux-devtools，异步中间件 redux-thunk，防止用户修改 state 的redux-immutable-state-invariant，检测是否存在不可序列化 state(例如有函数属性)serializable-state-invariant-middleware。这样用户就不会再抱怨配置 store 太复杂了。
  - 整合了业界一些优秀的三方库，例如 immer.js，让我们可以用 mutable 的写法处理 state，但是最后还是 immutable 的更新。
    - 原理是采用了 proxy 对用户的 mutable 操作做搜集，在对原有 state 进行结构复用，只修改受影响的节点到根节点。
    - 由于内部采用了结构复用而不是深拷贝，性能问题其实不大。有了 immer.js，其实就没必要用 immutable.js 了。
    - 还从 Reselect 中重新导出了 createSelector ，尽量让用户可以直接使用社区的最佳实践。
  - 提供了一些辅助 API 来减少模板代码
    - 以前我们写 redux 一般是三个文件夹：constants 用于放 action type 常量，actions 用于放 action creator，reducers 用于放拆分后的子 reducer，现在只需要一个 features 文件夹即可。
    - 具体来说提供了 createAction()用户方便的生成 action creator，createSlice() 让用户可以集中声明一个分割的子 state 的初始 state，reducers，同时 reducers 的函数名和 name 属性会自动合并成 action type，
    - 正是由于 createSlice 我们就可以只在一个文件 UserSlice 编写以前得在三个分离的文件 reducers/user，actions/user, constants/user 的代码。

- [用redux-toolkit 改造你的redux](https://juejin.im/post/6844904129178009613)
  - https://github.com/acivan/react-rtk-ts

## ref

- [Why you should NEVER use Redux with Angular](https://morioh.com/p/548aad273e3e)
  - Angular is a highly opinionated framework around dependency injection (DI). 
    - This makes it easy to share state out of the box. 
    - Services can easily be shared across different component classes
  - While you can achieve something similar with React, the easier option is to use Redux.
  - This is why Redux became so popular with React. 
  - It's the same way other third party libraries (like Axios) became popular with React. 
  - These libraries are necessary because React is simply a UI component library.
  - And just like Angular doesn't need Axios because of it's own httpClientModule, it doesn't need Redux because of things like DI, services, and RxJS
  - RxJS is a library for making async requests. It leverages the observable design pattern to bring a reactive pub/sub functionality to Angular.
  - you can argue that Redux is a redundant addition to Angular because Angular achieves the same behavior using RxJS.
- [6 things I wished I knew about state management when I started writing React apps](https://medium.com/@veeralpatel/things-ive-learned-about-state-management-for-react-apps-174b8bde87fb)
  - [reddit discussion](https://www.reddit.com/r/javascript/comments/f1jop9/6_things_i_wished_i_knew_about_state_management/)
