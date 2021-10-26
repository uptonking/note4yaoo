---
title: docs-web-html-dom-element-api
tags: [docs, dom, web]
created: '2020-08-05T12:22:15.902Z'
modified: '2020-08-05T12:29:43.618Z'
---

# docs-web-html-dom-element-api

# Document

## DocumentOrShadowRoot.elementFromPoint()

- The `elementFromPoint()` method—available on both the Document and ShadowRoot objects—returns the topmost Element at the specified coordinates (relative to the viewport).
- Elements with pointer-events set to `none` will be ignored, and the element below it will be returned.
- If the element at the specified point belongs to another document (for example, the document of an `<iframe>` ), that document's parent element is returned (the `<iframe>` itself). 
- If the element at the given point is anonymous or XBL generated content, such as a textbox's scroll bars, then the first non-anonymous ancestor element (for example, the textbox) is returned.
- If you need to find the specific position inside the element, use `Document.caretPositionFromPoint()` .

# Element

- Node.parentNode
  - returns the parent of the specified node in the DOM tree.
  - `parentNode` is the parent of the current node. 
  - The parent of an element is an Element node, a Document node, or a DocumentFragment node.

## Element.clientHeight

- This read-only property is zero for elements with no CSS or inline layout boxes; 
  - otherwise, it's the inner height of an element in pixels
  - It includes padding but excludes borders, margins, and horizontal scrollbars (if present).
- `clientHeight` can be calculated as: CSS height + CSS padding - height of horizontal scrollbar (if present).
  - This property will round the value to an integer. 
  - If you need a fractional value, use `element.getBoundingClientRect()` .

- When `clientHeight` is used on the root element (the `<html>` element), (or on `<body>` if the document is in quirks mode), the viewport's height (excluding any scrollbar) is returned. 
  - This is a special case of clientHeight.
