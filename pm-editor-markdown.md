---
title: pm-editor-markdown
tags: [editor, markdown, pm, pmgr]
created: 2019-08-22T03:45:48.886Z
modified: 2021-05-14T14:33:33.975Z
---

# pm-editor-markdown

# guide

- 与交互相关的操作非常容易与编辑器的功能产生联系
- 可以考虑通过提供某一类的拖拽组件代替一类应用场景的editor/builder

- 注意文档渲染的宽度
  - 若过窄，则空白太多；若过宽，则半屏显示文档时会发生layout trash
  - 可参考dev.to、twitter等网站滚动内容区的宽度

- tips
  - 主流的编辑器采用的是live preview，实时预览

- faq-not-yet
  - 如何指向当前页面的标题

- pros
  - 纯文本易搜索

- cons-painful
  - 对于页面不需要展示，但跳转需要用到的标题id，如何设计和书写
  - 用markdown生成ppt的体验，很难控制空行高度、空白大小、双栏布局；
    - 对可视化要求高时，千万别用markdown或简单文本自动生成
    - 应该使用编辑器，导出markdown
    - 就算使用类似latex纯文本的布局方案，布局代码仍会污染内容文本
# features
- core
  - optional block style editor
  - powerful table editor crafted for markdown
  - configuration/customizable editor with a settings page

- key-problems
  - realtime collaboration
  - sync files(git/onedrive)

- options-syntax
  - render line breaks in .md as line breaks in html

- json editor
  - json <> json5
  - 支持superjson，属性值支持的类型包括Date、RegExp、bigint、Set、Map

- later
  - pdf studio阅读的文字是正常的，但复制文字粘贴下来却很多乱码，，，很安全
  - mobile reponsive editor
  - 代码块支持高亮mdx的内容
  - 支持html，但不支持web components组件的标签
  - lint markdown format
    - 检查重要区块的语法、自定义语法
    - 检查头部元数据格式
  - table-renderer
    - for cli
    - for 鸿蒙OS
  - 协同编辑，更适合用在文档或笔记中
  - turn two-column PDFs into a single column
  - 图文混排，侧重于表格挂件，而不是可视化

- 细节设计
  - 类似github的readme，点击顶部标题，只显示一级目录大纲
  - [Tips and Tricks for using Markdown](https://github.com/MishManners/GitHub-Like-A-Boss/blob/main/markdowntricks.md)
# draft
- links
  - 在即时渲染模式下，弱化链接url样式，突出链接文字

- code highlighting

- 允许半个符号而不抛出异常，如`>, 1)`
  - wolai支持将某些中文符号转换成常用md语法，如 `1。`也能转换成数字列表

- format
  - 格式化时，不应该在用引号包裹的字符串内自动插入空格

- 提示上一个标题h? 的级别，甚至自动补全当前标题的等级，不用到处查找

- list
  - 提供有序列表和无序列表的自动转换功能
  - 复制ol有序列表时，可选择自动复制序号
  - 可自动统计ul无序列表的总数量

- link
  - url包含中文时，复制下来又乱又长，渲染显示时应该在文档中显示中文而不是url编码
# extensions
- 扩展markdown的方法
  - 参考asciidoc, rst
  - 参考mdx

- code block extensions
  - 支持markdown作为内容语法高亮
  - 支持json5
  - 支持切换代码高亮主题，类似[carbon](https://carbon.now.sh/)

## md-table

- 目标
  - 在普通md预览器中显示较友好的表格
  - 参考textbundle格式的csv来与表格交互

- table-features
  - 预置theming切换，同时支持设置表格样式

- `<table src=data.csv></table>`
  - 可以考虑使用mdx中支持的自定义组件的标签
  - 甚至可以直接在markdown中书写web components组件的标签
  - 还计划在markdown中实现类似react-live的编辑效果

## experimental

- better collaborative editor
- better code editor in doc editor
- better math/latex
- canvas renderer for partial/full doc 
- headless component
- 针对常见使用场景进行优化
  - 如代码ide、笔记、markdown、block-editor、分享、streamlit、移动端
- fast long documents with hosted sqlite and http range
# integrations/connections
- github-readme-editor

- mermaid-flow-uml
- excalidraw
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
- https://nhn.github.io/tui.editor/latest/ToastUIEditor
- https://github.com/RIP21/react-simplemde-editor
- https://github.com/sparksuite/simplemde-markdown-editor
- https://github.com/tuture-dev/editure
- https://github.com/andrerpena/react-mde
- https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
