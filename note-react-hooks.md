---
tags: [hooks, react]
title: note-react-hooks
created: '2020-06-24T08:36:20.056Z'
modified: '2020-06-29T13:14:27.166Z'
---

# note-react-hooks

## faq

- ### Why not just useMemo?
  - In the future, React may choose to “forget” some previously memoized values 
    - and recalculate them on next render, e.g. to free memory for offscreen components. 
    - Write your code so that it still works without useMemo — and then add it to optimize performance.
  - In cases where the value must never change, the recommended workaround is to store it with `useRef` , but refs are more awkward to initialize and don't enforce or even communicate that the value should be immutable. 
  - An alternative workaround is `const [value] = useState(initializer)` , but this is semantically wrong and more costly under the hood.
  - `useConst` will always return the same value
  - https://github.com/microsoft/fluentui/blob/master/packages/react-hooks/README.md

- ### React.memo vs reselect
  - [React.memo vs Memoize: What’s the difference and when to use them](https://medium.com/better-programming/react-memo-vs-memoize-71f85eb4e1a)
    - In computing, memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.
    - This points out a fundamental rule when using the memoization function. 
      - You should only ever use memoization with pure functions. 
      - For our purposes, there should be no side effects in our function. 
      - Given a set of arguments to a function, we should always expect the same result.
    - First, `memoize-one` is an arbitrary library in this example. We could have picked any memoization library, such as `reselect` , `lodash` , or `ramda` . Memoize-one is a tiny library that only memoizes the latest arguments and results. 
    - React.memo is intended to be wrapped around a functional component.
    - So, `memoize-one` (in common with most memoization libraries) remembers the result of a given function with a set of arguments, despite where the last execution occurs. 
      - `React.memo` , on the other hand, is for memoizing a single occurrence of a component when attempting to re-render, and it will not work outside of its instance.
  - 在 reselect 中默认的 memorize 函数依靠闭包来做缓存，缺点是不能记录多次。

- ### useMemo vs reselect
  - [Will useMemo replace reselect?](https://github.com/reduxjs/reselect/issues/386)
    - `reselect` can be used anywhere, as it has no dependencies
    - `reselect` is indeed useful anywhere, and can be used totally independent of Redux. 
      - Really, its competition is libs like `memoize-one` , not `useMemo()` .
    - For Redux usage, we recommend using selectors anywhere you access the Redux state tree, not just in mapState functions. 
    - I would assume that `useMemo` cannot replace `reselect` simply because `useMemo` is a hook and therefore will only work with functional components. While `reselect` works with any type of component.
  - [useMemo: the most underrated Hook](https://twitter.com/dan_abramov/status/1055689046117105664)
    - To me, it looks like reselect.
    - Yep but tied to component

- ### `useImperativeHandle` vs assign `ref.current` directly
  - [What benefit does useImperativeHandle provide over assigning a forwarded ref in useEffect?](https://stackoverflow.com/questions/59860956/what-benefit-does-useimperativehandle-provide-over-assigning-a-forwarded-ref-in)
  - It's the same and useImperativeHandle just handles all of the ref cases and makes sure the passed value is a ref and not just any value. So it saves some code
  - useImperativeHandle is almost the same as your approach with useEffect
  - So apparently, under the hood, it's the same thing, but with when using useImperativeHandle you don't need to handle the part of `.current` , it already checks for null values, checks if it's a ref and sets in returned value in `.current`
  - useImperativeHandle needs to have the component use forwardRef
  - It appears that `useImperativeHandle` is simply an effect that takes care of the necessary checks, cleanups and accounting for both function and object refs, but instead of using the high level useEffect, it works directly with the low level effect lifecycle functions. I think the biggest reason that it is its own hook could be to ensure backwards compatibility with function refs

``` JS
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} />;
}
FancyInput = forwardRef(FancyInput);
```

``` JS
function FancyInput(props, ref) {
  const inputRef = useRef();
  useEffect(() => {
    if (ref) {
      ref.current = {
        focus: () => {
          inputRef.current.focus();
        }
      };
    }
  }, [ref]);
  return <input ref={inputRef} />;
}
FancyInput = forwardRef(FancyInput);
```

- ### `useCallback` vs `useMemo`
  - `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)` .
  - useMemo() makes the function run only when inputs change. 
    - Else it returns the memoized(cached) result.
  - useCallback() prevents the new instance of funtion being created on each rerender
    - thus prevents the rerendering of child components if we pass the function as props to them

- react生命周期方法的执行时，是处于浏览器渲染过程中的什么位置(js-style-layout-paint-composite)
  - render方法的执行时机
  - One drawback of using `componentDidUpdate` , or `componentDidMount` is that they are actually executed before the dom elements are done being drawn, but after they've been passed from React to the browser's DOM.

- ### `useEffect` vs `useLayoutEffect`
  - 结论
    - useLayoutEffect总是比useEffect先执行
    - useLayoutEffect: If you need to mutate the DOM and/or do need to perform measurements
    - useEffect: If you don't need to interact with the DOM at all or your DOM changes are unobservable (seriously, most of the time you should use this). 
    - componentDidMount and useLayoutEffect both run before paint. useEffect yields (so the browser can paint) before running.
    - We suggest using the passive effect (useEffect) for things that don't affect display, like logging or setting timeouts etc. 
    - Use layout effect for e.g. adjusting tooltip position or size, things you want to tweak before the user sees your component's rendered output.
  - 正常情况用默认的useEffect钩子就够了，这可以保证状态变更不阻塞渲染过程
    - 但如果effect更新（清理）中涉及DOM更新操作，用useEffect就会有意想不到的效果。
    - 比如逐帧动画 requestAnimationFrame ，要做一个 useRaf hook 就得用上后者，需要保证同步变更。
    - useLayoutEffect > requestAnimationFrame > useEffect
  - useEffect的时期非常晚，可以保证页面是稳定下来再做事情
    - useEffect的函数会在最后才执行，可能晚于包含它的父组件的did update
  - `useEffect` runs asynchronously and after a render is painted to the screen.
    - You cause a render somehow (change state, or the parent re-renders)
    - React renders your component (calls it)
    - The screen is visually updated
    - THEN useEffect runs.
  - `useLayoutEffect` runs synchronously after a render but before the screen is updated
    - You cause a render somehow (change state, or the parent re-renders)
    - React renders your component (calls it)
    - useLayoutEffect runs, and React waits for it to finish.
    - The screen is visually updated
  - **useEffect**
    - It runs after the render is committed to the screen i.e. **after Layout and Paint phase**. 
    - Use this whenever possible to avoid blocking visual updates
  - **useLayoutEffect**
    - It **fires synchronously after all DOM mutations but before Paint phase**.
    - Use this to read layout(styles or layout information) from the DOM and then perform blocking custom DOM mutations based on layout.
  - useMutationEffect
    - It fires synchronously before Layout phase i.e. during the same phase that React performs its DOM mutations.
    - Use it to perform blocking custom DOM mutations without taking any DOM measurement/reading layout.
  - `useMutationEffect` has problems (namely, refs aren't attached at the time that it runs) and we're not positive it's necessary. 
    - we should use useLayoutEffect if we want to read Layout from the DOM. Otherwise we should use useMutationEffect
    - `useLayoutEffect` runs at the same time as componentDidMount/Update, so it's sufficient for all existing use cases; it can be used in any case that useEffect happens too late. Until we figure out what we want to do, let's delete it.
    - https://github.com/facebook/react/pull/
  - useEffect runs after react renders your component 
    - and ensures that your effect callback does not block browser painting. 
    - This differs from the behavior in class components where componentDidMount and componentDidUpdate run synchronously after rendering
    - However, if your effect is mutating the DOM (via a DOM node ref) and the DOM mutation will change the appearance of the DOM node between the time that it is rendered and your effect mutates it, then you don't want to use useEffect. You'll want to use useLayoutEffect.
    - Otherwise the user could see a flicker when your DOM mutations take effect.
    - This is pretty much the only time you want to avoid useEffect and use useLayoutEffect instead.
  - useLayoutEffect
    - This runs synchronously immediately after React has performed all DOM mutations. 
    - This can be useful if you need to make DOM measurements (like getting the scroll position or other styles for an element) and then make DOM mutations or trigger a synchronous re-render by updating state.
    - As far as scheduling, this works the same way as componentDidMount and componentDidUpdate. 
    - Your code runs immediately after the DOM has been updated, but before the browser has had a chance to "paint" those changes (the user doesn't actually see the updates until after the browser has repainted)
  - ref
    - https://kentcdodds.com/blog/useeffect-vs-uselayouteffect
    - https://stackoverflow.com/questions/53513872/react-hooks-what-is-the-difference-between-usemutationeffect-and-uselayoutef

- ### How to pass arguments to `onClick` events in React Hooks 
  - simple: `<Button onClick={() => handleClick(myValue)}></Button>`
    - onClick prop has new value on each render and triggers a re-render of child component - even if it's pure. 
  - If a value is static, a callback can be defined as constant function outside a component

``` js
    // outside function component
    const myValue = "Hello World";
    const myHandleClick = () => handleClick(myValue);

    // inside function component
    <Button onClick={myHandleClick}></Button>
```

  - If a value is dynamic and is available only inside a component, a function can be defined inside a component and memoized with useMemo or useCallback hook 

``` js
    // inside function component
    const myHandleClick = useCallback(() => handleClick(myValue), [myValue]);
    ...
    <Button onClick={myHandleClick}></Button>
```

## pieces

- ref
  - https://medium.com/@unbug/ive-completely-rewritten-two-projects-with-react-hooks-here-is-the-good-and-the-ugly-48c28a103f52
- 考虑因素
  - 可能会使用的第三方库/组件是否提供hooks相关api
    - react-router,redux
    - enzyme等测试框架是否提供hooks
    - react-motion如何实现与修改
    - table/tree如何实现与修改
    - 参考ant design这样的大厂大项目如何选择
  - 若将来要替换react，复杂度如何
  - 自己开发组件库，要考虑提供和维护class和hooks两套api
  - class实例变量要替换为useRef hook
  - ref要替换为useImperativeHandle hook
  - 生命周期函数大多可替换，目前不支持getSnapshotBeforeUpdate
    - getDerivedStateFromProps需要重写在函数体
- syntax
  - useState
  - useEffect
    - The empty set of dependencies, `[]` , means that effect will only run once when the component mounts, and not on every re-render. 
      - This tells React that your effect doesn’t depend on any values from props or state, so it never needs to re-run.
      - If you pass an empty array ([]), the props and state inside the effect will always have their initial values. 
    - 在useEffect中使用setInterval要注意问题
    - React defers running useEffect until after the browser has painted, so doing extra work is less of a problem
- pros
  - reuse components state/lifecycle logic become possible
  - Separate (and isolated) concerns
  - mitigate wrapper hell, no deep component tree nesting 
  - classes can be a barrier to learning React
  - Only to write new components, not to refactor old ones
- cons
  - not easy to debug and test
  - mess side-effects within the component
  - 函数组件的函数体相当于class组件的render方法，当在函数体中实现getDerivedStateFromProps的内容时，会出现类似于在render方法中修改state的情况，破坏了render方法的纯净，和类组件提倡的pure render不一致
  - useState返回的更新状态的方式是replace，而不是类组件的merge
  - effects run on every update， which make cache local values as instance properties in React Class Components  difficult
  - turn a React Class into a React Function is easier, turn a React Function with React Hooks into React Class is hard
  - no way to handle Error Boundaries with React Hooks right now
- hooks出现前的常见问题
  - 函数组件 vs class组件
  - 生命周期componentDidMount和componentDidUpdate需要做相同的事情
  - this指向 
- hooks作用
  - 函数变成了一个有状态的函数
  - Hooks本质上就是一类特殊的函数，它们可以为你的函数型组件（function component）注入一些特殊的功能（生命周期钩子, useEffect, useContext）
  - 解决this指向问题
- 函数型组件 vs 类组件 vs hooks
  - 函数组件每次渲染都拥有独立的props，这是因为在react中props是不可变的，每次重新render，函数都捕获到新的独立的props
  - class组件编译es5后会多出一堆辅助函数（继承React. Component），而fc组件只有一个createElement
  - 纯函数组件的渲染优化方法有很多，如useMemo, 还可以借助web worker
  - react hooks和class component只是写法上、范式上的差别，极限性能上的差距，可忽略不计，本质还是diff and patch
  - 使用hooks要更注意缓存的使用，否则很容易出现性能问题
  - 使用场景
    - hoc特别适合做装饰插件，hooks的处理过程会与目标插件强绑定
    - render props自身可以作为jsx的一部分，适合放置简单逻辑
- 迁移到hooks
  - hooks无法与Class组件同时使用
  - hooks写法还是主要替换setState以及生命周期为主, useState/Effect/Context
  - 各种最佳实践社区还在探索中

- ref
  - [hoc转hooks](https://zhuanlan.zhihu.com/p/56617944)
  - [hooks使用现状](https://www.zhihu.com/question/327685582/answers)
  - [hooks体验](https://zhuanlan.zhihu.com/p/62791765)
