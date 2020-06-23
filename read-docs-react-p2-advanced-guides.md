---
tags: [docs, react]
title: read-docs-react-p2-advanced-guides
created: '2020-06-23T06:10:10.882Z'
modified: '2020-06-23T13:52:57.802Z'
---

# read-docs-react-p2-advanced-guides

## JSX In Depth
- 
- 
- 
-
- 
- 
- 
- 
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
- props.children可以像其它属性一样传递任何数据，而不仅仅是React元素，如果你使用自定义组件，则可以将调用props.children来获得传递的子代
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
	
## React Without ES6

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
	
## React Without JSX

- 每一个 JSX 元素都是调用 `React.createElement(component, props, ...children)` 的语法糖

## Context
- 
- 
- 
- 
-
- 
- 
- 
- 
- Context提供了一种通过组件树传递数据的方法，无需在每个级别手动传递props
- 在典型的React应用程序中，数据通过props自上而下（父到子）传递，但对于应用程序中许多组件所需的某些类型的 props（例如语言偏好,UI主题），这可能很繁琐
- Context旨在共享一个组件树内可被视为全局的数据，常见的使用场景
    - 当前经过身份验证的用户
    - 主题设置
    - 语言设置
    - 查询缓存
- 不要仅仅为了避免在几个层级下的组件传递props而使用 context
    - 它适用于在**多个层级的多个组件**需要访问相同数据的情景
    - 请谨慎使用context，因为它使组件重用更加困难
    - 如果只想避免在多个级别上传递一些props，那么组件组合component composition通常比Context更简单
- API	
    - React.createContext(defaultValue)
        - 创建一个Context对象，当React渲染订阅这个Context对象的组件时，它将从组件树中匹配**最近的Provider**中读取当前context的值
        - defaultValue只在provider不存在时使用
    - Context.Provider
        - 每个Context对象都附带一个Provider组件，允许Consumer组件订阅context的改变
        - 接受一个value属性用来传递给Consumer
        - 每当Provider的value属性发生变化时，所有作为Provider后代的Consumer组件都将重新渲染
        - 从Provider到其后代使用者的传播不受shouldComponentUpdate()的约束
    - Context.Consumer
        - 用来定义一个订阅context变化的组件
        - 需要接收一个函数作为子节点，该函数接收当前context值并返回一个React节点
    - Class.contextType	
        - 可以为类上的contextType属性分配由React.createContext()创建的Context对象，这样this.context就能获取到该Context类型最近的当前值
        - 使用这个API只能订阅一个context
        - 语法上可以使用static类属性代替
- 可以在context中向下传递一个函数，以允许Consumer更新context
- 为了保持context的快速重新渲染，React需要使每个Consumer成为树中的一个独立节点
- Provider和Consumer都支持嵌套
- 因为context使用reference相等来确定何时重新渲染，每当Provider重新渲染时，Consumer子组件也会渲染，解决方法是将Provider的value属性值放在state中初始化

## Context API (Legacy)

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


## Refs and the DOM
- 
- 
- 
- 
-
- 
- 
- 
- 
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
 <input type="text" ref={el=>this.myRef=el}  />
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

## Forwarding Refs
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


##  Uncontrolled Components

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

## Fragments
- 
- 
- 
- 
-
- 
- 
- 
- 
- Fragments 可以让你聚合一个子元素列表，并且不在DOM中增加额外节点
- `<></>`是`<React.Fragment>`的语法糖，只是它不支持 键(keys) 或 属性(attributes)
- key is the only attribute that can be passed to Fragment. In the future, we may add support for additional attributes, such as event handlers.

## Higher-Order Components

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

## Render Props

- `render prop` refers to a technique for sharing code between React components using a prop whose value is a function.
	  - Libraries that use render props include React Router and Downshift
-  component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic.   
- 具有render prop 组件接受一个函数，该函数返回一个React元素并调用它，而不是实现自己的渲染逻辑
```
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```
- Use Render Props for Cross-Cutting Concerns
- you can implement most higher-order components (HOC) using a regular component with a render prop. 
- Using Props  name Other Than  *render*     
    - you don’t have to use a prop named render to use this pattern
    - any prop that is a function that a component uses to know what to render is technically a "render prop"   
```
<Mouse children={mouse => (
  <p>The mouse position is {mouse.x}, {mouse.y}</p>
)}/>
```
等价于   
```
<Mouse>
  {mouse => (
    <p>The mouse position is {mouse.x}, {mouse.y}</p>
  )}
</Mouse>
```   
- render prop会抵消使用`React.PureComponent`带来的优势
    -  each time `<MouseTracker>` renders, it generates a new function as the value of the `<Mouse render>` prop
  	- because the shallow prop comparison will always return false for new props, and each render in this case will generate a new value for the render prop.
    - define the prop as an instance method可以避免
    - 也可以直接继承React.Component



## Portals

- Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.
	- `ReactDOM.createPortal(child, container)`
	- child is any renderable React child, such as an element, string, or fragment
	- container is a DOM element
- Normally, when you return an element from a component's render method, it's mounted into the DOM as a child of the nearest parent node
- A typical use case for portals is when a parent component has an overflow: hidden or z-index style, but you need the child to visually break outof its container. 
	- For example, dialogs, hovercards, and tooltips.
- Even though a portal can be anywhere in the DOM tree, it behaves like a normal React child in every other way. Features like context work exactly the same
- An event fired from inside a portal will propagate to ancestors in the containing React tree, even if those elements are not ancestors in the DOM tree.

## Optimizing Performance

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
	
## Profiler
- 
- 
- 
- 
-
- 
- 
- 
- 


## Reconciliation 协调
- https://reactjs.org/docs/reconciliation.html  
- 
- 
- 
-
- 
- 
- 
- 
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



## Code-Splitting
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


## Static Type Checking

- 对于复杂的代码库，建议使用 Flow 或者 TypeScript 来替代 PropTypes
- flow
- typescript
- reason： 是一门基于 OCaml 的语言，既可以通过 BuckleScript 被同编译为 JavaScript，也支持直接编译为原生的二进制汇编

## Strict Mode

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

## Error Boundaries
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

## Integrating with Other Libraries

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


## Accessibility
- 
- 
- 
- 
-
- 
- 
- 
- 
- Web accessibility (also referred to as `a11y`) is the design and creation of websites that can be used by everyone.  
- WCAG: The Web Content Accessibility Guidelines provides guidelines for creating accessible web sites.
- WAI-ARIA: The Web Accessibility Initiative - Accessible Rich Internet Applications document contains techniques for building fully accessible JavaScript widgets.  



## Web Components

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
	
