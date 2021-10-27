---
title: lib-editor-ckeditor5-dev-log
tags: [ckeditor, dev-log]
created: '2021-10-27T03:20:11.947Z'
modified: '2021-10-27T03:20:45.841Z'
---

# lib-editor-ckeditor5-dev-log

# daily

## 1027

- conversion提供的3种转换方式的时机确认
  - upcast
  - dataDowncast
  - editingDowncast

## 1026

- 创建简单plugin的基本步骤
  - 确定插件功能目标和依赖
  - 继承Plugin class
  - 在init方法中创建ui
  - 在ui组件中注册execute事件处理函数
  - 通过editor.model.insertContent插入内容到目标位置

- 状态放在plugin，还是放在command
  - 放在plugin，可方便获取
  - 放在command，可方便修改 refresh() --> this.value
  - answer
    - 一般放在command，方便从外部触发修改
    - ui相关状态一般用react管理，而不是ckeditor
    - 编辑器内容相关状态，还可以考虑放在attributes

- EmitterMixin、ObservableMixin 的区别
  - 用的很少

- 怎么知道要将view放在plugin的位置
  - editor.model.insertContent的第2个参数指定插入位置

- 如何使用自定义react组件定制ui
  - 参考文档示例，思路实现是ui插件时ui渲染部分使用react组件
