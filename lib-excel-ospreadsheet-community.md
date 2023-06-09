---
title: lib-excel-ospreadsheet-community
tags: [community, ospreadsheet]
created: 2023-06-07T22:37:30.774Z
modified: 2023-06-07T22:37:47.793Z
---

# lib-excel-ospreadsheet-community

# guide

# issues
- ## 

- ## [[IMP] commands: Introducing TRANSACTION to batch commands](https://github.com/odoo/o-spreadsheet/pull/1682)
  - Unfortunately, dispatching several commands from the outside means different entries in the history stack; meaning we won't be able to undo/redo the commands together.
  - doesn't and won't work. it cannot handle the allowdispatch of other commands. We need to find another approach

- ## [[IMP] find_and_replace: sheet granularity in Find & Replace](https://github.com/odoo/o-spreadsheet/pull/2330)
- Previously, the find and replace functionality only worked on the active sheet, which made it difficult to determine if the content was available in any other sheet or to replace content in all sheets.
- the code has been updated to search for content in all available sheets and replace it in all sheets.

- ## [[IMP] add history in CoreView plugins](https://github.com/odoo/o-spreadsheet/pull/2408)
- add history to some CoreView plugins

- ## [[IMP] selection: drag and drop selection on the grid](https://github.com/odoo/o-spreadsheet/pull/1023)
- Add a new component named "selection" allowing to cut/paste a selection by grabbing and moving it.

- ## [Can extract data from the sheet](https://github.com/odoo/o-spreadsheet/issues/2030)
- I just set my model mode from headless to normal and it worked but only for
one sheet while the evaluated data in other sheets shows 'Loading'

- ## [Possible to use formula parser as a backend library?](https://github.com/odoo/o-spreadsheet/issues/2187)
- owl is a frontend library but can be used in the backend. While the App of owl is not mounted, it should be good.

- we tried to install the library as a backend (full nodejs app) and it cannot run as it is. 
  - the data model is relying on the owl library as well, which simply cannot run on a nodejs server because it uses the web API. Sorry for misleading you. 
  - However, we are currently considering different approaches to make the lib backend-only asap.
# discuss
- ## 

- ## [[IMP] spreadsheet: Add data filters](https://github.com/odoo/o-spreadsheet/pull/1447)
- It is now possible to create tables in
sheets that allow to filter the rows that contain certain values.
  - Add a Filter plugin that manage the data of the filters and adapt their zone with the grid modification. 
  - A new UI plugin FilterEvaluation will keep track of which rows are currently filtered by the defined filters.
  - The core plugin will manage the col/row hidden by the user, and the UI plugin will combine these with the filtered rows. 
  - Many visibility getters are thus moved in UIGetters and cannot be accessed in core plugins.

- ## [Master allow dispatch UI plugin generic adrm](https://github.com/odoo/o-spreadsheet/pull/2364)
- Before this commit, local commands were going through the allowDispatch
of core plugins. This wasn't a problem per se, but was wrong from an
architecture standpoint, core plugins shouldn't be aware of what's
happening locally. This also made it so that zones/ranges of local commands
missing a sheetId (because it is implicitly the active sheet) weren't
checked.

- ## [[IMP] Convert AST to formula string and batch row deletions](https://github.com/odoo/o-spreadsheet/pull/480)
- With this commit, consecutive rows are deleted in batch, reducing cell visits.

- ## [[REF] range: Remove rows and columns in batch](https://github.com/odoo/o-spreadsheet/pull/708)
- To speed up the process, we remove consecutive rows/columns in one go
