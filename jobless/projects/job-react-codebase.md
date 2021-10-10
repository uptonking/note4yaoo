---
title: job-react-codebase
tags: [codebase, job, react]
created: '2021-09-23T05:18:52.323Z'
modified: '2021-10-10T09:25:07.095Z'
---

# job-react-codebase

# guide

- 架构要点
  - React v16将递归的无法中断的更新重构为异步的可中断更新
# faq-vdom-fiber

## vdom的优缺点
### 优点
- 内存操作，更新快
- 无需手动操作DOM
  - 虚拟DOM的diff和patch都是在一次更新中自动进行的,我们无需手动操作DOM,极大提高开发效率
- 保证性能下限
  - 虚拟DOM可以经过diff找出最小差异,然后批量进行patch,这种操作虽然比不上手动优化,但是比起粗暴的DOM操作性能要好很多,因此虚拟DOM可以保证性能下限
- 跨平台
  - 虚拟DOM本质上是JavaScript对象,而DOM与平台强相关,相比之下虚拟DOM可以进行更方便地跨平台操作,例如服务器渲染、移动端开发等等

### 缺点
- 无法直接更新html，需要commit
- 无法进行极致优化
  - 在一些性能要求极高的应用中虚拟DOM无法进行针对性的极致优化,比如VScode采用直接手动操作DOM的方式进行极端的性能优化


## 

## 什么是 React Fiber?

- 主要特性是增量渲染: 能够将递归的无法中断的更新重构为异步的可中断更新

## vdom-common

### 什么是虚拟DOM？

- 虚拟DOM本质上是JavaScript对象,是对真实DOM的抽象,VD是真实DOM在内存中的数据结构。
- 状态变更时，计算新树和旧树的差异
- 最后把差异更新到真正的dom中


# faq-reconciler

## 

## 

## 当调用setState时，React render 是如何工作的？

- 从render phase + commit phase的流程
# faq-state


## setState到底是异步还是同步?
- setState只在合成事件和钩子函数中是“异步”的，在原生事件和setTimeout中都是同步的。
- setState 的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的，只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形成了所谓的“异步”，当然可以通过第二个参数 setState(partialState, callback) 中的callback拿到更新后的结果。
- setState 的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的，在原生事件和setTimeout 中不会批量更新，在“异步”中如果对同一个值进行多次setState，setState的批量更新策略会对其进行覆盖，取最后一次的执行，如果是同时setState多个不同的值，在更新时会对其进行合并批量更新。
## 为什么不直接更新 state 呢 ?

- 对于class组件
- 对于函数组件
  - useState返回的state只是一个局部变量，修改会丢失



## 

# faq-SyntheticEvent

## 

## 

## React是如何处理事件的

- SyntheticEvent是 React 跨浏览器的浏览器原生事件包装器，它还拥有和浏览器原生事件相同的接口，包括 stopPropagation() 和 preventDefault()
- React实际上并不将事件附加到子节点本身。React使用单个事件侦听器侦听顶层的所有事件。
  - 这对性能有好处，也意味着 React 在更新 DOM 时不需要跟踪事件监听器。
