---
tags: [blog, react]
title: page-blog-react-dev
created: '2020-06-29T08:43:56.344Z'
modified: '2020-06-30T07:17:58.437Z'
---

# page-blog-react-dev

## react hooks开发实践总结

- 函数式组件
  - 在本文中，我们给函数式组件的函数起个简单一点的名字：render函数
  - 在React内部，它会决定在何时调用render函数，并对返回的React Elements进行遍历，如果遇到函数组件，React便会继续调用这个函数组件
  - 这种把render函数交给React内部处理的机制，为引入状态带来了可能
  - 在本文中，为了方便描述，对于render函数的每次调用，我想称它为一帧。

``` JS
// 函数式组件就是在一个函数中返回React Element
const App = (props) => {
  const { title } = props;
  return (
    <h1>{title}</h1>
  );
};

// 调用render函数以执行渲染，会转译成React.createElement
// const appElement = App({ title: "XXX" }); // 不常用
const appElement = <App title="XXX" />; // 常用
ReactDOM.render(
  appElement,
  document.getElementById('app')
);
```

- 每一帧拥有独立的变量
  - 案例-props的行为差异
  - count属性由父组件传入，初始值为0，每隔一秒增加1。点击“Alert Count”按钮，将延迟3秒钟弹出count的值
    - 函数组件弹窗中出现的值，与页面中文本展示的值不同，count是点击时的旧值
    - class组件弹窗值与页面中文本展示的值是一样，都是最新值
  - class组件中，我们是从this中获取到的props.count。this是固定指向同一个组件实例的。在3秒的延时器生效后，组件重新进行了渲染，this.props也发生了改变。当延时的回调函数执行时，读取到的this.props是当前组件最新的属性值
  - 函数组件中，每一次执行render函数时，props作为该函数的参数传入，它是函数作用域下的变量
  - 由于props是Example函数作用域下的变量，可以说对于这个函数的每一次调用中，都产生了新的props变量，它在声明时被赋予了当前的属性，他们相互间互不影响
  - 换一种说法，对于其中任一个props ，其值在声明时便已经决定，不会随着时间产生变化。handleClick函数亦是如此。例如定时器的回调函数是在未来发生的，但props.count的值是在声明handleClick函数时就已经决定好的。
- useState为当前的函数组件创建了一个状态，这个状态的值独立于函数存放。 useState会返回一个数组，在该数组中，得到该状态的值和更新该状态的方法。通过解构，该状态的值会赋值到当前render函数作用域下的一个常量state中
  - 当组件被创建而不是重用时，即在组件的第一帧中，该状态将被赋予初始值 initialState，而之后的重用过程中，不会被重复赋予初始值。
- 每一帧拥有独立的状态
  - state作为函数中的一个常量，就是普通的数据，并不存在诸如数据绑定这样的操作来驱使DOM发生更新。在调用setState后，React将重新执行render函数，仅此而已。
  - 状态也是函数作用域下的普通变量。我们可以说每次函数执行拥有独立的状态。
- 获取过去或未来帧中的值
  - 对于state，如果想要在第一帧时点击“Delay setCount”，在一个异步回调函数的执行中，获取到count最新一帧中的值，不妨向setCount传入函数作为参数
  - 其他情况下，例如需要读取到state及其衍生的某个常量，相对于变量声明时所在帧过去或未来的值，就需要使用 `useRef` ，通过它来拥有一个在所有帧中共享的变量
  - 如果要与class组件进行比较，useRef的作用相对于让你在class组件的this上追加属性。
  - `const refContainer = useRef(initialValue);` 你可以自己去设置它的值。设置它的值不会重新触发render函数
  - 同样的方法，我们可以用于保存任何值：某 prop，某个state变量，甚至一个函数等。在后面的Effects部分会很有用
- 每一帧可以拥有独立的Effects
  - 若某个useEffect/useLayoutEffect有且仅有一个函数作为参数，那么每次render函数执行时该Effects也是独立的。因为它是在render函数中选择适当时机的执行。

- hooks的使用体验就是简单，无生命周期，无this指向，逻辑复用也简单，无HOC或Render Props的繁琐
- ref
  - [React Hooks 最佳实践 by 网易云音乐前端团队](https://zh-hans.reactjs.org/blog/2020/05/22/react-hooks.html)
  - [React Hooks工程实践总结](https://github.com/forthealllight/blog/issues/49)

## react开发实践总结

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

- ref
  - [React设计模式和最佳实践总结]([hlinkttps://](https://blog.poetries.top/2019/08/10/react-good-practice/))
  - [11 lessons react](https://hackernoon.com/11-lessons-learned-as-a-react-contractor-f515cd0491cf)
  - [React小技巧汇总](https://www.yuque.com/runarale/gau4ci/qhsaxk)

## You Probably Don't Need Derived State

- ref
  - https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
  - [你可能不需要 Derived State](https://zhuanlan.zhihu.com/p/38090110)

- To recap, when designing a component, it is important to decide whether its data will be controlled or uncontrolled.
  - The terms “controlled” and “uncontrolled” usually refer to form inputs, but they can also describe where any component’s data lives. 
  - Data passed in as props can be thought of as **controlled** (because the parent component controls that data). 
  - Data that exists only in internal state can be thought of as **uncontrolled** (because the parent can’t directly change it).
  - Instead of trying to “mirror” a prop value in state, make the component controlled, and consolidate the two diverging values in the state of some parent component. This makes the data flow more explicit and predictable.
  - For uncontrolled components, if you’re trying to reset state when a particular prop (usually an ID) changes, you have a few options:
    - Recommendation: To reset all internal state, use the `key` attribute.
    - Alternative 1: Reset uncontrolled component with an ID prop
      - To reset only certain state fields, watch for changes in a special property (e.g. props.userID).
    - Alternative 2: Reset uncontrolled component with an instance method
      - consider fall back to an imperative instance method using refs.
- bugs
  - If our component’s parent rerenders, anything we’ve typed into the `<input>` will be lost!
  - In practice, components usually accept multiple props; 
    - another prop changing would still cause a rerender and improper reset. 
    - Function and object props are also often created inline, making it hard to implement a shouldComponentUpdate that reliably returns true only when a material change has happened.
    - As a result, shouldComponentUpdate is best used as a performance optimization, not to ensure correctness of derived state
    - It is a bad idea to unconditionally copy props to state.
    - When navigating between details for two accounts with the same email, the input would fail to reset. This is because the prop value passed to the component would be the same for both accounts! 
- When a `key` prop changes, React will create a new component instance rather than update the current one.
  - Keys are usually used for dynamic lists but are also useful here. 
  - Sometimes it might make more sense to put a key on the whole form instead. Every time the key changes, all components within the form will be recreated with a freshly initialized state.
  - While this may sound slow, the performance difference is usually insignificant. Using a key can even be faster if the components have heavy logic that runs on updates since diffing gets bypassed for that subtree.

## react component vs element vs instance

- ref
  - [React Components, Elements, and Instances](https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html)
- An element is a plain object describing a component instance or DOM node and its desired properties. 
  - It contains only information about the component type (for example, a Button), its properties (for example, its color), and any child elements inside it.
  - It is a way to tell React what you want to see on the screen. 
  - You can’t call any methods on the element.
  - It’s just an immutable description object with two fields: `type: (string | ReactClass)` and `props: Object`
  - An element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components.
  - Elements can contain other elements in their props. 
  - Creating a React element is cheap. 
  - Once an element is created, it is never mutated.
- A React component takes props as an input, and returns an element tree as the output.
  - A component can be declared in several different ways. class/func
  - props flows one way in React: from parents to children.
- An instance is what you refer to as `this` in the component class you write. 
  - It is useful for storing local state and reacting to the lifecycle events.
  - Only components declared as classes have instances, and you never create them directly: React does that for you
  - While mechanisms for a parent component instance to access a child component instance exist, they are only used for imperative actions (such as setting focus on a field), and should generally be avoided.
  - React takes care of creating an instance for every class component, so you can write components in an object-oriented way with methods and local state, but other than that, instances are not very important in the React’s programming model and are managed by React itself.
  - Function components don’t have instances at all.
