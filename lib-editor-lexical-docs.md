---
title: lib-editor-lexical-docs
tags: [docs, lexical-editor, lib, text-editor]
created: 2022-05-15T18:36:02.090Z
modified: 2022-05-15T18:36:36.524Z
---

# lib-editor-lexical-docs

# guide

# blogs

## [Meta出的富文本编辑器Lexical_202205](https://marvinsblog.net/post/2022-05-17-lexical-rich-text-editor/)

- Lexical与ProseMirror的差异
  - 没有ProseMirror中的Mark的概念
  - Editor State即反映文档结构，又反映虚拟DOM
  - 使用DOM reconciler
  - 文本（text）有不同的属性
  - 可以分段以及分号牌，用于提升可访问性，在编辑自定义emojis、hashtag、mentions的时候不用将contenteditable设置为false，因为会导致NVDA、Jaws、VoiceOver这些访问性工具将其跳过

- Lexical的特点
  - 核心比ProseMiirror小
  - 协作功能依赖于yjs
  - 文档没有schema，但是可以通过扩展ElementNode类型来达成
  - Flow/TypeScript是必须的
  - 已用于FB的众多产品
  - 有开发平台原生的打算
  - 不支持IE或老的Edge，与Mozilla和Google一起改进浏览器（使用了很多beforeinput）
  - 强调一流的可访问性，所以PM的横板光标不受支持，因为不符合WCAG准则
# docs
