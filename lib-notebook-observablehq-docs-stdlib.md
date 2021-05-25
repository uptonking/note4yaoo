---
title: lib-notebook-observablehq-docs-stdlib
tags: [docs, observablehq, stdlib]
created: '2021-05-14T14:50:08.532Z'
modified: '2021-05-14T14:50:35.347Z'
---

# lib-notebook-observablehq-docs-stdlib

# guide

# docs

## [Standard Library](https://observablehq.com/@observablehq/stdlib)

- https://github.com/observablehq/stdlib
  - provides helpful functions for working with HTML, SVG, generators, files and promises among other useful sundries

- The Observable standard library is built-in to Observable, so you don’t normally need to install or instantiate it directly.
- `Library([resolve])`
- Returns a new standard library object. 
  - The properties on the returned library instance correspond to the symbols that are available in Observable notebooks.

* [DOM](#dom) - create HTML and SVG elements.
* [Files](#files) - read local files into memory.
* [FileAttachments](#file-attachments) - read remote files.
* [Generators](#generators) - utilities for generators and iterators.
* [Promises](#promises) - utilities for promises.
* [require](#require) - load third-party libraries.
* [html](#html) - render HTML.
* [md](#markdown) - render Markdown.
* [svg](#svg) - render SVG.
* [tex](#tex) - render LaTeX.
* [now](#now) - the current value of Date.now.
* [width](#width) - the current page width.
* [invalidation](#invalidation) - dispose resources.
* [visibility](#visibility) - wait for visibility.

## [Recommended Libraries](https://observablehq.com/@observablehq/recommended-libraries)

- To help you get work done quickly, the Observable standard library provides a handful of recommended open-source libraries by default in all notebooks
- lodash, `_`
- d3.js, `d3`
- vega-lite, `vl`
- observable Inputs, `Inputs`
- Observable Plot, `Plot`
- Observable Graphviz, `dot`
- Observable Hypertext Literal, `htl`
