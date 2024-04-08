---
title: lib-excel-handsontable-docs
tags: [changelog, docs, list, table]
created: 2019-08-01T16:03:46.386Z
modified: 2022-08-21T09:57:36.123Z
---

# lib-excel-handsontable-docs

# guide

# overview
- rowHeights/colWidths能够设置各行/各列的高度/宽度的默认值，也是最小值
- stretchH能使表格充满容器宽度，且各列水平均分

- handsontable大小尺寸
  - Handsontable by default fills its nearest parent element which has a defined `width/height` and the CSS `overflow` property set to `hidden` .
    - Having that, you can expand your Handsontable to the window’s dimension and use the native scrollbars to navigate through the grid.
  - If you provide height only and decide to leave the width indefinite, then the spreadsheet will expand to the window’s full width (or any parent element with defined dimensions and `overflow: hidden` )
  - If you set only the table’s width, it won’t render properly until you use the `preventOverflow` option. 
    - By setting it to horizontal your spreadsheet will have the width of a parent container and the height of the window. 
    - Scrollbars will appear if needed. 
    - Basically, the `preventOverflow` option prevents the table from overflowing the parent container in the provided dimension, in this case – horizontal.
    - If there are no height and width settings passed in the configuration, the table will vertically and horizontally fill the entire window (again, or any parent element with defined dimensions and `overflow: hidden` ).
    - you can change the size dynamically any time after the initialization by using the `updateSettings` code to update the dimensions.
  - ref
    - [A Complete Guide to Changing the Size of Handsontable](https://handsontable.com/blog/articles/2016/3/a-complete-guide-to-changing-size-of-handsontable)

- To set up Handsontable DOM structure in your application, you have to define its container as a starting point to initialize component.
  - Usually, the `div` element becomes this container. 
  - This container should **have defined dimensions** as well as the rest of your layout. 
  - If container is a block element, then its parent has to have defined height. By default block element is 0px height, so 100% from 0px is still 0px.
  - Since v7.0.0, Handsontable supports relative units such as %, rem, em, vh, vw or as exact size in px.
- Handsontable looks for the closest element with `overflow: auto` or `overflow: hidden` to use it as a scrollable container. 
  - If no such element is found， a window will be used.
- If you don't define dimensions, Handsontable will generate as many rows and columns to fill available space and will also provide full support for virtual rendering and fixed parts.
- Since v7.0.0 we observe window resizing. 
  - If the window's dimensions have changed, then we check if Handsontable should resize itself too. 
  - Due to the performance issue, we use debounce method to response on window resize.
- ref
  - [Grid sizing](https://handsontable.com/docs/7.4.2/tutorial-grid-sizing.html)

- **Walkontable** is the return value of many methods but not mentioned in the docs
  - Walkontable is for internal use only. 
  - It used to be a separate library, but now it is included to HOT repository and it's core functionality is to render HTML table.
  - Walkontable table renderer was refactored on 20190705.
    - This change introduces new files and code structures, which makes table rendering easier to maintain. 
    - In this approach, every TABLE element which can hold children is rendered separately by an individual unit called internally `OrderView` . 
    - A specialized renderer wraps each unit.
    - This change helps us to implement an EcoRendering idea

- What is eco-rendering
  - This issue is about implementing a new feature internally called as `EcoRenderers` . 
  - The idea of this is to increasing Handsontable performance by re-rendering cells only when their value has changed. 
  - I assume that after implementing this feature issues related to scroll performance or refresh table lag after cell edit should recede
  - ref
    - https://github.com/handsontable/handsontable/issues/5769
    - https://github.com/handsontable/handsontable/pull/6089

- Currently the best way to style Handsontable is to use custom renderers.
- Links/click events from custom renderers not working 
# docs
- Handsontable binds to your data source (list of arrays or list of objects) by reference. 
  - Therefore, all the data entered in the grid will alter the original data source. 
  - In complex applications, you may want to change the data source from outside Handsontable. 
  - A change being made will not be presented on the screen unless you refresh the grid on the screen using the `render` method.
- it is suggested to clone the data source before loading it into Handsontable. 
  - This can be done with `JSON.parse(JSON.stringify(data))` or another deep-cloning function.

- Handsontable separates the process of displaying the cell value from the process of changing the value. 
- Renderers are responsible for presenting the data and Editors for altering it. 
  - As a renderer has only one simple task: get actual value of the cell and return its representation as a HTML code they can be a single function. 
- Editors, however, need to handle user input (that is, mouse and keyboard events), validate data and behave according to validation results, so putting all those functionalities into a single function wouldn't be a good idea. 
  - That's why Handsontable editors are represented by editor classes.

- 
- 
- 
- 

# Known limitations
- It uses several dependencies
  - Our team follows the "proudly found elsewhere" principle which encourages us to make use of the great work done by other developers. 
  - numbro.js (handles numeric data)
  - Pikaday (displays a date picker)
  - moment.js (parses, validates and displays dates)
  - json-patch-duplex.js (implementation of JSON-Patch - RFC 6902)
  - jStat (statistical library)
  - tiny-emitter (a tiny event emitter library)
- [github-issues-most-commented](https://github.com/handsontable/handsontable/issues?q=is%3Aissue+is%3Aopen+sort%3Acomments-desc)
  - [cell is focusing, when focus in another input (modal)](https://github.com/handsontable/handsontable/issues/401)
  - [Issues with scrolling in a parent element](https://github.com/handsontable/handsontable/issues/3119)
  - [Fixing more columns than visible in the viewport breaks scrolling](https://github.com/handsontable/handsontable/issues/4259)
  - [Rewrite custom borders to use SVGs instead of DIVs](https://github.com/handsontable/handsontable/issues/6467)
# more
