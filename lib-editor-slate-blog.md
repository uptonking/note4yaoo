---
title: lib-editor-slate-blog
tags: [blog, slate-editor]
created: 2022-05-15T21:14:02.900Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-blog

# guide

# slate-blogs

## [新版编辑器 Slate.js 的设计 - 知乎](https://zhuanlan.zhihu.com/p/179253951)

- 目前这套插件机制真是优雅（简陋），用的函数链式调用的方法，对调用次序敏感是个大问题。
  - slate-react层问题很多而且没写测试，用了model immer的情况下，为了性能和保持对象，多级嵌套用了dirtyPath层层刷新对象这个机制很蛋疼，还不如直接可变数据算了
- 插件机制确实是简陋，但这只是最简单的一种思路。针对复杂的业务场景扩展可以像 webpack plugin或者vscode plugin去实现。
- 至于嵌套更新问题，如果全用可变的数据结构，在每个组件项的渲染上，光用shallowEqual可能就不管用了，需要采用类似 lodash 的deep equal，这会增加diff 对比的成本，而更新嵌套对象只是新开辟空间再赋值而已。（您也提到了性能问题，像百度脑图的更新机制就如同您所说，就是一个可变数据结构，当节点多的时候，卡顿的问题就会比较明显了）

## [slate系列 - 不同空格的处理](https://yasinchan.com/post/html-different-space-slate.html)

- slate的数据在最终渲染到页面后会出现问题，表现为行首空格消失，文字之间的多个空格变成一个空格。而一般的 div contenteditable 中的空格可以连续渲染。
  - 为避免这种情况，我们可以在 slate 中可以在最终保存的数据做二次处理
- https://yasinchan.com/post/
  - slate系列

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
# more-slate
- [slate-angular 正式开源 202106](https://zhuanlan.zhihu.com/p/382685492)

- [slatejs 编辑器表格---合并单元格 - 掘金](https://juejin.cn/post/7080046216259567646)
