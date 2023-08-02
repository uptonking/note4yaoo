---
title: lib-state-signal-dev
tags: [signal, state]
created: 2023-04-07T04:05:16.623Z
modified: 2023-04-07T04:09:30.491Z
---

# lib-state-signal-dev

# guide

# dev

# blogs

## [从 Signals 看响应式状态管理 - 掘金](https://juejin.cn/post/7148001367947214856)

- signals解决了哪些问题？
  - 传统useState的状态提升可能造成过度rerender，需要memo
  - context内容混乱，订阅者下面的任何组件现在必须重新渲染

- signals特点
  - 能根据值的变化自动更新
  - 没有依赖数组
  - Signals 跳过了数据在组件树中的传递，而是直接更新所引用的组件。
  - 默认惰性求值（lazy evaluate）- 只有被使用到的才会被监听和更新
  - 直接访问状态值，不需要 selector 或其他 hooks

- Signals，类似的方案有Observables(Mobx等)，Atoms(Recoil, Jotai等)，Refs(Vue等)。
  - 不过基本意思都一样，表示一个响应式数据的单元。
- reaction, 类似effect
- derivation也叫 computed, memo 等
  - 衍生能缓存计算结果，避免重复的计算，并且也能自动追踪依赖以及同步更新。
- 响应式数据管理会存储不同节点之间的链接关系，当每次节点更新之后，会重新检查链接关系。如果不在关联，就会解绑链接，取消依赖

- 另外响应式还有一点就是同步更新，同步更新避免了状态不一致的问题（相信使用React的同学深有感受），也提高了更好的预测性和可测试性。
  - 在响应式数据更新的基础上，有些也会加入比如批量更新，批量更新在避免重复执行反应和衍生上大有好处，大大避免了一些多余额外的执行消耗

## [Signals vs. Observables, what's all the fuss about?](https://www.builder.io/blog/signals-vs-observables)

- ### Want to know what all the fuss is about Signals vs. Observables?
- https://twitter.com/mhevery/status/1637911322745802752
- Signals are values in the bucket that can be accessed synchronously.
  - Observables are values delivered over time asynchronously through a callback.

- The concept of "time' is critical to observables. 
  - Observables are values delivered over time (or events over time.)
  - This implies that observables can't be read synchronously and have no "current" value. 
  - This makes observable a "push" model.(Think browser events.)
- Signals have no concept of "time." It is just a current value in a bucket.
  - The signal's value can be accessed synchronously through a getter. This makes them pull-based. (no callback required.)

- Observables require explicit subscriptions.
  - Signal subscriptions are created automatically when your code reads the signal's value. (no unsubscribe required.)
  - It also means that as the code runs, the reactivity graph of signals can change and so it is highly dynamic.

- It is a spectrum:
  - Values have no reactivity.
  - Observable can express things that can't be expressed in Signals at the expense of more complex API.
  - Signals are a happy medium where API is simple and good enough for most things UI.

## [The Evolution of Signals in JavaScript - DEV Community](https://dev.to/this-is-learning/the-evolution-of-signals-in-javascript-8ob)

- The starting of declarative JavaScript frameworks had 3 takes on it all released within 3 months of each other: Knockout.js (July 2010), Backbone.js (October 2010), Angular.js (October 2010).
  - Angular's Dirty Checking, Backbone's model-driven re-renders, and Knockout's fine-grained updates. 
  - Each was a little different but would ultimately serve as the basis for how we manage state and update the DOM today.
- Knockout.js is of special importance to the topic of this article, as their fine-grained updates were built on what we've come to call Signals. 
  - They introduced initially 2 concepts observable (the state) and computed (side effect) but over the next couple of years would introduce the 3rd pureComputed (derived state) to the language of the frontend.

## [[译]关于Angular脏值检查你应该知道的最新指南_202008](https://segmentfault.com/a/1190000023558780)

- [The Last Guide For Angular Change Detection You'll Ever Need - Angular inDepth](https://indepth.dev/posts/1305/the-last-guide-for-angular-change-detection-youll-ever-need)

- Angular’s Change Detection is a core mechanic of the framework
- It is also necessary to update the DOM if any changes happen to the state. 
- This mechanism of syncing the HTML with our data is called “Change Detection”.
- Change Detection: The process of updating the DOM when the data has changed
- Each frontend framework uses its implementation, e.g. React uses Virtual DOM, Angular uses change detection and so on.

- In short, the framework will trigger a change detection if one of the following events occurs:
  - any browser event (click, keyup, etc.)
  - setInterval() and setTimeout()
  - HTTP requests via XMLHttpRequest

- By default, Angular Change Detection checks for all components from top to bottom if a template value has changed.

- Angular provides two strategies to run change detections: Default, OnPush

- Default Change Detection Strategy
  - By default, Angular uses the `ChangeDetectionStrategy.Default` change detection strategy. 
  - This default strategy checks every component in the component tree from top to bottom every time an event triggers change detection (like user event, timer, XHR, promise and so on). 
  - This conservative way of checking without making any assumption on the component's dependencies is called dirty checking. 
  - It can negatively influence your application's performance in large applications which consists of many components.

- OnPush Change Detection Strategy
  - This change detection strategy provides the possibility to skip unnecessary checks for this component and all it's child components.

### [angular v1 脏检查机制](https://github.com/zhazhanitian/weekly/blob/main/learning/%E8%84%8F%E6%A3%80%E6%9F%A5%E6%9C%BA%E5%88%B6.md)

- 前端三大主流框架 Angular 为啥逐渐不再耳闻，从而联想到了 Angular 被众人所认知的最大弊端脏检查机制
- 2005年，微软的架构师 John Gossman 推出了 MVVM 模式，其核心部分是 DataBinding 机制。顾名思义，其功能就是将 Model 的数据绑定到 View 层，甚至是将 View 层控件的变换绑定到Model的双向绑定
  - 但是 Model 是对现实场景的建模，但并非对UI界面的建模，所以 Model 往往并不能直接与 View 进行绑定，所以需要添加一个中介，对View层进行建模，即 ViewModel
  - MVVM真正的创举在于对视图建模的思想，特别是当下的移动时代，对于开发有着丰富界面交互体验的开发者来说，ViewModel似乎更契合业务场景。同时，强大的DataBinding机制也大大减少了工作量
- AngularJS是一个基于MVC处理模式，实现了MVVM数据双向绑定的用于开发动态Web项目的框架，以其数据和展现分离、MVVM、MVC、DI等强大的特性活跃于前端开发市场
- 作为首款成熟的 MVVM 前端框架，Angularjs 可以说是试吃第一口双向数据绑定苹果的先行者
- 熟悉 vue 的人都知道，vue 的数据响应机制是通过发布订阅模式去监听实现的，并且在 vue 2 和 vue 3 中实现的方式还不相同，vue 2 基于 Object.defineProperty 实现，而 vue 3 却是通过 proxy 实现
- 那么，在代码层面，Angularjs 及 Angular 是怎么做到监听数据变动然后更新界面的呢？
  - 答案是，他们根本不监听数据的变动，而是在恰当的时机从 $rootScope 开始遍历所有 $scope，检查它们上面的属性值是否有变化，如果有变化，就用一个变量 dirty 记录为 true，再次进行遍历，如此往复，直到某一个遍历完成时，这些 scope 的属性值都没有变化时，结束遍历。
  - 由于使用了一个 dirty 变量作为记录，因此被称为脏检查机制
- 简而言之脏值检测的基本原理是存储旧数值，并在进行检测时，把当前时刻的新值和旧值比对，若相等则没有变化，反之则检测到变化，需要更新视图
- Angular 把页面切分成若干个Component（组件），组成一棵组件树，进入脏值检测后，从根组件自顶向下进行检测，Angular 有两种策略：Default和OnPush，它们配置在组件上，决定脏值检测过程中不同的行为

- “恰当的时机”是什么时候
- 如何做到知道属性值是否有变化
- 这个遍历循环是怎么实现的

- $watch 绑定要检查的值
  - angular会去解析模板中当前作用域下的模板结构，并且自动将那些插值（如{{text}}）或调用（如ng-click="update"）找出来，并利用 $watch 建立绑定，它的回调函数用于决定如果新值和旧值不同时（或相同时）要干什么事

- $digest 遍历递归
  - 当使用 $watch 绑定了要检查的属性之后，当这个属性发生变化，就会执行回调函数，这里用到的就是脏检查机制，脏检查的核心，就是 $digest 循环。
  - 调用 $watch 之后，对应的信息被绑定到 Angular 内部的一个 $watchers 中，它是一个数组，
  - 而当​ $digest 被触发时，Angular 就会去遍历这个数组，并且用一个 dirty 变量记录 $watchers 里面记录的那些 $scope 属性是否有变化，
  - 遍历 $watchers，取出对应的属性值的老值和新值
  - 当有变化的时候，dirty 被设置为 true，在 $digest 执行结束的时候，它会再检查 dirty，如果 dirty 为true，它会再调用自己，直到 dirty 为 false。
    - 用新值代替老值，再次调用 $digest，直到 dirty 为 false
  - 但是为了防止死循环，Angular规定，当递归发生了10次或以上时，直接抛出一个错误，并跳出循环

- 从上面的 $digest 遍历递归我们就可以了解到，Angular 的脏检查机制每次最低遍历两次，而且是整个树结构的遍历，从性能上来说不能被接受也很正常

- 但也不能说其设计思想不可取，比如说目前较火的 React ，它采用的是虚拟 DOM，简单来说就是将页面上的DOM 和 JS 里面的虚拟 DOM 进行对比，然后将不一样的地方渲染到页面上去，这个思想就是 AngularJS 的脏检查机制，只不过 Angular 是检查的数据，React 是检查的 DOM 而已

## [What are Signals? | signia](https://signia.tldraw.dev/docs/what-are-signals)

- Let's start with an extremely broad definition:
  - A signal is a value that changes over time and whose change events can trigger side effects.
  - A signals library, or framework, provides a cohesive set of tools for managing these changing values and their side effects in an automated way that ensures consistency.

- There are many well-known software patterns matching this description, but that we wouldn't normally call 'signals'. 
  - For example, using the above definition you could argue that React is a signals library specifically for UI view trees.

- Breaking signals down
  - A root value is any state value that is updated directly, normally in response to external events, e.g. user input.
  - A derived value is any state value that is computed exclusively by looking at other state values.
  - A side effect is any process which runs in response to a state change event.

- The Signals Design Space
  - How do you access the value of a signal?
  - How does data flow?

- Conclusion
  - Signals are just a way to model and use reactive data, and they do it in a very pure, stripped-down way.
  - There are a million implementation details that give flavor to a particular signals library. Some big differences, some small differences, but the core concepts are shared.
# more
- [I changed my mind. Angular needs a reactive primitive - DEV Community](https://dev.to/this-is-angular/i-changed-my-mind-angular-needs-a-reactive-primitive-n2g)
