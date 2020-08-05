---
title: docs-ag-grid
tags: [ag-grid, docs, grid, list, table]
created: '2020-07-14T13:01:37.940Z'
modified: '2020-08-05T04:35:33.164Z'
---

# docs-ag-grid

## ag-grid表格组件ui结构层次

- ag-root-wrapper: 最顶层容器，ref是eRootWrapper
  - ag-root-wrapper-body
    - ag-tab-guard-top
    - **ag-root**: 这里是grid component的根组件
      - ag-header
        - ag-pinned-left-header
        - ag-header-viewport: 这里是表头内容
        - ag-pinned-right-header
      - ag-floating-top: 所有子节点都没有text
      - ag-body-viewport
        - ag-pinned-left-cols-container
        - ag-center-cols-clipper: 这里是内容区
          - ag-center-cols-viewport
            - ag-center-cols-container
              - ag-row
              - **ag-row**: 行组件
                - **ag-cell**: 最内层单元格，内容直接是文字
              - ag-row
        - ag-pinned-right-cols-container
        - ag-full-width-container: 无text
      - ag-floating-bottom
      - ag-body-horizontal-scroll
      - ag-overlay
    - ag-tab-guard-bottom
  - ag-paging-panel: 默认隐藏分页组件

``` CSS
.ag-root {
  position: relative;
  flex: 1 1 auto;
  display: flex;
  /* 竖向放置header，body，paging */
  flex-direction: column;
  width: 0;
  height: 100%;
  overflow: hidden;
}

.ag-header {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 100%;
  min-height: 49px;
  overflow: hidden;
}

.ag-body-viewport {
  position: relative;
  flex: 1 1 auto;
  display: flex;
  /* 水平放置左固定列，表格内容，右固定列 */
  flex-direction: row;
  min-width: 0;
  height: 100%;
  overflow: hidden;
  overflow-y: auto;
}

.ag-center-cols-clipper {
  /* 父元素ag-body-viewport，是flex容器 */
  display: block;
  flex: 1;
  min-width: 0;
  min-height: 100%;
  height: 361956px;
  overflow: hidden;
}

.ag-center-cols-viewport {
  /* 父元素ag-center-cols-clipper，是display block */
  position: relative;
  flex: 1 1 auto;
  display: block;
  min-width: 0;
  width: 100%;
  /* height开始是100% */
  height: calc(100% + 15px);
  overflow: hidden;
  overflow-x: auto;
}

.ag-center-cols-container {
  position: relative;
  display: block;
  width: 1590px;
  height: 361956px;
}

.ag-row {
  position: absolute;
  top: 42*Npx;
  display: block;

  width: 100%;
  height: 42px;

  transition: background-color .1s;
}

.ag-cell {
  position: absolute;
  left: 200*Npx;
  display: inline-block;

  width: 200px;
  /* height实际是41px */
  height: 100%;
  overflow: hidden;
  border: 1px solid transparent;

  line-height: 40px;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

- ### ag-grid的row span基于z-index实现
  - 给需要合并的单元格元素中第一个元素加上class: cell-span ag-cell-focus
    - 必需设置背景，如果background不设置，则默认transparent，仍可以看见下层单元格
  - 同时使用行内样式控制第一个单元格的高度，主要是增加单元格的高度来模拟合并单元格的视觉效果 
    - `style="width: 200px; left: 0px;  height: 84px; z-index: 1;"`
  - 对除第一个单元格外的其他单元格，不需要处理样式，作为普通单元格显示，但被第一个单元格挡住了
  - ref
    - [ag-grid row spanning simple example preview](https://www.ag-grid.com/example-runner/grid-vanilla.php?section=javascript-grid-row-spanning&example=row-spanning-simple)

``` CSS
.rowspan-cell-style {
  z-index: 1;
  position: absolute;
  left: 200*Npx;
  display: inline-block;

  width: 200px;
  /* height实际是84px */
  height: 40*spanpx;
  white-space: nowrap;
}

.cell-span {
  background-color: #00e5ff;
}

.ag-cell-focus {
  /* 为空 */
}
```

- ### ag-grid的column span基于position-absolute实现
  - 使用行内样式控制合并后单元格的宽度
    - `style="width: 600px; left: 0px;"`
    - 合并后单元格显示的位置由行内样式left控制
  - 合并列后的单元格在源码上是位于ag-row一行单元格的最后面的，然后通过 `colindex=3` 可设置其列顺序
  - 对于某些没有合并列单元格的行ag-row，其单元格在源码上的顺序仍然在一行的最后，对应其他行被合并的位置上
    - 至少被合并的那列单元格是在最后
    - 紧跟着的那列也在最后

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

## DOM Virtualisation

- https://www.ag-grid.com/javascript-grid-dom-virtualisation/

- The grid uses DOM virtualistaion to vastly improve rendering performance.
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
