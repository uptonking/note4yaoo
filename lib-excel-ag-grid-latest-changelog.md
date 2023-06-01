---
title: lib-excel-ag-grid-latest-changelog
tags: [ag-grid, changelog]
created: 2020-08-31T13:21:59.547Z
modified: 2022-08-21T09:55:17.539Z
---

# lib-excel-ag-grid-latest-changelog

# guide

- [ag-Grid Changelog](https://www.ag-grid.com/ag-grid-changelog/)

- What's Next for React UI
  - In AG Grid v26.2 has a production ready version of React UI, by setting the grid property reactUi=true.
  - In AG Grid v27 we plan to make this the default with a fallback property to keep the old rendering. 
  - In AG Grid v28 we plan to remove the old way of React rendering.
# changelog

## v27

- [Regarding removal of Immutable data mode](https://github.com/ag-grid/ag-grid/issues/5139)
  - Immutable data is now just working by default, all you have to do is set the getRowId, and all should work as before

## v24.0.0-20200909

- rowDeselection is now true by default and should be suppressed by using suppressRowDeselection
- Allow more combining multiple column filters on one column (see Multi Filter)
- Reactive Columns - Enhancements to Column Definitions
  - Revamped Updating Column Definitions to make it easier to make changes to columns. 
  - Revamped Column State to allow more powerful and fine grained control of Column State without touching the Column Definitions. 
-  Allow aggregation without totalling on pivot column groups
- Add API methods indicating whether the undo/redo stack is empty
- Chart Themes Customization

- 23.0.0
  - a major rewrite of the Sass code behind our provided themes
  - Migrate ag-grid-angular/@ag-grid-community/angular to use CLI for build

## v22.0.0

- introduce ag-grid modules to reduce bundle size
- Columns toolpanel - Allow preventing dragging columns from the columns tool panel into the grid
- SetFilter: Remove selectAllOnMiniFilter and have it as default behaviour

- 21.0.0
  - Cell Range API Changes
- 20.0.0
  - SASS Themes revamp
  - Improve horizontal and vertical scrolling in other browsers
- 19.0.0
  - Remove theme-material (deprecated)
  - Improvements to Printing Functionality
  - Allow delta changes to columns
- 18.0.0
  - Events - Make event param mandatory
