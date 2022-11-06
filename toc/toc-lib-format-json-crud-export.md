---
title: toc-lib-format-json-crud-export
tags: [crud, json, toc, utils]
created: 2022-11-06T16:46:37.865Z
modified: 2022-11-06T16:47:43.444Z
---

# toc-lib-format-json-crud-export

# json-crud-operations
- https://github.com/streamich/json-joy
  - JSON utilities for joy and collaborative editing with OT and CRDT approaches. 

- https://github.com/Elijah-trillionz/native-json-db
  - native-json-db offers a JSONDB class with methods for structuring, adding, removing, and updating data in the json file
  - Native-JSON-DB or JSONDb is a NoSQL database system on your local server.

- https://github.com/Starcounter-Jack/JSON-Patch
  - Update JSON documents using delta patches.
  - JSON-Patch (RFC6902) is a standard format that allows you to update a JSON document by sending the changes rather than the whole document. 
  - JSON Patch plays well with the HTTP PATCH verb (method) and REST style programming.
  - Lean and mean Javascript implementation of the JSON-Patch standard (RFC 6902).

- https://github.com/Palindrom/Palindrom
  - Library for two-way data binding between local and remote JSON models. 
  - It uses JSON-Patch for data updates and Operational Transformation for versioning and data consistency. 
  - It operates via HTTP or WebSocket or both.

- https://github.com/typewriter-editor/json-patch
  - Immutable JSON Patch implementation based on RFC 6902 which adds operational transformation (OT) and last-writer-wins (LWW) support for syncing between client and server. 
  - Does not support the full OT algorithm because copy and move operations cannot be transformed correctly in all cases, so operations must always be applied in correct order. This means a central server is required to determine order.
- https://github.com/typewriter-editor/typewriter
  - A rich text editor based off of Quill.js and Ultradom, and using Svelte for UI.

- https://github.com/cujojs/jiff
  - JSON Patch and diff based on rfc6902
- https://github.com/wizedix/json-patch-apply
  - an implementation of JSON patch RFC 6902

- https://github.com/jpbnetley/test-json-patch
  - 👉🏻 Test different implementations for json patch RFC6902

- https://github.com/robwatkin/japer-example
  - An example JSON Patch Server
- https://github.com/SandunWebDev/JSON-Patch-API
  - Express Server API Project that provides endpoints for JSON Patching and Image Resizing. 
- https://github.com/ken107/push-model
  - A JSON-RPC server with object synchronization based on JSON-Patch

- https://github.com/mongodb-js/jsonpatch-to-mongodb
  - Convert JSON patches into a MongoDB update
# json-diff
- https://github.com/benjamine/jsondiffpatch
  - Diff & patch JavaScript objects
  - simplistic, pure JSON, low footprint delta format
  - reverse a delta
  - unpatch (eg. revert object to its original state using a delta)

- https://github.com/pierreinglebert/json-merge-patch
  - An implementation of the JSON Merge Patch (RFC 7396)
- https://github.com/riagominota/ts-merge-patch
  - Typescript ready attempt of RFC 7396 JSON Merge Patch method
# export/import
- https://github.com/zheeeng/export-from-json
  - Export to plain text, css, html, json, csv, xls, xml files from JSON.
# extension-superset
- https://github.com/Belphemur/node-json-db
  - A simple "database" that use JSON file for Node. JS.
  - Every method are now asynchronous
  - easily traverse the data to reach directly the interesting property using the DataPath. 
    - The principle of DataPath is the same as XMLPath.

- https://github.com/thearkxd/ark.db
  - Small and fast JSON database for Node and browser

- https://github.com/leoncvlt/minim-json-db
  - Minimal NoSQL database implementation for node.js / electron apps which stores data locally in .json files with a simple MongoDB-inspired API
# utils
- https://github.com/pschiffmann/json-flatten-relational
  - https://pschiffmann.github.io/json-flatten-relational/
  - Converts deeply nested JSON data to flat tables with foreign key references.

- https://github.com/ansteh/shape-json
  - convert a flat json array into a nested json object with a predefined scheme

- https://github.com/rentzsch/jsongo
  - like mongo db, except stores data in git-friendly flat json files
  - It consists of a data format, a code library, and a CLI tool.
  - Jsongo's data format is basically the same as MongoDB's semantic data model: Database > Collection > Document

- https://github.com/RebelRae/JSON2FlatDB
  - Recursive function to coonvert deeply-nested JSON taxanomic data into a file-based database
