---
title: note-react-dev
tags: [dev, react]
favorited: true
created: '2019-08-01T05:09:11.917Z'
modified: '2020-07-14T10:38:48.217Z'
---

# note-react-dev

# dev-xp

- 多用useEffect，少在event handler里面执行side effects
  - 特别是data fetching
# guide
- react-rfc
  - [react context selectors](https://github.com/reactjs/rfcs/pull/119)
  - trending：jquery > querySelector, react > web components
- react-style-guide
  - create-react-app
  - airbnb react style guide

- react-like/alternatives: preact, inferno, rewrite
  - lit-html/hyperhtml

- **react-features**
- 虚拟DOM
  - dom操作进行优化的空间，如Concurrent Mode，只更新必须变化的部分
  - 容易实现跨平台
- 函数式组件架构
  - 在组件层解决更新dom与状态数据一致的问题(keep dom in sync with state), 这是前端框架都需考虑的问题，web components标准没有涉及，需自己实现
  - 组件写法上更简单，写法上只需一个jsx, 传统组件需要先写html元素标签，再引入js操作元素
  - 组件易复用，关注点分离，local state
  - 组件可组合，函数更适合扩展到更多规模
- 单向数据流
  - 思路更清晰，容易定位和调试
- 声明式的组件
  - 由框架隐藏底层操作细节，降低开发复杂度
  - 由框架操作底层dom更新，组件代码更关注业务操作，更简单清晰，更适合大规模开发
- all in js

- why react components
  - 核心优点：非常丰富的生态与扩展，同时具有良好的性能
    - 其他框架就算在框架层能胜出性能，也无时间精力推出快速开发的生态
  - 最顶级公司的支持与推广
  - 最优秀的开发者主导的项目，修bug、制定方向与计划
- react优点
  - 核心优点：可复用的组件模型
  - 声明式组件，简单清晰
  - 单向数据流
  - 只是js，没有引入模版和新语法(后面hooks引入了对js功能的部分限制)
- react缺点
  - 不利于seo
- vdom优点
  - 方便跨平台
  - 方便实现更多ui操作
    - 如storybook跨框架的组件模型，能够编辑

- why hooks
  - One of the design constraints and motivations for hooks was to represent a component being multiple states concurrently. 
  - That's something classes cannot express properly.
- ??? 用一个ref对象保存另一个ref对象，如react-table中 `useGetLatest(instanceRef.current); `，可以方便垃圾回收
- 在requestAnimationFrame中setState的性能

- react开放的生态
  - 状态管理、路由管理、取数、不可变数据结构、服务端渲染
  - 选择方式：面向star的编程、大公司支持、团队技术擅长
  - Reach Router and it’s sibling project React Router are merging as React Router v6. 
    - In other words, Reach Router v2 and React Router v6 are the same
    - We are bringing together the best of React Router and Reach Router into a new, hook-based API.
# tips

- 

- 

- 

- [react 16: setState() in render()](https://reactjs.org/blog/2017/09/26/react-v16.0.html)
  - Calling `setState` directly in `render` always causes an update. This was not previously the case. Regardless, you should not be calling setState from render.
  - Calling `setState` with `null` no longer triggers an update. This allows you to decide in an updater function if you want to re-render.
    - 但可以设置为undefined来触发rerender
  - setState callbacks (second argument) now fire immediately after `componentDidMount/componentDidUpdate` instead of after all components have rendered.

- ReactDOM.createPortal出现前的方案
  - 在v16之前，Use `ReactDOM.unstable_renderSubtreeIntoContainer()` instead if you need to preserve context.

- React guarantees that refs are set before `componentDidMount` or `componentDidUpdate` hooks. But only for children that actually got rendered.
  - Note this doesn’t mean “React always sets all refs before these hooks run”.
  - React will only call ref callbacks for elements that you actually returned from render.
  - 有时候条件渲染会导致ref所在元素没有返回

- The issue can also arise when you try to use a ref of a unmounted component like using a ref in setinterval and do not clear set interval during component unmount.
  - always clearInterval(id) in willUnmount
  - https://stackoverflow.com/questions/44074747

- React. PureComponent的原理，会分别比较props和state的第一层级所有属性的属性值引用是否相等

```JS
import React, { Component } from 'react';

function shallowEqual(obj1, obj2) {
  if (obj1 === obj2) {
    return true
  }
  if (typeof obj1 !== 'object' || obj1 === null || typeof obj2 !== 'object' || obj2 === null) {
    return false
  }
  let keys1 = Object.keys(obj1)
  let keys2 = Object.keys(obj2)
  if (keys1.length !== keys2.length) {
    return false
  }
  for (const key of keys1) {
    if (!obj2.hasOwnProperty(key) || obj1[key] !== obj2[key]) {
      return false
    }
  }
  return true
}

class PureComponent extends Component {
  shouldComponentUpdate(nextProps, nextState) {
    return !shallowEqual(this.props, nextProps) || !shallowEqual(this.state, nextState)
  }
  render() {
    return this.props.children;
  }
}
```

- I avoid declaring React components via the concise arrow syntax. 
  - Instead, I prefer to use plain old function declarations. Here's why:
    1. I can set a debugger inside a function declaration.
    2. I can export default on the same line as the declaration. 
- react 16.13.0使用后可能出现一些warning的问题
  - I agree this warning requires some prior context. Essentially, you needed to know two things from the class era:
    - That you shouldn’t `setState` during render. Classes always warned about this.
    - That function component body is essentially the same thing as class component render method.
  - The rule of thumb has always been “don’t perform side effects while rendering”. 
    - Think of rendering as a pure computation. 
    - Side effects go into a different place (lifecycle methods in classes, or useEffect in function components). 
- There are three things that will cause a render method to automatically get called:
  - A prop that lives on your component gets updated
  - A state property that lives on your component gets updated
  - A parent component's render method gets called
- react code splitting的方式
  - Dynamic Imports
- portal示例中child组件会在portal挂载前先挂载
- https://github.com/reactjs/reactjs.org/issues/272
-  If a child component requires to be attached to the DOM tree immediately when mounted, for example to measure a DOM node, or uses 'autoFocus' in a descendant, add state to Modal and only render the children when Modal is inserted in the DOM tree.
- This guarantees that any children's componentDidMount is called when that child is inserted in the DOM tree, and enabling props like autoFocus to work as expected
- componentWillMount and render methods should not have side effects. 
- Side effects (like modifying the DOM) are only safe in componentDidMount, componentDidUpdate, and componentWillUnmount methods.
- ref使用
  - 基础组件最好都加上 `forwardRef` ，如果不加很可能出错
  - 实例：Input要计算forwardRef，是因为当用做OverlayTrigger的children时，需要通过HTMLElement去计算clientRect，from react-ui-components
- 请求相关问题-waterfalls 
  - 当请求存在依赖关系时，一个请求结束，才开始下一个请求，等待的时间过长
- 请求相关问题-race conditions 
  - 当请求过快(如快速点击)时，后发的请求结果先到达，最后显示的数据是先前请求的数据
  - [race condition with Promise](https://twitter.com/LaraNerdsom/status/1219825132702785537)
- how to reuse ref passed from forwardRef()
  - [使用自定义hooks `useCombinedRefs`](https://itnext.io/reusing-the-ref-from-forwardref-with-react-hooks-4ce9df693dd)
  - 使用useImperativeHandle
    - imperative code using refs should be avoided in most cases. 
- An idiomatic React application consists mostly of function components. Function components have several key advantages:
  - They help prevent abuse of `setState()` API, favoring props instead.
  - They encourage the "smart" vs "dumb" component pattern.
  - They encourage code that is more reusable and modular.
  - They discourage giant, complicated components that do too many things.
  - They allow React to make performance optimizations by avoiding unnecessary checks and memory allocations.
- react组件A的render方法中，传递给子组件的属性使用箭头函数或使用bind方法，有什么问题
  - 若使用箭头函数或bind后的函数作为属性来传递，组件A的render方法每次调用都会创建一个匿名函数，会增加垃圾回收的次数
  - An arrow function does not have its own this; the this value of the enclosing execution context is used
  - 传递事件处理函数到子组件时，若要在事件处理函数中访问父组件的props/state
    - 在constructor中bind
    - 使用class实例属性和箭头函数
    - 在render方法中使用箭头函数或bind，都会有问题
      - Using Function.prototype.bind in render creates a new function each time the component renders, which may have performance implications
  - 示例
    - `<a onClick={() => this.props.handleClick(this.props.item)} />`

```js
      // 更好的方式如下
      <a  onClick={this.onClick} />
      onClick = () => { this.props.handleClick(this.props.item); }
```

  - ref
      - https://stackoverflow.com/questions/39226757/react-passing-parameter-with-arrow-function-in-child-component
      - https://stackoverflow.com/questions/47679673/how-does-event-handlers-with-arrow-functions-achieve-context-binding
- 通过 `cloneElement(element , [extraProps], [...children])`直接给children添加新props，灵活性很高
  - 参考案例包括react-draggable/resizable
  - 通过 `createElement(children , props, children)`也能直接给children添加新属性
- `getDerivedStateFromProps(props, state)`
  - 会在调用render()方法前调用，具体包括
    - 首次挂载时在调用constructor之后
    - 接收到new props之后
    - 调用setState()之后，此时getDerivedStateFromProps方法参数的state已更新
    - 调用forceUpdate()之后
  - ref
      - https://stackoverflow.com/questions/51019936/why-getderivedstatefromprops-is-called-after-setstate
- getSnapshotBeforeUpdate() 
  - is invoked right before the most recently rendered output is committed to e.g. the DOM. 
  - It enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed.
  - Any value returned by this lifecycle will be passed as a parameter to componentDidUpdate().
- cloneElement
  - Clone and return a new React element 
  - The resulting element will have the original element’s props with the new props merged in shallowly. 
  - New children will replace existing children. 
  - `key` and `ref` from the original element will be `preserved` .
  - React.cloneElement(this.props.children, this.props) 

```js
React.cloneElement(
    element,
    [props],
    [...children]
  )

  // is almost equivalent to   

  <
  element.type { ...element.props } { ...props } > { children }
</element.type>
```

- 条件渲染
  - 使用场景
      - 数据为空, 空页面
      - 取数据时发生错误, 错误页面
      - 数据正常
      - 加载状态
  - if/else
  - 三目运算符 `? :`
  - 组件变量：可以实现路由
  - **逻辑与运算符**： `shouldRender && <Button />`
  - IIFE：立即执行函数
  - 普通函数组件
  - 自己抽象出IF组件
  - 高阶组件：根据条件返回不同的新组件
  - 使用children函数，子组件由父组件传入的参数决定
  - https://zhuanlan.zhihu.com/p/38220426
- react render 顺序
  - 当一个组件被调用的时候, 会先调用getDefaultProps，getInitialState，constructor
  - 然后执行componentWillMount
  - render()并不做实际的渲染动作，只是返回一个JSX描述的结构ReactElement
      - render开始执行子组件的constructor...DidMount
      - 然后再返回父组件的DidMount
  - 进行渲染到DOM上, 渲染完成之后触发componentDidMount方法
  - 注意
      - render函数被调用完之后，componentDidMount函数并不是会被立刻调用
      - componentDidMount被调用的时候，render函数返回的东西已经引发了渲染，组件已经被装载到了DOM树上
- props改变
  - 先触发componentWillReceiveProps
  - 然后利用shouldComponentUpdate判断是否需要重新渲染
  - 如果不需要渲染, 状态不变, 不执行其他操作
- state改变
  - 直接利用shouldComponentUpdate判断是否需要重新渲染
  - 如果不需要渲染, 走2->3 ; 如果不需要渲染, 状态不变, 不执行其他操作
- 将函数作为属性传递的6种方式
  - https://daveceddia.com/avoid-bind-when-passing-props/
  - 推荐使用箭头函数定义，然后直接传递函数名，不要在属性值中bind
- render props
  - 定义类组件时，在render()方法中使用**值为函数的属性**
  - 使用方式
      - 定义组件时，在组件的render()方法return()部分调用 `this.props.f(param)`
      - 使用组件时，给组件中添加名为f的属性 `f=()=>()`
      - 从组件jsx内部实现考虑 `React.createElement(type,props,children[])`
  - 定义组件时，在render()或函数方法中直接向children/任意名称传递props数据，使用时将函数作为组件children/任意名称属性的值
      - 使用children作为属性名的好处是使用组件时，可直接写在子组件的位置写上函数
      - 若使用其他任意名称，则需要在使用组件时显式写出属性名称并传递函数
  - https://medium.com/@pshrmn/dont-call-it-a-render-prop-810b80b9c5c5
  - https://www.robinwieruch.de/react-render-props-pattern
  - 强推 https://zhuanlan.zhihu.com/p/43457891
- context
  - 使用场景是跨层级、跨组件数据通信
  - 新版本的Context只能在render方法里面访问，因为Context只暴露在Consumer的render prop里面，若要在生命周期中访问context，需要在包裹组件，将context作为属性传递给该组件
  - 当你封装完一个Consumer之后，或许你想要用ref来获取Consumer里面根组件的实例或者对应的DOM，如果直接在Consumer上使用ref，是得不到想要的结果的，React.forwardRef
  - `getChildContext` function will be called when the state or props changes. (e.g. `getChildContext(){return {type:this.state.type};}` )
      - In order to update data in the context, trigger a local state update with this.setState. This will trigger a new context and changes will be received by the children.
      - if a context value changes, descendants that use that value won’t update if an intermediate parent returns `false` from `shouldComponentUpdate`
  - 参考
      - https://juejin.im/post/5ac598916fb9a028ca53333c
      - https://juejin.im/post/5c74026ce51d4520f0178e06
- hoc
  - HOC属于静态构建, 静态构建即是重新生成一个组件，即返回的新组件不会马上渲染，HOC工厂函数里定义的生命周期函数只有新组件渲染时才会执行
- props.children的理解
  - In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a special prop: `props.children`
  - 所有嵌套在组件中的JSX结构都可以在组件内部通过 `props.children` 获取到
  - children本身就是一个属性，属性名就是children，属性值可以是jsx或返回jsx的函数
  - 只有当子节点多余1个时，this.props.children才是一个数组，否则是不能用map方法的，使用children[i]还可以实现容器类布局组件的开发
  - props.children可以是普通字符串、jsx组件、返回字符串或jsx组件的函数
  - this.props.children用在class定义的类中，函数式组件中无this
  - 在render()方法中只包含 `return this.props.children` 的组件可以用来做容器组件，只包含业务逻辑，等价于 `return <div>{ this.props.children }</div>`
  - http://huziketang.mangojuice.top/books/react/lesson22
  - false, null, undefined, and true are valid children. They simply don’t render. These JSX expressions will all render to the same thing
- 用户要离开页面的时候提示用户正在编辑是否确认要离开，react-router4提供了prompt
- 组件export时使用装饰器会改变ref
- ReactDom.render()不仅能写在页尾，也可以写在函数体中
- React的props 有两个是私有的：key 和 ref，这两者是不能作为普通props传递给子组件的
- `{...this.props}` 不要滥用，请只传递component需要的props，传得太多，或者层次传得太深，都会加重shouldComponentUpdate里面的数据比较负担，因此，也请慎用spread attributes `<Component {...props} />`
- 不需要传入状态的component写成const element的形式，这样能加快初始渲染速度
- react官方提供插件React.addons. Perf可以帮助我们分析组件的性能，以确定是否需要优化
  - React 16干掉了React.addons. Perf，官方推荐使用浏览器的profiling tools 
  - react-perf-tool为React应用提供了一种可视化的性能检测方案，该工程同样是基于React.addons，但是使用图表来显示结果
- 首屏时间可能会比较原生的慢一些，可以尝试用React Server Render(又称Isomorphic)去提高效率，还有利于SEO
- 推荐在 `componentDidMount()` 中发起数据请求
  - https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html
      - There is a common misconception that fetching in componentWillMount lets you avoid the first empty rendering state.
      - In practice this was never true because React has always executed render immediately after componentWillMount. 
      - If the data is not available by the time componentWillMount fires, the first render will still show a loading state regardless of where you initiate the fetch.
      - This is why moving the fetch to componentDidMount has no perceptible effect in the vast majority of cases.
- 不要在同一个方法连续写两个setState()，异步更新可能只更新一个
- fiber是React 16中新的和解引擎，它的主要目的是使虚拟DOM能够进行增量渲染   
- vdom虚拟的视图被保存在内存中，并通过诸如ReactDOM这样的库与真实的DOM保持同步
# react-basis
- react要点
  - 组件的设计：jsx、生命周期、高阶组件、容器组件、非受控组件
  - 单向数据流
  - 虚拟DOM结构
  - ref引用
  - context
- render()
  - 返回值类型包括
      - 原生DOM元素标签，如div
      - React Component
      - Fragment `<>`
      - `ReactDOM.createPortal(child, container)` ,参数2是DOMNode
      - 字符串和数字，被渲染成text节点
      - boolean和null，不会渲染任何东西
- react包
  - react-dom
      - ReactDOM.render, .unmountComponentAtNode, .findDOMNode  
  - react-dom/server
      - ReactDOMServer.renderToString, .renderToStaticMarkup.
  - prop-types
- 常用的受控组件
  - input, textarea, select, checkbox, radio, form
- 高阶组件 Higher-Order Components  
  - 高阶组件是一个函数，接收一个组件作为输入，返回一个功能进行处理后的新组件      
  - 多个hoc嵌套的执行顺序 

 `withDefaultProps(withCalSize(withAccessor(withTooltip(PiePlot)))); `

  属性从外层向里传，越来越多  

  - 使用  
      - 高阶组件调用wrapper组件的方法：使用ref    

```js
            var Wrapper = (Home) => {
              return React.createClass({
                render() {
                  return (
                    <div>
                          <button onClick={() => {this.home.someFunc()}} />
                          <Home
                              {...this.props}
                              ref={(c) => this.home = c;}
                          />
                      </div>
                  );
                }
              })
            }
```

  - 注意事项
      - 不要在render()方法中使用高阶组件
      - wrapped组件的静态方法要手动拷贝
      - 避免将高阶组件的refs传递给wrapped组件
  - 实现方法 
      - 属性代理
      - 继承反转
- react mixins 
  - mixins引入了隐式依赖关系
  - 不同mixins的相同方法会导致命名冲突
  - mixins之间相互依赖容易增加复杂度
- 核心
  - 组件声明周期
  - 单向数据流
# react events
- SyntheticEvent是支持跨览器原生事件接口的跨浏览器实现
- The SyntheticEvent is pooled
- SyntheticEvent object will be reused and all properties will be nullified after the event callback has been invoked
- you cannot use `return false` to prevent default behavior in React
  - You must call preventDefault explicitly
- you cannot access the event in an asynchronous way
- If you want to access the event properties in an asynchronous way, you should call `event.persist()` on the event, which will remove the synthetic event from the pool and allow references to the event to be retained by user code.
- 如果要以异步方式访问事件属性，则应调用event.persist()，该方法将从池中删除合成事件，并允许用户代码保留对事件的引用
- 在使用debounce函数时，其内部实际上是使用setTimeout异步调用回调函数，所以直接在debounce函数内部获取外部的event对象是不能直接拿到的，这时调用event.persist()就可以拿到事件的引用
