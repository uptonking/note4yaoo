---
title: lib-excel-tanstack-table-docs
tags: [changelog, docs, list, tanstack-table]
created: 2020-07-13T02:29:20.525Z
modified: 2022-08-21T10:19:58.757Z
---

# lib-excel-tanstack-table-docs
- Hooks for building lightweight, fast and extendable datagrids for React
- A Table Utility, not a Table Component
# guide
- Try rewriting your plugin (v8 doesn't have a plugin system any more) as a functional wrapper that uses TanStack Table internally.
# overview
- Features
  - Lightweight (small size and tree-shaking)
  - Headless (100% customizable, Bring-your-own-UI)
  - Auto out of the box, fully controllable API
  - Sorting (Multi and Stable)
  - Filters(global/column)
  - Aggregation/Pivoting
  - Pagination
  - Row grouping
  - Row Selection
  - Row Expansion
  - Sub row componnets
  - Column Ordering
  - column resizable
  - column hiding
  - header nested/grouped
  - custom cell formatter
  - footer
  - Animatable
  - Virtualizable
  - Server-side/controlled data/state
  - Extensible via hook-based plugin system
  - Table, Flex, and Grid Helpers

- React Table v7 refactors the entire library to a hooks-only UI/Style/Markup agnostic table building utility.
- This latest version is a collection of React hooks and plugins (which are also hooks!) that help you flexibly compose logical features of the most complex data grids into a single API returned by the primary `useTable` hook. 
- This API is performant, extensible, and unopinionated about markup, styles or rendering.
- By acting as an ultra-smart table utility, React Table opens up the possibility for your tables to integrate into any existing theme, UI library or existing table markup. 
  - This also means that if you don't have an existing table component or table styles, React Table will help you learn to build the table markup and styles required to display great tables.
# Concepts
- React Table v7 is a headless utility, 
  - which means out of the box, it doesn't render or supply any actual UI elements.
  - You are in charge of utilizing the state and callbacks of the hooks provided by this library to render your own table markup.
- Separation of Concerns 
  - React Table as a library honestly has no business being in charge of your UI. 
  - The look, feel, and overall experience of your table is what makes your app or product great. 
  - The less React Table gets in the way of that, the better!
- Maintenance  
  - By removing the massive (and seemingly endless) API surface area required to support every UI use-case, 
  - React Table can remain small, easy-to-use and simple to update/maintain.
- Extensibility  
  - UI presents countless edge cases for a library simply because it's a creative medium, and one where every developer does things differently. 
  - By not dictating UI concerns, React Table empowers the developer to design and extend the UI based on their unique use-case.
- At the heart of every React Table is the `useTable` hook and the table `instance` object that it returns. 
- This `instance` object contains everything you'll ever need to build a table and interact with its state. 
- This includes, but is not limited to:
  - Columns
  - Materialized Data
  - Sorting
  - Filtering
  - Grouping
  - Pagination
  - Expanded State
  - Any functionality provided by custom plugin hooks, too!
# API 
- The primary React Table hook
  - [ `useTable` ](https://react-table.tanstack.com/docs/api/useTable)
- Plugin Hooks
  - Core Plugin Hooks
    - [ `useSortBy` ](./useSortBy.md)
    - [ `useFilters` ](./useFilters.md)
    - [ `useGlobalFilter` ](./useGlobalFilter.md)
    - [ `useGroupBy` ](./useGroupBy.md)
    - [ `useExpanded` ](./useExpanded.md)
    - [ `usePagination` ](./usePagination.md)
    - [ `useTokenPagination` (Coming Soon)](./useTokenPagination.md)
    - [ `useRowSelect` ](./useRowSelect.md)
    - [ `useRowState` ](./useRowState.md)
    - [ `useColumnOrder` ](./useColumnOrder.md)
    - [ `useResizeColumns` ](./useResizeColumns.md)
  - Layout Hooks
    - [ `useBlockLayout` ](./useBlockLayout.md)
    - [ `useAbsoluteLayout` ](./useAbsoluteLayout.md)
    - [ `useFlexLayout` ](./useFlexLayout.md)
- 3rd Party Plugin Hooks

- `useTable` is the primary hook used to build a React Table. 
  - It serves as the starting point for every option and every plugin hook that React Table supports. 
  - The options passed into `useTable` are supplied to every plugin hook after it in the order they are supplied, eventually resulting in a final `instance` object that you can use to build your table UI and interact with the table's state.

```JS
const instance = useTable({
    data: [...],
    columns: [...],
  },
  useGroupBy,
  useFilters,
  useSortBy,
  useExpanded,
  usePagination
)
```

- The stages of React Table and plugins
  - `useTable` is called. A table `instance` is created.
  - The `instance.state` is resolved from either a custom user state or an automatically generated one.
  - A collection of plugin points is created at `instance.hooks` .
  - Each plugin is given the opportunity to add hooks to `instance.hook` .
  - As the `useTable` logic proceeds to run, each plugin hook type is used at a specific point in time with each individual hook function being executed the order it was registered.
  - The final instance object is returned from `useTable` , which the developer then uses to construct their table.
- This multi-stage process is the secret sauce that allows React Table plugin hooks to work together and compose nicely, while not stepping on each others toes.
- In the event that you want to programmatically enable or disable plugin hooks, most of them provide options to disable their functionality, eg. `options.disableSortBy`
- React Table relies on memoization to determine when state and side effects should update or be calculated. 
  - This means that every option you pass to useTable should be memoized either via `React.useMemo` (for objects) or `React.useCallback` (for functions).
# changelog
- ref
  - https://github.com/tannerlinsley/react-table/blob/master/CHANGELOG.md
  - https://github.com/tannerlinsley/react-table/releases/tag/v7.0.0

- 7.2.0-20200609
  - add initialRows property on instance 
- 7.1.0-20200515
  - useFilters: add filterTypes: includesSome & includesValue
- 7.0.0-20200311
  - Massive changes to the entire project and library
