---
title: lib-editor-codemirror-examples
tags: [code-editor, codemirror, examples]
created: 2023-06-23T12:46:36.949Z
modified: 2023-06-23T12:46:53.288Z
---

# lib-editor-codemirror-examples

# guide

- 支持切换editor的方案: overleaf(ace/src/visual), sandpack, jupyter(只接口), @uiw/react-*-editor

- examples
  - 类似打字机动态输出文字, 多用于ai生成代码/文本
    - **pausable**
    - multi-writer的效果
  - (diff)字符渐变的动画效果, 🤔 和时间旅行的回放过程有何区别
    - diff只需初始结束状态, 而时间旅行支持中间状态
  - codemirror + dockview/fileTree

- fans-codemirror
  - https://github.com/val-town/codemirror-ts
  - https://github.com/uiwjs/react-codemirror 
  - https://github.com/yeliex/codemirror-extensions 
  - https://github.com/exuanbo/codemirror-toolkit 
  - https://www.npmjs.com/package/collaborative-codemirror
  - [Monkatraz - discuss. CodeMirror](https://discuss.codemirror.net/u/Monkatraz/summary)

- resources
  - https://codemirror.net/docs/community/
  - https://news.ycombinator.com/threads?id=CompuIves
  - [List of community extensions? - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/list-of-community-extensions/4899)
  - https://www.npmjs.com/search?ranking=maintenance&q=codemirror
    - https://github.com/search?type=registrypackages&q=codemirror&s=created&o=desc
    - https://x.com/search?q=codemirror&src=typed_query&f=live
# popular
- https://github.com/tmcw/awesome-codemirror
  - Awesome CodeMirror plugins, themes, wrappers, and more

- https://github.com/milahu/browserforge /202303/方案收集markdown
  - run github + github-pages + codesandbox in your browser, offline-first - CONCEPT

- overleaf /12.6kStar/AGPLv3/202407/js/ts(codemirror)/latex/ace>codemirror
  - https://github.com/overleaf/overleaf
  - https://github.com/overleaf/overleaf/wiki
  - https://github.com/overleaf/overleaf/tree/main/services/web/frontend/js/features/source-editor
  - A web-based collaborative LaTeX editor
  - CodeEditor和VisualEditor都基于codemirror6实现
  - source-editor支持codemirror6/ace(deprecated)
  - 🔌 实现的codemirror ext包括100多个 codemirrorDevTools, trackChanges, bracketSelection, mathjax, thirdPartyExtensions
  - 线上体验xp
    - 版本历史类似github的仓库快照，能查看某一时刻的所有文件状态，支持显示每个文件的修改数量
    - 版本会隔一段时间自动保存，支持添加label
    - 版本历史的内容差异未使用官方的diff视图，自定义渲染行内diff，history界面的内容差异视图支持显示删除线
  - 编辑器体验xp
    - 💬 支持comment，但实现方式不是extension
    - collab基于sharejs.v0.5魔改实现，未使用官方collab插件
    - latex出现语法错误时，编辑器会将对应的部分渲染为纯文本
  - [Compile Error and PDF Download Notifications](https://github.com/overleaf/overleaf/issues/1031)
    - migrate from ACE to CodeMirror 6. Yes, the CM6 work will be coming to CE soon. _202206
  - https://github.com/overleaf/overleaf/tree/main/services/document-updater/app/js/sharejs /202205/MIT/js
    - 🔀 协作基于sharejs.v0.5修改实现
  - https://github.com/overleaf/overleaf/blob/main/services/web/frontend/js/features/source-editor/extensions/track-changes.ts
    - 基于codemirror6实现track-changes的示例
    - 在生产环境编辑器的track-changes试用入口播放了添加和删除文字的动画，没有直接实现删除线但效果类似； history界面的内容差异视图支持显示删除线
    - [Track changes and commenting in LaTeX - Overleaf, Online LaTeX Editor](https://www.overleaf.com/track-changes-and-comments-in-latex)
    - [Track Changes in Overleaf intro](https://www.overleaf.com/learn/how-to/Track_Changes_in_Overleaf)
    - [Tracking changes in LaTeX with "changes" package _201908](https://www.overleaf.com/latex/examples/tracking-changes-in-latex-with-changes-package/fnpkpytjjwhj)
  - 🫧 [Horizontal Scaling: Starting with version 3.5.6 Server Pro supports horizontal scaling _202305](https://github.com/overleaf/overleaf/wiki/Horizontal-Scaling)
    - A deployment of Server Pro with horizontal scaling involves a set of external components, such as a Load Balancer and an S3-compatible backend
    - [We do a customer-taylored capacity planning as part of our Enterprise Solution, Overleaf Server Pro _202009](https://github.com/overleaf/overleaf/issues/784)
  - [Is it possible to include the commenting feature in the Community Edition? _202402](https://github.com/overleaf/overleaf/issues/1193)
    - You can try to develop it by yourself, or purchase server pro. Btw, I think commenting feature is not something difficult to imply, the core code is open-source, just need a proxy.
    - 🌵 I created a new branch, which includes only the code for enabling **comments and changes tracking** features. 
  - 🐛未解决: [[Feature Request] Enable to display 4-byte characters in the editor _202406](https://github.com/overleaf/overleaf/issues/1234)
    - The editor can display basic 3-byte emojis (without some emojis with ligature) (on row 16), but it cannot display any 4-byte emojis (on row 17).
    - CJK IME shows converting candidates including emoji while inputting, however, the current candidate turns into a "non-compliant" string when those emoji appear as the current candidate. It terminates the converting process, thus we cannot select the correct candidate, making it hard to input our languages in the editor.
  - [Node 20 Compile Issues · Issue · mscdex/mmmagic](https://github.com/mscdex/mmmagic/issues/169)
    - I've just updated the @picturae/mmmagic package to support node 22 as well
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
  - https://git.szumserver.eu/szymon/overleaf
  - https://github.com/smhaller/ldap-overleaf-sl
    - Free LDAP and OAuth2 Authentication and Authorisation for Sharelatex / Overleaf (Community Edition)

- https://github.com/codesandbox/sandpack /4.5kStar/apache2/202405/ts
  - https://sandpack.codesandbox.io/
  - https://sandpack.codesandbox.io/docs
  - https://sandpack.codesandbox.io/docs/advanced-usage/components
  - Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.
  - sandpack-client依赖nodebox、static-browser-server
  - sandpack-react依赖sandpack-client、codemirror6、@lezer/highlight、lz-string、react-devtools-inline
  - 提供了很多示例，包括cm-DecoratorsDynamic/FileExplorer/ReactDevTools
  - 自定义实现的codemirror ext很少
  - codemirror editor不支持跳转到定义
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
  - https://github.com/danilowoz/sandpack-tsserver  /202203/ts/inactive
    - https://github.com/aboveyunhai/playground-ts /202303/ts/inactive
    - [TypeScript integration · codesandbox/sandpack _202112](https://github.com/codesandbox/sandpack/discussions/237)
      - once you start to edit the code or change tab (trig render basically), ts-server will start to kick in
      - Vocs is solving this elegantly with Twoslash

- https://github.com/jupyterlab/jupyterlab/tree/main/packages/codemirror /BSD/202405/ts
  - A JupyterLab package which provides the default implementation of the `@jupyterlab/codeeditor` interface, using the `CodeMirror` editor.
  - cm编辑器及ext相关代码不多
    - 协作基于yjs实现
  - 仓库代码整体用了很多class和namespace
    - 很多配置和扩展都采用了registry的设计
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
  - https://github.com/osscar-org/widget-code-input /BSD/202406/python/js
    - A jupyter widget to allow input of a python function, with syntax highlighting
  - https://github.com/jupyter/nbdime /BSD/202408/python/ts
    - 🆚️ Tools for diffing and merging of Jupyter notebooks.
- https://github.com/pretzelai/pretzelai /AGPL/202408/ts/python
  - https://withpretzel.com/
  - Modern, open-source Jupyter alternative
  - 🍴 Pretzel is a fork of Jupyter with the goal to improve Jupyter's capabilities. We've added AI code generation and editing, inline tab completion, sidebar chat and error fixing to Jupyter for now with a lot more to come.
  - 依赖codemirror
  - To use your own model (OpenAI, Anthropic/Claude, Ollama or Groq), see the Configuration section
  - Inline Tab Completion
    - Wait for 1 second to trigger completions. 
    - The default Pretzel AI Server uses Mistral's Codestral but you can switch the inline completion model in Settings
  - We DO NOT store any code or data you send to the Pretzel AI Server

- Zettlr /9.3kStar/GPLv3/202408/ts/vue/偏学术编辑器
  - https://github.com/Zettlr/Zettlr
  - https://www.zettlr.com/
  - https://docs.zettlr.com/
  - Your One-Stop Publication Workbench
  - 依赖electron-forge、codemirror.v6、@lezer/highlight、d3.v7、katex、remark-math、vue3、vuex4、pinia
  - exports with Pandoc, LaTeX, and Textbundle
  - support LaTeX and Word template
  - Citations made easy: Tight and ever-growing integration with your favourite reference manager (Zotero, JabRef, and many others)
  - Support for state of the art knowledge management techniques (Zettelkasten)
  - https://github.com/Zettlr/Zettlr/tree/develop/source/common/modules/markdown-editor/plugins
    - 🔌 ext实现了typewriter(当前行居中),contextMenu,statistics-fields,toc

- https://github.com/wikimedia/mediawiki-extensions-CodeMirror /GPL/202410/js
  - https://doc.wikimedia.org/CodeMirror/master/js/js/
  - MediaWiki extension CodeMirror
  - provides syntax highlighting in MediaWiki wikitext editors using CodeMirror
- https://github.com/bhsd-harry/codemirror-mediawiki /GPLv2/202407/ts
  - https://bhsd-harry.github.io/codemirror-mediawiki/
  - Modified CodeMirror mode based on wikimedia/mediawiki-extensions-CodeMirror
  - 💡 The goal is to support a standalone integration between CodeMirror and Wikitext, without the need for a MediaWiki environment

- https://github.com/tidbcloud/tisqleditor /MIT/202408/ts
  - https://tisqleditor.vercel.app/
  - https://tisqleditor.vercel.app/playground
  - https://tisqleditor.vercel.app/examples?ex=all&theme=default
  - old-eg
    - https://tisqleditor-playground.netlify.app/
  - CodeMirror6 based SQL code editor which is used in TiDB Cloud Console
  - Supply React component and Vue component
  - 提供了ai-widget 👾🆚️

- https://github.com/vizhub-core/vzcode /MIT/202406/ts/js(server)
  - VZCode: Multiplayer Code Editor
  - VZCode offers a multiplayer code editing environment that caters to a real-time collaborative development experience. It's the code editor component of VizHub, and can also be used independently from VizHub.
  - Browser-based editing environment
  - Real-time collaboration via LAN or using services like NGrok
  - 自定义的ext不多
  - 协作基于自定义codemirror-ot及sharedb
  - A known shortcoming of VZCode is that it does not (yet) watch for changes from the file system. VZCode assumes that no other programs are modifying the same files.
  - You can also expose your VZCode instance publicly using a tunneling service such as NGrok.
  - Auto-save, debounced after code changes
  - I also have a history of working with CodeMirror 5 + ShareDB for the real-time integration, and was able to "unlock" that CodeMirror 6 + ShareDB integration successfully
  - [VSCode-ish: Jump to Definition of Variable ](https://github.com/vizhub-core/vzcode/issues/177)
    - 🌰 [202406已合并pr, 只实现了文件内跳转定义，且需要按住`Ctrl`键(macos下也是)同时移动鼠标](https://github.com/vizhub-core/vzcode/pull/717)
    - 基于遍历syntaxTree判断节点类型实现，纯前端的实现方案，触发时机没有注册在editor `document.addEventListener('mouseover', handleMouseOver)`;
    - 似乎只支持.js文件，.java文件不支持显示下划线
  - [pr已合并_Intelligent Autocompletions _202311](https://github.com/vizhub-core/vzcode/pull/305)
  - https://github.com/vizhub-core/vizhub /v3
    - possible to self-host your own instance
    - possible to extend the core with plugins
    - vzhub网站不支持跳转到定义
  - https://github.com/vizhub-core/vizhub-legacy /202206/js/inactive
    - https://vizhub.community/
    - Self Hosted CMS for Web-based Dataviz
    - VizHub 2 has been used in Data Visualization Course 2018, Datavis 2020
    - iFrame-based code execution environment.
  - https://github.com/vizhub-core/codemirror-6-experiments /MIT/201811/js
    - [Codemirror 6 Experiments _201811](https://currankelleher.medium.com/codemirror-6-experiments-a3930bf03781)

- silverbullet /2.4kStar/MIT/202410/ts
  - https://github.com/silverbulletmd/silverbullet
  - https://silverbullet.md/
  - SilverBullet is an extensible, open source personal knowledge platform. 
  - implemented as an open-source offline-capable web application.
  - written in TypeScript and built on top of the excellent CodeMirror 6, preact
    - The server backend runs as a HTTP server on Deno using and is written using Oak.
  - At its core it’s a clean markdown-based writing/note taking application that stores your pages (notes) as plain markdown files in a folder referred to as a space. 
  - While SB uses a database for indexing and caching some indexes, all of that can be rebuilt from its markdown source at any time. 
  - extensible with plugs, and you can customize it
  - [Silver Bullet: Markdown-based extensible open source personal knowledge platform | Hacker News_202212](https://news.ycombinator.com/item?id=33843009)

- https://github.com/sourcegraph/openctx/tree/main/client/codemirror /apache2/202405/ts
  - https://openctx.org/playground
  - implements a CodeMirror extension that shows OpenCtx items in the editor
  - OpenCtx shows you contextual info about code from your dev tools, in your editor, in code review, and anywhere else you read code
  - https://github.com/sourcegraph/codeintellify /MIT/202111/ts/archived
    - Adds code intelligence to code views on the web
    - This library manages all of the inputs (mouse/keyboard events, location changes, hover information, and hover actions) necessary to display hover tooltips on with a code view.
    - 依赖rxjs、sourcegraph
  - [Changelog - Sourcegraph docs](https://sourcegraph.com/docs/CHANGELOG)

- https://github.com/KittyCAD/modeling-app /MIT/202408/rust/ts
  - https://kittycad.io/modeling-app/download
  - https://app.zoo.dev/
  - https://zoo.dev/diff-viewer
  - The KittyCAD modeling app
  - 依赖codemirror6、Custom WASM LSP Server、codemirror-lsp-client-kcl、xstate4、threejs、@headlessui/react、fortawesome、@tweenjs/tween.js、fuse.js、json-rpc-2.0
  - ZMA is an open-source CAD application for creating accurate 3D models for use in manufacturing. It is built on top of KittyCAD, the design API from Zoo. 
  - Modeling App and Diff Viewer are currently free.
  - Modeling App is a hybrid user interface for CAD modeling. 
    - You can point-and-click to design parts (and soon assemblies), but everything you make is really just kcl code under the hood. 
    - All of your CAD models can be checked into source control such as GitHub and responsibly versioned, rolled back, and more.
  - The 3D view in Modeling App is just a video stream from our hosted geometry engine. 
    - The app sends new modeling commands to the engine via WebSockets, which returns back video frames of the view within the engine.

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

- https://github.com/davidmyersdev/ink-mde /206Star/MIT/202507/ts/函数式/typora风格
  - https://stackblitz.com/fork/github/davidmyersdev/ink-mde/tree/main/examples/template-ts
  - A beautiful, modern, customizable Markdown editor powered by CodeMirror 6 and TypeScript
  - This is the editor that powers https://octo.app.
  - Inline Markdown image previews
  - Framework agnostic, 支持vue/svelte; 👀 但部分ui及示例使用了solidjs
  - Supports Server-Side Rendering (SSR)
  - Wrap a native `textarea` element with the `wrap` export
  - 🔌 Plugin API (experimental): blockquote, image, codeblock
  - https://github.com/davidmyersdev/octo /MPLv2/202405/ts/vue
    - https://octo.app/
    - A local-first, progressive web app for knowledge management
    - End-to-End Encryption (E2EE) support

- https://github.com/gaelj/BlazorCodeMirror6 /MIT/202407/csharp/ts/typora风格
  - https://gaelj.github.io/BlazorCodeMirror6/
  - Blazor CodeMirror 6 brings the power of the CodeMirror 6 code editor to Blazor, offering a comprehensive . NET6/7/8 component
  - Markdown editor for Blazor
  - 支持编辑时开启/关闭diff-view，✨ diff视图下accept变更后立即撤销会先回到diff视图
  - 实现了diff上下视图，支持高亮变更及gutter，支持accept/reject变更action
    - 亮变更内容的粒度是字符，但未突出删除字符的样式
  - markdown编辑体验支持行内切换md代码和预览，✨ 类似typora
  - 支持图片、emoji
  - 依赖thememirror、emojilib
  - manual resizing of the editor (similar to html textarea)
  - custom linting
  - allow undo/redo toolbar buttons, 实现了UndoSelection
  - 📈 CSV mode: add column paddings for alignment, navigate columns with tab / shift-tab; 支持markdown-table 📈
  - 支持emoji

- https://github.com/imzbf/md-editor-rt /MIT/202407/ts/非及时预览
  - https://imzbf.github.io/md-editor-rt
  - https://imzbf.github.io/md-editor-rt/en-US/demo
  - react版本的 Markdown 编辑器
  - 源码与预览同步滚动, 预览组件非codemirror
  - 支持切换预览风格、代码风格主题、emoji、prettier
  - 当使用服务端渲染时，请务必设置editorId为固定值
  - 自定义 markdown-it 核心库扩展、属性等
  - 功能丰富，示例丰富
  - https://github.com/imzbf/md-editor-v3 /MIT/202407/ts
    - https://imzbf.github.io/md-editor-v3
    - vue3 环境的 Markdown 编辑器
  - https://github.com/imzbf/md-editor-extension
    - Common extensions for md-editor-v3 and md-editor-rt

- https://github.com/Type-32/codemirror-rich-obsidian /202508/ts
  - Obsidian-Flavored WYSIWYG Markdown Editor using CodeMirror 6

- https://github.com/emdashcodes/codemirror-markdown-canvas /MIT/202506/ts
  - a plugin for CodeMirror 6 that provides a rich editing experience for Markdown content.
  - Inspired by Obsidian's Markdown Live Preview.
  - The plugin takes advantage of the lezer-markdown tokenizer that comes with CodeMirror's Markdown language support. 

- https://github.com/glifox/gnosis /MIT/202507/ts
  - http://gnosis.feraxhp.com/
  - GNOSIS is an extension-pack for codemirror to support WYSIWYG markdown 
  - The Obsidian editor is nice but not Open Source... So I decided to start a new project.

- https://github.com/marcoklein/noteberry /MIT/202204/ts/archived/notion-like
  - https://marcoklein.github.io/noteberry/
  - https://marcoklein.github.io/noteberry/codemirror-block-editor/
  - A toolbox for working with block-based linked markdown notes
  - https://github.com/marcoklein/codemirror-block-editor /archived

- https://github.com/JerryI/wljs-editor /202407/js/多层嵌套cm/formula
  - https://jerryi.github.io/wljs-editor/
  - A cell editor & supporting packages for wolfram-frontend project written in JS with Codemirror 6. Support mathematical expressions rendered inline, Mathematica's boxes and many more...
  - This is a core component of Wolfram JS Frontend project
  - 多个编辑器nested示例
  - [Multiple Editable Columns with CodeMirror 6 - v6 - discuss. CodeMirror](https://discuss.codemirror.net/t/multiple-editable-columns-with-codemirror-6/8514)
    - here is an example with even ~10 nested editor, which can perfectly work with all updates and mutations and cursor movements
  - https://github.com/JerryI/wolfram-js-frontend
    - Dynamic Notebook Environment for Wolfram Language written in Javascript

- https://github.com/getcursor/old /192Star/MIT/202304/ts/inactive
  - https://github.com/fovi-llc/cursor-codemirror/blob/main/src/components/codemirrorHooks/extensions.ts
  - A Codemirror-based editor with many modern need-to-haves (e.g. LSP, Copilot, Vim, Remote SSH)
  - This is an old version of Cursor based off of the Codemirror text editing component. If you're looking to build your own code editor from the ground-up, this may serve as a useful guide. Cursor is now based on a fork of VSCodium.
  - 依赖codemirror6、@headlessui/react、@reduxjs/toolkit、electron-store、markdown-it、vscode-languageserver-protocol、xterm、xterm-addon-search
  - 🔌 扩展多，包括diffExtension, hackDiff, rejectSuggestionCommand, copilotStatus, updateCommentsEffect
  - AI Features: auto-generated inline diffs and completions, a ChatGPT-style embedded chat, on-hover documentation suggestions
  - Deep language server support: intellisense, go-to-definition, code actions, linting, symantic syntax highlighting
  - 🍴 forks
  - https://github.com/abdulrahman305/cursor
  - https://github.com/fovi-llc/cursor-codemirror
  - https://github.com/kumar045/cursor-codemirror
  - https://github.com/carloslfu/cursor-old
  - https://github.com/tyyxuhao/cursor
    - 专为 AI 编程而生的编辑器
  - https://github.com/beachstrider/cursor-assist-electron-openai /202303/ts/inactive
    - This is an OpenAI based code editor built for pair programming with AI

- https://github.com/replit/codemirror-minimap /202401/ts
  - Minimap extension for Codemirror 6

- https://github.com/replit/codemirror-interact /202403/ts
  - https://replit.com/@util/codemirror-interact
  - A CodeMirror extension that lets you interact with different values (clicking, dragging, etc).

- https://github.com/marimo-team/codemirror-ai /apache2/202508/ts
  - https://marimo-team.github.io/codemirror-ai/
  - 👾 A CodeMirror extension that adds AI-assisted inline code editing capabilities to your editor (like Continue.dev and Cursor)
  - Accept/reject AI suggestions with a clean, modern interface
  - 输入提示词实现为嵌入式卡片
  - 🆚 ai的修改建议会显示为diff视图(无打字动画)，但accept后undo时不会恢复diff视图
  - 还实现了在浮窗中显示suggest edit
  - https://github.com/Oxen-AI/codemirror-copilot
    - Integrating Oxen.ai's autocomplete into codemirror as a POC for Marimo notebooks

- https://github.com/val-town/codemirror-codeium /ISC/202404/ts
  - https://val-town.github.io/codemirror-codeium/
  - Codeium code completion integration for CodeMirror 6
  - 👾 Copilot-like ghost text code from modeling-app by Jess Frazelle and based on Cursor.
    - 等1s会显示补全预览，支持切换8个补全方案
  - This makes requests against the Codeium hosted product, using their Protocol Buffer-based interface

- https://github.com/yuri2peter/codemirror-ai-enhancer /MIT/202503/ts
  - https://codemirror-ai-enhancer.vercel.app/
  - extension that leverages AI to perform localized text modifications and continuations.
  - 仅灰色修改提示，无diff
  - Customizable LLM invocation

- https://github.com/marimo-team/codemirror-mcp /apache2/202501/ts/inactive
  - https://marimo-team.github.io/codemirror-mcp/
  - A CodeMirror extension that implements the Model Context Protocol (MCP) for resource mentions and prompt commands.
  - Autocomplete for @resource mentions, Use @resource-uri syntax to reference resources
  - Autocomplete for /prompt commands
  - 依赖 @modelcontextprotocol/sdk

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
- https://github.com/hostilefork/replpad-js /LGPLv3/202206/js
  - Interactive Web Console for Rebol language (Ren-C branch)
  - This project is an effort to build an interactive GUI console that runs in a web browser, for the Ren-C branch of Rebol3

- https://github.com/uiwjs/react-markdown-editor /MIT/202404/ts
  - https://uiwjs.github.io/react-markdown-editor
  - A markdown editor with preview, implemented with React.js and TypeScript.
  - 依赖@uiw/react-codemirror、@uiw/react-markdown-preview
  - 支持源码和预览同步滚动
  - https://github.com/jaywcjlove/wxmp /MIT
    - 微信公众号文章 Markdown 在线编辑器，使用 markdown 语法创建一篇简介美观大方的微信公众号图文
    - 未来不再开发 Chrome 的插件(暂存在 chrome 分支)，通过 web 版本定制更丰富的功能

- https://github.com/uiwjs/react-codemirror /MIT/202404/ts
  - https://uiwjs.github.io/react-codemirror/
  - https://uiwjs.github.io/react-codemirror/#/merge/document
  - CodeMirror 6 component for React
  - Versions after `@uiw/react-codemirror@v4` use codemirror 6.
    - 从v4(202109)开始使用cm6，[v3.0 cannot be upgraded to 4.0+](https://github.com/uiwjs/react-codemirror/issues/88)
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

- https://github.com/handlewithcarecollective/react-codemirror /MIT/202506/ts
  - A simple library for safely integrating React and CodeMirror.

- https://github.com/scniro/react-codemirror2 /MIT/202108/ts/v5/inactive
  - https://scniro.github.io/react-codemirror2/
  - ships with the notion of an uncontrolled and controlled component

- https://github.com/ui-schema/react-codemirror /MIT/202409/ts
  - https://github.com/ui-schema/demo-mui-kit-codemirror
  - React CodeMirror v6 Component - and UI-Schema widget for MUI
  - Example with CodeMirror + MUI styling - but no further @ui-schema/ packages.

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

- https://github.com/0xsuk/agitcms /MIT/202212/ts/inactive
  - A hackable headless CMS for markdown blogs
  - Agit CMS is a simple web frontend interface that utilizes filesystem to manage markdown/media contents. 
  - 依赖codemirror6、mui5、remark-gfm、remark-parse、xterm
  - Built for markdown-based static site generators, like Hugo and Jekyll.
  - vertical split style markdown editor, 左右分屏
  - reads from and writes to your filesystem

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

- https://github.com/JPerez00/typesavior /202503/ts
  - https://typesavior.vercel.app/
  - Your AI JavaScript to TypeScript Converter.
  - Code Conversion: Paste your JavaScript code and receive the TypeScript version.
  - Detailed Summaries: Get concise explanations of the changes made 
  - Model Selection: Choose between different OpenAI models for code conversion.
  - TypeSavior uses the power of OpenAI's language models to convert your JavaScript code to TypeScript.

- https://github.com/Sagargupta16/ai-code-translator /202311/ts
  - https://ai-code-translator-delta-six.vercel.app/
  - Use AI to translate code from one language to another
  - 依赖@uiw/react-codemirror、next

- https://github.com/EditableBlock/EditableBlock /NonOpen
  - https://editableblock.github.io/EditableBlock/
  - EditableBlock 开发阶段快速测试平台 + 试用Demo
  - MdEditor: 纯文本
  - MdViewer: 渲染，使用markdown-it引擎 + EditableBlock 插件，不可编辑
  - CodeMirror: 渲染，使用CodeMirror引擎 + EditableBlock 插件，可编辑
  - CodeMirrorOld: 渲染，使用CodeMirror引擎，可编辑

- https://github.com/oscarmarina/monaco-editor-vs-codemirror /MIT/202501/ts/inactive
  - This project is a playground to compare the CodeMirror and Monaco Editor libraries

## typewriter/Text Generate Effect

- https://stackblitz.com/edit/react-ts-yiu185
  - [How To Create A Text Generate Effect In React | Algochurn _202209](https://www.algochurn.com/blog/how-to-create-a-text-generate-effect-in-react)
  - https://www.algochurn.com/frontend/text-generate-effect
  - create a Typewriter Effect from scratch using native React and/or Javascript functions
  - 动画打字完undo会撤销所有字
  - 依赖codemirror6、@uiw/react-codemirror

- https://github.com/gitdog01/AnimateTyping-cm6 /MIT/202507
  - a plugin for CodeMirror 6 that adds dynamic CSS-based typing animations to your editor.
  - As you type, visually engaging effects like bouncing letters, glowing text, and motion trails enhance the user experience 
  - perfect for presentations, educational tools, or just making coding more fun.
  - Multiple Animation Types: Choose from fadeIn, glow, shootingStar, rollingThunder, frenchFries, and bubble effects
  - Configurable: Customize animation duration and style
  - Only animates newly typed characters

### typewriter-css-only

- https://github.com/Mikulew/css-typewriter-effect /202112/css
  - https://mikulew.github.io/css-typewriter-effect/
  - Typewriter effect using CSS animation only
  - Pure CSS3 typing animation with steps()

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

- https://github.com/meowtec/diffani /ISC/202307/ts/inactive
  - https://diffani.co/
  - Diff code and render to animation video
  - 依赖codemirror6、diff、d3-ease、jsdom、prismjs、zustand、webm-writer、vite

- https://github.com/shikijs/shiki-magic-move /MIT/202405/ts
  - https://shiki-magic-move.netlify.app/
  - Smoothly animated code blocks with Shiki.
  - The package provides framework-agnostic core and renderer and framework wrappers for Vue and React.
  - 依赖diff-match-patch-es、ohash
  - 不依赖codemirror
  - [The Magic in Shiki Magic Move _202403](https://antfu.me/posts/shiki-magic-move)

- https://github.com/uxiew/codemirror-shiki /202408/ts
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

- https://github.com/mcnuttandrew/prong /MIT/202310/ts/inactive
  - https://prong-editor.netlify.app/
  - https://prong-editor.netlify.app/#/vega-lite
  - Prong (PRojectional jsON Gui) is an editor framework for creating bespoke in-browser editors for JSON-based domain-specific languages (such as Vega, Vega-Lite, Tracery, and many others). 
  - These editors allow for things like drag-and-drop interactions, inline-interactive spreadsheets, in-situ recommenders and sparklines, and many more elements that would require significant engineering effort to create otherwise.
  - 依赖codemirror6、react-markdown、jsonc-parser
  - 支持在编辑器内渲染 table
  - This system isn't really for interacting with data. There are lots of other great systems for wrangling JSON data of various kinds (such as JSON Crack, jq, and many others), it's just for DSL style usage. 

- https://github.com/evinowen/tome /MIT/202406/ts/vue
  - https://tome.evinowen.net/
  - 🌵 git integrated cross-platform markdown editor
  - 依赖codemirror6、marked、nodegit、vue3、@electron/rebuild

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

- https://github.com/minditor/minditor /MIT/202403/ts/inactive
  - https://minditor.dev/
  - A plug-and-play, highly customizable block-based rich text editor. 
  - Supports block/inlineBlock development with any framework, including React/Vue.
  - 未使用react/vue, ~~使用自研未开源的视图框架axii~~
  - 依赖codemirror6、highlight.js、eventemitter3、thememirror、@uppy/xhr-upload
  - 由 Zhenyu Hou 独立开发和维护
  - 不支持拖拽改变block顺序
  - [开源富文本编辑器，支持用 React/Vue 或任何框架开发 Block/InlineBlock。 - V2EX _202403](https://v2ex.com/t/1019749)
    - 保存的是 json 。类似的有 editor.js ，quilljs 。他们好像不支持 inlineBlock ，写复杂插件缺少了一些系统应该提供的 reactive state ，要自己注册各种事件监听。比较麻烦，所以我自己写了这个编辑器。

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

- https://github.com/unvalley/ephe /MIT/202508/ts/极简风格
  - https://ephe.app/landing
  - Ephe is an ephemeral markdown paper to organize your daily todos and thoughts.
  - Ephe is designed to organize your tasks with plain Markdown.

- https://github.com/retronav/ixora /apache2/202305/ts/inactive
  - a CodeMirror 6 extension pack to make writing Markdown fun and beautiful.
  - Auto link detection
  - https://codeberg.org/retronav/ixora /202305/ts/inactive

- https://github.com/madeyoga/chun-mde /MIT/202207/ts/inactive
  - https://madeyoga.github.io/chun-mde/
  - Markdown editor based on codemirror 6

- https://github.com/jalalmanafi/ownmd /MIT/202410/ts
  - https://ownmd.io/
  - open-source Markdown editor for the web. Write, preview, and share your Markdown content with ease.
  - Client-side saving

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
  - 其他的属性你们就可以直接参考 vue-codemirror6 了，我就是个二道贩子，基于 vue-codemirror6 做的一层封装，让大家感觉更方便用一点

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

- https://github.com/dxos/dxos/tree/main/packages/ui/react-ui-editor /MIT/202408/ts
  - Document editing experience within a DXOS shell
  - 依赖codemirror6、react-dropzone

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

- https://github.com/common-repository/codemirror-file-editor /GPL/202411/js
  - https://wordpress.org/plugins/codemirror-file-editor/
  - Replaces defaults WordPress Theme and Plugin Editors with CodeMirror
  - https://github.com/common-repository/codemirror-for-codeeditor
    - Just another code syntaxhighligher for the theme and plugin editor with CodeMirror. This plugin can highlight sourcecodes in the theme/plugin editor and provide a useful toolbar.
  - https://github.com/common-repository/codemirror-for-post-editor
    - This plugin adds an editor button that will let you use the great [CodeMirror](http://codemirror.net) editor to edit the HTML code of your posts.
  - https://github.com/common-repository/wp-codemirror-block
  - https://github.com/common-repository/codemirror-2

- https://github.com/frabjous/open-guide-editor /GPLv3/202404/php/js
  - Web based editor based on codemirror for editing markdown and LaTeX files with live updating HTML and PDF previews
  - Highly configurable web-based text editor based on codemirror primarily designed for editing markdown, LaTeX, and html files with live-updating html and pdf previews.
  - it can be used to edit other plain text files as well, including subsidiary files (css, javascript, csv, json, pandoc templates, etc.) and see their effects live-update in their chosen root markdown/LaTeX/html document. 

- https://github.com/geometryzen/stemcstudio-codemirror /MIT/202406/ts/单文件
  - Bundle of CodeMirror Editor
  - A wrapper around the CodeMirror editor for use in STEMCstudio.

- https://github.com/riccardoperra/solid-codemirror /MIT/202305/ts/inactive
  - A library of SolidJS primitives to build code editors using CodeMirror 6
  - https://github.com/nimeshnayaju/solid-codemirror /202207/ts/inactive

- https://github.com/touchifyapp/svelte-codemirror-editor /MIT/202405/ts
  - https://touchifyapp.github.io/svelte-codemirror-editor/
  - A svelte component to create a CodeMirror 6 editor.

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

- https://github.com/festerduck/codemirror-markdown /202406/ts
  - https://composr-omega.vercel.app/
  - Composr is a markdown writer with real-time compiler for the web.

- https://github.com/openwebwork/pg-codemirror-editor /MIT/202410/ts
  - This package implements a CodeMirror 6 editor that is primarily intended for editing PG problem files for the WeBWorK Online Homework Delivery System. 
  - However, it also supports editing Perl, HTML, XML, Mojolicious HTML templates, and Mojolicious raw text templates since those are needed by webwork2.
  - https://github.com/openwebwork/codemirror-lang-pg /MIT
    - This package implements PG language support for the CodeMirror code editor.
    - PG is the problem generation language for the WeBWorK online homework delivery system.

- https://github.com/lhlyu/pure-editor /MIT/202302/ts/inactive
  - a pure editor developed using codemirror6

- https://github.com/RaspberryPiFoundation/editor-ui /apache2/202405/js
  - https://editor.raspberrypi.org/
  - Code Editor frontend
  - https://github.com/RaspberryPiFoundation/editor-api /AGPLv3/202405/ruby/python
    - https://editor.raspberrypi.org/
    - Code Editor backend

- https://github.com/ufuayk/hey-markdown /GPLv3/202410/js/分屏视图
  - https://ufuayk.github.io/hey-markdown
  - a powerful, lightweight Markdown editor built for simplicity and flexibility. 
  - This tool provides an intuitive interface to create and preview Markdown files side-by-side with useful formatting tools.
  - 依赖codemirror5

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
    - 🍴 forks
    - https://github.com/quadre-code/quadre /202409
# collab
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

- https://github.com/eclipse-oct/open-collaboration-tools /MIT/202408/ts
  - https://www.open-collab.tools/
  - ⚖️ Open Collaboration Tools: live-sharing solution for Eclipse Theia, VS Code and other editors and IDEs
  - This is how it works: one person starts a collaboration session as host and invites others to join. The IDE extension distributes the contents of the hostʼs workspace and highlights text selections and cursor positions of other participants. 
  - A public instance of the collaboration server is available at open-collab.tools.
  - [Announcing the Open Collaboration Tools | TypeFox _202407](https://www.typefox.io/blog/open-collaboration-tools-announcement/)
    - It's a collection of libraries and tools for live-sharing of IDE contents, designed to boost remote teamwork with open technologies.
    - The basic idea is simple: one person starts a collaboration session as host and invites others to join. The IDE extension distributes the contents of the hostʼs workspace and highlights text selections and cursor positions of other participants. 
    - A VS Code Extension available on Open VSX and the VS Code Marketplace

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

- https://github.com/JohnnyAir/codemirror-collab-extension /202401/ts/inactive
  - Real-time collaboration plugin for CodeMirror 6
  - 依赖@codemirror/collab, 依赖很少

- https://github.com/akashahmad/codemirror-collab-example-react /202406/ts
  - https://codemirror-collab-example-react.vercel.app/
  - React + TypeScript + Vite
  - 依赖@codemirror/collab
  - 前端2个编辑器协同，无后端

- https://github.com/MINERVA-MD/minerva /GPLv3/202302/ts/vue/inactive
  - Minerva is a simple, performant, and hackable Markdown editor that provides seamless GitHub integration and real-time collaboration.
  - 依赖codemirror6、@headlessui/vue、vue3
  - https://github.com/MINERVA-MD/minerva-core
  - https://github.com/MINERVA-MD/minerva-collab /GPLv3/202204/ts/inactive
    - 🔀 A socket server using the codemirror 6 collab library, allowing for real-time collaborative document editing.

- https://github.com/sahilatahar/Code-Sync /MIT/202409/ts
  - https://code-sync-live.vercel.app/
  - A real-time collaborative code editor featuring unique room generation, syntax highlighting, and auto-suggestions. 
  - 依赖@uiw/react-codemirror、react-split、tldraw2、socket.io
  - Users can seamlessly edit, save, and download files while communicating through group chat
  - Real-time collaboration on code editing across multiple files
  - Create, open, edit, save, delete, and organize files and folders
  - Code Execution: Users can execute the code directly within the collaboration environment, providing instant feedback and results.
  - Collaborative Drawing: Enable users to draw and sketch collaboratively in real-time

- https://github.com/YashNuhash/Realtime-Collaborative-Code-Editor

- https://github.com/streamich/collaborative-codemirror /202407/ts/inactive
  - Codemirror support for collaborative editing using JSON CRDT
  - Makes a plain Codemirror editor instance collaborative by binding it to a JSON CRDT document str node.
  - allows multiple users to edit the same document `json-joy` JSON CRDT document concurrently through the Codemirror editor.
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
- https://github.com/dinavinter/y-block /202407/ts
  - https://dinavinter.github.io/y-block/
  - YJS in custom elements, simple collabrative components powered by YJS.

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
- https://github.com/ekzhang/rustpad /MIT/202409/rust
  - https://rustpad.io/
  - an efficient and minimal open-source collaborative text editor based on the operational transformation algorithm. 
  - It lets users collaborate in real time while writing code in their browser. 
  - Rustpad is completely self-hosted and fits in a tiny Docker image, no database required.
  - client-side code communicates via WebSocket with a central server that stores in-memory data structures. 
    - The tradeoff is that documents are transient and lost between server restarts, or after 24 hours of inactivity
  - The server is written in Rust using the warp web server framework and the operational-transform library.
    - warp builds on top of hyper
  - We use wasm-bindgen to compile text operation logic to WebAssembly code, which runs in the browser. 
  - The frontend is written in TypeScript using React and interfaces with Monaco
  - [Rustpad is an efficient and minimal open-source collaborative text editor | Hacker News](https://news.ycombinator.com/item?id=41573866)

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

- https://github.com/YashNuhash/Realtime-Collaborative-Code-Editor /202504/ts
  - A Real-time Collaborative Code Editor built with Next.js, Socket.io & Express.js Which Provides a Range of Powerful Features Like Instant Code Synchronization While Code Changes to Across all the Users
  - Room-based Collaboration: Create or join coding rooms with unique room IDs

- https://github.com/AlbertArakelyan/collaborative-markdown-editor-example /MIT/202405/ts
  - Collaborative Markdown Editor built on modern and simple web technologies with markdown editing libraries integrations

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

- https://github.com/codersgyan/realtime-code-editor /202203/js
  - 依赖codemirror5、socket.io

- https://github.com/himanshugoyal77/codeSync-realtime-code-editor /202407/js
  - https://code-sync-realtime-coding.vercel.app/
  - Realtime code collaboration tool with code editor, compiler and realtime cursors
  - 依赖codemirror5, socket.io-client, react

- https://github.com/loro-dev/loro-codemirror /MIT/202505/ts
  - codemirror binding for loro
  - Sync cursors with Loro's Awareness and Cursor

## undo

- yjs undoManager支持selective undo

- https://github.com/ktsn/selective-undo-text /MIT/201612/ts/inactive
  - https://codepen.io/ktsn/pen/qZxdaY /示例使用codemirror5
  - A Selective Undo library for text editing
  - [Undo for selection/emacs · Issue · microsoft/vscode](https://github.com/microsoft/vscode/issues/108098)
    - When there is an active region, any use of undo performs selective undo: 
    - it undoes the most recent change within the region, instead of the entire buffer.

- [Undo/Redo | CKEditor 5 Documentation](https://ckeditor.com/docs/ckeditor5/latest/features/undo-redo.html)
  - The undo feature lets you withdraw recent changes to your content as well as bring them back. 
  - You can also selectively revert past changes, not just the latest ones.
  - The selective undo is heavily used in real-time collaboration environments. In such a scenario, a specific user should only be able to revert their changes, while keeping the changes made by other users intact

- [Undo (GNU Emacs Manual)](https://www.gnu.org/software/emacs/manual/html_node/emacs/Undo.html)
  - When there is an active region, any use of undo performs selective undo: it undoes the most recent change within the region, instead of the entire buffer

## diff

- diff视图
  - 上下版: 参考 BlazorCodeMirror6, code-editor-angular
  - 左右版: 参考 mdxeditor, jupyter-nbdime
  - cursor的代码修改使用了aider的codeblock diff格式
  - [Snapshot Compare extension | Tiptap Editor Docs](https://tiptap.dev/docs/collaboration/documents/snapshot-compare)

- https://github.com/lfnandoo/codemirror-merge-fork /MIT/202508/ts
  - Implement inverted effects in order to support undo/redo
  - https://github.com/AlpineX-Labs/codemirror-merge

- https://github.com/OrgFlow/codemirror-conflicts /MIT/202408/ts
  - A CodeMirror extension that displays Git conflict markers (`<<<<<<<` syntax) as side-by-side pieces of conflicting code, and provides an interface for accepting, copying, and deleting the chunks, with a top toolbar that shows information about remaining conflicts.
  - [Feasability Assessment: Extension to decorate conflict markers - v6 - discuss. CodeMirror _202407](https://discuss.codemirror.net/t/feasability-assessment-extension-to-decorate-conflict-markers/8459)

- https://github.com/acrodata/code-editor /MIT/202405/ts
  - https://acrodata.github.io/code-editor/
  - CodeMirror 6 wrapper for Angular
  - 实现了diff上下视图、✨左右视图，支持高亮变更内容及gutter，支持撤销变更action
  - 支持a2b/b2a正反向计算

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

- https://github.com/GerritCodeReview/plugins_codemirror-editor /apache2/202410/ts
  - A plugin that uses CodeMirror to provide a rich code editing experience in PolyGerrit.
  - The `codemirror-element` using CodeMirror is loaded lazily from another js bundle
  - https://github.com/GerritCodeReview/gerrit /java
    - Gerrit makes reviews easier by showing changes in a side-by-side display, and allowing inline comments to be added by any reviewer.

- https://github.com/jupyterlab/jupyterlab-git /BSD/202407/python/ts
  - A JupyterLab extension for version control using Git

- https://codepen.io/GwapongProgrammer/pen/yLXqWMK
  - 依赖codemirror6

- https://github.com/ngalaiko/codemirror-lang-diff /MIT/202304/ts/inactive
  - This is a CodeMirror 6 extension that adds support for `.diff` files syntax.

- https://github.com/codedownio/codemirror-compose-change /MIT/202306/ts/inactive
  - Compose two sequential CodeMirror changes, for v5

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

- https://github.com/Wilfred/difftastic /MIT/202408/rust
  - https://difftastic.wilfred.me.uk/
  - a structural diff tool that compares files based on their syntax
  - Difftastic supports over 30 programming languages
  - 🐛 issues
    - Difftastic output is intended for human consumption, and it does not generate patches that you can apply later. Use diff if you need a patch.
      - AST merging is a hard problem that difftastic does not address.
    - Difftastic scales relatively poorly on files with a large number of changes, and can use a lot of memory.
    - Difftastic has a side-by-side display which usually works well, but can be confusing.
    - Difftastic regularly has releases that fix crashes.

- https://github.com/personalizedrefrigerator/joplin-plugin-diff-tool /MIT/202407/ts
  - Diff and conflict resolution tool that supports Joplin Mobile

- https://konnorrogers.github.io/diff-view-element/components/diff-view-element/
  - A diff viewer complete with PrismJS for syntax highlighting

- https://github.com/hisashim/docdiff /BSD/202106/ruby
  - Compares two text files by word, by character, or by line

- https://github.com/github/semantic /202405/haskell
  - semantic is a Haskell library and command line tool for parsing, analyzing, and comparing source code
  - [How we parse source code into ASTs](https://github.com/github/semantic/blob/main/docs/why-tree-sitter.md)
  - Why we use tree-sitter
    - Reusability and ease of implementation
    - We want to parse all versions of a language
    - We parse comments and have them in the AST
    - Decoupled from a specific grammar format
    - Performance is decoupled from specific algorithm
    - There isn’t a universally accepted format for grammar specification
    - Language specifications are complex
    - Multiple algorithms for handling ambiguity. Precedence annotations at compile time, GLR at runtime
    - We have full control over the shape and productions of trees
    - Incremental parsing and error recovery
    - External scanner support. In case you need to parse a context-sensitive gramma
  - Drawbacks of tree-sitter
    - Error-recovery is sometimes opaque
    - External scanners also allow you to write custom C code for the purpose of handling lexical rules. This means running arbitrary C code
    - Though not unique to tree-sitter, grammar development is often a tedious task.
    - Convenient usage of a grammar often requires something like parser combinators, again tying the grammar specification to a single language. 
    - Generated C programs can be quite large.
    - Parsing can be extremely slow for pathological inputs such as infinite loops, sometimes taking hours and even days.
    - Support for unicode is currently lagging.

- https://github.com/so-fancy/diff-so-fancy /MIT/202505/perl
  - make your diffs human readable
  - Simply copy the `diff-so-fancy` script from the latest release into your `$PATH` and you're done.

- https://github.com/aazzroy/VersaDiff /MIT/202503/python/js/inactive
  - a modern open-source web app for comparing multiple code versions. 
  - Using Python, Flask, CodeMirror, and Bootstrap, it offers interactive editors, dynamic language support, and clear diff visualizations to help developers quickly analyze code changes.
  - Multi-Version Comparison: Compare between 2 to 5 versions of your code.
  - Diff Visualization: Generates clear, color-coded HTML diff tables using Python's `difflib`.

## lint

- https://github.com/duncanpierce/codemirror-reflector /MIT/202410/ts
  - https://duncanpierce.github.io/
  - Refactoring, smart navigation and code assistance for CodeMirror
  - Reflector is a CodeMirror extension that allows language packages to provide refactoring, code navigation and linting features.
  - It plugs into CodeMirror's Lint extension and uses it to display problems and suggestions it has found. It also provides Autocomplete suggestions using the identifiers that are in scope.

- https://github.com/3fuyang/zhlint-demo /202409/ts
  - https://zhlint-playground.netlify.app/
  - An intuitive playground for zhlint.
  - The diffing is provided by diff.

- https://github.com/KELs7/contracting-linting-codemirror6 /202405/ts
  - Demo: Contracting Linting in Codemirror6
  - Only few linting rules have been implemented
  - 示例lint python2代码

- https://github.com/azu/codemirror-textlint /MIT/202507/ts
  - https://azu.github.io/codemirror-textlint/
  - CodeMirror 6 integration with textlint using @textlint/kernel.
# extensions
- https://github.com/val-town/codemirror-ts /ISC/202503/ts
  - https://val-town.github.io/codemirror-ts/
  - a set of extensions for CodeMirror 6 that add support for TypeScript
  - [x] Autocomplete 
  - [x] Hover hints for types 
  - [x] Diagnostics (lints, in CodeMirror's terminology)
  - [x] Go-to definition, 🧐 未实现按住cmd/ctrl显示下划线
  - [x] Twoslash support
  - [x] ATA(automatic type acquisition): emulate what you'd get in a local editor
  - This uses `Comlink` as an abstraction for the WebWorker. 
  - 🧐 This module uses TypeScript’s public APIs to power its functionality: it doesn't use the Language Server Protocol
    - Most good TypeScript language tooling, like VS Code’s autocompletion, does not use the LSP specification. 
  - [Go to definition _202311](https://github.com/val-town/codemirror-ts/issues/8)
    - 👷202404: This module currently uses TypeScript, but not the extra language server. It'd probably use the language server if this adopted more of a client-server architecture, or maybe it should in general, but for now, it's integrating with TypeScript, and we'll need to figure out what's under the hood of the LSP adapter's implementation.
  - [Add recipe for remote node modules _202406](https://github.com/val-town/codemirror-ts/issues/27)
    - The answer to this is ata but the long answer is, whew, it's hard and we've poured days into improving type acquisition and it is still really tough. 
    - Making TypeScript and Deno get along is extremely hard - TypeScript doesn't support npm: or jsr: prefixes, doesn't support URLs for imports, etc. So you have to do a lot of arbitrary trickery to make the two get along.
    - 202502: Landed #57, which includes an example of ATA hooked into codemirror-ts

- https://github.com/modderme123/codemirror-extension-typescript /202310/ts/inactive
  - https://typescript-codemirror.netlify.app/
  - A codemirror extension providing useful features for typescript, such as a language server with autocomplete and error reporting
  - 纯前端的hover/autocomplete/lint
  - vite构建时会打包类型 `const types = import.meta.glob("../../../../node_modules/typescript/lib/*.d.ts", { eager: true, as: "raw" });`

- https://github.com/handlebauer/codemirror-extensions /202502/ts/inactive
  - A powerful set of sidebar extensions for CodeMirror 6 that adds file explorer and AI assistance capabilities to your editor. 
  - Sidebar Framework: A flexible and customizable sidebar system that can be docked to either side of the editor
  - File Explorer: A full-featured file explorer panel for navigating and managing your project files
  - AI Assistant: An intelligent coding assistant panel with support for multiple AI models

- https://github.com/exuanbo/codemirror-toolkit /MIT/202312/ts/侧重架构组织而弱功能
  - A batteries-included toolset for efficient development of CodeMirror 6 based editors (w/o React).
  - https://github.com/code4mk/codemirror-toolkit /202208/ts/inactive
    - easily use codemirror editor with codemirror-toolkit on react , vue , svelte
  - [@codemirror-toolkit/react - A small and flexible solution for binding CodeMirror 6 to React : r/reactjs _202301](https://www.reddit.com/r/reactjs/comments/107to4j/codemirrortoolkitreact_a_small_and_flexible/)
    - I always wanted to use such a library when I was developing my Assembler Simulator in React. 
    - But all I could find at the moment was like @uiw/react-codemirror, it's "badly written" (e.g. reading a ref's current value during rendering) and contains too many dependencies I don't need, which cannot be tree-shaked so that you can toggle them in props.
    - So I decided to write it my self and here it is! The API design is inspired by zustand btw

- https://github.com/yeliex/codemirror-extensions /MIT/202403/ts
  - https://cm.yeliex.dev/
  - codemirror extensions includes toolbar, helper, image-upload, event-emitter
  - codemirror-final-newline
  - codemirror-markdown-commands
  - codemirror-markdown-image
  - codemirror-toolbar 非浮动工具条

- https://github.com/overleaf/codemirror-tree-view /MIT/202311/ts
  - A CodeMirror 6 extension providing an interactive view of a document's syntax tree
  - ⛏ 更偏向于作为codemirror的devtools
  - https://github.com/overleaf/codemirror-autocomplete
- https://github.com/GamerGirlandCo/datacore-autocomplete
  - codemirror autocompletion for datacore

- https://github.com/overleaf/codemirror-search
  - https://github.com/GavinRigsby/codemirror-vscodeSearch /MIT/202504/ts
    - A VS Code style search and replace control for codemirror
    - built on top of the core @codemirror/search
    - Toggle options: Regex, Case Sensitivity, Whole Word
    - Fully integrated with CodeMirror's state and view systems

- https://github.com/GavinRigsby/codemirror-symboltree /MIT/202504/ts
  - extension that provides a Symbol Tree sidebar for visualizing the symbols in your code
  - It allows you to explore the structure of your code just like the Outline view in vscode
  - The sidebar displays a hierarchical tree of symbols (functions, classes, variables, etc.) with nesting, making it easier to navigate large codebases.
  - The extension leverages the Abstract Syntax Tree (AST) from any language extension used for syntax highlighting. 

- https://github.com/jmkng/sen /MIT/202310/ts
  - Simple, reusable CodeMirror (v6+) extensions: markdown bold, heading, block
  - The extensions are exported as functions that return an array of extensions that you can apply to your view.

- https://github.com/eivmosn/plugin-mirror /202311/ts
  - codemirror plugins

- https://github.com/saminzadeh/codemirror-extension-inline-suggestion /MIT/202402/ts
  - 👾 A CodeMirror extension to display inline suggestions
  - https://github.com/rizerphe/codemirror-companion-extension /MIT/202311/ts
    - a backward-compatible fork of saminzadeh's project that allows the user to display text different than that being accepted, and to instantly trigger the completion function upon accepting the previous completion.

- https://github.com/replit/codemirror-vscode-keymap /202212/ts/inactive
  - Ports VSCode's keyboard shortcuts to CodeMirror 6.

- https://github.com/replit/codemirror-indentation-markers /MIT/202403/ts
  - extension that renders indentation markers using a heuristic similar to what other popular editors, like Ace and Monaco, use.

- https://github.com/ShadowWolf308/codemirror-indent-wrapped-line /MIT/202406/ts
  - An extension to CodeMirror to indent wrapped newlines

- https://github.com/fauzi9331/codemirror-wrapped-line-indent /MIT/202403/ts
  - An extension for CodeMirror that adds indentation for wrapped lines.

- https://github.com/replit/Codemirror-CSS-color-picker /202310/ts
  - https://replit.com/@util/Codemirror-CSS-color-picker
  - extension that adds a color picker input next to CSS color values.

- https://github.com/emmetio/codemirror6-plugin /202408/ts/Emmet
  - CodeMirror 6 extension that adds Emmet support to text editor.
  - Emmet extension can track abbreviations that user enters in some known syntaxes like HTML and CSS. When abbreviation becomes complex (expands to more that one element), it displays abbreviation preview
  - Currently, CodeMirror API doesn’t provide viable option to get document syntax to allow plugins to understand how to work with document. So you have to specify document syntax manually in Emmet plugin.
  - Extension development is sponsored by Replit

- https://github.com/val-town/codemirror-continue /202401/ts
  - https://val-town.github.io/codemirror-continue/
  - Continue TypeScript/JavaScript block comments in CodeMirror

- https://github.com/luizzappa/codemirror-app-spreadsheet /202304/ts/inactive
  - https://luizzappa.github.io/codemirror-app-spreadsheet/
  - 📈 Excel formula editor
  - a demo implementation of the CodeMirror spreadsheet language package.
  - https://github.com/luizzappa/codemirror-lang-spreadsheet /MIT/202304/ts
    - Spreadsheet language support for CodeMirror

- https://github.com/personalizedrefrigerator/joplin-plugin-extra-editor-settings /MIT/202407/ts
  - This plugin exposes several CodeMirror 6 settings, including line numbers and code folding.

- https://github.com/andrebnassis/codemirror-readonly-ranges /202311/ts
  - https://andrebnassis.github.io/codemirror-readonly-ranges
  - Codemirror extension for read-only ranges
  - This library aims to help you dealing with read-only ranges on CodeMirror 6.

- https://github.com/WtecHtec/codemirror-placeholder-plugin
  - 可以创建可编辑的占位符区域

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

- https://github.com/cookshack/codemirror-bracket-matching /MIT/202503/ts
  - extension for highlighting matching brackets
  - Based on the builtin CodeMirror bracket matching, with two additional options for the config argument of bracketMatching: `directional/enclosing`

- https://github.com/eriknewland/rainbowbrackets /202304/js/inactive
  - https://codepengpt.netlify.app/
  - This is a working attempt at a rainbowBracket extension for CodeMirror6.

- https://github.com/cloudflypeng/codemirror-ext /202408/ts
  - an image upload plugin for CodeMirror that supports pasting or dragging and dropping images and uploading them to a server. 
  - allows using either a default fetch upload logic or custom upload logic.
  - feat: 添加 CodeMirror 的图片转换base64 插件
  - https://github.com/cloudflypeng/codemirror-upload

- https://github.com/ficristo/codemirror-addon-toggle-comment /MIT/202409/tsc
  - CodeMirror 5 does come with a comment addon, but I wanted to use the same algorithm used in Brackets
  - I ported the code related to commenting code from Brackets and experimented a bit, integrating features of the original one
# utils
- https://github.com/lume/code-mirror-el /MIT/202405/ts
  - https://codepen.io/trusktr/pen/poGZYOy?editors=1000
  - A customizeable `<code-mirror>` element that makes a code editor powered by CodeMirror 

- https://github.com/justinfagnani/codemirror-elements /MIT/202308/ts/inactive
  - A set of HTML custom elements for editing source code with CodeMirror.
  - Extensions are also HTML elements that you add as children of `<cm-editor>`

- https://github.com/flawiddsouza/code-mirror-custom-element /MIT/202312/js
  - https://flawiddsouza.github.io/code-mirror-custom-element/
  - CodeMirror 6 as a custom element (web component)
  - https://github.com/markwylde/codemirror-element

- https://github.com/0xdevalias/userscripts/tree/main/userscripts/github-gist-codemirror-resizer
  - Makes the CodeMirror editor resizable when creating/editing a gist on GitHub

- https://github.com/A99US/codemirror-6-snippetbuilder /MIT/202304/js
  - This is a function for CodeMirror 6 to convert a standard array of snippet (like this one) and turn it into snippet array that is ready to use in CodeMirror 6 extension.

- https://github.com/PuruVJ/neocodemirror /202407/ts/svelte
  - Aims to provide Codemirror 6 as an easy to use codemirror action.
  - https://x.com/puruvjdev/status/1780560310547436002
    - ⌛️ Anytime you change documentId, it stores the state in a map, and when the documentID changes back to the one stored, we apply the history

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

- https://github.com/hata6502/codemirror-view /202110/inactive
  - [Dynamic line height - discuss. CodeMirror _202106](https://discuss.codemirror.net/t/dynamic-line-height/3257)
  - I forked codemirror/view to hata6502/codemirror-view , and disabled viewport.
  - Disabling viewport may occur the performance issue, but it resolves the following scroll problem.

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
  - this is an editor for the Tidal language. It requires Tidal to be installed independently.
  - https://github.com/mindofmatthew/text.management/tree/main/packages/codemirror/evaluate
    - CodeMirror 6 extension for enabling lines of code to be evaluated

- https://github.com/Monkatraz/cm-tarnation /MPLv2/202207/ts/inactive
  - 🧮 An alternative parser for CodeMirror 6
  - Tarnation is not line-based. It is capable of reusing both previous and ahead data when parsing, making it fully incremental
  - Tarnation can do things that Lezer (the parser you'd usually use for CodeMirror) can't. For example, Tarnation can parse something like Markdown, and other weird esoteric markup/formatting languages.
  - [Showing off: cm-tarnation, an alternative parser - v6 - discuss. CodeMirror _202109](https://discuss.codemirror.net/t/showing-off-cm-tarnation-an-alternative-parser/3558)

- https://github.com/realdennis/md2pdf /MIT/202407/js
  - https://realdennis.github.io/md2pdf/
  - https://md2pdf.netlify.com/
  - Offline markdown to pdf, choose -> edit -> transform
- https://github.com/sahilatahar/markdown2pdf
  - An Impressive Markdown to PDF Converter

## utils-vscode

- https://github.com/samestep/codemirror-vscode /MIT/202504/ts
  - CodeMirror as a VS Code extension.
  - Use the Open in CodeMirror command (bound to ctrl+alt+c ctrl+alt+m by default) to open the current file in a new CodeMirror editor.

- https://github.com/JackieScorpio/convert-json-to-ts /MIT/202404/ts
  - use codemirror and vscode webview to achieve a vscode extension
  - Convert Json to Typescript

- https://github.com/greeenboi/vscodex /202402/ts/inactive
  - Vs code Clone
  - 依赖codemirror6、tauri
# lsp
- https://github.com/codemirror/lsp-client /MIT/202508/ts
  - Language server protocol client for CodeMirror
  - https://github.com/andy0130tw/codemirror-lsp-client-demo /202507/ts
    - Demo on wiring up tsserver with CodeMirror's lsp-client module

- https://github.com/FurqanSoftware/codemirror-languageserver /161Star/BSD/202502/ts/inactive
  - Language Server integration for CodeMirror6
  - This plugin enables code completion, hover tooltips, and linter functionality by connecting a CodeMirror 6 editor with a language server over WebSocket.
  - [feat: Transport agnostic _202205](https://github.com/FurqanSoftware/codemirror-languageserver/pull/13)
    - It now accepts any object implementing `Transport`. I have tried it with Event Emitter and WebSockets transports and both work fine
  - [Sharing lsp clients between multiple editors _202204](https://github.com/FurqanSoftware/codemirror-languageserver/issues/11)
    - I have added preliminary support for reusing the LSP client across multiple plugin instances.
  - 📝 [Using Language Servers with CodeMirror 6 _202103](https://hjr265.me/blog/codemirror-lsp/)
  - 🍴 forks
  - https://github.com/marimo-team/codemirror-languageserver /BSD/202504/ts
    - https://marimo-team.github.io/codemirror-languageserver/
    - a fork of FurqanSoftware/codemirror-languageserver with additional features and modernization.
    - ✨ Go to Definition - Jump to symbol definitions
    - Symbol Renaming - Smart symbol renaming across files
    - Hover Information - Rich documentation on hover
  - https://github.com/databutton/codemirror-languageserver /202309/ts
- https://github.com/guanyou-git/codemirror-react-test /202107/python/js/inactive
  - Dockerized codemirror6, pyls application
  - https://github.com/BX-Coding/python-lsp-server-docker
  - https://github.com/BX-Coding/patch-ide

- https://github.com/TypeFox/monaco-languageclient /MIT/202504/ts
  - monaco-languageclient to connect Monaco editor with language servers.
  - monaco-languageclient-examples provides the examples which allows to use them externally.
  - [Teaching the Language Server Protocol to Microsoft's Monaco Editor | TypeFox _201704](https://www.typefox.io/blog/teaching-the-language-server-protocol-to-microsofts-monaco-editor/)
  - [如何创建集成 LSP 支持多语言的 Web 代码编辑器 - 米开朗基杨 - 博客园 _202309](https://www.cnblogs.com/ryanyangcs/p/17693108.html)

- https://github.com/remcohaszing/codemirror-languageservice /MIT/202408/ts
  - https://codemirror-languageservice.js.org/
  - https://codemirror-languageservice.js.org/typescript
  - Integrate a Language Server Protocol compatible language service into CodeMirror6
  - 🌰 This demo shows how you can integrate an LSP based language service into CodeMirror.
    - The completion source autocompletes words based on the words in the document and the character typed.
    - The hover tooltip source shows a tooltip which displays the word you’re hovering over.
    - The lint source shows diagnostics for the words hint, info, warning, error, unnecessary, and deprecated.
  - Since LSP uses markdown, you need to provide a function to convert markdown to DOM. A good option is to combine hast-util-to-dom, mdast-util-from-markdown, and mdast-util-to-hast
  - codemirror-languageservice was developed as part of the Transloadit JSON editor.

- https://github.com/qualified/lsps /MIT/202206/ts/inactive
  - Use Language Servers with in-browser editors. 
  - Monorepo of **editor agnostic packages and CodeMirror5 client**.
  - ✨ 支持多种编辑器，示例使用CodeMirror5
  - 示例使用 lsp-ws-proxy ， 可参考配置方法
  - See examples/rust-analyzer to run this locally.
  - See examples/web-worker for an example with simple JSON Language Server running in Web Worker. A live demo is also available at https://qualified.github.io/lsps/.
  - [Codemirror v6 support? _202310](https://github.com/qualified/lsps/issues/109)
    - Are there any plans to integrate CodeMirror v6 support?
    - No, there's no plan to make this support CodeMirror v6 because the APIs are incompatible. It's probably easier to create a new project instead. 
    - I'm not sure if there are packages supporting multiple editors like ours, but I've seen a few packages providing Language Server support for CM6, so you might want to check them out.

- https://github.com/wylieconlon/lsp-editor-adapter /ISC/201911/ts/inactive
  - connect a CodeMirror document to a language server over WebSockets
  - 依赖codemirror5
  - 示例使用 jsonrpc-ws-proxy, 可参考配置方法，但使用的是旧版 javascript-typescript-langserver
  - https://github.com/wylieconlon/codemirror-lsp-example
    - CodeMirror connected to remotely-hosted language server over Web Socket
  - 🍴 forks
  - https://github.com/goorm-dev/lsp-editor-adapter /202111
  - https://github.com/krassowski/lsp-ws-connection /201910

- https://github.com/marc2332/lsp-codemirror /ISC/202008/ts/codemirror5
  - LSP integration for CodeMirror5
  - Support for custom autocompletion dropmenu
  - 依赖https://github.com/marc2332/node-jsonrpc-lsp, (based on https://github.com/wylieconlon/jsonrpc-ws-proxy, 而不是直接依赖vscode-jsonrpc)
  - 🍴 forks
  - https://github.com/lukehaas/lsp-codemirror /202503/ts/CodeMirror5
    - a more updated and better version of the original client
    - https://github.com/lukehaas/lsp-codemirror-debug

- https://github.com/jackhodkinson/lsp-editor /202407/ts/electron
  - A simple python code editor with code formatting and linting.
  - This is a toy experiment to show how to integrate the ruff language server into a code editor.
  - This editor is built with Electron, CodeMirror, and VS Code's language server client library.
  - [Integrating the ruff language server _202407](https://jack-hodkinson.medium.com/integrating-the-ruff-language-server-4f6b0d126ebd)
  - https://github.com/rice-cracker-dev/electron-codemirror-lua-example

- https://github.com/coder0107git/codemirror-web-workers-lsp-demo /202403/ts
  - https://codemirror-web-workers-lsp-demo.coder0107git.v6.rocks/
  - Demo of using a Web Worker LSP in CodeMirror 6， 示例是json格式
  - 实现了ipc通信/补全，未实现lint
  - 依赖codemirror-languageserver、@codemirror/lang-json、svelte4、svelte-codemirror-editor
  - This is a fork of https://gitlab.com/aedge/codemirror-web-workers-lsp-demo /202301

- https://github.com/ConorBobbleHat/codemirror-clangd-demo /202303/ts/inactive
  - https://conorbobblehat.github.io/codemirror-clangd-demo/
  - clangd, but in the browser

- https://github.com/AlecDivito/forge-editor /202503/ts
  - what if we had a editor in the browser that anyone could visit and just start programming. 
  - The "editor" would run on the server and use a LSP-like protocol to communicate between the client and the server using websockets. 
  - You need to setup redis, S3 server

- https://github.com/lbb00/codemirror-typespec /202409/js
  - This project is a demo of useing Typespec with Codemirror.
  - A Node.js server is running the Typespec compiler language server, connected via codemirror-languageserver, because the @typespec/compiler does not support browser environments.

- https://github.com/alanko0511/codemirror-editor-experiment
  - CodeMirror + TypeScript (experiment)

- https://github.com/okikio/codemirror/tree/lsp-dev /MIT/202110/ts/inactive
  - https://okikio-codemirror.netlify.app/
  - A minor test of Codemirror
  - https://x.com/SergeiChestakov/status/1486025274240090114
    - I now have a ~relatively~ functional lsp adapter for Codemirror 6, you may want to take a look. The main limitation is recreating a monaco esque environment for Codemirror, e.g. autocomplete doesn't work the same way on Codemirror that it did on Monaco
- https://github.com/hyrious/cm.ts /202401/ts/基于worker实现
  - Trying to integrate TypeScript language server in CodeMirror 6.

- https://github.com/SilasMarvin/lsp-ai /MIT/202501/rust
  - LSP-AI is an open source language server that serves as a backend for performing completion with large language models and soon other AI powered functionality. 
  - Because it is a language server, it works with any editor that has LSP support.
  - LSP-AI can work as an alternative to Github Copilot.
  - The goal of LSP-AI is to assist and empower software engineers by integrating with the tools they already know and love not replace software engineers.

- [@shopify/codemirror-language-client - npm](https://www.npmjs.com/package/@shopify/codemirror-language-client)
  - CodeMirror is the open source library that powers the Online Store Code Editor.

- https://github.com/schizobulia/ide-study /202310/js
  - [实现一个简单的ide-demo(未使用codemirror) - 知乎](https://zhuanlan.zhihu.com/p/659653723)
  - id为content的div为显示开发者的输入容器，cursor为光标组件
  - 先通过node开启一个websocket客户端与lsp-server通信，参考monaco中使用的pyright-langserver
  - 后端依赖vscode-ws-jsonrpc

- https://github.com/intansemc2/monaco-online-ide /MIT/202410/ts/svelte
  - This project is a webapp allow user to run code from browser in some languages, include python, c++, java, javascript, php.
  - This project uses Docker for easy deployment and high compatibility, but it can take a lot of storage
  - Run code in: python, c++, java, javascript, php
  - Svelte (SvelteKit): this is the framework for the front-end
  - Judge0: this is the back-end to run the code
  - Libraries: monaco-editor, monaco-languageclient, ...

- https://github.com/tbodt/js-langserver /202009/js/inactive
  - A simple language server for JavaScript, powered by ESLint and Tern.
  - I made this because sourcegraph/javascript-typescript-langserver is really bad at untyped JavaScript.
  - [Microsoft Language Server Protocol · Issue · ternjs/tern _201607](https://github.com/ternjs/tern/issues/799)
  - https://github.com/hsiaosiyuan0/vscode-ternjs
  - [Is Tern.js library in active development/support? _202208](https://github.com/ternjs/tern/issues/1051)
    - 👷: I'd recommend going with TypeScript (even if just running it on plain JavaScript) nowadays.
    - Brackets currently uses a webwoker to host tern and directly uses the is API.

- https://github.com/jupyter-lsp/jupyterlab-lsp /BSD/202503/ts/python
  - https://jupyterlab-lsp.readthedocs.io/
  - Coding assistance for JupyterLab (code navigation + hover suggestions + linters + autocompletion + rename) using Language Server Protocol
  - Jump to Definition and References
  - 依赖 JupyterLab >=4.1.0, <5.0.0a0, Python 3.9+
- https://github.com/krassowski/jupyterlab-go-to-definition /BSD/201908/ts/inactive
  - Navigate to variable's definition with a click in JupyterLab 
  - 依赖codemirror5、@jupyterlab/application.v1

- https://github.com/RahulBadenkal/ide /202410/ts/inactive
  - A real-time collaborative platform that combines a whiteboard, code editor and workspace sharing for seamless teamwork - all in one place
  - improving the editor capabilities by adding LSP support

- https://github.com/snuffyDev/svelte-language-server-web /MIT/202408/ts/inactive
  - https://svelte-language-server-web.vercel.app/
  - Svelte language server within a web worker.
  - Based on/inspired by: https://github.com/asafamr/monaco-svelte/
  - Editor-agnostic, use with Monaco, VSCode Web, CodeMirror...
  - Essentially this repo emulates Node.js wherever it can, otherwise it will just do a barebones shim so that 'it works'.

- https://github.com/dirkarnez/go-lsp-playground /202501/go
  - go-lsp-playground

## utils-lang

- https://github.com/codemirror/lang-markdown
  - Language support for GFM plus subscript, superscript, and emoji syntax.

- https://github.com/cookshack/codemirror-lang-csv /MIT/202411/js/inactive
  - Minimal CSV language package for CodeMirror 6, with basic rainbow highlighting.

- https://github.com/cookshack/codemirror-lang-lezer-tree /MIT/202409/js
  - Language support for Lezer trees, for CodeMirror 6
  - https://github.com/cookshack/codemirror-ruler
    - Draws a vertical line at a certain column

- https://github.com/zweifisch/lezer-ast-explorer /MIT/202308/ts
  - https://zweifisch.github.io/lezer-ast-explorer/
  - [I've made an AST explorer for lezer - discuss. CodeMirror _202308](https://discuss.codemirror.net/t/ive-made-an-ast-explorer-for-lezer/6986)

- https://github.com/mattmundell/codemirror-lang-git-log /MIT/202406/ts
  - https://git.sr.ht/~mattmundell/codemirror-lang-git-log
  - CodeMirror language for 'git log' output

- https://github.com/inspirnathan/codemirror-lang-mermaid /MIT/202309/ts
  - Mermaid language support for CodeMirror 6
  - This package implements Mermaid language support for the CodeMirror code editor. 
  - Get syntax highlighting for Mermaid diagrams

- https://github.com/eliasfeijo/codemirror-lang-ejs /MIT/202302/ts
  - EJS templating language implementation for CodeMirror v6

- https://github.com/orionlee/codemirror-js-mixed /MIT/202008/js/inactive
  - A language mode for CodeMirror, support highlighting HTML/CSS in javascript codes.

- https://github.com/n8n-io/codemirror-lang-n8n /MIT/202404/ts
  - n8n expression language support for CodeMirror 6

- https://github.com/neo4j/cypher-editor /apache2/202404/js
  - Codemirror editor for Cypher, with syntax awareness and auto-completion

- [CodeMirror extension to detect and fix missing JSX Pragma](https://gist.github.com/tmcw/fefe8b5c0a63b51bc8a303c8a3553fac)
  - detects the lack of a pragma and the presence of JSX syntax, by using CodeMirror's existing syntax tree

- https://github.com/Juexro/codemirror-iecst /MIT/202408/js
  - https://demo.jsmile.top/codemirror-iecst-editor
  - Structured Text language support, includes syntax highlight based on IEC 61131-3.
  - This package implements iecst language support for the CodeMirror code editor.
  - https://github.com/Juexro/livedemo

- https://github.com/eecavanna/monocle /202410/ts
  - https://eecavanna.github.io/monocle
  - Web-based visualizer for Makefiles
  - You can use it to view a Makefile as a graph of its targets and their dependencies—in your web browser.

- https://github.com/citedrive/lang-bibtex /MIT/202508/ts
  - BibTeX language support for the CodeMirror editor.
  - https://github.com/TeXlyre/codemirror-lang-bib

- https://github.com/xavierog/codemirror-mode-nginx-renewed
  - This is a CodeMirror mode that provides syntax highlighting for nginx configuration files.
# syntax-highlighting
- https://github.com/M-AnasGit/Codemirror-custom-highlighting /202410/ts
  - Using codemirror in react for custom syntax highlighting
  - This project demonstrates how to integrate CodeMirror into a React application and implement custom syntax highlighting. 
  - The example highlights any text wrapped in !{} with a specific style using CodeMirror's extensions API.
  - Uses `@uiw/react-codemirror` for seamless integration of CodeMirror with React.

- https://github.com/litingyes/shikimirror /MIT/202503/ts
  - Integrate Shiki into CodeMirror

- https://github.com/craftzdog/react-codemirror-runmode /MIT/202503/ts
  - Syntax highlighting for react, utilizing CodeMirror6's parser
  - It automatically loads the language metadata and dynamically loads language parser modules based on the specified language.

- https://github.com/highlightjs/highlight.js /24.5kStar/BSD/202507/js
  - https://highlightjs.org/
  - https://highlightjs.readthedocs.io/en/latest/readme.html
  - JavaScript syntax highlighter with language auto-detection and zero dependencies.
  - Compatible with any JS framework
  - It works in the browser as well as on the server.
  - 🆚 [Prism vs Highlight.js: Why choose one over the other? _202209](https://github.com/highlightjs/highlight.js/issues/3625)
    - automatic language detection
    - 👷 Neither library uses a simple lexer/tokenizer (that walks the code one character at a time).
      - Both parsers tokenize based on regex scanning.
      - Both can highlight operators/punctuation 
      - Both have line number plugins.
    - I think a major weakness of both syntax highlighters is they're based on regular expressions. Most if not all of the languages they highlight are not regular languages. They run into issues with things such as nesting.
    - A syntax highlighter having proper context-free parsers would be a major reason to prefer one over all others. An earley parser with grammar data for all supported languages, for example.
    - In the end, I chose Shiki, it's a heavier and slower highlighter, that's more suited for server-side rendering, rather than client-side.

- https://github.com/PrismJS/prism /12.7kStar/MIT/202506/ts
  - https://prismjs.com/
  - a lightweight, robust, and elegant syntax highlighting library. It's a spin-off project from Dabblet.
  - Supports parallelism with Web Workers, if available. 
  - 🧮 Regex-based so it *will* fail on certain edge cases, which are documented
  - [Roadmap for Prism v2 _202208](https://github.com/orgs/PrismJS/discussions/3531)
    - This is by far the most important change in v2: ES modules.
# code-playgrounds
- https://github.com/PotatoGroup/code-editor /ISC/202402/ts
  - a JS code editor based on codeMirror6, support code autoCompletion, which can be used with @astii/expression-sandbox
  - 依赖react
  - https://github.com/PotatoGroup/expression-sandbox /202309/ts
    - a simple sandbox for excute js expression

- https://github.com/mdn/bob /MIT/202407/ts
  - ✨ Builder of Bits aka The MDN Web Docs interactive examples, example builder
  - [Migrate to CodeMirror v6 _202208](https://github.com/mdn/bob/issues/851)
  - https://developer.mozilla.org/en-US/play
  - [Introducing the MDN Playground: Bring your code to life! | MDN Blog _202306](https://developer.mozilla.org/en-US/blog/introducing-the-mdn-playground/)
  - features: Instant prototyping, Live interaction, collaborative
  - We decided to go with CodeMirror. We considered Monaco, but decided for a more lightweight approach

- https://github.com/google/playground-elements /BSD/202409/ts/客户端执行
  - https://google.github.io/playground-elements/
  - Serverless coding environments for the web.
  - 依赖CodeMirror5
  - Playground never sends code to a backend server. Instead, Playground uses a Service Worker to create a virtual URL-space that runs 100% within the browser. If you can host static files, you can host a Playground.
  - Playground is broken up into small components like an editor, file picker, and preview. Mix-and-match components to create any layout you want
  - Playground uses a Web Worker to perform TypeScript compilation
  - Playground previews work by using a service worker.
  - 💡 use two iframes to the untrusted origin. One only loads untrusted code, the other loads a control API that talks to the trusted code. You can then to the loading into the iframe with a service worker. This is how the Playground Elements work
  - Some browsers such as Chrome are sometimes able to allocate a separate process or thread for iframes. This is highly desirable for Playground, because it improves responsiveness and prevents full lockups (resulting from e.g. an infinite loop accidentally written by a user).
  - Playground uses the `google_modes` CodeMirror syntax highlighting modes for TS/JS/HTML, because they support highlighting of HTML and CSS within JavaScript tagged template literals.
  - 🔲 Support for build plugins like JSX, SASS, and CSS modules are on the roadmap, but are not yet available.

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
  - 依赖codemirror6、solid-js1、typescript-language-server

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

- https://github.com/ronit-ghosh/Dev-Sandbox /202407/js
  - https://dev-sandbox-three.vercel.app/
  - A web application for rendering HTML, CSS, and JavaScript
  - https://x.com/ronit__ghosh/status/1817939216778850699
    - a web application designed to render HTML, CSS, and JavaScript. 
    - Built with React.js and used CodeMirror and react-codemirror2 for the code editor functionality, and Tailwind CSS for styling.

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

- https://github.com/live-codes/livecodes /933Star/MIT/202503/ts
  - https://livecodes.io/
  - 🛝 A feature-rich, open-source, client-side code playground for React, Vue, Svelte, Solid, Typescript, Python, Go, Ruby, PHP and 80+ languages/frameworks.
  - 依赖codemirror6、monaco-editor、codejar、codejar、yjs
  - 代码编辑器依赖 monaco-editor, Monaco editor is used on desktop, CodeMirror is used on mobile and CodeJar is used in codeblocks, in lite mode and in readonly playgrounds.
  - Powerful SDK (available for vanilla JavaScript, TypeScript, React, Vue and Svelte)
  - No servers to configure 
  - No databases to maintain 
  - Use modules from npm, deno.land/x, jsr, GitHub, and others
  - SDK provides an easy, yet powerful, interface to embed and communicate with LiveCodes playgrounds.
    - SDK methods allow programmatic communication and control of the playgrounds during runtime.
  - [Improve Vue support  _202503](https://github.com/live-codes/livecodes/issues/757)
    - Please note that LiveCodes does not allow having a file system. It only has 3 editors (markup, style and script) which when combined produce the result page. 
    - This is similar to CodePen and JSFiddle and unlike CodeSandbox and StackBlitz.
    - This is not an issue with other frameworks like React and Solid since they use functions (or classes) as components and a single file can have many of these. In Vue (and Svelte) the SFC format allows only 1 component per file.
  - [Programmatic engine? _202301](https://github.com/live-codes/livecodes/issues/294)
    - there is quite a powerful SDK that allows embedding and communicating with playgrounds and provides lots of configuration options.
    - the officially supported headless mode
  - [Would it be possible to use a locally run LLM instead of Codeium, e.g. via Ollama? _202504](https://github.com/orgs/live-codes/discussions/784)
    - The codeium integration is currently achieved using: Monaco editor: Monaco Codeium Provider, which is a fork of the codeium official codeium-react-code-editor
    - So to use another backend server (including a local one), you will have to provide the same API and change the URL to it. This is not currently in my scope.
    - If you need to modify these, you will have to fork the projects, make your modifications and then re-publish them as new packages which can then be used instead of the original ones. The real problem you are trying to solve are not modifying these. The actual problem is providing the code suggestions in the same format that the codeium server does. The actual codeium backend server running the AI models is not open-source.
    - this is not easily done. :( Thank you for the explanations
  - https://x.com/hatem_hosny_/status/1753930554540499064
    - Check this where I dynamically select the editor and load it (e.g. on desktop -> monaco, on mobile -> codemirror, user preference, etc.)
    - Also unified the interface of loading and communicating with the editor
  - [Why Another Playground? | LiveCodes](https://livecodes.io/docs/why/)
    - There are great products like CodePen, JSFiddle, JS Bin, CodeSandbox, Replit and many others, which LiveCodes does not aim to replace or compete with.
    - On the contrary, it aims to integrate with as many of these services as their APIs allow.
    - All processing and code transformations run in the browser on the client-side.
    - The LiveCodes app (standalone or self-hosted) can be embedded in any web page.
  - [Introducing LiveCodes _202308](https://blog.livecodes.io/introducing-livecodes/)
    - All processing and code transformations run in the browser on the client-side. 
    - On mobile, a lighter-weight touch-friendly code editor (CodeMirror 6) is used

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

- https://github.com/cookshack/bred /CC0-1.0/202504/js
  - I'm playing with CodeMirror, Monaco and Ace inside Electron.

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
  - 依赖monaco-editor

- https://github.com/rin-yato/miracle-diagram /202312/ts/inactive
  - https://miracle-diagram.vercel.app/
  - A code first database diagram design tool. 
  - 依赖codemirror6、lezer、shadcn、reactflow、dexie
  - 功能似乎无法正常使用

- https://github.com/ShankarDutta/codecraft-webapp /MIT/202508/ts
  - https://codecraft-v1.netlify.app/
  - CodeCraft is a frontend code playground built with React, Next.js, CodeMirror, and shadcn/ui. 
  - It lets users write and preview HTML, CSS, and JavaScript in real time
  - Built with technologies like Next.js, React, @uiw/react-codemirror, and Tailwind CSS

- https://github.com/BaseMax/MarkdownLiveEditor /202411/js
  - Real-time Markdown editor with live preview support, automatic scrolling synchronization and full support for right-to-left (RTL) languages. Built using CodeMirror and Marked.js.

- https://github.com/sumeetgodse/code-snippet-runner /202411/js
  - https://code-snippet-runner.netlify.app/
  - A snipper runner built with CodeMirror5 & React that can run HTML, CSS, JS

- https://github.com/kazzkiq/CodeFlask /MIT/202006/js/inactive
  - https://kazzkiq.github.io/CodeFlask/
  - A micro code-editor for awesome web pages
  - 依赖prismjs

- https://github.com/codepod-io/codepod /MIT/202311/ts/inactive
  - Codepod provides the interactive coding experience popularized by Jupyter, but with scalability and production-readiness
  - 画板上的代码沙盒，使用monaco而不是codemirror

- https://github.com/gravity-ui/markdown-editor /MIT/202408/js
  - An implementation of "codemirror.net" designed for easy access to coding for kids and schools

- https://github.com/thexeromin/webcode /202408/ts
  - https://webcode-client.netlify.app/
  - a web-based C compiler and terminal, allowing you to write, compile, and run C code directly in your browser with no installation needed.

- https://github.com/rxliuli/typescript-console /MIT/202409/ts/svelte
  - Run and debug TypeScript code in the Chrome DevTools
  - 依赖@swc/wasm-web、esbuild-wasm、bits-ui

- code-play
  - https://github.com/xorazmiy-dev/code-mirror /js

- https://github.com/val-town/playground /MIT/202505/ts
  - This repository provides a React component that you can use to embed an interactive coding playground on a website that uses Val Town to execute code.
  - `<Playground env={{ YOUR_API_KEY: 'something' }} code="console.log(1);" workerPath="/public/worker.ts" />`

## playgrounds

- playground-examples
  - https://arktype.io/playground

- https://github.com/vercel/satori /MPLv2/202411/ts
  - https://og-playground.vercel.app/
  - Enlightened library to convert HTML and CSS to SVG
  - ✨ 提供了支持可视化配置的playground
  - 不支持html字符串渲染和dangerouslySetInnerHTML
  - What if there’s a `<Satori>` component that adds fluid layout & style transitions to your elements?

- https://github.com/divriots/universal-story-render /202205/ts/inactive
  - Universal story renderer, compatible with most JS UI frameworks out there.

## repl

- https://github.com/rspack-contrib/rspack-repl /202508/ts
  - https://repl.rspack.rs/
  - The REPL for Rspack based on @rspack/browser.
  - https://x.com/WhoKnow50498590/status/1952523801092403358
    - rspack/browser means bundle on the browser side?
    - Yep, run rspack build in your browser
# starter
- https://github.com/nothingislost/obsidian-cm6-attributes /202112/ts/inactive
  - This reference plugin implements a ViewPlugin which will parse the markdown syntaxTree and add various Decorations to enhance the editor.

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

- https://github.com/yuanyxh/codemirror-demo /202410/ts
  - 复制了codemirror的各源码包作为普通的文件夹，未使用npm包
  - @vitejs/plugin-react uses Babel for Fast Refresh
  - @vitejs/plugin-react-swc uses SWC for Fast Refresh

- https://github.com/datacamp/codemirror-6-getting-started /202102/js
  - Getting started with CodeMirror 6, the popular code editor library
  - [Getting started with the new CodeMirror 6 | DataCamp Engineering _202102](https://blog.datacamp.engineering/codemirror-6-getting-started-7fd08f467ed2)

- https://github.com/load1n9/codemirror /MIT/202410/ts
  - This is a simple wrapper around the codemirror editor for use with Preact for deno.
  - Completely stolen from react-codemirror and adapted to Preact

- https://github.com/codepen/CodeMirror-6-Needs /202208/js/inactive
  - https://objective-blackwell-d4efc9.netlify.app/
  - An exploration of CodeMirror 6 to integrate everything 🏭 CodePen needs to use it in the future.
  - It's a Next.js app as that is the context we hope to be using CodeMirror 6 in.
  - 提供了yjs示例

- https://github.com/craftzdog/electron-markdown-editor-tutorial /MIT/202108/ts/inactive
  - A tutorial for building a beautiful Markdown editor
  - electron + vite + CodeMirror 6 + remark
  - [How to build a Markdown editor using Electron, ReactJS, Vite, CodeMirror, and Remark - YouTube ](https://www.youtube.com/watch?v=gxBis8EgoAg)

- https://github.com/Bilal-Belli/Basic-IDE /MIT/202403/js
  - This is a basic Desktop IDE made using ElectronJS NodeJS CodeMirror and JsTree, jquery
- https://github.com/RAGHAV-N5/CodeIt /202312/js
  - a React Project with NodeJs and expressJs using CodeMirror5 and compilex libraries

- https://github.com/pelevesque/codemirror_implementations /202407/js
  - A collection of Code Mirror implementations.

- https://github.com/GiorgiKumelashvili/codemirror-6-playground /202407/ts
  - Nextjs Shadcn Codemirror 6 Examples

- examples
  - [editor | calculang metal](https://finding-calculang-foc.netlify.app/editor)

- https://github.com/PlayerMiller109/obsidian-cm-decorations /202408/js
  - a codemirror 6 learning case in Obsidian, create static and dynamic decorations

- https://github.com/enibook/enibook /MIT/202404/js/inactive
  - https://enibook.github.io/enibook/
  - Collection of educational components in the form of custom HTML elements
# examples
- https://github.com/ralismark/ibis-wiki /202406/ts
  - http://www.ralismark.xyz/ibis-wiki/
  - personal wiki, built to fit a personal niche, inspired by the likes of TiddlyWiki and Logseq
  - This wiki is a purely static site, and does not have its own backend
  - 依赖codemirror6、wink-nlp
  - 实现了diff上下视图，The merge plugin doesn't really have a way to have it conditionally enabled -- it has to be always enabled.
  - notes are stored via an external storage provider -- the only kind supported at the moment is S3-like
  - there are [[internal-links]] a la Roam Research, 类似双链
  - https://github.com/ralismark/ibis-wiki/blob/main/src/codemirror/merge.ts

- https://github.com/alexwkleung/Iris /MIT/202312/ts/inactive
  - https://irisnotes.vercel.app/
  - A comfortable note-taking app powered by Markdown
  - 依赖codemirror6、prosemirror、markdown-it、electron-window-state、remark-gfm

- https://github.com/brunodavi/quick-planner /202409/ts
  - https://quick-planner.vercel.app/
  - a fast calendar routine generator
  - export ics to Import into any calendar

- https://github.com/Hussseinkizz/writter-desktop /202506/ts
  - The fully offline-first desktop minimalistic markdown editor for your notes and thoughts

- https://github.com/BruceHong666/xwsitch-v3 /MIT/202508/ts
  - A modern HTTP request forwarding and debugging tool for developers, built with React, TypeScript, and Manifest V3.
  - This project is deeply inspired by [xswitch](https://github.com/yize/xswitch)
  - Why Rewrite: With the release of Chrome Extension Manifest V3, the classic xswitch extension can no longer run properly in modern browsers 

- https://github.com/danielgolden/volon /202408/ts/vue
  - https://volon.app/
  - a plain text, markdown-focused, local-first notes app with text-editing keyboard shortcuts

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

- https://github.com/surrealdb/codemirror /apache2/202408/ts/js
  - This library provides full support for the SurrealQL language within your CodeMirror editors.
  - https://github.com/surrealdb/surrealist /MIT/202408/ts
    - https://surrealist.app/
    - Surrealist is the ultimate way to visually manage your SurrealDB database. 
    - Effortlessly connect to any SurrealDB database and execute queries
    - 依赖codemirror、tauri
    - The Surrealist web app provides a fully functional database management experience with support for multiple connections and an integrated sandbox environment.

- https://github.com/GaganpreetKaurKalsi/SQL-Editor /202206/js/inactive
  - https://sql-editor-react.vercel.app/sql-editor
  - A frontend application for running SQL queries.
  - Note : For now only SELECT queries on given tables are supported. Will increase it's application in future.

- https://github.com/aidenlx/cm-chs-patch /MIT/202405/ts
  - 增加 Obsidian 内置编辑器的(简体)中文分词支持，使得编辑模式的双击可以选中中文，以及在 Vim 模式下可以按中文分词移动光标
  - 从 v1.8.0 开始，默认分词引擎由结巴分词更换为系统自带分词引擎，结巴分词不再是必备组件
  - 手动安装结巴分词组件：在设置中启用结巴分词后，从CDN下载得到 jieba_rs_wasm_bg.wasm 文件，将 wasm 文件放在 Obsidian 库的 .obsidian 或者其它指定的配置文件夹下后重启 Obsidian

- https://github.com/prisma/text-editors /apache2/202211/ts/inactive
  - https://qc.prisma-adp.vercel.app/
  - these editors were built for the Prisma Data Platform's Query Console
  - This is only a demo of Prisma's text editors. To try out the query console, head over to the Prisma Data Platform

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

- https://github.com/yerlantemir/vimracing /202308/ts/inactive
  - Vimracing is a minimalistic vim arena. It allows you to compete on code refactoring speed by using vim hotkeys.

- https://github.com/fregante/GhostText /MIT/202408/js
  - https://ghosttext.fregante.com/
  - Use your text editor to write in your browser. Everything you type in the editor will be instantly updated in the browser (and vice versa).
  - 提供了浏览器插件和ide插件

- https://github.com/librogamesland/magebook /MIT/202401/ts/inactive
  - https://magebook.github.io/
  - A web editor for gamebook writing
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
  - I love CodePen. I like it so much I decided to see what it would

- https://github.com/darrowv/JsLogs /202310/js
  - https://darrowv.github.io/JsLogs/
  - Online JS Code Console

- https://github.com/worktile/ng-codemirror /202408/ts
  - codemirror component for Angular（^8.0+）
  - 依赖codemirror5、ng-zorro-antd、rxjs
  - support all options by codemirror（^5.52.0）.

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
    - Cloud Commander file manager for the web with console and editor

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

- https://github.com/github/codemirror-contrib /archived
  - CodeMirror community contributions as used by GitHub.
# pm-code-docs/notebook
- https://github.com/srcbookdev/srcbook /apache2/202408/ts
  - https://srcbook.com/
  - TypeScript & JavaScript notebooks.
  - Create, run, and share reproducible programs and ideas
  - Export to valid markdown format (.src.md)
  - Local execution with a web interface
  - Powered by Node.js

- https://github.com/expressive-code/expressive-code /MIT/202507/ts/不依赖codemirror
  - https://expressive-code.com/
  - https://expressive-code.com/key-features/text-markers/
  - A text marking & annotation engine for presenting source code on the web
  - 通过配置可在codeblock高亮指定行、指定文本
  - Expressive Code is an engine for presenting source code on the web, aiming to make your code easy to understand and visually stunning.
  - On top of accurate syntax highlighting powered by the same engine as VS Code, Expressive Code allows you to annotate code blocks using text markers, diff highlighting, code editor & terminal window frames, and more.
    - @expressive-code/plugin-shiki - Adds syntax highlighting to your code blocks, using the same engine as VS Code.
  - All annotations are based on a powerful plugin architecture 
  - Zero dependencies on React, Vue, or any other front-end framework.
    - Works with popular site generators like Astro and Next.js, as well as plain markdown and MDX

- Starboard Notebook /889Star/MPLv2/202206/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.
  - 编辑器已分离，基于rich-markdown-editor和prosemirror、codemirror6
  - 前端基于lit

- https://github.com/wagmi-dev/vocs /MIT/202408/ts
  - https://vocs.dev/
  - Minimal Documentation Framework, powered by React + Vite
  - Vocs is a minimal static documentation generator designed to supercharge your documentation workflow
  - Write your content in Markdown or MDX, and Vocs will generate a static site with a default theme.
  - Code Snippets in Vocs come in two forms: a virtual file snippet in your Markdown code (Virtual File Snippets), or a physical file snippet in your file system (Physical File Snippets)
  - [Twoslash – Vocs](https://vocs.dev/docs/guides/twoslash)
    - TypeScript Twoslash can be seen as a pre-processor that enhances your code-samples. It is a markup language for JavaScript and TypeScript.
    - It leverages the compiler APIs used by text editors to offer type-driven hover information, precise error messages, and type callouts.

- https://github.com/difizen/libro /MIT/202409/ts
  - https://libro.difizen.net/
  - 大模型时代的 notebook 产品方案, 灵活定制、轻松集成的 Notebook 产品方案
  - 定义大模型工作流，内置大模型交互和辅助开发能力
  - 更优雅的交互体验，兼容 jupyter notebook
  - 可以在自己的工作流中使用 prompt cell，快速完成与大模型的交互，生成的结果也可以在上下文中继续访问
  - 支持 Cell 级别的版本 Diff 能力，方便更好的进行版本管理、CR
  - https://github.com/difizen/libro-server /202404/python
    - 基于 jupyter-server 开发
    - 您至少需要安装 jupyter-server 来支持 libro 运行，此时您可以使用 jupyter notebook 的能力，如果需要使用更多 libro 定义的能力，您需要安装 libro-server。
    - 使用 rye 来管理多 python 包组成 monorepo，多个包会共享同一个虚拟环境 venv

- https://github.com/dralletje/Notebook-Experiments /202304/ts/js/inactive
  - http://lezer-playground.vercel.app/
  - Notebook Experiments for Notebook Scientists
  - Experimenting with all things codemirror. A product that is housed in this repo is Lezer Playground.

- https://github.com/shahenalgoo/snippad /MIT/202306/ts/inactive
  - https://www.snippad.io/
  - open-source code snippet & notebook app for developers.
  - It is a web/cloud based open-source application made in React/Next.js that you can easily deploy on Appwrite and Vercel for free.
  - 依赖tiptap、appwrite
# pm-coding-ai
- https://github.com/asadm/codemirror-copilot /MIT/202401/ts/inactive
  - https://copilot.asadmemon.com/
  - CodeMirror extension to add GPT autocompletion like GitHub's Copilot
  - This code is based on codemirror-extension-inline-suggestion

- https://github.com/continuedev/continue /21.3kStar/apache2/202508/ts
  - https://docs.continue.dev/
  - Continue is the leading open-source AI code assistant. You can connect any models and any context to build custom autocomplete and chat experiences inside VS Code and JetBrains
  - Tab to autocomplete code suggestions
  - [Continue 实现原理 · Pines-Cheng/blog _202505](https://github.com/Pines-Cheng/blog/issues/108)

- https://github.com/useScriba/useScriba /202308/ts
  - https://docs.usescriba.com/
  - Highly customizable AI completion plugin for web-based code editors.

- https://github.com/mattelim/text-gpt-p5-app /MIT/202311/js
  - https://text-gpt-p5.vercel.app/
  - A text to p5.js generative editor powered by GPT-3.5
  - react-codemirror
  - A Next.js full-stack app (React, Next API routes).

- https://github.com/sourcegraph/cody /2kStar/apache2/202405/ts
  - https://cody.dev/
  - https://sourcegraph.com/cody
  - Cody is a free, open-source AI coding assistant that can write and fix code, provide AI-generated autocomplete, and answer your coding questions. 
  - Cody fetches relevant code context from across your entire codebase to write better code that uses more of your codebase's APIs, impls, and idioms, with less hallucination.
  - Cody is currently in Beta and available for VS Code and JetBrains.
  - 👣 Swappable LLMs: Support for Anthropic Claude, Claude 2, and OpenAI GPT-4/3.5, with more coming soon.
  - You can use Cody Free or Cody Pro when Codying on your work code.
  - Cody is available for VS Code, JetBrains, and on the web.

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

- https://github.com/e2b-dev/code-interpreter /apache2/202407/python/ts
  - https://e2b.dev/
  - 🧊 Python & JS/TS SDK for adding code interpreting to your AI app
  - The code interpreter runs inside the E2B Sandbox - an open-source secure sandbox made for running untrusted AI-generated code and AI agents.
  - https://github.com/e2b-dev/e2b /apache2/202407/python/ts
    - Secure open source cloud runtime for AI apps & AI agents
    - The E2B sandbox can be connected to any LLM and any AI agent or app.
  - https://github.com/e2b-dev/infra /apache2/202408/go
    - Infrastructure powering E2B - Secure Runtime for AI Agents & Apps
    - there are several components written in Go and a Terraform configuration for the deployment.
  - [Self-hosting E2B on Google Cloud](https://github.com/e2b-dev/infra/blob/main/self-host.md)
    - 🧐 Supported cloud providers: GCP (wip: AWS, Azure, General linux machine)
    - We ask for Terraform v1.5.x because starting from v1.6 Terraform switched their license from Mozilla Public License to Business Source License.
    - PostgreSQL database (Supabase's DB only supported for now)
    - E2B is using Firecracker for Sandboxes. You can build your own kernel and Firecracker version from source by running make build-and-upload-fc-components
  - [E2B Code Interpreter Sandbox _202311](https://medium.com/e-two-b/e2b-sandbox-bb146264f4c4)
    - You can create your own Custom Sandboxes for different purposes, from data analysis through AI internet browsing to very popular code execution.
    - The E2B Code Interpreter Sandbox is just a sandbox — without any LLM “connected” to it. 
    - Our Sandbox can be controlled with SDK (run_code, install_pkg, create_file, etc) and gives you the freedom to connect it to (any) LLM.
    - OpenAI Code Interpreter is controlled by talking to an AI assistant.

- https://github.com/Exafunction/codeium-react-code-editor /MIT/202402/ts/inactive
  - https://codeium.com/playground
  - open-source code editor as a React component with unlimited AI autocomplete. 
  - Brought to you by the team at Codeium. Free with no account required.
  - Customizable API extended from Monaco React

- https://github.com/buildownai/buddy /CC-NC/202410/ts/vue
  - https://buildown.ai/
  - 👨🏻‍🏫 AI driven IDE in the browser - Showcase from the book: Build Your Own AI
  - a demonstration application showcasing how to build an AI-driven solution in TypeScript, leveraging Ollama 

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

- https://github.com/hiterusrk/codemirror.next /202009/ts
  - This code is dual-licensed under the MIT and GPL-v3 licenses
