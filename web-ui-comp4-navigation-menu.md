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

- ## 

- ## 

- ## for shadcn [Sidebar ](https://ui.shadcn.com/docs/components/sidebar) component, what's the different among sidebar, floating and inset variants ?
- sidebar: 普通模式，侧边栏固定全高，内容内容区可竖直滚动
  - This is the standard, classic sidebar look. It takes up the full height of the container (h-svh or h-full) and is rigidly attached to the side edge (left or right)
  - It typically has a simple border separating it from the main content.
  - Use Case: Best for traditional dashboard layouts where the navigation is a permanent, structural part of the page.

- inset(镶入物, 嵌入物, 插页): 侧边栏视觉上是底部背景，内容区是突出的大卡片, 高度不会超过可视区的卡片，与浏览器4边都有间隔，所以视觉上侧边栏比sidebar模式宽一点
  - This variant creates a specific "panel" or "app-like" layout where the sidebar usually shares a background with the outer container, and the main content area acts as a distinct "inset" panel.
  - You must wrap your main content in the `<SidebarInset>` component
  - Use Case: Ideal for complex web apps (like Notion or Linear) where the sidebar blends into the global background, and the page content is the focal "card."
  - suitable for layouts where the sidebar feels part of the page rather than separate.

- floating
  - a complete border around it (not just the side connecting to content).
  - Use Case: Great for modern, cleaner interfaces or when you want the navigation to feel less heavy and more like an overlaying element.

- ## for a simple tab component, Which would you choose and why?
- https://twitter.com/AdhamDannaway/status/1729884552896864453
  - C is a common tabs pattern, making it more easily understood (Jakob's Law).
  - A isn’t accessible to those with colour blindness, as it uses colour alone to show its selected.
  - B looks like a primary button, making it more prominent than it needs to be. This could break the visual hierarchy of a page.

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
