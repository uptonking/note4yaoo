---
title: note-react-in-action
tags: [dev, react]
created: 1970-01-01T00:00:00.000Z
modified: 2020-07-14T11:59:09.463Z
---

# note-react-in-action

- react开发实践总结

# guide

- 司徒正美文章
  - [发布高性能迷你React框架anu](https://www.cnblogs.com/rubylouvre/p/6954037.html)
  - [去哪儿网迷你React的研发心得](https://segmentfault.com/a/1190000011235844)
  - [从Anu中探索react构建思想](https://github.com/mosikoo/blog/issues/7)
  - [React16的组件类型](https://zhuanlan.zhihu.com/p/55000793)
  - [React转微信小程序：从React类定义到Component调用](https://zhuanlan.zhihu.com/p/38903385)
- ref
  - [React小技巧汇总](https://www.yuque.com/runarale/gau4ci/qhsaxk)
  - [React设计模式和最佳实践总结](https://blog.poetries.top/2019/08/10/react-good-practice/)
  - [精读《Function VS Class 组件》](https://zhuanlan.zhihu.com/p/59558396)
  - [精读《React 性能调试》](https://zhuanlan.zhihu.com/p/136665404)
  - [精读《setState 做了什么》](https://zhuanlan.zhihu.com/p/54217391)
  - [精读《结合React使用原生 Drag Drop API》](https://zhuanlan.zhihu.com/p/108742572)
  - [精读《Scheduling in React》](https://zhuanlan.zhihu.com/p/62428928)
  - [11 lessons react](https://hackernoon.com/11-lessons-learned-as-a-react-contractor-f515cd0491cf)

# pieces

- JSX is transpiled to function calls: `<Log /> -> createElement(Log, {})` . 
  - So if you put the JSX in your render you're calling a function and getting a new return value each time.
-  If you move the JSX up a level out of the re-rendering component then, it won't get re-created each time

``` JS
  // 仅供参考
  function Counter(props) {
    return (
        <Logger level='info'>
    )
  }

  function Counter2({logger}){
    return {logger}
  }
```

- 虽然props不可变，但 `this` 在Class Component中是可变的，因此 `this.props` 的调用会导致每次都访问最新的props
- 而Function Component不存在this.props的语法，因此 `props` 总是不可变的。
- FC怎么替代 `shouldComponentUpdate`

``` typescript
// 使用React.memo
const Button = React.memo(props => {
  // your component
});

// 或者在父级就直接生成一个被useMemo包裹的子元素
function Parent({ a, b }) {
  // Only re-rendered if `a` changes:
  const child1 = useMemo(() => <Child1 a={a} />, [a]);
  // Only re-rendered if `b` changes:
  const child2 = useMemo(() => <Child2 b={b} />, [b]);
  return (
    <>
      {child1}
      {child2}
    </>
  );
}

// 对于class组件
class Button extends React.PureComponent {}
```

- FC怎么替代didUpdate
  - useEffect
- FC怎么替代forceUpdate
  - `const [ignored, forceUpdate] = useReducer(x => x + 1, 0);`
  - `const useUpdate = () => useState(0)[1];`
- useState目前的一种实践，是将变量名打平，而非像Class组件一样写在一个 `this.state` 对象里
  - FC中若state拆分过多，也可以写在一个state对象中
  - 只是更新的时候，不再会自动merge而是replace，而需要使用 `...state` 语法
- Class Component可以通过 `componentWillReceiveProps` 拿到 `previousProps` 与 `nextProps` ，对于Function Component，最好通过自定义Hooks方式拿到上一个状态

 

``` JS
 function usePrevious(value) {
   const ref = useRef();
   useEffect(() => {
     ref.current = value;
   });
   return ref.current;
 }
```

- `useState` 函数的参数虽然是初始值，但由于整个函数都是render，因此每次初始化都会被调用
  - 如果初始值计算非常消耗时间，建议使用函数传入，这样只会执行一次
  - `useRef` 不支持这种特性，需要写一些冗余的判断来确定是否进行过初始化

- 当我们想添加一个新功能而引入一个新依赖时，我们往往会评估该依赖的大小以及引入该依赖会对原有bundle造成多大影响。
  - 假如该功能很少被用到，那么我们可以痛快地使用 `React.lazy` 和 `React.Suspense` 来按需加载该功能，而无需牺牲用户体验了
- 单个react组件性能优化
  - render方法里面尽量减少新建变量和bind函数，传递参数是尽量减少传递参数的数量
    - 优先在构造函数中绑定this到方法
    - render中使用类似 `<Foo style={{ color:"red" }}` ，每一次渲染都会被认为是一个style这个prop发生了变化，因为每一次都会创建一个新的对象传递给style
    - 如果想要让react渲染的时候认为前后对象类型prop相同，则必须要保证prop指向同一个javascript对象

``` js
// 要确保这个初始化只执行一次，不要放在render中，可以放在构造函数中
const fooStyle = { color: "red" };
<Foo style={fooStyle} />
```

  - 实现自定义的shouldComponentUpdate
    - 使用PureComponent和定制shouldComponentUpdate的效果是一致的，都是浅比较
    - 不要直接为props设置对象或者数组、不要将方法直接绑定在元素上，因为其实函数也是对象
  - 多个react组件性能优化
    - 当一个列表顺序会重排时，不适合使用数组的索引作为 `key`
    - 不能使用random来生成key
    - key相同，若组件属性有所变化，则react只更新组件对应的属性；没有变化则不更新。
    - key值不同，则react先销毁该组件(componentWillUnmount会执行)，然后重新创建该组件
- 父组件向子组件通信
  - 通过props
- 子组件向父组件通信
  - 使用回调函数
  - 使用自定义事件机制
- 跨级组件通信
  - 处于同一颗子树且不复杂时，层层组件传递props
  - 处于不同子树时，使用context
- 没有嵌套关系的组件通信
  - 使用自定义事件机制
  - 在componentDidMount中订阅事件，在componentWillUnmount中取消订阅
  - 以常用的发布/订阅模式举例, 借用Node.js Events模块的浏览器版实现
  - 自定义事件是典型的发布订阅模式, 通过向事件对象上添加监听器和触发事件来实现组件之间的通信

``` js
// events.js
import { EventEmitter } from 'events';
export default new EventEmitter();

// App.js
export default class App extends Component {
  render() {
    return (
      <div>
        <List1 />
        <List2 />
      </div>
    );
  }
}

import emitter from '../util/events';
class List extends Component {
  constructor(props) {
    super(props);
    this.state = {
      message: 'List1',
    };
  }

  componentDidMount() {
    // 组件装载完成以后声明一个自定义事件
    this.eventEmitter = emitter.addListener('changeMessage', (message) => {
      this.setState({
        message,
      });
    });
  }

  componentWillUnmount() {
    emitter.removeListener(this.eventEmitter);
  }

  render() {
    return (
      <div>
        {this.state.message}
      </div>
    );
  }
}

class List2 extends Component {

  handleClick = (message) => {
    // 触发自定义事件
    emitter.emit('changeMessage', message);
  };

  render() {
    return (
      <div>
        <button 
        onClick={this.handleClick.bind(this, 'List2')}>
          点击我改变List1组件中显示信息
        </button>
      </div>
    );
  }
}
```

- 组件间的通信还可通过callback ref来实现
  - 父组件可将callback ref作为一个prop传递给子组件，可以保存子组件实例的引用
  - 不建议过度依赖ref，会增加复杂度，降低可复用性
  - 原理
    - 当在子组件中调用onRef函数时，正在调用从父组件传递的函数。
    - this.props.onRef（this）这里的参数指向子组件本身，父组件接收该引用作为第一个参数：onRef = {ref =>（this.child = ref）}然后它使用this.child保存引用。
    - 之后，可以在父组件内访问整个子组件实例，并且可以调用子组件函数。

``` js
class Parent extends React.Component {
  testRef = (ref) => {
    this.child = ref
    console.log(ref) // -> 获取整个Child元素
  }
  handleClick = () => {
    alert(this.child.state.info) // -> 通过this.child可以拿到child所有状态和方法
  }
  render() {
    return <div>
      <Child onRef={this.testRef} />
      <button onClick={this.handleClick}>父组件按钮</button>
    </div>
  }
}

class Child extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      info: '快点击子组件按钮哈哈哈'
    }
  }
  componentDidMount() {
    this.props.onRef(this)
    console.log(this) // ->将child传递给this.props.onRef()方法
  }
  handleChildClick = () => {
    this.setState({ info: '通过父组件按钮获取到子组件信息啦啦啦' })
  }
  render() {
    return <button onClick={this.handleChildClick}>子组件按钮</button>
  }
}
```

- 自定义组件上的ref对象就是组件实例化之后的对象，包含props, context和state等属性。这种特性可以允许我们访问某个子组件的内部状态
- 可以尝试靠后命名，写完后对组件的功能与认识更清晰
- 从API层面归纳出6种组件类型
  - 结构型组件
    - 定义了组件大体结构，结构的具体实现由外部传递
    - 对于比较通用的组件，例如Button、Modal、Form等，不应仅提供样式型实现，应该抽象出结构型组件
  - 样式型组件
    - 确定了组件结构细节，外部只需传递参数即可渲染预期样式
    - 可扩展性与复用性偏弱
    - 结构型与样式型组件并不是非此即彼的关系，样式型组件固定的API参数可以降低使用成本，结构型组件弹性的API设定可以提供扩展性，结合两者的优点可以构造出既简单又可拓展的组件

``` typescript
// 结构型组件
interface ModalProps{
  content:React.ReactNode;
}
<Modal content={<input />} />

// 样式型组件
interface ModalProps{
  content:string;
}
<Modal content='text' />
```

  - 组合型组件
    - 以JSX为主体，通过组件间的嵌套组合描述业务逻辑
    - 组合型组件结构清晰，扩展性高，组件使用者通过阅读JSX的render函数即可了解业务逻辑，但组件间联系微弱，ref引用相互隔离难操作
    - 比较基础的组件，例如Form，Select等，建议采用组合型，有利于使用者组织业务代码
    - 组合型组件最具代表性的实践是Ant Design
  - 配置型组件
    - 通过props传递数据结构，组件内部根据预先设定好的逻辑渲染视图
    - 配置型组件需要写的代码量少，但组件内部渲染处于黑箱，使用者难以理解组件逻辑，使其在拓展性上偏弱

``` typescript
// 组合型组件
<Select defaultValue='a'>
  <Select.Option value='a'>a</Select.Option>
  <Select.Option value='b'>a</Select.Option>
</Select>

// 配置型组件
<Select defaultValue='a' options={['a','b']}>
```

  - 受控组件
    - 受控型组件内部只负责展示，仅对外提供回调，以表达改变的期望，其最终行为完全由外部驱动
    - 官方推荐输出无状态受控组件，但是有状态的组件在项目开发中仍是必要的
    - 受控型组件在自身层面规范了单向数据流，可以与其他数据层框架整合，但是开发一个复杂的受控型组件，开发者可能需要向外提供大量的接口与回调
    - 大型受控组件，所有状态都由外部控制，使用者需要写大量配置代码才能跑通一个大型组件，使用成本极高
  - 非受控组件
    - 非受控组件由内部处理某些行为，并不强制外部状态同步
    - 组件可以自主维护状态，但开发者常常因此懒于做状态同步，上层组件重新渲染时，非受控组件会丢失内部的状态

``` typescript
// 受控组件
<Input value={val} onChange={handleCHange} />
// 非受控组件
<Input defaultValue={val}  />
```

- 如果props的数据不会改变，就不需要在state或者组件实例属性里拷贝一份
- 设置状态会触发组件重新渲染
  - 因此应该只将渲染方法要用到的值保存在状态中
  - 不要把没有参与渲染的数据放进state状态里
- 关于render函数里面的条件判断
  - 如果只是简单的条件判断，三目和与或运算符已经满足大多数人的需求；
  - 如果想让关注点分离，renderIf是个不错的注意；
  - 最后如果你希望你的判断逻辑能够被复用（就好像多个页面多个组件都需要用到判断登录状态和用户权限的逻辑），可以使用onlyIf构建项目内可复用的高阶组件。
  - 避免在JSX中写复杂的三元表达式，应通过封装函数或组件实现，如renderXxx
- 组件设计原则
  - 保持接口小，props数量要少
  - 根据数据边界来划分组件，充分利用组合
  - 把state往上层组件提取，让下层组件只需要实现为纯函数
- 组件划分
  - 一个复杂组件都是从简单组件开始的，一开始我们在render函数里写的代码不多，但是随着逻辑的复杂，JSX代码越来越多，于是就需要拆分函数中的内容
  - 有一个误区，就是把render中的代码分拆到多个 `renderXxx()` 函数中去
  - 因为这些 `renderXxx()` 函数访问的是同样的props和state，这样代码依然耦合在了一起。更好的方法，是把这些 `renderXXXX` 重构成各自独立的React组件

``` js
  class StopWatch extends React.Component {
    renderControlButtons() {
      //TODO: 返回两个按钮的JSX
    }
    render() {
      const majorClock = this.renderMajorClock();
      const controlButtons = this.renderControlButtons();
      const splitTimes = this.renderSplitTimes();

      return (
        <div>
          {majorClock}
          {controlButtons}
          {splitTimes}
       </div>
      );
    }
  }

  return (
    <div>
      <MajorClock>
      <ControlButtons>
      <SplitTimes>
    </div>
  );
```

- 尽量不要在JSX中写内联函数，比如 `<MyButton onClick={()=>{/*doSth*/}} >` ，每次渲染都会创建新函数
  - Every time the parent component renders, a new function is created and passed to the Child.
- Render props其实就是React用法中的“依赖注入”
  - 所谓依赖注入，指的是解决这样一个问题：逻辑A依赖于逻辑B，如果让A直接依赖于B，当然可行，但是A就没法做得通用了。
  - 依赖注入就是把B的逻辑以函数形式传递给A，A和B之间只需要对这个函数接口达成一致就行，如此一来，再来一个逻辑C，也可以用一样的方法重用逻辑A
- 当需要重用React组件的逻辑时，建议首先看这个功能是否可以抽象为一个简单的组件；如果行不通的话，考虑是否可以应用render props模式；再不行的话，才考虑应用高阶组件模式。
- Facebook在开发INS时遇到两个问题：
  - 数据绑定的时候，大量操作真实dom，性能成本太高
  - 网站的数据流向太混乱，不好控制

- 11 lessons learned as a React contractor
  - Multiple simple components are better than one highly customisable one
    - if a composable component is causing bugs, break it into more simple single use components, even if you’re repeating code
  - Always raise an Issue or Pull Request if you find bugs in libraries
  - If you’re implementing React in an existing project, migrate your build process to Browserify or Webpack first.
  - Raw SVG is better than D3 for simple data visualisation
  - When all you have is two weeks, keep it lean
  - Relying on CSS animation alone to move a lot of elements can be slow
    - Make sure you’re only rendering or re-rendering components that really need it.
    - That might mean, calculating what components are visible in the viewport and only rendering those.
    - Test on lower spec machines, but also test with extreme data to see how well things run when they’re pushed to the limit.
  - Only use boilerplates for what they’re good at — getting a project started quickly. 
    - Don’t be afraid to break them, twist them and generally misuse them to your will.
  - Maintain a predictable Components, connected Components and Container pattern
  - Strict linting is a blessing and a curse
  - Retrofitting Universal React rendering into an existing Express project is doable
    - how to just render a single React component into an existing multi-page Express app
    - ReactDOMServer
  - Learning Sagas may melt your brain
    - Make sure you have a deep understanding of Promises and Generators before you dive in
