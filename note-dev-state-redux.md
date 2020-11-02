---
title: note-dev-state-redux
tags: [redux, state]
created: '2020-11-02T06:05:20.019Z'
modified: '2020-11-02T06:05:38.780Z'
---

# note-dev-state-redux

- Redux is a predictable state container for JavaScript apps.

## faq

- 为什么很多人将fetch请求和redux绑定在一起使用
  - 因为不管是改全局state还是fetch什么的，在我的组件内部都是副作用，副作用的东西之后，它还要改一层全局状态，如果你的场景是请求了改这个组件，那没啥问题，但如果你请求了数据，这个数据在多层次都要用到，你得放全局，这个fetch得副作用你觉得放哪能解决你的问题？既然redux那块有一层改全局state的功能划分，再加一层副作用异步改全局state的能力，redux-thunk提供了，所以effects这种副作用理应靠在redux那边。这个你用一下dva+umi的方式可能更好理解。

- redux vs event pub

## pieces

- Redux is not supposed to "replace the initial idea of react.js", 
  - think of it more like a library to managed shared state between components and to coordinate state mutations. 
  - Redux does use a pub/sub pattern indeed

- redux适合管理全局app状态，局部component的状态无需额外状态管理或过重的状态管理

- create-react-app creates apps with one command and no build config
  - React, JSX, ES6(最新语法), TypeScript and Flow syntax support.
  - Autoprefixed CSS
  - A fast interactive unit test runner 
  - A live development server(使用的是webpack-dev-server)
  - A build script to bundle JS, CSS, and images for production
  - An offline-first service worker and a web app manifest for PWA
- dva是基于redux、redux-saga和react-router的轻量级前端框架，偏数据流
  - dva: react + redux + redux-saga + react-router + 其他
  - 相比于cra多了内置的redux、redux-saga、react-router
  - 仅有6个api(但有很多约定)
  - app = dva(opts)
  - app.use(hooks)
  - app.model(model)
  - app.unmodel(namespace)
  - app.replaceModel(model)
  - app.router(({ history, app }) => RouterConfig)
  - app.start(selector?)
- umi是插件化的企业级前端应用框架，偏构建工具，但支持很多插件引入框架
  - umi: react-router + webpack + babel；
  - 内置了路由、构建、部署、测试等

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

## redux-blog

### [Redux without React — State Management in Vanilla JavaScript](https://www.sitepoint.com/redux-without-react-state-management-vanilla-javascript/)

- https://github.com/morkro/tetrys

- What makes Redux great is that it forces you to think ahead and get an early picture of your application design. 
  - You start to define what should actually be stored, which data can and should change, and which components can access the store.
- I decided to adopt a file structure commonly found in Redux and React projects. 
  - store, actions, reducers
  - components
  - constants, utils
  - It’s a logical structure and is applicable to many different setups. 
  - There are many variations on this theme, and most projects do things a little differently, but the overall structure is the same.
- To access the store, it needs to be created once and passed down to all instances of an application. 
  - Most frameworks work with some sort of dependency injection container, so we as a user of the framework don’t have to come up with our own solution. 

- Originally I put the store in its own module (`scripts/store/index.js`), which could then be imported by other parts of my application. 
  - I ended up regretting this and dealing with circular dependencies real quick. 
  - The issue was that the store didn’t get properly initialized when a component tried to access it.
  - The application entry point was initializing all the components, which then made internal use of the store directly or via helper functions (called `connect` here). 
  - But since the store wasn’t explicitly created, but only as a side effect in its own module, components ended up using the store before it has been created.
  - There was no way to control when a component or a helper function called the store for the first time. It was chaotic.

``` JS
// scripts/store/index.js (☓ bad)
import { createStore } from 'redux'
import reducers from '../reducers'

const store = createStore(reducers)

export default store
export { getItemList } from './connect'

// scripts/store/connect.js (☓ bad)
import store from './'

export function getItemList() {
  return store.getState().items.all
}
```

- This is the exact moment when my components ended up being mutually recursive. 
  - The helper functions require the store to function, 
  - and are at the same time exported from within store initialization file to make them accessible to other parts of my application.

- I solved this problem by moving the initialization to my application entry point (`scripts/index.js`) , and passing it down to all required components instead.
  - this is very similar to how React actually makes the store accessible
- The application entry point creates the store first of all, then passes it down to all the components. 
- Then, a component can connect with the store and dispatch actions, subscribe to changes or get specific data.

``` JS
// scripts/store/configureStore.js (✓ good)
import { createStore } from 'redux'
import reducers from '../reducers'

export default function configureStore() {
  return createStore(reducers)
}

// scripts/store/connect.js (✓ good)
export function getItemList(store) {
  return store.getState().items.all
}

// scripts/index.js
import configureStore from './store'
import { PageControls, TetrisGame } from './components'

const store = configureStore()
const pageControls = new PageControls(store)
const tetrisGame = new TetrisGame(store)
```

- Presentational components do nothing else besides pure DOM handling; they aren’t aware of the store. 
- Container components on the other hand can dispatch actions or subscribe for changes.
- For me there are exceptions though. 
  - Sometimes a component is really minimal and only does one thing. 
  - I didn’t want to split them up into one of the aforementioned patterns, so I decided to mix them. 
  - If the component grows and gets more logic, I will separate it.

- One of the bigger questions I had, when starting the project, was how to actually update the DOM. 
  - React uses a fast in-memory representation of the DOM called Virtual DOM to keep DOM updates to a minimum.
  - I could well switch to Virtual DOM, if my application should grow bigger and more DOM heavy, 
  - but for now I do classic DOM manipulation and that works fine with Redux.
- The basic flow is as follows:
  - A new instance of a container component is initialized and passed the store for internal use
  - The component subscribes to changes in the store
  - And uses a different presentational component to render updates in the DOM

- Another important point is to implement a use case driven store. 
  - In my opinion it’s important to only store what is essential for the application. 
  - At the very beginning I stored almost everything: current active view, game settings, scores, hover effects, the user’s breathing pattern, and so on.

- I have worked on Redux projects with and without React and my main take-away is, that huge differences in application design aren’t necessary. 
  - Most methodologies used in React can actually be adapted to any other view handling setup. 
  - I took me a while to realize this, as I started off thinking I have to do things differently, but eventually I figured this is not necessary.
- What is different however, is the way you initialize your modules, your store, and how much awareness a component can have of the overall application state. 
  - The concepts stay the same, but the implementation and amount of code is suited to exactly your needs.
