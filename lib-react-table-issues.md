---
title: lib-react-table-issues
tags: [issues, react-table]
created: '2020-07-15T13:08:35.143Z'
modified: '2020-07-15T13:10:31.179Z'
---

# lib-react-table-issues

## not-yet

- resizing does not follow the mouse
  - https://github.com/tannerlinsley/react-table/issues/2185

## features

- ### row span /WIP
- [cell-level rowspan/colspan](https://github.com/tannerlinsley/react-table/issues/1933)
- [How to use rowSpan](https://github.com/tannerlinsley/react-table/discussions/2233)
- [pr: Add useRowSpan plugin](https://github.com/tannerlinsley/react-table/pull/2534)
  -  this comes to a need having virtualization with row spans, now i can't use row span html attribute because my HoCs are divs and React naturally can't handle that nested DOM validation.

- ### virtualized
- [react-table supports infinite scrolling? ](https://github.com/tannerlinsley/react-table/issues/1735)
    - When implementing virtual scrolling, you cannot use traditional table elements because:
      - To virtualize, you must nest a few divs and create a scrollable overflow container, which you cannot do with table elements
      - This would produce non-semantic HTML (which produces errors in React)
      - Table elements do not behave normally in an absolutely positioned environment
    - FWIW, you can implement virtual scrolling with traditional table elements. 
      - The trick is to set the height of the top and bottom `<tr>` tags (e.g., `<tr style="height: 2536px;">` ).
      - Change the heights of them both whenever you scroll far enough to swap rows in/out.
- [react-virtual usage with react-table?](https://github.com/tannerlinsley/react-virtual/issues/10)
  - You can't virtualize `<table>` elements. You'll need to use divs and one of the flex/absolute/block layout plugins from `react-table`
  - To really achieve what you're talking about requires 2 virtualizers placed at differing layers. 
  - 1 vertical virtualizer for the rows, and another horizontal virtualizer for the entire table. 
  - This can get quite complex, and there are tons of edge cases, like handling header groupings in separate virtualizers, always showings scrollbars (which is extremely difficult). 
  - All reasons that I am building **React Table Pro** (working title) that will do all of this automatically.

## issues

- [v7 Feedback & Ideas ](https://github.com/tannerlinsley/react-table/issues/1252)

- [[v7] can some one explain useGetLatest(instanceRef.current)](https://spectrum.chat/react-table/general/v7-can-some-one-explain-usegetlatest-instanceref-current~54763a00-66ae-4211-bb35-52ca25686546)
  - `const getInstance = useGetLatest(instanceRef.current);`
  - Instead of using `instanceRef.current` all over the place, you just use `getInstance()` which just looks better imo less clutter(n,杂乱，混乱)
  - as for memory leaks, it’s not the getLatest implementation that does this. It’s just the fact that it’s used at all as opposed to creating closures around `instanceRef.current`
