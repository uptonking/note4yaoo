---
title: web-dev-ui-navbar-sidebar
tags: [components, navbar, sidebar, ui]
created: '2021-03-22T19:03:11.916Z'
modified: '2021-03-22T19:03:55.040Z'
---

# web-dev-ui-navbar-sidebar

# navbar

## tips

- 导航条的汉堡菜单在 左侧
  - github，spectrum，halfmoon
- 导航条的汉堡菜单在 右侧
  - bulma，bootstrap

- navbar结构 display: flex
  - brand: text/image
  - nav-link/item: active
  - text: muted color
  - content: container for buttons, dropdowns...
  - form-inline: create forms inside navbar

## halfmoon

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

- 点击导航条的汉堡菜单，出现左侧sidebar
  - spectrum，halfmoon
- 点击导航条的汉堡菜单，不出现sidebar，额外内容显示在导航条下方
  - github，bulma，bootstrap
