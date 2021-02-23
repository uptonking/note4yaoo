---
title: spec-format-json
tags: [format, json]
created: '2019-12-24T12:57:52.481Z'
modified: '2020-10-15T13:41:01.275Z'
---

# spec-format-json

# spec

- https://www.json.org/json-en.html
- https://json5.org

# guide

- 类json格式的操作
  - 从devDependencies移动到dependencies后，需要手动添加逗号和删除逗号

- ## json-extensions
- json5
  - Main JSON5 features: comments, trailing commas.
- geo
  - geojson
  - topojson
- json-more
  - dson, cson
- [Amazon Ion](https://amzn.github.io/ion-docs/)
  - Amazon Ion is a richly-typed, self-describing, hierarchical data serialization format offering interchangeable binary and text representations.
  - The text format (a superset of JSON) is easy to read and author, supporting rapid prototyping.
  - The binary representation is efficient to store, transmit, and skip-scan parse. 
- https://github.com/yahoo/serialize-javascript
  - Serialize JavaScript to a superset of JSON that includes regular expressions and functions.
  - this package began its life as an internal module to express-state
- https://github.com/blitz-js/superjson
  - Safely serialize JavaScript expressions to a superset of JSON, which includes Dates, BigInts, and more.

# faq

- 

# summary

- 列表插件设计
  - 列表类
  - 图表类
  - 地图类
  - 搜索类

# json5

- ref
  - http://json5.org/
  - https://github.com/json5/json5

- ## Features
- Comments
  - Single and multi-line comments are allowed.
- Objects
  - Object keys may be an ECMAScript 5.1 IdentifierName.
  - Objects may have a single trailing comma.
- Arrays
  - Arrays may have a single trailing comma.
- Strings
  - Strings may be single quoted.
  - Strings may span multiple lines by escaping new line characters.
  - Strings may include character escapes.
- Numbers
  - Numbers may be hexadecimal.
  - Numbers may have a leading or trailing decimal point.
  - Numbers may be IEEE 754 positive infinity, negative infinity, and NaN
  - Numbers may begin with an explicit plus sign.
- White Space
  - Additional white space characters are allowed.

# geojson

- https://github.com/mapbox/geojson.io
- https://github.com/topojson/topojson  

# dev
