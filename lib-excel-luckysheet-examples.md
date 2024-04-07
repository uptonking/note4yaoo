---
title: lib-excel-luckysheet-examples
tags: [examples, luckysheet, toc]
created: 2022-08-13T18:32:43.761Z
modified: 2022-08-21T10:37:45.959Z
---

# lib-excel-luckysheet-examples

# popular

- https://github.com/mengshukeji/Luckysheet /js
  - https://dream-num.github.io/LuckysheetDocs/zh/guide/
  - https://dream-num.github.io/LuckysheetDemo/
  - an online spreadsheet like excel
  - 基于canvas实现
  - 依赖jspdf
  - 最好通过 iframe 使用 - 嵌入到页面会污染当前环境
- https://github.com/mengshukeji/Luckyexcel
  - an excel import and export library adapted to Luckysheet.
  - only supports .xlsx format files (not .xls).
- https://github.com/mengshukeji/luckysheet-react
  - a simple project that shows the use of luckysheet in a React project

- fortune-sheet /1.4kStar/MIT/202208/ts
  - https://github.com/ruilisi/fortune-sheet
  - https://ruilisi.github.io/fortune-sheet-docs/zh/guide/
  - https://ruilisi.github.io/fortune-sheet-demo
  - FortuneSheet是一款开箱即用的类似Excel和Google Sheets的javascript表格组件。
  - 本项目源于 Luckysheet，并继承了它的很多代码。我们为将其转换为typescript做了很多努力，并且解决了一些原项目设计层面的问题。
  - 完全使用typescript编写。
  - 去掉了 jQuery 的依赖, 用React/Vue + immer来管理DOM和状态。
  - 同页面支持多个实例。目前只支持单个实例，因为有全局状态
  - 避免在window对象上存储数据。
  - 用一个forked handsontable/formula-parser 来处理公式计算。
  - 基于operation实现undo/redo和协同编辑
  - 用SVG代替iconfont的图标，因为iconfont的图标对其他开发者而言很不方便改动。
  - 容器外面不创建可见的页面元素。
  - 数据结构总体兼容Luckysheet
  - 👀 从luckysheet未迁移的功能
    - 透视表、图表、截图
  - [Is there any plan to make a Vue version? soon](https://github.com/ruilisi/fortune-sheet/issues/14)
  - 🔀 [collabration 是如何解决两个用户操作冲突的](https://github.com/ruilisi/fortune-sheet/issues/308)
    - collabration是当一位用户进行操作时，会将用户操作转化为op并使用websocket对其它客户端通信，其它客户端收到op后会进行相应更改
    - 如果两个人同时更改某个单元格的同一个属性，后来的更改会覆盖之前的更改
    - 👉🏻 暂时没有这样的计划来引入ot
    - 我们还是更倾向于将单元格的属性作为原子，而不是属性的内容作为原子，而单元格的内容也是一个单元格属性
# collab
- https://git.qmpoa.com/fe_common_lib/y-luckysheet /202403/ts
  - 将 Luckysheet 数据映射到 Y. Map
  - 同步 Luckysheet 数据、光标
  - Undo / Redo 仅对删除 sheet 做了管理，其它依赖 Luckysheet 自有逻辑
  - https://git.qmpoa.com/fe_common_lib/luckysheet

- https://gitee.com/wfeng0/mpoe /apache2/202402/js/vue
  - 多人协同编辑器开发 MPOE（Multi person online edit）
  - node采用较强的模块化思想，每个单独的模块都会独立导出 index.js ，因此，node有很多的 index.js，注意区分; 
  - 使用Yjs、Quill、LuckySheet 等技术实现的markdown、txt、excel 等文件的多人在线协同编辑，支持以 websocket、webRTC、组合API等形式实现通信
  - 对pako压缩数据进行解析，这是第一个难点；
  - exceljs file-saver 实现文件导出；
  - [Luckysheet 实现excel多人在线协同编辑 - 掘金](https://juejin.cn/post/7298170736480485376)
  - [Yjs + Quill 实现文档多人协同编辑器开发（基础+实战） - 掘金 _202309](https://juejin.cn/post/7273432426772070457)

- https://github.com/DilemmaVi/ecsheet /java/js
  - 基于Luckysheet实现的协同编辑在线表格
  - SpringBoot + Websocket
  - MongoDB 4.4.0
# more-luckysheet
