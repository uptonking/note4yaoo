---
tags: [faq, react]
title: note-react-faq
created: '2020-06-29T08:30:13.355Z'
modified: '2020-06-30T12:51:08.791Z'
---

# note-react-faq

# faq-not-yet

- ~~`React.forwardRef()` 是高阶组件吗~~

- 包含ref的react组件，ref指向的dom是由react更新/rerender吗

- createPortal的render、commit过程是怎样的
  - 注意createPortal()方法的返回值是存在children属性的ReactElement
  - createPortal()是否存在commit phase?
    - 不存在commit阶段，createPortal的返回值就是普通的react element，和普通的函数组件返回值一样
    - 而ReactDOM.render() return a reference to the component (or returns null for stateless components).

```typescript
function createPortal(children: ReactNode, container: Element, key?: null | string): ReactPortal;

interface ReactPortal extends ReactElement {
    key: Key | null;
    children: ReactNode;
}

// ReactDOM.render
export const render: Renderer;
export interface Renderer {
    // Deprecated(render): The return value is deprecated. In future releases the render function's return type will be void.

    <T extends Element>(
        element: DOMElement<DOMAttributes<T>, T>,
        container: Container| null,
        callback?: () => void
    ): T;

    <P, T extends Component<P, ComponentState>>(
        element: CElement<P, T>,
        container: Container| null,
        callback?: () => void
    ): T;
    // ...

}

```

# faq
- ## [why not implement new context API in userland with an event emitter?](https://twitter.com/dan_abramov/status/976486152197812229?s=19)
- We want to fix the “deep update propagation” problem. 
  - But we don’t want to pay the memory and initialization time cost for every single component that consumes context. 
  - Many context values change very rarely! 
  - It’s wasteful to subscribe all those callbacks.
- The new context API has zero cost for the initial rendering. 
  - It doesn’t perform any subscriptions. 
  - Even if you read the context in many components (e.g. for passing a theme), React doesn’t need to collect all those subscriptions in a giant array.
- When there *is* an update, React walks the tree and marks matching nodes as dirty. 
  - The nodes are monomorphic(单一形态的), so traversal is very fast. 
  - `<Consumer>` is a special type known to React, so a single field comparison is enough to detect and mark it. 
  - And the marking can be time-sliced!
- It’s plausible that we can add some caching for a list of subscribed components in the future, 
  - but for now we don’t think it’s necessary in practice. We’ll see. 
  - But importantly, you only “pay” for context updates when you actually use them. Static values are free.
- Another interesting about this approach is that this traversal is completely integrated with React, 
  - and thus works with async features (time slicing and suspense). 
  - You can switch a UI theme even while suspense waits for a page to load. 
  - Can’t do this with a custom event emitter.
- Whats the meaning by “user land with an event emitter?”? They mean adding event emitter to new react context api?
  - Using old context API to pass an event emitter, subscribe() on mount, and then setState() in individual component on change
- I suppose suspense’d component trees would not rerender context change (i.e. delayed theme change) until their promises resolve?
  - If data for theme change is available immediately (and doesn’t suspend itself), no, React can apply it to the “previous” screen while the new screen is being loaded. No need to wait.
- If there is a simple answer. Could context api replace the need for Redux in most cases?
  - It can replace react redux for simplest cases, but react redux does some caching work.
  - react-redux(v6), which uses context internally to fight props (actually, data from the store) passing issue.
  - The purpose of Redux is NOT to facilitate passing props to deeply nested children. 
    - Redux is meant to provide a predictable state tree, even as our app grows and our data becomes more dynamic. 
    - Context does NOT solve those problems.
  - Therefore, no, context is not a replacement for Redux, as it does not solve the problems Redux does. 
    - If you were just using Redux to avoid passing props, then you probably never really needed Redux in the first place. 

- ## createRef vs useRef
- `createRef` is as simple as return `{current: null}`. It's a way to handle ref prop in most modern way and that's it(while string-based is too magic and callback-based looks too verbose).
  - `useRef` keeps some data before renders and changing it does not cause re-render
  - `useRef(null)` is basically `useState(React.createRef())[0]` .
  - A ref is a plain object `{ current:  value }` .
  - React.createRef() creates { current: null } - no magic
- useRef(initialValue) creates { current: initialValue } like React.createRef(). 
  - Besides, it memoizes this ref to be useable across multiple renders in a function component
  - In summary, use the optimized API for its intended use case:
    - useState → immutable state/values
    - useRef → mutable DOM node references or stored values in function components
    - createRef → mutable DOM node references in class components; you can use instance variables for other values
  - You can't set a new value for createRef. But you can for useRef. ??? 待验证
  - [What's the difference between `useRef` and `createRef` ](https://stackoverflow.com/questions/54620698/whats-the-difference-between-useref-and-createref)

- ## createRef vs callback ref
- In terms of use cases, callback refs can do anything createRef can do, but not vice versa.
- Things you can't do with createRef
  - React to a ref being set or cleared
  - Use an externally and internally provided ref on the same React element at the same time. (e.g. you need to measure a DOM element's clientHeight whilst, at the same time, allowing an externally provided ref (via forwardRef) to be attached to it.)
- createRef is returning either a DOM node or a mounted instance of a component, depending on where you call it. Either way, what you have in hand is indeed straightforward as you've noted. But what if you want to do something with that reference? What if you want to do it when the component mounts?
- Ref callbacks are great for that because they are invoked before componentDidMount and componentDidUpdate. This is how you get more fine-grained control over the ref. You are now not just grabbing DOM elements imperatively, but instead dynamically updating the DOM in the React lifecycle, but with fine-grained access to your DOM via the ref API.
- forwardRef lets us deprecate findDOMNode (in strict mode). And once we decide where to put ref (second arg or props object) we can deprecate forwardRef and it'll just always be passed. But often need to add before we can remove. Stepping stones.
- ref
  - [React createRef() vs callback refs](https://stackoverflow.com/questions/53624712/react-createref-vs-callback-refs-is-there-any-advantage-of-using-one-over-the)

- ## forwardRef vs callback ref
- Is there any difference between forwardRef and callbackRefs? We can access the child node's reference from parent in both of these cases.
- the difference between the use of forwardingRef vs callback ref is in the HOC.
- If you pass ref prop to HOC, then inside HOC you cannot further pass it down to the enclosing component(which HOC wraps) since the props attributes does not store the ref inside it. ref is not a prop
- callback refs are commonly used when we need to dynamically set refs. 
- forwardRefs are commonly used when access to child refs are needed
- We already have a work-around for passing ref to child components. 
  - The work-around is to pass the ref as some other prop. 
  - In this case, we used `ssnRef` prop to pass the ref to a child component.
- Why should the React team consider adding this API? It is for third-party package developers.
- When we pass the ref like this, we really don’t know that it is being forwarded. By providing an explicit alternate prop, we are clear that the ref is going to be forwarded.
- ref
  - [What is the difference between forwardingRef vs callback refs in React?](hhttps://stackoverflow.com/questions/59045294/what-is-the-difference-between-forwardingref-vs-callback-refs-in-react)
  - [React forwardRef example and why it should not be part of React API](https://vijayt.com/post/react-forwardref-example-and-why-it-should-not-be-part-of-react-api/)

```JS
// callback ref
function CustomTextInput(props) {
  return (
    <div>
    <input ref={props.inputRef} />
  </div>
  );
}

class Parent extends React.Component {
  componentDidMount(props) {
    //Here, this.inputElement in Parent will be set to the DOM node corresponding to the element in the CustomTextInput
    console.log(this.inputElement);
  }
  render() {
    return (
      <CustomTextInput
      inputRef={el => this.inputElement = el}
    />
    );
  }
}
```

```JS
// forwardRef
const FancyButton = React.forwardRef((props, ref) => {
  return (
    <button ref={ref}   data-name="My button">
    {props.children}
  </button>
  );
});

//Parent Component
class FancyButtonWrapper extends React.Component {
  constructor(props) {
    super(props);
    this.buttonRef = React.createRef();
  }

  componentDidMount(props) {
    //Here this.ref will point to button element. Because of this reason, ref.current will give the value of button.
    console.log(this.buttonRef.current.getAttribute("data-name"));
  }

  render() {
    return (
      //Here we are passing the ref to the child component.
      <FancyButton ref={this.buttonRef} data-attr="Hello">
      Click me! 
    </FancyButton>
    );
  }
}
```

- ## `props.children` not re-rendered on parent state change
- When clicking on Child 'Hi' text, only Container component keeps re-rendering but Child component is not re-rendered.
- Since the Container's render is executed, so must the components returned from it call their own render methods.
- No matter how many times Container get's re-rendered, since its children are always referentially the same thing between renders (**because that React Element was created in the App level** and it has no reason to change), they don't get re-rendered.
- In short, React doesn't bother to render a React Element again if it is referentially (===) equal to what it was in the previous render.
- ref
  - [this.props.children not re-rendered](https://stackoverflow.com/questions/47567429/this-props-children-not-re-rendered-on-parent-state-change)

```typescript
class App extends Component {
  render() {
    return (
      <Container>
        <Child/>
      </Container>
    )
  }
}

class Container extends Component {
  render() {
    console.log('Container render');
    return (
      <div onClick={() => this.setState({})}>
        {this.props.children}
      </div>
    )
  }
}

class Child extends Component {
  render() {
    console.log('Child render');
    return <h1>Hi</h1>
  }
}

<div onClick={() => this.setState({})}>
  {this.props.children}
</div>
// is equal to
React.createElement(
  'div', 
  { onClick: () => this.setState({}) },
  this.props.children
)

<div onClick={() => this.setState({})}>
  <Child />
</div>
// is equal to
React.createElement(
  'div', 
  {onClick: () => this.setState({})}, 
  React.createElement(
    Child, 
    {}, 
    {}
  ) 
)
```

- ## useState vs useReducer
- useReducer is usually preferable to useState when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one. 
- useReducer also lets you optimize performance for components that trigger deep updates because you can pass dispatch down instead of callbacks.
- The above statement is not trying to indicate that the setter returned by useState is being created newly on each update or render. 
  - What it means is that when you have a complex logic to update state, you simply won't use the setter directly to update state, instead you will write a complex function which in turn would call the setter with updated state
- Hence it is recommended to use useReducer which returns a dispatch method that doesn't change between re-renders and you can have the manipulation logic in the reducers

- When it's just an independent element of state you're managing: useState
- When one element of your state relies on the value of another element of your state in order to update: useReducer
- useReducer() is preferable
  - Next state depends on the previous
  - Complex state shape
    - useState不对状态做浅层合并了，而useReducer会合并，待验证？？？
    - useReducer一次更新多个状态更方便
  - Easy to test(Reducers are pure functions)
- UseReducer has a stable dispatch which is better for passing down the tree. UseState uses useReducer, but you may need to wrap your state update functions in useCallback which isn’t an issue with dispatch.
- ref
  - react-table is migrating away from useReducer to useState, allowing for more imperative control over the table state
  - https://www.robinwieruch.de/react-usereducer-vs-usestate
  - https://dev.to/spukas/3-reasons-to-usereducer-over-usestate-43ad
  - https://www.freecodecamp.org/news/why-you-should-choose-usestate-instead-of-usereducer-ffc80057f815/
  - https://juejin.im/post/5df993e3e51d4558270efa4d
  -  - https://stackoverflow.com/questions/54646553/usestate-vs-usereducer

- ## 为什么不能 setState in render
- Calling setState in render can cause infinite loop 
- ref
  - https://github.com/facebook/react/issues/5591

- ## defaultProps设置默认值的方式
- 推荐只使用解构的方式，带来的问题是如何在函数体内获取到props对象
- 在参数处解构，则难以获得props，在函数内解构，则可以获得props
- One of the differences I can think of, and I suppose the most important, is that on the second case, while you are destructing your props object in function body, you are using `const` on declaration.
  - In that way, you can no longer change these values on your MyComponent, while on your first case you could easily modify them.
  - 对react组件来说，props不能改变，推荐只用const解构，但对普通函数参数解构时，要考虑用let

```JS
const Component = (props) => {
  const { x = 0 } = props;
  // ...
}

const Component = ({ x = 0 }) => {
  // ...
}

const MyComponent = (props) => {
  const { x } = props
  // ...
};
MyComponent.defaultProps = { x: 0 };
```

- defaultProps is very useful on classes because the props object gets passed to many different methods. Life-cycles, callbacks etc. 
  - This makes it hard to use JS default arguments because you'd have to replicate the same defaults in each function.
  - However, in function components there really isn't much need for this pattern since you can just use JS default arguments and all the places where you typically use these values are within the same scope.

- pass object literals as props create new object every render
- If a parent component is updated, does React always update all the direct children within that component?
  - No. React will only re-render a component if `shouldComponentUpdate()` returns `true` . 
  - By default, that method always returns `true` to avoid any subtle bugs 
  - By default, if parent changes, all its direct children are re-rendered but that re-render doesn't necessarily changes the actual DOM. The DOM won't actually update unless something changed, lowering the impact
  - To prevent even re-rendering of virtual DOM
    - implement the shouldComponentUpdate
    - use Use React.PureComponent or React.memo
  - In the future, React may treat shouldComponentUpdate() as a hint rather than a strict directive, and returning false may still result in a re-rendering of the component.

- ## When will Function Component render?
- 父子组件挂载的先后顺序、生命周期顺序、DOM生成顺序
  - 参考[implementation notes for stack reconciler](https://reactjs.org/docs/implementation-notes.html)
  - mount时，顶层父组件最先调用 `render()` ，然后从上到下从外到内依次调用下层子组件的render
  - 接着调用最下层组件的didMount，依次向上调用didMount，最后调用顶层父组件的didMount

- ## How does React know the component is removed from the DOM?
- There is no watcher on the actual DOM. 
- Everytime the render function of a component gets called, the Virtual DOM gets re-build. 
- If a component is no longer necessary, it gets removed from the virtual DOM.
- A diffing algorithm identifies those parts of the actual DOM that need to be changed for the actual DOM to be a reflection of the virtual DOM: 
  - some components will have to be added to the actual DOM (= called mounting)
  - other components will have to be removed (= unmounting).
  - This whole process is called *reconciliation*.
- It is because of this reconciliation process, that React knows which components are to be removed from the actual DOM. Right before the component is removed, React calls the `componentWillUnmount()` lifecycle hook.
- If another script (Javascript or jQuery) causes the removal of a certain component from the actual DOM, React will never notice it and therefore will not call the componentWillUnmount() lifecycle hook.
- https://stackoverflow.com/questions/44996941/how-does-react-know-the-component-is-removed-from-the-dom

- ## Is it antipattern to use React.cloneElement to extend an element and modify props in child components
- `React.cloneElement(element, [props], [...children])`
  - 相当于 `<element.type {...element.props} {...props}>{children}</element.type>`
  - Clone and return a new React element using element as the starting point. 
  - The resulting element will have the original element’s props with the new props merged in shallowly. 
  - New children will **replace** existing children. 
  - key and ref from the original element will be preserved.
- cloneElement gives the developer full control of the button instance, except the props you need to access/add/modify.
- React.cloneElement is a helper that's usually used to pass inline-props to avoid polluted codes
- renderProps is a technique to reuse stateful logic and has different applications than cloneElement.
- the React.cloneElement example only works if your child is a single React element.
- For almost everything `this.props.children` is the one you want. Cloning is useful in some more advanced scenarios, where a parent sends in an element and the child component needs to change some props on that element or add things like ref for accessing the actual DOM element.
- 常用来修改现有的组件，如添加onClick函数，通过cloneElement为组件添加新的属性
- React. Children提供了直接访问黑盒props.children数据结构的能力；
- React.cloneElement接收一个React element并支持往其中浅层合并props，替换旧children；笔者看来该API可以从一定程度上减少代码的重复书写，使组件标签表达更加清晰

- ## Is setting state with `this.setState` inside the render method of a class component, the same as setting state inside the function body of a function component with hooks?
- Techincally yes.
- setting a state directly in render method will cause the function to trigger re-render in case of class component causing an infinite loop which is the case for functional components provided the state values are different. 
- Regardless of that, it will still cause an issue because any other state update will be reverted back due to functional component calling state update directly 
- In a class component, if we set state in the render method an infinite loop will occur. This is because the class component does not care that the new state is the same as the previous state. It just keeps re-rendering on every this.setState. Yes, hence its recommended not to call setState directly in render

- ## react中setState是同步的还是异步？
- **合成事件中的setState是异步的**
  - 合成事件是react为了解决跨平台封装的一套事件机制，代理了原生的事件，像在jsx中常见的onClick、onChange这些都是合成事件
- **生命周期钩子函数中的setState是异步的**
- **原生事件中的setState是同步执行的**
  - 原生事件是指非react合成事件，原生自带的事件监听`addEventListener`注册事件函数
  - 或者也可以用原生js、jq直接 `document.querySelector().onclick` 这种绑定事件的形式都属于原生事件
  - 当你在原生事件中setState后，能同步拿到更新后的state值
- 不管是哪个场景(合成/原生/钩子)下，在基于event loop的模型下，**setTimeout中去取setState总能拿到最新的state值**
- setState的“异步”并不是说内部由异步代码实现，其实本身执行的过程和代码都是同步的
  - 只是合成事件和钩子函数的调用顺序在更新之前，导致在合成事件和钩子函数中没法立马拿到更新后的值，形式了所谓的“异步”
  - 当然可以通过 `setState(partialState, callback)` 的第二个参数callback拿到更新后的结果
- setState的批量更新优化也是建立在“异步”（合成事件、钩子函数）之上的
  - 在原生事件和setTimeout中不会批量更新
  - 在“异步”中如果对同一个值进行多次setState，setState的批量更新策略会对其进行覆盖，取最后一次的执行
  - 如果是同时setState多个不同的值，在更新时会对其进行合并批量更新
- ref
  - [你真的理解setState吗] https://juejin.im/post/5b45c57c51882519790c7441

- ## setState是同步还是异步
- setState() does not always immediately update the component. It may batch or defer the update until later. This makes reading `this.state` right after calling setState() a potential pitfall
- 由React控制的事件处理过程setState不会同步更新this.state，在React控制之外的情况，setState会同步更新this.state
- 绕过React通过js原生addEventListener直接添加的事件处理函数，还有使用setTimeout或setInterval等React无法掌控的API情况下，就会出现同步更新state的情况
- 在componentWillMount中调用setState
  - componentWillMount() is invoked immediately before mounting occurs. 
  - It is called before render(), therefore setting state in this method will not trigger a re-render.
  - Avoid introducing any side-effects or subscriptions in this method. in componentDidMount instead.

- ## Does render get called any time setState is called?
  - By default - yes
  - By default,  `shouldComponentUpdate` always `return true` to prevent subtle bugs when the state is mutated in place
  - Virtual DOM renders: when render method is called it returns a new virtual dom structure of the component. As I mentioned before, this render method is called always when you call setState(), because shouldComponentUpdate always returns true by default. So, by default, there is no optimization here in React.
  - Native DOM renders: React changes real DOM nodes in your browser only if they were changed in the Virtual DOM and as little as needed - this is that great React's feature which optimizes real DOM mutation and makes React fast.
  - In React class components, we are told that setState always causes a re-render, regardless of whether or not the state actually changed to a new value. In effect, a component will re-render, when state updates to the same value it was before. 
    - setState() will always lead to a re-render unless shouldComponentUpdate() returns false. 
    - If you set a valid value apart from returning null within setState, a re-render will always be triggered by react in a class component unless your component is a PureComponent or you implement shouldComponentUpdate
  - With hooks however, the docs specify that updating state to a value identical to the previous state, will not cause a re-render (of child components). 
    - If you update a State Hook to the same value as the current state, React will bail out without rendering the children or firing effects. 
    - (React uses the Object.is comparison algorithm.)
  - For a functional component using useState hook, the setter if called with the same state will not trigger a re-render. 
  - However for an occasional case if the setter is called immediately it does result in two renders instead of one
  - ref
    - https://reactjs.org/docs/hooks-faq.html#how-do-i-implement-getderivedstatefromprops

- ## 给React组件的状态每次设置相同的值，如 `setState({count: 1})` ，React组件是否会发生渲染？ 
  - 会重复渲染. 可利用PureComponent组件来减少重复渲染。
  - 利用PureComponent组件可减少组件的重复渲染，那么是否代表组件的状态没有发生变化呢？即引用地址是否依旧是上次地址呢？
  - 虽然PureComponent组件减少了组件的重复渲染，但是组件状态的引用地址却发生了变化.
  - react内部(ReactUpdateQueue.js文件)的getStateFromUpdate()会通过Object.assign生成一个全新的状态state， state的引用地址发生了变化. `return Object.assign({}, prevState, partialState); `
  - Object.assign第一个参数是空对象，就说明新的state对象的引用地址发生了变化
  - Object.assign进行的是浅拷贝，不是深拷贝
- 一个React组件，它包含两个子组件，分别是函数组件和Class组件。当这个React组件的state发生变化时，两个子组件的props并没有发生变化，此时是否会导致函数子组件和Class子组件发生重复渲染呢？
  - 实验结果表明，无论是函数组件还是Class组件，只要父组件的state发生了变化，二者均会产生重复渲染
  - React官方提供了memo组件和PureComponent组件分别用于减少函数组件和类组件的重复渲染
- 每次调用函数setState，react都会将要更新的状态添加到更新队列中，并产生一个调度任务。调度任务在执行的过程中会做两个事情：
    - 遍历更新队列，计算出全新的状态 state，更新到组件实例中
    - 根据标识shouldUpdate来决定是否对组件实例进行重新渲染，而标识shouldUpdate的值则取决于PureComponent组件浅比较结果或者生命周期函数shouldComponentUpdate执行结果；
- ref
    - https://stackoverflow.com/questions/24718709/reactjs-does-render-get-called-any-time-setstate-is-called
    - https://stackoverflow.com/questions/55373878/what-are-the-differences-when-re-rendering-after-state-was-set-with-hooks-compar
    - [浅谈setState的更新机制] https://zhuanlan.zhihu.com/p/95865701
    - [PureComponent与memo] https://juejin.im/post/5de364a4f265da05be3e5af3

- ## side effects的类型和处理方式
  - data-fetching
  - manual-dom-mutation
  - sub and unsub

- ## 为避免过多rerender的常用处理方式
- render props中函数每次执行时，都会新生成一个 `value => <ValueUI value={value} />` 函数，即Container的children属性，也就是说每次Main重渲染，Container的prop都会改变。解决方法是把这个函数独立出来，提取成renderValueUI()的单独函数
- Provider本身是一个组件，当它所处层级发生重渲染时，它与普通组件一样会触发自身与children的重渲染
  - 另一方面，只要Provider的value发生改变(使用Object.is来判断)，它的子树上的所有Consumer也都会发生重渲染
  - Main执行render -> render中的JSX重新解析(React. CreateElement) -> OtherComp执行render
  - 可以不让Main来做管理Context的value这件事：建一个独立的组件来管理value和Provider，把children的JSX写在这个组件之外
- ref
  - https://github.com/shaozj/blog/issues/36
  - https://www.jianshu.com/p/033409adf916

- ## `Context. Provider`的value经常变化时，为避免过多rerender，应如何处理
- `<Context.Provider>` will only re-render if its children prop does not share reference equality with its previous children prop.
- `<Context.Provider>` will not re-render if its value changes while its children stay the same. 
- To ensure that the entire app isn’t re-rendered on each context change, you’ll need to keep the children prop of your providers equal between renders.
- All you’ll need to do is move the state that you’ll provide into a separate component, with the children passed into that component from above
- to put it simply, you just need to create a `<SomethingProvider>` component that doesn’t except any props other than children
- try running with the **production** flags to see if your performance issue went away? Looking into the development bundle, 10ms of the time taken seems to be due to performance.measure markers being really bad for performance 
- 问题案例
  - https://blog.theodo.com/2019/07/how-i-ruined-my-application-performances-by-using-react-context-instead-of-redux/
  - From my experience, when you experience slowness with redux, the problem is often not redux itself, but because of the way redux is being used
  - This would kinda be a big deal for react-redux, actually, because we're trying to switch to using `createContext` in version 6 instead of having all connected components be separate subscribers.
  - we(react-redux) stopped passing the store state in context (the v6 implementation) and switched back to direct store subscriptions (the v7 implementation) due to a combination of performance problems and the inability to bail out of updates caused by context (which made it impossible to create a React-Redux hooks API based on the v6 approach).
- ref
  - https://github.com/facebook/react/issues/13739
  - https://frontarm.com/james-k-nelson/react-context-performance/
  - https://frontarm.com/james-k-nelson/when-context-replaces-redux/
  - https://www.reddit.com/r/reactjs/comments/9kq2c7/react_context_isnt_for_state_management/
  - https://www.reddit.com/r/reactjs/comments/a5sddz/redux_vs_context_api_performance/
  - https://blog.isquaredsoftware.com/2018/11/react-redux-history-implementation/
- 组件间通信的方式
- props
- context
- eventbus
- redux/mobx
- ref
    - https://blog.csdn.net/wengqt/article/details/80114590
- 如何为现有组件添加props，比如添加样式属性props
- react.cloneElement
- hoc高阶组件

- ## componentWillReceiveProps vs getDerivedStateFromProps 
  - componentWillReceiveProps在每次rerender时都会调用，无论props变了没
      - 死循环的出现场景：在componentWillReceiveProps中不加条件限制地调用回调函数修改父组件state，父组件在state变化后rerender
  - getDerivedStateFromProps是用来替代componentWillReceiveProps的，即允许props变化引发state变化（称之为derived state，即派生state）
      - 记录当前滚动方向（recording the current scroll direction based on a changing offset prop）
      - 取props发请求（loading external data specified by a source prop）
  - With 16.4.0 the expected behavior is for getDerivedStateFromProps to fire in all cases before shouldComponentUpdate.
  - `getDerivedStateFromProps` is invoked right before calling the render method, both on the initial mount and on subsequent updates
    - 首次渲染也会调用
    - It should return an object to update the state, or null to update nothing.
  - 参考
    - http://www.ayqy.net/blog/%E4%BB%8Ecomponentwillreceiveprops%E8%AF%B4%E8%B5%B7/

- 当context变化后，与consumer同级但未被consumer包裹的组件会重新渲染吗
  - App状态被改变，它的willUpdate与render方法会被调用，此时Context. Provider的value也被重新创建，value与之前不同，所以所有子组件包括非consumer组件也会被渲染
  - 解决方法是将provider的vaule值放到state，或创建一个独立的组件来管理state和Provider
  - 结论是provider的value属性值不要直接写字面量对象，建议在state中初始化
  - 参考
      - https://zhuanlan.zhihu.com/p/50336226

- antd的国际化方案是如何基于context实现的
  - ConfigProvider组件的render()方法返回的是  
    - `<ConfigConsumer>{this.renderProvider}</ConfigConsumer>;`
    - renderProvider由context api规定必须是函数，接收context作为参数，并返回react节点，本例返回如下

```js
  //config由context计算得到
  <ConfigContext.Provider value={config}> 
      <LocaleProvider locale={locale} _ANT_MARK__={ANT_MARK}>
          {children}
      </LocaleProvider>
  </ConfigContext.Provider>
```

  - ConfigProvider自身并没有实现国际化，而是依赖LocaleProvider实现国际化
  - 这样做的作用是在ConfigProvider的上层组件使用context的defaultValue(因为上层组件一般不会再有provider了，还可以有其他默认值)，而在它的下层组件使用当前传入的context，这也要求下层具体UI组件最外层必须是ConfigConsumer和LocaleReceiver
  - ConfigProvider相关配置
    - prefixCls：设置样式命名统一前缀
    - renderEmpty：自定义组件空状态
    - autoInsertSpaceInButton：若false，则移除按钮中汉字之间的空格
    - csp：部分组件为了支持波纹效果，使用了动态样式，如果开启了Content Security Policy(CSP)，你可以通过 `csp` 属性来进行配置
    - locale
    - getPopupContainer：弹出框（Select, Tooltip, Menu等）渲染父节点，默认渲染到body上

- ## hoc vs render props
  - hoc优点
    - 复用方式简单
    - HOC是一个函数，返回值为组件，可以多层嵌套，但看起来不直观，还要自己看内部实现
    - 支持传入多个参数
  - hoc缺点
    - 当多个HOC一起使用时，无法直接判断子组件的props是哪个HOC负责传递的
    - 同名属性会覆盖，若父子组件有同样名称的props，或使用的多个HOC中存在相同名称的props，则存在覆盖问题，而且react并不会报错
    - wrapper hell，产生无意义的标签，嵌套层级太深
  - hoc使用场景
    - 组件异步加载、异步加载script后显示组件、数据源绑定、拖拽排序
  - render prop优点
    - 不用担心props是从哪里来的，它只能从父组件传递过来，也减少了命名冲突
    - 相较于HOC，不会产生无用的组件加深层级
    - 组件是动态构建的，所有改变都在render中触发，可直接利用生命周期
    - 参数类型可直接带过去，方便使用ts进行类型检查
  - render prop缺点
    - hoc复用代码只需一行，render prop需要额外的工作
    - 组件可读性降低
  - 参考
    - HOC的控制权在Wrapper组件，最后的渲染结果其实是由父组件决定的
    - render props是父组件将数据传递给子组件，子组件自己决定渲染
    - https://www.zhihu.com/question/269915942

- hoc vs hooks
  - hooks does great job at avoiding wrapper hell
- react PropTypes vs typescript 
  - TypeScript validate types at compile time while PropTypes validate types at runtime
  - When you build for production and are using prop types, ensure to remove them. If using Create React App, this is already handled for you
  - 没有propTypes定义，组件依然能够正常工作，而且，即使在propTypes检查出错的情况下，组件依然能工作，propTypes只是一个辅助开发的功能，并不会改变组件的行为
  - 还要考虑以后复用propTypes的问题
  - 当项目是TS+JS混合开发时，并不能保证引用你组件的开发者使用了TS，PropTypes至少能够在它们运行期间进行验证
  - 同时维护TypeScript Type和 React PropTypes也是一件很痛苦的事情，如果能有一个工具可以在编译时自动从TypeScript interface生成PropTypes就方便了
  - ref
    - https://www.jianshu.com/p/3609626bd43a
    - https://github.com/milesj/babel-plugin-typescript-to-proptypes

- ## Why did react decides not to support components as classes that don’t extend `React. Component`?_201508
- https://github.com/facebook/react/issues/4599
- To support arrow functions and plain functions as "components" we need to know if we can call `new` on them.
- We need to detect if a component is a "function" or a "class" before calling `new` on it.
- We can call new on everything if they're plain functions as long as they return a ReactElement. 
  - However, that won't work for null/false/string return values 
  - and we want to support those too. 
  - We also can't call `new` on arrow functions. 
  - Likewise, we can't NOT call `new` on classes.
- Unfortunately ECMAScript doesn't have a way to detect if something is newable or not.
- The current plan is to add our own static flag to `React.Component` so that we can detect if something is a class.
