---
title: lib-excel-handsontable-docs
tags: [changelog, docs, list, table]
created: 2019-08-01T16:03:46.386Z
modified: 2022-08-21T09:57:36.123Z
---

# lib-excel-handsontable-docs

# guide

# overview
- rowHeights/colWidths能够设置各行/各列的高度/宽度的默认值，也是最小值
- stretchH能使表格充满容器宽度，且各列水平均分

- handsontable大小尺寸
  - Handsontable by default fills its nearest parent element which has a defined `width` ,  `height` and the CSS `overflow` property set to `hidden` .
    - Having that, you can expand your Handsontable to the window’s dimension and use the native scrollbars to navigate through the grid.
  - If you provide height only and decide to leave the width indefinite, then the spreadsheet will expand to the window’s full width (or any parent element with defined dimensions and `overflow: hidden` )
  - If you set only the table’s width, it won’t render properly until you use the `preventOverflow` option. 
    - By setting it to horizontal your spreadsheet will have the width of a parent container and the height of the window. 
    - Scrollbars will appear if needed. 
    - Basically, the `preventOverflow` option prevents the table from overflowing the parent container in the provided dimension, in this case – horizontal.
    - If there are no height and width settings passed in the configuration, the table will vertically and horizontally fill the entire window (again, or any parent element with defined dimensions and `overflow: hidden` ).
    - you can change the size dynamically any time after the initialization by using the `updateSettings` code to update the dimensions.
  - ref
    - [A Complete Guide to Changing the Size of Handsontable](https://handsontable.com/blog/articles/2016/3/a-complete-guide-to-changing-size-of-handsontable)

- To set up Handsontable DOM structure in your application, you have to define its container as a starting point to initialize component.
  - Usually, the `div` element becomes this container. 
  - This container should **have defined dimensions** as well as the rest of your layout. 
  - If container is a block element, then its parent has to have defined height. By default block element is 0px height, so 100% from 0px is still 0px.
  - Since v7.0.0, Handsontable supports relative units such as %, rem, em, vh, vw or as exact size in px.
- Handsontable looks for the closest element with `overflow: auto` or `overflow: hidden` to use it as a scrollable container. 
  - If no such element is found， a window will be used.
- If you don't define dimensions, Handsontable will generate as many rows and columns to fill available space and will also provide full support for virtual rendering and fixed parts.
- Since v7.0.0 we observe window resizing. 
  - If the window's dimensions have changed, then we check if Handsontable should resize itself too. 
  - Due to the performance issue, we use debounce method to response on window resize.
- ref
  - [Grid sizing](https://handsontable.com/docs/7.4.2/tutorial-grid-sizing.html)

- **Walkontable** is the return value of many methods but not mentioned in the docs
  - Walkontable is for internal use only. 
  - It used to be a separate library, but now it is included to HOT repository and it's core functionality is to render HTML table.
  - Walkontable table renderer was refactored on 20190705.
    - This change introduces new files and code structures, which makes table rendering easier to maintain. 
    - In this approach, every TABLE element which can hold children is rendered separately by an individual unit called internally `OrderView` . 
    - A specialized renderer wraps each unit.
    - This change helps us to implement an EcoRendering idea

- What is eco-rendering
  - This issue is about implementing a new feature internally called as `EcoRenderers` . 
  - The idea of this is to increasing Handsontable performance by re-rendering cells only when their value has changed. 
  - I assume that after implementing this feature issues related to scroll performance or refresh table lag after cell edit should recede
  - ref
    - https://github.com/handsontable/handsontable/issues/5769
    - https://github.com/handsontable/handsontable/pull/6089

- Currently the best way to style Handsontable is to use custom renderers.
- Links/click events from custom renderers not working 
# Known limitations
- It uses several dependencies
  - Our team follows the "proudly found elsewhere" principle which encourages us to make use of the great work done by other developers. 
  - numbro.js (handles numeric data)
  - Pikaday (displays a date picker)
  - moment.js (parses, validates and displays dates)
  - json-patch-duplex.js (implementation of JSON-Patch - RFC 6902)
  - jStat (statistical library)
  - tiny-emitter (a tiny event emitter library)
- [github-issues-most-commented](https://github.com/handsontable/handsontable/issues?q=is%3Aissue+is%3Aopen+sort%3Acomments-desc)
  - [cell is focusing, when focus in another input (modal)](https://github.com/handsontable/handsontable/issues/401)
  - [Issues with scrolling in a parent element](https://github.com/handsontable/handsontable/issues/3119)
  - [Fixing more columns than visible in the viewport breaks scrolling](https://github.com/handsontable/handsontable/issues/4259)
  - [Rewrite custom borders to use SVGs instead of DIVs](https://github.com/handsontable/handsontable/issues/6467)
# dev
- handsontable分离了cell value的显示displaying和修改altering，renderer负责displaying，editor负责altering。
  - renderer是function，接受实际值，返回html
  - editor较复杂，是class，负责处理输入及数据验证

- EditorManager 管理所有的editor，在调用handsontable()构造方法时，EditorManager object会实例化，EditorManager 包含4类task
  - 为当前单元格选择合适editor
      - 查找当前cell的editor属性，找到editor class并实例化
      - 在同一个table中，editor class是单例的
  - 调用editor object的prepare()
      - 用户每选择一个单元格，prepare()就被调用一次，选择同一单元格可能被调用多次
  - displaying editor，即对cell开启编辑
      - 触发条件是 ENTER、双击单元格 或 F2
      - 实际是调用editor object的beginEditing()
  - closing editor，即对cell关闭编辑
      - 触发条件是 ENTER、ESC、点击另一个单元格、上下左右箭头、TAB、HOME、END、PAGE_UP/DOWM
      - 实际是调用editor object的finishEditing()
- BaseEditor 是所有editor的抽象类基类，包含7个公共方法
  - prepare(): 设置属性
  - beginEditing(): 
  - finishEditing(): 
  - discardEditor(): cell验证结束时调用
  - saveValue(): 保存cal作为cell的新值
  - isOpened(): Editor is considered to be opened after open() has been called， closed after close() has been called.
  - extend(): 
- 每一个editor class自己该实现的方法
  - init(): 创建editor class实例时调用，每个table最多调用一次，常用于创建html的结构
  - getValue()：返回当前新值
  - setValue():
  - open(): Displays the editor.
  - close(): Hides the editor after cell value has been changed.
  - focus()： This method is called when user wants to close the editor by selecting another cell and the value in editor does not validate (and allowInvalid is false)
- editor实例的公共属性
  - instance：指当前editor所属的handsontable实例，不可变
  - row：当前cell的行索引
  - col：当前cell的列索引
  - prop：当前cell的相关属性名，only when data source is an array of objects
  - TD：当前cell的节点对象，类型是HTMLTableCellNode
  - cellProperties：代表当前cell所有属性的对象
- 自定义编辑器
  - PasswordEditor是扩展的TextEditor
  - SelectEditor通过继承BaseEditor来创建
  - Handsontable.editors.registerEditor()为editor创建别名，重名时后者覆盖前者

- 每个单元格都关联3个函数：renderer()、editor()、validator()
- 每个函数负责不同行为，可以分别定义3个函数，也可以使用cell type一次定义3个

- renderer()接受数据值和cell dom node，返回html，内置5个render
  - TextRenderer，默认renderer for all cells
  - NumericRenderer
  - AutocompleteRenderer
  - CheckboxRenderer
  - PasswordRenderer
- 在table渲染时，每个cell的renderer方法会被分别调用，在滚动、排序或单元格编辑时，table可能会被多次渲染，因此renderer()应使用简单方法来避免性能问题
- 每个cell的renderer()方法可能会被调用多次，这可能导致监听事件重复
- 当滚动或增删行列时，会重用单元格，此时可能发生事件绑定到错误的单元格
- 推荐使用 handsontable events system，若必须自定义事件，则将cell内容包裹在 `<div>` 中，再给div添加监听器
- Handsontable renders only the visible part of the table plus a fixed amount of rows and columns. 

- editor()

- validator()：cell validator既可以是方法，也可以是正则表达式
  - Contrary to renderer and editor functions, the validator function doesn't have to be defined for each cell.
  - 若validator()未定义，则默认valid

- 可以使用getCellMeta(row, col) method to get all properties of particular cell and then refer to cell functions
  - cellProperties.renderer; // get cell renderer
  - cellProperties.editor; // get cell editor
  - cellProperties.validator; // get cell validator
- 当使用cell type定义3个方法时，getCellMeta()取到的3个方法均为undefined，此时可以直接使用
  - getCellRenderer(row, col)
  - getCellEditor(row, col)
  - getCellValidator(row, col)

- 内置9种cellTypes

```
text for Handsontable.cellTypes.text
numeric for Handsontable.cellTypes.numeric
checkbox for Handsontable.cellTypes.checkbox
date for Handsontable.cellTypes.date
time for Handsontable.cellTypes.time
dropdown/select for Handsontable.cellTypes.dropdown
autocomplete for Handsontable.cellTypes.autocomplete
password for Handsontable.cellTypes.password
handsontable for Handsontable.cellTypes.handsontable
```

- 自定义cellType的方法
  - Handsontable.cellTypes.registerCellType()
- cell type name若重复，则后者覆盖前者
- text是默认type
- 可以覆盖type的renderer、editor、validator

- 性能调优
  - 可以尝试将表格的列宽设置为常量值
  - Turn off autoRowSize and/or autoColumnSize
  - Define the number of pre-rendered rows and columns，可以显式指定非可见区域的行列
  - 不要使用过多的样式，特别是动画、过渡
  - always prefer removeNode() over innerHTML = ''
  - forEach and filter are MUCH slower than for
  - Get first element using DOM `getElementsByTagName('span')[0]` or `firstChild`
  - Create text elements: createTextNode can be many times faster than innerHTML
  - Check if element has child nodes: if (DIV.firstChild)
  - Change style by caching var style = element.style

- handsontable基本用法

```js
var container1 = document.getElementById('example1'),
  settings1 = {
    data: data1
  },
  hot1;

hot1 = new Handsontable(container1, settings1);
data1[0][1] = 'Ford';
hot1.render();
```

- 要想改变数据后立即显示，需要调用render()
- handsontable支持的数据源    
  - 数组的数组
  - 对象的数组
  - 嵌套对象的数组
  - 自定义schema
  - 自定义schema函数
- AJAX is used to load and save grid data
- 建议使用 persistentState hooks rather than a regular LocalStorage API，便于隔离同一个页面上多个handsontable的数据
- Cascading Configuration model is based on prototypal inheritance
  - constructor
    - columns
    - cells
- Constructor options -> columns -> cells -> cellProperties
- handsontable.js 与 handsontable.full.js的区别
  - 代码压缩程度不同

- demo摘要
  - select是dropdown的简化版
  - You'll need horizontal scrollbars, so just set a container width and `overflow: hidden` in CSS.
  - fixed指定前几行前几列，freeze手动指定某一列，且freeze要和context menu一起使用
  - 扩大列宽或行宽的方法，拖拽列的右边或行的下边，双击这些地方会自动调整size
  - Pre-populating rows 可以为行预定义数据模板
  - StretchH可以自动调整列宽
  - 列排序插件作为数据源和render之间的代理，并未修改数据源
  - 排序3方式：点击header、columnSorting属性、直接调用插件的sort()
  - search默认大小写不敏感
  - search本质是基于indexOf()
  - render前都要validate
  - auto fill 向下拖动时默认复制，双击十字图标会自动复制到最长的列
  - 可以向4个方向拖动，拖出区域时，会自动添加列/行
  - Alignment changes can be tracked using afterSetCellMeta hook callback.
  - readonly后可以键盘导航和复制，不能粘贴到cell或编辑cell，拖动不能覆盖
  - disallow editing 可以复制粘贴，可以拖动
  - cell和header都支持context menu
  - 可以通过code选择单元格、增删行列
  - copy&paste **暂不支持** 样式，只支持字符串
  - checkbox copy之后是true
  - linux 不能使用ctrl多选
# more
