---
title: docs-ag-grid
tags: [ag-grid, docs, grid, list, table]
created: '2020-07-14T13:01:37.940Z'
modified: '2020-07-14T13:02:06.602Z'
---

# docs-ag-grid

## DOM Virtualisation

- https://www.ag-grid.com/javascript-grid-dom-virtualisation/

- The grid uses DOM virtualistaion to vastly improve rendering performance.
- If you loaded 1, 000 records with 20 columns into the browser without using a datagrid (eg using 'table', 'tr' and 'td' tags), then the page would end up with a lot of rendered DOM elements. 
  - This would drastically slow down the web page. 
  - This results in either a very poor user experience, or simply crashing the browser as the browser runs out of memory.
- To get around this, the grid only renders what you see on the screen. 
  - For example if you load 1, 000 records and 20 columns into the grid, 
  - but the user can only see 50 records and 10 columns (as the rest are not scrolled into view), 
  - then the grid only renders the 50 rows adn 10 columns that the user can actually see.
- As the user scrolls horizontally or vertically, 
  - the grid dynamically updates the DOM and renders the additional cells that are required while also removing the cells that are no longer in view.
- This technique of only rendering into the DOM what is in the visible scrollable viewport is known as row and column virtualisation.
- **Row virtualisation** is the insertion and removal of rows as the grid scrolls vertically.
  - By default the grid will render 10 rows before the first visible row and 10 rows after the last visible row, thus 20 additional rows get rendered. 
  - This is to act as a buffer as on some slower machines and browsers, a blank space can be seen as the user scrolls.
  - As a safety measure, the grid will render a maximum of 500 rows. 
    - This is to stop applications from crashing if they incorrectly set the grid size 
    - (ie if they don't size the grid correctly, and the grid tries to render 10,000 rows, this can crash the browser). 
    - To remove this restriction set the property `suppressMaxRenderedRowRestriction=true` .
- **Column virtualisation** is the insertion and removal of columns as the grid scrolls horizontally.
  - There is no column buffer - no additional columns are rendered apart from the visible set. 
  - This is because horizontal scrolling is not as CPU intensive as vertical scrolling, thus the buffer is not needed for a good UI experience.
  - To turn column virtualisation off set the grid property `suppressColumnVirtualisation=true` .
