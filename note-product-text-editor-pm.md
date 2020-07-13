---
title: note-product-text-editor-pm
tags: [editor, product]
created: '2020-07-13T13:50:42.498Z'
modified: '2020-07-13T13:54:55.572Z'
---

# note-product-text-editor-pm

## 编辑器开发体验

- 编辑器大致分为两种: 源代码编辑器和富文本编辑器，可以基于富文本实现源代码编辑器
- 基于HTML DOM的Contenteditable属性来实现(传统方式)
  - 代表是UEditor、TinyMCE、Quill
  - contenteditable是浏览器DOM的一个原生属性，值为true时表示该元素变为可编辑状态
  - 因此原生就直接支持很多内容编辑操作，包括光标位移、内容选择的行为、键盘事件（如方向键控制光标）等等
  - 辅以iframe技术，可以将编辑器放在一个独立的docment对象下，与页面的document对象分离
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

## solution-catalog-text-editor 

- react-page
  - renderer package基于slate实现
