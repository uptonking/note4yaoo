---
title: docs-ag-grid-extensions
tags: [ag-grid, docs]
created: '2020-08-25T13:52:05.478Z'
modified: '2020-08-25T13:53:39.494Z'
---

# docs-ag-grid-extensions

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
  - When the table is first initialized, the loading panel is displayed if rowData is set to `null` or `undefined`. 
  - When the api function `setRowData` is called, the loading panel is hidden.

