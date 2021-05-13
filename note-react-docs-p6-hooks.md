---
title: note-react-docs-p6-hooks
tags: [docs, hooks, react]
created: '2020-06-23T07:26:09.551Z'
modified: '2021-05-13T03:46:18.143Z'
---

# note-react-docs-p6-hooks

# Introducing Hooks

- Hooks are JavaScript functions letting you use state and other React features without writing a class. 
  - React 16.8.0 is the first release to support Hooks
- Hooks are completely opt-in. You don't have to use it if you don't want to.
- Hooks are 100% backwards-compatible. Hooks don’t contain any breaking changes.
- There are no plans to remove classes from React. 
- Hooks don’t replace your knowledge of React concepts.
- Motivation
	- It's hard to reuse stateful logic between components
    - React doesn’t offer a way to “attach” reusable behavior to a component (for example, connecting it to a store). 
		- render props and higher-order components try to solve this.
		- But these patterns require you to restructure your components when you use them
      - which can be cumbersome and make code harder to follow.
		- If you look at a typical React application in React DevTools, you will likely find a “wrapper hell” of components surrounded by layers of providers, consumers, higher-order components, render props, and other abstractions. 
		- With Hooks, you can extract stateful logic from a component so it can be tested independently and reused. 
		- **Hooks allow you to reuse stateful logic without changing your component hierarchy**. 
	- Complex components become hard to understand
		- Each lifecycle method often contains a mix of unrelated logic. 
    - Mutually related code(add and remove listener) that changes together gets split apart, but completely unrelated code(data fetch and add listener) ends up combined in a single method. 
    - In many cases it’s not possible to break these components into smaller ones because the stateful logic is all over the place. 
      - It’s also difficult to test them. 
      - This is one of the reasons many people prefer to combine React with a separate state management library. 
		  - However, that often introduces too much abstraction, requires you to jump between different files, and makes reusing components more difficult.
		- **Hooks let you split one component into smaller functions based on what pieces are related** (such as setting up a subscription or fetching data), rather than forcing a split based on lifecycle methods. 
    - You may also opt into managing the component’s local state with a reducer to make it more predictable.
	- Classes confuse both people and machines
    - You have to understand how `this` works in js, and bind the event handlers.
		- To make React stays relevant in the next five years using AOT compilation
      - class components can encourage unintentional patterns that make these optimizations fall back to a slower path
		- Classes present issues for today’s tools, too. 
      - For example, classes don’t minify very well
      - they make hot reloading flaky and unreliable.
		- **Hooks let you use more of React's features without classes**, but with functions.
- Gradual Adoption Strategy
	- There are no plans to remove classes from React.
  - Hooks work side-by-side with existing code so you can adopt them gradually.
	- We intend for Hooks to cover all existing use cases for classes
	- we will keep supporting class components for the foreseeable future.

# Hooks at a Glance

``` js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times` ;
  });

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

- State Hook
  - You can declare multiple state variables
  - Hooks are functions that let you "hook into" React state and lifecycle features from function components.
  - Hooks don't work inside classes - they let you use React without classes
  - React provides a few built-in Hooks like `useState` . 
  - You can also create your own Hooks to reuse stateful behavior between different components.
- Effect Hook
  - You've likely performed data fetching, subscriptions, or manually changing the DOM from React components before. 
  - We call these operations **side effects** (or "effects" for short) because they can affect other components and can't be done during rendering.
  - `useEffect` Hook adds the ability to perform side effects from a function component. 
  - It serves the same purpose as `componentDidMount` , `componentDidUpdate` , and `componentWillUnmount` in React classes, but unified into a single API.
  - When you call `useEffect` , you’re telling React to run your “effect” function after flushing changes to the DOM. 
  - Effects are declared inside the component so they have access to its props and state. 
  - By default, React runs the effects after every render - including the first render.
  - You can use more than a single effect in a component
- Rules of Hooks
- Building Your Own Hooks
	- Sometimes, we want to reuse some stateful logic between components. 
	- Traditionally, there were two popular solutions to this problem: higher-order components and render props. 
	- Custom Hooks let you do this, but without adding more components to your tree.
  - Hooks are a way to reuse stateful logic, not state itself. 
  - In fact, each call to a Hook has a completely isolated state
    - so you can even use the same custom Hook twice in one component.
  - If a function’s name starts with ”use” and it calls other Hooks, we say it is a custom Hook.
- Other Hooks
	- useContext
	- useReducer

# Using the State Hook

- A Hook is a special function that lets you “hook into” React features. 
- For example, `useState` is a Hook that lets you add React state to function components. 
- In a function component, we have no `this` , so we can’t assign or read `this.state` .
- `useState` Hook is a new way to use the exact same capabilities that `this.state` provides in a class.
  - It declares a new *state variable*. 
  - This is a way to “preserve” some values between the function calls 
  - It lets us keep local state in a function component.
  - Normally, variables “disappear” when the function exits, but state variables are preserved by React.
- The only argument to the `useState()` Hook is the initial state. 
  - Unlike with classes, the state doesn’t have to be an object. We can also keep a number or a string 
- `useState` returns a pair of values: the current state and a function that updates it. 
  - This is why we write `const [count, setCount] = useState(0)` . 
  - This is similar to `this.state.count` and `this.setState` in a class
- React will remember state's current value between re-renders, and provide the most recent one to our function
  - state is only created the first time our component renders.
  - During the next renders, useState gives us the current state. 
- When we declare a state variable with `useState` , it returns a pair - an array with two items. 
  - The first item is the current value, and the second is a function that lets us update it.
  - Using `[0]` and `[1]` to access them is a bit confusing because they have a specific meaning. 
  - This is why we use array destructuring instead.
- You can use multiple state variables
  - we can update them individually
  - You don’t have to use many state variables. 
- State variables can hold objects and arrays just fine, so you can still group related data together. 
- Unlike `this.setState` in a class, **updating a state variable always replaces it** instead of merging it.

# Using the Effect Hook

- `useEffect` Hook lets you perform side effects in function components
  - Data fetching, setting up a subscription, and manually changing the DOM in React components are all examples of side effects (or just “effects”). 
  - You can think of useEffect Hook as `componentDidMount` , `componentDidUpdate` , and `componentWillUnmount` combined.
- There are two common kinds of side effects in React components: those that don’t require cleanup, and those that do
- Effects Without Cleanup
  - Sometimes, we want to run some additional code after React has updated the DOM. 
  - Network requests, manual DOM mutations, and logging are common examples of effects that don’t require a cleanup. 
- In React class components, the `render` method itself shouldn’t cause side effects. 
  - It would be too early - we typically want to perform our effects after React has updated the DOM.
  - We often put side effects into componentDidMount and componentDidUpdate
  - we have to duplicate the code
- `useEffect` tells React that your component needs to do something after render.
  - React will remember the function you passed (we’ll refer to it as our “effect”)
    - and call it later after performing the DOM updates. 
  - In the effect, we could change the DOM, perform data fetching or call some other imperative API.
  - Placing `useEffect` inside the component lets us access its state variable (or any props) right from the effect. 
  - Hooks embrace JavaScript closures and avoid introducing React-specific APIs where JavaScript already provides a solution
  - `useEffect` runs both after the first render and after every update. 
  - Instead of thinking in terms of “mounting” and “updating”, you might find it easier to think that effects happen “after render”. 
  - React guarantees the DOM has been updated by the time it runs the effects.
- The function passed to `useEffect` is going to be different on every render. This is intentional. 
  - This is what lets us read the latest state value `count` from inside the effect without worrying about it getting stale. 
  - Every time we re-render, we schedule a different effect, replacing the previous one. 
  - In a way, this makes the effects behave more like a part of the render result - each effect “belongs” to a particular render
- Unlike `componentDidMount` or `componentDidUpdate` , effects scheduled with `useEffect` don’t block the browser from updating the screen.
  - The majority of effects don’t need to happen synchronously. 
  - In the uncommon cases where they do (such as measuring the layout), there is a separate `useLayoutEffect` Hook with an API identical to useEffect.
  - componentDidMount and componentDidUpdate run synchronously after rendering
- Effects with Cleanup
  - For example, we might want to set up a subscription to some external data source. 
  - It is important to clean up so that we don’t introduce a memory leak! 
- In a React class, you would typically set up a subscription in `componentDidMount/Update` , and clean it up in `componentWillUnmount` . 
  - Lifecycle methods force us to split this logic even though conceptually code in both of them is related to the same effect
- `useEffect` returns a function from our effect.
  - This is the optional cleanup mechanism for effects. 
  - Every effect may return a function that cleans up after it. 
  - This lets us keep the logic for adding and removing subscriptions close to each other. 
  - React performs the cleanup when the component unmounts. 
  - However, effects run for every render and not just once. 
  - This is why React also cleans up effects from the previous render before running the effects next time.
  - We don’t have to return a named function from the effect, an arrow function ok too.
- Use Multiple Effects to Separate Concerns
  - class lifecycle methods often contain unrelated logic, but related logic gets broken up into several methods. 
  - Just like you can use the `useState` Hook more than once, you can also use several `useEffect`
  - Hooks let us split the code based on what it is doing rather than a lifecycle method name. 
  - React will apply every effect used by the component, in the order they were specified.
- Why Effects Run on Each Update
  - This behavior ensures consistency by default and prevents bugs that are common in class components due to missing update logic.
  - What happens if the friend prop changes while the component is on the screen? 
    - Our component would continue displaying the online status of a different friend. This is a bug.
    - We would also cause a memory leak or crash when unmounting since the unsubscribe call would use the wrong friend ID.
  - In a class component, we would need to add `componentDidUpdate` to handle this case
  - There is no special code for handling updates because `useEffect` handles them by default.
  - It cleans up the previous effects before applying the next effects. 
- Optimizing Performance by Skipping Effects
  - In some cases, cleaning up or applying the effect after every render might create a performance problem.
  - In class components, we can solve this by writing an extra comparison with prevProps or prevState inside componentDidUpdate
  - You can tell React to skip applying an effect if certain values haven’t changed between re-renders. 
  - To do so, pass an array as an optional second argument to useEffect
  - If all items in the array are the same (5 === 5), React would skip the effect. 
  - This also works for effects that have a cleanup phase
  - In the future, the second argument might get added automatically by a build-time transformation.
  - If you use this optimization, make sure the array includes all values from the component scope (such as props and state) that change over time and that are used by the effect.
  - Otherwise, your code will reference stale values from previous renders. 
  - If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array ( `[]` ) 
  - If you pass an empty array ( `[]` ), the props and state inside the effect will always have their initial values
    - there are usually better solutions to avoid re-running effects too often. 
    - React defers running useEffect until after the browser has painted, so doing extra work is less of a problem.

# Rules of Hooks

- Only call Hooks at the top level
  - Don't call Hooks inside conditions, loops, or nested functions.
  - By following this rule, you ensure that Hooks are called in the same order each time a component renders. 
  - That’s what allows React to correctly preserve the state of Hooks between multiple `useState` and `useEffect` calls
- Only call Hooks from React functions
  - Don't call Hooks from regular JavaScript functions. 
  - Call Hooks from React function components.
  - Call Hooks from custom Hooks 
  - By following this rule, you ensure that all stateful logic in a component is clearly visible from its source code.
- How does React know which state corresponds to which `useState` call? 
  - React relies on the order in which Hooks are called. 
  - Our example works because the order of the Hook calls is the same on every render
  - As long as the order of the Hook calls is the same between renders, React can associate some local state with each of them. 
  - If the order of the Hook calls becomes different, skip one useState for example , from that point, every next Hook call after the one we skipped would also shift by one, leading to bugs.
  - This is why Hooks must be called on the top level of our components.
  - If we want to run an effect conditionally, we can put that condition inside our Hook function

# Building Your Own Hooks

- Building your own Hooks lets you extract component logic into reusable functions.
- When we want to share logic between two JavaScript functions, we extract it to a third function. 
- Both components and Hooks are functions, so this works for them too!
- **A custom Hook is a JavaScript function whose name starts with `use` and that may call other Hooks**.
  - You can decide what it takes as arguments, and what, if anything, it should return.
  - It’s just like a normal function
- Make sure to only call other Hooks unconditionally at the top level of your custom Hook
- All we did was to extract some common code between two functions into a separate function. 
- Custom Hooks are a convention that naturally follows from the design of Hooks, rather than a React feature.
- Custom Hooks are a mechanism to reuse stateful logic (such as setting up a subscription and remembering the current value)
  - but every time you use a custom Hook, **all state and effects inside of it are fully isolated**.
- Each call to a Hook gets isolated state. 
  - Because we call `useFriendStatus` custom Hook directly
  - From React’s point of view, our component just calls `useState` and `useEffect` . 
  - We can call useState and useEffect many times in one component, and they will be completely independent.
- Since Hooks are functions, we can pass information between them.
  - Because the useState Hook call gives us the latest value of the recipientID state variable, we can pass it to our custom useFriendStatus Hook as an argument
  - If we pick a different friend and update the recipientID state variable, our useFriendStatus Hook will unsubscribe from the previously selected friend, and subscribe to the status of the newly selected one.
- You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven’t considered.
- It’s likely that the average function component in your codebase will become longer. 
  - This is normal - don’t feel like you have to immediately split it into Hooks. 
  - But we also encourage you to start spotting cases where a custom Hook could hide complex logic behind a simple interface, or help untangle a messy component.
  - For example, maybe you have a complex component that contains a lot of local state that is managed in an ad-hoc way. 
    - `useState` doesn’t make centralizing the update logic any easier 
    - so you might prefer to write it as a Redux reducer
    - Reducers are very convenient to test in isolation, and scale to express complex update logic.
    - You can further break them apart into smaller reducers if necessary. 
    - However, you might also enjoy the benefits of using React local state, or might not want to install another library.

# Hooks FAQ

- **Adoption Strategy**
- Starting with 16.8.0, React includes a stable implementation of React Hooks for:
  - React DOM
  - React Native
  - React DOM Server
  - React Test Renderer
  - React Shallow Renderer
  - To enable Hooks, all React packages need to be 16.8.0 or higher
- What can I do with Hooks that I couldn’t with classes?
  - https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889
- Should I use Hooks, classes, or a mix of both?
  - We don't recommend rewriting your existing classes to Hooks
  - You can't use Hooks inside of a class component, but you can definitely mix classes and function components with Hooks in a single tree. 
  - Whether a component is a class or a function that uses Hooks is an implementation detail of that component. 
  - In the longer term, we expect Hooks to be the primary way to write React components.
- Do Hooks cover all use cases for classes?
  - Our goal is for Hooks to cover all use cases for classes as soon as possible. 
  - There are no Hook equivalents to the uncommon `getSnapshotBeforeUpdate` , `getDerivedStateFromError` and `componentDidCatch` lifecycles yet, but we plan to add them soon.
  - It is an early time for Hooks, so some integrations like DevTools support、FLow、TypeScript、3rd-party libraries  might be incompatible
- Do Hooks replace render props and higher-order components?
  - Often, render props and higher-order components render only a single child. We think Hooks are a simpler way to serve this use case.
  - There is still a place for both patterns (for example, a virtual scroller component might have a renderItem prop, or a visual container component might have its own DOM structure).
  - But in most cases, Hooks will be sufficient and can help reduce nesting in your tree.
- What do Hooks mean for popular APIs like Redux `connect()` and React Router?
  - You can continue to use the exact same APIs as you always have; they'll continue to work.
  - In the future, new versions of these libraries might also export custom Hooks such as useRedux() or useRouter() that let you use the same features without needing wrapper components.
  - Other libraries might support hooks in the future too.
- Do Hooks work with static typing?
  - Flow and TypeScript teams plan to include definitions for React Hooks in the future.
- Do Hooks work with static typing?
  - Hooks are functions, they are easier to type correctly than patterns like higher-order components. 
  - The latest Flow and TypeScript React definitions include support for React Hooks.
- How to test components that use Hooks?
  - From React’s point of view, a component using Hooks is just a regular component.
  - If your testing solution doesn’t rely on React internals, testing components with Hooks shouldn’t be different from how you normally test components.
  - To reduce the boilerplate, we recommend using React Testing Library which is designed to encourage writing tests that use your components as the end users do.

  

- **From Classes to Hooks**
- How do lifecycle methods correspond to Hooks?
  - `constructor`
    - Function components don't need a constructor. 
    - You can initialize the state in the useState call.
    - If computing it is expensive, you can pass a function to useState.
  - `getDerivedStateFromProps`
    - Schedule an update while rendering instead.
  - `shouldComponentUpdate`
    - use React.memo 
  - `render`
    - This is the function component body itself.
  - `componentDidMount` , `componentDidUpdate` , `componentWillUnmount`
    - The useEffect Hook can express all combinations of these (including less common cases).
  - `getSnapshotBeforeUpdate` , `componentDidCatch` and `getDerivedStateFromError`
    - There are no Hook equivalents for these methods yet, but they will be added soon.
- How can I do data fetching with Hooks
  - https://www.robinwieruch.de/react-hooks-fetch-data/
- Is there something like instance variables?
  - `useRef()` Hook isn’t just for DOM refs. 
  - The “ref” object is a generic container whose `current` property is mutable and can hold any value, similar to an instance property on a class.
  - avoid setting refs during rendering - this can lead to surprising behavior. 
  - Instead, typically you want to modify refs in event handlers and effects.
- Should I use one or many state variables?
  - If you're coming from classes, you might be tempted to always call useState() once and put all state into a single object
  - However, we recommend to split state into multiple state variables based on which values tend to change together.
  - Separating independent state variables also has another benefit. It makes it easy to later extract some related logic into a custom Hook
  - If the state logic becomes complex, we recommend managing it with a `useReducer` or a custom Hook.
- Can I run an effect only on updates?
  - If you need it, you can use a mutable ref to manually store a boolean value corresponding to whether you are on the first or a subsequent render, then check that flag in your effect
- How to get the previous props or state?
  - Currently, you can do it manually with a ref 
  - You can extract it into a custom Hook
  - Note how this would work for props, state, or any other calculated value.
  - It’s possible that in the future React will provide a `usePrevious` Hook out of the box since it’s a relatively common use case.
- Why am I seeing stale props or state inside my function?
  - Any function inside a component, including event handlers and effects, “sees” the props and state from the render it was created in
  - If you first click “Show alert” and then increment the counter, the alert will show the count variable at the time you clicked the “Show alert” button
  - If you intentionally want to read the latest state from some asynchronous callback, you could keep it in a ref, mutate it, and read from it.
  - Another possible reason you’re seeing stale props or state is if you use the “dependency array” optimization but didn’t correctly specify all the dependencies. 
    - The solution is to either remove the dependency array, or to fix it. 
- How do I implement `getDerivedStateFromProps` ?
  - You can update the state right during rendering.
  - React will **re-run the component with updated state immediately after exiting the first render** so it wouldn’t be expensive.
  - We can store the previous value of the prop in a state variable so that we can compare
  - This might look strange at first, but an update during rendering is exactly what `getDerivedStateFromProps` has always been like conceptually.
- Is there something like forceUpdate?
  - Both useState and useReducer Hooks bail out of updates if the next value is the same as the previous one. 
  - Mutating state in place and calling setState will not cause a re-render.
  - Normally, you shouldn’t mutate local state in React. 
  - However, as an escape hatch, you can use an incrementing counter to force a re-render even if the state has not changed
  - `const [ignored, forceUpdate] = useReducer(x => x + 1, 0);`
  - Try to avoid this pattern if possible.
- Can I make a ref to a function component?
  - You may expose some imperative methods to a parent component with the `useImperativeMethods` Hook.
- How can I measure a DOM node?
  - use a callback ref. 
  - React will call that callback whenever the ref gets attached to a different node. 
  - Using a callback ref ensures that even if a child component displays the measured node later (e.g. in response to a click), we still get notified about it in the parent component and can update the measurements.
  - We pass [] as a dependency array to useCallback. This ensures that our ref callback doesn’t change between the re-renders, and so React won’t call it unnecessarily.

- **Performance Optimizations**
- Is it safe to omit functions from the list of dependencies?
  - Generally speaking, no
  - It’s difficult to remember which props or state are used by functions outside of the effect. 
  - This is why usually you’ll want to declare functions needed by an effect inside of it.
  - It is only safe to omit a function from the dependency list if nothing in it (or the functions called by it) references props, state, or values derived from them. 
  - The recommended fix is to move that function inside of your effect.
    - That makes it easy to see which props or state your effect uses, and to ensure they’re all declared
    - This also allows you to handle out-of-order responses with a local variable inside the effect
  - If for some reason you can’t move a function inside an effect
    - You can try moving that function outside of your component.
    - If the function you’re calling is a pure computation and is safe to call while rendering, you may call it outside of the effect instead, and make the effect depend on the returned value.
    - As a last resort, you can add a function to effect dependencies but wrap its definition into the useCallback Hook. This ensures it doesn’t change on every render unless its own dependencies also change
- What can I do if my effect dependencies change too often?
  - We can **use the functional update form of `setState` **. It lets us specify how the state needs to change without referencing the current state
  - The identity of the `setCount` function is guaranteed to be stable so it’s safe to omit.
  - In more complex cases (such as if one state depends on another state), try moving the state update logic outside the effect with the useReducer Hook.
  - The identity of the dispatch function from useReducer is always stable - even if the reducer function is declared inside the component and reads its props.
  - As a last resort, if you want something like this in a class, you can use a `ref` to hold a mutable variable. Then you can write and read to it. 
- How do I implement `shouldComponentUpdate` ?
  - You can wrap a function component with `React.memo` to shallowly compare its props
  - It's not a Hook because it doesn't compose like Hooks do. 
  - `React.memo` is equivalent to `PureComponent` , but it only compares props.
  - React.memo doesn’t compare state because there is no single state object to compare. 
- How to memoize calculations?
  - `useMemo` Hook lets you cache calculations between multiple renders by "remembering" the previous computation
  - The function passed to useMemo runs during rendering. Don’t do anything there that you wouldn’t normally do while rendering. For example, side effects belong in useEffect, not useMemo.
- How to create expensive objects lazily?
  - `useMemo` lets you memoize an expensive calculation if the dependencies are the same. 
  - However, it only serves as a hint, and doesn’t guarantee the computation won’t re-run. 
  - But sometimes you need to be sure an object is only created once.
  - To avoid re-creating the ignored initial state, we can pass a function to useState
- Are Hooks slow because of creating functions in render?
  - No. In modern browsers, the raw performance of closures compared to classes doesn’t differ significantly except in extreme scenarios.
  - Hooks avoid a lot of the overhead that classes require, like the cost of creating class instances and binding event handlers in the constructor.
  - Idiomatic code using Hooks doesn't need the deep component tree nesting that is prevalent in codebases that use higher-order components, render props, and context. 
    - With smaller component trees, React has less work to do.
  - Traditionally, performance concerns around inline functions in React have been related to how passing new callbacks on each render breaks `shouldComponentUpdate` optimizations in child components. 
  - Hooks approach this problem from three sides
    - `useCallback` Hook lets you keep the same callback reference between re-renders so that shouldComponentUpdate continues to work
    - `useMemo` Hook makes it easier to control when individual children update, reducing the need for pure components.
    - `useReducer` Hook reduces the need to pass callbacks deeply
- How to avoid passing callbacks down?
  - an alternative we recommend is to pass down a `dispatch` function from `useReducer` via `useContext`
  - You can still choose whether to pass the application state down as props (more explicit) or as context (more convenient for very deep updates).
  - If you use context to pass down the state too, use two different context types - the dispatch context never changes, so components that read it don’t need to rerender unless they also need the application state.
- How to read an often-changing value from `useCallback` ?
  - We recommend to pass `dispatch` down in context rather than individual callbacks in props.
    - this pattern might cause problems in the concurrent mode.
  - In some rare cases you might need to memoize a callback with useCallback but the memoization doesn’t work very well because the inner function has to be re-created too often. 
  - If the function you’re memoizing is an event handler and isn’t used during rendering, you can use ref as an instance variable, and save the last committed value into it manually
  - It’s more bearable if you extract it to a custom Hook
  - In either case, we don’t recommend this pattern and only show it here for completeness. 
  - Instead, it is preferable to avoid passing callbacks deep down.

- **Under the Hood**
- How does React associate Hook calls with components?
  - React keeps track of the currently rendering component.
  - Hooks are only called from React components (or custom Hooks - which are also only called from React components).
  - There is an internal list of "memory cells" associated with each component. 
  - They're just JavaScript objects where we can put some data. 
  - When you call a Hook like `useState()` , it reads the current cell (or initializes it during the first render), and then moves the pointer to the next one. 
  - This is how multiple `useState()` calls each get independent local state.
- What is the prior art for Hooks?
  - Our old experiments with functional APIs in the react-future repository.
