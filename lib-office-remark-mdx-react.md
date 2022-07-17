---
title: lib-office-remark-mdx-react
tags: [lib, mdx, react, remark]
created: 2021-06-02T16:46:04.864Z
modified: 2021-06-02T16:46:45.119Z
---

# lib-office-remark-mdx-react

# guide

# mdx
- 处理mdx中ojs的思路
  - transform: 对mdxast使用remark插件提取code blocks
  - generate: 定制输出 mdxhast -> jsx

# ref

- jsxtreme-markdown /81Star/MIT/202006/js
  - https://github.com/mapbox/jsxtreme-markdown
  - https://mapbox.github.io/jsxtreme-markdown/
  - 依赖remark-*、rehype-raw、hast-util-to-jsx、unist-util
  - Transform Markdown into JSX or React component modules
  - You can interpolate JS expression and JSX elements between designated delimiters`{{}}`.

- readmeio-markdown /2Star/ISC/202105/js
  - https://github.com/readmeio/markdown
  - https://rdmd.readme.io/docs/syntax-extensions
  - 依赖remark-*、rehype-react、rehype-raw、unist-util
  - 主要语法扩展包括gfm、code-tabs、callouts、embed
  - ReadMe's flavored Markdown parser and MDX rendering engine
  - this package exports a function which takes a string of ReadMe-flavored markdown and returns a tree of React components
