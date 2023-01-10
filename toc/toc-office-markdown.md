---
title: toc-office-markdown
tags: [doc, markdown, toc]
created: 2020-10-05T09:49:50.474Z
modified: 2021-01-04T17:26:25.032Z
---

# toc-office-markdown

# guide

# md-examples
- https://github.com/Harry-Hopkinson/markdown-editor
  - A markdown editor written in Typescript.
  - Vite+Electron

- https://github.com/ahmedsaheed/Leaflet
  - A minimal distractionless markdown editor designed to quickly navigate between multiple `.md` files in a directory and its sub directories.
  - It features a clean mathematical typesetting, chemical equation rendering, code blocks highlighting and writing statistics 
  - 依赖codemirror6、@uiw/react-codemirror、electron

- https://github.com/foambubble/foam
  - /7.3kStar/MIT/202010/ts
  - Foam is a personal knowledge management and sharing system built on VSCode and GitHub.
- https://github.com/atom-community/markdown-preview-plus
  - a fork of Markdown Preview that provides a real-time preview of markdown documents.

- markdoc /5.8kStar/MIT/202211/ts/inactive
  - https://github.com/markdoc/markdoc
  - https://markdoc.dev/
  - Markdoc is a Markdown-based syntax and toolchain for creating custom documentation sites and experiences.
  - 依赖markdown-it
  - We designed Markdoc to power Stripe's public docs
  - Markdoc extends Markdown with a custom syntax for tags and annotations
  - Markdoc uses markdown-it as a tokenizer, building an Abstract Syntax Tree (AST) from the array of tokens emitted by markdown-it.
    - The logic that parses the tag syntax is generated from a peg.js grammar.
  - Markdoc has its own dedicated rendering architecture rather than relying on markdown-it to generate its output. 
    - Developing an independent rendering system was necessary in order to handle Markdoc's custom tags and support multiple output formats.
# md-parser-generator
- markdown-it /10.4kStar/MIT/202009
  - https://github.com/markdown-it/markdown-it
  - https://markdown-it.github.io/
  - Markdown parser. 
  - 100% CommonMark support, extensions, syntax plugins & high speed

- remark 
  - https://github.com/remarkjs/remark/tree/main/packages/remark-parse
  - Parses Markdown to mdast syntax trees. 
  - Built on micromark and mdast-util-from-markdown

- marked /24kStar/MIT/202012/js
  - https://github.com/markedjs/marked
  - A markdown parser and compiler. Built for speed.
  - light-weight while implementing all markdown features from the supported flavors & specification

- snarkdown /2kStar/MIT/202201/js/单文件
  - https://github.com/developit/snarkdown
  - pass a Markdown string, get back an HTML string
  - it's basically one regex and a huge if statement

- https://github.com/eczn/down-parse /ts/2019
  - markdown parser with a wonderful plugin system
# md-slide
- https://github.com/hiroppy/fusuma /js
  - https://hiroppy.github.io/fusuma
  - Fusuma makes slides with Markdown easily.
  - Markdown and MDX
  - core依赖mdx、webpack.v5、express
  - client依赖react-modal、prismjs、swiper、screenfull、react-burger-menu、react-event-timeline
  - 支持导出pdf
  - https://github.com/nolimits4web/swiper
    - https://swiperjs.com/
    - Most modern mobile touch slider with hardware accelerated transitions
# md-database
- https://github.com/lukesrw/md-database /202109/ts
  - Middleware for producing SQL queries from Markdown
  - Currently only SQLite is fully supported, with support for MySQL being worked on.

- https://github.com/fictorial/gg /201903/js
  - Markdown-backed database with queries, user-defined actions, validators, variable expansion, and reporters in JavaScript
  - gg is a CLI to import, query, act on, and report on local Markdown files with support for user-defined JavaScript extensions.
  - gg supports a subset of Markdown for parsing: headers, paragraphs (the "type-inferred values"), and un-nested bullet lists 
# more-md
- https://github.com/rstudio/rmarkdown
  - rmarkdown package helps you create dynamic analysis documents
