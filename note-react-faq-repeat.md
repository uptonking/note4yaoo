---
title: note-react-faq-repeat
tags: [faq, react]
created: '2021-06-10T06:26:55.150Z'
modified: '2021-06-10T06:44:27.120Z'
---

# note-react-faq-repeat

# faq
## 

## useEffect vs useLayoutEffect

- [useEffect vs. useLayoutEffect in plain, approachable language](https://blog.logrocket.com/useeffect-vs-uselayouteffect/)
- With every click of the button, the counter state is updated, the DOM mutation printed to the screen, and the effect function triggered.
  1. The user performs an action, i.e., clicks the button.
  2. React updates the count state variable internally.
  3. React handles the DOM mutation.
    - The text content of the h1 element has to be changed from “the current count is previous value” to “the current count is new value.”
  4. The browser paints this DOM change to the browser’s screen. 浏览器自身的渲染管线在这里
    - React hands over the details about the DOM mutation to the browser engine, which figures out the entire process of painting the change to the screen.
  5. Only after the browser has painted the DOM change(s) is the `useEffect` function fired.
    - Although useEffect is deferred until after the browser has painted, it’s guaranteed to fire before any new renders.

- Unlike `useEffect`, the function passed to the `useLayoutEffect` Hook is fired synchronously after all DOM mutations.
  - `useLayoutEffect` doesn’t really care whether the browser has painted the DOM changes or not. 
  - It triggers the function right after the DOM mutations are computed.
  - updates scheduled inside `useLayoutEffect` will be flushed synchronously, before the browser has a chance to paint.

- I’ll highlight three examples that amplify the significance of the differences between useEffect and useLayoutEffect.
  - https://codesandbox.io/s/useeffect-uselayouteffect-time-of-execution-2-kqnqp


## 使用ReactDOM.createPortal和ReactDOM.render的区别

- https://codesandbox.io/s/42x771ykwx
  - 在render()方法中，在可以使用ReactDOM.createPortal的地方也可以使用ReactDOM.render
  - ReactDOM.unstable_renderSubtreeIntoContainer 也能传递context

- [How to use ReactDOM.createPortal() in React 16?](https://stackoverflow.com/questions/46393642)
  - Even though the component rendered through the portal is rendered somewhere else (Outside the current container root), it remains present as the child of the same parent component. (Who invoked the ReactDOM.createPortal) So **any events on the child are propagated to the parent**.
  - Same **context is accessible inside the component rendered through a portal**. But not in the case when we do `ReactDOM.render` directly.

## context selector

- [Implement useSelector equivalent for React Context?](https://stackoverflow.com/questions/59741558)
- No, it's not possible. 
  - Any time you put a new context value into a provider, all consumers will re-render, even if they only need part of that context value.
  - That's specifically one of the reasons why we gave up on using context to propagate state updates in React-Redux v6, and switched back to using direct store subscriptions in v7.
  - Last time I checked, the `useContextSelector` lib works by hacking around its normal behavior. It uses the undocumented `unstable_changedBits` option to force the context consumers to never actually update as they normally would, then uses subscriptions to bypass the normal rendering flow and trigger additional re-renders. 
- it is not possible, but you can work around it without using external dependencies and without falling back to doing manual subscriptions.
  - As a workaround, you can let the component re-render, but skip the VDOM reconciliation by memoizing the returned React element with `useMemo`.

```JS
function Section(props) {
  const partOfState = selectPartOfState(useContext(StateContext))

  // Memoize the returned node
  return useMemo(() => {
    return <div>{partOfState}</div>
  }, [partOfState])
}
```

## useMemo vs React.memo

- `useMemo` is a function as a hook that returns a memoized value.
  - useMemo will only recompute the memoized value when one of the dependencies (either a or b) has changed
  - hooks should be used only at the top level from react functions
- `React.memo` is a higher order component that can optimize rendition of your component given that it renders the same output with the same properties.
  - props itself is a new object on every render. memo() does shallow comparison by default. 
  - You can think of memo() as a useMemo() with a list of all your props like [props.foo, props.bar, props.foobar] except you don't need to type them all manually. It's a shortcut for the most common case.
  - Basically if your component breaks without memo then you're not using it correctly. It only serves as perf optimization.

- https://stackoverflow.com/questions/55466104
- React.memo is a higher order component.
- React.useMemo on the other hand is more generic hook function, and returns a memoized value
  - while it can be hacked to be used instead of React.memo, it's not its purpose and it will add to the confusion more than it will help
  - useMemo is a hook and is subject to the certain usage rules.

- [Is it safe to useMemo for JSX?](https://stackoverflow.com/questions/60453845)
- Memoizing JSX expressions is part of the official useMemo API
  - `useMemo` memoizes individual children and computed values, given any dependencies. 
  - You can think of `memo` as a shortcut of `useMemo` for the whole component, that compares all props.
- But `memo` has one flaw - it doesn't work with `children` prop
  - children are part of the props.
  - And React.createElement always creates a new immutable object reference (REPL). 
  - So each time `memo` compares props, it will determine that `children` reference has changed, if not a primitive.
  - To prevent this, you can either use useMemo in parent App to memoize children (which you already did). Or define a custom comparison function for memo, so Modal component now becomes responsible for performance optimization itself. react-fast-compare is a handy library to avoid boilerplate for areEqual.

```typescript

function Parent({ a, b }) {
  // Only re-rendered if `a` changes:
  const child1 = useMemo(() => <Child1 a={a} />, [a]);
  // Only re-rendered if `b` changes:
  const child2 = useMemo(() => <Child2 b={b} />, [b]);
  return (
    <>
      {child1}
      {child2}
    </>
  )
}
```

- Is it safe? Yes. At the end of the day the JSX is just converted into a JSON object, which is totally fine to memoize.

## How to implement useState with useReducer

```JS
// 简单版
const stateReducer = (prevState, newState) =>
  typeof newState === 'function' ? newState(prevState) : newState

const stateInitializer = initialValue =>
  typeof initialValue === 'function' ? initialValue() : initialValue

function useState(initialValue) {
  return React.useReducer(stateReducer, initialValue, stateInitializer)
}
```

```typescript
// 完整版
function useState<T>(initialState: T | (() => T)) {
  const initState: T =
    typeof initialState === 'function' ? initialState() : initialState;

  const [state, dispatch] = React.useReducer(
    (state: T, action: T | ((prev: T) => T)) => {
      return typeof action === 'function' ? action(state) : action;
    },
    initState,
  );

  return [
    state,
    (value: T | ((prev: T) => T)) => {
      if (value !== state) {
        dispatch(value);
      }
    },
  ];
}
```

- ref
  - https://kentcdodds.com/blog/how-to-implement-usestate-with-usereducer
  - https://www.jianshu.com/p/7cbf04c6bcc6

## redux vs useReducer

- [Why React Context is Not a "State Management" Tool (and Why It Doesn't Replace Redux)](https://blog.isquaredsoftware.com/2021/01/context-redux-differences/)
- React-Redux uses Context internally. 
  - However, it's critical to note that React-Redux only passes down the Redux store instance via context, not the current state value!.
  - The actual Redux store is injected into the tree at runtime using the React-Redux `<Provider>` component.
- "state management" means having ways to:
  - store an initial value
  - read the current value
  - update a value
- React's useState and useReducer hooks are good example of state management.
- Redux and MobX are clearly state management as well
- We can even say that server caching tools like React-Query, SWR, Apollo, and Urql fit the definition of "state management"
  - they store initial values based on the fetched data, return the current value via their hooks, 
  - allow updates via "server mutations", and notify of changes via re-rendering the component.
- Context is not a "state management" tool!
  - Context does not "store" anything itself.
  - The parent component that renders a `<MyContext.Provider>` is responsible for deciding what value is passed into the context, and that value typically is based on React component state. 
  - The actual "state management" is happening with the `useState/useReducer` hook.

- Context + useReducer does look an awful lot like Redux + React-Redux.
- Context + useReducer relies on passing the current state value via Context. React-Redux passes the current Redux store instance via Context.
  - That means that when `useReducer` produces a new state value, all components that are subscribed to that context will be forced to re-render, even if they only care about part of the data. This may lead to performances issue
  - With React-Redux, components can subscribe to specific pieces of the store state, and only re-render when those values change.
- Context + useReducer are React features, and therefore cannot be used outside of React. 
  - A Redux store is independent of any UI, and so it can be used separate from React.
- The React DevTools allow viewing the current context value, but not any of the historical values or changes over time.
  - The Redux DevTools allow seeing all actions that were dispatched, the contents of each action, the state as it existed after each action was processed, and the diffs between each state over time.
- `useReducer` does not have middleware. 
  - You can do some side-effect-y things with `useEffect` in combination with useReducer
  - I've even seen some attempts to wrap useReducer with something that resembles a middleware, but both of those are severely limited in comparison to the functionality and capabilities of Redux middleware.
- There's a lot of posts out there that recommend setting up multiple separate contexts for different chunks of state, both to cut down on unnecessary re-renders and to scope concerns. 
  - Some of those also suggest adding your own "context selector components", which require a mixture of React.memo(), useMemo(), and carefully splitting things up so there's two separate contexts for each segment of state (one for the data, and one for the updater functions). 
  - Sure, it's possible to write code that way, but at that point you're just reinventing React-Redux, poorly.

- useReducer+useContext优点
  - 减少依赖和复杂度，减少样板代码，减少组件的wrapper hell
  - 缺点
    - 需要手动组装成全局对象
    - 混淆了容器组件和展示组件
- redux优点
  - 框架无关
  - redux dev tools支持time travel debugging
  - 全局中心化的状态对象
- There are two ingredients missing from Redux to make it one and global.
- First, there is no native feature (yet) which combines all reducers to one ultimate reducer. 
  - Redux is offering this feature.
  - Only if we were able to combine all state containers form all useReducer hooks, we could speak of one state container.
- Second, every useReducer comes with its own dispatch function. There is no native feature (yet) which combines all dispatch functions to one dispatch function. 
  - Redux provides one dispatch function that consumes any action dedicated for any reducer function. 
  - The dispatch function from useReducer, in contrast, only deals with action that are specified by the reducer function to be consumed.
  - The useReducer function is tightly coupled to its reducer which holds also true for its dispatch function.
- There is **no middleware** for useReducer (yet). Since it's not one global state container (see previous section), it's difficult to apply such middleware globally
- useReducer's state is local to a single component - if you wanted to use this state throughout your app, you'd need to pass it (and/or the dispatch function) down via the props. It's effectively just a more structured version of useState - in fact, useState is implemented using useReducer under the hood!
- Redux, on the other hand, does a bit more - among other things, it makes the state available to the entire app via a Context, and then provides APIs to connect your deeply nested components to this state without passing props down.

## context vs redux

- 使用context作为全局唯一store和redux的区别?
- Redux解决了，Context API没有解决的问题
  - 逻辑/数据/视图分离的代码结构（reducer/store/component），很好地划分了代码职责
  - 在不同项目之间通用的存储和事件机制，从而允许redux-devtools和time travel这种通用的开发工具、以及类似redux-observable这种强大中间件的存在（store/action）
- 适合redux的使用场景
  - 与redux对比，感觉context适合很少修改，主要从根节点下发数据的情形，比如locale/主题。个人登录信息呢？这还有点迷惑。redux啰嗦点，但万能。
  - 作为路由信息的补充，也就是完全可以序列化到路由，但因为设计原因无法放进路由的那些内容
  - 存储跟领域模型相关的数据，例如后端Model的缓存以及会话认证信息等
  - 其他例如窗口大小、临时Modal状态、视觉主题等等状态，都适合放在新Context或props中
- ref
  - 和组件props相比，新旧的Context API和Redux都解决了props存在的“只要是子组件需要的信息，即使父组件不需要，也必须先传给父组件然后一层层传到子组件”的问题
  - 和Redux相比，新旧的Context API都解决了Redux存在的“一些信息的内容需要根据组件的包含关系决定，而React难以处理这类包含关系”的问题
  - 和旧的Context API相比，新API解决了旧API无法处理“两个互相嵌套的组件提供的两个Context中，key相同的部分会冲突”的问题
  - 考虑：共享的业务数据，非UI数据，如登录信息、操作进度信息，应该存放在哪里

## state vs redux

- 当你想一定要把一个状态放在Redux Store上，先问自己两个问题：
  - 这个状态是否需要其他组件访问？（例如，一个“关注”按钮，是否要让其他组件也知道是否正在关注某人）
  - 当组件unmount之后重新mount，状态是否要保存？（例如，一个对话框打开，输入一些内容，关闭对话框，重新打开对话框，要不要看见刚才输入的内容？）
  - 只有这两个问题的回答都是“是”的时候，才有充足的理由把状态放在Redux Store上，除此之外，能在React上放state就在React上放吧
- 用action/reducer能够让代码结构更清晰，但是我也见过海量action/reducer把程序搞得一团糟的，对于大项目，还是要能够分解成各自独立的小块好，而React组件模型天生就适合分解为小块，但Redux不是，Redux中action type可能发生冲突，state key也是全局的，这些都是要考虑的因素

- react组件总是有第一次无意义的渲染，对性能影响大吗
  - 如react-data-grid首次渲染每列使用默认宽度80px
- 一个组件设计出来有50多个属性，有什么问题
  - 不便于查找和维护，可考虑拆分出容器组件、展示组件、高阶组件
  - 不便于测试，一般每个prop都需要一个单元测试
  - 若把可定制的属性全放到顶层组件，就可能出现组件属性过多，可考虑使用redux或context
  - Put them inside an object , so you can destructor and use default props 
  - If a parent component re-renders, so do its children, and their children, and so on. It doesn't matter how many props were passed down, or even if any of them changed - the default behavior is that they all re-render.
- ref
  - https://jxnblk.com/blog/defining-component-apis-in-react/

- 在react-window的FixedSizeList中，render()的return返回的是createElement
  - 若第3个参数有值，且使用组件时children部分也是组件，最终的渲染顺序应该怎样
  - 思考的方向是组件最终会转换成React.createElement, children若有指定则直接用
- react element vs component
  - react element is a plain js object that describes a DOM node and its attributes
  - react component is a factory for creating elements, accepting input and returning a React element
  - ReactElement is a stateless, immutable, virtual representation of a DOM Element
  - React Element does not have any methods and nothing on the prototype, making it fast

## how to write `onClick` (with arguments) optimized by `useCallback` in React?

- [React useCallback with Parameter](https://stackoverflow.com/questions/61255053)

```JS
const Button = props => {
  const [loading, setLoading] = React.useState(false)
  const cb = React.useCallback(() => { setLoading(!loading) }, [loading]);
  return <button onClick={cb}>{props.children}</button>
}
```

- [React hooks useCallback with parameters inside loop](https://stackoverflow.com/questions/55006061)
- The simple answer here is, you probably shouldn't use useCallback here. 
  - The point of useCallback is to pass the same function instance to components
  - the best solution here is probably to use a single function instead of five by `event.target.dataset["key"]`

```JS
const Example = (props) => {
  // Single callback, shared by all buttons
  const onClick = React.useCallback((e) => {
    // Check which button was clicked
    const key = e.target.dataset["key"]
    console.log("You clicked: ", key);
  }, [ /* dependencies */ ]);

  return (
    <div>
      {
        _.times(5, (key) => {
          return (
            <button data-key={key} onClick={onClick}>
              {key}
            </button>
          );
        })
      }
    </div>
  );
};
```

- All that being said, it is possible to memoize multiple functions in a single hook.
  - useMemo can be used to memoize multiple functions at once

```js
const Example = (props) => {
  const clickHandlers = React.useMemo(() => _.times(5, key =>
    () => console.log("You clicked", key)
  ), [ /* dependencies */ ])

  return (
    <div>
      {
        _.times(5, (key) => {
          return (
            <button onClick={clickHandlers[key]}>
              {key}
            </button>
          );
        })
      }
    </div>
  );
};
```

- [useLoopCallback — useCallback hook for components created inside a loop](https://stackoverflow.com/questions/57663003)
- With redux this would not be a problem because deleting items would be accomplished by dispatching an action and will be changed by a reducer that is always the same function.
- React happens to have a useReducer hook that you can use

```JS
import React, { useMemo, useReducer, memo } from 'react';

const Item = props => {
  //calling remove will dispatch {type:'REMOVE', payload:{id}}. 
  //no arguments are needed. 
  const { remove } = props;
  console.log('component render', props);
  return (
    <div>
      <div>{JSON.stringify(props)}</div>
      <div>
        <button onClick={remove}>REMOVE</button>
      </div>
    </div>
  );
};

//wrap in React.memo, so when props don't change,ItemContainer will not rerender
const ItemContainer = memo(props => {
  console.log('in the item container');
  //dispatch passed by parent use it to dispatch an action
  const { dispatch, id } = props;
  const remove = () =>
    dispatch({
      type: 'REMOVE',
      payload: { id },
    });
  return <Item {...props} remove={remove} />;
});

const initialState = [{ id: 1 }, { id: 2 }, { id: 3 }];
//Reducer is static it doesn't need list to be in it's
// scope through closure
const reducer = (state, action) => {
  if (action.type === 'REMOVE') {
    //remove the id from the list
    return state.filter(
      item => item.id !== action.payload.id
    );
  }
  return state;
};
export default App() {
  //initialize state and reducer
  const [list, dispatch] = useReducer(
    reducer,
    initialState
  );
  console.log('parent render', list);
  return (
    <div>
      {list.map(({ id }) => (
        <ItemContainer
          key={id}
          id={id}
          dispatch={dispatch}
        />
      ))}
    </div>
  );
};
```

- https://stackoverflow.com/questions/62955597

```JS
//make Counter a pure component (only re renders if something changed)
const Counter = React.memo(function Counter({
  counter,
  up,
  index,
}) {
  // ok to do onClick={new=>'function'} because we do not pass
  // onClick to sub components unless counter changes
  // 这里的事件函数直接传到button元素了，没有子组件了
  console.log('rendering index:', index);
  return (
    <button onClick={() => up(index)}>{counter}</button>
  );
});
const App = () => {
  //fixed amount of items that does not re order so can use index
  //  in key, do not use index as key when you don't have fixed
  //  amount of items or re order the list.
  const [counters, setCounters] = React.useState([0, 0]);
  const up = React.useCallback(
    (index) =>
    //pass callback to setCounters so counters is not
    //  a dependency of useCallback
    setCounters((counters) =>
      counters.map((counter, i) =>
        i === index ? counter + 1 : counter
      )
    ),
    [] //empty dependency, only created when App mounts
  );
  return (
    <ul>
      {counters.map((counter, index) => (
        <Counter
          up={up}
          counter={counter}
          key={index}
          index={index}
        />
      ))}
    </ul>
  );
};
```

## [Can I Use Decorators?](https://create-react-app.dev/docs/can-i-use-decorators/)

- Create React App intentionally doesn’t support decorator syntax at the moment because:
  - It is an experimental proposal and is subject to change (in fact, it has already changed once, and will change again).
  - Most libraries currently support only the old version of the proposal — which will never be a standard.
- However in many cases you can rewrite decorator-based code without decorators and achieve the same result.
- Create React App will add decorator support when the specification advances to a stable stage.
# faq-why-react

## [我们为什么需要 React？](hhttps://www.zhihu.com/question/47161776/answers/updated)

- 我们需要技术栈
  - 需要技术栈提供好用的模块化方式，一次构建，多处复用的能力
  - 需要数据绑定，不用重复手写本质上并不依赖场景的从视图到数据从数据到视图的更新
    - 否则我们就得自己操作DOM，优化DOM操作，还要自己维护状态
  - 需要技术栈隐藏掉平台的微妙差异
  - 需要库或者框架好学好用，能快速开发
  - 希望技术栈有非常好的性能，性能的水平和垂直扩展性都很好
  - 需要使用的工具有专业的团队或者社区持续地跟进
- 你需要React，是因为
  - 你充分评估了你的项目需求，理解你要解决的问题是什么，是快速开发，性能，团队的ergonomics，多数情况下要解决的问题是多个要素的平衡
  - 你充分评估了React技术栈，理解它是解决你的具体问题的最佳工具，你真的理解了自己的场景中非用React不可的那些事情

## [Why use react and not jquery?_201804](https://twitter.com/paulhtrott/status/982373883402752001)

- What makes a component-based library better than a non-component-based is the ability to wrap specific functionalities and UI inside components. 
- You get a lot of reusability
  - React's specialty is how it controls functionality and UI inside and between  components
  - In jQuery you loose capacity to orchestrate your code, and your application.
- The bottleneck of most applications is the frontend.
  - The goal is to let the application go faster and better, and allow it to grow when required, an option more aligned to the new requirements of the web can be better.
  - jQuery is so heavy for small requirements, and falls short for biggers.
  - Depends on what you define as your bottleneck metric here, I’d argue if you’re referring to performance it’s very rarely the front end that’s the bottle neck. 
    - If you meant feature scalability then you’d have my vote.
- Why I love React:
  - Quality of solutions in the ecosystem are top notch(等级；档次) 
  - Component model is readily applicable to a surprising number of web's needs (render props amirite)
  - Functional views are way easier.
  - I don't have to think about DOM manipulation anymore.
- Using React, the different parts of your app stay in sync. 
  - Using jQuery, you basically have to reimplement a crappy version of React, 
  - telling this script to re-run after that script does something, and so on.
- The most important thing that React brings to the table for me is the change in the mindset. 
  - Instead of "DOM is your state", now it is "Your state creates the DOM".
  - There's no element selector.
  - And you'll be much more confident that your state is correctly reflected. 
  - Think about those time when a data change and you have to make multiple updates in the DOM. It's prone to error and messy.
  - That being said, there's right tool for the right job. If you're building a simple info page or a classic CRUD app. React might be an overkill.
- At a larger scale, it becomes very difficult to maintain the state of many little bits of UI like “unread message count”, online indicators, etc. 
  - In jQuery you’d end up with more and more `$()` calls for each datapoint and bit of view. 
  - React‘s structure solves this more efficiently
- I learned React last summer for kicks, but am using jQuery to build UI for a medium sized app. 
  - I’m writing handlers to update the DOM, directly, based on user input and AJAX and doing A LOT of thinking about how updates affect which handlers, 
  - wishing I had all the niceties of a virtual DOM that handled its own re-rendering upon receiving new props. 
- For me it’s that it shifts the focus of web app development 
  - from “how do I manipulate the DOM based on app logic and user actions” 
  - to “how do I change app state based on user actions”, 
  - which is a much cleaner problem to work on.
- One major reason for me: where I work the back end DB spits the HTML out to the page. 
  - We on the front end have control over the css and js. 
  - With React, we get control over the HTML back. 
  - Now we just pass data via JSON. 
  - Other tools like Handlebars can achieve this too.
- After I started my first full-time job, another dev and I spent 6 months migrating some jQuery/nunjucks apps to @reactjs.
  - The old jQuery apps were unwieldy, hard to extend, hard to maintain as people just added things everywhere (not really jQuery's fault though
  - We switched to @reactjs cause it gave us clear, maintainable & extendable component based state management (rather than global's and callbacks) + heaps of reusable pieces of UI that only needed to be written once rather than copy pasted between new apps or files.
  - It also placed the HTML (JSX) in the Javascript so there was no more always needing at least 2+ files open to make a UI change
  - Overall, I wasn't convinced at the time - I always thought React was just a 'fad' but after using it for the last year and building 2 more apps with, I'll never go back!
- I currently only use React with Redux, 
  - and one of the things I like the most, is the unidirectional data flow. 
  - This makes extremely easy to create and maintain generic modules, 
  - because I always know what will be affected by my changes. 
  - This also means that testing is pretty easy.
- Most other frameworks (and web components) take an HTML-centric approach to building Web UIs.  
  - React takes a JavaScript-centric approach.  
- In the jQ era of libs, doing DOM related things, esp events was always a mess. 
  - JSX and the "reactive flow" aspects of React are what makes it great for me
  - To add to that, I think the post-jQuery era (backbone, Angular, Ember) tried to MVC-ize the front-end, the FE is a different animal than the back-end. 
  - MVC works there, but doesn't work out as well in the FE because 1. JS isn't OOP, and 2, it's not request/response oriented

- [For those of you who use React: why do you use React?_201707](https://twitter.com/kentcdodds/status/884583205692612608)
- First time we had a sensible model for server rendering single page apps—harnessing it well is a competitive advantage.
- It gives me the clearest, easiest to use abstraction for composable components, with no template-specific DSL to learn.
- Simplest way to build view as declarative function of state that I know of. Simple API, huge community.
- Components, all rendered output as a function of props + state ONLY, no need for bespoke DOM updates, JSX
- no templating language gotchas (for loops, if else, etc...).
- Because it is just JavaScript (save time and pain since no need to spend hours on documentation) and it gives the expected results
- primarily because it has very well-established patterns that solve a lot of problems before you run into them.

- [The most striking benefit of dev in React/Angular/Vue vs jQuery: ](https://twitter.com/housecor/status/1047298692091404288)
- Components free our minds.
  - We can create portions of the UI in complete isolation, 
  - so we only need to load one component into our brain at a time. 
  - The result: High reliability, more reuse, and low cognitive load.
- For me it's top-down data flow. 
  - Older frameworks had components but really what sells the new ones to me is not being based on firing off an event and having who knows what other component(s) do something in response. 
  - Custom events are the gotos of frontend.
- Like jquery components never existed? Bootstrap was just a mirage?
  -  jQuery plugins wired up to global event handlers instead of enforcing clear top down data flows for nested components. 
  - So even with jQuery plugins, the resulting cognitive load was higher.
  - I agree it was less robust and clean
- For me it was also the DOM manipulation for so many states spread across functions. 
  - It is difficult to visualize what the DOM will look like after bunch of events. 
  - Way easier to visualize it as templates/JSX with conditional statements and manipulating the states instead.

- [I never had difficulties integrating a jQuery widget into a React app.](https://twitter.com/dan_abramov/status/717448496064888832) 
- There were many *other reasons* why I usually made it from scratch.
- Examples: I wanted to override some parts of UI in a declarative way, wanted a different way to style it, have it keep state elsewhere, etc
  - None of these problems, as far as I see, would be solved by adding a blessed imperative layer. But that’s just my personal experience
- Exactly! That's why I said WC don't solve real problems. 
  - There are almost no cases where you reuse high level components.
  - Two exceptions are maybe maps and video players.
  - And even in those two cases the completeness bites you back, when styling is pain and it's hard to fit into UI.

- [Don't build your portfolio with just React](https://dev.to/flexdinesh/dont-build-your-portfolio-with-just-react-11a9)
- Why you should use React
  - Component based
  - Pre-configured (for most part) starter with create-react-app
  - Faster development
- Why you shouldn't use just React
  - DOM is constructed in the browser (client-side)
  - SEO implications
  - Higher Time to Interactive (TTI)

## [The deepest reason why modern JavaScript frameworks exist_201803](https://medium.com/dailyjs/the-deepest-reason-why-modern-javascript-frameworks-exist-933b86ebc445)

- Conclusion
  - The main problem modern JavaScript frameworks solve is keeping the UI in sync with the state.
  - It is not possible to write complex, efficient and easy to maintain UIs with Vanilla JavaScript.
  - Web components do not provide a solution to this problem.
  - It’s not that hard to make your own framework using an existing Virtual DOM library. But I’m not suggesting you to do that!
- the biggest benefit these frameworks provide: keeping the UI in sync with the state.
  - the framework automatically updates it after the state changes.
- How does it work? There are two basic strategies:
  - Re-render the whole component: React. 
    - When the state of a component changes it renders a DOM in memory and compares it with the existing DOM. 
    - Actually since that would be very expensive it renders a Virtual DOM and compares it with the previous Virtual DOM snapshot. 
    - Then it calculates the changes and performs the same changes to the real DOM. 
    - This process is called reconciliation.
  - Watch for changes using observers: Angular and Vue.js. 
    - Your state variables are observed 
    - and when they change only the DOM elements where those values are/were involved in the rendering are updated.
- web components doesn’t provide anything for that. 
  - They just provide a `<template>` tag but it doesn’t provide any reconciliation mechanism. 
  - If you want to use web components and have the UI in sync with the internal state of your app you have to do it by hand, 
  - or you can use something like Stencil.js (which internally uses a Virtual DOM, like React).

## why use react for threejs?

- https://twitter.com/0xca0a/status/1282999626782650368
- same reason you use it for the dom. 
- this is not a dig at the dom or three. 
  - these are imperative systems and i'm glad they don't add high level features, because that's not their domain. 
  - react simply expresses sth imperative in a declarative way with a common ground that makes management and sharing much easier.
- threejs
  - cube affects *every* aspect of the app: setup, state, view, resize, events and render, 
  - it is not re-usable at that point. 32 hits. 
- react
  - a re-usable self-contained self-cleaning component and one invocation.
- r3f does the same for three that react-dom does for the dom, updates or not. 
  - you can write small-ish vanilla dom apps relatively clean, in three that is less likely bc a "thing" always has to reach everywhere to function.
- RTF is great for adding scalability to any threejs project. 
  - For small projects it might be overkill depending on the scope, 
  - but as soon as it evolves to a medium to large scale project, this cube problem becomes so much worse.
- I'm not saying use React because everyone else does.
  - I'm saying use React because their resources and constraints are way bigger than yours (and everyone else), 
  - and they're giving it to you for free.

## [React 的 Concurrent Mode 是否有过度设计的成分？](https://www.zhihu.com/question/434791954/answers/updated)

- 对于web工程而言，其实更多的是要在工程环境、开发体验、持续迭代上不断创新。但react项目明显不是，它自己不提供官方工程环境，开发体验也不怎么好
  - 但是从另一方面看，整个前端领域，除了react，你很难再找到一个项目，在运行时（重点）领域有react这般的创新。
  - 为什么整个前端，只有一个virtual dom方案？而没有同时期出现一个hard dom, quick dom之类的方案，形成百花齐放百家争鸣的局面？包括hooks？前端领域的发展脉络越来越死板，也就react，这个全身心只在搞运行时渲染库（却被当作工程框架在用）有在做一些探索，每年都有一些新方案出现在它的计划中。
  - react在DOM领域是做的很烂的，它的核心成就在React而非ReactDOM。
  - react native, react+canvas实际上可能正好会用到concurrent mode的东西，我们却会忽略了
  - react明显不想在dom上渲染花太多功夫，已逝大佬司徒正美在书中提到的那些DOM魔法，react-dom好像根本没怎么用。整个react团队几乎没想过在DOM上优化的事，大部分第三方的优化，都是伪装成react组件的原生DOM操作，比如大数据量的list渲染
