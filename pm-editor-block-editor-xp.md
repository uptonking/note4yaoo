---
title: pm-editor-block-editor-xp
tags: [block-editor, pm, xp]
created: '2022-06-08T11:04:31.291Z'
modified: '2022-06-08T11:05:33.767Z'
---

# pm-editor-block-editor-xp

# guide
- block-editor基于多编辑器实例
  - pros
    - 将slate作为主体应用渲染层的一小部分，开发者对数据和定制掌控力更强，方便替换掉slate
  - cons
    - 处理跨block选区需要自己计算选取信息和计算文字偏移量
    - 需要自己实现基础计算：选区、光标、键盘、滚动条

- block-editor基于单编辑器实例
  - pros
    - 更易复用slate的selection、工具方法
  - cons
    - 实现水平分栏可能更复杂
    - 实现鼠标左移右移更简单

- 块编辑器的tradeoff
  - 基于块来复用各种子块、资源
  - 多维表格的特性在于数据展示和分析，而不是local-first
# not-yet
- 普通react table组件和基于slate的table有什么区别？

- 更适合block-editor的数据结构是否是 mongodb ？

- 块编辑器开始支持跨区选择，后面禁用此功能改为只支持单行选择的原因
  - 跨区选择时，会将各子块的contenteditable改为false，此时选中的内容无法响应键盘事件
# block-editor相对于notion的feature

## 文字格式

- 段落左中右对齐的实现方式
  - 通过给p元素添加style对象实现
    - slate-plate
    - ckeditor 
    - TinyMCE
  - 通过给p元素添加className实现
    - atlaskit
    - quill

- 文本中添加前景色背景色的实现方式
  - 通过给span添加style对象实现
    - ckeditor
    - slate-plate
    - atlaskit
      - style添加的是css var颜色定义

- 文本内链接设计
  - 区分产品内链接和外部链接
  - 标识图片链接
# inline-toolbar
- 选中区域文本格式在工具条的高亮色判断
  - 全部加粗才高亮
    - notion
  - 部分加粗也高亮
    - 飞书
