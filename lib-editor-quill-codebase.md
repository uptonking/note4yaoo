---
title: lib-editor-quill-codebase
tags: [codebase, quill]
created: 2023-02-09T18:24:22.295Z
modified: 2023-02-09T18:24:31.494Z
---

# lib-editor-quill-codebase

# guide
- delta
  - 内容元素: block, inline-text, inline-non-text
  - 更新操作: insert, delete, retain, format
# not-yet
- why eventemitter3?

- 
- 
- 

# codebase
- 整体class风格

- 通过全局instances支持多实例 `WeakMap<HTMLElement, Quill>`

- quill/core只注册了核心模块
  - blots: block, inline, embed, text, container, break, cursor, scroll
  - modules: uiNode, input, keyboard, history, clipboard, uploader 
- quill完整版注册了很多模块
  - attributors: align, color, font
  - formats: align, color, font, size, blockquote, code, list, link, formula, image, video
  - modules: table, toolbar
  - themes
  - ui: icons, picker, tooltip

- 语法高亮使用 highlight.js

- `Quill.import()` doesn't load scripts over the network, it just returns the corresponding module from the Quill library without causing any side-effects.

- 
- 
- 

# 🏘️ architecture
- 用户输入时如何更新dom
  - 通过mutationObserver获取变更，然后更新model-delta

- 外部工具条按钮的逻辑
  - 先计算op，再更新model和view

## init-dataflow

- instances.set(this.container, this); 
- `this.scroll = new ScrollBlot` // 创建的是quill包的ScrollBlot子类对象，方法都被封装过
  - this.build() // 遍历domNode下的元素，创建为bolt，成为链表
  - this.observer = new MutationObserver
  - 🧐 this.observer.observe(this.domNode, OBSERVER_CONFIG); 
  - 每次检测到dom变化，会遍历变化，找到对应bolt并执行blot.update
  - bolt.update的末尾，会触发`SCROLL_UPDATE`事件，来更新model/delta
- this.editor = new Editor(this.scroll)
- this.selection = new Selection(this.scroll, this.emitter); 
- addModule input/uiNode/keyboard/clipboard/history/uploader
- this.theme.init(); 
  - 初始化内置或自定义的module: `new ModuleClass()`.
- this.emitter.on `EDITOR_CHANGE/SCROLL_UPDATE` 注册事件
  - 注册事件监听器，当注册的事件触发时，仅触发model更新
# model-delta

## update

- quill.setContents(delta) 未使用emitter，直接先更新dom，再更新delta
  - this.editor.deleteText // set empty editor to \n
  - this.editor.insertContents(0, delta); 
  - this.scroll.insertContents(index, normalizedDelta); // 更新bolt
    - const renderBlocks = deltaToRenderBlocks()
    - renderBlocks.forEach > insertInlineContents
  - this.update(change); // 更新model，this.delta
  - modify() // Handle selection preservation and TEXT_CHANGE emission

- Input module会在rootElem上注册`beforeinput`，这里会处理中文输入法相关的isComposing
  - 还会处理android输入法相关事件

- Quill 只用 mutation observer 监听文本改动。其他的 enter delete 等，都还是劫持 keydown，修改 model
# view

# command
- 没有单独的command设计，insertText/formatText直接定义在quill编辑器实例上
# collab

## undo

- history对象保存 `stack = { undo: [], redo: [] }`

- quill.on `EDITOR_CHANGE` 事件
  - this.record(value, oldValue); 
  - undoDelta = changeDelta.invert(oldDelta); 
  - this.stack.undo.push({ delta: undoDelta, range: undoRange }); 

- this.undo

```JS
const inverseDelta = item.delta.invert(base);
this.stack[dest].push({
  delta: inverseDelta,
  range: transformRange(item.range, inverseDelta),
});
this.quill.updateContents(item.delta, Quill.sources.USER);
```

# modules
- toolbar
  - 用户定义的工具条配置会保存到`container`属性名
# keywords

# more
- https://github.com/xiaochengzi6/quill-scource-code /202303/js
  - 仅此用于学习 & 记录 quill 源码，目前基于 quill v1.3.4 版本
  - 左移运算符 << 实现 x2
