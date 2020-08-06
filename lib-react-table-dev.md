---
title: lib-react-table-dev
tags: [lib, list, react-table]
created: '2020-07-13T02:29:20.525Z'
modified: '2020-07-14T10:27:12.335Z'
---

# lib-react-table-dev

## guide

- ### [table vs div](https://twitter.com/tannerlinsley/status/1254534413741780992)
- `<table>` Table
  - Auto col width
  - Native aria/structure
  - Native col/row span
  - No infinite scroll
  - No sticky/pinned cols
- `<div>` Table
  - Manual col width
  - Resizable cols
  - Simulated col/row span
  - Infinite Scroll
  - Sticky cols
- ref
  - [twitter survey](https://twitter.com/tannerlinsley/status/1254534413741780992)
  - [aria grid pattern](https://www.w3.org/TR/wai-aria-practices/#grid)
  - today has left me with a pretty solid plan that anything that is missing from `<table>` grids can *almost* be replicated fully in a `<div>` grid, plus all the other great possibilities you gain by not locking yourself into the `<table>` spec.
    - What interesting is that *most* things that native tables have over div tables can be ported to div tables including a11y, col/rowSpan, etc.
    - Auto col-width though is problematic. There's just not a good solution that I've seen to do that.
  - I chose table over div.  
    - The no sticky columns thing can be solved, and flawlessly-smooth infinite scroll is low on my list.
    - The biggest issue for me is the incessant tinkering with column widths when using a div, especially when headers, footers, and grouping is involved.
    - How did you solve sticky cols?
    - Two tables side by side.  One fixed and one scrolling.
  - The most important one IMO to cross-port to divs properly is the auto width or at the very least, flex-fill for when tables are wide and columns can fill the extra space
    - not an easy one. We did that in the past in a custom table implementation (2-pass render) but I was never proud of it. 
    - I like the flex-fill approach though. I think having something pragmatic enough will be ok. It's not that auto-width is required for any table out there.
  - You can get auto column width with div tables :). We do this at my work. We do a two-pass render to measure and it's fast enough most of the time. Working on an implementation with CSS Grid that I'll write about soon.
    - [not ssr friendly yet](https://ministrycentered.github.io/ui-kit/datatable)

  - 

## pieces

- [react-virtual usage with react-table?](https://github.com/tannerlinsley/react-virtual/issues/10)
- You can't virtualize `<table>` elements. You'll need to use divs and one of the flex/absolute/block layout plugins from `react-table`
- To really achieve what you're talking about requires 2 virtualizers placed at differing layers. 
  - 1 vertical virtualizer for the rows, and another horizontal virtualizer for the entire table. 
  - This can get quite complex, and there are tons of edge cases, like handling header groupings in separate virtualizers, always showings scrollbars (which is extremely difficult). 
  - All reasons that I am building **React Table Pro** (working title) that will do all of this automatically.
