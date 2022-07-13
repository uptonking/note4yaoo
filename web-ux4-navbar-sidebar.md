---
title: web-ux4-navbar-sidebar
tags: [components, navbar, sidebar, ui]
created: '2021-03-22T19:03:11.916Z'
modified: '2021-07-29T20:37:50.995Z'
---

# web-ux4-navbar-sidebar

# tabs

- react-tabs的api结构
- Tabs
  - TabList
    - Tab 1
    - Tab 2
  - TabPanel 1
  - TabPanel 2

- hooks
  - Tabs顶层组件, useTabState, usePanelState
  - 将tabs状态都放在context里面，分 activeIndex 和 tabs/panels内容 两种状态
# navbar
- mobile
  - form elements表单元素会折叠或收起或收缩为图标

## tips

- 导航条的汉堡菜单在 左侧
  - github，spectrum，halfmoon
- 导航条的汉堡菜单在 右侧
  - bulma，bootstrap

- collapsible navbar
  - bootstrap导航菜单上的内容可折叠展开
    - 展开时会平滑地增加navbar的高度，仍是原位置，体验很好
  - halfmoon可通过下拉菜单dropdown收起部分内容，如登录按钮
    - 展开时通过小弹出菜单展示，场景更通用，体验还行

- ## eg-halfmoon

- navbar结构 display: flex
  - content: container for buttons, dropdowns...
  - brand: text/image
  - nav-link/item: active
  - text: muted color
  - form-inline: create forms inside navbar

- Navbars are made responsive by strategically showing/hiding different elements for different breakpoints using display utilities
  - .form-inline displayed only on screen lg+
- .ml-auto class will push that component and all the others that come after it, to the right.
- use flex utilities to justify the content inside
- You can create static navbars by simply placing the navbars inside the content wrapper (.content-wrapper). 
  - This way, they are not the immediate child of the page wrapper (.page-wrapper), so they will not stay fixed in one place.
  - 适合实现同一页面多个导航条，例子中底部导航条始终在页面最后，就像footer
- You can use any of the above containers inside navbars to align everything inside the navbar with the content of the page.
  - containers do not have margin or padding in Halfmoon. 
  - So this alignment is assuming that you are actually building the page using.content and .card inside the actual containers
  - this works best with static navbars, because if navbars are fixed in place and if the content scrolls, then the alignment is off on the right side due to the presence of the scrollbar inside the .content-wrapper
  - However, you can still use containers inside fixed navbars for the max-width property, which can be useful in certain situations.
# sidebar
- a.k.a.
  - side menu

- usecase
  - side menu

- should i use an alternative
  - dockable panel

- examples
  - https://getbootstrap.com/docs/5.0/examples/sidebars/

- 点击导航条的汉堡菜单，出现左侧sidebar
  - spectrum，halfmoon
- 点击导航条的汉堡菜单，不出现sidebar，额外内容显示在导航条下方
  - github，bulma，bootstrap

- sidebar作为放置目录TOC的容器
  - spectrum css docs的目录用的是多层嵌套列表 nav > ul > li > ul >li
  - bulma docs的目录用的是 div > ul > li
  - pico docs的目录用的是 details > ul >li
  - bootstrap docs的目录用的是 aside > nav > ul > li > ul > li
  - halfmoon docs的目录用的是 div > a

- ## eg-halfmoon

- sidebar结构
  - menu: main container
  - content: container for content like buttons...
  - brand: brand text/image
  - title: section titles
  - link: active
  - divider: div element as divider

- sidebar type
  - default: make space for the navbars on top
  - full height: take up the full height of the page
  - overlayed: float on top of the page
  - composite & responsive

- ## eg-bootstrap-offcanvas

- Offcanvas is a sidebar component that can be toggled via JavaScript to appear from the left, right, or bottom edge of the viewport.
  - Offcanvas shares some of the same JavaScript code as modals. 
    - Conceptually, they are quite similar, but they are separate plugins.
  - some source Sass variables for offcanvas’s styles and dimensions are inherited from the modal’s variables.
  - When shown, offcanvas includes a default backdrop(背景幕布；背景) that can be clicked to hide the offcanvas.
  - Similar to modals, only one offcanvas can be shown at a time.

- Scrolling the `<body>` element is disabled when an offcanvas and its backdrop are visible. 
  - Use the `data-bs-scroll` attribute to toggle `<body>` scrolling and `data-bs-backdrop` to toggle the backdrop.

- Since the offcanvas panel is conceptually a modal dialog, be sure to add aria-labelledby="..."—referencing the offcanvas title—to .offcanvas. 
  - Note that you don’t need to add `role="dialog"` since we already add it via JavaScript.
