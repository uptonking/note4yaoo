---
title: lib-excel-tanstack-table-dev-v7
tags: [tanstack-table]
created: 2023-05-10T13:04:26.124Z
modified: 2023-05-10T13:04:37.492Z
---

# lib-excel-tanstack-table-dev-v7

# guide

# v7

## react-table表格实现的ui结构层次

### useFlexLayout
- div-table
  - div-thead
    - row-tr
    - row-tr
      - columnheader
    - row-tr
  - div-tbody
    - row-tr
    - row-tr
      - cell
    - row-tr

```CSS
.table {
  min-width: 735px;
  border-spacing: 0;
  border: 1px solid black;
}

/* todo flex without container 表头行和数据行的样式 */
.row-tr {
  flex: 1 0 auto;
  display: flex;
  min-width: 215px;
  border-bottom: 1px solid black;
}

.cell,
.columnheader {
  position: relative;
  flex: 150 0 auto;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  box-sizing: border-box;
  width: 150px;
  min-width: 30px;
  padding: 0.5rem;
  margin: 0;
  border-right: 1px solid black;
}

.tbody {
  display: block;
  height: 250px;
  overflow-x: hidden;
  overflow-y: scroll;
}

.cell {}
```

### useBlockLayout

> 必须设置cell的width，使用行内样式设置

- div-table
  - div-thead
    - row/tr
    - row/tr
      - columnheader/th
    - row/tr
  - div-tbody/rowgroup
    - row/tr
    - row/tr
      - cell/td
    - row/tr

```CSS
.table {
  display: inline-block;
  border-spacing: 0;
  border: 1px solid black;
}

/* 设置表头行或数据行 */
.row {
  display: flex;
  width: 710px;
}

.cell,
.columnheader {
  display: inline-block;
  box-sizing: border-box;
  width: 150px;
  margin: 0;
  padding: 0.5rem;
  border-bottom: 1px solid black;
  border-right: 1px solid black;
  /* font-weight: bold; */
}

.rowgroup {}

.cell {}
```

# v6
