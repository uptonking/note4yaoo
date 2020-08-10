---
title: lib-react-virtualized-dev
tags: [lib, list, react-virtualized]
created: '2020-08-05T09:34:25.307Z'
modified: '2020-08-05T09:35:05.094Z'
---

# lib-react-virtualized-dev

## react-virtualized的ui结构层次

- list
  - grid/GridReactVirtualized__List
    - Grid__innerScrollContainer
      - row
      - row
      - row

## guide 

- [How does windowing work?](https://bvaughn.github.io/forward-js-2017/#/12/3)

## issues

- [FlexTable - rowspan would be a nice to have feature](https://github.com/bvaughn/react-virtualized/issues/245)
  - I don't think the FlexTable interface has a meaningful way to accommodate a rowSpan attribute. 
  - With HTML tables, rowSpan and colSpan are specified on a `<td>` , but with react-virtualized, cell-rendering is managed by FlexTable itself in order to simplify the flexbox display properties. (That's actually the primary function of FlexTable - you could just use VirtualScroll if you want to manage the flexbox properties manually.)
  - Api aside, there are some additional complexities:
    - Since FlexTable is flexbox based, actually implementing rowSpan would be a little tricky. We'd have to render empty column(s) in the later row(s)- so that flex sizing for that "row" would not get screwy- and position the spanned column so that it extended over top of the lower columns.
    - react-virtualized windows rows and columns (for performance purposes) but in the case of row/col span this opens some complicated edge-cases. If a given row or column could extend past its normal grid boundaries, then the logic for determining which rows/columns to display for a given scroll position becomes significantly more complicated. (For example, if row 2 had a rowSpan of 10, I'd have to know to render it too even if the user had scrolled down to row 10.)

- [Grid: colspan, rowspan support](https://github.com/bvaughn/react-virtualized/issues/123)
  - This isn't going to be implemented.
  - I've considered it before and it would add a lot of complication. 
  - If you'd like to control this level of cell-sizing, you should create your own high-order component wrapper around VirtualScroll.
  - `cellRangeRenderer` is the solution I used and it works well. Just adjust the columnStartIndex to make sure it captures the first 'real' column.

- [Tag independent rendering for Table](https://github.com/bvaughn/react-virtualized/issues/817)
  - For some complex data structures, nested headers are a good way to give your data structure hierarchy. 
  - In my use case we intent to implement a nested header structure using `<table>` markup like this
  - It's a bit hacky, but I believe you can accomplish the layout (or a similar one) to what you're describing using the existing `headerRowRenderer` prop 

## Rendering large lists with React Virtualized

- [Rendering large lists with React Virtualized_201805](https://blog.logrocket.com/rendering-large-lists-with-react-virtualized-82741907a6b3/)
  - [Rendering Lists Using React Virtualized](https://css-tricks.com/rendering-lists-using-react-virtualized/)

- So many elements in the DOM can cause two problems:
  - Slow initial rendering
  - Laggy scrolling
- However, if you scroll through the list, you may not notice any lagging. After all, the app isn’t rendering something complex.
- If you’re using Chrome, follow these steps to do a quick test:
  - Open the Developer tools panel.
  - Press Command+Shift+P (Mac) or Control+Shift+P (Windows, Linux) to open the Command Menu.
  - Start typing Rendering in the Command Menu and select Show Rendering.
  - In the Rendering tab, enable FPS Meter.
  - Scroll through the list one more time.
  - In my case, the frames went from 60 to around 38 frames per second

- ### How does react-virtualized work?
  - The main concept behind virtual rendering is rendering only what is visible.
  - There are one thousand comment items in the app, but it only shows around ten at any moment (the ones that fit on the screen), until you scroll to show more.
  - So it makes sense to load only the elements that are visible and unload them when they are not by replacing them with new ones.
  - React-virtualized **implements virtual rendering** with a set of components that basically work in the following way:

    - They calculate which items are visible inside the area where the list is displayed (the viewport).
    - They use a container (div) with relative positioning to absolute position the children elements inside of it by controlling its top, left, width and height style properties.

- There are five main components:
  - Grid. 

    - It renders tabular data along the vertical and horizontal axes.

  - List. 

    - It renders a list of elements using a Grid component internally.

  - Table. 

    - It renders a table with a fixed header and vertically scrollable body content. 
    - It also uses a Grid component internally.

  - Masonry. 

    - It renders dynamically-sized, user-positioned cells with vertical scrolling support.

  - Collection. 

    - It renders arbitrarily positioned and overlapping data.

- On the other hand, react-virtualized also includes some HOC components:
  - ArrowKeyStepper. 

    - It decorates another component so it can respond to arrow-key events.

  - AutoSizer. 

    - It automatically adjusts the width and height of another component.

  - CellMeasurer. 

    - It automatically measures a cell’s contents by temporarily rendering it in a way that is not visible to the user.

  - ColumnSizer. 

    - It calculates column-widths for Grid cells.

  - InfiniteLoader. 

    - It manages the fetching of data as a user scrolls a List, Table, or Grid.

  - MultiGrid. 

    - It decorates a Grid component to add fixed columns and/or rows.

  - ScrollSync.

    - It synchronizes scrolling between two or more components.

  - WindowScroller. 

    - It enables a Table or List component to be scrolled based on the window’s scroll positions.

- If we look at the elements of the page in the developer tools tab, you’ll see that now the rows are placed inside two additional div elements
- **react-virtualized的ui结构层次**
- list
  - grid/GridReactVirtualized__List
    - Grid__innerScrollContainer
      - row
      - row
      - row
- The outer div element (the one with the CSS class `GridReactVirtualized__List` ) has the width and height specified in the component (800px and 600px, respectively), has a `relative` position and the value `auto` for `overflow` (to add scrollbars).
- The inner div element (the one with the CSS class `Grid__innerScrollContainer` ) has a max-width of 800px but a `height` of `50000px` , the result of multiplying the number of rows (1000) by the height of each row (50). 
  - It also has a `relative` position but a `hidden` value for `overflow` .
  - All the rows are children of this div element, and this time, there are not one thousand elements.
  - However, there are not eight or nine elements either. There’s like ten more.
  - That’s because the List component renders additional elements to reduce the chance of flickering due to fast scrolling.
  - The number of additional elements is controlled with the property `overscanRowCount` .
- The downside is that you have to specify the `width` and `height` of the list as well as the `height` of the row.
  - Luckily, you can use the `AutoSizer` and `CellMeasurer` components to solve this.
- The `AutoSizer` component will fill all of the available space of its parent so if you want to fill all the space after the header, in src/App.css, you can add the following line to the list class:

``` CSS
.list {
  height: calc(100vh - 210px)
}
```

- The `vh` unit corresponds to the height to the viewport (the browser window size), so `100vh` is equivalent to `100%` of the height of the viewport. 
  - 210px are subtracted because of the size of the header (200px) and the padding that the list class adds (10px).
  - If you resize the window, the list height should adjust automatically
- Calculating the height of a row automatically
  - If you want to have dynamic height, you have to use the `CellMeasurer` component.
