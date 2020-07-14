---
title: note-pm-list-grid-blog
tags: [blog, grid, list]
created: '2020-07-14T13:04:22.299Z'
modified: '2020-07-14T13:06:56.027Z'
---

# note-pm-list-grid-blog

## Comparison: Why ag-Grid is the best when it comes to Column Pinnin

- ref
  - [Comparison: Why ag-Grid is the best when it comes to Column Pinning](https://blog.ag-grid.com/javascript-grid-comparison-column-pinning-ag-grid/)
  - [Here's why column pinning by ag-Grid wins over competition](https://blog.ag-grid.com/heres-why-column-pinning-in-react-datagrid-by-ag-grid-wins-over-competition/)

- Column pinning is a standard feature of all datagrids. 
  - Sometimes it’s also referred to as column fixing or column freezing. 
  - This feature is useful in cases when a javascript datagrid contains many columns that cause horizontal scrolling. 
  - With column pinning you can fix a column on the left or on the right side of the grid to prevent it getting out of user view when scrolling horizontally.
- In effect, this feature splits a datagrid into two separate parts: the “frozen” one and the “scrollable” one. 
  - The “frozen” part of the datatable will be fixed, while the scrollable part will remain movable.
- Functionality overview
  - pinning a column on both left and right sides
  - pinning a column from a column menu
  - pinning a column by dragging
  - pinning an initial column dynamically
  - pinning subsequent columns dynamically
- Pinning on both sides effectively splits a grid into 3 parts with the horizontal scroll only available for the middle “non-freezed” part. 
- ag-Grid doesn’t force you to indicate an initial pinned column or the specify the number of pinned columns in the configuration. 
  - This can all be done after the grid is initialized
  - All other React datagrids either require at least one pinned column all the time or limit you by specifying the number of pinned columns in advance.

## list-blog-collection

- [Testing with Jest & Enzyme - querying JSDOM vs ag-Grid API](https://blog.ag-grid.com/testing-ag-grid-react-jest-enzyme/)
  - jsdom: test user behavior
  - ag-grid api: compatible with dom virtualisation, test implementation
