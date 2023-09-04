---
title: lib-utils-gesture-beautiful-dnd-dev
tags: [dnd, react-beautiful-dnd]
created: 2023-09-03T13:19:51.200Z
modified: 2023-09-03T13:20:58.188Z
---

# lib-utils-gesture-beautiful-dnd-dev

# guide

- pros
  - support combining draggables
  - accessible with keyboard/screen-reader

- cons
  - react-only
  - not support drag axis locking
  - dynamic add/remove items while dragging 功能有问题

- features
  - accessible with keyboard/screen-reader
  - performant
  - No creation of additional wrapper dom nodes - flexbox and focus management friendly
  - Movement between lists
  - Combining items
  - Multi drag support
  - Conditional dragging and conditional dropping
  - Plays well with nested interactive elements by default
  - Multiple independent lists on the one page
  - Flexible item sizes - the draggable items can have different height/width
  - Add and remove items during a drag
  - Tree support through the @atlaskit/tree package
  - Compatible with semantic `<table>` reordering - table pattern
# roadmap
- [Roadmap](https://github.com/hello-pangea/dnd/issues/419)
  - Remove redux connected api in favor of redux hooks
  - storybook examples with mui/antd/tailwind
  - support grid layout

- [CSS `will-change` attribute massively improve performance](https://github.com/atlassian/react-beautiful-dnd/issues/1892)
# changelog
- [v15.0.0_202204](https://github.com/hello-pangea/dnd/issues/293)
  - Support react v18
# dev

# more
