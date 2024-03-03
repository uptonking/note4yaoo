---
title: note-react-state-dev
tags: [blog, react, state]
created: 1970-01-01T00:00:00.000Z
modified: 2020-12-08T13:40:02.577Z
---

# note-react-state-dev

# guide

- [A community-maintained spec for global state libraries: 3 levels](https://github.com/reactwg/react-18/discussions/116)
  - https://github.com/dai-shi/will-this-react-global-state-work-in-concurrent-rendering

- context-selector的主要实现
  - 依赖scheduler: dashi/use-context-selector, @fluentui/react-context-selector
  - 其他实现: mohebifar/react-use-context-selector(无依赖)

- 基于hooks模仿redux的api
  - [State Management with React Hooks and Context API](https://devsmitra.medium.com/state-management-with-react-hooks-and-context-api-2968a5cf5c83)

- state management using context
  - [Simple example to create global providers easily in the application](https://gist.github.com/nicolasmelo1/82e00970c1dce080bda349e3f0697152)

## [React doesn't need state management tool, I said; build a redux-like api using context](https://dev.to/tolgee_i18n/react-doesnt-need-state-management-tool-i-said-31l4)

- https://github.com/tolgee/tolgee-platform/blob/main/webapp/src/fixtures/createProvider.tsx

- I've used REDUX about 2 years ago and now I'm working on project where the redux is used, but basically have it's there as a legacy and are trying to get rid of it. 
  - So I haven't used it yet. And store based testing? No, honestly I've never had a use case for it. 
  - We either were writing unit tests for small components or using cypress for testing the app as a whole.

- this approach will have problems when hot module enabled. 
  - I have also developed this kind of lib for Form and FormElements. 
  - When you build form there will be no problem, but when you change the body (main sate) and hot module updates it, the Provider context will lost its value and recreate it from scratch since Form and form element is attached to previous context the render will fail. (using CreateContext from React)

- The problem with React Context is that (due to the nature of React itself) it behaves like a state management tool, while in reality it is a tool for dependency injection. This confusion often leads to the idea to use React Context as a state manager, which it was never intended for.
- 💡 If you take a closer look at any decent state management solution, you will quickly notice that these tools never pass "naked" state (values that change frequently) directly via context, they instead wrap the state with "something" and then pass this "something" through the context. This "something" is generally called "an observable store".
- Different tools use different names 
  - ("store" - redux, effector, zustand, etc.; 
  - "client (cache)" - apollo-client; 
  - "query client (cache)" - react-query), 
  - but the end result is the same - "naked" state is wrapped and the referential equality is preserved even when the state changes.
- So, instead of using cryptic(使用代码的，使用密码的) libraries like use-context-selector, it might be a better idea to take advantage of the "observable store" pattern. If you don't feel like using an existing solution, you can easily implement everything yourself, it's like ~30 LOC with all the infrastructure.

- Use the container -> presentation pattern.. 
  - make each route in the app a container, use react router V6 object routing to pass observable stores to your containers and prop drill to presentation components so things are easier to test.
  - Keep presentation components dumb, containers complex.
  - The parent route where page is uses an observer/observable, Content uses context to access the pages mobx observable so it can add content to the page.
  - Mobx memoizes components automatically for you. I like it way better than redux.
# dev
- state management
  1. Context + useState
  2. Context + useReducer
  3. DispatchContext + StateContext + useReducer
  4. Multiple Providers of #3 for state "slices"
  - They are stages of state management complexity from simple to complex. Performance potentially increases as you go to higher stages
  - At any stage: Profile for slow renders, then useMemo
  - With those 4 stages and useMemo, I believe you can solve 99% of perf challenges.

- state-multi-context
  - diegohaz/constate
  - CharlesStover/react-multi-context
  - dai-shi/react-context-global-state

- list of atomic module state libs
  - jotai
  - recoil
  - reatom
  - klyva
  - xoid
  - pipestate

- state-状态管理技术选型
  - recoil (要等到API稳定、功能齐全)
  - constate
  - unstated-next
  - react-hooks-global-state
  - misc
    - concent

- [will-this-react-global-state-work-in-concurrent-mode](https://github.com/dai-shi/will-this-react-global-state-work-in-concurrent-mode)
  - Check tearing in React concurrent mode

- if you're working with an outside REST API, and not GraphQL, what are you using for state these days? Still Redux? Big state object at the top level that you access with context? Something else?
  - TBH I don't really build apps in the last few years (unless you count DevTools)
  - For DevTools, I just used React's built-in state (useState) and shared via context when needed.
  - We're in the process of replacing Redux with React Context API
  - Global state:
    - I'd go with context, if redux wasn't already present or needed in the app.
    - If I need to permanently cache a few pieces of global state (e.g. theme), I may do so manually. 
    - If I need to cache many pieces (offline app), I'd go with redux + redux-persist.
  - Local state:
    - If I need in-memory caching + suspense support I'd go with SWR or React Query.
  - Background work:
    - If I have long running API calls/processing that would be complex to manage, I'd use redux-observable
  - https://twitter.com/cwbuecheler/status/1253711795459588097
# discuss
- ## 

- ## 

- ## Prediction: Third-party React state libraries will become less relevant in 2024.
- https://twitter.com/housecor/status/1763919937481973801
  - 1. Routers are becoming state managers. Example: @tan_stack router has built in loaders and caching. 
  - 2. React Server Components (RSC). RSC enables server-side fetching and caching. Example: @nextjs .
  - @tan_stack query already taught us - *most state is server state* (data fetched from a server). Both 1 and 2 above handle "server state".

- This is a web centric take
- For cloud-first apps maybe.

- Wasn't @remix_run the first to change the game?
  - Yes I believe they popularized loaders.

- ## [Implement naive version of context selectors](https://github.com/facebook/react/pull/20646)
- `const selection = useSelectedContext(Context, c => select(c));`

- For internal experimentation only.
- This implements `unstable_useSelectedContext` behind a feature flag.
- The key feature is that if the selected value does not change between renders, the component will bail out of rendering its children, a la memo, PureComponent, or the useState bailout mechanism. 
  - (Unless some other state, props, or context was updated in the same render.)
- I also added an optional third argument `isSelectionEqual` . 
  - If defined, it will override the default comparison function used to check if the selected value has changed ( `Object.is` ).
- However, I have not implemented the RFC's proposed optimizations to context propagation. 
  - We would like to land those eventually, but doing so will require a refactor that we don't currently have the bandwidth to complete. 
  - It will need to wait until after React 18.
- In the meantime though, we believe there may be value in landing this more naive implementation. 
  - It's designed to be API-compatible with the full proposal, so we have the option to make those optimizations in a non-breaking release. 
  - However, since it's still behind a flag, this currently has no impact on the stable release channel. 
  - We reserve the right to change or remove it, as we conduct internal testing.

- ref
  - [RFC: Context selectors](https://github.com/reactjs/rfcs/pull/119)

- ## [Preventing rerenders with React.memo and useContext hook](https://github.com/facebook/react/issues/15156)

- 状态管理要解决的问题是跨组件状态共享
  - state数据结构定义和存放、读取、修改
- `useState` doesn't offer a way to bail out of rendering once an update is being processed. 
  - This gets a bit weird because we actually process updates during the rendering phase. So we're already rendering. 
  - But we could offer a way to bail on children. 
  - Edit: we now do bail out on rendering children if the next state is identical.
- `useContext` doesn't let you subscribe to *a part of the context value* (or some memoized selector) without fully re-rendering.

- `React.memo` cannot prevent rerender caused by high-frequency updates of context value
  - Let's say for some reason you have `AppContext` whose value has a theme property, and you want to only re-render some `ExpensiveTree` on `appContextValue.theme` changes.
  - note that option 1 is preferable — if some context changes too often, consider splitting it out.

- ### Option 1(Preferred): Split contexts that don't change together
  - If we just need `appContextValue.theme` in many components but `appContextValue` itself changes too often, we could split `ThemeContext` from `AppContext` .
  - Now any change of `AppContext` won't re-render `ThemeContext` consumers.
  - This is the preferred fix. Then you don't need any special bailout.

```JS
  function Button() {
    let theme = useContext(ThemeContext);
    // The rest of your rendering logic
    return <ExpensiveTree className={theme} />;
  }
```

- ### Option 2: Split your component in two, put `memo` in between
  - If for some reason you can't split out contexts, you can still optimize rendering by splitting a component in two, and passing more specific props to the inner one.
  - You'd still render the outer one, but it should be cheap since it doesn't do anything.

```JS
function Button() {
  let appContextValue = useContext(AppContext);
  let theme = appContextValue.theme; // Your "selector"
  return <ThemedButton theme={theme} />
}

const ThemedButton = memo(({ theme }) => {
  // The rest of your rendering logic
  return <ExpensiveTree className={theme} />;
});
```

- ### Option 3: One component with `useMemo` inside
  - Finally, we could make our code a bit more verbose but keep it in a single component by wrapping return value in `useMemo` and specifying its dependencies. 
  - Our component would still re-execute, but React wouldn't re-render the child tree if all `useMemo` inputs are the same.

```JS
function Button() {
  let appContextValue = useContext(AppContext);
  let theme = appContextValue.theme; // Your "selector"

  return useMemo(() => {
    // The rest of your rendering logic
    return <ExpensiveTree className={theme} />;
  }, [theme])
}
```

- ### Option 4: Pass a subscribe function as context value, just like in legacy context era
  - It might be the only option if you don't control the usages (needed for options 2-3) and can't enumerate all the possible selectors (needed for option 1), but still want to expose a Hooks API
  - This is basically what react-redux does internally
  - To implement subscribe function, you can use something like Observables or EventEmitter, or just write a basic subscription logic yourself
  - we stopped passing the store state in context (the v6 implementation) and switched back to direct store subscriptions (the v7 implementation) due to a combination of performance problems and the inability to bail out of updates caused by context (which made it impossible to create a React-Redux hooks API based on the v6 approach).

```JSX
const MyContext = createContext();
export const Provider = ({ children }) => (
  <MyContext.provider value={{subscribe: listener => ..., getValue: () => ...}}>
    {children}
  </MyContext.provider>
)

export const useSelector = (selector, equalityFunction = (a, b) => a === b) => {
    const { subscribe, getValue } = useContext(MyContext)
    const [value, setValue] = useState(getValue())
    useEffect(() => subscribe(state => {
        const newValue = selector(state)
        if (!equalityFunction(newValue, value) {
            setValue(newValue)
          }
        }), [selector, equalityFunction])
    }
```

```JS
function StateProvider({ children }) {
  const [state, dispatch] = useReducer(reducer, initialState);
  const listeners = useRef([]);
  // custom subscription
  const subscribe = listener => {
    listeners.current.push(listener)
  }
  useEffect(() => {
    listeners.current.forEach(listener => listener(state)
    }, [state]))

  return (
    <DispatchContext.Provider value={dispatch}>
      <SubscribeContext.Provider value={{subscribe, getValue: () => state}}>
          {children}      
      </SubscribeContext.Provider>
    </DispatchContext.Provider>
  );
}
```

- ### Option 5: Do not use context for data propagation but data subscription
  - Use useSubscription (because it's hard to write to cover all cases).

- ### Option x1: use an unofficial workaround.
  - useContextSelector proposal and use-context-selector library in userland.

- ## [5 Layers of State Management in React Applications](https://joelhooks.com/5-layers-react-state)
- local
- shared
- remote
- meta
- router

- ## [The 5 Types Of React Application State_201608](http://jamesknelson.com/5-types-react-application-state/)
- Data
- Communication
- Control
- Session
- Location
- https://twitter.com/acemarke/status/1368660030740963329

- ## History of React State Management
- https://twitter.com/leeerob/status/1353523847937536000
  - [React State Management in 2021](https://egghead.io/playlists/react-state-management-in-2021-6732)

  • 2013 – Introduction
  • 2015 – Redux
  • 2016 – MobX
  • 2018 – Context
  • 2019 – Hooks
  • 2019 – Zustand
  • 2020 – Jotai, Recoil
  • 2021 – useSelectedContext

- React's component model helped create reusable, composable applications. Each component had its own local state.
  - As web apps became more complex, new solutions emerged to more easily share logic between components.
- Redux quickly grew to the most popular state management solution. 
  - It's ecosystem of tools and libraries encapsulated both UI state and server caching state.
- React Context gave us a first-party solution to share logic between components. This solved UI state for many cases.
  - React Hooks made Context simple to use (`useContext`). It also allowed libraries like SWR and React Query to solve server caching state.
- In the past few years, we've also seen Zustand, Jotai, and Recoil emerge.
  - They aim to solve common performance issues from state management at scale (and for specific types of apps).
  - FWIW, jotai is developed on `use-context-selector`, which is a userland solution with Concurrent Mode support (best-effort) in mind. 
  - Once `useSelectedContext` is a real thing in a whatever form, we should be able to instantly migrate.
- 2021 will introduce the`useSelectedContext` hook (eventually).
  - This is a first-party solution for the previously mentioned performance issues.
  - In the future, React will automatically figure out which components to re-render ("auto-memoization") 
- I predict humorously that by 2022? or later React may adopt `ECS entity-component-system` using entities (in place of hooks) to manage a local state, contain blocks of components, update their blocks across frames/life cycles, making scale, multi-user, webworkers, & 3D apps easier.

- ## [React state management in 2020](https://twitter.com/chrisachard/status/1272963243225632768)
- React includes: local state (which nearly every app uses at some point) and Context
- Props and State
  - Pros: super simple; built in; nothing extra to learn
  - Cons: "Prop Drilling" can lead to really complex data passing
- Context
  - Pros: built into react, simple interface, "just works"
  - Cons: over re-rendering can lead to slow performance
- redux
  - Pros: Doesn't unnecessarily re-render (as long as you keep things shallow equal)
  - Cons: Can have a huge learning curve.
- mobx
  - Pros: It isn't redux 🤣 (easy to learn); 2 way binding if nice if you like it
  - Cons: observables aren't actually plain JS objects so have some quirks
- React Apollo
  - Pros: Automatically shares state pulled from GraphQL endpoints
  - Cons: Only works with GraphQL Smiling face with open mouth and smiling eyes
- Recoil
  - Pros: Doesn't unnecessarily re-render, can create variable number of stores, simple.
  - Cons: Brand new! Looks promising, but who knows
- So what should you use?
  1. Props and state at first
  2. Context to share simple things
  3. Then Redux if you like it
  4. MobX if you don't like Redux
  5. Or Apollo if you're using GraphQL
  6. Recoil if you know that you need it and are willing to bet on an unfinished library
- react-query or swr replace the biggest need for Redux or MobX: server cache. 
  - Context is great for what’s left.

- ## [I'm kind of surprised it's 2020 and nobody tried using SQL for frontend state management](https://twitter.com/lmatteis/status/1258503426817785857)
  - I mean, indexedDB is pretty much SQL on local storage.  
- To clarify slightly: I didn't say I "advise against it". I was saying that _if_ the majority of your app is just fetching server state, _and_ you are already using a purpose-built "server fetching/caching" tool, then you probably don't _need_ Redux.
  - Using Redux to cache server-side data is a valid use case.  
  - It's just that Redux isn't a *purpose-built* server cache - you end up writing your own logic to do so.
  - So, I'm not saying you _should_ or _shouldn't_ use Redux either way - just that you wouldn't use both at once.
  - ref

    - https://twitter.com/tannerlinsley/status/1283467225677000706

- ## [Why I Stopped Using Redux](https://dev.to/g_abud/why-i-quit-redux-1knl)
- The Problem with Single Page Applications
  - A big part of frontend development now becomes burdened with how to maintain our global store without suffering from state bugs, data denormalization, and stale data.
- Redux is not a Cache
- A Simpler Approach to Backend State
  - react-query
  - swr
  - apollo-client
- What About Frontend State
  - When the data fetching/caching part of your app is taken care of, there is very little global state for you to handle on the frontend. 
  - What little amount is left can be handled using Context or useContext + useReducer to make your own pseudo-Redux.

- I personally even think `context` is not a primary building block if we go with `useMutableSource` . 
  - My proposal in reactive-react-redux (not react-redux) is not to use context at all
  - ref: [Allow for optionally using React Context instead of Redux under the hood](https://github.com/reduxjs/react-redux/issues/1612)

- ## [Four different approaches to non-Redux global state libraries_201907](https://blog.axlight.com/posts/four-different-approaches-to-non-redux-global-state-libraries/)
  - There are several implementations how to store state and notify changes.

    - whether context based or external store
    - whether context propagation or subscriptions based 

  - S1: Multiple contexts

    - One could easily implement this approach with React context and useContext.
    - lib: constate, unstated-next

  - S2: Select by property names (or paths)

    - This approach is to put more values in a single store. 
    - A single store allows to dispatch one action to change multiple values. 
    - You specify a property name to get a corresponding value. 
    - It’s simple to specify by a name, but somewhat limited in a complex case.
    - lib: react-hooks-global-state, shareon

  - S3: Select by selector functions

    - Selector functions are more flexible than property names. So flexible that it may be misused like doing expensive computations. 
    - Most importantly, performance optimization often requires to keep object referential equality.
    - lib: zustand, react-sweet-state

  - S4: State usage tracking

    - This approach eliminates selector functions, and it’s hardly misused. One big concern is performance optimization.
    - lib: react-tracked

- ## [Four patterns for global state with React hooks: Context or Redux_201905](https://blog.axlight.com/posts/four-patterns-for-global-state-with-react-hooks-context-or-redux/)
- S1: the most basic pattern should still be **prop passing**
  - alternative to Prop passing: [Component passing](https://patrickroza.com/blog/component-vs-prop-drilling-in-react/)

- S2: If an app needs to share state among components that are more deep than two level, it’s time to introduce **context**
  - Note that all components with `useContext(ContextA)` will re-render if stateA is changed, even if it’s only a tiny part of the state. 
  - Hence, it’s not recommended to use a context for multiple purpose.

- S3: Using **multiple contexts** is fine and rather recommended to separate concerns. 
  - Contexts don’t have to be application-wide and they can be used for parts of component tree. 
  - Only if your contexts can be used anywhere in your app, defining them at the root is a good reason.

- S4: The biggest limitation with multiple contexts is that dispatch functions are also separated. 
  - If your app gets big and several contexts need to be updated with a single action, it’s time to introduce **Redux**. 
  - (Or, actually you could dispatch multiple actions for a single event, I personally don’t like that pattern very much.)

- ## 精读《React Hooks 数据流》
- 单组件最简单的数据流一定是 `useState`

- 组件间共享数据流最简单的方案就是 `useContext`

  - 问题是数据与UI不解耦，这个问题 `unstated-next` 可以作为解决方案
- 数据流与组件解耦 `unstated-next`

  - 可以将定义在App中的数据单独出来，然后Counter和App不再绑定
  - 但是useState无法合并更新，可以使用useReducer
  - Counter.useContainer提供的数据流是一个引用整体，其子节点foo引用变化后会导致整个Hook重新执行，继而所有引用它的组件也会重新渲染，此时可以使用可以利用Redux的 `useSelector` 实现按需更新
- 对于极限场景，即便控制了重渲染次数与返回结果的引用最大程度不变，还是可能存在性能问题，这最后一块性能问题就出在useSelector上
  - useSelector的第二个参数靠考虑使用deepEquals
  - 一种方式是利用reselect根据参数引用进行缓存
- 结合外部变量的缓存查询
  - 为了不在组件函数内调用 createSelector，我们需要尽可能将用到外部变量的地方抽象成一个通用 Selector，并作为 createSelector 的一个先手环节
  - 对于外部变量结合的环节，还需要 useMemo 与 useSelector 结合使用，useMemo 处理外部变量依赖的引用缓存，useSelector 处理 Store 相关引用缓存。

```JS
// 只用context
const CountContext = createContext();

function App() {
  const [count, setCount] = useState();
  return (
    <CountContext.Provider value={{ count, setCount }}>
      <Child />
    </CountContext.Provider>
  );
}

function Child() {
  const { count } = useContext(CountContext);
}

// 使用unstated-next
import { createContainer } from "unstated-next";

function useCounter() {
  const [count, setCount] = useState();
  return { count, setCount };
}

const Counter = createContainer(useCounter);

function App() {
  return (
    <Counter.Provider>
      <Child />
    </Counter.Provider>
  );
}

function Child() {
  const { count } = Counter.useContainer();
}
```

- ## 针对context的value频繁更新导致重复渲染性能降低的问题
- [RFC: Context selectors](https://github.com/gnoff/rfcs/blob/context-selectors/text/0000-context-selectors.md)
  - https://github.com/reactjs/rfcs/pull/119

- [RFC: useMutableSource](https://github.com/reactjs/rfcs/blob/master/text/0147-use-mutable-source.md)
  - enables React components to safely and efficiently read from a mutable external source in Concurrent Mode

- With context selectors, we might still be facing the "unconditional render starting at the root" and "calculating selectors while rendering" aspects. It's possible that useMutableSource may allow us to work around that. But, at least we wouldn't be forcing every connected component to fully re-render.
  - `useMutableSource()` seems to aim at solving this problem officially

- 有没有什么办法可以优化一下：使得不该更新的组件不rerender呢？
  - 定义了一个Provider组件，但是它的 value 是一个通过 useRef 创建的值。
  - 只有触发 forceUpdate 才会更新组件
  - 总不能每次改变应用状态的时候，都要调用一次 forceupdate 吧，再对上面的示例做一次优化，请看这个优化版本 ，在这个版本中，我们实现一个简单的发布订阅库，在 useStore 方法中订阅子组件的 forceUpdate 到 subscribers 中 ，在 Provider 组件 render 的时候，调用 notify 方法依次调用 subscribers 中的所有 foreUpdate，以此来触发子组件rerender。
# survey: state management

- [How are you currently managing your state? Redux/hooks/MobX/something else?](https://twitter.com/kefimochi/status/1248006010972692481)
- [How are you handling React state today?](https://twitter.com/housecor/status/1252306374375149568)
  - react
  - redux
  - mobx
  - other
- ## [survey: What is your go-to for consuming server-state in your React apps?](https://twitter.com/tannerlinsley/status/1283112469574021120)
  1. ReactQuery / SWR / Apollo
  2. Redux / Mobx / other "global state" manager
  3. useState/Reducer + context / roll it myself
  - Answered #3. 

    - Reason being is that our server state isn't at a complexity where it would heavily benefit from an Apollo or Redux and it's easier for other engineers to understand if we all just stuck with vanilla React.

  - Pick #3 for global stuff, like a user or a cart (in e commerce), 

    - because I havent figured out how #1 does with a context global state. 
    - Full ignorance on my side, but local component state, i have used swr when it needs to fetch data

  - I've tried them all. 

    - I think they all can have a place. Redux worked really well in the pre-hook era. 
    - If you want to tightly control your actions, use all sorts of middleware, observables, it's the thing to use.
    - There was an era where I was using context too as I saw it as "native redux." 
    - It was nice to use as much boilerplate as I wanted, but really that was still too much boilerplate. 
    - There were examples of when I had to have useCallback or complicated reducer patterns.
    - Finally, I worked with/made with GraphQL APIs for about a year. 
    - I loved Apollo. Really gave me it all. 
    - Originally had it with behind context, ended up just using Apollo. 
    - Now I'm consuming more RESTful APIs and wanted something with similar benefits. Went with react-query.
    - I really think react-query and SWR are often the best choice for folks. 
    - They're SIMPLE solutions to manage state globally and at a component level. 
    - There can be as much boilerplate as you want too. 
    - Use the hook directly or hide it behind something else. Either works.
    - I went with react-query because of the quality of it's docs too. Redux and Apollo have had GREAT docs for a long time. As long as I have used react-query, it has too. TypeScript support was also a must for me. Even though swr has better ts support, React-query's was good enough.

  - With Firestore I’m using Redux + Redux-observable as middleware. Next time I’ll go with react query but I should pay attention to the number of reads/writes because u pay for those with Firebase
# context vs redux
- viewpoint
  - My personal summary is that new context is ready to be used for low frequency unlikely updates (like locale/theme). It's also good to use it in the same way as old context was used. I.e. for static values and then propagate updates through subscriptions. It's not ready to be used as a replacement for all Flux-like state propagation.
  - The Context API (currently) is not built for high-frequency updates (quote of Sebastian Markbage, React Team), it’s not optimized for that. The react-redux people ran into this problem when they tried to switch to React Context internally in their package
  - In my opinion, for low-frequency updates like locale, theme changes, user authentication, etc. the React Context is perfectly fine. But with a more complex state which has high-frequency updates, the React Context won't be a good solution. Because, the React Context will trigger a re-render on each update, and optimizing it manually can be really tough. And there, a solution like Redux is much easier to implement.

- Redux is a predictable state management library and architecture which easily integrates with React.
- The primary selling points of Redux are:
  - Deterministic state resolution
    - enabling deterministic view renders when combined with pure components
  - Transactional state.
  - Isolate state management from I/O and side-effects.
  - Single source of truth for application state.
  - Easily share state between different components.
  - Transaction telemetry (auto-logging action objects).
  - Time travel debugging.
- The primary selling points of React hooks are:
  - Use state and hook into the component lifecycle without using a class.
  - Colocate related logic in one place in your component, rather than splitting it between various lifecycle methods.
  - Share reusable behaviors independent of component implementations (like the render prop pattern).
- You may have a good use case for React’s built-in component state model if your component:
  - Doesn’t use the network I/O.
  - Doesn’t save or load state.
  - Doesn’t share state with other non-child components.
  - Does need some ephemeral local component state
- should you put everything in Redux? Won’t it break time travel debugging if you don’t?
  - No, because there is a lot of state in an application which is ephemeral and too granular to provide very useful information for things like logging telemetry or time travel debugging.
- Redux is useful if your component:
  - Uses I/O like network or device APIs.
  - Saves or loads state.
  - Shares its state with non-child components.
  - Deals with any business logic or data processing shared with other parts of the application.
- It uses Redux because we need the data this form cares about in other parts of the UI, and when we’re done with the purchase flow, we’ll need to save the data to a database.
  - The state it cares about is shared between components, not localized to a single component, it’s persisted rather than ephemeral, and it potentially spans multiple page views or sessions. 
  - These are all things that local component state won’t help with unless you build your own state container library on top of the React API — and that’s a lot more complicated than just using Redux.
- In the future, React’s suspense API may help with saving and loading state. 
  - We’ll need to wait until the suspense API lands to see if it can replace my saving/loading patterns in Redux.
  - Redux allows us to cleanly separate side-effects from the rest of the component logic without requiring us to mock I/O services. (Isolation of effects is why I prefer redux-saga over thunks). 
  - In order to compete with this use-case for Redux, React’s API’s will need to afford effect isolation.
- Redux is a lot more (and often a lot less) than a state management library. 
  - It’s also essentially a subset of the Flux Architecture which is more opinionated about how state changes are made.
  - Redux has always been more architecture and unenforced convention than library. 
  - In fact, the essential implementation of Redux can be reproduced in a couple dozen lines of code.
- Does determinism break if everything isn’t in Redux?
  - No. In fact, Redux doesn’t enforce determinism, either. Convention does. If you want your Redux state to be deterministic, use pure functions. If you want your ephemeral component state to be deterministic, use pure functions.
- Don’t you need Redux as a single source of truth?
  - The single source of truth principle does not state that you need all of your state to come from a single source. Instead, it means that for each piece of state, there should be a single source of truth for that state. You can have many different pieces of state, each with their own single source of truth.
  - That means you can choose what goes into Redux, and what goes into component state. You can also get state from other sources, like the browser APIs for the current location href.
  - If your component state is localized to a single component and only used in one place, by definition, it already has a single source of truth for that state: React component state.
  - It’s fine to put everything in Redux if you need to. There may be performance implications for state that needs to update frequently, or components with lots of dependent state. You shouldn’t worry about performance unless it becomes an issue, but when you do, try both ways and see if it has an impact. Profile, and remember the RAIL performance model.
- Should I use react-redux connect, or the hooks API?
  - That depends. 
  - `connect` creates a reusable higher-order component, whereas the hooks API is optimized for integration with a single component.
  - Will you need to connect the same store props to other components? Go with `connect` . 
  - Otherwise, I prefer how the hooks API reads. 
  - In other words, I find the `connect` API does the job with concise code, but it’s not particularly readable or ergonomic. If I don’t need to reuse the connection for other components, I much prefer the infinitely more readable hooks API, even though it involves slightly more typing.
- If singletons are an anti-pattern, and Redux is a singleton, isn’t Redux an anti-pattern?
  - No. Singletons are a code-smell that could indicate shared mutable state, which is the real anti-pattern. 
  - Redux prevents shared mutable state via encapsulation (you should not be mutating app state directly outside of reducers, instead, Redux handles state updates) and message passing (only dispatched action objects can trigger state updates).

- Is Redux dead, dying, deprecated, or about to be replaced?
  - No
- Like any tool, it's important to understand the tradeoffs and benefits before deciding to use something.
- The new context API is going to be great for passing down data to deeply nested components - that's exactly what it was designed for. 
  - If you're only using Redux to avoid passing down props, context could replace Redux - but then you probably didn't need Redux in the first place. 
  - Context also doesn't give you anything like the Redux DevTools, the ability to trace your state updates, middleware to add centralized application logic, and other powerful capabilities that Redux enables.
- It's also worth noting that context is just a mechanism for making a value available to a nested subtree of components, and it's not a state management approach in and of itself. 
- React-Redux does use context, but only to pass down the store instance, not the current state value.
- As already mentioned, if avoiding prop-drilling was the only reason you were using Redux (and React-Redux), then sure, Redux isn't necessary in this case.
- However, as with the Context API itself, the `useReducer()` hook doesn't have the additional capabilities that Redux allows. There's no time-travel debugging, no middleware, and no DevTools Extension to see how the state has changed over time.
- There are still many excellent reasons to choose Redux:
  - **Debugging capabilities like time-travel**
  - **Middleware**
  - Consistent architectural patterns
  - Addons and extensibility
  - Cross-platform and cross-framework usage
  - Depending on your app's setup, much better performance than working with just Context

- ref
  - [Redux - Not Dead Yet!](https://blog.isquaredsoftware.com/2018/03/redux-not-dead-yet/)
  - [Do React Hooks Replace Redux?](https://medium.com/javascript-scene/do-react-hooks-replace-redux-210bab340672)
# fetchData

# 基于context

- ref
  - [基于 React Context 的状态管理思考（一）](https://juejin.im/post/5d5ea99be51d45620064bb52)

- constate
  - With Constate, you'll have multiple contexts provided at different levels of your component tree (depending on each components use them). 
  - Also, it's a seamlessly migration from local state (with React hooks) to shared ones, which is not supported by Redux (so easily).
  - ref
    - https://github.com/diegohaz/constate/issues/81

- unstated-next
  - My advice is to avoid putting everything at the top-level of your app unless it actually needs to be there.
  - But if this is actually a problem, you can use compose
  - Of course this still produces a fairly large tree. 
  - But I don't want to build anything more complex in, and until/unless React gives us a useProvider(...) or a way to provide multiple contexts at once, that problem is gonna stick around.

- `Context.Provider` 的 `value` 更新的时候，会默认通知所有使用了useContext该Context订阅的子组件重新渲染。这个在项目复杂的时候，性能上会变差。
- 所以要么就对多个模块分别使用不同Context来管理状态，要么就得参考react-redux的思路，通过对比新旧值来让真正需要渲染的子组件重新渲染。
- 比较难解决的是thunk，redux中在dispatch执行前对action做判断，如果是异步action则传入middlewareAPI并执行，如果是同步action则立即dispatch。react中的dispatcher是一个用于启动performWork的scheduler（用于安排调度任务到任务队列）。redux的dispatch是原子操作，只有当所有reducers执行完毕才会通知订阅者进行下一步操作（redux理念中reducers是纯函数，subscriptions是副作用），确保getState不会脏读state，但是react是吗？ReactDispatcher执行单元是一个fiber，每个hook fiber实例（使用了useReducer）执行reducer后进行setState操作，组件实例执行的同时也等于通知订阅，它并不会关心（或者等）其他组件是否执行完毕，也就是在reducers没有全部执行完就去读全局state，造成脏读。（如果此时往全局state写入新值就更加错误了，也可以说没有保证事务隔离。）这也是concurrent并发调度模式所存在的难题。所以，既然难以保证IO操作拥有足够的隔离性，所以可以使用惰性求值（或者异步）来进行IO操作，即将所有组件pure纯化（访问全局context就不纯），将所有IO操作推迟到纯函数执行之后。譬如ReactDOM.render的第三个参数表示在一次完整的render之后执行一次操作，此时进行副作用IO。
- 全局变量共享是一个复杂的问题，在并发访问时尤为突出。不过只要保证组件足够纯，再隔离副作用就好了。纯函数的优势就是并发，副作用IO可以交给异步任务队列执行，或者是用Monad来处理IO，保证IO操作次序，IO操作是需要保证先后顺序的，纯函数不需要
- react的useEffect就是pure操作，将副作用包裹在了Monad里（可以理解为外面又包了一层函数），react调度机制会在一轮渲染之后执行这些副作用操作，保证了副作用与函数组件主体的充分隔离。也就是目前的react已经实现了部分Monad机制。（说是部分因为现在还没有join运算，没办法把一个IO操作映射为另一个IO操作，即(a -> b) -> IO a -> IO b，也就是Functor，可以将Monad解包运算后再封包，，好吧其实这个理解了之后可以自己实现，封包就是f变成()=>f()，解包就是执行封包后的函数即(()=>f())()，解包运算之后再包一层函数纯化返回到Monad即可。）
# recoil
- ref
  - [Recoil - Facebook官方React状态管理器](https://juejin.im/post/5ec0f5905188256d8c4a99b8)
- 优点
  - 之前状态管理器满天飞，如果官方能一统天下，应该算一件好事情。
  - 对React concurrent模式支持良好。
- 不足
  - 当前Recoil还处于开发阶段，文档都还不是很全。
  - 目前不支持ts，需要@types/recoil
  - 目前没有支持Class组件消费状态
  - API偏多，一共19个，同类可以合并
  - 消费状态需要import多项，useRecoilState, store
  - 没有足够的亮点吸引用户
# state management using subscription
- ref 
  - [使用React Hooks进行状态管理 - 无Redux和Context](https://juejin.im/post/5d783fca6fb9a06af50ff577)
  - [State Management with React Hooks — No Redux or Context API](https://medium.com/javascript-in-plain-english/state-management-with-react-hooks-no-redux-or-context-api-8b3035ceecf8)
  - 实现时只用到了 `useState` 返回值的第2个变量，用来触发内部state更新
  - If you ever worked with complex state management library, you know that it is not the best idea to manipulate global state directly from the components

    - The best way is to separate the business logic by creating actions which manipulate the state.

```JS
import { useState, useEffect } from 'react;

// 设置为let因为清理时会替换
let listeners = [];
// 每次都会创建新的state对象
let state = { counter: 0 };

const setState = (newState) => {
  // 每次都会创建一个新的state对象，那每次都会render
  state = { ...state, ...newState }
  listeners.forEach((listener) => {
    listener(state)
  })
}

// 自定义hook
const useGlobalState = () => {
  // 不提供初始state只是第一次为undefined，后面每次render都会用新state对象replace
  const newListener = useState()[1];
  useEffect(
    () => {
      listeners.push(newListener);

      return () => {
        listeners = listeners.filter(listener => listener != newListener)
      }
    },
    []
  )
  // 直接暴露
  return [state, setState];
}

// 使用示例
const Counter = () => {
  const [globalState, setGlobalState] = useGlobalState();

  const add1Global = () => {
    const newCounterValue = globalState.counter + 1;
    setGlobalState({ counter: newCounterValue });
  };

  return (
    <div>
      <p>
        counter: {globalState.counter}
      </p>
      <button type="button" onClick={add1Global}>
        +1 to global
      </button>
    </div>
  );
};
```

- [Steps to Develop Global State for React With Hooks Without Context](https://blog.axlight.com/posts/steps-to-develop-global-state-for-react/)
  - Usually, the global variable is in a file scope. Let’s put it in a function scope to narrow down the scope a bit and make it more reusable.
  - Although we can create multiple containers, usually we put several items in a global state.
    - Typical global state libraries have some functionality to scope only a part of the state. 
    - For example, React Redux uses selector interface to get a derived value from a global state.
    - We take a simpler approach here, which is to use a string key of a global state.
- **react-hooks-global-state** is a library to provide a global state with React Hooks
  - Optimization for shallow state getter and setter.
    - The library cares the state object **only one-level deep**.
  - TypeScript type definitions
    - A creator function creates hooks with types inferred.
  - Redux middleware support to some extent
    - Some of libraries in Redux ecosystem can be used.
    - Redux DevTools Extension could be used in a simple scenario.
  - Concurrent Mode support (Experimental)
    - Undocumented useGlobalStateProvider supports CM without React Context.
  - [v2] new implementation with useMutableSource
- issues
  - [changelog](https://github.com/dai-shi/react-hooks-global-state/blob/master/CHANGELOG.md)
  - observedBits 32bit limitation
    - Option 1: we rotate the index. % 31
    - Option 2: we use multiple contexts for each 31 items.
    - Option 3: multiple contexts for each items. Do not rely on observedBits
    - Option 4: we pass non-updating "store" in the context, and let hooks subscribe for key-based changes. This is mostly like the previous implementation which requires useState.
    - https://github.com/dai-shi/react-hooks-global-state/issues/1
  - redux-like API design question
    - https://github.com/dai-shi/react-hooks-global-state/issues/3
    - dispatch vs update 
  - Great work! And some comments/tips
    - https://github.com/dai-shi/react-hooks-global-state/issues/8
  - react-hooks-global-state vs react-tracked
    - https://github.com/dai-shi/react-hooks-global-state/issues/40
    - react-hooks-global-state offers the property-based accessor useGlobalState(name) where name has to be a property (string).
    - react-tracked provides useTrackedState which is a unique API with "state usage tracking". 
      - It will track the state object usage in deep (even nested objects are tracked) and only trigger re-renders if the used part of the state is changed. 
      - It also provides useSelector which is similar to the one in react-redux.
    - react-hooks-global-state has an external store just like Redux.
      - Although it's tied to React unlike Redux, it's definitely defined outside React.
    - react-tracked has a state internally in the React component. 
      - You can only update through React just like normal React state + context.
    - A general note about external stores: 
      - With upcoming Concurrent Mode, there's useTransition hook which allows "branching state". 
      - This is only possible with state inside React. 
      - So, react-hooks-global-state won't get benefits from that feature. 
      - react-hooks-global-state should still be CM-safe though.
# ref
- [精读《React Hooks 数据流》](https://zhuanlan.zhihu.com/p/126476910)
- [精读《Hooks 取数 - swr 源码》](https://zhuanlan.zhihu.com/p/91228591)
- [精读《recoil》](https://zhuanlan.zhihu.com/p/143335599)
- [编写一个管理异步的React Hook](https://zhuanlan.zhihu.com/p/58840809)
- [Provide more ways to bail out inside Hooks](https://github.com/facebook/react/issues/14110)
- [XState状态管理 - 基于Actor模式](https://blog.zfanw.com/xstate-state-management/)
- [说说react hooks做状态管理这件事-hooks+Context篇](https://webfe.kujiale.com/yong-hooks/)
- [The Problem with React's Context API](https://leewarrick.com/blog/the-problem-with-context/)
- [Steps to Develop Global State for React With Hooks Without Context](https://blog.axlight.com/posts/steps-to-develop-global-state-for-react/)
- [useReducer + useContext vs react-hooks-global-state](https://blog.axlight.com/posts/react-hooks-tutorial-for-pure-usereducer-usecontext-for-global-state-like-redux-and-comparison/)
- [How to Handle Async Actions for Global State With React Hooks and Context](https://blog.axlight.com/posts/how-to-handle-async-actions-for-global-state-with-react-hooks-and-context/)
- [Unstated vs Unstated-Next](https://github.com/jamiebuilds/unstated-next/issues/20)
- [细聊Concent&Recoil , 探索react数据流的新开发模式](https://zhuanlan.zhihu.com/p/148280552)
- [深入理解 react/redux 数据流并基于其优化前端性能](https://github.com/shaozj/blog/issues/36)
- [`useSubscription` and `useMutableSource` tearing and deopt behavior.](https://gist.github.com/bvaughn/054b82781bec875345bd85a5b1344698)
