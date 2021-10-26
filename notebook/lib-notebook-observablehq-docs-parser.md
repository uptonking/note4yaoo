---
title: lib-notebook-observablehq-docs-parser
tags: [docs, observablehq]
created: '2021-05-14T14:45:11.807Z'
modified: '2021-05-14T14:45:40.999Z'
---

# lib-notebook-observablehq-docs-parser

# guide

# docs

- https://github.com/observablehq/parser
  - parse a cell to a json object

``` JS
// 1 + 2
{
  "type": "Cell",
  "id": null,
  "async": false,
  "generator": false,
  "body": {
    "type": "BinaryExpression",
    "left": {
      "type": "Literal",
      "value": 1,
      "raw": "1"
    },
    "operator": "+",
    "right": {
      "type": "Literal",
      "value": 2,
      "raw": "2"
    }
  }
}
```
