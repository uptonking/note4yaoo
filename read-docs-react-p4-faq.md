---
tags: [docs, react]
title: read-docs-react-p4-faq
created: '2020-06-23T07:27:08.496Z'
modified: '2020-06-25T17:55:34.129Z'
---

# read-docs-react-p4-faq

## AJAX and APIs

- how to make an ajax call
	- jQuery `$.ajax()`
	- window.fetch()
	- axios
- where to make an ajax call
	- componentDidMount()

## Babel, JSX, and Build Steps

- react without es6
- react without jsx

## Passing Functions to Components

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

## Component State

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
	

## Styling and CSS

- className
- CSS classes are generally better for performance than inline styles.
- “CSS-in-JS” refers to a pattern where CSS is composed using JavaScript instead of defined in external files.
- React can be used to power animations. See React Transition Group and React Motion

## File Structure

- Grouping by features or routes
- Grouping by file type
- Avoid too much nesting
- don't spend more than 5 minutes on choosing a file structure.

## Versioning Policy

- React follows semantic versioning (semver) principles with a version number x.y.z:
	- When releasing breaking changes, we make a major release by changing the x number (ex: 15.6.2 to 16.0.0).
	- When releasing new features, we make a minor release by changing the y number (ex: 15.6.2 to 15.7.0).
	- When releasing bug fixes, we make a patch release by changing the z number (ex: 15.6.2 to 15.6.3).

## Virtual DOM and Internals

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



