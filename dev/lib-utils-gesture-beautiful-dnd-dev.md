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
# pragmatic-drag-and-drop
- [@atlaskit/pragmatic-drag-and-drop - npm](https://www.npmjs.com/package/@atlaskit/pragmatic-drag-and-drop)
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/pragmatic-drag-and-drop/core/
  - A performance optimized drag and drop framework

- Every drag and drop solution will make tradeoffs regarding feature sets, user experience, startup performance and runtime performance.

- goals
  - Speed: Best of class startup and runtime performance
  - Flexibility: Can be used to power any interaction
  - Accessibility*: Ensuring that all users have a good experience through alternative keyboard and screen reader

- features
  - leverages the browsers drag and drop capabilities
    - full feature support in Firefox, Safari and Chrome
    - Touch device compatible
  - Headless: full rendering and style control
  - Framework agnostic: works with any frontend framework
  - Virtualization support
  - Tiny: ~4.5kB base
  - Deferred compatible: consumers can delay the loading
  - Addons: patterns that allow sharing small pieces of functionality that can be added together
  - Accessible: achieved through alternative keyboard and screen reader flows. Unfortunately, the browsers drag and drop behaviour is not accessible (yet). But don't worry, we have a comprehensive guide and toolchain to help you be successful here
# dev

# more
