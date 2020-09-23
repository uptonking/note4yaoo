---
title: docs-ag-grid-features-extensions
tags: [ag-grid, docs]
created: '2020-08-25T13:52:05.478Z'
modified: '2020-09-23T05:47:02.075Z'
---

# docs-ag-grid-features-extensions

## features

- [Features Overview](https://www.ag-grid.com/javascript-grid-features/)
- [Community and Enterprise Feature Comparison](https://www.ag-grid.com/javascript-grid-set-license/)

### Enterprise Only

- Filtering
  - Set Filter
  - Multi Filter
- Grouping
  - Row Grouping
  - Aggregation
  - Pivoting
  - Tree Data
  - Master/Detail
- Range Selection
  - Range Handle
  - Fill Handle
- I/O
  - Export Excel
  - Clipboard
- Accessories/Extensions
  - Tool Panel
    - Side Bar
    - Columns Tool Panel
    - Filters Tool Panel
  - Column Menu
  - Context Menu
  - Status Bar
- Charts
  - Range Chart
  - Pivot Chart
  - Chart Toolbar

### Community Features

- Row
  - Row Sorting
  - Row Selection
  - Row Spanning
  - Row Pinning
  - Row Height
  - Full Width Rows
    - 不推荐使用本功能，推荐使用最新的Master/Detail
  - Row Animation
  - Row Dragging
    - External DropZone
    - Grid to Grid

- Column
  - Column Filter
  - Custom Filter
  - Column Pinning
  - Column Groups
  - Column Moving
  - Column Resizing

- Filtering
  - Column Filters
    - Simple Column Filters: Text,Number,Date
    - Floating Filters
    - Custom Filter
  - External Filter
  - Quick Filter

- Rendering
  - Cell Content
  - Cell Rendering
  - View Refresh
  - Flashing Cells
  - Change Detection

- Editing
  - Cell Editing
  - Provided Editors
  - Undo/Redo Edits

- Scrolling
  - Row Pagination
  - Aligned Grids
  - DOM Virtualisation
  - Scrolling Performance

- Accessibility
  - Keyboard Navigation
  - Touch Support
  - Localization
  - RTL

- Charts
  - Pie/Line/Bar/Histogram/Area/Scatter
  - layout/axes/legend/theme/tooltip

### Styling

- Styling Rows/Cells
- Theming
- Grid Size
- Custom Icons
- Animation
- Cell Rendering
- Cell Styling
- Column Headers
- Column Spanning
- Overlays

### Working with Data

- Row Models
  - ClientSideRowModel
  - InfiniteRowModel
- Accessing Data
- Change Detection
- Expressions
- Reference Data
- Setters and Parsers
- Value Getters & Value Formatters
- Updating Data
  - Single Row/Cell
  - Transactions
  - High Frequency
- Value Cache
- Value Handlers
- View Refresh
- Context
- Immutable Data
- I/O
  - Drag & Drop
  - export csv
  - Printing

## Tool Panels - Side Bar

- Tool Panels are panels that sit in the Side Bar to the right of the grid. 
- The Side Bar allows access to the tool panels via buttons that work like tabs. 

## Tool Panels - Columns Panel

## Tool Panels - Filters Panel

## Context Menu

## Column Menu

## Status Bar

## Overlays

- At present, there are two overlays for the grid:
  - Loading: Gets displayed when the grid is loading data.
  - No Rows: Gets displayed when loading has complete but no rows to show.
- The grid manages showing and hiding of the overlays for you, so you may not ever need to call the above API methods. 
  - When the table is first initialized, the loading panel is displayed if rowData is set to `null` or `undefined` . 
  - When the api function `setRowData` is called, the loading panel is hidden.
