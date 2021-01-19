---
title: note-react-blog
tags: [blog, dev, react]
created: '2020-06-29T08:43:56.344Z'
modified: '2020-07-14T11:51:59.253Z'
---

# note-react-blog

# [Why React Context is Not a "State Management" Tool (and Why It Doesn't Replace Redux)](https://blog.isquaredsoftware.com/2021/01/blogged-answers-why-react-context-is-not-a-state-management-tool-and-why-it-doesnt-replace-redux/)

- Is Context a "state management" tool?
  - No. Context is a form of Dependency Injection. 
  - It is a transport mechanism - it doesn't "manage" anything. 
  - Any "state management" is done by you and your own code, typically via useState/useReducer.
- Are Context and useReducer a replacement for Redux?
  - No. They have some similarities and overlap, but there are major differences in their capabilities.
- When should I use Context?
  - Any time you have some value that you want to make accessible to a portion of your React component tree, without passing that value down as props through each level of components.
- When should I use Context and useReducer?
  - When you have moderately complex React component state management needs within a specific section of your application.
- When should I use Redux instead?
  - Redux is most useful in cases when:
    - You have larger amounts of application state that are needed in many places in the app
    - The app state is updated frequently over time
    - You need more powerful capabilities for managing side effects, persistence, and data serialization

- discussion

- There are _multiple_ differences in behavior and functionality between Context+useReducer and React-Redux
  - The "boilerplate" concerns have been eliminated by Redux Toolkit
  - While Redux isn't always the right choice, there are many reasons to choose it over Context+useReducer

# [JSX Gotchas](https://shripadk.github.io/react/docs/jsx-gotchas.html)

- JSX looks like HTML but there are some important differences you may run into.
  - For DOM differences, such as the inline `style` attribute, see DOM Differences
- You can insert HTML entities within literal text in JSX
  - `<div>First &middot; Second</div>`
  - If you want to display an HTML entity within dynamic content, you will run into double escaping issues as React escapes all the strings you are displaying in order to prevent a wide range of XSS attacks by default.
  - The easiest way is to write unicode character directly in Javascript. 
    - `<div>{'First · Second'}</div>`
  - A safer alternative is to find the unicode number corresponding to the entity and use it inside of a JavaScript string. 
    - `\u00b7` 或者 `String.fromCharCode(183)`
  - You can use mixed arrays with strings and JSX elements.
    - `<div>{['First ', <span>&middot;</span>, ' Second']}</div>`
  - As a last resort, you always have the ability to insert raw HTML.
    - `<div dangerouslySetInnerHTML={{__html: 'First &middot; Second'}} />`
- If you pass properties to native HTML elements that do not exist in the HTML specification, React will not render them. 
  - If you want to use a custom attribute, you should prefix it with `data-`.
- Web Accessibility attributes starting with `aria-` will be rendered properly.

- [DOM Differences](https://shripadk.github.io/react/docs/dom-differences.html)
- React has implemented a browser-independent events and DOM system for performance and cross-browser compatibility reasons. 
- We took the opportunity to clean up a few rough edges in browser DOM implementations.
  - All DOM properties and attributes (including event handlers) should be camelCased to be consistent with standard JavaScript style. 
    - We intentionally break with the spec here since the spec is inconsistent. 
    - However, `data-*` and `aria-*` attributes conform to the specs and should be lower-cased only.
  - The `style` attribute accepts a JavaScript object with camelCased properties rather than a CSS string. 
    - This is consistent with the DOM style JavaScript property, is more efficient, and prevents XSS security holes.
  - All event objects conform to the W3C spec, and all events (including submit) bubble correctly per the W3C spec.
  - The `onChange` event behaves as you would expect it to: 
    - whenever a form field is changed this event is fired rather than inconsistently on blur. 
    - We intentionally break from existing browser behavior because onChange is a misnomer for its behavior and React relies on this event to react to user input in real time.
  - Form input attributes such as `value` and `checked`, as well as `textarea`.

# [Four Ways to Fetch Data in React_202007](https://www.bitnative.com/2020/07/06/four-ways-to-fetch-data-in-react/)

- React is a focused component library. So it has no opinion on how to request remote data.
- If you’re requesting and sending data to web APIs via HTTP, here are four options to consider.

- ## Option 1: Inline
- This is the simplest and most obvious option.
- Make the HTTP call in the React component and handle the response.

``` JS
// simple
fetch("/users").then(response => response.json());
```

- Looks simple enough. But this example overlooks loading state, error handling, declaring and setting related state, and more. 
- In the real world, HTTP calls look more like this.

``` JS
// request
export default function InlineDemo() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(`${process.env.REACT_APP_API_BASE_URL}users`)
      .then(response => {
        if (response.ok) return response.json();
        throw response;
      })
      .then(json => {
        setUsers(json);
      })
      .catch(err => {
        console.error(err);
        setError(err);
      })
      .finally(() => {
        setLoading(false);
      });
  }, []);

  if (loading) return "Loading...";
  if (error) return "Oops!";
  return users[0].username;
}
```

- For a simple app with a few calls, this works fine. 
- But the state declarations and useEffect above are boilerplate. 
- If I’m making many HTTP calls, I don’t want to duplicate and maintain around 20 lines of code for each one. Inline calls get ugly fast.

- ## Option 2: Centralized folder
- What if we handled all HTTP calls in one folder? 
- With this approach, we create a folder called services and place functions that make HTTP calls inside there. 
- Services is the most popular term, but plenty of other good alternative names like “client”, or “api” are discussed here.
- Point is, all HTTP calls are handled via plain ‘ol JavaScript functions, stored in one folder. 
- The primary benefit is it enforces consistently handling HTTP calls. 
- Here’s the idea: When related functions are handled together, it’s easier to handle them consistently. 
- If the `userService` folder is full of functions that make HTTP calls, it’s easy for me to assure they do so consistently. 
- Also, if the calls are reused, they’re easy to call from this centralized location.
- However, there’s still a lot of boilerplate at the call site.

- ## Option 3 – Custom Hook
- With the magic of React Hooks, we can finally centralize repeated logic. 
- So how about creating a custom `useFetch` hook to streamline our HTTP calls?

``` JS
// This custom hook centralizes and streamlines handling of HTTP calls
export default function useFetch(url, init) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const prevInit = useRef();
  const prevUrl = useRef();

  useEffect(() => {
    // Only refetch if url or init params change.
    if (prevUrl.current === url && prevInit.current === init) return;
    prevUrl.current = url;
    prevInit.current = init;
    fetch(process.env.REACT_APP_API_BASE_URL + url, init)
      .then(response => {
        if (response.ok) return response.json();
        setError(response);
      })
      .then(data => setData(data))
      .catch(err => {
        console.error(err);
        setError(err);
      })
      .finally(() => setLoading(false));
  }, [init, url]);

  return { data, loading, error };
}
```

- This single hook dramatically simplifies all call sites

``` JS
export default function HookDemo() {
  const { data, loading, error } = useFetch("users");
  if (loading) return "Loading...";
  if (error) return "Oops!";
  return data[0].username;
}
```

- But this hook is already quite complex, and it’s omitting a variety of concerns. What about caching? What about refetching if the client’s connection is unreliable? Would you like to refetch fresh data when the user refocuses the tab? What about eliminating duplicate queries?

- ## react-query/swr
- With react-query or swr, caching, retry, refetch on focus, duplicated queries, and much more are handled for me. 
- I don’t have to maintain a custom hook. 
- And each HTTP call requires little code:

``` JS
import React from "react";
import { getUsers } from "./services/userService";
import { useQuery } from "react-query";

export default function ReactQueryDemo() {
  const { data, isLoading, error } = useQuery("users", getUsers);
  if (isLoading) return "Loading...";
  if (error) return "Oops!";
  return data[0].username;
}
```

- ref
  - I am really enjoying using redux middleware to handle fetching data and dumping it into the store. E.g. Redux Saga, Redux observable.
    - However, for multiple requests actions dispatched I am using redux-api-middleware.
    - It doesn’t handle the storing into state but it does a great job of allowing all your http requests to be defined in one place including the option to pass state into either the headers or the url for example.
  - [React-query and swr, ask a bunch of questions](https://twitter.com/housecor/status/1265103048365441024)
    1. Should I cache data on the client for a certain period?
    2. Should I load fresh data when the tab is refocused, or the network reconnects?
    3. Should I retry failed HTTP calls?
    4. Should I return cached data, then fetch fresh data behind the scenes?
    5. Should I handle server cache separately from app state?
    6. Should I avoid refetching recently fetched data?
    7. Should I prefetch data the user is likely to want?

# [Fetching Data in React using React Async](https://css-tricks.com/fetching-data-in-react-using-react-async/)

  - [Using data in React with the Fetch API and axios](https://css-tricks.com/using-data-in-react-with-the-fetch-api-and-axios/)

# [Fetching Data in React using Hooks](https://blog.bitsrc.io/fetching-data-in-react-using-hooks-c6fdd71cb24a)

# [Patterns for data fetching in React](https://blog.logrocket.com/patterns-for-data-fetching-in-react-981ced7e5c56/)

- Data fetching strategies in React
  - Server-provided data
  - Components fetch their own data
  - HOCs fetch data and propagate to children
  - Generic fetcher component
- Ensure components render in production
  - Fetching data with React Hooks
  - Suspenseful data fetching
  - Hybrid approaches
- Data fetching tactics
  - Using the Fetch API
  - Using Axios
  - Utilizing async/await
  - REST vs. GraphQL back end
- Conclusion

# [How to fetch data with React Hooks?_201903](https://www.robinwieruch.de/react-hooks-fetch-data)

- In this tutorial, I want to show you how to fetch data in React with Hooks by using the state and effect hooks. 
- Data Fetching with React Hooks
- How to trigger a hook programmatically / manually?
- Loading Indicator with React Hooks
- Error Handling with React Hooks
- Fetching Data with Forms and React
- Custom Data Fetching Hook
- Reducer Hook for Data Fetching
- Abort Data Fetching in Effect Hook

# [How to fetch data in React_201807](https://www.robinwieruch.de/react-fetching-data)

- The article gives you a walkthrough on how to fetch data in React. 
- There is no external state management solution, such as Redux or MobX, involved to store your fetched data. 
- Instead you will use React's local state management.
- ## Where to fetch in React's component tree?
- ## How to fetch data in React?
- ## What about loading spinner and error handling?
- ## How to fetch data with Axios in React
- ## How to test data fetching in React?
- ## How to fetch data with Async/Await in React?
- ## How to fetch data in Higher-Order Components?
- ## How to fetch data in Render Props?
- ## How to fetch data from a GraphQL API in React?

- ref
  - [Example: Using AJAX results to set local state](https://reactjs.org/docs/faq-ajax.html)

# [React-cache, time slicing, and fetching with a synchronous API_201901](https://www.freecodecamp.org/news/react-cache-time-slicing-and-fetching-with-a-synchronous-api-2a57dc9c2e6d/)

- This article doesn’t aim at describing how to use some of the new features but rather at proving how they may have been built. Just for the sake of understanding what we are playing with.
- This kind of modification has allowed React to split into three phases with their own advantages and particularities:
  - The render phase is pure and deterministic. 
    - It has no side effects and the different functions that it’s composed of can be called multiple times. 
    - The render phase is interruptible — it’s not the render function that is in pause mode, but the whole phase
  - The pre-commit phrase aims to provide access to the actual DOM state, 
    - like the scrollbar positions, in read mode.
  - The commit phase actually modifies the DOM and is not interruptible. 
    - React can’t pause during that phase.
- This set of three phases has introduced the Time Slicing capabilities. 
- React is able to pause during the render phase, in between two component function calls, and to resume that phase when necessary.

# [Update on Async Rendering_20180327](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html)

# [React Hooks 你真的用对了吗？](https://zhuanlan.zhihu.com/p/85969406)

- ## 问题一：我该使用单个 state 变量还是多个 state 变量？
- 如果使用单个 state 变量，每次更新 state 时需要合并之前的 state
- 使用多个 state 变量可以让 state 的粒度更细，更易于逻辑的拆分和组合
- 在使用 state 之前，我们需要考虑状态拆分的「粒度」问题。
  - 如果粒度过细，代码就会变得比较冗余。
  - 如果粒度过粗，代码的可复用性就会降低
- 总结
  - 将完全不相关的 state 拆分为多组 state。比如 size 和 position。
  - 如果某些 state 是相互关联的，或者需要一起发生改变，就可以把它们合并为一组 state。比如 left 和 top。

- ## 问题二：deps 依赖过多，导致 Hooks 难以维护？
- 使用 useEffect hook 时，为了避免每次 render 都去执行它的 callback，我们通常会传入第二个参数「dependency array」（下面统称为依赖数组）。这样，只有当依赖数组发生变化时，才会执行 useEffect 的回调函数
- 依赖数组中必须包含在 callback 内部用到的所有参与 React 数据流的值，比如 state、props 以及它们的衍生物
- 依赖数组中千万不要遗漏回调函数内部依赖的值。但是，如果依赖数组依赖了过多东西，可能导致代码难以维护
- 依赖数组依赖的值最好不要超过 3 个，否则会导致代码会难以维护。
- 如果发现依赖数组依赖的值过多，我们应该采取一些方法来减少它。
  - 去掉不必要的依赖。
  - 将 Hook 拆分为更小的单元，每个 Hook 依赖于各自的依赖数组。
  - 通过合并相关的 state，将多个依赖值聚合为一个。
  - 通过 setState 回调函数获取最新的 state，以减少外部依赖。
  - 通过 ref 来读取可变变量的值，不过需要注意控制修改它的途径。

- ## 问题三：该不该使用 useMemo？
- useMemo本身也有开销。useMemo 会「记住」一些值，同时在后续 render 时，将依赖数组中的值取出来和上一次记录的值进行比较，如果不相等才会重新执行回调函数，否则直接返回「记住」的值。
- 这个过程本身就会消耗一定的内存和计算资源。因此，过度使用 useMemo 可能会影响程序的性能。
- useMemo适用的场景：
  - 有些计算开销很大，我们就需要「记住」它的返回值，避免每次 render 都去重新计算。
  - 由于值的引用发生变化，导致下游组件重新渲染，我们也需要「记住」这个值。
- 在使用 useMemo 之前，我们不妨先问自己几个问题：
  - 要记住的函数开销很大吗？
  - 返回的值是原始值吗？
  - 记忆的值会被其他 Hook 或者子组件用到吗？
- 应该使用 useMemo 的场景
  - 保持引用相等
    - 对于组件内部用到的 object、array、函数等，如果用在了其他 Hook 的依赖数组中，或者作为 props 传递给了下游组件，应该使用 useMemo。
    - 自定义 Hook 中暴露出来的 object、array、函数等，都应该使用 useMemo 。以确保当值相同时，引用不发生变化。
    - 使用 Context 时，如果 Provider 的 value 中定义的值（第一层）发生了变化，即便用了 Pure Component 或者 React.memo，仍然会导致子组件 re-render。这种情况下，仍然建议使用 useMemo 保持引用的一致性。
  - 成本很高的计算
    - 比如 cloneDeep 一个很大并且层级很深的数据
- 无需使用 useMemo 的场景
  - 如果返回的值是原始值： string, boolean, null, undefined, number, symbol（不包括动态声明的 Symbol），一般不需要使用 useMemo。
  - 仅在组件内部用到的 object、array、函数等（没有作为 props 传递给子组件），且没有用到其他 Hook 的依赖数组中，一般不需要使用 useMemo。

- ## 问题四：Hooks 能替代高阶组件和 Render Props 吗？
- 官方给出的回答是，在高阶组件或者 Render Props 只渲染一个子组件时，Hook 提供了一种更简单的方式
- 高阶组件采用了装饰器模式，让我们可以增强原有组件的功能，并且不破坏它原有的特性
- Render Props 通过父组件将可复用逻辑封装起来，并把数据提供给子组件。至于子组件拿到数据之后要怎么渲染，完全由子组件自己决定，灵活性非常高。而高阶组件中，渲染结果是由父组件决定的。Render Props 不会产生新的组件，而且更加直观的体现了「父子关系」。
- 高阶组件和 Render Props 本质上都是将复用逻辑提升到父组件中。
- 而 Hooks 出现之后，我们将复用逻辑提取到组件顶层，而不是强行提升到父组件中。这样就能够避免 HOC 和 Render Props 带来的「嵌套地域」。
- 但是，像 Context 的 `<Provider/>` 和 `<Consumer/>` 这样有父子层级关系（树状结构关系）的，还是只能使用 Render Props 或者 HOC
- Hooks：
  - 替代 Class 的大部分用例，除了 getSnapshotBeforeUpdate 和 componentDidCatch 还不支持。
  - 提取复用逻辑。除了有明确父子关系的，其他场景都可以使用 Hooks。
- Render Props：在组件渲染上拥有更高的自由度，可以根据父组件提供的数据进行动态渲染。适合有明确父子关系的场景。
- 高阶组件：适合用来做注入，并且生成一个新的可复用组件。适合用来写插件。复用最简单。

- ## 问题五： 使用 Hooks 时还有哪些好的实践？
- 若 Hook 类型相同，且依赖数组一致时，应该合并成一个 Hook。否则会产生更多开销
- 参考原生 Hooks 的设计，自定义 Hooks 的返回值可以使用 Tuple 类型，更易于在外部重命名。但如果返回值的数量超过三个，还是建议返回一个对象
- ref 不要直接暴露给外部使用，而是提供一个修改值的方法
- 在使用 useMemo 或者 useCallback 时，确保返回的函数只创建一次。也就是说，函数不会根据依赖数组的变化而二次创建
- useEffect可能导致频繁地绑定事件监听以及解除事件监听
  - 通过使用setState回调函数的方式，让函数不依赖外部变量
  - 通过 ref 来保存可变变量

- ## 实践总结
- 将完全不相关的 state 拆分为多组 state。
- 如果某些 state 是相互关联的，或者需要一起发生改变，就可以把它们合并为一组 state。
- 依赖数组依赖的值最好不要超过 3 个，否则会导致代码会难以维护。
- 如果发现依赖数组依赖的值过多，我们应该采取一些方法来减少它。
  - 去掉不必要的依赖。
  - 将 Hook 拆分为更小的单元，每个 Hook 依赖于各自的依赖数组。
  - 通过合并相关的 state，将多个依赖值聚合为一个。
  - 通过 setState 回调函数获取最新的 state，以减少外部依赖。
  - 通过 ref 来读取可变变量的值，不过需要注意控制修改它的途径。
- 应该使用 useMemo 的场景：
  - 保持引用相等
  - 成本很高的计算
- 无需使用 useMemo 的场景：
  - 如果返回的值是原始值： string, boolean, null, undefined, number, symbol（不包括动态声明的 Symbol），一般不需要使用 useMemo。
  - 仅在组件内部用到的 object、array、函数等（没有作为 props 传递给子组件），且没有用到其他 Hook 的依赖数组中，一般不需要使用 useMemo。
- Hooks、Render Props 和高阶组件都有各自的使用场景，具体使用哪一种要看实际情况。
- 若 Hook 类型相同，且依赖数组一致时，应该合并成一个 Hook。
- 自定义 Hooks 的返回值可以使用 Tuple 类型，更易于在外部重命名。如果返回的值过多，则不建议使用。
- ref 不要直接暴露给外部使用，而是提供一个修改值的方法。
- 在使用 useMemo 或者 useCallback 时，可以借助 ref 或者 setState callback，确保返回的函数只创建一次。也就是说，函数不会根据依赖数组的变化而二次创建。

# When to useMemo and useCallback

- ref
  - [When to useMemo and useCallback](https://kentcdodds.com/blog/usememo-and-usecallback)
  - [【译】什么时候使用useMemo和useCallback](https://jancat.github.io/post/2019/translation-usememo-and-usecallback/)
  - [React, Inline Functions, and Performance](https://reacttraining.com/blog/react-inline-functions-and-performance/)
- The point is this:
  - Performance optimizations are not free. 
  - They ALWAYS come with a cost but do NOT always come with a benefit to offset that cost.
  - Therefore, optimize responsibly.
- So when should I useMemo and useCallback?
- There are specific reasons both of these hooks are built into React:
  - Referential equality
  - Computationally expensive calculations

``` JS
function Foo({ bar, baz }) {
  const options = { bar, baz }
  React.useEffect(() => {
    buzz(options)
  }, [options]) // we want this to re-run if bar or baz change
  return <div>foobar</div>
}

function Blub() {
  return <Foo bar="bar value" baz={3} />
}
```

- The reason this is problematic is because `useEffect` is going to do a referential equality check on options between every render, 
  - and thanks to the way JavaScript works options` will be new every time 
  - so when React tests, whether `options` changed between renders, it'll always evaluate to `true` , 
  - meaning the `useEffect` callback will be called after every render rather than only when `bar` and `baz` change.

``` JS
function Foo({ bar, baz }) {
  React.useEffect(() => {
    const options = { bar, baz }
    buzz(options)
  }, [bar, baz]) // we want this to re-run if bar or baz change
  return <div>foobar</div>
}
```

- But there's one situation when this isn't a practical solution: If `bar` or `baz` are (non-primitive) objects/arrays/functions/etc

``` JS
function Foo({ bar, baz }) {
  React.useEffect(() => {
    const options = { bar, baz }
    buzz(options)
  }, [bar, baz])
  return <div>foobar</div>
}

function Blub() {
  const bar = React.useCallback(() => {}, [])
  const baz = React.useMemo(() => [1, 2, 3], [])
  return <Foo bar={bar} baz={baz} />
}
```

- This is precisely the reason why `useCallback` and `useMemo` exist. So here's how you'd fix that (all together now)
- Note that this same thing applies for the dependencies array passed to `useEffect/useLayoutEffect/useCallback` , and `useMemo` .

``` typescript
function CountButton({onClick, count}) {
  return <button onClick={onClick}>{count}</button>
}

function DualCounter() {
  const [count1, setCount1] = React.useState(0)
  const increment1 = () => setCount1(c => c + 1)
  const [count2, setCount2] = React.useState(0)
  const increment2 = () => setCount2(c => c + 1)
  return (
    <>
      <CountButton count={count1} onClick={increment1} />
      <CountButton count={count2} onClick={increment2} />
    </>
  )
}
```

- Every time you click on either of those buttons, the `DualCounter` 's state changes and therefore re-renders which in turn will re-render both of the CountButtons.
  - However, the only one that actually needs to re-render is the one that was clicked right? 
  - So if you click the first one, the second one gets re-rendered, but nothing changes.
  - We call this an "unnecessary re-render."
- MOST OF THE TIME YOU SHOULD NOT BOTHER OPTIMIZING UNNECESSARY RERENDERS. 
  - React is VERY fast 
  - and there are so many things I can think of for you to do with your time that would be better than optimizing things like this. 
- However, there are situations when rendering can take a substantial amount of time (think highly interactive Graphs/Charts/Animations/etc.).

``` typescript
const CountButton = React.memo(function CountButton({onClick, count}) {
  return <button onClick={onClick}>{count}</button>
})

function DualCounter() {
  const [count1, setCount1] = React.useState(0)
  const increment1 = React.useCallback(() => setCount1(c => c + 1), [])
  const [count2, setCount2] = React.useState(0)
  const increment2 = React.useCallback(() => setCount2(c => c + 1), [])
  return (
    <>
      <CountButton count={count1} onClick={increment1} />
      <CountButton count={count2} onClick={increment2} />
    </>
  )
}
```

- Now we can avoid the so-called "unnecessary re-renders" of CountButton.
  - I would like to re-iterate that I strongly advise against using React.memo (or it's friends PureComponent and shouldComponentUpdate) without measuring 
  - because those optimizations come with a cost 
  - and you need to make sure you know what that cost will be as well as the associated benefit 
  - so you can determine whether it will actually be helpful (and not harmful) in your case, 
  - and as we observe above it can be tricky to get right all the time so you may not be reaping any benefits at all anyway.
- This is the other reason that `useMemo` is a built-in hook for React (note that this one does not apply to `useCallback` ).
  - React stores previous values given the inputs and will return the previous value given the same previous inputs. 
  - That's memoization at work.
  - This is useful for computationally expensive calculations
- I'd just like to wrap this up by saying that every abstraction (and performance optimization) comes at a cost. 
- Apply the AHA Programming principle and wait until the abstraction/optimization is screaming at you before applying it and you'll save yourself from incurring the costs without reaping the benefit.
- Specifically the cost for `useCallback` and `useMemo` are that you make the code more complex for your co-workers, 
  - you could make a mistake in the dependencies array, and you're potentially making performance worse by invoking the built-in hooks and preventing dependencies and memoized values from being garbage collected. 
  - Those are all fine costs to incur if you get the performance benefits necessary, but it's best to measure first.

``` JS
class FavoriteNumbers extends React.Component {
  render() {
    return (
      <ul>
        {this.props.favoriteNumbers.map(number => (
          // TADA! 
          // This is a function defined in the render method!
          // Hooks did not introduce this concept.
          // We've been doing this all along.
          <li key={number}>{number}</li>
        ))}
      </ul>
    )
  }
}
```

# You Probably Don't Need Derived State

- ref
  - https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
  - [你可能不需要Derived State](https://zhuanlan.zhihu.com/p/38090110)

- To recap, when designing a component, it is important to decide whether its data will be controlled or uncontrolled.
  - The terms “controlled” and “uncontrolled” usually refer to form inputs, but they can also describe where any component’s data lives. 
  - Data passed in as props can be thought of as **controlled** (because the parent component controls that data). 
  - Data that exists only in internal state can be thought of as **uncontrolled** (because the parent can’t directly change it).
  - Instead of trying to “mirror” a prop value in state, make the component controlled, and consolidate the two diverging values in the state of some parent component. This makes the data flow more explicit and predictable.
  - For uncontrolled components, if you’re trying to reset state when a particular prop (usually an ID) changes, you have a few options:
    - Recommendation: To reset all internal state, use the `key` attribute.
    - Alternative 1: Reset uncontrolled component with an ID prop
      - To reset only certain state fields, watch for changes in a special property (e.g. props.userID).
    - Alternative 2: Reset uncontrolled component with an instance method
      - consider fall back to an imperative instance method using refs.
- bugs
  - If our component’s parent rerenders, anything we’ve typed into the `<input>` will be lost!
  - In practice, components usually accept multiple props; 
    - another prop changing would still cause a rerender and improper reset. 
    - Function and object props are also often created inline, making it hard to implement a shouldComponentUpdate that reliably returns true only when a material change has happened.
    - As a result, shouldComponentUpdate is best used as a performance optimization, not to ensure correctness of derived state
    - It is a bad idea to unconditionally copy props to state.
    - When navigating between details for two accounts with the same email, the input would fail to reset. This is because the prop value passed to the component would be the same for both accounts! 
- When a `key` prop changes, React will create a new component instance rather than update the current one.
  - Keys are usually used for dynamic lists but are also useful here. 
  - Sometimes it might make more sense to put a key on the whole form instead. Every time the key changes, all components within the form will be recreated with a freshly initialized state.
  - While this may sound slow, the performance difference is usually insignificant. Using a key can even be faster if the components have heavy logic that runs on updates since diffing gets bypassed for that subtree.

# react component vs element vs instance

- ref
  - [React Components, Elements, and Instances](https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html)
- An element is a plain object describing a component instance or DOM node and its desired properties. 
  - It contains only information about the component type (for example, a Button), its properties (for example, its color), and any child elements inside it.
  - It is a way to tell React what you want to see on the screen. 
  - You can’t call any methods on the element.
  - It’s just an immutable description object with two fields: `type: (string | ReactClass)` and `props: Object`
  - An element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components.
  - Elements can contain other elements in their props. 
  - Creating a React element is cheap. 
  - Once an element is created, it is never mutated.
- A React component takes props as an input, and returns an element tree as the output.
  - A component can be declared in several different ways. class/func
  - props flows one way in React: from parents to children.
- An instance is what you refer to as `this` in the component class you write. 
  - It is useful for storing local state and reacting to the lifecycle events.
  - Only components declared as classes have instances, and you never create them directly: React does that for you
  - While mechanisms for a parent component instance to access a child component instance exist, they are only used for imperative actions (such as setting focus on a field), and should generally be avoided.
  - React takes care of creating an instance for every class component, so you can write components in an object-oriented way with methods and local state, but other than that, instances are not very important in the React’s programming model and are managed by React itself.
  - Function components don’t have instances at all.

# A Complete Guide to useEffect

- ref
  - [A Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
- Question: How do I replicate `componentDidMount` with `useEffect` ?
- Question: How do I correctly fetch data inside `useEffect` ? What is `[]` ?
- Question: Do I need to specify functions as effect dependencies or not?
- Question: Why do I sometimes get an infinite refetching loop?
- Question: Why do I sometimes get an old state or prop value inside my effect?
- Each Render Has Its Own Props and State
- Each Render Has Its Own Event Handlers
- Each Render Has Its Own Effects
- Each Render Has Its Own… Everything
  - We know now that effects run after every render, are conceptually a part of the component output, and “see” the props and state from that particular render.
  - Closures are great when the values you close over never change. That makes them easy to think about because you’re essentially referring to constants.
  - And as we discussed, props and state never change within a particular render.
