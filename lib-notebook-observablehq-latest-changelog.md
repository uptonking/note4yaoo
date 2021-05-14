---
title: lib-notebook-observablehq-latest-changelog
tags: [changelog, observablehq]
created: '2021-05-14T14:52:22.020Z'
modified: '2021-05-14T14:52:48.486Z'
---

# lib-notebook-observablehq-latest-changelog

# guide

# discuss-stars

- ## [Cell Modes](https://observablehq.com/@observablehq/cell-modes)
- Previously, writing an Observable notebook was optimized for JavaScript. 
  - there was a little extra work for non-JavaScript cells -- for example, you had to manage the opening and closing backticks for a Markdown cell.
- Now, you can choose the mode in which you want to edit a cell. 
  - The mode of a cell affects the way the cell is parsed and evaluated (treating the contents of the cell as if it were wrapped in the appropriate tagged template), as well as the editing options displayed in the editor.
- The mode defaults to JavaScript for newly created cells, but newly split cells will keep the mode of the original cell.

# changelog

- 2021-05-13
  - We're excited to announce Cell Modes!
  - You can choose the mode you want to edit - Javascript, Markdown, HTML and TeX.
  - when editing a cell in Markdown mode, you can simply write plain Markdown and get the output that you want. 
  - No more managing the opening and closing backticks of the Markdown tagged template literal, no more need to escape backticks!
