---
title: pm-list-grid-table-blog
tags: [blog, grid, list]
created: '2020-07-14T13:04:22.299Z'
modified: '2020-11-16T12:42:45.751Z'
---

# pm-list-grid-table-blog

## [在线Excel项目到底有多刺激](https://mp.weixin.qq.com/s/f1vwzuPryc8ag6nd5Ngr5A)

- 冲突处理
- 版本管理
- 房间管理
- 多种通信方式
- 每个格子都是一个富文本编辑器
- 富文本
- 复制粘贴
- 表格渲染有多复杂
- 数据管理的难题

## Five Fast JavaScript Data Grids — A Performance Review

- [Five Fast JavaScript Data Grids — A Performance Review_201909](https://dzone.com/articles/data-grid-performance-comparison)

- The following popular data grids were used in this comparison:
  - ag-grid (ag-grid.com)
  - Bryntum Grid (bryntum.com/products/grid)
  - DevExtreme Grid (js.devexpress.com/Overview/DataGrid)
  - DHTMLX Grid (dhtmlx.com/docs/products/dhtmlxGrid)
  - Ext JS Modern Grid (sencha.com/products/extjs)
- git repo: https://github.com/bryntum/grid-performance
- Benchmarking Methodology
  - Two test cases were created per grid, one with locked/fixed/pinned columns and one without.
  - The same dataset was used for all grids, consisting of 10, 000 JSON objects with ten fields each
  - Columns were configured as similar as possible for all grids
    - Ten columns, some with custom settings:
      - One column with cells that has their background color set from data.
      - One column with a custom progress bar.
      - One date column.
      - One boolean column displaying Yes/No.
    - The first three columns locked/fixed/pinned in the relevant test case.
    - For fairness, all non-essential features such as sorting, grouping, filtering and so on were turned off
    - All grids were rendered into a 1280 x 1024 px sized container.
    - All measurements were taken on a 2016 MacBook Pro 13" (2 GHz Intel Core i5, 8GB RAM).
    - Scrollbars were turned on
- Measuring
  - JavaScripts `performance.now()` was used to measure time in the benchmarks.
- Initial Rendering Time(ms) Result 
  - for simple grid 
    - dhtmlX: 55
    - bryntum: 104
    - ag-grid: 210
    - devExtreme: 216
    - extjs: 281
  - For all practical applications though, the difference between the best and the worst, in this case, is negligible. 
  - A real world application loading and displaying 10, 000 records will spend much more time retrieving the data from the backend than the time it takes to display it.
  - 带有locked/pinned/fixed列的首屏渲染测试结果排名与上面相同
- Scrolling FPS Result 肉眼更易察觉
  - for scrolling simple grid
    - dhtmlX: 25
    - devExtreme: 38
    - ag-grid: 57
    - extjs: 59
    - brytum: 60
  - for scrolling grid with pinned
    - dhtmlX: 19
    - devExtreme: 29
    - ag-grid: 53
    - extjs: 54
    - brytum: 59

## The simplest way to create a Data Grid in React - Tabelify

- [The simplest way to create a Data Grid in React_201606](https://medium.com/myntra-engineering/the-simplest-way-to-create-a-data-grid-in-react-ccdd4368ee7a)
  - [react-tabelify](https://github.com/rishabhbits038/react-tabelify)
    - /NALic/28Star/201606

- We finally decided to create our own library 'Tabelify' from scratch.
- Tableify is a highly customisable library that can be used to display data in different formats. 
  - Tabelify is a controlled react component. 
  - Its parent has complete control over its state.
  - Any change in tabelify triggers an event, which can be caught at a central location. 
  - The required changes are made in the store/state and then modified data is passed to tabely as props.
- Some of the important ways to modify the way data is represented are:
  - Custom Columns: 
    - User can pass a render method as params in `columnMetadata` . 
    - The method renders a custom column.
  - CustomRow: 
    - User can choose not to display the data in a tabular format as well. 
    - The user can pass a `CustomRow` as a prop to Tabelify. 
    - Tabelify renders the Custom Row instead of the default.
    - `CustomRow` takes in the data as props and the value it returns is rendered in the row
  - Similarly, user can also pass a `CustomHeader` and a `CustomFooter` to the table.
  - There is also an option to enable/disable the checkbox by just passing a flag
  - There is a search box at the bottom left of the grid. It filters the data and shows only the ones which contain the text typed.
  - Tabelify also supports pagination by default. 
  - It supports in build sort on columns.
  - A function ‘onRowClick’ is passed as a callback to Tabelify which returns the row data when a it is clicked. Appropriate actions can be performed on it.
- Tablelify takes in data as props. Whenever a change is to be trigerred, tableify return the event along with the updated data to its parent via a callback onChangeGrid.
- react component tree diagram of Tabelify
  - GridHeader
  - GridRows
  - GridFooter
- any change in the header, footer or rows is passed on to the parent via callback(onChangeGrid)
  - onChangeGrid modifies the state of the page. 
  - The updated state is then passed on as props to tabelify which passes it down to each of the components and thus the updated values are rendered.
- To keep things simple, we kept the entire props to be passed to tabelify in a single json object, tableConfig, which it stores in the state.
- The entire state of tabelify is stored in the state of page in the variable tableConfig.
- Whenever there is some change inside the grid, onChangeGrid is called, which is a callback. 
  - It takes in event and the updated data as parameter. 
  - TableConfig is modified and setState is called. 
  - setState triggers rerender of the Page with updated state. 
  - Thus the updated values are passed on to Tabelify as well.

## React — Code Your Own DataTable Step by Step

- [React — Code Your Own DataTable Step by Step (Video Tutorial by udemy)](https://codeburst.io/react-code-your-own-datatable-step-by-step-video-tutorial-34fca0ca34e7)
  - [udemy-react-datatable](https://github.com/rajeshpillai/udemy-react-datatable)
    - /NALic/9Star/201810
- Code a working version of a simple data table using no 3rd party library and using pure React.
- The following features are covered in the tutorial
  - Binding data to the datatable dynamically
  - Sorting
  - Searching on multiple columns/fields
  - Pagination with customization
  - Reorder columns by dragging and dropping
  - Custom Cell renderer using Render prop pattern
  - Basic CRUD template
  - ...

## Building a Data Table Component in React

- [Building a Data Table Component in React_by polaris_201810](https://engineering.shopify.com/blogs/engineering/building-data-table-component-react)

- The Challenge
  - Must Be Responsive
    - Typically, responsive designs either stack or collapse elements at narrow widths
    - but these solutions break the grid structure of a data table
  - Must Be Readable
    - The purpose of the data table is to organize the information in a way that makes it easy for the users to compare and analyze
    - so proper alignment is important
  - Must Be Contextual
    - a well-designed data table that provides context around the information, preventing the user from getting confused by seemingly random cell values. 
    - This means keeping headings visible at all times so that whichever data a user is seeing, it still has meaning.
  - Must Be Accessible
    - Finally, to accommodate users with screen readers a data table needs to have proper semantic markup and attributes.

- Here’s how to create a stripped down version of the data table we built for Polaris using React
  - note: This post requires `polaris-react` .
  - 基于table标签和display:table布局实现
  - 基本功能有scroll, fixed column, variable height

- **Building a Data Table**
- ### Start With a Basic React Data Table
  - table-thead-tbody-tr-td
  - With this many columns, the width of the table exceeds the screen width and scrolls the entire document horizontally, which isn’t ideal.
  - One way to handle a wide table is to collapse the columns and make them expandable, but this solution only works with a limited number of columns. 
  - Beyond a certain number, the collapsed width of each column still exceeds the total screen width, especially in portrait orientation. 
  - The columns are also awkward to expand and collapse, which is a poor experience for users. 
  - To solve this, restrict the width of the table.

- ### Making it Responsive: Add Max-width
  - Wrap the entire table in a div element with `max-width: 100vw` and give the table itself `width: 100%` .
  - Unfortunately, this doesn’t work properly at very narrow screen widths when the cell content contains long words. 
  - The longest word forces the cell width to expand and pushes the table width beyond the screen’s right edge.
  - you can solve this with word-break: break-all, but that violates the design requirements to keep the data readable
  - So, the next thing to do is force only the table to scroll instead of the entire document.

- ### Making it Responsive and Readable: Create a Scroll Container
  - Wrap the `table` in a `div` element with `overflow: auto` to cause a scrolling behavior for the overflow content.
  - The data is difficult to understand without the context of the first column header 只能看到后几列
  - We chose to keep the first column visible at all times by fixing it in place and preventing it from scrolling along with the other columns as a solution.

- ### Adding Context: Create a Fixed First Column
  - Give each cell in the first column an explicit width, then position them with `position: absolute` and `left: 0` . 
    - Then add `margin-left: 145px` to the remaining columns’ cells (the value must be equal to the width of the first column cells).
    - Add `className='Cell-fixed'` to the first cell of each row.
  - Using an absolute position on each cell gives us a fixed first column, but creates another problem.
  - Typically, the DOM renders each cell height to match the height of the tallest cell in the same row, but this behavior breaks when the cells are positioned absolutely, so cell heights need to be adjusted manually.

- ### Fixing a Bug: Adjust Cell Heights
  - Absolute positioning converts the fixed column to a block and breaks the natural behavior of the table, so the cell heights no longer adjust according to the height of the other cells in their row. 
  - To fix this, pull the `clientHeight` value from both the fixed cell and the remaining cells for each row in the array. 
  - Write a function that uses `Math.max` to find the highest number (the tallest height) of each cell in each row and return an array of those values.
  - The `handleCellHeightResize()` is called after the component is mounted and is never called again unless the page is refreshed. This means the height values for each cell remain the same even if the window is resized.
  - Set up an event listener and call the function any time the window is resized, so the cell heights readjust.

- ### Making it Accessible
  - Two important attributes make a data table accessible. 
  - Add a `caption` that a screen reader will read and a `scope` tag for each cell. 
  - For more details, the a11y project has an article about how to create accessible data tables.

## ref

- [A React Data Grid Template Powered By ElasticSearch](https://medium.appbase.io/a-react-data-grid-template-powered-by-elasticsearch-a-react-data-grid-template-powered-by-10b21609b67b)
  - build a data grid app from ground up using ReactiveSearch, react-virtualized, and ElasticSearch.
- [How to Make a Data Grid Scale_201708](https://www.smartly.io/blog/how-to-make-a-data-grid-scale)
  - Find the right tools: react-virtualized
  - make it scroll 
- [基于 Angular Material 的 Data Grid 设计实现](https://zhuanlan.zhihu.com/p/150868481)
  - declaration, row selection, expandable row, column hide 
