---
title: toc-lib-format-office-excel-xlsx-utils
tags: [excel, format, ooxml, xlsx]
created: 2022-11-06T15:46:14.325Z
modified: 2023-01-09T11:04:13.958Z
---

# toc-lib-format-office-excel-xlsx-utils

# guide

# popular
- https://github.com/x2bool/xlite /rust
  - Query Excel spreadsheets (.xlsx, .xls, .ods) using SQLite
  - allow working with spreadsheets from SQLite exposing them as virtual tables.
  - XLite is a SQLite extension written in Rust. 

- https://github.com/dinedal/textql /go
  - Execute SQL against structured text like CSV or TSV

- https://github.com/zhangyu836/node-xlsx-template
  - A node module to generate .xlsx files from a .xlsx template.
  - When xltpl reads a xlsx file, it creates a tree for each worksheet.
  - And, each tree is translated to a nunjucks(jinja2) template with custom tags.

- https://github.com/sail-sail/ejsExcel /js
  - node export excel, ejsExcel
  - https://github.com/sail-sail/ejsexcel-browserify

- https://github.com/open-xml-templating/docxtemplater /MIT/js/excel收费
  - a library to generate docx/pptx documents from a docx/pptx template.
  - Functionality can be added with the following paid modules

- SheetJS js-xlsx Community Edition /Apache2/21.9kStar/202006
  - https://github.com/SheetJS/sheetjs
  - https://oss.sheetjs.com/
  - https://sheetjs.com/pro/
  - [sheetjs data model: csf](https://docs.sheetjs.com/docs/csf/)
  - 依赖cfb(Compound File Binary File Format extractor), ssf  
  - 常作为excel读写的工具库，而不用来渲染，官网示例上传excel可渲染成canvas或td
  - 无依赖，自己实现了办公类文档的各种解析器 js-word、js-ppt、ssf、js-cfb
  - pro: edit/image/chart
  - SheetJS presents a simple JS interface that works with "Array of Arrays" and "Array of JS Objects".
  - https://github.com/mgcrea/node-xlsx
    - excel file parser and builder, using sheetjs

- https://github.com/exceljs/exceljs /6.4kStar/MIT/202010/js
  - Read, manipulate and write spreadsheet data and styles to XLSX and JSON.
- https://github.com/zurmokeeper/excelize
  - 需要完成一个读取WPS带密码保密的excel功能，找遍了社区所有的库，都没有找到，一开始发现 xlsx-populate 支持解密，后面发现只支持 ecma376 agile encryption。是现在office xlsx格式的加密方式，不是WPS的加密方法，所以无法解密.
  - 后面发现 WPS 对xlsx文件的加解密用的是 ecma376 standard encryption
  - 本来是想给exceljs提PR的，但是发现exceljs快2年没人维护了
  - xlsx，是sheetjs出的，这个功能最广，支持读取xls格式。但是这个库其实是个社区版，阉割了加解密功能

- https://github.com/vweevers/spreadsheet-stream /js
  - Semi-streaming XLS(X) / ODS / QPW (and more) parser.
  - "Semi" because these spreadsheet formats are not streamable so the whole thing is buffered in memory. Same as excel-stream but faster because there's no filesystem IO or child process.

- https://github.com/liyuec/easyExcelJs /js
  - 简单的操作生成漂亮的EXCEL，快速上手。提供漂亮模板直接使用
  - 组件依附 exceljs 和 file-saver 进行封装
# examples
- https://github.com/renanlecaro/importabular /js/MIT
  - https://importabular.lecaro.me/
  - Lightweight spreadsheet editor for the web, to easily let your users import their data from excel.
  - No sorting, pivot, formula, etc
  - No sorting, pivot, formula, etc
# parser-generator
- https://github.com/Claviz/xlstream /ts
  - Turns XLSX into a readable stream.
  - Stream is pausable.

- https://github.com/Neovici/nullxlsx
  - Minimal JavaScript library to create XLSX spreadsheet and ZIP archive files.

- https://github.com/optilude/xlsx-template /ts
  - A NodeJS module to generate Excel files in .xlsx format from a template created with Excel itself

- https://github.com/NickStefan/parsexcel.js /201412/js
  - Parse entire excel workbooks in native node.js. 
  - Get cell styles, formats, formulas, and values.
# extension-superset
- https://github.com/harunou/SheetsDB
  - SheetsDB is a simple tool to read and write data from/to Google spreadsheet as JavaScript objects
# formula
- https://github.com/handsontable/formula.js /MIT/js
  - JavaScript implementation of most Microsoft Excel formula functions
  - forks
  - https://github.com/jspreadsheet/formulajs
  - https://github.com/formulajs/formulajs

- https://github.com/borgar/fx /js
  - Utilities for working with Excel formulas
  - A tokenizer, parser, and other utilities to work with Excel formula code, specifically syntax highlighting.
  - This utility is partially developed as tooling for GRID – The new face of spreadsheets

- https://github.com/taggon/tiny-formula /ts/NoDeps
  - A toolset for parsing excel-like formula and calculating with custom functions.

- https://github.com/LeanyLabs/formula-engine
  - Extendable formula parser and executor.
  - It supports three types of literals (data types): string/number/boolean
# template
- https://github.com/Siemienik/XToolset /ts
  - Export data to Ecma-376 . XLSX Excel files based on template
  - Import data from Workbooks / Worksheets Excel files

- https://github.com/plantain-00/js-excel-template
  - A js excel template used in browser or nodejs environment.
  - Generate Excel based on Excel template

- https://github.com/yumdocs/yumdocs
  - https://dev.yumdocs.com/docs/tutorials/typescript-tutorial
  - a template engine to automate Word, PowerPoint and Excel documents.
# utils
- https://github.com/joway/sheetsql
  - Google Spreadsheet as a Database.

- https://github.com/github/paste-markdown
  - Paste spreadsheet cells and HTML tables as a Markdown tables.

- https://github.com/cujarrett/markdown-tables /js
  - Convert Excel (.xlsx) data into markdown tables friendly for GitHub or GitLab.

- https://github.com/DHTMLX/excel2table /js
  - render an Excel file as an HTML table
  - uses excel2json

- https://github.com/hyperjumptech/xcs-translator
  - a web app to convert EXCEL file to JSON and SQL so that you can quickly and easily import data from your sheets to your database.

- https://github.com/JasonThon/fastexcel /202112/java/inactive
  - A high-performance streaming processing excel lib
  - A Java lib to read excel providing stream-processing program model
  - 依赖poi-ooxml

- https://github.com/hyberbin/J-Excel /202111/java
  - J-Excel 万能的Excel导入导出工具

- https://github.com/idw111/table-renderer /js
  - convert table or spreadsheet data into an image
  - `node-canvas` module is peer-dependency
# excel-utils
- https://github.com/protobi/msexcel-builder /202301/js
  - A simple and fast library to create MS Office Excel(>2007) xlsx files(Compatible with the OpenOffice document format).

- https://github.com/protobi/js-xlsx /202008/js/inactive
  - a fork of the original SheetJS/sheetjs
  - extended to enable cell formats to be read from and written to .xlsx workbooks. 
  - The intent is to provide a temporary means of using these features in practice, and ultimately to merge this into the primary project.
  - https://github.com/protobi/workbook /201602/js
    - Wrapper for js-xlsx providing convenient way to accumulate sheets, rows, styles

- https://github.com/hxj9102/table2excel
  - text and image save to excel
# excel-db
- https://github.com/vkareh/spreaddb /201406/js
  - SpreadDB is a spreadsheet-oriented database server. 
  - It currently exposes csv, xls, and xlsx files as JSON data through a REST API. 
  - This is work in progress and currently only exposes non-indexed read-only data.

- https://github.com/ngudbhav/excel-to-mongoDB
  - This module converts your correctly formatted Excel spreadsheet to a collection in specified database in MongoDB.
  - Supported Excel formats are XLS/XLSX/CSV

- https://github.com/Paultje52/excel-to-sqlite /js
  - Convert excel documents to sqlite!

- https://github.com/CotalkerPartners/mongo-xlsx
  - convert excel spreadsheets into/from MongoDB data. (MongoDB data -> Array of JSONs)

- https://github.com/ngudbhav/TriCo-electron-app /js
  - This App Converts your correctly formatted Excel Spreadsheet to a specified table/collection in specified Database in MYSQL/MongoDB.
  - Dump your excel/csv sheet into your preferred your DB.

- https://github.com/RyanXu-jn/excel2db /java
  - 实现excel导入数据库的一个web项目
  - 读取excel循环批量插入数据库，可实现自动建表
# export/import
- https://github.com/huanz/tableExport
  - table导出文件，支持导出json、txt、csv、xml、doc、xls、image、 pdf

- https://github.com/koalaylj/xlsx2json
  - convert excel to json , support object/array/number/bool data type.
  - 目前只支持.xlsx格式，不支持.xls格式
  - https://github.com/rikkertkoppes/json2xls
- https://github.com/catamphetamine/read-excel-file
  - Parse to JSON with a strict schema

- https://github.com/egeriis/zipcelx
  - Turns JSON data into `.xlsx` files in the browser

- https://github.com/kinddde/js-export-excel
  - json导出excel（纯js 支持中文）
# converters
- https://github.com/kaxifakl/excel-convert
  - 可自定义解析的excel转json、ts工具

- https://github.com/washingtonpost/crosswalker
  - https://crosswalker.washingtonpost.com/
  - Crosswalker is a general purpose tool for joining columns of text data(csv/json) that don't perfectly match
# xls

# more

- https://github.com/rohanhrk/Excel-clone
  - I've made a google sheet clone using HTML, CSS, Javascript
