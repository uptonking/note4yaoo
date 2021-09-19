---
title: spec-format-json-dev
tags: [format, json]
created: '2021-02-27T15:29:51.481Z'
modified: '2021-02-27T15:31:23.130Z'
---

# spec-format-json-dev

# guide

# discuss
- ## [JSON 可以替代 XML，为什么网页不用 JSON 格式来写呢？](https://www.zhihu.com/question/373946861)
- XML 和 JSON 的复杂度完全不在一个数量级上。JSON 的 ECMA-404 规范，其 PDF 内容部分仅 4 页。而 XML 1.0 规范 则有整整 50 多页。
  - 因此，哪怕是工业级的 JSON Parser，靠递归下降这样基础的算法照标准硬写就足够了。
  - 像 Google 在 V8 引擎里就是这么实现了 JSON.parse 十多年，直到2019年才做了解决递归爆栈风险的重构优化
  - 一个高质量的 XML Parser 则涉及流式处理、多线程、错误容忍等维度，已经相当于 Blink 和 Webkit 等现代浏览器引擎中的一个核心模块，甚至很难从引擎中单独抽出来开源。

- 可行。毕竟两者都是树状结构，建立一个一一映射就行了。
  - 哪些地方不方便呢？
  - 最重要的是文本和标签混排的场景
    - 首先本来是完整的一句话里夹杂着标签，现在变成了非常复杂的嵌套结构，很难连起来看到原文，对齐各层嵌套的括号也很麻烦。
    - 另外，引号实在是太多了。这还没有涉及到转义字符和换行符，像多行、有排版的内容要手写就更难了。
    - 如果要在`<script>`里写javascript，在javascript里再处理dom，然后整个转换成JSON里的字符串，大量引号嵌套引号
  - HTML适合的是大量文本内容配合少量标签的场景，这些情况下JSON并不合适
# parser-ast
- https://github.com/humanwhocodes/momoa
  - A JSON parser, tokenizer, traverser, and printer.
  - A ECMA-404 compliant parser that produces an abstract syntax tree (AST) representing everything inside of a JSON string.
  - A tokenizer that allows you to separate a JSON string into its component parts.
  - A traverser that visits an AST produced by the parser in order.
  - A printer that can convert an AST produced by the parser back into a valid JSON string.

- https://github.com/JohannesOehm/json-parse-ast
  - JSON Tokenizer & AST (Abstract Syntax Tree) parser
  - I wrote my custom parser since monaco's built-in JSON library does not expose any syntax tree

- https://github.com/rse/json-asty
  - Lossless JSON-to-AST Parser and AST-to-JSON Generator
  - The AST is based on ASTy-ASTq
# ref
- [从零开始的JSON库教程](https://zhuanlan.zhihu.com/json-tutorial)
  - https://github.com/miloyip/json-tutorial
