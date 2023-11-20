---
title: web-ui-comp4-navigation-menu
tags: [components, ui, web]
created: 2021-04-23T15:31:34.983Z
modified: 2021-07-28T20:11:14.714Z
---

# web-ui-comp4-navigation-menu

> 导航/菜单类组件

# guide

# discuss

- ## 

- ## 

- ## When tired of the basic sliders
- https://twitter.com/zhenyary/status/1726597979333890337
  - 动画效果，滑动时会切换书的封面

- ## how the hell do I code GUI state? Menus and submenus and different modes and cancelling actions.... 
- https://twitter.com/liz_love_lace/status/1690100806983233536
  - Surely no one actually models this stuff using finite state machines?
- Here’s how we do it in tldraw: https://github.com/tldraw/tldraw/blob/main/packages/tldraw/src/lib/ui/hooks/useMenuSchema.tsx
  - It’s essentially a big function that returns the state of the menu (there are others for context menu, help menu, etc).
- I do* It works really well *okay I use statecharts, which are like state machines with superpowers

# more
- [Building A Stepper Component](https://ishadeed.com/article/stepper-component-html-css/)
  - https://twitter.com/shadeed9/status/1432756615137173506
