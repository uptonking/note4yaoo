---
title: lib-pattern-rxjs-blog
tags: [blog, pattern, rxjs]
created: '2020-12-10T10:07:47.193Z'
modified: '2020-12-14T11:23:05.184Z'
---

# lib-pattern-rxjs-blog

## rxjs-7

### [The State of RxJS. RxJS 7 and Beyond_202010](https://indepth.dev/posts/1353/the-state-of-rxjs-rxjs-7-and-beyond)

- Improved Stability
  - The RxJS team is partnering with Google, thus ensuring smooth and stable releases. 
  - Google will run pre-release versions of RxJS against their mono-repo build targets where RxJS is used widely.
- Latest Typescript Version Support
- toPromise Operator is being deprecated
  - toPromise operator is getting deprecated in RxJS 7 and will get removed completely in v8. 
  - In its place, there are two operators – lastValueFrom() and firstValueFrom(). 
- new animationFrame() method
  - It is a new static method that fires an observable that gives the amount of time elapsed in milliseconds since the start of the observable.
  - This provides a method to measure the progress of an observable without the need of a deeper understanding of how RxJS works under the hood.
- Consuming AsyncIterable Support
- Renamed Operators
  - Some of the legacy operators including deprecated ones that has the same names as their creation methods
  - the following operators: zip, combineLatest, merge, concat have been renamed to zipWith, combineLatestWith, mergeWith, concatWith.
- new resetOnSuccess option for retry
- Reducing Scheduler Footprint
  - The goal is to ensure that extra code from the Scheduler ends up in your final bundle when you explicitly need it.
- Scheduler Arguments are being Deprecated
- Removing Subscription and Tap Callback Options
- subscription.add() returns a void
- v7.1
  - a minor change with non-breaking features and improvements. 
  - ESLint Rules and Transformations
- v8
  - we will see the deprecations where the team was able to add ESLint code transformations removed.
  - This is to ensure that developers have an uncomplicated way of replacing deprecated APIs and are following the best practices. 
  - smaller bundle size

## rxjs-blog

### [Optimizing Batch Processing Jobs with RxJS_201904](https://medium.com/@ravishivt/batch-processing-with-rxjs-6408b0761f39)

- Batch processing may not appear too exciting. 
  - Retrieve some data, do some operations on that data, repeat. 
  - They do their job silently and take minimal input params to run with no fancy UIs. 
  - But finding ways to optimize a batch processing job can be a very rewarding process. 
- The optimization technique is always the same: maximize concurrency without overloading our resources. 
  - Balancing the two can be a challenge.
  - One such candidate is RxJS.
- In this article, we’ll approach a common batch processing pattern in a reactive way using RxJS.
- tl; dr
  - Observables are awesome and can be used to really ramp up efficiency of a batch processing job. 
  - The tradeoff is some additional complexity to think about the problem in a reactive way 
  - but it would be much more complex (i.e. impossible) to achieve the same level of efficiency and flexibility with other approaches.
- Some examples of batch processing jobs include:
  - Traverse an API’s paginated list of data, fetch each record’s details, and index it in ElasticSearch.
  - Fetch data from a database, aggregate with additional data, generate HTML reports, and email them out.
  - Read database and generate sitemap.xml for search crawlers.
  - Initialize a database with randomized seed data while satisfying all DB relations.
- Note that converting a batch job to Observables and RxJS won’t automatically improve its efficiency. 
  - It’s up to us to design a chain of observable operators that maximizes overall efficiency. 
  - This design is dependent on the task at hand. 
- Approach 1 — Sequential with Async/Wait
- Approach 2 — Adding concurrency with Promise.all()
- Approach 3 — Converting approach 2 to observables
- Approach 4 — Optimizing observable concurrency
- One hard part we haven’t yet solved is how to optimize the constraints to create a perfect balance between efficiency and resource consumption. 
  - We’ve seen how to easily set higher-limit constraints in RxJS 
  - but we have no guarantee that the observable pipeline we craft will maximize the data flow and come close to those limits. 
  - we might be able to leverage tools like rxjs-spy to accomplish it.

### [HOW TO DEBUG RXJS CODE_201512](https://staltz.com/how-to-debug-rxjs-code.html)

- The short answer is: you have to depend mostly on drawing diagrams on paper and adding `.do(x => console.log(x))` after operators, 
  - but it will get a lot better with the arrival of RxJS 5.
- Once you have Observables everywhere and RxJS is taking over control flow, the traditional debugger stops being useful. 
- The conventional debugger was engineered for procedural programming, not for any programming paradigm. 
- Code built with RxJS Observables live in a higher level of abstraction than plain procedural JavaScript code.
- Using the procedural debugger will reveal lower-level details that do not usually help to solve our bugs. 
- The same applies to debugging Promises or callback-based code. 
- Instead of blaming Promises as “not debuggable”, we need Promise-specific debugging tools, such as Chrome’s Promise Tab in DevTools.
  - Warning: Support for the Promise inspector has been removed.
  - [How to step through your code](https://developers.google.com/web/tools/chrome-devtools/javascript/step-code#enable_the_async_call_stack)
- there are 3 techniques you can use today to debug RxJS:
  - Adding `.do(x => console.log(x))` to trace to the console
  - Drawing a dependency graph and following the flow
  - Drawing a marble diagram
- The goal of debugging is simply to help you get an accurate mental model of the execution of your code. 
- This is the most rudimentary technique: to just “console.log” events happening on the streams.
- We can add `.do(x => console.log(x))` between operators
- Because Observables are lazy until you subscribe, a subscription triggers the operator chain to execute. 
  - If you have the `console.log` inside a `do` and no subscription, the `console.log` will not happen at all.
  - So `.do(x => console.log(x))` is a non-intrusive tracing technique that does not change the behavior of your program
  - A subscription is intrusive(侵入的；闯入的) because it requests the operator chain to execute, changing the behavior of your program
- If you follow the dependencies (e.g. shortLowerCaseName$ depends on name$) and build the dependency graph
  - This can be easily drawn just by statically analyzing your code. 
  - Each circle is an Observable, and each declaration var b$ = a$.flatMap(...) represents an arrow a$ --> b$.
  - Observable dependency graphs should be the first tool you use to detect where does a bug live. 
  - Once you have the dependency graph drawn on paper, you can add .do(x => console.log(x)) on key locations, for instance after every Observable declaration.
  - Then, when executing code you will get a log that tells you how code flowed through the dependency graph
  - Always be aware that Observables in the dependency graph are either cold or hot
- Usually the dependency graph is enough to point out which part of the dataflow is not working as you expected it to. 
  - Then, you can zoom into a specific Observable and use a marble diagram to debug it.
- Most basic RxJS operators have marble diagrams
  - A marble diagram expresses how an operator works by displaying its input Observable (an arrow with dots, at the top) and output Observable (an arrow with dots, at the bottom) behaving over time. 
  - you can draw marble diagrams for any function you write which takes Observables as input and outputs Observables.
  - If you are unsure how an operator (or a sequence of operators) works, add .do(x => console.log(x)) before and after the operator
- the procedural debugger is rather useless for debugging RxJS code, 
  - and you might have seen huge stack traces full of functions from the RxJS library.
- The new Lift-based architecture in RxJS 5 makes it possible and easy to inject behaviors into all observers in an operator chain. 
  - Ben Lesh at Netflix has mentioned future plans for building a debugging tool for Observables based on lift().
- In the near future, we may see real-time rendering of the dependency graph or real-time rendering of marble diagrams. 
  - The former is made possible with static analysis or the Lift architecture.
- Marble diagrams (in text format) are used extensively in RxJS 5 for unit tests
  - These text-based marble diagrams can already be used by RxJS 5 users. 
  - Also, their correspondent PNG diagrams can be automatically generated too

### [使用RxJS管理React应用状态的实践分享](https://zhuanlan.zhihu.com/p/63587161)

- https://github.com/shayeLee/floway

- 我们认为应用的数据大体上可以分为四类：
  - 状态：随着时间空间变化的数据，始终会存储一个当前值/最新值。
  - 事件：瞬间产生的数据，数据被消费后立即销毁，不存储。
  - 异步：异步获取的数据；类似于事件，是瞬间数据，不存储。
  - 常量：固定不变的数据。
- 使用RxJS越久，越令人受益匪浅。
  - 因为它基于observable序列提供了较高层次的抽象，并且是观察者模式，可以尽可能地减少各组件各模块之间的耦合度
  - 因为是基于observable序列来编写代码的，所以遇到复杂的业务场景，总能按照一定的顺序使用observable描述出来，代码的可读性很强。
    - 并且当需求变动时，我可能只需要调整下observable的顺序，或者加个操作符就行了。再也不必因为一个复杂的业务流程改动了，需要去改好几个地方的代码

- 小程序上我实践过这种方案，不好的地方在于订阅方压根不知道这个流发出空值时是没初始化、还是他是请求返回一个空列表，直接的表现就是进入页面之前都会闪一下空页面。还没初始化之前不想触发某些动作，这个也有点麻烦
  - 我的解决方案是自己封装了一个Subject来代替原生的BehaviorSubject

### [如何用Rxjs做状态管理](https://zhuanlan.zhihu.com/p/140352608 )

- Rxjs是Javascript响应式编程的工具，采用非阻塞的事件驱动模型，并有流处理的特点
- 简单假设一个小的业务场景，我们在做一个书籍贩卖的网站Demo
  - Demo的上部分是一个书籍列表，下部分是一个书籍的详情部分，点击书籍后会打开详情页
- 最后可以总结一下，上面的状态管理其实是一种典型的事件驱动的写法，单纯来看，事件驱动的一个比较大的弊端是通常耦合比较严重。
  - 这里必须要说明一点的是，这种耦合性不是Angular的问题，甚至不是在Rxjs在Angular中带来的问题。
  - 相比React，诚然，React在组件化方面做的比较好，但是耦合的问题还是存在的，譬如 Redux 就会有 connect HOC 的耦合，Context（上下文）的耦合等。
  - Vue也有同样的问题，这个问题的问题域是一样的，不过各有各的解决方法。
- 正所谓有得必有失，我们有 Rxjs 的诸多好处，例如事件驱动，非阻塞，数据流等，也有耦合性的挑战，不过好的是，这种耦合性并不是不能解决。
- 我们衡量组件化的标准是组件是否能复用，是否有外部依赖，重构是否方便等等
  - 当一个页面全部都是纯组件，可以有一些“组件”承担着业务逻辑，所以，我们大可放心地把一些耦合性强地依赖放在业务组件上，也就是所谓地智能组件，容器组件，
  - 而把可以复用地组件移除依赖，只传入相应地数据，不要在里面管理业务状态，这就是所谓的哑组件。

## ref

- [聊一聊Observable和RxJS](https://juejin.cn/post/6844904145854398471)
- [RxJS 系列之二 - Observable 详解](https://juejin.cn/post/6844903472509222925)
- [Redux、Rxjs结合TypeScript在react中的简单使用](https://juejin.cn/post/6844904032180535304)
  - https://github.com/piotrwitek/react-redux-typescript-realworld-app
- [用 TypeScript 写 React & Redux - 完全指南](https://segmentfault.com/a/1190000023908144)
  - 使用 redux-observable 编写异步流
- [Why use Redux-Observable over Redux-Saga?](https://stackoverflow.com/questions/40021344/why-use-redux-observable-over-redux-saga)
  - tl; dr 
    - there are pros and cons to both. 
    - Many will find one more intuitive than the other, 
    - but both are complex to learn in different ways if you don't know RxJS (redux-observable) or generators/"effects as data" (redux-saga).
  - Complexity, Coding Style, Learning Curve, Testability
  - I use Redux-Observable over Redux-Saga because prefer to work with observables over generators. 
    - I use it with RXJS, which is a powerful library for working with streams of data. Think of it like lodash for async.
  - redux-observable is super simple internally, it's really just giving you a natural way for you to use RxJS.
  - [Redux-Saga vs Redux-Observable](https://hackmd.io/@2qVnJRlJRHCk20dvVxsySA/H1xLHUQ8e?type=view#side-by-side-comparison)
    - Metal Model 
      - Saga = Worker + Watcher
      - Rxjs = Epic( Type + Operators )
    - Saga
      - Effects as data
      - Imperative style
    - Rxjs
      - Events as data
      - Declarative Style
