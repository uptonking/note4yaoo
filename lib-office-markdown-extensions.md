---
title: lib-office-markdown-extensions
tags: [markdown, proposal]
created: '2021-06-02T15:23:28.922Z'
modified: '2021-06-02T15:26:19.890Z'
---

# lib-office-markdown-extensions

# guide
- markdown-pros

- markdown-cons
  - 需要多个空格才会渲染line-break

- markdown-extensions

- mdx-extensions
  - readmeio-markdown
  - jsxtreme-markdown

- markdown-files-suffix
  - ["md", "markdown", "mdown", "mkdn", "mkd", "mdwn", "mkdown", "ron"]

- ref
  - commonmark rfcs
# popular

## [Tables in pure Markdown](https://talk.commonmark.org/t/tables-in-pure-markdown/81)

# draft

## [Support for image dimensions](https://talk.commonmark.org/t/support-for-image-dimensions/148)

## [Anchors in markdown](https://talk.commonmark.org/t/anchors-in-markdown/247)

## [Letter-ordered lists](https://talk.commonmark.org/t/letter-ordered-lists/173)

## Generic directives/plugins syntax

- There are three different kinds of directives:
  - Inline, start with one colon 
    - (analogous to spans)
  - Leaf block, start with two colons 
    - (analogous to empty divs)
  - Container block, start with at least three colons 
    - (analogous to divs containing further blocks)

- callout组件
  - 用来显示提示信息或警告信息
  - 样式与已有的blockquote很像，所以扩展时应该基于blockquote `>` ，可以加上特殊字符组合
  - 也要考虑流行项目的选择，如docusaurus选择::

- ref
  - https://talk.commonmark.org/t/generic-directives-plugins-syntax/444
# more
- https://github.com/mamamia5x/markdownpedia
  - https://markdownpedia.tk/
  - A site similar to Wikipedia written in Markdown.
  - 依赖express、fs-extra、readdirp、showdown

- https://github.com/mity/md4c
  - C Markdown parser. Fast. SAX-like interface. 
  - Compliant to CommonMark specification.
