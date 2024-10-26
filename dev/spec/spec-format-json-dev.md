---
title: spec-format-json-dev
tags: [format, json]
created: 2021-02-27T15:29:51.481Z
modified: 2021-02-27T15:31:23.130Z
---

# spec-format-json-dev

# guide

# json-parser/generator
- https://github.com/Tencent/rapidjson
  - JSON parser/generator for C++ with both SAX/DOM style API
 - https://github.com/miloyip/json-tutorial
    - 从零开始的JSON库教程，教程对象适合学习过基本 C/C++

- [基于状态机的JSON解析](https://juejin.cn/post/7032491400516075557)
# faq

## [Can an array be top-level JSON-text?](https://stackoverflow.com/questions/3833299/can-an-array-be-top-level-json-text)

- yes, valid `["apple","pear","banana"]`

- Yes, an array is legal as top-level JSON-text.
- There are four standard documents defining JSON: RFC 4627, RFC 7159 (which obsoletes RFC 4627), ECMA-404, and RFC 8259 (which obsoletes RFC 7159, and calls ECMA-404 normative). 
  - They differ in which top-level elements they allow, but all allow an object or an array as the top-level element.

- Yes, but you should consider making the root an object instead in some scenarios, due to JSON hijacking.
  - but JSON hijacking is not an issue for modern browsers

- [Can JSON start with "["? - Stack Overflow](https://stackoverflow.com/questions/5034444/can-json-start-with)

- Short answer is YES
  - In a .json file you can put Numbers (even just 10), Strings (even just "hello"), Booleans (true, false), Null (even just null), arrays and objects. https://www.json.org/json-en.html

- JSON is built on two structures:
  - A collection of name/value pairs. In various languages, this is realized as an object, record, struct, dictionary, hash table, keyed list, or associative array.
  - An ordered list of values. In most languages, this is realized as an array, vector, list, or sequence.

- Apparently it's safer to have it start with { and not [ so that it isn't a valid Javascript array, and can't be used for CSRF attacks.
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
# discuss-parser/generator
- ## 

- ## 

- ## 

- ## One coding project that I recommend every engineer to build at least once is to write your own JSON parser that converts the given string into a language-native object like a dictionary.
- https://x.com/arpit_bhayani/status/1848931553281450419
- Building a JSON-parser really taught me a lot

# discuss
- ## 

- ## 

- ## On-demand JSON: A better way to parse documents?
- https://twitter.com/lemire/status/1787494558122574019
  - JSON is a popular standard for data interchange on the Internet. 
  - Ingesting JSON documents can be a performance bottleneck. 
  - A popular parsing strategy consists in converting the input text into a tree-based data structure—sometimes called a Document Object Model or DOM. 
  - We designed and implemented a novel JSON parsing interface—called On-Demand—that appears to the programmer like a conventional DOM-based approach. 
  - However, the underlying implementation is a pointer iterating through the content, only materializing the results (objects, arrays, strings, numbers) lazily. 
  - On recent commodity processors, an implementation of our approach provides superior performance in multiple benchmarks. 
  - To ensure reproducibility, our work is freely available as open source software. 
  - Several systems use On Demand: for example, Apache Doris, the Node.js JavaScript runtime, Milvus, and Velox.
- StAX for JSON ?
  -  No. That's not what this is. I invite you to check the paper out 

- This sounds like it is sacrificing latency for throughput. What is the latency on this approach for any individual piece of data?
  - It is not sacrificing latency.
- “Only materializing the results lazily” sounds like sacrificing latency to me.
  - Only doing the work that needs doing does not sacrifice latency, it improves latency. The benchmarks report the total time spent…
- It improves initialization latency, but sacrifices fields access latency as you need to parse and create objects JIT instead of pre-parsing everything AOT and serving pre-built objects.

- The fundamental question is why is JSON so popular when proto/flat buffers exist.
  - Why is node popular on the backend when languages that isn't JS exist?

- How about using binary format instead of JSON?
  - It seems like a popular binary format protobuf may be slower to parse than json for comparable documents.
- Better to use binary serialization without copying data.

- There was a proposal by Joe Armstrong of Erlang fame to make a universal binary format which can be converted to text, somehow like how #UnrealEngine shows its UObjects as text when you diff them. Unfortunately he gave a talk in a conference about it and it never took off

- ## 💡 Did you know that in #javascript `JSON.stringify()` removes `undefined` properties from objects? 
- https://twitter.com/SergiiShymko/status/1768671330734407684
  - There’s no concept of `undefined` in JSON format, only `null` .
- maybe that's because undefined means absence of value and is not a value by itself.

- ## whats the best way to diff two big json files?
- https://twitter.com/jarredsumner/status/1673782475573850113
- difftastic seems best
- ave enjoyed using jsondiffpatch

- I always use a good old fashioned printer. Then using a ruler go line by line. Never failed me.

- ## The advantage of JSON Schema is that it's JSON. I can use the same schema in the frontend or backend, across languages, etc. I can generate a form from it.
- https://twitter.com/DavidKPiano/status/1621243040034611204
  - Zod is JS/TS-only (but can be converted to JSON Schema, like you said)

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
# ref
- [从零开始的JSON库教程](https://zhuanlan.zhihu.com/json-tutorial)
  - https://github.com/miloyip/json-tutorial
