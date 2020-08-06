---
title: lib-react-window-dev
tags: [lib, list, react-window]
created: '2020-08-05T10:10:09.535Z'
modified: '2020-08-05T10:10:27.845Z'
---

# lib-react-window-dev

## issues

- ### [Adds range rendering](https://github.com/bvaughn/react-window/pull/218)
  - Getting rid of the range renderer prop felt like a nice change from react-virtualized to react-window. 
  - Re-adding it would add extra function calls to relatively hot code.

- ### [Feature Request: How can we handle rowspan and colspan](https://github.com/pupudu/window-table/issues/21)
- Unfortunately, there's no easy and trivial way to do that yet.

- ### [Why items are absolutely positioned?](https://github.com/bvaughn/react-window/issues/133)
- In both react-virtualized and react-window cells are absolutely positioned. Why?
- I have made react-virtualized work with statically positioned items, by inserting a "spacer" div before rows via `cellRangeRenderer` . 
  - That spacer div has margin-top set to the `style.top` of first rendered row.
  - When rows are positioned statically
    - There is no need to update top on each row element during scrolling, which makes React update faster.
    - Overlap issues are completely impossible, because rows naturally flow one after another. 
      - By saying overlap issues I mean issues when some row dynamically changes its height but Grid consumer don't call recomputeBodyGridSize to make Grid recalculate top offsets for each row so as a result upper row renders overlapping next row.
    - There is no need in storing top offsets for each row and maintaining style cache.

- My answer is going to be brief: It has to do with reflow and preserving the appearance of smooth scrolling when scrolling back up past items that have changed size since they were initially rendered.

- ### [Using html table element](https://github.com/bvaughn/react-window/issues/60)
  - [react-window using tr-td](https://codesandbox.io/s/rrn61wkzwm?file=/index.js)
- Idon't think table-tr-td will really work. 
- To my knowledge, `HTMLTableElement` doesn't really support overflow in the way a windowing component would need. 
- You could change the style to `display: block` but I still don't think it would quite work right
- Why do you need a table? I think you can achieve the same column layout with inline blocks or flex layouts

## Infinite lists and reflow

- [Infinite lists and reflow](https://gist.github.com/bvaughn/ded0061d712a30c22b0a591cec4aa576)

- In my experience, infinite lists use two basic layout strategies. 
  - The first uses absolute positioning to control where visible items are rendered. 
  - The second uses relative positioning (with top/left padding to offset for unrendered items).
- In both cases, the list abstraction caches some metadata about the size of items once they have been rendered– so that it knows where to position the items that come after them.
- Both of these strategies need to handle reflow. 
  - For example, changing the width of a list often affects the height of its items. 
  - Generally speaking, only the "window" of rendered (visible) items are remeasured in this case (because it would be too slow to rerender and remeasure all of the items before). 
  - But once a user scrolls backwards (up/left) – the list needs to account for the reflowed sizes. 
  - If it didn't, items would appear to jump up or down (depending on the delta between the previous, cached sizes and the new/reflowed sizes).
- How the list deals with new sizes depends on which of the two layout strategies it uses.
- In the first case (absolute positioning), the list can make small adjustments to the scroll offset to account for the size differences. 
  - Since each adjustment typically only takes a small number of items into account, it's not too noticeable. 
  - Eventually if a user scrolls all the way back to the first item in the list, it will align with scroll offset 0. 
  - Unfortunately in some browsers, adjusting scroll offset will interrupt momentum scrolling– resulting in a very jerky scrolling experience.
- The second strategy (relative positing) does not need to adjust scroll offset, and so it does not have the problem of interrupting momentum scrolling. 
  - It uses a similar technique but adjusts the top/left padding to preserve the appearance of smooth scrolling. 
  - The downside of this approach is that item 0 may not line up with scroll offset 0. 
  - In the event that item size decreases, the list can handle this by doing a final adjustment to set padding to 0 when the first item is scrolled back into view. 
  - (This would cause the scrolling to jump a little but it's not that bad of a user experience.) 
  - However in the event that item size increases, the list will run out of padding (since padding cannot go negative) and scroll offset 0 will be reached when there are still more items to render. (This is a very bad user experience.)
