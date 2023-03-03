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

- prezly在最外层`Editable`组件上注册的事件有，onCut，onKeyDown

- 很多编辑器框架都有先从options/plugins中收集依赖，然后再将分类过的props传入Editable组件的逻辑，如atlaskit、taze
# faq

## not-yet

- contenteditable内的元素，mousedown可以触发，keydown不能触发
  - 因为只有能够获取focus的元素才能触发key事件

- 光标在斜体粗体文字边上时，选区对应的具体位置在里面还是外面

- 使用tree存储数据，还是使用map存储数据+关系，如何设计更好

## answers

- 🤔 输入字母时，为什么beforeinput的selection为5，onChange方法里的selection为6，何时更新的
  - 首先确认更新范围，onChange执行后useEffect才执行将 slateSel-TO-domSel，所以更新sel发生在渲染前
  - 排查定位到，执行op `insert_text`时，顺便就把selection更新了
  - 不需要在op-text执行后单独执行op-selection来更新sel
# slate-react
- 监听 beforeinput
  - beforeinput 这个事件会在 `<input>, <select> 或 <textarea> 或者 contenteditable` 的值即将被修改前触发，这样我们可以获取到输入框更新之前的值，实际上对于编辑器内部的一些编辑内容的操作是通过这个劫持这个事件，然后再把用户的一系列操作转化成调用 slate api 去更新编辑器内容。

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
