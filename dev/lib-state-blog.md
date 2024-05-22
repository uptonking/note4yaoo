---
title: lib-state-blog
tags: [blog, dev, state]
created: 2020-11-02T05:18:43.747Z
modified: 2021-05-13T03:12:40.723Z
---

# lib-state-blog

# state-blog

## 🌰 [The History of State Management at CodeSandbox - CodeSandbox _202312](https://codesandbox.io/blog/the-history-of-state-management-at-codesandbox)

- At the inception of the CodeSandbox application, Redux was the big hype. 
  - as CodeSandbox grew it had two problems: understanding how the application works and it had subpar performance.
  - Even though Redux allowed us to narrow down what state components require, it is impossible for a human being to infer how the scope of the state will affect the component reconciliation performance as a whole.

- This led us to our second iteration: Cerebral JS. 
  - The performance gains came from us combining Cerebral with Mobx.
  - Cerebral JS, with its exotic declarative sequence API, would never work with TypeScript. 

- Overmind was born and it was built from the ground up to be a spiritual successor to Cerebral.
  - But one day we wanted to make TypeScript even stricter, so we turned on strictNullChecks.

- Around this time, CodeSandbox had become a company and we were planning, unknowingly at the time, our move into the Cloud Development Environment space. 
  - In the web ecosystem, state machines were the big thing and we also experimented with this
  - we had challenges with performance again as we were relying on React contexts to share state

- With our fifth approach, we embrace the fact that React has contexts to share state management across components, allowing us to initialize state closer to where it is used and take advantage of React data fetching patterns. 
  - The only real problem with contexts is their performance. 
  - With `Impact` we create a reactive context instead, using reactive primitives
  - With Impact and React, the observability is tied to the component. The drawback of that is that you are not as “surgically” updating the actual element bound to a signal, but you keep your control flow in the language.
  - as components only reconcile based on signals accessed, it is a huge performance boost regardless.

## [wordpress frontend: Our Approach to Data](https://github.com/Automattic/wp-calypso/blob/trunk/docs/our-approach-to-data.md)

- [wordpress client utils](https://github.com/Automattic/wp-calypso/tree/trunk/client/lib)

- History
- First Era: Emitter Objects (June 2014 - April 2015)
  - Our original approach to managing data took an object-oriented approach, wherein an instance of the store would inherit the `EventEmitter` interface.
  - Typically, a single instance of each object store was shared across the entire application
  - Used in combination with a data-observe mixin, a developer could monitor an instance of the store passed as a prop to a React component to automatically re-render its contents if the store emitted a change event.
- Second Era: Facebook Flux (April 2015 - December 2015)
  - a unidirectional data flow in which stores can only be manipulated via actions dispatched by a global dispatcher object.
  - data can only be accessed by using helper ("getter") methods from the exported object. 
  - Much like the event emitter object approach, a Flux store module inherits from the EventEmitter interface, though a Flux store should only ever emit a change event
- Third Era: Redux Global State Tree (December 2015 - February 2020)
  - a single store instance which maintains all state for the entire application
- Fourth Era: Modularized Redux State Tree (February 2020 - Present)
  - instead of creating a single monolithic root reducer on boot, the goal is instead to have individual reducers register themselves when needed. This is done synchronously and automatically through dependency graph resolution.
  - Modularized reducers are not imported in the root reducer
  - Modularized portions of state include an init module that registers the reducer as a side effect

- Data Normalization
- When a subject needs to refer to another part of the tree, store a reference (likely an ID). 
  - Tracking an indexed set of items makes it easy to navigate the tree when needing to perform a lookup.
  - data is normalized in a way such that it is always kept in sync, avoiding duplication, and facilitating lookup.

- splitting data and visual concerns:
  - Presentational and Container Components
- An app component wraps a visual component, connecting it to the global application state. 
  - We use the react-redux library to assist in creating bindings between React components and the Redux store instance.
- Query components
  - Query components accept as few props as possible to describe the data needs of the context in which they're used. 
  - They are responsible for dispatching the actions that fetch the desired data from the WordPress.com REST API. 
  - They should neither accept nor render any children. 自身作为leaf，没有children
  - That they neither accept nor render children eliminates the need for ancestor components to concern themselves with the data needs of leaf components and can be more performant.

- it's important to distinguish when and why it's appropriate to use the Redux store over, say, a React component's state.
  - We recommend that you only use the global state tree to store user interface state when you know that the data being stored should be persisted between page views, or when it's to be used by distinct areas of the application on the same page
  - I don't have the same expectation that this interaction be preserved when I later leave and return to the page. In these cases, it might be more appropriate to use React state to track the expanded status of the component, local only to the current rendering context. 

- Persisting our Redux state to browser storage (IndexedDB) allows us to avoid completely rebuilding the Redux tree from scratch on each page load and to display cached data in the UI (instead of placeholders) while fetching the latest updates from the REST API is still in progress.

### [Reactivity and Loading States](https://github.com/Automattic/wp-calypso/blob/trunk/docs/reactivity.md)

- If something changes on the server, Calypso needs to be able to reflect that without user intervention. 
- We currently have a `data-poller` module that continuously request data from the server, but we may switch that to an open `WebSocket` connection in the future to establish a more explicit flow of data from both sides. 
  - To achieve this, initially, we had a simple `data-observe` module that handled the event listeners and re-rendered a component when its registered props emitted a change event. 
  - We have since moved towards more robust Redux-like approaches to handle these flows.

- [Data Poller](https://github.com/Automattic/wp-calypso/tree/trunk/client/lib/data-poller)

- Poller is an abstraction that can be used to add polling to any data module that uses the following conventions:
  - The module emits change events when data changes and expects consumers to bind to the change event to be notified when a change occurs
  - Uses the EventEmitter or a derivative to emit the change event
  - Has a method or public function that can be called to initiate an AJAX request for new data
  - The data module is a single object instance that is used throughout

- The module works by initiating polling when the data module has one or more objects listening for a change and stopping when there are no longer any change events bound. 
  - Polling is also paused when the visibility state of the page changes to hidden and resumed when the page is focused.

### [Server-side Rendering](https://github.com/Automattic/wp-calypso/blob/trunk/docs/server-side-rendering.md)

- When rendering on the server, we have a special set of constraints that we need to follow when building components and libraries.
- tl; dr: 
  - Don't depend on the DOM/BOM; 
  - make sure your initial render is synchronous; 
  - don't mutate class variables; 
  - add a test to `renderToString` your server-side rendered page.

- Because it is necessary to serve the redux state along with a server-rendered page, we use two levels of cache on the server: one to store the redux state, and one to store rendered layouts.
- data cache
  - At render time, the Redux state is serialized and cached, using the current path as the cache key, unless there is a query string, in which case we don't cache.
  - This means that all data that was fetched to render a given page is available the next time the corresponding route is hit
- render cache
  - There is a shared cache for rendered layouts
  - Multiple paths resulting in the same rendered content should ideally map to one cache entry

- I want to server-side render my components!
  - Have a look at the Isomorphic Routing docs to see how to achieve this. 
- In addition, there are a couple of things you'll need to keep in mind: 
  - if your components need dynamic data, we'll need to cache; 
  - `renderToString` is synchronous, and will affect server response time; 
  - you should add a test to your section that ensures that it can really be rendered with renderToString; 
  - if you want to SSR something logged in, dependency nightmares will ensue.

### [Isomorphic Routing](https://github.com/Automattic/wp-calypso/blob/trunk/docs/server-side-rendering.md)

- Isomorphic routing means that you define your routes (i.e. what middleware to run for which path) only once, using them both on the client, and the server.
- The contract is that at the end of each route's middleware chain, context.layout should contain the React render tree to be rendered, which will be done magically by either the client or the server render, as appropriate. 
  - (This is clearly different from the previous client-side-only routing approach where you'd have to render to #primary/#secondary DOM elements.)

## [现代前端框架响应模型对比: Vue, Mobx, React, Redux - 掘金](https://juejin.cn/post/6929727475304005639)

- 一个核心流程是 state 映射到 view，这里是渲染和更新过程，虚拟 dom 在这个过程发挥作用，
  - 而如何订阅和处理 state 的变更则是另一个核心流程，也就是响应过程。
- 数据状态发生变化时通知方式的区别是目前 React 和 Vue 两大阵营之间的最大差异。
- React的响应的方式最简单直接，代码中通过 setState 触发数据变化，然后会直接通知组件进行更新。
  - 跟 React 配套的 Redux 也是一样，state 更改后会直接通知全部相关视图进行更新，而是否真的需要更新则留给视图自己做决定。
  - 实际上 React/Redux 的模型就是全体数据统一通知，Redux 是应用的全体数据，而 React setState 是组件的全体数据，没有更细的粒度。

- Vue 的响应过程则要精细的多，我们可能或多或少都有了解，它的发布订阅模型是精细到数据的每一个属性的

- 发布订阅模型有两个角色，发布者和订阅者，对前端模型来说，发布者就是 state，订阅者则是渲染函数，或者其他一些响应函数，比如 computed 和 watch 函数。

- Vue 需要在两个方面做处理来让他们形成精细的发布订阅关系。通过劫持待发布对象的 get 方法，同时对可能成为订阅者的函数包装 effect 方法，effect 方法会在函数执行的时候将全局 currentEffect 设为当前执行函数，从而在有方法使用了 get 的时候取 currentEffect 为订阅函数，进而存储数据对象、属性和订阅函数之间的关系。再通过劫持 set 方法，就可以在属性变化的时候通过关系找到订阅函数去执行。

- 但从另一个角度看，正是由于 React 没有使用基于 mutable 的响应模型，使得它的数据状态历史更加容易追溯，简单的发布模型，也使得 Redux 中间件成为可能，他们在大型项目中可以定义出更加可维护的逻辑写法，比如 Redux saga。

- Mobx 与 Vue 的响应模型接近，实际上它是最早把这种细粒度响应模型抽象并且推广开来的框架。

- 人们把 Mobx 与 React 一起使用，Mobx 来处理发布订阅模型，React 做单纯的视图层。实际上，Mobx 的响应模型可以拿出来做很多事，比如 Formily 用 Mobx 的响应模型实现了复杂表单的高性能，滴滴的跨端框架 CML 的数据层 chameleon-store 用 Mobx 模拟了 Vuex 的 api。

- Mobx 的 api 基本上能与 Vue 3.0 的 Reactive 模块的 api 对应上
- observable => reactive
- observer => effect
- computed => computed
- autorun => watch
- Mobx 的核心实现思路与 Vue 也大致相同，同样是劫持对象属性的 get set，在订阅函数执行的时候全局记录当前执行函数。
  - 不同的是记录发布订阅关系是记录在每个 observable 实例的 $mobx 对象中的，由抽象的 Atom 类型管理。
  - 整体思路上有observable 和 derivation 两个类型作为基础的响应逻辑模型，observable 是发布者，derivation 是订阅者。
  - derivation 是 Mobx提出的概念，autorun 和 reaction 继承自 derivation，computed 则是 observable 和 derivation 的综合体，对这些通用概念的系统抽象使得 Mobx 成为一个更通用的响应式框架。
  - 注意，Mobx 是一个 functional reactive programming，即函数式响应式编程，并不能说是响应式编程，reactive programming，因为 reactive programming 是特指事件流式的编程形式，在 js 里面的相应实现是 Rxjs。

- 除了基本的发布订阅之外，Vue 和 Mobx 还需要处理一些其他问题，比如对于他们都有的 computed 概念，触发顺序是一个重要问题。

## [The best part of Effector - DEV Community_202110](https://dev.to/effector/the-best-part-of-effector-4c27)

- problem
  - Creating complex business scenarios frequently includes waiting for all computations to be completed. 
  - Moreover, if an application is built over event-oriented architecture, it will be quite difficult to define the end of events processing. 
  - In the common case, we need this opportunity in two situations. 
  - The first one is widely used, any good application requires it. 
  - The second one is more specific, but it is pretty important too.

- We have identified a problem of waiting for computations to be completed, so let us see how classic state managers solve it.
- redux itself does not have any mechanism to handle asynchronous actions and side effects. 
  - A common application uses something like redux-saga or redux-thunk
  - The simplest way to detect the end of computations is to add the new action “computations is ended”. It is a simple and working solution, but it has a fatal problem — you (as an engineer) should think about “end-of-computations” actions in any scenario, you should adopt a domain-specific logic to it.
  - Another option is to put the whole scenario logic to a single entity (thunk, saga, whatever). In this case, we can just wait for the end of the entity.
- MobX uses the same techniques as Redux for the solution of our problem. E.g., we can just add a boolean property to the store and wait for its changes 
  - So, it is working, except for one thing. We cannot use this solution for a complex scenario, if it works with many stores.
  - Moreover, we can put the whole scenario in single asynchronous function, it will simplify the tests

- In Effector-world, we can fix it with a special function `allSettled`. 
  - It starts a unit (event or effect) and waits for end of computations on the specified scope. 
  - To get a state of store in particular scope, we can use `scope.getState` method.
  - Fork API has a built-in mechanism to replace any effect-handler in a specific scope

- So, we decided to use Effector because it is based on multi-stores. It helps to create more solid applications and develop them in large teams

## [My State Management Mistake](https://epicreact.dev/my-state-management-mistake/)

- Frankly, what happened was we decided to avoid Redux, but then grabbed another library and made the same mistakes that made Redux such a problem: Almost all state was globally managed by the library.
- If I could go back in time and could only say one thing, here's what I would say: 
  - Server cache is not the same as UI state, and should be handled differently.
  -  React Query is simply the perfect abstraction that can handle the server cache for me.
- And once my server cache is handled so perfectly by react-query, I don't have enough state left to feel like I need a library for the rest of it. 
  - React is a state management solution and it's a really good one when you componentize your state like you do your UI.

## [What is state? Why do I need to manage it?](https://egghead.io/articles/what-is-state-why-do-i-need-to-manage-it)

- When it comes to client-side JavaScript applications, I like to think of state as “the outcome of all of the actions that the user has taken since the page loaded”.
- This isn’t an all-encompassing way of thinking about state, 
  - as other agents might affect state — the server might set some variables, a service worker might do something in the background, etc. 
  - However, I found it a useful place to start when I was building my understanding.
- when we manage our state, we create an explicit data structure (in my case, an object with a key named ‘errors’) to record the outcomes of the user’s actions.
- State management libraries provide us with tools for creating these data structures, and updating them when new actions occur. 
  - For example, with Redux, your state is stored as a JavaScript object. 
  - With MobX, it’s stored as an Observable. 
  - If you use React’s component state, your state could be a string, or a number, or anything you like.

- Without a state management system, how do we know what the state of our application is? 
  - We look at the DOM. We can check DOM elements to see if they have certain classes (‘active’, ‘error’), or to check whether certain elements exist.
- With a state management system, to find out what the state of our application is, 
  - we check our state data structure. 
  - The DOM should reflect the data, but the data is the Source Of Truth.

- **Why would I want to use state management tools?**
  - For me, the key to understanding state management was when I realised that there is always state. 
  - Whether or not I’m managing it, with an interactive web application, there is always state — users perform actions, and things change in response to those actions.
  - State management makes the state of your app tangible(可触摸到的，可感知的，具体的) in the form of a data structure that you can read from and write to. 
  - It makes your ‘invisible’ state clearly visible for you to work with.
  - Rather than looking at the DOM and deducing(推断、追溯) state based on what is there and what is not, an explicit data structure is much easier to understand.
  - When you’re creating larger and more complex JavaScript applications, having explicit data to work with in a predictable way is a huge boon to developers. 
  - It’s much easier to reason about and manipulate, and it’s less bug-prone (though of course, you can still create a lot of bugs with any code you write with a state management system).

- Some bonus benefits to understanding state management
  - Before working with JavaScript frameworks, I had never thought of the actions that a user makes as a holistic(整体的，全面的) group of causes and effects. 
    - The way I had written JavaScript before, it was just a bunch of one-off operations that manipulated the DOM and may or may not have had any relation to each other.
  - I also never saw ‘state’ and the DOM as separate entities from each other — to me, they were the same thing. 
    - In the DOM, there is an error message, so the state is that there is an error message.
  - By separating out the data (there is an error message) from the effects (an error message is displayed on the screen), I found myself thinking about my code in a much more declarative way, which was extremely powerful as I learned more and took a a dive into functional programming.

## [为什么要做状态管理](https://zhuanlan.zhihu.com/p/140073055)

- 近年来，随着单页面应用的兴起，JavaScript 需要管理比任何时候都要多的状态，或者可以说是数据，这些状态可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等
- 就是把业务的信息渲染出来，并进行人机交互，返回给服务端，这是前端技术解决的核心问题
- 几乎所有的 web 系统都不会把用户的一些数据和系统的状态维护在客户端，例如用户的会员信息
- 现在的状态管理已经成为了前端开发技术栈的一个主题
  - 数据流的方向性管理，如 Flux
  - 系统状态的框架性工具管理，例如 Redux，Mobx
  - 组件生命周期内的状态管理，例如在 React 中使用 setState 或者 hooks
- 现在前端开发谈及状态管理，其实就是指的是像 Redux 这样的东西，用单一数据流的思想指导整个系统，并把状态存储到特定的地方，在 UI 组件层通过一些选择器把需要组件取出，渲染到 UI 上。
- 状态管理的工具库并不仅仅有 Redux，像 Mobx，Vuex 等，都是十分优秀的库，思想也大抵相似。
  - 像 Angular 技术栈，有人会通过 Angular Service 这个载体，利用 Rxjs 做简单的状态管理，也有亮点
  - 状态管理设计这个事情并不需要囿于框架和工具库，甚至在工具库中也可以有自己的玩法。
- 好的状态管理应该做到 UI 层独立，并让状态管理的逻辑尽量少侵入到 UI 层
  - 除了 UI 层，也应该对那些核心逻辑进行建模和分层，维护双核心。
  - 不过，除了一些富应用（例如思维导图应用，drawio 一样的工具），我十分不建议在前端放过多的领域/业务逻辑。
- 单一数据源要求客户端应用的关键数据都要从同一个地方获取，而单向数据流要求应用内状态管理的参与者都要按照一条流向来获取数据和发出动作，不允许双向交换数据
  - 单一数据源保证了 UI 渲染的单纯性和可预测性，只需要对单一来源的数据做出响应，来什么样的数据就通过可以预测的数据来转换 UI
  - 单向数据流通过限制数据和动作的流向令数据可以进行追溯，可以实现一些日志打印，热加载，时间旅行，同构应用等功能，另一个作用是在 UI 层对状态变更进行控制反转(Inversion of Control)，从而实现解耦的目的。
- 状态管理的好处
  - 能有效分离 UI 层和数据处理层
  - 帮助前端应用结构化数据
  - 有效控制状态的变化
  - 处理同步与异步
  - 实现一些日志打印，热加载，时间旅行，同构应用等功能
- 状态管理也有缺点
  - 就是代码会变得更复杂
    - 这一点并不完全是缺点，当一个应用业务用例和代码量不断上升的时候，代码不可能维持简单

## [Write your own javascript state management library](https://medium.com/swlh/write-your-own-javascript-state-management-library-3687d3c09aae)

- State management is basically a two-way path management: 
  - you should let your application update the state 
  - and you should notify other parts of your application that the state has been changed, so they could react to this and do whatever they need to.
- The first part is the easy one. 
  - All we have to do is write a class that has an internal state (an object) 
  - and a method that when called change this state accordingly to the new state received by the method.
  - For this we’ll use getter and setter pattern to retrieve the state and to deny directly state changing (return false).
  - To change the state in an immutable way, we’ll provide the setState method. 
  - and we’ll make it possible to set the initial state by using the constructor method.

```JS
const clone = o => JSON.parse(JSON.stringify(o));

const isObject = val => val != null && typeof val === 'object' && Array.isArray(val) === false;

// 提供状态读写的api
class Store {

  #internalState;

  constructor(initialState = {}) {
    if (!isObject(initialState)) throw new Error('initial state must be a object');
    this.#internalState = initialState;
  }

  get state() {
    return clone(this.#internalState);
  }

  set state(value) {
    return false;
  }

  setState(value) {
    if (!isObject(value)) throw new Error('value must be a object');
    const currentState = clone(this.#internalState);
    const nextState = Object.assign(clone(currentState), clone(value))
    this.#internalState = nextState
    return nextState;
  }
}
```

- we must think about a way to let other parts of the application know the state have changed. 
  - For this we’ll be using one very know pattern in the development world: pubsub, or publisher-subscriber.

```JS
// 提供状态变化时执行回调函数的api
class PubSub {

  #callbackList;

  constructor() {
    this.#callbackList = [];
  }

  publish(state) {
    if (!isObject(state)) throw new Error('state should be and object');
    this.callbackList.forEach(callback => {
      callback(state);
    });
  }

  subscribe(callback) {
    if (typeof callback !== 'function')
      throw new Error('callback should be a function');
    this.#callbackList = [
      ...this.#callbackList,
      callback
    ];
    return true;
  }
}
```

```JS
// 使用示例
const store = new Store();

const firstCallback = state => { console.log('first callback', state) };
const secondCallback = state => { console.log('second callback', state) };

store.subscribe(firstCallback);
store.subscribe(secondCallback);

store.setState({ a: 1 });
store.setState({ b: 1 });
```

- you’ll see that everything works 
  - and whenever the state is modified, both callback functions are called and the state is logged in the console.

- This seems good for small applications, 
  - but in most cases we only want to execute the callback function when certain parts of the state are modified, 
  - otherwise we can have unnecessary code execution, leading to performance issues. 
  - The pubsub pattern implements this using named channels. 
  - So whenever you want to subscribe, you need to inform the channel you’re interested. 
  - The same happens to the publish method, you must inform in which channel the information must be published, so the correspondent subscribers are notified.

- This kind of solution doesn’t seem optimal, at least to me. 
  - So we’ll try to make another type of implementation. 
  - where subscribers have to inform in which part of the state they’re interested in.
- In the available solutions in the market, there’s one that implements this kind of solution the most easy way (IMHO): React-redux `connect` method.
  - the connect method first parameter `mapStateToProps`, is a function that receives the updated state and returns an object that is part of this state. 
  - This way the connect method knows if it must update the component’s props or not.
- We can do the same in our little state management library. 
  - Whenever someone wants to subscribe to the state changes, it will pass the callback function and other function similar to the mapStateToProps. 
  - We’ll call this second function the config function from now on.

- With this assumption, well change our `subscribe` method to receive these two functions and store them in an object (`{callback, config}`) in the callbackList array. 
  - In our `publish` method, we’ll receive the current and next state that is stored in the `Store` class.
  - Then inside the loop that’s responsible to call the callback functions, we’ll apply both states to the config function of each subscriber and check if they’re not equal. 
  - When this is true, we’ll then call the callback function passing the result of the next state applied to the config function. 
  - It all seems too difficult when reading like this, but as soon as we make the code you’ll see it’s very simple.

```JS
const clone = o => JSON.parse(JSON.stringify(o));
const isObject = val => val != null && typeof val === 'object' && Array.isArray(val) === false;
const isEqual = (a, b) => JSON.stringify(a) === JSON.stringify(b)

class PubSub {

  #callbackList;

  constructor() {
    this.#callbackList = [];
  }

  publish(currentState, nextState) {
    if (!isObject(currentState)) throw new Error('currentState should be and object');
    if (!isObject(nextState)) throw new Error('nextState should be and object');
    this.callbackList.forEach(item => {
      const currentValue = item.config(currentState);
      const nextValue = item.config(nextState);
      if (!isEqual(currentValue, nextValue)) {
        item.callback(nextValue);
      }
    });
  }

  subscribe(callback, config) {
    if (typeof callback !== 'function')
      throw new Error('callback should be a function');
    if (typeof config !== 'function')
      throw new Error('config should be a function');
    this.#callbackList = [
      ...this.#callbackList,
      { callback, config }
    ];
    return true;
  }
}

class Store {

  #internalState;
  #pubsub;

  constructor(initialState = {}) {
    if (!isObject(initialState)) throw new Error('initial state must be a object');
    this.#internalState = clone(initialState);
    this.#pubsub = new Pubsub()
  }

  get state() {
    return clone(this.#internalState);
  }

  set state(value) {
    return false;
  }

  setState(value) {
    if (!isObject(value)) throw new Error('value must be a object');
    const currentState = clone(this.#internalState);
    const nextState = Object.assign(clone(currentState), clone(value))
    this.#internalState = nextState
    this.#pubsub.publish(currentState, nextState)
    return nextState;
  }

  subscribe(callback, config) {
    return this.#pubsub.subscribe(callback, config)
  }

}
```

```JS
// 使用示例
const store = new Store();

const firstCallback = state => { console.log('first callback', state); };
const firstConfig = state => { return { a: state.a }; };

const secondCallback = state => { console.log('second callback', state) };
const secondConfig = state => { return { b: state.b }; };

store.subscribe(firstCallback, firstConfig);
store.subscribe(secondCallback, secondConfig);

store.setState({ a: 1 });
store.setState({ a: 2 });
store.setState({ b: 1 });
store.setState({ b: 2 });
```

- When you execute the code above, 
  - the first callback will be called two times, and the correspondent a value will be logged. 
  - Then the second callback is called twice, logging only b value, first 1 then 2. 
  - The a value is not logged because it’s not defined in the second config function.

## [Build a state management system with vanilla JavaScript_2018](https://css-tricks.com/build-a-state-management-system-with-vanilla-javascript/)

- https://github.com/hankchizljaw/vanilla-js-state-management
- https://github.com/hankchizljaw/beedle
  - /306Star/MIT/201006/js
  - A tiny library inspired by Redux & Vuex to help you manage state in your JS apps
  - creates a central store that enables you predictably control 

- Traditionally, we’d keep state within the DOM itself or even assign it to a global object in the window
- Libraries like Redux, MobX and Vuex make managing cross-component state almost trivial(微不足道的，不重要的)
  - This is great for an application’s resilience and it works really well with a state-first, reactive framework such as React or Vue.
- Take a look at what we’re building. It’s a "done list"

- Pub/Sub
- We’re creating the functionality that allows other parts of our application to subscribe to named events.
- Another part of the application can then publish those events, often with some sort of relevant payload.
- The PubSub pattern loops through all of the subscriptions and fires their callbacks with that payload.
- It’s a great way of creating a pretty elegant reactive flow for your app

- The core Store object
- The Store is our central object.
- Each time you see `import store from '../lib/store.js`, you’ll be pulling in the object that we’re going to write. 
  - It’ll contain a `state` object that, in turn, contains our application state, 
  - a `commit` method that will call our >mutations, 
  - and lastly, a `dispatch` function that will call our actions. 
  - Amongst this and core to the Store object, there will be a Proxy-based system that will monitor and broadcast state changes with our PubSub module.
- Let’s take a look at how our `Store` object keeps track of all of the changes. 
  - We’re going to use a Proxy to do this
  - If we add a `get` trap, we can monitor every time that the object is asked for data. 
  - Similarly with a `set` trap, we can keep an eye on changes that are made to the object.
  - when a mutation runs something like `state.name = 'Foo'` , this trap catches it before it can be set and provides us an opportunity to work with the change or even reject it completely. 
- There’s a lot going on there, but I hope you’re starting to see 
  - how this is all coming together and importantly, 
  - how we’re able to maintain state centrally, thanks to Proxy and Pub/Sub.

- Now that we’ve got our front-end components(Counter) and our main Store, all we’ve got to do is wire it all up.

## [Stateful Components in Vanilla JS](https://yamagata-developers-society.github.io/blog/stateful-components-vanilla-js/)

- Today I’d like to show you how to create stateful components with vanilla JavaScript, and demonstrate 
  - You don’t need to download any library to apply the amazing concepts used by React.js in your JavaScript programming.
- Even though we can’t benefit from React’s virtual DOM or setState({}) method, this is a powerful way to think and program — and there is no external dependency to worry about!
- What are the benefits?
  - Write organized, reactive code without the increased bundle size
  - Simplify DOM manipulations and state logic
  - Improve the versatility and strength of your standard JavaScript coding!

- [demo on jsfiddle](https://jsfiddle.net/jzft0o7r/)

```HTML
<div class="App__container" id="app">
  <div>Count: <span id="display">0</span></div>

  <button onclick="incCountUp()">+Count</button>
</div>
```

```CSS
.App__container {
  padding: 15px;
}

.Score {
  font-size: 28px;
}

.text-error {
  color: red;
}

.text-success {
  color: green;
  font-size: 40px;
}
```

```JS
const display = document.getElementById("display");

//  start with a simple object, which will represent the initial state of our data
const state = {
  count: 0,
}

// Components
const counter = count => {
  let classname = "text-error";

  if (count > 10) {
    classname = "text-success";
  }

  return (
    `<p class="Counter">Count: <span class="${classname}">${count}</span></p>`
  );
};

// Render Function
function renderCount() {
  display.innerHTML = counter(state.count);
}

// Update methods
function incCountUp() {
  let newCount = state.count + 1;
  state.count = newCount;

  renderCount();
}

renderCount();
```

# ref
- [Simple State Management With Vanilla JS](https://viktorfejes.com/article/simple-state-management-with-vanilla-js)
  - The most important part is that the state shouldn't be updated through its properties but rather using the state.setState() method. 
  - This way it's easy to know using the stateChange() function when the state updates.
