---
tags: [blog, react]
title: page-blog-react-hooks-in-action
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-03T13:52:52.979Z'
---

# page-blog-react-hooks-in-action

- react hooks开发实践总结

## guide

- hooks rfc 
  - usePrevious
- ref
  - [React Hooks 最佳实践 by 网易云音乐前端团队](https://zh-hans.reactjs.org/blog/2020/05/22/react-hooks.html)
  - [React Hooks工程实践总结](https://github.com/forthealllight/blog/issues/49)
  - [React Hook的实现原理和最佳实践 by 携程](https://zhuanlan.zhihu.com/p/75146261)
  - [精读《React Hooks》](https://zhuanlan.zhihu.com/p/49408348)
  - [精读《React Hooks 最佳实践》](https://zhuanlan.zhihu.com/p/81752821)
  - [精读《Function Component 入门 - 使用hooks》](https://zhuanlan.zhihu.com/p/67087685)
  - [精读《useEffect 完全指南》](https://zhuanlan.zhihu.com/p/60277120)
  - [精读《怎么用 React Hooks 造轮子》](https://zhuanlan.zhihu.com/p/50274018)
  - [对React Hooks的一些思考](https://zhuanlan.zhihu.com/p/48264713)
  - [React Hooks的体系设计之一 - 分层](https://zhuanlan.zhihu.com/p/106665408)
  - [useCallback invalidates too often in practice](https://github.com/facebook/react/issues/14099)
  - [React hooks: not magic, just arrays](https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e)
    - [CN](https://zhuanlan.zhihu.com/p/66923924)

## pieces

- 未来函数组件在使用Hooks时，统一将Hooks的调用放在函数的开头部分，随后紧跟一个纯函数组件的渲染逻辑，即一个组件的逻辑拆分为

``` js
const FunctionComponent = props => {
  // 对所有Hooks的调用，声明前置条件

  // 对props及hooks提供的内容的运算处理，数据加工

  // 将数据转变为JSX并返回
};
```

- 在 `useState` 的冲击下，开发者应当思考：
  - 为何没有将“状态”与“变更状态的逻辑”两两配对，用更好的代码结构来组织它们。
  - 为何没有将状态进行更细粒度的拆分，没有联动关系的状态放到不同的组件中单独管理，而是习惯性地使用一个大的状态，以及多处setState进行部分状态的更新。
  - 为何没有将状态的管理与视图的渲染进行隔离，把一个带有复杂的render实现的类组件拆分为一个“单纯管理状态的类组件”和一个“实现渲染逻辑的纯函数组件”，并让前者的render方法直接返回后者。
- useState正是将以上三个理论合而为一，用一个非常简洁的API表现出来的经典设计：
  - value和setValue配对，后者一定影响前者，前者仅被后者影响，作为一个整体它们完全不受外界的影响。
  - 在几乎所有的示例中，都推荐value是一个非常细粒度的值，甚至可以是一个字符串之类的原子值（在原本的React中使用非namespace型的对象作为state并不被提倡）。鼓励在一个函数组件中多次使用useState来得到不同维度的状态。
  - 在调用useState之外，函数组件依然会是一个实现渲染逻辑的纯组件，对状态的管理已经被Hooks内部所实现。
- 在我们的团队中，不定期地会相互强调一个原则：**有状态的组件没有渲染，有渲染的组件没有状态**
- getDerivedStateFromProps这一API想传递给开发者的思想，即不要再区分组件是否已经mount，使用统一的API来统一地进行状态管理
- 用3个属性来声明一个外部的依赖：
  - 数据在哪里（grab）：当数据有的时候，就没必要发起请求，这是一个很直接的逻辑。
  - 数据与什么相关（selector）：可以认为这是“获取数据的参数”，仅当参数发生变化时，请求才会被重新发起（当然数据不存在依然是前提）。
  - 怎么发起请求（fetch）：真正的请求逻辑。
- React的API设计
  - 对API的废弃有一整套成熟的流程。
    - 并不会在一个大版本中就立即抛弃N多的API，而是通过标记UNSAFE_、使用StrictMode等形式，给开发者一个平滑的过渡。
    - 这种跨越大版本的API废弃模式，我只在语言级框架如.NET、Java中见过，尚未在任何一个视图层的框架中见识。
  - 不该用而又不得不存在的API，会用尽办法恶心调用者。
    - 最为经典的dangerouslySetInnerHTML这一属性，除了加一个dangerously这么显眼的前缀外，还非得让它的值是一个对象，对象里还要有一个__html这样逼死强迫症的属性名。
    - 凡是对代码美感有一些些追求的开发者，都会想方设法让这东西消失在自己的眼前。
  - 所有的API都具备非常强的最佳实践引导性。
    - 比如getDerivedStateFromProps这一方法，硬是给做成了静态的，让开发者用不到this，也自然很难胡乱地在里面做出有副作用的事情来。
    - 现比如setState使用callback而不是Promise，并且官方义正言辞地拒绝了转为Promise实现。
    - 现在看到useState的出现，再回过头去看setState一直控制着让开发者尽量不使用callback是多么明智。
  - API的发布具有很好的承接性。
    - 先是componentDidCatch这一API，提供了Error Boundary的概念并让广大开发者接受，随后才是Suspence这个非常具备破坏力的炸弹，实际则是通过Error Bounday和Promise的类型判断来完成。
    - 这给了开发者接受和准备的时间，不至于因为一下子连带的太多概念而产生更强烈的抵触情绪。
  - 完全突破原有理论的API可以在没有大版本的情况下发布。
    - 从Suspence到Hooks，这两个API的发布确实给了我很大的震憾，而这震憾有很大一部分来自于它们居然只在一个小版本上就发布出来了，可见React原本简洁的API有着多大的包容性。
- 正因为有这么强大的API设计能力，React在引入Fiber这种几乎破坏性的底层变化之际，几乎没有在社区掀起反对的波浪。事实上有很多对React使用不当的场合是没有办法无缝地迁移到异步Fiber之上的，而15版本的React本身是可以搞出很多使用不当的场合的。依靠着自身API强大的最佳实践引导能力，Fiber的推进到开发者的适配几乎没有出现过大的失败案例

- 从HOC迁移到hooks的建议
  - 如果觉得实现hook没有思路，可以先实现HOC再翻译过来。
  - 组件的重要功能几乎都有hooks的对应，主要的setState -> useState和生命周期转为useEffect。
  - useEffect一共有3部分，即本体、返回的清理函数、依赖数组，分别对应生命周期的主要部分、componentDidUpdate和componentWillUnmount里的清理逻辑、componentDidUpdate里的if分支用到的属性。
  - 可以把原来用于HOC的展示组件继续复用，以前是包一层HOC，现在是新加一个组件先调用hook再渲染组件。当然这样依旧会造出组件树上多一个节点，是否要合并可以自行权衡。
  - hooks的一个特征是不访问props，因此通常调用HOC时传的propName之类的参数，在hook里会消失，变为直接将对应的属性值传过去
  - useCallback和useMemo对应以前reselect库提供的选择器

  

- 分析了这么多React-类的库，其核心思想有两个：
  - 将原生API转换为框架特有API，比如React系列的Hooks与ref
  - 处理生命周期导致的边界情况，比如dom被更新时先unobserve再重新observe

- 可以利用React Hooks，将React组件打造成：任何事物的变化都是输入源，当这些源变化时会重新触发组件的render，你只需要挑选组件绑定哪些数据源（use哪些Hooks），然后只管写render函数就行了
- DOM副作用修改/监听
  - 修改页面title
  - 监听window size变化
  - 监听网络断开
- 组件增强或辅助
  - 获取组件宽高
  - 我们对组件增强时，组件的回调一般不需要销毁监听，而且仅需监听一次，这与DOM监听不同
  - 因此大部分场景，我们需要利用 useCallback 包裹，并传一个空数组，来保证永远只监听一次，而且不需要在组件销毁时注销这个 callback
- 动画
  - useRaf
  - useSPring：获取动画值，组件以固定频率刷新，而这个动画值以弹性函数进行增减
  - useTween: 这个值的动画曲线是tween
- network
  - 可以将任意请求Promise封装为带有标准状态的对象：loading、error、result
  - useAsync
  - useService
  - useForm
- hooks模拟生命周期
  - useMount
  - useUpdate
- 存数据
  - 全局store
- 封装现有库
  - 用hooks替换render rops，可以包两层

``` JS
// class组件用法
import { Toggle } from 'react-powerplug'

function App() {
  return (
    <Toggle initial={true}>
      {({ on, toggle }) => (
        <Checkbox checked={on} onChange={toggle} />
      )}
    </Toggle>
  )
}
// ↓ ↓ ↓ ↓ ↓ ↓  hooks用法
import { useToggle } from 'react-powerhooks'

function App() {
  const [on, toggle] = useToggle()
  return <Checkbox checked={on} onChange={toggle} />
}

// hooks实现
export function Toggle() {
  // 这是 Toggle 的源码
}
const App = wrap(() => {
  // 第一步：包 wrap
  const [on, toggle] = useRenderProps(Toggle); // 第二步：包 useRenderProps
});
const wrappers = []; // 全局存储 wrappers

export const useRenderProps = (WrapperComponent, wrapperProps) => {
  const [args, setArgs] = useState([]);
  const ref = useRef({});
  if (!ref.current.initialized) {
    wrappers.push({
      WrapperComponent,
      wrapperProps,
      setArgs
    });
  }
  useEffect(() => {
    ref.current.initialized = true;
  }, []);
  return args; // 通过下面 wrap 调用 setArgs 获取值。
};
export const wrap = FunctionComponent => props => {
  const element = FunctionComponent(props);
  const ref = useRef({ wrapper: wrappers.pop() }); // 拿到 useRenderProps 提供的 Toggle
  const { WrapperComponent, wrapperProps } = ref.current.wrapper;
  return createElement(WrapperComponent, wrapperProps, (...args) => {
    // WrapperComponent => Toggle，这一步是在构造 RenderProps 执行环境
    if (!ref.current.processed) {
      ref.current.wrapper.setArgs(args); // 拿到 on、toggle 后，通过 setArgs 传给上面的 args。
      ref.current.processed = true;
    } else {
      ref.current.processed = false;
    }
    return element;
  });
};
```

- 封装原本对 `setState` 增强的库
  - immer
- 本文列出了React Hooks的以下几种使用方式以及实现思路：
  - DOM副作用修改/监听
  - 组件辅助
  - 做动画
  - 发请求
  - 填表单
  - 模拟生命周期
  - 存数据
  - 封装原有库

- `useState<S>(initialState: (() => S) | S)`
  - initialState初始值的类型S可以是函数
  - 注意不要写成下面的样子，类型S是 `undefined`
    - `const [f, setF] = useState(() => console.log("default ooops"));`
  - ` const [f, setF] = useState(() => () => console.log("default ooops"));`
- When you pass a function to `useState` , that function is meant to lazily initialize the initial state.
- If you want to use a function as a state value, you'll need to wrap it in another function that then returns that function.
- `useReducer` is more suitable in most cases when you would like to pass a function as a state 

``` JS
function testPromise() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve("done");
    }, 1000);
  });
}

function testRegular() {
  return "done";
}

function App() {
  const [p1, setP1] = useState(testPromise);
  const [r1, setR1] = useState(testRegular);
  const [p2, setP2] = useState(testPromise());
  const [r2, setR2] = useState(testRegular());
  console.log(p1, r1);
  console.log(p2, r2);

  // false
  console.log(p1 === p2)
  // true，useState的参数为函数时，会自动调用，都为done
  console.log(r1 === r2)
  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
    </div>
  );
}
```

- 每次Render都有自己的Props与State
- 每次Render都有自己的事件处理
- 每次Render都有自己的Effects
- 不仅是对象，函数在每次渲染时也是独立的，这就是Capture Value特性
- 利用 `useRef` 就可以绕过Capture Value的特性。可以认为 ref 在所有 Render 过程中保持着唯一引用，因此所有对ref 赋值或取值，拿到的都只有一个最终状态，而不会在每个Render间存在隔离
- 在组件被销毁时，会执行 `useEffect` 返回值函数内回调函数。同样，由于Capture Value特性，每次 “注册” “回收” 拿到的都是成对的固定值。
- 如果你明明使用了某个变量，却没有声明在依赖中，后果就是，当依赖的变量改变时，useEffect也不会再次执行，effect内拿到的就是旧值或初始值
- 如何保证useEffect高效执行
  - 尽量不依赖外部变量，如setState第一次参数写成函数
- 若同时依赖多个变量，可以使用useReducer
  - 不管更新时需要依赖多少变量，在调用更新的动作里都不需要依赖任何变量
  - 具体更新操作在reducer函数里写就可以了。
- 将函数写在useEffect中，如果函数不在useEffect内，可能会遗漏依赖
- 如果非要把函数写在useEffect外面，经过useCallback包装过的函数可以当作普通变量作为useEffect的依赖
- useEffect只要关心取数函数的变化，而取数参数的变化在useCallback时关心，再配合eslint插件的扫描，能做到依赖不丢、逻辑内聚，从而容易维护
- useEffect只是底层API，未来业务接触到的是更多封装后的上层API，比如 useFetch 或者 useTheme
- 重新梳理一下这篇文章的思路：

``` 
从介绍 Render 引出 Capture Value 的特性。
拓展到 Function Component 一切均可 Capture，除了 Ref。
从 Capture Value 角度介绍 useEffect 的 API。
介绍了 Function Component 只关注渲染状态的事实。
引发了如何提高 useEffect 性能的思考。
介绍了不要对 Dependencies 撒谎的基本原则。
从不得不撒谎的特例中介绍了如何用 Function Component 思维解决这些问题。
当你学会用 Function Component 理念思考时，你逐渐发现它的一些优势。
最后点出了逻辑内聚，高阶封装这两大特点
```

- useEffect在渲染结束时执行，所以不会阻塞浏览器渲染进程，所以使用Function Component写的项目一般都有用更好的性能。
- 自然符合React Fiber 的理念，因为Fiber会根据情况暂停或插队执行不同组件的Render，如果代码遵循了 Capture Value 的特性，在Fiber环境下会保证值的安全访问，同时弱化生命周期也能解决中断执行时带来的问题。
- useEffect不会在服务端渲染时执行。

- React Hooks要解决的问题是状态逻辑复用，只共享数据处理逻辑，不会共享数据本身
- hooks优点
  - 多个状态不会产生嵌套，写法还是平铺的
    - renderProps可以通过compose解决，不但使用略为繁琐，而且因为强制封装一个新对象而增加了实体数量。
  - Hooks可以引用其他Hooks。
  - 更容易将组件的UI与状态分离
- 一种实践：有状态的组件(使用useState)没有渲染(返回非UI)，有渲染(返回jsx)的组件没有状态(使用useState)
  - 也可以类比容器组件和展示组件
- 每次 `useReducer` 或者自己的 `useCustomHooks` 都不会持久化数据
  - React Hooks只提供状态处理方法，不会持久化状态
  - 如果要真正实现一个Redux功能，也就是全局维持一个状态，任何组件 `useReducer` 都会访问到同一份数据，可以和 `useContext` 一起使用。
- React Hooks并不是通过Proxy或者getters实现的，而是通过数组实现的，每次useState都会改变下标，如果useState被包裹在condition中，那每次执行的下标就可能对不上，导致useState导出的setter更新错数据。
- 第一次将 “约定优先” 理念引入了React框架中，带来了前所未有的代码命名和顺序限制，但带来的便利也是前所未有的。没有比React Hooks更好的状态共享方案了，约定带来提效，自由的代价就是回到Render Props or HOC，各团队可以自行评估
- 因为React Hooks的特性，如果一个Hook不产生 UI，那么它可以永远被其他Hook封装，虽然允许有副作用，但是被包裹在 `useEffect` 里，总体来说还是挺函数式的。而Hooks要集中在UI函数顶部写，也很容易养成书写无状态UI组件的好习惯，践行 “状态与 UI 分开” 这个理念会更容易。
- hooks组件里的状态何时被销毁呢？
  - 类似闭包，等待系统回收。组件销毁后不再产生状态。

- 如何不在每次渲染时重新实例化 `setInterval`

``` JS
// setState第一个参数使用函数
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      // 不依赖count状态
      setCount(c => c + 1);
    }, 1000);
    return () => clearInterval(id);
  }, []); // 依赖项为[]，只有初始化会对setInterval进行实例化

  return <h1>{count}</h1>;
}
```

  - 如果同时需要对count与step两个变量做累加，那 `useEffect` 的依赖必然要写上一种某一个值，频繁实例化的问题就又出现了
    - useReducer本质是让函数与数据解耦，函数只管发出指令，而不需要关心使用的数据被更新时，需要重新初始化自身
    - React确保dispatch的引用稳定不变

``` JS
// JavaScript
function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const { count, step } = state;

  useEffect(() => {
    const id = setInterval(() => {
      dispatch({ type: "tick" });
    }, 1000);
    return () => clearInterval(id);
  }, [dispatch]);

  return <h1>{count}</h1>;
}

function reducer(state, action) {
  switch (action.type) {
    case "tick":
      return {
        ...state,
        count: state.count + state.step
      };
  }
}
```

- 将函数写在 `useEffect` 内部
  - 可避免遗漏依赖项
- `useCallback` 可以将函数抽到 `useEffect` 外部
  - 方便传递事件处理方法

``` JS
function Counter() {
  const [count, setCount] = useState(0);

  const getFetchUrl = useCallback(() => {
    return "https://v?query=" + count;
  }, [count]);

  useEffect(() => {
    getFetchUrl();
  }, [getFetchUrl]);

  return <h1>{count}</h1>;
}
```

- 为什么 `useCallback` 比 `componentDidUpdate` 更好用
  - 以在函数参数变化时进行重新取数为例
  - 在componentDidUpdate中，判断这两个参数发生了变化就触发重新取数，，如果某一天fetchData多依赖了paramN这个参数，下游函数将需要全部在componentDidUpdate覆盖到这个逻辑
  - 换成Function Component后，eslint-plugin-react-hooks 会自动补上更新后的依赖，而下游的代码不需要做任何改变
- `useEffect` 对业务的抽象非常方便，举几个例子：
  - 依赖项是查询参数，那么useEffect内可以进行取数请求，那么只要查询参数变化了，列表就会自动取数刷新。注意我们将取数时机从触发端改成了接收端。
  - 当列表更新后，重新注册一遍拖拽响应事件。也是同理，依赖参数是列表，只要列表变化，拖拽响应就会重新初始化，这样我们可以放心的修改列表，而不用担心拖拽事件失效。
  - 只要数据流某个数据变化，页面标题就同步修改。同理，也不需要在每次数据变化时修改标题，而是通过 useEffect “监听” 数据的变化，这是一种 “控制反转” 的思维
- useCustomHooks可以将函数抽到组件外部
  - 如果要抽到整个组件的外部，就不是利用 `useCallback` 做到了，而是利用自定义Hooks来做
- 利用 `useRef` 保证耗时函数依赖不变
  - 将需要更新的区域与耗时区域分离，再将需更新的内容通过Ref提供给耗时的区域，实现性能优化。
  - 然而这样做对函数的改动成本比较高，有一种更通用的做法解决此类问题
- 通用的自定义Hooks解决函数重新实例化问题
  - 可以利用 `useRef` 创造一个自定义Hook代替 `useCallback` ，使其依赖的值变化时，回调不会重新执行，却能拿到最新的值
  - React官方不推荐使用此范式，因此对于这种场景，利用 `useReducer` ，将函数通过 `dispatch` 中调用，也可以
- 比 `React.memo` 更好用的渲染优化函数 `useMemo`
  - useMemo可以更细粒度的优化渲染
  - 所谓更细粒度的优化渲染，是指函数Child整体可能用到了 A、B 两个props，而渲染仅用到了 B，那么使用 `React.memo` 方案时，A 的变化会导致重渲染，而使用 `useMemo` 的方案则不会

``` JS
const Child = memo((props) => {
  useEffect(() => {
    props.fetchData()
  }, [props.fetchData])

  return (
    // ...
  )
})

const Child = (props) => {
  useEffect(() => {
    props.fetchData()
  }, [props.fetchData])

  return useMemo(() => (
    // ...
  ), [props.fetchData])
}
```

- 当参数越来越多时，使用props将函数、值在组件间传递非常冗长
- 当程序复杂时，可能存在多个函数在所有Function Component间共享的情况，此时useContext更合适
  - 这样就不需要在每个函数间进行参数透传了，公共函数可以都放在 `Context` 里
- 但是当函数多了， `Provider` 的 `value` 会变得很臃肿，可以结合 `useReducer` 解决问题
- 使用 `useReducer` ，所有回调函数都通过调用 `dispatch` 完成，那么 `Context` 只要传递 `dispatch` 一个函数就可以了

``` JS
// JavaScript
const Store = createContext(null);

function Parent() {
  const [state, dispatch] = useReducer(reducer, { count: 0, step: 0 });

  return (
    <Store.Provider value={dispatch}>
      <Child />
    </Store.Provider>
  );
}

const Child = useMemo((props) => {
  const dispatch = useContext(Store)

  function onClick() {
    dispatch({
      type: 'countInc'
    })
  }

  return (
    // ...
  )
})
```

- 将state也放到Context中，这下赋值与取值都非常方便了
- 问题在于：memo只能挡在最外层，而通过useContext的数据注入发生在函数内部，会绕过memo
  - 当触发 `dispatch` 导致state变化时，所有使用了state的组件内部都会强制重新刷新，此时想要对渲染次数做优化，只有拿出 `useMemo` 了
  - 使用useContext的组件，如果自身不使用props，就可以完全使用useMemo代替memo做性能优化

``` JS
// 
const Store = createContext(null);

function Parent() {
  const [state, dispatch] = useReducer(reducer, { count: 0, step: 0 });

  return (
    <Store.Provider value={{ state, dispatch }}>
      <Count />
      <Step />
    </Store.Provider>
  );
}
// 无论点击 incCount 还是 incStep，都会同时触发这两个组件rerender
const Count = memo(() => {
  const { state, dispatch } = useContext(Store);
  return (
    <button onClick={() => dispatch("incCount")}>incCount {state.count}</button>
  );
});

const Count = () => {
  const { state, dispatch } = useContext(Store);
  return useMemo(
    () => (
      <button onClick={() => dispatch("incCount")}>
        incCount {state.count}
      </button>
    ),
    [state.count, dispatch]
  );
};
```

- redux的 `Connect` 与 `useMemo`
  - 下面例子的功能一样，Function Component能自动进行依赖推导
  - Connect的场景：由于不知道子组件使用了哪些数据，因此需要在 mapStateToProps 提前写好，而当需要使用数据流内新变量时，组件里是无法访问的，我们要回到 mapStateToProps 加上这个依赖，再回到组件中使用它
  - useContext + useMemo 的场景：由于注入的state是全量的，Render函数中想用什么都可直接用，eslint-plugin-react-hooks会通过静态分析，在useMemo第二个参数自动补上代码里使用到的外部变量，比如state.count、dispatch。
  - Context很像Redux，那么Class Component模式下的异步中间件实现的异步取数怎么利用 `useReducer` 做呢？答案是：做不到
  - 比如上面抛出的异步取数场景，在Function Component的最佳做法是封装成一个自定义Hook
  - 如果这个值需要存储到数据流，在所有组件之间共享，我们可以结合useEffect与useReducer

``` JS
// redux
const mapStateToProps = state => ({ count: state.count });
const mapDispatchToProps = dispatch => dispatch;

@Connect(mapStateToProps, mapDispatchToProps)
class Count extends React.PureComponent {
  render() {
    return (
      <button onClick={() => this.props.dispatch("incCount")}>
        incCount {this.props.count}
      </button>
    );
  }
}

// useMemo
const Count = () => {
  const { state, dispatch } = useContext(Store);
  return useMemo(
    () => (
      <button onClick={() => dispatch("incCount")}>
        incCount {state.count}
      </button>
    ),
    [state.count, dispatch]
  );
};
```

- 对Function Component的defaultProps进行赋值
  - 建议使用React内置方案解决，因为纯函数的方案不利于保持引用不变

``` JS
// 每次默认值都会创建新对象，props都不同
function Button({ type = "primary", onChange = () => {} }) {}

// 不太优雅
const defaultType = { a: 1 };
const Child = ({ type = defaultType }) => {
  useEffect(() => {
    console.log("type", type);
  }, [type]);

  return <div>Child</div>;
};

// React内置方案
const Child = ({ type }) => {
  useEffect(() => {
    console.log("type", type);
  }, [type]);

  return <div>Child</div>;
};
Child.defaultProps = {
  type: { a: 1 }
};
```

- 案例：传递对象字面量作为prop给子组件

``` JS
// 父组件每次点击后都会刷新
function App() {
  const [count, forceUpdate] = useState(0);

  const schema = { b: 1 };

  return (
    <div>
      <Child schema={schema} />
      <div onClick={() => forceUpdate(count + 1)}>Count {count}</div>
    </div>
  );
}
// 父组件每次刷新，子组件都会打印日志，因为[props.schema]引用一直在变化
const Child = memo(props => {
  useEffect(() => {
    console.log("schema", props.schema);
  }, [props.schema]);

  return <div>Child</div>;
});

// 使用ref优化
function App() {
  const [count, forceUpdate] = useState(0);
  const schema = useRef({ b: 1 });

  return (
    <div>
      <Child schema={schema.current} />
      <div onClick={() => forceUpdate(count + 1)}>Count {count}</div>
    </div>
  );
}
```

  

- Function Component采用 `const + 箭头函数` 方式定义

``` typescript
//用React.FC申明组件类型与定义Props参数类型
const App: React.FC < { title: string } > = ({ title }) => {
    // 用useMemo优化渲染性能
  return React.useMemo(() => <div>{title}</div>, [title]);
};

// 用App.defaultProps定义Props的默认值
App.defaultProps = {
  title: 'Function Component'
}
```

- 为什么不用 `React.memo` ?
  - 推荐使用 `React.useMemo` 而不是 `React.memo` ，因为在组件通信时存在 `React.useContext` 的用法，这种用法会使所有用到的组件重渲染，只有 `React.useMemo` 能处理这种场景的按需渲染。
- 没有性能问题的组件也要使用 `useMemo` 吗？
  - 要，考虑未来维护这个组件的时候，随时可能会通过 useContext 等注入一些数据，这时候谁会想起来添加 useMemo 呢？
- 为什么不用解构方式代替 defaultProps?
  - 虽然解构方式书写defaultProps更优雅，但存在一个硬伤：对于对象类型每次rerender时引用都会变化，这会带来性能问题，因此不要这么做
- 局部状态有三种，常用的有： useState, useRef, useReducer 
- `useState` 的状态函数名要表意，尽量聚集在一起申明，方便查阅
- `useRef` 尽量少用，大量Mutable的数据会影响代码的可维护性
  - 但对于不需重复初始化的对象推荐使用useRef存储，比如 new G2()
- 局部状态不推荐使用 `useReducer` ，会导致函数内部状态过于复杂，难以阅读。 
  - useReducer建议在多组件间通信时，结合useContext一起使用。
- 可以在函数内直接申明普通常量或普通函数吗？
  - 不可以，Function Component每次渲染都会重新执行
  - 常量推荐放到函数外层避免性能问题，函数推荐使用useCallback声明
- 所有Function Component内函数必须用React.useCallback包裹，以保证准确性与性能。
  - 和任何场景都使用PureComponent一个道理, 假设你useCallback的依赖每次渲染都会改变, 那么这个useCallback就是负作用。
  - 以我个人的经验, useMemo主要用于memo类型组件的props上（如果不用这个memo类型组件就是负作用）, 以及创建开销过大的场景。
  - useCallback本质是useMemo的语法糖, 而function本身并不是创建开销过大的。
  - 所以我认为useCallback设计出来是和React.memo配套使用的。
  - 就算你用useCallback包裹了, 这个func每次render的时候也会重新创建，useCallback只是确定最终你传给组件的那个func是新的func还是旧的func, 所以说从开销上去讲并讲不通。
  - 我个人觉得useCallback主要是为了和memo组件组合使用，方便memo优化策略由于func props而失效
- If something is slow then try using PureComponent and see if it helps.
- If nothing is slow then don’t bother optimizing it.
- There is no sure way to tell which is going to be slower: reconciliation or shallow comparisons everywhere. 
- In pathological cases (shallow equality checks often failing) PureComponents can be slower. 
- So the only rule of thumb is to only add one when you know you have a perf problem and you can verify adding it solves that problem.
- useCallback 和 useMemo 用得好可以带来性能优化，但是它们本身也是有代价的。因为要缓存上一次的结果，而势必引起更大的内存开销，并不是做一下比较而已
- 加useMemo就是希望减少re-render，类似于pureComponent。但是我们已经知道在某些场景下是没法或者几乎很难memorize的。
  - 比如render中含有props.children的、依赖的观测值会频繁发生变化的。
  - 那么对这些组件进行useMemo就没什么效果，起不到减少re-render的效果。
- 我觉得用 `useMemo` 之前要确保真的性能提升了，否则可能并没有甚至更糟糕了。
  - React文档中确实有用 `useMemo` 来替代 `shouldComponentUpdate` 的用例，但并不代表他们提倡总是使用 useMemo。后者属于过早优化。
  - 我觉得大部分组件都不需要特地去做性能优化，除非涉及*高性能动画、长列表或者图表*等场景。
- `useMemo` 主要还是用来，防止在闭包中频繁触发**昂贵计算**。另外不在乎开销拿useMemo做scu也不是不可以，但你要做很多工作才能保证useMemo真的生效。比如像楼上提的，涉及组件有绑定函数的，除非可以在组件外定义再传进来，涉及动态传参的， useCallback 和 useMemo 往往要配对使用才有效
- `React.memo` 还是要用的，它比 `useMemo` 更往前一步，连实际的函数都不会执行。而useMemo还是会执行一次组件函数的，只是返回值是之前的，不会重复渲染子组件。这个能体现在react的profiler工具里。
- 发请求分为操作型发请求与渲染型发请求。

``` JS
// 操作型发请求，作为回调函数
return React.useMemo(() => {
  return (
    <div onClick={requestService.addList} />
  )
}, [requestService.addList])

// 渲染型发请求在 useAsync 中进行，比如刷新列表页，获取基础信息，或者进行搜索， 
// 都可以抽象为依赖了某些变量，当这些变量变化时要重新取数
const { loading, error, value } = useAsync(async () => {
  return requestService.freshList(id);
}, [requestService.freshList, id]);
```

- 简单的组件间通信使用透传props变量的方式，而频繁组件间通信使用useContext
- 当输入框频繁输入时，为了保证页面流畅，我们会选择在 `onChange` 时进行debounce 
  - 然而在Function Component中，我们有更优雅的方式实现
  - 其实在Input组件onChange使用debounce有一个问题，就是当Input组件受控时，debounce的值不能及时回填，导致甚至无法输入
  - React scheduling通过智能调度系统优化渲染优先级，我们其实不用担心频繁变更状态会导致性能问题。
  - 如果联动一个文本还觉得慢吗？ onChange本不慢，大部分使用值的组件也不慢，没有必要从onChange源头开始就debounce 。
  - 找到渲染性能最慢的组件（比如iframe组件），对一些频繁导致其渲染的入参进行useDebounce 。
- 对于父级 `onChange` 引用总是变动时，在使用 `useEffect` 时要注意调试上下文，注意父级传递的参数引用是否正确

- 函数式组件
  - 函数式组件就是在一个函数中返回React Element
  - 在本文中，我们给函数式组件的函数起个简单一点的名字：render函数
  - 在React内部，它会决定在何时调用render函数，并对返回的React Elements进行遍历，如果遇到函数组件，React便会继续调用这个函数组件
  - 这种把render函数交给React内部处理的机制，为引入状态带来了可能
  - 在本文中，为了方便描述，对于render函数的每次调用，称它为一帧

``` js
// 函数式组件就是在一个函数中返回React Element
const App = (props) => {
  const { title } = props;
  return (
    <h1>{title}</h1>
  );
};

// 调用render函数以执行渲染，会转译成React.createElement
// const appElement = App({ title: "XXX" }); // 不常用
const appElement = <App title="XXX" />; // 常用
ReactDOM.render(
  appElement,
  document.getElementById('app')
);
```

- **每一帧拥有独立的变量**
  - 案例: props的行为差异
  - count属性由父组件传入，初始值为0，每隔一秒增加1。点击“Alert Count”按钮，将延迟3秒钟弹出count的值
    - 函数组件弹窗中出现的值，与页面中文本展示的值不同，count是点击时的旧值
    - class组件弹窗值与页面中文本展示的值是一样，都是最新值
  - class组件中，我们是从this中获取到的props.count。this是固定指向同一个组件实例的。在3秒的延时器生效后，组件重新进行了渲染，this.props也发生了改变。当延时的回调函数执行时，读取到的this.props是当前组件最新的属性值
  - 函数组件中，每一次执行render函数时，props作为该函数的参数传入，它是函数作用域下的变量
  - 由于props是Example函数作用域下的变量，可以说对于这个函数的每一次调用中，都产生了新的props变量，它在声明时被赋予了当前帧的属性，他们相互间互不影响
  - 换一种说法，对于其中任一个props，其值在声明时便已经决定，不会随着时间产生变化。handleClick函数亦是如此。例如定时器的回调函数是在未来发生的，但props.count的值是在声明handleClick函数时就已经决定好的。
- `useState` 为当前的函数组件创建了一个状态，这个状态的值独立于函数存放。
  - useState会返回一个数组，在该数组中，得到该状态的值和更新该状态的方法。
  - 通过解构，该状态的值会赋值到当前render函数作用域下的一个常量state中
  - 当组件被创建而不是重用时，即在组件的第一帧中，该状态将被赋予初始值initialState，而之后的重用过程中，不会被重复赋予初始值。
- **每一帧拥有独立的状态**
  - state作为函数中的一个常量，就是普通的数据，并不存在诸如数据绑定这样的操作来驱使DOM发生更新。在调用setState后，React将重新执行render函数，仅此而已。
  - 状态也是函数作用域下的普通变量。我们可以说每次函数执行拥有独立的状态。
- 获取过去或未来帧中的值
  - 对于state，如果想要在第一帧时点击“Delay setCount”，在一个异步回调函数的执行中，获取到count最新一帧中的值，不妨向setCount传入函数作为参数
  - 其他情况下，例如需要读取到state及其衍生的某个常量，相对于变量声明时所在帧过去或未来的值，就需要使用 `useRef` ，通过它来**存放一个在所有帧中共享的变量**
  - 如果要与class组件进行比较，useRef的作用相对于让你在class组件的this上追加属性。
  - `const refObj = useRef(initialValue);` 你可以自己去设置 `refObj.current` 的值，设置它的值不会重新触发render函数
  - 同样的方法，我们可以用于保存任何值：某个prop，某个state变量，甚至一个函数等。在后面的Effects部分会很有用
- **每一帧可以拥有独立的Effects**
  - 若某个useEffect/useLayoutEffect有且仅有一个函数作为参数，那么每次render函数执行时该Effects也是独立的。因为它是在render函数中选择适当的时机执行。
  - 如果useEffect没有传入第二个参数，那么第一个参数传入的effect函数在每次render函数执行是都是独立的。每个effect函数中捕获的props或state都来自于那一次的render函数。
- 可以给 `useEffect` 传入第二个参数，作为依赖数组(deps)，避免Effects不必要的重复调用
  - deps的含义是当前Effect依赖了哪些变量
  - 若Effects依赖了函数或者其他引用类型，与原始数据类型不同的是，在未优化的情况下，每次render函数调用时，因为对这些内容的重新创建，其值总是发生了变化，导致Effects在使用deps的情况下依然会频繁被调用。
  - 对于函数，使用 `useCallback` 避免重复创建；对于对象或者数组，则可以使用 `useMemo` 。从而减少deps的变化。
- 有一个最佳实践：状态变更时，应该通过 `setState` 的函数形式来代替直接获取当前状态
- 对于一些变量不希望引起effect重新更新的，使用ref解决。
- 对于获取状态用于计算新的状态的，尝试 `setState` 的函数入参，或者使用 `useReducer` 整合多个类型的状态。
- `useMemo` 的含义是，通过一些变量计算得到新的值，通过把这些变量加入依赖deps，当deps中的值均未发生变化时，跳过这次计算。
  - useMemo中传入的函数，将在render函数调用过程被同步调用。
  - 可以使用useMemo缓存一些相对耗时的计算。
  - 除此以外，useMemo也非常适合用于存储引用类型的数据，可以传入对象字面量，匿名函数等，甚至是React Elements。
  - 在这些例子中，useMemo的目的其实是尽量使用缓存的值。
  - 对于函数，其作为另外一个useEffect的deps时，减少函数的重新生成，就能减少该Effect的调用，甚至避免一些死循环的产生; 
  - 对于对象和数组，如果某个子组件使用了它作为props，减少它的重新生成，就能避免子组件不必要的重复渲染，提升性能。
  - 对于组件返回的React Elements，我们可以选择性地提取其中一部分elements，通过useMemo进行缓存，也能避免这一部分的重复渲染。
- 在过去的class组件中，我们通过 `shouldComponentUpdate` 判断当前属性和状态是否和上一次的相同，来避免组件不必要的更新。
  - 其中的比较是对于本组件的所有属性和状态而言的，无法根据 `shouldComponentUpdate` 的返回值来使该组件一部分elements更新，另一部分不更新。
  - 为了进一步优化性能，我们会对大组件进行拆分，拆分出的小组件只关心其中一部分属性，从而有更多的机会不去更新。
  - 而函数组件中的 `useMemo` 其实就可以代替这一部分工作。
- 虽然initialState的计算只在初始化时有其存在的价值，但在每一帧都被调用了，如果是一个相对耗时的操作，也可能占用很多性能
  - 可以使用惰性初始化
  - 因 `someExpensiveComputation` 运行在一个匿名函数下，该函数当且仅当初始化时被调用，从而优化性能。
  - 我们甚至可以跳出计算state这一规定，来完成任何昂贵的初始化操作

``` JS
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});

useState(() => {
  someExpensiveComputation(props);
  return null;
});
```

- **避免滥用refs**
  - 当 `useEffect` 的依赖频繁变化，你可能想到把频繁变化的值用 `ref` 保存起来。
  - 然而， `useReducer` 可能是更好的解决方式：使用 `dispatch` 消除对一些状态的依赖
- 最终可以总结出这样的实践
  - useEffect对于函数依赖，尝试将该函数放置在effect内，或者使用 `useCallback` 包裹；
  - useEffect/useCallback/useMemo，对于state或者其他属性的依赖，根据eslint的提示填入deps；
  - 如果不直接使用state，只是想修改state，用setState的函数入参方式 `setState(c => c + 1)` 代替；
  - 如果修改state的过程依赖了其他属性，尝试将state和属性聚合，改写成 `useReducer` 的形式。
  - 当这些方法都不奏效，使用 `ref` ，但是依然要谨慎操作。
- **避免滥用useMemo**
  - 使用 `useMemo` 当deps不变时，直接返回上一次计算的结果，从而使子组件跳过渲染。
  - 但是当返回的是原始数据类型（如字符串、数字、布尔值）。即使参与了计算，只要deps依赖的内容不变，返回结果也很可能是不变的。
  - 此时就需要权衡这个计算的时间成本和useMemo额外带来的空间成本（缓存上一次的结果）了。
  - 此外，如果useMemo的deps依赖数组为空，这样做说明你只是希望存储一个值，这个值在重新render时永远不会变。

``` JS
const Comp = () => {
    const data = useMemo(() => ({ type: 'xxx' }), []);
    return <Child data={data}>;
}

// 可被替换为

const Comp = () => {
    const { current: data } = useRef({ type: 'xxx' });
    return <Child data={data}>;
}

const data = { type: 'xxx' };
const Comp = () => {
    return <Child data={data}>;
}
```

- 如果deps频繁变动，我们也要思考，使用 `useMemo` 是否有必要。
- 因为 `useMemo` 占用了额外的空间，还需要在每次render时检查deps是否变动，反而比不使用useMemo开销更大
- 外部无法直接控制state的方式，我们称为**非受控hook**

``` JS
// 非受控hook示例
// 因为useState参数代表的是初始值，仅在useSomething初始时赋值给了count state。
// 后续count的状态将与inputCount无关，若外部传入的inputCount属性发生了变化，count不会更新

useSomething = (inputCount) => {
  const [count, setCount] = useState(inputCount);
};
```

- 若要在props变化的同时更新state，这就是drived state，尽量不要这么用，容易引发新问题
  - setCount后，React会立即退出当前的render并用更新后的state重新运行render函数
  - 在这种的机制下，state由外界同步的同时，内部又有可能通过setState来修改state，可能引发新的问题
  - 建议将inputCount的当前值与上一次的值进行比较，只有确定发生变化时执行setCount(inputCount)

``` JS
// 可以在渲染过程中更新state，React会立即退出第一次渲染并用更新后的state重新运行组件以避免耗费太多性能
useSomething = (inputCount) => {
  const [count, setCount] = setState(inputCount);
  setCount(inputCount);
};
```

- hooks的使用体验就是简单，无生命周期，无this指向问题，逻辑复用也简单，无HOC或Render Props的繁琐
- hooks组件的每一次渲染都是独立的，每一次的render都是一个独立的作用域，拥有自己的props和state、事件处理函数等
  - 每一次的render都是一个互不相关的独立的函数，拥有完全独立的函数作用域，执行该渲染函数，返回相应的渲染结果
- 而类组件则不同，类组件中的props和state在整个生命周期中都是指向最新的那次渲染
  - 类组件在渲染开始的时候会在类组件的构造函数中生成一个props和state, 所有的渲染过程都是在一个渲染函数中进行的并且，每一次的渲染中都不会去生成新的state和props，而是将值赋值给最开始被初始化的this.props和this.state
- 因为React hooks组件在每一次渲染的过程中都会生成独立的所用域，在组件内部的子函数和变量等在每次渲染的时候都会重新生成
  - 因此我们应该减少在React hooks组件内部声明函数。
  - 如果函数与组件内的state和props无相关性，那可以声明在组件的外部
  - 如果函数与组件内的state和props强相关性，那可以使用useCallback和useMemo
- React hooks中的state和props, 在每次渲染的过程中都是重新生成和独立的，那么我们如果需要一个对象，从开始到一次次的render1 , render2, ... 中引用地址都是不变的，可以使用 `useRef`
- `useRef` 使用场景
  - 存放上一次渲染的state
- 每次渲染都会生成不同的render函数，并且每一次渲染通过useEffect会生成一个不同的Effects，Effects在每次渲染后生效
- 将与state和props无关的函数，声明在hooks组件外面可以提高组件的性能，减少每次在渲染中重新声明该无关函数
- 有时候我们必须要在hooks组件内定义函数或者方法，那么推荐用 `useCallback` 缓存这个方法，当useCallback的依赖项不发生变化的时候，该函数在每次渲染的过程中不需要重新声明
- useCallback接受两个参数，第一个参数是要缓存的函数，第二个参数是一个数组，表示依赖项，当依赖项改变的时候会去重新声明一个新的函数，否则就返回这个被缓存的函数.
- `useMemo` 与 `useCallback` 大同小异，区别就是useMemo缓存的不是函数，缓存的是对象（可以是jsx虚拟dom对象），同样的，当依赖项不变的时候就返回这个被缓存的对象，否则就重新生成一个新的对象。
- 建议：在hooks组件中声明的任何方法，或者任何对象都必须要包裹在useCallback或者useMemo中。
- useCallback和useMemo中的依赖项前后是通过 `Object.is` 来比较是否相同的，因此是浅比较。
- 最基础的想法可能就是通过useContext来解决组件间的通信问题
- 在useContext的基础上，业界有几个比较简单的封装 
  - [unstated-next](https://github.com/jamiebuilds/unstated-next)
  - [constate](https://github.com/diegohaz/constate)
- 如果context太多，那么如何维护这些context
  - 在大量组件通信的场景下，用context进行组件通信代码的可读性很差。
  - 这和类组件的场景一致，context不是一个新的东西，虽然用了useContext减少了context的使用复杂度。
- hooks组件间的通信，同样可以使用redux来实现
  - 可以使用react-redux 7.1提供的hooks
  - useSelector()、useDispatch()、useStore()这3个主要方法，分别对应与mapState、mapDispatch以及直接拿到redux中store的实例
