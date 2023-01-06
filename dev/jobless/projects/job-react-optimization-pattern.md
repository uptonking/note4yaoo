---
title: job-react-optimization-pattern
tags: [job, optimization, pattern, react]
created: 2021-09-23T05:26:17.336Z
modified: 2021-10-10T09:25:37.896Z
---

# job-react-optimization-pattern

# guide

# faq-redux

## 

## 

## redux与mobx的区别?

- redux将数据保存在单一的store中
  - mobx将数据保存在分散的多个store中
- redux使用plain object保存数据，需要手动处理变化后的操作
  - mobx适用observable保存数据，数据变化后自动处理响应的操作
- redux使用不可变状态，这意味着状态是只读的，不能直接去修改它，而是应该返回一个新的状态，同时使用纯函数；
  - mobx中的状态是可变的，可以直接对其进行修改
- redux会比较复杂，因为其中的函数式编程思想掌握起来不是那么容易，同时需要借助一系列的中间件来处理异步和副作用
  - mobx相对来说比较简单，在其中有很多的抽象，mobx更多的使用面向对象的编程思维
- redux提供能够进行时间回溯的开发工具，同时其纯函数以及更少的抽象，让调试变得更加的容易
  - mobx中有更多的抽象和封装，调试会比较困难，同时结果也难以预测；

## redux的原理

- 整个工作流程：
  - 用户（通过View）发出Action，发出方式就用到了dispatch方法。
  - Store自动调用Reducer，并且传入两个参数：当前State和收到的Action，Reducer会返回新的State
  - State一旦有变化，Store就会调用监听函数，来更新View。

## redux中如何进行异步操作?

- 可以在`componentDidmount中直接进行请求无须借助redux.
- 在一定规模的项目中, 上述方法很难进行异步流的管理, 通常情况下我们会借助redux的异步中间件进行异步处理.
# faq

## 

## 

## the "object map lookup" pattern (whatever you want to call it) is extremely useful and more concise than switch/ternary/if-statements IMO

- https://twitter.com/DavidKPiano/status/1564950527477252098

- Relevant not only for React, but for any switch/case or if/else logic in JS, when you're mapping one set of values to another
  - This should not just be a react tip but a programming tip. Use clear mappings vs long conditional statements. #developer
  - I believe this is called the “Strategy Pattern” 

## React组件通信如何实现?

- 父组件向子组件通讯
  - 父组件可以向子组件通过传 props 的方式，向子组件进行通讯
- 子组件向父组件通讯
  - props+回调的方式, 父组件向子组件传递props进行通讯，此props为作用域为父组件自身的函数，子组件调用该函数，将子组件想要传递的信息，作为参数，传递到父组件的作用域中
- 兄弟组件通信
  - 找到这两个兄弟节点共同的父节点, 结合上面两种方式由父节点转发信息进行通信
- 跨层级通信
  - Context设计目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言, 对于跨越多层的全局数据通过Context通信再适合不过
- 发布订阅模式
  - 发布者发布事件，订阅者监听事件并做出反应, 我们可以通过引入event模块进行通信
- 全局状态管理工具
  - 借助Redux或者Mobx等全局状态管理工具进行通信, 这种工具会维护一个全局状态中心Store, 并根据不同的事件产生新的状态

## flux vs mvc

- 传统的MVC模式在分离数据(Model)、UI(View和逻辑(Controller)方面工作得很好，但是MVC架构经常遇到两个主要问题:
  - 数据流不够清晰: 跨视图发生的级联更新常常会导致混乱的事件网络，难于调试。
  - 缺乏数据完整性: 模型数据可以在任何地方发生突变，从而在整个UI中产生不可预测的结果。

## context有什么用

- 提供了一个传递数据的方法，从而避免了在每一个层级手动的传递 props 属性。

## 什么是 prop drilling，如何避免？

- 在多层嵌套组件来使用另一个嵌套组件提供的数据。最简单的方法是将一个 prop 从每个组件一层层的传递下去，从源组件传递到深层嵌套组件，这叫做prop drilling。
- 缺点是原本不需要数据的组件变得不必要地复杂，并且难以维护
- 一种常用的方法是使用React Context

## 受控组件和非受控组件区别是啥？

- 受控组件是 React 控制中的组件，并且是表单数据真实的唯一来源。
- 非受控组件是由DOM处理表单数据的地方，而不是在 React 组件中。

## 什么是受控组件

- 在HTML中，表单元素如 `<input>、<textarea>和<select>` 通常维护自己的状态，并根据用户输入进行更新。
- 由React控制其值的输入表单元素称为受控组件。

## 什么是高阶组件？

- HOC是接受一个组件并返回一个新组件的函数。
- 使用场景
  - 代码重用、逻辑和引导抽象
  - 渲染劫持
  - state 抽象和操作
  - props 处理

## Hooks会取代 render props 和高阶组件吗？

- 功能上，hooks能取代它们
  - 通常，render props和高阶组件仅渲染一个子组件

- hooks优点
  - 灵活性更高，方便自定义
  - 减少嵌套，避免wrapper hell

- render props
  - 某些场景下性能更高
  - prop的值是函数

- hoc
  - 复用最简单 connect()(MyComponent)
