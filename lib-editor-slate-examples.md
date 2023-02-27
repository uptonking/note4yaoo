---
title: lib-editor-slate-examples
tags: [examples, slate-editor, toc]
created: 2022-05-15T18:45:14.380Z
modified: 2023-02-05T19:03:12.723Z
---

# lib-editor-slate-examples

# guide

- collab
  - json patch
# popular-slate
- plate /1.6kStar/MIT/202208/ts/block-style
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但list内所有item不支持拖拽
  - core依赖zustand、zustood、jotai、react-hotkeys-hook
  - code-block自研实现，不依赖第三方代码编辑器
  - A plugin framework for building rich text editors with slate.

- editablejs-editable /17Star/GPL/202208/ts/自绘光标/模型层block
  - https://github.com/editablejs/editable
  - https://github.com/editablejs/editable/blob/main/README.zh-CN.md
  - https://docs.editablejs.com/playground
  - 依赖slate、zustand
  - 只依赖slate不依赖slate-react，但实现是类似的，react组件逻辑并不多
  - 一个可扩展的富文本编辑器框架，专注于稳定性、可控性和性能
    - 为此，我们没有使用原生的可编辑属性contenteditable，而是使用了一个自定义的渲染器
    - canvas的开发体验不佳，需要编写更多代码
  - 使用slatejs数据模型，借助 react 使用自绘光标的模式渲染，不再依赖 contenteditable 属性
  - [修改license为GPL_20220204](https://github.com/editablejs/editable/commits/main?after=d61da6caa411139cddb0ae0e8eeeeaee05893610+69&branch=main&qualified_name=refs%2Fheads%2Fmain)
  - unicode-trie主要对一些 unicode 字符进行索引的计算。因为有些字符占位所占的字节数不确定，造成某些字符拆分后的索引不准确

- wangEditor.v5 /14.3kStar/MIT/202208/ts/vanillajs
  - https://github.com/wangeditor-team/wangEditor
  - https://www.wangeditor.com/
  - core依赖slate、snabbdom、dom7、is-hotkey、lodash、uppy(file uploader)、event-emitter、i18next
  - 源码是函数式风格
  - 开箱即用，配置简单。
  - 支持 JS Vue React
  - L1级编辑器，弃用了 document.execCommand，使用 slate.js（但不依赖 React）为内核
  - 使用vdom（基于 snabbdom.js）做视图更新，model 和 view 分离，增加稳定性
  - 扩展性
    - 使用扩展插件和模块的机制，保证扩展性
    - 现在wangEditor内置的各个功能，也都是通过扩展插件和模块的形式搭建起来的
  - https://github.com/wangfupeng1988/slate-dom-view
    - slate.js for DOM, without React.

- https://github.com/JokerLHF/mini-slate
  - 使用 ts 实现 slate 富文本

- prezly-slate /31Star/MIT/202208/ts/提交多
  - https://github.com/prezly/slate 
  - 依赖 `plate`的工具方法而不依赖编辑器、popperjs2、@prezly/sdk、react-bootstrap
  - Prezly software built upon Slate
  - 悬浮工具条使用卡片的形式
  - https://www.prezly.com/
    - Successful businesses need a fanbase. Use Prezly to build yours.
    - With Prezly, you can publish and share your content with your audience, directly. No algorithms, no middlemen, no BS.

- https://github.com/Darginec05/Yopta-Editor
  - https://yopta-editor.vercel.app/basic
  - Notion-like editor with similar behaviour
  - 支持跨block选择部分文字
  - list不支持多级
  - list item暂不支持拖出去
  - Offline ready mode, 离线基于localStorage

- https://github.com/dsvgit/slatesbox
  - https://dsvgit.github.io/slatesbox/
  - Slate editor plugins system. 
  - Drag and drop, folding implementation.
  - [Slate.js + dnd-kit = 🔥. Improving Rich Text Editor UX by adding Drag and Drop.](https://dev.to/devterminal/slatejs-dnd-kit-improving-rich-text-editor-ux-by-adding-drag-and-drop-23d3)

- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.
  - v1 of changing the index of an object causes a lot of adding and deleting. This is a limitation of the path based scheme.

- https://github.com/nivekithan/slate-devtools
  - devtool for slatejs which will assist you in debugging the code
  - 依赖slate.v0.59, jotai
  - [I created a devtool to assist in debugging](https://github.com/ianstormtaylor/slate/issues/4112)

- quadrats /4Star/MIT/202203/ts
  - https://github.com/Quadrats/quadrats
  - https://quadrats.github.io/quadrats
  - A complete rich text editor. Currently based on Slate framework.
  - storybook示例非常丰富，但和artibox一样
  - 依赖 slate.v0.75.0
  - https://github.com/React-Artibox/artibox /202011
    - https://react-artibox.github.io/artibox
    - Artibox - A complete rich text editor based on Slate framework.

- whim-notion-like /6Star/MIT/202108/ts
  - https://github.com/coniel/whim-editor
  - A highly customisable block based rich text editor inspired by Notion.
  - core依赖 slate.v0.65.3，fuse.js(fuzzy-search)
  - ui依赖@braindrop-editor/core
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序，特别是支持将list item拖入拖出列表
  - Whim is currently undergoing a complete re-write for version 2.0, with an initial release planned for the end of August 2022. 
    - Version 2.0 will include a much improved API, detailed docs, and solid test coverage.

- slate-angular /93Star/MIT/202205/ts
  - https://github.com/worktile/slate-angular
  - http://slate-angular.ngnice.com/
  - Angular view layer for Slate

- edu-editor /2Star/MIT/202207/ts/slate/inactive
  - https://github.com/kiaksarg/edu-editor
  - https://edu-editor.netlify.app/
  - a basic medium/notion like rich text editor based on Slate.js
  - 依赖 chakra-ui、nextjs、react-table.v7
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - 支持只读模式
  - 代码量不大，思路清晰
- https://github.com/masnormen/noshon
  - https://noshon.vercel.app/
  - Notion-inspired rich-text editor, powered by Next.js, Tailwind CSS, and Slate.js.

- hero-editor /10Star/MIT/202205/js/代码少/mobile
  - https://github.com/Thinkei/hero-editor
  - http://hero-editor.surge.sh/
  - Hero editor is a WYSIWYG built on top of Slate (v0.58.3).
  - It's designed for mobile-first, hence all of the communications from plugins to the editor must go through message channel. 
  - This package also includes serializers and renderers for the Slate content.

- taze-editor /6Star/MIT/202210/ts/inactive
  - https://github.com/taze-editor/taze-editor
  - http://taze-editor.vercel.app/
  - Create your own plugin-based rich text editor easily
  - built on top of Slate and heavily inspired by Plate.

- circu /1Star/MIT/202211/ts/blocksuite
  - https://github.com/Flrande/circu
  - 一个支持多人协同的在线文档应用
  - 修改了slate-react
  - 协作基于yjs

- react-rich-editor /3Star/MIT/202203/js
  - https://github.com/Rajatm544/react-rich-editor
  - https://reactricheditor.netlify.app/
  - A rich text editor built using React and Slate as part of the internship assignment for Plotline

- https://github.com/eduardmisa/slateless
  - https://www.emisa.me/npm/slateless/
  - A minimal richtext editor based on Slate
  - 显示编辑器、模型，方便调试
- https://github.com/ahmedosama7450/rich-slate
  - Opinionated rich text editor on top of slate (Under development)

- full-slate-editor-example /3Star/MIT/202208/ts
  - https://github.com/Dev-CasperTheGhost/full-slate-editor-example
  - http://full-slate-editor-example.vercel.app/
  - A full Slate editor example with many features such as text formatting, block formatting (quotes, headers, lists) and text alignment

- material-slate /20Star/MIT/202111/js/inactive
  - https://github.com/unicef/material-slate
  - https://unicef.github.io/material-slate/
  - 依赖slate.v0.57、material-ui.v4
  - Rich text editor based on Slate for Material UI (React)
  - 实现了简单的评论列表、脚注序列

- https://github.com/seafileltd/seafile-editor /RepoNA
  - 项目是基于 react-slate 组件库的二次封装, 用于满足公司富文本编辑器的使用需求

- https://github.com/portive/wysimark
  - Wysiwyg Editor for Markdown: 100% CommonMark + GFM with Uploads and Image Resizing
  - 依赖slate-react
  - https://github.com/portive/slate-plugin
    - Add beautiful and intuitive images and attachments to Slate with support for paste, drag and drop and `<input type="file">` uploads.
# slate-based-editors
- boatproject-editor /1Star/MIT/202208/ts/plate/提交多/inactive
  - https://github.com/boatproject/editor
  - 依赖 plate、slate、styled-components
  - Rich text editor component for React. Built with Plate and MUI

- https://github.com/sodenn/react-fluent-edit
  - https://react-fluent-edit.vercel.app/
  - Brings easy-to-use mentions, markdown and DnD (WIP) features to Slate.

- https://github.com/webkom/lego-editor /ts
  - A React rich text editor written in TS with Slate.js for lego-webapp
  - 代码量少，适合入门，支持上传图片

- https://github.com/accordproject/web-components/tree/master/packages/ui-markdown-editor
  - https://ap-web-components.netlify.app/
  - a WYSIWYG editor for markdown that conforms to the CommonMark specification
  - 依赖markdown-it、slate、semantic-ui-react

- https://github.com/bipboy/rich-slate-editor
  - A small react implementation of a text editor based on Slate and Baseweb(css-in-js)

- dslate /6Star/MIT/202207/ts/antd
  - https://github.com/rojer95/dslate
  - https://rojer95.github.io/dslate/#/
  - https://rojer95.github.io/dslate/#/docs/getting-started
  - DSlate 是一个基于 Slate 构建的 Ant Design 风格的富文本编辑器
  - core依赖slate-react

- https://github.com/mbehr1/json-editor
  - slate.js based json editor to embed into webpages

- https://github.com/dsvgit/mide
  - https://dsvgit.github.io/mide/
  - Slate.js code editor extension

- slatejsx /48Star/Apache2/202203/js/antd
  - https://github.com/slatejsx/slatejsx
  - http://seditor.open.heyphp.com/
  - 项目基于slate.js框架开发，项目内所有图标，风格组件均使用antd

- https://github.com/slatable/slate /202006
  - 基于 slatejs 封装富文本编辑器

- https://github.com/zanuarmirza/text-editor
  - markdown editor using slate.js
- https://github.com/xiaolu-lujunji/note
  - https://note-dev.vercel.app/
  - An online markdown editor

- https://github.com/Aerobird98/flow /js
  - https://aerobird98.github.io/flow/
  - A compact web based rich-text editor that builds on top of Slate-js with powerful, yet simple and accessible editing capabilities.
  - Flow is using Preact-js
  - Using Theme-ui, fontawesome

- https://github.com/longlongago2/bricky /ts
  - rich editor based on slatejs
- https://github.com/workwithizzi/limber-text-editor /js
  - https://limber-text-editor.vercel.app/
  - Rich Text Editor built on top of React and Slate.

- https://github.com/tiddly-gittly/slate-write
  - WYSIWYG editor for TiddlyWiki. (WIP)

- https://github.com/usunil0/slate-paged /202010
  - https://slate-paged-demo.vercel.app/
  - 依赖slate.v0.59, nestjs，ts
  - A paged editor rather than a continuous block. built using slate js.
  - done: basic editor setup basic functionalities figure out the nodes length and paging

- volto-slate /23Star/MIT/202203/js/依赖后端
  - https://github.com/eea/volto-slate
  - https://6.demo.plone.org/
  - An alternative text editor for Volto, capable of completely replacing the default richtext editor
  - Some of the main reasons that drove us to create volto-slate instead of enhancing Volto's draftjs implementation
  - 样式陈旧，编辑器和业务代码有联系
  - repos
    - https://github.com/plone/volto
      - React-based frontend for the Plone Content Management System
    - https://github.com/plone/Products.CMFPlone
      - Plone is a mature, secure and user-friendly Content Management System (CMS).
      - 后端基于python实现
    - https://github.com/eea/volto-slate-metadata-mentions
    - https://github.com/eea/volto-slate-footnote

- https://github.com/sanity-io/sanity/tree/next/packages/%40sanity/portable-text-editor
  - Sanity.io is the platform for structured content. 
  - It comes with an open-source editing environment called Sanity Studio that you can customize with JavaScript and a real-time hosted data store. 
  - 依赖slate.v0.72.3，自研slate-react
  - 包含test，但测试示例storybook效果过于简单
  - [V3 portable text editor_202208](https://github.com/sanity-io/sanity/pull/3465)
  - https://github.com/sanity-io/sanity  /MIT
    - Sanity.io is the platform for structured content. 
    - It comes with an open-source editing environment called Sanity Studio that you can customize with JavaScript and a real-time hosted data store. 
    - Sanity Studio is an open source headless real-time CMS, that you can customize with JavaScript and React.
    - Sanity.io has powerful APIs for querying, patching, and mutating data in the real-time content backend. In addition to our GROQ(Graph-Relational Object Queries) API, we also support deploying GraphQL APIs to query your content.
    - [Query JSON documents in the Terminal with GROQ](https://css-tricks.com/query-json-documents-in-the-terminal-with-groq/)
      - Graph-Relational Object Queries (GROQ) is a query language (like SQL, but different) which is designed to work directly on JSON documents.

- payload /9.1kStar/MIT/202301/ts/slate
  - https://github.com/payloadcms/payload
  - https://payloadcms.com/
  - https://demo.payloadcms.com/admin
  - Headless CMS and Application Framework built with TypeScript, Node.js, React and MongoDB
  - 不是典型的block-editor
  - Block-based Layout Builder
  - Extensible SlateJS rich text editor
  - A Mongo database to store your data
  - retrieve, and manipulate data of any shape via full REST and GraphQL APIs
  - File storage and access control
  - Payload dynamically generates a React admin panel to manage your data. 
    - Admin panel is built with Webpack, code-split, highly performant (even with 100+ fields), and written fully in TypeScript.

- https://github.com/contentful/field-editors/tree/master/packages/rich-text
  - https://contentful-field-editors.netlify.app/rich-text
  - This package contains a React RichTextEditor component that is used as default for RichText field type in the Contentful web application.
  - Since these are developed using the App SDK, this will allow you to understand how each editor works, fork existing apps or create your own apps based on existing Contentful components' source rather than starting from scratch.

- https://github.com/Yan-Boogie/highlighter
  - A complete rich text editor based on Slate framework with extended 'Highlighting' functionality.

- https://github.com/sympto-health/slate-rte
  - Pre-built rich text editor for Slate in React.
  - 基于ts，但所有源码都放在src文件夹，看起来较乱
  - https://github.com/sympto-health/slate-rte-demo  /js

- https://github.com/gwwyn/react-editor
  - https://gwwyn.github.io/react-editor/
  - Rich-text editor build with React and Slate
  - 支持 add column，但看起来乱

- https://github.com/rs-pro/rocket-slate /202008/inactive
  - A rich text editor based on SlateJS framework and slate-plugin-next
  - Supports slate 0.57 only

- https://github.com/quillforms/quillforms
  - https://www.quillforms.com/
  - Open Source TypeForm Alternative Based on React JS and Typescript | Best Typeform Clone

- more-slate-editor
  - https://github.com/marsprince/slate-vue

- deprecated
  - https://github.com/kanweiwei/easy-editor
  - https://github.com/roast-cms/french-press-editor
  - https://github.com/Canner/canner-slate-editor
  - https://github.com/chatterbugapp/chatterslate
  - https://github.com/nossas/slate-editor
  - https://github.com/nareshbhatia/react-force/tree/master/packages/slate-editor

- https://github.com/naufaldi/slate-js-editor
  - Framer Motion, NextJS and Chakra UI
# slate-plugins
- https://github.com/imdbsd/slate-plugin
  - Rich text editor plugin for slate.js

## markdown

- https://github.com/hanford/remark-slate
  - Transform the contents of a slate 0.50+ editor into markdown and back again.
- https://github.com/inokawa/remark-slate-transformer
  - remark plugin to transform remark syntax tree (mdast) to Slate document tree, and vice versa. Made for WYSIWYG markdown editor.
- https://github.com/accordproject/markdown-transform
  - A transformation and parsing framework for converting markdown content to HTML, Slate (for rich-text editing) and other structured document object models (DOMs).
  - 提供了很多子包，本身类似于remark

- https://github.com/zhangyu836/docx-slate
  - slatejs-based docx editor for demonstration of docxjs.
  - https://github.com/zhangyu836/docxjs
    - Javascript port of python-docx.

## table

- https://github.com/lqs469/slate-table /202003/ts
  - https://slate-table.vercel.app/
  - A pretty Slate.js table plugin (Slate.js version > 0.5)
  - 支持合并、拆分单元格
  - 支持调整列宽、行高
  - cons
    - 双击无法选中单元格内单词
- https://github.com/daibin0809/slate-table-demo /ts
  - 依赖event-emitter
  - slate编辑器完成的一个表格功能，能够进行表格的选区、单元格操作和行列操作等操作。
  - 表格中右键唤起工具菜单
  - cons
    - 表格中无法再添加表格
- https://github.com/Kikky/slate-table-example /js
  - https://codesandbox.io/s/github/Kikky/slate-table-example
  - 表格内文本支持加粗，实现十分简洁
- https://github.com/cihad/slate-table /202107/ts
  - https://cihad.github.io/slate-table/
  - Table Plugin for Slate (based on @udecode/slate-plugins above v1.0). 
  - Inspired by the Atlassian editor's table plugin.
  - 依赖 slate.v0.61, @udecode/slate-plugins-table(2021)
  - 支持调整列宽
  - 不支持合并单元格
- https://github.com/nod-engineering/slate-table
  - /202106/js/v0.59

- https://github.com/jasonphillips/slate-deep-table
  - https://jasonphillips.github.io/slate-deep-table/
  - /201910/js/v0.44
  - 支持table in table
  - Forked from the slate-edit-table implementation, allowing for creation of tables with nested content
  - https://github.com/George-A-Payne/slate-tables
    - Forked from slate-deep-tables
  - https://github.com/GitbookIO/slate-edit-table
    - archived and has moved to GitBook's private fork
- https://github.com/whatever-company/slate-tables /js/依赖v0.47
  - https://whatever-company.github.io/slate-tables/
  - A Slate plugin to handle table edition.
  - The plugin supports nested tables natively.
  - Colspan and Rowspan are supported. All operations create a matrix containing all cells' positions.

- https://github.com/1build/leyden
  - https://1build-org.gitbook.io/leyden/
  - a data table framework powered by Slate.
  - Leyden's coordinate system is simple and fully interoperable with Slate's Path system.
  - Cells can access data from other cells using absolute coordinates and relative positions.
  - Leyden exposes several pre-built validators (such as numeric and integer) for your cell data
  - Slate requires users to define complicated render functions to detect different types of elements. Leyden handles this automatically
  - Leyden builds upon Slate's schema definition system, providing an interface for users to define table-shaped schemas with powerfully customization cells.

- https://github.com/shrutikachawla/slateTables /js
  - 依赖material-ui.v4、antd

## plugins

- https://github.com/mwood23/slate-test-utils
  - A toolkit to test Slate rich text editors with Jest, React Testing Library, and hyperscript! 
  - There's so many user input mechanisms, edge cases, selection, state, normalization, and more to keep in mind when developing.
  - It's an abstraction that uses hyperscript to generate editor states that can be tested in a JSDOM environment with a bit of black magic.
  - It's well documented that JSDOM does not support `contenteditable`

- https://github.com/lukesmurray/use-slate-with-extensions
  - https://use-slate-with-extensions.netlify.app/
  - a simple, powerful, and tiny (< 2KB) hook which helps you build self contained and composable extensions for Slate. 

- https://github.com/Simplicity-Tech/sim-slate-types
  - Common typings & helper functions for all slate related Simplicity projects.

- https://github.com/afeiship/next-slate-plugin
  - Slate plugin manager.

- https://github.com/enzoferey/slate-instant-replace
  - A Slate plugin that gives you full power on the last word your user typed.
  - This package is compatible with <= slate@0.47

- https://github.com/palerdot/react-slite /代码过于简单
  - This react component provides a slack like rich text editing experience powered by slate.js

- https://github.com/rockettomatooo/slate-react-presentation
  - a small package that lets you render a slate.js document without the overhead of the actual editor.
# mobile
- https://github.com/juliankrispel/slate-in-react-native
  - Proof of concept - Slate in react-native Webview

- https://github.com/arrizalamin/slate-fast-renderer /201911/js
  - small renderer for read-only slate.js document for web and react-native
# slate-examples
- https://github.com/inthelamp/book-reviewer
  - a learning project to obtain knowledge and skills about the MERN stack
  - Redux, Redux Thunk, axios, Slate, Lodash
  - Sign-in with JWT token

- https://github.com/RealRong/Rendevoz
  - open-source knowledge management application built with React and TypeScript
  - 依赖slate、yjs、rxjs
  - WYSIWYG Block Editor built upon Slate.js, with drag & drop, custom block rendering, etc.
  - Cross platform powered by Electron.

- https://github.com/wwsalmon/postulate
  - http://postulate.us/
  - Postulate is an all-in-one tool for collecting and publishing your knowledge.
  - Built on Next.js and MongoDB.

- https://github.com/thesunny/slate-experiments
  - 依赖slate.v0.63

- https://github.com/madmaxmehdi44/platforms-slate-supabase
  - Build a blogging platform based on Slate.js, Supabase and Vercel.
  - Skip the PlanetScale installation and instead create a database on Supabase
  - [Platforms Starter Kit: a template for site builders, multi-tenant platforms, and low-code tools.](https://demo.vercel.pub/platforms-starter-kit)
  - [How to Build a Multi-Tenant App with Custom Domains Using Next.js](https://vercel.com/guides/nextjs-multi-tenant-application)
# slate-collab
- https://github.com/typewriter-editor/json-patch
  - Immutable JSON Patch implementation based on RFC 6902 which adds operational transformation (OT) and last-writer-wins (LWW) support for syncing between client and server. 
  - Does not support the full OT algorithm because `copy` and `move` operations cannot be transformed correctly in all cases, so operations must always be applied in correct order. 
    - This means a central server is required to determine order.
  - 👉🏻 json-patch provides a utility that will help sync an object field-by-field using the Last-Writer-Wins (LWW) algorithm. 
    - This sync method is not as robust as operational transformation, but it only stores a little data in addition to the object and is much simpler
    - It does not handle adding/removing array items, though entire arrays can be set. 
    - It should work great for documents that don't need merging text like Figma

- https://github.com/solidoc/slate-ot /ts/202006
  - Operation Transformations for slate 0.5x.
  - 依赖sharedb
- https://github.com/Immortalin/slate-operational-transform
  - Slate JS Editor Operational Transform Example using ShareDB (used in production at Narration Box)
  - Invoking JSON0-ot-diff on every edit is not very efficient.
- https://github.com/onechunlin/collaborative-docs
  - 基于 Slate 和 ShareDb 实现的基于 OT 算法的协同文档

- https://github.com/timbuckley/slate-collaborative
  - A collaborative implementation for the slatejs editor using operational transform
  - 依赖很少
- https://github.com/4molybdenum2/Metanoia
  - Metanoia is a Real-time Collaborative Text Editor made with the help of Slate JS and Socket. IO
  - onChange直接发送op，未使用冲突处理算法
- https://github.com/Regloom/slatesyncedit
  - 每次同步全量数据
  - 注意测试时要用相同url代表在一个房间里面

- https://github.com/itoumlilt/crdt-md-editor /ts/slate/CouchDB
  - React Typescript CRDT based Collaborative Markdown Editor

- https://github.com/BitPhinix/slate-yjs
  - https://docs.slate-yjs.dev/
  - Slate-yjs aims to be the goto collaboration solution for slate. 
  - Slate-yjs will overwrite the current editor value with the state contained in the shared type.
  - [Linearising document content](https://github.com/BitPhinix/slate-yjs/issues/296)

- https://github.com/6thfdwp/crdt-editor
  - A collaborating editor based on Slate and Yjs

- https://github.com/cudr/slate-collaborative
  - A example of a collaborative editor using Slate and Automerge
  - Based on idea of https://github.com/humandx/slate-automerge
  - https://github.com/mms-gianni/slate-collaborationserver
# more-slate
- https://github.com/tiddly-gittly/slate-write
  - A WYSIWYG editor for TiddlyWiki. (WIP)
  - 一个用于 太微TiddlyWiki 的所见即所得编辑器。 

- https://github.com/vip-git/universal-json-schema
  - https://react-jsonschema-form-material-ui.github56.now.sh/
  - Universal JSON Schema Form - Currently Support for React - Material UI components for building Web forms from JSON Schema.
  - A Material UI port of jsonschema-form. (mui5)

- https://github.com/commercetools/ui-kit
  - Component library based on our design system

- https://github.com/johnsonandjohnson/bodiless-js
  - Framework for building editable websites on the JAMStack

- https://github.com/react-page/react-page
  - 使用redux作为状态管理
  - 提供了 @react-page/plugins-slate

- https://github.com/grafana/grafana
  - ui依赖slate.v0.47.8

- https://github.com/wowlusitong/re-editor /201908
  - 一个开箱即用的React富文本编辑器

- https://github.com/concord-consortium/slate-editor
  - Rich text editor based on Slate 0.47

- https://github.com/Mirrorgo/slatejs
  - 基于slate.js实现一个富文本编辑器, 用以学习富文本编辑器相关知识

- https://github.com/gwwyn/react-editor
  - Rich-text editor build with React and Slate

- https://github.com/ccjr1120/story-editor_slate
  - 基于slate的文本编辑器
- https://github.com/lingjieee/fantasy-editor 、202006
  - https://fantasy-editor.jieee.dev/
  - A React Rich Text Editor Based On Slate

- https://www.npmjs.com/package/@nocobase/client
