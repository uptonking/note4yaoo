---
title: lib-ui-bootstrap-react-dev
tags: [bootstrap, lib, react-bootstrap, ui]
created: '2020-12-25T12:09:41.310Z'
modified: '2021-04-14T17:36:17.442Z'
---

# lib-ui-bootstrap-react-dev

# guide

- features
  - Rebuilt with React
    - Each component has been built from scratch as a true React component
  - Bootstrap at its core
    - By relying entirely on the Bootstrap stylesheet, React-Bootstrap just works with the thousands of Bootstrap themes you already love.
  - Accessible by default
    - Each component is implemented with accessibility in mind

- react-bootstrap vs reactstrap
  - 差别很小，可以考虑更新频率是否支持bootstrap.v5，对自定义className的支持，对第三方主题的支持
  - react-bootstrap(ts+hooks)依赖较多，但模块化解耦程度更高
  - reactstrap(js+class/hooks)部分复杂组件如Modal/Tab还未迁移到hooks
  - reactstrap的样式使用了cssModules
  - Both work in the same way, from the perspective of use
  - You can view both implementations, comparing a basic component as Button in the packages source code
    - Despite some differences such as the approach with the use of `prototype` that `reactstrap` implements, and specifically in this component, the handling of some additional props, in general, there are no significant differences between them.
  - ref
    - [Using Bootstrap in ReactJS: reactstrap or react-bootstrap?_202106](https://dev.to/cassiolacerda/using-bootstrap-in-reactjs-reactstrap-or-react-bootstrap-gng)
    - [Why would you prefer ReactStrap over React Bootstrap or vice versa?__201906](https://twitter.com/_ooade/status/1143141483069005824)
# codebase
- 组件的基本结构
  - 根组件大多为Component，也有很多为Tag
  - 很多组件使用模版高阶函数createWithBsPrefix()创建
    - 模板返回的react元素类似`<Tag ref={ref} className={classnamesX} {...props}>`

- 组件的常用属性
  - ref
  - className会用classnames计算拼接，className最终值中各字符串顺序不重要，最终样式由具体class样式规则的声明顺序决定
  - onClick
  - {...restProps}，注意书写顺序，后面的props会覆盖前面的props
    - 常放在最后，可以覆盖前面组件内设置的属性默认值
    - 要将不支持覆盖的属性名放在{...restProps}后面
    - Remember, the attribute on the right will override the attribute on the left. 

- 常用的hook
  - useEventCallback
# Overview
- [Why React-Bootstrap?](https://react-bootstrap.github.io/getting-started/why-react-bootstrap/)
  - 总结
    - no jquery
    - no imperative dom update
    - easier styling, easier state management not from dom
  - React-Bootstrap is a complete re-implementation of the Bootstrap components using React. 
    - It has no dependency on either bootstrap.js or jQuery.
  - Methods and events using jQuery is done imperatively by directly manipulating the DOM. 
  - In contrast, React uses updates to the state to update the virtual DOM. 
    - In this way, React-Bootstrap provides a more reliable solution by incorporating Bootstrap functionality into React's virtual DOM.
  - The CSS and details of Bootstrap components are rather opinionated and lengthy. 
    - React-Bootstrap simplifies this by condensing(使浓缩；使冷凝) the original Bootstrap into React-styled components.
  - Since React-Bootstrap is built with React Javascript, state can be passed within React-Bootstrap components as a prop. 
    - It also makes it easier to manage the state as updates are made using React’s state instead of directly manipulating the state of the DOM. 

- You should import individual components like: `react-bootstrap/Button` rather than the entire library. 
  - Doing so pulls in only the specific components that you use, 
  - which can significantly reduce the amount of code you end up sending to the client.

- Because React-Bootstrap doesn't depend on a very precise version of Bootstrap, **we don't ship with any included CSS**. 
  - However, some stylesheet **is required** to use these components.
  - `import 'bootstrap/dist/css/bootstrap.min.css'; `
- React-Bootstrap is compatible with existing Bootstrap themes. 
  - Just follow the installation instructions for your theme of choice.
  - Because React-Bootstrap completely reimplements Bootstrap's JavaScript, it's not automatically compatible with themes that extend the default JavaScript behaviors.
- Theming
  - If you stick to the Bootstrap defined classes and variants, there isn't anything you need to do to use a custom theme with React-Bootstrap. 
    - It just works. 
  - But we also make coloring outside the lines easy to do.
    - React bootstrap builds the component classNames in a consistent way that you can rely on
    - You can control how a Component prefixes its classes locally by changing the bsPrefix prop
    - Or globally via the `ThemeProvider` Component.

- React Bootstrap v1 adds full compatibility with Bootstrap 4. 
  - Because bootstrap 4 is a major rewrite of the project, there are significant breaking changes from the pre v1 react-bootstrap.
  - Bootstrap 3 support will continue in react-bootstrap versions < v1.0.0
  - Bootstrap 4 support will be in react-bootstrap versions >= v1.0.0
  - React-Bootstrap only contains components that are present in vanilla Bootstrap. 
    - If functionality was removed from Bootstrap, then it was also removed from React-Bootstrap. 
# pieces

# [changelog of react-bootstrap](https://github.com/react-bootstrap/react-bootstrap/blob/master/CHANGELOG.md)

- v2.0.0-alpha.0__202103
  - RTL support
  - add Offcanvas component
  - components update

- v1.4.0__202010
  - carousel: re-implement with committed ref
