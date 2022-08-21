---
title: lib-excel-ag-grid-docs-styling-layout
tags: [ag-grid, docs, layout, styling]
created: 2020-08-24T09:18:14.273Z
modified: 2022-08-21T09:55:04.928Z
---

# lib-excel-ag-grid-docs-styling-layout

# pieces

- How Flashing Works
  - Each time the call value is changed, the grid adds the CSS class `ag-cell-data-changed` for 500ms by default, and then then CSS class `ag-cell-data-changed-animation` for 1, 000ms by default. 
  - The grid provided themes use this to apply a background color.

# Grid Size

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

# Styling Rows

- style object inline
- row className
- If you refresh a row, or a cell is updated due to editing, the rowStyle, rowClass and rowClassRules are all applied again. 

# Styling Cells

- style object inline
- cell className
- If you refresh a cell, or a cell is updated due to editing, the cellStyle, cellClass and cellClassRules are all applied again. 

# Themes

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

# Overlays

- At present, there are two overlays for the grid:
  - Loading: Gets displayed when the grid is loading data.
  - No Rows: Gets displayed when loading has complete but no rows to show.
- provide your own overlay templates with the grid properties `overlayLoadingTemplate` and `overlayNoRowsTemplate` . 
  - These templates should be plain HTML
