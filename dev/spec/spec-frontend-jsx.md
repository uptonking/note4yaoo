---
title: spec-frontend-jsx
tags: [format, jsx, spec]
created: 2020-12-16T12:40:54.817Z
modified: 2021-01-14T13:21:33.678Z
---

# spec-frontend-jsx

# guide

- [60行代码实现简单模板语法 - 掘金](https://juejin.cn/post/6844903734095380494)
# [facebook jsx](https://facebook.github.io/jsx/)
- Why not Template Literals
  - ES6 introduces template literals which are intended to be used for embedding DSL in ECMAScript.
  - Template literals work well for long embedded DSLs.
    - Unfortunately the syntax noise is substantial(大量的) when you exit in and out of embedded arbitrary ECMAScript expressions with identifiers in scope.
  - It would be possible to use template literals as a syntactic entry point and change the semantics inside the template literal to allow embedded scripts that can be evaluated in scope
  - However, this would lead to further divergence(分歧；违背). 
    - Tooling that is built around the assumptions imposed by template literals wouldn't work. 
    - It would undermine the meaning of template literals. 
    - It would be necessary to define how JSX behaves within the rest of the ECMAScript grammar within the template literal anyway.
  - Therefore it's better to introduce JSX as an entirely new type of PrimaryExpression
- JXON (lossless JavaScript XML Object Notation) is a generic name by which is defined the representation of JavaScript Objects using XML
  - Unfortunately, balanced braces `{}` do not give great syntactic hints for where an element starts and ends in large trees. 
  - **Balanced named tags** `<Comp>` is a critical syntactic feature of the XML-style notation.
- JSX syntax is similar to the E4X Specification
  - E4X is a deprecated specification with deep reaching semantic meaning. 
  - JSX partially overlaps with a tiny subset of the E4X syntax. 
  - However, JSX has no relation to the E4X specification.
