---
title: note-web-layout-catalog
tags: [layout, web]
created: '2020-07-25T10:01:27.897Z'
modified: '2020-07-25T10:02:25.426Z'
---

# note-web-layout-catalog

## faq
- [CSS Grid布局那么好，为什么至今没有人开发出基于Grid布局的前端框架呢？](https://www.zhihu.com/question/397861009/answers/updated)
  - css其实本身就是高度封装的东东了，可能有安卓iOS原生写样式，远远不像css这么好
  - 现在前端css相关的库卖点是design，而不是用的技术，企业关注的不是前端是不是用了grid

## guide

- angular/flex-layout /MIT/5kStar/202007
  - https://github.com/angular/flex-layout
  - https://tburleson-layouts-demos.firebaseapp.com
    - These Layout demos are curated from the AngularJS Material documentation, GitHub Issues, StackOverflow, and CodePen.
    - demos: static, grids, responsive, github, StackOverflow
  - The Angular Layout features provide smart, syntactic directives to allow developers to easily and intuitively create responsive and adaptive layouts using Flexbox and CSS Grid.
  - [Static/Declarative API](https://github.com/angular/flex-layout/wiki/Declarative-API-Overview)
    - The API outline here is considered static and provides a UX that will adjust element sizes and positions as the browser window width changes.
    - The static API can be considered the default desktop layout API.
    - Developers should use the Responsive API to support alternate layout configurations for mobile or tablet devices
  - [Responsive API](https://github.com/angular/flex-layout/wiki/Responsive-API)
    - Google's specifications provide guidance that includes a flexible grid that ensures consistency across layouts, breakpoint details about how content reflows on different screens, and a description of how an app can scale from small to extra-large screens.

## CSS Normal Flow Layout

- [Normal Flow Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout)

- Normal Flow, or Flow Layout, is the way that Block and Inline elements are displayed on a page before any changes are made to their layout. 
  - The flow is essentially a set of things that are all working together and know about each other in your layout. 
  - Once something is taken out of flow it works independently.
- In normal flow, inline elements display in the inline direction, that is in the direction words are displayed in a sentence according to the Writing Mode of the document. 
- Block elements display one after the other, as paragraphs do in the Writing Mode of that document. 
- In English therefore, inline elements display one after the other, starting on the left, and block elements start at the top and move down the page.
