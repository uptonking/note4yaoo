---
title: lib-excel-handsontable-issues
tags: [handsontable, issues]
created: 2024-04-21T12:51:14.185Z
modified: 2024-04-21T12:51:25.525Z
---

# lib-excel-handsontable-issues

# guide

# issues-stars
- ## 

- ## 

- ## [nested rows doesn't work with loadData _201611](https://github.com/handsontable/handsontable/issues/3914)
- The remaining part of the issue has been already described by #7138 and added as a part of the scope of Interoperability problems between Nested Rows and some core features 

# issues-not-yet
- ## 

- ## 

- ## 

- ## [Is partial rendering possible? _202101](https://forum.handsontable.com/t/is-partial-rendering-possible/4921)
  - is it possible to only re-render affect cells so that I don’t lose my editor?

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
# issues
- ## 

- ## 

- ## 
# issues-done
- ## 

- ## 

- ## 🗑️ [Split `loadData` into `updateData` and `setData` _202009](https://github.com/handsontable/handsontable/issues/7263)
- loadData is reinitializing all states kept internally in Handsontable

- [Remove the redundant `setData` method _202201](https://github.com/handsontable/handsontable/issues/9095)
  - we decided to remove the `setData` method (planned to be released in 11.1.0), as it doesn't introduce much value when compared to `loadData`.
  - [Remove the `setData` method and replace it with the previously-used `loadData`](https://github.com/handsontable/handsontable/pull/9096)

- ## [How to trigger a click on a handsontable row/cell? - Stack Overflow _202004](https://stackoverflow.com/questions/61325139/how-to-trigger-a-click-on-a-handsontable-row-cell)
- handsontable can't listen to click because the click is fired after a full click action occurs; that is, the mouse button is pressed and released
  - `mousedown` is fired the moment the button is initially pressed. 

- [Can I trigger a click event on a cell manually? _202004](https://github.com/handsontable/handsontable/issues/6822)
  - A single click on a cell only results in a cell selection. You do not need to fake the click event to achieve this goal - you can call instance.selectCell(row_index, column_index). 

- ## [[GL #153] Extra row added after refresh data ](https://forum.handsontable.com/t/gl-153-extra-row-added-after-refresh-data/364)
- I have configured the handsontable to have one min spare rows, it is working fine if I didn’t reload my data. Recently, I am having a requirement to reload the data from a REST service, when the data come back from the server i am using `hotInstance.updateSettings({data: data});` to update the data into datasheet. Then there will always an extra row in my datasheet.

- This issue is fixed with version 8.0.0-beta1 http://jsfiddle.net/w87rjc0b/

- [Blank Rows in Middle of Grid [PRO] ](https://github.com/handsontable/handsontable/issues/3937)
  - I can confirm that initializing with data and minSpareRows in one go works, but initializing and adding the data after does not work. 
  - Once initialized the right way updating the data seems to work fine.
