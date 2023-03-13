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
  - Query Excel spredsheets (.xlsx, .xls, .ods) using SQLite
  - allow working with spreadsheets from SQLite exposing them as virtual tables.
  - XLite is a SQLite extension written in Rust. 

- https://github.com/dinedal/textql /go
  - Execute SQL against structured text like CSV or TSV
# examples

# parser-generator
- https://github.com/Neovici/nullxlsx
  - Minimal JavaScript library to create XLSX spreadsheet and ZIP archive files.

- https://github.com/NickStefan/parsexcel.js /201412/js
  - Parse entire excel workbooks in native node.js. 
  - Get cell styles, formats, formulas, and values.
# extension-superset
- https://github.com/harunou/SheetsDB
  - SheetsDB is a simple tool to read and write data from/to Google spreadsheet as JavaScript objects
# utils
- https://github.com/joway/sheetsql
  - Google Spreadsheet as a Database.

- https://github.com/hyperjumptech/xcs-translator
  - a web app to convert EXCEL file to JSON and SQL so that you can quickly and easily import data from your sheets to your database.

- https://github.com/JasonThon/fastexcel /202112/java/inactive
  - A high-performance streaming processing excel lib
  - A Java lib to read excel providing stream-processing program model
  - 依赖poi-ooxml

- https://github.com/hyberbin/J-Excel /202111/java
  - J-Excel 万能的Excel导入导出工具
# excel-utils
- https://github.com/protobi/msexcel-builder /202301/js
  - A simple and fast library to create MS Office Excel(>2007) xlsx files(Compatible with the OpenOffice document format).

- SheetJS js-xlsx Community Edition /Apache2/21.9kStar/202006
  - https://github.com/SheetJS/sheetjs
  - https://oss.sheetjs.com/
  - 依赖cfb(Compound File Binary File Format extractor), ssf  
  - 常作为excel读写的工具库，而不用来渲染，官网示例上传excel可渲染成canvas或td
  - 无依赖，自己实现了办公类文档的各种解析器 js-word、js-ppt、ssf、js-cfb
- https://github.com/protobi/js-xlsx /202008/js/inactive
  - a fork of the original SheetJS/sheetjs
  - extended to enable cell formats to be read from and written to .xlsx workbooks. 
  - The intent is to provide a temporary means of using these features in practice, and ultimately to merge this into the primary project.
  - https://github.com/protobi/workbook /201602/js
    - Wrapper for js-xlsx providing convenient way to accumulate sheets, rows, styles

- https://github.com/exceljs/exceljs
  - /6.4kStar/MIT/202010
  - Read, manipulate and write spreadsheet data and styles to XLSX and JSON.
# excel-db
- https://github.com/vkareh/spreaddb /201406/js
  - SpreadDB is a spreadsheet-oriented database server. 
  - It currently exposes csv, xls, and xlsx files as JSON data through a REST API. 
  - This is work in progress and currently only exposes non-indexed read-only data.

- https://github.com/ngudbhav/excel-to-mongoDB
  - This module converts your correctly formatted Excel spreadsheet to a collection in specified database in MongoDB.
  - Supported Excel formats are XLS/XLSX/CSV

- https://github.com/CotalkerPartners/mongo-xlsx
  - convert excel spreadsheets into/from MongoDB data. (MongoDB data -> Array of JSONs)

- https://github.com/ngudbhav/TriCo-electron-app
  - This App Converts your correctly formatted Excel Spreadsheet to a specified table/collection in specified Database in MYSQL/MongoDB.
  - Dump your excel/csv sheet into your preferred your DB.

- https://github.com/RyanXu-jn/excel2db /java/js
  - 实现excel导入数据库的一个web项目
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
# csv
- https://github.com/washingtonpost/crosswalker
  - https://crosswalker.washingtonpost.com/
  - Crosswalker is a general purpose tool for joining columns of text data(csv/json) that don't perfectly match
# xls

# more

- https://github.com/rohanhrk/Excel-clone
  - I've made a google sheet clone using HTML, CSS, Javascript
