---
title: lib-excel-spreadjs-dev
tags: [excel, spreadjs]
created: 2022-08-24T10:48:04.246Z
modified: 2022-08-24T10:48:29.318Z
---

# lib-excel-spreadjs-dev

# guide

- demos
  - [Rows and Columns](https://www.grapecity.com/spreadjs/demos/features/worksheet/rows-and-columns/purejs)
  - [custom toolbar](https://www.grapecity.com/spreadjs/spreadsheet/)
  - [Web Designer](https://demo.grapecity.com.cn/SpreadJS/WebDesigner/)

- resources
  - [spreadjs技术博客](https://www.grapecity.com.cn/blogs/categories/spread)
  - [SegmentFault D-Day 技术分享：葡萄城电子表格技术__202108](https://www.grapecity.com.cn/blogs/spreadjs-segmentfault-d-day)
# discuss
- ## 

- ## 

- ## [spreadJS designer source code_202007](https://www.grapecity.com/forums/spreadjs/spreadjs-designer-source-code)
  - How to integrate it into reactJS?

- Currently, the Designer is built as a standalone application using VanillaJS, JQuery, and Knockout. So if you need to use it inside a react application, you would have to create a react wrapper around the designer to use it in the react.
# docs
- [SpreadJS Designer Component](https://www.grapecity.com/spreadjs/docs/spreadjs_designer_component)
  - The designer components include ribbon, formula bar, status bar, side panel, and context menu. 

- [Introduction to the SpreadJS Designer Component_202011](https://www.grapecity.com/blogs/introduction-to-the-spread-designer-component)
  - we now also offer a new separate designer add-on component that is highly customizable, flexible, and could be easily embedded into your web application.
  - Although the new designer UI looks like the previous designer, it is a significant upgrade over its predecessor in terms of usability and customization.
  - Pure JS component
  - Easily customizable using JSON config files.
# blogs-spreadjs

## [葡萄城 SpreadJS 前端表格技术分享_202007](https://zhuanlan.zhihu.com/p/164731403)

- 针对前端表格开发的三大技术难点：性能、内存消耗和可靠性，SpreadJS分别提出了应对措施：
  - 基于双缓存画布绘制引擎，SpreadJS实现了极高的处理性能
    - 使用缓存画布
    - 类似油画的分层绘制
  - 基于行模式的稀松矩阵存储策略，SpreadJS可大幅节省内存消耗
  - 基于计算引擎技术，SpreadJS可实现稳定可靠的应用系统

## [如何写成高性能的代码（三）：巧用稀疏矩阵节省内存占用 - 掘金](https://juejin.cn/post/7160964641063960612)

- [电子表格实战锦囊: 巧用稀疏数组是关键! - 掘金](https://juejin.cn/post/7046958838100492318)

- [用时间置换空间，聊聊稀疏数组的那些事儿 - 掘金](https://juejin.cn/post/7012806847048450078)

## [前后端结合解决Excel海量公式计算的性能问题 - 掘金](https://juejin.cn/post/7169405648491249701)

1．读取模型之前，先用GcExcel在后端打开。在后端进行完整的计算。 
2．前端根据所展示的Sheet工作表，从后端读取对应的工作表并序列化进行传输。
3．前端SpreadJS禁用公式计算，设置计算按钮改为触发式计算。
4．前端通过脏数据获取修改记录。
5．当主动点击计算或者切换工作表Sheet页签时触发请求，将修改记录发送后端，后端将修改内容修改并整体计算。再将结果根据前端所展示的Sheet做序列化处理并传输至前端。
6．前端进行反序列化处理展示。

## [葡萄城高性能表格技术优化实践](https://ke.segmentfault.com/course/1650000038945137)

- 性能优化实践
  - 减少垃圾回收
  - 共享存储和数据压缩
  - 其他优化实践

- 表格技术落地：SpreadJS & GcExcel

## [如何实现可多人协作的“在线excel”系统？ - 掘金](https://juejin.cn/post/6844904017152180238)

- [如何实现可多人协同的“在线Excel”系统？](https://live.vhall.com/483759540)
# changelog
- resources
  - [JavaScript Spreadsheet Release Information | SpreadJS](https://www.grapecity.com/spreadjs/releases)

## v16_202212

- The new `.sjs` file format works by bypassing the previous need to first export to SSJSON and now translates the data directly to the model. 
  - The resulting data is saved to a zipped .sjs file with smaller SSJSON files, making it similar to Excel’s own XML structure. 
  - This format now makes the ExcelIO process much faster and smaller.

- TableSheet Enhancements
  - Hierarchy in Data Manager

- Designer Enhancements
  - Selection-Level Find/Replace

- Workbook Enhancements
  - Copy/Cut Cancel Event

## v15_202201

- Two of the most significant features we have added to SpreadJS v15 are the TableSheet and Data Manager.

- Workbook Enhancements
  - Context Menu Scrolling

## v14_202011

- SpreadJS Designer is the implementation of an Excel-like user interface with SpreadJS. 
  - Features include a ribbon, status bar, formula bar, context menus, and associated dialogs
  - GrapeCity made the SpreadJS Designer more flexible by componentizing it
- The SpreadJS v14 Designer includes:
  - Add or remove buttons for tabs in the ribbon
  - The option to change styling
  - The ability to change the functionality of different buttons
  - Custom dialogs

- Incremental Loading
  - When the feature is enabled, SpreadJS loads values and formulas piece-by-piece in the background, so the user can see the workbook as data is loaded. 

## v13_201912

- SpreadJS will now support keeping hyperlinks in imported Excel files intact. 
  - Users can create hyperlinks with SpreadJS and export those successfully to Excel. 
  - Also, hyperlinks can be managed with the SpreadJS Designer dialog and the context menu at runtime.

- Now, Formulas can be set as formatting and applied to different cells.

## v12_201811

- Printing in SpreadJS has been enhanced with a new event, print preview lines, printing info for the page, and background watermark images.
- Drag-filling in SpreadJS has been enhanced with support for days of a month, strings with numbers, and custom lists. 

## v11_201712

- Spread Sheets can now successfully import and export Excel files with charts.

- SpreadJS now features a more extensive formula/function library with 462 functions—more than any other spreadsheet component! 

- The HitTest functionality is now supported at the workbook level.
- Columns can now be easily indented for tree structures.
- Excel 2013-2016 functions are now supported.
# more-blogs
- [简介：开发在线文档时，这个技术难点你解决了吗？ 多人协作](https://www.grapecity.com.cn/blogs/spreadjs-technical-difficulties-of-online-documentation)
- SpreadJS 采用了稀疏数组 (Sparse Array) 作为存储模型，相较于传统的链式存储或数组存储，稀疏数组只会对非空数据进行存储，而不需要对空数据开辟额外的内存空间。
  - 除了节省内存空间外，对于表格这类布局松散的数据类型，稀疏数组也更易于构建基于行索引的数据字典，以便随时替换或恢复整个存储结构中的任何一个级别的节点，
  - 借助这一特性，SpreadJS 在多人协同中实现了高效的数据回滚和数据恢复 (Redo/Undo)。

- [手把手教你用Canvas电子表格做电子签名](https://www.grapecity.com.cn/blogs/spreadjs-use-canvas-spreadsheet-for-electronic-signature)

- [详解Canvas优越性能和实际应用](https://www.grapecity.com.cn/blogs/spreadjs-advantages-and-practical-applications-of-canvas)
