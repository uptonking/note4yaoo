---
title: lib-editor-codemirror-examples
tags: [code-editor, codemirror, examples]
created: 2023-06-23T12:46:36.949Z
modified: 2023-06-23T12:46:53.288Z
---

# lib-editor-codemirror-examples

# guide

# popular
- https://github.com/tmcw/awesome-codemirror
  - Awesome CodeMirror plugins, themes, wrappers, and more

- https://github.com/replit/codemirror-minimap /202401/ts
  - Minimap extension for Codemirror 6

- https://github.com/replit/codemirror-interact /202403/ts
  - https://replit.com/@util/codemirror-interact
  - A CodeMirror extension that lets you interact with different values (clicking, dragging, etc).

- https://github.com/val-town/codemirror-codeium /ISC/202404/ts
  - https://val-town.github.io/codemirror-codeium/
  - Codeium code completion integration for CodeMirror 6
  - 🤖 Copilot-like ghost text code from modeling-app by Jess Frazelle and based on Cursor.

- https://github.com/expressive-code/expressive-code /ts
  - Expressive Code is an engine for presenting source code on the web, aiming to make your code easy to understand and visually stunning.
  - On top of accurate syntax highlighting powered by the same engine as VS Code, Expressive Code allows you to annotate code blocks using text markers, diff highlighting, code editor & terminal window frames, and more.
  - All annotations are based on a powerful plugin architecture 

- https://github.com/exuanbo/codemirror-toolkit /MIT/202312/ts
  - A batteries-included toolset for efficient development of CodeMirror 6 based editors (w/o React).

- https://github.com/sachinraja/rodemirror /MIT/202112/ts/inactive
  - React component for CodeMirror 6
  - Efficient, only renders when necessary and uses StateEffect to update the editor state on prop changes. The view and state are never recreated.

- https://github.com/azu/codemirror-console /202404/js
  - https://codemirror-console.netlify.com/
  - Web Console UI for JavaScript.
  - 依赖codemirror5、in-browser-language

- https://github.com/uiwjs/react-markdown-editor /MIT/202404/ts
  - https://uiwjs.github.io/react-markdown-editor
  - A markdown editor with preview, implemented with React.js and TypeScript.
  - 依赖codemirror6、@uiw/react-markdown-preview、highlight.js

- https://github.com/uiwjs/react-md-editor /MIT/202403/ts
  - https://uiwjs.github.io/react-md-editor
  - A simple markdown editor with preview, implemented with React.js and TypeScript.
  - This is based on `textarea` encapsulation, so it does not depend on any modern code editors such as Acs, CodeMirror, Monaco etc.
  - 依赖rehype-prism-plus、@uiw/react-markdown-preview

- https://github.com/uiwjs/react-codemirror /MIT/202404/ts
  - https://uiwjs.github.io/react-codemirror/
  - CodeMirror 6 component for React
  - Versions after @uiw/react-codemirror@v4 use codemirror 6.
  - The bundled version supports use directly in the browser
  - Support theme customization, provide theme editor.

- https://github.com/scniro/react-codemirror2 /MIT/202108/ts/v5/inactive
  - https://scniro.github.io/react-codemirror2/
  - ships with the notion of an uncontrolled and controlled component

- https://github.com/rennzhang/codemirror-editor-vue3 /MIT/202204/ts
  - https://rennzhang.github.io/codemirror-editor-vue3
  - CodeMirror component for Vue3
  - https://github.com/cloudacy/vue-markdown-edit /202112/ts
    - simple markdown editor based on CodeMirror built for VueJS.
  - https://github.com/logue/vue-codemirror6
    - @codemirror 6 component for @vuejs. Vue2 & Vue3 both supported.
  - https://github.com/leon-kfd/OnlineCodeEditor /202311/ts/vue
    - An online code Editor like CodePen, built by Vue3.
- https://github.com/surmon-china/vue-codemirror /MIT/202208/ts/vue/inactive
  - @codemirror code editor component for @vuejs
  - a new version based on CodeMirror@6 and is available to Vue3 only.

- https://github.com/getcursor/old /MIT/202304/ts/inactive
  - A Codemirror-based editor with many modern need-to-haves (e.g. LSP, Copilot, Vim, Remote SSH)
  - This is an old version of Cursor based off of the Codemirror text editing component. If you're looking to build your own code editor from the ground-up, this may serve as a useful guide. Cursor is now based on a fork of VSCodium.
  - 依赖codemirror6、@headlessui/react、@reduxjs/toolkit、electron-store、markdown-it、vscode-languageserver-protocol、xterm、xterm-addon-search
  - AI Features: auto-generated inline diffs and completions, a ChatGPT-style embedded chat, on-hover documentation suggestions

- https://github.com/0xsuk/agitcms /MIT/202212/ts/inactive
  - A hackable headless CMS for markdown blogs
  - Agit CMS is a simple web frontend interface that utilizes filesystem to manage markdown/media contents. Built for markdown-based static site generators, like Hugo and Jekyll.
  - 依赖codemirror6、mui5、remark-gfm、remark-parse、xterm

- https://github.com/neo4j/cypher-editor /apache2/202404/js
  - Codemirror editor for Cypher, with syntax awareness and auto-completion

- https://github.com/Jisuanke/CodeMirror-Record /202112/js/inactive
  - https://codemirror-record.haoranyu.com/
  - https://codemirror-record.haoranyu.com/demo/
  - ⌛️ It is a project for recording and playing back activities in the CodeMirror 5 editor and the surrounding environment
  - version 6.x is not yet supported by this library.

- https://github.com/sibiraj-s/prosemirror-codemirror-6 /MIT/202206/ts/inactive
  - https://sibiraj-s.github.io/prosemirror-codemirror-6/
  - Prosemirror with Codemirror 6 (demo)
  - Based on the example from https://prosemirror.net/examples/codemirror/. This is just an example setup and might not be very reusable. Use this to get something up-and-running quickly.
# editors-based-on-codemirror
- https://github.com/davidmyersdev/ink-mde /MIT/202404/ts
  - A beautiful, modern, customizable Markdown editor powered by CodeMirror 6 and TypeScript
  - This is the editor that powers https://octo.app.
  - Inline Markdown image previews
  - Framework agnostic, 支持vue/svelte
  - Supports Server-Side Rendering (SSR)
  - Wrap a native `textarea` element with the `wrap` export
  - Plugin API (experimental)

- https://github.com/retronav/ixora /apache2/202305/ts/inactive
  - a CodeMirror 6 extension pack to make writing Markdown fun and beautiful.
  - Auto link detection
  - https://codeberg.org/retronav/ixora

- https://github.com/madeyoga/chunchunmaru-mde /MIT/202207/ts/inactive
  - https://madeyoga.github.io/chunchunmaru-mde/
  - Markdown editor based on codemirror 6

- https://github.com/segphault/codemirror-rich-markdoc /202301/ts/inactive
  - https://markdoc-hybrid-editor.netlify.app/
  - This is a plugin for CodeMirror 6 that adds a hybrid rich-text editing mode for Markdown content. 
  - This is a plugin for CodeMirror 6 that adds a hybrid rich-text editing mode for Markdown content. 
  - This plugin is inspired by HyperMD, a CodeMirror 5 rich Markdown plugin that is no longer actively maintained. This plugin is written from scratch and does not use any existing HyperMD code, but it aims to bring similar functionality to CodeMirror 6.

- https://github.com/fuermosi777/markword /202403/ts
  - A WYSIWYG markdown extension set for Codemirror 6.

- https://github.com/asciidoctor/codemirror-asciidoc /BSD/202112/js/inactive
  - AsciiDoc mode for CodeMirror
  - Usage for CM5 with codemirror-asciidoc@1.x
  - Usage for CM6 with codemirror-asciidoc@2.x

- https://github.com/dyq086/formula-editor /202303/ts/vue/inactive
  - 基于vue3+codeMirror 6 公式表达式编辑器

- https://github.com/chordbook/editor /GPLv3/202404/ts
  - https://chordbook.github.io/editor/
  - A web-based editor for editing chord sheets in the ChordPro format, built on CodeMirror.
  - ChordPro, a simple text format for the notation of lyrics with chords. Although initially intended for guitarists, it can be used for all kinds of musical purposes.

- https://github.com/warmachine028/markdown-editor /MIT/202202/ts/inactive
  - A markdown editor using Electron, ReactJS, Vite, CodeMirror6, and Remark

- https://github.com/croxydeveloper/croxy-editor /202309/js/inactive
  - Minimal code editor made with Nextron (Next. JS + Electron) and CodeMirror

- https://github.com/For-0/simple-text-editor /MIT/202307/ts/inactive
  - https://editor.forzero.vocabustudy.org/
  - a text editor for the web
  - 依赖codemirror6、bulma、idb
# collab
- https://github.com/BjornTheProgrammer/react-codemirror-collab-sockets /MIT/202306/ts/inactive
  - An example of a react-codemirror implementation of the codemirror collab package, with cursor and multiple document examples.
  - 依赖codemirror6、@uiw/react-codemirror、@uiw/react-codemirror
  - 未使用ot和crdt

- https://github.com/codemirror/collab /MIT/202309/ts
  - Collaborative editing for the CodeMirror code editor

- https://github.com/yjs/y-codemirror.next /MIT/202403/js
  - https://demos.yjs.dev/codemirror/codemirror.html
  - Collaborative extensions for CodeMirror6
  - This binding binds a `Y.Text` to a CodeMirror editor.
  - Awareness: Render remote selection ranges and cursors - as a separate plugin
  - Shared Undo/Redo (each client has its own undo-/redo-history) - as a separate plugin

- https://github.com/ekzhang/rushlight /MIT/202306/ts/inactive  
  - https://github.com/ekzhang/cm-collab /ts
  - A tiny collaborative Markdown editor based on CodeMirror, communicating with a minimal server and database.
  - Make collaborative code editors that run on your own infrastructure: just Redis and a database.
  - Supports multiple real-time documents, with live cursors. 
  - 🔀 Based on CodeMirror 6 and operational transformation, so all changes are resolved by server code.
  - The backend is stateless, and you can bring your own transport; even a single HTTP handler is enough.
  - Unlike most toy examples, Rushlight supports persistence in any durable database you choose. Real-time updates are replicated in-memory by Redis, with automatic log compaction.

- https://github.com/vizhub-core/codemirror-ot /MIT/202403/js
  - Real-time collaboration plugin for CodeMirror 6.
  - Overhauled in May 2022 to work with the latest CodeMirror 6 APIs and JSON1. A fully functioning collaborative editor that leverages this library can be found in VZCode.
  - At its core this library is a translator between Operational Transformation and CodeMirror 6. This is one piece of the puzzle for enabling real-time collaboration on text documents using CodeMirror and ShareDB.

- https://github.com/qwikcollab/qwikcollab /202306/ts/inactive
  - https://qwikcollab.netlify.app/
  - open source collaborative code editor you have been searching for
  - Qwikcollab uses operational transformation for managing document versions when multiple people edit it, it uses codemirror which is an extensible code editor package and also helps in merging changes from different clients. The changes are transferred using websockets.

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

- https://github.com/automerge/automerge-codemirror /202404/ts
  -  adds collaborative editing to codemirror using automerge-repo
- https://github.com/aslakhellesoy/automerge-codemirror /MIT/202005/ts
  - brings collaborative editing to CodeMirror by linking it to an `Automerge.Text` object
  - 依赖codemirror5、automerge.v0.14

- https://github.com/abhishekashyap/codeRigade /MIT/202005/js/inactive
  - https://coderigade.netlify.app/
  - Realtime collaborative code-editor
  - 依赖codemirror5、socket.io-client

- https://github.com/chakri68/codeCollab /202306/js
  - A simple code editor to share code and collab with other developers
# extensions
- https://github.com/FurqanSoftware/codemirror-languageserver /161Star/BSD/202212/ts/inactive
  - Language Server integration for CodeMirror 6
  - This plugin enables code completion, hover tooltips, and linter functionality by connecting a CodeMirror 6 editor with a language server over WebSocket.
  - [Using Language Servers with CodeMirror 6 _202103](https://hjr265.me/blog/codemirror-lsp/)

- https://github.com/qualified/lsps /MIT/202206/ts/inactive
  - Use Language Servers with in-browser editors. 
  - Monorepo of editor agnostic packages and CodeMirror client.

- https://github.com/marc2332/lsp-codemirror /ISC/202008/ts/inactive
  - LSP integration for CodeMirror

- https://github.com/val-town/codemirror-ts /ISC/202402/ts
  - https://val-town.github.io/codemirror-ts/
  - a set of extensions for CodeMirror 6 that add support for TypeScript.
  - Hover hints for types 
  - Autocomplete 
  - Diagnostics (lints, in CodeMirror's terminology)

- https://github.com/replit/codemirror-vscode-keymap /202212/ts/inactive
  - Ports VSCode's keyboard shortcuts to CodeMirror 6.

- https://github.com/replit/codemirror-indentation-markers /MIT/202403/ts
  - extension that renders indentation markers using a heuristic similar to what other popular editors, like Ace and Monaco, use.

- https://github.com/replit/Codemirror-CSS-color-picker /202310/ts
  - https://replit.com/@util/Codemirror-CSS-color-picker
  - extension that adds a color picker input next to CSS color values.

- https://github.com/asadm/codemirror-copilot /MIT/202401/ts
  - https://copilot.asadmemon.com/
  - CodeMirror extension to add GPT autocompletion like GitHub's Copilot

- https://github.com/useScriba/useScriba /202308/ts
  - https://docs.usescriba.com/
  - Highly customizable AI completion plugin for web-based code editors.

- https://github.com/saminzadeh/codemirror-extension-inline-suggestion /MIT/202402/ts
  - A CodeMirror extension to display inline suggestions

- https://github.com/emmetio/codemirror6-plugin /202404/ts
  - CodeMirror 6 extension that adds Emmet support to text editor.
  - Extension development is sponsored by Replit

- https://github.com/luizzappa/codemirror-app-spreadsheet /202304/ts/inactive
  - https://luizzappa.github.io/codemirror-app-spreadsheet/
  - a demo implementation of the CodeMirror spreadsheet language package.
  - https://github.com/luizzappa/codemirror-lang-spreadsheet /202304/ts
    - Spreadsheet language support for CodeMirror

- https://github.com/andrebnassis/codemirror-readonly-ranges /202311/ts
  - https://andrebnassis.github.io/codemirror-readonly-ranges
  - Codemirror extension for read-only ranges
  - This library aims to help you dealing with read-only ranges on CodeMirror 6.

- https://github.com/modderme123/codemirror-extension-typescript /202312/ts/inactive
  - A codemirror extension providing useful features for typescript, such as a language server with autocomplete and error reporting

- https://github.com/dimfeld/codemirror-json5 /202306/ts
  - This package implements JSON5 support for Codemirror 6.
# utils
- https://github.com/lume/code-mirror-el /MIT/202405/ts
  - https://codepen.io/trusktr/pen/poGZYOy?editors=1000
  - A customizeable `<code-mirror>` element that makes a code editor powered by CodeMirror 

- https://github.com/justinfagnani/codemirror-elements /MIT/202308/ts/inactive
  - A set of HTML custom elements for editing source code with CodeMirror.

- https://github.com/flawiddsouza/code-mirror-custom-element /202312/js
  - https://flawiddsouza.github.io/code-mirror-custom-element/
  - CodeMirror 6 as a custom element (web component)
  - https://github.com/markwylde/codemirror-element

- https://github.com/PuruVJ/neocodemirror /202311/ts
  - Aims to provide Codemirror 6 as an easy to use codemirror action.

- https://github.com/acao/codemirror-json-schema /MIT/202404/ts
  - Codemirror 6 extensions that provide full JSON Schema support for @codemirror/lang-json & codemirror-json5 language modes

- https://github.com/val-town/codemirror-continue /202401/ts
  - https://val-town.github.io/codemirror-continue/
  - Continue TypeScript/JavaScript block comments in CodeMirror

- https://github.com/thetrevorharmon/zephyr-demo /202402/ts
  - https://zephyr-demo.netlify.app/
  - CodeMirror 6 🤝 ANTLR
- https://github.com/RuslanZh/codemirror-antlr4 /202208/ts/inactive
  - This project shows example of integration Antlr 4 grammar tool with Codemirror editor.

- https://github.com/Gk0Wk/TW5-CodeMirror-Enhanced /MIT/202305/ts/inactive
  - https://gk0wk.github.io/TW5-CodeMirror-Enhanced/
  - An enhanced for CodeMirror framework in TiddlyWiki, including TW5 highlight, WikiLink auto-completion, expandable hint, snippets, etc.
  - 为 TiddlyWiki5 的 CodeMirror 编辑器实现一个灵活而丰富的扩展框架，包括 TiddlyWiki5(text/vnd.tiddlywiki)语法高亮、Wiki 链接自动补全、可点击链接、Tiddler 预览等功能。更多功能(语法树、语法补全、所见即所得模式、快捷模板输入等)正在开发中。本框架是开源框架，欢迎任何人加入开发，框架文档正在编写中。
  - https://github.com/BurningTreeC/tiddlywiki-codemirror-6 /202403/js
    - https://burningtreec.github.io/tiddlywiki-codemirror-6/
    - The plugin adds the CodeMirror 6 editor to TiddlyWiki
  - https://github.com/oeyoews/tiddlywiki-codemirror6

- https://github.com/wikimedia/mediawiki-extensions-CodeMirror /202405/js
  - MediaWiki extension CodeMirror

- https://github.com/BrianHung/tldraw-yjs /202402/ts
  - https://canvas-yjs.vercel.app/
  - An example of using tldraw together with yjs with codemirror and prosemirror.

- https://github.com/google/codemirror.dart /BSD/202403/dart
  - A Dart wrapper around the CodeMirror text editor
# code-playgrounds
- https://github.com/munshkr/flok /GPLv3/202404/ts
  - https://flok.cc/
  - Web-based P2P collaborative editor for live coding sounds and images
  - Similar to Etherpad, but focused on code evaluation for livecoding.
  - REPL plugins: allows user to locally evaluate code from interpreters (like Haskell, Ruby, Python, etc.)
  - Web Plugins, for languages embedded in editor
  - Use CodeMirror 6
  - Use Yjs for collaborative editor
  - nice to have Import external JS libraries dynamically, instead of bundling them with Flok
# starter
- https://github.com/RPGillespie6/codemirror-quickstart /202402/js
  - Quickstart guide and examples for those who prefer a more hands on approach to bootstrapping CodeMirror 6

- https://github.com/datacamp/codemirror-6-getting-started /202102/js
  - Getting started with CodeMirror 6, the popular code editor library

- https://github.com/codepen/CodeMirror-6-Needs /202208/js/inactive
  - https://objective-blackwell-d4efc9.netlify.app/
  - An exploration of CodeMirror 6 to integrate everything CodePen needs to use it in the future.
  - It's a Next.js app as that is the context we hope to be using CodeMirror 6 in.
  - 提供了yjs示例

- https://github.com/craftzdog/electron-markdown-editor-tutorial /MIT/202108/ts/inactive
  - A tutorial for building a beautiful Markdown editor
  - electron + vite + CodeMirror 6 + remark

- https://github.com/greeenboi/vscodex /202402/ts
  - Vs code Clone
  - 依赖codemirror6、tauri
# examples
- https://github.com/alexwkleung/Iris /MIT/202312/ts/inactive
  - https://irisnotes.vercel.app/
  - A comfortable note-taking app powered by Markdown
  - 依赖codemirror6、prosemirror、markdown-it、electron-window-state、remark-gfm

- https://github.com/onderonur/code-image-generator /GPLv3/202404/ts
  - https://onderonur.github.io/code-image-generator/
  - Create your code images by choosing different themes and visual settings.
  - Next.js

- https://github.com/wajeshubham/snippng /MIT/202306/ts/inactive
  - https://snippng.wajeshubham.in/
  - Create and share beautiful images of your source code.
  - 依赖@uiw/react-codemirror、firebase、next

- https://github.com/vizhub-core/vzcode /MIT/202405/ts
  - VZCode: Multiplayer Code Editor
  - VZCode offers a multiplayer code editing environment that caters to a real-time collaborative development experience. It's the code editor component of VizHub, and can also be used independently from VizHub.
  - Browser-based editing environment
  - Real-time collaboration via LAN or using services like NGrok
  - A known shortcoming of VZCode is that it does not (yet) watch for changes from the file system. VZCode assumes that no other programs are modifying the same files.
  - You can also expose your VZCode instance publicly using a tunneling service such as NGrok.
  - Auto-save, debounced after code changes
  - https://github.com/vizhub-core/vizhub
    - https://vizhub.community/
    - Self Hosted CMS for Web-based Dataviz
    - VizHub 2 has been used in Data Visualization Course 2018, Datavis 2020
    - iFrame-based code execution environment.
  - VizHub 3
    - possible to self-host your own instance
    - possible to extend the core with plugins

- https://github.com/aidenlx/cm-chs-patch /MIT/202405/ts
  - 增加 Obsidian 内置编辑器的(简体)中文分词支持，使得编辑模式的双击可以选中中文，以及在 Vim 模式下可以按中文分词移动光标
  - 从 v1.8.0 开始，默认分词引擎由结巴分词更换为系统自带分词引擎，结巴分词不再是必备组件
  - 手动安装结巴分词组件：在设置中启用结巴分词后，从CDN下载得到 jieba_rs_wasm_bg.wasm 文件，将 wasm 文件放在 Obsidian 库的 .obsidian 或者其它指定的配置文件夹下后重启 Obsidian

- https://github.com/do-me/SemanticFinder /MIT/202405/js
  - https://do-me.github.io/SemanticFinder/
  - frontend-only live semantic search with transformers.js
  - Calculates the embeddings and cosine similarity client-side without server-side inferencing, using transformers.js and latest SOTA embedding models from Huggingface.

- https://github.com/mattelim/text-gpt-p5-app /MIT/202311/js
  - A text to p5.js generative editor powered by GPT-3.5
  - react-codemirror

- https://github.com/GaganpreetKaurKalsi/SQL-Editor /202206/js/inactive
  - https://sql-editor-react.vercel.app/sql-editor
  - A frontend application for running SQL queries.
  - Note : For now only SELECT queries on given tables are supported. Will increase it's application in future.

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
# diff
- https://github.com/MrWangJustToDo/git-diff-view /MIT/202404/ts
  - https://mrwangjusttodo.github.io/git-diff-view/
  - A Diff View component for React/Vue, just like Github
  - core只依赖lowlight, 不依赖codemirror
  - https://github.com/wooorm/lowlight /MIT/202310/js
    - Virtual syntax highlighting for virtual DOMs and non-HTML things
    - This package uses `highlight.js` for syntax highlighting and outputs objects (ASTs) instead of a string of HTML.
    - This package is useful when you want to perform syntax highlighting in a place where serialized HTML wouldn’t work or wouldn’t work well. 
    - You can use the similar `refractor` if you want to use `Prism` grammars instead. 
    - If you’re looking for a really good (but rather heavy) alternative, use `starry-night`.
# theme
- https://github.com/nodetec/mirrorshades /GPLv3/202403/ts
  - A react library to create themes for codemirror
  - I mostly made this to support the fat cursor in used in codemirror-vim, but it can be used to create any theme for codemirror.

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

- https://github.com/vadimdemedes/thememirror /202206/ts
  - Beautiful themes for CodeMirror

- https://github.com/cossssmin/codemirror-theme-github /202102
  - A CodeMirror theme inspired by the GitHub editor.
# v5
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

- https://github.com/starwiz-7/codestream /MIT/202204/js/inactive
  - https://codestream.vercel.app/
  - A web app for users to collaborate while solving a coding problem
  - 依赖codemirror5、katex

- https://github.com/inducer/edit-on-web /202403/python/js
  - Edit files in a local directory through a web browser (using CodeMirror5)

- https://github.com/Yash-Singh1/monkeyide /MIT/202105/js
  - A lightweight multi-tab IDE based on CodeMirror
# more
- https://github.com/datavis-tech/codearea /MIT/201908/js
  - A proof-of-concept code editor with syntax highlighting that uses
    - highlighted-pre-over-textarea approach (like react-simple-code-editor)
    - web-tree-sitter for incremental parsing
    - `diff-match-patch` via `json0-ot-diff` for computing text diffs (needed for using tree-sitter)
    - React for DOM updates
