---
title: tech-cs-compiler
tags: [antlr, compiler, cs]
created: 2019-10-29T09:57:32.290Z
modified: 2020-10-22T14:01:20.636Z
---

# tech-cs-compiler

# summary

- topics
  - 编译器结构
  - 词法分析
  - 语法分析
  - 中间代码生成
# 编译器
- 编译器工作流

```

       前端              |         中端（优化）       |          后端
词法分析 -> 语法X -> 语义X | 平台无关优化 -> 平台相关优化 | 寄存器分配 -> 代码生成
```

# antlr
- ANTLR自身覆盖词法分析与语法分析部分，可以生成词法分析器、语法分析器和parse tree
- 应用案例
  - Hive SQL，Hibernate SQL等都是使用antlr来进行分析的，查询引擎的DSL部分
  - 查询引擎presto就是用的antlr做底层sql语法解析
- sql语法分析器
  - 可以使用第三方Parser生成工具（对于Java是ANTLR，对于C语言是lex/yacc之类），也可以使用统一实现的Parser/Grammar（比较纯粹的是Apache Calcite，当然所有open source的SQL实现理论上都可以剥离出来一个Parser/Grammar）
  - 要注意SQL语法其实在不同实现之间的分歧是很大的，事实上没有一款统一实现的Parser/Grammar可以解析某种特定的语法，例如Oracle的语法
  - Druid的SQL Parser是手工编写，性能非常好，目标就是在生产环境运行时使用的SQL Parser，性能比antlr、javacc之类工具生成的Parser快10倍甚至100倍以上
  - https://github.com/alibaba/druid/wiki/SQL-Parser
# discuss
- ## 

- ## 

- ## 

- ## Ironically, the "parse, don't validate" mantra doesn't apply to compilers as much.
- https://x.com/effectfully/status/1954202257211249050
  - An AST parser should be a function that handles all kinds of invalid syntax, so that you can report multiple compilation errors gracefully and encourage generalization of syntax.
  - You'll probably end up parsing (in the mantra sense) the parsed AST into a more refined representation just to get some correct-by-construction representation, but even then it's best to keep it light.

- Real mean have two ASTs in their compiler frontend before typechecking. Source AST and then Canonicalization.
  - Yes. But it's still fine for Canonicalization to have some unenforced invariants, even if it's possible to enforce them.

- That's an interesting point. I thought at least for parsers, you should maintain invalid representations of the tree as a part of the parsing workflows, doing a best-effort to get as much as the tree representable. Not for the compilers themselves but for tooling like LSPs.
