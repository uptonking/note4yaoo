---
title: lib-list-ag-grid-docs-rendering-customization
tags: [ag-grid, docs]
created: 2020-08-26T11:00:16.149Z
modified: 2021-05-13T02:43:04.944Z
---

# lib-list-ag-grid-docs-rendering-customization

# Components

- You can create your own custom components to customize the behavior of the grid. 
- The full list of component types you can provide in ag-Grid are as follows:
  - Cell Renderer: To customizes the contents of a cell.
  - Cell Editor: To customizes editing of a cell.
  - Date Component: To customize the date selection component in the date filter.
  - Filter Component: For custom column filter that appears inside the column menu.
  - Floating Filter: For custom column filter that appears inside the column menu.
  - Header Component: To customize the header of a column and column groups.
  - Loading Cell Renderer: To customize the loading cell row when using Server Side row model.
  - Overlay Component: To customize loading and no rows overlay components.
  - Status Bar Component: For custom status bar components.
  - Tool Panel Component: For custom tool panel components.
  - Tooltip Component: For custom cell tooltip components.
- There are two ways to register custom components:
  - By name.
  - Direct reference.
- Both options are fully supported by the grid, however the preferred options is by name as it's more flexible. 
  - All of the examples in the documentation use this approach. 
  - The direct reference approach is kept for backwards compatibility reasons as this was the original way to do it in ag-Grid.
- Registering components by name has the following advantages:
  - Implementations can change without having to change all the column definitions
  - The part of the grid specifying column definitions is plain JSON. 
