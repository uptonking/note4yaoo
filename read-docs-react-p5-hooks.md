---
tags: [docs, react]
title: read-docs-react-p5-hooks
created: '2020-06-23T07:26:09.551Z'
modified: '2020-06-23T07:34:45.376Z'
---

# read-docs-react-p5-hooks


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


