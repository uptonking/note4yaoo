---
title: lib-editor-codemirror-examples
tags: [code-editor, codemirror, examples]
created: 2023-06-23T12:46:36.949Z
modified: 2023-06-23T12:46:53.288Z
---

# lib-editor-codemirror-examples

# guide

- fans-codemirror
  - https://github.com/yeliex/codemirror-extensions
  - https://github.com/val-town/codemirror-ts 
  - https://github.com/exuanbo/codemirror-toolkit
  - https://github.com/uiwjs/react-codemirror
  - https://www.npmjs.com/package/collaborative-codemirror
  - https://news.ycombinator.com/threads?id=CompuIves
# popular
- https://github.com/tmcw/awesome-codemirror
  - Awesome CodeMirror plugins, themes, wrappers, and more

- https://github.com/milahu/browserforge /202303
  - run github + github-pages + codesandbox in your browser, offline-first - CONCEPT

- https://github.com/codesandbox/sandpack /4.5kStar/apache2/202405/ts
  - https://sandpack.codesandbox.io/
  - https://sandpack.codesandbox.io/docs
  - Sandpack is a component toolkit for creating your own live running code editing experience powered by CodeSandbox.
  - sandpack-react依赖codemirror6、lz-string、react-devtools-inline
  - sandpack-client依赖nodebox、static-browser-server
  - CodeEditor支持codemirror/monaco/vscode
  - 提供了很多示例，包括cm-DecoratorsDynamic/FileExplorer/ReactDevTools
  - Sandpack Client: This is a small foundation package that sits on top of the bundler. It is framework agnostic and facilitates the handshake between your context and the bundler iframe.
  - Sandpack React: React components that give you the power of editable sandboxes that run in the browser
  - https://github.com/AaronPowell96/sandpack-file-explorer /MIT/202312/ts
    - Enhanced File Explorer for Sandpack. Providing immense flexibility to Sandpack's capabilities.
  - https://github.com/codeamigo/codeamigo /GPLv3/202401/ts/inactive
    - codeamigo is a platform that helps people learn to code with an AI assistant.
    - 依赖express、apollo-server、graphql、next.js、postgresql、redis

- https://github.com/jupyterlab/jupyterlab/tree/main/packages/codemirror /202405/ts
  - A JupyterLab package which provides the default implementation of the `@jupyterlab/codeeditor` interface, using the `CodeMirror` editor.
  - https://github.com/jupyterlab/jupyterlab/tree/main/packages/codemirror-extension
    - A JupyterLab package which provides an entry point, commands, and keyboard shortcuts for the `@jupyterlab/codemirror` package.
  - https://github.com/jupyterlab/jupyterlab/tree/main/packages/codeeditor
    - A JupyterLab package which defines an abstract interface to a code editor, which is used in many places in the application, including cells and the file editor.
  - https://github.com/jupyterlab/jupyterlab-monaco /BSD/201807/ts/archived
    - A JupyterLab extension providing the Monaco editor.
  - [Explore monaco editor integration · jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab/issues/135)
  - [Update Codemirror to version 6 _202106](https://github.com/jupyterlab/jupyterlab/issues/10370)
  - https://github.com/jupyter/nbdime
    - Tools for diffing and merging of Jupyter notebooks.

- https://github.com/sourcegraph/openctx/tree/main/client/codemirror /apache2/202405/ts
  - https://openctx.org/playground
  - implements a CodeMirror extension that shows OpenCtx items in the editor.

- overleaf /12.6kStar/AGPLv3/202405/js/latex/ace>codemirror
  - https://github.com/overleaf/overleaf
  - https://github.com/overleaf/overleaf/wiki
  - https://github.com/overleaf/overleaf/tree/main/services/web/frontend/js/features/source-editor
  - A web-based collaborative LaTeX editor
  - source-editor支持codemirror6、ace
  - https://github.com/overleaf/ace /Ajax.org Cloud9 Editor
  - [Compile Error and PDF Download Notifications](https://github.com/overleaf/overleaf/issues/1031)
    - migrate from ACE to CodeMirror 6. Yes, the CM6 work will be coming to CE soon. _202206

- https://github.com/yuku/textcomplete /MIT/202312/ts
  - https://yuku.takahashi.coffee/textcomplete/
  - Autocomplete for HTMLTextAreaElement and more
  - 支持 textarea/contenteditable/codemirror

- https://github.com/minditor/minditor /MIT/202403/ts
  - https://minditor.dev/
  - A plug-and-play, highly customizable block-based rich text editor. 
  - Supports block/inlineBlock development with any framework, including React/Vue.
  - 依赖codemirror6、eventemitter3、thememirror、@uppy/xhr-upload
  - Minditor 目前由 Zhenyu Hou 独立开发和维护

- https://github.com/replit/codemirror-minimap /202401/ts
  - Minimap extension for Codemirror 6

- https://github.com/replit/codemirror-interact /202403/ts
  - https://replit.com/@util/codemirror-interact
  - A CodeMirror extension that lets you interact with different values (clicking, dragging, etc).

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

- https://github.com/val-town/codemirror-codeium /ISC/202404/ts
  - https://val-town.github.io/codemirror-codeium/
  - Codeium code completion integration for CodeMirror 6
  - 🤖 Copilot-like ghost text code from modeling-app by Jess Frazelle and based on Cursor.

- https://github.com/exuanbo/codemirror-toolkit /MIT/202312/ts
  - A batteries-included toolset for efficient development of CodeMirror 6 based editors (w/o React).
  - https://github.com/code4mk/codemirror-toolkit /202208/ts/inactive
    - easily use codemirror editor with codemirror-toolkit on react , vue , svelte

- https://github.com/sachinraja/rodemirror /MIT/202112/ts/inactive
  - React component for CodeMirror 6
  - Efficient, only renders when necessary and uses StateEffect to update the editor state on prop changes. The view and state are never recreated.
  - https://github.com/atassis/react-codemirror-ts /MIT/202206/ts/inactive
    - Codemirror react wrapper made with typescript

- https://github.com/azu/codemirror-console /202404/js
  - https://codemirror-console.netlify.com/
  - Web Console UI for JavaScript.
  - 依赖codemirror5、in-browser-language

- https://github.com/uiwjs/react-markdown-editor /MIT/202404/ts
  - https://uiwjs.github.io/react-markdown-editor
  - A markdown editor with preview, implemented with React.js and TypeScript.
  - 依赖@uiw/react-codemirror、@uiw/react-markdown-preview

- https://github.com/uiwjs/react-codemirror /MIT/202404/ts
  - https://uiwjs.github.io/react-codemirror/
  - https://uiwjs.github.io/react-codemirror/#/merge/document
  - CodeMirror 6 component for React
  - Versions after `@uiw/react-codemirror@v4` use codemirror 6.
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
  - https://uiwjs.github.io/react-code-preview
  - Code edit preview for React
  - 编辑代码时立刻刷新预览

- https://github.com/phartenfeller/react-readonly-codemirror6 /MIT/202402/js
  - https://phartenfeller.github.io/react-readonly-codemirror6/
  - I use this component for server-side generated code previews (with Gatsby). It uses Codemirror 6 which is currently in preview.

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

- https://github.com/surmon-china/vue-codemirror /MIT/202208/ts/vue/inactive
  - @codemirror code editor component for @vuejs
  - a new version based on CodeMirror@6 and is available to Vue3 only.

- https://github.com/getcursor/old /MIT/202304/ts/inactive
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

- https://github.com/jamischarles/codemirror-server-render /202302/js/inactive
  - Renders CodeMirror 6 syntax highlighting as a string so you can use it at build time (ie: blog) or server-side
- https://github.com/readmeio/codemirror-node /ISC/202202/js/inactive
  - CodeMirror on the server
  - 依赖codemirror5

- https://github.com/glacambre/editor-adapter /MIT/202211/ts/inactive
  - A library to interact with in-browser JS editors like Ace, CodeMirror or Monaco

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

- https://github.com/expressive-code/expressive-code /MIT/202405/ts/不依赖codemirror
  - https://expressive-code.com/
  - A text marking & annotation engine for presenting source code on the web
  - Expressive Code is an engine for presenting source code on the web, aiming to make your code easy to understand and visually stunning.
  - On top of accurate syntax highlighting powered by the same engine as VS Code, Expressive Code allows you to annotate code blocks using text markers, diff highlighting, code editor & terminal window frames, and more.
  - All annotations are based on a powerful plugin architecture 
# editors-based-on-codemirror
- https://github.com/tagspaces/tagspaces-common/tree/develop/packages/tagspaces-codemirror /MIT/202312/ts
  - 依赖codemirror6

- https://github.com/davidmyersdev/ink-mde /MIT/202404/ts
  - A beautiful, modern, customizable Markdown editor powered by CodeMirror 6 and TypeScript
  - This is the editor that powers https://octo.app.
  - Inline Markdown image previews
  - Framework agnostic, 支持vue/svelte
  - Supports Server-Side Rendering (SSR)
  - Wrap a native `textarea` element with the `wrap` export
  - Plugin API (experimental)

- https://github.com/sanity-io/code-input /MIT/202404/ts
  - Sanity input component for code, powered by CodeMirror

- https://github.com/mongodb-js/compass/blob/main/packages/compass-editor/package.json /SSPL/202404/ts
  - Reusable Compass editor component based on codemirror editor, themes, and autocompleters
  - 依赖codemirror6、react

- https://github.com/yanthink/pingfan.ts /202204/ts/inactive
  - 基于 codemirror6 的 markdown 编辑器

- https://github.com/scalar/scalar/tree/main/packages/use-codemirror /202305/ts
  - CodeMirror + vue3

- https://github.com/lakejs/lake-codemirror /MIT/202404/ts
  - https://lakejs.org/
  - This package provides a CodeMirror configuration for Lake
  - Code block基于codemirror实现

- https://github.com/emberry-org/lemon-editor /GPLv3/202208/ts/inactive
  - a Rich Text Editor build upon Codemirror for the Emberry client.

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

- https://github.com/prevwong/reka.js/tree/main/packages/react-code-editor /202404/ts
  - Codemirror editor for editing Reka AST in code

- https://github.com/dyq086/formula-editor /202303/ts/vue/inactive
  - 基于vue3+codeMirror 6 公式表达式编辑器

- https://github.com/chordbook/editor /GPLv3/202404/ts
  - https://chordbook.github.io/editor/
  - A web-based editor for editing chord sheets in the ChordPro format, built on CodeMirror.
  - ChordPro, a simple text format for the notation of lyrics with chords. Although initially intended for guitarists, it can be used for all kinds of musical purposes.
  - https://github.com/chordbook/codemirror-lang-chordpro

- https://github.com/fsegurai/Electron-React-Markdown-Editor /MIT/202311/ts
  - Electron Markdown Editor based on React
  - 依赖codemirror6、remark-parse

- https://github.com/warmachine028/markdown-editor /MIT/202202/ts/inactive
  - A markdown editor using Electron, ReactJS, Vite, CodeMirror6, and Remark

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

- https://github.com/geometryzen/stemcstudio-codemirror /MIT/202401/ts
  - Bundle of CodeMirror Editor

- https://github.com/riccardoperra/solid-codemirror /MIT/202305/ts/inactive
  - A library of SolidJS primitives to build code editors using CodeMirror 6
  - https://github.com/nimeshnayaju/solid-codemirror /202207/ts/inactive

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
  - https://github.com/michioxd/mdxeditor-modified

- https://github.com/mcnuttandrew/prong /MIT/202310/ts
  - https://prong-editor.netlify.app/
  - Prong (PRojectional jsON Gui) is an editor framework for creating bespoke in-browser editors for JSON-based domain-specific languages (such as Vega, Vega-Lite, Tracery, and many others). 
  - These editors allow for things like drag-and-drop interactions, inline-interactive spreadsheets, in-situ recommenders and sparklines, and many more elements that would require significant engineering effort to create otherwise.
  - 依赖codemirror6、react-markdown、jsonc-parser

- Starboard Notebook /889Star/MPLv2/202206/ts
  - https://github.com/gzuidhof/starboard-notebook
  - https://unpkg.com/starboard-notebook/dist/index.html
  - https://starboard.gg/
  - In-browser literal notebook runtime used in Starboard.
  - 编辑器已分离，基于rich-markdown-editor和prosemirror
  - 前端基于lit

- https://github.com/lhlyu/pure-editor /MIT/202302/ts/inactive
  - a pure editor developed using codemirror6

- https://github.com/RaspberryPiFoundation/editor-ui /apache2/202405/js
  - https://editor.raspberrypi.org/
  - Code Editor frontend
  - https://github.com/RaspberryPiFoundation/editor-api /AGPLv3/202405/ruby/python
    - https://editor.raspberrypi.org/
    - Code Editor backend

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
  - Firepad is an open-source library for adding collaborative capabilities into text and code editors. Firepad uses Google Firebase as a backend, so it requires no server-side code. It supports out of the box popular web editors such as Codemirror, Ace and Monaco.
  - new adapter to add compatibility with Codemirror6, arguably one of the best web editor out there. Check the demo here
  - https://github.com/lucafabbian/codemirror6-firepad-demo /202206/js
    - Demo of Codemirror6 using the Google Firebase service to achieve real time collaboration with minimal setup.

- https://github.com/interviewstreet/firepad-x /202401/ts
  - We have rewritten all the modules and few extras using TypeScript while enhancing earlier implemented Adapter Pattern to integrate with external modules, such as Database (preferably Firebase) and editors (as of now only Monaco is supported, but PRs are welcomed). 

## diff

- https://github.com/codemirror/merge /MIT/202403/ts
  - https://codemirror.net/try/?example=Merge%20View
  - Merge view for CodeMirror

- https://codepen.io/GwapongProgrammer/pen/yLXqWMK
  - 依赖codemirror6

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

## lint

- https://github.com/KELs7/contracting-linting-codemirror6 /202405/ts
  - Demo: Contracting Linting in Codemirror6
  - Only few linting rules have been implemented
  - 示例lint python2代码
# extensions
- https://github.com/val-town/codemirror-ts /ISC/202402/ts
  - https://val-town.github.io/codemirror-ts/
  - a set of extensions for CodeMirror 6 that add support for TypeScript
  - lint, hover, and autocomplete extensions for CodeMirror + TypeScript
  - Hover hints for types 
  - Autocomplete 
  - Diagnostics (lints, in CodeMirror's terminology)

- https://github.com/yeliex/codemirror-extensions /MIT/202403/ts
  - https://cm.yeliex.dev/
  - codemirror extensions includes toolbar, helper, image-upload, event-emitter
  - codemirror-final-newline
  - codemirror-markdown-commands
  - codemirror-markdown-image
  - codemirror-toolbar

- https://github.com/overleaf/codemirror-tree-view /MIT/202311/ts
  - A CodeMirror 6 extension providing an interactive view of a document's syntax tree
  - 更偏向于作为codemirror的devtools
  - https://github.com/overleaf/codemirror-autocomplete
  - https://github.com/overleaf/codemirror-search

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

- https://github.com/JackieScorpio/convert-json-to-ts /MIT/202404/ts
  - use codemirror and vscode webview to achieve a vscode extension
  - Convert Json to Typescript

- https://github.com/A99US/codemirror-6-snippetbuilder /MIT/202304/js
  - This is a function for CodeMirror 6 to convert a standard array of snippet (like this one) and turn it into snippet array that is ready to use in CodeMirror 6 extension.

- https://github.com/PuruVJ/neocodemirror /202311/ts
  - Aims to provide Codemirror 6 as an easy to use codemirror action.

- https://github.com/acao/codemirror-json-schema /MIT/202404/ts
  - Codemirror 6 extensions that provide full JSON Schema support for @codemirror/lang-json & codemirror-json5 language modes
- https://github.com/acao/json-schema-workbench /202311/ts
  - https://json-schema-workbench.vercel.app/
  - A reference implementation for codemirror-json-schema
  - A Next.js 13 template for building apps with Radix UI and Tailwind CSS.

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
- https://github.com/bhsd-harry/codemirror-mediawiki /GPLv2/202405/ts
  - https://bhsd-harry.github.io/codemirror-mediawiki/
  - Modified CodeMirror mode based on wikimedia/mediawiki-extensions-CodeMirror

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

## lsp

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

- https://github.com/okikio/codemirror /MIT/202110/ts/inactive
  - https://okikio-codemirror.netlify.app/
  - A minor test of Codemirror

## utils-lang

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
# code-playgrounds
- react-runner /382Star/MIT/202303/ts/inactive
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

- https://github.com/leon-kfd/OnlineCodeEditor /202311/ts/vue
  - An online code Editor like CodePen, built by Vue3.

- https://github.com/live-codes/livecodes /MIT/202405/ts
  - https://livecodes.io/
  - A feature-rich, open-source, client-side code playground for React, Vue, Svelte, Solid, Typescript, Python, Go, Ruby, PHP and 80+ languages/frameworks.
  - 依赖codemirror6、monaco、codejar、codejar、yjs
  - [Why Another Playground? | LiveCodes](https://livecodes.io/docs/why/)
    - There are great products like CodePen, JSFiddle, JS Bin, CodeSandbox, Replit and many others, which LiveCodes does not aim to replace or compete with.
    - On the contrary, it aims to integrate with as many of these services as their APIs allow.
    - All processing and code transformations run in the browser on the client-side.
    - The LiveCodes app (standalone or self-hosted) can be embedded in any web page.

- https://github.com/lucademenego99/icp-bundle /apache2/202307/svelte
  - Interactive Code Playgrounds Bundle is a plugin for embedding interactive code playgrounds in HTML pages.
  - The editor used in these playgrounds is CodeMirror6, an in-browser editor distributed as a collection of modules.
  - The project is based on Svelte, a tool for building web applications. The actual build step is performed through Vite and the gulp tool.
  - The most computationally expensive tasks the bundle does are performed using Web Workers and SharedWorkers.
  - https://github.com/lucademenego99/icp-slides /202307/html
    - https://lucademenego99.github.io/icp-slides/
    - Slides created with Reveal.js for the Interactive Code Playgrounds project, hosted directly from the repository as a Github Pages website.

- https://github.com/java-sheets/java-sheets /MIT/202207/java/ts
  - Browser Based Java REPL
  - Jsheet lets you create and share Java snippets, ranging from single expressions to complex classes, methods and even Markdown comments.

- https://github.com/jsbin/jsbin /MIT/202402/js
  - http://jsbin.com/
  - Collaborative JavaScript Debugging App
  - this current version of jsbin (v4.x.x) is no longer actively maintained and the new version of jsbin (v5) is currently in active development
  - 依赖codemirror5
  - https://github.com/jsbin/jsbin/tree/feat/next-v5 /201906/js/inactive

- https://github.com/chinchang/web-maker /MIT/202405/js
  - https://webmaker.app/
  - A blazing fast & offline frontend playground
  - 依赖codemirror5
# starter
- https://github.com/falk-werner/codemirror-example /202312/js/单文件
  - a brief example how to integrate Code-Mirror using vite.

- https://github.com/RPGillespie6/codemirror-quickstart /202402/js
  - Quickstart guide and examples for those who prefer a more hands on approach to bootstrapping CodeMirror 6
  - Example 1: a minimal example HTML page
  - [Example 2: choose the editor theme on the fly](https://www.bryanpg.com/codemirror-quickstart/examples/example2.html)
  - [Example 3: Try making edits above, saving state, then loading a different state.](https://www.bryanpg.com/codemirror-quickstart/examples/example3.html)

- https://github.com/datacamp/codemirror-6-getting-started /202102/js
  - Getting started with CodeMirror 6, the popular code editor library
  - [Getting started with the new CodeMirror 6 | DataCamp Engineering _202102](https://blog.datacamp.engineering/codemirror-6-getting-started-7fd08f467ed2)

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
  - Beautiful themes for CodeMirror
  - https://github.com/satansdeer/thememirror

- https://github.com/cossssmin/codemirror-theme-github /202102/inactive
  - A CodeMirror theme inspired by the GitHub editor.
# v5
- https://github.com/0xGG/EchoMD /AGPLv3/202103/ts/inactive
  - An experimental WYSIWYG markdown editor built on top of HyperMD with extended Widgets support
  - This WYSIWYG markdown editor is built and modified on top of @laobubu's awesome project HyperMD.
  - We will migrate to codemirror 6 in the future, which is going to be a complete rewrite. But for now, we will just stick to the current codemirror 5 codebase, that is what HyperMD currently uses.
  - https://github.com/laobubu/HyperMD /MIT/201810/ts/inactive

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
# code-ai
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
  - frontend-only live semantic search with transformers.js
  - Calculates the embeddings and cosine similarity client-side without server-side inferencing, using transformers.js and latest SOTA embedding models from Huggingface.

- https://github.com/rvion/CushyStudio /AGPLv3/202403/ts
  - https://docs.cushystudio.com/
  - The AI and Generative Art platform for everyone

- https://github.com/sweepai/sweep /202405/python
  - https://sweep.dev/
  - Sweep: open-source AI-powered Software Developer for small features and bug fixes.
  - Sweep is an AI junior developer that turns bugs and feature requests into code changes. Sweep automatically handles devex improvements like adding typehints/improving test coverage. 
  - Turns issues directly into pull requests (without an IDE)
# more
- https://github.com/datavis-tech/codearea /MIT/201908/js
  - A proof-of-concept code editor with syntax highlighting that uses
    - highlighted-pre-over-textarea approach (like react-simple-code-editor)
    - web-tree-sitter for incremental parsing
    - `diff-match-patch` via `json0-ot-diff` for computing text diffs (needed for using tree-sitter)
    - React for DOM updates
