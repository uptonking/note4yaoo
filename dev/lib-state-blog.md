---
title: lib-state-blog
tags: [blog, dev, state]
created: '2020-11-02T05:18:43.747Z'
modified: '2021-05-13T03:12:40.723Z'
---

# lib-state-blog

# state-blog

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

``` JS
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

``` JS
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

``` JS
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

``` JS
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

``` JS
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
  - Beedle creates a central store that enables you predictably control 

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

``` HTML
<div class="App__container" id="app">
  <div>Count: <span id="display">0</span></div>

  <button onclick="incCountUp()">+Count</button>
</div>
```

``` CSS
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

``` JS
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
