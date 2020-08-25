---
title: docs-ag-grid-style-layout
tags: [ag-grid, docs, layout, style]
created: '2020-08-24T09:18:14.273Z'
modified: '2020-08-24T09:19:54.911Z'
---

# docs-ag-grid-style-layout

## Grid Size

- Under normal usage, your application should set the `width` and `height` of the grid using CSS styles. 
  - The grid will then fit the width you provide and use scrolling inside the grid to allowing viewing all rows and columns.
  - If using `%` for your height, then make sure the container you are putting the grid into also has height specified, as the browser will fit the div according to a percentage of the parents height, and if the parent has no height, then this `%` will always be zero.
  - If your grid is not the size you think , it should be then put a border on the grid's div and see if that's the size you want (the grid will fill this div). 
  - If it is not the size you want, then you have a CSS layout issue in your application.
- If the width and / or height change after the grid is initialized, the grid will automatically resize to fill the new area.

- Depending on your scenario, you may wish for the grid to auto-size its height to the number of rows displayed inside the grid. 
  - This is useful if you have relatively few rows and don't want empty space between the last row and the bottom of the grid.
  - To allow the grid to auto-size, it's height to fit rows, set grid property `domLayout='autoHeight'` .
- When `domLayout='autoHeight'` , then your application should not set height on the grid `div` , as the div should be allowed flow naturally to fit the grid contents. 
  - When auto height is off, then your application should set height on the grid div, as the grid will fill the div you provide it.
- Don't use Grid Auto Height when displaying large numbers of rows.
  - If using Grid Auto Height, then the grid will render all rows into the DOM. 
  - This is different to normal operation where the grid will only render rows that are visible inside the grid's scrollable viewport. 
  - For large grids (eg >1, 000 rows) the draw time of the grid will be slow, or for very large grids, your application can freeze. 
  - This is not a problem with the grid, it is a limitation on browsers on how much data they can easily display on one web page. 
  - For this reason, if showing large amounts of data, it is not adviseable to use Grid Auto Height. 
  - Instead use the grid as normal and the grid's row virtualisation will take care of this problem for you.

- There are three DOM Layout values the grid can have
  - normal
    - This is the default if nothing is specified. 
    - The grid fits the width and height of the div you provide and scrolls in both directions.
  - autoHeight
    - The grid's height is set to fit the number of rows, so no vertical scrollbar is provided by the grid. 
    - The grid scrolls horizontally as normal.
  - print
    - No scroll bars are used and the grid renders all rows and columns. 

- There is a minimum height of 50px for displaying the rows for autoheight. 
  - This is for aesthetic purposes, in particular to allow room to show the 'no rows' message when no rows are in the grid otherwise this message would be overlaying on top of the header which does not look well.
  - It is not possible to specify a max height when using auto-height.
  - If using auto-height, the grid is set up to work in a different way. It is not possible to switch. If you do need to switch, you will need to turn auto-height off.

## Styling Rows

- style object inline
- row className
- If you refresh a row, or a cell is updated due to editing, the rowStyle, rowClass and rowClassRules are all applied again. 

## Styling Cells

- style object inline
- cell className
- If you refresh a cell, or a cell is updated due to editing, the cellStyle, cellClass and cellClassRules are all applied again. 

## Themes

- The grid is styled using CSS, and a theme is a set of CSS rules styling the grid. 
- The grid comes bundled with Provided Themes, or you can create your own.

- With the release of ag-Grid version 23, we have undertaken a major rewrite of the Sass code behind our provided themes, with the goal of making it easier to write custom themes.
  - Themes are now configured using parameters
    - We have moved from global variables to passing configuration to themes as a map of key/value parameters
    - The major advantage of this approach is that we are now able to warn when you pass a parameter that is not supported
  - Renamed variables
  - Renamed CSS classes
  - Variables removed with no equivalent parameter
    - We have removed variables where it is trivial to achieve the same effect using a CSS selector. 
    - Instead of using a parameter, create a CSS rule to apply your desired effect. 
  - Deleted placeholder selectors

## Printing

- Keep Print Layout for Print Only
  - When the grid is in print layout, it will be rendering all cells without using row virtualisation. 
  - This means that the grid will be slower given the amount of DOM it is rendering. 
  - Only use print layout when you actually want to print. 
  - All of the functions (filtering, sorting, dragging columns etc) will work, however the performance will be impacted if the data set is large and will frustrate your users. 
  - For this reason it's best keeping print layout for printing only and normal (or auto-height) layout at all other times.

- A grid using print layout will not use any scrollbars so all rows and columns will get printed. 
- The grid will auto-size width and height to fit all contents. 
- This means if the grid is printed on paper, all the cells will get included, as apposed to printing a grid with scrollbars and only cells within the visible area will get printed.

- The only Row Model that print layout works with is the default Client Side row model. 
  - It will not work with the others ( Infinite, Server-Side or Viewport). 
  - This is because the grid will render the entire data-set which goes against the philosophy of the other row models which lazy load data.

- Don't Print Large Data
  - This is not a problem with the grid, it is a limitation on browsers on how much data they can easily display in one web page. 
  - If you try to render lots of data into the web page, the web page will create lots of DOM elements and will either slow things down or simply hang the browser. 
  - ag-Grid gets around this problem by virtualising the rows and columns. 
  - However if you render the whole grid, there is no possibility of virtualising the rows or columns.
  - If you want to allow printing large datasets, it's best to get your users to export to CSV or Excel and then print from another non-web based application.
