---
title: toc-lib-format-office-excel-xlsx-utils
tags: [excel, format, ooxml, xlsx]
created: 2022-11-06T15:46:14.325Z
modified: 2023-01-09T11:04:13.958Z
---

# toc-lib-format-office-excel-xlsx-utils

# guide

- https://github.com/SheetJS/notes
  - Various spreadsheet file format notes

- resources
  - [Exceljs VS Sheetjs(xlsx.js) VS xlsx-populate.js](https://jstool.gitlab.io/demo/exceljs-vs-sheetjs-vs-xlsx-populate/)
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

- https://github.com/PengChen96/table-xlsx /MIT/202401/ts
  - https://pengchen96.github.io/table-xlsx/docs/intro
  - 基于SheetJS封装，帮助你快速将xlsx文件转换成表格数据或表格数据导出生成xlsx文件，
  - 导出支持简单样式设置、多sheet页、行/列合并等
  - SheetJS/js-xlsx社区版本不支持样式，您可以使用@pengchen/xlsx
  - 依赖自定义fork @pengchen/xlsx，基于js-xlsx@0.17.0修改
  - https://github.com/PengChen96/sheetjs /202206/js/inactive

- https://github.com/sail-sail/ejsExcel /js
  - node export excel, ejsExcel
  - https://github.com/sail-sail/ejsexcel-browserify

- https://github.com/open-xml-templating/docxtemplater /MIT/js/excel收费
  - a library to generate docx/pptx documents from a docx/pptx template.
  - Functionality can be added with the following paid modules

- SheetJS/xlsx /33.4kStar/apache2/202209/ts/v0.18/大多功能在pro版
  - https://git.sheetjs.com/SheetJS/sheetjs
  - https://github.com/SheetJS/sheetjs
  - https://oss.sheetjs.com/
  - https://sheetjs.com/pro/
  - [sheetjs data model: csf](https://docs.sheetjs.com/docs/csf/)
  - 依赖cfb(Compound File Binary File Format extractor)、ssf
  - 常作为excel读写的工具库，而不用来渲染，官网示例上传excel可渲染成canvas或td
  - 无依赖，自己实现了办公类文档的各种解析器 js-word、js-ppt、ssf、js-cfb
  - pro: edit/image/chart
  - SheetJS presents a simple JS interface that works with "Array of Arrays" and "Array of JS Objects".
  - 源码托管在团队的gitea上
  - 🍴 forks
  - https://github.com/gitbrent/xlsx-js-style /202204/ts
    - Current version of sheetjs used: 0.18.5
    - This project is a fork of SheetJS/sheetjs combined with code from sheetjs-style (by ShanaMaid) and sheetjs-style-v2 (by Raul Gonzalez).
    - https://github.com/Sariyya/xlsx-js-style /202312
  - https://github.com/ShanaMaid/sheetjs-style /202106/js
    - support set cell style for sheetjs
    - API is the same as sheetjs!
    - https://github.com/rona354/sheetjs-style-roy /202208
  - https://github.com/Sariyya/xlsx-js-style /202312/js
  - https://github.com/Favro/sheetjs /202309
    - NUMBERS read/write threaded comments
- https://github.com/mgcrea/node-xlsx /ts
  - NodeJS excel file parser & builder
  - Relies on SheetJS xlsx module to parse/build excel sheets

- js-xlsx/xlsx-style /201706/js/inactive
  - https://github.com/protobi/js-xlsx
  - a fork of the original SheetJS/sheetjs
  - extended to enable cell formats to be read from and written to .xlsx workbooks.
  - The intent is to provide a temporary means of using these features in practice, and ultimately to merge this into the primary project.
  - 🍴 forks
  - https://github.com/iroot/sheetjs /202012/js
    - Manual merge branch 'protobi/master' into style
  - https://github.com/JimZhu6/js-xlsx /202312/js
    - 修复了找不到'./cptable'及其他引用问题
  - https://github.com/DmitriySlabodchikov/js-xlsx /202309
  - https://github.com/JonathanDn/js-xlsx-formula-and-rtl /202308/js
- https://github.com/protobi/workbook /201602/js
  - Wrapper for js-xlsx providing convenient way to accumulate sheets, rows, styles

- exceljs /11.7kStar/MIT/202401/js
  - https://github.com/exceljs/exceljs
  - Read, manipulate and write spreadsheet data and styles to XLSX and JSON.
- https://github.com/zurmokeeper/excelize /202310/js
  - forked from exceljs v4.3.0_20230505
  - 需要完成一个读取WPS带密码保密的excel功能，找遍了社区所有的库，都没有找到，一开始发现 xlsx-populate 支持解密，后面发现只支持 ecma376 agile encryption。是现在office xlsx格式的加密方式，不是WPS的加密方法，所以无法解密.
  - 后面发现 WPS 对xlsx文件的加解密用的是 ecma376 standard encryption
  - 本来是想给exceljs提PR的，但是发现exceljs快2年没人维护了
  - xlsx，是sheetjs出的，这个功能最广，支持读取xls格式。但是这个库其实是个社区版，阉割了加解密功能
  - [推荐一个新的excel处理库，支持xlsx文件的解密功能](https://cnodejs.org/topic/647e911256d983d3ff9d9cfa)

- https://github.com/Siemienik/XToolset /MIT/202311/ts
  - https://siemienik.com/docs/xlsx-renderer/
  - spreadsheet tools
  - XLSX-Renderer: Export data to Ecma-376 . XLSX Excel files based on template; generating Excel files with minimum code
  - XLSX-Import: Importing data from xlsx as simple as possible and map into configured data model

- https://github.com/dtjohnson/xlsx-populate /202003/js
  - Excel XLSX parser/generator written in JavaScript with Node.js and browser support, jQuery/d3-style method chaining, encryption, and a focus on keeping existing workbook features and styles in tact.

- https://github.com/vweevers/spreadsheet-stream /js
  - Semi-streaming XLS(X) / ODS / QPW (and more) parser.
  - "Semi" because these spreadsheet formats are not streamable so the whole thing is buffered in memory. Same as excel-stream but faster because there's no filesystem IO or child process.

- https://github.com/liyuec/easyExcelJs /js
  - 简单的操作生成漂亮的EXCEL，快速上手。提供漂亮模板直接使用
  - 组件依附 exceljs 和 file-saver 进行封装

- https://github.com/jmaister/excellentexport /MIT/202305/ts
  - JavaScript library to create export to Excel/CSV from HTML tables in the browser. No server required.
  - support XLSX
# examples
- https://github.com/renanlecaro/importabular /js/MIT
  - https://importabular.lecaro.me/
  - Lightweight spreadsheet editor for the web, to easily let your users import their data from excel.
  - No sorting, pivot, formula, etc

- https://github.com/ashishd751/react-excel-renderer /MIT/202006/js/inactive
  - react library to render and display excel sheets on webpage
# parser-generator
- https://github.com/Claviz/xlstream /ts
  - Turns XLSX into a readable stream.
  - Stream is pausable.

- https://github.com/Neovici/nullxlsx
  - Minimal JavaScript library to create XLSX spreadsheet and ZIP archive files.

- https://github.com/MathNya/umya-spreadsheet /MIT/202401/rust
  - rust library for reading and writing spreadsheet files
  - https://github.com/informationsea/xlsxwriter-rs /202304/rust/inactive

- https://github.com/protobi/msexcel-builder /202301/js
  - A simple and fast library to create MS Office Excel(>2007) xlsx files(Compatible with the OpenOffice document format).

- https://github.com/optilude/xlsx-template /ts
  - A NodeJS module to generate Excel files in .xlsx format from a template created with Excel itself

- https://github.com/NickStefan/parsexcel.js /201412/js
  - Parse entire excel workbooks in native node.js. 
  - Get cell styles, formats, formulas, and values.

- https://github.com/HarvestProfit/DocFlux /202009/js
  - https://harvestprofit.github.io/DocFlux/
  - Flux/React framework for creating any document, just define a few DOM components to transform into the document.
  - You will define a few document metadata options and specify which component it will render. 
  - 实现了react style Component class, 不依赖react
  - https://github.com/HarvestProfit/DocFlux-Spreadsheets
    - XLSX Spreadsheets parser for DocFlux
  - https://github.com/humphreyja/sample-doc-flux-spreadsheets
    - https://humphreyja.github.io/sample-doc-flux-spreadsheets/
    - Example of using DocFlux to generate spreadsheets with xlsx lib
  - https://github.com/HarvestProfit/DocFlux-PDFs
    - Allows you to create pdfMake pdfs using DocFlux.
    - 依赖pdfmake

- https://github.com/alibaba/easyexcel /30kStar/apache2/202312/java
  - 简单且能避免OOM的java处理Excel工具
  - Java解析、生成Excel比较有名的框架有Apache poi、jxl。但他们都存在一个严重的问题就是非常的耗内存，poi有一套SAX模式的API可以一定程度的解决一些内存溢出的问题，但POI还是有一些缺陷，比如07版Excel解压缩以及解压后存储都是在内存中完成的，内存消耗依然很大。
  - easyexcel重写了poi对07版Excel的解析，一个3M的excel用POI sax解析依然需要100M左右内存，改用easyexcel可以降低到几M，并且再大的excel也不会出现内存溢出；03版依赖POI的sax模式，在上层做了模型转换的封装，让使用者更加简单方便
# extension-superset
- https://github.com/harunou/SheetsDB
  - SheetsDB is a simple tool to read and write data from/to Google spreadsheet as JavaScript objects
# formula
- https://github.com/formulajs/formulajs /500Star/MIT/202310/js
  - https://formulajs.info/
  - JavaScript implementation of most Microsoft Excel formula functions
  - originally forked from @handsontable/formulajs version 2.0.2 (202001). There is no regression, only fixes and new functions since the fork.
  - 依赖jstat、bessel(fn)
  - 🍴 forks
  - https://github.com/handsontable/formula.js /MIT/202001/js
  - https://github.com/davidpolberger/formulajs /201801/js
    - improved error handling, cutting down on dependencies
  - https://github.com/jspreadsheet/formulajs
  - https://github.com/sutoiku/formula.js
- https://github.com/vogtb/spreadsheet /MIT/201807/ts
  - TypeScript/javascript spreadsheet parser, with formulas.
  - This is largely a re-write of Handsontable's https://github.com/handsontable/ruleJS, and https://github.com/sutoiku/formula.js/.
  - The parser was derived from Handsontable's, and many of the formulas were created with FormulaJS's formulas as a reference point.

- https://github.com/borgar/fx /js
  - Utilities for working with Excel formulas
  - A tokenizer, parser, and other utilities to work with Excel formula code, specifically syntax highlighting.
  - This utility is partially developed as tooling for GRID – The new face of spreadsheets

- https://github.com/taggon/tiny-formula /ts/NoDeps
  - A toolset for parsing excel-like formula and calculating with custom functions.

- https://github.com/LeanyLabs/formula-engine
  - Extendable formula parser and executor.
  - It supports three types of literals (data types): string/number/boolean

- https://github.com/plantain-00/expression-engine /MIT/202402/ts
  - An expression tokenizer, parser and evaluator.

- https://github.com/vinci1it2000/formulas /python
  - formulas implements an interpreter for Excel formulas, which parses and compile Excel formulas expressions.
  - it compiles Excel workbooks to python and executes without using the Excel COM server. Hence, Excel is not needed.

- https://github.com/omid/formula /MIT/202211/rust/inactive
  - A parser and evaluator of spreadsheet-like formulas
  - Add this library to your project with npm install formula-wasm
  - At the moment, we don't support table data. It means you need to extract table data and pass theirs values to this library
  - We still do not support parentheses to change the order of operations, but you can use our F. function
  - Inspired by formulajs
# template
- https://github.com/plantain-00/js-excel-template
  - A js excel template used in browser or nodejs environment.
  - Generate Excel based on Excel template

- https://github.com/yumdocs/yumdocs
  - https://dev.yumdocs.com/docs/tutorials/typescript-tutorial
  - a template engine to automate Word, PowerPoint and Excel documents.
# utils
- https://github.com/joway/sheetsql /202205/ts/inactive
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

- https://github.com/ngudbhav/TriCo-electron-app /MIT/202301/js/inactive
  - https://www.producthunt.com/posts/trico
  - This App Converts your correctly formatted Excel Spreadsheet to a specified table/collection in specified Database in MYSQL/MongoDB.
  - Dump your excel/csv sheet into your preferred your DB.
  - Batch Files support
  - You can also try selecting a range of columns and rows.
  - History Maintainance.
  - 依赖mongoose、nedb、excel-to-mongodb、excel-to-mongodb

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

# diff-excel/tables

- https://github.com/Caleydo/taco /ts
  - http://taco.caleydo.org/
  - https://jku-vds-lab.at/publications/2017_infovis_taco/
  - TACO (for Table Comparison) is an interactive comparison tool that effectively visualizes the differences between multiple tables at various levels of granularity.

- https://github.com/paulfitz/daff /HaxeLang
  - http://paulfitz.github.io/daff/
  - a library for comparing tables, producing a summary of their differences, and using such a summary as a patch file. 
  - It is optimized for comparing tables that share a common origin, in other words multiple versions of the "same" table.
  - The daff library is written in Haxe Lang, which can be translated reasonably well into js/python/java
  - example shows the changes made in the modified table with respect to the original table. The format used is the highlighter tabular diff.

- https://github.com/Yinger/ts-excel-compare /202009/ts
  - https://yinger.github.io/ts-excel-compare/
  - Diff Tool to Compare Two Excel Spreadsheet Files 
  - 依赖handsontable、sheetjs、daff、antd
# table-format
- https://github.com/microsoft/lst-bench /java
  - a framework that allows users to run benchmarks specifically designed for evaluating the performance, efficiency, and stability of Log-Structured Tables (LSTs), also commonly referred to as table formats, such as Delta Lake, Apache Hudi, and Apache Iceberg.
# canvas
- https://github.com/tzhangchi/canvas-table /js
  - https://tzhangchi.github.io/canvas-table/
  - define render function to calculate the visible range of cells based on the current scroll position and the viewport size
# more
- https://github.com/rohanhrk/Excel-clone
  - I've made a google sheet clone using HTML, CSS, Javascript
