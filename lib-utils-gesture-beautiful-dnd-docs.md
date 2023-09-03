---
title: lib-utils-gesture-beautiful-dnd-docs
tags: [docs, react-beautiful-dnd]
created: 2023-09-03T15:30:55.367Z
modified: 2023-09-03T15:31:12.260Z
---

# lib-utils-gesture-beautiful-dnd-docs

# guide

# docs

## Overview

- Patterns
  - Virtual lists
  - Multi drag
  - Tables
  - Reparenting a `<Draggable />` - Using our cloning API or your own portal

- There are a lot of libraries out there that allow for drag and drop interactions within React. 
- Most notable of these is the amazing `react-dnd`. 
  - It does an incredible job at providing a great set of drag and drop primitives which work especially well with the wildly inconsistent html5 drag and drop feature. 
- `@hello-pangea/dnd` is a higher level abstraction specifically built for lists (vertical, horizontal, movement between lists, nested lists and so on). 
  - Within that subset of functionality @hello-pangea/dnd offers a powerful, natural and beautiful drag and drop experience. 
  - However, it does not provide the breadth of functionality offered by react-dnd. 
  - 🚨 **One shortcoming is that grid layouts are not supported** (yet). 

## [pattern: Reparenting a `<Draggable />` ](https://github.com/hello-pangea/dnd/blob/main/docs/guides/reparenting.md)

- 
- 
- 
- 
- 
- 
- 
- 
- 

## [pattern: Tables](https://github.com/hello-pangea/dnd/blob/main/docs/patterns/tables.md)

- why use table
  - Clean way of displaying tabular data
  - Can copy paste the table into other applications
  - Great browser support
  - Can reorder items in the table with rbd

- There are two strategies you can use when reordering tables.
- 👉🏻 Fixed layouts (faster and simpler)
  - In order to use this strategy the widths of your columns need to be fixed - that is, they will not change
  - This can be achieved with either a `table-layout: fixed` or `table-layout: auto` as long as you manually set the width of the cells (eg 50%).
  - The only thing you need to do is set `display: table` on a `<Draggable />` row while it is dragging.
  - approach of fixed layouts doesn't keep the styling once an element is being dragged. An alternative is to not set table-layout or display: table when `<Draggable />` is dragging, but rather just set the width of each `<td>` permanently. This avoids the need to use any event responders. E.g. in the `<Draggable />`, set each `<td>` to `width: 100px` with inline styling or css. 

- 👉🏻 Dimension locking (slower but more robust)
  - This strategy will work with columns that have automatic column widths based on content. It will also work with fixed layouts. 
  - It is **a more robust strategy than the first, but it is also less performant**.
  - When we apply `position: fixed` to the dragging item, it removes it from the automatic column width calculations that a table uses. 
  - So before a drag starts we **lock all of the cell widths using inline styles to prevent the column dimensions from changing when a drag starts**. 
  - You can achieve this with the `onBeforeDragStart` responder.
- This has poor performance characteristics at scale as it requires: 
  - Calling render() on every row 
  - Reading the DOM (window.getComputedStyles) on every row
  - For tables with less than 50 rows this should approach be fine!

- If you want to use reparenting (cloning or your own portal) in combination with table row reordering, then there are few extra steps you need to go through.

- First up, have a read of our reparenting pattern to get familiar with the approach.
- 
- 
- 
- 
- 
- 

## [pattern: Virtual lists](https://github.com/hello-pangea/dnd/blob/main/docs/patterns/virtual-lists.md)

- 
- 
- 
- 
- 
- 

## pattern: 

- 
- 
- 
- 
- 
- 

## [How we detect scroll containers](https://github.com/hello-pangea/dnd/blob/main/docs/guides/how-we-detect-scroll-containers.md)

- @hello-pangea/dnd will automatically detect the scroll containers for your application when a drag is starting. 
  - It does this by looking at the computed `overflowX` and `overflowY` values of an element.
  - If @hello-pangea/dnd finds an element that has a computed `overflowX` or `overflowY` set to `scroll` or `auto`, then that element is marked as a scroll container.

- If only one axis has `overflow-[x|y]: hidden` and the other is `visible` (the default value), then it will be computed as `auto`.
  - visible/clip computing to auto/hidden (respectively) if one of overflow-x or overflow-y is neither visible nor clip

- `document.body` (`<body>`) is different from `document.documentElement` (the `<html>` element). 
  - Any scroll on the `html` element is considered a `window` scroll. 
  - Most of the time any scroll bar that would have appeared on the `body` will be merged with the `html` scroll bar. 
  - However, there are situations where they can have different scrollable areas.

> We have not been able to find a reliable cross browser mechanism for detecting if a `body` has an independent scroll bar to the `html` element.

- There seems to also be an additional requirement that we have not been able to accurately quantify(量化) regarding the relationship of the sizes of the `html` and `body` elements.

- It looks like when the `html` element has some `width` and `height` related properties set then this can impact things. 
- However, finding a purely javascript solution for detecting this has alluded us so far

## [Auto scrolling](https://github.com/hello-pangea/dnd/blob/main/docs/guides/auto-scrolling.md)

- When a user drags a `<Draggable />` near the edge of a container, we automatically scroll the container as we are able to in order make room for the `<Draggable />`.
  - When the center of a `<Draggable />` gets within a small distance from the edge of a container, we start auto scrolling.
- The distances required for auto scrolling are based on a percentage of the height or width of the container for vertical and horizontal scrolling respectively. 
  - By using percentages rather than raw pixel values we are able to have a great experience regardless of the size and shape of your containers.

> If the `<Draggable />` is bigger than a container on the axis you are trying to scroll - we will not permit scrolling on that axis. 

- In order to move a `<Draggable />` into the correct position, we can do a combination of a `<Droppable />` scroll, window scroll and manual movements to ensure the `<Draggable />` ends up in the correct position in response to user movement instructions. 
  - This is amazing for users with visual impairments as they can correctly move items around in big lists without needing to use mouse positioning.

## [Preset styles](https://github.com/hello-pangea/dnd/blob/main/docs/guides/preset-styles.md)

- It is a goal of the library to provide unopinioned styling. 
  - However, we do apply some reasonable `cursor` styling on drag handles by default. 
  - This is designed to make the library work as simply as possible out of the box.

- In every phase
- Phase: resting
- Phase: dragging
- Phase: dropping
- Phase: user cancel

- All styles applied are vendor prefixed correctly to meet the requirements of our supported browser matrix. This is done by hand to avoid adding to @hello-pangea/dnd's size by including a css-in-js library

## [Drop animation](https://github.com/hello-pangea/dnd/blob/main/docs/guides/drop-animation.md)

- A drop animation is an important affordance to communicate placement. 
  - Our drop animations do not prevent the user from dragging something else while the animation is running.
  - If you do have use case where it makes sense to remove the drop animation, you will need to add a `transition-duration` property of _almost_ `0s`. This will skip the drop animation.
  - Do not make the `transition-duration` actually `0s`. It should be set at a near 0s value such as `0.001s`. 
  - The reason for this is that if you set `transition-duration` to `0s` then a `onTransitionEnd` event will not fire - and **we use that to know when the drop animation is finished**.
