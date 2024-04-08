---
title: lib-excel-handsontable-blog
tags: [blog, handsontable]
created: 2024-04-08T17:14:50.416Z
modified: 2024-04-08T17:14:58.459Z
---

# lib-excel-handsontable-blog

# guide

# blogs

## 🚀📈 [Tabulator – Easy-to-use JavaScript library for interactive tables _201811](https://news.ycombinator.com/item?id=18568072)

- It seems standard that all of these JS table libraries are rendering using `<div>` elements instead of a `<table>` element. Why? As far as I can tell, all of the features could be implemented using the correct HTML element rather than using `<div>` to mimic a table.

- 🌰 Let me preface my answer by saying im the chap(对男子的友好称呼，家伙，伙计) that built Tabulator
- This is because the `<table>` element introduces a lot of design constraints.
  - There is a lot of inherent styling that would have to be overridden if a `table` element was to be used. 
  - It could also mess with the standard behaviour of other table elements that have been generically styled.
- Importantly when you start building interactive complex tables, there are 100's of different types of elements needed to make the table function correctly that a standard HTML element simple isn't designed to handle, event making the header and the body scroll separately requirements more elements that a standard table can handle 
  - and it would invalid HTML to use the tags inside the table that would be needed to achieve it.
  - Especially when you move into the world of the virtual DOM, a standard table element simply wont cut it
  - With the inclusion of aria tags, there are no accessibility issues as screen readers treat them just as any other tables.
- For Tabulator the virtual DOM is essential. 
  - If you try and load 10, 000 rows into a table either the browser will slow down and become almost unusable or crash entirely.
  - For large data sets it makes the table work regardless of the number of rows
- What if you just chunk your DOM writes into small batches, and then put them into a queue, which is then consumed within a requestAnimationFrame() handler?
  - A bit of indirection, but not nearly as much as a complete virtual DOM. (I assume this would result in the table "slowly" populating, but the browser and the page should both remain responsive.)
  - You can can do this but for large data sets it would take ages and doesnt over come the main issue.
  - Yes loading that many elements into the DOM is slow and your approach would stop it blocking, however what it doesnt do is stop the sheer(大量的，陡峭的) number of elements from overloading the DOM.
  - Most browsers simply cant handle that many elements in the DOM, if you try and scroll a div containing that may elements at best it will be sluggish and at worst it will simply crash the browser. 
  - on devices without much memory it is very likely that the whole DOM will freeze up and make the site unusable.
- By adding and deleting the elements as they become visible/hidden, it keeps the number of elements in the DOM to a minimum, while improving load time and adding only a bit of extra processing to the scroll event, which modern browsers can handle with ease. giving all round the best solution

- Olifolkerd, I would love to know more about Tabulator's approach to supporting multiple frameworks, please.
  - on the whole the key is to stick to vanilla JS and avoid trying to use to forcible a design paradigm that could conflict with other frameworks.
  - Removing dependencies on other libraries was key to making it interoperable.
  - Everything in Tabulator is built to be extensible so where an incompatibility exists it is easy to build a solution for a particular framework.
  - Tabulator still has one hangup in the way it works, in that it doesnt use reactive data (changing the array you passed into the table, does not automatically update the table, unlike react and view, you have to bind watchers at the moment) but this will be coming in the next release. at which point they should all work harmoniously
  - The biggest challenge is to ensure that things are drawn correctly at the correct time. 
  - 💡 Because Tabulator uses a virtual DOM it makes it a since to redraw parts of the table when needed
  - I wrote my own VDOM library, Tabulator has zero dependencies for its core functionality

- 👷🏻📈 Author of Handsontable, here. We actually use `<table>` , but there are many things that are easier with `<div>` :
  - With `<div>` , you have complete control over the positioning of the cells. 
    - With `<table>` , you delegate(委托，选派) the layout to the browser engine. 
  - `<table>` has lots of semantic meaning, which makes it slower to render than a `<div>` , because the browser engine needs to make a sense of it. 
    - There are differences in how `<table>` s are rendered in various browsers. 
    - This is especially a problem with old browsers such as IE6. 
    - `<table>` element is much more complex to process than a `<div>` .
    - Is this really slower overall? 
    - `<table>` is one of the few elements that actually have a dedicated "Processing model" section in the spec
    - It is not neccessarily a bottleneck, as long as your datagrid library uses the browser's ability to render the table. 
    - But if you want a custom look and feel, such as overlapping cells, irregular shaped cells, animated cells, it's far better to do it based on `<div>` s instead of fighting the browser engine.
    - This is why you need to use a virtual DOM to prevent the DOM from being filled with elements that consume memory and slow it down
    - it’s a real technique to render only a subset of elements that fit on ~2 screen lengths and swap them out as the user scrolls for arbitrarily large tables. Just using virtual dom doesn’t magically solve this but it does make doing things like this parlor trick easier IMO.
  - It is trickier to implement things like floating headers, virtual scrolling with `<table>`
  - Still, Handsontable uses `<table>` because you can overcome these problems if you're motivated enough. 
    - The biggest benefit is that `<table>` gives you enhanced semantics, which are good for Accessibility, SEO or any other form of code processing.
    - In addition to that, using `<table>` gives you out-of-the-box Excel file export because `.xlsx` files (which are basically zipped XML files) support HTML tables.
- 🤔🆚️ Could use use `<table>` for the semantics but set `display:block` to get `<div>` style layout?
  - the problem is it isnt just the table element, it is the thead, tbody, td, th elements as well
  - Complex interactive tables need a great number of elements to make them run and these wont conform(v, 遵守，服从) to the standards of using a table (you cant just put a div inside a tbody element) but that is exactly what you would need to get a table with a virtual DOM to work correctly.
  - There are a lot of different styling tweaks that would need to be overridden for each element, some of which arent consistent across each browser.
  - 💡 Also people have a tendency to put styles on the generic `table` tab to style tables across the site. if Tabulator was to then be used on the page, it could have any number of unknown CSS properties set on it, so would essentially have to look at overriding all possible style properties.
  - where as no one generically styles divs or spans and they come with very little built in styling making them the ideal choice for a library that wants to keeps its functionality isolated from the rest of the site
- table libraries using table tags:
  - handsontable, datatables.net(for jQuery)

## [hansontable编辑器 _201807](https://blog.csdn.net/qianqianyixiao1/article/details/80925480)

- handsontable分离了cell value的显示displaying和修改altering，renderer负责displaying，editor负责altering
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

## [使用handsontable插件修改bug心得 | 堂的博客](https://jintang.github.io/2016/10/18/%E4%BF%AE%E6%94%B9handsontable%E6%8F%92%E4%BB%B6%E5%BF%83%E5%BE%97/)

- 开发者工具查看绑定事件，找到可以搜索的关键字：click、mousedown、mouseup、edit、select、render
  - 搜索关键字，在觉得有可能影响的地方都打上断点，如果关键字是方法，那调用它的地方都有可能影响
  - 开始苦逼的调试，在触发哪个断点的时候导致了bug发生
  - 是否由包含该断点的方法里的步骤导致的，使用全局变量，在该步骤处”拨乱反正”

- 总结: 不清楚插件内部逻辑的情况下, 搜索关键字，根据打的断点找到关键性代码

## [4 Ways to Handle Read-only Cells](https://handsontable.com/blog/4-ways-to-handle-read-only-cells)

- When a cell is set to read-only, then:
  - It is immutable for changes
  - A cell editor doesn’t open
  - It has a new class name (htDimmed) which paints it gray
  - It doesn’t trigger beforeChange and afterChange callbacks
  - It can’t be changed via the context menu to editable if set in the cellsconfiguration
  - It still can be selected
  - It still can be copied

- Read-only: entire spreadsheet
- Read-only: columns only
- Read-only: rows only
- Read-only: certain cells
# blogs-collab
- [Build: Real-Time Collaborative Spreadsheets App | PubNub _201904](https://www.pubnub.com/blog/collaborative-spreadsheets-using-pubnub/)
# blogs-perf

## [Performance - JavaScript Data Grid | Handsontable](https://handsontable.com/docs/javascript-data-grid/performance/)

- Handsontable performs multiple calculations to display the grid properly. 
  - The most demanding actions are performed on load, change, and scroll events. 
  - Every single operation decreases the performance, but most of them are unavoidable.

- Set constant row and column sizes
- Turn off autoRowSize and/or autoColumnSize
- Define the number of pre-rendered rows and columns
  - You can explicitly specify the number of rows and columns to be rendered outside of the visible part of the table. 
- Rule of thumb: don't use too much styling
- Suspend rendering
  - By default, Handsontable will call the render after each CRUD operation. Usually, this is expected behavior, but you may find it slightly excessive in some use cases. 
  - By using one of the batching methods, you can suspend rendering and call it just once at the end. 
- 
- 

# more
