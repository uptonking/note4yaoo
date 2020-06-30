---
favorited: true
tags: [docs, react]
title: docs-react-p2-advanced-guides
created: '2020-06-23T06:10:10.882Z'
modified: '2020-06-30T05:13:45.128Z'
---

# docs-react-p2-advanced-guides

## JSX In Depth
- JSX just provides syntactic sugar for the `React.createElement(componentType, props, ...children)` function
  - Create and return a new React element of the given type. 
  - The type argument can be either a tag name string (such as 'div' or 'span'), a React component type (a class or a function), or a React fragment type
- Capitalized types indicate that the JSX tag is referring to a React component. 
  - These tags get compiled into a direct reference to the named variable
  - so if you use the JSX `<Foo />` expression, `Foo` must be in scope.
  - Since JSX compiles into calls to  `React.createElement`, the React library must also always be in scope from your JSX code.
- When an element type starts with a lowercase letter, it refers to a built-in component like `<div>` or `<span>` and results in a string 'div' or 'span' passed to React.createElement. 
- Types that start with a capital letter like `<Foo />` compile to `React.createElement(Foo)` and correspond to a component defined or imported in your JavaScript file.
- We recommend naming components with a capital letter. 
  - If you do have a component that starts with a lowercase letter, assign it to a capitalized variable before using it in JSX.
- If you do want to use a general expression to indicate the type of the element, just assign it to a capitalized variable first. 
  - This often comes up when you want to render a different component based on a prop    
  ```
    const components = {
      photo: PhotoStory,
      video: VideoStory
    };
    
   function Story(props) {
      // Correct! JSX type can be a capitalized variable.
      const SpecificStory = components[props.storyType];
      return <SpecificStory story={props.story} />;
    }
  ```
- **Props in JSX**
- You can pass any JavaScript expression as a prop, by surrounding it with `{}`
- You can pass a string literal as a prop.
  - When you pass a string literal, its value is HTML-unescaped
- If you pass no value for a prop, it defaults to `true`
  - we don’t recommend not passing a value for a prop, because it can be confused with the ES6 object shorthand
- If you already have props as an object, and you want to pass it in JSX, you can use `...` as a “spread” operator to pass the whole props object
  - Spread attributes can be useful 
  - but they also make it easy to pass unnecessary props to components that don’t care about them or to pass invalid HTML attributes to the DOM. 
  - We recommend using this syntax sparingly.
- **Children in JSX**
- In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a special prop: `props.children`
- You can put a string between the opening and closing tags and props.
  - children will just be that string. 
  - HTML is unescaped, so you can generally write JSX just like you would write HTML in this way
  - JSX removes whitespace at the beginning, ending of a line, blank lines
- You can provide more JSX elements as the children
  - You can mix together different types of children, so you can use string literals together with JSX children. 
  - A React component can also return an array of elements  
- You can pass any JavaScript expression as children, by enclosing it within `{}`
  - JavaScript expressions can be mixed with other types of children
- If you have a custom component, you could have it take a *callback function* as `props.children`
  - Children passed to a custom component can be anything, as long as that component transforms them into something React can understand before rendering
- `false`, `null`, `undefined`, and `true` are valid children. 
  - They simply don’t render. 
  - These JSX expressions will all render to the same thing
  ```
    <div />
    <div></div>
    <div>{false}</div>
    <div>{null}</div>
    <div>{undefined}</div>
    <div>{true}</div>
  ```
  - One caveat is that some “falsy” values, such as the 0 number, are still rendered by React.
  - make sure that the expression before `&&` is always boolean
- Conversely, if you want a value like false, true, null, or undefined to appear in the output, you have to convert it to a string first
- 可以使用JSX的点表示法来引用React组件，可以方便地从一个模块中导出许多React组件
- jsx的属性值
	- 用`{ }`包含的js表达式
	- 字符串
	- 如果你没有给属性传值，它默认为true
	``` 
	<MyTextBox autocomplete /> 等价于 <MyTextBox autocomplete={true} />
	```
	- 现有对象使用使用扩展操作符来将整个对象作为属性传递给子组件 `return <Greeting {...props} />;`
- This JSX only renders a `<Header />` if showHeader is true:
```
<div>
  {showHeader && <Header />}
  <Content />
</div>
```
	
## React Without ES6
- 声明类
	- `class Greeting extends React.Component{}`
	- 使用`var createReactClass = require('create-react-class');`
	```
	var Greeting = createReactClass({
	  render: function() {
		return <h1>Hello, {this.props.name}</h1>;
	  }
	});
	```
- 声明defaultProps
	- `Greeting.defaultProps = {}`
	- `createReactClass({ getDefaultProps: function() {} `
- 设置state初始值
	- 在class中 `constructor(props){ this.state={}}`
	- `createReactClass({ getInitialState: function() {}`
- 自动绑定
	- es6的class中方法没有自动绑定this，要在constructor()中`this.handleClick = this.handleClick.bind(this);`
	- With `createReactClass()`, this is not necessary because it binds all methods
- mixins
	- es6不支持混入，推荐使用高阶组件
	- createReactClass()作为一个属性`mixins: [SetIntervalMixin]`
	
## React Without JSX
- Each JSX element is just syntactic sugar for calling `React.createElement(component, props, ...children)`. 
  - So, anything you can do with JSX can also be done with just plain JavaScript.
- The component can either be provided as a string, as a subclass of React.Component, or a plain function.
- If you get tired of typing `React.createElement` so much, one common pattern is to assign a shorthand
```
const e = React.createElement;
ReactDOM.render(
  e('div', null, 'Hello World'),
  document.getElementById('root')
);
```

## Fragments
- A common pattern in React is for a component to *return multiple elements*. 
  - A common pattern is for a component to return a list of children. 
- **Fragments let you group a list of children without adding extra nodes to the DOM**.
- Fragments declared with the explicit `<React.Fragment>` syntax may have keys. 
- `key` is the only attribute that can be passed to `Fragment`. 
- In the future, we may add support for additional attributes, such as event handlers.
- You can use `<></>` the same way you’d use any other element except that it doesn’t support keys or attributes.

## Context
- Context provides a way to pass data through the component tree without having to pass props down manually at every level.
- In a typical React application, data is passed top-down (parent to child) via props
  - but this can be cumbersome for certain types of props (e.g. locale preference, UI theme) that are required by many components within an application. 
  - Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree.
- Context is designed to share data that can be considered *global* for a tree of React components, such as the current authenticated user, locale, theme, or data cache.
- Using context, we can avoid passing props through intermediate elements
- Context is primarily used when some data needs to be accessible by many components **at different nesting levels**. 
  - Apply it sparingly because it makes component reuse more difficult.
- If you *only want to avoid passing some props through many levels*, component composition is often a simpler solution than context
  - It might feel redundant to pass down the user and avatarSize props through many levels if in the end only the Avatar component really needs it. 
  - It’s also annoying that whenever the Avatar component needs more props from the top, you have to add them at all the intermediate levels too.
  - One way to solve this issue without context is to *pass down the Avatar component itself* so that the intermediate components don’t need to know about the user or avatarSize props
  - With this change, only the top-most Page component needs to know about the Link and Avatar components’ use of user and avatarSize
- This inversion of control can make your code cleaner in many cases by reducing the amount of props you need to pass through your application and giving more control to the root components. 
  - However, this isn’t the right choice in every case: 
    - moving more complexity higher in the tree makes those higher-level components more complicated and forces the lower-level components to be more flexible than you may want
- This pattern is sufficient for many cases when you need to decouple a child from its immediate parents. 
  - You can take it even further with render props if the child needs to communicate with the parent before rendering.
- However, sometimes the same data needs to be accessible by many components in the tree, and *at different nesting levels*. 
  - Context lets you “broadcast” such data, and changes to it, to all components below
- `const MyContext = React.createContext(defaultValue);`  
  - Creates a Context object. 
  - When React renders a component that subscribes to this Context object, it will read the current context value from the closest matching `Provider` above it in the tree.
  - The `defaultValue` argument is only used when a component does not have a matching Provider above it in the tree. 
  - This can be helpful for testing components in isolation without wrapping them. 
  - Note: passing `undefined` as a Provider value does not cause consuming components to use `defaultValue`.
- `<MyContext.Provider value={/* some value */}>`  
  - Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.
  - Accepts a `value` prop to be passed to consuming components that are descendants of this Provider. 
  - One Provider can be connected to many consumers. 
  - Providers can be nested to override values deeper within the tree.
  - All consumers that are descendants of a Provider will re-render *whenever the Provider’s `value` prop changes*. 
  - The propagation from Provider to its descendant consumers (including `.contextType` and `useContext`) is not subject to the `shouldComponentUpdate` method, so the consumer is updated even when an ancestor component skips an update.
  - Changes are determined by comparing the new and old values using the same algorithm as `Object.is`.
- `<MyContext.Consumer> {value => /* use context value */} </MyContext.Consumer>`
  - A React component that subscribes to context changes
  - Requires a function as a child. 
    - The function receives the current context value and returns a React node. 
    - The `value` argument passed to the function will be equal to the `value` prop of the closest Provider for this context above in the tree. 
    - If there is no Provider for this context above, the `value` argument will be equal to the `defaultValue` that was passed to `createContext()`
- `Class.contextType`
  - The `contextType` property on a class can be assigned a Context object created by `React.createContext()`. 
  - This lets you consume the nearest current value of that Context type using `this.context`. 
  - You can reference this in any of the lifecycle methods including the render function.
  - You can only subscribe to a single context using this API- 
- `Context.displayName`
  -  React DevTools uses this string to determine what to display for the context.
- It is often necessary to update the context from a component that is nested somewhere deeply in the component tree. 
  - you can pass a function down through the context to allow consumers to update the context
  ```
  export const ThemeContext = React.createContext({
    theme: themes.dark,
    toggleTheme: () => {},
  });
  ```
- To keep context re-rendering fast, React needs to make each context consumer a separate node in the tree.
- If *two or more context values are often used together*, you might want to consider creating your own render prop component that provides both.
- Because context uses reference identity to determine when to re-render, there are some gotchas that could trigger unintentional renders in consumers when a provider’s parent re-renders
  - For example, the code below will re-render all consumers every time the Provider re-renders because a new object is always created for `value`  
  ```
     <MyContext.Provider value={{something: 'something'}}>
        <Toolbar />
     </MyContext.Provider>
  ```
  - To get around this, lift the value into the parent’s state
  ```
  constructor(props) {
    super(props);
    this.state = {
      value: {something: 'something'},
    };
  }

  <Provider value={this.state.value}>
  ```
- Context旨在共享一个组件树内可被视为全局的数据，常见的使用场景
  - 当前经过身份验证的用户
  - 主题设置
  - 语言设置
  - 查询缓存
使用static类属性代替
- 可以在context中向下传递一个函数，以允许Consumer更新context
- 因为context使用reference相等来确定何时重新渲染，每当Provider重新渲染时，Consumer子组件也会渲染
  - 解决方法是将Provider的value属性值放在state中初始化

## Context API (Legacy)
```
const PropTypes = require('prop-types');
class Button extends React.Component {
  render() {
    return (
      // 从context中取值
      <button style={{background: this.context.color}}>      
        {this.props.children}
      </button>
    );
  }
}
Button.contextTypes = {
  color: PropTypes.string
};
```

```
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
  //声明并初始化context中的值
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
- Refs provide a way to access DOM nodes or React elements created in the render method.
- In the typical React dataflow, props are the only way that parent components interact with their children.
- However, there are a few cases where you need to **imperatively modify a child outside of the typical dataflow**.
- There are a few good use cases for refs:
  - Managing focus, text selection, or media playback.
  - Triggering imperative animations.
  - Integrating with third-party DOM libraries.
- Avoid using refs for anything that can be done declaratively.
  - For example, instead of exposing open() and close() methods on a Dialog component, pass an `isOpen` prop to it.
- Refs are created using `React.createRef()` and attached to React elements via the `ref` attribute. 
```jsx
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
- Refs are commonly assigned to an instance property when a component is constructed， so they can be referenced throughout the component.
- When a ref is passed to an element in render, a reference to the node becomes accessible at the `current` attribute of the ref.
- The value of the ref differs depending on the type of the node:
  - When the ref attribute is used on an HTML element,
    - the ref created in the constructor with `React.createRef()` receives the underlying DOM element as its `current` property.
    - React will assign the `current` property with the DOM element when the component mounts, and assign it back to `null` when it unmounts. 
    - ref updates happen before componentDidMount or componentDidUpdate lifecycle methods.
  - When the ref attribute is used on a custom class component
    - the ref object receives the mounted instance of the component as its `current`.
  - You **may not use the ref attribute on function components** because they don’t have instances.
    - If you want to allow people to take a ref to your function component, you can use forwardRef (possibly in conjunction with useImperativeHandle)
    - or you can convert the component to a class.
    - You can, however, use the `ref` attribute inside a function component as long as you refer to a DOM element or a class component
- In rare cases, you might want to have access to a child’s DOM node from a parent component. 
  - This is generally not recommended because it breaks component encapsulation
  - but it can occasionally be useful for triggering focus or measuring the size or position of a child DOM node.
  - While you could add a ref to the child component, this is not an ideal solution, as you would only get a component instance rather than a DOM node. 
    - Additionally, this wouldn’t work with function components.
  - We recommend to use ref forwarding for these cases. 
    - **Ref forwarding lets components opt into exposing any child component’s ref as their own**. 
  - If you need more flexibility than provided by ref forwarding, you can use this alternative approach and explicitly pass a ref as a differently named prop.
    - https://gist.github.com/gaearon/1a018a023347fe1c2476073330cc5509
- When possible, we advise against exposing DOM nodes
  - but it can be a useful escape hatch. 
  - Note that this approach requires you to add some code to the child component. 
  - If you have absolutely no control over the child component implementation, your last option is to use `findDOMNode()`, but it is discouraged and deprecated in StrictMode.
- React also supports another way to set refs called **callback refs**, which gives more fine-grain control over when refs are set and unset.
- Instead of passing a ref attribute created by createRef(), you pass a function.
  - **The function receives the React component instance or HTML DOM element as its argument**, which can be stored and accessed elsewhere.
- You can pass callback refs between components like you can with object refs that were created with React.createRef().
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
```
- In the example above, Parent passes its ref callback as an `inputRef` prop to the CustomTextInput, and the CustomTextInput passes the same function as a special `ref` attribute to the `<input>`. 
- As a result, `this.inputElement` in Parent will be set to the DOM node corresponding to the `<input>` element in the CustomTextInput.
- If the `ref` callback is defined as an inline function, it will get called twice during updates, first with `null` and then again with the DOM element.
  - This is because a new instance of the function is created with each render
  - so React needs to clear the old ref and set up the new one. 
  - You can avoid this by defining the ref callback as a bound method on the class
  - but note that it shouldn’t matter in most cases.
- We *advise against* using string refs because string refs have some issues, are considered legacy, and are likely to be removed
  - It requires that React keeps track of currently rendering component (since it can't guess `this`). This makes React a bit slower.
  - It doesn't work as most people would expect with the "render callback" pattern (e.g. `<DataGrid renderRow={this.renderRow} />`) because the ref would get placed on DataGrid for the above reason.
  - It is not composable, i.e. if a library puts a ref on the passed child, the user can't put another ref on it. Callback refs are perfectly composable.
    - https://github.com/facebook/react/issues/8734

- 字符串类型的ref不推荐使用
	- 问题
		- 不支持静态类型分析，如flow
		- string ref的指向与当前组件，容易出错，且需要react跟踪当前执行的组件
		- 参考 https://stackoverflow.com/questions/37468913/why-ref-string-is-legacy
	- 例子
	```
	<input ref="input1" />
	const inputEl = this.refs.input1;
	```
- 不管ref设置值是回调函数还是字符串，都可以通过`ReactDOM.findDOMNode(ref)`来获取组件挂载后真正的dom节点
- 但是对于html元素使用ref的情况，ref本身引用的就是该元素的实际dom节点，无需使用ReactDOM.findDOMNode(ref)来获取，该方法常用于React组件上的ref
- 不建议在父组件中直接访问子组件的实例方法来完成某些逻辑，在大部分情况下请使用标准的react数据流的方式来代替则更为清晰；
- 不要在组件的render方法中访问ref引用，render方法只是返回一个虚拟dom，这时组件不一定挂载到dom中或者render返回的虚拟dom不一定会更新到dom中。

## Forwarding Refs
- Ref forwarding is a technique for automatically passing a ref through a component to one of its children
- Forwarding refs to DOM components
  - Consider a `FancyButton` component that renders the native `button` DOM element
  - React components hide their implementation details, including their rendered output. 
  - Other components using FancyButton usually will not need to obtain a ref to the inner button DOM element.
  - This is good because it prevents components from relying on each other’s DOM structure too much
  - Although such encapsulation is desirable for application-level components like FeedStory or Comment, it *can be inconvenient* for highly reusable “leaf” components like FancyButton or MyTextInput.
  - These components tend to be used throughout the application in a similar manner as a regular DOM button and input, and accessing their DOM nodes may be unavoidable for managing focus, selection, or animations.
- Ref forwarding is an opt-in feature that lets some components take a ref they receive, and pass it further down (in other words, “forward” it) to a child.  
```
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```
- In the example, FancyButton uses React.forwardRef to obtain the ref passed to it, and then forward it to the DOM button that it renders
  - This way, **components using FancyButton can get a ref to the underlying button DOM node** and access it if necessary—just like if they used a DOM button directly.
  - When the ref is attached, `ref.current` will point to the `<button>` DOM node.
- The second ref argument only exists when you define a component with React.forwardRef call. 
- Regular function or class components don’t receive the ref argument, and `ref` is not available in `props` either.
- Ref forwarding is not limited to DOM components. 
  - You can forward refs to class component instances, too.
- Forwarding refs can also be useful with higher-order components (also known as HOCs). 
```
class FancyButton extends React.Component {
  focus() {
    // ...
  }

  // ...
}

// Rather than exporting FancyButton, we export LogProps.
// It will render a FancyButton though.
export default logProps(FancyButton);
```
- There is one caveat to the above example: refs will not get passed through. 
  - That’s because `ref` is not a prop. 
  - Like `key`, it’s handled differently by React. 
- If you add a ref to a HOC, the ref will refer to the outermost container component, not the wrapped component.
- We can explicitly forward refs to the inner FancyButton component using the `React.forwardRef` API. 
  - React.forwardRef accepts a render function that receives props and ref parameters and returns a React node.
  - If you name the render function, DevTools will also include its name (e.g. ”ForwardRef(myFunction)”) 

##  Uncontrolled Components
- In a controlled component, form data is handled by a React component. 
- The alternative is **uncontrolled components, where form data is handled by the DOM itself**.
- In most cases, we recommend using controlled components to implement forms. 
- To write an uncontrolled component, instead of writing an event handler for every state update, you can use a `ref` to get form values from the DOM.
- Since an uncontrolled component keeps the source of truth in the DOM, it is sometimes easier to integrate React and non-React code when using uncontrolled components.
- With an uncontrolled component, you often want React to specify the initial value, but leave subsequent updates uncontrolled.
  - To handle this case, you can specify a `defaultValue` attribute instead of value
- **In React, an `<input type="file" />` is always an uncontrolled component**
  - because its value can only be set by a user, and not programmatically.
  - You should use the File API to interact with the files. 
  - `this.fileInput.current.files[0].name`

## Higher-Order Components
- A higher-order component(HOC) is an advanced technique in React for reusing component logic
- **A higher-order component is a function that takes a component and returns a new component**.
- `const EnhancedComponent = higherOrderComponent(WrappedComponent);`  
- Note that a HOC doesn’t modify the input component, nor does it use inheritance to copy its behavior. 
- Rather, a *HOC composes the original component by wrapping it in a container component*. 
- A HOC is a pure function with zero side-effects.
- The wrapped component receives all the props of the container, along with new props
- The HOC isn’t concerned with how or why the data is used, and the wrapped component isn’t concerned with where the data came from.
- the HOC has full control over how the component is defined.
- Like components, the contract between HOC and the wrapped component is entirely props-based. 
  - This makes it easy to swap one HOC for a different one, as long as they provide the same props to the wrapped component.
  - This may be useful if you change data-fetching libraries, for example.
- There are a few problems with modifying a component’s prototype (or otherwise mutate it) inside a HOC.
  - One is that the input component cannot be reused separately from the enhanced component. 
  - More crucially, if you apply another HOC to EnhancedComponent that also mutates componentDidUpdate, the first HOC’s functionality will be overridden! 
  - This HOC also won’t work with function components, which do not have lifecycle methods.
- Instead of mutation, HOCs should use composition, by wrapping the input component in a container component
- It works equally well with class and function components. 
  - And because it’s a pure function, it’s composable with other HOCs, or even with itself.
- You may have noticed similarities between HOCs and a pattern called container components. 
  - Container components are part of a strategy of separating responsibility between high-level and low-level concerns. 
  - Containers manage things like subscriptions and state, and pass props to components that handle things like rendering UI. 
  - HOCs use containers as part of their implementation. 
  - You can *think of HOCs as parameterized container component definitions*.
- HOCs can add features to a component. 
  - They shouldn’t drastically alter its contract. 
  - It’s expected that the component returned from a HOC has a similar interface to the wrapped component.
- HOCs should pass through props that are unrelated to its specific concern. 
- Most HOCs contain a render method that looks something like this:
```js
render() {
  // Filter out extra props that are specific to this HOC and shouldn't be passed through
  const { extraProp, ...passThroughProps } = this.props;

  // Inject props into the wrapped component. These are usually state values or instance methods.
  const injectedProp = someStateOrInstanceMethod;

  // Pass props to wrapped component
  return (
    <WrappedComponent
      injectedProp={injectedProp}
      {...passThroughProps}
    />
  );
}
```
- Not all HOCs look the same. Sometimes they accept only a single argument, the wrapped component.
- Usually, HOCs accept additional arguments. The most common signature for HOCs looks like this:  
```js
// React Redux's `connect`
const ConnectedComment = connect(commentSelector, commentActions)(CommentList);

// connect is a function that returns another function
const enhance = connect(commentListSelector, commentListActions);
// The returned function is a HOC, which returns a component that is connected to the Redux store
const ConnectedComment = enhance(CommentList);
```
- In other words, **`connect` is a higher-order function that returns a higher-order component**!
  - This form may seem confusing or unnecessary, but it has a useful property. 
  - Single-argument HOCs like the one returned by the `connect` function have the signature `Component => Component`. 
  - Functions whose output type is the same as its input type are really easy to compose together.
  - This same property also allows `connect` and other enhancer-style HOCs to be used as decorators, an experimental JavaScript proposal  

```js
// Instead of doing this...
const EnhancedComponent = withRouter(connect(commentSelector)(WrappedComponent))

// ... you can use a function composition utility
// compose(f, g, h) is the same as (...args) => f(g(h(...args)))
const enhance = compose(
  // These are both single-argument HOCs
  withRouter,
  connect(commentSelector)
)
const EnhancedComponent = enhance(WrappedComponent)
```
- The `compose` utility function is provided by many third-party libraries including lodash (as lodash.flowRight), Redux, and Ramda
- The container components created by HOCs show up in the React Developer Tools like any other component. 
  - The most common technique is to wrap the display name of the wrapped component.   
```js
function withSubscription(WrappedComponent) {
  class WithSubscription extends React.Component {/* ... */}
  WithSubscription.displayName = `WithSubscription(${getDisplayName(WrappedComponent)})`;
  return WithSubscription;
}

function getDisplayName(WrappedComponent) {
  return WrappedComponent.displayName || WrappedComponent.name || 'Component';
}
```
- Don’t Use HOCs Inside the render Method
  - React’s diffing algorithm (called reconciliation) uses component identity to determine whether it should update the existing subtree or throw it away and mount a new one. 
  - If the component returned from `render` is identical (===) to the component from the previous render, React recursively updates the subtree by diffing it with the new one. 
  - If they’re not equal, the previous subtree is unmounted completely.
  - It matters for HOCs because it means you can’t apply a HOC to a component within the render method of a component
  - The problem here isn’t just about performance - remounting a component causes the state of that component and all of its children to be lost.
- Instead, **apply HOCs outside the component definition** so that the resulting component is created only once. 
  - Then, its identity will be consistent across renders. This is usually what you want, anyway.
  - In those rare cases where you need to apply a HOC dynamically, you can also do it inside a component’s lifecycle methods or its constructor.
- When you apply a HOC to a component, though, the original component is wrapped with a container component. 
  - That means the new component does not have any of the static methods of the original component.
  - To solve this, you could copy the methods onto the container before returning it manually
  - You can use `hoist-non-react-statics` to automatically copy all non-React static methods
  - Another possible solution is to export the static method separately from the component itself
- If you add a ref to an element whose component is the result of a HOC, the ref refers to an instance of the outermost container component, not the wrapped component.
  - The solution for this problem is to use the `React.forwardRef`

- 使用mixins处理交叉关注点的问题
  - mixin可能导致命名冲突
  - mixin引入了隐式依赖关系，不方便组件层级移动和修改
  - mixin会不断增加组件复杂度
  - 参考 https://lizhiyao.github.io/2018/01/05/mixins-considered-harmful/
- 高阶组件在React第三方库中很常见，比如Redux的connect和Relay的createFragmentContainer.
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

## Render Props
- render prop refers to a technique for sharing code between React components using a prop whose value is a function.
  - function as prop
- A component with a **render prop takes a function that returns a React element and calls it instead of implementing its own render logic**.   
```
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```
- Components are the primary unit of code reuse in React
  - but it’s not always obvious how to share the state or behavior that one component encapsulates to other components that need that same state.
  - For example, A component tracks the mouse position in a web app
  - If another component needs to know about the cursor position, can we encapsulate that behavior so that we can easily share it with that component?
- a render prop is a function prop that a component uses to know what to render.
- One interesting thing to note about render props is that you can implement most higher-order components (HOC) using a regular component with a render prop.
- In fact, any prop that is a function that a component uses to know what to render is technically a “render prop”
  - Although the examples above use `render`, we could just as easily use the `children` prop!
  - And remember, the `children` prop doesn’t actually need to be named in the list of “attributes” in your JSX element. 
  - Instead, you can put it directly inside the element!
```jsx
<Mouse children={mouse => (
  <p>The mouse position is {mouse.x}, {mouse.y}</p>
)}/>

<Mouse>
  {mouse => (
    <p>The mouse position is {mouse.x}, {mouse.y}</p>
  )}
</Mouse>
```
- Using a render prop can negate the advantage that comes from using `React.PureComponent` **if you create the function inside a `render` method**. 
  - This is because the shallow prop comparison will always return false for new props
  - and each `render` in this case will generate a new value for the render prop. So your Component would re-render all the time.
  - To get around this problem, you can sometimes define the prop as an instance method  
```js
class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>

        {/*
          This is bad! 
          The value of the `render` prop will be different on each render.
        */}
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}

class Mouse extends React.Pure/Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }
  handleMouseMove(event) {
    this.setState({
      y: event.clientY
    });
  }
  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>
        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}
class MouseTracker extends React.Component {
  // Defined as an instance method, 
  // `this.renderTheCat` always refers to *same* function when we use it in render
  renderTheCat(mouse) {
    return <Cat mouse={mouse} />;
  }

  render() {
    // 这么没绑定this，this value in an unbound renderTheCat will be the this.props object of Mouse.
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse render={this.renderTheCat} />
      </div>
    );
  }
}
```
- In cases where you cannot define the prop statically (e.g. because you need to close over the component’s props and/or state), `<Mouse>` should extends `React.Component` instead.
  - In cases where you cannot define the render prop method (renderTheCat) statically (e.g. because you need to close over the Mouse component's props and/or state), Mouse Component should extend React.Component instead. When Mouse is a PureComponent, the child Cat will not re-render when Mouse's state or props change, since Cat's own props and state will not have changed! If Mouse is a regular Component instead, a change to the Mouse's state or props will automatically cause it's child Cat to re-render.
  - I think including a bound method in the example is dangerous, because if the method did reference this.props or this.state, it would be incorrect to pass a bound version to the render prop because Mouse would fail to re-render when props/state change,
  - https://github.com/reactjs/reactjs.org/pull/700
```js
class Foo extends PureComponent {
  render() {
    return this.props.render('abc')
  }
}

class Bar extends Component {
  constructor(props, context) {
    super(props, context)
    this.renderBaz = this.renderBaz.bind(this)
  }

  // 绑定this后，若this.props变化，但renderBaz引用未变，所以Foo不会rerender
  // 若Foo继承的是Component，则Foo作为Bar的子组件会再次调用render
  renderBaz(value) {
    return value + this.props.value
  }

  render() {
    return <Foo render={this.renderBaz} />
  }
}

<Bar value="def" /> // renders "abcdef"
<Bar value="ghi" /> // still renders "abcdef"
It's a pretty subtle mistake, which is why I think it's dangerous/incorrect to suggest binding as a solution, especially when the binding isn't even necessary in the particular example.
```

## Portals
- Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.
- `ReactDOM.createPortal(child, container)`
	- `child` is any renderable React child, such as an element, string, or fragment
	- `container` is a DOM element
- Normally, when you return an element from a component's render method, it's mounted into the DOM as a child of the nearest parent node
- A typical use case for portals is when a parent component has an `overflow: hidden` or `z-index` style, but you need the child to visually break outof its container. 
	- For example, dialogs, hovercards, and tooltips.
  - When working with portals, remember that managing keyboard focus becomes very important.
- Even though a portal can be anywhere in the DOM tree, it behaves like a normal React child in every other way. 
  - Features like context work exactly the same regardless of whether the child is a portal, as the portal still exists in the React tree regardless of position in the DOM tree.
- An event fired from inside a portal will propagate to ancestors in the containing React tree, even if those elements are not ancestors in the DOM tree.
- The **portal element is inserted in the DOM tree after the Modal's children are mounted**
  - meaning that children will be mounted on a detached DOM node. 
- If a child component requires to be attached to the DOM tree immediately when mounted, for example to measure a DOM node, or uses 'autoFocus' in a descendant, *add state to Modal* and only render the children when Modal is inserted in the DOM tree.
- Catching an event bubbling up from a portal in a parent component allows the development of more flexible abstractions that are not inherently reliant on portals.

## Optimizing Performance
- Use the Production Build
- Profiling Components with the Chrome Performance Tab: 使用Chrome性能分析工具分析组件性能
	- 先暂停React DevTools扩展，再打开Chrome DevTools Performance并点击Record，在User Timing标签下，React事件将会分组列出
- Profiling Components with the Chrome Performance Tab
- In the development mode, you can visualize how components mount, update, and unmount, using the performance tools in supported browsers. 
- To do this in Chrome:
  - Temporarily disable all Chrome extensions, especially React DevTools. They can significantly skew the results!
  - Make sure you’re running the application in the development mode.
  - Open the Chrome DevTools Performance tab and press Record.
  - Perform the actions you want to profile. Don’t record more than 20 seconds or Chrome might hang.
  Stop recording.
  - React events will be grouped under the User Timing label.
- **Profiling Components with the DevTools Profiler**
- react-dom 16.5+ and react-native 0.57+ provide enhanced profiling capabilities in DEV mode with the React DevTools Profiler.
- The “Profiler” panel will be empty initially. Click the record button to start profiling
- Browsing commits
  - React does work in two phases
  - The **render phase determines what changes need to be made to e.g. the DOM**. 
    - During this phase, React calls `render` and then compares the result to the previous render.
  - The **commit phase is when React applies any changes**. 
    - In the case of React DOM, this is when React inserts, updates, and removes DOM nodes.
    - React also calls lifecycles like `componentDidMount` and `componentDidUpdate` during this phase.
  - The DevTools profiler groups performance info by commit. 
- Filtering commits
  - The longer you profile, the more times your application will render. 
  - In some cases you may end up with too many commits to easily process. 
  - The profiler offers a filtering mechanism to help with this. 
  - Use it to specify a threshold and the profiler will hide all commits that were faster than that value.
- The flame chart view represents the state of your application for a particular commit. 
  - Each bar in the chart represents a React component (e.g. App, Nav). 
  - The size and color of the bar represents how long it took to render the component and its children.
- The ranked chart view represents a single commit. 
  - Each bar in the chart represents a React component (e.g. App, Nav). 
  - The chart is ordered so that the components which took the longest to render are at the top.
  - A component’s render time includes the time spent rendering its children
    - so the components which took the longest to render are generally near the top of the tree.
- The component chart provides this information in the form of a bar chart
  - to see how many times a particular component rendered while you were profiling. 
  - Each bar in the chart represents a time when the component rendered. 
- React recently added another experimental API for tracing the cause of an update. 
  - “Interactions” traced with this API will also be shown in the profiler
  - `import { unstable_trace as trace } from "scheduler/tracing"`
  - https://gist.github.com/bvaughn/8de925562903afd2e7a12554adcdda16
- Virtualize Long Lists
	- If your application renders long lists of data (hundreds or thousands of rows), we recommended using a technique known as “windowing”.
	- This technique only renders a small subset of your rows at any given time, and can dramatically reduce the time it takes to re-render the components as well as the number of DOM nodes created.
	- `react-window` and `react-virtualized` are popular windowing libraries. They provide several reusable components for displaying lists, grids, and tabular data.
- Avoid Reconciliation
  - React builds and maintains an internal representation of the rendered UI. 
    - It includes the React elements you return from your components. 
    - This representation lets React avoid creating DOM nodes and accessing existing ones beyond necessity, as that can be slower than operations on JavaScript objects. 
    - Sometimes it is referred to as a *virtual DOM*
	- When a component’s props or state change, React decides whether an actual DOM update is necessary by comparing the newly returned element with the previously rendered one. 
    - When they are not equal, React will update the DOM.
  - Even though React only updates the changed DOM nodes, re-rendering still takes some time
	- `shouldComponentUpdate()` is triggered before the re-rendering process starts.
    - The default implementation of this function returns `true`, leaving React to perform the update
    - If you know that in some situations your component doesn’t need to update, you can return `false` from shouldComponentUpdate instead, to skip the whole rendering process, including calling render() on this component and below.
  - In most cases, instead of writing shouldComponentUpdate() by hand, you can inherit from `React.PureComponent`. 
    - It is equivalent to implementing shouldComponentUpdate() with a shallow comparison of current and previous props and state.
- shouldComponentUpdate原理示意图

## Profiler
- Profiler measures how often a React application renders and what the “cost” of rendering is. 
  - Its purpose is to help identify parts of an application that are slow and may benefit from optimizations such as memoization.
- A `Profiler` Component can be added anywhere in a React tree to measure the cost of rendering that part of the tree. 
  - It requires two props: an `id` (string) and an `onRender` callback function which React calls any time a component within the profiled tree “commits” an update.
- Multiple Profiler components can be used to measure different parts of an application
- Profiler components can also be nested to measure different components within the same subtree
- onRender Callback receives parameters describing what was rendered and how long it took.

## Reconciliation 协调
- https://reactjs.org/docs/reconciliation.html  
- When you use React, at a single point in time you can think of the `render()` function as creating a tree of React elements. 
- On the next state or props update, that `render()` function will return a different tree of React elements. 
- React then needs to figure out how to efficiently update the UI to match the most recent tree.
- There are some generic solutions to this algorithmic problem of generating the minimum number of operations to transform one tree into another. 
- However, the state of the art algorithms have a complexity in the order of O(n3) where n is the number of elements in the tree.
-  React implements a heuristic O(n) algorithm based on **two assumptions**:
  - Two elements of different types will produce different trees.
  - The developer can hint at which child elements may be stable across different renders with a `key` prop.
- In practice, these assumptions are valid for almost all practical use cases.
- The **Diffing Algorithm**
- When diffing two trees, React first compares the two root elements.
- **Elements Of Different Types**  
- Whenever the root elements have different types, React will tear down the old tree and build the new tree from scratch. 
  - When tearing down a tree, old DOM nodes are destroyed. 
  - Component instances receive `componentWillUnmount()`. 
  - When building up a new tree, new DOM nodes are inserted into the DOM. 
  - Component instances receive `componentWillMount()` and then `componentDidMount()`. 
  - Any state associated with the old tree is lost.
  - Any components below the root will also get unmounted and have their state destroyed. 
- **DOM Elements Of The Same Type**  
- When comparing two React DOM elements of the same type, React looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes
- After handling the DOM node, React then recurses on the children.
- **Component Elements Of The Same Type**
- When a component updates, the instance stays the same, so that state is maintained across renders. 
- React updates the props of the underlying component instance to match the new element, and calls `componentWillReceiveProps()` and `componentWillUpdate()` on the underlying instance.
- Next, the `render()` method is called and the diff algorithm recurses on the previous result and the new result.
- **Recursing On Children**  
- By default, when recursing on the children of a DOM node, React just iterates over both lists of children at the same time and generates a mutation whenever there’s a difference.
  - React will match the two `<li>first</li>` trees, match the two `<li>second</li>` trees, and then insert the `<li>third</li>` tree  
  ```
  <ul>
    <li>first</li>
    <li>second</li>
  </ul>

  <ul>
    <li>first</li>
    <li>second</li>
    <li>third</li>
  </ul>
  ```
  - React will mutate every child instead of realizing it can keep the `<li>Duke</li>` and `<li>Villanova</li>` subtrees intact. This inefficiency can be a problem.
  ```
  <ul>
    <li>Duke</li>
    <li>Villanova</li>
  </ul>

  <ul>
    <li>Connecticut</li>
    <li>Duke</li>
    <li>Villanova</li>
  </ul>
  ```
- In order to solve this issue, React supports a `key` attribute. 
- When children have keys, React uses the `key` to match children in the original tree with children in the subsequent tree. 
- Now React knows that the element with key '2014' is the new one, and the elements with the keys '2015' and '2016' have just moved.
```
  <ul>
    <li key="2015">Duke</li>
    <li key="2016">Villanova</li>
  </ul>

  <ul>
    <li key="2014">Connecticut</li>
    <li key="2015">Duke</li>
    <li key="2016">Villanova</li>
  </ul>
```
- Reorders can also cause issues with component state when indexes are used as keys. 
  - Component instances are updated and reused based on their key. 
  - If the key is an index, moving an item changes it. 
  - As a result, component state for things like uncontrolled inputs can get mixed up and updated in unexpected ways.
- It is important to remember that the reconciliation algorithm is an implementation detail. 
  - React could rerender the whole app on every action; the end result would be the same. 
  - Just to be clear, rerender in this context means calling `render` for all components
  - it doesn’t mean React will unmount and remount them. 
  - It will only apply the differences following the rules stated in the previous sections.
- In the current implementation, you can express the fact that a subtree has been moved amongst its siblings, but you cannot tell that it has moved somewhere else. The algorithm will rerender that full subtree.
- Because React relies on heuristics, if the assumptions behind them are not met, performance will suffer.
  - The algorithm will not try to match subtrees of different component types. 
    - If you see yourself alternating between two component types with very similar output, you may want to make it the same type. 
    - In practice, we haven’t found this to be an issue.
  - Keys should be stable, predictable, and unique. 
    - Unstable keys (like those produced by Math.random()) will cause many component instances and DOM nodes to be unnecessarily recreated, which can cause performance degradation and lost state in child components.

- 将一棵树转换为另一棵树的最小操作数算法问题的通用方案，树中元素个数为n，最先进的算法 的时间复杂度为O(n3) 
- React基于两点假设，实现了一个启发式的O(n)算法：
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
		- 当索引用作key时，组件状态在重新排序时也会有问题。
		- 组件实例基于key进行更新和重用。如果key是索引，则item的顺序变化会改变key值。这将导致非受控组件的状态可能会以意想不到的方式混淆和更新。

## Code-Splitting
- Most React apps will have their files “bundled” using tools like Webpack, Rollup. 
  - Bundling is the process of following imported files and merging them into a single file: a “bundle”.
  - This bundle can then be included on a webpage to load an entire app at once.
- Bundling is great, but as your app grows, your bundle will grow too. 
  - Especially if you are including large third-party libraries. 
  - To avoid winding up with a large bundle, it’s good to get ahead of the problem and start “splitting” your bundle
- Code-Splitting is a feature supported by bundlers like Webpack and Browserify (via factor-bundle) which can create multiple bundles that can be dynamically loaded at runtime.
- Code-splitting your app can help you "lazy-load" just the things that are currently needed by the user
	- While you haven’t reduced the overall amount of code in your app, you’ve avoided loading code that the user may never need, and reduced the amount of code needed during the initial load.
- The **best way to introduce code-splitting** into your app is through the dynamic `import()` syntax.
  - When Webpack comes across this syntax, it automatically starts code-splitting your app. 
  - you’ll need to make sure that Babel can parse the dynamic import syntax but is not transforming it. 
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
  - React.lazy takes a function that must call a dynamic import().
  - It returns a Promise which resolves to a module with a default export containing a React component.
  - This will automatically load the bundle containing the OtherComponent when this component is first rendered.
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
- The lazy component should then be rendered inside a `Suspense` component, which allows us to show some fallback content (such as a loading indicator) while we’re waiting for the lazy component to load.
  - The `fallback` prop accepts any React elements that you want to render while waiting for the component to load. 
  - You can place the `Suspense` component anywhere above the lazy component. 
  - You can even wrap multiple lazy components with a single `Suspense` component.
- Deciding where in your app to introduce code splitting can be a bit tricky. 
- You want to make sure you choose places that will split bundles evenly, but won’t disrupt the user experience.
- A good place to start is with routes. 
- You can setup route-based code splitting into your app using libraries like React Router with React.lazy
- React.lazy currently *only supports default exports*. 
  - If the module you want to import uses named exports, you can create an intermediate module that reexports it as the default.    
```
// ManyComponents.js
export const MyComponent = /* ... */;
export const MyUnusedComponent = /* ... */;

// MyComponent.js
export { MyComponent as default } from "./ManyComponents.js";

// MyApp.js
import React, { lazy } from 'react';
const MyComponent = lazy(() => import("./MyComponent.js"));
```
- React.lazy和Suspense尚不可用于服务器端渲染
  - 如果要在服务器渲染的应用程序中进行代码拆分，建议使用Loadable Components
  - https://github.com/gregberge/loadable-components

## Static Type Checking
- Static type checkers like Flow and TypeScript identify certain types of problems before you even run your code. 
- They can also improve developer workflow by adding features like auto-completion. 
- To be able to show errors and hints from other packages, the compiler relies on declaration files.
  - A declaration file provides all the type information about a library.
- Bundled - The library bundles its own declaration file. 
  - To check if a library has bundled types, look for an `index.d.ts` file in the project. 
  - Some libraries will have it specified in their `package.json` under the `typings` or `types` field.
- DefinitelyTyped - DefinitelyTyped is a huge repository of declarations for libraries that don’t bundle a declaration file. 
  - The declarations are crowd-sourced and managed by Microsoft and open source contributors. 
  - React for example doesn’t bundle its own declaration file. Instead we can get it from DefinitelyTyped. 
- Local Declarations 
  - Sometimes the package that you want to use doesn’t bundle declarations nor is it available on DefinitelyTyped. 
  - In that case, we can have a local declaration file.
  -  To do this, create a `declarations.d.ts` file in the root of your source directory. 
- https://www.typescriptlang.org/docs/handbook/react-&-webpack.html
- 对于复杂的代码库，建议使用Flow或者TypeScript来替代PropTypes
- Reason是一门基于OCaml的语言，既可以通过BuckleScript被编译为JavaScript，也支持直接编译为原生的二进制汇编

## Strict Mode
- `StrictMode` is a tool for highlighting potential problems in an application. 
  - Like `Fragment`, `StrictMode` does not render any visible UI. 
  - It activates additional checks and warnings for its descendants.
  - Strict mode checks are **run in development mode only**; they do not impact the production build.
- You can enable strict mode for any part of your application
- Identifying components with unsafe lifecycles
	- componentWillMount， componentWillReceiveProps， componentWillUpdate
- Warning about legacy string ref API usage
	- object refs by `React.createRef` were largely added as a replacement for string refs
  - You don’t need to replace callback refs in your components. 
    - They are slightly more flexible, so they will remain as an advanced feature.
- Warning about deprecated findDOMNode usage
	- React used to support `findDOMNode` to search the tree for a DOM node given a class instance. 
  - Normally you don’t need this because you can attach a `ref` directly to a DOM node.
  - `findDOMNode` can be used on class components but this was breaking abstraction levels by allowing a parent to demand that certain children was rendered. 
  - It creates a refactoring hazard where you can’t change the implementation details of a component because a parent might be reaching into its DOM node
  - `findDOMNode` is a one time read API. 
    - It only gave you an answer when you asked for it.
    - If a child component renders a different node, there is no way to handle this change. 
    - Therefore findDOMNode only worked if components always return a single DOM node that never changes.
- You can instead make this explicit by passing a ref to your custom component and pass that along to the DOM using ref forwarding.
- You can also add a wrapper DOM node in your component and attach a ref directly to it.
- In CSS, the `display: contents` attribute can be used if you don’t want the node to be part of the layout.
- Detecting legacy context API
  - The legacy context API is error-prone, and will be removed
- **Detecting unexpected side effects**
	- Conceptually, React does work in two phases
	- **render phase** determines what changes need to be made to e.g. the DOM. 
	- **commit phase** is when React applies any changes.
	- The commit phase is usually very fast, but rendering can be slow. 
  - For this reason, the upcoming concurrent mode (which is not enabled by default yet) *breaks the rendering work into pieces*, pausing and resuming the work to avoid blocking the browser. 
  - This means that React may invoke render phase lifecycles more than once before committing
    - or it may invoke them without committing at all (because of an error or a higher priority interruption)
  - Render phase lifecycles include the following class component methods:  
    - constructor
    - componentWillMount
    - componentWillReceiveProps
    - componentWillUpdate
    - getDerivedStateFromProps
    - shouldComponentUpdate
    - render
    - setState updater functions (the first argument)  
  - Because the above methods might be called more than once, it’s important that they do not contain side-effects. 
    - Ignoring this rule can lead to a variety of problems, including memory leaks and invalid application state. 
    - Unfortunately, it can be difficult to detect these problems as they can often be non-deterministic.
	- Strict mode can’t automatically detect side effects for you, but it can help you spot them by making them a little more deterministic. 
  - This is done by intentionally **double-invoking the following methods**:
    - Class component `constructor`, `render`, and `shouldComponentUpdate` methods
    - Class component static `getDerivedStateFromProps` method
    - Function component bodies
    - State updater functions (the first argument to `setState`)
    - Functions passed to `useState`, `useMemo`, or `useReducer`
    - This only applies to development mode. Lifecycles will not be double-invoked in production mode.
  - By intentionally double-invoking methods like the component constructor, strict mode makes patterns like this easier to spot.
    - 如在constructor中调用非幂等的方法`SharedApplicationState.recordEvent('ExampleComponent');`
    - instantiating this component multiple times could lead to invalid application state. 

## Error Boundaries
- A JavaScript error in a part of the UI shouldn’t break the whole app. 
  - To solve this problem for React users, React 16 introduces a new concept of an “error boundary”.
- Error boundaries are React components that **catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI** instead of the component tree that crashed. 
- Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.
- Error boundaries do not catch errors for:
	- Event handlers
	- Asynchronous code (e.g. setTimeout or requestAnimationFrame callbacks)
	- Server side rendering
	- Errors thrown in the error boundary itself (rather than its children)
- A class component becomes an error boundary if it defines either (or both) of the lifecycle methods  
	- `static getDerivedStateFromError(error)` to render a fallback UI after an error has been thrown.
	- `componentDidCatch(error, errorInfo)` to log error information.
  - Then you can use it as a regular component
- Error boundaries work like a JavaScript `catch {}` block, but for components.
- Only class components can be error boundaries. 
- In practice, most of the time you’ll want to declare an error boundary component once and use it throughout your application.
- Error boundaries only catch errors in the components below them in the tree. 
- An error boundary can’t catch an error within itself. 
- If an error boundary fails trying to render the error message, the error will propagate to the closest error boundary above it. 
  - This, too, is similar to how `catch {}` block works in JavaScript.
- You may wrap top-level route components to display a “Something went wrong” message to the user, just like server-side frameworks often handle crashes. 
- You may also wrap individual widgets in an error boundary to protect them from crashing the rest of the application.
- As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree.
  - We debated this decision, but in our experience it is worse to leave corrupted UI in place than to completely remove it.
  - It is worse for a payments app to display a wrong amount than to render nothing.
- We also encourage you to use JS error reporting services (or build your own) so that you can learn about unhandled exceptions as they happen in production, and fix them.
- React 16 prints all errors that occurred during rendering to the console in development, even if the application accidentally swallows them. 
  - In addition to the error message and the JavaScript stack, it also provides component stack traces. 
  - Component names displayed in the stack traces depend on the `Function.name` property. 
- `try/catch` is great but it only works for imperative code
- Error boundaries do not catch errors inside event handlers.
  - React doesn’t need error boundaries to recover from errors in event handlers. 
  - Unlike the render method and lifecycle methods, the event handlers don’t happen during rendering. 
  - So if they throw, React still knows what to display on the screen.
- If you need to catch an error inside event handler, use the regular JavaScript `try/catch` statement

## Integrating with Other Libraries
- Integrating with DOM Manipulation Plugins
- **React is unaware of changes made to the DOM outside of React**. It determines updates based on its own internal representation, and if the same DOM nodes are manipulated by another library, React gets confused and has no way to recover.
- The easiest way to avoid conflicts is to prevent the React component from updating. 
- You can do this by rendering elements that React has no reason to update, like an empty `<div />`.
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
- To prevent React from touching the DOM after mounting, we will return an empty `<div />` from the render() method.
- The `<div />` element has no properties or children, so React has no reason to update it, leaving the jQuery plugin free to manage that part of the DOM
- remember to remove any event listeners the plugin registered in `componentWillUnmount` to prevent memory leaks.
  - If the plugin does not provide a method for cleanup, you will probably have to provide your own
- We encourage you to use React components when you can.
- Integrating with Other View Libraries
	- Although React is commonly used at startup to load a single root React component into the DOM, `ReactDOM.render()` can also be called multiple times for independent parts of the UI which can be as small as a button, or as large as an app.
	- Replacing String-Based Rendering with React  
	```
	$('#container').html('<button id="btn">Say Hello</button>');
	$('#btn').click(function() {
	  alert('Hello!');
	});
	```
	- 对于`$el.html(htmlString)`：Just rewrite the string based rendering as a React component.
	```
  function Button() {
    return <button id="btn">Say Hello</button>;
  }
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
- You can have as many such isolated components as you like, and use `ReactDOM.render()` to render them to different DOM containers. 
  - Gradually, as you convert more of your app to React, you will be able to combine them into larger components, and move some of the `ReactDOM.render()` calls up the hierarchy.
- Integrating with Model Layers
- While it is generally recommended to use unidirectional data flow such as React state, Flux, or Redux, React components can use a model layer from other frameworks and libraries.
- You can use React with any model library by subscribing to its changes in the lifecycle methods and, optionally, copying the data into the local React state.

## Accessibility
- Web accessibility (also referred to as `a11y`) is the design and creation of websites that can be used by everyone.  
- WCAG: The Web Content Accessibility Guidelines provides guidelines for creating accessible websites.
- WAI-ARIA: The Web Accessibility Initiative - Accessible Rich Internet Applications document contains techniques for building fully accessible JavaScript widgets.  
- Note that all `aria-*` HTML attributes are fully supported in JSX. Whereas most DOM properties and attributes in React are camelCased, these attributes should be **hyphen-cased** (also known as kebab-case, lisp-case, etc) as they are in plain HTML
- Every HTML form control, such as `<input>` and `<textarea>`, needs to be labeled accessibly.
- Although these standard HTML practices can be directly used in React, note that the `for` attribute is written as `htmlFor` in JSX
- Only ever use CSS that removes this outline, for example by setting `outline: 0`, if you are replacing it with another keyboard focus outline implementation.
- MDN Web Docs takes a look at this and describes how we can build keyboard-navigable JavaScript widgets.
- To set focus in React, we can use Refs to DOM elements.
- Ensure that all functionality exposed through a mouse or pointer event can also be accessed using the keyboard alone. 
- Depending only on the pointer device will lead to many cases where keyboard users cannot use your application.
- Other Points for Consideration
  - Setting the language
  - Setting the document title
  - Ensure that all readable text on your website has sufficient color contrast to remain maximally readable by users with low vision

## Web Components
- React and Web Components are built to solve different problems. 
- Web Components provide strong encapsulation for reusable components
- React provides a declarative library that keeps the DOM in sync with your data.
- Using Web Components in React
  - Web Components often expose an imperative API. 
  - To access the imperative APIs of a Web Component, you will need to use a `ref` to interact with the DOM node directly. 
  - If you are using third-party Web Components, the best solution is to write a React component that behaves as a wrapper for your Web Component.
  - Events emitted by a Web Component may not properly propagate through a React render tree. 
  - You will need to manually attach event handlers to handle these events within your React components.
```
class HelloMessage extends React.Component {
  render() {
    return <div>Hello <x-search>{this.props.name}</x-search>!</div>;
  }
}
```
- Using React in your Web Components
  - This code will not work if you transform classes with Babel.
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
	
