---
title: docs-ag-grid-react
tags: [ag-grid, docs]
created: '2020-08-24T09:15:06.175Z'
modified: '2020-08-24T09:15:23.767Z'
---

# docs-ag-grid-react

## Get Started with ag-Grid and React

- AgGridReact
  - rowData
  - columnDefs
- Enable Sorting And Filtering
  - headerName, field, sortable, filter
- Fetch Remote Data
  - `componentDidMount()` or `useEffect`
- Enable Selection
  - headerName, field, checkboxSelection
  - rowSelection="multiple"
- Grouping
  - headerName, field, rowGroup
- ag-grid 18~21 -- react 15.x
- ag-grid 22.x  -- react 16.3+

- Columns can be defined in three ways: 
  - declaratively (i.e. via `<AgGridColumn>` markup), 
  - via `GridOptions` with `columnDefs` as prop
  - or by binding to `columnDefs` on the `AgGridReact` component.
