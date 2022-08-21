---
title: lib-excel-tanstack-table-api
tags: [api, tanstack-table]
created: 2020-07-15T13:40:45.982Z
modified: 2022-08-21T10:19:58.755Z
---

# lib-excel-tanstack-table-api

# guide

- ref
  - [useTable](https://react-table.tanstack.com/docs/api/useTable)

# useTable

# useBlockLayout

- `useBlockLayout` is a plugin hook that adds support for headers and cells to be rendered as `inline-block` divs (or other non-table elements) with explicit width. 

# useAbsoluteLayout

- `useAbsoluteLayout` is a plugin hook that adds support for headers and cells to be rendered as absolutely positioned divs (or other non-table elements) with explicit width. 

# useFlexLayout

- `useFlexLayout` is a plugin hook that adds support for headers and cells to be rendered as inline-block divs (or other non-table elements) with width being used as the flex-basis and flex-grow. 
- This hook becomes useful when implementing both virtualized and resizable tables that must also be able to stretch to fill all available space.
