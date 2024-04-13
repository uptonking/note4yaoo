---
title: lib-editor-editablejs-dev
tags: [editablejs, editor]
created: 2023-02-20T15:15:34.728Z
modified: 2023-02-20T15:15:50.211Z
---

# lib-editor-editablejs-dev

# guide

- features
  - not using `contenteditable` to avoid its compatibility issues
  - data model relies on Slate
    - 针对block editor，扩展了slate的model，增加了Grid、List相关数据结构和操作
  - collab using yjs
  - 示例是 block-editor，体验友好

- cons
  - 渲染层使用react，没有contenteditable事件，性能更高
  - ？选区变化完全由用户input事件触发，在移动端等设备上难以明确用户意图

- ✨ 不使用contenteditable而自绘光标，类似的有codemirror、textbus
  - 实现思路是在pointer事件的位置通过绝对定位放置一个oapcity为0宽约为1px的textarea来接收输入
  - 优势是避免浏览器自身特性的不兼容问题
  - 劣势是需要自己实现光标闪烁和选区变更
  - 影响accessibility
  - 浏览器devtools自身提供了的模拟focus的工具，是否可用？

- tips
  - 支持拖拽内嵌的二级列表

- demo
  - [Editable Playground](https://docs.editablejs.com/playground)
# dev

# docs
- Editable 是一个可扩展的富文本编辑器框架，专注于稳定性、可控性和性能。
  - 为此，我们没有使用原生的可编辑属性contenteditable，而是使用了一个自定义的渲染器，这使得我们可以更好地控制编辑器的行为。
  - 从此，您不必再担心跨平台和浏览器兼容性问题（例如Selection、Input），只需专注于您的业务逻辑。

- 为什么没有使用 canvas 渲染？
  - 虽然canvas渲染的性能可能比dom渲染更快，但是canvas的开发体验不佳，需要编写更多代码。
- 在富文本中我理想中的前端框架应该是这样的：
  - 没有虚拟DOM
  - 没有diff算法
  - 没有proxy对象
# more

# discuss
- ## 

- ## 

- ## [这个光标怎么实现的？ _202403](https://github.com/editablejs/editable/discussions/172)
- 使用 div 模拟光标的显示，然后再隐藏一个 textarea，需要输入的时候使用 textarea 接收输入的文本

- ## I'm hesitating between a canvas-based code, and a DOM-based approach
- https://stackoverflow.com/questions/33611482
- Canvas approach  
- pros:
  - dealing with everything myself
  - no limitations on event, contenteditable, 
  - ability to mix graphics & text

- cons:
  - have to draw and layout everything, painful (but doable)
  - browser clipboard is very painful (copy & paste):

- DOM based approach (à la MCE? CodeMirror?) 
- pros:
  - the browser is doing the layout
  - the clipboard & cut&paste might be easier

- cons:
  - contenteditable does not really work (why contenteditable is terrible)
  - event handling is messy. Can't figure out what are every possible user actions.
