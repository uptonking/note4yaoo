---
title: toc-office-markdown-mdx-extensions
tags: [extensions, markdown, mdx, toc]
created: 2021-01-16T20:24:19.876Z
modified: 2021-01-16T20:24:48.984Z
---

# toc-office-markdown-mdx-extensions
- 实现mdx文档编辑后自动更新的思路
  - (在当前app界面)编辑内容后直接渲染最新内容到dom，都在内存无需本地
  - (在3方编辑器界面)编辑内容后保存到本地文件，然后app扫描目录，渲染内容
- 方案1:ssg
  - 将扫描到的所有.mdx信息扫描保存到json文件，react应用import该文件，然后将所有.mdx作为源码进行build
  - 可以另外开一个命令行，定期扫描目录下的所有.mdx并输出新json替换原json，或者在后台定期通过ajax请求新json来更新页面
  - 也可以基于url进行code split，每请求一个组件或在请求前，就提前编译该路由相关的代码
- 方案2:ssr
  - 每次请求url，都会重新fetch请求mdx文件的内容

- ref
  - search: markdown plugin, md table, md electron, 缺点/mistakes
  - mdx: live edit, md in js, md superset
    - web components in md, mdx web components
  - 推广mdx的公司：gatsby、nextjs、storybook
  - I'm not an expert in JSX or MDX, but looking at the code example I would think MDX could also handle Web Components.
# mdx
- https://github.com/mdx-js/mdx
  - https://mdxjs.com/
  - /9.7kStar/MIT/202009
  - let you seamlessly use JSX in your markdown documents
- https://github.com/wooorm/xdm
  - xdm is an MDX compiler that focussed on two things:
    - Compiling the MDX syntax (markdown + JSX) to JavaScript
    - Making it easier to use the MDX syntax in different places
- https://github.com/kentcdodds/mdx-bundler
  - This is an async function that will compile and bundle your MDX files and their dependencies. It uses esbuild
  - It also uses xdm which is a more modern and powerful MDX compiler with fewer bugs and more features (and no extra runtime requirements).
  - Your source files could be local, in a remote github repo, in a CMS, or wherever else and it doesn't matter.
- https://github.com/frontarm/mdx-util
  - http://mdxc.reactarmory.com/
  - MDXC has been deprecated in favor of mdx-js/mdx.

- https://github.com/jxnblk/mdx-deck
  - https://mdx-deck.jxnblk.com/
  - React MDX-based presentation decks，依赖gatsby
- https://github.com/filoxo/minideck
  - 依赖parcel、tailwind，代码量很小，仅作demo示例
- https://github.com/PaulieScanlon/mdx-embed
  - allows you to easily embed popular 3rd party media content such as YouTube videos, Tweets, Instagram posts and many more straight into your .mdx - no import required!
  - 支持codepen, codesandbox, flickr
# mdx-docs
- https://github.com/callstack/component-docs
  - /120Star/MIT/202011/ts
  - 支持ssr，已实现自动搜索指定目录下的所有.mdx文件
  - Simple documentation for your React components.
  - component-docs is used for [react-native-paper](https://callstack.github.io/react-native-paper/)

- https://github.com/mitchgavan/react-mdx-styleguide
  - 标准的components文档网站，实现复杂度不大不小
  - 所有.mdx的路径目录通过开发者手动创建对应的路径json对象实现
  - 依赖react-router, react-live, emotion/core, prism-react-renderer, @mdx-js/loader

- https://github.com/esmevane/living-document
  - 所有.mdx的路径目录通过用户手动编辑markdown的链接`[]()`实现，自动化程度太低
  - 简洁的mdx文档网站模版，所有mdx放在pages文件夹
  - 只依赖react, react-router, styled-components, @mdx-js/loader
  - 动态请求的代码 `import(`!babel-loader!@mdx-js/loader!content/${content}`)`
- https://github.com/zaydek/esbuild-mdx
  - 依赖@mdx-js/mdx, @mdx-js/react, 例子太过简单
# mdx-tooling
- https://github.com/probablyup/markdown-to-jsx
  - The most lightweight, customizable React markdown component.
  - All this clocks in at around 5 kB gzipped
  - markdown-to-jsx uses a heavily-modified fork of simple-markdown as its parsing engine 
  - One limitation of markdown to jsx is that it does not have a transform pipeline, limiting the flexibility of the content.
  - Arbitrary HTML is supported and parsed into the appropriate JSX representation without `dangerouslySetInnerHTML`.
  - remarkjs/remark-react and mdx-js/mdx both can have plugins to the parser and transform plugins.
- mdx-scoped-runtime
  - https://github.com/karolis-sh/gatsby-mdx/tree/master/packages/mdx-scoped-runtime
  - This is a wrapper around mdx-runtime that strips down the import ... and export default Layout out of the MDX at runtime.

- https://github.com/remcohaszing/remark-mdx-code-meta
  - A remark MDX plugin for using markdown code block metadata
# md-web-components/mdjs
- https://github.com/modernweb-dev/rocket
  - https://rocket.modern-web.dev/
  - /7Star/MIT/202101
  - The modern web setup for static sites with a sprinkle of JavaScript
  - Build on top of giants like eleventy, Rollup, and Modern Web.
  - Small: No overblown tools or frontend frameworks, add JavaScript and/or Web Components only on pages where needed
  - Our goal is to provide developers with a meta framework for static websites with a sprinkle of JavaScript.
- https://github.com/open-wc/mdjs-viewer
  - Markdown JavaScript Viewer Chrome Extension
- https://github.com/zerodevx/zero-md
  - https://zerodevx.github.io/zero-md/
  - A native markdown-to-html web component based on Custom Elements V1 specs to load and display an external MD file.
  - Under the hood, it uses Marked for super-fast markdown transformation, and Prism for feature-packed syntax highlighting - automagically rendering into its own self-contained shadow DOM container

 

- https://github.com/Matsuuu/stoxy
  - Stoxy is a state management API equipped with Web Components for ease of use.
  - Stoxy is a Web Component based storage/state management tool
  - Stoxy allows you to easily handle, persist and update data in your DOM without the weight of a framework.
  - Stoxy stores the data in a in-browser Database called IndexedDB, only keeping the latest 5 accessed objects in-memory for faster access.
  - Stoxy utilizes a promise-based use flow making it really easy to asynchronously read and write from the storage.
  - If no indexeddb, Stoxy recognizes these cases automatically, and opts out of using it and utilizes a in-memory system only.
# more-md-mdx
- https://github.com/michael-klein/htmdx
  - This library is an attempt to provide a runtime to compile mdx-like markdown files (with the goal to support full JSX inside of markdown) using htm + marked that is much smaller in file-size as opposed to the official runtime
- https://github.com/wallapatta/wallapatta
  - Wallapatta is like Markdown, but has a layout inspired by handouts of Edward R. Tufte
