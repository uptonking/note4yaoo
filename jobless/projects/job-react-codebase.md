---
title: job-react-codebase
tags: [codebase, job, react]
created: '2021-09-23T05:18:52.323Z'
modified: '2021-10-10T09:25:07.095Z'
---

# job-react-codebase

# guide

- 关注点
  - vdom、reconciler、state、event

- 架构要点
  - React v16将递归的无法中断的更新重构为异步的可中断更新
  - [React高频面试题梳理，看看面试怎么答？](https://mp.weixin.qq.com/s/vJOAiiP0PSMOgPStZw-rQA)
# faq-vdom-fiber

## vdom的优缺点

### 优点
- 内存操作，更新快
- 无需手动操作DOM
  - 虚拟DOM的diff和patch都是在一次更新中自动进行的, 我们无需手动操作DOM, 极大提高开发效率
- 保证性能下限
  - 虚拟DOM可以经过diff找出最小差异, 然后批量进行patch, 这种操作虽然比不上手动优化, 但是比起粗暴的DOM操作性能要好很多, 因此虚拟DOM可以保证性能下限
- 跨平台
  - 虚拟DOM本质上是JavaScript对象, 而DOM与平台强相关, 相比之下虚拟DOM可以进行更方便地跨平台操作, 例如服务器渲染、移动端开发等等

### 缺点

- 无法直接更新html，需要commit
- 无法进行极致优化
  - 在一些性能要求极高的应用中虚拟DOM无法进行针对性的极致优化, 比如VScode采用直接手动操作DOM的方式进行极端的性能优化

## 

## 什么是 React Fiber?

- 主要特性是增量渲染: 能够将递归的无法中断的更新重构为异步的可中断更新

- 16.x版本之前，React的更新过程是同步的，当React决定要更新DOM时，从diff到更新DOM，一气呵成。
  - 这种就会有一个问题，更新的组件比较复杂并且多(层级深等)的时候，此时如果用户点击了页面某个按钮，可能会因为正在批量更新DOM还未进行完成，按钮无法响应的问题。

- fiber架构第一个阶段render是分片的，将一个任务成很多个小的任务去执行，每次只执行一个小的任务，然后去看一下有没有优先级更高的任务，如果有，则去执行优先级更好的任务，如果没有，接着再执行下一小段任务。
  - Commit Phase 更新渲染DOM，一气呵成。


## 什么是虚拟DOM？

- 虚拟DOM本质上是JavaScript对象, 是对真实DOM的抽象, VD是真实DOM在内存中的数据结构。
- 状态变更时，计算新树和旧树的差异
- 最后把差异更新到真正的dom中

- 当我们需要创建或更新元素时， React首先会让这个 VitrualDom对象进行创建和更改，然后再将 VitrualDom对象渲染成真实DOM。
  - 当我们需要创建或更新元素时， React首先会让这个 VitrualDom对象进行创建和更改，然后再将 VitrualDom对象渲染成真实DOM。

- 当我们需要创建或更新元素时， React首先会让这个 VitrualDom对象进行创建和更改，然后再将 VitrualDom对象渲染成真实DOM。
- VitrualDom的优势在于 React的 Diff算法和批处理策略， React在页面更新之前，提前计算好了如何进行更新和渲染 DOM

## 虚拟Dom中的$$typeof属性的作用是什么？
- ReactElement中有一个 $$typeof属性，它被赋值为 REACT_ELEMENT_TYPE
  - $$typeof是一个 Symbol类型的变量，这个变量可以防止 XSS。

- ReactElement.isValidElement=function(object){returntypeofobject==='object'&&object!==null&&object.$$typeof===REACT_ELEMENT_TYPE;};
# faq-reconciler

## 

## 

## 当调用setState时，React render 是如何工作的？

- 从render phase + commit phase的流程
# faq-state

## setState原理，什么时候同步，什么时候异步

- 这里的“异步”不是说异步代码实现，而是说React会收集变更，然后在统一更新。
- setState函数实现中，会根据一个变量isBatchingUpdates判断是直接更新this.state还是放到队列中回头再说，而isBatchingUpdates默认是false，也就表示setState会同步更新this.state，
  - 但是，有一个函数batchedUpdates，这个函数会把isBatchingUpdates修改为true，
  - 而当React在调用事件处理函数之前就会调用这个batchedUpdates，造成的后果，就是由React控制的事件处理过程setState不会同步更新this.state。
- 在React中，如果是由React引发的事件处理（比如通过 onClick引发的事件处理），调用 setState 不会同步更新this.state，除此之外的setState调用会同步执行this.state。
  - 所谓"除此之外”，指的是绕过React通过 `addEventListener` 直接添加的事件处理函数，还有通过 `setTimeout/setInterval`产生的异步调用。

## setState到底是异步还是同步?

- setState只在合成事件和钩子函数中是“异步”的，在原生事件和setTimeout中都是同步的。
- setState 的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的，只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形成了所谓的“异步”，当然可以通过第二个参数 setState(partialState, callback) 中的callback拿到更新后的结果。
- setState 的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的，在原生事件和setTimeout 中不会批量更新，在“异步”中如果对同一个值进行多次setState，setState的批量更新策略会对其进行覆盖，取最后一次的执行，如果是同时setState多个不同的值，在更新时会对其进行合并批量更新。

## 为什么不直接更新 state 呢 ?

- 对于class组件
- 对于函数组件
  - useState返回的state只是一个局部变量，修改会丢失


# faq-SyntheticEvent

## [React如何实现自己的事件机制？](https://mp.weixin.qq.com/s/vJOAiiP0PSMOgPStZw-rQA)
- React事件并没有绑定在真实的 DOM节点上，而是通过事件代理，在最外层的document上对事件进行统一分发。
- React在自己的合成事件中重写了stopPropagation方法，将 isPropagationStopped设置为true，然后在遍历每一级事件的过程中根据此遍历判断是否继续执行。这就是React自己实现的冒泡机制。

- React 根据 W3C 规范定义了每个事件处理函数的参数，即合成事件。
  - 事件处理程序将传递 SyntheticEvent 的实例，这是一个跨浏览器原生事件包装器。
  - 它具有与浏览器原生事件相同的接口，包括 stopPropagation() 和 preventDefault()，在所有浏览器中他们工作方式都相同。
  - React合成的 SyntheticEvent采用了事件池，这样做可以大大节省内存，而不会频繁的创建和销毁事件对象。

- React的所有事件都通过 document进行统一分发。
  - 当真实 Dom触发事件后冒泡到 document后才会对 React事件进行处理。
  - 所以原生的事件会先执行，然后执行React合成事件，最后执行真正在document上挂载的事件

- React事件和原生事件最好不要混用。
  - 原生事件中如果执行了 stopPropagation方法，则会导致其他 React事件失效。
  - 因为所有元素的事件将无法冒泡到 document上，导致所有的 React事件都将无法被触发。


## React事件和原生事件有什么区别
- React 事件使用驼峰命名，而不是全部小写。
- 通过 JSX , 你传递一个函数作为事件处理程序，而不是一个字符串。
- 在 React 中你不能通过返回 false 来阻止默认行为。必须明确调用 preventDefault。


## React是如何处理事件的

- SyntheticEvent是 React 跨浏览器的浏览器原生事件包装器，它还拥有和浏览器原生事件相同的接口，包括 stopPropagation() 和 preventDefault()
- React实际上并不将事件附加到子节点本身。React使用单个事件侦听器侦听顶层的所有事件。
  - 这对性能有好处，也意味着 React 在更新 DOM 时不需要跟踪事件监听器。
