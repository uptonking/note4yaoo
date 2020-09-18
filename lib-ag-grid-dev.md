---
title: lib-ag-grid-dev
tags: [ag-grid, dev, grid, lib]
created: '2020-08-10T06:07:14.084Z'
modified: '2020-09-17T17:17:12.914Z'
---

# lib-ag-grid-dev

## ag-grid表格组件ui结构层次

- ag-root-wrapper: 最顶层容器，ref是eRootWrapper
  - ag-root-wrapper-body
    - ag-tab-guard-top
    - **ag-root**: 这里是grid component的根组件
      - ag-header
        - ag-pinned-left-header
        - ag-header-viewport: 这里是表头内容
          - ag-header-container
            - ag-header-row/ag-header-row-column
              - ag-header-cell
                - ag-header-cell-resize
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

- AgGridReact组件会在ag-root-wrapper外层添加一个div `<div style="height: 100%;">`

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

## 功能实现细节

### 滚动条

- 滚动条一直显示的问题。It's no a bug, its a feature. 
  - A scrollbar appears if the total width count of all columns is bigger than your wrapper. 
  - You should change minWidth/maxWidth property of columnDefs' headerFields and you will be fine.
  - Side note: If the grid data is changed due to scope changes or not initial defined, you need to recall `sizeColumnsToFit()` in a new diggest circle like `setTimeout(() => {this.gridApi.sizeColumnsToFit();});` .
  - The best fix I found was to call `sizeColumnsToFit` in the `onModelUpdated` event handler. 
  - ref
    - [unnecessary horizontal scroll bar coming in spite of using sizeColumnsToFit in ag-grid](https://stackoverflow.com/questions/47454302/unnecessary-horizontal-scroll-bar-coming-inspite-of-using-sizecolumnstofit-in-ag)

### 注解装饰器元数据的使用

- __agComponentMetaData.constructorName.querySelectors

### row span基于z-index实现

  - 给需要合并的单元格元素中第一个元素加上className: `cell-span ag-cell-focus`
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

### column span基于position-absolute实现

  - 使用行内样式控制合并后单元格的宽度
    - `style="width: 600px; left: 0px;"`
    - 合并后单元格显示的位置由行内样式left控制
  - 合并列后的单元格在源码上是位于ag-row一行单元格的最后面的，然后通过 `colindex=3` 可设置其列顺序
  - 对于某些没有合并列单元格的行ag-row，其单元格在源码上的顺序仍然在一行的最后，对应其他行被合并的位置上
    - 至少被合并的那列单元格是在最后
    - 紧跟着的那列也在最后
