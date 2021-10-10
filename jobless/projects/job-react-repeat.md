---
title: job-react-repeat
tags: [job, react, repeat]
created: '2021-09-21T19:49:18.386Z'
modified: '2021-09-21T19:49:30.918Z'
---

# job-react-repeat

# not-yet

# guide

# faq-optimization

## react性能优化的方向

- 从源码的角度

## 如何避免组件的重新渲染？

- PureComponent
  - `React.PureComponent` implements `shouldComponentUpdate()` with a shallow prop and state comparison.
- React.memo is a higher order component.
  - only shallowly checks for prop changes. 
  - it will still rerender when state or context change.
# faq

## 

## 

## 

## 

## [react类组件中为什么要bind this](https://zhuanlan.zhihu.com/p/54962688)

- React class组件中，点击事件的handle方法其实就相当于回调函数传参方式赋值给了 callback，在执行 click 事件时类似 element.addEventListener('click', callback, false ), handle失去了隐式绑定的上下文，this 的值为 undefined

- 为什么React组件事件绑定需要 bind 来绑定，如果我们不绑定，this 的值为 undefined。
  - 为什么this的值不是全局对象，就像前面的 default binding, 而是undefined？ 
  - 因为class类不管是原型方法还是静态方法定义，“this”值在被调用的函数内部将为 undefined
  - The body of a `class` is executed in strict mode

- 函数内的this默认指向全局的 window, 在 strict 模式 this 的值为undefined。
- 当我们通过obj调用display()时，this 上下文指向 obj
  - 若display被赋给 outerDisplay 这个变量，调用 outerDisplay( ) 时，相当于Default Binding，this 上下文指向 global
- 很多时候，我们需要将函数作为参数通过callback方式来调用，也会使这个函数失去它的 this 上下文

- ref
  - [React中的事件函数为什么要bind this](https://github.com/Vibing/blog/issues/13)
  - React 通过 `React.createElement` 方法模拟 document.createElement 来创建 DOM
  - [React的事件绑定为什么要bind this](https://segmentfault.com/a/1190000038167700)
