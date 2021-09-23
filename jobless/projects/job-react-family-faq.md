---
title: job-react-family-faq
tags: [job, react]
created: '2021-09-21T19:31:15.701Z'
modified: '2021-09-22T16:36:57.040Z'
---

# job-react-family-faq

# guide

- react-pros: 声明式ui开发，易于维护
  - vdom abstraction，框架会掩盖dom操作，跨平台
  - 组件抽象，易于复用
  - 单向数据流，易于定位

- react-cons
  - 只是基础库，对于state、css、routing没有给出同一方案
  - jsx需要转译

- 基础资料
  - [Build your own React](https://pomb.us/build-your-own-react/)
  - [react技术揭秘](https://react.iamkasong.com/state/mental.html)
    - https://github.com/BetaSu/react-on-the-way
# [如何考察候选人的react技术水平？](https://www.zhihu.com/question/60548673)
* 懂 setState 是异步的
* 懂 synthetic event
* 懂 react-dom 分层和 react 没有关系
* 懂 reconciler
* 懂 fiber

- 炫技：
  * 写一个顺滑的拖拽
  * 用一个 component 递归渲染
  * 写一个 react router
# faq

## 如何在vue里用react渲染，如何在js/jquery中使用react组件

- 基本思路是 ReactDOM.render(reactElement, domContainer)，直接将react元素渲染到dom

- 如何在外部js中调用react组件的方法
  - 在react组件中通过callback的形式注册ref到`window`，然后在外部从window中获取ref
  - 还可以考虑基于addEventListener和标准/自定义事件

- `ReactDOM.render(element, container[, callback])` 方法的返回值
  - Render a React element into the DOM in the supplied container and return a reference to the component (or returns null for stateless components).
  - `ReactDOM.render()` currently returns a reference to the root ReactComponent instance. 
    - However, using this return value is legacy and should be avoided because future versions of React may render components asynchronously in some cases. 
    - If you need a reference to the root ReactComponent instance, the **preferred solution is to attach a callback ref to the root element**.

## 

## React的请求应该放在哪个生命周期中?

- 由于JavaScript中异步事件的性质，当发起请求时，浏览器会在此期间返回执行其他工作。当React渲染一个组件时，它不会等待componentWillMount它完成任何事情 - React继续前进并继续render, 没有办法“暂停”渲染以等待数据到达。
- 目前官方推荐的异步请求是在componentDidmount中进行.

## 为什么选择使用框架而不是原生?

- 开发效率
- 组件化：易复用、易维护
- 逻辑分层：状态管理、事件处理、网络请求
- 丰富生态

## 为什么类方法需要绑定到类实例？

- 在js中，this 值会根据当前上下文变化。
  - 在 React 类组件方法中，开发人员通常希望 this 引用组件的当前实例，因此有必要将这些方法绑定到实例。
  - 通常这是在构造函数中完成

## 类组件和函数组件之间的区别是啥？

- 声明周期函数
- this

## ref有什么用

- 函数组件的ref类似class的实例变量，能在多次执行同一函数时访问同一引用
- 常用来保存dom对象
- useRef
- callback ref

## state 和 props 区别是啥？

- state是组件自己管理数据，控制自己的状态，可变；
- props是外部传入的数据参数，不可变；

## StrictMode(严格模式)是什么？

- StrictMode是一种辅助组件，可以检查
  - 验证内部组件是否遵循某些推荐做法，如果没有，会在控制台给出警告。
  - 验证是否使用的已经废弃的方法，如果有，会在控制台给出警告。
  - 通过识别潜在的风险预防一些副作用。
- 会double invoke

## 

## 

## 

## 
