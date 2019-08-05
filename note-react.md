---
title: note-react
created: '2019-08-01T05:09:11.917Z'
modified: '2019-08-02T10:21:48.141Z'
tags: [js/react]
---

# note-react

## devlog
- 不要在同一个方法连续写两个setState()，异步更新可能只更新一个

## summary

- react要点
    - 组件通用格式
        - jsx
        - 声明周期
    - 单向数据流
    - 虚拟DOM结构
        - 减少DOM操作
        
    - 高阶组件
    - ref引用与非受控组件
    - context
    
- react包
    - react-dom
        - ReactDOM.render, .unmountComponentAtNode, .findDOMNode  
    - react-dom/server
        - ReactDOMServer.renderToString, .renderToStaticMarkup.
    - prop-types
    
- 高阶组件 Higher-Order Components  
    - 概念   
    高阶组件是一个函数，接收一个组件作为输入，返回一个功能进行处理后的新组件      
    - 多个hoc嵌套的执行顺序 
    `withDefaultProps(withCalSize(withAccessor(withTooltip(PiePlot))));`   
    属性从外层向里传，越来越多  
    - 使用  
        - 高阶组件调用wrapper组件的方法：使用ref    
        ```js
              var Wrapper = (Home) => {
                return React.createClass({
                  render() {
                    return (
                        <div>
                            <button onClick={() => {this.home.someFunc()}} />
                            <Home
                                {...this.props}
                                ref={(c) => this.home = c;}
                            />
                        </div>
                    );
                  }
                })
              }
        ```
    - 注意事项
        - 不要在render()方法中使用高阶组件
        - wrapped组件的静态方法要手动拷贝
        - 避免将高阶组件的refs传递给wrapped组件
    - 实现方法 
        - 属性代理
        - 继承反转
- react mixins 
    - mixins引入了隐式依赖关系
    - 不同mixins的相同方法会导致命名冲突
    - mixins之间相互依赖容易增加复杂度
- 核心
    - 组件声明周期
    - 单向数据流

## doc 4 react

>React is, in our opinion, the premier way to build big, fast Web apps with JavaScript. It has scaled very well for us at Facebook and Instagram.

- hello world
```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

- jsx  
    - 一种 JavaScript 的语法扩展，js表达式要包含在大括号里  
    - 推荐在 JSX 代码的外面扩上一个小括号，这样可以防止 分号自动插入 的 bug
    - 在编译之后呢，JSX 其实会被转化为普通的 JavaScript 对象。
    - 可以在 if 或者 for 语句里使用 JSX，将它赋值给变量，当作参数传入，作为返回值都可以
    - React DOM 在渲染之前默认会 过滤 所有传入的值，所有的内容在渲染之前都被转换成了字符串，可以有效地防止 XSS(跨站脚本) 攻击
    - Babel 转译器会把 JSX 转换成一个名为 React.createElement() 的方法调用。
    - 本质上来讲，JSX 只是为 `React.createElement(component, props, ...children)` 方法提供的语法糖
    如果没有子代，你还可以使用自闭合标签  
    - 大写开头的 JSX 标签表示一个 React 组件，这些标签将会被编译为同名变量并被引用
    - 由于 JSX 编译后会调用 React.createElement 方法，所以在你的 JSX 代码中必须首先声明 React 变量
    - 在运行时选择类型  
    不能使用表达式来作为 React 元素的标签。如果你的确想通过表达式来确定 React 元素的类型，请先将其赋值给大写开头的变量  
    ```js
    function Story(props) {
      // 错误！JSX 标签名不能为一个表达式。
      return <components[props.storyType] story={props.story} />;
    }
    ```
    ```js
    function Story(props) {
      // 正确！JSX 标签名可以为大写开头的变量。
      const SpecificStory = components[props.storyType];
      return <SpecificStory story={props.story} />;
    }
    ```
    - 如果你没有给属性传值，它默认为 true  
    ```
    <MyTextBox autocomplete />
    等价于
    <MyTextBox autocomplete={true} />
    ```
    - 在包含开始和结束标签的 JSX 表达式中，标记之间的内容作为特殊的参数传递：props.children
    ```
    <MyComponent>foo</MyComponent>
    等价于
    <MyComponent>{'foo'}</MyComponent>
    ```
    - false、null、undefined 和 true 都是有效的子代，但它们不会直接被渲染
    ```
    等价  
    <div />
    <div></div>
    <div>{false}</div>
    <div>{null}</div>
    <div>{undefined}</div>
    <div>{true}</div>
    ```
    ```
    <div>
      // 典型用法 
      {showHeader && <Header />}
    </div>
    ```

- react元素
    - 是react组件的一部分，是仅包含 dom结构的对象
    - React DOM 首先会比较元素内容先后的不同，而在渲染过程中只会更新改变了的部分。
    - React 元素都是immutable 不可变的，当元素被创建之后，你是无法改变其内容或属性的
    - 更新界面的唯一办法是创建一个新的元素，然后将它传入 ReactDOM.render() 方法：
    - 将界面视为一个个特定时刻的固定内容（就像一帧一帧的动画），而不是随时处于变化之中，将会有利于我们理清开发思路
    
- react 组件
    - 组件从概念上看就像 函数，它可以接收任意的输入值（props），并返回一个需要在页面上展示的React元素。
    - 函数定义组件  
    ```js
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    ```  
    - class定义组件
    - 组件名称必须以大写字母开头。
    - 当React遇到的元素是用户自定义的组件，它会将JSX属性作为单个对象props传递给该组件
    - 所有的React组件必须像纯函数那样使用它们的props，决不能修改它自己的props
    
-   state
    - state是私有的，完全受控于当前组件
    - 如果你不在 render() 中使用某些东西，它就不应该在状态中。
    - 构造函数是唯一能够初始化 this.state 的地方
    - 不要直接更新状态 `this.state.comment = 'Hello';` 不会触发重新渲染，应当使用 setState({})  
    - 除非shouldComponentUpdate() 返回false，否则setState()永远都会导致重渲
    - 状态更新可能是异步的，React 可以将多个setState() 调用合并成一个调用来提高性能  
     this.props 和 this.state 可能是异步更新的，你不应该依靠它们的值来计算下一个状态。
     ```
     // Wrong
     this.setState({
       counter: this.state.counter + this.props.increment,
     });
     ```
     - setState 的调用是异步的，在调用 setState 之后，不要依赖 this.state 来立即反映新值。  
     如果你需要基于当前状态的计算值（请参阅下面的详细信息），则传递更新函数而不是对象。  
     
     ```
     // Correct
     this.setState((prevState, props) => ({
       counter: prevState.counter + props.increment
     }));
     ```
     ```
     // Correct
     this.setState(function(prevState, props) {
       return {
         counter: prevState.counter + props.increment
       };
     });
     ```
    - 调用 setState() 时，React 将你提供的对象合并到当前状态，是浅合并       
    - 自顶向下或单向数据流，任何状态始终由某些特定组件所有，并且从该状态导出的任何数据或UI只能影响树中下方的组件
    - setState()将需要处理的变化塞入（setState源码中将一个需要改变的变化存放到组件的state对象中，采用队列处理）组件的state对象中， 
    并告诉该组件及其子组件需要用更新的状态来重新渲染。这是用于响应事件处理和服务端响应的更新用户界面的主要方式
    - setState()不是立刻更新组件。其可能是批处理或推迟更新。这使得在调用setState()后立刻读取this.state的一个潜在陷阱。  
    代替地，使用componentDidUpdate或一个setState回调（setState(updater, callback)），当中的每个方法都会保证在更新被应用之后触发。  
    - 调用forceUpdate()将会导致组件的 render()方法被调用，并忽略shouldComponentUpdate()
    这将会触发每一个子组件的生命周期方法，涵盖，每个子组件的shouldComponentUpdate() 方法
        
- 事件
    - 使用区别
    ```js
    //html
    <button onclick="activateLasers()">
      Activate Lasers
    </button>
    ```
    ```js
    //react
    <button onClick={activateLasers}>
      Activate Lasers
    </button>
    ```
    - 不能使用返回 false 的方式阻止默认行为。你必须明确的使用 `e.preventDefault()`
    这里的e是react定义的合成事件SyntheticEvent
    - 监听器  
    不需要使用 addEventListener 为一个已创建的 DOM 元素添加监听器。  
    仅仅需要在这个元素初始渲染的时候提供一个监听器
    - es6类的方法默认是不会绑定 this
    - 事件传参
    ```js
    <button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
    <button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
    ```
    参数 e 作为 React 事件对象将会被作为第二个参数进行传递   
    通过箭头函数的方式，事件对象必须显式的进行传递  
    但是通过 bind 的方式，事件对象以及更多的参数将会被隐式的进行传递  
    bind方式向监听函数传参，在类组件中定义的监听函数，事件对象 e 要排在所传递参数的后面
    
- 条件渲染
    - true && expression 总是返回 expression
    - 你可能希望隐藏组件，即使它被其他组件渲染  
    让 render 方法返回 null 而不是它的渲染结果即可实现

- list
    - 要给每个列表元素分配一个 key 
    - Keys可以在DOM中的某些元素被增加或删除的时候帮助React识别哪些元素发生了变化  
    - 当元素没有确定的id时，你可以使用他的序列号索引index作为ke
    - 如果列表可以重新排序，我们不建议使用索引来进行排序，因为这会导致渲染变得很慢

- form
    - 受控组件    
    值由React控制的输入表单元素称为“受控组件”  
    在HTML当中，像<input>,<textarea>, 和 <select>这类表单元素会维持自身状态，并根据用户输入进行更新。  
    但在React中，可变的状态通常保存在组件的state中，并且只能用 setState() 方法进行更新  
    - input file 是 React 中的一个非受控组件
    - 当有处理多个受控的input元素时，可以通过给每个元素添加一个name属性，来让处理event.target.name的值
    ```js
    inputChangeHandler(event) {
      this.setState({ [event.target.name]: event.target.value });
    }
    ```
    - 有时使用受控组件可能很繁琐，或许可以看看非受控组件，这是一种表单的替代技术

- 状态提升
    - lifting state up  
    状态分享是通过将state数据提升至离需要这些数据的组件最近的父组件来完成的。这就是状态提升
    - 在React应用中，对应任何可变数据理应只有一个单一“数据源”。  
    通常，状态都是首先添加在需要渲染数据的组件中。此时如果另一个组件也需要这些数据，可以将数据提升至离它们最近的父组件中   
    你应该在应用中保持 自上而下的数据流，而不是尝试在不同组件中同步状态。
    - 状态提升比双向绑定方式要写更多的“模版代码”，但带来的好处是，你也可以更快地寻找和定位bug的工作  
    
- Composition vs Inheritance
    - 建议使用组合而不是继承来复用组件之间的代码  
    - 一些组件不能提前知道它们的子组件是什么，如Dialog这类通用容器尤其常见  
    建议这些组件使用 children 属性将子元素直接传递到输出  
    ```js
       function FancyBorder(props) {
         return (
           <div className={'FancyBorder FancyBorder-' + props.color}>
             {props.children}
           </div>
         );
       }
    ```
    - Facebook网站使用了数以千计的react组件，然而却还未发现任何需要推荐你使用继承的情况
    - 属性和组合为你提供了以清晰和安全的方式自定义组件的样式和行为所需的所有灵活性
    - 组件可以接受任意元素，包括基本数据类型、React 元素或函数
    - 在组件之间复用 **UI无关** 的功能，我们建议将其提取到单独的js模块中  
    这样可以在不对组件进行扩展的前提下导入并使用该函数、对象或类
      
- Thinking In React
    - Start With A Mock
    想象我们已经有一个 JSON 接口、一个设计师给我们的原型图、json接口或数据
    - 第一步：把 UI 划分出组件层级
    - 第二步：用 React 创建一个静态版本，只使用props
    - 第三步：定义 UI 状态的最小(但完整)表示
    ```
    看每一条，找出哪一个是 state。每个数据只要考虑三个问题：
    它是通过 props 从父级传来的吗？如果是，他可能不是 state。
    它随着时间推移不变吗？如果是，它可能不是 state。
    你能够根据组件中任何其他的 state 或 props 把它计算出来吗？如果是，它不是 state。
    ```
    - 第四步：确定你的 State 应该位于哪里
    - 第五步：添加反向数据流
    确保每当用户更改表单时，我们更新状态来反应用户输入，可以使用输入上的 onChange 事件

- PropTypes 检查类型
    - 当你给属性传递了无效值时，JavsScript 控制台将会打印警告。出于性能原因，propTypes 只在开发模式下进行检查
    - PropTypes.element可以指定只传递一个子代
    - 类型检查发生在 defaultProps 赋值之后，所以类型检查也会应用在 defaultProps 上面
    
- ref
    - 通常props是父组件与子代交互的唯一方式，要修改子组件，你需要使用新的 props 重新渲染它
    - 某些情况下你需要在典型数据流外强制修改子代。要修改的子代可以是 React 组件实例，也可以是 DOM 元素
    - 使用ref的场景
        - 处理焦点、文本选择或媒体控制。
        - 触发强制动画。
        - 集成第三方 DOM 库
    - React支持给任意组件添加ref属性，ref接受一个回调函数，它在组件被加载或卸载时会立即执行
    - 当给 HTML 元素添加 ref 属性时，ref 回调接收了底层的 DOM 元素作为参数，使用 ref 回调来存储 DOM 节点的引用
    React 组件在加载时将 DOM 元素传入 ref 的回调函数，在卸载时则会传入 null。  
    ref 回调会在componentDidMount 或 componentDidUpdate 这些生命周期回调之前执行
    - 当 ref 属性用于使用 class 声明的自定义组件时，ref 的回调接收的是已经加载的 React 实例
    这种方法仅对 class 声明的组件有效
    - 不能在函数式组件上使用 ref 属性，因为它们没有实例
    但可以在函数式组件内部使用 ref，只要它指向一个 DOM 元素或者 class 组件
    - 你可能希望从父组件访问子节点的 DOM 节点。通常不建议这样做，因为它会破坏组件的封装
    虽然你可以向子组件添加 ref,但这不是一个理想的解决方案，因为你只能获取组件实例而不是 DOM 节点。  
    建议在子节点上暴露一个特殊的属性。子节点将会获得一个函数属性，并将其作为 ref 属性附加到 DOM 节点。  
    这允许父代通过中间件将 ref 回调给子代的 DOM 节点。
    ``` 
    function CustomTextInput(props) {
      return (
        <div>
          <input ref={props.inputRef} />
        </div>
      );
    }
    
    class Parent extends React.Component {
      render() {
        return (
          <CustomTextInput
            inputRef={el => this.inputElement = el}
          />
        );
      }
    }
    ```
    - 如果你无法完全控制子组件，最后的办法是使用 findDOMNode()，但是不推荐这样做
    - 如果 ref 回调以内联函数的方式定义，在更新期间它会被调用两次，第一次参数是 null ，之后参数是 DOM 元素  
    通过将 ref 的回调函数定义成类的绑定函数的方式可以避免上述问题  

- 非受控组件
    - 要编写一个非受控组件，而非为每个状态更新编写事件处理程序，你可以 使用 ref 从 DOM 获取表单值。
    - 非受控组件将真实数据保存在 DOM 中

- React性能优化
    - 避免重复渲染
    可以通过重写这个生命周期函数shouldComponentUpdate来提升速度， 它是在重新渲染过程开始前触发的。   
    这个函数默认返回true，可使React执行更新      
    - 大部分情况下，你可以使用React.PureComponent而不必写你自己的shouldComponentUpdate，它只做一个浅比较。  
    但是由于浅比较会忽略属性或状态改变的情况，此时你不能使用它
    - 使用不变的数据结构

- Reconciliation 协调
    - 目的
    当你使用React，在单一时间点你可以考虑render()函数作为创建React元素的树。    
    在下一次状态或属性更新，render()函数将返回一个不同的React元素的树。React需要算出如何高效更新UI以匹配最新的树  
    - 将一棵树转换为另一棵树的最小操作数算法
    React基于两点假设，实现了一个启发的O(n)算法：  
        - 两个不同类型的元素将产生不同的树。
        - 通过渲染器附带key属性，开发者可以示意哪些子元素可能是稳定的
    - 对比算法
    - 不同类型的元素
        - 对比两棵树时，React首先比较两个根节点。根节点的type不同，其行为也不同
        - 当树被卸载，旧的DOM节点将被销毁。组件实例会调用componentWillUnmount()。  
        - 当构建一棵新树，新的DOM节点被插入到DOM中。组件实例将依次调用componentWillMount()和DidMount()。任何与旧树有关的状态都将丢弃。
        - 这个根节点下所有的组件都将会被卸载，同时他们的状态将被销毁
    - 相同类型的DOM元素
        - 当比较两个相同类型的React DOM元素时，React则会观察二者的属性，保持相同的底层DOM节点，并仅更新变化的属性
        - 在处理完DOM元素后，React递归其子元素。
   - 相同类型的组件元素
        - 当组件更新时，实例仍保持一致，以让状态能够在渲染之间保留。
        - React通过更新底层组件实例的props来产生新元素，并在底层实例上依次调用componentWillReceiveProps()和WillUpdate() 方法。
        - 接下来，render()方法被调用，同时对比算法会递归处理之前的结果和新的结果   
   - list
        - 传递在数组中的索引作为key时，若元素没有重排，该方法效果不错，但重排会使得其变慢。
        - 不稳定的key（如Math.random()生成的）将使得大量组件实例和DOM节点进行不必要的重建，使得性能下降并丢失子组件的状态

- context
    - 跨层传递属性
    ``` 
      //父组件
      getChildContext() {
        return {color: "purple"};
      }
    ```
    ``` 
    //子孙组件
    this.context.color
    ```
    - 如果在一个组件中定义了contextTypes，那么下面这些生命周期函数中将会接收到额外的参数，即context对象
    作为最后一个参数
    - 无状态函数组件也是可以引用context
    - 没有一种可靠的方式来更新context，所以千万别更新

- Fragments
    - Fragments 可以让你聚合一个子元素列表，并且不在DOM中增加额外节点
    - 使用1 语法糖
    ``` 
    class Columns extends React.Component {
      render() {
        return (
          <>
            <td>Hello</td>
            <td>World</td>
          </>
        );
      }
    }
    ```
    - 使用2
    ``` 
    class Columns extends React.Component {
      render() {
        return (
          <React.Fragment  key={item.id}>
            <td>Hello</td>
            <td>World</td>
          </React.Fragment>
        );
      }
    }
    ```
    - key 是唯一可以传递给 Fragment 的属性。在将来，我们可能增加额外的属性支持，比如事件处理。

- Portals
    - Portals 提供了一种很好的将子节点渲染到父组件以外的 DOM 节点的方式。
    - 使用
    ``` 
    render() {
      // React does *not* create a new div. It renders the children into `domNode`.
      // `domNode` is any valid DOM node, regardless of its location in the DOM.
      return ReactDOM.createPortal(
        this.props.children,
        domNode,
      );
    }
    ```
    - 第一个参数（child）是任何可渲染的React子元素，例如元素，字符串或碎片。第二个参数（container）则是一个DOM元素
    - 一个从 portal 内部会触发的事件会一直冒泡至包含 React 树 的祖先

- Error Boundaries
    - 错误边界是用于捕获其子组件树 JavaScript 异常，记录错误并展示一个回退的 UI 的 React 组件，而不是整个组件树的异常
    - 错误组件在渲染期间，生命周期方法内，以及整个组件树构造函数内捕获错误。
    - 无法捕获的错误
        - 事件处理 （了解更多）
        - 异步代码 （例如 setTimeout 或 requestAnimationFrame 回调函数）
        - 服务端渲染
        - 错误边界自身抛出来的错误 （而不是其子组件）
    - componentDidCatch() 方法机制类似于 JavaScript catch {}，但是针对组件。仅有类组件可以成为错误边界
    
- Web Components
    - React是提供了保持DOM和数据同步的声明式库
    - Web组件为可重用组件提供了强大的封装能力
    - 由Web组件触发的事件可能无法通过React渲染树来正确冒泡。
      
- Render Props
    - 指一种在 React 组件之间使用一个值为函数的 prop 在 React 组件间共享代码的技术
    - 可以使用一个带有 render props 的常规组件来实现大量的 高阶组件 (HOC)

- React API
    - findDOMNode 是用于操作底层DOM节点的备用方案。在大部分情况下都不提倡使用这个方案，因为它破坏了组件的抽象化。
    - findDOMNode 只对挂载过的组件有效（也就是已经添加到DOM中去的组件）。如果你试图对一个未挂载的组件调用这个函数 （比如在一个还未创建的组件的 render() 函数中中调用 findDOMNode()），程序会抛出一个异常。
    - findDOMNode 不能用于函数式的组件中。
    - ReactDOM.render() 控制你传进来的容器节点里的的内容。第一次被调用时，内部所有已经存在的DOM元素都会被替换掉。  
    之后的调用会使用React的DOM比较算法进行高效的更新。
    - ReactDOM.render()不会修改容器节点（只修改容器的子项）。你可以在不覆盖已有子节点的情况下添加一个组件到已有的DOM节点中去。
    - ReactDOM.render() 目前会返回一个引用， 指向 ReactComponent的根实例。但是这个返回值是历史遗留，应该避免使用。  
    因为未来版本的React可能会在某些情况下进行异步渲染。如果你真的需要一个指向 ReactComponent 的根实例的引用，推荐的方法是添加一个 callback ref到根元素上。
    
## faq

- fiber是React 16中新的和解引擎，它的主要目的是使虚拟DOM能够进行增量渲染   
- vdom虚拟的视图被保存在内存中，并通过诸如ReactDOM这样的库与“真实”的DOM保持同步
- 常用的 受控组件
    - input
    - textarea
    - select
    - checkbox
    - radio button
    - form


    
