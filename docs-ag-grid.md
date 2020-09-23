---
title: docs-ag-grid
tags: [ag-grid, docs, grid, list, table]
created: '2020-07-14T13:01:37.940Z'
modified: '2020-08-05T04:35:33.164Z'
---

# docs-ag-grid

## Row Models

- The grid can be configured with different strategies for loading row data into the grid, which are encapsulated into different Row Models. 
  - Changing which Row Model the grid is using means changing the strategy the grid is using for loading rows.
- The grid comes with four row models
  - Client-Side
    - This is the default. 
    - The grid will load all of the data into the grid in one go. 
    - The grid can then perform filtering, sorting, grouping, pivoting and aggregation all in memory.
  - Infinite
    - This will present the data to the user and load more data as the user scrolls down. 
    - Use this if you want to display a large, flat (not grouped) list of data.
  - Server-Side
    - The Server-Side Row Model builds on the Infinite Row Model. 
    - In addition to lazy-loading the data as the user scrolls down, it also allows lazy-loading of grouped data with server-side grouping and aggregation. 
    - Advanced users will use Server-Side Row Model to do ad-hoc slice and dice of data with server-side aggregations.
  - Viewport
    - The grid will inform the server exactly what data it is displaying (first and last row) and the server will provide data for exactly those rows only. 
    - Use this if you want the server to know exactly what the user is viewing, useful for updates in very large live datastreams where the server only sends updates to clients viewing the impacted rows.
- The Client-Side Row Model deals with client-side data. 
  - The Server-Side, Infinite and Viewport Row Models deal with server-side data. 
  - Which row model you use is set as a grid property `rowModelType` . 
  - The default is 'clientSide'.
- Which row model you use will depend on your application. Here are some quick rules of thumb:
  - use Client-Side Row Model if you want to load all your data into the browser, or Infinite Row Model if you want to load it in blocks.
- Here are more detailed rules of thumb.
  - If you are not sure, use default Client-Side. 
    - The grid can handle massive amounts of data (100k+ rows). 
    - The grid will only render what's visible on the screen (40 rows approximately, depending on your screen size) even if you have thousands of rows returned from your server. 
    - You will not kill the grid with too much data - rather your browser will run out of memory before the grid gets into problems. 
    - So if you are unsure, go with Client-Side Row Model first and only change if you need to. 
    - With Client-Side, you get sorting, filtering, grouping, pivoting and aggregation all done for you by the grid. 
    - All of the examples in the documentation use the Client-Side model unless specified otherwise.
  - If you do not want to shift all the data from your server to your client, as the amount of data is too large to shift over the network or to extract from the underlying datasource, then use either Infinite, Server-Side or Viewport. 
    - Each one takes data from the server in different ways.
  - Use Infinite or Server-Side to bring back a list of data one block at a time from the server. 
    - As the user scrolls, the grid will ask for more rows. 
    - Server-Side has more features than Infinite and will allow row grouping, aggregation, lazy-loading of groups and slice and dice of data.
  - Use Viewport if you want the server to know exactly what the user is looking at. 
    - This is best when you have a large amount of changing data and want to push updates to the client when the server-side data changes. 
    - Knowing exactly what the user is looking at means you only have to push updates to the relevant users. 
    - All the row models can receive updates, but only the Viewport row model provides the server with the information of the rows the users currently sees on screen without scrolling.

- Deeper Understanding of Row Models
  - The grid follows an MVC pattern. 
  - Each data item is wrapped in a Row Node and then stored in the Row Model. 
  - The grid rendering engine is called Row Renderer and listens for changes to the row model and updates the DOM accordingly
  - The grid has exactly one `RowRenderer` instance. 
    - The RowRenderer contains a reference to the `PaginationProxy` where it asks for the rows one at a time for rendering.
  - The grid has exactly one `PaginationProxy` instance. 
    - The `PaginationProxy` will either a) do nothing if pagination is not active and just forward all requests to the Row Model or b) do pagination if pagination is active. 
    - The `PaginationProxy` has exactly one `RowModel` instance.
  - You can configure the grid to use any of the provided Row Models - that's why `RowModel` is in italics, it means it's an interface, the concrete implementation is what you decide when configuring the grid. 
    - The `RowModel` contains a list of RowNodes. 
    - The `RowModel` may have a list of all the RowNodes (Client-Side Row Model) or have a datasource where it can lazy-load RowNodes.
  - A `RowNode` has a reference to exactly one row data item (the client application provides the row data items). 
    - The `RowNode` has state information about the row item, such as whether it is selected and the height of it.
  - When there is a change of state in the `RowNode` s, the `RowModel` fires a `modelUpdated` event which gets the `RowRenderer` to refresh. 
    - This happens for many reasons, or example the data is sorted, filtered, a group is opened, or the underlying data has changed.

- Pagination can be applied to any of the row model types. 
  - The documentation on each row model type covers pagination for that row model type.

- The Client-Side row model does not need a datasource. 
  - Infinite, Viewport and Server-Side all use a datasource. 

## Client-Side Data Overview

- By default the grid expects you to provide all the data up front. 
  - In other words, your application loads the full set of data into the client and then passes it in its entirety to the grid. 
  - This is in contrast to Server-Side Data where the data is mostly kept on the server and loaded into the grid in parts.
- There is only one client-side row model, aptly named the "Client-Side Row Model". 
  - You don't need to configure the grid to use the Client-Side Row Model as it's used by default.

- ### Client-Side Row Model
- Once the grid has all of the data, it can perform many operations on it for you, such as sorting, filtering and grouping.
- The Client-Side Row Model is responsible for working out how to display the rows inside the grid. 
- It has a complex data structure, representing the data in different states. 
- State 1: Row Data
  - The data as provided by the application. 
  - The grid never modifies this array. 
  - It just takes the `rowData` items from it.
  - API: There is no API to get this data. However it was provided by the application so you should already have it.
- State 2: All Rows
  - `allRows` is similar to `rowData` except a new array is created which contains row nodes, with each row node pointing to exactly one data item. 
  - The length of the `allRows` array is the same as the `rowData` array.
  - API: There is no API to get this data. However there is no benefit over the `rowsAfterGroup` data.
- State 3: Rows After Group
  - `rowsAfterGroup` takes `allRows` , and if grouping, groups the data. 
  - If no grouping is done, then `rowsAfterGroup` will be identical to `allRows` . 
  - API: Use `api.forEachNode()` to access this structure.
- State 4: Rows After Filter
  - `rowsAfterFilter` goes through `rowsAfterGroup` and filters the data. 
  - API: Use `api.forEachNodeAfterFilter()` to access this structure.
- State 5: Rows After Sort
  - `rowsAfterSort` goes through `rowsAfterFilter` and sorts the data. 
  - API: Use `api.forEachNodeAfterFilterAndSort()` to access this structure.
- State 6: Rows After Map
  - `rowsAfterMap` maps the data to what should be drawn inside the grid, taking into account what groups are open and closed. 
  - This list is what is iterated through when the grid draws the rows.
  - API: Use `api.getModel()` and then `model.getVirtualRowCount()` and `getVirtualRow()` to get the nodes.

- Refreshing the Client-Side Model
  - If you do want to refresh the Client-Side Row Model, call `api.refreshClientSideRowModel(startingStage)` , where `startingStage` can be one of the stages above, i.e.: group, filter, pivot, aggregate, sort, map
  - Because each stage depends on the stage before, refreshing any particular stage means that stage executes and then all the stages after it will also execute again.

## Client-Side Data - Accessing Client-Side Data

- Each time you pass data to the grid, the grid wraps each data item with a RowNode object. 
- It is handy to access these Row Nodes. 

## Client-Side Data - Updating Client-Side Data

- Updating data in the grid via the grid's API does not cover all the ways in which data can change inside the grid. Data can also change in the grid in the following ways:
  - Editing data inside the grid using the grid's UI, e.g. by the user double-clicking on a cell and editing the cell's value. 
    - When this happens, the grid is in control and there is no need to explicitly tell the grid data has changed. 
    - See in-line editing on how to edit via the grid's UI.
  - The grid's data is updated from elsewhere in your application. 
    - This can happen if you pass data to the grid and then subsequently change that data outside of the grid. 
    - This leaves the grid's view out of sync with the data that it has. 
    - In this instance what you want to do is refresh the view to have the grid's UI redraw to display the data changes.

- Setting Fresh Row Data
  - The easiest way to update data inside the grid is to replace the data you gave it with a fresh set of data. 
  - This is done by either updating the `rowData` bound property (if using a framework) or calling `api.setRowData(newData)` .
  - Replacing the data with a fresh set means the grid will treat it as a brand new set of data and as such the following will occur:
    - Row selection will be cleared.
    - If grouping, the open/closed state of the groups will be cleared.
    - The entire grid's UI will be refreshed from scratch. This has the following drawbacks:
      - All Cell Renderers will be destroyed and re-created with no option to have them refresh, 
        - losing out on a chance to provide custom animation between value changes (e.g. fade or slide old value out).
      - Row Animation will not be applied. 
        - For example, if the difference in data is one row is removed, all rows below will jump up one position rather than having a smooth transition.
      - It is not possible to highlight data changes, e.g. to flash cells.
    - All of the Client-Side Row Model calculations will be redone from scratch, i.e. sorting, filtering, grouping, aggregation and pivoting.
    - Use the technique of setting new Row Data when you are dealing with a different distinct set of data e.g. loading a new report with a completely different dataset to the previous one. 
    - This makes sure nothing is lying around from the old dataset and all data-related grid state (selection, groups etc.) is cleared.

- Changes to Row Data means you want to change some of the data and have the grid keep all state that it had before the data change.
  - Keeping all state means items such as row selection and group open/closed state will be maintained.
- There are different ways of updating row data which are summarized as follows:
  - Single Row/Cell
    - Updates the value of a single row or cell. 
    - This is done by getting a reference to the Row Node and then calling either `rowNode.setData()` or `rowNode.setDataValue()` .
    - Use transactions for updating a small number of individual rows infrequently. There is no way to insert or remove rows with this method.
  - Transaction
    - The grid takes a transaction containing rows to add, remove and update. 
    - This is done using `api.applyTransaction(transaction)` .
    - Use transactions for doing add, remove or update operations on a large number of rows that are infrequent.
  - High Frequency
    - High Frequency (achieved with Async Transactions) is a mechanism of applying many transactions over a small space of time and have the grid apply all the transactions in batches. 
    - The high frequency/batch method is for when you need the fastest possible way to process many continuous updates, such as providing a stream of updates to the grid. 
    - This is done using the API `applyTransactionAsync(transaction)` .
    - Use Async Transactions for doing add, remove or update operations that are frequent, e.g. for managing streaming updates into the grid of tens, hundreds or thousands of updates a second.

### Single Row/Cell

- The easiest way to update data inside the grid is to replace the data you gave it with a fresh set of data. 
- This is done by either updating the `rowData` bound property (if using a framework) or calling `api.setRowData(newData)` .
- Replacing the data with a fresh set means the grid will treat it as a brand new set of data and as such the following will occur:
  - Row selection will be cleared.
  - If grouping, the open / closed state of the groups will be cleared.
  - The entire grid's UI will be refreshed from scratch. 
  - All of the ClientSideRowModel calculations will be redone from scratch, i.e. sorting, filtering, grouping, aggregation and pivoting.

### Transactions

- Transaction Updates allow adding, removing or updating large numbers of rows inside the grid in an efficient manner.
- Transaction Updates are excellent for applying large data changes with the following advantages:
  - Efficient operation.
  - Updates sort, filter, group, aggregation and pivot after changes applied.
- A transaction object contains the details of what rows should be added, removed and updated. 
  - The grid API applyTransaction(transaction) takes this transaction object and applies it to the grid's data.
  - The result of the applyTransaction(transaction) is also a transaction
- Row Data Transaction: Contains Row Data, the data that you are providing to the grid.
- Row Node Transaction: Contains Row Nodes, the grid-created objects that wrap row data items.

- Deciding what groups need to be operated on within the grid is called Changed Path Selection.
  - After the grid applies all adds, removes and updates from a transaction, it works out what groups were impacted and only executes the required operations on those groups.
  - The groups that were impacted include each group with data that was changed, as well as all parents of changed groups all the way up to the top level.

### High Frequency

- Every time you update data in the grid, the grid will rework all aggregations, sorts and filters as well as having the browser update its DOM. If you are streaming multiple updates into the grid this can be a bottleneck. 
- High Frequency Updates are achieved in the grid using Async Transactions. Async Transactions allow for efficient high-frequency grid updates.
- To help understand the interface for applyTransaction() and applyTransactionAsync(), here are both method signatures side by side. 
  - The first executes immediately. 
  - The second executes sometime later using a callback for providing a result.
- You might ask, wouldn't using a virtual DOM like React remove the necessity of Async Transactions? 
  - The answer is no. A virtual DOM would only batch the DOM related updates, it would not help with the batching of aggregations, sorts and filters.
- The default wait between executing batches is 50ms. This means when an Async Transaction is provided to the grid, it can take up to 50ms for that transaction to be applied.
- Sometimes you may want all transactions to be applied before doing something 
  - for example you may want to select a rows in the grid but want to make sure the grid has all the latest row data before doing so.
  - To make sure the grid has no Async Transactions pending, you can flush the Async Transaction queue. This is done by calling the API `flushAsyncTransactions` .

## Client-Side Data - Immutable Data

- Under normal operation when new data is set into the grid (e.g. the `rowData` bound property is updated with new data), the grid assumes the new data is a brand new set of data. 
  - It is common for applications to desire this behavior. 
  - However as explained in Setting Fresh Row Data this can be undesirable as grid state (selected rows etc.) is lost.
- For most applications, using grid Transaction Updates are what you should do if you want to make changes to the dataset rather than replace it. 
  - However this is not in line with how applications based on immutable stores desire to work.
- In applications using immutable stores (e.g. React and Redux), it could be desirable to treat changes to the bound `rowData` as updates to the current dataset rather than a brand new dataset. 
  - The grid has a mode of operation where it does exactly this. 
  - It works out what rows are added, removed and updated when new row data is provided by inspecting the new row data. 
  - This mode is called Immutable Data Mode and is enabled by setting the property `immutableData=true` .

- When in Immutable Data Mode, the grid assumes it is fed with data from an immutable store where the following is true about the data:
  - Changes to a single row data item results in a new row data item object instance.
  - Any changes within the list or row data results in a new list.

- For the Immutable Data Mode to work, you must be providing IDs for the row nodes.
- The grid works out what changes need to be applied to the grid using the following rules:
  - 新建。IF the ID for the new item doesn't have a corresponding item already in the grid THEN it's added as a new row to the grid.
  - 更新。IF the ID for the new item does have a corresponding item in the grid THEN compare the object references. If the object references are different, the row is updated with the new data, otherwise it's assumed the data is the same as the already present data.
  - 移除。IF there are items in the grid for which there are no corresponding items in the new data, THEN those rows are removed.
  - 重排序。Lastly the rows in the grid are sorted to match the order in the newly provided list.

## Client-Side Data - Context

- The context object is passed to most of the callbacks used in the grid. 
- The purpose of the context object is to allow the client application to pass details to custom callbacks such as the Cell Renderers and Cell Editors.
- Note that the grid does not place anything into the context and it is not used internally by the grid.

## Row Spanning

- By default, each cell will take up the height of one row.   
  - You can change this behaviour to allow cells to span multiple rows. 
  - This feature is similar to 'cell merging' in Excel or 'row spanning' in HTML tables.
- To allow row spanning, the grid must have property `suppressRowTransform=true` to turn off row translation.
  - `suppressRowTransform=true` is used to stop the grid positioning rows using CSS `transform` and instead the grid will use CSS `top` .
  - The reason row span will not work with CSS transform is that CSS transform creates a stacking context which constrains(限制) CSS `z-index` from placing cells on top of other cells in another row. 
  - Having cells extend into other rows is necessary for row span which means it will not work when using CSS transform. 
  - The downside to not using transform is performance; row animation (after sort or filter) will be slower.
- Row spanning is then configured at the column definition level. 
  - To have a cell span more than one row, return how many rows to span in the callback `colDef.rowSpan` .
- Row Spanning Simple Example
  - The Athlete column is configured to apply a CSS class to give a background to the cell. 
  - This is important because if a background was not set, the cell background would be `transparent` and the underlying cell would still be visible.
- Row Spanning Complex Example
  - Column Show row spans by 4 rows when it has content.
  - Column Show uses CSS class rules to specify background and border.
  - Column Show has a custom cell renderer to make use of the extra space.

- ### Constraints with Row Spanning
- Row Spanning breaks out of the row/cell calculations that a lot of features in the grid are based on. 
- If using Row Spanning, be aware of the following:
  - Responsibility is with the developer to not span past the last row. 
    - This is especially true if sorting and filtering 
    - (e.g. a cell may span outside the grid after the data is sorted and the cell's row ends up at the bottom of the grid).
  - Responsibility is with the developer to apply a `background` style to spanning cells so that overwritten cells cannot be seen.
  - Overwritten cells will still exist, but will not be visible. 
    - This means cell navigation will go to the other cells - e.g. if a row spanned cell has focus, and the user hits the 'arrow down' key, the focus will go to a hidden cell.
  - Row span does not work with dynamic row height or auto-height. 
    - The row span assumes default row height is used when calculating how high the cell should be.
  - Sorting and filtering will provide strange results when row spanning. 
    - For example a cell may span 4 rows, however applying a filter or a sort will probably change the requirements of what rows should be spanned.
  - Range Selection will not work correctly when spanning cells. 
    - This is because it is not possible to cover all scenarios, as a range is no longer a perfect rectangle.

- Comparison to Transaction Updates
  - When in Immutable Data Mode and the grid receives new data, it creates a Transaction Update underneath the hood. 
    - In other words, once the grid has worked out what rows have been added, updated and removed, it then creates a transaction with these details and applies it. 
    - This means all the operational benefits to Transaction Updates equally apply to Immutable Data Mode.
  - There are however some difference with Immutable Data Mode and Transaction Updates which are as follows:
    - When in Immutable Data Mode, the grid stores the data in the same order as the data was provided. 
      - For example if you provide a new list with data added in the middle of the list, the grid will also put the data into the middle of the list rather than just appending to the end. 
      - This decides the order of data when there is no grid sort applied. 
      - If this is not required by your application, then you can suppress this behavior for a performance boost by setting `suppressMaintainUnsortedOrder=true` .
    - There is no equivalent of Async Transactions when it comes to Immutable Data Mode. 
      - If you want a grid that manages high frequency data changes, it is advised to not use Immutable Data Mode and use Async Transactions instead.

## Column Spanning

- By default, each cell will take up the width of one column. 
  - You can change this behaviour to allow cells to span multiple columns. 
  - This feature is similar to 'cell merging' in Excel or 'column spanning' in HTML tables.
- Column spanning is set configured at the column definition level. 
  - To have a cell span more than one column, return how many columns to span in the callback `colDef.colSpan` .
- Column Spanning Simple Example
  - Resizing any columns that are spanned over will also resize the spanned cells. 
  - For example, resizing the column immediately to the right of 'Country' will resize all cells spanning over the resized column.
  - The first two columns are pinned. 
    - If you drag the country column into the pinned area, you will notice that the spanning is constrained within the pinned section, e.g. if you place Country as the last pinned column, no spanning will occur, as the spanning can only happen over cells in the same region, and Country now has no further columns inside the pinned region.
- Column Spanning Complex Example
  - The data is formatted in a certain way, it is not intended for the user to sort this data or reorder the columns.
  - The dataset has meta-data inside it, the `data.section` attribute. 
  - This meta-data, provided by the application, is used in the grid configuration in order to set the column spans and the background colours.
- ### Column Spanning Constraints
  - Range Selection will not work correctly when spanning cells. 
    - This is because it is not possible to cover all scenarios, as a range is no longer a perfect rectangle.

## DOM Virtualization

- https://www.ag-grid.com/javascript-grid-dom-virtualisation/

- The grid uses DOM virtualization to vastly improve rendering performance.
- If you loaded 1, 000 records with 20 columns into the browser without using a datagrid (eg using 'table', 'tr' and 'td' tags), then the page would end up with a lot of rendered DOM elements. 
  - This would drastically slow down the web page. 
  - This results in either a very poor user experience, or simply crashing the browser as the browser runs out of memory.
- To get around this, the grid only renders what you see on the screen. 
  - For example if you load 1, 000 records and 20 columns into the grid, 
  - but the user can only see 50 records and 10 columns (as the rest are not scrolled into view), 
  - then the grid only renders the 50 rows adn 10 columns that the user can actually see.
- As the user scrolls horizontally or vertically, 
  - the grid dynamically updates the DOM and renders the additional cells that are required while also removing the cells that are no longer in view.
- This technique of only rendering into the DOM what is in the visible scrollable viewport is known as row and column virtualisation.
- **Row virtualisation** is the insertion and removal of rows as the grid scrolls vertically.
  - By default the grid will render 10 rows before the first visible row and 10 rows after the last visible row, thus 20 additional rows get rendered. 
  - This is to act as a buffer as on some slower machines and browsers, a blank space can be seen as the user scrolls.
  - As a safety measure, the grid will render a maximum of 500 rows. 
    - This is to stop applications from crashing if they incorrectly set the grid size 
    - (ie if they don't size the grid correctly, and the grid tries to render 10,000 rows, this can crash the browser). 
    - To remove this restriction set the property `suppressMaxRenderedRowRestriction=true` .
- **Column virtualisation** is the insertion and removal of columns as the grid scrolls horizontally.
  - There is no column buffer - no additional columns are rendered apart from the visible set. 
  - This is because horizontal scrolling is not as CPU intensive as vertical scrolling, thus the buffer is not needed for a good UI experience.
  - To turn column virtualisation off set the grid property `suppressColumnVirtualisation=true` .

## Export

- The grid provides APIs to export data to CSV and Excel. 
- You can download a file to the user's computer or generate a string to be uploaded to a server. 
- What Gets Exported
  - The same data that is in the grid gets exported, but none of the GUI representation of the data will be. 
- What this means is:
  - The raw values, and not the result of cell renderer, will get used, meaning:
    - Cell Renderers will NOT be used.
    - Value Getters will be used.
    - Cell Formatters will NOT be used (use processCellCallback instead).
  - Cell styles are not exported by default. CSV does not allow styling. 
  - If row grouping:
    - all data will be exported regardless of whether groups are open in the UI.
    - by default, group names will be in the format "-> Parent Name -> Child Name" 
    - row group footers (groupIncludeFooter=true) will NOT be exported - this is a GUI addition that happens for displaying the data in the grid.
- It is not possible to download files directly from JavaScript to an iPad. 
  - This is a restriction of iOS and not something wrong with ag-Grid. 
  - For this reason, the download links in the context menu are removed when running on iPad.
