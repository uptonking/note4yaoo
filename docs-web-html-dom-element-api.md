---
title: docs-web-html-dom-element-api
tags: [docs, dom, web]
created: '2020-08-05T12:22:15.902Z'
modified: '2020-08-05T12:29:43.618Z'
---

# docs-web-html-dom-element-api

## Element

### Element.clientHeight

- This read-only property is zero for elements with no CSS or inline layout boxes; 
  - otherwise, it's the inner height of an element in pixels
  - It includes padding but excludes borders, margins, and horizontal scrollbars (if present).
- clientHeight can be calculated as: CSS height + CSS padding - height of horizontal scrollbar (if present).
  - This property will round the value to an integer. 
  - If you need a fractional value, use `element.getBoundingClientRect()` .

- When `clientHeight` is used on the root element (the `<html>` element), (or on `<body>` if the document is in quirks mode), the viewport's height (excluding any scrollbar) is returned. 
  - This is a special case of clientHeight.
