---
title: lib-editor-codemirror-examples
tags: [code-editor, codemirror, examples]
created: 2023-06-23T12:46:36.949Z
modified: 2023-06-23T12:46:53.288Z
---

# lib-editor-codemirror-examples

# guide

- 支持切换editor的方案: overleaf(ace/src/visual), sandpack, jupyter, livecodes, @uiw/react-*-editor

- examples
  - 类似打字机动态输出文字, 多用于ai生成代码/文本
    - **pausable**
    - multi-writer的效果
  - (diff)字符渐变的动画效果, 🤔 和时间旅行的回放过程有何区别
    - diff只需初始结束状态, 而时间旅行支持中间状态
  - codemirror + dockview/fileTree, partykit

- diff视图 unifiedMergeView
  - 上下版: 参考 BlazorCodeMirror6, code-editor-angular
  - 左右版: 参考 mdxeditor, jupyter-nbdime

- fans-codemirror
  - https://github.com/val-town/codemirror-ts
  - https://github.com/uiwjs/react-codemirror /华人
  - https://github.com/yeliex/codemirror-extensions /华人
  - https://github.com/exuanbo/codemirror-toolkit /华人
  - https://www.npmjs.com/package/collaborative-codemirror

- resources
  - https://codemirror.net/docs/community/
  - https://news.ycombinator.com/threads?id=CompuIves
  - [List of community extensions? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/list-of-community-extensions/4899)
# popular
- https://github.com/tmcw/awesome-codemirror
  - Awesome CodeMirror plugins, themes, wrappers, and more

- https://github.com/milahu/browserforge /202303/方案收集markdown
  - run github + github-pages + codesandbox in your browser, offline-first - CONCEPT

- overleaf /12.6kStar/AGPLv3/202407/js/ts/latex/ace>codemirror
  - https://github.com/overleaf/overleaf
  - https://github.com/overleaf/overleaf/wiki
  - https://github.com/overleaf/overleaf/tree/main/services/web/frontend/js/features/source-editor
  - A web-based collaborative LaTeX editor
  - CodeEditor和VisualEditor都基于codemirror6实现
  - source-editor支持codemirror6、ace
  - https://github.com/overleaf/ace /202108/js/inactive/Ajax.org Cloud9 Editor
  - [Compile Error and PDF Download Notifications](https://github.com/overleaf/overleaf/issues/1031)
    - migrate from ACE to CodeMirror 6. Yes, the CM6 work will be coming to CE soon. _202206
  - https://github.com/overleaf/overleaf/tree/main/services/document-updater/app/js/sharejs /202205/MIT/js
    - 🔀 协作基于sharejs.v0.5修改实现
  - https://github.com/overleaf/overleaf/blob/main/services/web/frontend/js/features/source-editor/extensions/track-changes.ts
    - 基于codemirror6实现track-changes的示例
    - 在生产环境编辑器的track-changes试用入口播放了添加和删除文字的动画，没有直接实现删除线但效果类似
    - [Track changes and commenting in LaTeX - Overleaf, Online LaTeX Editor](https://www.overleaf.com/track-changes-and-comments-in-latex)
    - [Track Changes in Overleaf intro](https://www.overleaf.com/learn/how-to/Track_Changes_in_Overleaf)
    - [Tracking changes in LaTeX with "changes" package _201908](https://www.overleaf.com/latex/examples/tracking-changes-in-latex-with-changes-package/fnpkpytjjwhj)
  - 🫧 [Horizontal Scaling: Starting with version 3.5.6 Server Pro supports horizontal scaling _202305](https://github.com/overleaf/overleaf/wiki/Horizontal-Scaling)
    - A deployment of Server Pro with horizontal scaling involves a set of external components, such as a Load Balancer and an S3-compatible backend
  - [Is it possible to include the commenting feature in the Community Edition? _202402](https://github.com/overleaf/overleaf/issues/1193)
    - You can try to develop it by yourself, or purchase server pro. Btw, I think commenting feature is not something difficult to imply, the core code is open-source, just need a proxy.
    - I created a new branch, which includes only the code for enabling comments and changes tracking features. 
  - 🍴 forks
  - https://github.com/yu-i-i/overleaf-cep /202408/AGPL
    - extended CE with changes tracking and LDAP authentication
    - 作者一直跟着官方上游更新
    - I'm not a programmer, just a LaTeX user with basic programming knowledge, and I don't plan to further develop this code. The current patched version meets my needs
    - https://github.com/yu-i-i/overleaf-cep/tree/track-changes
      - I created a new branch, which includes only the code for enabling comments and changes tracking features.
  - https://github.com/ayaka-notes/overleaf /202405
    - 如果你想用我开发的overleaf pro，你需要2c 4g以上的服务器，甚至更高配置的服务器才能运行
    - 2c 4g甚至只够几个人同时编辑，如果你需要更多，还需要更高昂的服务器配置。最低服务器的价格可能在720元
    - 进阶功能比如git、github同步，还有引文搜索，都无法使用
    - 此外，overleaf的API变化频繁，花时间去猜测他们修改了什么代码，查找API，没有任何意义而且浪费时间。哪怕我能维护一年两年，未来可能也不会一直跟进。
    - 同样的价格，甚至足以拿下overleaf学生版（600多一年），所以通过逆向API开发所谓的overleaf pro，并没有意义。此项目宣布终止维护。
    - [运行./dev.sh后编译论文报错 ](https://github.com/ayaka-notes/overleaf/issues/5)
  - https://github.com/ertuil/overleaf
    - a quick implication of review panel
  - https://github.com/smhaller/ldap-overleaf-sl
    - Free LDAP and OAuth2 Authentication and Authorisation for Sharelatex / Overleaf (Community Edition)

- https://github.com/codesandbox/sandpack /4.5kStar/apache2/202405/ts
  - https://sandpack.codesandbox.io/
  - https://sandpack.codesandbox.io/docs
  - https://sandpack.codesandbox.io/docs/advanced-usage/components
  - Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.
  - sandpack-react依赖codemirror6、lz-string、react-devtools-inline
  - sandpack-client依赖nodebox、static-browser-server
  - 提供了很多示例，包括cm-DecoratorsDynamic/FileExplorer/ReactDevTools
  - CodeEditor支持codemirror/monaco/vscode
  - `SandpackCodeEditor` component renders a wrapper over codemirror. You can extend the editor with any CodeMirror extensions
  - `SandpackCodeViewer` renders a read-only version of codemirror
  - `Preview` component is running the sandpack bundler, so without rendering a Preview component you will not have any bundling and evaluation of the code in sandpack
  - Sandpack Client: This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.
  - Sandpack React: React components that give you the power of editable sandboxes that run in the browser
  - https://github.com/AaronPowell96/sandpack-file-explorer /MIT/202312/ts
    - Enhanced File Explorer for Sandpack. Providing immense flexibility to Sandpack's capabilities.
    - Drag and drop to move files or directories
    - Add and remove files or directories
  - https://github.com/codeamigo/codeamigo /GPLv3/202401/ts/inactive
    - codeamigo is a platform that helps people learn to code with an AI assistant.
    - 依赖express、apollo-server、graphql、next.js、postgresql、redis
  - https://github.com/danilowoz/sandpack-tsserver
    - https://github.com/aboveyunhai/playground-ts
    - [TypeScript integration · codesandbox/sandpack _202112](https://github.com/codesandbox/sandpack/discussions/237)
      - once you start to edit the code or change tab (trig render basically), ts-server will start to kick in

- https://github.com/jupyterlab/jupyterlab/tree/main/packages/codemirror /202405/ts
  - A JupyterLab package which provides the default implementation of the `@jupyterlab/codeeditor` interface, using the `CodeMirror` editor.
  - cm编辑器及ext相关代码不多
  - https://github.com/jupyterlab/jupyterlab/tree/main/packages/codemirror-extension
    - A JupyterLab package which provides an entry point, commands, and keyboard shortcuts for the `@jupyterlab/codemirror` package.
  - https://github.com/jupyterlab/jupyterlab/tree/main/packages/codeeditor
    - A JupyterLab package which defines an abstract interface to a code editor, which is used in many places in the application, including cells and the file editor.
  - https://github.com/jupyterlab/jupyterlab-monaco /BSD/201807/ts/archived
    - A JupyterLab extension providing the Monaco editor.
    - This project has been archived by lack of maintainers
    - merely a 'proof-of-concept' implementation 
  - [Explore monaco editor integration · jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab/issues/135)
  - [Update Codemirror to version 6 _202106](https://github.com/jupyterlab/jupyterlab/issues/10370)
    - [pr已合并: Migrate to Codemirror 6 _202207](https://github.com/jupyterlab/jupyterlab/pull/11638)
  - https://github.com/jupyter/nbdime
    - Tools for diffing and merging of Jupyter notebooks.

- Zettlr /9.3kStar/GPLv3/202401/ts/vue/偏学术编辑器
  - https://github.com/Zettlr/Zettlr
  - https://www.zettlr.com/
  - https://docs.zettlr.com/
  - Your One-Stop Publication Workbench
  - 依赖electron-forge、codemirror.v6、@lezer/highlight、d3.v7、katex、remark-math、vue3、vuex4、pinia
  - exports with Pandoc, LaTeX, and Textbundle
  - support LaTeX and Word template
  - Citations made easy: Tight and ever-growing integration with your favourite reference manager (Zotero, JabRef, and many others)
  - Support for state of the art knowledge management techniques (Zettelkasten)

- https://github.com/sourcegraph/openctx/tree/main/client/codemirror /apache2/202405/ts
  - https://openctx.org/playground
  - implements a CodeMirror extension that shows OpenCtx items in the editor
  - OpenCtx shows you contextual info about code from your dev tools, in your editor, in code review, and anywhere else you read code
  - https://github.com/sourcegraph/codeintellify /MIT/202111/ts/archived
    - Adds code intelligence to code views on the web
    - This library manages all of the inputs (mouse/keyboard events, location changes, hover information, and hover actions) necessary to display hover tooltips on with a code view.
    - 依赖rxjs、sourcegraph

- https://github.com/vizhub-core/vzcode /MIT/202406/ts
  - VZCode: Multiplayer Code Editor
  - VZCode offers a multiplayer code editing environment that caters to a real-time collaborative development experience. It's the code editor component of VizHub, and can also be used independently from VizHub.
  - Browser-based editing environment
  - Real-time collaboration via LAN or using services like NGrok
  - A known shortcoming of VZCode is that it does not (yet) watch for changes from the file system. VZCode assumes that no other programs are modifying the same files.
  - You can also expose your VZCode instance publicly using a tunneling service such as NGrok.
  - Auto-save, debounced after code changes
  - [VSCode-ish: Jump to Definition of Variable ](https://github.com/vizhub-core/vzcode/issues/177)
    - [202406已合并pr](https://github.com/vizhub-core/vzcode/pull/717)
    - I also have a history of working with CodeMirror 5 + ShareDB for the real-time integration, and was able to "unlock" that CodeMirror 6 + ShareDB integration successfully
  - [Intelligent Autocompletions ](https://github.com/vizhub-core/vzcode/pull/305)
  - https://github.com/vizhub-core/vizhub
    - https://vizhub.community/
    - Self Hosted CMS for Web-based Dataviz
    - VizHub 2 has been used in Data Visualization Course 2018, Datavis 2020
    - iFrame-based code execution environment.
  - VizHub 3
    - possible to self-host your own instance
    - possible to extend the core with plugins
  - https://github.com/vizhub-core/codemirror-6-experiments /MIT/201811/js
    - [Codemirror 6 Experiments _201811](https://currankelleher.medium.com/codemirror-6-experiments-a3930bf03781)

- https://github.com/prevwong/reka.js /437Star/MIT/202404/ts/yjs/暂未用在craft
  - https://reka.js.org/
  - https://reka.js.org/docs/introduction
  - ✨ Reka is a state management system for building no-code editors
  - Reka solves this by providing an AST-powered state system that enables end-users to create UI components that are nearly as complex as ones that developers could write in code
  - along with an interpreter to efficiently compute an output that could be rendered on the browser.
  - core依赖mobx、nanoid, 周边依赖mobx-react-lite、codemirror6、@lezer/highlight、acorn-jsx、yjs
  - 示例使用unist-ast
  - https://github.com/prevwong/reka.js/tree/main/packages/codemirror
    - Contains the CodeMirror extension that provides syntax highlighting for Reka code
  - https://github.com/prevwong/reka.js/tree/main/packages/react-code-editor /202404/ts
    - Codemirror editor for editing Reka AST in code

- https://github.com/glacambre/editor-adapter /MIT/202211/ts/inactive
  - A library to interact with in-browser JS editors like Ace, CodeMirror or Monaco

- https://github.com/yuku/textcomplete /1.7kStar/MIT/202312/ts/inactive
  - https://yuku.takahashi.coffee/textcomplete/
  - Autocomplete for HTMLTextAreaElement and more
  - 支持 textarea/contenteditable/codemirror

- https://github.com/davidmyersdev/ink-mde /206Star/MIT/202405/ts
  - https://stackblitz.com/fork/github/davidmyersdev/ink-mde/tree/main/examples/template-ts
  - A beautiful, modern, customizable Markdown editor powered by CodeMirror 6 and TypeScript
  - This is the editor that powers https://octo.app.
  - Inline Markdown image previews
  - Framework agnostic, 支持vue/svelte
  - Supports Server-Side Rendering (SSR)
  - Wrap a native `textarea` element with the `wrap` export
  - Plugin API (experimental)
  - https://github.com/davidmyersdev/octo /MPLv2/202405/ts/vue
    - https://octo.app/
    - A local-first, progressive web app for knowledge management
    - End-to-End Encryption (E2EE) support

- https://github.com/imzbf/md-editor-rt /MIT/202407/ts
  - https://imzbf.github.io/md-editor-rt
  - https://imzbf.github.io/md-editor-rt/en-US/demo
  - react版本的 Markdown 编辑器
  - 源码与预览同步滚动
  - 支持切换预览风格、代码风格主题
  - 当使用服务端渲染时，请务必设置editorId为固定值
  - 自定义 markdown-it 核心库扩展、属性等
  - https://github.com/imzbf/md-editor-v3 /MIT/202407/ts
    - https://imzbf.github.io/md-editor-v3
    - vue3 环境的 Markdown 编辑器
  - https://github.com/imzbf/md-editor-extension
    - Common extensions for md-editor-v3 and md-editor-rt.

- https://github.com/replit/codemirror-minimap /202401/ts
  - Minimap extension for Codemirror 6

- https://github.com/replit/codemirror-interact /202403/ts
  - https://replit.com/@util/codemirror-interact
  - A CodeMirror extension that lets you interact with different values (clicking, dragging, etc).

- https://github.com/val-town/codemirror-codeium /ISC/202404/ts
  - https://val-town.github.io/codemirror-codeium/
  - Codeium code completion integration for CodeMirror 6
  - 🤖 Copilot-like ghost text code from modeling-app by Jess Frazelle and based on Cursor.

- https://github.com/exuanbo/codemirror-toolkit /MIT/202312/ts
  - A batteries-included toolset for efficient development of CodeMirror 6 based editors (w/o React).
  - https://github.com/code4mk/codemirror-toolkit /202208/ts/inactive
    - easily use codemirror editor with codemirror-toolkit on react , vue , svelte
  - [@codemirror-toolkit/react - A small and flexible solution for binding CodeMirror 6 to React : r/reactjs _202301](https://www.reddit.com/r/reactjs/comments/107to4j/codemirrortoolkitreact_a_small_and_flexible/)
    - I always wanted to use such a library when I was developing my Assembler Simulator in React. But all I could find at the moment was like @uiw/react-codemirror, it's "badly written" (e.g. reading a ref's current value during rendering) and contains too many dependencies I don't need, which cannot be tree-shaked so that you can toggle them in props.
    - So I decided to write it my self and here it is! The API design is inspired by zustand btw

- https://github.com/sachinraja/rodemirror /MIT/202112/ts/inactive
  - React component for CodeMirror 6
  - Efficient, only renders when necessary and uses StateEffect to update the editor state on prop changes. The view and state are never recreated.
- https://github.com/atassis/react-codemirror-ts /MIT/202206/ts/inactive
  - Codemirror react wrapper made with typescript

- https://github.com/azu/codemirror-console /202404/js
  - https://codemirror-console.netlify.com/
  - Web Console UI for JavaScript.
  - 依赖codemirror5、in-browser-language
  - https://github.com/aliyun/alibabacloud-console-base /MIT/202311/ts
    - 阿里云控制台基座, CodeMirror 5 的 React 封装，适用于极简的场景

- https://github.com/uiwjs/react-markdown-editor /MIT/202404/ts
  - https://uiwjs.github.io/react-markdown-editor
  - A markdown editor with preview, implemented with React.js and TypeScript.
  - 依赖@uiw/react-codemirror、@uiw/react-markdown-preview
  - 支持源码和预览同步滚动

- https://github.com/uiwjs/react-codemirror /MIT/202404/ts
  - https://uiwjs.github.io/react-codemirror/
  - https://uiwjs.github.io/react-codemirror/#/merge/document
  - CodeMirror 6 component for React
  - Versions after `@uiw/react-codemirror@v4` use codemirror 6.
    - 从v4开始使用cm6，v3.0 cannot be upgraded to 4.0+
    - [Codemirror 6 ](https://github.com/uiwjs/react-codemirror/issues/88)
  - 提供了很多示例和ext，包括theme-editor/mention/merge
  - The bundled version supports use directly in the browser
  - Support theme customization, provide theme editor.
  - 还提供了其他编辑器的示例，包括textarea/monaco/json
  - https://github.com/IBM/carbon-react-code-mirror /apache2/202311/js
    - Carbon React Code Mirror is a wrapper for @uiw/react-codemirror that uses Carbon styling.

- https://github.com/uiwjs/react-md-editor /MIT/202403/ts
  - https://uiwjs.github.io/react-md-editor
  - A simple markdown editor with preview, implemented with React.js and TypeScript.
  - This is based on `textarea` encapsulation, so it does not depend on any modern code editors such as Acs, CodeMirror, Monaco etc.
  - 依赖rehype-prism-plus、@uiw/react-markdown-preview
- https://github.com/uiwjs/react-code-preview /MIT/202403/ts
  - https://uiwjs.github.io/react-code-preview/
  - Code edit preview for React
  - 编辑代码时立刻刷新预览
  - 依赖@uiw/react-codesandbox、@uiw/react-codemirror

- https://github.com/scniro/react-codemirror2 /MIT/202108/ts/v5/inactive
  - https://scniro.github.io/react-codemirror2/
  - ships with the notion of an uncontrolled and controlled component

- https://github.com/rennzhang/codemirror-editor-vue3 /MIT/202204/ts
  - https://rennzhang.github.io/codemirror-editor-vue3
  - CodeMirror component for Vue3
  - https://github.com/cloudacy/vue-markdown-edit /202112/ts
    - simple markdown editor based on CodeMirror built for VueJS.
- https://github.com/logue/vue-codemirror6 /MIT/202407/ts
  - @codemirror 6 component for @vuejs. Vue2 & Vue3 both supported.

- https://github.com/surmon-china/vue-codemirror /MIT/202208/ts/vue/inactive
  - @codemirror code editor component for @vuejs
  - a new version based on CodeMirror@6 and is available to Vue3 only.

- https://github.com/getcursor/old /192Star/MIT/202304/ts/inactive
  - A Codemirror-based editor with many modern need-to-haves (e.g. LSP, Copilot, Vim, Remote SSH)
  - This is an old version of Cursor based off of the Codemirror text editing component. If you're looking to build your own code editor from the ground-up, this may serve as a useful guide. Cursor is now based on a fork of VSCodium.
  - 依赖codemirror6、@headlessui/react、@reduxjs/toolkit、electron-store、markdown-it、vscode-languageserver-protocol、xterm、xterm-addon-search
  - AI Features: auto-generated inline diffs and completions, a ChatGPT-style embedded chat, on-hover documentation suggestions

- https://github.com/difizen/libro /MIT/202404/ts
  - 大模型时代的 notebook 产品方案
  - 定义大模型工作流，内置大模型交互和辅助开发能力
  - 更优雅的交互体验，兼容 jupyter notebook
  - 您可以在自己的工作流中使用 prompt cell，快速完成与大模型的交互，生成的结果也可以在上下文中继续访问
  - https://github.com/difizen/libro-server /202404/python
    - 使用 rye 来管理多 python 包组成 monorepo，多个包会共享同一个虚拟环境 venv

- https://github.com/0xsuk/agitcms /MIT/202212/ts/inactive
  - A hackable headless CMS for markdown blogs
  - Agit CMS is a simple web frontend interface that utilizes filesystem to manage markdown/media contents. Built for markdown-based static site generators, like Hugo and Jekyll.
  - 依赖codemirror6、mui5、remark-gfm、remark-parse、xterm

- https://gitlab.com/emergence-engineering/prosemirror-codemirror-block /202310/ts
  - https://emergence-engineering.com/blog/prosemirror-codemirror-block
  - CodeMirror 6 code_block in ProseMirror
    - Legacy ( CodeMirror 5 ) language support trough @codemirror/legacy-modes
  - Customizable language selector
  - Lazy-loaded language support
- https://github.com/sibiraj-s/prosemirror-codemirror-6 /MIT/202206/ts/inactive
  - https://sibiraj-s.github.io/prosemirror-codemirror-6/
  - Prosemirror with Codemirror 6 (demo)
  - Based on the example from https://prosemirror.net/examples/codemirror/. This is just an example setup and might not be very reusable. Use this to get something up-and-running quickly.
- https://github.com/remirror/remirror/tree/main/packages/remirror__extension-codemirror6
  - Add CodeMirror to your editor

- https://github.com/phartenfeller/react-readonly-codemirror6 /MIT/202402/js
  - https://phartenfeller.github.io/react-readonly-codemirror6/
  - I use this component for server-side generated code previews (with Gatsby). It uses Codemirror 6 which is currently in preview.

- https://github.com/jamischarles/codemirror-server-render /202302/js/inactive
  - Renders CodeMirror 6 syntax highlighting as a string so you can use it at build time (ie: blog) or server-side
- https://github.com/readmeio/codemirror-node /ISC/202202/js/inactive
  - CodeMirror on the server
  - 依赖codemirror5

- https://github.com/joplin/website-plugin-discovery /MIT/202401/ts/mustache
  - https://joplinapp.org/plugins/
  - https://joplinapp.org/help/api/get_started/plugins/
  - The official plugin repository website
  - 依赖codemirror.v6、highlight.js、markdown-it、mustache、webpack
  - 详情页会显示Minimum app version、下载量
  - 搜索没有单独的页面

- https://github.com/expressive-code/expressive-code /MIT/202405/ts/不依赖codemirror
  - https://expressive-code.com/
  - A text marking & annotation engine for presenting source code on the web
  - Expressive Code is an engine for presenting source code on the web, aiming to make your code easy to understand and visually stunning.
  - On top of accurate syntax highlighting powered by the same engine as VS Code, Expressive Code allows you to annotate code blocks using text markers, diff highlighting, code editor & terminal window frames, and more.
  - All annotations are based on a powerful plugin architecture 

- https://github.com/Sagargupta16/ai-code-translator /202311/ts
  - https://ai-code-translator-delta-six.vercel.app/
  - Use AI to translate code from one language to another

## typewriter/Text Generate Effect

- https://stackblitz.com/edit/react-ts-yiu185
  - [How To Create A Text Generate Effect In React | Algochurn _202209](https://www.algochurn.com/blog/how-to-create-a-text-generate-effect-in-react)
  - https://www.algochurn.com/frontend/text-generate-effect
  - create a Typewriter Effect from scratch using native React and/or Javascript functions
  - 动画打字完undo会撤销所有字
  - 依赖codemirror6、@uiw/react-codemirror

## code-animation

- https://github.com/amasin76/code-motion /202404/ts
  - https://code-motion.vercel.app/
  - animate code changes, and export it as a video
  - An effortless video code diff-animation tool for visualizing code changes
  - 依赖@uiw/react-codemirror、diff、radix-ui、framer-motion、shiki、html2canvas、zustand、react-resizable-panels
  - canvas-based video
  - Export video to webm
  - in-browser code editor
  - App is designed to be offline-first, meaning that it does not rely on any external servers or backdoors
  - We're planning to move to an offline-first approach, which means there will be no servers involved, and all your work will be stored in your local storage.
- https://github.com/SymphonyIceAttack/code-animation /MIT/202405/ts
  - https://www.codeanimations.top/
  - code-animation
  - 依赖@uiw/react-codemirror、shiki-magic-move、zustand、next、dnd-kit

- https://github.com/meowtec/diffani /202307/ts
  - https://diffani.co/
  - Diff code and render to animation video
  - 依赖codemirror6、diff、jsdom、prismjs、zustand、vite

- https://github.com/shikijs/shiki-magic-move /MIT/202405/ts
  - https://shiki-magic-move.netlify.app/
  - Smoothly animated code blocks with Shiki.
  - The package provides framework-agnostic core and renderer and framework wrappers for Vue and React.
  - 依赖diff-match-patch-es、ohash
  - 不依赖codemirror
  - [The Magic in Shiki Magic Move _202403](https://antfu.me/posts/shiki-magic-move)

- https://github.com/uxiew/codemirror-shiki /202407/ts/vue
  - A code editor based on CodeMirror that using Shiki highlighting. 
  - codemirror highlighting using shiki
  - support custom themes and custom languages.

- https://github.com/sergeche/codemirror-movie /MIT/202006/ts/inactive
  - https://docs.emmet.io/
  - A plugin for CodeMirror editor for creating code demos as on Emmet Documentation
  - 依赖codemirror.v5

- https://github.com/Jisuanke/CodeMirror-Record /202112/js/inactive
  - https://codemirror-record.haoranyu.com/
  - https://codemirror-record.haoranyu.com/demo/
  - ⌛️ It is a project for recording and playing back activities in the CodeMirror 5 editor and the surrounding environment
  - version 6.x is not yet supported by this library.

- https://github.com/liqvidjs/plugins /MIT/202309/ts
  - This is a monorepo for a suite of plugins for recording interactive videos. While these were built for Liqvid, they are compatible with other animation libraries.
  - [CodeMirror | Liqvid](https://liqvidjs.org/docs/plugins/codemirror/)
    - @lqv/codemirror package allows you to record and replay CodeMirror typing.
  - https://github.com/ysulyma/rp-codemirror
    - CodeMirror recording/playing for Liqvid
    - This packages has been superseded by @lqv/codemirror. This repository is no longer used.

- https://github.com/wix-incubator/codio /MIT/202101/ts/kotlin/inactive
  - A media format to record and playback the process of programming
  - Codio is a media format for recording the process of programming.
  - The format is composed of code editor operations and audio/video.
  - Create interactive tutorials, code messages and embedded documentation with a media format that turns your IDE to a media player.
  - 🍴 forks
  - https://github.com/rbrisita/codio-sui /202207/ts/inactive
    - A media format for VS Code to record and playback the process of programming.
    - Record VS Code events with an audio commentary and subtitles to play back at a later time.

- products-code-animation
  - [Beautiful code animations - AnimateCode](https://www.animate-code.com/)

- https://github.com/code-hike/examples/tree/main/with-remotion
  - https://x.com/pomber/status/1800108854459715864
  - 不依赖codemirror
  - you can use Remotion's `useFrame` inside any Code Hike annotation to animate most of the examples from the docs
  - wondering if it can also display twoslash annotations, but I don't think remotion supports React Server Components

- https://github.com/pomber/code-surfer /MIT/202003/ts/js/inactive
  - https://codesurfer.pomb.us/
  - Code Surfer adds code highlighting, code zooming, code scrolling, code focusing, code morphing, and fun to MDX Deck slides.
# editors-based-on-codemirror
- https://github.com/inkandswitch/tiny-essay-editor /2023Star/NALic/202406/ts
  - https://tee.inkandswitch.com/
  - simple markdown editor w inline comments, on latest automerge stack
  - a simple collaborative Markdown editor built in React, with inline format preview and inline commenting.
  - built on automerge and automerge-repo for CRDT-based storage and sync. 
  - 依赖automerge2、codemirror6、@lezer/highlight、@radix-ui、tldraw2、@xstate/react、cmdk
  - https://x.com/geoffreylitt/status/1752379702377873894
    - Just gave a talk about Tiny Essay Editor, a collaborative markdown editor we're using at @inkandswitch based on Automerge _202401
    - We wanted a nice local-first editor for writing our research essays, so we built one
    - automerge as core CRDT
    - automerge-repo for networking/storage
    - codemirror for markdown editing, automerge-codemirror for editor integration
    - 💡 For TEE we just store a string for the contents, plus some JSON data for comments.
    - One feature that's *lovely* to build w/ Automerge: attaching comments to text.
    - TEE is local-first, meaning clients are source of truth and there's no central authority.

- https://github.com/tagspaces/tagspaces-common/tree/develop/packages/tagspaces-codemirror /MIT/202312/ts
  - 依赖codemirror6

- https://github.com/rookie-luochao/json-schema-editor /MIT/202406/ts
  - https://json-schema-enhanced-editor.vercel.app/
  - A lightweight json editor based on codemirror, providing smart prompts and verification based on json-schema
  - A json-schema-editor collection, support react、vue framework, will support svelte

- https://github.com/sanity-io/code-input /MIT/202404/ts
  - Sanity input component for code, powered by CodeMirror

- https://github.com/mongodb-js/compass/blob/main/packages/compass-editor/package.json /SSPL/202404/ts
  - Reusable Compass editor component based on codemirror editor, themes, and autocompleters
  - 依赖codemirror6、react

- https://github.com/evinowen/tome /MIT/202406/ts/vue
  - https://tome.evinowen.net/
  - 🌵 git integrated cross-platform markdown editor
  - 依赖codemirror6、marked、nodegit、vue3、@electron/rebuild

- https://github.com/minditor/minditor /MIT/202403/ts
  - https://minditor.dev/
  - A plug-and-play, highly customizable block-based rich text editor. 
  - Supports block/inlineBlock development with any framework, including React/Vue.
  - 未使用react/vue, 🐛 使用自研未开源的视图框架axii
  - 依赖codemirror6、highlight.js、eventemitter3、thememirror、@uppy/xhr-upload
  - 由 Zhenyu Hou 独立开发和维护
  - 不支持拖拽改变block顺序
  - [开源富文本编辑器，支持用 React/Vue 或任何框架开发 Block/InlineBlock。 - V2EX _202403](https://v2ex.com/t/1019749)
    - 保存的是 json 。类似的有 editor.js ，quilljs 。他们好像不支持 inlineBlock ，写复杂插件缺少了一些系统应该提供的 reactive state ，要自己注册各种事件监听。比较麻烦，所以我自己写了这个编辑器。

- https://github.com/wangpin34/wxformat /MIT/202408/ts
  - https://wangpin34.github.io/wxformat/
  - Markdown For Weixin 是一款用于生成兼容微信公众号图文素材内容的 Markdown 编辑器
  - 依赖codemirror6、daisyui、react-hook-form、recoil、remark-rehype
  - 示例是分屏视图，支持同步滚动

- https://github.com/wanglin2/markdown_editor_sync_scroll_demo /202210/js/vue/inactive
  - https://wanglin2.github.io/markdown_editor_sync_scroll_demo/
  - 基于CodeMirror和unified实现的一个能精确同步滚动的Markdown编辑器
  - 依赖codemirror5、vue3、remark-gfm
  - [如何实现一个能精确同步滚动的Markdown编辑器 - 掘金 _202205](https://juejin.cn/post/7100562751596003342)

- https://github.com/mdnice/markdown-nice /GPLv3/202109/js/inactive
  - 支持自定义样式的 Markdown 编辑器
  - 依赖@uiw/react-codemirror.v1、antd.v3
  - [一款开源的Markdown转富文本编辑器的实现原理剖析 - 知乎_202206](https://zhuanlan.zhihu.com/p/526702914)

- https://github.com/gravity-ui/markdown-editor /MIT/202407/ts/设计系统中的一个组件
  - https://preview.gravity-ui.com/md-editor/
  - a powerful tool for working with Markdown, which combines WYSIWYG and Markup modes
  - Support for the basic Markdown and YFM syntax.
  - Extensibility through the use of ProseMirror and CodeMirror engines.
  - 依赖 prosemirror, @diplodoc/transform, react, react-dom, @gravity-ui/uikit, @gravity-ui/components 

- https://github.com/yanthink/pingfan.ts /202204/ts/inactive
  - 基于 codemirror6 的 markdown 编辑器

- https://github.com/lakejs/lake-codemirror /MIT/202404/ts
  - https://lakejs.org/
  - This package provides a CodeMirror configuration for Lake
  - Code block基于codemirror实现

- https://github.com/emberry-org/lemon-editor /GPLv3/202208/ts/inactive
  - a Rich Text Editor build upon Codemirror for the Emberry client.

- https://github.com/retronav/ixora /apache2/202305/ts/inactive
  - a CodeMirror 6 extension pack to make writing Markdown fun and beautiful.
  - Auto link detection
  - https://codeberg.org/retronav/ixora /202305/ts/inactive

- https://github.com/madeyoga/chunchunmaru-mde /MIT/202207/ts/inactive
  - https://madeyoga.github.io/chunchunmaru-mde/
  - Markdown editor based on codemirror 6

- https://github.com/s-zeid/MarkupChisel /BSD/202407/js
  - https://code.s.zeid.me/markdownchisel
  - A minimal Markdown editor based on CodeMirror 6
  - Extra features (can be disabled by using the MarkupChiselBaseView class)

- https://github.com/segphault/codemirror-rich-markdoc /202301/ts/inactive
  - https://markdoc-hybrid-editor.netlify.app/
  - This is a plugin for CodeMirror 6 that adds a hybrid rich-text editing mode for Markdown content. 
  - It applies rich-text styling to Markdown content and hides the Markdown formatting syntax. It only shows the formatting characters for the specific element around the position of the text cursor.
  - This plugin is inspired by HyperMD, a CodeMirror 5 rich Markdown plugin that is no longer actively maintained. This plugin is written from scratch and does not use any existing HyperMD code, but it aims to bring similar functionality to CodeMirror 6.

- https://github.com/fuermosi777/markword /202403/ts
  - A WYSIWYG markdown extension set for Codemirror 6.

- https://github.com/asciidoctor/codemirror-asciidoc /BSD/202112/js/inactive
  - AsciiDoc mode for CodeMirror
  - Usage for CM5 with codemirror-asciidoc@1.x
  - Usage for CM6 with codemirror-asciidoc@2.x

- https://github.com/JinnElements/jinn-codemirror /GPLv3/202403/ts
  - https://jinnelements.github.io/jinn-codemirror/
  - A plain javascript web component based on codemirror. 
  - It adds support for toolbars, XML-specific shortcuts, linting for XML and XQuery, and helpers for the transcription of epigraphic documents.

- https://github.com/dyq086/formula-editor /202303/ts/vue/inactive
  - 基于vue3+codeMirror 6 公式表达式编辑器
- https://github.com/gkf442573575/formula-editor-vue3 /MIT/202406/ts/vue
  - https://gkf442573575.github.io/formula-editor-vue3/
  - Formula Editor for Vue3 Built with vue-codemirror + codemirror6

- https://github.com/amoayun/amoayun-vue-codemirror /202407/ts/vue
  - 其他的属性你们就可以直接参考 vue-codemirror6 了，我就是个二道贩子，哈哈哈，基于 vue-codemirror6 做的一层封装，让大家感觉更方便用一点

- https://github.com/chordbook/editor /GPLv3/202404/ts
  - https://chordbook.github.io/editor/
  - A web-based editor for editing chord sheets in the ChordPro format, built on CodeMirror.
  - ChordPro, a simple text format for the notation of lyrics with chords. Although initially intended for guitarists, it can be used for all kinds of musical purposes.
  - https://github.com/chordbook/codemirror-lang-chordpro

- https://github.com/fsegurai/Electron-React-Markdown-Editor /MIT/202310/ts
  - Electron Markdown Editor based on React
  - 依赖codemirror6、remark-parse、electron-builder

- https://github.com/ahmedsaheed/Leaflet /CC-BY-NC-SA/202305/ts/inactive
  - https://leaflet.saheed.codes/
  - A minimal distractionless markdown editor designed to quickly navigate between multiple `.md` files in a directory and its sub directories.
  - 依赖codemirror6、@uiw/react-codemirror、electron
  - It features a clean mathematical typesetting, chemical equation rendering, code blocks highlighting and writing statistics 

- https://github.com/warmachine028/markdown-editor /MIT/202202/ts/inactive
  - A markdown editor using Electron, ReactJS, Vite, CodeMirror6, and Remark

- https://github.com/voyagegroup/photon-editor /apache2/202304/ts/inactive
  - https://lighthouse-studio.voyage/
  - A full featured markdown editor by Lighthouse Studio
  - 依赖codemirror6、@lezer/highlight

- https://github.com/croxydeveloper/croxy-editor /202309/js/inactive
  - Minimal code editor made with Nextron (Next. JS + Electron) and CodeMirror

- https://github.com/For-0/simple-text-editor /MIT/202307/ts/inactive
  - https://editor.forzero.vocabustudy.org/
  - a text editor for the web
  - 依赖codemirror6、bulma、idb

- https://github.com/frabjous/open-guide-editor /GPLv3/202404/php/js
  - Web based editor based on codemirror for editing markdown and LaTeX files with live updating HTML and PDF previews
  - Highly configurable web-based text editor based on codemirror primarily designed for editing markdown, LaTeX, and html files with live-updating html and pdf previews.
  - it can be used to edit other plain text files as well, including subsidiary files (css, javascript, csv, json, pandoc templates, etc.) and see their effects live-update in their chosen root markdown/LaTeX/html document. 

- https://github.com/geometryzen/stemcstudio-codemirror /MIT/202406/ts
  - Bundle of CodeMirror Editor
  - A wrapper around the CodeMirror editor for use in STEMCstudio.

- https://github.com/riccardoperra/solid-codemirror /MIT/202305/ts/inactive
  - A library of SolidJS primitives to build code editors using CodeMirror 6
  - https://github.com/nimeshnayaju/solid-codemirror /202207/ts/inactive
- https://github.com/acrodata/code-editor /MIT/202405/ts
  - https://acrodata.github.io/code-editor/
  - CodeMirror 6 wrapper for Angular
  - 实现了上下布局的diff视图

- https://github.com/touchifyapp/svelte-codemirror-editor /MIT/202405/ts
  - https://touchifyapp.github.io/svelte-codemirror-editor/
  - A svelte component to create a CodeMirror 6 editor.

- https://github.com/PotatoGroup/code-editor /ISC/202402/ts
  - a JS code editor based on codeMirror6, support code autoCompletion, which can be used with @astii/expression-sandbox
  - 依赖react
  - https://github.com/PotatoGroup/expression-sandbox /202309/ts
    - a simple sandbox for excute js expression

- https://github.com/mdx-editor/editor /MIT/202405/ts/lexical
  - https://mdxeditor.dev/
  - https://mdxeditor.dev/editor/demo
  - open-source React component that allows users to author markdown documents naturally
  - MDXEditor is a rich, client-side component that does not benefit from server-side rendering. To use it in your server components, you should use next/dynamic
  - 依赖lexical、codemirror6、radix-ui、hast、mdast、react-diff-view、react-hook-form
  - diff分屏视图基于codemirror实现，左边不可编辑，右边可编辑，左右都是codemirror的md源码
  - https://github.com/michioxd/mdxeditor-modified /202310/inactive

- gem /10Star/MIT/202205/ts/inactive/代码量少
  - https://github.com/tanishqkancharla/gem
  - https://gem.tanishqkancharla.dev/
  - 只依赖prosemirror，不依赖react
  - Gem (previously called Editor) is a performant and simple plain text editor 
  - The design is very inspired by Paco Coursey's [Writer]().
  - [Gem, a plain-text editor based on prosemirror_202111](https://discuss.prosemirror.net/t/gem-a-plain-text-editor-based-on-prosemirror/4231)
    - I worked on moving to codemirror 6 
    - https://github.com/tanishqkancharla/gem/tree/codemirror /202112/cm6.v0.19

- https://github.com/mcnuttandrew/prong /MIT/202310/ts/inactive
  - https://prong-editor.netlify.app/
  - Prong (PRojectional jsON Gui) is an editor framework for creating bespoke in-browser editors for JSON-based domain-specific languages (such as Vega, Vega-Lite, Tracery, and many others). 
  - These editors allow for things like drag-and-drop interactions, inline-interactive spreadsheets, in-situ recommenders and sparklines, and many more elements that would require significant engineering effort to create otherwise.
  - 依赖codemirror6、react-markdown、jsonc-parser

- https://github.com/festerduck/codemirror-markdown /202406/ts
  - https://composr-omega.vercel.app/
  - Composr is a markdown writer with real-time compiler for the web.

- Starboard Notebook /889Star/MPLv2/202206/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.
  - 编辑器已分离，基于rich-markdown-editor和prosemirror、codemirror6
  - 前端基于lit

- https://github.com/wikimedia/mediawiki-extensions-CodeMirror /GPL/202405/js
  - MediaWiki extension CodeMirror
- https://github.com/bhsd-harry/codemirror-mediawiki /GPLv2/202407/ts
  - https://bhsd-harry.github.io/codemirror-mediawiki/
  - Modified CodeMirror mode based on wikimedia/mediawiki-extensions-CodeMirror
  - The goal is to support a standalone integration between CodeMirror and Wikitext, without the need for a MediaWiki environment

- https://github.com/lhlyu/pure-editor /MIT/202302/ts/inactive
  - a pure editor developed using codemirror6

- https://github.com/RaspberryPiFoundation/editor-ui /apache2/202405/js
  - https://editor.raspberrypi.org/
  - Code Editor frontend
  - https://github.com/RaspberryPiFoundation/editor-api /AGPLv3/202405/ruby/python
    - https://editor.raspberrypi.org/
    - Code Editor backend

- https://github.com/phcode-dev/phoenix /1.3kStar/AGPLv3/202405/js
  - https://phcode.dev/
  - Phoenix is a modern open-source Code Editor for the web, built for the browser
  - Extension support maintaining full compatibility with Brackets extensions (except brackets-node extensions).
  - Adobe 公司开发过一个代码编辑器 Bracket，现在将其做成了 Web 版，重新命名为 Phoenix，可以当作线上 IDE 使用。
  - 依赖codemirror5、@floating-ui/dom、file-saver、marked、mustache
  - Support for pluggable remote back-ends.
  - Phoenix core will work from a static web server.
- https://github.com/adobe/brackets /MIT/202003/js/archived
  - http://brackets.io/
  - a modern open-source code editor for HTML, CSS and JavaScript that's built in HTML, CSS and JavaScript.
  - [Notes on CodeMirror · adobe/brackets Wiki](https://github.com/adobe/brackets/wiki/Notes-on-CodeMirror)
    - Brackets uses a fork of CodeMirror as a submodule.
# collab
- https://github.com/BjornTheProgrammer/react-codemirror-collab-sockets /MIT/202306/ts/inactive
  - An example of a react-codemirror implementation of the codemirror collab package, with cursor and multiple document examples.
  - 依赖codemirror6、@uiw/react-codemirror
  - 未使用ot和crdt

- https://github.com/Princegupta101/Live-Code-Share /202403/js
  - https://live-code-share.vercel.app/
  - a collaborative, real-time code editor where users can seamlessly code together. 
  - 依赖@uiw/react-codemirror、react-split、socket.io-client
  - It provides a platform for multiple users to enter a room, share a unique room ID, and collaborate on code simultaneously.

- https://github.com/codemirror/collab /MIT/202309/ts
  - Collaborative editing for the CodeMirror code editor

- https://github.com/JohnnyAir/codemirror-collab-extension /202401/ts
  - Real-time collaboration plugin for CodeMirror 6
  - 依赖@codemirror/collab

- https://github.com/akashahmad/codemirror-collab-example-react /202406/ts
  - https://codemirror-collab-example-react.vercel.app/
  - React + TypeScript + Vite
  - 依赖@codemirror/collab

- https://github.com/MINERVA-MD/minerva /GPLv3/202302/ts/vue/inactive
  - Minerva is a simple, performant, and hackable Markdown editor that provides seamless GitHub integration and real-time collaboration.
  - 依赖codemirror6、@headlessui/vue、vue3
  - https://github.com/MINERVA-MD/minerva-core
  - https://github.com/MINERVA-MD/minerva-collab /GPLv3/202204/ts/inactive
    - 🔀 A socket server using the codemirror 6 collab library, allowing for real-time collaborative document editing.

- https://www.npmjs.com/package/collaborative-codemirror /202312/crdt
  - Makes a plain Codemirror editor instance collaborative by binding it to a JSON CRDT document str node. 
  - This allows multiple users to edit the same document `json-joy` JSON CRDT document concurrently through the Codemirror editor.
  - https://www.npmjs.com/package/collaborative-editor
    - This package provides bindings a generic implementation for binding any plain text editor to a JSON CRDT string.

- https://github.com/yjs/y-codemirror.next /MIT/202403/js
  - https://demos.yjs.dev/codemirror/codemirror.html
  - Collaborative extensions for CodeMirror6
  - This binding binds a `Y.Text` to a CodeMirror editor.
  - Awareness: Render remote selection ranges and cursors - as a separate plugin
  - Shared Undo/Redo (each client has its own undo-/redo-history) - as a separate plugin

- https://github.com/lirsacc/siren-chorus /202311/ts/inactive
  - Multiplayer mermaid diagram editor
  - WebRTC based collaborative MermaidJS editor.
  - 依赖codemirror6、mermaid、y-codemirror.next

- https://github.com/MyoniM/mirror-code-react-js /202210/js/inactive
  - https://mirror-code.web.app/
  - A collaborative Web IDE with Code Mirror's CRDT Server and Socket.io
  - 依赖codemirror6、y-codemirror.next
  - https://github.com/MyoniM/mirror-code-backend /202208/js
    - 基于express、socket.io

- https://github.com/cpinitiative/ide /MPLv2/202406/ts/js
  - https://ide.usaco.guide/
  - A realtime collaborative IDE with code execution, intellisense, mobile support, and built-in USACO submissions.
  - Designed primarily for Competitive Programming and USACO, with mobile support for coding on the go.
  - 依赖@uiw/react-codemirror、y-codemirror.next、firebase、monaco-editor、next、
  - https://github.com/cpinitiative/ide-yjs
  - https://github.com/cpinitiative/ide-lsp

- https://github.com/ekzhang/rushlight /MIT/202306/ts/inactive  
  - https://github.com/ekzhang/cm-collab /ts
  - ✏️ A tiny collaborative Markdown editor based on CodeMirror, communicating with a minimal server and database.
  - Make collaborative code editors that run on your own infrastructure: just Redis and a database.
  - Supports multiple real-time documents, with live cursors. 
  - 🔀 Based on CodeMirror 6 and operational transformation, so all changes are resolved by server code.
  - The backend is stateless, and you can bring your own transport; even a single HTTP handler is enough.
  - Unlike most toy examples, Rushlight supports persistence in any durable database you choose. Real-time updates are replicated in-memory by Redis, with automatic log compaction.

- https://github.com/vizhub-core/codemirror-ot /MIT/202403/js
  - Real-time collaboration plugin for CodeMirror 6.
  - Overhauled in May 2022 to work with the latest CodeMirror 6 APIs and JSON1. A fully functioning collaborative editor that leverages this library can be found in VZCode.
  - At its core this library is a translator between Operational Transformation and CodeMirror 6. This is one piece of the puzzle for enabling real-time collaboration on text documents using CodeMirror and ShareDB.
  - 依赖sharedb、ot-json1

- https://github.com/qwikcollab/qwikcollab /202306/ts/inactive
  - https://qwikcollab.netlify.app/
  - open source collaborative code editor you have been searching for
  - Qwikcollab uses operational transformation for managing document versions when multiple people edit it, it uses codemirror which is an extensible code editor package and also helps in merging changes from different clients. The changes are transferred using websockets.

- https://github.com/hussamkhatib/Real-time-collaborative-sandpack /MIT/202207/js
  - https://real-time-collaborative-sandpack.vercel.app/
  - This example shows how you can use Sandpack and firepad-x to build a collbrative text editor.
  - [[Feature Request] Multi-user support · Issue · codesandbox/sandpack _202203](https://github.com/codesandbox/sandpack/issues/405)
  - I was able to get it working with firepad. It gives live text updates, and cursor positions, and I am able to see the changes in the iframe as well.

- https://github.com/biomousavi/live-code /202312/ts/vue/inactive
  - https://code.biomousavi.com/
  - A real-time collaborative code editor in your browser.
  - 依赖codemirror6、socket.io-client、vue3

- https://github.com/YingshanDeng/SharedPen /MIT/201802/js/inactive
  - 包含了otjs源码和针对SharedPen的修改版，转换成了es6 class版
  - 关于扩展 ot.js 支持富文本属性，可以参考文件 TextAction.js 和 TextOperation.js
  - A (web-based) rich-text real-time collaborative editor using CodeMirror5 and ot.js
  - [SharedPen 之 Operational Transformation](http://objcer.com/2018/03/05/SharePen-Operational-Transformation/)
  - https://github.com/YingshanDeng/ot.js-demo

- https://github.com/zerosnake0/codeshare /202006/js/inactive
  - Code sharing using ShareDB + CodeMirror5

- https://github.com/Rishabh-malhotraa/caucus /MIT/202405/ts
  - https://caucus.rishabhmalhotra.in/
  - Realtime Collaborate Editor with Embedded Compiler
  - 类似协作codepen
  - Built With React Material UI yjs Written in TypeScript
  - 依赖knex、pg、yjs、codemirror5、mui.v4

- https://github.com/automerge/automerge-codemirror /MIT/202404/ts
  - This plugin adds collaborative editing to codemirror using `automerge-repo`.
- https://github.com/aslakhellesoy/automerge-codemirror /MIT/202005/ts
  - brings collaborative editing to CodeMirror by linking it to an `Automerge.Text` object
  - 依赖codemirror5、automerge.v0.14

- https://github.com/anurag270102/Code-Editor /202404/js
  - a powerful and intuitive code editor application designed for seamless real-time collaboration among developers. 
  - real-time collaborative code editor built using React, Node.js, Express, and Socket.io. 
  - 依赖codemirror5、socket.io-client

- https://github.com/abhishekashyap/codeRigade /MIT/202005/js/inactive
  - https://coderigade.netlify.app/
  - Realtime collaborative code-editor
  - 依赖codemirror5、socket.io-client

- https://github.com/Cosmin-Mare/y-codemirror-react /202403/js
  - https://y-codemirror-react-three.vercel.app/
  - 依赖codemirror5、y-codemirror2

- https://github.com/ROHITvisuals/Frontend-CodeEditor-Collaboration /202401/js
  - Real time Collaboration with CodeEditor (CodeMirror) and WebSocket.
  - 依赖codemirror5
  - https://github.com/ROHITvisuals/Backend-CodeEditor-Collaboration /js

- https://github.com/rockharshitmaurya/OneCode /202307/js/inactive
  - https://onecode.onrender.com/
  - real-time collaboration app that allows multiple users to code together in a live environment. 
  - It is built using the MERN (MongoDB, Express.js, React, Node.js) stack.
  - 依赖codemirror5、react
- https://github.com/soumya-maheshwari/CollaboWrite /202404/js
  - https://collabowr1te.vercel.app/
  - a real-time code editor that allows multiple users to collaborate and edit code together.

- https://github.com/AbdallaIB/collaborative-ide /MIT/202306/ts/inactive
  - https://collaborative-ide.netlify.app/
  - Collaborative platform to code with your friends in real-time
  - Login & sign up via JWT authentication + Demo account
  - 依赖codemirror5、yjs

- https://github.com/chakri68/codeCollab /202306/js
  - A simple code editor to share code and collab with other developers

- https://github.com/lucafabbian/firepad /202208/js/inactive
  - 🔥 Firepad is an open-source library for adding collaborative capabilities into text and code editors. Firepad uses Google Firebase as a backend, so it requires no server-side code. It supports out of the box popular web editors such as Codemirror, Ace and Monaco.
  - new adapter to add compatibility with Codemirror6, arguably one of the best web editor out there. Check the demo here
  - https://github.com/lucafabbian/codemirror6-firepad-demo /202206/js
    - Demo of Codemirror6 using the Google Firebase service to achieve real time collaboration with minimal setup.

- https://github.com/interviewstreet/firepad-x /202401/ts
  - We have rewritten all the modules and few extras using TypeScript while enhancing earlier implemented Adapter Pattern to integrate with external modules, such as Database (preferably Firebase) and editors (as of now only Monaco is supported, but PRs are welcomed). 

- https://github.com/jupyter-server/pycrdt /MIT/202312/python/rust
  - https://davidbrochart.github.io/pycrdt
  - https://jupyter-server.github.io/pycrdt
  - CRDTs based on Yrs
  - https://github.com/jupyter-server/pycrdt-websocket /python
    - async WebSocket connector for pycrdt

- https://github.com/TypeFox/open-collaboration-tools /MIT/202406/ts
  - https://www.open-collab.tools/
  - ⚖️ Open Collaboration Tools: live-sharing solution for Eclipse Theia, VS Code and other editors and IDEs
  - A public instance of the collaboration server is available at open-collab.tools.
  - This is how it works: one person starts a collaboration session as host and invites others to join. The IDE extension distributes the contents of the hostʼs workspace and highlights text selections and cursor positions of other participants. 

- https://github.com/codersgyan/realtime-code-editor /202203/js
  - 依赖codemirror5、socket.io

- https://github.com/himanshugoyal77/codeSync-realtime-code-editor /202407/js
  - https://code-sync-realtime-coding.vercel.app/
  - Realtime code collaboration tool with code editor, compiler and realtime cursors
  - 依赖codemirror5, socket.io-client, react

## diff

- https://github.com/acrodata/code-editor /MIT/202405/ts
  - https://acrodata.github.io/code-editor/
  - CodeMirror 6 wrapper for Angular
  - 实现了diff上下视图、✨左右视图，支持高亮变更内容及gutter，支持撤销变更action
  - 支持a2b/b2a正反向计算

- https://github.com/gaelj/BlazorCodeMirror6 /MIT/202407/csharp/ts
  - https://gaelj.github.io/BlazorCodeMirror6/
  - Blazor CodeMirror 6 brings the power of the CodeMirror 6 code editor to Blazor, offering a comprehensive . NET6/7/8 component
  - Markdown editor for Blazor
  - 支持编辑时开启/关闭diff-view，✨ diff视图下accept变更后立即撤销会先回到diff视图
  - 实现了diff上下视图，支持高亮变更及gutter，支持accept/reject变更action
    - 亮变更内容的粒度是字符，但未突出删除字符的样式
  - 支持编辑器中渲染图片
  - markdown编辑体验支持行内切换md代码和预览，类似typora
  - 依赖
  - manual resizing of the editor (similar to html textarea)
  - custom linting
  - allow undo / redo toolbar buttons
  - CSV mode: add column paddings for alignment, navigate columns with tab / shift-tab; 支持markdown-table 📈
  - 支持emoji

- https://github.com/mdx-editor/editor /MIT/202405/ts/lexical
  - https://mdxeditor.dev/
  - https://mdxeditor.dev/editor/demo
  - open-source React component that allows users to author markdown documents naturally
  - MDXEditor is a rich, client-side component that does not benefit from server-side rendering. To use it in your server components, you should use next/dynamic
  - 依赖lexical、codemirror6、radix-ui、hast、mdast、react-diff-view、react-hook-form
  - diff左右分屏视图基于codemirror实现，左边不可编辑，右边可编辑，左右都是codemirror的md源码

- https://github.com/codemirror/merge /MIT/202403/ts
  - https://codemirror.net/try/?example=Merge%20View
  - Merge view for CodeMirror
  - 左边旧代码可编辑，右边新代码不可编辑，与vscode相反

- https://codepen.io/GwapongProgrammer/pen/yLXqWMK
  - 依赖codemirror6

- https://github.com/ngalaiko/codemirror-lang-diff /MIT/202304/ts/inactive
  - This is a CodeMirror 6 extension that adds support for `.diff` files syntax.

- https://github.com/codedownio/codemirror-compose-change /MIT/202306/ts/inactive
  - Compose two sequential CodeMirror changes

- https://github.com/MrWangJustToDo/git-diff-view /MIT/202404/ts
  - https://mrwangjusttodo.github.io/git-diff-view/
  - 🆚️ A Diff View component for React/Vue, just like Github
  - core只依赖lowlight, 不依赖codemirror
  - https://github.com/wooorm/lowlight /MIT/202310/js
    - Virtual syntax highlighting for virtual DOMs and non-HTML things
    - This package uses `highlight.js` for syntax highlighting and outputs objects (ASTs) instead of a string of HTML.
    - This package is useful when you want to perform syntax highlighting in a place where serialized HTML wouldn’t work or wouldn’t work well. 
    - You can use the similar `refractor` if you want to use `Prism` grammars instead. 
    - If you’re looking for a really good (but rather heavy) alternative, use `starry-night`.

- https://github.com/BearToCode/mismerge /MIT/202402/ts/svelte
  - https://beartocode.github.io/mismerge/
  - Mismerge is a modern two-way and one-way merge editor for the web, built with Svelte
  - It is also available in React and Vue.
  - 示例是基于textarea实现合并代码

## lint

- https://github.com/KELs7/contracting-linting-codemirror6 /202405/ts
  - Demo: Contracting Linting in Codemirror6
  - Only few linting rules have been implemented
  - 示例lint python2代码
# extensions
- https://github.com/val-town/codemirror-ts /ISC/202405/ts
  - https://val-town.github.io/codemirror-ts/
  - a set of extensions for CodeMirror 6 that add support for TypeScript
  - lint, hover, and autocomplete extensions for CodeMirror + TypeScript
  - Hover hints for types 
  - Autocomplete 
  - Diagnostics (lints, in CodeMirror's terminology)
  - Running typescript in a web worker for perf
  - [Go to definition · val-town/codemirror-ts _202311](https://github.com/val-town/codemirror-ts/issues/8)
    - This module currently uses TypeScript, but not the extra language server. It'd probably use the language server if this adopted more of a client-server architecture, or maybe it should in general, but for now, it's integrating with TypeScript, and we'll need to figure out what's under the hood of the LSP adapter's implementation.

- https://github.com/yeliex/codemirror-extensions /MIT/202403/ts
  - https://cm.yeliex.dev/
  - codemirror extensions includes toolbar, helper, image-upload, event-emitter
  - codemirror-final-newline
  - codemirror-markdown-commands
  - codemirror-markdown-image
  - codemirror-toolbar

- https://github.com/overleaf/codemirror-tree-view /MIT/202311/ts
  - A CodeMirror 6 extension providing an interactive view of a document's syntax tree
  - ⛏ 更偏向于作为codemirror的devtools
  - https://github.com/overleaf/codemirror-autocomplete
  - https://github.com/overleaf/codemirror-search

- https://github.com/ShadowWolf308/codemirror-indent-wrapped-line /MIT/202406/ts
  - An extension to CodeMirror to indent wrapped newlines

- https://github.com/jmkng/sen /MIT/202310/ts
  - Simple, reusable CodeMirror (v6+) extensions.
  - The extensions are exported as functions that return an array of extensions that you can apply to your view.

- https://github.com/eivmosn/plugin-mirror /202311/ts
  - codemirror plugins

- https://github.com/replit/codemirror-vscode-keymap /202212/ts/inactive
  - Ports VSCode's keyboard shortcuts to CodeMirror 6.

- https://github.com/replit/codemirror-indentation-markers /MIT/202403/ts
  - extension that renders indentation markers using a heuristic similar to what other popular editors, like Ace and Monaco, use.

- https://github.com/fauzi9331/codemirror-wrapped-line-indent /MIT/202403/ts
  - An extension for CodeMirror that adds indentation for wrapped lines.

- https://github.com/replit/Codemirror-CSS-color-picker /202310/ts
  - https://replit.com/@util/Codemirror-CSS-color-picker
  - extension that adds a color picker input next to CSS color values.

- https://github.com/saminzadeh/codemirror-extension-inline-suggestion /MIT/202402/ts
  - A CodeMirror extension to display inline suggestions
  - https://github.com/rizerphe/codemirror-companion-extension

- https://github.com/emmetio/codemirror6-plugin /202404/ts/Emmet
  - CodeMirror 6 extension that adds Emmet support to text editor.
  - Extension development is sponsored by Replit

- https://github.com/val-town/codemirror-continue /202401/ts
  - https://val-town.github.io/codemirror-continue/
  - Continue TypeScript/JavaScript block comments in CodeMirror

- https://github.com/luizzappa/codemirror-app-spreadsheet /202304/ts/inactive
  - https://luizzappa.github.io/codemirror-app-spreadsheet/
  - a demo implementation of the CodeMirror spreadsheet language package.
  - https://github.com/luizzappa/codemirror-lang-spreadsheet /MIT/202304/ts
    - Spreadsheet language support for CodeMirror

- https://github.com/AlbertArakelyan/collaborative-markdown-editor-example /MIT/202405/ts
  - Collaborative Markdown Editor built on modern and simple web technologies with markdown editing libraries integrations

- https://github.com/personalizedrefrigerator/joplin-plugin-extra-editor-settings /MIT/202407/ts
  - This plugin exposes several CodeMirror 6 settings, including line numbers and code folding.

- https://github.com/andrebnassis/codemirror-readonly-ranges /202311/ts
  - https://andrebnassis.github.io/codemirror-readonly-ranges
  - Codemirror extension for read-only ranges
  - This library aims to help you dealing with read-only ranges on CodeMirror 6.

- https://github.com/modderme123/codemirror-extension-typescript /202312/ts/inactive
  - https://typescript-codemirror.netlify.app/
  - A codemirror extension providing useful features for typescript, such as a language server with autocomplete and error reporting

- https://github.com/dimfeld/codemirror-json5 /MIT/202306/ts
  - This package implements JSON5 support for Codemirror 6.

- https://github.com/josdejong/mathjs-codemirror /202402/ts
  - https://josdejong.github.io/mathjs-codemirror/
  - A mathjs editor in CodeMirror

- https://github.com/JerryI/codemirror6-mathematica-sugar /202310/js/archived
  - mathematica | Wolfram-language mode for CM6 with advanced syntax sugar
  - This is basically a fork of a legacy Mathematica tokenizer

- https://github.com/xQwexx/codemirror-beautify /202312/ts
  - This codemirror 6 extension add js html and css formatting support.

- https://github.com/oopscraft/duice-plugin /202404/ts
  - https://duice-plugin.oopscraft.org/
  - DUICE (Data oriented UI Component Element) Plugins

- https://github.com/A99US/CM6-TextToLink /MIT/202305/js/inactive
  - https://a99us.github.io/CM6-Browser-Wrapper/
  - an extension for CodeMirror 6 to add a clickable link icon next to a valid URL.
  - SVG Icon and CSS style are from @uiwjs/react-codemirror/hyper-link

- https://github.com/eriknewland/rainbowbrackets /202304/js/inactive
  - https://codepengpt.netlify.app/
  - This is a working attempt at a rainbowBracket extension for CodeMirror6.
# utils
- https://github.com/lume/code-mirror-el /MIT/202405/ts
  - https://codepen.io/trusktr/pen/poGZYOy?editors=1000
  - A customizeable `<code-mirror>` element that makes a code editor powered by CodeMirror 

- https://github.com/justinfagnani/codemirror-elements /MIT/202308/ts/inactive
  - A set of HTML custom elements for editing source code with CodeMirror.

- https://github.com/flawiddsouza/code-mirror-custom-element /MIT/202312/js
  - https://flawiddsouza.github.io/code-mirror-custom-element/
  - CodeMirror 6 as a custom element (web component)
  - https://github.com/markwylde/codemirror-element

- https://github.com/0xdevalias/userscripts/tree/main/userscripts/github-gist-codemirror-resizer
  - Makes the CodeMirror editor resizable when creating/editing a gist on GitHub

- https://github.com/JackieScorpio/convert-json-to-ts /MIT/202404/ts
  - use codemirror and vscode webview to achieve a vscode extension
  - Convert Json to Typescript

- https://github.com/A99US/codemirror-6-snippetbuilder /MIT/202304/js
  - This is a function for CodeMirror 6 to convert a standard array of snippet (like this one) and turn it into snippet array that is ready to use in CodeMirror 6 extension.

- https://github.com/PuruVJ/neocodemirror /202407/ts/svelte
  - Aims to provide Codemirror 6 as an easy to use codemirror action.
  - https://x.com/puruvjdev/status/1780560310547436002
    - Anytime you change documentId, it stores the state in a map, and when the documentID changes back to the one stored, we apply the history

- https://github.com/jsonnext/codemirror-json-schema /MIT/202406/ts
  - https://codemirror-json-schema.netlify.app/
  - A JSONSchema enabled mode for codemirror 6, for json4 and json5, inspired by monaco-json
  - Codemirror 6 extensions that provide full JSON Schema support for @codemirror/lang-json & codemirror-json5 language modes
- https://github.com/acao/codemirror-json-schema /MIT/202404/ts
  - Codemirror 6 extensions that provide full JSON Schema support for @codemirror/lang-json & codemirror-json5 language modes
- https://github.com/acao/json-schema-workbench /202311/ts
  - https://json-schema-workbench.vercel.app/
  - A reference implementation for codemirror-json-schema
  - A Next.js 13 template for building apps with Radix UI and Tailwind CSS.

- https://github.com/thetrevorharmon/zephyr-demo /202402/ts
  - https://zephyr-demo.netlify.app/
  - CodeMirror 6 + ANTLR
  - [Connecting ANTLR to CodeMirror 6: Building a Language Server _202402](https://thetrevorharmon.com/blog/connecting-antlr-to-codemirror-6-building-a-language-server/)
    - I spent *a lot* of time trying to get operability between CM6 and ANTLR as part of my work on the ShopifyQL code editor (which I've written about before). I didn't have any guide for how to do any of this before working on it, so my hope is that these help somebody
- https://github.com/RuslanZh/codemirror-antlr4 /202208/ts/inactive
  - This project shows example of integration Antlr 4 grammar tool with Codemirror editor.

- https://github.com/Gk0Wk/TW5-CodeMirror-Enhanced /MIT/202305/ts/inactive
  - https://gk0wk.github.io/TW5-CodeMirror-Enhanced/
  - An enhanced for CodeMirror framework in TiddlyWiki, including TW5 highlight, WikiLink auto-completion, expandable hint, snippets, etc.
  - 为 TiddlyWiki5 的 CodeMirror 编辑器实现一个灵活而丰富的扩展框架，包括 TiddlyWiki5(text/vnd.tiddlywiki)语法高亮、Wiki 链接自动补全、可点击链接、Tiddler 预览等功能。更多功能(语法树、语法补全、所见即所得模式、快捷模板输入等)正在开发中。本框架是开源框架，欢迎任何人加入开发，框架文档正在编写中。
  - https://github.com/BurningTreeC/tiddlywiki-codemirror-6 /202403/js
    - https://burningtreec.github.io/tiddlywiki-codemirror-6/
    - The plugin adds the CodeMirror 6 editor to TiddlyWiki
  - https://github.com/oeyoews/tiddlywiki-codemirror6 /MIT/202407/ts
    - The tiddlywiki-codemirror-6 plugin has entered maintenance status

- https://github.com/BrianHung/tldraw-yjs /202402/ts
  - https://canvas-yjs.vercel.app/
  - An example of using tldraw together with yjs with codemirror and prosemirror.

- https://github.com/Nexucis/kvsearch /MIT/202208/ts/inactive
  - This lib provides a plugin to codemirror (v6) in order to have autocompletion and linter that will help to write query compatible with @nexucis/kvsearch

- https://github.com/google/codemirror.dart /BSD/202403/dart
  - A Dart wrapper around the CodeMirror text editor

- https://github.com/NewDefectus/defasm /ISC/202404/js
  - DefAssembler is an incremental x86-64 assembler written in JavaScript. 
  - CodeMirror 6 extension utilizing DefAssembler
  - A CodeMirror 6 extension that highlights Assembly code and assembles it incrementally.

- https://github.com/gratico/codemirror /202307/ts
  - Codemirror packaged as an application for gratico platform

- https://github.com/mindofmatthew/text.management /GPLv3/202404/ts
  - Experimental Live Code Editor
  - In its initial form, this is an editor for the Tidal language. It requires Tidal to be installed independently.
  - https://github.com/mindofmatthew/text.management/tree/main/packages/codemirror/evaluate
    - CodeMirror 6 extension for enabling lines of code to be evaluated

- https://github.com/Monkatraz/cm-tarnation /MPLv2/202207/ts/inactive
  - 🧮 An alternative parser for CodeMirror 6
  - Tarnation is not line-based. It is capable of reusing both previous and ahead data when parsing, making it fully incremental
  - Tarnation can do things that Lezer (the parser you'd usually use for CodeMirror) can't. For example, Tarnation can parse something like Markdown, and other weird esoteric markup/formatting languages.

- https://github.com/realdennis/md2pdf /MIT/202407/js
  - https://realdennis.github.io/md2pdf/
  - https://md2pdf.netlify.com/
  - Offline markdown to pdf, choose -> edit -> transform

## lsp

- https://github.com/coder0107git/codemirror-web-workers-lsp-demo /202404/ts
  - https://codemirror-web-workers-lsp-demo.coder0107git.v6.rocks/
  - Demo of using a Web Worker LSP in CodeMirror 6
  - https://gitlab.com/aedge/codemirror-web-workers-lsp-demo

- https://github.com/FurqanSoftware/codemirror-languageserver /161Star/BSD/202212/ts/inactive
  - Language Server integration for CodeMirror 6
  - This plugin enables code completion, hover tooltips, and linter functionality by connecting a CodeMirror 6 editor with a language server over WebSocket.
  - [Using Language Servers with CodeMirror 6 _202103](https://hjr265.me/blog/codemirror-lsp/)
  - 🍴 forks
  - https://github.com/databutton/codemirror-languageserver /202309/ts

- https://github.com/qualified/lsps /MIT/202206/ts/inactive
  - Use Language Servers with in-browser editors. 
  - Monorepo of editor agnostic packages and CodeMirror client.

- https://github.com/marc2332/lsp-codemirror /ISC/202008/ts/inactive
  - LSP integration for CodeMirror

- https://github.com/okikio/codemirror/tree/lsp-dev /MIT/202110/ts/inactive
  - https://okikio-codemirror.netlify.app/
  - A minor test of Codemirror
  - https://x.com/SergeiChestakov/status/1486025274240090114
    - I now have a ~relatively~ functional lsp adapter for Codemirror 6, you may want to take a look. The main limitation is recreating a monaco esque environment for Codemirror, e.g. autocomplete doesn't work the same way on Codemirror that it did on Monaco

- https://github.com/SilasMarvin/lsp-ai /MIT/202406/rust
  - LSP-AI is an open source language server that serves as a backend for performing completion with large language models and soon other AI powered functionality. 
  - Because it is a language server, it works with any editor that has LSP support.
  - LSP-AI can work as an alternative to Github Copilot.
  - The goal of LSP-AI is to assist and empower software engineers by integrating with the tools they already know and love not replace software engineers.

- https://github.com/craftzdog/react-codemirror-runmode /MIT/202405/ts
  - Syntax highlighting for react, utilizing CodeMirror's parser
  - Syntax highlighter for React, using CodeMirror 6. It automatically loads the language metadata and dynamically loads language parser modules based on the specified language.

## utils-lang

- https://github.com/mattmundell/codemirror-lang-git-log /MIT/202406/ts
  - https://git.sr.ht/~mattmundell/codemirror-lang-git-log
  - CodeMirror language for 'git log' output

- https://github.com/inspirnathan/codemirror-lang-mermaid /MIT/202309/ts
  - Mermaid language support for CodeMirror 6
  - This package implements Mermaid language support for the CodeMirror code editor. 
  - Get syntax highlighting for Mermaid diagrams

- https://github.com/eliasfeijo/codemirror-lang-ejs /MIT/202302/ts
  - EJS templating language implementation for CodeMirror v6

- https://github.com/n8n-io/codemirror-lang-n8n /MIT/202404/ts
  - n8n expression language support for CodeMirror 6

- https://github.com/neo4j/cypher-editor /apache2/202404/js
  - Codemirror editor for Cypher, with syntax awareness and auto-completion

- https://github.com/JerryI/wljs-editor /202407/js
  - https://jerryi.github.io/wljs-editor/
  - A cell editor & supporting packages for wolfram-frontend project written in JS with Codemirror 6. Support mathematical expressions rendered inline, Mathematica's boxes and many more...
  - This is a core component of Wolfram JS Frontend project
  - https://github.com/JerryI/wolfram-js-frontend
    - Dynamic Notebook Environment for Wolfram Language written in Javascript

- [CodeMirror extension to detect and fix missing JSX Pragma](https://gist.github.com/tmcw/fefe8b5c0a63b51bc8a303c8a3553fac)
  - detects the lack of a pragma and the presence of JSX syntax, by using CodeMirror's existing syntax tree
# code-playgrounds
- https://github.com/mdn/bob /MIT/202407/ts
  - ✨ Builder of Bits aka The MDN Web Docs interactive examples, example builder
  - [Migrate to CodeMirror v6 _202208](https://github.com/mdn/bob/issues/851)
  - https://developer.mozilla.org/en-US/play
  - [Introducing the MDN Playground: Bring your code to life! | MDN Blog _202306](https://developer.mozilla.org/en-US/blog/introducing-the-mdn-playground/)
  - features: Instant prototyping, Live interaction, collaborative
  - We decided to go with CodeMirror. We considered Monaco, but decided for a more lightweight approach

- react-runner /382Star/MIT/202406/ts/inactive
  - https://github.com/nihgwu/react-runner
  - https://nihgwu.github.io/react-runner/
  - https://react-runner.vercel.app/
  - Run your React code on the go
  - 被Autodesk/react-base-table用来展示示例
  - react-runner依赖sucrase(alternative to Babel)、react
  - react-live-runner依赖react-simple-code-editor、react-runner
  - react-runner-codemirror依赖codemirror6、react、prism-react-renderer
    - React wrapper of CodeMirror6 for React code editing, Live preview powered byReact Runner
  - react-runner is inspired by `react-live` heavily, I love it, but I love arrow functions for event handlers instead of bind them manually 
  - use Sucrase instead of Bublé to transpile the code.
  - If you are using react-live and want a smooth transition, react-live-runner is there for you which provide the identical way
  - Server Side Rendering
  - You can even build your own async runner to support dynamic imports, try Play React
  - [[Feature]: Add React 18 support for `react-live-runner` _202205](https://github.com/nihgwu/react-runner/issues/123)
    - I've tried other solutions, like use-editable, but I'd say react-simple-code-editor provides the best UX and less bugs, I don't think there is anything preventing it's been used with React 18, just ignore the warnings for now, and react-live-runner aims to provide a smooth transition from react-live, 
    - if you want to use other code editors, you are free to use theme with react-runner, like CodeMirror, CodeJar or even Monaco, I don't have the bandwidth to maintain another editor which is complicated regarding multi browsers support

- react-live /4.1kStar/MIT/202402/ts/inactive
  - https://github.com/FormidableLabs/react-live
  - https://commerce.nearform.com/open-source/react-live/
  - https://react-live.netlify.com/
  - render React components with editable source code and live preview.
  - 依赖use-editable、sucrase、prism-react-renderer
  - 只支持直接编辑源码, 不支持类似storybook的knobs
  - https://github.com/FormidableLabs/use-editable
    - small React hook to turn elements into fully renderable & editable content surfaces, like code editors, using contenteditable (and magic)
  - https://github.com/FormidableLabs/component-playground
    - A component for rendering React components with editable source and live preview
  - [codemirror withlive](https://github.com/FormidableLabs/react-live/issues/210)
    - 202210: if you are using the standard LiveProvider, you can use `@uiw/react-codemirror` as a drop in replacement for LiveEditor

- https://github.com/reddit/play /BSD/202406/ts/lit
  - https://developers.reddit.com/play
  - A little playground for building apps on Reddit
  - We open-sourced a little playground for building apps on Reddit. 
  - It's all Lit web components, CodeMirror, CSS, TypeScript, and esbuild
  - 依赖codemirror6、devvit/ui-renderer、lit3

- https://github.com/abhirampai/CodeBoost /MIT/202304/js/inactive
  - https://codeboost.vercel.app/
  - CodeBoost is a code runner that allows you to refactor and run your code in one convenient location.
  - [CodeBoost _202303](https://medium.com/geekculture/codeboost-where-you-can-run-and-refactor-your-code-abe449cc1063)
    - run code using Judge0CE API

- https://github.com/solidjs-community/solid-playground-editor-cm /MIT/202302/ts/inactive
  - https://solidjs-community.github.io/solid-playground-editor-cm/
  - codemirror6-based editor with typescript support for the solid.js playground

- https://github.com/munshkr/flok /GPLv3/202404/ts
  - https://flok.cc/
  - Web-based P2P collaborative editor for live coding sounds and images
  - Similar to Etherpad, but focused on code evaluation for livecoding.
  - REPL plugins: allows user to locally evaluate code from interpreters (like Haskell, Ruby, Python, etc.)
  - Web Plugins, for languages embedded in editor
  - Use CodeMirror 6
  - Use Yjs for collaborative editor
  - nice to have Import external JS libraries dynamically, instead of bundling them wi  th Flok
  - `@flok-editor/cm-eval`: CodeMirror 6 extension for code evaluation

- https://github.com/anindya-dey/edtr /MIT/202207/ts
  - https://edtr.vercel.app/
  - An online code-editor
  - 依赖@uiw/react-codemirror、next

- https://github.com/badass-courses/course-builder /MIT/202406/ts
  - https://www.coursebuilder.dev/
  - experimental platform for building Badass Courses
  - Course Builder is a real-time multiplayer CMS for building and deploying the opinionated data structures of developer education products
  - [feat: codemirror + partykit markdown editor _202312](https://github.com/badass-courses/course-builder/pull/35)
    - used this Liveblocks guide to get this running with partykit.
  - [feat: collaborative codemirror editor _202401](https://github.com/badass-courses/course-builder/issues/54)
    - We've set up the basics for the collaborative editor, but the results are mixed and kind of janky where the text sometimes doubles up and it doesn't feel right in terms of the syncing between the CMS (Sanity) and the Partykit connection.

- https://github.com/leon-kfd/OnlineCodeEditor /202311/ts/vue
  - An online code Editor like CodePen, built by Vue3.

- https://github.com/live-codes/livecodes /MIT/202407/ts
  - https://livecodes.io/
  - A feature-rich, open-source, client-side code playground for React, Vue, Svelte, Solid, Typescript, Python, Go, Ruby, PHP and 80+ languages/frameworks.
  - 依赖codemirror6、monaco、codejar、codejar、yjs
  - Powerful SDK (available for vanilla JavaScript, TypeScript, React, Vue and Svelte)
  - https://x.com/hatem_hosny_/status/1753930554540499064
    - Check this where I dynamically select the editor and load it (e.g. on desktop -> monaco, on mobile -> codemirror, user preference, etc.)
    - Also unified the interface of loading and communicating with the editor
  - [Why Another Playground? | LiveCodes](https://livecodes.io/docs/why/)
    - There are great products like CodePen, JSFiddle, JS Bin, CodeSandbox, Replit and many others, which LiveCodes does not aim to replace or compete with.
    - On the contrary, it aims to integrate with as many of these services as their APIs allow.
    - All processing and code transformations run in the browser on the client-side.
    - The LiveCodes app (standalone or self-hosted) can be embedded in any web page.

- https://github.com/oxc-project/oxc/tree/main/website /202306/js/inactive
  - https://oxc-project.github.io/oxc/playground
  - Oxc has a playground now. Need more knobs but it works.
  - I built it with CodeMirror in plain JavaScript without any frameworks
  - https://x.com/TheLarkInn/status/1667266703745757184
    - Awesome now do the “click on AST on right to highlight code on left” like astexplorer does!
    - https://ast-grep.github.io/playground.html

- https://github.com/lucademenego99/icp-bundle /apache2/202307/svelte
  - Interactive Code Playgrounds Bundle is a plugin for embedding interactive code playgrounds in HTML pages.
  - The editor used in these playgrounds is CodeMirror6, an in-browser editor distributed as a collection of modules.
  - The project is based on Svelte, a tool for building web applications. The actual build step is performed through Vite and the gulp tool.
  - The most computationally expensive tasks the bundle does are performed using Web Workers and SharedWorkers.
  - https://github.com/lucademenego99/icp-slides /202307/html
    - https://lucademenego99.github.io/icp-slides/
    - Slides created with Reveal.js for the Interactive Code Playgrounds project, hosted directly from the repository as a Github Pages website.
  - https://github.com/lucademenego99/icp-editor /MIT/202307/ts/svelte/inactive
    - https://lucademenego99.github.io/icp-editor/
    - A web application used to create Reveal.js slides with Interactive Code Playgrounds
    - The editor exposes predefined slide templates, in which the user can add text, code playgrounds or images.
    - The text editor is powered by Quilljs

- https://github.com/java-sheets/java-sheets /MIT/202207/java/ts
  - Browser Based Java REPL
  - Jsheet lets you create and share Java snippets, ranging from single expressions to complex classes, methods and even Markdown comments.

- https://github.com/jsbin/jsbin /MIT/202402/js
  - http://jsbin.com/
  - Collaborative JavaScript Debugging App
  - this current version of jsbin (v4.x.x) is no longer actively maintained and the new version of jsbin (v5) is currently in active development
  - 依赖codemirror5
  - https://github.com/jsbin/jsbin/tree/feat/next-v5 /201906/js/inactive

- https://github.com/lewdev/extext /202302/js/inactive
  - https://lewdev.github.io/apps/extext
  - Fast web development now in your browser using CodeMirror.
  - This project started off from my tiny-code-editor which was inspired by Mini Code Editor by xem.

- https://github.com/chinchang/web-maker /MIT/202405/js
  - https://webmaker.app/
  - A blazing fast & offline frontend playground
  - 依赖codemirror5

- https://github.com/ast-grep/ast-grep /MIT/202408/rust
  - https://ast-grep.github.io/
  - https://ast-grep.github.io/playground.html
  - A CLI tool for code structural search, lint and rewriting. Written in Rust
  - playground的diff视图基于monaco实现
  - https://github.com/ast-grep/tree-sitter-wasm
  - https://github.com/ast-grep/ast-grep.github.io

- https://github.com/monis07/logicloom /202405/ts
  - https://logicloom-client.vercel.app/
  - a platform where you can test your coding skills by solving numerous data structures and algorithms
  - Judge0 code execution system is used to execute the codebase submitted by the user.
  - https://x.com/MonisAzeem/status/1786281021354479950
    - a platform where you can test your coding skills by solving numerous data structures and algorithms
    - Backend: I have used Express and MongoDB. Fetched everything like problem list and details of particular problem like title, description and testcases from MongoDB.
    - Frontend: I have used React. 
    - Whenever Submit button is pressed, function code from the editor goes to backend, got integrated with the driver code and passed to @judge0_official server. It returns you with output, id and status.
    - Judge0 also has a limit of 50 api request per day on the basic plan which means you can run 50 testcases at max.

- https://github.com/judge0/judge0 /GPLv3/202404/ruby
  - https://judge0.com/
  - The most advanced open-source online code execution system in the world
- https://github.com/judge0/ide /MIT/202403/js/monaco
  - https://ide.judge0.com/
  - free and open-source online code editor that allows you to write and execute code from a rich set of languages. 
  - Judge0 IDE is using Judge0 for executing user's source code.

- https://github.com/rin-yato/miracle-diagram /202312/ts/inactive
  - https://miracle-diagram.vercel.app/
  - A code first database diagram design tool. 
  - 依赖codemirror6、lezer、shadcn、reactflow、dexie
  - 功能似乎无法正常使用

- https://github.com/google/playground-elements /202405/ts
  - Serverless coding environments for the web.
  - 依赖CodeMirror5

- https://github.com/kazzkiq/CodeFlask /MIT/202006/js/inactive
  - https://kazzkiq.github.io/CodeFlask/
  - A micro code-editor for awesome web pages
  - 依赖prismjs

- https://github.com/codepod-io/codepod /MIT/202311/ts/inactive
  - Codepod provides the interactive coding experience popularized by Jupyter, but with scalability and production-readiness
  - 画板上的代码沙盒，使用monaco而不是codemirror
# starter
- https://github.com/A99US/CM6-Browser-Wrapper /MIT/202308/js/inactive
  - https://a99us.github.io/CM6-Browser-Wrapper/
  - a CodeMirror 6 Wrapper for browser so you don't need to rollup a new one everytime you want to try different setting
  - You need to include JQuery file because it needs JQuery to function

- https://github.com/falk-werner/codemirror-example /202312/js/单文件
  - a brief example how to integrate Code-Mirror using vite.

- https://github.com/RPGillespie6/codemirror-quickstart /202402/js
  - Quickstart guide and examples for those who prefer a more hands on approach to bootstrapping CodeMirror 6
  - Example 1: a minimal example HTML page
  - [Example 2: choose the editor theme on the fly](https://www.bryanpg.com/codemirror-quickstart/examples/example2.html)
  - [Example 3: Try making edits above, saving state, then loading a different state.](https://www.bryanpg.com/codemirror-quickstart/examples/example3.html)
- https://github.com/paul-norman/codemirror6-prebuilt /MIT/202406/js
  - Pre-built bundles for CodeMirror 6 languages
  - Building from Bryan Gillespie's CodeMirror Quickstart, this project adds simpler functions to work with HTML textareas, automatically syncing their values to the codemirror editor's value upon blur and providing placeholder support by default.

- https://github.com/SeonJun-Hwang/rspack-codemirror /202406/ts
  - ts

- https://github.com/datacamp/codemirror-6-getting-started /202102/js
  - Getting started with CodeMirror 6, the popular code editor library
  - [Getting started with the new CodeMirror 6 | DataCamp Engineering _202102](https://blog.datacamp.engineering/codemirror-6-getting-started-7fd08f467ed2)

- https://github.com/codepen/CodeMirror-6-Needs /202208/js/inactive
  - https://objective-blackwell-d4efc9.netlify.app/
  - An exploration of CodeMirror 6 to integrate everything 🏭 CodePen needs to use it in the future.
  - It's a Next.js app as that is the context we hope to be using CodeMirror 6 in.
  - 提供了yjs示例

- https://github.com/craftzdog/electron-markdown-editor-tutorial /MIT/202108/ts/inactive
  - A tutorial for building a beautiful Markdown editor
  - electron + vite + CodeMirror 6 + remark
  - [How to build a Markdown editor using Electron, ReactJS, Vite, CodeMirror, and Remark - YouTube ](https://www.youtube.com/watch?v=gxBis8EgoAg)

- https://github.com/greeenboi/vscodex /202402/ts
  - Vs code Clone
  - 依赖codemirror6、tauri

- https://github.com/Bilal-Belli/Basic-IDE /MIT/202403/js
  - This is a basic Desktop IDE made using ElectronJS NodeJS CodeMirror and JsTree, jquery
- https://github.com/RAGHAV-N5/CodeIt /202312/js
  - a React Project with NodeJs and expressJs using CodeMirror5 and compilex libraries

- https://github.com/pelevesque/codemirror_implementations /202407/js
  - A collection of Code Mirror implementations.

- https://github.com/GiorgiKumelashvili/codemirror-6-playground /202407/ts
  - Nextjs Shadcn Codemirror 6 Examples
# examples
- https://github.com/alexwkleung/Iris /MIT/202312/ts/inactive
  - https://irisnotes.vercel.app/
  - A comfortable note-taking app powered by Markdown
  - 依赖codemirror6、prosemirror、markdown-it、electron-window-state、remark-gfm

- https://github.com/stencila/stencila /apache2/202405/rust/ts
  - https://stenci.la/
  - a platform for authoring, collaborating on, and publishing executable documents.
  - This is v2 of Stencila, a rewrite in Rust focussed on the synergies between three recent and impactful innovations and trends: CRDT/LLM

- https://github.com/ChromeUniverse/luccanotes /202403/ts
  - https://luccanotes.vercel.app/
  - A full-stack note-taking app for Markdown lovers
  - Built with the awesome T3 stack for Next.js, deployed on Supabase and Vercel.
  - 依赖@uiw/react-codemirror、trpc、next、prisma

- https://github.com/jim-fx/notarium /202205/ts/svelte/inactive
  - a note taking and organizing application which uses a folder as a database. 
  - Because of this you can easily use a third party program like syncthing to keep your notes synchronised across all your devices

- https://github.com/kabalage/notesz /MIT/202312/ts/vue
  - https://notesz.app/
  - Note taking PWA that stores your notes on GitHub, built with Vue 3 and TypeScript

- https://github.com/jaywcjlove/code-image /MIT/202311/ts
  - https://jaywcjlove.github.io/code-image
  - Create beautiful images of your source code.
  - 依赖@uiw/react-codemirror、dom-to-image-more

- https://github.com/onderonur/code-image-generator /GPLv3/202404/ts
  - https://onderonur.github.io/code-image-generator/
  - Create your code images by choosing different themes and visual settings.
  - Next.js

- https://github.com/riccardoperra/codeimage /MIT/202405/ts
  - https://codeimage.dev/
  - A tool to beautify your code screenshots. Built with SolidJS
  - SSG+Partial hydration
  - https://x.com/riccardoperra0/status/1603412081054810112
    - lazy load @codemirror and motion without blocking rendering and losing performance.

- https://github.com/wajeshubham/snippng /MIT/202306/ts/inactive
  - https://snippng.wajeshubham.in/
  - Create and share beautiful images of your source code.
  - 依赖@uiw/react-codemirror、firebase、next

- https://github.com/EsperoTech/yaade /MIT/202404/ts/kotlin
  - https://docs.yaade.io/
  - Yaade is an open-source, self-hosted, collaborative API development environment.
  - I was looking for a self-hosted Postman alternative 
  - I've been using both codemirror and lezer in Yaade 

- https://github.com/aidenlx/cm-chs-patch /MIT/202405/ts
  - 增加 Obsidian 内置编辑器的(简体)中文分词支持，使得编辑模式的双击可以选中中文，以及在 Vim 模式下可以按中文分词移动光标
  - 从 v1.8.0 开始，默认分词引擎由结巴分词更换为系统自带分词引擎，结巴分词不再是必备组件
  - 手动安装结巴分词组件：在设置中启用结巴分词后，从CDN下载得到 jieba_rs_wasm_bg.wasm 文件，将 wasm 文件放在 Obsidian 库的 .obsidian 或者其它指定的配置文件夹下后重启 Obsidian

- https://github.com/GaganpreetKaurKalsi/SQL-Editor /202206/js/inactive
  - https://sql-editor-react.vercel.app/sql-editor
  - A frontend application for running SQL queries.
  - Note : For now only SELECT queries on given tables are supported. Will increase it's application in future.

- https://github.com/prisma/text-editors /apache2/202211/ts/inactive
  - https://qc.prisma-adp.vercel.app/
  - these editors were built for the Prisma Data Platform's Query Console
  - This is only a demo of Prisma's text editors. To try out the query console, head over to the Prisma Data Platform

- https://github.com/shahenalgoo/snippad /MIT/202306/ts/inactive
  - https://www.snippad.io/
  - open-source code snippet & notebook app for developers.
  - It is a web/cloud based open-source application made in React/Next.js that you can easily deploy on Appwrite and Vercel for free.
  - 依赖tiptap、appwrite

- https://github.com/spicybirsge/notebin /MIT/202306/js/ejs
  - https://notebin.cf/
  - A codebin / textbin or any thing you call it which will allow you to create "codebins"

- https://github.com/abhint/paste /MIT/202309/python/js
  - open-source and free web application. The Past allows users to upload and share text content online.

- https://github.com/node-projects/web-component-designer /MIT/202405/ts
  - A HTML web component for designing web components and HTML pages based on PolymerLabs wizzywid which can easily be integrated in your own software. Meanwhile polymer is not used anymore.
  - There is also a Preview VS-Code Addon using the Designer

- https://github.com/ambroiseRabier/readable-js /202205/ts/inactive
  - ReadableJS is a toolkit for teachers to craft small demos that can be explored interactively.

- https://github.com/StaticJsCMS/static-cms /MIT/202404/ts
  - https://staticcms.org/
  - A Git-based CMS for Static Site Generators

- https://github.com/blossom-editor/blossom /MIT/202404/java/vue
  - https://www.wangyunf.com/blossom-doc/index
  - 支持私有部署的云端存储双链笔记软件
  - 支持 Windows，Mac，网页客户端，网页移动端。
  - 基于 Markdown 编写，没有破坏性的语法拓展，在这里编写的内容在任何 Markdown 软件中都能正常显示。
  - 不依赖任何三方存储和图床，其本身就是一个图床，并且提供了完善的图片管理，防勿删，以及图片和文章的双向关系绑定。

- https://github.com/KyleleeSea/codemirror-experiments /202406/ts
  - penrose-editor
# theme
- https://github.com/nodetec/mirrorshades /GPLv3/202403/ts
  - A react library to create themes for codemirror
  - I mostly made this to support the fat cursor in used in codemirror-vim, but it can be used to create any theme for codemirror.

- https://github.com/fsegurai/codemirror-themes /MIT/202405/ts
  - https://fsegurai.github.io/codemirror-themes/
  - Themes for CodeMirror 6
  - 提供了GitHub Dark, Android Studio, Nord

- https://github.com/VickyAgravat/wp-codemirror-block /202404/php/js
  - CodeMirror Blocks is useful for tutorial site where display formatted (highlighted) code block. With support of 100+ Language/Mode and 56 Themes.
  - The Code Block is dependent on a CodeMirror library.

- https://github.com/drl990114/codemirror-themes /202311/ts
  - Themes for CodeMirror. forked by https://github.com/uiwjs/react-codemirror/tree/master/themes/theme

- https://github.com/antfu/codemirror-theme-vars /202103/inactive
  - A customizable CodeMirror theme using CSS variables

- https://github.com/craftzdog/cm6-themes /MIT/202312/ts
  - https://cm6-themes.netlify.app/
  - Themes for CodeMirror 6

- https://github.com/ivqonsanada/codemirror6-themes /202111/ts
  - Collection of themes for CodeMirror version 6 (next) code editor

- https://github.com/dennis84/codemirror-themes /MIT/202308/ts
  - Codemirror 6 Themes
  - Not perfect themes for cm6, generated from vscode themes.

- https://github.com/vadimdemedes/thememirror /202206/ts/inactive
  - https://thememirror.net/
  - Beautiful themes for CodeMirror
  - [Making CodeMirror themes look nice with shadcn/ui _202312](https://www.zackrw.com/cbz/codemirror-themes-with-shadcn-ui)
  - https://github.com/satansdeer/thememirror

- https://github.com/cossssmin/codemirror-theme-github /202102/inactive
  - A CodeMirror theme inspired by the GitHub editor.

- https://github.com/ntnyq/codemirror-theme-vitesse /MIT/202407/ts
  - https://codemirror-theme-vitesse.ntnyq.com/
  - Codemirror theme in vitesse style, light + dark
# v5
- examples-v5
  - strapi markdown editor

- https://github.com/0xGG/EchoMD /AGPLv3/202103/ts/inactive
  - An experimental WYSIWYG markdown editor built on top of HyperMD with extended Widgets support
  - This WYSIWYG markdown editor is built and modified on top of @laobubu's awesome project HyperMD.
  - We will migrate to 🎯 codemirror 6 in the future, which is going to be a complete rewrite. 
    - But for now, we will just stick to the current codemirror 5 codebase, that is what HyperMD currently uses.
  - https://github.com/laobubu/HyperMD /MIT/201810/ts/inactive
  - https://github.com/jsimonrichard/HyperMD /MIT/202407

- https://github.com/mirayatech/NinjaPen /202401/ts
  - https://ninja-pen.vercel.app/
  - CodePen clone built with React and TypeScript
  - 依赖codemirror5、react-codemirror2

- https://github.com/JS-Encoder/JS-Encoder /MIT/202212/js/vue/inactive
  - an online front-end code editor（前端在线代码编辑器）built with vue and codemirror
  - JS-Encoder gets some inspiration from JSBin, CodePen and JSFiddle
  - 依赖codemirror5、vue2

- https://github.com/sudipstha08/codepen /MIT/202107/js/inactive
  - https://sudipstha08.github.io/codepen/
  - Codepen clone using React and CodeMirror

- https://github.com/TheNewC0der-24/CodePen-Clone /202201/js/inactive
  - https://my-codepen-clone.netlify.app/
  - create my own CodePen.

- https://github.com/darrowv/JsLogs /202310/js
  - https://darrowv.github.io/JsLogs/
  - Online JS Code Console

- https://github.com/bootstrapworld/codemirror-blocks /202301/ts/inactive
  - A library for building language-specific, CodeMirror-friendly editors that are a11y-friendly.

- https://github.com/soumyajit4419/Editor.io /202102/js/inactive
  - https://code-web.vercel.app/
  - online code editor which supports HTML, CSS, and Javascript Development. 
  - A Markdown editor for generating readme.
  - 依赖codemirror5、remarkable

- https://github.com/cloudcmd/dword /MIT/202403/js
  - Web editor based on CodeMirror. Fork of edward.
  - Drag n drop (drag file from desktop to editor).
  - https://github.com/cloudcmd/edward /MIT/202403/js
    - Web editor used in Cloud Commander based on Ace.
  - https://github.com/cloudcmd/deepword /MIT/202404/js
    - Web editor used in Cloud Commander based on Monaco.
  - https://github.com/coderaiser/cloudcmd /MIT/202405/js
    - https://cloudcmd.io/
    - Cloud Commander file manager for the web with console and editor.

- https://github.com/starwiz-7/codestream /MIT/202204/js/inactive
  - https://codestream.vercel.app/
  - A web app for users to collaborate while solving a coding problem
  - 依赖codemirror5、katex

- https://github.com/inducer/edit-on-web /202403/python/js
  - Edit files in a local directory through a web browser (using CodeMirror5)

- https://github.com/Yash-Singh1/monkeyide /MIT/202105/js
  - A lightweight multi-tab IDE based on CodeMirror5
- https://github.com/praveen4463/out-front-end /202212/js/inactive
  - The front end for Outomated aka browser based IDE   and platform to write, run, debug and scale e2e tests

- https://github.com/youwol/rx-code-mirror-editors /MIT/202401/ts
  - Code editors (typescript, python) using codemirror & flux-view.
  - This library is part of the hybrid cloud/local ecosystem YouWol.
  - 依赖codemirror5、rxjs

- https://github.com/edemaine/codemirror-spell-checker /MIT/202308/js
  - http://nextstepwebs.github.io/codemirror-spell-checker/
  - a fork of sparksuite's codemirror-spell-checker.
  - Tweaked spell checker for CodeMirror5
  - https://github.com/inkdropapp/codemirror-spell-checker
    - It works only on Electron apps since it depends on NodeJS.

- https://github.com/L-Focus/cm-search-replace /202302/js
  - Implements the search and replace function of CodeMirror

- https://github.com/summernote/react-summernote /MIT/202007/js/inactive
  - Summernote (Super simple WYSIWYG editor) adaptation for react

- https://github.com/carbon-app/carbon /MIT/202403/js
  - https://carbon.now.sh/
  - Create and share beautiful images of your source code
  - 对源码生成截图时支持多种theme
  - 依赖codemirror5、puppeteer-core、morphmorph

- https://github.com/massCodeIO/massCode /AGPLv3/202401/ts/vue
  - https://masscode.io/
  - A free and open source code snippets manager for developers
  - 依赖codemirror5、d3、dom-to-image、electron-store、marked
  - 202208: I am excited that v3.0.0-beta.1 is out which now uses Codemirror instead of Ace
# coding-ai
- https://github.com/asadm/codemirror-copilot /MIT/202401/ts
  - https://copilot.asadmemon.com/
  - CodeMirror extension to add GPT autocompletion like GitHub's Copilot

- https://github.com/useScriba/useScriba /202308/ts
  - https://docs.usescriba.com/
  - Highly customizable AI completion plugin for web-based code editors.

- https://github.com/mattelim/text-gpt-p5-app /MIT/202311/js
  - A text to p5.js generative editor powered by GPT-3.5
  - react-codemirror

- https://github.com/sourcegraph/cody /2kStar/apache2/202405/ts
  - https://cody.dev/
  - Cody is a free, open-source AI coding assistant that can write and fix code, provide AI-generated autocomplete, and answer your coding questions. 
  - Cody fetches relevant code context from across your entire codebase to write better code that uses more of your codebase's APIs, impls, and idioms, with less hallucination.
  - Cody is currently in Beta and available for VS Code and JetBrains.
  - 👣 Swappable LLMs: Support for Anthropic Claude, Claude 2, and OpenAI GPT-4/3.5, with more coming soon.
  - You can use Cody Free or Cody Pro when Codying on your work code.

- https://github.com/do-me/SemanticFinder /MIT/202405/js
  - https://do-me.github.io/SemanticFinder/
  - Frontend-only live semantic search with transformers.js
  - Calculates the embeddings and cosine similarity client-side without server-side inferencing, using a quantized version of sentence-transformers/all-MiniLM-L6-v2.
  - https://x.com/DomeGIS/status/1646198509425639426
    - A browser-based semantic search engine you can use to query your own texts

- https://github.com/rvion/CushyStudio /AGPLv3/202403/ts
  - https://docs.cushystudio.com/
  - The AI and Generative Art platform for everyone

- https://github.com/sweepai/sweep /202405/python
  - https://sweep.dev/
  - open-source AI-powered Software Developer for small features and bug fixes.
  - Sweep is an AI junior developer that turns bugs and feature requests into code changes. Sweep automatically handles devex improvements like adding typehints/improving test coverage. 
  - Turns issues directly into pull requests (without an IDE)

## coding-toolchain-ai

- https://github.com/codefuse-ai/codefuse-chatbot /apache2/202405/python
  - CodeFuse-ChatBot是由蚂蚁CodeFuse团队开发的开源AI智能助手，致力于简化和优化软件开发生命周期中的各个环节。
  - 该项目结合了Multi-Agent的协同调度机制，并集成了丰富的工具库、代码库、知识库和沙盒环境，使得LLM模型能够在DevOps领域内有效执行和处理复杂任务
  - 可实现基于开源模型的离线私有部署, 也支持 OpenAI API 的调用
  - 本项目基于langchain-chatchat和codebox-api
# coding-products

- https://github.com/code-hike/codehike /MIT/202307/ts/inactive
  - https://codehike.org/
  - Build first-class code walkthroughs for the web
  - 依赖react、@codesandbox/sandpack-client、@mdx-js/mdx.v2、diff
  - https://github.com/code-hike/examples
- https://github.com/code-hike/examples/tree/main/with-remotion
  - https://x.com/pomber/status/1800108854459715864
  - 不依赖codemirror
  - you can use Remotion's `useFrame` inside any Code Hike annotation to animate most of the examples from the docs
  - wondering if it can also display twoslash annotations, but I don't think remotion supports React Server Components

- https://github.com/replit/desktop /202406/ts
  - Replit desktop app for MacOS, Windows, and Linux
  - 可作为将网站打包为pc-app的模版
  - developed using Electron and packaged and distributed using Electron Forge.
  - You can then launch a packaged version of the app (needed to test certain features like auto-updating) by running the outputted binary locally 
  - To test your changes on other platforms, we recommend using a Virtual Machine host like UTM.
  - The app supports deeplinks with the `replit://` protocol which can be used to open specific pages or flows directly, launching the app if it's not already running.
# more
- https://github.com/leaverou/rety /MIT/202302/js/inactive
  - https://rety.verou.me/
  - Record typing on one or more editors and replay it at will, to simulate live coding
  - Rety is a library that allows you to record the edits you make on one or more pieces of text (usually code) and replay them later to recreate the same typing flow.
  - It does not come with any particular UI, the UI is up to you. The UI you see in some of the demos in these docs is not part of Rety.
  - Rety is designed to work well with the code editors of Prism Live and CodeFlask but it should work with any `<input>, <textarea>` or even compatible custom elements.

- https://github.com/datavis-tech/codearea /MIT/201908/js/inactive
  - A proof-of-concept code editor with syntax highlighting that uses
    - highlighted-pre-over-textarea approach (like react-simple-code-editor)
    - web-tree-sitter for incremental parsing
    - `diff-match-patch` via `json0-ot-diff` for computing text diffs (needed for using tree-sitter)
    - React for DOM updates

- https://github.com/scalar/scalar /MIT/202406/ts/vue
  - https://scalar.com/swagger-editor
  - Beautiful API references from OpenAPI/Swagger files
  - Edit your OpenAPI/Swagger specification with a live preview
  - https://github.com/scalar/scalar/tree/main/packages/use-codemirror /202305/ts/vue3

- https://github.com/replit/crosis /MIT/202406/ts
  - A JavaScript client that speaks Replit's container protocol
  - You should probably familiarize yourself with the protocol before trying to use it. Crosis is just a client that helps you connect and communicate with the container using the protocol.
  - The central concept is a "channel" that you can send commands to and receive commands from. 

- https://github.com/FriendsOfREDAXO/aceeditor /MIT/202407/php/js
  - Ace-Editor - The high performance code editor for REDAXO - Replacement for codemirror
