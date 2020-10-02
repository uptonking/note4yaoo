---
title: note-components-design-pattern
tags: [components, pattern]
created: '2020-10-02T11:42:34.698Z'
modified: '2020-10-02T11:44:11.404Z'
---

# note-components-design-pattern

## latest

- 组件库研发方向及特色
  - [跨框架开发ui组件库(stencil)](https://zhuanlan.zhihu.com/p/41974042)
    - 开发者用起来framework-agnostic，但原作者很可能要维护多个port或bridge
  - headless ui
    - 只适合简单组件，复杂组件如table实现功能时很可能与layout密切相关
    - opinionated: ui交互或技术选型具有明显的偏向性
  - ui组件
    - dom结构(非视觉结构)、样式、行为
    - foundation + adapter

## opinionated

- ui设计
  - portal的target容器默认是组件自身或document.body
  - should we show a indeterminate for the header's checkbox if partial is selected
  - Inline Editing is a very common feature in a table, but it's highly coupled with specific ui libraries, so it won't be a part of BaseTable itself.
- 交互设计
  - should we select all the children if the parent is selected
  - how to sync the staled keys if those rows are removed
- 技术选型
  - all in js

## back-garden-design-in-action

- logo: green plum
- design-system-tokens
  - text: sans serif(衬线体多用于印刷)
  - color: mineral-ui-color-palette, primary-mediumseagreen
  - bezel-less
- interaction
  - hover-color
  - click-ripple
  - loader-flower
- animation
  - flip
  - misc
    - rotate
    - unfold
    - point movement
- shape
  - point/polygon-shape-based
  - https://medium.com/google-design/you-need-a-shape-system-8d2aa9016817
- 公共api
  - variant
    - borderless
      - 部分组件提供无边框的版本，如modal
      - 也可考虑实现成dark mode的形式

## material design

### guide

- [MDC-112 Web: Integrating MDC with Web Frameworks](https://codelabs.developers.google.com/codelabs/mdc-112-web/)
- ref
  - [rmwc: Foundation Adapter Implementation](https://github.com/jamesmfriedman/rmwc/issues/141)

### material-design-components-web

- Material Components for the web (MDC Web) are framework-agnostic, built using regular JavaScript. This helps make MDC Web work seamlessly with your development process. 
- MDC Web uses a CSS preprocessor called Sass.
- The MDC Select component wraps a native HTML `<select>` element.
- You've replaced some common components (text fields, select, and button) without doing a complete redesign of your app. 

- MDC Web is engineered to integrate into any front end framework while upholding the principles of Material Design. 
  - The following codelab guides you through building a React Component, which uses MDC Web as a foundation. 
  - The principles learned in this codelab can be applied to any JavaScript framework.
- MDC Web's JavaScript layer is comprised of three classes per component: the Component, Foundation, and Adapter. 
  - This pattern gives MDC Web the flexibility to integrate with frontend frameworks.
  - Foundation contains the business logic that implements Material Design. 
    - The Foundation does not reference any HTML elements. 
    - This lets us abstract HTML interaction logic into the Adapter. 
    - Foundation has an Adapter.
  - Adapter is an interface. 
    - The Adapter interface is referenced by the Foundation to implement Material Design business logic. 
    - You can implement the Adapter in different frameworks such as Angular or React. 
    - An implementation of an Adapter interacts with the DOM structure.
  - Component has a Foundation, and its role is to
    - Implement the Adapter, using non-framework JavaScript, and
    - Provide public methods that proxy to methods in the Foundation.
- Every package in MDC Web comes with a Component, Foundation, and Adapter. 
  - To instantiate a Component, you must pass the root element to the Component's constructor method. 
  - The Component implements an Adapter, which interacts with the DOM and HTML elements. 
  - The Component then instantiates the Foundation, which calls the Adapter methods.
- To integrate MDC Web into a framework, you need to create your own Component in that framework's language/syntax. 
  - The framework Component implements MDC Web's Adapter and uses MDC Web's Foundation.
- This codelab demonstrates how to build a custom Adapter to use the Foundation logic to achieve a Material Design React Component
- In React, the `render` method outputs the Component's HTML. 
- The approach
  - Implement the `Adapter` methods.
  - Initialize the `Foundation` in the `componentDidMount` .
  - Call the `Foundation.destroy` method in the `componentWillUnmount` .
  - Establish variant management via a getter method that combines appropriate class names.
- The non-framework JS `TopAppBar` Component implements the following Adapter methods
  - hasClass()/addClass()/setStyle()/getTopAppBarHeight()/...
  - notifyNavigationIconClicked()/registerScrollHandler()/...
- Because React has synthetic events and different best coding practices and patterns, the Adapter methods need to be reimplemented.
- React doesn't have an API to manage classes. 
  - To mimic native JavaScript's add/remove CSS class methods, add the `classList` state variable.
- Foundation instantiation happens in the componentDidMount method.
  - because the Foundation needs a DOM element.
- This tutorial highlights our decision to split MDC Web code into 3 parts, the Foundation, Adapter, and Component. 
  - This architecture allows components to share common code while working with all frameworks. 
