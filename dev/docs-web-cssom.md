---
title: docs-web-cssom
tags: [cssom, docs, web]
created: 2020-08-08T17:04:11.201Z
modified: 2020-08-08T17:06:31.817Z
---

# docs-web-cssom

# CSS Object Model (CSSOM)

- The CSS Object Model is a set of APIs allowing the manipulation of CSS from JavaScript. 
- It is much like the DOM, but for the CSS rather than the HTML. 
- It allows users to read and modify CSS style dynamically.

- CSSOM API Reference
  - CSSStyleSheet
  - CSSRuleList
  - ...
- CSS Typed Object Model 
  - CSSKeywordValue
  - CSSStyleValue
  - CSSPositionValue
  - StylePropertyMap
  - ...
- Obsolete CSSOM interfaces 
  - CSSValue
  - CSSValueList
  - CSSPrimitiveValue 

# ref

- [mdn: CSS Object Model (CSSOM)](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model)
- https://github.com/jsdom/cssstyle
  - /MIT/64Star/202004
  - A Node.js implementation of the CSS Object Model CSSStyleDeclaration interface
  - The primary use case is for testing browser code in a Node environment.
- https://github.com/cssobj/cssobj
  - /MIT/249Star/201803
  - Runtime CSS manager, Turn CSS into dynamic JS module, Stylesheet CRUD (Create, Read, Update, Delete) in CSSOM, Solve common problems of CSS-in-JS.
  - The power of cssobj is CSS CRUD (Create, Read, Update, Delete), dynamically change above CSS
  - How it worked?
    1. cssobj first parse js object into Virtual CSSOM middle format.
    2. The internal cssom plugin will create stylesheet dom, and apply rules from middle format.
    3. When the js object changed, cssobj will diff CSSOM rules (add/delete/change) accordingly.
- https://github.com/cssobj/cssobj-converter
  - Convert from normal css/LESS/SASS/SCSS to cssobj
