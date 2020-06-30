---
tags: [cs]
title: topic-cs-compiler
created: '2019-10-29T09:57:32.290Z'
modified: '2020-06-30T13:04:13.849Z'
---

# topic-cs-compiler

## summary

- topics
  - 编译器结构
  - 词法分析
  - 语法分析
  - 中间代码生成

## 编译器

- 编译器工作流

``` 
       前端              |         中端（优化）       |          后端
词法分析 -> 语法X -> 语义X | 平台无关优化 -> 平台相关优化 | 寄存器分配 -> 代码生成
```

## antlr

- ANTLR自身覆盖词法分析与语法分析部分，可以生成词法分析器、语法分析器和parse tree
- 应用案例
  - Hive SQL，Hibernate SQL等都是使用antlr来进行分析的，查询引擎的DSL部分
  - 查询引擎presto就是用的antlr做底层sql语法解析
- sql语法分析器
  - 可以使用第三方Parser生成工具（对于Java是ANTLR，对于C语言是lex/yacc之类），也可以使用统一实现的Parser/Grammar（比较纯粹的是Apache Calcite，当然所有open source的SQL实现理论上都可以剥离出来一个Parser/Grammar）
  - 要注意SQL语法其实在不同实现之间的分歧是很大的，事实上没有一款统一实现的Parser/Grammar可以解析某种特定的语法，例如Oracle的语法
  - Druid的SQL Parser是手工编写，性能非常好，目标就是在生产环境运行时使用的SQL Parser，性能比antlr、javacc之类工具生成的Parser快10倍甚至100倍以上
  - https://github.com/alibaba/druid/wiki/SQL-Parser
