---
title: lib-office-markdown-dev
tags: [markdown, markdown-extension, proposal]
created: 2021-06-02T15:23:28.922Z
modified: 2025-09-21T18:39:13.776Z
---

# lib-office-markdown-dev

# guide
- markdown-pros

- markdown-cons
  - 需要多个空格才会渲染line-break

- markdown-filename-suffix
  - ["md", "markdown", "mdown", "mkdn", "mkd", "mdwn", "mkdown", "ron", "rmd"]

- hashtag🤔
  - 有助于提取结构化内容

- markdown-table
  - csv常作为基于文本的表格的一种形式, 可参考现有的基于csv的扩展
  - 另一种方案是参考obsidian-bases, 用yaml来输入table

- markdown-layout
  - pdf2markdown后支持渲染为分栏布局, 自定义语法? 可参考 gitbook/YAMLResume?

- markdown-ai
  - 文生图包含元数据，方便复现
  - ai-friendly format: 图片/图形中带有元数据

- markdown-flowchart
  - Mermaid

- markdown-chart-viz
  - ?

- markdown-extensions
  - mdx
  - [R Markdown](https://rmarkdown.rstudio.com/)
  - [MyST(Markedly Structured Text)](https://github.com/executablebooks/markdown-it-myst)
    - [MyST Overview](https://myst-parser.readthedocs.io/en/latest/index.html)
    - who is using #MyST
      - curvenote
    - MyST is a rich and extensible flavor of Markdown.
    - MyST is inspired by Sphinx, and comes with its own Sphinx parser.
    - MyST markdown provides a markdown equivalent of the reStructuredText syntax
  - [kramdown](https://github.com/gettalong/kramdown)
    - kramdown is a fast, pure Ruby Markdown superset converter
    - input formats: kramdown (a Markdown superset), Markdown, GFM, HTML
    - output formats: HTML, kramdown, LaTeX (and therefore PDF), PDF via Prawn
    - https://github.com/asciidoctor/kramdown-asciidoc
      - a kramdown extension for converting Markdown documents to AsciiDoc. 
  - [readmeio-markdown](https://github.com/readmeio/markdown)
  - [jsxtreme-markdown](https://github.com/mapbox/jsxtreme-markdown)
  - [vfm(Vivliostyle Flavored Markdown (VFM))](https://github.com/vivliostyle/vfm)
    - a Markdown syntax optimized for book authoring. 
    - It is standardized and published for Vivliostyle and its sibling projects.
  - [Idyll markup](https://idyll-lang.org/docs/syntax)
    - The main extensions are reactive variables, and components. 
    - Together these two elements can be used to create dynamic, interactive articles.
- more-format-references
  - [Org mode for Emacs](https://orgmode.org/)

- rmarkdown
  - [cheatsheet: dynamic, reproducible, citations](https://blog.rstudio.com/2021/08/23/cheat-sheet-updates/)

- ref
  - commonmark rfcs
# table-md
- 参考textbundle格式的csv来与表格交互

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
