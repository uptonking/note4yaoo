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

## react设计有哪些缺陷

### 部分场景使用双向绑定比较繁琐

- 典型的例子是表单，通过state更新ui不算复杂，但通过ui更新state需要手动设置value和onChange，onChange与html标准里面的onInput不一致
- onchange vs oninput
  - onchange事件是在输入框输入完内容后，输入框失焦后触发；而onkeydown/onkeypress/onkeyup在处理复制、粘贴、拖拽、长按键（按住键盘不放）等细节上并不完好。Unlike oninput, the `onchange` event handler is not necessarily called for each alteration to an element's value.
  - onpropertychange为IE专属的。onpropertychange属性可在某些情况下解决上面存在的问题，不用考虑是否失去焦点。无论js操作还是键盘鼠标手动操作，仅仅要HTML元素属性发生改变就可以马上捕获到。
  - oninput事件是在输入框中输入时就会触发。HTML5中的标准事件oninput，实时监听（和ie的onpropertychange一样），只是IE9下面的浏览器是不支持oninput事件的。

- onChange触发频率过高时，也会对性能问题，影像输入体验
  - 可以考虑用非受控组件，使用更新频率低的事件，比如 onBlur。
- 对非受控组件，react只渲染一次不更新的解决方案有2种
  - 添加key，让input强制更新。受控组件是更新其中的值，而我们这里要更新整个 input 组件，虽然更新频率低了，但是更新一次代价大了。
  - 用 ref 指向真实 dom 节点，在适当时机手动更新其中的值。但是写的代码更多了，非常繁琐。

- debounce 做的是 debounce 的事情，他并不能修复 onChange 的语义，他考的是延时来完成任务，而原生 api 并不是靠这个触发。我们当然希望代码不仅能跑，还要跑得合乎道理，而不是凑合着看起来差不多。

- 非受控组件将真实数据储存在 DOM 节点中，所以在使用非受控组件时，有时候反而更容易同时集成 React 和非 React 代码。
  - 使用非受控组件往往可以减少你的代码量

### 合成事件层太厚了

- 只要放弃IE，打薄事件层，立刻可以让 react-dom 大幅度瘦身。
- 合成事件还有个问题，就是他的实现方式其实不是对开发者透明的，使用stopPropagation又要自己在document注册dom事件时就会变成一个坑

### children属性的困惑

- 当一个组件将children视为数据而非渲染内容时，children的结构不可随意封装。
- 在不仔细阅读文档（如果有的话）或者参考实现的情况下，无法分辨一个组件怎么使用children。

- children 的存在导致破坏 pure component 的默认优化

### js动画的实现与react的设计相悖

- 除了css动画，基于js的动画一般都是获取dom，然后操作style属性、调用animate()

### 生态非常丰富，很多方案没有最佳实践

- 状态管理，context vs redux
- css-in-js
- 网络请求, useEffect, onClick

- 已解决
  - 状态逻辑复用方法：hoc, render props --> hooks

### 缺乏把DOM对象从一个节点下直接移动到另一个节点下而不重建的方法

- HTML里可以

### JSX转换到JS丢失了一部分信息

- 这部分算是 JSX 的，可能和 React 关系不大。
- 在 JSX 中，className 的值都是静态的，在整个渲染周期内都没有改变的可能，而两个button中的 a 和 b 都是动态的，会随着应用状态的转移而发生改变。
- 是静态还是动态，我们在 JSX 中看得清清楚楚，然而转换成 JavaScript，喂给 React.createElement 函数，它并不能知道 "counter/output"这样的className字面量，和 a/b 这样的变量有什么不同。
- 这是静态分析就能知道的信息，可以提供给 diff 算法，减轻 diff 负担。
  - 这其中的想法来源于 lit-html，如果可能的话，是以后可以优化的点。

- 另外jsx信息丢失的问题，本质是编译器的能力问题，你不应该指望jsx编译到js后保留信息，而是应该先在jsx层面上做足优化，再去js，如babel的constant-element插件就在干这个事情。

- 写完发现槽点都是集中在 react-dom 上，其实 react 不一定是以 react-dom 为渲染器的，它还有其他的比如 react-native

### PureComponent 即便一个组件事实上是非纯的，实现者依然能声明它是纯的

- 这种声明与事实的相悖，潜藏着大量的BUG隐患。

### 没有slot

- 不能说这是一个缺陷，它有替代的解决方案，但对代码的可读性确实不友好。

### 其他设计缺失或缺陷

- hooks不支持class组件
  - 感觉有点太牵强了，思考一下，如果支持了，未来团队的代码该怎么维护，以什么为标准，以什么为最佳实践

- keep-alive
  - 指在 UnMount 时，并不删掉组件实例，而是在某时候调回来省去 Mount 过程的一种优化。
  - react是没有 keep-alive 的机制的，UnMount 了就 UnMount 了，下一次继续 Mount。
  - 它和上文提到的区分 Mount 和 Update 的问题合在一起，造成开发者总是在思考如何能【触发/不触发】一个特定的生命周期函数，从而达成自己的目的，但这个思路并不是很好，不够 react。
  - 当然，由于有太多组件依赖了 Mount，keep-alive 会导致组件的行为发生改变（Mount 钩子不被触发了），所以 keep-alive 做不了。

- 没有用typescript重写

- 很多unstable_useMutableSource/useSyncedStore/renderSubtreeIntoContainer/batchedUpdates/runWithPriority/

- prop drilling

## react优点

- React.createElement创造一个非平台相关的PlainObject来描述需要渲染的元素。
  - 提供PlainObject描述元素，维护状态，生命周期。跨平台Render部分实现渲染才是最牛逼的地方。
  - React.createElement很像编程语言里产生新的astNode，完全就是把任何代码通过jsx-parser转成了一个IR。

- 生态工具非常丰富：优点 + 缺点

## [React性能优化 | 包括原理、技巧、Demo、工具使用](https://juejin.cn/post/6935584878071119885)

- 跳过不必要的组件更新
  01. PureComponent、React.memo
  02. shouldComponentUpdate
  03. useMemo、useCallback 实现稳定的 Props 值
  04. useMemo返回虚拟DOM
  05. 列表项使用 key 属性
  06. 状态下放，缩小状态影响范围
  07. 跳过回调函数改变触发的 Render 过程
  08. 发布者订阅者跳过中间组件 Render 过程
  09. Hooks按需更新
  10. 动画库直接修改DOM属性
- 提交阶段优化
  - 避免在 didMount、didUpdate、useLayoutEffect 中更新组件 State
- 前端通用优化
  01. 组件按需挂载，懒加载
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
- JS代码调用 DOM API 必须挂起JS引擎、转换传入参数数据、激活DOM引擎，DOM重绘后再转换可能有的返回值，最后激活JS引擎并继续执行若有频繁的 DOM API 调用，且浏览器厂商不做“批量处理”优化，
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

- React在document上进行统一的事件分发， dispatchEvent通过循环调用所有层级的事件来模拟事件冒泡和捕获。
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
