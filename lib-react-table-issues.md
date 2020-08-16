---
title: lib-react-table-issues
tags: [issues, react-table]
created: '2020-07-15T13:08:35.143Z'
modified: '2020-07-15T13:10:31.179Z'
---

# lib-react-table-issues

## not-yet

- [add item after sortBy](https://github.com/tannerlinsley/react-table/issues/2641)
- [Cannot sort by Date](https://github.com/tannerlinsley/react-table/issues/2613)

- [the ID passed to the filter function is not an string](https://github.com/tannerlinsley/react-table/issues/2644)

- [useRowSelect relies on external state](https://github.com/tannerlinsley/react-table/issues/2171)
  - a workaround is to
    - avoid useRowSelect, or
    - use it in controlled state mode (so, avoiding selection state update logic), or
    - use selectedRowIds directly, ignoring helper methods and isSelected attribute.
      - It is an annoyance, but at least you can use all other parts of react-table normally.

- [useResizeColumns does not clean up eventlistener for touch events properly.](https://github.com/tannerlinsley/react-table/issues/2622)
- [resizing does not follow the mouse](https://github.com/tannerlinsley/react-table/issues/2185)

- [v8: useCellRangeSelection](https://github.com/tannerlinsley/react-table/issues/2476)

- [no horizontal scrollbar showing up when resizing columns to be wider than the available table width](https://github.com/tannerlinsley/react-table/issues/2630)

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

- ### layout
- [pr: useGridLayout](https://github.com/tannerlinsley/react-table/pull/2525)

## issues

- [v7 Feedback & Ideas ](https://github.com/tannerlinsley/react-table/issues/1252)

- `useGetLatest(instanceRef.current)` how it's helping avoiding memory leaks 
  - `const getInstance = useGetLatest(instanceRef.current);`
  - Instead of using `instanceRef.current` all over the place, you just use `getInstance()` which just looks better imo less clutter(n, 杂乱，混乱)
    - as for memory leaks, it’s not the getLatest implementation that does this. It’s just the fact that it’s used at all as opposed to creating closures around `instanceRef.current`
  - Converted almost all usages of `instanceRef.current` to use `useGetLatest(instanceRef.current)` to help with avoiding memory leaks and to be more terse.
    - It avoids closing over stale instance properties and holding on to them in memory. 
    - Only when they are needed, they are accessed on demand though the getter.
    - Could you please expand on why calling a function avoids closing over state instance properties?
    - I'm definitely not an expert, but I know that previously when we would simply close over the instance we were "snapshotting" the entire instances in a closure, and as long as that closure stuck around, that memory for the instance snapshot would be there.
    - Some of that doesn't matter if you are actually reusing or mutating a single instance, but if you are handling computed or immutable data that is changing, then you can potentially be hanging on to a lot of unused data for no reason.
    - By just storing a reference to a getter function, you aren't closing over the data, just the getter. 
    - Thus, the memory of the result of that getter doesn't come into play until you use it, which in the case of all of the callbacks and API used in something like React Table is alot
  - ref
    - https://twitter.com/tannerlinsley/status/1257068142242656256
    - https://spectrum.chat/react-table/general/v7-can-some-one-explain-usegetlatest-instanceref-current~54763a00-66ae-4211-bb35-52ca25686546

- [[v7] Table 100% width](https://github.com/tannerlinsley/react-table/issues/1639)
  - I use useBlockLayout and I don’t understand how to make the table stretch 100% of the width of the parent. In theory, the width of the columns should be adjusted as it was at V6
  - Out of the box, no, it does not behave like v6, since it is not using a flexbox model. 
  - useBlockLayout uses inline-block divs with precise widths. You can stretch the table container itself to take up the full width, but in a block or absolute layout, your columns will not grow automatically. 
  - The only way I know of to reliably do that is using the default html-table-element layout.
