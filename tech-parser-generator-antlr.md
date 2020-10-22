---
title: tech-parser-generator-antlr
tags: [antlr, format]
created: '2020-07-03T10:35:24.549Z'
modified: '2020-10-22T14:02:01.119Z'
---

# tech-parser-generator-antlr

## guide

- ref
  - https://www.antlr.org/
  - [JavaScript runtime for antlr](https://github.com/antlr/antlr4/blob/master/doc/javascript-target.md)
  - [Why Use ANTLR](http://bearcave.com/software/antlr/antlr_expr.html)
  - [Explain ANTLR like I'm five](https://dev.to/vesusaso/explain-antlr-like-im-five-4a9l)
  - [ANTLR：在浏览器中玩语法解析](https://juejin.im/post/5a3caaf0f265da4310489081)
  - [从antlr扯淡到一点点编译原理](https://awhisper.github.io/2016/11/18/%E4%BB%8Eantlr%E5%88%B0%E8%AF%AD%E6%B3%95%E8%A7%A3%E6%9E%90/)

## tips

- 可以脱离DOM，基于一个虚拟的数据结构来完成高亮和各种进一步的计算
- antlr是一个通用的语法解析工具，用它来做js的dsl解析缺点有
  - antlr的本体和语法定义过于庞大，在体积上很难控制。
  - 其JavaScript运行时的实现并非稳定可靠，在Java运行时正常运行的代码，转到JavaScript中就会出现错误。
  - 某些语言（如C++）的解析会丢到空格、换行之类的元素，虽然可以通过源代码字符串和AST中每个元素的位置重新再补回去，但实现之复杂让人觉得毫无意义。

## antlr docs

- ANTLR(ANother Tool for Language Recognition) is a powerful parser generator that you can use to read, process, execute, or translate structured text or binary files.
- From a formal language description called a grammar, ANTLR generates a parser for that language that can automatically build parse trees, which are data structures representing how a grammar matches the input.
- ANTLR also automatically generates tree walkers that you can use to visit the nodes of those trees to execute application-specific code.
- It’s widely used in academia and industry to build all sorts of languages, tools, and frameworks.
  - The languages for Hive and Pig, the data warehouse and analysis systems for Hadoop, both use ANTLR. 
  - NetBeans IDE parses C++ with ANTLR. 
  - The HQL language in the Hibernate object-relational mapping framework is built with ANTLR.
  - Twitter search uses ANTLR for query parsing, with over 2 billion queries a day. 
  - Lex Machina uses ANTLR for information extraction from legal texts. 
  - Oracle uses ANTLR within SQL Developer IDE and their migration tools. 
- Aside from these big-name, high-profile projects, you can build all sorts of useful tools like configuration file readers, legacy code converters, wiki markup renderers, and JSON parsers. 
  - I’ve built little tools for object-relational database mappings, describing 3D visualizations, injecting profiling code into Java source code, and have even done a simple DNA pattern matching example for a lecture.
