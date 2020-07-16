---
title: docs-redux
tags: [docs, state]
created: '2019-08-01T16:03:46.390Z'
modified: '2020-07-14T09:24:43.966Z'
---

# docs-redux

- Redux is a predictable state container for JavaScript apps.

## dev-tips

- we ultimately wound up shipping three hooks:
  - `useSelector` : subscribes to the store and returns the selected value
  - `useDispatch` : returns the store's dispatch function
  - `useStore` : returns the store instance itself
- 唯一会使用到bindActionCreators的场景是当你需要把action creator往下传到一个组件上，却不想让这个组件觉察到Redux的存在，而且不希望把dispatch或Redux store传给它
- 通过redux的combineReducers可以很好的扁平化数据
- compose：作用是从右到左来组合多个函数，其实就是让你少写几个函数嵌套， `compose(funcA, funcB, funcC)` 等价于 `funcA(funcB(funcC))`

## resources

- redux api docs
	- https://cn.redux.js.org/docs/api/
	- [react-redux v7 release notes](https://github.com/reduxjs/react-redux/releases/tag/v7.0.1)
	- [Discussion: Potential hooks API design](https://github.com/reduxjs/react-redux/issues/1179)
	- [React-Redux Roadmap: v6, Context, Subscriptions, and Hooks](https://github.com/reduxjs/react-redux/issues/1177)
	- [react-redux杂谈 - 设计结构变迁](https://zhuanlan.zhihu.com/p/86336676)
	- [React-Redux v7100行代码简易版（Hook+TS实现）](https://zhuanlan.zhihu.com/p/103016304)
	- [造玩具学原理系列 | redux 源码解析及模拟实现](https://zhuanlan.zhihu.com/p/82951588)
- examples
	- https://redux.js.org/introduction/examples

## react-redux 

- ref
  - [react-redux 杂谈 - 设计结构变迁](https://zhuanlan.zhihu.com/p/86336676)

- 在v5中，会优先查找上一级context的subscription(parentSub)，如果垂直多个层级的组件都使用connect订阅了全局state的变化，当state更新时，消息是从 `C --> B --> A` 一层一层往下传递的，而不是统一维护在store的listeners中
- In v6, every store update calls `setState()` at the root of the component tree in `<Provider>` , and forces React to walk the component tree to find the consumers before they can even run `mapState` . 
- v7重新使用了多个subscription逐层通知的结构，和5.x基本一致，并且使用React Hooks对项目进行了重构，增加了对hooks的支持
- In RRv6, there were four major issues with perf:
  - If I have N connected components, there are N wrapper components in the tree
  - If a Redux action was dispatched, we immediately put that into `setState({storeState})` in `<Provider>` at the root, 
    - which **unconditionally** forced a re-render even if 0 components were actually interested in the change, 
    - and that change was always starting at the root.
    - `<Provider>` memoized its children, so the render didn't completely cascade from the root, but React still had to traverse the tree to find all context consumers.
  - All N connected wrappers would have to re-render in order to run mapState and calculate if the wrapped child needed to re-render
  - All that mapState calculation was done synchronously while rendering the wrappers
  - In contrast, v7 and connect still have N wrapper components, 
    - but if only say 5 out of 100 components actually have new values returned from mapState, only those 5 will have renders queued, 
    - and they are much lower in the tree. 
    - So, while I know React always starts renders from the root, it can skip over most of the tree and just update the few sub-trees that have renders queued.
- So, huge differences in if renders are queued, and how many components are flagged for updates, and doing less work is generally going to be faster.
- With context selectors, we might still be facing the "unconditional render starting at the root" and "calculating selectors while rendering" aspects. 
  - It's possible that `useMutableSource` may allow us to work around that. 
  - But, at least we wouldn't be forcing every connected component to fully re-render.
- (and as I've said, it's also entirely possible that this is only something we can implement with useSelector and not connect.)

- Performance downgrade after update to v.6.0.0
  - In v5, connected components re-ran `mapState` immediately in the subscribe callbacks, and only called `setState()` once they knew they needed to re-render. 
  - In v6, every store update calls `setState()` at the root of the component tree in `<Provider>` , and forces React to walk the component tree to find the consumers before they can even run `mapState` . That's a very meaningful difference.

### v7

- As with v5 and earlier, v7 wrapper components all subscribe to the store directly, and only get React involved when the selector logic determines that the wrapper component needs to re-render. This was the first key step in bringing performance back to the level of v5.
  - React has always had an API called unstable_batchedUpdates(). Internally, React wraps all your event handlers inside of that, which is what allows React to batch together multiple state updates from one event tick into a single render pass.
  - The React team urged us to use unstable_batchedUpdates() directly in React-Redux. This was tricky, because it's actually exported from renderers like ReactDOM and React Native, not the core React package. React-Redux should work with any React renderer, so we couldn't add a direct dependency on either of those. We had to write some different wrapper files so that the "react-dom" import would get loaded in a web environment, and the "react-native" import when used with RN. For apps that might be using React-Redux with an alternate renderer, we added an additional entry point that falls back to a dummy batching implementation.
  - In particular, we couldn't enforce top-down updates in a hooks environment, because v7 relies on overriding context values to pass down nested Subscription instances, and you can't render context values from a hook. This meant users would potentially encounter the "zombie child" issue again.

- React-Redux version 7 resolves the performance issues that were reported with version 6, and lays the groundwork for us to design and ship a public useRedux()-type Hooks API in a later 7.x release.
  - The major change for this release is that `connect` is now implemented using Hooks internally. 
  - Because of this, we now require a minimum React version of 16.8.4 or higher
- `connect` now uses `React.memo()` internally, which returns a special object rather than a function. 
  - Any code that assumed React components are only functions is wrong, and has been wrong since the release of React 16.6. 
  - If you were using PropTypes to check for valid component types, you should change from PropTypes.func to PropTypes.elementType instead.
- In v6, we switched from individual components subscribing to the store, to having ` <Provider>` subscribe and components read the store state from React's Context API. 
  - This worked, but unfortunately the Context API isn't as optimized for frequent updates as we'd hoped, and our usage patterns led to some folks reporting performance issues in some scenarios.
- In v7, we've switched back to using direct subscriptions internally, which should improve performance considerably.
  - This does result in some changes that are visible to user-facing code, in that updates dispatched in React lifecycle methods are immediately reflected in later component updates. 
  - Examples of this include components dispatching while mounting in an SSR environment. 
  - This was the behavior through v5, and is not considered part of our public API.)
- React has an `unstable_batchedUpdates` API that it uses to group together multiple updates from the same event loop tick. 
  - The React team encouraged us to use this, and we've updated our internal Redux subscription handling to leverage this API. 
  - This should also help improve performance, by cutting down on the number of distinct renders caused by a Redux store update.
- We've reimplemented our connect wrapper component to use hooks internally. While it may not be visible to you, it's nice to know we can take advantage of the latest React goodies!
- React's `unstable_batchedUpdate()` API allows any React updates in an event loop tick to be batched together into a single render pass. 
  - React already uses this internally for its own event handler callbacks. 
  - This API is actually part of the renderer packages like ReactDOM and React Native, not the React core itself.

## redux docs

### Getting Started with Redux

- The whole state of your app is stored in an object tree inside a single store.  
- The only way to change the state tree is to emit an action, an object describing what happened.
- To specify how the actions transform the state tree, you write pure reducers.

- basic example    

``` js
import { createStore } from 'redux'

// reducer
function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}

// store
let store = createStore(counter)

//  update the UI in response to state changes. 
store.subscribe(() => console.log(store.getState()))

// dispatch an action 
store.dispatch({ type: 'INCREMENT' })
```

- In a typical Redux app, there is just a single store with a single root reducing function. As your app grows, you split the root reducer into smaller reducers independently
- Should You Use Redux?
	- You have reasonable amounts of data changing over time
	- You need a single source of truth for your state
	- You find that keeping all your state in a top-level component is no longer sufficient

### Motivation

- 随着单页应用开发日趋复杂，JavaScript需要管理比任何时候都要多的state 
	- 这些 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据
	- 也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等
- 考虑一些来自前端开发领域的新需求，如更新调优、服务端渲染、路由跳转前请求数据等等
- This complexity is difficult to handle as we're mixing two concepts: `mutation` and `asynchronicity` .
-  Libraries like React attempt to solve this problem in the view layer by removing both asynchrony and direct DOM manipulation.
	- However, managing the state of your data is left up to you. This is where Redux enters.
- Redux attempts to make state mutations predictable by imposing certain restrictions on how and when updates can happen. 

### Core Concepts

- your app's state is described as a plain object
	- This object is like a “model” except that there are no setters. 
	- To change something in the state, you need to dispatch an action.
- An action is a plain JavaScript object that describes what happened. 
	-  to tie state and actions together, we write a function called a reducer
- Reducer is a function that takes state and action as arguments, and returns the next state of the app.

### Three Principles

- Redux can be described in three fundamental principles:
- The state of your whole application is stored in an object tree within a single store.
- The only way to change the state is to emit an action, an object describing what happened.
- To specify how the state tree is transformed by actions, you write pure reducers.

### Prior Art 先前技术

- Flux
	- store, action, dispatcher, view
- Elm
	- Elm is a functional programming language inspired by Haskell
- Immutable js

### Ecosystem

- Library Integration and Bindings
	- react-redux
	- ng-redux
- Reducers
	- combineSectionReducers
	- redux-data-structures
	- Higher-Order Reducers
		- redux-undo 
		- redux-ignore 
- Actions
	- redux-actions
	- redux-create-types 
- Utilities
	- reselect :Creates composable memoized selector functions for efficiently deriving data from the store state
	- normalizr
- Store
	- redux-watch
	- redux-batched-subscribe 
	- redux-persist 
	- redux-storage 
	- redux-offline 
- Immutable Data
	- immutable-js
	- seamless-immutable 
	- crio
	- icepick 
	- immer
	- object-path-immutable 
	- redux-immutable 
- Side Effects
	- redux-saga
		- Best for: complex async logic, decoupled workflows
	- redux-thunk
		- Best for: getting started, simple async and complex synchronous logic.
	- redux-observable
	- redux-loop
	- redux-logic
	- redux-promise 
- Middleware
	- redux-axios-middleware 
	- redux-socket.io 
	- redux-action-buffer 
- Component State and Encapsulation
	- redux-ui
	- redux-react-local
	- lean-redux
	- redux-subspace
	- redux-doghouse

### Actions

- Actions are plain JavaScript objects. 
	- Actions must have a type property that indicates the type of action being performed. Types should typically be defined as string constants.
	- It's a good idea to pass as little data in each action as possible.
	- 参考 https://github.com/redux-utilities/flux-standard-action
- Actions are payloads of information that send data from your application to your store. 
	- They are the only source of information for the store. 
	- You send them to the store using store.dispatch().
- Action creators are functions that create actions.
-  to actually initiate a dispatch, pass the result to the dispatch() function 
	- `dispatch(addTodo(text))`
- Alternatively, you can create a bound action creator that automatically dispatches
	- `const boundAddTodo = text => dispatch(addTodo(text))`
- The dispatch() function can be accessed directly from the store as store.dispatch(), but more likely you'll access it using a helper like react-redux's ` connect()` . 
	- You can use `bindActionCreators()` to automatically bind many action creators to a dispatch() function.
- Action creators can also be asynchronous and have side-effects.

### Reducers

- Reducers specify how the application's state changes in response to actions sent to the store. 
	- actions only describe what happened, but don't describe how the application's state changes.
- In Redux, all the application state is stored as a single object.
	- You'll often find that you need to store some data, as well as some UI state, in the state tree. 
	- try to keep the data separate from the UI state.
- It's recommended  that you keep your state as normalized as possible, without any nesting. 
	- Keep every entity in an object stored with an ID as a key, and use IDs to reference it from other entities, or lists.
- The reducer is a pure function that takes the previous state and an action, and returns the next state.
	- `(previousState, action) => newState`
	- Things you should never do inside a reducer:
		- Mutate its arguments;
		- Perform side effects like API calls and routing transitions;
		- Call non-pure functions, e.g. Date.now() or Math.random().
- Given the same arguments, reducer should calculate the next state and return it. No surprises. No side effects. No API calls. No mutations. Just a calculation.
- each of these reducers is managing its own part of the global state. The state parameter is different for every reducer, and corresponds to the part of the state it manages.
- like other reducers, combineReducers() does not create a new object if all of the reducers provided to it do not change state.

### Store

- The store has the following responsibilities:
	- Holds application state;
	- Allows access to state via `getState()` ;
	- Allows state to be updated via `dispatch(action)` ;
	- Registers listeners via `subscribe(listener)` ;
	- Handles unregistering of listeners via `the function returned by subscribe(listener)`
- You may optionally specify the initial state as the second argument to createStore().
- `subscribe(listener)`
	- Arguments: `listener (Function)` : The callback to be invoked any time an action has been dispatched, and the state tree might have changed. 

	  You may call getState() inside this callback to read the current state tree. 
	  It is reasonable to expect that the store's reducer is a pure function, so you may compare references to some deep path in the state tree to learn whether its value has changed.

	  - Returns: `(Function)` : A function that unsubscribes the change listener.

### Data flow

- Redux architecture revolves around a strict unidirectional data flow
	- 严格的单向数据流是Redux架构的核心
- The data lifecycle in any Redux app follows these 4 steps
	- You call store.dispatch(action).
		- You can call store.dispatch(action) from anywhere in your app, including components and XHR callbacks, or even at scheduled intervals.
	- The Redux store calls the reducer function you gave it.
		-  It shouldn't perform any side effects like API calls or router transitions. These should happen before an action is dispatched.
	- The root reducer may combine the output of multiple reducers into a single state tree.
	- The Redux store saves the complete state tree returned by the root reducer.
		- This new tree is now the next state of your app! Every listener registered with store.subscribe(listener) will now be invoked; listeners may call store.getState() to get the current state.
	- Now, the UI can be updated to reflect the new state. 
		- If you use bindings like React Redux, this is the point at which component.setState(newState) is called.

### Redux used with React

- Designing Presentational Components
- Designing Container Components
- Passing the Store

### Async Actions

- When you call an asynchronous API, there are two crucial moments in time:
	- the moment you start the call
	- the moment when you receive an answer (or a timeout).
	- Each of these two moments usually require a change in the application state
- Usually, for any API request you'll want to dispatch at least three different kinds of actions:
	- 示例

	

``` 
	{ type: 'FETCH_POSTS_REQUEST' }
	{ type: 'FETCH_POSTS_FAILURE', error: 'Oops' }
	{ type: 'FETCH_POSTS_SUCCESS', response: { ... } }
	```

	

``` 
	{ type: 'FETCH_POSTS' }
	{ type: 'FETCH_POSTS', status: 'error', error: 'Oops' }
	{ type: 'FETCH_POSTS', status: 'success', response: { ... } }
	```

	- Choosing whether to use a single action type with flags, or multiple action types, is up to you or your team.
	- Multiple types leave less room for a mistake, 
-  it's not wise to couple fetching to some particular UI event。
- designing the state shape
	- We store each subreddit's information separately so we can cache every subreddit. When the user switches between them the second time, the update will be instant, and we won't need to refetch unless we want to
	- If you have nested entities, or if you let users edit received entities, you should keep them separately in the state as if it was a database.
-  The standard way to do it with Redux is to use the Redux Thunk middleware.
	- by using this specific middleware, an action creator can return a function instead of an action object.
	- When an action creator returns a function, that function will get executed by the Redux Thunk middleware. 
	- This function doesn't need to be pure;
- Async action creators are especially convenient for server rendering. 

### Async Flow

- Without middleware, Redux store only supports synchronous data flow. This is what you get by default with createStore().
- Asynchronous middleware like redux-thunk or redux-promise wraps the store's dispatch() method and allows you to dispatch something other than actions, for example, functions or Promises. 
	- When the last middleware in the chain dispatches an action, it has to be a plain object. This is when the synchronous Redux data flow takes place.

### Middleware

- Redux middleware provides a third-party extension point between dispatching an action, and the moment it reaches the reducer. 
	- Redux middleware can be used for logging, crash reporting, talking to an asynchronous API, routing, and more.
- middleware实现链式调用

``` 
function logger(store) {
  return function wrapDispatchToAddLogging(next) {
    return function dispatchAndLog(action) {
      console.log('dispatching', action)
      let result = next(action)
      console.log('next state', store.getState())
      return result
    }
  }
}
```

使用es6的箭头函数柯里化

``` 
const logger = store => next => action => {
  console.log('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  return result
}
```

### Usage with React Router

<Provider /> is the higher-order component provided by React Redux that lets you bind Redux to React

- We will wrap <Router /> in <Provider /> so that route handlers can get access to the store.
- React Router comes with a <Link /> component that lets you navigate around your application.
	-  If you want to add some styles, react-router-dom has another special <Link /> called <NavLink />
- React Router Redux 将你的 redux 应用和 react-router 绑定在一起，并且使它们保持同步
	- 如果没有这层绑定，你将不能通过时光旅行来回放 action，除非你需要这个，不然 React-router 和 Redux 完全可以分开操作

## Redux Tips

- we have to consider several things before we start coding, 
	- such as: how to configure a store, store size, data structure, state model, middlewares, environment, async transactions, immutability, etc..
-  UIs are simply data beautifully presented facilitates the process of building them
- 配置 store 时我们需要决定使用哪些 middleware
	-  redux-thunk/saga
	- redux-logger
- Naming Convention
	- Defining a naming convention for your actions at the very beginning of a project and sticking to that convention helps you to scale up as the scope of the project grows.
- redux comes with Scalability
-  the best practice is to keep coding and learning

### Configuring Your Store

- Most apps extend the functionality of their Redux store by adding middleware or store enhancers
	- middleware adds extra functionality to the Redux dispatch function
	- enhancers add extra functionality to the Redux store.
- 可以将所有配置 store 相关的逻辑（包括引入 reducer、middleware、enhancer）都放置于一个单独用于处理它们的文件中
- middlwares 和 enhancers 都被定义为数组，与实际使用它们的函数分离开来，这样可以很容易地为不同情况添加更多的 middleware 或 enhancer

### Implementing Undo History

- 撤销历史也是应用 state 的一部分，无论 state 如何随着时间不断变化，你都需要追踪 state 在不同时刻的历史记录
- state设计

``` 
{
  counterA: {
    past: [ 1, 0 ],
    present: 2,
    future: []
  },
  counterB: {
    past: [ 0 ],
    present: 1,
    future: []
  }
}
```

- 参考 https://cn.redux.js.org/docs/recipes/ImplementingUndoHistory.html

### Isolating Redux Sub-Apps

- 假设一个大应用（对应 <BigApp> 组件）包含了很多小的子应用（对应<SubApp />)
	- 这些 <SubApp> 是完全独立的，并不共享数据或 action，也互不可见且不需要通信
	- 这时最好的做法是不要把它混入到标准 Redux 的 reducer 组件中
	- 对于 “应用集合”，“仪表板”，或者企业级软件这些把多个本来独立的工具凑到一起打包的场景，可以试下子应用的方案
- 为了使用 React API 来隐藏 Redux 的痕迹，可以在组件的构造方法里初始化 store 并把它包到一个特殊的组件中
- 如果应用间需要共享数据，不 推荐使用这个模式

### Redux FAQ

https://cn.redux.js.org/docs/FAQ.html  

- When should I use Redux?
	- 推荐优先使用原生的框架系统来解决问题，因为这对于构建你的应用来说已经足够了
	- 当应用已经达到相当的复杂程度，以至“状态储存到哪了”、“状态怎么变化的”这样的问题开始困扰你，这就是学习 Redux 的时候
	- 在尝试与修改的过程中理解Redux对问题的抽象过程
	- redux是为了解决 “当有确定的状态发生改变时，数据从哪里来” 这种可预测行为的问题
	- redux要求你在应用程序中遵循特定的约定：应用的状态需要存储为纯数据的格式、用普通的对象描述状态的改变、用不可更新的纯函数式方式来处理状态变化
	- 这也成了抱怨是“样板代码”的来源

- How do I share state between two reducers? Do I have to use combineReducers?
	- store推荐的结构是将 state 对象按键值切分成 “层”（slice） 或者 “域”（domain），并提供独立的 reducer 方法管理各自的数据层
	- combineReducers is not necessary—it is simply a utility function for the common use case of having a single reducer function per state slice, with plain JavaScript objects for the data.
	- combineReducers 不是 必须的，它仅仅是通过简单的 JavaScript 对象作为数据，让 state 层能与 reducer 一一关联的函数而已
	- 要在reducer之间共享数据，combineReducers 不允许此种行为，解决方法如下
		- If a reducer needs to know data from another slice of state, the state tree shape may need to be reorganized so that a single reducer is handling more of the data.
		- You may need to write some custom functions for handling some of these actions. This may require replacing combineReducers with your own top-level reducer function. 
		- Async action creators such as redux-thunk have access to the entire state through getState(). 
			- An action creator can retrieve additional data from the state and put it in an action, so that each reducer has enough information to update its own state slice.
		-  reducers are just functions—you can organize them and subdivide them any way you want, and you are encouraged to break them down into smaller, reusable functions (“reducer composition”). 
			- While you do so, you may pass a custom third argument from a parent reducer if a child reducer needs additional data to calculate its next state. 
			- You just need to make sure that together they follow the basic rules of reducers: `(state, action) => newState` , and update state immutably rather than mutating it directly.

- Do I have to use the switch statement to handle actions?
	- No. The `switch` statement is the most common approach, but it's fine to use if statements, a lookup table of functions, or to create a function that abstracts this away. 
	- In fact, while Redux does require that action objects contain a type field, your reducer logic doesn't even have to rely on that to handle the action. 
	- the standard approach is definitely using a switch statement or a lookup table based on type.

- Do I have to put all my state into Redux? Should I ever use React's setState()?
	- no right answer
		- Some users prefer to keep every single piece of data in Redux, to maintain a fully serializable and controlled version of their application at all times. 
		- Others prefer to keep non-critical or UI state, such as “is this dropdown currently open”, inside a component's internal state.
	- Using local component state is fine.
	- Some common rules of thumb for determining what kind of data should be put into Redux:
		- Do other parts of the application care about this data?
		- Do you need to be able to create further derived data based on this original data?
		- Is the same data being used to drive multiple components?
		- Is there value to you in being able to restore this state to a given point in time (ie, time travel debugging)?
		- Do you want to cache the data (ie, use what's in state if it's already there instead of re-requesting it)?
		- Do you want to keep this data consistent while hot-reloading UI components (which may lose their internal state when swapped)?
	- There are a number of community packages that implement various approaches for storing per-component state in a Redux store instead, such as redux-ui, redux-component
		- It's also possible to apply Redux's principles and concept of reducers to the task of updating local component state as well
		- `this.setState( (previousState) => reducer(previousState, someAction)).`
		

- Can I put functions, promises, or other non-serializable items in my store state?
	- It is highly recommended that you only put plain serializable objects, arrays, and primitives into your store. 
	- It's technically possible to insert non-serializable items into the store, but doing so can break the ability to persist and rehydrate the contents of a store, as well as interfere with time-travel debugging.

- How do I organize nested or duplicate data in my state?
	- Data with IDs, nesting, or relationships should generally be stored in a “normalized” fashion: each object should be stored once, keyed by ID, and other objects that reference it should only store the ID rather than a copy of the entire object. 
	- It may help to think of parts of your store as a database, with individual “tables” per item type.
	- normalizr and redux-orm can provide help and abstractions in managing normalized data.

- Should I put form state or other UI state in my store?
	- Based on those rules of thumb, most form state doesn't need to go into Redux, as it's probably not being shared between components. 
	- You might choose to keep some form state in Redux because you are editing data that came from the store originally
	-  it may be a lot simpler to keep the form state local to the component, and only dispatch an action to put the data in the store once the user is done with the form.
	- If you are keeping form state in Redux, you should take some time to consider performance characteristics. Dispatching an action on every keystroke of a text input probably isn't worthwhile
	- Other kinds of UI state follow these rules of thumb as well. The classic example is tracking an isDropdownOpen flag. In most situations, the rest of the app doesn't care about this, so in most cases it should stay in component state. 
		- However, depending on your application, it may make sense to use Redux to manage dialogs and other popups, tabs, expanding panels, and so on.
- Can or should I create multiple stores? Can I import my store directly, and use it in components myself?
	- it is possible to create multiple distinct Redux stores in a page, but the intended pattern is to have only a single store. 
		- Having a single store enables using the Redux DevTools, makes persisting and rehydrating data simpler, and simplifies the subscription logic.
	- Some valid reasons for using multiple stores in Redux might include:
		- Solving a performance issue caused by too frequent updates of some part of the state, when confirmed by profiling the app.
		- Isolating a Redux app as a component in a bigger application, in which case you might want to create a store per root component instance.
	- However, creating new stores shouldn't be your first instinct, especially if you come from a Flux background. 
		- Try reducer composition first, and only use multiple stores if it doesn't solve your problem.
	- while you can reference your store instance by importing it directly, this is not a recommended pattern in Redux.
		- If you create a store instance and export it from a module, it will become a singleton. This means it will be harder to isolate a Redux app as a component of a larger app

		

- Is it OK to have more than one middleware chain in my store enhancer? What is the difference between next and dispatch in a middleware function?
	- Redux middleware act like a linked list. 

	  Each middleware function can either call `next(action)` to pass an action along to the next middleware in line, 
	  call `dispatch(action)` to restart the processing at the beginning of the list, 
	  or do nothing at all to stop the action from being processed further.

    - This chain of middleware is defined by the arguments passed to the `applyMiddleware()` function used when creating a store. 
    	- Defining multiple chains will not work correctly, as they would have distinctly different dispatch references and the different chains would effectively be disconnected.

- How do I subscribe to only a portion of the state? Can I get the dispatched action as part of the subscription?
	- redux provides a single store.subscribe method for notifying listeners that the store has updated. 

	  Listener callbacks do not receive the current state as an argument—it is simply an indication that something has changed. 
	  The subscriber logic can then call getState() to get the current state value.
       - UI bindings such as React Redux can create a subscription for each connected component. 
	  It is also possible to write functions that can intelligently compare the old state vs the new state, and execute additional logic if certain pieces have changed.
       - The new state is not passed to the listeners in order to simplify implementing store enhancers such as the Redux DevTools. 
       - subscribers are intended to react to the state value itself, not the action. Middleware can be used if the action is important and needs to be handled 
       

- Is there always a one-to-one mapping between reducers and actions?
	- No. We suggest you write independent small reducer functions that are each responsible for updates to a specific slice of state. We call this pattern “reducer composition”
		- A given action could be handled by all, some, or none of them. 
	- This keeps components decoupled from the actual data changes, as one action may affect different parts of the state tree
		-  you should break out of such a paradigm any time you feel you want to handle an action in many reducers.

- What async middleware should I use? How do you decide between thunks, sagas, observables, or something else?
	- `redux-thunk` are best for complex synchronous logic (especially code that needs access to the entire Redux store state), 

	    and simple async logic (like basic AJAX calls). With the use of async/await, it can be reasonable to use thunks for some more complex promise-based logic as well.

	- `redux-saga` are best for complex async logic and decoupled "background thread"-type behavior, 

	    especially if you need to listen to dispatched actions (which is something that can't be done with thunks). They require familiarity with ES6 generator functions and redux-saga's "effects" operators.

	- `redux-observable` solve the same problems as sagas, but rely on RxJS to implement async behavior. They require familiarity with the RxJS API.

- Should I dispatch multiple actions in a row from one action creator?
	- There's no specific rule for how you should structure your actions.

- reducer 中的不变性是如何导致组件非必要渲染的？
	- 在一个 reducer 里，如果你返回了一个没有进行任何修改、与原对象一模一样的拷贝，Redux 的 combineReducers 函数仍会认为 state 需要更新，因为你返回了一个与传入的 state 对象完全不同的对象。
	- combineReducers 会把这个新的根 state 对象返回给 store。新的对象与原有的根 state 对象的值是相同的，但由于对象本身不同，会导致 store 更新，从而所有已连接的组件都进行了毫无必要的重新渲染。
	- 为了防止这种现象的发生，当 reducer 没有改变 state 时，你必须直接返回的传入的 state 层。

- 浅比较和深比较有何区别？  
	- 浅比较（也被称为 引用相等）只检查两个不同 变量 是否为同一对象的引用；与之相反，深比较（也被称为 原值相等）必须检查两个对象所有属性的 值 是否相等。

	  所以，浅比较就是简单的（且快速的）a === b，而深比较需要以递归的方式遍历两个对象的所有属性，在每一个循环中对比各个属性的值。
	  正是因为性能考虑，Redux 使用浅比较。
	  

- Redux 是如何使用浅比较的？
	- combineReducers 函数使用浅比较来检查根 state 对象（root state object）是否发生变化，有修改时，返回经过修改的根 state 对象的拷贝，没有修改时，返回当前的根 state 对象

- React-Redux 是如何使用浅比较的？
	- React-Redux 使用浅比较来决定它包装的组件是否需要重新渲染。

	  为了检测改变是否发生，React-Redux 会保留一个对根 state 对象的引用，还会保留 mapStateToProps 返回的 props 对象的每个值的引用。
	  最后 React-Redux 会对根 state 对象的引用与传递给它的 state 对象进行浅比较，还会对每个 props 对象的每个值的引用与 mapStateToProps 返回的那些值进行一系列浅比较。

- What are the issues with using plain JavaScript for immutable operations?
	- 不小心直接修改了对象
	- 重复代码
	- 性能问题

	

- Won't calling “all my reducers” for each action be slow?
	- It's important to note that a Redux store really only has a single reducer function. The store passes the current state and dispatched action to that one reducer function, and lets the reducer handle things appropriately.
	- the common suggested pattern is to have a separate sub-reducer function that is responsible for managing updates to a particular slice of state at a specific key. 

	  The combineReducers() that comes with Redux is one of the many possible ways to achieve this. 
	  It's also highly suggested to keep your store state as flat and as normalized as possible.

- Do I have to deep-clone my state in a reducer? Isn't copying my state going to be slow?
	- Common Redux misconception: you need to deeply clone the state. 
	- Reality: if something inside doesn't change, keep its reference the same!

- How can I reduce the number of store update events?
	- If you use React, note that you can improve performance of multiple synchronous dispatches by wrapping them in ReactDOM.unstable_batchedUpdates()

- Will having “one state tree” cause memory problems? Will dispatching many actions take up memory?
	- First, in terms of raw memory usage, Redux is no different than any other JavaScript library. The only difference is that all the various object references are nested together into one tree
	- Second, a typical Redux app would probably have somewhat less memory usage than an equivalent Backbone app because Redux encourages use of plain JavaScript objects and arrays rather than creating instances of Models and Collections.
	- Finally, Redux only holds onto a single state tree reference at a time. Objects that are no longer referenced in that tree will be garbage collected, as usual.

	

- Will caching remote data cause memory problems?
	- Caching data will cause performance problems when the size of the cache approaches the amount of available memory. 
		- This tends to be a problem when the cached data is exceptionally large or the session is exceptionally long-running.
	- First, only cache as much data as the user needs.
	- Second, cache an abbreviated form of a record when possible. 
	- Third, only cache a single copy of a record. T

##  API Reference

## changelog

- 4.0.1-20181013
	- Use same return type for both StoreCreator signatures
	- Mark StoreCreator's preloadedState argument as optional
	- Add ES browser build
	- Throw an error if createStore is passed several enhancers
	- Upgrade to Babel 7
- 4.0.0-20180418
	- Make middleware API dispatch pass through all call arguments
	- Make bindActionCreators transparently pass `this`
	- Add DeepPartial type for preloaded state
	- The major changes are around TypeScript definitions, bundled CommonJS and ES builds
- 3.7.0-20170617
	- The biggest change, and the reason for the minor bump, is the UMD build is now done via `Rollup`
	- Remove filtering inside compose
	- Simplify compose
- 3.6.0-20160905
	- Add module entry point for webpack 2
	- Added a Redux logo
	- TypeScript: Improve typings for compose function 
- 3.1.0-20160129
	- createStore() now receives an enhancer such as applyMiddleware() as the last optional argument
	- The old way of doing things still works, too.
- 3.0.0-20150913
	- Action objects now must have a type property other than undefined
- 2.0.0-20150901
	- getReducer() is removed from Store public API 
	- compose() now acts like a proper compose()
	- process.env.NODE_ENV is required for CommonJS build 
- 1.0.0-20150815
	- If `dispatch` is attempted while reducer is executing, an error is thrown.
		-  you can dispatch from lifecycle hooks just fine. 
		- It's only reducers that are not allowed to dispatch. 
	- new official url to github
	- React-specific code has been moved to react-redux and will be versioned separately
	- 参考 https://github.com/reduxjs/redux/releases?after=v3.0.0
- 0.2.0-20150602
	- initial public release

# react-redux 

- react-redux is the official React binding for Redux.      
- It lets your React components read data from a Redux store, and dispatch actions to the store to update data.

## dev-tips

## resources

- docs
    - https://react-redux.js.org/introduction/quick-start

## react-redux docs 
