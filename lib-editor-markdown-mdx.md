---
title: lib-editor-markdown-mdx
tags: [editor, lib, markdown, mdx]
created: '2021-05-27T01:41:58.386Z'
modified: '2021-05-27T01:42:34.280Z'
---

# lib-editor-markdown-mdx

# guide

- ref
  - [@mdx-js/loader vs @mdx-js/mdx vs @mdx-js/react vs xdm](https://www.npmtrends.com/@mdx-js/loader-vs-@mdx-js/mdx-vs-@mdx-js/react-vs-xdm)
  - @mdx-js/mdx和xdm都依赖 remark-parse, remark-rehype的unified生态，还依赖 vfile、estree-walker
# mdx-pros

# mdx-cons
- 不支持在mdx中直接书写import esm-url
  - https://cdn.skypack.dev/jquery
  - https://cdn.jsdelivr.net/npm/jquery@3.6.0/dist/jquery.js
# faq

## 如何在.mdx文件中动态导入npm仓库中的js库？

- ### 尝试解决此问题的参考方案
- https://github.com/hashicorp/next-mdx-remote
  - 支持获取远程mdx文本内容和动态数据
  - The file content must be local.
  - You are bound to filesystem-based routing. 
  - You will end up running into performance issues. 
  - You will be limited in the ways you are able to structure relational data.
- https://github.com/kentcdodds/mdx-bundler
  - 支持获取远程mdx文本内容
  - The problem: You have a string of MDX and various TS/JS files that it uses and you want to get a bundled version of these files to eval in the browser.
  - next-mdx-remote is not a bundler, it's just a compiler. 
  - mdx-bundler is an MDX compiler and bundler.
  - Webpack/rollup/etc also require that all your MDX files are on the local filesystem to work.
  - mdx-bundler can definitely be used at build-time, but it's more powerfully used as a runtime bundler.
  - You might decide to go with a built-time approach (for Gatsby/CRA), but as mentioned, the true power of mdx-bundler comes in the form of on-demand bundling. 
  - So it's best suited for SSR frameworks like Remix/Next.

- 在.mdx文件中书写`import { useTable } from 'react-table'`时，会由webpack处理
  - 导入的依赖其实会在浏览器中变成全局依赖，挂再到浏览器的`window`上

- 若在mdx中import没有预先打包进bundle的库，会提示`Component Checkbox was not imported, exported, or provided by MDXProvider as global scope`
  - 所以需要预先提供到 MDXProvider
