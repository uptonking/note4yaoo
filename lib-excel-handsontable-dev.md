---
title: lib-excel-handsontable-dev
tags: [handsontable, lib]
created: 2020-08-06T05:37:04.641Z
modified: 2022-08-21T09:57:32.451Z
---

# lib-excel-handsontable-dev

# guide

- pros
  - features rich and open source

- cons
  - ? cell只支持string和number，不支持date

- features
  - ?
# dev

# changelog

## v7.0.0_20190306

- Starting with version 7.0.0, there is only one Handsontable, as Handsontable Pro has been merged with Handsontable Community Edition.
  - Handsontable is now "source-available" instead of "open source". 
  - **The MIT license has been replaced with custom, free for non-commercial license**.

- Removed the deprecated `selectCellByProp` method
- Added the possibility to declare the table’s width/height using relative values (%, vh, vw, rem, em).
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

## v6.0.0_20180927

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

## v5.0.0_20180711

- Refactored the Custom Borders plugin
  - added new methods such as getBorders, setBorders and clearBorders
- Added an ability to disable Byte Order Mark (BOM) while exporting table to the CSV file. 

## v4.0.0_20180613

- Changed the default values for the following configuration options
  - autoInsertRow (was: true, is: false)
  - autoWrapCol (was: false, is: true)
  - autoWrapRow (was: false, is: true)
- Updated our number-handling dependency, Numbro to the latest version

## v3.0.0_20180516

  - Column Sorting plugin is over the first stage of refactoring

## v2.0.0_20180411

  - Rewritten the Search and Custom Borders plugins to ES6.
  - Added the beforeContextMenuShow hook, triggered within the Context Menu plugin
  - Added extra parameters for the beforeFilter and afterFilter hooks
  - The corresponding Handsontable CE version is 2.0.0.

## v1.0.0_20160120

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

## v0.x_20110524

- Data Grid Component with Spreadsheet Look & Feel
- built with jquery
# more
