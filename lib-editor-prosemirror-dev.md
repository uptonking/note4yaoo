---
title: lib-editor-prosemirror-dev
tags: [lib, prosemirror, text-editor]
created: '2021-05-06T09:39:21.604Z'
modified: '2021-05-06T09:39:53.522Z'
---

# lib-editor-prosemirror-dev

# guide
- 编辑器问题
  - 光标、选区、输入法、键盘事件

- tips
  - 分析一个产品或框架，需要考虑的方面：存储的数据结构、状态管理(更新转换)、视图渲染、样式主题

- prosemirror-renderer
  - `<canvas>`是标准的html元素，考虑实现nodeViews将特殊文本渲染到canvas，如表格、图表
  - tiptap的drawing示例，可以在空svg元素上画路径
  - atlaskit-editor开源了自定义renderer可以参考

- prosemirror-examples
  - tiptap, rich-markdown-editor, @atlaskit/editor-core, remirror
  - atlaskit-editor实现了layout多列插件和图片排版插件
# pieces
