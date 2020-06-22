---
tags: [components, prototype, web]
title: note-dev-product-editor
created: '2019-08-22T03:45:48.886Z'
modified: '2020-06-22T09:10:43.309Z'
---

# note-dev-product-editor

## tips
- 与交互相关的操作非常容易与编辑器的功能产生联系
- 可以考虑通过提供丰富的拖拽组件代替editor

## solutions
- react-page
  - renderer package基于slate实现

## markdown-editor-as-component
- demo
```
<Editor value={value} onChange={() => this.handleChange()} />
```
- api-prop-common
  - value:str, 输入框内容
  - placeholder:str,占位文本
  - lineNum:bool,显示行号
  - style:obj,编辑器样式
  - height:str,编辑器高度    
  - width:str,编辑器宽度
  - preview:bool,显示预览
  - fullScreen:bool,全屏模式
  - splitView:bool,分屏双栏
  - syncScrolling:bool,同步滚动
  - autoFocus:bool,自动获取焦点    
  - autoSave:bool,自动保存
  - lang:str,编辑器语言
  - mdFlavor:gfm
  - readOnly:bool
  - editType: md, wysiwyg
  - previewOptions
      - anchor
  - textareaOptions
  - uploadOptions
- api-prop-optional
  - toolbar:obj,自定义工具栏
  - inlinePreview：只预览部分内联元素，包括标题、粗斜体、中下划线、code
  - theme
  - indentUnit:num,4
  - showTrailingSpace：bool,显示行尾空格
  - TrimEmptyLine:str,删除md文件最前和最后的空行,both,first,last
  - spellChecker:bool
- api-event
  - onChange:str,内容改变时回调
  - onSave:str,保存时回调
  - addImg:File,添加图片时回调
- editor-plugin
  - keyboard-shortcuts:preview,bold,checkbox,newLine
  - list-editing-sugar:enter,tab,delete
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
- ref
  - https://github.com/kkfor/for-editor
  - https://github.com/uiwjs/react-md-editor
  - https://nhn.github.io/tui.editor/latest/ToastUIEditor
  - https://github.com/RIP21/react-simplemde-editor
  - https://github.com/sparksuite/simplemde-markdown-editor
  - https://github.com/pandao/editor.md
  - https://github.com/tuture-dev/editure
  - https://github.com/andrerpena/react-mde
  - https://github.com/HarryChen0506/react-markdown-editor-lite
  - https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one


## 编辑器开发体验
- 编辑器大致分为两种:源代码编辑器和富文本编辑器，可以基于富文本实现源代码编辑器
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
- 参考
  - https://zhuanlan.zhihu.com/p/37051858
  - https://www.zhihu.com/question/24328297
  - https://www.oschina.net/translate/why-contenteditable-is-terrible
