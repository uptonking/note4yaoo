---
title: lib-excel-handsontable-community
tags: [community, data-grid, handsontable]
created: 2023-12-21T20:07:08.898Z
modified: 2023-12-21T20:07:29.584Z
---

# lib-excel-handsontable-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔💡 [What is the proper way to update data that has been returned from an API call after the table was already initialized/constructed? _202001](https://forum.handsontable.com/t/what-is-the-proper-way-to-update-data-that-has-been-returned-from-an-api-call-after-the-table-was-already-initialized-constructed/4030)
  - What is the best/proper way to reload the hands on table data with the data source that has come back from an API call to the server. 

- From what I know, I can think of 3 options:
  - Use hot.updateSettings({data: updatedData}); 
  - Use hot.loadData(updatedData); 
  - Use code to update the existing data collection which Handsontable is configured to reference to have all of the updates from the server. 

- there’s one more method (but if you load more than a few cells it is too overwhelming for the browser) - it’s the `setDataAtCell` method. It also triggers the `render()` method but it won’t change the sorting or filtering that is already applied.
  - Besides that the `loadData()` and updateSettings > data already call the render() method.
  - The same rules apply when you change the data via reference - the `loadData` for the same variable reloads the table without an additional render() call 

- ## 🐛 [Redux/Immutability issues _202005](https://github.com/handsontable/handsontable/issues/6909)
- The data provided to Handsontable is mutated on plugin instead of being only updated in the internal structure when using redux we need to block using Immutable data structures, this is not good to deal with.
- The thing is that mutating data in React is a bad practise and we get no control over it also when using Redux the data is only changed via a reducer action. With the time i see Handsontable doesn't support very well basic concepts nor React

- in AgGrid i can disable that because they notify me of that change and i can say to update internally or not and in that callback, i would update on redux and prevent the editing internally.

- ## [Update particular cell in Handsontable - Stack Overflow](https://stackoverflow.com/questions/33435741/update-particular-cell-in-handsontable)
- Re-rendering the entire table is the only way Handsontable will allow you to render and it's there for a few good reasons. 
  - First off, it doesn't matter how large your table is since there is virtual rendering in use. This means that it will only render what you can see plus a few more rows. 
  - The other reason why it renders everything from scratch is that it's Handsontable's way of keeping a stateless DOM object. If you started manually rendering specific cells then you could end up with an out of sync looking table.

- ## [Cell Double-Click and Supressing "Edit on Double Click" _201903](https://forum.handsontable.com/t/cell-double-click-and-supressing-edit-on-double-click/3081)
- you can use a native js event. 

- ### [Cell on double click event _201702](https://github.com/handsontable/handsontable/issues/4087)
  - Is there any possible way to execute a method when you double click on a cell?

- We do not provide any Handsontable double click event.
  - you could track `afterOnCellMouseDown` event. Write down the last clicked element and check the time between clicks. 

- ## [I’m surprised there’s not a `contenteditable` option for the renderer?](https://forum.handsontable.com/t/table-cell-styling-and-edit-styling/3216/5)
- The `contenteditable` works for DIV but Handsontable works on TD elements.
  - 如果添加了，那hot的事件拦截逻辑要进行很大的修改

- ## [Handsontable v6.2.2 doc is removed _202403](https://forum.handsontable.com/t/handsontable-v6-2-2-doc-is-removed/7490)

# issues-done
- ## 

- ## 

- ## [How to trigger a click on a handsontable row/cell? - Stack Overflow _202004](https://stackoverflow.com/questions/61325139/how-to-trigger-a-click-on-a-handsontable-row-cell)
- handsontable can't listen to click because the click is fired after a full click action occurs; that is, the mouse button is pressed and released
  - mousedown is fired the moment the button is initially pressed. 

- [Can I trigger a click event on a cell manually? _202004](https://github.com/handsontable/handsontable/issues/6822)
  - A single click on a cell only results in a cell selection. You do not need to fake the click event to achieve this goal - you can call instance.selectCell(row_index, column_index). 
# issues-not-yet
- ## 

- ## 

- ## [Is partial rendering possible? _202101](https://forum.handsontable.com/t/is-partial-rendering-possible/4921)
- We are planning to add an ability to partially render cells, but this hasn’t been finished yet. Maybe you can try to
  - save the editor value
  - re-render the table to change the background
  - open editor again
  - place the saved value into the editor

- batch doesn’t allow us to rerender only a single cell but it allows us to block the whole rendering process for some particular task.
- ## [Grouping and ungrouping of rows or columns _201405](https://github.com/handsontable/handsontable/issues/1463)
- Grouping and ungrouping of rows or columns - in the same way as availabe in Excel
  - Released in Handsontable 0.11.4 

- 201711: We have abandoned the grouping feature. Now we use only nested headers and rows. If you want to collapse columns you can use collapsing.
# discuss-collab
- ## 

- ## [setDataAtCell inside useEffect _202309](https://forum.handsontable.com/t/setdataatcell-inside-useeffect/7138)
  - I am trying to get handsontable to work with websockets to allow multi-user editing. 
  - I have a listener for changes to the selection and that works great, and I can set the border etc. as expected. 
  - But trying to update the cell using hot.setDataAtCell(e.row, e.column, 'test test', 'websocket') does not update the table.
  - The only way I have found to work around this, is to call the update webhook in a `setInterval` , which seems quite brittle
  - So I finally got it working. Simply moved all logic into `afterInit()` and stopped using `useState` in any way at all. Just plain js objects and arrays, set inside that the init function.

- ## [Collaboration guide ](https://github.com/handsontable/handsontable/discussions/8517)
- currently we are not in business of answering these topics.

- ## 🔀 [Remove non used dependencies jsonpatch in v9 _202106](https://github.com/handsontable/handsontable/issues/8140)
- Since the `ObservedChanges` plugin has been removed recently there are still some artifacts in the source code that should be removed. 
  - The `jsonpatch` internal lib is no longer used and can be safely removed. Probably the dependency list on docs should also be updated.

- [Fixed ObserveChanges plugin memory leak ](https://github.com/handsontable/handsontable/pull/4710)

- ## [Hot to use setDataAtCell while editing a cell and not get blured _202103](https://forum.handsontable.com/t/hot-to-use-setdataatcell-while-editing-a-cell-and-not-get-blured/5068)
  - I’m working on a collaborative sheet, basically someone could change the data of his sheet and broadcast the change to everyone else, and I’m using setDataAtCell to do that.
  - And the problem occurs when you are editing a cell, meanwhile setDataAtCell triggered to set the value of another cell, then you’ll lost focus on the cell and what you’ve been editing.

# discuss-perf
- ## 

- ## 

- ## [Alternative of setDataAtCell  _202008](https://forum.handsontable.com/t/alternative-of-setdataatcell/4641)
- If you are running the `setDataAtCell` method 1000 times in the run I recommend changing the source data and use `loadData()` afterwards. It will result in 1 call to Handsontable instead of 1000.

- ## [Performance issue: splicing source data with observeChanges/columnSorting triggers "observe change" on all data that comes after the spliced index ](https://github.com/handsontable/handsontable/issues/5274)
- It looks like the `observeChanges` is used to perform proper sorting after adding or removing rows. It fires for `afterCreateRow` and `afterRemoveRow` hooks.

# discuss
- ## 

- ## 

- ## 

- ## [Programatically updating data in Handsontable 11.1 - Getting help / Questions - Handsontable Forum _202205](https://forum.handsontable.com/t/programatically-updating-data-in-handsontable-11-1/6128)
  - In our app we only use this kind of methods to improve performance and to not have to reload the whole table at each and every external change or side effect changes
- 
- It’s expected behavior while using `updateData` method to alter the rows as it does not reset index mapper information and the rows indexes are being changed when you are adding the new ones. 
  - `loadData` however do this and let you add the new rows this way.
- Expanded nestedRows is their default state, that’s why after adding/deleting the rows they are expanded again. You can alter this behavior by using `collapseAll()` method.

- using loadData() method instead of updateData() as the first one was created specifically for React in mind and works correctly in most cases.

- ## [Rendering and Scrolling Slow for Large Tables _201606](https://github.com/handsontable/handsontable/issues/3591)
- Virtual scrolling will mitigate this by only creating those elements that are actually visible to the user, which greatly improves performance.

- ## [Virtual rendering for columns doesn't seem to work _201603](https://github.com/handsontable/handsontable/issues/3364)
- Handsontable triggers virtual rendering if there are more columns than visible + defined by `viewportColumnRenderingOffset` . When I changed your grid's width to 200px it worked.

- ## 🤔 [WTF is a Walkontable?_201508](https://github.com/handsontable/handsontable/issues/2716)
- Walkontable is for internal use only. It used to be a separate library, but now it is included to HOT repository and it's core functionality is to render HTML table.

- ## 💰 [Handsontable drops open source for a non-commercial license | Hacker News_201903](https://news.ycombinator.com/item?id=19488642)

> "Essentially, [Handsontable] was kept running thanks to the money earned from Handsontable Pro. Unfortunately, our observation is that the ratio of commercial to free users is about 1 to 25. Hence, the only way for us to keep investing in the product is to convert more free users into paying."

- About ag-Grid and Handsontable... I am founder of another JavaScript Grid product. FancyGrid. I know much about this market and situation. 
  - ag-Grid is too popular and trampled all competitors over catching almost all possible commercial clients. It is unreal to compete with them, they killed this market and become monopolist. 
  - Handsontable has no way to do. Now ag-Grid also is going to kill JavaScript Chart Libraries market. 
  - Sorely ag-Grid is too successful and leaves no chance for competitors to survive.

- We ( https://sheetjs.com/ ) started from a series of open source projects and offer a slew of related solutions
  - The ratio of customers to open source users is largely useless. 
  - To "convert" users, you need to offer something above and beyond what is available in the open source offering.
  - Unless you have something compelling, people won't "convert" out of altruistic desires. 
  - Unfortunately that's not how business works. 

- ## 🚀 [Handsontable - Excel-like table editor in HTML & jQuery | Hacker News_201206](https://news.ycombinator.com/item?id=4162808)
- There is also Dan Bricklin's socialcalc https://github.com/DanBricklin/socialcalc which has some relatively active forks including audreyt's ethercalc
  - For just viewing and editing spreadsheets without social features, you can ignore the servers included, the javascript widget works just fine by itself.
  - Dan Bricklin co-authored VisiCalc, the first spreadsheet program for the masses.

- `contentEditable` is a terrible hack and difficult to use when you only want a subset of features. You need to blacklist a bunch of events like pasting, keyboard formatting (e.g. ctrl+i, drag and drop and inserting new lines.
