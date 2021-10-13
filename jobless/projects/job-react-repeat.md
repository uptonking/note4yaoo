---
title: job-react-repeat
tags: [job, react, repeat]
created: '2021-09-21T19:49:18.386Z'
modified: '2021-09-21T19:49:30.918Z'
---

# job-react-repeat

# not-yet

# guide
- [React我就问这些问题！能不能刷到我就看你的造化了](https://juejin.cn/post/6933197531606155272)
# faq-optimization

## [React性能优化 | 包括原理、技巧、Demo、工具使用](https://juejin.cn/post/6935584878071119885)

- 跳过不必要的组件更新
  01. PureComponent、React.memo
  02. shouldComponentUpdate
  03. useMemo、useCallback 实现稳定的 Props 值
  04. 发布者订阅者跳过中间组件 Render 过程
  05. 状态下放，缩小状态影响范围
  06. 列表项使用 key 属性
  07. useMemo 返回虚拟 DOM
  08. 跳过回调函数改变触发的 Render 过程
  09. Hooks 按需更新
  10. 动画库直接修改 DOM 属性
- 提交阶段优化
  - 避免在 didMount、didUpdate、useLayoutEffect 中更新组件 State
- 前端通用优化
  01. 组件按需挂载
  02. 批量更新
  03. 按优先级更新，及时响应用户
  04. 缓存优化
  05. debounce、throttle优化频繁触发的回调

## [react性能优化的方向](https://juejin.cn/post/6844903865926549511)

- React渲染性能优化的三个方向，其实也适用于其他软件开发领域，这三个方向分别是
- 减少计算的量
  - 对应到React中就是减少渲染的节点 或者 降低组件渲染的复杂度
- 精确重新计算的范围
  - 对应到React中就是绑定组件和状态关系，精确判断更新的'时机'和'范围'
  - 只重新渲染'脏'的组件，或者说降低渲染范围
- 利用缓存
  - 对应到React中就是如何避免重新渲染，利用函数式编程的 memo 方式来避免组件重新渲染

  - 减少渲染的节点/降低渲染计算量(复杂度)
  1️⃣ 减少不必要的嵌套
    - 一般不必要的节点嵌套都是滥用高阶组件/RenderProps导致的
  2️⃣ 虚拟列表
    - 只渲染当前视口可见元素
  3️⃣ 惰性渲染
    - 只在必要时才去渲染对应的节点
  4️⃣ 选择合适的样式方案
    - CSS > 大部分CSS-in-js > inline style
  0️⃣ 不要在渲染函数都进行不必要的计算
    - 数组排序、数据转换、订阅事件、创建事件处理器等等. 渲染函数中不应该放置太多副作用

- 避免重新渲染
  0️⃣ 简化 props
    - 简化的 props 更容易理解, 且可以提高组件缓存的命中率
  1️⃣ 不变的事件处理器
    - 避免使用箭头函数形式的事件处理器
  2️⃣ 不可变数据
    - 不可变数据可以让状态变得可预测，也让 shouldComponentUpdate '浅比较'变得更可靠和高效
  3️⃣ 简化 state
    - 不是所有状态都应该放在组件的 state 中. 例如缓存数据
  4️⃣ 使用 recompose 精细化比对

- 精细化渲染
  0️⃣ 响应式数据的精细化渲染
  1️⃣ 不要滥用 Context

- [React项目性能分析及优化](https://github.com/brickspert/blog/issues/36)
- PureComponent/ShouldComponentUpdate
- React.memo
- 善用 React.useMemo
- 合理使用 React.useCallback
- 谨慎使用 Context
- 小心使用 Redux

- [React性能优化的8种方式了解一下](https://juejin.cn/post/6844903924302888973)
- 使用`React. Memo`来缓存组件
- 使用useMemo缓存大量的计算
- 使用`React. PureComponent` , shouldComponentUpdate
- 避免使用内联对象
- 避免使用匿名函数
- 延迟加载不是立即需要的组件
- 调整CSS而不是强制组件加载和卸载
- 使用`React. Fragment`避免添加额外的DOM

## 如何避免组件的重新渲染？

- PureComponent
  - `React.PureComponent` implements `shouldComponentUpdate()` with a shallow prop and state comparison.
- React.memo is a higher order component.
  - only shallowly checks for prop changes. 
  - it will still rerender when state or context change.
# faq

## Virtual DOM 的优势

- DOM引擎、JS引擎相互独立，但又工作在同一线程（主线程）
- JS代码调用 DOM API 必须挂起 JS引擎、转换传入参数数据、激活DOM引擎，DOM 重绘后再转换可能有的返回值，最后激活 JS 引擎并继续执行若有频繁的 DOM API 调用，且浏览器厂商不做“批量处理”优化，
- 引擎间切换的单位代价将迅速积累若其中有强制重绘的 DOM API 调用，重新计算布局、重新绘制图像会引起更大的性能消耗。

- 虚拟 DOM 不会立马进行排版与重绘操作
- 虚拟 DOM 进行频繁修改，然后一次性比较并修改真实 DOM 中需要改的部分，最后在真实 DOM 中进行排版与重绘，减少过多DOM节点排版与重绘损耗
- 虚拟 DOM 有效降低大面积真实 DOM 的重绘与排版，因为最终与真实 DOM 比较差异，可以只渲染局部

- 虚拟DOM更多的是方便了声明式、基于状态数据驱动UI的开发
  - 还可以跨端

## react diff算法

- 浏览器性能瓶颈是 DOM, react 是采用虚拟 DOM 思想, 当需要重新渲染, 将新旧 DOM 数快照对比, 找出变化的部分, 尽可能较少 DOM 的变更, 
- 而将一个树形结构转化成另一种树形结构, 通常算法复杂度是 On3 次方, 于是结合前端使用场景特征进行了算法优化
  - 首选前端很少有节点跨层级移动
  - 拥有相同类型的组件会生成相似的结构
  - 对于同一层级节点, 他们可以通过唯一key区分

- react为了降低复杂度，提出了三个前提：
  - 只对同级比较，跨层级的dom不会进行复用
  - 不同类型节点生成的dom树不同，此时会直接销毁老节点及子孙节点，并新建节点
  - 可以通过key来对元素diff的过程提供复用的线索

- 首先会一层层比较, (通过 updateDepth 控制), 假如同层发现不同, 销毁结点及其下面所有结点, 哪怕其子节点是可复用的
- 然后同层级比较过程中, diff 提供了插入/删除/移动三个操作, 而判断依据的唯一 ID 就是 标签类型, 或者组件的 key 属性. 
  - 通过唯一key可以判断新老集合中是否存在相同的节点, 如果存在相同节点, 会将新旧快照的索引进行对比, 新快照节点索引 > 旧快照节点索引，才需要进行移动操作。 

## 组件的key的作用

- key是React用于判断哪些列表中元素被修改、被添加或者被移除的辅助标识。
  - 相同的key，react认为是同一个组件，这样后续相同的key对应组件会被复用
  - key相同，若组件属性有所变化，则react只更新组件对应的属性；没有变化则不更新。
  - key值不同，则react先销毁该组件(有状态组件的componentWillUnmount会执行)，然后重新创建该组件（有状态组件的constructor和componentWillUnmount都会执行）

- 两棵树的完全的 diff 算法是一个时间复杂度为 O(n^3) 的问题。但是在前端当中，很少出现跨越层级移动DOM元素的情况，所以React采用了简化的diff算法，只会对virtual dom中同一个层级的元素进行对比，这样算法复杂度就可以达到 O(n)。
- 由于React采用的diff算法是对新旧虚拟dom树同层级的元素挨个比较，碰到循环输出的元素时会有一些问题，比如列表。
- key是一个字符串，用来唯一标识同父同层级的兄弟元素
- 当React作diff时，只要子元素有key属性，便会去原v-dom树中相应位置（当前横向比较的层级）寻找是否有同key元素，比较它们是否完全相同，若是则复用该元素，免去不必要的操作。

- 不推荐用数组index来作为key。如果数据更新仅仅是数组重新排序或在其中间位置插入新元素，那么视图元素都将重新渲染。
- 碰到数组->列表的映射，或是同级元素需要移位的情况，一定要给元素加上key属性！

## [为什么getDrivedStatefromProps是静态的](https://stackoverflow.com/questions/52886075)

- The goal of this proposal is to reduce the risk of writing async-compatible React components.
  - Replace error-prone render phase lifecycle hooks with static methods to make it easier to write async-compatible React components.
  - Making certain lifecycles static to prevent unsafe access of instance properties.
  - It is not possible to detect or prevent all side-effects (eg mutations of global/shared objects).

- 静态函数的特点就是，他不属于任何一个实例，因此，他的内部 this 指向并不是组件的本身
  - 用户不能做以下几个事情：用this.refs.... 用this. 上的任何方法
  - 使得 getDerivedStateFromProps 这个函数强迫变成一个纯函数，逻辑也相对简单，就没那么多错误了。
  -  在这个静态方法中, 除了两个默认的位置参数 nextProps 和 currentState 以外, 你无法访问任何组件上的数据.

- getDerivedStateFromProps(nextProps, prevState) 会在每次组件渲染前被调用
  - getDerivedStateFromProps is invoked right before calling the render method, both on the initial mount and on subsequent updates.
  - 参数是组件接收到的新的 props 和组件当前的数据. 用户需要在这个函数中返回一个对象, 它将作为 setState() 中的 Updater 更新组件.
- 无论是组件调用了 setState(), 接收的 props 发生了变化, 或是父组件的更新都会导致子组件上的 getDerivedStateFromProps被触发.

- 在使用 getDerivedStateFromProps 时, 必须添加很多逻辑判断语句来处理 props 上的更新和 state 上的更新, 避免意外地返回了一个 Updater 再次更新数据, 导致数据异常

## [react类组件中为什么要bind this](https://zhuanlan.zhihu.com/p/54962688)

- React在 document上进行统一的事件分发， dispatchEvent通过循环调用所有层级的事件来模拟事件冒泡和捕获。
  - 事件处理函数是直接调用的，并没有指定调用的组件，所以不进行手动绑定的情况下直接获取到的 this是不准确的

- React class组件中，点击事件的handle方法其实就相当于回调函数传参方式赋值给了 callback，在执行 click 事件时类似 `element.addEventListener('click', callback, false)`, handle失去了隐式绑定的上下文，this 的值为 undefined

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
