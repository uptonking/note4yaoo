---
title: toc-office-notion-like-examples
tags: [block-editor, examples, notion-like]
created: 2022-06-03T21:57:31.178Z
modified: 2023-11-28T14:48:45.911Z
---

# toc-office-notion-like-examples

# guide

- 编辑器功能检查
  - 是否支持跨block选择部分文字、并加粗 (重要)
  - 是否支持拖拽block修改顺序 (重要)
  - 支持协作

- 想要分析notion的block架构设计，可以参考clone示例
- block可以抽象成ast，结构设计可参考 gutenberg
- 除了数据模型层、视图层的设计，还要考虑持久化保存和实时更新的实现
  - 甚至可以考虑更通用的场景，如何将树型数据结构保存到数据库的表，如何打平更高效
  - 分层级的数据，探索更高效的方式

- notion-resources
  - [The data model behind Notion's flexibility](https://www.notion.so/blog/data-model-behind-notion)
  - [A More Human Approach To Databases](https://ccorcos.github.io/filing-cabinets/)
    - Notion 工程师 Chet 以警察信息管理系统为例，用普通人能理解的大白话，从文件、文件夹、文件柜逐步介绍关系型数据库的构成和实现原理
  - [Notion 编辑器原理分析](https://zhuanlan.zhihu.com/p/359122473)
  - [探索 Notion 的实现](https://zhuanlan.zhihu.com/p/152964640)
  - [Notion 的数据协同原理](https://juejin.cn/post/7070062834901598216)
  - [Notion 编辑器是怎么实现的？](https://www.yuexun.me/blog/how-the-notion-editor-is-implemented/)
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

- notitap /39Star/MIT/202209/ts
  - https://github.com/sereneinserenade/notitap
  - https://sereneinserenade.github.io/notitap/
  - 依赖daisyui、tippyjs、floating-ui、fuzzysort
  - Notion like editor built on top of tiptap.
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但list item不支持拖入拖出

- novel /13.7kStar/apache2/202501/ts
  - https://github.com/steven-tey/novel
  - https://novel.sh/
  - Notion-style WYSIWYG editor with AI-powered autocompletion. 
  - Built with [Tiptap](https://tiptap.dev/) + [Vercel AI SDK](https://sdk.vercel.ai).
  - 依赖tiptap、@vercel/kv/blob、nextjs、react-markdown.v8、tailwindcss

- https://github.com/kiaksarg/edu-editor  /slate
  - https://edu-editor.netlify.app/
  - a basic medium/notion like rich text editor based on Slate.js framework
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序
  - 暂不支持块级拖拽

- whim-notion-like /6Star/MIT/202108/ts
  - https://github.com/coniel/whim-editor
  - A highly customisable block based rich text editor inspired by Notion.
  - core依赖 slate.v0.65.3，fuse.js(fuzzy-search)
  - ui依赖@braindrop-editor/core
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序，特别是支持将list item拖入拖出列表
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
  - Currently, the document tree of BlockyEditor supports collaborative editing using operation transforming(known as OT).
  - You can also use a CRDT library such as YJS and bind the data model to it.

- NotionEditor /30Star/GPLv2/202103/ts/inactive
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

- boring-editor /10Star/MIT/202205/ts/tiptap
  - https://github.com/gridaco/boring
  - A very boring text editor engine like notion.
  - 不支持block-ui
  - 支持斜杠菜单、协作
  - 依赖tiptap2、yjs

- https://github.com/ericyip/hexx /archived
  - https://hexx.vercel.app/
  - notion like block editor in react
  - 不支持跨block选择部分文字
  - 不支持拖拽block修改顺序

- https://github.com/CedarXi/All-in-one /63Star/NALic/202004/js/vue/inactive
  - http://all-in-one.qingzhu.co/
  - https://all-in-one-kappa.vercel.app/
  - All-in-one 是一个开源的模块化内容构建编辑器，基于Vue和element的打造
  - 它不同于传统的文本编辑器，所有的内容都是以模块的概念来打造。灵感来自Notion
  - 所有的模块都以VUE组件的形式编写，可以灵活插拔。
  - 所有组件保存的数据，都以Json的形式存储在Vuex里供不同组件调用

- https://github.com/shreyasmanolkar/notion-browser-client /MIT/202308/ts
  - https://www.notion-s.co/
  - develop a comprehensive clone resembling the popular platform Notion.
  - 依赖tiptap、reduxjs/toolkit、firebase
  - https://github.com/shreyasmanolkar/notion-api /ts
    - Notion Clone API built with TypeScript and MongoDB, using TDD
    - 依赖mongodb、express
  - [Building Notion Clone: Part 1 — Planning the Architecture | by Shreyas manolkar | Medium _202307](https://medium.com/@shreyasmanolkar123/building-notion-clone-part-1-planning-the-architecture-f50342e58019)
  - [Building Notion Clone: Part 2 — Crafting the Front-end Experience | by Shreyas manolkar | Medium _202307](https://medium.com/@shreyasmanolkar123/building-notion-clone-part-2-crafting-the-front-end-experience-cb194c1d132c)

- https://github.com/Mabloq/mabloq-notion /apache2/202304/ts
  - An implementation of the popular Workspace App: Notion.
  - 依赖 nestjs、mongoose、passport、rxjs
  - [Minimalist Notion Implementation: Part 1-Everything Is a Block_202203](https://medium.com/@arcilamatt/minimalist-notion-implementation-part-1-everything-is-a-block-debda338b61a)

- https://github.com/fouita/tailwind-editor
  - notion like tailwindcss editor built with svelte

- https://github.com/ryuever/react-tapable-editor /328Star/MIT/202010/ts
  - A pluginable, intuitive medium/notion like rich text editor
  - built on draft-js, and its plugin system is based on tapable which is famous as the engine of webpack.

- https://github.com/desyed/likho /202308/ts
  - https://likho.site/
  - AI powered, multi-tenant website builder with notion like WYSIWYG.

- https://github.com/youking-lib/marktion
  - https://editor.marktion.io/
  - an inspiring markdown editor

- https://github.com/gabrielcoder247/notion-like-editor
  - https://notion-like-editor-kappa.vercel.app/
  - a react based text editor that allows a user to add text anywhere and covert the text to H1

- https://github.com/omarsalem7/notion
  - https://notion-editor.netlify.app/
  - a simple functionality for notion like h1, h2.

- https://github.com/factly/scooter /202308/js
  - https://scooter-storybook.pages.dev/
  - a Notion like editor built on top of TipTap & Prosemirror
  - https://github.com/factly/dega /go
    - lightweight, scalable & high performant CMS written in Go & React
# notion-block-api/self-hosted
- https://github.com/dragonman225/nast /MIT/202211/ts/inactive
  - ✨ A block-based intermediate representation for document-like content.
  - `nast-types`: A TypeScript type definition module to specify data models for intermediate representation of data.
  - `nast-util-from-notionapi`: Import data from a Notion page.
  - `nast-util-to-react`: Render data to JSX. Element or HTML. (Preferred)

- https://github.com/makenotion/notion-sdk-js
  - Official Notion JavaScript Client
  - api-endpoints提供了model定义

- https://github.com/justjake/monorepo/tree/main/packages/notion-api
  - The missing companion library for the official Notion public API.

- https://github.com/onedebos/notion-api-server-demo
  - This NodeJS application demonstrates how to read and write data to your Notion Workspace using the new Notion APIs.

- https://github.com/benborgers/potion /MIT/202111/js/inactive
  - Reverse-engineered Notion API
  - Write your content in Notion, and use Potion's hosted API endpoints to read your content.
  - 🗑️ I no longer maintain Potion, since the official Notion API has been released and is more stable than Notion’s internal API, which Potion relies on.

- https://github.com/anconprotocol/parkydb
  - block based, linkable and verifiable document database
  - A data mesh database using Web 3.0 technology
  - Note: Requires Node v18 and up for development
  - 对数据的查询依赖 graphql.v15、graphql-compose-json

- https://github.com/tyleregeto/autoblock-editor
  - Very minimal multi-user block based document editor to play with CRDT in that context. 
  - Uses automerge for CRDT implementation. Doesn't do anything useful.

- https://github.com/brenogcota/simple-notion-api-clone
  - a simple Notion API clone, made with Typescript, Express, Prisma ORM

- notionapi /1.7kStar/BSD/202208/go
  - https://github.com/kjk/notionapi
  - https://developers.notion.com/reference/block
  - [Using Notion API Go client](https://blog.kowalczyk.info/article/c9df78cbeaae4e0cb2848c9964bcfc94/using-notion-api-go-client.html)
# notion-sketch-drawing
- https://github.com/MrFoxPro/bloki
  - https://bloki.app/
  - 支持在文档上放画板，ui设计友好
# notion-api-usage
- https://github.com/minwook-shin/notion-database
  - https://notion-database.readthedocs.io/
  - Notion API Database Python Implementation
- https://github.com/dryadsoft/node-notion-database
  - 只是 notion database api 使用示例
- https://github.com/JPDesignTech/NotionAPI
  - This project's main goal is to show off all the cool things you can do with the Official Notion API. 
  - This project will use Nest.js as a framework to create a simple RESTful API whose endpoints will plug into Notion's API References

- https://github.com/justjake/monorepo/tree/main/packages/notion-api
  - Use Notion as a headless content management system a la Contentful.
  - Recursively fetch page content while building backlinks.

- https://github.com/zhaowb/notion-params
  - a helper to build Notion API params, parse markdown text into Notion API blocks, include a simple client support all APIs version
  - 基于python
# notion-clone-frontend
- https://github.com/deve-sh/NoteItDown
  - https://noteitdown.vercel.app/
  - 不支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - A Simple Yet Extensive Note Taking Workspace Application for an entire team. Inspired By Notion
  - Thanks to Chakra UI for making styling so simple.
  - A Simple Note Taking App For an Entire Team, pre-packaged with support for Google and GitHub logins with Firebase Auth, database as Firestore.

- notion-clone /2.3kStar/MIT/202106/js/inactive
  - https://github.com/konstantinmuenster/notion-clone
  - https://notion-clone.kmuenster.com/
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

- https://github.com/AntonioErdeljac/notion-clone-tutorial /202310/ts
  - https://note-taking-app-rose.vercel.app/
  - Fullstack Notion Clone: Next.js 13, React, Convex, Tailwind | Full Course 2023

- https://github.com/amjadbouhouch/notion-clone /仅前端
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

- https://github.com/BadaHertz52/notion /202212/ts/提交多
  - cloning Notion with React
  - 依赖react-contenteditable、redux、styled-components
- https://github.com/genuine-seok/motion-web /202209/ts
  - https://genuine-seok.github.io/motion-web/
  - [toy project] notion basic features cloning project

- https://github.com/Lameck1/simple_notion /202212/js/NoDeps
  - https://simplenotion.netlify.app/
  - lightweight clone of a Notion-like editor.

- https://github.com/girishsontakke/notion-task-board-clone /202211/js
  - https://notion-task-board-clone.netlify.app/
  - Notion task board clone having drag and drop functionality.
  - 依赖antd

- https://github.com/hr0123/vanillajs-notion-clone-haeri /202210/ts/starter
  - brew install pkg-config cairo pango libpng jpeg giflib

- https://github.com/wendelchinsamy/notion-clone-web
  - https://github.com/wendelchinsamy/notion-clone-api

- https://github.com/huewilliams/notion-clone /202311/ts
  - https://notion-clone-kappa.vercel.app/
  - notion.so clone (React + ProseMirror)
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
- https://github.com/takux/notion-block-renderer
  - This package is suitable for use with Reactjs or Nextjs. Notion blocks are rendered into React components. That component has a CSS class name corresponding to the block type.

- https://github.com/tugboatcoding/react-potion  /js/inactive
  - A Notion-like design system

- https://github.com/tryfabric/martian
  - Convert Markdown and GitHub Flavoured Markdown to Notion API Blocks and RichText 

- https://github.com/nartc/notion-stuff
  - Notion Blocks to Markdown parser
  - Notion Blocks to HTML parser

- https://github.com/nategadzhi/notoma
  - https://nategadzhi.github.io/notoma/
  - Use Notion as your blogging editor, with any static gen blog engine. Notoma converts Notion pages to Markdown files.

- https://github.com/ridafkih/notion-react
  - Easily map Notion blocks to React components, completely customizable and type-safe

- https://github.com/webclipper/web-clipper
  - https://clipper.website/
  - For Notion, OneNote, Bear, Yuque, Joplin。Clip anything to anywhere

- https://github.com/tangly1024/NotionNext
  - 一个使用 NextJS + Notion API 实现的，部署在 Vercel 上的静态博客系统。为Notion和所有创作者设计。

- https://github.com/Lalit2005/pagely /inactive
  - Launch beautiful websites straight from your Notion workspace or from your GitHub repo

- https://github.com/Dashibase/lotion /GPLv3/vue/ts
  - An open-source Notion UI built with Vue 3
# more-notion-like
- https://github.com/tzhangchi/Travel
  - https://tzhangchi.github.io/Travel/
  - Building travels and blocks , presentation like a doc, travel is written by react+ lit + yjs + vite + tailwind.css

- https://anytype.io/
  - Anytype is a next generation software that breaks down barriers between applications, **gives back privacy and data ownership to users**.

- https://github.com/mraht-apps/notie
  - Notion-like workspace with offline mode and encryption
  - Completely offline (online synchronisation by storing encrypted file in cloud folder possible)

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

- [Building a Notion-like system with Socket.io And React](https://novu.co/blog/building-a-notion-like-system-with-socket-io-and-react/)
