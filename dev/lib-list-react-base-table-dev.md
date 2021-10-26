---
title: lib-list-react-base-table-dev
tags: [grid]
created: '2020-08-09T12:49:34.732Z'
modified: '2021-05-13T02:51:13.937Z'
---

# lib-list-react-base-table-dev

# BaseTable表格组件ui结构层次

- BaseTable/--fixed
  - BaseTable__table/-main
    - BaseTable__body
      - div(height10000,width1500)
        - BaseTable__row/--customized
        - BaseTable__row 
          - BaseTable__row-cell
        - BaseTable__row 
    - BaseTable__header
  - BaseTable__overlay

``` CSS
.BaseTable {
  position: relative;
  box-sizing: border-box;
}

.BaseTable__table {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  /* 因为源码顺序上body在前header在后，这里能使header在body之上 */
  flex-direction: column-reverse;
}

.BaseTable__body {
  position: relative;
  height: 350px;
  width: 700px;
  overflow: auto;
  will-change: transform;
  direction: ltr;
  outline: none;
}

.BaseTable__body>div {
  width: 1500px;
  height: 10000px;
}

.BaseTable__row {
  position: absolute;
  left: 0px;
  top: 0px;
  display: flex;
  align-items: center;
  width: 1500px;
  height: 50px;
}

.BaseTable__row-cell {
  position: static;
  /* 单元格的宽度使用width决定，不放大，也不缩小 */
  flex: 0 0 auto;
  display: flex;
  align-items: center;
  width: 150px;
  height: 100%;
  padding: 0 7.5px;
  /* padding-left: 15px; */
  overflow: hidden;
}
```

# 功能实现细节

- row是flex container
- col span
  - 合并后的单元格 `width` 为 `N*150px`
  - 所有单元格作为行容器的flex item都有 `flex: 0 0 auto;`
- row span
  - 基于z-index实现，合并后的第一个单元格的样式，通过行内样式style object设置
  - 下一行同一位置的元素就是普通单元格，被作为合并后单元格的第一个挡住了，在DevTools中可以选中
  - ag-grid也是基于z-index实现

``` CSS
.rowspan-cell {
  z-index: 1;
  position: static;
  flex: 0 0 auto;
  align-self: flex-start;
  display: flex;
  align-items: center;
  width: 150px;
  /* 这里是两行的高度 */
  height: 99px;
  overflow: hidden;
}
```

# issues

- [pr: Row select and customized row select with prop feature](https://github.com/Autodesk/react-base-table/pull/39)
  - I'd say I didn't include selection feature to BaseTable on purpose, as there are different behaviors for that, and I want to keep BaseTable unopinionated
- [表头分组，并且支持fixed和拖动配置有什么好的方案吗](https://github.com/Autodesk/react-base-table/issues/198)
  - 我的意思是表头分组，我这样实现了以后 ，调整列大小用不了了，设置fixed={false}后 表头和表内容会对不齐
  - 因为merged cell width是直接根据 `style.width` 来的，对于 `fixed={false}` 的情况，width其实并不是真实的宽度，因为是flex布局，是个好问题，之前从来没考虑过这种情况，我们内部是必须 `fixed={true}` 的时候才能用column groups， `fixed && columnGroups && !Array.isArray(headerHeight) && !headerRenderer && headerGroupHeight` ; 
  - 感觉想不到比较好的解决办法，因为在flex布局下，每个cell的宽度都是自动计算的，里面还涉及flexGrow/flexShrink/flexBasis的情况，唯一能想到的方法就是去取渲染后每个cell的真实宽度，然后再render group cell，这里就必须用 `flex: 0 0 widthpx` 了，不过还是感觉有点复杂

# roadmap

- ## [Roadmap for V2.0](https://github.com/Autodesk/react-base-table/issues/3)
  - Don't use Grid for table header
  - Replace react-virtualized with react-window 
  - remove deprecated lifecycles #10
  - Dynamic row heights #170
  - Make virtualization configurable
