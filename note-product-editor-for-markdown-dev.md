---
title: note-product-editor-for-markdown-dev
tags: [dev, editor, markdown, product]
created: '2020-07-13T13:39:04.621Z'
modified: '2020-07-14T10:21:23.376Z'
---

# note-product-editor-for-markdown-dev

## usage

``` js
<Editor value={value} onChange={() => this.handleChange()} />
```

## api 

- api-props-common
  - value:str, 输入框内容
  - placeholder:str, 占位文本
  - lineNum:bool, 显示行号
  - style:obj, 编辑器样式
  - height:str, 编辑器高度    
  - width:str, 编辑器宽度
  - preview:bool, 显示预览
  - fullScreen:bool, 全屏模式
  - splitView:bool, 分屏双栏
  - syncScrolling:bool, 同步滚动
  - autoFocus:bool, 自动获取焦点    
  - autoSave:bool, 自动保存
  - lang:str, 编辑器语言
  - mdFlavor:gfm
  - readOnly:bool
  - editType: md, wysiwyg
  - previewOptions
    - anchor
  - textareaOptions
  - uploadOptions
- api-props-optional
  - toolbar:obj, 自定义工具栏
  - inlinePreview：只预览部分内联元素，包括标题、粗斜体、中下划线、code
- demo
  - theme
  - indentUnit:num, 4
  - showTrailingSpace：bool, 显示行尾空格
  - TrimEmptyLine:str, 删除md文件最前和最后的空行, both, first, last
  - spellChecker:bool
- api-event
  - onChange:str, 内容改变时回调
  - onSave:str, 保存时回调
  - addImg: File, 添加图片时回调
