---
title: toc-office-notion-like-editor-examples
tags: [block-editor, examples, notion]
created: 2022-06-03T21:57:31.178Z
modified: 2022-06-03T22:07:23.308Z
---

# toc-office-notion-like-editor-examples

# guide

- 编辑器功能检查
  - 是否支持跨block选择部分文字、并加粗 (重要)
  - 是否支持拖拽block修改顺序 (重要)
  - 支持协作

- 想要分析notion的block架构设计，可以参考clone示例
- block可以抽象成ast，结构设计可参考 gutenberg
- 除了数据模型层、视图层的设计，还要考虑持久化保存和实时更新的实现

- notion-resources
  - [The data model behind Notion's flexibility](https://www.notion.so/blog/data-model-behind-notion)
  - [A More Human Approach To Databases](https://ccorcos.github.io/filing-cabinets/)
    - Notion 工程师 Chet 以警察信息管理系统为例，用普通人能理解的大白话，从文件、文件夹、文件柜逐步介绍关系型数据库的构成和实现原理
  - [Notion 编辑器原理分析](https://zhuanlan.zhihu.com/p/359122473)
  - [探索 Notion 的实现](https://zhuanlan.zhihu.com/p/152964640)
  - [Notion 的数据协同原理](https://juejin.cn/post/7070062834901598216)
  - [Notion 编辑器是怎么实现的？](https://www.yuexun.me/blog/how-the-notion-editor-is-implemented/)
# notion-sketch-drawing
- https://github.com/MrFoxPro/bloki
  - https://bloki.app/
  - 支持在文档上放画板，ui设计友好
# notion-like-editor
- plate /1.6kStar/MIT/202208/ts
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - code-block自研实现，不依赖第三方代码编辑器
  - A plugin framework for building rich text editors with slate.

- tiny-write /4Star/NALic/202208/ts/prosemirror/markdown-it/web版+桌面版
  - https://github.com/dennis84/tiny-write
  - https://tiny-write.pages.dev/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 依赖solid-js、codemirror6、idb-keyval、date-fns、markdown-it、y-prosemirror
  - Just a little writing tool with markdown shortcuts that saves every change to local indexeddb.
  - 跨平台客户端基于tauri实现，tari部分使用rust实现

- https://github.com/sereneinserenade/notitap
  - https://sereneinserenade.github.io/notitap/
  - Notion like editor built on top of tiptap.
  - 块级拖拽是pro版，暂无预览体验

- https://github.com/kiaksarg/edu-editor  /slate
  - https://edu-editor.netlify.app/
  - a basic medium/notion like rich text editor based on Slate.js framework
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - 暂不支持块级拖拽

- whim-notion-like /6Star/MIT/202108/ts
  - https://github.com/coniel/whim 
  - A highly customisable block based rich text editor inspired by Notion.
  - 依赖 slate.v0.65.3，fuse.js(fuzzy-search)
  - Whim is currently undergoing a complete re-write for version 2.0, with an initial release planned for the end of August 2022. 
    - Version 2.0 will include a much improved API, detailed docs, and solid test coverage.

- blocky-editor /150Star/MIT/202208/ts
  - https://github.com/vincentdchan/blocky-editor
  - https://blocky-editor.dev/
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - 支持协作
  - an editor which supports the concept of blocks. It can help you to build an editor like Notion. 
  - Extensible. Extend the editor with custom blocks and spans.

- NotionEditor /30Star/GPL.v2/202103/ts/inactive
  - https://github.com/Xheldon/NotionEditor
  - A Notion's editor implement based on ProseMirror, just for feasibility studies.
  - 不允许跨 block 选择部分文本内容
  - 基础 schema 是两个 doc 和 text, 这是 Prosemirror 默认的两个最大和最小可编辑 schema. 而设计 schema 的时候我使用的最小编辑单元是 textblock, 表现形式是一个 div 中包含着 text
  - 所有的元素都是使用 div 进行模拟, 而不是使用语义化的 p/ul/ol 等进行, 这是为了摆脱浏览器的限制, 如段落嵌套段落的时候, p 标签无法嵌套块级元素等.
  - 使用了 React 构建界面的有: Slash

- cm-page-builder /26Star/ISC/202106/js/inactive/提交多
  - https://github.com/commutatus/cm-page-builder
  - http://cm-page-builder.herokuapp.com/
  - a modern rich text component based page builder inspired from Notion. 
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序

- https://github.com/ryuever/react-tapable-editor  /328Star/MIT/202010/ts
  - A pluginable, intuitive medium/notion like rich text editor
  - built on draft-js, and its plugin system is based on tapable which is famous as the engine of webpack.

- https://github.com/ericyip/hexx /archived
  - https://hexx.vercel.app/
  - notion like block editor in react
  - 不支持跨block选择部分文字
  - 不支持拖拽block修改顺序

- https://github.com/CedarXi/All-in-one
  - http://all-in-one.qingzhu.co/
  - https://all-in-one-kappa.vercel.app/
  - /63Star/NALic/202004/js/vue/inactive
  - All-in-one 是一个开源的模块化内容构建编辑器，基于Vue和element的打造
  - 它不同于传统的文本编辑器，所有的内容都是以模块的概念来打造。灵感来自Notion
  - 所有的模块都以VUE组件的形式编写，可以灵活插拔。
  - 所有组件保存的数据，都以Json的形式存储在Vuex里供不同组件调用

- https://github.com/fouita/tailwind-editor
  - notion like tailwindcss editor built with svelte
# notion-block-structure
- https://github.com/dragonman225/nast
  - A block-based intermediate representation for document-like content.
  - `nast-types`: A TypeScript type definition module to specify data models for intermediate representation of data.
  - `nast-util-from-notionapi`: Import data from a Notion page.
  - `nast-util-to-react`: Render data to JSX. Element or HTML. (Preferred)

- https://github.com/anconprotocol/parkydb
  - block based, linkable and verifiable document database
  - A data mesh database using Web 3.0 technology
  - Note: Requires Node v18 and up for development
  - 对数据的查询依赖 graphql.v15、graphql-compose-json

- https://github.com/tyleregeto/autoblock-editor
  - Very minimal multi-user block based document editor to play with CRDT in that context. 
  - Uses automerge for CRDT implementation. Doesn't do anything useful.
# notion-clone-with-workspace
- https://github.com/brenogcota/simple-notion-api-clone
  - a simple Notion API clone, made with Typescript, Express, Prisma ORM

- https://github.com/Mabloq/mabloq-notion
  - An implementation of the popular Workspace App: Notion.
  - 依赖 nestjs、mongoose、passport、rxjs
  - [Minimalist Notion Implementation: Part 1-Everything Is a Block](https://medium.com/@arcilamatt/minimalist-notion-implementation-part-1-everything-is-a-block-debda338b61a)

- https://github.com/minwook-shin/notion-database
  - https://notion-database.readthedocs.io/
  - Notion API Database Python Implementation
- https://github.com/dryadsoft/node-notion-database
  - 只是 notion database api 使用示例
- https://github.com/JPDesignTech/NotionAPI
  - This project's main goal is to show off all the cool things you can do with the Official Notion API. 
  - This project will use Nest.js as a framework to create a simple RESTful API whose endpoints will plug into Notion's API References

- https://github.com/zhaowb/notion-params
  - a helper to build Notion API params, parse markdown text into Notion API blocks, include a simple client support all APIs version
  - 基于python

- https://github.com/deve-sh/NoteItDown
  - https://noteitdown.vercel.app/
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - A Simple Yet Extensive Note Taking Workspace Application for an entire team. Inspired By Notion
  - Thanks to Chakra UI for making styling so simple.
  - A Simple Note Taking App For an Entire Team, pre-packaged with support for Google and GitHub logins with Firebase Auth, database as Firestore.

- https://github.com/konstantinmuenster/notion-clone
  - https://notion-clone.kmuenster.com/
  - /2.3kStar/MIT/202106/js
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 前端依赖 next9、react-beautiful-dnd、react-contenteditable，未使用复杂编辑器
  - 后端依赖 express、jsonwebtoken、mongoose
  -  This clone tries to replicate some of the great note-taking features Notion has.
  - The frontend is built with Next.js and fully server-side rendered. 
    - Next.js · React.js · SCSS/SASS
  - On the backend, a REST API handles saving user content and user management.
    - Express.js · MongoDB with Mongoose · Nodemailer · JWT (Cookie-based)

- https://github.com/tobi4120/notion-clone  /146Star/NALic/202203/js
  - https://notion-app-clone.herokuapp.com/
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 整体还原度非常高，包括page-tree
  - This website allows users to create pages, add notes to those pages, add to-do's, link to other pages and more!

- https://github.com/amjadbouhouch/notion-clone
  - https://notion-clone-react.netlify.app/
  - a front-end build with React and Tailwind CSS
  - 不支持跨block选择部分文字
  - 不支持拖拽block修改顺序

- https://github.com/tramio/JUN22-NOTION
  - https://tramio.github.io/JUN22-NOTION/
  - building a Notion clone with React.js and Firebase
  - 只实现了落地页，未实现编辑器

- https://github.com/fedeloterstein/open-notion
  - Notion clone using Next.js with Typescript
# notion-ecosystem
- https://github.com/NotionX/react-notion-x
  - https://react-notion-x-demo.transitivebullsh.it/
  - Fast and accurate React renderer for Notion.
  - react-notion-x is a fork of react-notion with better support for different types of Notion content (especially collections).
  - When we want to retrieve the content of a Notion page, using the Notion API we will obtain a complex block structure
  - This package solves that structure and takes care of rendering that response.

- https://github.com/splitbee/react-notion /inactive
  - A fast React renderer for Notion pages

- https://github.com/viqueen/notion-renderer
  - Simple and naive Notion react renderer, not as advanced as react-notion-x
- https://github.com/piotrzaborow/notion-blocks-react-renderer
  - React Renderer for @notionhq/client blocks

- https://github.com/tugboatcoding/react-potion  /js/inactive
  - A Notion-like design system

- https://github.com/nategadzhi/notoma
  - https://nategadzhi.github.io/notoma/
  - Use Notion as your blogging editor, with any static gen blog engine. Notoma converts Notion pages to Markdown files.

- https://github.com/takux/notion-block-renderer
  - This package is suitable for use with Reactjs or Nextjs. Notion blocks are rendered into React components. That component has a CSS class name corresponding to the block type.
- https://github.com/ridafkih/notion-react
  - Easily map Notion blocks to React components, completely customizable and type-safe

- https://github.com/webclipper/web-clipper
  - https://clipper.website/
  - For Notion, OneNote, Bear, Yuque, Joplin。Clip anything to anywhere

- https://github.com/tangly1024/NotionNext
  - 一个使用 NextJS + Notion API 实现的，部署在 Vercel 上的静态博客系统。为Notion和所有创作者设计。

- https://github.com/Lalit2005/pagely /inactive
  - Launch beautiful websites straight from your Notion workspace or from your GitHub repo
# more-notion-like
- https://anytype.io/
  - Anytype is a next generation software that breaks down barriers between applications, **gives back privacy and data ownership to users**.

- https://github.com/mraht-apps/notie
  - Notion-like workspace with offline mode and encryption
  - Completely offline (online synchronisation by storing encrypted file in cloud folder possible)

- https://github.com/gridaco/boring
  - A very boring text editor engine like notion. 

- https://github.com/likhaCMS/likhaCMS
  - https://likhacms.github.io/
  - a Web App Builder with Built-in UI Building Blocks, Drag and Drop Page Builder, Component Code Editor, Dev and Staging Environment
  - https://github.com/likhaCMS/likhaCMS.github.io

- https://github.com/bdryanovski/block-editor
  - Experimental block-editor based on the idea of Notion Editor - build only with WebComponents

- https://github.com/4teamwork/ftw.simplelayout
  - SimpleLayout provides an intuitive way of adding and arranging the different elements of a page such as paragraphs, images, files and links using drag-and-drop functionality. 
  - These elements are implemented as addable and easily arrangeable "blocks".

- https://github.com/GSS-Cogs/dd-cms
  - A data-driven content management system prototype, based on Plone/Volto and data blocks
  - https://github.com/plone/volto
    - React-based frontend for the Plone Content Management System

- https://github.com/jan9won/notion-page-tree/tree/main/packages/notion-page-tree
  - readme里面的短横文本构成的表格特别多
  - Pages inside non-page blocks are also fetched.
  - Max request-depth can be set in your preference.
