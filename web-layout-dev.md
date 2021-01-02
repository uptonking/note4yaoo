---
title: web-layout-dev
tags: [layout, web]
created: '2020-07-25T10:01:27.897Z'
modified: '2021-01-01T20:17:05.116Z'
---

# web-layout-dev

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

- ### [Normal Flow Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout)
- Normal Flow, or Flow Layout, is the way that Block and Inline elements are displayed on a page before any changes are made to their layout. 
  - The flow is essentially a set of things that are all working together and know about each other in your layout. 
  - Once something is taken out of flow it works independently.
- In normal flow, inline elements display in the inline direction, that is in the direction words are displayed in a sentence according to the Writing Mode of the document. 
- Block elements display one after the other, as paragraphs do in the Writing Mode of that document. 
- In English therefore, inline elements display one after the other, starting on the left, and block elements start at the top and move down the page.

## discuss

 

- ### Flexbox vs CSS Grid? Which do you prefer?
- https://twitter.com/Tyler_Potts_/status/1344946469707554817
- They can be used together. It's not like you can only use one or the other. 
  - I like using Grid for bigger things or layouts and flex for smaller things or things inside the layouts.
  - Also, during the Chrome summit 2020 they talked about some cool existing things that are making flex box more powerful. 
  - Flexbox will have now something that grid has like gaping
- Personal opinion is mostly grid for layout and then use flexbox for inner small layout.
- Grid for 2 dimension, flex box for 1 dimension
- flexbox is for designing components, while grid is for page layout, or at least that’s what they were originally created for and that’s what I always used them for. 
  - So, to answer your question, I prefer both

- ### [flexbox vs css grid, Which one do you use more, and why?](https://twitter.com/eelisabethhv/status/1289594963152367616)
- flexbox: grid = 0.635: 0.365
- I love flexbox. almost use it for everything lol but yea, mostly navigation bar, mobile layout etc basically anything comes in a “strip” format.
  - Whereas grid I’d use it for larger page layout, ie web/desktop layout, eg blogs, or gallery with photos in different sizes
- Good thing is, you can use them both. 
  - I like grid to establish the overall page structure. 
    - You can do some cool responsive layouts without media queries. 
    - CSS grid: to create layout and grids
  - I use flex on the content elements.
    - Flexbox: to position the elements in the cells

## ref

- [CSS Flex vs Grid Tutorial](https://t.co/NPuEsH0BwT?amp=1)
