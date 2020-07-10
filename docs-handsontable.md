---
tags: [changelog, docs/handsontable]
title: docs-handsontable
created: '2019-08-01T16:03:46.386Z'
modified: '2020-07-10T02:32:14.667Z'
---

# docs-handsontable

## dev-tips

- rowHeights/colWidths能够设置各行/各列的高度/宽度的默认值，也是最小值
- stretchH能使表格充满容器宽度，且各列水平均分
- handsontable大小尺寸
  - Handsontable by default fills its nearest parent element which has a defined width, height and the CSS overflow property set to hidden.
  - If there are no height and width settings passed in the configuration, the table will vertically and horizontally fill the entire window (again, or any parent element with defined dimensions and overflow: hidden).
  - you can change the size dynamically any time after the initialization by using the updateSettings code to update the dimensions.
  - 参考 https://handsontable.com/blog/articles/2016/3/a-complete-guide-to-changing-size-of-handsontable

## faq

- **Walkontable** is the return value of many methods but not mentioned in the docs
  - Walkontable is for internal use only. 
  - It used to be a separate library, but now it is included to HOT repository and it's core functionality is to render HTML table.
- Currently the best way to style Handsontable is to use custom renderers.
- Links/click events from custom renderers not working 

## resources

- docs
  - https://handsontable.com/docs

## handsontable docs

- handsontable分离了cell vaule的显示displaying和修改altering，renderer负责displaying，editor负责altering。
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
- 推荐使用 handsontable envents system，若必须自定义事件，则将cell内容包裹在<div>中，再给div添加监听器
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

``` js
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
  - You'll need horizontal scrollbars, so just set a container width and overflow: hidden in CSS.
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

## changelog

- 7.0.0-20190306
  - Starting with version 7.0.0, there is only one Handsontable, as Handsontable Pro has been merged with Handsontable Community Edition.
  - Handsontable is now "source-available" instead of "open source". The MIT license has been replaced with custom, free for non-commercial license.
  - Removed the deprecated selectCellByProp method
  - Added the possibility to declare the table’s width/height using relative values (%, vh, vw, rem, em).
      - https://github.com/handsontable/handsontable/issues/5749
  - Added the beforeTrimRows and beforeUntrimRows
  - Refactored the following classes to ES6 
      - BaseEditor
      - AutocompleteEditor
      - HandsontableEditor
      - SelectEditor
      - TextEditor
      - Walkontable -> Event
      - EditorManager
      - MultiMap
      - TableView
      - DataMap
- 6.2.2-20181219
  - Updated babel to 7.x
  - Corrected the CSS property assignment to zero from 0 to '0'
- 6.2.0-20181114
  - Added the Korean, Latvian language support
  - Updated the TypeScript definition file for ColumnSorting, MultiColumnSorting, beforeColumnMove
  - Refactored the columnSorting plugin to be reusable with the multiColumnSorting plugin
  - Refactored the multiColumnSorting plugin to use the columnSorting plugin
- 6.1.0-20181017
  - Moved the fixedRowsBottom functionality to Handsontable CE
  - Introduced a new functionality to the Copy/Paste plugin. From version 6.1.0, it supports the text/html data type alongside text/plain
- 6.0.0-20180927
  - This release contains changes to the ColumnSorting plugin exclusively
  - refactored and rewrote parts of the ColumnSorting plugin in order for it to work seamlessly with the new MultiColumnSorting plugin
  - Added a new plugin - MultiColumnSorting
  - Added a possibility to disable the action of sorting by clicking on the headers, using the headerAction option
- 5.0.0-20180711
  - Refactored the Custom Borders plugin
      - added new methods such as getBorders, setBorders and clearBorders
  - Added an ability to disable Byte Order Mark (BOM) while exporting table to the CSV file. 
- 4.0.0-20180613
  - Changed the default values for the following configuration options
      - autoInsertRow (was: true, is: false)
      - autoWrapCol (was: false, is: true)
      - autoWrapRow (was: false, is: true)
  - Updated our number-handling dependency, Numbro to the latest version
- 3.0.0-20180516
  - Column Sorting plugin is over the first stage of refactoring
- 2.0.0-20180411
  - Rewritten the Search and Custom Borders plugins to ES6.
  - Added the beforeContextMenuShow hook, triggered within the Context Menu plugin
  - Added extra parameters for the beforeFilter and afterFilter hooks
  - The corresponding Handsontable CE version is 2.0.0.
- 1.18.0-20180314
  - Removed the mobile editor from the repository. After this version, a standard editor will be used when using mobile devices
  - Added a cellProperties argument for the beforeValueRender hook.
- 1.14.0-20170912
  - Since version 1.14.0, it is required to pass a valid Handsontable Pro license key in the settings object under the licenseKey property
  - The corresponding Handsontable CE version is 0.34.2.
- 1.11.0-beta1-20170517
  - Migration from Traceur to Babel. We're now using Babel to transpile our code.
- 1.0.0-20160120
  - Backward incompatible change 
  - Prevent displaying the dropdown header buttons in higher levels of headers (for example, when using the nested headers plugin).

  
