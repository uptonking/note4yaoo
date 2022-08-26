---
title: lib-editor-slate-blog
tags: [blog, slate]
created: 2022-05-15T21:14:02.900Z
modified: 2022-05-15T21:14:14.339Z
---

# lib-editor-slate-blog

# guide

# slate-blogs

## [Adding A Commenting System To A WYSIWYG Editor/Slate](https://www.smashingmagazine.com/2021/05/commenting-system-wysiwyg-editor/)

- https://github.com/shalabhvyas/wysiwyg-editor
  - /202106

- Comment Threads As Marks 
  - The way we represent comment threads as marks is that each comment thread is represented by a mark named as `commentThread_threadID` where threadID is a unique ID we assign to each comment thread.
  - The way this works (as it does with any mark) is that when a mark property is being set on the selected text, Slate’s `Editor.addMark` API would split the text node(s) if needed such that in the resulting structure, text nodes are set up in a way that each text node has the exact same value of the mark.

- Highlighting Commented Text 
  - 每个评论部分在编辑器数据模型中对应的属性名是 COMMENT_PREFIX_ID，值是boolean
  - 直接根据slate的leaf对象计算comment数量，然后渲染对应的CommentedText组件

- add a button to the toolbar that lets the user add comments
  - assign an id to the new comment
  - add a new mark to slate document

- Overlapping Comments
- This implies in the case of overlapping comments, the most important thing to consider is — once the user has inserted a comment thread, would there be a way for them to be able to select that comment thread in the future by clicking on some text inside it? 
  - If not, we probably don’t want to allow them to insert it in the first place.
  - To ensure this principle is respected most of the time in our editor, we introduce two rules
- Before we define those rules, it’s worth calling out that different editors and word processors have different approaches when it comes to overlapping comments. 
- 👉 Shortest Comment Range Rule  
  - 若当前文档包含多条评论，第一条该显示哪条？
  - If the user clicks on text that has multiple comment threads on it, we find the comment thread of the shortest text range and select that.
  - 若当前选择重叠时，是否存在完全被挡住永远无法展示的评论，如选区A=选区B+选区C，使用评论侧边栏更好
- 👉 Insertion Rule
  - If the text user has selected and is trying to comment on is already fully covered by comment thread(s), don’t allow that insertion.
  - This is so because if we did allow this insertion, each character in that range would end up having at least two comment threads (one existing and another the new one we just allowed) making it difficult for us to determine which one to select when the user clicks on that character later.
  - 但飞书和notion都支持在已评论文字内部再选择文字评论，问题是光标处于文字内部时，该显示那条评论无法确定

- 点击已评论的文字，onClick方法会将当前最短评论id设为activeId
  - 其实不需要单独在全局保存此状态，只需要在editor.selection中判断当前光标位置文本的Comment_id是否和文本相等

- when the user clicks on a commented text node, we use the Shortest Comment Range Rule to determine which comment thread should be selected
  - 1. Find the shortest comment where click
    - Get all the comment threads at the text node
    - Traverse in either direction from that text node and keep updating the thread lengths being tracked
    - 找到最短评论长度：非评论节点、起止节点、公共空白节点
  - 2. Set that comment thread to be the active comment id
  - 3. hightlight active comment
    - 利用 `CommentedText` 组件的 `is-active` 属性

- Adding Comment Thread Popovers
  - build a Comment Popover to let the user add comments
  - find the Slate Node closest to the DOM node where the click event happened
  - ReactEditor.toSlateNode(editor, clickedDOMNode)
  - Slate has a helper method toSlateNode that returns the Slate node that maps to a DOM node or its closest ancestor if itself isn’t a Slate Node
  - Comment Popover has all the code it needs to allow inserting new comments and updating the Recoil state

- sidebar用来解决编辑器内部分评论可能无法选中的问题
  - we need a Comments Sidebar that lets the user get to any and all comment threads in the document.
  - When the document is loaded in the editor, we need to scan the document to find all the comment threads and add them to the Recoil atoms

- In the real-world usage of the Commenting System, comment threads are likely to be stored separately from the document contents themselves. 
- If a document is really long and has a lot of users collaborating on it on a lot of comment threads, we might have to optimize the initialization code to only load comment threads for the first few pages of the document. 
- Alternatively, we may choose to only load the light-weight metadata of all the comment threads instead of the entire list of comments which is likely the heavier part of the payload.

- Resolving And Re-Opening Comments
  - is-resolved
  - is-active

## [Slate 介绍分析与实践](https://coldstone.fun/post/2020/12/13/slate-intro/)

- 特点
  - 插件作为一等公民，能够完全修改编辑器行为
  - 数据层和渲染层分离，更新数据触发渲染
  - 文档数据类似于 DOM 树，可嵌套
  - 具有原子化操作 API，理论上支持协同编辑
  - 使用 React 作为渲染层
  - 不可变数据结构 Immer

- 渲染原理
  - Slate的文档数据是一颗类似DOM的节点树，slate-react 通过递归这颗树生成 children 数组，这个数组有两种类型的组件 Element 和 Text， 最终 react 将 children 数组中的组件渲染到页面上
- 传递渲染函数 renderElement 和 renderLeaf 给 Editable 组件，对元素和叶子节点进行自定义渲染。

- 不足
  - 还没有发布正式版，处于 Beta 阶段，API 可能会有变化
  - 渲染层目前只有 React，要在其他框架中使用需要自行实现
  - 数据渲染分离，需要完全控制用户输入行为，否则可能导致数据和渲染不同步
  - 基于 contenteditable 无法突破浏览器的排版效果
  - 对中文输入支持不足，详见此 链接
  - 社区驱动开发，问题可能得不到及时修复

## [富文本编辑器 wangEditor v5 渲染逻辑 - Model ，DOM，HTML 三者的关系](https://juejin.cn/post/7055206586175717390)

> 暂不支持移动端。

- wangEditor v5 是基于 slate.js 为内核进行开发的，slate.js 输入输出的数据一直是 JSON 格式，没有 HTML 格式。所以，我也就基于这一点，一直坚持用 JSON 格式数据。
- slate.js 能基于 JSON 格式，本质原因是它完全依赖于 React 框架，使用 React 来渲染页面。而 React 本身就是一个“数据驱动视图”的框架，所以 slate.js 提供 JSON 作为数据，交给 React 来渲染视图，这很合理。
- 而 wangEditor 虽然基于 slate.js 为内核，但它没有基于 Vue React 等任何框架。既然没有框架要求，那就需要自己去考虑渲染逻辑，那也就需要 HTML 。
- 很不幸，HTML 格式就是“乱来”的代名词。
- 但是呢，对 HTML 的支持又是势在必行的，所以这个问题我想了好久，最终得出一个虽不完美但可行的方案：HTML 仅支持 wangEditor 输出的格式（包括 V4 和 V5），其他的格式就保证了。

- JSON 数据就是编辑器的 Model 。可以把编辑器认为是一个黑盒，输入输出的可以是 HTML ，但其内部数据是规定格式的 JSON 数据。
  - 现代富文本编辑器的 Model 都是基于一种 DSL 的，不会直接基于 HTML 。因为 HTML 格式过于灵活，不好控制，而自己的 DSL 是完全可控的。
- Model（即 JSON 数据）需要实时的渲染到编辑器视图中，即把 Model 渲染为 View 。而且不同的组件要渲染为不同的 DOM 类型
- 数据驱动视图，这一点和 Vue React 一样，所以我们也做了类似的设计：第一，把 Model 转换为 vdom ；第二，把 vdom patch 到真实 DOM 中（使用 snabbdom.js）
- 但是还要考虑各个组件渲染为不同的 DOM 类型，所以需要让各个模块注册自己的 Render 函数，再统一渲染。
# more-slate
- [slate-angular 正式开源 202106](https://zhuanlan.zhihu.com/p/382685492)
