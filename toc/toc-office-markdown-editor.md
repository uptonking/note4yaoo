---
title: toc-office-markdown-editor
tags: [editor, markdown, toc]
created: 2022-11-09T11:52:30.801Z
modified: 2022-11-09T11:53:13.093Z
---

# toc-office-markdown-editor

# guide

- tips
  - 没必要找单独的md编辑器，一般主流的wysiwyg会有第三方支持md的版本

- popular-md-products(产品核心部分都是编辑器)
  - outline, HedgeDoc/CodiMD/HackMD, Crowi
  - gitbook, bookdown, docsify, docusaurus, nextra
  - foam, dendron, gistpad, obsidian-dataview
  - notable, BoostNote, standardnotes/web, notea, laverna, vnote
  - mdx-deck, md2googleslides, marp, nodeppt, gitpitch
  - react-resume-site

- popular-md-editor
  - milkdown, tui.editor, milkdown, rich-markdown-editor, vditor
  - zettlr
  - mermaid
# markdown-editor
- web-editor-markdown /392Star/MIT/202211/ts/vanillajs/NoDeps/inactive
  - https://github.com/Ben-love-zy/web-editor-markdown
  - 基于 Web 浏览器，即时渲染的 Markdown 编辑器
  - 基于 TypeScript 和 vanillajs 打造，并且不依赖任何第三方框架，对中文支持友好
  - 提供源码模式、双屏渲染模式、实时编辑模式和只读模式四种渲染模式。
  - 如果有需要，它的底层同时也支持了协同编辑的能力，提供了原子操作 Operation 用于扩展协同编辑。

- https://github.com/marktext/muya /549Star/MIT/202404/ts
  - markdown editor for web browser applications development
  - 依赖fuse.js、marked、katex、ot-json1、prismjs、snabbdom、turndown、vega-lite
  - Muya originated from MarkText, which was originally used in the MarkText and provides Markdown editing support for MarkText. Today, Muya is available as a stand-alone library 
  - What is the relationship between MarkText's version and the Muya's version? None
  - https://github.com/Jocs/muya-example /201906/js

- rich-markdown-editor /2kStar/BSD/202105/ts
  - https://github.com/outline/rich-markdown-editor
  - 依赖react、styled-components、prosemirror-markdown、markdown-it、prism-refractor、fuzzy-search、react-medium-image-zoom
  - React and Prosemirror based markdown editor that powers Outline.
  - The editor is WYSIWYG and includes formatting tools whilst retaining the ability to write markdown shortcuts inline and output plain Markdown.
  - https://atlaskit.atlassian.com/packages/editor/editor-markdown-transformer
    - A Markdown to ProseMirror Node parser.

- milkdown /6.5kStar/MIT/202208/ts
  - https://github.com/Saul-Mirone/milkdown
  - https://milkdown.dev/
  - https://milkdown.dev/online-demo
  - 依赖prosemirror、remark、prism、katex，但不依赖prosemirror-markdown、react
  - A plugin-driven WYSIWYG markdown Editor, inspired by Typora, built on top of prosemirror and remark.
  - 不同于其他prosemirror项目，可配置支持的markdown特性
  - ⚠️️breaking: @milkdown/core@4.4.0(202107) migrate from markdown-it to remark

- react-markdown-editor-lite /833Star/MIT/202205/ts/非所见即所得/inactive
  - https://github.com/HarryChen0506/react-markdown-editor-lite
  - https://harrychen0506.github.io/react-markdown-editor-lite/
  - 基于textarea和React的markdown编辑器，实现简单且清晰
  - UI可配置, 如只显示编辑区或预览区，支持编辑区和预览区同步滚动
  - 依赖react、eventemitter3
  - 支持配置markdown-parser, 示例使用markdown-it

- react-universal-markdown /202107/js/inactive
  - https://github.com/iddan/react-universal-markdown
  - Markdown component for Web and Native powered by CommonMark
  - With React Native/DOM
  - 依赖commonmark

- https://github.com/mdx-editor/editor /ts/lexical
  - https://mdxeditor.dev/
  - https://mdxeditor.dev/editor/demo
  - open-source React component that allows users to author markdown documents naturally
  - MDXEditor is a rich, client-side component that does not benefit from server-side rendering. To use it in your server components, you should use next/dynamic
  - 依赖lexical、codemirror6、radix-ui、hast、mdast、react-diff-view、react-hook-form

- https://github.com/uiwjs/react-md-editor /MIT/202403/ts
  - https://uiwjs.github.io/react-md-editor
  - A simple markdown editor with preview, implemented with React.js and TypeScript.
  - This is based on `textarea` encapsulation, so it does not depend on any modern code editors such as Acs, CodeMirror, Monaco etc.
  - 依赖rehype-prism-plus、@uiw/react-markdown-preview
- https://github.com/uiwjs/react-markdown-editor /MIT/202404/ts
  - https://uiwjs.github.io/react-markdown-editor
  - A markdown editor with preview, implemented with React.js and TypeScript.
  - 依赖codemirror6、@uiw/react-markdown-preview、highlight.js

- vditor /1.3kStar/MIT/202009
  - https://github.com/Vanessa219/vditor
  - In-browser Markdown editor, support WYSIWYG (Rich Text), Instant Rendering (Typora-like) and Split View modes.
  - 依赖lute(go语言实现md解析)、hightlight、echarts、katex、mermaid、mathjax，注意依赖文件直接在源码的js/文件夹，不在package.json

- https://github.com/LHRUN/md-editor
  - https://songlh.top/md-editor/
  - 基于markdown-it打造的markdown编辑器，功能包括：同步滚动、目录列表生成、快捷编辑按钮、代码块主题切换、内容状态缓存
  - 依赖antd、highlight.js、md-it
  - [基于markdown-it打造的markdown编辑器](https://songlh.top/2022/10/12/%E5%9F%BA%E4%BA%8Emarkdown-it%E6%89%93%E9%80%A0%E7%9A%84markdown%E7%BC%96%E8%BE%91%E5%99%A8/)

- yfm-editor /3Star/MIT/202211/ts/md-it
  - https://github.com/yandex-cloud/yfm-editor
  - https://ydocs.tech/en/
  - https://preview.yandexcloud.dev/yfm-editor/
  - 依赖prosemirror、markdown-it、react-use、gravity-ui
  - Yandex Flavored Markdown (YFM) is a Markdown dialect and a set of tools for transforming Markdown to HTML in real time and building complete documentation projects.
  - Expandable: you can add any plugin for markdown-it or write your own.

- https://github.com/Resetand/textarea-markdown-editor  /ts
  - UI headless simple markdown editor using only textarea
  - 依赖react
  - You can choose any markdown parser, create your own layout, and use your own textarea component that is styled and behaves however you like

- https://github.com/kumachan-mis/react-realtime-markup-editor
  - A text document editor which is syntactically formattable in real time
  - 类似typora的即时渲染
  - 依赖react、katex、emotion
  - 组件采用atoms/molecules/organisms结构

- https://github.com/GDUcrash/write
  - https://writeapp.vercel.app/
  - Extremely minimalistic text editor
  - 依赖react-markdown

- https://github.com/donny-chan/qingshu /MIT/202307/ts/vue/inactive
  - 现代的、极简的、美观、对中文友好的 Markdown 编辑器。
  - A modern, minimalistic Markdown editor for Windows, implemented in Vue + Electron + TypeScript.
  - Support GitHub Flavored Markdown + LaTeX (including inline math).

- https://github.com/Eroxl/Note-Rack
  - An inline WYSIWYG markdown editor built for students to manage school work

- https://github.com/remarkjs/react-markdown /12.1kStar/MIT/202309/js/单文件
  - https://remarkjs.github.io/react-markdown/
  - 依赖remark-parse、remark-rehype、unified, vfile
  - React component to render markdown
  - safe by default (no `dangerouslySetInnerHTML` or XSS attacks)
  -  plugins (many plugins you can pick and choose from)
  - why this one?
    - The two main reasons are that they often rely on `dangerouslySetInnerHTML` or have bugs with how they handle markdown. 
    - react-markdown uses a syntax tree to build the virtual dom which allows for updating only the changing DOM instead of completely overwriting.
  - https://github.com/remarkjs/remark /MIT/202403/js
    - remark is a tool that transforms markdown with plugins.
    - You can use remark on the server, the client, CLIs, deno, etc.
    - 100% to CommonMark, 100% to GFM or MDX with a plugin

- https://github.com/StackExchange/Stacks-Editor
  - Stack Overflow's Combination Rich Text/Markdown Editor
  - 依赖prosemirror, hightlight.js，不依赖react

- https://github.com/benweet/stackedit
  - In-browser Markdown editor
- https://github.com/pandao/editor.md
  - The open source embeddable online markdown editor (component).

- https://github.com/bytedance/bytemd /202210/ts/svelte
  - https://bytemd.js.org/
  - https://bytemd.js.org/playground/
  - Markdown editor component built with Svelte.
  - ByteMD could be used in the Server-side rendering(SSR) environment without extra config.
  - ByteMD uses remark and rehype ecosystem to process Markdown

- https://github.com/Tencent/cherry-markdown /3kStar/apache2/202311/js
  - https://tencent.github.io/cherry-markdown/examples/index.html
  - a Javascript Markdown editor
  - 代码结构很清晰
  - 依赖jsdom、mitt
  - It can run in browser or server(with NodeJs).
  - 多种模式
    - 双栏编辑预览模式（支持同步滚动）
    - 纯预览模式
    - 无工具栏模式（极简编辑模式）
    - 移动端预览模式
  - Editor supports most commonly used markdown syntax (such as title, TOC, flowchart, formula, etc.) by default.

- https://github.com/voracious/ink-mde
  - The flexible TypeScript Markdown editor that powers https://octo.app
  - 依赖codemirror6、lezer、solidjs
  - ui部分代码少

- https://github.com/mermaid-js/mermaid-live-editor /MIT/202403/ts/svelte
  - https://mermaid-js.github.io/mermaid-live-editor/
  - https://mermaid.live/
  - Edit, preview and share mermaid charts/diagrams. 
  - New implementation of the live editor.
  - 左侧代码，右侧流程图，整体类似markdown编辑器
# md-app
- https://github.com/1943time/bluestone /AGPLv3/202403/ts
  - https://www.bluemd.me/
  - 青石是一个开源的所见即所得Markdown编辑器
  - markdown的table元素也不利于书写，双栏模式并不利于聚焦，所以开发了青石编辑器。
  - 使用了富文本的编辑模式，同时兼容Markdown语法转换与编辑习惯，当使用搜索功能时，Markdown符号不会被搜索。
  - Using shiki as a code shader to make code highlights more fine-grained
  - 依赖electron-store、rxjs、mobx-react-lite、remark-gfm、antd

- https://github.com/tk04/Marker /MIT/202403/ts/tauri
  - A Desktop App for Easily Viewing and Editing Markdown Files
  - user-friendly UI for viewing and editing markdown files
# examples
- https://github.com/joshnuss/hypersonic /202401/js/svelte
  - https://hypersonic.wiki/
  - A multi-player markdown editor and wiki
  - https://twitter.com/joshnuss/status/1744412987862007968
    - PWA-ready, Self-hostable
# more-markdown-editor
- vscode-monaco-editor
