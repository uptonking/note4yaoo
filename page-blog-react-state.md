---
tags: [blog, react, state]
title: page-blog-react-state
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-04T18:05:21.229Z'
---

# page-blog-react-state

## pieces

---

- 精读《React Hooks 数据流》
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

``` JS
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

---

- 针对conetxt的value频繁更新导致重复渲染性能降低的问题
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

- 状态管理要解决的问题是跨组件状态共享
  - state声明、读取、修改
- `useState` doesn't offer a way to bail out of rendering once an update is being processed. 
  - This gets a bit weird because we actually process updates during the rendering phase. So we're already rendering. 
  - But we could offer a way to bail on children. 
  - Edit: we now do bail out on rendering children if the next state is identical.
- `useContext` doesn't let you subscribe to *a part of the context value* (or some memoized selector) without fully re-rendering.

- `React.memo` cannot prevent rerender caused by high-frequency updates of context value
  - Let's say for some reason you have `AppContext` whose value has a theme property, and you want to only re-render some `ExpensiveTree` on `appContextValue.theme` changes.
  - note that option 1 is preferable — if some context changes too often, consider splitting it out.
  - **Option 1 (Preferred): Split contexts that don't change together**
    - If we just need `appContextValue.theme` in many components but `appContextValue` itself changes too often, we could split `ThemeContext` from `AppContext` .
    - Now any change of `AppContext` won't re-render `ThemeContext` consumers.
    - This is the preferred fix. Then you don't need any special bailout.

``` JS
  function Button() {
    let theme = useContext(ThemeContext);
    // The rest of your rendering logic
    return <ExpensiveTree className={theme} />;
  }
```

  - **Option 2: Split your component in two, put `memo` in between**
    - If for some reason you can't split out contexts, you can still optimize rendering by splitting a component in two, and passing more specific props to the inner one.
    - You'd still render the outer one, but it should be cheap since it doesn't do anything.

``` JS
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

  - **Option 3: One component with `useMemo` inside**
    - Finally, we could make our code a bit more verbose but keep it in a single component by wrapping return value in `useMemo` and specifying its dependencies. 
    - Our component would still re-execute, but React wouldn't re-render the child tree if all `useMemo` inputs are the same.

``` JS
function Button() {
  let appContextValue = useContext(AppContext);
  let theme = appContextValue.theme; // Your "selector"

  return useMemo(() => {
    // The rest of your rendering logic
    return <ExpensiveTree className={theme} />;
  }, [theme])
}
```

  - **Option 4: Pass a subscribe function as context value**, just like in legacy context era
    - It might be the only option if you don't control the usages (needed for options 2-3) and can't enumerate all the possible selectors (needed for option 1), but still want to expose a Hooks API
    - This is basically what react-redux does internally
    - To implement subscribe function, you can use something like Observables or EventEmitter, or just write a basic subscription logic yourself
    - we stopped passing the store state in context (the v6 implementation) and switched back to direct store subscriptions (the v7 implementation) due to a combination of performance problems and the inability to bail out of updates caused by context (which made it impossible to create a React-Redux hooks API based on the v6 approach).

``` JS
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

``` JS
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

  - **Option 5: Do not use context for data propagation but data subscription**  
    - Use useSubscription (because it's hard to write to cover all cases).

  - Option x1: use an unofficial workaround.
    - useContextSelector proposal and use-context-selector library in userland.

## context vs redux

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

- Redux offers a tradeoff. It asks you to:
  - Describe application state as plain objects and arrays.[state]
  - Describe changes in the system as plain objects.[action]
  - Describe the logic for handling changes as pure functions.[reducer]
- None of these limitations are required to build an app, with or without React. In fact these are pretty strong constraints, and you should think carefully before adopting them even in parts of your app.
- These limitations are appealing to me because they help to
  - Persist state to a local storage 
  - Pre-fill state on the server, send it to the client in HTML 
  - Serialize user actions and attach them, together with a state snapshot, to automated bug reports, so that the product developers can replay them to reproduce the errors.
  - Pass action objects over the network to implement collaborative environments without dramatic changes to how the code is written.
  - Maintain an undo history or implement optimistic mutations without dramatic changes to how the code is written.
  - Travel between the state history in development, and re-evaluate the current state from the action history when the code changes, a la TDD.
  - Provide full inspection and control capabilities to the development tooling so that product developers can build custom tools for their apps.
  - Provide alternative UIs while reusing most of the business logic.
- However, if you’re just learning React, don’t make Redux your first choice. Instead learn to think in React. Come back to Redux if you find a real need for it, or if you want to try something new.
- Finally, don’t forget that you can apply ideas from Redux without using Redux.

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
  - [You Might Not Need Redux_2016](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)
  - [Redux - Not Dead Yet!](https://blog.isquaredsoftware.com/2018/03/redux-not-dead-yet/)
  - [Do React Hooks Replace Redux?](https://medium.com/javascript-scene/do-react-hooks-replace-redux-210bab340672)

## fetchData

## 基于context

- ref
  - [基于 React Context 的状态管理思考（一）](https://juejin.im/post/5d5ea99be51d45620064bb52)

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

## recoil

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

## state management using subscription

- ref 
  - [使用React Hooks进行状态管理 - 无Redux和Context](https://juejin.im/post/5d783fca6fb9a06af50ff577)
  - [State Management with React Hooks — No Redux or Context API](https://medium.com/javascript-in-plain-english/state-management-with-react-hooks-no-redux-or-context-api-8b3035ceecf8)
  - 实现时只用到了 `useState` 返回值的第2个变量，用来触发内部state更新
  - If you ever worked with complex state management library, you know that it is not the best idea to manipulate global state directly from the components
    - The best way is to separate the business logic by creating actions which manipulate the state.

``` JS
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

## guide

- ref
  - [精读《React Hooks 数据流》](https://zhuanlan.zhihu.com/p/126476910)
  - [精读《Hooks 取数 - swr 源码》](https://zhuanlan.zhihu.com/p/91228591)
  - [精读《recoil》](https://zhuanlan.zhihu.com/p/143335599)
  - [编写一个管理异步的React Hook](https://zhuanlan.zhihu.com/p/58840809)
  - [Provide more ways to bail out inside Hooks](https://github.com/facebook/react/issues/14110)
  - [Preventing rerenders with React.memo and useContext hook](https://github.com/facebook/react/issues/15156)
  - [XState状态管理 - 基于Actor模式](https://blog.zfanw.com/xstate-state-management/)
  - [说说react hooks做状态管理这件事-hooks+Context篇](https://webfe.kujiale.com/yong-hooks/)
  - [The Problem with React's Context API](https://leewarrick.com/blog/the-problem-with-context/)
  - [Steps to Develop Global State for React With Hooks Without Context](https://blog.axlight.com/posts/steps-to-develop-global-state-for-react/)
  - [useReducer + useContext vs react-hooks-global-state](https://blog.axlight.com/posts/react-hooks-tutorial-for-pure-usereducer-usecontext-for-global-state-like-redux-and-comparison/)
  - [How to Handle Async Actions for Global State With React Hooks and Context](https://blog.axlight.com/posts/how-to-handle-async-actions-for-global-state-with-react-hooks-and-context/)
  - [Unstated vs Unstated-Next](https://github.com/jamiebuilds/unstated-next/issues/20)
