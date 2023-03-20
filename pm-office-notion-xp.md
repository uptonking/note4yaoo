---
title: pm-office-notion-xp
tags: [notion, office, pm, xp]
created: 2022-03-17T17:49:28.980Z
modified: 2022-03-17T17:49:45.743Z
---

# pm-office-notion-xp

# inspiring

- 使用多维表格组件进行文档管理，而不是用文档树、文件夹
# usage

# pros

# cons

# features

## 文本格式类

- notion不支持左中右对齐
  - [How to center text alignment like this?__202201](https://www.reddit.com/r/Notion/comments/rry43b)

## block操作类

# notion教程-沙牛清单
- notion三大特性
  - 模块化操作：拖拽、转换、分栏
  - 内容结构化：子页面
  - 数据化
# guide
- [Notion保姆级公开课](https://www.bilibili.com/video/BV1EP4y1s7Bp/)

- [Obsidian的保姆级公开课](https://www.bilibili.com/video/BV1H44y1n71k/)
# discuss
- ## 

- ## 

- ## 

- ## Craft 对开发者太不友好，社区也没运营起来，因此我又从 Craft 转移到 Notion 了。
- https://twitter.com/_Xheldon/status/1637481908136468480
  - 本来想找个现成的迁移工具，研究了一下 Notion API，发现它不支持图片上传，然后正当要放弃的时候，尝试了 Notion 导入 Word，发现它可以把 Word 中内嵌的图片上传到自己的 AWS 服务上，因此我想了个曲线救国的办法，
  - 就是先将 Craft 全部文件导出到 Markdown 格式，同时它会在导出的时候，将文件中引用的图片放到 .md 文件的同级目录，之后我再使用 pandoc 工具，将 Markdown 文件转成 docx 文件即可。当然，Notion 导入 Word 不支持嵌套文件夹，所以我只能将所有文件到处到同一个目录后，手动调整层级。
  - 需要注意的是，Notion 不支持超过 50M 的文件导入，因此你可能需要分割一下大文件，导入后再合并。

- ## Front-end Practical Q: Has a particular algorithm in a function body ever been the reason your app is slow?
- https://twitter.com/jitl/status/1615423205380091904
  - e.g. I used `Array.indexOf` instead of keeping track of nodes I've seen in an object.
- indexOf very well could be faster in most cases than using a set

- Yes in @NotionHQ:
  - O(n^3) checks against a block's ancestors; always lock up the UI or cause backend latency spikes
  - O(n^2) checks for "closest neighbor UI element" in list of UI elements; caused jank on large pages
  - Array.indexOf -> Set.contains is a win in inner loops with big N
- Another case is searching our tree-like data model, eg for "what is the next block with a comment after this block, in DFS order?". 
  - For that use-case, I built a memoized, reactive subtree traversal. Substantially reduced jank on larger pages for a bunch of systems.

- My exp: large app had a lot of perf problems stemming for inefficient uses of simple loops, for instance: instead of using Array.filter folks would Array.forEach into another array and return the new array. Do this nonsense enough times and you will see perf issues. Sometimes for virtualized lists. They did this when chunking (lazy display) of data for instance. Some loops were simply unbound. Others were nested. It was just poorly architected across the board

- In Flutter Apps working with long lists or graphics based on lots of data, the types of loops I use and how I keep track of things I've seen and can disregard on future iterations makes a huge difference in rendering performance.
