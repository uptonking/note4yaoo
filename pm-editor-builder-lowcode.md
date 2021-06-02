---
title: pm-editor-builder-lowcode
tags: [builder, editor, lowcode, pm]
created: '2020-08-08T19:39:58.351Z'
modified: '2021-06-02T17:21:11.227Z'
---

# pm-editor-builder-lowcode

# guide

- 不建议做得过于通用，过于细节
- 建议根据应用场景，研发一个主题的组件，然后拖拽拼装
- table component/app builder
  - export html/gist
  - export png

# product-blocks

- blocks /MIT/3.5kStar/202006
  - https://github.com/blocks/blocks
  - https://blocks-ui.com/
  - A JSX-based page builder for creating beautiful websites without writing code
- How it works
  - Blocks is a parser, transformer, and renderer/compiler.
  - It's unique because it reads in valid, production-ready JSX code and treats the AST as its data structure. 
  - Information is queried from the AST and then changes to the canvas transform the AST.
  - It uses Babel and its plugin API for parsing and transforming. 
  - Events that happen in the canvas are emitted and run corresponding plugins on the source code.

# solution-catalog-builder

- VvvebJs /Apache2/3.3kStar/202007
- grapesjs /BSD/11.4kStar/202008
- react-page /LGPLv3/8.2kStar/202008/ts

# blog

- more
  - [React组件可视化拖拽页面搭建，源码生成，你有什么想法？](https://www.zhihu.com/question/392818555)
