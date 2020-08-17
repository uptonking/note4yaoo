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
  - this comes to a need having virtualization with row spans, now i can't use row span html attribute because my HoCs are divs and React naturally can't handle that nested DOM validation.

- ### column pin 
- [pr: useColumnPin](https://github.com/tannerlinsley/react-table/pull/1962)
  - This plugin is already implemented on v8

- ### virtualized
- [react-table supports infinite scrolling?](https://github.com/tannerlinsley/react-table/issues/1735)
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
- [Now we got header and filter virtualization too!(free for personal use) ](https://twitter.com/tannerlinsley/status/1258104396451213313)
  - Nested headers
  - Filter Row
  - 100, 000 rows x 20 cols
  - 100% flawless alignment
  - grid-area x/y Positioning (positioning without the all the css `position: absolute` crap)

- ### layout
- [pr: useGridLayout](https://github.com/tannerlinsley/react-table/pull/2525)

## issues

- [v7 Feedback & Ideas](https://github.com/tannerlinsley/react-table/issues/1252)

- [[v7] Table 100% width](https://github.com/tannerlinsley/react-table/issues/1639)
  - I use `useBlockLayout` and I don’t understand how to make the table stretch 100% of the width of the parent. In theory, the width of the columns should be adjusted as it was at V6
  - Out of the box, no, it does not behave like v6, since it is not using a flexbox model. 
  - useBlockLayout uses inline-block divs with precise widths. You can stretch the table container itself to take up the full width, but in a block or absolute layout, your columns will not grow automatically. 
  - The only way I know of to reliably do that is using the default html-table-element layout.
