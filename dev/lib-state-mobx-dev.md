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
  - linear
# dev
- Mobx数据管理方案，采用观察者模式，观察可变数据，持有细粒度的数据响应模式，感知到哪些组件需要被更新的时间复杂度是`O(1)`的
# rewrite
- https://github.com/liam61/minbx
  - [从零到 observable 一个 object 如何](https://github.com/liam61/blog/blob/master/js/mobx-source/1.observable-an-object.md)

- https://github.com/Jacky-Summer/mini-mobx /js
  - 模拟实现 MobX 的 observable 和 autorun 方法
# blogs

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
