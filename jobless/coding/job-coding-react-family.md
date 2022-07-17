---
title: job-coding-react-family
tags: [coding, job, react, 手撕代码]
created: 2021-09-22T17:13:19.314Z
modified: 2021-10-05T15:35:15.751Z
---

# job-coding-react-family

# redux-like

## [手写一个Redux，深入理解其原理](https://segmentfault.com/a/1190000023084074)

```JS
function createStore() {
  let state; // state记录所有状态
  let listeners = []; // 保存所有注册的回调

  function subscribe(callback) {
    listeners.push(callback); // subscribe就是将回调保存下来
  }

  // dispatch就是将所有的回调拿出来依次执行就行
  function dispatch() {
    for (let i = 0; i < listeners.length; i++) {
      const listener = listeners[i];
      listener();
    }
  }

  // getState直接返回state
  function getState() {
    return state;
  }

  // store包装一下前面的方法直接返回
  const store = {
    subscribe,
    dispatch,
    getState
  }

  return store;
}
```

```js
function combineReducers(reducerMap) {
  const reducerKeys = Object.keys(reducerMap); // 先把参数里面所有的键值拿出来

  // 返回值是一个普通结构的reducer函数
  const reducer = (state = {}, action) => {
    const newState = {};

    for (let i = 0; i < reducerKeys.length; i++) {
      // reducerMap里面每个键的值都是一个reducer，我们把它拿出来运行下就可以得到对应键新的state值
      // 然后将所有reducer返回的state按照参数里面的key组装好
      // 最后再返回组装好的newState就行
      const key = reducerKeys[i];
      const currentReducer = reducerMap[key];
      const prevState = state[key];
      newState[key] = currentReducer(prevState, action);
    }

    return newState;
  };

  return reducer;
}
```

- Redux还支持enhancer，enhancer其实就是一个装饰者模式，传入当前的createStore，返回一个增强的createStore。
  - applyMiddleware的返回值其实就是一个enhancer。

- 准确的说是applyMiddleware的返回值是一个enhancer，因为我们传给createStore的是他的执行结果applyMiddleware()
- 中间件就是加强dispatch的功能，用新的dispatch替换老的dispatch，这不就是个装饰者模式吗？其实前面enhancer也是一个装饰者模式，传入一个createStore，在createStore执行前后加上些代码，最后又返回一个增强版的createStore。

- 中间件为什么要包裹几层函数
  - 第一层：目的是传入store参数
  - 第二层：第二层的结构是dispatch => newDispatch，多个中间件的这层函数可以compose起来，形成一个大的dispatch => newDispatch
  - 第三层：这层就是最终的返回值了，其实就是newDispatch，是增强过的dispatch，是中间件的真正逻辑所在。

```JS
// 参数支持多个中间件
function applyMiddleware(...middlewares) {
  function enhancer(createStore) {
    function newCreateStore(reducer) {
      const store = createStore(reducer);

      // 多个middleware，先解构出dispatch => newDispatch的结构
      const chain = middlewares.map(middleware => middleware(store));
      const { dispatch } = store;

      // 用compose得到一个组合了所有newDispatch的函数
      const newDispatchGen = compose(...chain);
      // 执行这个函数得到newDispatch
      const newDispatch = newDispatchGen(dispatch);

      return { ...store, dispatch: newDispatch }
    }

    return newCreateStore;
  }

  return enhancer;
}
```

# react-redux
- [手写一个React-Redux，玩转React的Context API](https://segmentfault.com/a/1190000023142285)

- 要点
  - state变化时自动更新组件
  - 如何保证组件更新顺序

- React是单向数据流，但是子组件完全可以不从父组件拿这个参数，而是直接从Redux拿，这样就打破了React本来的数据流向，不能完全保证父级先更新，子级再更新的流程

- 如何保证组件更新顺序
  - React-Redux保证这个更新顺序的方案是在redux store外，再单独创建一个监听者类Subscription
  - Subscription负责处理所有的state变化的回调
  - 如果当前连接redux的组件是第一个连接redux的组件，也就是说他是连接redux的根组件，他的state回调直接注册到redux store；同时新建一个Subscription实例subscription通过context传递给子级。
  - 如果当前连接redux的组件不是连接redux的根组件，也就是说他上面有组件已经注册到redux store了，那么他可以拿到上面通过context传下来的subscription，源码里面这个变量叫parentSub，那当前组件的更新回调就注册到parentSub上。同时再新建一个Subscription实例，替代context上的subscription，继续往下传，也就是说他的子组件的回调会注册到当前subscription上。
  - 当state变化了，根组件注册到redux store上的回调会执行更新根组件，同时根组件需要手动执行子组件的回调，子组件回调执行会触发子组件更新，然后子组件再执行自己subscription上注册的回调，触发孙子组件更新，孙子组件再调用注册到自己subscription上的回调。。。这样就实现了从根组件开始，一层一层更新子组件的目的，保证了父->子这样的更新顺序。

- 有了Subscription类，connect就不能直接注册到store了，而是应该注册到父级subscription上
  - 更新的时候除了更新自己还要通知子组件更新
  - 在渲染包裹的组件时，也不能直接渲染了，而是应该再次使用Context. Provider包裹下，传入修改过的contextValue

- 只有连接到Redux最顶级的组件才会直接注册到Redux store，其他子组件都会注册到最近父组件的subscription实例上。
  - 通知的时候从根组件开始依次通知自己的子组件，子组件接收到通知的时候，先更新自己再通知自己的子组件。

- redux自身是与ui渲染无关的
- react-redux作用是将Redux的状态机和React的UI呈现绑定在一起，当你dispatch action改变state的时候，会自动更新页面

- Provider提供了一个参数，Redux的createStore生成的store

- `connect(mapStateToProps,mapDispatchToProps)(Counter)` 高阶函数/高阶组件，会返回一个新组件
  - mapStateToProps可以自定义需要将哪些state连接到当前组件，这些自定义的state可以在组件里面通过props拿到
  - mapDispatchToProps方法会传入dispatch函数，我们可以自定义一些方法，这些方法可以调用dispatch去dispatch action，从而触发state的更新
- React-Redux核心其实就两个API，而且两个都是组件，作用还很类似
  - Provider是往根组件注入store，connect是往需要的组件注入state和dispatch。

```JS
const ReactReduxContext = React.createContext();

function Provider(props) {
  const { store, children } = props;

  // 这是要传递的context
  const contextValue = { store };

  // 返回ReactReduxContext包裹的组件，传入contextValue
  // 里面的内容就直接是children，我们不动他
  return (
    <ReactReduxContext.Provider value={contextValue}>
      {children}
    </ReactReduxContext.Provider>
  )
}
```

```JS
// 第一层函数接收mapStateToProps和mapDispatchToProps
function connect(mapStateToProps, mapDispatchToProps) {
  // 第二层函数是个高阶组件，里面获取context
  // 然后执行mapStateToProps和mapDispatchToProps
  // 再将这个结果组合用户的参数作为最终参数渲染WrappedComponent
  // WrappedComponent就是我们使用connext包裹的自己的组件
  return function connectHOC(WrappedComponent) {

    function ConnectFunction(props) {
      // 复制一份props到wrapperProps
      const { ...wrapperProps } = props;

      // 获取context的值
      const context = useContext(ReactReduxContext);

      const { store } = context; // 解构出store
      const state = store.getState(); // 拿到state

      // 执行mapStateToProps和mapDispatchToProps
      const stateProps = mapStateToProps(state);
      const dispatchProps = mapDispatchToProps(store.dispatch);

      // 组装最终的props
      const actualChildProps = Object.assign({}, stateProps, dispatchProps, wrapperProps);

      // 渲染WrappedComponent
      return <WrappedComponent {...actualChildProps}></WrappedComponent>
    }

    return ConnectFunction;
  }
}

export default connect;
```

- 虽然通过dispatch改变了store中的state，但是这种改变并没有触发我们组件的更新
  - 这里需要注册回调, 检查我们最终给WrappedComponent的props有没有变化，如果有变化就重新渲染ConnectFunction

```js
function storeStateUpdatesReducer(count) {
  return count + 1;
}

// ConnectFunction里面
function ConnectFunction(props) {
  // ... 前面省略n行代码 ... 

  // 使用useReducer触发强制更新
  const [,
    forceComponentUpdateDispatch
  ] = useReducer(storeStateUpdatesReducer, 0);

  // 记录上次渲染参数,
  const lastChildProps = useRef();
  useLayoutEffect(() => {
    // 要使用useLayoutEffect来保证渲染后立即同步执行。
    lastChildProps.current = actualChildProps;
  }, []);

  // 注册回调
  store.subscribe(() => {
    const newChildProps = childPropsSelector(store, wrapperProps);
    if (!shallowEqual(newChildProps, lastChildProps.current)) {
      lastChildProps.current = newChildProps;
      forceComponentUpdateDispatch();
    }
  });

  // ... 后面省略n行代码 ...
}
```

# react-router-like

# jsx-parser
