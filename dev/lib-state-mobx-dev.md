---
title: lib-state-mobx-dev
tags: [mobx, state]
created: 2023-04-07T03:10:37.987Z
modified: 2023-04-07T03:10:46.225Z
---

# lib-state-mobx-dev

# guide

- pros
  - popular with signals

- cons
  - 设计模式不是immutable
  - 示例很多使用@装饰器
  - bundle size

- who is using #mobx
  - reka/craftjs
  - apps: linear
  - [Who uses MobX?](https://github.com/mobxjs/mobx/discussions/681)
# dev
- Mobx数据管理方案，采用观察者模式，观察可变数据，持有细粒度的数据响应模式，感知到哪些组件需要被更新的时间复杂度是`O(1)`的
# rewrite
- https://github.com/liam61/minbx
  - [从零到 observable 一个 object 如何](https://github.com/liam61/blog/blob/master/js/mobx-source/1.observable-an-object.md)

- https://github.com/Jacky-Summer/mini-mobx /js
  - 模拟实现 MobX 的 observable 和 autorun 方法
# examples
- https://github.com/xaviergonz/mobx-keystone /ts
  - https://mobx-keystone.js.org/
  - A MobX powered state management solution based on data trees with first class support for Typescript, support for snapshots, patches and much more
  - it tries to combine the best features of both immutability (transactionality, traceability and composition) and mutability (discoverability, co-location and encapsulation) based approaches to state management
  - Central in mobx-keystone is the concept of a living tree. 
  - By default trees can only be modified by using an action that belongs to the same subtree
  - because changes can be detected on a fine-grained level, JSON patches are supported out of the box.
  - because it supports snapshots, action middlewares and replayable actions out of the box, it is possible to replace a Redux store and reducer with a MobX data model. This makes it possible to connect the Redux devtools to mobx-keystone.

- https://github.com/EasyWebApp/WebCell /202402/ts
  - https://web-cell.dev/WebCell/
  - Web Components engine based on VDOM, JSX, MobX & TypeScript

## mobx-view

- https://github.com/botverse/vdom-mobx-example /201606/js
  - Small example on how to use virtual-dom with MobX

- https://github.com/ryansolid/mobx-jsx /MIT/202210/ts/inactive
  - Raw MobX performance without being restrained by a Virtual DOM
  - a demonstration of how MobX fine grain control can be leveraged directly in JSX for considerably better performance than pairing it with a Virtual DOM library
  - It compiles JSX to DOM statements and wraps expressions in functions that can be called by the library of choice.
    - Unlike Virtual DOM only the changed nodes are affected and the whole tree is not re-rendered over and over.
  - MobX JSX works both with function and Class components
  - MobX JSX also supports a Context API.
  - Alternatively supports Tagged Template Literals or HyperScript
  - Tagged Template solution is much more performant that the HyperScript version, but HyperScript opens up compatibility with some companion tooling
  - [Solid and mobx-jsx comparison _202005](https://github.com/ryansolid/mobx-jsx/issues/17)

## undo/time-travel

- https://github.com/httptoolkit/mobx-shallow-undo /apache2/202209/ts/inactive
  - Zero-config undo & redo for Mobx

- https://github.com/mobxjs/mobx-devtools /MIT/202106/js/inactive
  - Mobx Devtools (React, Chrome Extension) - Looking for maintainers
  - Track changes in MobX observables
  - MST support

- https://github.com/zalmoxisus/mobx-remotedev /MIT/201902/js/inactive
  - MobX DevTools extension
  - Remote debugging for MobX with Redux DevTools extension
  - 🍴 forks
    - https://github.com/hlhr202/mobx-remotedev /MIT/202107/js/inactive
  - [MobX 6 (Cannot obtain atom from undefined) ](https://github.com/zalmoxisus/mobx-remotedev/issues/55)
    - I've switched from Redux devtools to a simple browser logger: kubk/mobx-log ; I am going to add Redux devtools support but for me it's no longer needed, because the logger already covers most of its usecases like inspecting store, calling actions and computeds.
  - [Roadmap _201607](https://github.com/zalmoxisus/mobx-remotedev/issues/1)
    - Support for non-browser environment (unify with remotedev)
    - As far as I know the Slider monitor just reverts to a previous state and then reapplies actions after that point. That's all what replaying does.
  - [redux-devtools integrations for js and non-js frameworks](https://github.com/reduxjs/redux-devtools/blob/main/extension/docs/Integrations.md)
  - https://github.com/zalmoxisus/remotedev /MIT/201812/js/inactive
    - Remote debugging for any flux architecture.
    - https://github.com/zalmoxisus/remotedev/tree/master/examples
    - 示例包括 redux/flux/alt/rxjs/reflux
  - https://github.com/zalmoxisus/remotedev-app /MIT/201812/js/inactive
    - Web, Electron and Chrome app for monitoring remote-redux-devtools. Can be accessed on remotedev.io

- https://github.com/antitoxic/mobx-redux-devtools /201607/js
  - Sync redux-devtools with mobx structure and get of all devtool goodness like time-travel (undo/redo), persistence, charts, etc.

- https://github.com/BrascoJS/delorean /201711/js/inactive
  - A MobX-React Time Travel Debugger

## utils

- https://github.com/sindresorhus/on-change /js
  - Watch an object or array for changes
  - It works recursively, so it will even detect if you modify a deep property like `obj.a.b[0].c = true`.
  - Uses the `Proxy` API.
# docs
- `runInAction(fn)`: Use this utility to create a temporary action that is immediately invoked. 
  - Can be useful in asynchronous processes. 
  - [Mobx - runInAction() usage. Why do we need it? - Stack Overflow](https://stackoverflow.com/questions/57271153/mobx-runinaction-usage-why-do-we-need-it)
    - The short answer is: you don't really need runInAction. You can write an application without using it, and it should work just fine.
    - But if you're working on a larger codebase, and you want to enforce some best practices, you can use the mobx feature "enforce actions / strict mode", which basically enforces that any modification to the state must happen inside of an action. This is useful because actions make it obvious why a piece of state changed, and they provide useful debugging information in the mobx devtools.
    - By default, MobX 6 and later require that you use actions to make changes to the state. However, you can configure MobX to disable this behavior.

- 
- 
- 
- 
- 
- 
- 

# blogs
- [Cool Software | Benchmarking MobX-State-Tree Performance](https://coolsoftware.dev/blog/benchmarking-mobx-state-tree/)

##  🆚️ [Comparison with Other Frameworks — Vue2](https://v2.vuejs.org/v2/guide/comparison.html)

- MobX has become quite popular in the React community and it actually uses a nearly identical reactivity system to Vue. 
  - To a limited extent, the React + MobX workflow can be thought of as a more verbose Vue, so if you’re using that combination and are enjoying it, jumping into Vue is probably the next logical step.

## [Mobx 思想的实现原理，及与 Redux 对比 - 知乎](https://zhuanlan.zhihu.com/p/25585910)

- Mobx 最关键的函数在于 autoRun，
  - 这个函数非常智能，用到了什么属性，就会和这个属性挂上钩，从此一旦这个属性发生了改变，就会触发回调，通知你可以拿到新值了。
  - 没有用到的属性，无论你怎么修改，它都不会触发回调，这就是神奇的地方。
- 使用 autoRun 实现 mobx-react 非常简单，核心思想是将组件外面包上 autoRun，这样代码中用到的所有属性都会像上面 Demo 一样，与当前组件绑定，一旦任何值发生了修改，就直接 forceUpdate，而且精确命中，效率最高。
- autoRun 的专业名词叫做依赖收集，也就是通过自然的使用，来收集依赖，当变量改变时，根据收集的依赖来判断是否需要更新。

- 为了兼容，Mobx 使用了 Object.defineProperty 拦截 getter 和 setter，但是无法拦截未定义的变量，为了方便，我们使用 proxy 来讲解，而且可以监听未定义的变量哦。

- 本文限于篇幅没有讲彻底。其实这种方式是一种懒初始化，具体怎么实现的呢。
  - 当我们 `const obj = observer({// 层次很深的对象})` 的时候，并不会递归生成 proxy 替代，而是仅在最外层生成 proxy，
  - 然后通过给 get 加入 **用到某个属性，并且这个属性是对象，就重新返回 observer 后的此属性，这个属性如果层级深了，也不会递归，而是继续给他加 get，以此类推** 的方式，在访问到的时候动态绑定的，有点绕，应该描述清楚了，
  - 同理，set 也是 proxy 的时候加上的，因此并不会初始化全部加上。

- 其实跟 Vue, Knockout, Meteor Tracker 原理是一样的，这套前端用的最早的应该还是 knockout。

- Mobx 其实就是 Vue 的核心，自动收集依赖。这样理解正确吗
  - vue 没有直接使用 mobx，但原理是一致的。

- 没有研究过vue的源码不清楚vue的原理是怎么实现的，但是感觉可以做到触发get时候才绑定set，这样应该会提高不少性能（对于mobx）。
  - 不会的，绑定所有set最多也只是拖了一点初始化的时间而已

## [从零开始用 proxy 实现 mobx](https://github.com/ascoders/blog/issues/19)

- [精读《dob - 框架实现》](https://github.com/ascoders/weekly/blob/master/%E5%89%8D%E6%B2%BF%E6%8A%80%E6%9C%AF/35.%E7%B2%BE%E8%AF%BB%E3%80%8Adob%20-%20%E6%A1%86%E6%9E%B6%E5%AE%9E%E7%8E%B0%E3%80%8B.md)

- https://github.com/dobjs/dob
  - Dob is a tool for monitoring object changes. Using Proxy
  - state management tool using proxy.

## [从零实现 Mobx：深入理解 Mobx 原理 ](https://github.com/yinguangyao/blog/issues/54)

- https://github.com/yinguangyao/simple-mobx

- Mobx 和 Redux 不同的地方是 Mobx 是一个响应式编程（Reactive Programming）库，在一定程度上可以看做没有模板的 Vue，基本原理和 Vue 一致
- Mobx 借助于装饰器的实现，使得代码更加简洁易懂。由于使用了可观察对象，所以 Mobx 可以做到直接修改状态，而不必像 Redux 一样编写繁琐的 actions 和 reducers。

- Mobx 的执行流程和 Redux 有一些相似，简单的概括一下，一共有这么几个步骤：
  - 页面事件（生命周期、点击事件等等）触发 action 的执行。
  - 通过 action 来修改状态。
  - 状态更新后，computed 计算属性也会根据依赖的状态重新计算属性值。
  - 状态更新后会触发 reaction，从而响应这次状态变化来进行一些操作（渲染组件、打印日志等等）。

- 由于 Redux 监听的是整个 store 的变化，所以无法准确的监听到 B、C、D 变化后才重新计算 A。 
  - 但是 Mobx 中提供了 computed 来解决这个问题。
  - computed 是基于现有状态或计算值衍生出的值

- autorun 接收一个函数，当这个函数中依赖的可观察属性发生变化的时候，autorun 里面的函数就会被触发
- reaction 则是和 autorun 功能类似，但是 autorun 会立即执行一次，而 reaction 不会，
  - 使用 reaction 可以在监听到指定数据变化的时候执行一些操作，有利于和副作用代码解耦。
  - reaction 和 Vue 中的 `watch` 非常像。
- 看到 autorun 和 reaction 的用法后，也许你会想到，如果将其和 React 组件结合到一起，那不就可以实现很细粒度的更新了吗？ 没错，Mobx-React 就是来解决这个问题的。
- Mobx-React 中提供了一个 observer 方法，这个方法主要是改写了 React 的 render 函数，当监听到 render 中依赖属性变化的时候就会重新渲染组件，这样就可以做到高性能更新。

- mobx 原理
- 实现上用到了 `Object.defineProperty` 或者 `Proxy`。
  - 当 autorun 第一次执行的时候会触发依赖属性的 getter，从而收集当前函数的依赖。
  - 当依赖属性触发 setter 的时候，就会将所有订阅了变化的函数都执行一遍，从而实现了数据响应式。

- 这个发布订阅模型要比 React 精细得多，因而 Vue 的性能要比未经优化的 React 好很多，从某种程度上讲，也正是因为 React 的性能问题更突出，才需要有更先进的渲染调度架构 React Fiber 的出现。
  - 作者没有真正理解react和vue的发展吧。
  - 这里我说一下我的见解。
  - 首先vue1没有虚拟dom为什么vue2要加上，竟然vue的发布订阅要比react精细。实际上这种精细是以牺牲性能为代价的。
  - vue1为data的每一个属性配置一个watcher, 每一个属性变化就通知视图更新，所以粒度更加精细。
  - 实际这种方法根本没法适应大型项目开发，试想一个页面100个watcher是什么情况。
  - 这也是vue2中要引入虚拟dom只为每个组件配置一个watcher的原因，这是不得不承认的。
  - 我并不想在这里又引起一次关于react和vue优劣的讨论。但有些事实不吐不快。
  - vue2借鉴react引入虚拟dom是事实，vue3借鉴hooks也是事实。这里可能不是原理上的借鉴，而是编程思想上的借鉴。
  - setup的写法解决的首要问题和hooks是一致的这个一目了然。

- Vuex的响应原理跟vue是一样的，因为对比的是响应原理，不是用法

## 🆚️ [Comparing reactivity models - React vs Vue vs Svelte vs MobX vs Solid vs Redux _202008](https://dev.to/lloyds-digital/comparing-reactivity-models-react-vs-vue-vs-svelte-vs-mobx-vs-solid-29m8)

- In React, reactive state is created using the useState hook - it returns the state itself, and a setter function to update the state.
  - When the setter is called the whole component re-renders - this makes it really simple to declare derived data - we simply declare a variable that uses the reactive state.
  - It's possible to run a function whenever some reactive state changes using the useEffect hook.
  - There's one downside to Reacts reactivity model - the hooks (useState and useEffect) have to always be called in the same order and you can't put them inside an if block. 

- In Vue we can declare reactive values using the ref function from the Composition API. 
  - It returns a reactive value with a value property that tracks everytime you access it. 
  - We can declare derived values using the computed function. 
  - Updating state is as simple as writing to the .value prop of reactive data. Arrays can be changed directly using push, pop, splice and other array methods.
  - We can run effects when some data changes using watchEffect - it takes a function that runs whenever a reactive value used inside changes.

- Svelte uses a "radical new approach" to building UI - it's a compiler that generates code and leaves no traces of the framework at runtime.
  - any variable declared with let can be reactive. Derived data is declared with the $: label

- MobX is a state management solution and can be used with React, Vue or any UI library. 
  - we first pass some data to observable to make it observable.
  - Updating values is very simple - we can use all the common array methods like push, pop, slice etc. on observable arrays.
  - The only caveat is that MobX doesn't actually track usage, but rather it tracks data access, so you have to make sure you access the data through a property inside the observer component.
  - Running effects is as simple as passing the effect to autorun. Any observable or computed values accessed in the function become the effect dependency - when they change, the effects re-runs.

- Solid is kinda like if React and Svelte had a baby
  - We can create observable state using createSignal
  - To create derived data we can use createMemo
  - createEffect function that also tracks dependencies, but instead of returning values it just runs some arbitrary effect.

- Redux is a predictable state container for JavaScript apps.
  - To define the initial state we use the createSlice
  - Derived data can be defined by creating selectors 
  - Running effects when state changes can be achieved by simply subscribing to the store using store.subscribe and passing it a function that runs whenever the state changes.
  - Only thing to remember is that in Redux you have to dispatch the actions.
# blogs-rewrite
- [手写实现MobX的observable和autorun方法 | JackySummer](https://jacky-summer.github.io/2021/01/01/%E6%89%8B%E5%86%99%E5%AE%9E%E7%8E%B0MobX%E7%9A%84observable%E5%92%8Cautorun%E6%96%B9%E6%B3%95/)
  - [手写状态管理库: Mobx - 掘金](https://juejin.cn/post/7076329672706883591)
  - https://github.com/Jacky-Summer/mini-mobx /js

- [实现一个简单的 MobX](https://xie.infoq.cn/article/d90440a8fb574299b4454ef96)

- [mobx的原理以及 仿写自己的状态管理库](https://lastnigtic.cn/posts/mobx/)

## [Build your own MobX-like state management library in 40 lines of code

](https://czaplinski.io/blog/make-your-own-mobx/)

- We want our library to build up a mapping between every property available in the store and a list of components that should re-render when that property changes.
# more

# discuss-mobx

- ## 

- ## 

- ## [Undo Redo manager with mobx-utils `deepObserve` _202202](https://github.com/mobxjs/mobx/discussions/3281)
- here's a new version that runs synchronously: codesandbox.io/s/mobx-undo-redo-v4-mwyi6

- ## [Performant undo without spies in MobX 4+ _201810](https://github.com/mobxjs/mobx/issues/1764)
- I think the freshly released `deepObserve` utility should be able to help you out
  - Unfortunately, I don't think we can guarantee that the state is fully cycle-free.

- ## [Q: building an undo/redo using Mobx 5 _201807](https://github.com/mobxjs/mobx/issues/1630)
- snapshots are not the best basis for undo/redo, patches are more
reliable if you are building a multi actor system (e.g. changes are being received from the server, which you don't want to undo)
  - To record mutations without MST,  `deepObserve` from mobx-utils can now be used

- ## [I'm confused a bit with spy removal at 5.x. _201902](https://github.com/mobxjs/mobx/issues/1906)
- You might want to try `mobx-utils.deepObserve` instead. 
  - Spy triggers on anything, not just the relevant pieces of your model, so it isn't a scalable solution
