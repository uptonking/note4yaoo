---
title: lib-editor-quill-blog
tags: [blog, quill]
created: 2023-02-09T18:30:10.814Z
modified: 2023-02-09T18:30:19.001Z
---

# lib-editor-quill-blog

# guide

# blogs-collab

## ⌛️ [A Document Revisions System in JavaScript - DEV Community_202208](https://dev.to/kornatzky/a-document-revisions-system-in-javascript-1o3h)

## [Yjs + Quill 实现文档多人协同编辑器开发（基础+实战） - 掘金 _202309](https://juejin.cn/post/7273432426772070457)

- 
- 
- 
- 

# blogs

## [现代 Web 富文本编辑器 Quill.js - 从基本使用到核心概念 - 掘金_202101](https://juejin.cn/post/6918893948412887053)

## [How Quill module works? 1/10 - DEV Community_202103](https://dev.to/kagol/how-quill-module-works-319f)

- [How does Quill describe editor content?2/10](https://dev.to/kagol/how-does-quill-describe-editor-content-1i5g)
- [How does Quill convert Delta to DOM? 3/10_202104](https://dev.to/kagol/how-does-quill-convert-delta-to-dom-2664)

## [Quill internals and the jumping cursor + the Selection and Cursor classes _202112](https://billauer.co.il/blog/2021/12/quill-cursor-jump/)

- Everything in this post relates to Quill v1.3.7. I don’t do web tech for a living, and my knowledge on Quill is merely based upon reading its sources.
- I can suggest one thing to do: With your browser’s JavaScript debugger (Google Chrome recommended), put a breakpoint on the Selection class’ setNativeRange() method, and an additional breakpoint on the return statement marked below in read. 
- 

# blogs-internals
- [Quill源码初探 - 掘金 _202105](https://juejin.cn/post/6957219459421437966)
  - quill实例化的过程
  - 选区文字加粗流程
  - 输入和删除文本的流程: ScrollBlot作为所有blots的根节点, 使用了MutationObserver监听dom结点的变化

- [QuillJS 编辑器源码学习 - 知乎 _202105](https://zhuanlan.zhihu.com/p/374592382)
  - 描述文档内容的时候，为什么都是insert？
    - insert比text更通用，因为富文本编辑器里面不仅仅有文字，还有图片、视频等元素
  - 描述文档内容的时候为什么最后要有一个换行（\n）?
    - 把行格式的属性放到换行符上去， 这样在删除换行符的时候行样式也会跟着被删除，

- [现代富文本编辑器Quill的内容渲染机制 - 知乎 _202005](https://zhuanlan.zhihu.com/p/139533735)
  - [Quill富文本编辑器的实践 - DevUI - 知乎 _202105](https://zhuanlan.zhihu.com/p/375896194)
  - [对富文本编辑器的探索 - 掘金 _202104](https://juejin.cn/post/6952115345968594974)

- [富文本编辑器 Quill.js 系列一：Delta 文档结构 - 掘金 _202211](https://juejin.cn/post/7166159151880486925)
- [富文本编辑器 Quill.js 系列二：Parchment 文档模型 - 掘金](https://juejin.cn/post/7166160927128043528)
- [富文本编辑器 Quill.js 系列三：架构与扩展 - 掘金](https://juejin.cn/post/7166171572372242463)

- [富文本编辑器 quill.js 开发(二): 升级与表格功能 - Grewer - 博客园 _202211](https://www.cnblogs.com/Grewer/p/16853103.html)
  - [富文本编辑器 quill.js 开发(三): 光标和选区 - Grewer - 博客园](https://www.cnblogs.com/Grewer/p/17074202.html)
  - [富文本编辑器 quill.js 开发(四): 自定义格式扩展 format - Grewer - 博客园](https://www.cnblogs.com/Grewer/p/17430021.html)
  - [富文本编辑器 quill.js 开发(五): 自定义插件 Modules - Grewer - 博客园](https://www.cnblogs.com/Grewer/p/17627630.html)

- [quill深入浅出 - 前端技术杂谈 - SegmentFault 思否 _201905](https://segmentfault.com/a/1190000019114688)
  - vue-quill-practice 中的src/components/RichTextEditor/index.vue提供一些示例, 但是因为是从业务代码中拿出来的
  - dom修改后，如何同步到delta?
    - ScrollBlot会创建一个 MutationObserver, 用来监控DOM更新。DOM更新时会调用ScrollBlot的update方法。在Quill的scroll blot中重写了update方法，其中对外抛出SCROLL_UPDATE事件和mutations参数。
    - editor会监听SCROLL_UPDATE事件，然后触发editor的update方法
    - 在editor的update方法中，会依据mutations构建出对应的delta数组，与已有的delta合并，使当前delta保持最新
  - delta修改后，如何同步到dom?
    - setContents传入delta后，会遍历delta数组, 生成相应的Blot, Attributor， 然后生成DOM结构，然后进行format
    - quill.setContents -> this.editor.applyDelta -> this.scroll.formatAt
# blogs-vendors

## 🌰 [appflowy: How we built a highly customizable rich-text editor for Flutter _202212](https://blog.appflowy.io/how-we-built-a-highly-customizable-rich-text-editor-for-flutter/)

- in the early versions (v0.0.1 to v0.0.5) of AppFlowy, we used flutter_quill as our editor component.
  - we have encountered problems with extensibility, consistency, and code coverage.
- we have decided to design and develop the new AppFlowy Editor component ourselves.

- Quill.js uses Delta as the data structure, while Slate.js uses tree nodes as the data structure. 
  - 💡 Ultimately we have elected to use a tree node like Slate.js to assemble the documents while continuing to use Delta for the data storage of text nodes.
- Why do we use a node tree?
  - The entirety of the document data is described using a single Delta data which does not allow us to easily describe complex nested scenarios.
  - our preference is to use a node tree like Slate.js to describe the document in chunks, where each chunk’s additions, deletions, and modifications only affect the changes to the current node.
- Why do we still use Delta for the text node?
  - If text with different styles continues to be split into different nodes, it will increase the complexity of the tree node structure.
  - The ability to export a text change delta is already supported in Flutter, so it is easy to substitute the Flutter text change delta to Delta.
# more
- [Quill: The DOM, Parchment, and Delta views of the document](http://billauer.co.il/blog/2021/12/quill-document-views/)
