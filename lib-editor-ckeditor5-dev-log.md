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

- 创建block widget的基本流程
  - 设计插件和widget的层次结构：entry、editing、ui、cmd
  - 在editing中定义schema
  - 在editing中定义converter
  - 将converter细粒度定义，editingDowncast的view方法的返回值使用toWidget/toWidgetEditable
  - 继承Command，实现execute/refresh
  - 在editing中注册commands
  - 在ui中创建图标，并添加到toolbar

- 创建inline widget的基本流程
  - 设计插件和widget的层次结构
  - _defineSchema
  - _defineConverters
  - 继承Command，实现execute/refresh
  - 在editing中注册commands
  - fix position mapping 解决点击inline文字中间会抛出异常的问题
  - 创建dropdown ui，并添加到toolbar
  - 将placeholder的预定义类型在editing中定义，而不是硬编码

## 1026

- 创建简单plugin的基本流程
  - 确定插件功能目标、依赖关系、数据流或架构
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
