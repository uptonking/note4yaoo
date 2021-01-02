---
title: toc-lib-fwk-tagged-template-literals
tags: [js, tagged-template-literals]
created: '2020-11-05T09:27:49.883Z'
modified: '2020-12-19T13:03:37.613Z'
---

# toc-lib-fwk-tagged-template-literals

## tagged-template 

- https://github.com/developit/htm
  - htm is JSX-like syntax in plain JavaScript - no transpiler necessary.
  - JSX alternative using standard tagged templates, with compiler support.
  - HTM (Hyperscript Tagged Markup)
  - Develop with React/Preact directly in the browser, then compile htm away for production.

- https://github.com/choojs/nanohtml
  - HTML template strings for the Browser with support for Server Side Rendering in Node.
  - lit-html has similar promises as React, except it uses browser native mechanisms to deliver, like `<template>` and shadow-dom. 
    - Nanohtml seems just like DOM literals (at first sight, I have none experience with it) without rendering optimizations.
  - https://github.com/choojs/nanomorph
    - fast diffing algorithm for real DOM nodes

## more-ttls

- https://github.com/shama/yo-yoify
  - Transform choo, yo-yo, or bel template strings into pure and fast document calls.

- https://github.com/zspecza/common-tags
  - A set of well-tested, commonly used template literal tag functions for use in ES2015+
  - common-tags initially started out as two template tags I'd always find myself writing - one for stripping indents, and one for trimming multiline strings down to a single line.
  - Over time, I found myself needing a few more template tags to cover edge cases - ones that supported including arrays, or ones that helped to render out tiny bits of HTML not large enough to deserve their own file or an entire template engine. So I packaged all of these up into this module.

``` JS
import { html } from 'common-tags'
let fruits = ['apple', 'orange', 'watermelon']
html `
  <div class="list">
    <ul>
      ${fruits.map(fruit => `<li>${fruit}</li>`)}
      ${'<li>kiwi</li>\n<li>guava</li>'}
    </ul>
  </div>
`
```
