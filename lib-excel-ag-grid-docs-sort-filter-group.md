---
title: lib-excel-ag-grid-docs-sort-filter-group
tags: [ag-grid]
created: 2020-08-24T09:17:28.346Z
modified: 2022-08-21T09:55:01.585Z
---

# lib-excel-ag-grid-docs-sort-filter-group

# Row Sorting

- Enable sorting for columns by setting the `sortable` column definition attribute. 
  - You can then sort a column by clicking on the column header.
- You cannot use variable row height when using Viewport Row Model. 
  - This is because this row model needs to work out the position of rows that are not loaded and hence needs to assume the row height is fixed.
- To change the row height for the whole grid, set the property `gridOptions.rowHeight` to a positive number. 
- To change the row height so that each row can have a different height, implement the `getRowHeight()` callback.

# Filtering Overview

- different types of filtering that can be performed in the grid as follows:
  - Column Filters
    - Column filters appear in the column menu and/or in the Filters Tool Panel. 
    - A filter set on a column filters using data in that column only.
  - Quick Filter
    - Quick filter is a piece of text given to the grid (typically the user will type it in somewhere in your application) that is used to filter rows using data in all columns in the grid.
  - External Filter
    - An external filter is a mechanism for the application to filter out rows independently of any filtering done by the grid.

- Column filters are accessed in the grid UI either through the Column Menu or the Tool Panel.
- Filtering causes the following events to be emitted:
  - Filter Changed: Filter has changed and been applied by the grid.
  - Filter Modified: Filter UI has changed but not necessarily applied. This is useful when using an apply button if you want to know if the filter changed but was not applied.
- Column filters work independently of Quick Filter and External Filter. 
  - If a quick filter and/or external filter are applied along with a column filter, each filter type is considered and the row will only show if it passes all three types.
  - Column filters are tied to a specific column. Quick filter and external filter are not tied to any particular column.  
- builtin providedFilters
  - agNumberColumnFilter
  - agTextColumnFilter
  - agDateColumnFilter
  - agSetColumnFilter
- Provided filters maintain a separate model representing what is shown in the UI, which might change without having yet been applied, for example when an Apply button is present and the user has made changes in the UI but not yet clicked Apply.

- Floating Filters are an additional row under the column headers where the user will be able to see and optionally edit the filters associated with each column.

# Row Grouping

- To group rows by a particular column, mark the column you want to group with `rowGroup=true` . 
  - There is no limit on the number of columns that the grid can group by.
- The grid lets you automatically create one column for each individual group. 
    - This is achieved by setting `gridOptions.groupMultiAutoColumn = true` . 

- If there are rows containing `null` or `undefined` values for the column that is being grouped, then these rows will not be grouped. 
  - We refer to this scenario as Unbalanced Groups in that there is a mix of groups and rows as siblings. 

# Master/Detail

- Master Detail refers to a top level grid called a Master Grid having rows that expand. 
  - When the row is expanded, another grid is displayed with more details related to the expanded row. 
  - The grid that appears is known as the Detail Grid.
- When using Master/Detail, the Master Grid must be using either the Client-Side or Server-Side Row Models. 
  - It is not supported with the Viewport or Infinite Row Models.
- The Detail Grid on the other hand can use any Row Model.

# Tree Data

- Use Tree Data to display data that has parent/child relationships where the parent/child relationships are provided as part of the data. 
  - For example, a folder can contain zero or more files and other folders.
  - TreeDataView和groupView的区别在于，group后某些不能聚集计算的字段会为空，但treeData每一级的所有中间节点及子节点都可显示
- When providing tree data to the grid, you implement the `gridOptions.getDataPath(data)` callback to tell the grid the hierarchy for each row. 
  - The callback returns back a `string[]` with each element specifying a level of the tree.
- When using Tree Data, columns defined with an aggregation function will always perform aggregations on the group nodes. 
  - This means any supplied group data will be ignored in favour of the aggregated values.
  - However if there are no child nodes to aggregate it will default to the provided value in the row data.

# Aggregation

- When grouping, you can apply an aggregation function to any column to populate the group row with values. 
- You can pick from the grid's built in aggregation functions or provide your own.
- You can define aggregations on columns in the following three ways:
  - Built In Functions
    - Out of the box the grid provides sum, min, max, count, avg, first, last. 
    - To use one of these, set `colDef.aggFunc` to the string of the function you require.
  - User Registered Functions
    - You can install your own aggregation functions into the grid and reference them as if they were grid provided functions by calling `api.addAggFunc(key,func)` .
  - Direct Functions
    - Lastly you can provide a function directly by setting `colDef.aggFunc` to your custom function. 
    - Direct functions do not appear in the toolPanel when selecting functions for your columns.
- Aggregation functions are provided with an array of values that it should aggregate into one value that it then returns. 
- Using a function directly will not work with column state, like Saving and Restoring Column State. 
  - If you require state management with custom aggregation, use `addAggFunc` to register it.

# Pivoting

- Pivoting allows you to take a columns values and turn them into columns. 
  - For example you can pivot on Country to make columns for Ireland, United Kingdom, USA etc.
  - pivot与group的主要区别是
    - pivot侧重基于现有列计算新值，如sum,avg
    - group侧重基于某列的各个唯一值显示值相同的行组成一个group，常以折叠形式显示
- Pivoting only makes sense when mixed with aggregation. 
  - If you turn a column into a pivot column, you must have at least one aggregation (value) active for the configuration to make sense. 
  - For example, if pivoting by country, you must provide something you are measuring such as 'gold medals per country'.

# Selection Overview

- Row Selection selects rows, i.e. data entries from the provided data set.
- Range Selection selects ranges of cells, i.e. a rectangular block of cells.
- If you want to use a regular text selection as if the grid were a regular table. 
  - Use `enableCellTextSelection=true` in the `gridOptions` .
