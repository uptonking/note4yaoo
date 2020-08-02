---
title: note-pm-list-grid-table-dev
tags: [dev, grid, list, product, table]
created: '2020-07-13T13:34:22.833Z'
modified: '2020-07-26T04:15:29.049Z'
---

# note-pm-list-grid-table-dev

## api

- ### react-table
  - required-props: data, columns
  - data: 必需，类型是 array of objects
  - style: 自定义
  - ui实现：自定义，headless
  - note
    - 基于react实现，react only 
    - 用于方便实现ui的工具: useBlock/Absolute/FlexLayout
      - 不同布局需要的条件不一样，如BlockLayout需要指定宽度
- ### ag-grid
  - required-props:rowData, columnDefs, 父元素width, height
  - data: 必需，类型是 array of objects
  - style: ag-grid.css, ag-theme-alpine.css
  - ui实现：div-flex
  - note
    - 基于js实现，可用于react/vue/angular
- ### handsontable
  - required-props: 都是非必需，宽高也是非必需
  - data: 非必需，类型可以是array of arrays, array of objects, 还可以将columns值设为函数再计算处理后返回列信息
    - 不传入data时，会显示占满父元素的空格表格
    - 可以通过columns设置处理方式，从nested object的属性中取值
  - style: handsontable.full.css
  - ui实现: 基于table, tr, td和display-table-cell
  - note
    - 从自身向父元素查找带有width,height和 `overflow:hidden` 的元素并占满
- ### react-virtualized
  - required-props: cellRenderer, width, height，rowCount, rowHeight, colCount, colWidth
    - cellRenderer is responsible for rendering a single cell, given its row and column index.
  - data: 必需，间接通过cellRenderer传入
  - style: styles.css, ReactVirtualized__Grid
  - ui实现: div-position-absolute
  - note
    - Grid row heights and column widths must be calculated ahead of time and specified as a fixed size or returned by a getter function.
    - `List` uses a `Grid` internally to render the rows and all props are relayed to that inner `Grid`
    - `Table` Component is created with flexbox. 
      - This allows it to have a fixed header and scrollable body content. 
      - It also makes use of `Grid` for windowing table content so that large lists are rendered efficiently
- ### react-window
  - required-props:children, width, height, rowCount, rowHeight, colCount, colWidth
  - data: 必需，通过react component的children传入，类型自定义
    - 要能在children中通过rowIndex,colIndex获取
  - style: 无内置，需要自定义
  - ui实现: div-flexbox
  - note
    - VariableSizeGrid的colWidth和rowHeight值类型都是函数
- ### react-data-grid

## usage

``` JS
// demo for ag-grid
// two essential configuration properties of the grid - the column definitions (columnDefs) and the data (rowData).
import { AgGridReact } from 'ag-grid-react';
import 'ag-grid-community/dist/styles/ag-grid.css';
import 'ag-grid-community/dist/styles/ag-theme-alpine.css';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      columnDefs: [
        { headerName: "Make", field: "make" },
        { headerName: "Model", field: "model" },
        { headerName: "Price", field: "price" }
      ],
      rowData: [
        { make: "Toyota", model: "Celica", price: 35000 },
        { make: "Ford", model: "Mondeo", price: 32000 },
        { make: "Porsche", model: "Boxter", price: 72000 }
      ]
    }
  }

  render() {
    return (
      <div className="ag-theme-alpine" style={ {height: '200px', width: '600px'} }>
        <AgGridReact
            columnDefs={this.state.columnDefs}
            rowData={this.state.rowData}>
        </AgGridReact>
      </div>
    );
  }
}

render(<App />, document.getElementById('root'));
```

``` JS
// demo for react-virtualized
import React from 'react';
import ReactDOM from 'react-dom';
import { Grid } from 'react-virtualized';

// Grid data as an array of arrays
const list = [
  ['Brian Vaughn', 'Software Engineer', 'San Jose', 'CA', 95125],
  // And so on...
];

function cellRenderer({ columnIndex, key, rowIndex, style }) {
  return (
    <div key={key} style={style}>
      {list[rowIndex][columnIndex]}
    </div>
  );
}
// Render your grid
ReactDOM.render(
  <Grid
    cellRenderer={cellRenderer}
    columnCount={list[0].length}
    columnWidth={100}
    height={300}
    rowCount={list.length}
    rowHeight={30}
    width={300}
  />,
  document.getElementById('example'),
);
```

``` JS
// demo for react-window
import { FixedSizeList as List, FixedSizeGrid as Grid } from 'react-window';

const Row = ({ index, style }) => (
  <div style={style}>Row {index}</div>
);

const Example = () => (
  <List
    height={150}
    itemCount={1000}
    itemSize={35}
    width={300}
  >
    {Row}
  </List>
);

const Cell = ({ columnIndex, rowIndex, style }) => (
  <div style={style}>
    Item {rowIndex},{columnIndex}
  </div>
);

const Example = () => (
  <Grid
    columnCount={1000}
    columnWidth={100}
    height={150}
    rowCount={1000}
    rowHeight={35}
    width={300}
  >
    {Cell}
  </Grid>
);
```

``` JS
// demo for handsontable
import React from 'react';
import { HotTable } from '@handsontable/react';
import 'handsontable/dist/handsontable.full.css';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.data = [
      ["", "Ford", "Volvo", "Toyota", "Honda"],
      ["2016", 10, 11, 12, 13],
      ["2017", 20, 11, 14, 13],
      ["2018", 30, 15, 12, 13]
    ];
  }

  render() {
    return (
      <div id="hot-app">
        <HotTable data={this.data} colHeaders={true} rowHeaders={true} width="600" height="300" />
      </div>
    );
  }
}
```

## summary

- 如何区分click和double click
  - setTimeout
- infinite scroll vs pagination
  - An infinite scroller is a modern alternative to pagination.
  - Rather than wait for the user to click 'next page', new content is automatically loaded everytime the user reaches the bottom of the page. 
  - 手动实现无限滚动的方法
    - 在componentDidMount方法中this.refs.myscroll.addEventListener("scroll",f)
    - 在滚动事件处理函数中判断，若到达底部，则触发请求新数据，再setState
  - pagination ux vs infinite scroll + search/filter
- infinite scroll vs regular scroll
  - 无限滚动因为在开始时渲染的DOM元素较少而性能较高，在滚动时会不停地添加列表项到列表元素，一旦滚动数量过多，仍会由于DOM节点过多造成样式计算或DOM操作开销大，性能就变差了
  - 无限滚动最好还是结合virtualized使用，在每次scroll事件触发时请求数据
- 列表类组件开发常见问题
  - 是否使用virtualized/window来显示可滚动的表格
    - 虚拟化要求定高，可参考react-window的VariableSizeList提供的解决方案
  - 一个单元格或一行数据的更新会触发整个表格的重新渲染
    - 虽然调用了render方法，真实更新的DOM不一定是所有元素节点
    - 可考虑mini store进行数据分片
    - react-table generates a key for row-group div (trGroup). As a result only the rows that are "actually" updated are re-rendered
    - 使用window来显示数据，就算每次重新渲染整个表格，代价也不会特别高
      - With virtual views, data is rendered only in active viewport 
      - element are added/removed upon scroll reducing the rendering/reconciliation payload
      - The *cells and rows are properly keyed* to allow React to only re-render what has changed. If it is causing performance issues then you may need to consider a different package.
  - 使用**table/tr/td**标签还是使用div来显示列表
      - even minor changes will cause reflows of all other nodes in the table
      - div based table is faster in rendering, animation and reflow
      - 使用tr-td会使后面实现drag,resize,sort ,group更复杂
      - ref
        - https://developer.mozilla.org/en-US/docs/Archive/Table_Reflow_Internals
        - http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/
- 列表组件开发难点
  - try to avoid scroll events, especially if they’re not debounced
    - react-intersection-observer falls back to scroll events *only* if necessary
  - 虚拟滚动时如何实现拖拽排序动画
- virtualized or window
  - List virtualization, or "windowing", is the concept of only rendering what is visible to the user. 
  - The number of elements that are rendered at first is a very small subset of the entire list and the "window" of visible content moves when the user continues to scroll. 
  - This improves both rendering and scrolling performance of the list.
  - "Virtualizing" a list of items involves maintaining a window and moving that window around your list. 
  - virtualization focuses on rendering just items visible to the user.
  - 参考
    - https://addyosmani.com/blog/react-window/
