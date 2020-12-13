---
title: lib-state-rxjs-blog
tags: [blog, rxjs]
created: '2020-12-10T10:07:47.193Z'
modified: '2020-12-10T10:10:33.437Z'
---

# lib-state-rxjs-blog

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
