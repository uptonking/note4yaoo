---
title: lib-editor-typewriter-codebase
tags: [codebase, typewriter]
created: 2023-02-09T12:26:00.002Z
modified: 2023-02-09T12:26:14.281Z
---

# lib-editor-typewriter-codebase

# guide

- dev-xp
  - 视图层实现和wangEditor类似，但wangEditor使用了主流vdom工具库snabbdom

- dev-to
  - 支持表格
# not-yet
- 示例文档有100行，每行`\n+字母`的场景
  - doc的length为293？
# codebase
- lines是块级元素
  - 类似quill中的blocks, formats, embeds

- Editor自身是一个经典自定义eventemitter，
  - 注意触发事件基于dom event，类似`this.dispatchEvent(new Event('root'));`，默认不冒泡
  - 在editor的构造函数中，初始化rendering模块时会注册事件， `editor.on('change', renderOnChange);`。
  - editor数据更新时，会手动执行this.update，从而触发view更新 `editor.dispatchEvent(new EditorChangeEvent())`
  - prosemirror的数据变化后，可以手动在dispatchTransaction中view.updateState(newState)

- 触发rerender/update的场景
  - scroll
  - resize

## model/TextDocument/Delta

- typewriter的delta就是一系列op操作集合构成的flat/linear线性结构
  - op的内容非常类似经典OT算法

- 模型中的数据editor.doc并不会包含所有op记录，只包含insert，不包含delete/retain
  - 和quill的parchment结构非常类似，都只包含insert
  - 带格式的富文本会

- delta无法直观的看出一行block的起点在哪里
  - TextDocument将\n作为分隔符，拆分出了一个段落的op作为分隔符

## view/render

- render渲染，基于自定义vdom实现，类似react
  - lines/formats/embeds的render属性定义了渲染细节，`() => h('img', props)`

```typescript
// vnode中不包含真实dom
export interface VNode {
  type: string;
  props: Props;
  children: VChild[];
  key: any;
}
```

- 对于renderSingleLine
  - line.content会作为children渲染，`type.render( line.attributes, renderInline(editor, line.content) )`; 
  - renderInline会遍历operations，分别处理insert text和embeds，返回 VChild[]

- view update
  - 对于renderWhole和renderChanges，都是最小化dom更新操作 patchDom(newDom, oldDom, vdom)

- 视图层在apply op时会设置change的来源 Source
  - user, input, history, paste, api

### virtual-render

- virtualized-render示例要点
  - 仍将所有内容字符串放在内存
  - 但只显示指定区域高度大小的view元素
  - 需要计算每行元素的高度放在内存，这样在滚动被隐藏的区域只需要显示一个空div，高度为隐藏所有行的元素高度和

- dom元素结构，注意滚动位置不同时可视区域上下虚拟区域高度会变化
- div.editor contenteditable
  - div.spacer style="height: 4319px; "
  - p
  - p
  - div.spacer style="height: 319px; "
  - p end, 最后一个dom元素一直存在

- 🤔 虚拟渲染时每行高度如何计算
  - p标签的mt和mb为16px=1rem，但单行高度与语言相关，英文一行height为18px，中文一行height为24px
  - https://codepen.io/uptonking/pen/QWVwNRr
  - 👉🏻 每行的高度依赖滚动时去计算，开始必须是从上向下的滚动，所以会动态渲染并计算每行高度，然后缓存已滚动行的高度
  - 后面未滚动行的行高会使用averageHeight，取的是已滚动行高度的平均值

- 滚动条的长度如何实现
  - 在可见区域上方和下方显示一个height为 已滚动元素和未滚动元素个数*averageHeight 的空白div

- editor会监听第一个可滚动父元素的scroll事件，然后计算当前需要渲染的元素范围

## commands/op/editor-change

- 主要基于 MutationObserver 获取用户输入来更新editor.doc模型
  - 在beforeinput中处理了Gboard输入bugs、historyUndo

## collab

### undo

- 会保存op记录: `{ undo: [], redo: [] }`，都是 `TextChange[]`

```JS
const undoOp = new TextChange(
  null,
  change.delta.invert(oldDoc.toDelta()), // 👈🏻 相反指令
  oldDoc.selection,
);

const redoOp = new TextChange(null, change.delta, change.selection);
```
