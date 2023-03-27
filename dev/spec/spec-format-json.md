---
title: spec-format-json
tags: [format, json]
created: 2019-12-24T12:57:52.481Z
modified: 2020-10-15T13:41:01.275Z
---

# spec-format-json

# spec

- json
  - https://www.json.org/json-en.html
  - [RFC 6901 - JavaScript Object Notation (JSON) Pointer](https://datatracker.ietf.org/doc/html/rfc6901)
    - JSON Pointer defines a string syntax for identifying a specific value
   within a JavaScript Object Notation (JSON) document.

- json5
  - https://json5.org

- BSON is short for "Binary JSON"
  - https://github.com/mongodb/js-bson
  - jsonb

- JSONL
  - http://jsonlines.org/
- ndjson / Newline delimited JSON
  - http://ndjson.org/

- JSON-LD
  - https://json-ld.org/
  - JSON-LD is a lightweight Linked Data format. 
  - provides a way to help JSON data interoperate at Web-scale.
  - JSON-LD is an ideal data format for programming environments, REST Web services, and unstructured databases such as Apache CouchDB and MongoDB.

- JSONC
  - JSONC is JSON with JavaScript style comments. 
  - This node module provides a scanner and fault tolerant parser that can process JSONC but is also useful for standard JSON.
  - https://github.com/microsoft/node-jsonc-parser
# guide
- 类json格式的操作
  - 从devDependencies移动到dependencies后，需要手动添加逗号和删除逗号

- ## json-extensions
- json-superset
  - json5: 官方只实现了js解析器
  - hjson: 官方实现了很多解析器js, py, go
  - json5 vs hjson
    - stars: 4.3k vs 2.2k
    - npmtrends: 36m > 0.17m
- gis-json
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
# json-rpc
- trpc内部

- [simple is better - JSON-RPC](http://www.simple-is-better.org/rpc/)
- Differences between 1.0 and 2.0
- here is a list of the main differences of JSON-RPC 2.0, compared with 1.0:
  - client-server instead of peer-to-peer:
    - JSON-RPC 2.0 uses a client-server-architecture.
    - V1.0 used a peer-to-peer-architecture where every peer was both server and client.
  - Transport independence:
    - JSON-RPC 2.0 doesn't define any transport-specific issues, since transport and RPC are independent.
    - V1.0 defined that exceptions must be raised if the connection is closed, and that invalid requests/responses must close the connection (and raise exceptions).
  - Named parameters added
  - Reduced fields: req/res
  - Optional parameters
  - Extensions: added optional extensions, e.g. for service description or multicall; moved "class hinting" from the base specification to an (optional) extension.

- https://github.com/elpheria/rpc-websockets /ts
  - JSON-RPC 2.0 implementation over WebSockets for Node.js and JavaScript/TypeScript
- https://github.com/teambition/jsonrpc-lite
  - Parse and Serialize JSON-RPC2 messages in node.js or browser.

- https://github.com/dabblewriter/websocket-rpc-protocol
  - Client and server libraries for handling RPC calls between the browser and a Cloudflare websocket interface. 

- https://github.com/tedeh/jayson /js
  - a simple but featureful JSON-RPC 2.0/1.0 client and server for node.js

- https://github.com/k8w/tsrpc
  - 专为 TypeScript 设计的 RPC 框架
  - 支持在 JSON 中传输更多数据类型，例如 ArrayBuffer、Date、ObjectId
  - 同时支持 HTTP/WebSocket
# more
