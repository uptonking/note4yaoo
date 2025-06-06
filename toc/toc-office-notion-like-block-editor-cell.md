---
title: toc-office-notion-like-block-editor-cell
tags: [block-editor, editorjs, lib, notion-like, toc]
created: 2020-11-17T13:37:09.407Z
modified: 2022-08-14T16:26:48.558Z
---

# toc-office-notion-like-block-editor-cell

> search: block-editor, notion-editor

# guide
- 编辑器功能检查
  - 是否支持跨block选择部分文字、并加粗 (重要)
  - 是否支持拖拽block修改顺序 (重要)
  - 支持协作

- 想要分析notion的block架构设计，可参考clone示例
  - 实现思路: 将editor作为一种类似table/kanban的数据视图来开发实现
  - 扩展思路，前端的block通常对应后端的field字段

- resources
  - https://github.com/wenerme/wener/blob/master/notes/web/editor/editor-awesome.md
# block-style-editor
- plate /1.6kStar/MIT/202208/ts
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - core依赖zustand、zustood、jotai、react-hotkeys-hook
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但不支持拖入拖出list item
  - code-block自研实现，不依赖第三方代码编辑器
  - A plugin framework for building rich text editors with slate.

- blocky-editor /150Star/MIT/202208/ts
  - https://github.com/vincentdchan/blocky-editor
  - https://blocky-editor.dev/
  - https://blocky-editor.dev/loro
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - 支持协作
  - preact的封装很少，大部分vanillajs
  - An headless editor built with blocks
  - 依赖quill-delta、lodash
  - v202210版不依赖rxjs，后面引入rxjs
  - Extensible. Extend the editor with custom blocks and spans.
  - Currently, the document tree of BlockyEditor supports collaborative editing using operation transforming(known as OT).
  - You can also use a CRDT library such as YJS and bind the data model to it.

- BlockNote /14Star/MPLv2/202208/ts
  - https://github.com/YousefED/BlockNote
  - https://blocknote-main.vercel.app/
  - A "Notion-style" block-based extensible text editor built on top of Prosemirror and Tiptap.
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，特别是支持将list item拖入拖出列表
  - 支持斜杠菜单、悬浮菜单修改标题层级、多级列表、顺滑动画
  - 支持协作
  - 依赖tiptap.v2、tippyjs、styled-components
  - bugs
    - 复制粘贴多行文本

- notitap /39Star/MIT/202209/ts
  - https://github.com/sereneinserenade/notitap
  - https://sereneinserenade.github.io/notitap/
  - 依赖daisyui、tippyjs、floating-ui、fuzzysort
  - Notion like editor built on top of tiptap.
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但不支持拖入拖出list item

- https://github.com/Darginec05/Yopta-Editor /MIT/202310/ts
  - https://yopta-editor.vercel.app/basic
  - Notion-like editor with similar behaviour
  - 几乎无依赖
  - 支持跨block选择部分文字
  - list不支持多级
  - list item暂不支持拖出去
  - Offline ready mode, 离线基于localStorage
  - [plans for v2](https://yopage.co/blog/0zntIA46L4/5iK8VNiBI8)

- https://github.com/djyde/plastic-editor /202103/ts/svelte
  - A block-based editor
  - https://github.com/relm-us/svelt-yjs
  - https://github.com/fengkx/plastic-editor-react
    - Plastic Editor implentation with React.js

- tiny-write /4Star/NALic/202208/ts/prosemirror/markdown-it/web版+桌面版
  - https://github.com/dennis84/tiny-write
  - https://tiny-write.pages.dev/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但不支持拖入拖出list item
  - 不支持/斜杠菜单
  - 依赖solid-js、codemirror6、idb-keyval、date-fns、markdown-it、y-prosemirror
  - Just a little writing tool with markdown shortcuts that saves every change to local indexeddb.
  - 跨平台客户端基于tauri实现，tauri部分使用rust实现

- editorjs /19.8kStar/Apache2/202206/ts/vanillajs
  - https://github.com/codex-team/editor.js
  - https://editorjs.io/
  - A block-styled editor with clean JSON output
  - 不支持跨block选择部分文字，只能全选block
  - 不支持拖拽block修改顺序
  - [wip: feat(ui) : the block can be drag n drop](https://github.com/codex-team/editor.js/pull/2285)
  - https://github.com/editor-js/awesome-editorjs
  - https://github.com/omegion/horul-editor
    - horul-editor is editorjs wrapper component with vue

- gutenberg /9.2kStar/GPLv2/202311/js
  - https://github.com/WordPress/gutenberg
  - https://wordpress.org/gutenberg/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但不支持拖入拖出list item，蓝色拖拽指示器已实现
  - The Block Editor project for WordPress and beyond
  - 依赖react
  - 第三方的插件特别丰富
  - https://github.com/Automattic/isolated-block-editor /js
    - Repackages Gutenberg's editor playground as a full-featured multi-instance editor that does not require WordPress.
    - Examples: Plain Text Editor, Blocks Everywhere, Gutenberg Desktop
    - Allows multiple onscreen instances with seperate data stores and keyboard handlers
    - Undo history
    - Dynamic switching of data stores for compatability with third-party blocks
    - Gutenberg already provides a playground which allows it to be used outside of WordPress. This is actually used as the basis for the Isolated Block Editor.
    - The Isolated Block Editor is a full editor that handles a lot of these complexities. It should not be considered a replacement for the Gutenberg playground, but more of an opinionated layer on top.
  - https://github.com/gambitph/Stackable
    - a beautiful collection of ready-to-use blocks for Gutenberg
  - https://github.com/CakeWP/block-options /js
    - https://editorskit.com/
    - EditorsKit provides set of page building block options and tools for the new WordPress Gutenberg editor.

- dmeditor /14Star/GPL/202306/ts
  - https://github.com/dmeditor/dmeditor
  - https://dmeditor.io/
  - https://demo.dmeditor.io/editor?d=demo
  - a block-based visual editor, written in React.
  - 不支持跨block选择部分文字
  - 可切换设备尺寸查看效果
  - 依赖mui、react-bootstrap、slate
  - https://github.com/dmeditor/dmeditor-sample

- https://github.com/Blocks-Editor/react-blocks-editor /ts
  - Embed the Blocks Editor anywhere using a React component.
  - 偏向计算函数
  - https://github.com/Blocks-Editor/blocks /js
    - https://blocks-editor.github.io/blocks 
    - An online drag-and-drop smart contract builder.

- smartblock /249Star/MIT/202003/ts/inactive/prosemirror
  - https://github.com/appleple/smartblock
  - https://appleple.github.io/smartblock/
  - 依赖prosemirror、codemirror5、react-highlight.js、react-svg、styled-components
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序，但有上下箭头按钮
  - intuitive block based wysiwyg editor built with React and ProseMirror

- https://github.com/WeiWenda/effect-note /MIT/202412/ts
  - 一款免费的大纲笔记软件，纯文件存储，Gitee云端同步
  - 交互较差
  - 支持插入 vditor/wangeditor/monaco-editor
  - 依赖electron-store、lunr2、node-git-server、react-redux、react-dnd、vditor
  - https://github.com/WeiWenda/effect-note-mobile
  - https://github.com/WeiWenda/effect-note-excalidraw

- https://github.com/pierre-lgb/slashwriter /NALic/202312/ts
  - https://slashwriter.fly.dev/
  - 依赖tiptap.v2、redux-toolkit、supabase、express、yjs、hocuspocus、mui5
  - App for editing and sharing documents online, with a Notion-like block-based collaborative editor.

- https://github.com/karpov-kir/canvas-block-editor /ts
  - A block based canvas text editor.

- MoEditor /2Star/NALic/202208/ts
  - https://github.com/spaced-all/MoEditor
  - https://github.com/spaced-all/Mono.editor
  - 一款基于 React 的、块级风格的、Markdown 友好的，富文本编辑器。
  - 跨block选区实现存在问题
  - 不支持拖拽block修改顺序
  - 支持类似typora的点击时触发行内编辑源码
  - floating-ui: 右键菜单，行内公式的编辑，Heading 的左侧提示，在 floating-ui 的支持下都可以很简单的实现
  - Danfo.js: 提供了 js 上和 Python.pandas 类似的 DataFrame 类，用于表格支持

- mt-block-editor /2Star/paid/ts/202208/提交多
  - https://github.com/movabletype/mt-block-editor
  - https://movabletype.github.io/mt-block-editor/
  - 依赖react-dnd、react-shadow、i18next，与具体编辑器无关
  - 示例使用的是 tinymce.v6
  - 不支持跨block选择部分文字，偶尔也支持，体验很不流畅
  - 支持拖拽block修改顺序
  - 可自定义block的block editor
  - https://github.com/movabletype/mt-plugin-MTBlockEditor
    - This plugin enables you to use Movable Type Block Editor for Movable Type.

- https://github.com/psyhyde/domino-editor
  - https://domino-editor.vercel.app/
  - /6Star/NALic/202009/js/未开源代码-仅文档
  - Document Site for a Block Style Editor
  - A Playbook for Block Style Editor (BSE): Text Styling, Block Components, Misc Functions & Theme Switcher

- sir-trevor-js /4.5kStar/MIT/202103/js/inactive
  - https://github.com/madebymany/sir-trevor-js
  - http://madebymany.github.io/sir-trevor-js/
  - 依赖只有svg4everybody，编辑器完全自己实现，代码量较大
  - 提供的示例就是分块的
  - 不支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - Rich content editing entirely re-imagined for the web
  - Stored in structured JSON with limited inline HTML markup
  - Trivial to extend and create your own block types

- colonel-kurtz /304Star/MIT/201909/js/inactive
  - https://github.com/vigetlabs/colonel-kurtz
  - http://colonel-kurtz.netlify.com/
  - 只支持3类block:text/image/media，且实现较简单，不依赖编辑器
  - A block based content editor powered by React. 
  - Colonel Kurtz provides a front-end for building pages as a series of blocks, serializing to a JSON data structure.

- https://github.com/johnthethird/makona-editor  /archived--201504
  - http://johnthethird.github.io/makona-editor/
  - a block-style editor written in ReactJS.
  - 不支持跨block选择部分文字
  - 不支持拖拽block修改顺序

- https://github.com/CedarXi/All-in-one /63Star/NALic/202004/js/vue/inactive
  - http://all-in-one.qingzhu.co/
  - https://all-in-one-kappa.vercel.app/
  - All-in-one 是一个开源的模块化内容构建编辑器，基于Vue和element的打造
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 它不同于传统的文本编辑器，所有的内容都是以模块的概念来打造。灵感来自Notion
  - 所有的模块都以VUE组件的形式编写，可以灵活插拔。
  - 所有组件保存的数据，都以Json的形式存储在Vuex里供不同组件调用
  - ref
    - https://github.com/renmu123/v-block-editor

- https://github.com/Eroxl/Note-Rack
  - An inline WYSIWYG markdown editor built for students to manage school work
  - 依赖react-dnd
# editorjs-plugins
- https://github.com/yijian166/all-in-one-editorjs

- https://github.com/affandes/katex-editorjs
- https://github.com/affandes/image-editorjs

- https://github.com/jakekara/editorjs-footnotes
- https://github.com/hata6502/editorjs-inline
- https://github.com/hata6502/editorjs-style
- https://github.com/chanhha91/editorjs-title
# editorjs-repos
- https://github.com/codex-team/codex.docs /apache2/202212/ts/inactive
  - https://docs.codex.so/
  - a free docs application. It's based on Editor.js ecosystem
  - Docs nesting — create any structure you need
  - Misprints reports to the Telegram / Slack

- https://github.com/dev-juju/EditorJS-React-Renderer
  - https://err.bomdisoft.com/
  - A library for rendering styled, responsive and flexible React components from block style data objects like those generated by codex editors like Editor.js.
  - This package works well with output from the Editor.js rich text editor library. 
  - However, there is no dependency on Editor.js.
- https://github.com/moveyourdigital/editorjs-blocks-react-renderer
  - Renders EditorJS blocks to semantic React HTML5 components. Unnopinated and flexible.
- https://github.com/antoineaudrain/react-editorjs-renderer
  - A library for rendering styled, responsive, and flexible React components from block style data objects generated by codex editors like Editor.js.

- codex.notes /81Star/MIT/202009/js/inactive
  - https://github.com/codex-team/codex.notes
  - 依赖旧版codex.editor, graphql-request, electron-pug, nedb, tapable, winston
  - CodeX Notes is a crossplatform text editor, built on Electron. It integrates Editor.js and supports cloud backups of your notes.
  - Organize notes by folders

- https://github.com/Jungwoo-An/react-editor-js
- https://github.com/jessypouliot98/advanced-react-input

- https://github.com/pavittarx/editorjs-html
  - parse editorjs clean data to html. 
- https://github.com/hata6502/editorjs-element
  - DOM event, CSS Style, etc may conflict each other when multiple Editor.js instances are launched in same page. 
  - By launching Editor.js in iframe, these problems are resolved forcibly. 
  - This repository provides the template of Editor.js in iframe.

- https://github.com/FireEnjin/Editor
  - A block editor component made with Editor. JS and Stencil. JS
# more-block-editor
- https://github.com/hashintel/hash
  - https://hash.dev/
  - Data management, integration and modeling with blocks
  - The Block Protocol is an open-source standard and registry for sharing interactive blocks connected to structured data.
  - You can build your own blocks, embed them in a website, or allow your users to embed blocks directly within your application.
  - HASH is our forthcoming open-source, all-in-one workspace platform built around structured data and interactive blocks.
  - 前端依赖 mui5、headlessui、graphql、apollo/client、prosemirror

- https://github.com/LuceusXylian/BausteinEditor
  - Editor in Blocks: Import, Edit, Move, Delete, Add, Export

- https://github.com/TorstenDittmann/omnia-editor
  - https://omnia-editor.vercel.app/
  - 依赖 svelte
  - A lightweight open source block style editor built for the modern web.
