---
title: lib-react-table-dev
tags: [lib, list, react-table]
created: '2020-07-13T02:29:20.525Z'
modified: '2020-07-14T10:27:12.335Z'
---

# lib-react-table-dev

## guide

## pieces

- You can't virtualize `<table>` elements. You'll need to use divs and one of the flex/absolute/block layout plugins from `react-table`
- To really achieve what you're talking about requires 2 virtualizers placed at differing layers. 
  - 1 vertical virtualizer for the rows, and another horizontal virtualizer for the entire table. 
  - This can get quite complex, and there are tons of edge cases, like handling header groupings in separate virtualizers, always showings scrollbars (which is extremely difficult). 
  - All reasons that I am building **React Table Pro** (working title) that will do all of this automatically.
  - https://github.com/tannerlinsley/react-virtual/issues/10
