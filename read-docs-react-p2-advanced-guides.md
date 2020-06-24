---
tags: [docs, react]
title: read-docs-react-p2-advanced-guides
created: '2020-06-23T06:10:10.882Z'
modified: '2020-06-24T13:50:41.178Z'
---

# read-docs-react-p2-advanced-guides

## JSX In Depth
- JSX just provides syntactic sugar for the `React.createElement(componentType, props, ...children)` function
  - Create and return a new React element of the given type. 
  - The type argument can be either a tag name string (such as 'div' or 'span'), a React component type (a class or a function), or a React fragment type
- Capitalized types indicate that the JSX tag is referring to a React component. 
  - These tags get compiled into a direct reference to the named variable
  - so if you use the JSX `<Foo />` expression, `Foo` must be in scope.
- Since JSX compiles into calls to  React.createElement`, the React library must also always be in scope from your JSX code.
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
- You can pass any JavaScript expression as a prop, by surrounding it with `{}`
- You can pass a string literal as a prop.
  - When you pass a string literal, its value is HTML-unescaped
- If you pass no value for a prop, it defaults to true
  - we don’t recommend not passing a value for a prop, because it can be confused with the ES6 object shorthand
- If you already have props as an object, and you want to pass it in JSX, you can use `...` as a “spread” operator to pass the whole props object
  - Spread attributes can be useful but they also make it easy to pass unnecessary props to components that don’t care about them or to pass invalid HTML attributes to the DOM. 
  - We recommend using this syntax sparingly.
- In JSX expressions that contain both an opening tag and a closing tag, the content between those tags is passed as a special prop: `props.children`
- You can put a string between the opening and closing tags and props.
  - children will just be that string. 
  - HTML is unescaped, so you can generally write JSX just like you would write HTML in this way
  - JSX removes whitespace at the beginning, ending of a line, blank lines
- You can provide more JSX elements as the children
  - A React component can also return an array of elements  
- You can pass any JavaScript expression as children, by enclosing it within `{}`
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
	- createReactClass()作为一个属性 ` mixins: [SetIntervalMixin]`
	
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
- Fragments let you group a list of children without adding extra nodes to the DOM.
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
- Context is primarily used when some data needs to be accessible by many components *at different nesting levels*. 
  - Apply it sparingly because it makes component reuse more difficult.
- If you *only want to avoid passing some props through many levels*, component composition is often a simpler solution than context
  - It might feel redundant to pass down the user and avatarSize props through many levels if in the end only the Avatar component really needs it. 
  - It’s also annoying that whenever the Avatar component needs more props from the top, you have to add them at all the intermediate levels too.
  - One way to solve this issue without context is to *pass down the Avatar component itself* so that the intermediate components don’t need to know about the user or avatarSize props
  - With this change, only the top-most Page component needs to know about the Link and Avatar components’ use of user and avatarSize
- This inversion of control can make your code cleaner in many cases by reducing the amount of props you need to pass through your application and giving more control to the root components. 
  - However, this isn’t the right choice in every case: moving more complexity higher in the tree makes those higher-level components more complicated and forces the lower-level components to be more flexible than you may want
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
- If two or more context values are often used together, you might want to consider creating your own render prop component that provides both.
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
- However, there are a few cases where you need to imperatively modify a child outside of the typical dataflow.
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
  - You may not use the ref attribute on function components because they don’t have instances.
    - If you want to allow people to take a ref to your function component, you can use forwardRef (possibly in conjunction with useImperativeHandle)
    - or you can convert the component to a class.
    - You can, however, use the `ref` attribute inside a function component as long as you refer to a DOM element or a class component
- In rare cases, you might want to have access to a child’s DOM node from a parent component. 
  - This is generally not recommended because it breaks component encapsulation
  - but it can occasionally be useful for triggering focus or measuring the size or position of a child DOM node.
  - While you could add a ref to the child component, this is not an ideal solution, as you would only get a component instance rather than a DOM node. 
    - Additionally, this wouldn’t work with function components.
  - We recommend to use ref forwarding for these cases. 
    - Ref forwarding lets components opt into exposing any child 
  component’s ref as their own. 
  - If you need more flexibility than provided by ref forwarding, you can use this alternative approach and explicitly pass a ref as a differently named prop.
    - https://gist.github.com/gaearon/1a018a023347fe1c2476073330cc5509
  - When possible, we advise against exposing DOM nodes
    - but it can be a useful escape hatch. 
    - Note that this approach requires you to add some code to the child component. 
    - If you have absolutely no control over the child component implementation, your last option is to use `findDOMNode()`, but it is discouraged and deprecated in StrictMode.
- React also supports another way to set refs called **callback refs**, which gives more fine-grain control over when refs are set and unset.
- Instead of passing a ref attribute created by createRef(), you pass a function.
  - The function receives the React component instance or HTML DOM element as its argument, which can be stored and accessed elsewhere.
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
  - This way, components using FancyButton can get a ref to the underlying button DOM node and access it if necessary—just like if they used a DOM button directly.
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
- The alternative is uncontrolled components, where form data is handled by the DOM itself.
- In most cases, we recommend using controlled components to implement forms. 
- To write an uncontrolled component, instead of writing an event handler for every state update, you can use a `ref` to get form values from the DOM.
- Since an uncontrolled component keeps the source of truth in the DOM, it is sometimes easier to integrate React and non-React code when using uncontrolled components.
- With an uncontrolled component, you often want React to specify the initial value, but leave subsequent updates uncontrolled.
  - To handle this case, you can specify a `defaultValue` attribute instead of value
-In React, an `<input type="file" />` is always an uncontrolled component because its value can only be set by a user, and not programmatically.
  - You should use the File API to interact with the files. 
  - `this.fileInput.current.files[0].name`


## Higher-Order Components
- A higher-order component (HOC) is an advanced technique in React for reusing component logic
- A higher-order component is a function that takes a component and returns a new component.
- `const EnhancedComponent = higherOrderComponent(WrappedComponent);`
- Note that a HOC doesn’t modify the input component, nor does it use inheritance to copy its behavior. 
- Rather, a HOC composes the original component by wrapping it in a container component. 
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
- It works equally well with class and function components. And because it’s a pure function, it’s composable with other HOCs, or even with itself.
- You may have noticed similarities between HOCs and a pattern called container components. 
  - Container components are part of a strategy of separating responsibility between high-level and low-level concerns. 
  - Containers manage things like subscriptions and state, and pass props to components that handle things like rendering UI. 
  - HOCs use containers as part of their implementation. 
  - You can think of HOCs as parameterized container component definitions.
- HOCs can add features to a component. 
  - They shouldn’t drastically alter its contract. 
  - It’s expected that the component returned from a HOC has a similar interface to the wrapped component.
- HOCs should pass through props that are unrelated to its specific concern. Most HOCs contain a render method that looks something like this:
```
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
- Usually, HOCs accept additional arguments.
```
// React Redux's `connect`
const ConnectedComment = connect(commentSelector, commentActions)(CommentList);

// connect is a function that returns another function
const enhance = connect(commentListSelector, commentListActions);
// The returned function is a HOC, which returns a component that is connected to the Redux store
const ConnectedComment = enhance(CommentList);
```
- In other words, connect is a higher-order function that returns a higher-order component!
```
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
```
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
  - The problem here isn’t just about performance — remounting a component causes the state of that component and all of its children to be lost.
- Instead, apply HOCs outside the component definition so that the resulting component is created only once. 
  - Then, its identity will be consistent across renders. This is usually what you want, anyway.
  - In those rare cases where you need to apply a HOC dynamically, you can also do it inside a component’s lifecycle methods or its constructor.
- When you apply a HOC to a component, though, the original component is wrapped with a container component. 
  - That means the new component does not have any of the static methods of the original component.
  - To solve this, you could copy the methods onto the container before returning it manually
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
- A component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic.   
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
- StrictMode不会渲染任何真实的UI
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
	
