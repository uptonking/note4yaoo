---
title: lib-editor-slate-codebase
tags: [codebase, slate-editor]
created: 2022-05-15T18:46:02.235Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-codebase

# guide

- dev-to
  - createDraft + applyToDraft + finishDraft
  - toSlateRange, toDOMRange
  - dirtyPath
  - decoarate
  - op move/split/merge
  - 支持tiptap/prosemirror的json

- 若slate-model层采用扁平化Node
  - 如何保持path和key同步，参考 getKeysToPathsTable, getByKey实现上基于getByPath
  - 优化方向可参考tree的crud及协作
  - 协作时还应该考虑 json patch, last-write-win, map, shelf
  - Node定义采用unist
  - lww的字符串改为针对crdt优化的类型如?
  - 分2步，先将数据全部放在内存但virtual-render，再按需请求数据懒加载

- 实现扁平化Node的方式
  - 理想方式是每个op会在apply结束后顺便计算dirtyPath相关的数据变化
  - 临时方案，diff当前op的最高节点作为根节点的树，先flat再diff计算出added/removed

- virtual render在渲染层实现
  - 此时选区和范围如何表示，因为dom可能不存在
  - 复制粘贴的范围
  - 考虑成本和收益
  - 比如浏览器的翻译、朗读、页面内查找、页面内快捷键、锚点跳转功能、广告屏蔽插件
  - 口口声声说为了性能，用户体验都没了

- prezly在最外层`Editable`组件上注册的事件有，onCut，onKeyDown

- 很多编辑器框架都有先从options/plugins中收集依赖，然后再将分类过的props传入Editable组件的逻辑，如atlaskit、taze

- slate-plugin/feature
  - 定义接口
  - 工具方法、queries
    - 可能在插件外部其他逻辑中通过如 YjsEditor.connect(editor) 的方式执行
  - withPlugin(editor)
    - 增强editor对象
# faq

## not-yet

- 使用tree存储数据，还是使用map存储数据+关系，如何设计更好

- remirror的api设计 uncontrolled by default
  - 支持设置state+onChange让ReEditor组件变成controlled

## answers

- 光标在斜体粗体文字边上时，选区对应的具体位置在里面还是外面
  - 粗体、斜体只是文本节点的属性

- contenteditable内的元素，mousedown可以触发，keydown不能触发
  - 因为只有能够获取focus的元素才能触发key事件

- 🤔 输入字母时，为什么beforeinput的selection为5，onChange方法里的selection为6，何时更新的
  - 首先确认更新范围，onChange执行后useEffect才执行将 slateSel-TO-domSel，所以更新sel发生在渲染前
  - 排查定位到，执行op `insert_text`时，顺便就把selection更新了
  - 不需要在op-text执行后单独执行op-selection来更新sel
# undo/history
- 思路是先计算inverseOps，再执行它

```JS
e.history = { undos: [], redos: [] }; // 👈🏻 都是 BaseOperation[][]，可包括选区/文本/节点op

e.undo = () => {
  const { history } = e;
  const { undos } = history;
  const batch = undos[undos.length - 1];
  const inverseOps = batch.map(Operation.inverse).reverse();

  for (const op of inverseOps) {
    e.apply(op);
  }

  history.redos.push(batch);
  history.undos.pop();
}

e.apply = (op: Operation) => {
  undos.push([op]);

  apply(op);
}
```

# slate-yjs
- not-yet
  - undo/redo的按键事件是在哪里处理的

- tips
  - 协作3大要点: 模型数据、光标选区、undo/redo

- 网络通信socket，基于框架隐藏了网络通信的细节
  - 客户端连接使用HocuspocusProvider
  - 服务端使用@hocuspocus/server

- `editor.sharedRoot`共享状态在createEditor时作为插件参数传入
  - sharedRoot直接挂在slate editor对象上，方便存取

- each time slate doc change, update ydoc
  - e.onChange = ()=> YjsEditor.flushLocalChanges(e); 

- each time ydoc change, update slate doc
  - e.connect = ()=> e.sharedRoot.observeDeep(handleYEvents); 

- connect时会初始化editor数据
  - editor.children = convertToSlate(editor.sharedRoot)

- slate的move/split在ytext中是delete+insert
  - 采用了stored positions的设计将pos的relative pos保存在sharedRoot下
  - 一旦执行move/split, binding就会更新sharedRoot下的relative pos

```JS
// yEvent to slateOp
const op = {
  "type": "insert_node",
  "path": [
    4,
    1
  ],
  "node": {
    "text": "e"
  }
};
```

## hocuspocus-provider

- ydoc/awareness的set方法会自动send

## hocuspocus-server

# selection
- slateSel to domSel
  - 场景: 
  - 方向键，在keydown事件中处理
  - click-void，dragStart, drop, 在对应事件中处理

- domSel to slateSel
  - 场景: click事件的domSel在useEffect里面会同步到slateSel
# slate-react
- 监听 beforeinput
  - 这个事件会在 `<input>, <select> 或 <textarea> 或者 contenteditable` 的值即将被修改前触发，这样我们可以获取到输入框更新之前的值，实际上对于编辑器内部的一些编辑内容的操作是通过这个劫持这个事件，然后再把用户的一系列操作转化成调用 slate api 去更新编辑器内容。

- 监听 selectionchange
  - 对于在编辑区域内的一些选区操作，就是通过这个方法去劫持选区的变动，首先获取到原生的 Selection，然后调用 toSlateRange方法将原生的选区转化成 slate 自定义的 Range 格式，然后调用相应方法更新 slate 自己定义的选区。
​
- slate-react 大量 WeakMap 数据结构的使用，如果看过 Vue3.0 源码的 reactivity 的源码，应该对这种数据结构不陌生。
  - 使用 WeakMap 的好处是它的键值对象是一种弱引用，所以它的 key 是不能枚举的，能一定程度上节约内存，防止内存泄漏。
​

## Editable

- 默认是div
- 解构props剩下的参数放在 attributes 中

- 接受的实参中包含事件处理器时，若事件处理器中`return true`，则不会执行slate内置逻辑
  - 受影响的内置事件包括
    - onBeforeInput
    - onBlur
    - onClick
    - onCompositionStart
    - onCompositionEnd
    - onCompositionUpdate
    - onCopy
    - onCut
    - onPaste
    - onDragOver
    - onDragStart
    - onDragEnd
    - onDrop
    - onFocus
    - onKeyDown
  - 始终会执行的内置事件包括
    - onInput

## 中文输入法

- [slate.js源码分析（一） —— slate渲染机制 - 知乎](https://zhuanlan.zhihu.com/p/266438572)
- 在输入法输入的过程中，如果我们去实时修改文档内容，会和输入法产生冲突。
  - 所以在 compositionUpdate 期间，Slate Value不做任何更新，任由 dom 自己改变。
  - 在 compositionEnd 时再去更新 Slate Value。
- 会发生报错的原因则是，在 CompositionStart 时，文档内容被删除。在 CompositionEnd 时，slate 找不到对应的 dom 节点，然后报错
  - 解决也不难，只需要在 CompositionStart 删除文档内容时，更新一下文档 value 更新即可
  - 修复这个问题，我们团队目前的选择是fork改源码。
# slate-src-more
- 其测试的编写是一种数据驱动的思路，通过给每个测试文件定义输入和输出以及要执行的测试逻辑，最后通过统一的 runner 运行，极大提供了编写测试的效率，让人耳目一新。
- Slate测试挺别具一格，反正我第一次看的时候，反应就是原来测试还可以这样写。​
  - 这些文件里没有任何跟测试相关的断言之类的调用。
  - 其实，所有 test 目录下的只是 fixtures 。
  - 那么什么是 fixtures？在测试领域里面，测试fixture的目的是确保有一个众所周知的、固定的环境来运行测试，以便结果是可重复的，也有的人称 fixtures 为测试上下文。
- 以下是 fixtures 的一些例子：
  - 用特定的已知数据集加载数据库；
  - 复制特定已知的一组文件；
  - 编写输入数据和假设或模拟对象的设置/创建。
- Slate这里的场景就属于复制特定已知的一组文件
- 短短五十几行代码就搞定了 slate 这个 package 下的所有测试，我称之为”数据驱动测试“。​
