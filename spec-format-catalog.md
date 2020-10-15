---
title: spec-format-catalog
tags: [catalog, format, spec]
created: '2019-12-02T10:25:27.789Z'
modified: '2020-10-15T13:42:23.746Z'
---

# spec-format-catalog

- specifications about file format  

## popular-file-formats

- csf (Component Story Format)
  - title, component, parameters, decrators
- mdx
  - 优点
    - 支持markdown+jsx
    - 支持直接引入a.mdx作为一个组件
    - 支持定义和导出variable
  - 问题
    - code block的语法高亮不可更改样式
    - 不支持live editor
- jsx
  - https://facebook.github.io/jsx/
  - Why not Template Literals
    - Template literals work well for long embedded DSLs.
    - Unfortunately the syntax noise is substantial when you exit in and out of embedded arbitrary ECMAScript expressions with identifiers in scope.
    - It would be possible to use template literals as a syntactic entry point and change the semantics inside the template literal to allow embedded scripts that can be evaluated in scope
    - However, this would lead to further divergence. Tooling that is built around the assumptions imposed by template literals wouldn't work. It would undermine the meaning of template literals. It would be necessary to define how JSX behaves within the rest of the ECMAScript grammar within the template literal anyway.
    - Therefore it's better to introduce JSX as an entirely new type of PrimaryExpression
  - JXON (lossless JavaScript XML Object Notation) is a generic name by which is defined the representation of JavaScript Objects using XML
    - Unfortunately, balanced braces `{}` do not give great syntactic hints for where an element starts and ends in large trees. 
    - **Balanced named tags** `<Comp>` is a critical syntactic feature of the XML-style notation.
  - JSX syntax is similar to the E4X Specification
    - E4X is a deprecated specification with deep reaching semantic meaning. JSX partially overlaps with a tiny subset of the E4X syntax. However, JSX has no relation to the E4X specification.
