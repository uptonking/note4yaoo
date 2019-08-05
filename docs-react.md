---
title: docs-react
created: '2019-08-01T16:03:46.386Z'
modified: '2019-08-02T10:17:19.789Z'
tags: [docs/react]
---

# docs-react
- React is a JavaScript library for building user interfaces.

## dev tips
- 在所有页面都能触发的行为
	- toast
	- language switch
- props.children的理解
    - In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a special prop: `props.children`
    - props.children可以是普通字符串，也可以是jsx组件，还可以是返回字符串或jsx组件的函数
    - this.props.children用在class定义的类中，函数式组件中无this
    - 在render()方法中只包含`return this.props.children`的组件可以用来做容器组件，只包含业务逻辑
        - 等价于`return <div>{ this.props.children }</div>`
- 用户要离开页面的时候提示用户正在编辑是否确认要离开，react-router4提供了prompt
- 组件export时使用装饰器会改变ref
- ReactDom.render()不仅能写在页尾，也可以写在函数体中
- React的props 有两个是私有的：key 和 ref，这两者是不能作为普通props传递给子组件的
- `{...this.props}`不要滥用，请只传递component需要的props，传得太多，或者层次传得太深，都会加重shouldComponentUpdate里面的数据比较负担，因此，也请慎用spread attributes `<Component {...props} />`
- 不需要传入状态的component写成const element的形式，这样能加快这个element的初始渲染速度
- react官方提供一个插件React.addons.Perf可以帮助我们分析组件的性能，以确定是否需要优化。
	- React 16 干掉了React.addons.Perf，官方现在推荐使用 your browser's profiling tools 
	- react-perf-tool为React应用提供了一种可视化的性能检测方案，该工程同样是基于React.addons，但是使用图表来显示结果
- 首屏时间可能会比较原生的慢一些，可以尝试用React Server Render (又称Isomorphic)去提高效率，还有利于SEO
- 推荐在`componentDidMount()`中发起数据请求
    - 参考 https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html
	- There is a common misconception that fetching in componentWillMount lets you avoid the first empty rendering state.
    	In practice this was never true because React has always executed render immediately after componentWillMount. 
    	If the data is not available by the time componentWillMount fires, the first render will still show a loading state regardless of where you initiate the fetch.
    	This is why moving the fetch to componentDidMount has no perceptible effect in the vast majority of cases.

### resources

- docs
    - https://reactjs.org/docs/hello-world.html
    - https://react.docschina.org/docs/hello-world.html  
- react api docs
    - https://reactjs.org/docs/react-api.html
- React Fiber Architecture
    https://github.com/acdlite/react-fiber-architecture
- reactjs 官方组件
    - https://github.com/reactjs/react-tabs
- react社区组件 https://github.com/react-component
    - https://github.com/react-component/upload
    - https://github.com/react-component/form

## react docs  

### 1. dev/build
- react for developer/designer
- https://unpkg.com/react@16/umd/react.development.js
- https://unpkg.com/react@16/umd/react.production.min.js
- unpkg.com/react@16.6.0/umd/react.production.min.js  
- https://cdn.bootcss.com/react/16.7.0/umd/react.development.js

### 2. concepts

#### get started      

- react应用的构成：元素 -> 组件 -> 应用，元素是构成react应用的最小单位

#### jsx

- jsx是js语法的一种扩展，用来声明react中的元素
- 可以在jsx中使用js表达式，用{}包含
- react声明组件时，组件名称必须以大写字母开头如`<Todo />` ，每个标签必须闭合,因为采用的 js+xml 写法，如` <input />`，组件的返回值只能有一个顶层元素
- jsx本身也是表达式，编译后会转换成普通js对象，可以作为参数，也可以作为返回值
- jsx的属性可以为字符串或js表达式
- jsx中可以放心使用用户输入，因为react dom在渲染前默认会将传入值转换成字符串，可以有效防止xss跨站脚本攻击
- 推荐使用括号将 JSX 包裹起来，虽然这不是必须的，但这样做可以避免分号自动插入的陷阱。
	- We split JSX over multiple lines for readability. While it isn't required, when doing this, we also recommend wrapping it in parentheses to avoid the pitfalls of automatic semicolon insertion.
- Babel 转译器会把 JSX 转换成一个名为 React.createElement() 的方法调用   
- 例子
```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```
```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```
- 返回值示例，返回的是react元素
```
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```

#### rendering elements    

- react元素其实是普通js对象，react dom可以确保浏览器dom的数据内容与react元素保持一致
- 用React 开发应用时一般只会定义一个根节点，但如果是在一个已有的项目当中引入 React ，可能会需要在不同的部分单独定义 React 根节点
- 要将React元素渲染到根DOM节点中，我们通过把它们都传递给 ReactDOM.render() 的方法来将其渲染到页面上：
- react元素都是immutable不可变的，将界面视为一个个特定时刻的固定内容
- 更新界面的唯一办法是创建一个新的元素，然后将它传入 ReactDOM.render() 方法
- React DOM 首先会比较元素内容先后的不同，而在渲染过程中只会更新改变了的部分。

#### components & props    
 
- 组件是ui中独立可复用的部件
- 组件从概念上看就像是函数，它可以接收任意的输入值（称之为“props”），并返回一个需要在页面上展示的React元素。
- 组件名称必须以大写字母开头，包括函数式组件
- 组件的返回值只能有一个根元素，通常要用一个`<div>`来包裹react元素
- 组件不能修改自己的props，所有的React组件必须像纯函数那样使用它们的props
   
#### state & lifecycle     

- 状态与属性十分相似，但是状态是私有的，完全受控于当前组件
- 如果需要存储不用于视觉输出的东西，则可以手动向类中添加不同于props和state的其他字段，如果你不在 render() 中使用某些东西，它就不应该在状态中
- 当 `<Clock />`被传递给 ReactDOM.render() 时，React先调用Clock组件的constructor()，然后调用Clock组件的 render()
- state要点
	- 不要直接更新state，即不要使用`this.state.var1 = 'Hello'`，应当使用`this.setState({var1: 'Hello'});`
	- setState()可能是异步的，React会将多个setState() 调用合并成一个调用来提高性能
		- 所以最好不要依靠this.props和this.state来计算下一个状态，必要时可以使用
		```
		this.setState((prevState, props) => ({
		  	counter: prevState.counter + props.increment
		}));
		```
	- setState()会将你提供的对象合并到当前状态，是浅合并
- 父组件或子组件都不能知道某个组件是有状态还是无状态，并且它们不应该关心某组件是被定义为一个函数还是一个类。
- state除了拥有并设置它的组件外，其它组件不可访问，组件可以选择将其状态作为属性传递给其子组件
- 任何状态始终由某些特定组件所有，并且从该状态导出的任何数据或 UI 只能影响树中下方的组件
- 可以在有状态组件中使用无状态组件，反之亦然

#### handling events      

- React元素的事件处理和 DOM元素的很相似，不同点：
	- React事件绑定属性的命名采用驼峰式写法，而不是小写
	- 如果采用 JSX 的语法你需要传入一个函数作为事件处理函数，而不是一个字符串
	- React中不能使用`return false`的方式阻止默认行为，必须明确的使用`e.preventDefault()`
- React根据 W3C spec 来定义这些合成事件，所以你不需要担心跨浏览器的兼容性问题
- 使用 React 的时候不需要使用 addEventListener 为一个已创建的 DOM 元素添加监听器，需要在这个元素初始渲染的时候提供一个监听器。
- 必须谨慎对待 JSX 回调函数中的 this，类的方法默认不会绑定 this，需要在constructor()中绑定`this.handleClick = this.handleClick.bind(this);`
- 不使用bind()的方式，参考 https://reactjs.org/docs/handling-events.html
	- 定义handleClick时使用箭头函数
	- 在jsx中调用时使用箭头函数` <button onClick={(e) => this.handleClick(e)}>`
		- 这种方式的缺点是，每次渲染button都会创建一个不同的回调函数，不推荐这种方式，推荐使用前两种
- 向事件处理程序传递参数的方法：
	- `<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>`
	- `<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>`
	- 上面两个例子中，参数 e 作为 React 事件对象将会被作为第二个参数进行传递
		- 通过箭头函数的方式，事件对象必须显式的进行传递
		- 但是通过 bind 的方式，事件对象以及更多的参数将会被隐式的进行传递
		- 通过 bind 方式向监听函数传参，在类组件中定义的监听函数，事件对象 e 要排在所传递参数的后面

#### conditional rendering   

- 使用 JavaScript 操作符 if 或条件运算符来创建表示当前状态的元素，然后让 React 根据它们来更新 UI
- true && expression 总是返回 expression，而 false && expression 总是返回 false，如果条件是 true，&& 右侧的元素就会被渲染，如果是 false，React 会忽略并跳过它
- 三目条件运算符可以用来渲染小段文本，用在较大的表达式中不直观
- 条件变得复杂时，要考虑提取组件
- 在组件的render()中`return null`可以阻止组件渲染，也是实现条件渲染的一种方法
- 组件的 render 方法返回 null 并不会影响该组件生命周期方法的回调，componentWillUpdate 和 componentDidUpdate 依然可以被调用。

#### lists & keys   

- 应当给数组中的每一个元素赋予一个确定的标识key，可以在DOM中的某些元素被增加或删除的时候帮助React识别哪些元素发生了变化
- 一个元素的key最好是这个元素在列表中拥有的一个独一无二的字符串，元素没有确定的id时，你可以使用他的序列号索引index作为key
- 如果列表可以重新排序，就不建议使用索引来进行排序，因为这会导致渲染变得很慢 
	- 参考 https://reactjs.org/docs/reconciliation.html
- 元素的key只有在它和它的兄弟节点对比时才有意义	
	- 如果你提取出一个ListItem组件，你应该把key保存在数组中的这个<`ListItem />`元素上，而不是放在ListItem组件中的`<li>`元素上。
- 数组元素中使用的key在其兄弟之间应该是独一无二的，但不需要是全局唯一的，在生成两个不同的数组时，可以使用相同的key
- key会作为给React的提示，但不会传递给你的组件，如果您的组件中需要使用和key相同的值，请将其作为属性传递
	- 不能使用props.key来获取key
- 如果在map()嵌套了太多层级的组件，要考虑提取组件

#### form   

- 表单元素本身有内部状态
- 受控组件的状态值由react控制
- react种主要表单元素的特点
	- `<textarea>`用value属性表示内容，而不用节点内的text
	- `<select>`用value属性表示选中项的值，而不用selected
- input file是非受控组件
- 多个受控的input元素可以共用一个处理方法，可以根据 event.target.name的值来选择执行处理逻辑
- 可以使用ES6中的计算属性名语法来更新与给定输入名称相对应的状态键
	- 示例
	```
	this.setState({
	  [name]: value
	});	 
	```
	等价于    
	```
	var partialState = {};
	partialState[name] = value;
	this.setState(partialState);
	```
	- 参考 https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names
	```
	var param = 'size';
	var config = {
	  [param]: 12,
	  ['mobile' + param.charAt(0).toUpperCase() + param.slice(1)]: 4
	};
	```
-  有时使用受控组件可能很繁琐，因为要为数据可能发生变化的每一种方式都编写一个事件处理程序，并通过一个组件来管理全部的状态。
- 过于繁琐时，考虑使用非受控组件

#### lifting state up    

- 几个组件需要共用状态数据时，最好将这部分共享的状态提升至他们最近的父组件当中进行管理
- 通常，state都是首先添加在需要渲染数据的组件中，此时如果另一个组件也需要这些数据，你可以将数据提升至离它们最近的父组件中
- 状态提升比双向绑定方式要写更多的“模版代码”，但带来的好处是，你也可以更快地寻找和定位bug

#### composition vs inheritance   

- 建议使用组合而不是继承来复用组件之间的代码
- 一些组件不能提前知道它们的子组件是什么，比如Modal弹出框、Sidebar、Dialog 这类通用容器
	- 建议这类组件使用 children 属性将子元素直接传递到输出
	- 示例
	```
	function FancyCard(props) {
	  return (
		<div className={'f-' + props.color}>
		  {props.children}
		</div>
	  );
	}
	```
	```
	function WelcomeDialog() {
	  return (
		<FancyCard color="blue">
		  <h1 className="Dialog-title">
			Welcome
		  </h1>
		  <p className="Dialog-message">
			Thank you for visiting our spacecraft!
		  </p>
		</FancyCard>
	  );
	}
	```
	- `<FancyCard>`JSX标签内的任何内容都将通过children属性传入FancyCard，由于FancyCard在一个 <div> 内渲染了 {props.children}，所以被传递的所有元素都会出现在最终输出中。
- 有时你可能需要在组件中有多个入口，这种情况下你可以使用自己约定的属性而不是 children     
```
	function SplitPane(props) {
	  return (
		<div className="SplitPane">
		  <div className="SplitPane-left">
			{props.left}
		  </div>
		  <div className="SplitPane-right">
			{props.right}
		  </div>
		</div>
	  );
	}
	
	function App() {
	  return (
		<SplitPane
		  left={
			<Contacts />
		  }
		  right={
			<Chat />
		  } />
	  );
	}
```
- WelcomeDialog是Dialog的特殊实例，在React中通过组合来实现，通过配置属性用较特殊的组件来渲染较通用的组件
- 在Facebook使用了数以千计的React组件，还未发现需要推荐使用继承的情况
- 属性和组合为你提供了以清晰和安全的方式自定义组件的样式和行为所需的所有灵活性
- React组件可以接受任意属性，包括基本数据类型、React 元素或函数
- 如果要在组件之间复用 UI 无关的功能，建议将其提取到单独的 JavaScript 模块中

#### thinking in react    

使用react创建应用的一般思路： 
0. 准备：设计原型图和json接口  
1. 将UI划分出组件层级
	- 根据单一功能原则划分组件
	- 考虑数据表示的结构，检查`数据 -> 组件`的映射
	- 整理组件的层级结构，最终树型
2. 用React创建一个静态版本
	- 只使用props，不用state
	- 这些组件只会有 render() 方法
	- 在较为简单的例子中，通常自顶向下更容易，而在较大的项目中，自底向上会更容易并且在你构建的时候有利于编写测试
3. 确定state的最小表示
	- 考虑应用所需要的最小可变状态集作为state
	- 如果数据不会随时间变化，就不用state
	- 如果变量是通过props从父组件传过来，就不用state
	- 如果变量可以根据组件中任何其他的 state 或 props 计算出来，就不用state
4. 确定state的位置
	- 考虑与该state相关的组件
	- 确定公共最小父组件
5. 添加反向数据流
	- 子组件通过回调函数修改父组件的状态
	
### 3. guides

#### Accessibility

- Web accessibility (also referred to as `a11y`) is the design and creation of websites that can be used by everyone.  
- WCAG: The Web Content Accessibility Guidelines provides guidelines for creating accessible web sites.
- WAI-ARIA: The Web Accessibility Initiative - Accessible Rich Internet Applications document contains techniques for building fully accessible JavaScript widgets.  

#### Code-Splitting

-  Code-Splitting is a feature supported by bundlers like Webpack and Browserify (via factor-bundle) 
    which can create multiple bundles that can be dynamically loaded at runtime.
- Code-splitting your app can help you "lazy-load" just the things that are currently needed by the user
	- 虽然没有减少应用程序中的代码总量，但是已经避免了加载用户可能不需要的代码，并且减少了初始加载过程中的代码量
- 动态import: The best way to introduce code-splitting into your app is through the dynamic import() syntax.
```
import { add } from './math';
console.log(add(16, 26));
```
之后  
```
import("./math").then(math => {
  console.log(math.add(16, 26));
});
```
- `React.lazy()`  function lets you render a dynamic import as a regular component.   
```
const OtherComponent = React.lazy(() => import('./OtherComponent'));
function MyComponent() {
	  return (  
	  <MyErrorBoundary>
		 <Suspense fallback={<div>Loading...</div>}>
			  <OtherComponent />
		 </Suspense>
	 <MyErrorBoundary>
	  );
}
```
- React.lazy takes a function that must call a dynamic import(). 
    This must return a Promise which resolves to a module with a default export containing a React component.
- Suspense：如果在 MyComponent 渲染时尚未加载包含 OtherComponent 的模块，我们必须在等待加载时显示一些后备内容，如加载指示符，这是使用Suspense组件完成的
- 可以将 Suspense 组件放在惰性组件上方的任何位置，甚至可以使用一个 Suspense 组件包装多个惰性组件
- React.lazy() 和 Suspense 尚不可用于服务器端渲染。
    如果要在服务器渲染的应用程序中进行代码拆分，我们建议使用 Loadable Components 。
- Once you've created your Error Boundary, you can use it anywhere above your lazy components to display an error state when there's an error.
- 基于路由的代码分割
	- 可以使用React Router之类的库和React.lazy()一起 基于路由来拆分你的应用程序
	- React.lazy()目前仅支持默认导出， 如果要导入的模块使用命名导出，则可以创建一个中间模块，将其重新导出为默认模块

#### Context

- Context提供了一种通过组件树传递数据的方法，无需在每个级别手动传递props
- 在典型的 React 应用程序中，数据通过 props 自上而下（父到子）传递，
    但对于应用程序中许多组件所需的某些类型的 props（例如语言偏好,UI主题），这可能很繁琐
- Context 旨在共享一个组件树内可被视为 “全局” 的数据，例如当前经过身份验证的用户、主题、查询缓存或首选语言等。
- 不要仅仅为了避免在几个层级下的组件传递 props 而使用 context
	- 它适用于在**多个层级的多个组件**需要访问相同数据的情景
	- 请谨慎使用context，因为它使组件重用更加困难
	- 如果只想避免在多个级别上传递一些 props ，那么组件组合 component composition 通常比 Context 更简单
- API	
	- React.createContext()
		- 创建一个Context对象，当React渲染订阅这 个Context 对象的组件时，它将从组件树中匹配最接近的Provider中读取当前context的值
	- Context.Provider
		- 每个Context对象都附带一个Provider组件，允许Consumer组件订阅context的改变
		- 接受一个 value 属性用来传递给Consumer
		- 每当Provider的value属性发生变化时，所有作为Provider后代的Consumer组件都将重新渲染，从Provider到其后代使用者的传播不受shouldComponentUpdate()的约束
	- Context.Consumer
		- 用来定义一个订阅context变化的组件，需要接收一个函数作为子节点， 该函数接收当前context值并返回一个React节点
	- class.contextType	
		- 可以为类上的contextType属性分配由React.createContext()创建的Context对象，这样this.context就能获取到该Context类型最近的当前值
- 可以在 context 中向下传递一个函数，以允许 Consumer 更新 context
- 为了保持 context 的快速重新渲染，React 需要使每个 context Consumer 成为树中的一个独立节点
- Provider和Consumer都支持嵌套
- 因为context使用引用标识来确定何时重新渲染，当Provider的父节点重新渲染时，有一些陷阱可能触发 Consumer无意渲染

#### Legacy Context

示例   

```
const PropTypes = require('prop-types');

class Button extends React.Component {
  render() {
    return (
    // 从context中获取颜色
      <button style={{background: this.context.color}}>      
        {this.props.children}
      </button>
    );
  }
}
Button.contextTypes = {
  color: PropTypes.string
};

class Message extends React.Component {
  render() {
    return (
      <div>
        {this.props.text} <Button>Delete</Button>
      </div>
    );
  }
}

class MessageList extends React.Component {

  //定义context变量
  getChildContext() {
    return {color: "purple"};
  }

  render() {
    const children = this.props.messages.map((message) =>
      <Message text={message.text} />
    );
    return <div>{children}</div>;
  }
}
MessageList.childContextTypes = {
  color: PropTypes.string
};
```
#### Error Boundaries

- Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed. 
- Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.
- 错误边界无法捕获以下错误：
	- Event handlers
	- Asynchronous code (e.g. setTimeout or requestAnimationFrame callbacks)
	- Server side rendering
	- Errors thrown in the error boundary itself (rather than its children)
- A class component becomes an error boundary if it defines either (or both) of the lifecycle methods 
	- static getDerivedStateFromError() to render a fallback UI after an error has been thrown.
	- componentDidCatch() to log error information.
- Only class components can be error boundaries. 
- 错误边界仅获取其子组件的错误，无法捕获其自身的错误，如果一个错误边界无法渲染错误信息，则错误会向上冒泡至最接近的错误边界，这也类似于 JavaScript 中 catch {} 的工作机制
- 可以将错误边界包装在最顶层的路由组件并为用户展示一个异常的错误信息，就像服务端框架通常处理崩溃一样，也可以将单独的插件包装在错误边界内部以保护应用不受该组件崩溃的影响
- As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree.
- 放置一个异常的UI比完全移除它要更糟糕。对于支付类的应用来说，什么都不展示也比显示一堆错误更好。
- try / catch 非常棒，但其仅能在命令式代码（imperative code）下可用
- 如果需要在事件处理器内部捕获错误，使用普通的 JavaScript try / catch

#### Refs and the DOM

- ref提供了一种访问render()中创建的DOM节点或React元素的方式
- 在典型的React数据流中，props是父组件与子组件交互的唯一方式，修改子组件，需要使用新的 props 重新渲染它。
但是，某些情况下你需要**在常规数据流外强制修改子组件**。
要修改的子组件可以是React组件的实例，也可以是DOM元素。对于这两种情况，React 提供了解决办法。
- refs使用场景：
	- 处理focus、文本选择或媒体控制
	- 触发强制动画
	- 集成第三方 DOM 库
- Avoid using refs for anything that can be done declaratively. 
	- For example, instead of exposing open() and close() methods on a Dialog component, pass an isOpen prop to it.
- 使用 React.createRef() 创建 ref，通过 ref 属性来获得 React 元素
```
class MyComponent extends React.Component {

	  constructor(props) {
		super(props);
		this.myRef = React.createRef();
	  }
	  
	  render() {		  	       		
		return <div ref={this.myRef} />;
	  }
}
```
- 当一个 ref 属性被传递给一个 render()中的元素时，可以使用 ref 中的 current 属性对节点的引用进行访问。
- 当 ref 属性被用于一个普通的 HTML 元素时，React.createRef() 将接收底层 DOM 元素作为它的 current 属性以创建 ref 。
- 当 ref 属性被用于一个自定义类组件时，ref 对象将接收该组件已挂载的实例作为它的 current 。
- 不能在函数式组件上使用 ref 属性，因为它们没有实例。
	- `<MyFunctionalComponent ref={this.textInput} />`这样不会工作，但在MyFunctionalComponent()内部可以使用ref指向一个dom元素或class组件
- React会在组件加载时将DOM元素传入current属性，在卸载时则会改回 null。ref 的更新会发生在componentDidMount 或 componentDidUpdate 生命周期钩子之前。
- 在极少数情况下，你可能希望从父组件访问子节点的 DOM 节点，不建议这样做，因为它会破坏组件的封装
- Forwarding Refs使组件可以像暴露自己的 ref 一样暴露子组件的 ref
- 如果你对子组件的实现没有控制权的话，你剩下的选择是使用 findDOMNode()，但是不推荐
- 使用回调函数创建ref
```
 <input    type="text"     ref={el=>this.myRef=el}  />
```
- React将在组件挂载时将DOM元素传入ref 回调函数并调用，当卸载时传入 null 并调用它
	- ref中的回调函数会在组件componentDidMount，ComponentDidUpdate之前，或者componentWillUnmount之后执行
	- componentWillUnmount之后执行时，callback接收到的参数是null
- 可以在组件间传递回调形式的 refs，就像你可以传递通过 React.createRef() 创建的对象 refs 一样。
```
	function CustomTextInput(props) {
	  return (
		<div>
		  <input ref={props.inputRef} />
		</div>
	  );
	}
	
	class Parent extends React.Component {
	  render() {
		return (
		  <CustomTextInput
			inputRef={el => this.inputElement = el}
		  />
		);
	  }
	}
	Parent 传递给它的 ref 回调函数作为 inputRef 传递给 CustomTextInput，然后 CustomTextInput 通过 ref属性将其传递给 <input>。
	最终，Parent 中的 this.inputElement 将被设置为与 CustomTextIput 中的 <input> 元素相对应的 DOM 节点
	
	像上面通过内联函数来写ref，在更新期间它会被调用两次，因为函数的引用变了，react要清除掉老的ref，创建一个新的。
	清除掉老的ref时，给回调传入的参数是null，新建ref时，传入的是组件或者dom的引用。
	You can avoid this by defining the ref callback as a bound method on the class, but note that it shouldn’t matter in most cases.
```
- 字符串类型的ref不推荐使用
	- 问题
		- 不支持静态类型分析，如flow
		- string ref的指向与当前组件相关，容易出错，且需要react跟踪当前执行的组件
		- 参考 https://stackoverflow.com/questions/37468913/why-ref-string-is-legacy
	- 例子
	```
	<input ref="input1" />
	let inputEl = this.refs.input1;
	```
- 不管ref设置值是回调函数还是字符串，都可以通过ReactDOM.findDOMNode(ref)来获取组件挂载后真正的dom节点。
- 但是对于html元素使用ref的情况，ref本身引用的就是该元素的实际dom节点，无需使用ReactDOM.findDOMNode(ref)来获取，该方法常用于React组件上的ref。
- 不建议在父组件中直接访问子组件的实例方法来完成某些逻辑，在大部分情况下请使用标准的react数据流的方式来代替则更为清晰；
- 不要在组件的render方法中访问ref引用，render方法只是返回一个虚拟dom，这时组件不一定挂载到dom中或者render返回的虚拟dom不一定会更新到dom中。

#### Forwarding Refs

- Ref forwarding is a technique for automatically passing a ref through a component to one of its children
	- 对高阶组件非常有用
- 示例
```
	const FancyButton = React.forwardRef((props, ref) => (
	  <button ref={ref} className="FancyButton">
		{props.children}
	  </button>
	));
	
	// You can now get a ref directly to the DOM button:
	const ref = React.createRef();
	<FancyButton ref={ref}>Click me!</FancyButton>;
	
	通过这种方式，使用FancyButton的组件可以获得底层 button DOM节点的引用并在必要时访问它 - 就像他们直接使用DOM button 一样。
	ref.current 将指向 <button> DOM节点     
```    
- ref转发不限于DOM 组件，也可以将ref转发给类组件实例   
- 例子   
```
	一个打印输入组件props的高阶组件：
	
	function logProps(WrappedComponent) {
	
		  class LogProps extends React.Component {
			componentDidUpdate(prevProps) {
			  console.log('old props:', prevProps);
			  console.log('new props:', this.props);
			}
		
			render() {
			  return <WrappedComponent {...this.props} />;
			}
		  }
	
	  return LogProps;
	}
	
	class FancyButton extends React.Component {
		focus() {
			// ...
		  }
		render(){
			//...
		}
	}
	
	// Rather than exporting FancyButton, we export LogProps.
	// It will render a FancyButton though.
	export default logProps(FancyButton);
```
- If you add a ref to a HOC, the ref will refer to the outermost container component, not the wrapped component.
```
	import FancyButton from './FancyButton';
	
	const ref = React.createRef();
	
	// The FancyButton component we imported is the LogProps HOC.
	// Even though the rendered output will be the same,
	// Our ref will point to LogProps instead of the inner FancyButton component!
	// This means we can't call e.g. ref.current.focus()
	<FancyButton  label="Click Me"  handleClick={handleClick}
	  ref={ref}
	/>;
```
- ref和key都不是props，不会传递给子组件，ref会指向最外层容器组件，而不是内部组件
- React.forwardRef可以显示传递ref到内部组件
- React.forwardRef accepts a render function that receives props and ref parameters and returns a React node.
```
function logProps(Component) {

  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      const {forwardedRef, ...rest} = this.props;

      // Assign the custom prop "forwardedRef" as a ref
      return <Component ref={forwardedRef} {...rest} />;
    }
  }

  // Note the second param "ref" provided by React.forwardRef.
  // We can pass it along to LogProps as a regular prop, e.g. "forwardedRef"
  // And it can then be attached to the Component.
  function forwardRef(props, ref) {
    return <LogProps {...props} forwardedRef={ref} />;
  }

  forwardRef.displayName = Component.displayName || Component.name;
  
  return React.forwardRef(forwardRef);
}
```

#### Fragments

- Fragments 可以让你聚合一个子元素列表，并且不在DOM中增加额外节点
- `<></>`是`<React.Fragment>`的语法糖，只是它不支持 键(keys) 或 属性(attributes)
- key is the only attribute that can be passed to Fragment. In the future, we may add support for additional attributes, such as event handlers.

#### Higher-Order Components

- A higher-order component (HOC) is an advanced technique in React for reusing component logic
- a higher-order component is a function that takes a component and returns a new component.
- 高阶组件在React第三方库中很常见，比如Redux的connect和Relay的createFragmentContainer.
- Use HOCs For Cross-Cutting Concerns
	- 之前建议使用mixins解决交叉问题
	- mixin可能导致命名冲突
	- mixin引入了隐式依赖关系，不方便组件层级移动和修改
	- mixin会不断增加组件复杂度
	- 参考 https://lizhiyao.github.io/2018/01/05/mixins-considered-harmful/
- 高阶组件最好是通过将输入组件包裹在容器组件的方式来使用组合，不要直接修改输入组件，高阶组件使用容器作为其实现的一部分，可以将高阶组件视为定义参数化容器组件
```
function logProps(WrappedComponent) {
  return class extends React.Component {
    componentWillReceiveProps(nextProps) {
      console.log('Current props: ', this.props);
      console.log('Next props: ', nextProps);
    }
    render() {
      // 用容器组件组合包裹组件且不修改包裹组件，这才是正确的打开方式。
      return <WrappedComponent {...this.props} />;
    }
  }
}
```
- 高阶组件可以向组件添加功能，不应该大幅度地改变功能，应该通过props传递那些与特定功能无关的特性
- redux的connect是一个返回高阶组件的高阶函数
- 注意
	- 不要在render()中使用高阶组件
		- 示例
		```
		render() {
		  // 每一次render函数调用都会创建一个新的EnhancedComponent实例
		  // EnhancedComponent1 !== EnhancedComponent2
		  const EnhancedComponent = enhance(MyComponent);
		  // 每一次都会使子对象树完全被卸载或移除
		  return <EnhancedComponent />;
		}
		```
		- 重新加载一个组件会引起原有组件的所有状态和子组件丢失
		- 在一些极少的例子中需要动态地引用高阶组件，可以在组件的声明周期函数中使用或者在构造函数中使用  
	- 输入组件的静态方法要做拷贝
		- 示例
		```
		// 定义静态方法
		WrappedComponent.staticMethod = function() {/*...*/}
		// 使用高阶组件
		const EnhancedComponent = enhance(WrappedComponent);
		// 增强型组件没有静态方法
		typeof EnhancedComponent.staticMethod === 'undefined'  // true
		```
		- 这需要清楚的知道有哪些静态方法需要拷贝，可以使用hoist-non-react-statics来自动处理，它会自动拷贝所有非React的静态方法
	- 高阶组件可以传递所有的props属性给包裹的组件，但是不能传递ref引用
		-  如果向一个由高阶组件创建的组件的元素添加ref应用，那么ref指向的是最外层容器组件实例的，而不是包裹组件
		- 解决这个问题的方法是使用 React.forwardRef

#### Integrating with Other Libraries

- Integrating with DOM Manipulation Plugins
	- React is unaware of changes made to the DOM outside of React. It determines updates based on its own internal representation
	- The easiest way to avoid conflicts is to prevent the React component from updating. You can do this by rendering elements that React has no reason to update, like an empty <div />.
	- 与jQuery集成示例
	```
	class SomePlugin extends React.Component {
		  componentDidMount() {
			this.$el = $(this.el);
			this.$el.somePlugin();
		  }
		
		  componentWillUnmount() {
			this.$el.somePlugin('destroy');
		  }
		
		  render() {
			return <div ref={el => this.el = el} />;
		  }
	}
	```
	- 为了防止内存泄漏，请务必在生命周期函数中移除插件挂载的事件监听器
- Integrating with Other View Libraries
	- Although React is commonly used at startup to load a single root React component into the DOM, 
	  ReactDOM.render() can also be called multiple times for independent parts of the UI which can be as small as a button, or as large as an app.
	- Replacing String-Based Rendering with React  
	```
	$('#container').html('<button id="btn">Say Hello</button>');
	$('#btn').click(function() {
	  alert('Hello!');
	});
	```
	- 对于$el.html(htmlString)：Just rewrite the string based rendering as a React component.
	```
	ReactDOM.render(
	  <Button />,
	  document.getElementById('container'),
	  function() {
		$('#btn').click(function() {
		  alert('Hello!');
		});
	  }
	);
	```
- Integrating with Model Layers
	- React components can use a model layer from other frameworks and libraries.
	- 更推荐使用redux

#### JSX In Depth

- JSX是为 `React.createElement(component, props, ...children) ` 方法提供的语法糖
- 如果没有子代，你还可以使用自闭合标签，如`<div className="sidebar" />`   ->  `React.createElement( 'div', {className: 'sidebar'}, null )`  
- JSX 的标签名决定了 React 元素的类型，大写开头的 JSX 标签表示一个 React 组件，这些标签将会被编译为同名变量并被引用
- 可以使用JSX的点表示法来引用 React 组件，可以方便地从一个模块中导出许多 React 组件
- 当元素类型以小写字母开头时，它表示一个内置的组件，如` <div>` 或` <span>` ，React 会将小写开头的标签名认为是 HTML 原生标签  
- 建议用大写开头命名组件，如果你的组件以小写字母开头，请在JSX中使用之前其赋值给大写开头的变量
- 想通过属性值条件渲染组件时，要先将类型赋值给大写开头的变量
```
	import React from 'react';
	import { PhotoStory, VideoStory } from './stories';
	
	const components = {
	  photo: PhotoStory,
	  video: VideoStory
	};
	
	function Story(props) {
	  // 正确！JSX 标签名可以为大写开头的变量。
	  const SpecificStory = components[props.storyType];
	  return <SpecificStory story={props.story} />;
	}
```
- jsx的属性值
	- 用 `{ }` 包含的js表达式
	- 字符串
	- 如果你没有给属性传值，它默认为 true
	``` 
	<MyTextBox autocomplete />
	等价于
	<MyTextBox autocomplete={true} />
	```
	- 现有对象使用使用扩展操作符来将整个对象作为属性传递给子组件 `return <Greeting {...props} />;`
- 在包含开始和结束标签的JSX表达式中，标记之间的内容作为特殊的参数传递：props.children
- 可以在开始和结束标签之间放入一个字符串，则 props.children 就是那个字符串
- `<MyComponent>Hello world!</MyComponent>`，MyComponent 的 props.children 值将会直接是 "hello world!"
- JSX 会移除空行和开始与结尾处的空格。标签邻近的新行也会被移除，字符串常量内部的换行会被压缩成一个空格
- props.children可以像其它属性一样传递任何数据，而不仅仅是 React 元素，如果你使用自定义组件，则可以将调用 props.children 来获得传递的子代
- false、null、undefined 和 true 都是有效的子代，但它们不会直接被渲染
	- 数字0会被渲染，请确保 && 前面的表达式始终为布尔值
	- 想让类似 false、true、null 或 undefined 出现在输出中，必须先把它转换成字符串
- These JSX expressions will all render to the same thing:
```
<div />
<div></div>
<div>{true}</div>
<div>{false}</div>
<div>{null}</div>
<div>{undefined}</div>
```
- This JSX only renders a <Header /> if showHeader is true:
```
<div>
{showHeader && <Header />}
<Content />
</div>
```
	
#### Optimizing Performance

- Use the Production Build
- Profiling Components with the Chrome Performance Tab: 使用Chrome性能分析工具分析组件性能
	- 先暂停React DevTools扩展，再打开Chrome DevTools Performance并点击Record，在User Timing标签下，React事件将会分组列出
- Profiling Components with the React DevTools Profiler
- Virtualize Long Lists
	- If your application renders long lists of data (hundreds or thousands of rows), we recommended using a technique known as “windowing”.
	- This technique only renders a small subset of your rows at any given time, and can dramatically reduce the time it takes to re-render the components as well as the number of DOM nodes created.
	- react-window and react-virtualized are popular windowing libraries. They provide several reusable components for displaying lists, grids, and tabular data.
- Avoid Reconciliation
	- When a component’s props or state change, React decides whether an actual DOM update is necessary 
	  by comparing the newly returned element with the previously rendered one. When they are not equal, React will update the DOM.
	- shouldComponentUpdate() is triggered before the re-rendering process starts. The default implementation of this function returns true
	- 示例：when we’re entering a second todo, the first todo also flashes on the screen on every keystroke.
	- In most cases, instead of writing shouldComponentUpdate() by hand, you can inherit from React.PureComponent. 
	  It is equivalent to implementing shouldComponentUpdate() with a shallow comparison of current and previous props and state.
- shouldComponentUpdate原理示意图
- Using Immutable Data Structures
 	- Immutable.js 通过结构共享实现(Structural Sharing)地不可变的(Immutable)、持久的(Persistent)集合
 		- Immutable: once created, a collection cannot be altered at another point in time.
 		- Persistent: new collections can be created from a previous collection and a mutation such as set. The original collection is still valid after the new collection is created.
 		- Structural Sharing: new collections are created using as much of the same structure as the original collection as possible, reducing copying to a minimum to improve performance.
	- 不可变数据提供了一种更简单的方式来追踪对象的改变，这正是实现 shouldComponentUpdate 所需要的
	
#### Portals

- Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.
	- `ReactDOM.createPortal(child, container)`
	- child is any renderable React child, such as an element, string, or fragment
	- container is a DOM element
- Normally, when you return an element from a component's render method, it's mounted into the DOM as a child of the nearest parent node
- A typical use case for portals is when a parent component has an overflow: hidden or z-index style, but you need the child to visually break outof its container. 
	- For example, dialogs, hovercards, and tooltips.
- Even though a portal can be anywhere in the DOM tree, it behaves like a normal React child in every other way. Features like context work exactly the same
- An event fired from inside a portal will propagate to ancestors in the containing React tree, even if those elements are not ancestors in the DOM tree.

#### React Without ES6

- 定义类
	- `class Greeting extends React.Component{}`
	- 使用 create-react-class
	```
	var createReactClass = require('create-react-class');
	var Greeting = createReactClass({
	  render: function() {
		return <h1>Hello, {this.props.name}</h1>;
	  }
	});
	```
- 声明defaultProps
	- `Greeting.defaultProps = {}`
	- `getDefaultProps: function() {}`
- 设置初始state
	- 在class的constructor(){ this.state={}}
	- ` getInitialState: function() {}`
- 自动绑定
	- es6的class中方法没有自动绑定this，需要在constructor()中`this.handleClick = this.handleClick.bind(this);
	- createReactClass()内会自动绑定
- mixins
	- es6不支持混入，推荐使用高阶组件
	- createReactClass()作为一个属性 ` mixins: [SetIntervalMixin]`
	
#### React Without JSX

- 每一个 JSX 元素都是调用 `React.createElement(component, props, ...children)` 的语法糖

#### Reconciliation 一致性比较

参考 https://reactjs.org/docs/reconciliation.html  

- When you use React, at a single point in time you can think of the render() function as creating a tree of React elements. 
On the next state or props update, that render() function will return a different tree of React elements. 
React then needs to figure out how to efficiently update the UI to match the most recent tree.
- 将一棵树转换为另一棵树的最小操作数算法问题的通用方案，树中元素个数为n，最先进的算法 的时间复杂度为O(n3) 
- React基于两点假设，实现了一个启发的O(n)算法：
	- 两个不同类型的元素将产生不同的树
	- 通过渲染器附带key属性，开发者可以示意哪些子元素可能是稳定的
- 对比算法
	- 当对比两棵树时，React首先比较两个根节点。
	- 当两棵树根元素类型类型不同时，React将卸载旧树并重新构建新树
		- 当树被卸载，旧的DOM节点将被销毁，会调用componentWillUnmount()
		- 当构建一棵新树，新的DOM节点被插入到DOM中，将依次调用componentWillMount()和componentDidMount()，任何与旧树有关的状态都将丢弃
	- 当根元素类型相同时，react会比较两者的属性，然后只更新改变过的属性
	- react再递归处理子元素
		- 组件更新时，实例保持不变，state能够在渲染之间保留
		- React通过更新底层组件实例的props来产生新元素，并在底层实例上依次调用componentWillReceiveProps() 和 componentWillUpdate() 方法。
	- 接下来，render()方法被调用，同时对比算法会递归处理之前的结果和新的结果。
	- 递归处理节点的子元素时，react会同时遍历两者的子元素列表，一旦有不同，react就会做出变化
	- react支持key属性，当子节点有key时，React使用key来匹配原本树的子节点和新树的子节点
		- key必须在其兄弟节点中是唯一的，而非全局唯一。
		- 可以传递他们在数组中的索引作为key。若元素没有重排，该方法效果不错，但重排会使得其变慢。
		```
		当索引用作key时，组件状态在重新排序时也会有问题。
		组件实例基于key进行更新和重用。如果key是索引，则item的顺序变化会改变key值。
		这将导致非受控组件的状态可能会以意想不到的方式混淆和更新。
		```
		- In the current implementation, you can express the fact that a subtree has been moved amongst its siblings,
		but you cannot tell that it has moved somewhere else. The algorithm will rerender that full subtree.
- react依赖于启发式算法，两个前提条件应该得到满足，若不满足会有性能问题
	- The algorithm will not try to match subtrees of different component types.
	  If you see yourself alternating between two component types with very similar output, you may want to make it the same type. 
	  In practice, we haven't found this to be an issue.
	- Keys should be stable, predictable, and unique. Unstable keys (like those produced by Math.random()) will cause many component instances
	  and DOM nodes to be unnecessarily recreated, which can cause performance degradation and lost state in child components.

#### Render Props

- "render prop" refers to a technique for sharing code between React components using a prop whose value is a function.
	- Libraries that use render props include React Router and Downshift.
-  component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic.
```
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```
- Use Render Props for Cross-Cutting Concerns
- you can implement most higher-order components (HOC) using a regular component with a render prop. 
- Using Props  name Other Than  *render*     

```
<Mouse children={mouse => (
  <p>The mouse position is {mouse.x}, {mouse.y}</p>
)}/>

等价于

<Mouse>
  {mouse => (
    <p>The mouse position is {mouse.x}, {mouse.y}</p>
  )}
</Mouse>
```   
- render prop 会抵消使用 React.PureComponent 带来的优势
	- because the shallow prop comparison will always return false for new props, and each render in this case will generate a new value for the render prop.

#### Typechecking With PropTypes

- 要检查组件的属性，需要配置propTypes ，出于性能原因，propTypes 只在开发模式下进行检查
- PropTypes.element 可以指定只传递一个子代
- 可以通过配置 defaultProps 为 props定义默认值                                                                            
- defaultProps 用来确保this.props.name在父组件没有特别指定的情况下，有一个初始值，类型检查发生在defaultProps赋值之后，所以类型检查也会应用在defaultProps上

#### Static Type Checking

- 对于复杂的代码库，建议使用 Flow 或者 TypeScript 来替代 PropTypes
- flow
- typescript
- reason： 是一门基于 OCaml 的语言，既可以通过 BuckleScript 被同编译为 JavaScript，也支持直接编译为原生的二进制汇编

#### Strict Mode

- StrictMode is a tool for highlighting potential problems in an application. 
- StrictMode 不会渲染任何真实的UI
- 严格模式检查只在开发模式下运行，不会与生产模式冲突
1. Identifying components with unsafe lifecycles
	- componentWillMount， componentWillReceiveProps， componentWillUpdate
2. Warning about legacy string ref API usage
	- 推荐使用回调函数或React.createRef();
3. Warning about deprecated findDOMNode usage
	- 推荐直接将 ref 附加到 DOM 节点上
4. Detecting unexpected side effects
	- react在 render 和 commit 两个阶段起作用
	- render phase determines what changes need to be made to e.g. the DOM. 
	  During this phase, React calls render and then compares the result to the previous render.
	- commit phase is when React applies any changes.
	  (In the case of React DOM, this is when React inserts, updates, and removes DOM nodes.) 
	  React also calls lifecycles like componentDidMount and componentDidUpdate during this phase.
	-  commit phase is usually very fast, but rendering can be slow
	- the upcoming async mode ( not enabled by default yet) breaks the rendering work into pieces, pausing and resuming the work to avoid blocking the browser.
	- This means that React may invoke render phase lifecycles more than once before committing,
	  or it may invoke them without committing at all (because of an error or a higher priority interruption).
	- Render phase lifecycles include the following class component methods:
		- constructor
		- componentWillMount
		- componentWillReceiveProps
		- componentWillUpdate
		- getDerivedStateFromProps
		- shouldComponentUpdate
		- render
		- setState updater functions (the first argument)
	- 因为渲染阶段的方法可能会调用多次，所以尽量不放在这些方法中包含副作用
	- Strict mode can’t automatically detect side effects for you, but it can help you spot them by making them a little more deterministic. 
	  This is done by intentionally double-invoking the following methods:  
		- constructor, render, setState
		- 只在开发模式生效，生产模式下生命周期不会被双调用

5. Detecting legacy context API

####  Uncontrolled Components

- 如果要让表单数据由DOM处理，替代方案为使用非受控组件    
- 要编写一个非受控组件，而非为每个状态更新编写事件处理程序，你可以 使用 ref 从 DOM 获取表单值。
- 非受控组件将真实数据保存在 DOM 中，更容易集成 React 和非 React 代码。如果想快速而随性，这样可以减少代码。否则，应使用受控组件。
- 使用非受控组件时，通常你希望 React 可以为其指定初始值，但不再控制后续更新，可以指定一个 defaultValue 属性而不是 value
- 在 React 的生命周期中，表单元素上的 value 属性将会覆盖 DOM 中的值
- `<input type="file" /> `始终是一个非受控制的组件，因为它的值只能由用户设置，而不是以编程方式设置
- 示例  
```
	class FileInput extends React.Component {
	  constructor(props) {
		super(props);
		this.handleSubmit = this.handleSubmit.bind(this);
	  }
	  handleSubmit(event) {
		event.preventDefault();
		alert(      `Selected file - ${this.fileInput.files[0].name}`    );
	  }
	
	  render() {
		return (
		  <form onSubmit={this.handleSubmit}>
			<label>
			  Upload file:
			  <input
				type="file"
				ref={input => { this.fileInput = input;  }}
			  />
	
			</label>
			<br />
			<button type="submit">Submit</button>
		  </form>
		);
	  }
	}
	
	ReactDOM.render(
	  <FileInput />,
	  document.getElementById('root')
	);
```

#### Web Components

- React and Web Components are built to solve different problems. 
- Web Components provide strong encapsulation for reusable components
- React provides a declarative library that keeps the DOM in sync with your data.
- Using Web Components in React
```
class HelloMessage extends React.Component {
  render() {
    return <div>Hello <x-search>{this.props.name}</x-search>!</div>;
  }
}
```
- Using React in your Web Components
```
class XSearch extends HTMLElement {
  connectedCallback() {
    const mountPoint = document.createElement('span');
    this.attachShadow({ mode: 'open' }).appendChild(mountPoint);

    const name = this.getAttribute('name');
    const url = 'https://www.google.com/search?q=' + encodeURIComponent(name);
    ReactDOM.render(<a href={url}>{name}</a>, mountPoint);
  }
}
customElements.define('x-search', XSearch);
```
	
### 4. api

#### React API

- React.Component
- React.PureComponent
- React.memo
- React.Fragment

- createElement()
- createFactory()      

- cloneElement()
- isValidElement()
- React.Children

- React.createRef
- React.forwardRef

- Suspense
	- Suspense lets components “wait” for something before rendering. 
		- Today, Suspense only supports one use case: loading components dynamically with React.lazy. 
		- In the future, it will support other use cases like data fetching.
	- React.lazy
	- React.Suspense

#### React.Component

- The Component Lifecycle
	- Mounting：methods are called in the following order when an instance of a component is being created and inserted into the DOM
		- constructor()
		- static getDerivedStateFromProps()
		- render()
		- componentDidMount()
	- Updating：methods are called in the following order when a component is being re-rendered
		- static getDerivedStateFromProps()
		- shouldComponentUpdate()
		- render()
		- getSnapshotBeforeUpdate()
		- componentDidUpdate()
	- Unmounting： method is called when a component is being removed from the DOM
		- componentWillUnmount()
	- Error Handling：methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.
		- static getDerivedStateFromError()
		- componentDidCatch()
- Other APIs
	- setState()
	- forceUpdate()
- Class Properties
	- defaultProps
	- displayName
- Instance Properties
	- props
	- state

#### ReactDOM

- `ReactDOM.render(element, container[, callback])`
	- Render a React element into the DOM in the supplied container and return a reference to the component (or returns null for stateless components).
	- If the React element was previously rendered into container, this will perform an update on it 
	  and only mutate the DOM as necessary to reflect the latest React element.
        -  If the optional callback is provided, it will be executed after the component is rendered or updated.
        - ReactDOM.render() does not modify the container node (only modifies the children of the container)
        - ReactDOM.render() currently returns a reference to the root ReactComponent instance. 
        	- 不推荐直接使用返回值的引用，因为后期版本的React可能会异步渲染组件
        	- 如果要使用组件实例的引用，推荐使用 callback ref
	- Using ReactDOM.render() to hydrate a server-rendered container is deprecated and will be removed in React 17. Use hydrate() instead.
- `ReactDOM.hydrate(element, container[, callback])`
	- Same as render(), but is used to hydrate a container whose HTML contents were rendered by ReactDOMServer. 
	- React will attempt to attach event listeners to the existing markup.
	- React expects that the rendered content is identical between the server and the client. It can patch up differences in text content
	- If you intentionally need to render something different on the server and the client, you can do a two-pass rendering. 
- `ReactDOM.unmountComponentAtNode(container)`
	- Remove a mounted React component from the DOM and clean up its event handlers and state. 
	- If no component was mounted in the container, calling this function does nothing. 
	- Returns true if a component was unmounted and false if there was no component to unmount.
- `ReactDOM.findDOMNode(component)`
	- findDOMNode is an escape hatch used to access the underlying DOM node. 
	- In most cases, use of this escape hatch is discouraged because it pierces the component abstraction. 
	- It has been deprecated in StrictMode.
	- If ` component` has been mounted into the DOM, this returns the corresponding native browser DOM element. 
	- This method is useful for reading values out of the DOM,
		- such as form field values and performing DOM measurements. 
	- In most cases, you can attach a ref to the DOM node and avoid using findDOMNode at all.
	- When a component renders to null or false, findDOMNode returns null. 
	- When a component renders to a string, findDOMNode returns a text DOM node containing that value. 
	- As of React 16, a component may return a fragment with multiple children, in which case findDOMNode will return the DOM node corresponding to the first non-empty child.
	- findDOMNode only works on mounted components (that is, components that have been placed in the DOM).
	- If you try to call this on a component that has not been mounted yet (like calling findDOMNode() in render() on a component that has yet to be created) an exception will be thrown.
	- findDOMNode cannot be used on function components.
- `ReactDOM.createPortal(child, container)`
	- Portals provide a way to render children into a DOM node that exists outside the hierarchy of the DOM component.

#### ReactDOMServer

- ReactDOMServer enables you to render components to static markup.
	- Typically, it's used on a Node server:
- The following methods can be used in both the server and browser environments
	- renderToString()
	- renderToStaticMarkup()
- The following methods depend on a package (stream) that is only available on the server, and won't work in the browser.
	- renderToNodeStream()
	- renderToStaticNodeStream()
- `ReactDOMServer.renderToString(element)`
	- Render a React element to its initial HTML. 
	- Return an HTML string. 
- `ReactDOMServer.renderToStaticMarkup(element)`
	- Similar to renderToString, except this doesn't create extra DOM attributes that React uses internally, such as `data-reactroot.`
	- If you plan to use React on the client to make the markup interactive, do not use this method. Instead, use renderToString on the server and ReactDOM.hydrate() on the client.
- `ReactDOMServer.renderToNodeStream(element)`
	- Render a React element to its initial HTML. 
	- Return a Readable stream that outputs an HTML string. 
	- The HTML output by this stream is exactly equal to what `ReactDOMServer.renderToString` would return.
- `ReactDOMServer.renderToStaticNodeStream(element)`
	- Similar to renderToNodeStream, except this doesn’t create extra DOM attributes that React uses internally

#### DOM Elements

- React implements a browser-independent DOM system for performance and cross-browser compatibility. 
- In React, all DOM properties and attributes (including event handlers) should be camelCased.
	- The exception is aria-* and data-* attributes, which should be lowercased. For example, you can keep aria-label as aria-label.
- There are a number of attributes that work differently between React and HTML:
	- input-checkbox/radio: checked, defaultChecked
	- className
	- dangerouslySetInnerHTML
		- 不推荐使用，很容易暴露用户，收到xss攻击
		-  React's replacement for using innerHTML in the browser DOM
		- 示例
		```
		function MyComponent() {
		  return <div dangerouslySetInnerHTML={ {__html: 'First &middot; Second'} } />;
		}
		```
	- htmlFor
	- onChange
		- whenever a form field is changed, this event is fired.
		-  React relies on this event to handle user input in real time.
	- selected
		- selected attribute is supported by `<option>` components.
	- style
		- 不推荐直接使用style属性，推荐使用className
		- 一般用来实现动态样式
		- React 会自动为某些内联样式的数字属性值附加一个 “px” 后缀
	- suppressContentEditableWarning
	- suppressHydrationWarning
	- value
		- `<input>` 和 `<textarea>` 组件支持 value 属性，一般用于受控组件
		- `defaultValue` is the uncontrolled equivalent, which sets the value of the component when it is first mounted.
- As of React 16, any standard or custom DOM attributes are fully supported.
- Similarly, all SVG attributes are fully supported:

#### SyntheticEvent

- Your event handlers will be passed instances of SyntheticEvent, a cross-browser wrapper around the browser's native event. 
	- It has the same interface as the browser's native event, including stopPropagation() and preventDefault(), except the events work identically across all browsers.
- If you find that you need the underlying browser event for some reason, simply use the nativeEvent attribute to get it.
- 从v0.14起，从事件处理程序return false将不再停止事件冒泡，应该根据需要手动 e.stopPropagation() 或 e.preventDefault() 
- SyntheticEvent is pooled.
	- This means that the SyntheticEvent object will be reused and all properties will be nullified after the event callback has been invoked.
	-  you cannot access the event in an asynchronous way.
		- If you want to access the event properties in an asynchronous way, you should call event.persist() on the event
- React normalizes events so that they have consistent properties across different browsers.
- Supported Events
	- Clipboard Events
	- Composition Events
	- Keyboard Events
	- Focus Events
	- Form Events
	- Mouse Events
	- Pointer Events
		- As defined in the W3 spec, pointer events extend Mouse Events 
	- Selection Events
	- Touch Events
	- UI Events
	- Wheel Events
	- Media Events
	- Image Events
	- Animation Events
	- Transition Events
	- Other Events

#### Test Utilities

- `import ReactTestUtils from 'react-dom/test-utils';`
- jest是Facebook发布的js测试工具
- enzyme是Airbnb发布的react测试工具
- Shallow Rendering
	- Shallow rendering lets you render a component "one level deep" and assert facts about what its render method returns, 
	  without worrying about the behavior of child components, which are not instantiated or rendered. 
        - This does not require a DOM.  
- Simulate an event dispatch on a DOM node with optional eventData event data.
- renderIntoDocument()
	- Render a React element into a detached DOM node in the document. This function requires a DOM.
- mockComponent()
	- We recommend using shallow rendering or jest.mock() instead.
- isElement()
- isElementOfType()
- isDOMComponent()
- isCompositeComponent()
	- Returns true if instance is a user-defined component, such as a class or a function.
- findAllInRenderedTree()
- findRenderedDOMComponentWithClass()
- findRenderedDOMComponentWithTag()
- findRenderedComponentWithType()

#### Shallow Renderer

- 组件
```
function MyComponent() {
  return (
    <div>
      <span className="heading">Title</span>
      <Subcomponent foo="bar" />
    </div>
  );
}
```

- 测试    

```
import ShallowRenderer from 'react-test-renderer/shallow';

// in your test:
const renderer = new ShallowRenderer();
renderer.render(<MyComponent />);
const result = renderer.getRenderOutput();

expect(result.type).toBe('div');
expect(result.props.children).toEqual([
  <span className="heading">Title</span>,
  <Subcomponent foo="bar" />
]);
```
- Shallow testing currently has some limitations, namely not supporting refs.
- We also recommend checking out Enzyme’s Shallow Rendering API. 
	- It provides a nicer higher-level API over the same functionality.
- `shallowRenderer.render()`
	- similar to ReactDOM.render() but it doesn't require DOM and only renders a single level deep.
- `shallowRenderer.getRenderOutput()`
	- get the shallowly rendered output.

#### Test Renderer

- `import TestRenderer from 'react-test-renderer';`
- This package provides a React renderer that can be used to render React components to pure JavaScript objects,
	- without depending on the DOM or a native mobile environment.
-  this package makes it easy to grab a snapshot of the platform view hierarchy (similar to a DOM tree) rendered by a React DOM or React Native component 
	- without using a browser or jsdom.

#### JavaScript Environment Requirements

- React 16 depends on the collection types Map and Set.
- React also depends on requestAnimationFrame (even in test environments).

#### Glossary of React Terms

- Single-page Application
	- 所有的交互行为不会导致页面重新加载
- js compiler
	- babel
- bundler
	- Bundlers take JavaScript and CSS code written as separate modules (often hundreds of them), and combine them together into a few files better optimized for the browsers. 
	- Some bundlers commonly used in React applications include Webpack and Browserify.
- Package Managers
	- npm
	- yarn
- jsx
- React Elements
	-  An element describes what you want to see on the screen. 
	- React elements are immutable.
	- Typically, elements are not used directly, but get returned from components.
- React Components
	- React components are small, reusable pieces of code that return a React element to be rendered to the page.
	-  if a part of your UI is used several times (Button, Panel, Avatar), or is complex enough on its own (App, FeedStory, Comment), it is a good candidate to be a reusable component.
- props
	- readonly
	- props are inputs to a React component. They are data passed down from a parent component to a child component.
	- props.children is available on every component. It contains the content between the opening and closing tags of a component. 
- state
	- to change state, you must call this.setState()
	- A component needs state when some data associated with it changes over time.
	- Only components defined as classes can have state.
- The most important difference between state and props is that 
	- props are passed from a parent component, but state is managed by the component itself.
- Controlled vs. Uncontrolled Components
	- An input form element whose value is controlled by React is called a controlled component. 
	- An uncontrolled component works like form elements do outside of React. 
- key
	- A `key` is a special string attribute you need to include when creating arrays of elements. 
	- Keys help React identify which items have changed, are added, or are removed.
- ref
	- ref is an attribute that you can attach to any component.
	- 不要过度使用 Refs。如果你发现自己经常在应用程序中使用refs来“搞事情”，请考虑使用状态提升。
- Reconciliation
	- When a component's props or state change, 
	  React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. 
	  When they are not equal, React will update the DOM.
	  This process is called “reconciliation”.
  
### 5. hooks

#### Introducing Hooks

- Hooks are an upcoming feature that lets you use state and other React features without writing a class. 
	- They're currently in React v16.7.0-alpha.    
  
```
import { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
- Hooks are 100% backwards-compatible. Hooks don’t contain any breaking changes.
- There are no plans to remove classes from React. 
- Motivation
	- It's hard to reuse stateful logic between components
		- render props and higher-order components that try to solve this.
		- 但是这些模式要求您在使用它们时重构组件，这可能很麻烦并且使代码更难以跟踪。
		- If you look at a typical React application in React DevTools, you will likely find a “wrapper hell” of components surrounded by layers of providers, consumers, higher-order components, render props, and other abstractions. 
		- With Hooks, you can extract stateful logic from a component so it can be tested independently and reused. 
		- Hooks allow you to reuse stateful logic without changing your component hierarchy. 
	- Complex components become hard to understand
		- . Each lifecycle method often contains a mix of unrelated logic. 
		- This is one of the reasons many people prefer to combine React with a separate state management library.
		- However, that often introduces too much abstraction, requires you to jump between different files, and makes reusing components more difficult.
		-  Hooks let you split one component into smaller functions based on what pieces are related (such as setting up a subscription or fetching data), rather than forcing a split based on lifecycle methods. 
	- Classes confuse both people and machines
		- this的指向问题
		- 事件绑定
		-  make sure React stays relevant in the next five years.
		-  ahead-of-time compilation of components has a lot of future potential.
		- Hooks let you use more of React's features without classes， but with functions.
- Gradual Adoption Strategy
	- There are no plans to remove classes from React.
	- We intend for Hooks to cover all existing use cases for classes,
	- but we will keep supporting class components for the foreseeable future.
	
#### Hooks at a Glance

- State Hook
	- Declaring multiple state variables
	- Hooks are functions that let you "hook into" React state and lifecycle features from function components.
		- Hooks don't work inside classes — they let you use React without classes
		- React provides a few built-in Hooks like useState. You can also create your own Hooks to reuse stateful behavior between different components.

- Effect Hook
	- You've likely performed data fetching, subscriptions, or manually changing the DOM from React components before. 
		- We call these operations  `side effects`  (or "effects" for short) because they can affect other components and can't be done during rendering.
		- useEffect, adds the ability to perform side effects from a function component. 
		- It serves the same purpose as componentDidMount, componentDidUpdate, and componentWillUnmount in React classes, but unified into a single API.

- Rules of Hooks
	- Only call Hooks at the top level. Don't call Hooks inside loops, conditions, or nested functions.
	- Only call Hooks from React function components. Don't call Hooks from regular JavaScript functions. 

- Building Your Own Hooks
	- Sometimes, we want to reuse some stateful logic between components. 
	- Traditionally, there were two popular solutions to this problem: higher-order components and render props. 
	- Custom Hooks let you do this, but without adding more components to your tree.

- Other Hooks
	- useContext
	- useReducer

#### Using the State Hook


#### Using the Effect Hook


#### Rules of Hooks


#### Building Your Own Hooks


#### Hooks API Reference


#### Hooks FAQ

- Adoption Strategy
	- Should I use Hooks, classes, or a mix of both?
		- We don't recommend rewriting your existing classes to Hooks
		- You can't use Hooks inside of a class component, but you can definitely mix classes and function components with Hooks in a single tree. 
		- Whether a component is a class or a function that uses Hooks is an implementation detail of that component. 
		- In the longer term, we expect Hooks to be the primary way people write React components.
	
	- Do Hooks cover all use cases for classes?
		- Our goal is for Hooks to cover all use cases for classes as soon as possible. 
		- There are no Hook equivalents to the uncommon getSnapshotBeforeUpdate and componentDidCatch lifecycles yet, but we plan to add them soon.
		- It is a very early time for Hooks, so some integrations like DevTools support、FLow、TypeScript、3rd-party libraries  might be incompatible
		
	- Do Hooks replace render props and higher-order components?
		- Often, render props and higher-order components render only a single child. 
		- There is still a place for both patterns (for example, a virtual scroller component might have a renderItem prop, or a visual container component might have its own DOM structure).
		- But in most cases, Hooks will be sufficient and can help reduce nesting in your tree.
	
	- What do Hooks mean for popular APIs like Redux connect() and React Router?
		- You can continue to use the exact same APIs as you always have; they'll continue to work.
		- In the future, new versions of these libraries might also export custom Hooks such as useRedux() or useRouter() that let you use the same features without needing wrapper components.
		
	- Do Hooks work with static typing?
		-  Flow and TypeScript teams plan to include definitions for React Hooks in the future.
	
	- How to test components that use Hooks?
		-  If your testing solution doesn’t rely on React internals, testing components with Hooks shouldn’t be different from how you normally test components.
		
- From Classes to Hooks
	- How do lifecycle methods correspond to Hooks?
		- constructor: Function components don't need a constructor. You can initialize the state in the useState call. If computing it is expensive, you can pass a function to useState.
		- getDerivedStateFromProps: Schedule an update while rendering instead.
		- shouldComponentUpdate: See React.memo below.
		- render: This is the function component body itself.
		- componentDidMount, componentDidUpdate, componentWillUnmount: The useEffect Hook can express all combinations of these (including less common cases).
		- componentDidCatch and getDerivedStateFromError: There are no Hook equivalents for these methods yet, but they will be added soon.
	- Should I use one or many state variables?
		- If you're coming from classes, you might be tempted to always call useState() once and put all state into a single object
		- However, instead we recommend to split state into multiple state variables based on which values tend to change together.
		- Separating independent state variables also has another benefit. It makes it easy to later extract some related logic into a custom Hook
		-  If the state logic becomes complex, we recommend managing it with a `useReducer` or a custom Hook.
	- How to get the previous props or state?
		- Currently, you can do it manually with a ref: 
		-  you can extract it into a custom Hook
	- Can I make a ref to a function component?
		-  you may expose some imperative methods to a parent component with the 	`useImperativeMethods` Hook.

- Performance Optimizations
	- How do I implement shouldComponentUpdate?
		- You can wrap a function component with React.memo to shallowly compare its props
		- It's not a Hook because it doesn't compose like Hooks do. React.memo is equivalent to PureComponent, but it only compares props.
	- How to memoize calculations?
		- `useMemo` Hook lets you cache calculations between multiple renders by "remembering" the previous computation
	- Are Hooks slow because of creating functions in render?
		- Hooks avoid a lot of the overhead that classes require, like the cost of creating class instances and binding event handlers in the constructor.
		- Idiomatic code using Hooks doesn't need the deep component tree nesting that is prevalent in codebases that use higher-order components, render props, and context. 
		    With smaller component trees, React has less work to do.
	- How to avoid passing callbacks down?
		- an alternative we recommend is to pass down a `dispatch` function from `useReducer` via `useContext`
		- it is preferable to avoid passing callbacks deep down
	
- Under the Hood
	- How does React associate Hook calls with components?
		- There is an internal list of "memory cells" associated with each component. 
		- They're just JavaScript objects where we can put some data. 
		- When you call a Hook like useState(), it reads the current cell (or initializes it during the first render), and then moves the pointer to the next one. 
		- This is how multiple useState() calls each get independent local state.

### 6. design

#### How to Contribute

- https://reactjs.org/docs/how-to-contribute.html   

- Before submitting a pull request, please make sure the following is done:
	- Fork the repository and create your branch from master.
	- Run yarn in the repository root.
	- If you've fixed a bug or added code that should be tested, add tests!
	- Ensure the test suite passes (yarn test). 
	- yarn flow runs the Flow typechecks.
	- yarn build creates a build folder with all the packages.
	- yarn build react/index,react-dom/index --type=UMD creates UMD builds of just React and ReactDOM.

#### Codebase Overview

- React has almost no external dependencies. However, there are a few relatively rare exceptions, such as fbjs.
- After cloning the React repository, you will see a few top-level folders in it
	- `packages` contains metadata (such as package.json) and the source code (src subdirectory) for all packages in the React repository. 
	  If your change is related to the code, the src subdirectory of each package is where you'll spend most of your time.
	- `fixtures` contains a few small React test applications for contributors.
	- `build` is the build output of React. It is not in the repository but it will appear in your React clone after you build it for the first time.
- We don't have a top-level directory for unit tests. Instead, we put them into a directory called __tests__ relative to the files that they test.
- We recently started introducing Flow checks to the codebase. Files marked with the @flow annotation in the license header comment are being typechecked.
- React uses dynamic injection in some modules. 
	- The main reason it exists is because React originally only supported DOM as a target. 
	- React Native started as a React fork. We had to add dynamic injection to let React Native override some behaviors.
	- In the future, we intend to get rid of the dynamic injection mechanism and wire up all the pieces statically during the build.
- React is a monorepo. Its repository contains multiple separate packages
	-  React core is located in `packages/react` in the source tree. 
		-  includes all the top-level React APIs
		- React.createElement()
		- React.Component
		- React.Children
		- React core only includes the APIs necessary to define components. It does not include the reconciliation algorithm or any platform-specific code.
		- It is used both by React DOM and React Native components.
	- Renderers manage how a React tree turns into the underlying platform calls.
		- React DOM Renderer renders React components to the DOM. 
		- React Native Renderer renders React components to native views. It is used internally by React Native.
		- React Test Renderer renders React components to JSON trees.
	-  different renderers share some code between them. We call this part of React a “reconciler”.
		- Reconcilers are not packaged separately because they currently have no public API. 
		- Instead, they are exclusively used by renderers such as React DOM and React Native.
		- The “stack” reconciler is the implementation powering React 15 and earlier. We have since stopped using it
		- The “fiber” reconciler is a new effort aiming to resolve the problems inherent in the stack reconciler and fix a few long-standing issues. It has been the default reconciler since React 16.
			- Ability to split interruptible work in chunks.
			- Ability to prioritize, rebase and reuse work in progress.
			- Ability to yield back and forth between parents and children to support layout in React.
			- Ability to return multiple elements from render().
			- Better support for error boundaries.
			- While it has shipped with React 16, the async features are not enabled by default yet.
			- Its source code is located in `packages/react-reconciler`
	- `packages/events`
		- React 实现了一个合成的事件系统，它是渲染器不可知的，在React DOM 和React Native 中工作

#### Implementation Notes for  Stack Reconciler

-  located at `src/renderers/shared/stack/reconciler`
- Mounting as a Recursive Process
	- React elements are plain objects representing the component type (e.g. App) and the props.
	- User-defined components (e.g. App) can be classes or functions but they all “render to” elements.
	- Mounting is a recursive process that creates a DOM or Native tree given the top-level React element (e.g. <App />).
- Mounting Host Elements
	- In addition to user-defined (“composite”) components, React elements may also represent platform-specific (“host”) components. 
	- If element's type property is a string, we are dealing with a host element:
	- When the reconciler encounters a host element, it lets the renderer take care of mounting it. For example, React DOM would create a DOM node.
- Introducing Internal Instances
	- The key feature of React is that you can re-render everything, and it won't recreate the DOM or reset the state:
	- Instead of separate mountHost and mountComposite functions, we will create two classes: DOMComponent and CompositeComponent.
	- The composite internal instances need to store:
		- The current element.
		- The public instance if element type is a class.
		- The single rendered internal instance. It can be either a DOMComponent or a CompositeComponent.
	- The host internal instances need to store:
		- The current element.
		- The DOM node.
		- All the child internal instances. Each of them can be either a DOMComponent or a CompositeComponent.
- Unmounting
	- unmounting DOM components also removes the event listeners and clears some caches
- Updating
	- The goal of the reconciler is to reuse existing instances where possible to preserve the DOM and the state
	- When a composite component receives a new element, we run the componentWillUpdate() 
	- Host component implementations, such as DOMComponent, update differently. When they receive an element, they need to update the underlying platform-specific view. 
		- In case of React DOM, this means updating the DOM attributes
- Stack reconciler has inherent limitations such as being synchronous and unable to interrupt the work or split it in chunks. 
- https://reactjs.org/docs/implementation-notes.html
	- more details

#### Design Principles

- This document assumes a strong understanding of React. It describes the design principles of React itself, not React components or applications.
- The key feature of React is composition of components. 
	- Components written by different people should work well together. 
- Common Abstraction
	- If we notice that many components implement a certain feature in incompatible or inefficient ways, we might prefer to bake it into React. 
	-  raising the abstraction level benefits the whole ecosystem. State, lifecycle methods, cross-browser event normalization are good examples of this.
- Escape Hatches
	- If we can't figure out a perfect API for something that we found necessary in many apps, 
	   we will provide a temporary subpar working API as long as it is possible to get rid of it later and it leaves the door open for future improvements.
- Stability
	- We value API stability. At Facebook, we have more than 50 thousand components using React. 
	- When we add a deprecation warning, we keep it for the rest of the current major version, and change the behavior in the next major version.
- We place high value in interoperability with existing systems and gradual adoption.
	- This is why React provides escape hatches to work with mutable models, and tries to work well together with other UI libraries. 
- Scheduling
	- It is a key goal for React that the amount of the user code that executes before yielding back into React is minimal. 
	- This ensures that React retains the capability to schedule and split work in chunks according to what it knows about the UI.
- Developer Experience
- Debugging
- Configuration
	-  global configuration doesn't work well with composition. Since composition is central to React, we don't provide global configuration in code.
	- We do, however, provide some global configuration on the build level.
- Beyond the DOM
	- Being renderer-agnostic is an important design constraint of React.
	- React Native
- Implementation
	- We try to provide elegant APIs where possible. 
	- When we evaluate new code, we are looking for an implementation that is correct, performant and affords a good developer experience. Elegance is secondary.
- Optimized for Tooling
	- make the points of interaction with the library highly visible.
	- We value distinct verbose names, and especially for the features that should be used sparingly.
	- optimized for search
- Dogfooding
	- Dogfooding it means that our vision stays sharp and we have a focused direction going forward.

### 7. faq

#### AJAX and APIs

- how to make an ajax call
	- jQuery `$.ajax()`
	- window.fetch()
	- axios
- where to make an ajax call
	- componentDidMount()

#### Babel, JSX, and Build Steps

- react without es6
- react without jsx

#### Passing Functions to Components

- How to pass an event handler (like onClick) to a component
	- Pass event handlers and other functions as props to child components:
	- If you need to have access to the parent component in the handler, you also need to bind the function to the component instance
- How do I bind a function to a component instance
	- There are several ways to make sure functions have access to component attributes like `this.props` and `this.state`
	- Bind in Constructor (ES2015)
	```
	class Foo extends Component {
	  constructor(props) {
		super(props);
		this.handleClick = this.handleClick.bind(this);
	  }
	  handleClick() {
		console.log('Click happened');
	  }
	  render() {
		return <button onClick={this.handleClick}>Click Me</button>;
	  }
	}
	```
	- Class Properties (Stage 3 Proposal)  推荐使用这种写法，不用在render中绑定
	```
	class Foo extends Component {
	  // Note: this syntax is experimental and not standardized yet.
	  handleClick = () => {
		console.log('Click happened');
	  }
	  render() {
		return <button onClick={this.handleClick}>Click Me</button>;
	  }
	}
	```
	- Bind in Render
		- Using Function.prototype.bind in render creates a new function each time the component renders, which may have performance implications
	```
	class Foo extends Component {
	  handleClick() {
		console.log('Click happened');
	  }
	  render() {
		return <button onClick={this.handleClick.bind(this)}>Click Me</button>;
	  }
	}
	```
	- Arrow Function in Render
		- Using an arrow function in render creates a new function each time the component renders, which may have performance implications
	```
	class Foo extends Component {
	  handleClick() {
		console.log('Click happened');
	  }
	  render() {
		return <button onClick={() => this.handleClick()}>Click Me</button>;
	  }
	}
	```
- How to pass a parameter to an event handler or callback
	- `<button onClick={() => this.handleClick(id)} />`
	- `<button onClick={this.handleClick.bind(this, id)} />`
- How to prevent a function from being called too quickly or too many times in a row
	- If you have an event handler such as onClick or onScroll and want to prevent the callback from being fired too quickly, then you can limit the rate
	- throttling: sample changes based on a time based frequency (eg _.throttle)
	- debouncing: publish changes after a period of inactivity (eg _.debounce)
	- requestAnimationFrame throttling: sample changes based on requestAnimationFrame (eg raf-schd)
	- _.debounce, _.throttle and raf-schd provide a cancel method to cancel delayed callbacks. 
	  You should either call this method from componentWillUnmount or check to ensure that the component is still mounted within the delayed function. 
- Throttling prevents a function from being called more than once in a given window of time. 
- Debouncing ensures that a function will not be executed until after a certain amount of time has passed since it was last called. T
- requestAnimationFrame is a way of queuing a function to be executed in the browser at the optimal time for rendering performance.

#### Component State

- props vs state
- Why is setState giving me the wrong value?  
	- In React, both this.props and this.state represent the rendered values, i.e. whats currently on the screen.
	- Calls to setState are asynchronous
	- if you need to compute values based on the current state , Pass an updater function instead of an object  to setState()
	- pass an object   
	```
	incrementCount() {
	  // Note: this will not work as intended.
	  this.setState({count: this.state.count + 1});
	}
	handleSomething() {
	  // Let's say this.state.count starts at 0.
	  this.incrementCount();
	  this.incrementCount();
	  this.incrementCount();
	  // When React re-renders the component, this.state.count will be 1, but you expected 3.
	
	  // This is because incrementCount() function above reads from this.state.count,
	  // but React doesn't update this.state.count until the component is re-rendered.
	  // So incrementCount() ends up reading this.state.count as 0 every time, and sets it to 1.
	}
	```
	- Passing an update function allows you to access the current state value inside the updater. 
	  Since setState calls are batched, this lets you chain updates and ensure they build on top of each other instead of conflicting  
	```
	 incrementCount() {
	  this.setState((state) => {
		// Important: read state instead of this.state when updating.
		return {count: state.count + 1}
	  });
	}
	handleSomething() {
	  // Let's say this.state.count starts at 0.
	  this.incrementCount();
	  this.incrementCount();
	  this.incrementCount();
	
	  // If you read this.state.count now, it would still be 0.
	  // But when React re-renders the component, it will be 3.
	}
	```       
- Currently, setState is asynchronous inside event handlers.
	- This ensures, for example, that if both Parent and Child call setState during a click event, Child isn't re-rendered twice.  
	- In the future versions, React will batch updates by default in more cases.
	-  React intentionally “waits” until all components call setState() in their event handlers before starting to re-render. This boosts performance by avoiding unnecessary re-renders.
	

#### Styling and CSS

- className
- CSS classes are generally better for performance than inline styles.
- “CSS-in-JS” refers to a pattern where CSS is composed using JavaScript instead of defined in external files.
- React can be used to power animations. See React Transition Group and React Motion

#### File Structure

- Grouping by features or routes
- Grouping by file type
- Avoid too much nesting
- don't spend more than 5 minutes on choosing a file structure.

#### Versioning Policy

- React follows semantic versioning (semver) principles with a version number x.y.z:
	- When releasing breaking changes, we make a major release by changing the x number (ex: 15.6.2 to 16.0.0).
	- When releasing new features, we make a minor release by changing the y number (ex: 15.6.2 to 15.7.0).
	- When releasing bug fixes, we make a patch release by changing the z number (ex: 15.6.2 to 15.6.3).

#### Virtual DOM and Internals

- The virtual DOM (VDOM) is a programming concept
	- representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called reconciliation.
	- “virtual DOM” is more of a pattern than a specific technology
- In React world, the term “virtual DOM” is usually associated with React elements since they are the objects representing the user interface. 
	- React, however, also uses internal objects called “fibers” to hold additional information about the component tree. 
	- They may also be considered a part of “virtual DOM” implementation in React.
- The Shadow DOM is a browser technology designed primarily for scoping variables and CSS in web components.
	- Shadow DOM它允许在document渲染时插入一棵DOM元素子树，但这棵子树不在主DOM树中。
	- 例如video标签下面会有 `# shadow root`
- The Virtual DOM is a concept implemented by libraries in JavaScript on top of browser APIs.

##  API Reference  


## changelog

https://github.com/facebook/react/blob/master/CHANGELOG.md         
https://reactjs.org/versions      

- 16.7.0-20181219
	- deprecated: componentWillMount()，componentWillUpdate()，componentWillReceiveProps()
		- 关于提早发送数据请求，官方鼓励将数据请求部分的代码放在组件的constructor()中，将现有componentWillMount中的代码迁移至componentDidMount即可
		- new: getSnapshotBeforeUpdate()与componentDidUpdate()一起使用可以取代componentWillUpdate
		- new: getDerivedStateFromProps()与componentDidUpdate()一起使用可以取代componentWillReceiveProps    
	- Clear fields on unmount to avoid memory leaks.  
	- Post to MessageChannel instead of window.   
- 16.6.0-20181023
	- Add React.memo() as an alternative to PureComponent for functions.：PureComponent 要依靠 class 才能使用，而React.memo()可以和functional component一起使用
	- Add React.lazy() for code splitting components：使用 React Suspense 进行代码拆分和懒加载
	- React.StrictMode now warns about legacy context API, findDOMNode.
	- Rename unstable_Placeholder to Suspense, and delayMs to maxDuration.
	- Add contextType as a more ergonomic way to subscribe to context from a class.
- 16.5.0-20180905
	- Add a warning if React.forwardRef render function doesn't take exactly two arguments 
	- Add support for React DevTools Profiler 
	- Minimally support iframes (nested browsing contexts) in selection event handling
- 16.4.0-20180523
	- Add a new experimental React.unstable_Profiler component for measuring performance.
	- Add support for the Pointer Events specification. 
	- Add the ability to specify propTypes on a context provider component.
	- You can now assign propTypes to components returned by React.ForwardRef.
- 16.3.0-20180329
    - new Context API：父组件向嵌套内层子组件传递props
    - React.createRef()：在编码中提前声明需要获取 Ref，as an ergonomic alternative to callback refs.
    - React.forwardRef()：let components forward their refs to a child. 用于高阶组件传递ref，使包裹的无状态组件可以接收ref作为第二个参数，并且可以传递下去
    - Add a new getDerivedStateFromProps() lifecycle
    - Add a new getSnapshotBeforeUpdate() lifecycle.
    - Add a new <React.StrictMode> wrapper to help prepare apps for async rendering. 
    - StrictMode：用于在开发环境下提醒组件内使用不推荐写法和即将废弃的API，不会被渲染成真实DOM
    - Add support for onLoad and onError events on the <link> tag. 
    - Prevent an infinite loop when attempting to render portals with SSR.
    - Improve user timing API messages for profiling.
- 16.2.0-20171128
	- Add Fragment as named export to React: Fragment可以让聚合一个子元素列表，并且不在DOM中增加额外节点。
	- Support experimental Call/Return types in React.Children utilities.
- 16.1.0-20171109
	- Add support for portals in React.Children utilities.
	- Move link in the warning message to avoid redirect.
	- Include the autoFocus attribute into SSR markup.
	- Support string values for the capture attribute.
- 16.0.0-20170926
	- React Fiber：使得大量的计算可以被拆解分片、异步化
	- Components can now return arrays and strings from render.
	- Improved error handling with introduction of "error boundaries"：componentDidCatch()捕获render()时的错误
	- ReactDOM.createPortal()： support for declaratively rendering a subtree into another DOM node. 解决modal不需要渲染到parent node的问题
	- Streaming mode for server side rendering is enabled with ReactDOMServer.renderToNodeStream()
	- React DOM now allows passing non-standard attributes.
	- ReactDOM.render() now return null if called from inside a lifecycle method.
	- Calling setState with null no longer triggers an update.
	- Calling setState directly in render always causes an update. Regardless, you should not be calling setState from render.
	- setState callback (second argument) now fires immediately after componentDidMount / componentDidUpdate instead of after all components have rendered.
	- When replacing <A /> with <B />, B.componentWillMount now always happens before A.componentWillUnmount.
	- Shallow renderer no longer calls componentDidUpdate() because DOM refs are not available. 
	- The server renderer has been completely rewritten
	- When "unknown" props are passed to DOM components, for valid values, React will now render them in the DOM. 
	- Errors in the render and lifecycle methods now unmount the component tree by default. To prevent this, add error boundaries.
	- React.createClass, React.PropTypes, React.DOM have been removed from the core package. 
- 15.6.2-20170925
	- Switch from BSD + Patents to MIT license
	- Prevent event handlers from receiving extra argument in development.
	- Add support for controlList attribute to DOM property whitelist 
- 15.6.0-20170613
	- Add support for CSS variables in style attribute
	- Add support for CSS Grid style properties.
- 15.5.0-20170407
	- Added react-dom/test-utils, which exports the React Test Utils.
- 15.4.0-20161116
	- Improved development performance by freezing children instead of copying.
	- The unstable batchedUpdates API now passes the wrapped function's return value through.
- 15.3.0-20160729
	- Add `React.PureComponent`  
	- Add xmlns, xmlnsXlink to supported SVG attributes. 
- 15.2.0-20160701
	- Stop validating props at mount time, only validate at element creation. 
	- Add warning for unknown properties on DOM elements. 
- 15.1.0-20160520
	- Add a new warning to communicate that props objects passed to createElement must be plain objects. 
	- Add additional information to the controlled input warning.
- 15.0.0-20160407
	- Initial render now uses document.createElement instead of generating HTML. 
	- No more extra <span>s. ReactDOM will now render plain text nodes interspersed with comment nodes that are used for demarcation.
	- Rendering null now uses comment nodes. Previously null would render to `<noscript>` elements. We now use comment nodes. 
	- Functional components can now return null.
	- All SVG tags are now fully supported.   
- 0.14.0-20151007
	- Split the main react package into two: react and react-dom
	- Stateless functional components：使用js函数直接定义react组件
	- Refs to DOM components as the DOM node itself.  Note that refs to custom (user-defined) components work exactly as before; only the built-in DOM components are affected by this change.
	- The props object is now frozen, so mutating props after creating a component element is no longer supported.
	- Plain objects are no longer supported as React children; arrays should be used instead.
	- setProps and replaceProps are now deprecated. 
	- Added React.Children.toArray
- 0.13.0-20150310
	- Calls to setState in life-cycle methods are now always batched and therefore asynchronous.
	- Support for using ES6 classes to build React components
	- Added new top-level API `React.findDOMNode(component)`  as a replacement for `component.getDOMNode()`
		- The findDOMNode method has moved from react module to the react-dom module.
	- Added a new top-level API React.cloneElement(el, props)
	- New ref style, allowing a callback to be used in place of  string
	- this.setState() can now take a function as the first argument for transactional state updates, such as this.setState((state, props) => ({count: state.count + 1}));
	- Support for iterators and immutable-js sequences as children
- 0.12.0-20141028
	- key and ref moved off props object, now accessible on the element directly
	- React is now BSD licensed with accompanying Patents grant
	- Spread operator ({...}) introduced to deprecate this.transferPropsTo
	- Added support for more HTML attributes: acceptCharset, classID, manifest
- 0.11.0-20140717
	- Support rendering to null
	- React.Children.count has been added as a helper for counting the number of children
- 0.10.0-20140321
	- Made it possible to server render without React-related markup 
- 0.9.0-20140220
	- Added support for SVG tags defs, linearGradient, polygon
	- On input, select, and textarea elements, .getValue() is no longer supported; use .getDOMNode().value instead
- 0.8.0-20131219
	- Support for more dom attributes
- 0.5.0-20131016
	- Support for Selection events., Composition events
	- Support for additional DOM properties, SVG properties
- 0.4.0-20130717  
	- Support for more DOM elements and attributes (e.g., `<canvas>`)
	- Support for the `key` prop
- 0.3.0-20130529
	- initial public release
