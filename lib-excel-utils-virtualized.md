---
title: lib-excel-utils-virtualized
tags: [excel, lib, utils, virtualized]
created: 2022-08-24T10:48:42.566Z
modified: 2022-08-24T10:49:48.139Z
---

# lib-excel-utils-virtualized

# guide

- ref
  - [How does windowing work?](https://bvaughn.github.io/forward-js-2017/#/12/5)
  - [List Virtualization](https://www.patterns.dev/posts/virtual-lists/)
# virtualized-blog
- [React Virtual Window - virtualise anything for a performance boost!](https://dev.to/miketalbot/react-virtual-window-virtualise-anything-for-a-performance-boost-full-tutorial-3moe)
  - A virtualised array of items with variable height, each item can change height.
  - https://github.com/miketalbot/virtual-window /js
  - https://codesandbox.io/s/virtual-nlm7m-nlm7m

- [Virtualization: A method to render your data efficiently](https://medium.com/@unnatibamania8/virtualization-a-method-to-render-your-data-efficiently-f5b325214ce8)
  - List virtualization is a concept where a window or a section loads and renders when you keep scrolling.
  - we’ll use tanstack-virtual library in this tutorial.
# discuss
- ## 

- ## 

- ## Would it be possible to render only the text of the components that are off-screen, 
- https://twitter.com/tomlienard/status/1554016255430066176
  - then render them completely as they appear on screen? That would allow Cmd+F but not sure if it's really feasible.
- Yep this is what I’ve done in the past - for each table row I rendered a 90% simpler version with the text to search - with css to maintain future height. Then when it comes into view render the full functionality
- there will be jarring content shift once the user reached / moved to the content, so we need to think about solving that first
  - 1 - Do not use the search and find native to browse, 
  - 2 - Do the search query directly on the data model, 
  - 3 - Virtualization implies computing layout, (items position and dimension) so once you have identified the data matching the search, just compute how much you need to scroll

- ## Killer browser/library feature: a virtualized list that only renders what is currently visible, 
- https://twitter.com/erikras/status/1285241033694105601
  - but ALSO puts the text content of the non-visible items of the list into a place where the browser's "Find..." feature can locate it and scroll to it.
