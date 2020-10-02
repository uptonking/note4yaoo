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
    - dom结构、样式、行为

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
