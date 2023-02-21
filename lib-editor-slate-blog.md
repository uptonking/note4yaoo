---
title: lib-editor-slate-blog
tags: [blog, slate-editor]
created: 2022-05-15T21:14:02.900Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-blog

# guide

# slate-blogs

## [slate 系列 - 不同空格的处理 | YasinChan 的博客](https://yasinchan.com/post/html-different-space-slate.html)

- slate的数据在最终渲染到页面后会出现问题，表现为行首空格消失，文字之间的多个空格变成一个空格。而一般的 div contenteditable 中的空格可以连续渲染。
  - 为避免这种情况，我们可以在 slate 中可以在最终保存的数据做二次处理
- https://yasinchan.com/post/
  - slate系列

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

- [Building A Rich Text Editor (WYSIWYG)](https://www.smashingmagazine.com/2021/05/building-wysiwyg-editor-javascript-slatejs/)

## [Slate 介绍分析与实践_202012](https://coldstone.fun/post/2020/12/13/slate-intro/)

- 特点
  - 插件作为一等公民，能够完全修改编辑器行为
  - 数据层和渲染层分离，更新数据触发渲染
  - 文档数据类似于 DOM 树，可嵌套
  - 具有原子化操作 API，理论上支持协同编辑
  - 使用 React 作为渲染层
  - 不可变数据结构

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

## [基于 slate.js（不依赖 React）设计富文本编辑器_王福朋_202105](https://juejin.cn/post/6968061014046670884)

- 为何要基于 slate.js ？ 为何不是自研内核？
  - 核心目的，是做出一款稳定、易用、高扩展性的开源产品，并不是搞极客精神和造轮子。
  - 自研成本非常高，耗时长，bug 多。
  - PS：如果你有深度的技术追求，可以先从解读源码、写 demo 开始，看个人精力和能力
- 基于 slate.js 并不意味着就很简单
  - 不依赖 React ，重写 View
  - 设计各种操作功能，如 toolbar 、tooltip 等
  - 设计扩展性，全面插件化
  - 开发各个富文本编辑器功能，特别是复杂的功能，如表格、代码高亮

- 整体设计
- 底层依赖
  - slate.js - 编辑器内核
  - snbbdom - view model 分离，使用 vdom 渲染 view
- view core
  - core 本身没有任何实际功能。需要通过 module 来扩展 formats、menus、plugins 等，来定义具体的功能。
  - editor - 定义 slate 用于 DOM UI 的一些 API
  - text-area - 输入区域 DOM 渲染，DOM 事件，选区同步，
  - formats - 输入区域不同数据的渲染规则，如怎样渲染加粗、颜色、图片、list 等。可扩展注册。
  - menus - 菜单，包括 toolbar、悬浮菜单、tooltip、右键菜单、DropPanel、Modal 等。可扩展注册。
- view-core 。它的核心作用：
  - 劫持用户输入和修改，使用 editor API 去触发 model 修改（或者 selection 修改）
  - editor change 要实时更新到 DOM ，保持 DOM 和 model（或 selection）的同步
  - 定义扩展机制（它本身没有什么实际功能），通过扩展 module 来实现具体的功能

- beforeinput 是一个比较新的 DOM 事件，去年还没有得到普遍支持。当前看来，主流浏览器已经支持了，特别是 FireFox 87 发布之后，参考 caniuse 
  - 对于还不支持的浏览器，可以用 keydown/keypress 来兼容
  - 监听 beforeinput 事件，然后根据不同的 inputType 执行不同的 editor API 。
- selection同步
  - DOM selection 变化会触发 document.addEvenListener('selectionchange', fn)
  - editor selection 变化会触发 editor.onChange事件。这样就可以做到相互同步。
- updateView 同步视图
  - editor onChange 时会触发更新视图，以保证 view 和 model 实时同步。分为两步：
  - 根据 model 生成 vnode
  - patch vnode
  - 第二步很简单，我们利用 snabbdom.js 来做 vdom 渲染
  - 关键在于第一步，生成 vnode 。 我们将逻辑拆分为两段： renderElement 和 renderText
- menu 应该是一个抽象，基于它来生成各种类型的菜单：
  - 传统的工具栏
  - 选中文字、元素之后的悬浮菜单
  - 右键菜单等
  - 还要支持各种类型：button select 等
- editor API 和 plugins
  - 参考 slate-react 源码，定义了一些全局 command ，在渲染 DOM 时很有用
- module 的设计
  - core 没有任何基础功能，所有功能都是 module 来扩展实现。module 可扩展的有：
  - menu
  - formats
    - renderElement
    - addTextStyle
  - plugin（即 slate plugin）
- 后续计划
  - 粘贴
  - 上传
  - i18n

## [富文本编辑器 L1 能力调研记录_王福朋_202104](https://juejin.cn/post/6954896971370856485)

## [Web 富文本编辑器 embed 卡片机制的设计与实践_王福朋_202103](https://juejin.cn/post/6939724738818211870)

## [slate.js - 从基本使用到核心概念_王福朋_202101](https://juejin.cn/post/6917123466307698696)

## [【译】自己实现 document.execCommand 富文本编辑器核心 API_王福朋_202008](https://juejin.cn/post/6864916875390910472)

## [富文本编辑器 wangEditor v5 渲染逻辑 - Model ，DOM，HTML 三者的关系_王福朋_202201](https://juejin.cn/post/7055206586175717390)

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
