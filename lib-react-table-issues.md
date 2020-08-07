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
