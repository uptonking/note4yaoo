---
title: lib-editor-ckeditor5-blog
tags: [blog, ckeditor]
created: 2021-10-31T15:56:15.028Z
modified: 2021-10-31T15:56:24.071Z
---

# lib-editor-ckeditor5-blog

# 2022

# guide

# ckeditor-faq-repeat
- ckeditor通知更新react组件
  - react组件将自身setState方法注册到eventEmitter，在editingDowncast中更新view时触发执行更新react组件的方法，并传入最新编辑器状态作为参数

- react组件通知更新ckeditor状态
  - 自定义command
# 富文本编辑器ckeditor5源码分析
- ckeditor5/engine封装了model tree的几个概念。
- 主要数据类型，其中Node、NodeList、Element、RootElement、Text、TextProxy和DocumentFragment具有类似的结构

- ckeditor5定义了8个主要的操作（operation）
  - insert, move, rename, attribute, split, merge, no, marker
- 通过model.applyOperation(opt)的方式应用operation，在model和model.documention中通过observablemixin和emittermixin使得其可以将applyOperation转换成事件名，当model调用applyOperation方法时，触发applyOperation事件的回调

- CommandCollection用于管理command，包括新增、查找、迭代（iterator）、执行和销毁。

- 绑定到可观察对象的模板使得用户界面具有动态和交互式特质。一些基本类如Editor、Command可也是可观察对象。
- 如何设置类为observable
- set
- delegate
- bind
  - editor.commands.isEnabled必须使用set方法定义，才能保证bind方法的有效性
- decorate
  - 通过decorate方法，可以将object methods转换为事件驱动性质的方法。
  - 当某个方法被decorate后，那么当方法被执行时，一个同名的事件将会被创建和触发

- EmitterMixin 主要负责事件绑定、触发和代理用。
  - 主要方法有listenTo/stopListening、fire和delegate/stopDelegating。

- extend( ObservableMixin, EmitterMixin )
  - extend的作用就是将EmitterMixin关于事件触发、监听和代理等方法引入有到ObservableMixin中

- ckeditor5的locale方案会往全局变量`window. CKEDITOR_TRANSLATIONS`上挂载映射用的字典信息
# blogging

## [CKEditor 5: New approach to rich text editing on the web_201710](https://news.ycombinator.com/item?id=15497972)

- That's always the way I thought it should be done, with a separation of display and structure.

- Former member of the CKE team here. Three words: it was hell.
  - The CKE people are some of the most hard working devs I've ever encountered in my life. I still find it funny how making little details like backspace/delete key behavior work is such a gargantuan task. And almost nobody gets it right.

## [CKEditor 5: The Future of Rich Text Editing_201510](https://medium.com/content-uneditable/ckeditor-5-the-future-of-rich-text-editing-2b9300f9df2c)

- Why CKEditor 5?
  - (tl; dr) To keep leading on innovation everything is to be re-thought.
