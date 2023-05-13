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
  - [如何实现一个高度自适应的虚拟列表 - 知乎](https://zhuanlan.zhihu.com/p/366416646)
# virtualized-blog

## [长列表优化之虚拟列表 - 知乎](https://zhuanlan.zhihu.com/p/444778554)

- 实际上在业务开发中，基本很少碰到高度项列表固定的情况，大部分是文本、图片、富文本等不定的高度，对于这类不定的高度那我们该如何处理呢？
- 对于这类不定的高度，我们一般可以分为两种类型：
  - 1. 逻辑动态高度
  - 2. 动态高度（由渲染内容决定高度）比如，文本、图片、富文本。
  - 以上两种类型都可以在内容渲染完成后，获得其高度；
  - 但是不同的是 逻辑动态高度 也可以在渲染前通过业务数据计算得出，本质上也可以理解为固定高度，只是获取方式复杂了些；
  - 而类型2中的只能在内容渲染完成后才可以获取。

- 探索优化
- 滚动过快出现会白屏
  - 列表渲染区是可以大于等于可视区，这里的采取措施就是列表渲染区域要大于可视区。
  - 采用skeleton加载骨架屏来代替原有的不渲染部分，这样当滚动过快时，白屏也就替换为了加载屏。
- 滚动时有大量的计算
  - positions数组其实是个标准的按照各项位置升序的有序数组
  - 最重要的和调用次数最多的逻辑是计算startIndex
  - 可以采用二分查找法来进行优化，时间复杂度也从O(n) 降为 O(logn)

- 虚拟列表的通用模型 ，而对于其他平台如小程序、IOS、flutter等的实现，或者能不能抽象出一套通用架构

## [React Virtual Window - virtualise anything for a performance boost!](https://dev.to/miketalbot/react-virtual-window-virtualise-anything-for-a-performance-boost-full-tutorial-3moe)

  - A virtualised array of items with variable height, each item can change height.
  - https://github.com/miketalbot/virtual-window /js
  - https://codesandbox.io/s/virtual-nlm7m-nlm7m

- [Virtualization: A method to render your data efficiently](https://medium.com/@unnatibamania8/virtualization-a-method-to-render-your-data-efficiently-f5b325214ce8)
  - List virtualization is a concept where a window or a section loads and renders when you keep scrolling.
  - we’ll use tanstack-virtual library in this tutorial.
# discuss
- ## 

- ## An interesting virtualization strategy: just render some placeholder content and replace it with the actual content once it becomes visible.
- https://twitter.com/fabiospampinato/status/1653083336510783489
  - See how much less lag my EmojiPicker virtualized like this causes. 
  - You get most of the performance _and_ most of the simplicity also.
- Currently working on building very large (50-100k rows x 10+ columns) data tables at work. 
  - We are using tanstack virtual core as a base. 
  - Currently for render layer using the absolute positioning + transformY approach recommended by the docs.
- Yeah that's like the normal row-based approach. It can be pushed a bit further than that potentially, depending on what one is optimizing for.

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
