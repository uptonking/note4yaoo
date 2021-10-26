---
title: web-ui-comp2-foundation
tags: [components, ui, web]
created: '2021-04-23T15:22:22.358Z'
modified: '2021-07-28T20:10:46.188Z'
---

# web-ui-comp2-foundation

> 不直接提供ui视图的组件

# guide

# discuss

- ## 

- ## Working on an official drag-to-reorder API for @framer Motion 5.
- https://twitter.com/mattgperry/status/1435179287338962944
- For the first version, it will:
  - Handle single axis lists
  - Work with variable-size items
  - Auto-apply zIndex to the dragged item
- Playing around with it, I decided to drop Trigger in favour of letting people wire this up themselves with useDragControls
  - More flexible without adding much complexity, and will be smaller in filesize without the extra components/context.
- Will virtualization of long lists be supported?
  - Not initially, it'll depend on demand
- Would this work with react-three-fiber or DOM only?
  - DOM only
