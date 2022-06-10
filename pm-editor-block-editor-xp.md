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

- 普通react table组件和基于slate的table有什么区别？
# block-editor相对于notion的feature

## 文字格式

- 文本内链接设计
  - 区分产品内链接和外部链接
  - 标识图片链接
# inline-toolbar
- 选中区域文本格式在工具条的高亮色判断
  - 全部加粗才高亮
    - notion
  - 部分加粗也高亮
    - 飞书
