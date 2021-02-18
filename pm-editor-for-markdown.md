---
title: pm-editor-for-markdown
tags: [editor, markdown, pm, product]
created: '2019-08-22T03:45:48.886Z'
modified: '2020-10-22T13:33:45.146Z'
---

# pm-editor-for-markdown

# guide

- 与交互相关的操作非常容易与编辑器的功能产生联系
- 可以考虑通过提供某一类的拖拽组件代替一类应用场景的editor/builder

- 注意文档渲染的宽度
  - 若过窄，则空白太多；若过宽，则半屏显示文档时会发生layout trash
  - 可参考dev.to、twitter等网站滚动内容区的宽度

- tips
  - 主流的编辑器采用的是live preview，实时预览

# features

- table editor for markdown

- json editor
  - json <> json5

- later
  - pdf studio阅读的文字是正常的，但复制文字粘贴下来却很多乱码，，，很安全
  - mobile reponsive editor
  - 代码块支持高亮mdx的内容
  - 支持html，但不支持web components组件的标签
  - lint markdown format
    - 检查重要区块的语法、自定义语法
    - 检查头部元数据格式

- 细节设计

# md-extensions

- 扩展markdown的方法
  - 参考asciidoc, rst
  - 参考mdx

- code block extensions
  - 支持markdown作为内容语法高亮
  - 支持json5
  - 支持切换代码高亮主题，类似[carbon](https://carbon.now.sh/)

## 表格扩展相关

- 目标
  - 在普通md预览器中显示较友好的表格

- table-features
  - 预置theming切换，同时支持设置表格样式

- `<table src=data.csv></table>`
  - 可以考虑使用mdx中支持的自定义组件的标签
  - 甚至可以直接在markdown中书写web components组件的标签
  - 还计划在markdown中实现类似react-live的编辑效果

# md-editor-as-component

- editor-plugins
  - keyboard-shortcuts:preview, bold, checkbox, newLine
  - list-editing-sugar:enter, tab, delete
  - export & print    
  - import
  - auto-completion
    - math
    - link
    - @username
    - predefined-text-suggestion
  - toolbar
  - img-upload
  - word-counter
  - collapsible

- md-extension
  - gfm
      - checkbox-task-list
      - automatic-linking
      - strikethrough
      - table
      - emoji
      - syntax-highlight
      - github-only
          - issue-reference
          - username-mention
  - toc
  - footnote
  - mathTeX: formula
  - flowChart

# solution-catalog-editor-for-markdown

- https://github.com/kkfor/for-editor
- https://github.com/uiwjs/react-md-editor
- https://nhn.github.io/tui.editor/latest/ToastUIEditor
- https://github.com/RIP21/react-simplemde-editor
- https://github.com/sparksuite/simplemde-markdown-editor
- https://github.com/tuture-dev/editure
- https://github.com/andrerpena/react-mde
- https://github.com/HarryChen0506/react-markdown-editor-lite
- https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
