---
title: lib-editor-slate-examples
tags: [examples, slate, toc]
created: 2022-05-15T18:45:14.380Z
modified: 2022-05-15T18:45:27.570Z
---

# lib-editor-slate-examples

# popular-slate

- plate /1.6kStar/MIT/202208/ts
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但list内所有item不支持拖拽
  - code-block自研实现，不依赖第三方代码编辑器
  - A plugin framework for building rich text editors with slate.

- wangEditor.v5 /14.3kkStar/MIT/202208/ts
  - https://github.com/wangeditor-team/wangEditor
  - https://www.wangeditor.com/
  - core依赖slate、snabbdom、dom7、is-hotkey、lodash、uppy(file uploader)、event-emitter、i18next
  - 开箱即用，配置简单。支持 JS Vue React
  - L1级编辑器
    - 弃用了 document.execCommand API ，使用 slate.js（但不依赖 React）为内核，升级为 L1 能力。
  - 使用vdom
    - 使用 vdom 技术（基于 snabbdom.js）做视图更新，model 和 view 分离，增加稳定性
  - 扩展性
    - 使用扩展插件和模块的机制，保证扩展性
    - 现在 wangEditor 内置的各个功能，也都是通过扩展插件和模块的形式搭建起来的

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

- prezly-slate /31Star/MIT/202208/ts/提交多
  - https://github.com/prezly/slate 
  - 依赖 @udecode/plate-core、popperjs2、@prezly/sdk、react-bootstrap
  - Prezly software built upon Slate
  - 悬浮工具条使用卡片的形式
  - https://www.prezly.com/
    - Successful businesses need a fanbase. Use Prezly to build yours.
    - With Prezly, you can publish and share your content with your audience, directly. No algorithms, no middlemen, no BS.

- slate-angular /93Star/MIT/202205/ts
  - https://github.com/worktile/slate-angular
  - http://slate-angular.ngnice.com/
  - Angular view layer for Slate

- edu-editor /2Star/MIT/202207/ts/slate
  - https://github.com/kiaksarg/edu-editor
  - https://edu-editor.netlify.app/
  - a basic medium/notion like rich text editor based on Slate.js framework
  - 依赖 chakra-ui、nextjs、react-table.v7、slate.v0.72
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - 支持只读模式
  - 代码量不大，思路清晰

- editablejs-editable /17Star/MIT/202208/ts/只依赖slate不依赖slate-react/自绘光标
  - https://github.com/editablejs/editable
  - https://docs.editablejs.com/playground
  - 依赖slate、zustand
  - 一个实验性的富文本编辑器框架，希望通过自绘光标来替代原生 contenteditable 属性，提供更丰富、稳定的编辑能力。
  - 使用slatejs数据模型，借助 react 使用自绘光标的模式渲染，不再依赖 contenteditable 属性
  - 主要对一些 unicode 字符进行索引的计算。因为有些字符占位所占的字节数不确定，造成某些字符拆分后的索引不准确，所以需要这个工具包来解决这个问题。

- hero-editor /10Star/MIT/202205/js/代码少/mobile
  - https://github.com/Thinkei/hero-editor
  - http://hero-editor.surge.sh/
  - Hero editor is a WYSIWYG built on top of Slate (v0.58.3).
  - It's designed for mobile-first, hence all of the communications from plugins to the editor must go through message channel. 
  - This package also includes serializers and renderers for the Slate content.

- taze-editor /6Star/MIT/202211/ts
  - https://github.com/taze-editor/taze-editor
  - http://taze-editor.vercel.app/
  - Create your own plugin-based rich text editor easily
  - Taze Editor is built on top of Slate and heavily inspired by Plate.

- circu /1Star/MIT/202211/ts
  - https://github.com/Flrande/circu
  - 一个支持多人协同的在线文档应用
  - 修改了slate-react
  - 协作基于yjs

- react-rich-editor /3Star/MIT/202203/js
  - https://github.com/Rajatm544/react-rich-editor
  - https://reactricheditor.netlify.app/
  - A rich text editor built using React and Slate as part of the internship assignment for Plotline

- rich-slate /1Star/ts/active
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

- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.
# slate-based-editors
- boatproject-editor /1Star/MIT/202208/ts/plate/提交多
  - https://github.com/boatproject/editor
  - 依赖 plate、slate、styled-components
  - Rich text editor component for React. Built with Plate and MUI

- https://github.com/webkom/lego-editor /ts
  - A React rich text editor written in TS with Slate.js for lego-webapp
  - 代码量少，适合入门，支持上传图片

- @tinacms/toolkit
  - https://github.com/tinacms/tinacms/blob/main/packages/%40tinacms/toolkit
  - 依赖 @udecode/plate、headlessui、floating-ui

- https://github.com/accordproject/web-components/tree/master/packages/ui-markdown-editor
  - https://ap-web-components.netlify.app/
  - a WYSIWYG editor for markdown that conforms to the CommonMark specification
  - 依赖markdown-it、slate、semantic-ui-react

- dslate /6Star/MIT/202207/ts/antd
  - https://github.com/rojer95/dslate
  - https://rojer95.github.io/dslate/#/
  - https://rojer95.github.io/dslate/#/docs/getting-started
  - DSlate 是一个基于 Slate 构建的 Ant Design 风格的富文本编辑器

- slatejsx /48Star/Apache2/202203/js/antd
  - https://github.com/slatejsx/slatejsx
  - http://seditor.open.heyphp.com/
  - 项目基于slate.js框架开发，项目内所有图标，风格组件均使用antd

- https://github.com/slatable/slate /202006
  - 基于 slatejs 封装富文本编辑器

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
# slate-plugins
- https://github.com/hanford/remark-slate
  - Transform the contents of a slate 0.50+ editor into markdown and back again.
- https://github.com/inokawa/remark-slate-transformer
  - remark plugin to transform remark syntax tree (mdast) to Slate document tree, and vice versa. Made for WYSIWYG markdown editor.
- https://github.com/accordproject/markdown-transform
  - A transformation and parsing framework for converting markdown content to HTML, Slate (for rich-text editing) and other structured document object models (DOMs).
  - 提供了很多子包，本身类似于remark

- https://github.com/cihad/slate-table  /202107/ts
  - https://cihad.github.io/slate-table/
  - Table Plugin for Slate (based on @udecode/slate-plugins above v1.0). 
  - Inspired by the Atlassian editor's table plugin.
  - 依赖 slate.v0.61, @udecode/slate-plugins-table(2021)
- https://github.com/lqs469/slate-table  /202003/ts
  - https://slate-table.vercel.app/
  - A pretty Slate.js table plugin (Slate.js version > 0.5)
- https://github.com/daibin0809/slate-table-demo
  - 依赖event-emitter
  - slate 编辑器完成的一个表格功能，能够进行表格的选区、单元格操作和行列操作等操作。
  - 表格中无法再添加表格；
  - 表格中右键唤起工具菜单
- https://github.com/nod-engineering/slate-table
  - /202106/js

- https://github.com/1build/leyden
  - https://1build-org.gitbook.io/leyden/
  - a data table framework powered by Slate.
  - Leyden's coordinate system is simple and fully interoperable with Slate's Path system.
  - Cells can access data from other cells using absolute coordinates and relative positions.
  - Leyden exposes several pre-built validators (such as numeric and integer) for your cell data
  - Slate requires users to define complicated render functions to detect different types of elements. Leyden handles this automatically
  - Leyden builds upon Slate's schema definition system, providing an interface for users to define table-shaped schemas with powerfully customization cells.

- https://github.com/whatever-company/slate-tables
  - https://whatever-company.github.io/slate-tables/
  - 依赖slate.v0.47
  - A Slate plugin to handle table edition.
  - The plugin supports nested tables natively.
  - Colspan and Rowspan are supported. All operations create a matrix containing all cells' positions.
- https://github.com/jasonphillips/slate-deep-table
  - https://jasonphillips.github.io/slate-deep-table/
  - /201910/js/v0.44
  - Forked from the slate-edit-table implementation, allowing for creation of tables with nested content
  - https://github.com/George-A-Payne/slate-tables
    - Forked from slate-deep-tables

- https://github.com/shrutikachawla/slateTables /js
  - 依赖material-ui.v4、antd

- https://github.com/sodenn/react-fluent-edit
  - https://react-fluent-edit.vercel.app/
  - Brings easy-to-use mentions and rich text (WIP) features to Slate.

- https://github.com/afeiship/next-slate-plugin
  - Slate plugin manager.

- https://github.com/mwood23/slate-test-utils
  - A toolkit to test Slate rich text editors with Jest, React Testing Library, and hyperscript! 
  - There's so many user input mechanisms, edge cases, selection, state, normalization, and more to keep in mind when developing.
  - It's an abstraction that uses hyperscript to generate editor states that can be tested in a JSDOM environment with a bit of black magic.
  - It's well documented that JSDOM does not support `contenteditable`

- https://github.com/lukesmurray/use-slate-with-extensions
  - https://use-slate-with-extensions.netlify.app/
  - a simple, powerful, and tiny (< 2KB) hook which helps you build self contained and composable extensions for Slate. 

- https://github.com/enzoferey/slate-instant-replace
  - A Slate plugin that gives you full power on the last word your user typed.
  - This package is compatible with <= slate@0.47

- https://github.com/palerdot/react-slite /代码过于简单
  - This react component provides a slack like rich text editing experience powered by slate.js

- https://github.com/rockettomatooo/slate-react-presentation
  - a small package that lets you render a slate.js document without the overhead of the actual editor.
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

- https://github.com/madmaxmehdi44/platforms-slate-supabase
  - Build a blogging platform based on Slate.js, Supabase and Vercel.
  - Skip the PlanetScale installation and instead create a database on Supabase
  - [Platforms Starter Kit: a template for site builders, multi-tenant platforms, and low-code tools.](https://demo.vercel.pub/platforms-starter-kit)
  - [How to Build a Multi-Tenant App with Custom Domains Using Next.js](https://vercel.com/guides/nextjs-multi-tenant-application)
# slate-collab
- https://github.com/solidoc/slate-ot /ts/202006
  - Operation Transformations for slate 0.5x.
  - 依赖sharedb
- https://github.com/Immortalin/slate-operational-transform
  - Slate JS Editor Operational Transform Example using ShareDB (used in production at Narration Box)
  - Invoking JSON0-ot-diff on every edit is not very efficient.

- https://github.com/itoumlilt/crdt-md-editor /ts/slate
  - React Typescript CRDT based Collaborative Markdown Editor

- https://github.com/BitPhinix/slate-yjs-example
  - https://bitphinix.github.io/slate-yjs-example
  - Minimal example project for slate-yjs
  - [How to boostrap slate with a persisted doc?](https://github.com/BitPhinix/slate-yjs-example/issues/80)
  - https://github.com/BitPhinix/slate-yjs
    - Yjs binding for Slate

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
