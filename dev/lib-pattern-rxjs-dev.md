---
title: lib-pattern-rxjs-dev
tags: [observer, pattern, rxjs]
created: 2020-12-10T10:02:32.636Z
modified: 2021-05-13T04:02:49.797Z
---

# lib-pattern-rxjs-dev
- A reactive programming library for JavaScript
# guide
- rxjs-features
  - follow the Observable Spec Proposal
  - like lodash for events

- rxjs-usecase
  - 作为观察者模式的一种实现
  - 代替Promise异步操作
  - 事件处理
    - 用户输入事件
    - 拖拽
    - 滚动
  - 网络请求的数据流
    - 支持fetch、ajax、websocket
  - 状态管理
    - rxjs适合管理组件的局部状态，要注意引入rxjs的花费
    - 参考redux-observable

- who is using #rxjs
  - google/angular

- examples
  - libs
    - angular2用在httpclient,router
    - nestjs

- rxjs-tips
  - 若将rxjs引入框架，会在很大程度上增加复杂度
    - 但将rxjs引入应用程序，因为各种业务计算本身就很复杂，增加的复杂度就显得小了，反而能使代码更清晰，带来的好处更多
  - Use forkJoin to join multiple results.

- redux-observable
  - An Epic is a function which takes a stream of actions and returns a stream of actions. Actions in, actions out.

- [RxJS的另外四种实现方式](https://zhuanlan.zhihu.com/p/45005457)
# dev
- The most obvious streams in a front end app are streams of user inputs, and streams of data from a server. 

- One of the things which is very easy to do with rxjs and hard with promises is to treat multiple "function calls" together
  - Stuff like batching, buffering, debouncing, windowing, orchestration etc would require complex, ad hoc error prone state... OR clean declarative rxjs stream

- RxJS 7没有采用callbags的架构
# more
- [响应式编程与实时数据处理：从 RxJS 到 Flink（一）](https://zhuanlan.zhihu.com/p/335227503)
# discuss
- ## 

- ## 

- ## 

- ## With asynchronous code, you can either have simple code, or you can have correct code, you can't really have both. Sorry.
- https://twitter.com/BenLesh/status/1739696843213189569
  - Please don't use this as an excuse to chain 8 RxJS operators back-to-back. Stop it. Don't do that.
- With async await I find it pretty simple and clean, what is the problem?
  - I think Ben meant to say the "correct" (and complex) cases of error handling and potential retry that should be thought of at every "await". A big try/catch will lose the source of error whereas writing a lot try-catch is going to be ugly.
- We do non-blocking, async ACID all the way to SNAPSHOT with better (with much less latency variance) delivery promises than any other existing framework. Async code is complex due to concurrency, unidirectional consistent streaming fixes that.

- ## Pedantically(卖弄学问地), React component is effectively a specialized Subject, in RxJS terms. 
- https://twitter.com/BenLesh/status/1009957226956480512
- A React component wraps state, provides an API for reactivity via calling `setState` or updating props. 
- `render()` basically multicasts to any child components in the view.
- that's obviously an over-simplification of what react is doing with the component. I'm not here to argue that.
- if all frameworks could narrow down their components to a function that basically accepted (in React terms) a mixture of state and props, and a bit to say whether you were initializing or updating DOM, it could be a very powerful, light, common API.
- Of course, templated frameworks could compile directly to such a function. 
  - This is what Glimmer and Ivy are (almost) doing. 
  - Approaches like React would presumably require a small adapter, I suppose.

```typescript
ReactComponentSubject {
next({ State, Props }): void;
subscribe(value: JSX.Element): Subscription
}
```

- the `render()` mechanism is obviously pull-based.
- If a developer does all of their calculations prior to updating state, rather than when render is called, it seems like they're accidentally opting out of that optimization. And it's not really obvious that they are like it would be in some frameworks.

- ## [单页应用数据抽象层的思考和实践_2018](https://zhuanlan.zhihu.com/p/47562673)
- Angular深度依赖的 RxJS，技术栈无关，是非常先进地响应式数据流管理工具，天生适合做数据的状态管理，产品中只将 RxJS 用于组件之间的通信，并没有充分发挥出 RxJS 的作用。
- 在单页应用中，会频繁的从服务端获取数据、读取浏览器端的缓存，在函数式编程里，这些被称做 side effects，将上面请求服务端的 side effects 代码抽象为 epic函数，我们延用了 redux-observable 中间件里的叫法
- 一些列 Epic 产生的数据，最终会被推送给不同的领域模型，最终要修改模型的状态，我们将这些 Epic 集成到 rxloop 库中去管理
- 目前前端社区不乏优秀的状态管理方案，这些方案大致可归为两类
  - 一类在 redux 基础上，加上异步中间件，再进行上层的抽象，其中蚂蚁金服的 dva 属于这一类，rxloop 参考了 dva 的 API 设计。
  - 另外一类是将 redux 作为规范，用其它数据流方案来模拟数据的单向流动，状态的叠加修改，rxloop 可以归为这一类，在 RxJS 的基础上进行抽象。
- rxloop 在 rxjs 擅长管理异步事件流的基础上，引入了 redux 的同步数据流“规范”，超轻量级的实现了 redux 加中间件体系完成的工作，理念一致
- rxloop 的核心还实现了 Redux 的 store 接口，
  - 可以直接借助 react-redux 绑定 React 框架在 react-redux代码的基础上 fork 出了 react-rxloop，
  - 并用 @rxloop/core替换对了 redux 的依赖，并跑通了 react-redux 里面 70 多个测试用例，可以放心的将 Redux 的代码升级到 rxloop 体系。

- ## [RxJS 入门指引和初步应用_2017](https://zhuanlan.zhihu.com/p/25383159)
- 在前端，我们通常有这么一些方式来处理异步：回调、事件、Promise、Generator
  - 在处理分发的需求的时候，回调、事件或者类似订阅发布这种模式是比较合适的；
  - 而在处理流程性质的需求时，Promise和Generator比较合适。
  - RxJS的优势在于结合了两种模式，它的每个Observable上都能够订阅，而Observable之间的关系，则能够体现流程
- 我们可以把一切输入都当做数据流来处理
  - 用户操作、网络响应、定时器、Worker
- RxJS提供了各种API来创建数据流：
  - 单值：of, empty, never
  - 多值：from
  - 定时：interval, timer
  - 从事件创建：fromEvent
  - 从Promise创建：fromPromise
  - 自定义创建：create
- 创建出来的数据流是一种可观察的序列，可以被订阅，也可以被用来做一些转换操作，比如：
  - 改变数据形态：map, mapTo, pluck
  - 过滤一些值：filter, skip, first, last, take
  - 时间轴上的操作：delay, timeout, throttle, debounce, audit, bufferTime
  - 累加：reduce, scan
  - 异常处理：throw, catch, retry, finally
  - 条件执行：takeUntil, delayWhen, retryWhen, subscribeOn, ObserveOn
  - 转接：switch
- 也可以对若干个数据流进行组合：
  - concat，保持原来的序列顺序连接两个数据流
  - merge，合并序列
  - race，预设条件为其中一个数据流完成
  - forkJoin，预设条件为所有数据流都完成
  - zip，取各来源数据流最后一个值合并为对象
  - combineLatest，取各来源数据流最后一个值合并为数组
- 数据流这个词，很多时候，是从data-flow翻译过来的，但flow跟stream是不一样的，我的理解是：flow只关注一个大致方向，而stream是受到更严格约束的，它更像是在无形的管道里面流动。
- 在RxJS中，存在这么几种东西：
  - Observable 可观察序列，只出不进
  - Observer 观察者，只进不出
  - Subject 可出可进的可观察序列，可作为观察者
  - ReplaySubject 带回放
  - Subscription 是订阅之后形成的一个订阅关系，可以用于取消订阅。
- 示例一：简单的订阅
- 示例二：对时间轴的操纵
- 示例三：可回放的主题
- 示例四：自动更新的状态树
- 示例五：房租收入业务分析
- 蚂蚁的大部分业务系统前端不太适合用RxJS，大部分是中后台CRUD系统，因为两个原因：整体性、实时性的要求不高。
- 在分发和联动关系多的时候，RxJS才能更加体现出它比Generator、Promise的优势。

- ## [RxJS/Cycle.js 与 React/Vue 相比更适用于什么样的应用场景？](https://www.zhihu.com/question/40195289)
- Cycle本身定位是框架，定义了整个应用的代码组织方式和开发范式，那就是无论是用户事件处理还是服务端数据同步，统统用 Rx 来做，
  - Cycle自己也提供了偏好的 view layer（基 virtual-dom的DOM driver）。
  - 总的来说Cycle的范式侵入性很强，属于要么不用要用就得全盘接受 Rx for everything 的理念
  - 目前还没有看到过大型Cycle应用的例子
- 在React/Vue应用中部分使用 Rx 是完全没有问题的。
  - 思路上来说就是把 React/Vue 组件的 local state 当做一个『中介』，在一个 Rx Observable 的 subscribe 回调里面更新组件状态。
  - 通过简单的绑定库支持，可以完全把 component state 作为一个实现细节封装掉，实现 Observable -> view 的声明式绑定。
- 我个人倾向于在适合 Rx 的地方用 Rx，但是不强求 Rx for everything。
  - 比较合适的例子就是比如多个服务端实时消息流，通过 Rx 进行高阶处理，最后到 view 层就是很清晰的一个 Observable，
  - 但是 view 层本身处理用户事件依然可以沿用现有的范式。
- React 如果没有 Flux，其实也是依赖 component local state。
  - React + Redux 做的事情说到底就是把应用状态从组件本身隔离出去统一管理，这种思路并不是只有 React 能做到，只要有个声明式的视图层就行了。
  - 这也是为什么Redux是 view-layer agnostic，Vue，Angular 2 都有配合 Redux 使用的例子，Vue 自己也有专属的状态管理方案 Vuex。
- RxJS/Cycle.js解决的是数据流的问题，为什么有数据流的问题，是因为更倾向于或者受限于使用单向数据绑定，核心其实解决的是State管理的问题
  - 偏向于Redux或者Flux架构会有全局State的困扰，而最近Redux作者也在新的文章中写到“Local State is Fine”
  - 我们厂（小厂）在iOS（Native）、Android（ReactNative）和Web上都选择了Data Flow驱动的设定思路，
  - 使用RxJS（RxSwift）来作为Data Flow驱动的核心组件，架构基本类似，把全局状态和组件局部状态分开，结构很清楚，因为Data Flow会让你比较容易追踪到数据变化的原因，最终导致UI变化的原因
  - 其实只要把全局状态和局部状态有效管理，使用Redux也很好，不过使用RxJS是因为我们可以很轻松的把全局状态Stream和组件局部状态的Stream通过Rx运算子共同运算，代码会更加清晰，同时大大减少对全局状态的污染，有效控制数据状态变化传播的范围。
- Observable Stream + FRP围绕数据流驱动设计App架构，会大大减少UI上的复杂度，非常看好的结构方向。
  - 而React本身定义了数据流向的要求，但是没有定义如何解决这个问题，所以，React和RxJS解决的不是一个问题

- ## [race condition with Promise; 使用rxjs解决](https://twitter.com/LaraNerdsom/status/1219825132702785537)
- Lack of cancellation (or even disinterest signaling) alone is a solid reason not to use promises.
- This is an eventual race condition:
  - if `getPromise` varies in latency, and `arg` changes quickly, there's a problem.

```JS
useEffect(() => {
  getPromise(arg).then(setValue)
}, [arg]);
```

- So you end up needing to do something like:
  - Just to guard against that. you need to do it everywhere.

```JS
useEffect(() => {
  let cancelled = false;
  getPromise.then(data => !cancelled && setValue(data));
  return () => cancelled = true;
}, [arg]);
```

- Folks using RxJS are used to having a subscription given back to them that they can use for teardown:

```JS
useEffect(() => {
  const subs = getObservable(arg).subscribe(setValue);
  return () => subs.unsubscribe();
}, [arg]);
```

- ## [create a polling component in React with React Hooks](https://twitter.com/The_React_Dev/status/1176133411926368256)

```JS
const [data, setData] = useState(null);

const poll$ = timer(5000).pipe(
  mergeMap(() => fromFetch(url)) repeat();
);

useEffect(() => {
  const s = poll$.subscribe(setData);
  return () => s.unsubscribe();
}, []);
```

- ## [survey: When you look at the codebases you work most frequently on, what are you primarily using for async?](https://twitter.com/sarah_edo/status/1046526452932333569)
- async+await:    41.8%
- promise:        37.6%
- callbacks:      13.4%
- libs like rxjs: 7.2%
- This is hard cause it all depends! Single value, async/await, for everything else callbacks.
  - And sometimes I wrap a callback API with “new Promise()” so I can use async/await
- I use callbacks for almost everything that's not promise based (aka fetch)
- Single async value: async/await
  - Multiple async values: callbacks
  - Even RxJS implements thing$.subscribe(callback) for handling multiple async values. it's the lowest-common denominator for that.
  - Why callback for multiple?
  - I'd personally use RxJS, but in creating APIs for others, callbacks for multiple async values seem to be the most idiomatic
- I use practically all of the last three. 
  - RxJS and Promises have great interop. 
  - Sometimes a .then or .catch is easier to reason about than async/await.
- I’m surprised I don’t see any responses stating generators!
  - They give the syntax benefits of async/await coupled with the power of rxjs (e.g. cancellation). 
  - We use Redux Saga to run all our async generators and it is great!

- ## [Is there any good reason to NOT use RxJS and Observables in Node.js for a highly event-based system – instead of native EventEmitters? ](https://twitter.com/fmalcher01/status/1317393487025868800)
- Team does not understand observables and project does not allow for time to train the team.
- [How to Avoid Observables in Angular](https://dev.to/angular/how-to-avoid-observables-in-angular-273h)
- Angular is an object-oriented framework.
- Even if there are a lot of things imperatively implemented, some services, and therefore also some third party libs, are reactive.
- Observables are a unified API for pull- and push-based collections, that can be composed in a functional way
- Think about all the different APIs in the browser for asynchronous operations:
  - setInterval and clearInterval
  - addEventListener and removeEventListener
  - new Promise and [no dispose logic implemented]
  - requestAnimationFrame and cancelAnimationFrame
  - async and await
  - new AbortController and AbortController.abort
- These are just some of them and we can already see they are all implemented differently.
- Some of them, i.e. promises, are not even disposable at all.
- RxJS wraps all of them and provides the following API: `subscribe` and `unsubscribe`

- This is meant by "a unified API".
- RxJS gave me a hard time learning it, but the code I produced with it was (mostly ) more maintainable, stable and elegant than any other.
  - it gives me a tool to model and compost complex asynchronous processes
- If we take the above examples we see that if we don't use observables we:
  - produce more lines of code
  - the level of complexity in the code is much higher
  - we have to put the logic for one process in multiple places
  - it is very hard to maintain the code
  - it is very hard to add features
  - even the number of indentations in the textual process description is way deeper
  - And we maintained the state in a mutable instead of an immutable way.
- IMHO FRP pays off quickly if you need to compose asynchronous processes
- [Building an infinite scrolling list in typescript with rxjs5](https://stackoverflow.com/questions/45383857/building-an-infinite-scrolling-list-in-typescript-with-rxjs5)

- ## [Just put a PR up to finally land streaming progress events to the #RxJS AJAX implementation (for both upload and download!).](https://twitter.com/BenLesh/status/1358669689325555714)
- Basically, you'll be able to get all of the events out of one observable. 
- any chance you'll be supporting signals soon with this? 
- And to be clear: I wouldn't have recommended `fetch` before they added cancellation.
  - I'd have recommended something like axios for the simple cases where you didn't already have RxJS, because they had cancellation at that point.
  - But now that fetch can be aborted? It's fine.
