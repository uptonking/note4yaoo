---
title: pm-editor-text
tags: [editor, pm, pmgr, text-editor]
created: 2020-07-13T13:50:42.498Z
modified: 2021-05-14T14:33:52.786Z
---

# pm-editor-text

# guide

- features
  - local-first
  - database views
  - collaborative editing
  - markdown text with extensions
  - table designer
  - 类似notion-database支持多视图的page支持多视图，摘要版、完整版、卡片版

- block-style editor
  - 内容视觉上为block，默认互不影响
  - 能够选择多个block/card，然后一起拖拽移动
    - 优点是灵活，缺点是凌乱，还可以参考masonry布局

- comparison
  - popular: [prosemirror, codemirror, slate, draft](https://www.npmtrends.com/prosemirror-state-vs-draft-js-vs-@codemirror/state-vs-slate-vs-codemirror-vs-@editorjs/editorjs)
  - unpopular: @editorjs/editorjs, @craftjs/core, @tiptap/core, @codemirror/basic-setup

- one data model to power editor and rendering
  - 默认渲染为普通html元素，获取到焦点时变为编辑器
  - 使用场景是评论
# draft
- 可拖拽的主界面
  - 考虑设计成类似trello这类数据卡片，可以任意拖动、缩放、auto-layout自动对齐

- 编辑器文内拖动有什么用
  - 这是word很早就提供的特性，也是浏览器contenteditable默认支持的特性
  - 但浏览器实现得并不好，如拖动blockquote的p标签内的文本时，chrome会添加新标签span，但firefox不会

- 难点
  - 渲染wysiwyg时采用virtual render
  - 支持可缩放的编辑器，用于将编辑器嵌入画板/设计工具的场景
# 协作相关

# track-changes 和 评论在UI上具有相似性

- UI上
  - 一般都放在侧边栏
  - 都提供操作按钮，如track-changes支持accept/reject，评论支持resolve/delete
  - 都支持回复

- 评论只能自己删除自己的

- 实时协作时，一般会自动生成track-changes的消息，如insert/remove
# track-changes vs revision-history
- [CKEditor 5 - comparing Revision History with Track Changes](https://ckeditor.com/blog/ckeditor-5-comparing-revision-history-with-track-changes/)

- Revision History, on the other hand, focuses on providing users with three additional and key functionalities that Track Changes does not have. 
  - creating snapshots (revisions) of content, where such a snapshot is the state of the content at the time the user makes a save
  - comparing individual revisions with each other
  - restoring individual revisions

- In summary, Track Changes is more of a functionality improving the aspect of collaboration between users, 
  - while Revision History extends the application’s capabilities with content audit-trail and versioning functionality.
# notion细节记录

## 文本格式相关

- 对于加粗、斜体，只有选中的所有内容都为加粗时，工具条的加粗按钮才是高亮颜色

## markdown支持

# 编辑器开发体验
- 编辑器大致分为两种: 源代码编辑器和富文本编辑器，可以基于富文本实现源代码编辑器
- 基于HTML DOM的Contenteditable属性来实现(传统方式)
  - 代表是UEditor、TinyMCE、Quill
  - contenteditable是浏览器DOM的一个原生属性，值为true时表示该元素变为可编辑状态
  - 因此原生就直接支持很多内容编辑操作，包括光标位移、内容选择的行为、键盘事件（如方向键控制光标）等等
  - 辅以iframe技术，可以将编辑器放在一个独立的document对象下，与页面的document对象分离
  - 问题
    - 编辑器中存在不可编辑元素，会有浏览器兼容性的问题，如火狐浏览器下光标无法正确移动甚至无法删除这个元素
    - 用户行为难以控制，难以抽象编辑器内的视图逻辑关系并将它们映射到代码模型中
    - 光标（选区）的视觉位置与逻辑位置可能不吻合
- 基于自定义Model的实现
  - 代表是draft.js、trix
  - 定义一套编辑器内部使用的数据结构（model），与用户在编辑器内所见的Dom视图相映射
  - 通过捕获用户的操作行为，由原先的直接操作Dom，改为更新数据结构状态，再将更新后的状态映射至视图的方式，来实现编辑器的所见即所得
  - 由于用户操作实际影响的是内部的数据结构，且每次操作产生的结果都被控制在一定范围内（只影响部分节点），可以较为容易的通过锁和diff算法来合并短时间内的多次修改
- ref
  - https://zhuanlan.zhihu.com/p/37051858
  - https://www.zhihu.com/question/24328297
  - https://www.oschina.net/translate/why-contenteditable-is-terrible
# text-editor-solution-catalog
- react-page
  - renderer package基于slate实现
# ref
