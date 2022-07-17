---
title: lib-list-ag-grid-docs-react
tags: [ag-grid, docs]
created: 2020-08-24T09:15:06.175Z
modified: 2021-05-13T02:43:00.595Z
---

# lib-list-ag-grid-docs-react

# Get Started with ag-Grid and React

- AgGridReact
  - rowData
  - columnDefs
- Enable Sorting And Filtering
  - headerName, field, sortable, filter
- Fetch Remote Data
  - `componentDidMount()` or `useEffect()`
- Enable Selection
  - headerName, field, checkboxSelection
  - rowSelection="multiple"
- Grouping
  - headerName, field, rowGroup
- ag-grid 18~21.2 -- react 15.x
- ag-grid 22+  -- react 16.3+/17+

- Columns can be defined in three ways: 
  - declaratively (i.e. via `<AgGridColumn>` markup), 
  - via `GridOptions` with `columnDefs` prop
  - or by binding to `columnDefs` prop on the `AgGridReact` component.
  - In all cases all column definition properties can be defined to make up a column definition.

- By default user supplied React components will be wrapped in a `div` , 
  - but it is possible to have your component wrapped in a container of your choice (i.e. a `span` etc), perhaps to override/control a third party component.
  - If you wish to override the style of this div, you can either provide an implementation of the `ag-react-container` class, or via the `getReactContainerStyle` or `getReactContainerClasses` callbacks on the React component

# More Control of ag-Grid with React

- When the grid is initialized, it will fire the `gridReady` event. 
  - If you want to use the API of the grid, you should put an `onGridReady(params)` callback onto the grid and grab the api from the params. 
  - You can then call this api at a later stage to interact with the grid (on top of the interaction that can be done by setting and changing the props).
- React renders components asynchronously and although this is fine in the majority of use cases, 
  - it can be the case that in certain circumstances a very slight flicker can be seen where an old component is destroyed but the new one is not yet rendered by React.
  - In order to eliminate this behavior, the Grid will "pre-render" cell components and replace them with the real component once they are ready.
  - What this means is that the `render` method on a given `Cell` Component will be invoked twice, once for the pre-render and once for the actual component creation.
    - 注意：Cell组件的render会调用2次
  - Note that this pre-render only applies to Cell Components - other types of Components are unaffected.
- By default the ag-Grid React component will check props passed in to determine if data has changed and will only re-render based on actual changes.
  - IdentityCheck/referenceEqual
  - DeepValueCheck/deepEqual
  - NoCheck/AlwaysRender

# Hooks for ag-grid

- We can break down the type of Hooks you can use within ag-Grid into two broad categories - those that have lifecycle methods (such as Filters) and those that don't (such as Cell Renderers).
- Hooks without Lifecycle Methods
  - Cell Renderers, Loading Cell Renderers and Overlay Components are examples of components without lifecycle methods.
  - For this type of Hook you don't have to do anything special and the Hook should work as expected within ag-Grid, although it would often be easier to simply use a functional component in these cases (as there won't be any state to maintain).
- Hooks with Lifecycle Methods
  - Filters, Cell Editors and Floating Filter Components are examples of components that have mandatory lifecycle methods.
  - For these types of components, you'll need to wrap your hook with `forwardRef` and then expose Grid related lifecycle methods `useImperativeHandle`
- Rendering Null
  - If you don't want to output anything on render then return an empty string rather than `null` .
  - If you return `null` , then React simply won't render the component and the Grid is unable to determine if this is by design or an error.
