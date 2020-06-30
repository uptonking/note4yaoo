---
tags: [blog, react]
title: page-blog-react-dev
created: '2020-06-29T08:43:56.344Z'
modified: '2020-06-30T07:17:58.437Z'
---

# page-blog-react-dev

## react hooks 开发实践总结

- hooks的使用体验就是简单，无生命周期，无this指向，逻辑复用也简单，无HOC或Render Props的繁琐
- ref
  - https://github.com/forthealllight/blog/issues/49

## react开发总结

- 自定义组件上的ref对象就是组件实例化之后的对象，包含props, context和state等属性。这种特性可以允许我们访问某个子组件的内部状态
- 如果props的数据不会改变，就不需要在state或者组件实例属性里拷贝一份
- 设置状态会触发组件重新渲染
  - 因此应该只将渲染方法要用到的值保存在状态中
  - 不要把没有参与渲染的数据放进state状态里
- 关于render函数里面的条件判断
  - 如果只是简单的条件判断，三目和与或运算符已经满足大多数人的需求；
  - 如果想让关注点分离，renderIf是个不错的注意；
  - 最后如果你希望你的判断逻辑能够被复用（就好像多个页面多个组件都需要用到判断登录状态和用户权限的逻辑），可以使用onlyIf构建项目内可复用的高阶组件。
  - 避免在JSX中写复杂的三元表达式，应通过封装函数或组件实现，如renderXxx
- 组件设计原则
  - 保持接口小，props数量要少
  - 根据数据边界来划分组件，充分利用组合
  - 把state往上层组件提取，让下层组件只需要实现为纯函数
- 组件划分
  - 一个复杂组件都是从简单组件开始的，一开始我们在render函数里写的代码不多，但是随着逻辑的复杂，JSX代码越来越多，于是就需要拆分函数中的内容
  - 有一个误区，就是把render中的代码分拆到多个 `renderXxx()` 函数中去
  - 因为这些 `renderXxx()` 函数访问的是同样的props和state，这样代码依然耦合在了一起。更好的方法，是把这些 `renderXXXX` 重构成各自独立的React组件

``` js
  class StopWatch extends React.Component {
    renderControlButtons() {
      //TODO: 返回两个按钮的JSX
    }
    render() {
      const majorClock = this.renderMajorClock();
      const controlButtons = this.renderControlButtons();
      const splitTimes = this.renderSplitTimes();

      return (
        <div>
          {majorClock}
          {controlButtons}
          {splitTimes}
       </div>
      );
    }
  }

  return (
    <div>
      <MajorClock>
      <ControlButtons>
      <SplitTimes>
    </div>
  );
```

- 尽量不要在JSX中写内联函数，比如 `<MyButton onClick={()=>{/*doSth*/}} >` ，每次渲染都会创建新函数
  - Every time the parent component renders, a new function is created and passed to the Child.
- Render props其实就是React用法中的“依赖注入”
  - 所谓依赖注入，指的是解决这样一个问题：逻辑A依赖于逻辑B，如果让A直接依赖于B，当然可行，但是A就没法做得通用了。
  - 依赖注入就是把B的逻辑以函数形式传递给A，A和B之间只需要对这个函数接口达成一致就行，如此一来，再来一个逻辑C，也可以用一样的方法重用逻辑A
- 当需要重用React组件的逻辑时，建议首先看这个功能是否可以抽象为一个简单的组件；如果行不通的话，考虑是否可以应用render props模式；再不行的话，才考虑应用高阶组件模式。
- Facebook在开发INS时遇到两个问题：
  - 数据绑定的时候，大量操作真实dom，性能成本太高
  - 网站的数据流向太混乱，不好控制

- 11 lessons learned as a React contractor
  - Multiple simple components are better than one highly customisable one
    - if a composable component is causing bugs, break it into more simple single use components, even if you’re repeating code
  - Always raise an Issue or Pull Request if you find bugs in libraries
  - If you’re implementing React in an existing project, migrate your build process to Browserify or Webpack first.
  - Raw SVG is better than D3 for simple data visualisation
  - When all you have is two weeks, keep it lean
  - Relying on CSS animation alone to move a lot of elements can be slow
    - Make sure you’re only rendering or re-rendering components that really need it.
    - That might mean, calculating what components are visible in the viewport and only rendering those.
    - Test on lower spec machines, but also test with extreme data to see how well things run when they’re pushed to the limit.
  - Only use boilerplates for what they’re good at — getting a project started quickly. 
    - Don’t be afraid to break them, twist them and generally misuse them to your will.
  - Maintain a predictable Components, connected Components and Container pattern
  - Strict linting is a blessing and a curse
  - Retrofitting Universal React rendering into an existing Express project is doable
    - how to just render a single React component into an existing multi-page Express app
    - ReactDOMServer
  - Learning Sagas may melt your brain
    - Make sure you have a deep understanding of Promises and Generators before you dive in

- ref
  - [React设计模式和最佳实践总结]([hlinkttps://](https://blog.poetries.top/2019/08/10/react-good-practice/))
  - [11 lessons react](https://hackernoon.com/11-lessons-learned-as-a-react-contractor-f515cd0491cf)

## react component vs element vs instance

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
