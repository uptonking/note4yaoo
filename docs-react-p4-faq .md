---
tags: [docs, faq, react]
title: docs-react-p4-faq
created: '2020-06-23T07:27:08.496Z'
modified: '2020-06-30T05:14:08.093Z'
---

# docs-react-p4-faq

# AJAX and APIs

- how to make an ajax call
  - Some popular ones are Axios, jQuery AJAX, and the browser built-in `window.fetch` .
- where to make an ajax call
	- componentDidMount()
  - This is so you can use `setState` to update your component when the data is retrieved.

# Babel, JSX, and Build Steps

- react without es6
- react without jsx

# Passing Functions to Components

- How to pass an event handler (like `onClick` ) to a component
	- Pass event handlers and other functions as props to child components:
	- If you need to have access to the parent component in the handler, you also need to bind the function to the component instance
- Why is binding necessary at all?
  - `this` is a property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object and in strict mode can be any value.
  - In most cases, the value of `this` is determined by how a function is called (runtime binding). 
  - It can't be set by assignment during execution, and it may be different each time the function is called. 
  - ES5 introduced the `bind()` method to set the value of a function's this regardless of how it's called
  - and ES2015 introduced arrow functions which don't provide their own `this` binding (it retains the `this` value of the enclosing lexical context).
  - In the global execution context (outside of any function), `this` refers to the global object whether in strict mode or not.
    - You can always easily get the global object using the global `globalThis` property, regardless of the current context in which your code is running
    - In web browsers, the `window` object is also the global object
  - Inside a function, the value of this depends on how the function is called.

``` js
    function f1() {
      return this;
    }
```

    - In Non-strict mode, `this` will default to the global object, which is `window` in a browser
    - In strict mode, however, if the value of `this` is not set when entering an execution context, it remains as `undefined`
    - To set the value of this to a particular value when calling a function, use `call()` , or `apply()`
    - When a function is used as a constructor (with the `new` keyword), its `this` is bound to the new object being constructed.
  - The behavior of `this` in classes and functions is similar, since classes are functions under the hood.
    - Within a class constructor, `this` is a regular object. All non-static methods within the class are added to the prototype of `this`
    - Static methods are not properties of this. They are properties of the class itself.
  - Unlike base class constructors, derived constructors have no initial `this` binding. 
    - Calling `super()` creates a `this` binding within the constructor and essentially has the effect of evaluating `this = new Base();`
    - Referring to this before calling `super()` will throw an error.
- How do I bind a function to a component instance
  - With React, typically you only need to bind the methods you pass to other components.
	- There are several ways to make sure functions have access to component attributes like `this.props` and `this.state`
	- Bind in Constructor (ES2015)

``` js
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

	- Class Properties (Stage 3 Proposal)  
    - 推荐使用这种写法，不用在render中绑定

``` js
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
      - **Using `Function.prototype.bind` in render creates a new function each time the component renders**, which may have performance implications

``` js
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

``` js
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
  -  Passing params using the DOM API `data-*` attributes
    - Consider this approach if you need to optimize a large number of elements or have a render tree that relies on React.PureComponent equality checks.
- How to prevent a function from being called too quickly or too many times in a row
	- If you have an event handler such as onClick or onScroll and want to prevent the callback from being fired too quickly, then you can limit the rate
	- throttling: sample changes based on a time based frequency (eg `_.throttle` )
	- debouncing: publish changes after a period of inactivity (eg `_.debounce` )
	- requestAnimationFrame throttling: sample changes based on requestAnimationFrame (eg `raf-schd` )
	- _.debounce, _.throttle and raf-schd provide a `cancel` method to cancel delayed callbacks. 
	  - You should either call this method from componentWillUnmount or check to ensure that the component is still mounted within the delayed function. 
- Throttling prevents a function from being called more than once in a given window of time. 
- Debouncing ensures that a function will not be executed until after a certain amount of time has passed since it was last called. T
- requestAnimationFrame is a way of queuing a function to be executed in the browser at the optimal time for rendering performance.
  - A function that is queued with requestAnimationFrame will fire in the next frame
  - The browser will work hard to ensure that there are 60 frames per second (60 fps). 
  - A device might only be able to handle 30 fps and so you will only get 30 frames in that second.
  - Using requestAnimationFrame for throttling is a useful technique in that it prevents you from doing more than 60 updates in a second.
  - Using this technique will only capture the last published value in a frame.
- When testing your rate limiting code works correctly it is helpful to have the ability to fast forward time. 
  - If you are using jest then you can use mock timers to fast forward time.

# Component State

- props vs state
  - `props` and `state` are both plain JavaScript objects
  - `props` get passed to the component (similar to function parameters) whereas `state` is managed within the component (similar to variables declared within a function).
  - ref
    - https://github.com/uberVU/react-guide/blob/master/props-vs-state.md
    - https://lucybain.com/blog/2016/react-state-vs-pros/
- Why is setState giving me the wrong value?  
	- Calls to `setState` are asynchronous
  - don’t rely on `this.state` to reflect the new value immediately after `calling setState`
	- If you need to compute values based on the current state , pass an updater function instead of an object  to setState()
	- pass an object    

``` js
    incrementCount() {
      // Note: this will not work as intended.
      this.setState({ count: this.state.count + 1 });
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

	- Passing an updater function allows you to access the current state value inside the updater. 
    - Pass a function instead of an object to setState to ensure the call always uses the most updated version of state
    - Since setState calls are batched, this lets you chain updates and ensure they build on top of each other instead of conflicting  

	```js
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

- Currently, `setState` is asynchronous inside event handlers.
	- This ensures, for example, that if both Parent and Child call setState during a click event, Child isn't re-rendered twice.  
  - Instead, React “flushes” the state updates at the end of the browser event
	- In the future versions, React will batch updates by default in more cases.
- React intentionally “waits” until all components call setState() in their event handlers before starting to re-render. This boosts performance by avoiding unnecessary re-renders.
- Why doesn’t React update `this.state` synchronously?
  - why React doesn’t just update `this.state` immediately without re-rendering.
    - https://github.com/facebook/react/issues/11527#issuecomment-360199710
  - This would break the consistency between props and state, causing issues that are very hard to debug.
    - Even if state is updated synchronously, props are not. 
    - You can’t know props until you re-render the parent component
    - if you do this synchronously, batching goes out of the window.
    - we can’t immediately flush this.props without re-rendering the parent, which means we would have to give up on batching 
    - Right now the objects provided by React (state, props, refs) are internally consistent with each other. This means that if you only use those objects, they are guaranteed to refer to a fully reconciled tree(even if it’s an older version of that tree)
    - In React, both this.state and this.props update only after the reconciliation and flushing, so you would see 0 being printed both before and after refactoring. This makes lifting state up safe
  - This would make some of the new features(Concurrent Updates) we’re working on impossible to implement.
    - React could assign different priorities to setState() calls depending on where they’re coming from: an event handler, a network response, an animation, etc.

# Styling and CSS

- className
- Are inline styles bad?
  - CSS classes are generally better for performance than inline styles.
- “CSS-in-JS” refers to a pattern where CSS is composed using JavaScript instead of defined in external files.
- React does not have an opinion about how styles are defined; if in doubt, a good starting point is to define your styles in a separate `*.css` file as usual and refer to them using `className` .
- React can be used to power animations. See React Transition Group and React Motion

# File Structure

- Grouping by features or routes
  - locate CSS, JS, and tests together inside folders 
- Grouping by file type
- Avoid too much nesting
- Don't spend more than 5 minutes on choosing a file structure.
  - If you feel completely stuck, start by keeping all files in a single folder. 
  - Eventually it will grow large enough that you will want to separate some files from the rest.
  - By that time you’ll have enough knowledge to tell which files you edit together most often. 
  - In general, it is a good idea to keep files that often change together close to each other. 
  - This principle is called “colocation”.
  - As projects grow larger, they often use a mix of both of the above approaches in practice. 
  - So choosing the “right” one in the beginning isn’t very important.

# Versioning Policy

- React follows semantic versioning (semver) principles with a version number x.y.z:
	- When releasing breaking changes, we make a major release by changing the x number (ex: 15.6.2 to 16.0.0).
    - Major releases can also contain new features, and any release can include bug fixes.
	- When releasing new features, we make a minor release by changing the y number (ex: 15.6.2 to 15.7.0).
	- When releasing bug fixes, we make a patch release by changing the z number (ex: 15.6.2 to 15.6.3).
- What Counts as a Breaking Change?
  - In general, we don’t bump the major version number for changes to:
  - Development warnings.
  - APIs starting with unstable_.
  - Alpha and canary versions of React
  - Undocumented APIs and internal data structures

# Virtual DOM and Internals

- The **virtual DOM(VDOM)** is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. 
  - This process is called reconciliation.
- VDOM is more of a pattern than a specific technology
- In React world, the term “virtual DOM” is usually associated with React elements since they are the objects representing the user interface. 
- React, however, also uses internal objects called “fibers” to hold additional information about the component tree. They may also be considered a part of “virtual DOM” implementation in React.
- The **Shadow DOM** is a browser technology designed primarily for scoping variables and CSS in web components.
  - Shadow DOM允许在document渲染时插入一棵DOM元素子树，但这棵子树不在主DOM树中。
  - 例如video标签下面会有 `# shadow root`
  - The Virtual DOM is a concept implemented by libraries in JavaScript on top of browser APIs.
- Fiber is the new reconciliation engine in React 16. 
  - Its main goal is to enable incremental rendering of the virtual DOM. 
