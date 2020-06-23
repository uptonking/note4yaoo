---
tags: [docs, react]
title: read-docs-react-p4-faq
created: '2020-06-23T07:27:08.496Z'
modified: '2020-06-23T07:34:38.825Z'
---

# read-docs-react-p4-faq

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


