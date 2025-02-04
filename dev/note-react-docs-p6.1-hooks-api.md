---
title: note-react-docs-p6.1-hooks-api
tags: [api, docs, hooks]
created: 2020-07-17T04:31:41.903Z
modified: 2021-05-13T03:46:22.741Z
---

# note-react-docs-p6.1-hooks-api

# Hooks API Reference

- built-in hooks(10 api)
  - useState
  - useEffect
  - useLayoutEffect
  - useContext
  - useReducer
  - useMemo
  - useCallback
  - useRef
  - useImperativeHandle
  - useDebugValue

- ## `const [state, setState] = useState(initialState); `
- Returns a stateful value, and a function to update it.
- During the initial render, the returned state ( `state` ) is the same as the value passed as the first argument ( `initialState` ).
- During subsequent re-renders, the first value returned by `useState` will always be the most recent state after applying updates.
- `useState` 基于 `useReducer` 实现
- Why does useState return array?
  - Because compared to an object, an array is more flexible and easy to use.
  - If the method returned an object with a fixed set of properties, you wouldn’t be able to assign custom names in an easy way.
  - 若使用对象，每次都要重命名
  - 如 `const { state:list, setState:setList } = useState([]); `
- `setState(newState)` function is used to update the state. 
  - It accepts a new state value and enqueues a re-render of the component
  - React guarantees that `setState` function identity is stable and won’t change on re-renders. 
    - This is why it’s safe to omit from the `useEffect` or `useCallback` dependency list.

- If the new state is computed using the previous state, you can pass a function to `setState`
  - **If your update function returns the exact same value as the current state, the subsequent rerender will be skipped completely**.
  - If you use the same value as the current state to update the state (React uses `Object.is` for comparing), React won’t trigger a re-render.
- `useState` does not automatically merge update objects. 
  - You can replicate this behavior by combining the function updater form with object spread syntax

``` js
  setState(prevState => {
    // Object.assign would also work
    return { ...prevState, ...updatedValues };
  });
```

  - Another option is `useReducer` , which is more suited for managing state objects that contain multiple sub-values
  - It's better to split the state into multiple state variables based on which values tend to change together.
  - The function returned by `useState` does not automatically merge update objects, it **replaces** them

- The `initialState` argument is the state used during the initial render. 
  - In subsequent renders, it is disregarded. 
  - If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render
  - 如果initialState为函数，则useState在初始化时会立刻执行该函数和获取函数的返回值，在没有任何返回值得情况下为undefined。
    - 这里需要注意的是每次组件re-render都会导致useState中的函数重新计算，这里可以使用闭包函数来解决问题。在优化后只有组件初始化时才会执行一遍loop函数。
  - The initial value will be assigned only on the initial render (if it’s a function, it will be executed only on the initial render).

``` JS
// useState参数为函数时，会在首次render时自动执行，只执行这一次
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});

const loop = () => {
  console.log("calc!");
  let res = 0;
  for (let i = 0, len = 1000; i < len; i++) {
    res += i;
  }
  return res;
};

const App = () => {
  // 这样每次render都会执行
  // const [value, setValue] = useState(loop());

  // 这样只有首次会执行一次
  const [value, setValue] = useState(() => {
    return loop();
  });

  //...
}
```

- If you update a State Hook to the same value as the current state, React will bail out without rendering the children or firing effects
  - React uses the `Object.is` comparison algorithm
  - React may still need to render that specific component again before bailing out. 
- In general terms, here’s an example of how this works step-by-step:
  - React initializes the list of Hooks and the variable that keeps track of the current Hook
  - React calls your component for the first time
  - React finds a call to `useState` , creates a new Hook object (with the initial state), changes the current Hook variable to point to this object, adds the object to the Hooks list, and return the array with the initial state and the function to update it
  - React finds another call to `useState` and repeats the actions of the previous step, storing a new Hook object and changing the current Hook variable
  - The component state changes
  - React sends the state update operation (performed by the function returned by `useState` ) to a queue to be processed
  - React determines it needs to re-render the component
  - React resets the current Hook variable and calls your component
  - React finds a call to `useState` , but this time, since there’s already a Hook at the first position of the list of Hooks, it just changes the current Hook variable and returns the array with the current state and the function to update it
  - React finds another call to `useState` and since a Hook exists in the second position, once again, it just changes the current Hook variable and returns the array with the current state and the function to update it
  - If you like to read code,  `ReactFiberHooks` is the class where you can learn how Hooks work under the hood.
- ref
  - [A guide to useState in React](https://blog.logrocket.com/a-guide-to-usestate-in-react-ecb9952e406c/)

- ## `useEffect(didUpdate); `
- Accepts a function that contains imperative, possibly effectful code.
- Mutations, subscriptions, timers, logging, and other side effects are not allowed inside the main body of a function component (referred to as React’s render phase). 
  - Doing so will lead to confusing bugs and inconsistencies in the UI.
  - Instead, use useEffect
  - The function passed to useEffect will run after the render is committed to the screen. 
  - Think of effects as an escape hatch from React’s purely functional world into the imperative world
- By default, effects run after every completed render, 
- The function passed to useEffect may return a clean-up function.
  - The clean-up function runs before the component is removed from the UI to prevent memory leaks. 
  - If a component renders multiple times (as they typically do), the previous effect is cleaned up before executing the next effect.
- Unlike `componentDidMount` and `componentDidUpdate` , **the function passed to `useEffect` fires after layout and paint**, during a deferred event. 
  - This makes it suitable for the many common side effects, like setting up subscriptions and event handlers, because most types of work shouldn’t block the browser from updating the screen.
  - Not all effects can be deferred. 
  - For example, a DOM mutation that is visible to the user must **fire synchronously before the next paint** so that the user does not perceive a visual inconsistency.
  - The distinction is conceptually similar to passive versus active event listeners.
  - For these types of effects, React provides one additional Hook called `useLayoutEffect` . 
  - It has the same signature as `useEffect` , and only differs in when it is fired
  - Although useEffect is deferred until after the browser has painted, it’s guaranteed to fire before any new renders. React will always flush a previous render’s effects before starting a new update.
  - The default behavior for effects is to fire the effect after every completed render.
    - That way an effect is always recreated if one of its dependencies changes.
    - We don’t need to create a new subscription on every update, only if the source prop has changed.
  - The array of dependencies is not passed as arguments to the effect function
    - Every value referenced inside the effect function should also appear in the dependencies array
    - In the future, a sufficiently advanced compiler could create this array automatically.
- We don't have a commit phase on the server, so `useEffect` will be a no-op for server side rendering.
- `useEffect` and `componentDidMount` both don't run during SSR
  - useEffect will be a no-op for server side rendering.
  - Set the initial state to all items and in useEffect (which is only run client side after hydration) check the url and update state

- ## `useLayoutEffect`
- The signature is identical to `useEffect` , but it fires synchronously after all DOM mutations. 
- Use this to read layout from the DOM and synchronously re-render. 
- Updates scheduled inside `useLayoutEffect` will be flushed synchronously, before the browser has a chance to paint.
- With `useLayoutEffect` , the computation will be triggered before the browser has painted the update. 
- Since the computation takes some time, this eats into the browser’s paint time.
- Prefer the standard `useEffect` when possible to avoid blocking visual updates.
- If you rely on these refs to perform an animation as soon as the component mounts, then you’ll find an unpleasant flickering of browser paints happen before your animation kicks in. This is the case with useEffect, but not useLayoutEffect.

- ## `const value = useContext(MyContext); `
- Accepts a context object(the value returned from `React.createContext` ) 
- Returns the current context value for that context.
  - The current context value is determined by the `value` prop of the **nearest** `<MyContext.Provider>` above the calling component in the tree.
- `useContext(MyContext)` is **equivalent** to `static contextType = MyContext` in a class, or to `<MyContext.Consumer>` .
  - `useContext(MyContext)` only lets you read the context and subscribe to its changes. 
  - You still need a `<MyContext.Provider>` above in the tree to provide the value for this context.
- When the nearest `<MyContext.Provider>` above the component updates, this Hook will trigger a rerender 
- Even if an ancestor uses `React.memo` or `shouldComponentUpdate` , a rerender will still happen starting at the component itself using `useContext` .
- A component calling `useContext` will always re-render when the context value changes. 
- If re-rendering the component is expensive, you can optimize it by using memoization.

- ## `const [state, dispatch] = useReducer(reducer, initialState, init); `
- An alternative to `useState`
- Accepts a reducer of type `(state, action) => newState`
- Returns the current state paired with a `dispatch` method.
- `useReducer` is usually preferable to `useState`
  - when you have complex state logic that involves multiple sub-values 
  - or when the next state depends on the previous one. 
- `useReducer` also lets you optimize performance for components that trigger deep updates because you can pass `dispatch` down instead of callbacks.
- React guarantees that `dispatch` function identity is stable and won’t change on re-renders.

- There are two different ways to initialize `useReducer` state.
- The simplest way is to pass the initial state as a second argument
  - `const [state, dispatch] = useReducer( reducer, {count: initialCount} ); `
  - The initial state for `useReducer` hook should be passed as a second argument to useReducer.
  - React doesn’t use the `state = initialState` argument convention popularized by Redux. 
    - the default state value will be returned when an invalid action is dispatched.
  - The initial value sometimes needs to depend on props and so is specified from the Hook call instead. 
  - If you feel strongly about this, you can call `useReducer(reducer, undefined, reducer)` to emulate the Redux behavior, but it’s not encouraged.
    - `useReducer(reducer, undefined, { type: 'INIT' })` will work as you expect. 
    - It will execute the reducer initially, once, with a `{ type: 'INIT' }` action, thus falling through to the default case. 
    - Because `initialState` is provided as `undefined` , it will appropriately default to `5` as specified in the reducer.

``` JS
function reducer(state = 5, { type }) {
  switch (type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}

function Counter() {
  const [count] = useReducer(reducer)
  return <span>{count}</span>
}
```

- You can also create the initial state lazily.
  - To do this, you can pass an `init` function as the third argument. 
  - The initial state will be set to `init(initialState)` .
  - It lets you extract the logic for calculating the initial state outside the reducer.
  - This is also handy for resetting the state later in response to an action

- If you return the same value from a Reducer Hook as the current state, React will bail out without rendering the children or firing effects.
  - React uses the `Object.is` comparison algorithm.
  - React may still need to render that specific component  again before bailing out.
  - If you’re doing expensive calculations while rendering, you can optimize them with `useMemo` .

``` typescript
// 将状态初始化的逻辑提取到reducer函数外
function init(initialCount) {
return { count: initialCount };
}

// 状态数据更新的具体计算逻辑
function reducer(state, action) {
switch (action.type) {
  case 'increment':
    return { count: state.count + 1 };
  case 'decrement':
    return { count: state.count - 1 };
  case 'reset':
    return init(action.payload);
  default:
    throw new Error();
}
}

function Counter({initialCount}) {
// The initial state will be set to `init(initialArg)` .
const [state, dispatch] = useReducer(reducer, initialCount, init);
return (
  <>
    Count: {state.count}
    <button
      onClick={() => dispatch({type: 'reset', payload: initialCount})}>
      Reset
    </button>
    <button onClick={() => dispatch({type: 'decrement'})}>-</button>
    <button onClick={() => dispatch({type: 'increment'})}>+</button>
  </>
);
}
```

- ## `const memoizedVal = useMemo(() => computeExpensiveValue(a, b), [a, b]); `
- Pass a “create” function and an array of dependencies. 
- Returns a memoized value.
- `useMemo` will only recompute the memoized value when one of the dependencies has changed.
- This optimization helps to avoid expensive calculations on every render.
- The function passed to useMemo runs during rendering. 
  - Don’t do anything there that you wouldn’t normally do while rendering. 
  - For example, side effects belong in useEffect, not useMemo.
- If no array is provided, a new value will be computed on every render.
- You may rely on `useMemo` as a performance optimization, not as a semantic guarantee. 
- In the future, React may choose to “forget” some previously memoized values and recalculate them on next render, e.g. to free memory for offscreen components.
- Write your code so that it still works without useMemo — and then add it to optimize performance.

- ## `const memoizedCb = useCallback( () => { doSomething(a, b); }, [a, b] ); `
- Pass an inline callback and an array of dependencies. 
- Return a memoized version of the callback that **only changes if one of the dependencies has changed**. 
- `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)` .
- This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders (e.g. shouldComponentUpdate).
- The array of dependencies is not passed as arguments to the callback. 

- ## `const refContainer = useRef(initialValue); `
- `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument ( `initialValue` ).
- The **returned object will persist for the full lifetime** of the component.
- A common use case is to access a child imperatively
- If you pass a ref object to React with `<div ref={myRef} />` , React will set its `.current` property to the corresponding DOM node whenever that node changes.
- `useRef` is handy for keeping any mutable value around, similar to how you’d use instance fields in classes.
- This works because `useRef()` creates a plain JavaScript object. 
  - The only difference between `useRef()` and creating a `{current: ...}` object yourself is that `useRef` will give you the same ref object on every render.
- `useRef` doesn’t notify you when its content changes. 
  - Mutating the `.current` property doesn’t cause a re-render.
  - If you want to run some code when React attaches or detaches a ref to a DOM node, you may want to use a callback ref instead.

- ## `useImperativeHandle(ref, createHandle, [deps])`
- It customizes the instance value that is exposed to parent components when using `ref`.
- It should be used with `forwardRef`
- As always, imperative code using refs should be avoided in most cases.

``` js
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus1: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);

// in parent component
<FancyInput ref={inputRef} />
inputRef.current.focus();
```

- Usually when you use `useRef` , you are given the instance value of the component the `ref` is attached to. 
  - This allows you to interact with the DOM element directly.
- useImperativeHandle is very similar, but it lets you do two things
  - It gives you control over the value that is returned. Instead of returning the instance element, you explicitly state what the return value will be
  - It allows you to replace native functions (such as blur, focus, etc) with functions of your own, thus allowing side-effects to the normal behavior, or a different behavior altogether. Though, you can call the function whatever you like. 
- However, useImperativeHandle is rarely used. It makes it easier to integrate with imperative libraries.

- ref
  - [When to use useImperativeHandle](https://stackoverflow.com/questions/57005663/when-to-use-useimperativehandle-uselayouteffect-and-usedebugvalue)
  - [使用ref来获取DOM元素的节点和获取子组件的实例](https://juejin.cn/post/6844903929499615240)

- ## `useDebugValue(value)`
- It can be used to display a label for custom hooks in React DevTools.
- We don’t recommend adding debug values to every custom Hook. 
- It’s most valuable for custom Hooks that are part of shared libraries.
- In some cases formatting a value for display might be an expensive operation.
- It’s also unnecessary unless a Hook is actually inspected.
- For this reason useDebugValue accepts a formatting function as an optional second parameter. 
  - This function is only called if the Hooks are inspected. 
  - It receives the debug value as a parameter and should return a formatted display value.
