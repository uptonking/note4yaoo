---
title: job-react-family-faq
tags: [job, react]
created: '2021-09-21T19:31:15.701Z'
modified: '2021-09-22T16:36:57.040Z'
---

# job-react-family-faq

# guide

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

## react源码相关

- React v16将递归的无法中断的更新重构为异步的可中断更新

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
