---
title: lib-state-redux-blog
tags: [blog, redux, state]
created: 2020-11-03T13:12:54.267Z
modified: 2021-05-13T03:19:30.464Z
---

# lib-state-redux-blog

# guide

# blogs

## 🆚️ [redux, koa, express 中间件实现对比解析](https://segmentfault.com/a/1190000016386740)

- 本文主要对比redux, koa, express 的中间件实现，为了更直观，我会抽取出三者中间件相关的核心代码，精简化，写出模拟示例。
  - https://github.com/nanjixiong218/analys-middlewares

- 大部分人了解的express和koa的中间件差异在于：
  - express采用“尾递归”方式，中间件一个接一个的顺序执行, 习惯于将response响应写在最后一个中间件中；
  - 而koa的中间件支持 generator, 执行顺序是“洋葱圈”模型。
- 不过实际上，express 的中间件也可以形成“洋葱圈”模型，在 next 调用后写的代码同样会执行到，
  - 不过express中一般不会这么做，因为 express的response一般在最后一个中间件，那么其它中间件 next() 后的代码已经影响不到最终响应结果了; 

- express本质上就是一个中间件管理器，当进入到 app.handle 的时候就是对中间件进行执行的时候，所以，最关键的两个函数就是：
  - app.use 添加中间件
  - app.handle 尾递归调用中间件处理 req 和 res
- 全局维护一个stack数组用来存储所有中间件，app.use 的实现就很简单了 this.stack.push(fn)
  - express 的真正实现当然不会这么简单，它内置实现了路由功能
- app.handle 即对 stack 数组进行处理
  - 这里就是所谓的"尾递归调用"，next 方法不断的取出stack中的“中间件”函数进行调用，同时把next 本身传递给“中间件”作为第三个参数，每个中间件约定的固定形式为 (req, res, next) => {}, 这样每个“中间件“函数中只要调用 next 方法即可传递调用下一个中间件。
  - 之所以说是”尾递归“是因为递归函数的最后一条语句是调用函数本身，所以每一个中间件的最后一条语句需要是next()才能形成”尾递归“，否则就是普通递归，”尾递归“相对于普通”递归“的好处在于节省内存空间，不会形成深度嵌套的函数调用栈。

- koa代码基于ES6实现，支持generator(async await), 没有内置的路由实现和任何内置中间件
  - 和 express 不同，因为没有router的实现，所有this.middleware 中就是普通的”中间件“函数而非复杂的 layer 实例
- 处理的关键在compose方法, 和express中的next是不是很像，
  - 只不过他是promise形式的，因为要支持异步，所以理解起来就稍微麻烦点
- 这里和express很不同的一点就是，**koa的响应的处理并不在"中间件"中**，而是在中间件执行完返回的promise.resolve后
  - 通过 handleResponse 最后对响应做处理，”中间件“会设置ctx.body, handleResponse也会主要处理 ctx.body，所以 koa 的”洋葱圈“模型才会成立，await next()后的代码也会影响到最后的响应。

- redux核心的”中间件" 实现部分即 applyMiddleware.js
  - redux 中间件提供的扩展是在 action 发起之后，到达 reducer 之前，它的实现思路就和express 、 koa 有些不同了，它没有通过封装 store.dispatch, 在它前面添加 中间件处理程序，而是通过递归覆写 dispatch ，不断的传递上一个覆写的 dispatch 来实现。
  - 每一个 redux 中间件的形式为 store => next => action => { xxx }
  - 这里主要有两层函数嵌套
  - 最外层函数接收参数store, 这一层是为了把 store 的 api 传递给中间件使用，主要就是两个api: getState, dispatch
  - 第二层的数组，数组的每个元素都是这样一个函数next => action => { xxx }, 这个函数可以理解为 接受一个dispatch返回一个dispatch, 接受的dispatch 是后一个中间件返回的dispatch.
  - 现在在来理解 `dispatch = compose(...chain)(store.dispatch)` 就相对容易了，`原生的 store.dispatch` 传入最后一个“中间件”，返回一个新的 dispatch , 再向外传递到前一个中间件，直至返回最终的 dispatch, 当覆写后的dispatch调用时，每个“中间件“的执行又是从外向内的”洋葱圈“模型。
- redux 中间件的实现中还有一点实现也值得学习，为了让”中间件“只能应用一次，applyMiddleware 并不是作用在 store 实例上，而是作用在 createStore 工厂方法上
- redux 的中间件使用可以有两种写法
- 第一种：用 applyMiddleware 返回 enhance 增强 createStore
  - store = applyMiddleware(middleware1, middleware2)(createStore)(reducer, initState)
- 第二种: createStore 接收一个 enhancer 参数用于自增强
  - store = createStore(reducer, initState, applyMiddleware(middleware1, middleware2))

- 总结
  - 总体而言，express 和 koa 的实现很类似，都是next 方法传递进行递归调用，只不过 koa 是promise 形式。
  - redux 相较前两者有些许不同，先通过递归向外覆写，形成执行时递归向里调用。
- 总结一下三者关键异同点（不仅限于中间件）：
  - 实例创建： express使用工厂方法, koa是类
  - koa实现的语法更高级，使用ES6，支持generator(async await)
  - koa没有内置router, 增加了ctx全局对象，整体代码更简洁，使用更方便。
  - koa中间件的递归为promise形式，express使用while 循环加 next 尾递归
  - 我更喜欢 redux 的实现，柯里化中间件形式，更简洁灵活，函数式编程体现的更明显
  - redux 以 dispatch 覆写的方式进行中间件增强

- 有人说，express中也可以用 async function 作为中间件用于异步处理? 
  - ~~其实是不可以的，因为 express 的中间件执行是同步的 while 循环，当中间件中同时包含 普通函数 和 async 函数 时，执行顺序会打乱~~
  - 2020-03-10 问题修正: express的中间件可以使用 async, 只要不是按洋葱圈的方式使用

- [Redux, Koa, Express之middleware机制对比](https://www.jianshu.com/p/922194db2ae2)

- express
  - 由于是在ES6之前出现的，所以中间件的基础原理还是callback方式
- koa
  - koa1得益于generator特性并通过co框架加入了自动流程管理。（co会把所有generator的返回封装成为Promise对象）
  - koa2则使用了Async/Await的形式（仅仅知识genertator函数的语法糖）
- redux
  - 更准确的应该是异步的action的方式。
  - 解决异步action的方式有多种，比如：redux-thunk, redux-saga, redux-promise等
- Koa是Express框架原班人马基于ES6新特性重新开发的敏捷开发框架。
  - Express主要是基于Connect中间件框架，其自身封装了大量的功能，比如路由、请求等。
  - 而Koa是基于co(koa2基于async/await)中间件框架，框架自身并没集成太多功能，大部分功能需要用户自行require中间件去解决。
- redux的compose跟上文中的koa-compose有些类似。
  - 属于函数式编程中的组合，它将chain中的所有匿名函数[f1, f2, f3, ..., fn]组成一个新的函数，即新的dispatch
  - dispatch = f1(f2(f3(store.dispatch)))
  - 这时调用新dispatch，每一个middleware就依次执行了。
- middleware通过next(action)一层层处理和传递action直到redux原生的dispatch。
  - 而如果某个middleware使用store.dispatch(action)来分发action，就相当于重新来一遍。

- express
  - 中间件为一个方法，接受 req, res, next 三个参数。
  - 中间可以执行任何方法包括异步方法。
  - 最后一定要通过res.end或者next来通知结束这个中间件方法。
  - 如果没有执行res.end或者next访问会一直卡着不动直到超时。
  - 并且在这之后的中间件也会没法执行到。

- koa
  - 中间件为一个方法或者其它，接受ctx, next两个参数。
  - 方法中可以执行任何同步方法。可以使用返回一个Promise来做异步。
  - 中间件通过方法结束时的返回来判断是否进入下一个中间件。
  - 返回一个Promise对象koa会等待异步通知完成。then中可以返回next()来跳转到下一个中间件。
  - 如果Promise没有异步通知也会卡住。

- Redux
  - 中间件为一个方法，接受store参数。
  - 中间可以执行任何方法包括异步方法。
  - 中间件通过组合串联middleware。
  - 通过next(action)处理和传递action直到redux原生的dispatch, 或使用store.dispatch(action)来分发action。
  - 如果一只简单粗暴调用store.dispatch(action)，就会形成无限循环。

- [koa redux middleware 深入解析](https://www.cnblogs.com/dh-dh/p/7475083.html)

- 对于中间件的处理，redux重写了dispatch方法，在dispatch action的时候先经过一遍中间件，流式的通过中间件处理，再进行dispatch。
  - dispatch触发之后，需要经过各个自执行的中间件。
  - next的后的代码其实是可以用的，但是有一点问题就是还是执行顺序的问题，如果某个中间件是异步执行，执行顺序就无法保证了。

- koa 1.x的时候支持了generator，现在支持了async函数，
  - 所以现在的koa的中间件系统是“洋葱圈”式的处理方式，也就是上面的先执行每个中间件的before，再倒叙执行xxx函数。
  - 值得一提的点就是koa为async函数特制的compose函数，async函数的awiat需要每次异步都是一个promise，如果为值，那就是同步处理。所以返回的middleware都被包了一层Promise.resolve。

## [Redux without React — State Management in Vanilla JavaScript_201610](https://www.sitepoint.com/redux-without-react-state-management-vanilla-javascript/)

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

```JS
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

```JS
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

## [Life after Redux: React’s new APIs can provide pause as to whether or not it is a necessity in your next app](https://itnext.io/life-after-redux-21f33b7f189e)

- There are many benefits to using Redux.
  - It allows developers to easily share state data between different components throughout an application via the use of helper libs such as react-redux.
  - You get control flow, a middleware pattern and the resulting ecosystem of middleware extensions available.
  - By using a single master store, you can be sure your state remains consistent which has been an issue prior to Redux and Flux with certain MVC patterns.
  - Subsequently centralisation allows for developers to potentially explore and debug application state over time a technique supported by Redux Devtools also known as time travel debugging.
  - The state reducer pattern is an effective and simple way to manage and configure atomic state changes and importantly Redux provides a common language and conventions for managing state within JavaScript applications.
- So that all is great however Redux is still not without some problems:
  - Redux tends towards becoming a global dependency that will have its tentacles throughout your codebase.
  - It can lead developers to be tempted to store far more state globally than is actually required.
  - Redux is considered as a state management container but is often used as an event bus which is a practice that depending on context could be considered an anti-pattern.
  - Redux does not deal well with asynchronicity out of the box and requires middleware to even support async events.
  - Redux does not deal with side effects out of the box either.
  - Integration with other implicit state management containers such as Routers have always been problematic.
  - You don’t actually need Redux to manage your application data because of the new React APIs.

- The (`state, action) => state` Reducer is at the heart of Redux as it controls the transformation stage of a data transaction. 
- When building a Redux driven React app you might want to think about the building blocks looking a little like this
  - A Component dispatches data in the form of an Action to the Pub/Sub or Event Bus implementation within Redux.
  - The Pub/Sub sends the data through a series of Middleware that manipulate the Action proceed with a mutation or defer it. I like to call this Transaction Pre-processing
  - Eventually the Action is sent through to a Transaction Engine which runs a pure Reducer function to merge the current State with the given Action immutably to produce a new state tree.
  - The new state tree is stored in a Data Store which exists as an in memory object but can also be cached elsewhere such as localStorage or a database.
  - The State Dependency Injector receives changes from the data store and provides the new state to components that require it
  - A recipient Component finally receives the new state and re-renders displaying the updated data.
- You can think about this flow and the technology mix that provides each piece in the following way where react-redux is the state dependency injector and redux itself provides several pieces. 

- The useReducer hook also manages to provide an immutable data store. 
- Then we can take advantage of the new useContext API to act as a state dependency injector. 

- Now above you can see that what is missing is a Pub/Sub (or Event System) and a Transaction Pre-processor.
- Some might argue that `useReducer` provides an Event System already in that it exposes a `dispatch` function that can be shared to children. 
  - The thing is that because of the details of React’s Fibre re-write and eventually-consistent state resolution, there is no easy way to apply a sequential transaction-preprocessing layer to useReducer. 
  - Basically this means it is far less problematic to use dispatch as a client of an Event System and the influx into the React side of the transaction as opposed to the Event System itself. 
  - You also get an extra advantage in separating your event dispatcher from your state which becomes important when you are temporally tying app contexts together that should not mix their data.
- There are also some concerns about `createContext`’s performance in terms of being able to render very fast state updates to a large shared state redux tree. 
- One of the things you gain by separating your event bus out from your state management is 
  - the ability to treat each part of state differently in terms of it’s performance requirements. 
  - So for most situations, using React’s createContext will be fine 
  - but when you require faster update performance, one technique available to you is to simply listen directly to dispatched events from the event bus and manage this internally with a local cache if required.

- With projects such as reinspect allowing developers to hook up Devtools to useReducer and useState, there is now no hard dependency on Redux for Redux devtools anymore

- So what should you actually use as your event system? 
- You might consider something like RxJS because you get a transaction pre-processing engine for free.
- Alternatively, we could use the isomorphic port of Node’s EventEmitter module to dispatch events. 
- This will work but it doesn’t support listening to wild-carded or name-spaced events which can be useful when we want to separate out sections of our app to only respond to relevant events. 
- I have found success with EventEmitter2 that allows for wildcard events. 
- It may not be for everyone but my technique was to wrap this in a simple Event Bus API that contains good TypeScript support providing only the small subset of the features I actually needed in an Event Bus. 
- I have created my own library for this technique called ts-bus .
- https://github.com/ryardley/ts-bus
  - TypeScript event bus to help manage your application architecture
- Either of these arrangements provides more flexibility than using Redux alone.

- There are many benefits to separating out the Event System from state management.
- You don’t always need state to change based on an event
  - Whilst it is common for state to be changed in response to an event, you don’t always need to connect state change with an event. 
  - Sometimes all that is needed is to start an asynchronous background process and have it report when it is done. 
  - Bringing external state in where it is not required leads to added complexity and overhead.
- You have limited your dependency exposure to a small simple component
  - An eventing system will become a major dependency hazard for any large app as every component that has to communicate with another will need to have access to an instance of your event dispatcher. 
  - By using a separate Event System we have avoided automatically connected state management to all your app components.
- You can manage asynchronicity however you like
  - Events are no longer tied to state change so async becomes easier. 
  - Want to use an async function to manage asynchronous events? 
  - Easy. You control how asynchronicity is managed and what state dependencies you have available. 
  - Admittedly, implementing a cancellable saga workflow is more difficult but that is never an easy problem to solve to begin with and is rarely actually required.
- It’s simple to track state in a separate store such as a Router
  - Occasionally state needs to be managed but cannot be tracked in your state container. 
  - This most often occurs with navigation where state is held within the browser URL via some kind of Router. 
  - Having a separate Event System means that you can easily provide a point of abstraction for your Router. 
  - An added benefit to this technique is that you don’t need to share your router code all over your application.
- You have the flexibility of an event driven architecture
  - By using a simple Event Emitter you can handle your events however you like. 
  - Whether that be by running handlers in service workers or by setting up Observable streams or offloading computation to a server. 
  - Send events to the server, receive events from the server, synchronise a second micro-Vue frontend application, Manage side effects with RxJS; 
  - So long as you can share your event bus, your application architecture can support it. 
  - This is the power of an event based architecture you have the ability to connect up your app however you like.

- Lastly, because we are talking about basic Event Bus architectures and Redux contains an Event Bus, 
  - these systems can certainly be set up by using Redux itself. 
  - The caveat here is that with Redux you drag along data with your bus that may actually cause more harm than good as developers inadvertently(不经意地) share state between systems that should remain separate.

- Redux is a valuable and versatile library but it is more than just a state management container. 
  - When you choose to use Redux, you are choosing your Event Bus, your Data Store, your canonical DI mechanism and so on 
  - and depending on a single package for all of these separate application functions may not be what you need in every situation.
- Whilst it certainly makes no sense to re-write a large app to remove Redux, 
  - due to Redux’s tendency towards becoming a global dependency, 
  - new or smaller apps should think carefully about whether or not their needs can be served by selecting an appropriate event bus and using in-built React state management 
  - as this will lead to a cleaner and more flexible architecture.

## [Why you should use an object, and not an array, for lists in Redux _201905](https://javascript.plainenglish.io/https-medium-com-javascript-in-plain-english-why-you-should-use-an-object-not-an-array-for-lists-bee4a1fbc8bd)

- With object solution you won’t get duplicated items.
- Using an object will save your future self some time and bugs.
- CRUD operations do not iterate over all items each time.
- If you need an array of items, just add selector that will convert object to array.
# more-blogs
