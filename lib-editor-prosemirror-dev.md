---
title: lib-editor-prosemirror-dev
tags: [lib, prosemirror, text-editor]
created: 2021-05-06T09:39:21.604Z
modified: 2021-05-06T09:39:53.522Z
---

# lib-editor-prosemirror-dev

# guide
- prosemirror-pros
  - modular and extensible

- prosemirror-cons
  - 不支持动态改变schema
  - 与其他框架的集成不是很完美，ReactNodeView用不用portal的最佳实践不明确
  - 编辑器的多个插件存在依赖关系时如何处理

- features
  - Unopinionated
    - core is small and generic, allowing different types of editors
  - Customizable schemas
    - Document schemas allow editing documents with a custom structure
  - Modular
    - only load the code you need
  - Pluggable/Extensible
    - easily enable additional functionality
  - Collaborative editing
    - multiple people can work on the same document in real time
  - Functional
    - largely functional and immutable architecture to implement complex behavior

- who is using #prosemirror
  - atlassian, nytimes, guardian...

- roadmap-toys
  - prosemirror offline / local-first
  - prosemirror-codeblock
  - prosemirror-handsontable/data-grid
  - prosemirror-css/theming
  - vscode-prosemirror
  - page builder: WordPress-gutenberg, wix

- tips
  - 实现复杂组件可参考
    - 官方基于CodeMirror实现Embedded code editor的例子，使用NodeView，没用contentDOM
    - 官方Footnotes的例子，使用NodeView，没用contentDOM，但用了sub-editor，总共2个editor
  - 一个prosemirror document是一个无依赖的普通js object对象，所以实现第三方renderer也可行
  - 如果关注的重点是markdown和table，那就将更多的工作放在prosemirror层，增强通用性，将react wrapper层的工作尽量减少，方便迁移
  - 提供renderless/themeable不同封装层次/灵活性的组件
  - 类似footnotes使用多个pm-EditorView的例子

- 编辑器问题
  - 光标、选区、输入法、键盘事件
  - 首屏渲染完成后，用户输入文本时，是否还需要走一次完整的解析渲染流程
  - 分析一个产品或框架，需要考虑的方面：存储的数据结构、状态管理(更新转换)、视图渲染、样式主题

- prosemirror-renderer
  - `<canvas>`是标准的html元素，考虑实现nodeViews将特殊文本渲染到canvas，如表格、图表
  - tiptap的drawing示例，可以在空svg元素上画路径
  - atlaskit-editor开源了自定义renderer可以参考
  - atlaskit-editor实现了layout多列插件和图片排版插件
# [Marijn Haverbeke: Salvaging contentEditable: Building a Robust WYSIWYG Editor | JSConf EU 2015 - YouTube_201510](https://www.youtube.com/watch?v=EEF2DlOUkag)
- some new editors like google docs drop contenteditable and create their own selection and caret
  - good xp
- problems: 
  - 1. mobile touch interfaces, native selection is subtle
  - 2. if u maintain your own selection and caret entirely, you get all the complexity of bi-directional text on your plate. you have to implement what the cursor is supposed to be doing if it moves left-to-right/r-to-l.
  - 3. if you are mixing Arabic or Hebrew, you get islands inside of your paragraphs that are running in different directions.
  - 4. for context menu like cut/paste, you have to decide the position/range.
# dev

# more
