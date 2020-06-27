---
tags: [docs, react]
title: read-docs-react-p1-main-concepts
created: '2019-08-01T16:03:46.386Z'
modified: '2020-06-27T15:10:06.744Z'
---

# read-docs-react-p1-main-concepts
- React is a javaScript library for building user interfaces.

## resources 
- docs
  - https://reactjs.org/docs/hello-world.html
  - https://zh-hans.reactjs.org/docs/hello-world.html
- docs-topic
  - https://github.com/acdlite/react-fiber-architecture
  - https://reactjs.org/docs/reconciliation.html
- api 
  - https://reactjs.org/docs/react-api.html
  - https://reactjs.org/docs/react-component.html
  - https://reactjs.org/docs/react-dom.html
- components-common
  - https://github.com/reactjs/react-modal
  - https://github.com/reactjs/react-tabs
  - https://github.com/reactjs/react-transition-group
  - https://github.com/react-component/upload
  - https://github.com/react-component/form

## installation
- react for developer/designer
- https://unpkg.com/react@16/umd/react.development.js
- https://unpkg.com/react@16/umd/react.production.min.js
- https://unpkg.com/react-dom@16/umd/react-dom.development.js
- unpkg.com/react@16.8.0/umd/react.production.min.js  
- https://cdn.bootcdn.net/ajax/libs/react/16.13.1/umd/react.development.js

## 1.hello world     
- examine the building blocks of React apps: elements and components.
- The smallest React example looks like this
```jsx
  ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('root')
  );
```

## 2.jsx
- `const element = <h1>Hello, world!</h1>;`
  - This funny tag syntax is neither a string nor HTML.
  - It is called JSX, and it is a syntax extension to JavaScript. 
  - We recommend using it with React to describe what the UI should look like. 
  - JSX produces React “elements”
- React embraces the fact that rendering logic is inherently coupled with other UI logic: 
  - how events are handled
  - how the state changes over time
  - how the data is prepared for display
- React separates concerns with loosely coupled units called “components” that contain both markup and logic.
- React doesn’t require using JSX, but most people find it helpful as a visual aid when working with UI inside the JavaScript code. 
  - It also allows React to show more useful error and warning messages.
- You can put any valid JavaScript expression inside the curly braces in JSX
- **JSX is an Expression Too**  
  - After compilation, JSX expressions become regular JavaScript function calls and evaluate to JavaScript objects
  - you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions
- By default, React DOM escapes any values embedded in JSX before rendering them. 
  - Thus it ensures that you can never inject anything that’s not explicitly written in your application. 
  - *Everything is converted to a string* before being rendered. 
  - This helps prevent XSS(cross-site-scripting) attacks
- **JSX Represents Objects**
  - Babel compiles JSX down to `React.createElement()` calls.
  - These two examples are identical:
  ```
  const element = (
    <h1 className="greeting">
      Hello, world!
    </h1>
  );

  const element = React.createElement(
    'h1',
    {className: 'greeting'},
    'Hello, world!'
  );
  ```
  - React.createElement() performs a few checks to help you write bug-free code but essentially it creates an object like this:
  ```
  // Note: this structure is simplified
  const element = {
    type: 'h1',
    props: {
      className: 'greeting',
      children: 'Hello, world!'
    }
  };
  ```
  - These objects are called “React elements”. 
    - You can think of them as descriptions of what you want to see on the screen. 
    - React reads these objects and uses them to construct the DOM and keep it up to date.

## 3.rendering elements    
- Elements are the smallest building blocks of React apps.
  - An element describes what you want to see on the screen
  - Unlike browser DOM elements, React elements are plain objects, and are cheap to create. 
  - React DOM takes care of updating the DOM to match the React elements.
- Applications built with just React usually have a single root DOM node
  - We call this a “root” DOM node because everything inside it will be managed by React DOM.
- React elements are immutable. 
  - Once you create an element, you can’t change its children or attributes. 
  - An element represents the UI at a certain point in time.
  - With our knowledge so far, the only way to update the UI is to create a new element, and pass it to `ReactDOM.render()`
- React DOM compares the element and its children to the previous one, and **only applies the DOM updates necessary** to bring the DOM to the desired state.
- Even though we create an element describing the whole UI tree on every tick, *only the text node whose contents have changed gets updated* by React DOM
- In our experience, thinking about how the UI should look at any given moment, rather than how to change it over time, eliminates a whole class of bugs.

## 4.components & props    
- Components let you split the UI into independent, reusable pieces, and think about each piece in isolation
  - Conceptually, components are like JavaScript functions. 
  - They **accept arbitrary inputs (called “props”) and return React elements** describing what should appear on the screen.
- We call such components “function components” because they are literally JavaScript functions.
  - accepts a single props object argument with data and returns a React element. 
- React elements can represent DOM tags, elements can also represent user-defined components
- When React sees an element representing a user-defined component, it passes JSX attributes and children to this component as a single object. We call this object `props`.
- React treats components starting with lowercase letters as DOM tags. 
- We recommend naming props from the component’s own point of view rather than the context in which it is being used.
- extract components
  - A good rule of thumb is that if a part of your UI is *used several times* (Button, Panel, Avatar), or is *complex enough* on its own (App, FeedStory, Comment), it is a good candidate to be extracted to a separate component
- Such functions are called “pure” because they do not attempt to change their inputs, and always return the same result for the same inputs.
- All React components must act like pure functions with respect to their props.
  - Whether you declare a component as a function or a class, it must never modify its own props
   
## 5.state & lifecycle     
- State is similar to props, but it is private and fully controlled by the component.
- The render method will be called each time an update happens
  - but as long as we render `<Clock />` into the same DOM node, only a single instance of the Clock class will be used. 
  - This lets us use additional features such as local state and lifecycle methods.
- While `this.props` is set up by React itself and `this.state` has a special meaning, you are free to add additional fields to the class manually if you need to store something that doesn’t participate in the data flow (like a timer ID).
- **Using State Correctly**
  - Do Not Modify State Directly
  - State Updates May Be Asynchronous
  - State Updates are Merged
    - React merges the object you provide into the current state.
- Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn’t care whether it is defined as a function or a class.
- This is why state is often called local or encapsulated. 
  - It is not accessible to any component other than the one that owns and sets it.
- A component may choose to pass its state down as props to its child components
- This is commonly called a “top-down” or “unidirectional” data flow. 
  - Any state is always owned by some specific component
  - and any data or UI derived from that state can only affect components “below” them in the tree.
- 如果需要存储不用于视觉输出的东西，则可以手动向类中添加不同于props和state的其他字段，如果你不在render()中使用某些东西，它就不应该在状态中
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

## 6.handling events      
- Handling events with React elements is very similar to handling events on DOM elements. 
- There are some syntax **differences**:
  - React events are named using camelCase, rather than lowercase.
  - With JSX you pass a function as the event handler, rather than a string.
  - Another difference is that you cannot use `return false` to prevent default behavior in React. 
    - You must call `preventDefault` explicitly.
- In react events, `e` is a synthetic event. React defines these synthetic events according to the W3C spec, so you don’t need to worry about cross-browser compatibility. 
- When using React, you generally don’t need to call `addEventListener` to add listeners to a DOM element after it is created. 
  - Instead, just provide a listener when the element is initially rendered.
- it is common to want to pass an extra parameter to an event handler. 
  ```
  <button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
  <button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
  ```
  - In both cases, the `e` argument representing the React event will be passed as a second argument after the ID. 
  - With an arrow function, we have to pass it explicitly, but with bind any further arguments are automatically forwarded.
- 必须谨慎对待JSX回调函数中的this，类的方法默认不会绑定this，需要在constructor()中绑定`this.handleClick = this.handleClick.bind(this);`
- 不使用bind()的方式，参考 https://reactjs.org/docs/handling-events.html
	- 定义handleClick时使用箭头函数
	- 在jsx中调用时使用箭头函数`<button onClick={(e) => this.handleClick(e)}>`
		- 这种方式的缺点是，每次渲染button都会创建一个不同的回调函数
    - 不推荐这种方式，推荐使用前两种
- 向事件处理程序传递参数的方法的例子，上面两个例子中，参数`e`作为React事件对象将会被作为第二个参数进行传递
  - 通过箭头函数的方式，事件对象必须显式的进行传递
  - 但是通过bind的方式，事件对象以及更多的参数将会被隐式的进行传递
  - 通过bind方式向监听函数传参，在类组件中定义的监听函数，事件对象e要排在所传递参数的后面

## 7.conditional rendering   
- In React, you can create distinct components that encapsulate behavior you need. 
  - Then, you can render only some of them, depending on the state of your application.
- Conditional rendering in React works the same way conditions work in JavaScript. 
  - Use JavaScript operators like `if` or the conditional operator to create elements representing the current state, and let React update the UI to match them.
- You can **use variables to store elements**. 
  - This can help you conditionally render a part of the component while the rest of the output doesn’t change.
- In JavaScript, `true && expression` always evaluates to `expression`, and `false && expression` always evaluates to `false`.
  - Therefore, if the condition is true, the element right after `&&` will appear in the output. 
  - If it is false, React will ignore and skip it.
- remember that whenever conditions become too complex, it might be a good time to extract a component
- In rare cases you might want a component to hide itself even though it was rendered by another component. 
  - To do this `return null` instead of its render output.
- Returning null from a component’s render method does not affect the firing of the component’s lifecycle methods. 
  - For instance componentDidUpdate will still be called.
- 三目条件运算符可以用来渲染小段文本，用在较大的表达式中不直观
- 在组件的render()中`return null`，也是实现条件渲染的一种方法
  - If a component `return null` in its render function, why componentDidMount is triggered?
    - componentDidMount() will fire exactly after render()! so you're saying that your render function returns null, which means render function executes

## 8.lists & keys   
- You can build collections of elements and include them in JSX using curly braces `{}`
- you’ll be given a warning that a key should be provided for list items. 
  - A `key` is a special string attribute you need to include when creating lists of elements. 
- Keys help React identify which items have changed, are added, or are removed. 
  - Keys should be given to the elements inside the array to give the elements a stable identity
  - Keys only make sense in the context of the surrounding array.
  - A good rule of thumb is that **elements inside the map() call need keys**.
- The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. 
  - Most often you would use IDs from your data as keys
  - When you don’t have stable IDs for rendered items, you may use the item index as a key as a last resort
  - We *don’t recommend* using indexes for keys if the order of items may change. 
    - This can negatively impact performance and may cause issues with component state.
  - If you choose not to assign an explicit key to list items, then React will default to using indexes as keys.
- Keys used within arrays should be unique among their siblings. 
  - However they don’t need to be globally unique. 
  - We can use the same keys when we produce two different arrays
- Keys serve as a hint to React but they don’t get passed to your components. 
  - If you need the same value in your component, pass it explicitly as a prop with a different prop name
- Keep in mind that if the `map()` body is too nested, it might be a good time to extract a component.
- 元素的key只有在它和它的兄弟节点对比时才有意义	
	- 如果你提取出一个ListItem组件，你应该把key保存在数组中的这个<`ListItem />`元素上，而不是放在ListItem组件中的`<li>`元素上。
- key会作为给React的提示，但不会传递给你的组件，如果您的组件中需要使用和key相同的值，请将其作为属性传递
	- 不能使用props.key来获取key

## 9.forms   
- HTML form elements work a little bit differently from other DOM elements in React
  - because **form elements naturally keep some internal state**.   
  ```
  <form>
    <label>
      Name:
      <input type="text" name="name" />
    </label>
    <input type="submit" value="Submit" />
  </form>
  ```
- This form has the default HTML form behavior of browsing to a new page when the user submits the form. 
  - If you want this behavior in React, it just works. 
  - But in most cases, it’s convenient to have a JavaScript function that handles the submission of the form and has access to the data that the user entered into the form.
  - The standard way to achieve this is with a technique called **controlled components**.
- With a controlled component, the input’s value is always driven by the React state. 
  - While this means you have to type a bit more code, you can now pass the value to other UI elements too, or reset it from other event handlers.
- Overall, this makes it so that `<input type="text">`, `<textarea>`, and `<select>` all work very similarly 
  - they all accept a `value` attribute that you can use to implement a controlled component.
- In HTML, an `<input type="file">` lets the user choose one or more files from their device storage to be uploaded to a server or manipulated by JavaScript via the `File` API.
  - Because its value is read-only, it is an **uncontrolled component** in React
- When you need to handle multiple controlled input elements
  - you can add a `name` attribute to each element 
  - and let the handler function choose what to do based on the value of `event.target.name`
- It can sometimes be tedious to use controlled components
  - because you need to write an event handler for every way your data can change and pipe all of the input state through a React component. 
  - you might want to check out uncontrolled components, an alternative technique for implementing input forms.
-  a complete solution for form
  - validation
  - track values
  - handle submit
- 用react表示主要表单元素
	- `<textarea>`用value属性表示内容，而不用节点内的text
	- `<select>`用value属性表示选中项的值，而不用selected这个boolean属性
- input file是非受控组件
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
- 有时使用受控组件可能很繁琐，因为要为数据可能发生变化的每一种方式都编写一个事件处理程序，并通过一个组件来管理全部的状态。
- 过于繁琐时，考虑使用非受控组件

## 10.lifting state up    
- Often, several components need to reflect the same changing data. 
  - We recommend **lifting the shared state up to their closest common ancestor**.
- Components independently keep their values in the local state
  - However, we may **want these two inputs to be in sync** with each other. 
- In React, sharing state is accomplished by moving it up to the closest common ancestor of the components that need it. 
  - This is called “lifting state up”. 
  - We will remove the local state from the TemperatureInput and move it into the Calculator instead.
  - It can instruct them both to have values that are consistent with each other.
  - Since the props of both TemperatureInput components are coming from the same parent Calculator component, the two inputs will always be in sync.
- Just like the DOM `<input>` accepts both a `value` and an `onChange` prop
  - so can the custom TemperatureInput accept both temperature and onTemperatureChange props from its parent Calculator.
- There should be a single “source of truth” for any data that changes in a React application. 
  - Usually, the state is first added to the component that needs it for rendering. 
  - Then, if other components also need it, you can lift it up to their closest common ancestor. 
  - Instead of trying to sync the state between different components, you should rely on this top-down data flow.
- Lifting state involves writing more “boilerplate” code than two-way binding approaches
  - but as a benefit, it takes less work to find and isolate bugs
  - Since any state “lives” in some component and that component alone can change it, the surface area for bugs is greatly reduced. 
  - Additionally, you can implement any custom logic to reject or transform user input.
- If something can be derived from either props or state, it probably shouldn’t be in the state.

## 11.composition vs inheritance
- we recommend using composition instead of inheritance to reuse code between components.
- **Containment** 使用组合处理组件间的包含关系
- Some components don’t know their children ahead of time. 
  - This is especially common for components like Sidebar or Dialog that represent generic “boxes”.
  - We recommend that such components use the special `children` prop to pass children elements directly into their output
  - Anything inside the` <FancyBorder>` JSX tag gets passed into the `FancyBorder` component as a children prop. 
- Sometimes you might need multiple “holes” in a component. 
  - In such cases you may come up with your own convention instead of using `children` prop
  - React elements are just objects, so you can pass them as props like any other data. 
  - This approach may remind you of “slots” in other libraries 
  - but there are no limitations on what you can pass as props in React.
- **Specialization** 使用组合处理组件间的泛化关系
- In React, this is also achieved by composition
  - where a more “specific” component renders a more “generic” one and configures it with props  
```
function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}
```
- At Facebook, we use React in thousands of components
  - and we haven’t found any use cases where we would recommend creating component inheritance hierarchies.
- Props and composition give you all the flexibility you need to customize a component’s look and behavior in an explicit and safe way. 
- Remember that **components may accept arbitrary props**, including primitive values, React elements, or functions.
- If you want to reuse non-UI functionality between components, we suggest extracting it into a separate JavaScript module. 
  - The components may import it and use that function, object, or a class, without extending it.   
- 有时你可能需要在组件中有多个入口，这种情况下你可以使用自己约定的属性而不是children     
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
- 如果要在组件之间复用UI无关的功能，建议将其提取到单独的JavaScript模块中

## 12.thinking in react    
- **Start With A Mock**
  - Imagine that we already have a JSON API and a mock from our designer.
- **Step 1: Break The UI Into A Component Hierarchy**
  - The first thing you’ll want to do is to draw boxes around every component (and subcomponent) in the mock and give them all names. 
  - If you’re working with a designer, they may have already done this, so go talk to them! 
  - Their Photoshop layer names may end up being the names of your React components
  - how do you know what should be its own component? 
    - Use the same techniques for deciding if you should create a new function or object. 
    - One such technique is the single responsibility principle, that is, a component should ideally only do one thing. 
    - If it ends up growing, it should be decomposed into smaller subcomponents.
  - Since you’re often displaying a JSON data model to a user, you’ll find that if your model was built correctly, your UI (and therefore your component structure) will map nicely. 
    - That’s because UI and data models tend to adhere to the same information architecture. Separate your UI into components, where each component matches one piece of your data model.
  - Components that appear within another component in the mock should appear as a child in the hierarchy
- **Step 2: Build A Static Version in React**
  - The easiest way is to build a version that takes your data model and renders the UI but has no interactivity. 
  - It’s best to decouple these processes because building a static version requires a lot of typing and no thinking, and adding interactivity requires a lot of thinking and not a lot of typing
  - To build a static version of your app that renders your data model, you’ll want to build components that reuse other components and pass data using props. 
    - don’t use state at all to build this static version
    - State is reserved only for interactivity, that is, data that changes over time
  - You can build top-down or bottom-up.
    - In simpler examples, it’s usually easier to go top-down
    - On larger projects, it’s easier to go bottom-up and write tests as you build
  - At the end of this step, you’ll have a library of reusable components that render your data model. 
    - The components will only have `render()` methods since this is a static version of your app. 
    - The component at the top of the hierarchy will take your data model as a prop. 
    - If you make a change to your underlying data model and call `ReactDOM.render()` again, the UI will be updated. 
    - You can see how your UI is updated and where to make changes. 
    - React’s one-way data flow (also called one-way binding) keeps everything modular and fast.
- **Step 3: Identify The Minimal (but complete) Representation Of UI State**
  - To make your UI interactive, you need to be able to trigger changes to your underlying data model. 
    - React achieves this with state.
  - To build your app correctly, you first need to think of the minimal set of mutable state that your app needs. 
    - The key here is DRY: Don’t Repeat Yourself.
  - Think of all of the pieces of data in our example application. 
  - Go through each one and figure out which one is state. Ask three questions about each piece of data:
    - Is it passed in from a parent via props? If so, it probably isn’t state.
    - Does it remain unchanged over time? If so, it probably isn’t state.
    - Can you compute it based on any other state or props in your component? If so, it isn’t state.
- **Step 4: Identify Where Your State Should Live**
  - we need to identify which component mutates, or owns, this state.
  - It may not be immediately clear which component should own what state.
  - Remember: React is all about one-way data flow down the component hierarchy. 
  - Follow these steps to figure it out. For each piece of state in your application
    - Identify every component that renders something based on that state.
    - Find a common owner component (a single component above all the components that need the state in the hierarchy).
    - Either the common owner or another component higher up in the hierarchy should own the state.
    - If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
    - You can start seeing how your application will behave: set `filterText` to "ball" and refresh your app. You’ll see that the data table is updated correctly.
- **Step 5: Add Inverse Data Flow**
  - So far, we’ve built an app that renders correctly as a function of props and state flowing down the hierarchy. 
  - Now it’s time to support data flowing the other way
    - the form components deep in the hierarchy need to update the state in ancestor component FilterableProductTable.
    - We want to make sure that whenever the user changes the form, we update the state to reflect the user input. 
    - Since components should only update their own state, FilterableProductTable will pass callbacks to SearchBar that will fire whenever the state should be updated. 
    - We can use the onChange event on the inputs to be notified of it. 
    - The callbacks passed by FilterableProductTable will call `setState()`, and the app will be updated.
- 使用react创建应用的一般思路： 
0. 准备：原型图和json数据接口  
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



