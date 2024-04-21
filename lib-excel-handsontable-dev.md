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
  - 有很多公开插件，如formula
  - 支持virtual-render
  - Merge cells
  - Freeze rows/columns
  - Define custom cell types
  - Add comments to cells
  - Non-contiguous selection
  - 使用table标签和布局，而不是div，enhanced semantics, good for a11y, SEO 
  - Auto fill: Dragging fill handle to populate data
  - Drag rows or columns to swap them 
  - Stretching: Allow columns to the parent container width

- cons
  - 🐛 model-view的架构不清晰
    - 非immutable的架构,不modern，可直接通过指针修改data+手动render
    - 非immutable的架构对从外部更新数据和视图不友好
  - ~~没有对外notify changes的功能~~
  - v6未实现batch，最新版支持; 不支持 transaction
  - 视图层更新时渲染粒度很粗，full rerender, 基于virtual-render使得渲染成本低
  - 事件系统依赖domElement.dispatchEvent
  - non-commercial
  - 💰 paid: Filtering, Collapsing columns, hiding row/col
    - Formulas, Gantt Chart, Nested rows, Nested headers
  - no group/aggregations
  - ? cell只支持string和number，不支持date

- features
  - cell-types: Dropdown, Select, Checkbox
  - Alignment
  - Autocomplete
  - Sorting
  - Data validation
  - Conditional formatting
  - Moving rows/columns
  - Resize rows/columns
  - Context menu
  - Highlighting current row/col
  - Scroll: Use native scrollbars to navigate within the table
  - Internationalization

- who is using #handsontable
  - growi(hot.v6)

- dev-xp
  - mutable data before v8
# draft
- handsontable该如何与使用contenteditable的文本编辑器结合
  - 需要改造事件的dispatch机制

- 当container的height未设置时, 若设置了minRows/minCols，尝试为container设置默认高度和overflow:hidden
# dev

# changelog

## v14.0.0_20231130

- [What’s new in Handsontable 14: Improvements to accessibility](https://handsontable.com/blog/whats-new-in-handsontable-14-improvements-to-accessibility)
  - In this release, we’ve introduced features to enhance the overall accessibility of Handsontable, ensuring it meets WCAG 2.1 AA standards
  - A big update is that you can now use your keyboard to navigate through row and column headers
  - We’ve also improved support for screen readers like JAWS, NVDA, and VoiceOver by expanding the HTML markup with ARIA attributes.

## v13.0.0_20230622

- [Handsontable 13.0.0: Support for Angular 16, and new frameworks-support policy](https://handsontable.com/blog/handsontable-13-0-0-support-for-angular-16-and-new-frameworks-support-policy)
  - This version adds support for Angular 16, cleans up a few long-deprecated methods, and introduces a more transparent policy toward older versions of supported frameworks.
  - When a maintainer drops support for an old framework version, we will drop it in the nearest major or minor release of Handsontable – we won’t treat it as a breaking change.
  - When we drop support for an old version of any framework, we’ll provide 18 months of long-term support (LTS) for it

## v12.0.0_20220428

- [Handsontable 12.0.0: RTL support, and a new keyboard shortcuts API _202204](https://handsontable.com/blog/handsontable-12.0.0-data-grid-rtl-support-and-a-new-keyboard-shortcuts-api)
  - This version adds support for right-to-left (RTL) languages, introduces a new API for managing keyboard shortcuts, and improves the behavior of the `updateSettings()` method.
  - The RTL direction is applied automatically through the inheritance of the `dir` attribute from the HTML element. You can also control it programmatically, using a new configuration option: `layoutDirection`.

## v11.0.0_20211117

- [Handsontable 11.0.0: Modularization for React, Angular, and Vue _202111](https://handsontable.com/blog/handsontable-11.0.0-modularization-for-react-angular-and-vue)
  - This version adds modularization features to the framework wrappers, improves the monorepo structure, adds a new locale option, and more.
  - Since Handsontable 8.3.0, you’ve been able to use modules with the vanilla JavaScript version of Handsontable. 
  - Now, you can use modules with each of Handsontable’s framework versions (React, Angular, and Vue) as well.
  - Ever since we introduced modularization in Handsontable 8.3.0, we wanted to give every module full TypeScript support.

## v10.0.0_20210929

- [Handsontable 10.0.0: Improved performance and consistency](https://handsontable.com/blog/handsontable-10.0.0-improved-performance-and-consistency)
  - One of the biggest changes in Handsontable 10.0.0 is the improved performance of the `getCellMeta()` method.
  - Because getCellMeta() gets called very often from different parts of Handsontable’s source code, and its performance may impact the overall efficiency of your grid.
  - To achieve this, we introduced an additional cache layer that gets cleared once every slow render cycle.
  - While working on the getCellMeta() cache layer, we noticed an inconsistency in some of the related hooks: beforeRender and afterRender. To clear things out, we decided to rename them, and add two new hooks along the way

## v9.0.0_20210601

- [Handsontable 9.0.0: New formula plugin _202106](https://handsontable.com/blog/handsontable-9.0.0-new-formula-plugin)
  - The new formula plugin is now out! It integrates our powerful calculation engine – HyperFormula
  - Up to version 8.4.0 there was a formula plugin that was built by us based on two other projects: our own formula parser, and an external library of spreadsheet functions, called formula.js. The problem with this solution was that we couldn’t easily extend or improve it.
  - We also ran into some performance issues which required a completely different approach in the way we parse formulas and build AST, as well as calculate and recalculate input data.
  - In 2018 we started working on a new formula engine. We named it HyperFormula and, once it was ready, published it on GitHub under an open-source license. At that point, we started to incorporate it into Handsontable

## v8.0.0_20200805

- One of the breaking changes in 8.0.0 is:
  - 🚨 Modifying the table’s data by reference and calling `render()` will not work as it used to anymore. 
  - From this point onward, all the data-related operations need to be performed using the API methods, such as `populateFromArray` or `setDataAtCell`.

- Handsontable 8.3.2: Introducing monorepo

- Ever since we introduced modularization in Handsontable 8.3.0, we wanted to give every module full TypeScript support.

- [The new Handsontable 8 is now available](https://handsontable.com/blog/the-new-handsontable-8-is-now-available)
  - We redesigned the internal data flow, which determines the flawlessness and speed of the core engine and plugins. Thanks to the new architecture, the library is now less error-prone and provides a solid foundation for future developments.
  - Even though the functionality has been extended by new methods and hooks, we added zero new features. New features are great, but no matter how hard you try, it’s almost impossible to make them bug-free. That is why we decided to take a break from the feature creep and focus solely on improving the existing features.
  - The new management system for translating the physical indexes to visual indexes stabilizes the way that plugins exchange information about the order and states of the records in the data set.
  - Since the dependency of callbacks was removed, the plugins are more independent and easier to use.
  - We added the `setSourceDataAtCell` method and `modifySourceData` hooks, and thanks to that modifying the data by reference is no longer necessary.
  - The `ObserveChanges` plugin is now deprecated and we plan to remove it in the future. It performs a deep comparison of two objects in a loop and attempts to find the differences between them. However, this operation is inefficient and prone to errors. The same results can be now achieved by using the API methods, which are much more efficient.

- [Need a way to update source data in filtered state ](https://github.com/handsontable/handsontable/issues/6680)
  - v8.0.0 from beta.2 introduces `setSourceDataAtCell` to modify source data and it's using physical indexes / object props.

## v7.0.0_20190306

- 💰 Starting with version 7.0.0, there is only one Handsontable, as Handsontable Pro has been merged with Handsontable Community Edition.
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
  - This release contains changes to the `ColumnSorting` plugin exclusively
  - refactored and rewrote parts of the ColumnSorting plugin in order for it to work seamlessly with the new MultiColumnSorting plugin
  - Added a new plugin - `MultiColumnSorting`.
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
