---
title: lib-state-rxjs-dev
tags: [rxjs]
created: '2020-12-10T10:02:32.636Z'
modified: '2020-12-10T10:03:14.191Z'
---

# lib-state-rxjs-dev

## guide

- rxjs-usecase
  - 实现观察者模式
  - 状态管理，参考redux-observable
  - libs
    - angular2
    - nestjs

## rxjs 7

- RxJS 7 is based on callbags

## pieces

- [RxJS/Cycle.js 与 React/Vue 相比更适用于什么样的应用场景？](https://www.zhihu.com/question/40195289)
  - Cycle本身定位是框架，定义了整个应用的代码组织方式和开发范式，那就是无论是用户事件处理还是服务端数据同步，统统用 Rx 来做，
    - Cycle 自己也提供了偏好的 view layer（基于 virtual-dom 的 DOM driver）。
    - 总的来说 Cycle 的范式侵入性很强，属于要么不用要用就得全盘接受 Rx for everything 的理念
    - 目前还没有看到过大型 Cycle 应用的例子
  - 在 React/Vue 应用中部分使用 Rx 是完全没有问题的。
    - 思路上来说就是把 React/Vue 组件的 local state 当做一个『中介』，在一个 Rx Observable 的 subscribe 回调里面更新组件状态。
    - 通过简单的绑定库支持，可以完全把 component state 作为一个实现细节封装掉，实现 Observable -> view 的声明式绑定。
  - 我个人倾向于在适合 Rx 的地方用 Rx，但是不强求 Rx for everything。
    - 比较合适的例子就是比如多个服务端实时消息流，通过 Rx 进行高阶处理，最后到 view 层就是很清晰的一个 Observable，
    - 但是 view 层本身处理用户事件依然可以沿用现有的范式。
  - React 如果没有 Flux，其实也是依赖 component local state。
    - React + Redux 做的事情说到底就是把应用状态从组件本身隔离出去统一管理，这种思路并不是只有 React 能做到，只要有个声明式的视图层就行了。
    - 这也是为什么 Redux 是 view-layer agnostic，Vue，Angular 2 都有配合 Redux 使用的例子，Vue 自己也有专属的状态管理方案 Vuex。
  - RxJS/Cycle.js解决的是数据流的问题，为什么有数据流的问题，是因为更倾向于或者受限于使用单向数据绑定，核心其实解决的是State管理的问题
    - 偏向于Redux或者Flux架构会有全局State的困扰，而最近Redux作者也在新的文章中写到“Local State is Fine”
    - 我们厂（小厂）在iOS（Native）、Android（ReactNative）和Web上都选择了Data Flow驱动的设定思路，
    - 使用RxJS（RxSwift）来作为Data Flow驱动的核心组件，架构基本类似，把全局状态和组件局部状态分开，结构很清楚，因为Data Flow会让你比较容易追踪到数据变化的原因，最终导致UI变化的原因
    - 其实只要把全局状态和局部状态有效管理，使用Redux也很好，不过使用RxJS是因为我们可以很轻松的把全局状态Stream和组件局部状态的Stream通过Rx运算子共同运算，代码会更加清晰，同时大大减少对全局状态的污染，有效控制数据状态变化传播的范围。
  - Observable Stream + FRP围绕数据流驱动设计App架构，会大大减少UI上的复杂度，非常看好的结构方向。
    - 而React本身定义了数据流向的要求，但是没有定义如何解决这个问题，所以，React和RxJS解决的不是一个问题

## ref
