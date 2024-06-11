---
title: toc-lib-format-csv-utils
tags: [csv, format, toc, utils]
created: 2022-11-06T15:45:43.066Z
modified: 2022-11-06T15:46:05.676Z
---

# toc-lib-format-csv-utils

# guide

- tips
  - csv常作为基于文本的表格的一种形式
# popular
- https://github.com/mholt/PapaParse /js
  - https://www.papaparse.com/
  - the fastest in-browser CSV (or delimited text) parser for JavaScript. 
  - Papa Parse can parse a Readable Stream instead of a File when used in Node.js 
  - It is reliable and correct according to [RFC 4180 - Common Format and MIME Type for Comma-Separated Values (CSV) Files](https://datatracker.ietf.org/doc/html/rfc4180)

- https://github.com/fabiospampinato/csv-simple-parser /ts
  - A simple, fast and configurable CSV parser.
# examples
- https://github.com/UgnisSoftware/react-spreadsheet-import /403Star/MIT/202401/ts/inactive
  - https://ugnissoftware.github.io/react-spreadsheet-import
  - Import flow for Excel (.xlsx) and CSV file with automated column matching and validation.
  - A component used for importing XLS / XLSX / CSV documents built with Chakra UI.
  - 上传流程 upload-file > set-header > match > validate
  - 依赖react-data-grid.v7-beta13、react-data-grid、xlsx-ugnis、@chakra-ui/react.v2、framer-motion、lodash

- https://github.com/tableflowhq/csv-import /1.6kStar/MIT/202404/ts/react
  - https://tableflow.com/
  - Open-source CSV and XLS/XLSX file importer for React and JavaScript
  - Embed the CSV Importer in your app with the React or JavaScript SDK
  - 依赖react、@chakra-ui/react.v2、papaparse、xlsx、react-dropzone、zustand
  - 上传流程 upload > review > complete
  - https://www.npmjs.com/package/csv-import-js

- https://github.com/beamworks/react-csv-importer /MIT/202305/ts/仅csv无xlsx
  - https://codesandbox.io/s/github/beamworks/react-csv-importer/tree/master/demo-sandbox
  - This library combines an uploader + CSV parser + raw file preview + UI for custom user column mapping, all in one.
  - 依赖papaparse、react-dropzone、@use-gesture/react
  - drag-drop UI to remap input columns as needed
  - 1GB+ CSV file size (true streaming support without crashing browser)
  - automatically strip leading BOM character in data
  - Papa Parse for CSV parsing
  - react-dropzone for file upload
  - @use-gesture/react for drag-and-drop

- https://github.com/Bunlong/react-papaparse /MIT/202310/ts
  - https://react-papaparse.js.org/
  - https://react-papaparse.js.org/demo
  - the fastest in-browser CSV (or delimited text) parser for React
  - Stream large files (even via HTTP)
  - One of the only parsers that correctly handles line-breaks and quotations

- https://github.com/mirite/csv-magic /ts
  - https://csvmagic.cloud/
  - CSV Magic is a spreadsheet editor that allows for sorting, filtering, and other large scale manipulations within one or multiple CSV files. 
  - The app runs entirely in browser with no backend supporting it.
  - 依赖react、csvtojson、json2csv

- https://github.com/react-csv/react-csv /MIT/202201/js/inactive
  - https://react-csv.github.io/react-csv/
  - React components to build CSV files on the fly basing on Array/literal object of data
  - Generate a CSV file from given data.
  - This data can be an array of arrays, an array of literal objects, or strings.
  - It triggers downloading ONLY on mounting the component. so , be careful to render this component whenever it is needed.

- https://github.com/dumbmatter/csv-sql-live /202206/js
  - http://dumbmatter.com/csv-sql-live/
  - Run SQL queries on CSV files in your web browser
# parser-generator
- https://github.com/C2FO/fast-csv
  - library for parsing and formatting CSVs or any other delimited value file in node.
  - CSV Formatting
  - CSV Parsing
  - Built with streams first to avoid creating large memory footprint when parsing large files.

- https://github.com/mafintosh/csv-parser
  - Streaming csv parser inspired by binary-csv that aims to be faster than everyone else
# extension-superset

# utils

# more
- https://github.com/allain/bench-csv /201708/js
  - Simple benchmarking tool that spits its results out in csv format.
