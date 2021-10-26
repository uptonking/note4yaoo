---
title: job-react-faq
tags: [job, react]
created: '2021-09-21T19:31:15.701Z'
modified: '2021-10-05T08:23:17.099Z'
---

# job-react-faq

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
# to-do

# 为什么用useReducer使用useState，而不是反过来
- 我倒觉得reducer实现state才是正道，为啥要反过来……
  - 不要把reducer理解成有actionType才工作的，reducer就是一个old => new的函数，而setState是一种固定的reducer（只认new）。这就像是map基于reduce实现，而不可能反过来
# unstable_renderSubtreeIntoContainer vs portal
- unstable_renderSubtreeIntoContainer现在已经被Portal组件取代
- Portal不需要自己管理组件的生命周期。
  - 用ReactDOM.render()渲染到某个DOM节点，如果要卸载的话需要手动执行unmountComponentAtNode()
- Portal可以接受到Context的值。
  - 用render()渲染的组件是无法获取到上级节点的Context值的。比如多语言机制实现
# 为什么自定义的React组件必须大写
- string 类型 React会当做原生的DOM节点进行解析
- ReactClass type 类型 自定义组件

- babel在编译过程中会判断jsx组件的首字母，如果是小写，则当做原生的DOM标签解析，就编译成字符串。如果是大写，则认为是自定义组件，编译成对象。
# [Vue Composition API 和 React Hooks 对比](https://juejin.cn/post/6847902223918170126)
- Hooks 通过 function 抽离的方式，实现了复杂逻辑的内部封装
- Vue Composition API 围绕一个新的组件选项 setup 而创建。setup() 为 Vue 组件提供了状态、计算值、watcher 和生命周期钩子

- 原理区别
- React Hooks底层是基于链表实现，调用的条件是每次组件被 render 的时候都会顺序执行所有的 Hooks 
  - 因为底层是链表，每一个 Hook 的 next 是指向下一个 Hook 的，if 会导致顺序不正确，从而导致报错，所以 React 是不允许这样使用 Hook 的。
  - React数据更改的时候，会导致重新 render，重新 render 又会重新把 Hooks 重新注册一次 
- Vue Hook 只会被注册调用一次，Vue能避开这些麻烦的问题，原因在于它对数据的响应是基于 proxy 的，对数据直接代理观察。
  - 这种场景下，只要任何一个更改 data 的地方，相关的 function 或者 template 都会被重新计算，因此避开了 React 可能遇到的性能上的问题

- 代码的执行
  - Vue中，“钩子”就是一个生命周期方法
  - Vue Composition API 的 setup() 晚于 beforeCreate 钩子，早于 created 钩子被调用
  - React Hooks 会在组件每次渲染时候运行，而 Vue setup() 只在组件创建时运行一次
  - Vue 中 setup() 只会运行一次，可以将 Composition API 中不同的函数 (reactive、ref、computed、watch、生命周期钩子等) 作为循环或条件语句的一部分

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

## react 懒加载

- 比如某个体积相对比较大的第三方库或插件（比如JS版的PDF预览库），只在单页应用（SPA）的某一个不是首页的页面使用了，这种情况就可以考虑代码分割，增加首屏的加载速度

- import()、React.lazy 和 Suspense 共同一起实现了 React 的懒加载，也就是我们常说了运行时动态加载，
  - 即 OtherComponent 组件文件被拆分打包为一个新的包（bundle）文件，并且只会在 OtherComponent 组件渲染时，才会被下载到本地。
- 当 webpack 解析到该`import()`语法时，会自动进行代码分割。

- React.lazy返回了一个 LazyComponent 对象，其 _status 默认是 -1
- 随后会检查模块是否 Resolved，如果已经Resolved了（已经加载完毕）则直接返回moduleObject.default（动态加载的模块的默认导出），否则将通过 throw 将 thenable 抛出到上层。
- React捕获到异常之后，会判断异常是不是一个 thenable，如果是则会找到 `SuspenseComponent` ，
  - 如果 thenable 处于 pending 状态，则会将其 children 都渲染成 fallback 的值，
  - 一旦 thenable 被 resolve 则 SuspenseComponent 的子组件会重新渲染一次。

```JS
class Suspense extends React.Component {
  state = {
    promise: null
  }

  componentDidCatch(err) {
    // 判断 err 是否是 thenable
    if (err !== null && typeof err === 'object' && typeof err.then === 'function') {
      this.setState({ promise: err }, () => {
        err.then(() => {
          this.setState({
            promise: null
          })
        })
      })
    }
  }

  render() {
    const { fallback, children } = this.props
    const { promise } = this.state;
    return <>{ promise ? fallback : children }</>
  }
}
```

- `React.lazy(() => import('./SomeComponent'))`; 
  - define a component that is loaded dynamically
  - Note that rendering lazy components requires that there’s a `<React.Suspense>` component higher in the rendering tree. 
- `<React. Suspense fallback={<Spinner />}>`; 
  - Today, lazy loading components is the only use case supported
  - While this is not supported today, in the future we plan to let Suspense handle more scenarios such as data fetching.

- ref
  - [深入理解React：懒加载（lazy）实现原理](https://juejin.cn/post/6844904191853494280)

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
