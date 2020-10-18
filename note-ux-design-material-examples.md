---
title: note-ux-design-material-examples
tags: [examples, material-design]
created: '2020-10-18T14:01:57.034Z'
modified: '2020-10-18T14:02:22.054Z'
---

# note-ux-design-material-examples

## material components for react

- ### material-components-web-react
- https://github.com/material-components/material-components-web-react
  - 未使用hooks，基于class组件实现
  - 常用props
    - className,id,label,selected
  - 常用state
    - classList,leadingIconClassList,value
  - 实现的简单组件示例，如Fab
  - 在componentDidMount中创建MDCFoundation实例，并调用 `this.foundation.init();`
  - 在componentWillUnmount中调用 `this.foundation.destroy();`
  - adapter存取器方法的属性中很多setState
  - 一般都有根据props计算拼接classes的方法
  - 组件暴露的handleChange等事件处理方法，大多都调用foundation中的方法
  - 函数ref可作为普通属性向下多级传递
  - foundation也可以放到state的属性中，参考Menu、select
    - [fix(text-field): put foundation on state and do render input unless foundation is present](https://github.com/material-components/material-components-web-react/pull/353)
    - Well the inner components of a component will be initialized first. 
    - In this case, text field initializes before it considers itself "mounted". 
    - So the innerComp's componentDidMount is called before text field's componentDidMount. relies on the foundation existing, which only happens after the text field's componentDidMount.
    - So by adding foundation to state, we can guarantee that the will always have a foundation.
    - foundation is moved to state so that Text Field's componentDidMount will trigger a re-render through setState after initializing the foundation

``` jsx
// 将复杂组件拆分成可组合的小组件
return (
  <div className={classes} {...otherProps}>
    {children}
  </div>
);
```

 

- ### rmwc
- https://github.com/jamesmfriedman/rmwc
  - Tag组件可通过tag属性设置html标签名或react组件，还可设置ref属性
  - createComponent方法会获取传入的组件，返回一个调用forwardRef生成的组件
    - 有部分额外代码只为生成类型声明，在runtime不存在，但会增加阅读代码时的复杂度
  - createMemoComponent会返回依次调用forwardRef和React.memo生成的组件
  - FoundationElement不是React组件，此方法不依赖外部
    - 代表一个dom元素，存放了该元素相关的属性、样式、事件、ref
    - 封装了组件通用操作方法，以及类似setState强制触发render的方法
    - 一个React的Component对应一个或多个FoundationElement
    - ?? 其构造函数的参数会接收调用了setState的函数作为实参，那其对象算得上是自定义hook吗
  - useFoundation自定义hook，作用主要是创建MDCFoundation实例
    - 会返回 `{foundation, ...elements}`
    - 参数对象包含的属性
      - `props:inputProps`
        - 某组件props对象的引用，除ref外完全相同
      - `elements:elementsInput`
        - 某组件内部包含的最外层元素或内部input元素ref名称的映射表集合
      - `foundation:foundationFactory`
        - 本方法的参数包含组件内部元素ref引用，还包含与元素交互方法的对象getProps、emit
        - adapter方法多是一行，直接操作元素ref的属性值或方法
      - `api`
        - 本方法会在useFoundation方法内被调用，在MDCFoundation对象创建或更新时执行
  - useCompFoundation是某个组件内部使用的总体大hook
    - 此hook函数的参数和组件参数props的类型完全相同，除了没有ref
    - 返回值一般包含具体组件dom元素对象的引用、setRef方法、组件其他子元素需要的方法
    - 元素引用一般有rootEl, compEl, inputEl
    - 还会返回api方法给组件函数使用
    - 函数组件中不涉及具体状态计算，简单处理useCompFoundation返回值中属性和props属性就写到子元素 `<element p1={} />` 上
  - ripple实现
    - mdc的ripple是以点击处为圆心向四周发散，ant-design的ripple是从元素边框向四周发散半透明
    - 内部结构包括withDomNode、Ripple、RippleSurface、withRipple
  - Button的实现
    - dom结构：Tag > ButtonRipple & ButtonIcon & span
  - Checkbox的实现
    - dom结构：CheckboxRoot > input & CheckboxBackground & CheckboxRipple
    - useCheckboxFoundation
      - 会传入adapter对象创建MDCCheckboxFoundation
      - 然后调用useFoundation获取返回值中的elements元素引用，再直接操作rootEl/checkboxEl
  - useToggleFoundation
    - 内部被Checkbox、Radio、Switch组件使用
    - id通过调用useId计算得到
    - 返回值 `return { id, renderToggle, toggleRootProps };`
 

- ### preact-material-components
- https://github.com/prateekbh/preact-material-components
  - `abstract class MaterialComponent extends React.Component`
    - 实例属性: MDComponent,mdcProps,mdcNotifyProps,classText,control,ripple
    - 实例方法: render返回VNode,react生命周期，setControlRef,buildClassName,materialDom
  - 实现简单组件如Button/Checkbox/Fab时，只需实现materialDom方法，预定义组件的dom结构
  - 在componentDidMount中创建MDC组件实例，并注册事件监听器
  - 在componentWillUnmount中移除监听器，再调用MDC组件实例的destroy方法
  - 使用此方法创建react组件的优缺点
    - 工作量较小，因为直接使用了MDC组件的class
    - react组件的api完全自己定义，受MDC组件api变化的影响较小
    - foundation/adapter的架构从长远看更适合与其他前端框架集成

 

- ### 使用material-design-web的示例项目
- https://github.com/lucka-me/mapler
  - Web app to make map as wallpaper
  - 入口组件下只有4个二级组件，个别组件实现代码较长
  - 多次手动调用 `this.comp.init(parentNode)` 来挂载组件到parentNode下
  - 子组件通过 `this.parent.append(Element)` 挂载
  - 封装了创建html元素的方法 `document.createElement(tag)` ，未拼接html结构字符串
- https://github.com/gamesminer/Spotty-Vanilla
  - music streaming service，依赖vanilla js和firebase
  - 顶层组件或二级组件手动调用mount方法，mount方法中会调用mountChildren来初始化子组件，而mountChildren方法中又会调用下层子组件的mount方法，会自动初始化整棵dom树
  - mount方法中会动态创建子组件内容 `this.mountPoint.innerHTML = 'domstring'`
  - 通过ejs-loader将import导入的.html模板文件转换成js函数，来创建对应的html字符串

``` JS
// Use the "interpolate" delimiter to create a compiled template.
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'
```

- https://github.com/enbock/Time-Tracker
  - 基于react，但使用的是纯js `import * as mdc from 'material-components-web';`
  - 在componentDidMount中创建MDCTopAppBar对象，并添加 `listen('MDCTopAppBar:nav',handleEvent)`
  - `new mdc.topAppBar.MDCTopAppBar(ReactDOM.findDOMNode(this))`
- https://github.com/abraham/slides-today
  - Slides.today is a site dedicated to the presentations
  - 依赖 angular
- https://github.com/Growthfilev2/admin_panel
  - Admin Panel For Growthfile
- https://github.com/srinathh/reactmdcweb
- https://github.com/chrisromito/action_tracker
- https://github.com/nadsadin/nuppi_shoping
- https://github.com/ableron/ableron
- https://github.com/Cuke7/material_template
- https://github.com/jersoncarranza/sabroso
- https://github.com/squirrel-labs/GameLobby
  - 手动创建MDCDrawer等组件，并添加监听器
  - 通过 `document.createElement('div')` 动态创建元素，然后再创建MDCSnackbar组件实例
- https://github.com/ThisNameWasTaken/disaster-ready  
- https://github.com/littleGabriel/music-chart
