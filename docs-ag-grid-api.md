---
title: docs-ag-grid-api
tags: [ag-grid, api, docs]
created: '2020-08-24T09:15:27.178Z'
modified: '2020-08-24T09:16:38.313Z'
---

# docs-ag-grid-api

## Grid Interface

- The grid interface is the combination of the following items:
- Grid Properties
  - properties used to configure the grid, e.g. `pagination = true` .
- Grid API
  - methods used to interact with the grid after it's created, e.g. `api.getSelectedRows()` .
- Events
  - events published by the grid to inform applications of changes in state, e.g. `rowSelected` .
- Grid Callbacks
  - callbacks are used by the grid to retrieve required information from your application, e.g. `getRowHeight()` .
- Row Node
  - each row in the grid is represented by a Row Node object, which in turn has a reference to the piece of row data provided by the application. 
  - The Row Node wraps the row data item. 
  - The Row Node has attributes, methods and events for interacting with the specific row e.g. `rowNode.setSelected(true)` .

### Grid Options

- `gridOptions` object is a 'one stop shop' for the entire interface into the grid. 
  - The grid options can be used regardless of the framework you are using, 
  - but if you are using a framework you might find it easier to use your framework's bindings.
  - `gridOptions` 对象的属性支持配置 Properties, Events, Callbacks
- Once the grid is initialized, you will also have access to the grid API ( `api` ) and column API ( `columnApi` ) on the `gridOptions` object 

``` JS
// refresh the grid
gridOptions.api.refreshView();

// resize columns in the grid to fit the available space
gridOptions.columnApi.sizeColumnsToFit();
```

### Listening to Events

- In addition to adding event listeners directly via the `onXxx` prop of `gridOptions` object, it is possible to register for events using `addEventListener` , similar to registering for events on native DOM elements. 
  - This means there are two ways to listen for events: either to use the `onXXX(` ) method on the API, or to register for the event. 
  - The latter option allows you to add multiple handlers for the same event. 

``` JS
// create handler function
function myRowClickedHandler(event) {
  console.log('The row was clicked');
}

// option 1: use the API
gridOptions.onRowClicked = myRowClickedHandler;

// option 2: register the handler
gridOptions.api.addEventListener('rowClicked', myRowClickedHandler);
```

- Grid events are asynchronous so that the state of the grid will be settled by the time your event callback gets invoked.

### more about ag-grid api

- Where the property is a boolean ( `true` or `false` ), then `false` (or left blank) is the default value. 
  - For this reason, on/off items are presented in a way that causes the most common behavior to be used when the value is `false` . 
  - For example, suppressCellSelection is named as such because most people will want cell selection to be enabled.
- If you are using plain Javascript, all of your interaction with ag-Grid will be through `gridOptions` .
- The `gridOptions` are fully available as stated above for React. However you can take advantage of React's properties and events provided by ag-Grid's React Component. 
  - Properties: properties are defined by passing React props down to ag-Grid.
  - Event Handlers: event handlers are also defined using React Props.
  - Callbacks: callbacks are also defined using React Props.
  - API: The grid API and column API are provided to you via the `onGridReady()` event callback.
    - The APIs are also accessible through the component ref itself. 
- So in summary, in React, everything is done via React Props.

## Column interface

- The column interface is the combination of the following items:
  - Column Properties
    - Columns are configured through column definitions. 
    - A column definition contains the column properties e.g. `colDef.pinned='left'` .
  - Column API
    - The column API is similar to the grid API, the difference is that the column API provides methods relevant to columns e.g. `columnApi.setColumnVisible('country', false)` .
  - Column Object
    - Each column in the grid is represented by a Column object, which in turn has a reference to the column definition provided by the application. 
    - The Column wraps the Column Definition. 
    - The Column object has attributes, methods and events for interacting with the specific column e.g. `column.isVisible()` .

## Grid Properties

- All of these grid properties are available through the GridOptions interface.
- Columns
  - columnDefs: Array of Column Definitions.
  - defaultColDef
  - defaultColGroupDef
  - columnTypes
  - suppressMovableColumns
  - skipHeaderOnAutoSize: 
  - suppressMultiSort
  - autoGroupColumnDef
- Sort and Filter
  - quickFilterText
  - multiSortKey
  - sortingOrder
- Selection
  - rowSelection
  - rowDeselection
  - suppressCellSelection
  - enableRangeSelection
- Row Dragging
  - suppressRowDrag
  - rowDragManaged
  - suppressMoveWhenRowDragging
- Editing
  - singleClickEdit
  - editType: 'fullRow'. Otherwise leave blank to edit one cell at a time.
- Headers
  - headerHeight
  - floatingFiltersHeight: The height for the row containing the floating filters
  - pivotHeaderHeight
- Row Grouping
  - groupDefaultExpanded: If grouping, set to the number of levels to expand by default
  - rowGroupPanelShow
- Row Pivoting
  - pivotMode
  - pivotPanelShow
  - aggregateOnlyChangedColumns
- Data and Row Models
  - rowData: Client-Side Row Model only
  - immutableData: Client-Side Row Model only
  - rowModelType: 'clientSide', 'infinite', 'viewport', 'serverSide'
  - pinnedTopRowData: Data to be displayed as Pinned Top Rows in the grid.
- Row Model: Server-Side
  - cacheBlockSize
  - cacheOverflowSize
  - infiniteInitialRowCount
- Row Model: Viewport
  - viewportRowModelPageSize
  - viewportRowModelBufferSize
  - viewportDatasource
- Scrolling
  - alwaysShowVerticalScroll
  - suppressHorizontalScroll
  - suppressColumnVirtualisation
- Pagination
  - pagination
  - paginationPageSize
  - paginationAutoPageSize
- Full Width Renderers
  - groupRowRenderer
  - groupRowInnerRenderer
  - fullWidthCellRenderer
- Master Detail
  - masterDetail
  - keepDetailRows
  - detailRowHeight
- Rendering and Styling
  - rowHeight
  - rowStyle
  - excelStyles: The list of Excel styles to be used when exporting to Excel
  - scrollbarWidth
- Clipboard
  - copyHeadersToClipboard
  - clipboardDeliminator: Specify the deliminator to use when copying to clipboard.
  - enableCellTextSelection
- Localization
  - localeText
- Overlays
  - suppressLoadingOverlay
  - suppressNoRowsOverlay
  - overlayLoadingTemplate
  - loadingOverlayComponent
  - noRowsOverlayComponent
- Charts
  - enableCharts
- Components
  - components: A map of component names to plain JavaScript components.
  - frameworkComponents: A map of component names to framework (React, Angular etc) components.
- Miscellaneous
  - popupParent: DOM element to use as popup parent for grid popups (context menu, column menu etc).
  - valueCache
  - tooltipShowDelay
  - domLayout
  - rowBuffer

## Grid API

Columns
Data
Accessing Row Nodes
Displayed Rows
Master Detail
Selection
Refresh
Sort and Filter
Navigation
Editing
Export
Events
Row Groups
Row Drag
Rendering
Scrolling
Infinite Scrolling
Overlays
Clipboard
Pagination
Headers
Status Bar
Charts
Miscellaneous

## Grid Events

- This is a list of the events that the grid raises. 
  - You can register callbacks for these events through the `GridOptions` interface.
  - The name of the callback is constructed by prefixing the event name with on.
  - For example, the callback for the cellClicked event is `gridOptions.onCellClicked` .
- TypeScript users can take advantage of the events' interfaces. 
  - You can construct the interface name by suffixing the event name with Event. 
  - For example, the cellClicked event uses the interface `CellClickedEvent` .

- Selection
- Editing
- Sort and Filter
- Row Drag and Drop
- Columns
- Miscellaneous
- Event Properties and Hierarchy

- Event hierarchy, and properties, for all ag-Grid events. (All properties are inherited.)
- AgEvent
  - AgGridEvent
    - GridReadyEvent
    - SelectionChangedEvent
    - SortChangedEvent
    - RowDataChangedEvent
    - FilterChangedEvent
    - BodyScrollEvent
    - DragEvent
    - RowDragEvent
    - ColumnEvent
      - ColumnPivotChangedEvent
      - ColumnValueChangedEvent
      - ColumnResizedEvent
      - ColumnVisibleEvent
    - RowEvent
      - RowSelectedEvent
      - RowClickedEvent
      - RowEditingStartedEvent
      - RowValueChangedEvent
      - CellEvent
        - CellClickedEvent
        - CellDoubleClickedEvent
        - CellMouseDownEvent
        - CellEditingStartedEvent
        - CellContextMenuEvent
        - CellKeyDown
        - CellValueChangedEvent

## Grid Callbacks

- All of these grid callbacks are available through the `GridOptions` interface.
- getRowHeight(params): 
- headerCellRenderer(params): 
- groupRowAggNodes(nodes): 

## Row Node Object

- A Row Node represents one row of data. 
  - The Row Node will contain a reference to the data item your application provided as well as other runtime information about the row. 
  - The Row Node contains attributes, methods and emits events. 
  - Additional attributes are used if the Row Node is a group.
- All Row Node Attributes
- Group Node Attributes
- Row Node Methods
  - setData(newData): 
  - setRowHeight(height): 
  - addEventListener(eventType: string, listener: Function)
  - removeEventListener(eventType: string, listener: Function)
  - isSelected(): 
- Events on Row Nodes
  - rowSelected
  - mouseEnter/Leave
  - cellChanged
  - allChildrenCountChanged: 
  - dataChanged
  - heightChanged
  - topChanged
  - first/lastChildChanged
  - childIndexChanged
  - rowIndexChanged
  - expandedChanged
  - uiLevelChanged
- Row Node Events
  - All **events fired by the `rowNode` are synchronous** (events are normally asynchronous). 
    - The grid is also listening for these events internally. 
    - This means that when you receive an event, the grid may still have some work to do (e.g. if `rowTop` changed, the grid UI may still have to update to reflect this change). 
    - It is also best you do not call any grid API functions while receiving events from the `rowNode` (as the grid is still processing). 
    - Instead, it is best to put your logic into a timeout and call the grid in another VM tick.
  - When adding event listeners to a row, they will stay with the row until the row is destroyed. 
    - This means if the row is taken out of memory (pagination or virtual paging), then the listener will be removed. 
    - Likewise, if you set new data into the grid, all listeners on the old data will be removed.
  - Be careful when adding listeners to `rowNodes` in cell renderers that you remove the listener when the rendered row is destroyed due to row virtualisation.
- Row Node IDs
  - Each Row Node is identified by a unique ID. 
  - The ID of the Row Node is used by the grid to identify the row and can be used by your application to look up the Row Node using the grid API `getRowNode(id)`
  - By default IDs are assigned by the grid when data is set into the grid. 
    - The grid uses a sequence starting at `0` and incrementing by 1 to assign row IDs
    - The row ID is constant for as long as the data item lives in the grid.
  - When using Row Grouping, the grid assigns IDs to the row groups as the row groups are created. 
    - It uses another sequence again starting at `0` and incrementing by 1 and also prefixes the sequence number with `row-group-` . 
    - If the groups are destroyed (eg the user removes the grouping) and recreated again (the user groups by a column) then new ID's will be created 
    - As with normal rows, the ID's for group rows do not change for as long as the row group exists, 
      - however removing and re-adding the grouping will result in new row group ID's even if the row group represents the same group as before.
  - In some applications it is useful to tell the grid what IDs to use for particular rows. 
    - For example, if you are showing employees, you could configure the grid to use the Employee ID as the row node ID. 
    - That would then enable the grid API `getRowNode(id)` to be called with the Employee ID.
    - To get the grid to use application assigned IDs, implement the grid callback `getRowNodeId()` . 
    - The callback should return back the ID for a particular piece of row data. 
    - If using Row Grouping, the grid will always assign IDs for the group level (as there is not a one-to-one mapping with application-supplied row data). The callback `getRowNodeId()` is only used for non-group level rows.
  - When providing IDs the following rules must be obeyed:
    - IDs must be unique
    - IDs must not change

## Column Properties

- For column groups, the property `children` is mandatory. When the grid sees `children` it knows it's a column group.
- Columns and Column Groups
  - headerName
  - headerClass
  - columnGroupShow
  - toolPanelClass
  - suppressColumnsToolPanel
  - suppressFiltersToolPanel
- Columns Only
  - field
  - colId
  - type
  - width
  - flex: Used instead of width when the goal is to fill the remaining empty space of the grid.
  - filter 
  - hide
  - sortable
  - sort 
  - resizable
  - ...
- Column Group
  - groupId 
  - children: A list containing a mix of columns and column groups.
  - marryChildren: Moving the columns outside of the group (and hence breaking the group) is not allowed.
  - openByDefault
  - headerGroupComponent: Component to use header group.
  - headerGroupComponentParams: Params for the header group component.

## Column API

- Some of the API methods take Column Key (named `colKey` ) which has type `Column | string` . 
  - This means you can pass either a `Column` object (that you receive from calling one of the other methods) or you pass in the Column ID (which is a `string` ). 
  - The Column ID is a property of the column definition. 
  - If you do not provide the Column ID, the grid will create one for you (first by trying to use the field if it is unique, otherwise it will generate an ID).
- sizeColumnsToFit(width): Gets the grid to size the columns to the specified width in pixels
- getColumnGroup(name)
- getColumn(colKey)

## Column object

- A `Column` object represents a column in the grid. 
  - The `Column` will contain a reference to the column definition your application provided as well as other column runtime information. 
  - The column contains methods and emits events.
- Column Methods
  - getColId()
  - getParent()
  - getColDef()
  - isPrimary()
  - isFilterAllowed()
  - getSort()
  - getAggFunc()
  - isPivotActive()
  - addEventListener(): Add event listener to the column.
  - removeEventListener()
- Events on Column(Columns emit the following events)
  - filterActiveChanged: The filter active value has changed.
  - sortChanged: The sort value has changed.
  - leftChanged: The left position has changed (e.g. column has moved).
  - widthChanged: The width value has changed.
  - visibleChanged: The visibility value has changed.
  - menuVisibleChanged: The column menu was shown / hidden.
  - columnRowGroupChanged: The row group value has changed.
  - columnPivotChanged: The pivot value has changed.
  - columnValueChanged: The 'value' value has changed.
  - movingChanged: The column has started/finished moving (i.e. user is dragging the column to a new location).

- All events fired by the column are synchronous (events are normally asynchronous). 
- It is best that you do not call any grid API functions while receiving events from the column (as the grid is still processing), but instead put your logic into a timeout and call the grid in another VM tick.
- When adding event listeners to a column, they will stay with the column until the column is destroyed. 
  - Columns are destroyed when you add new columns to the grid. 
  - Column objects are NOT destroyed when the columns is removed from the DOM (e.g. column virtualisation removes the column due to horizontal scrolling, or the column is made invisible via the column API).
  - If you add listeners to columns in custom header components, be sure to remove the listener when the header component is destroyed.
