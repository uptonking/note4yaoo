---
title: lib-editor-tiptap-examples
tags: [examples, prosemirror, tiptap-editor, toc]
created: 2022-08-19T23:00:04.811Z
modified: 2023-02-05T19:03:27.730Z
---

# lib-editor-tiptap-examples

# guide

- resources
  - https://github.com/ueberdosis/awesome-tiptap
  - https://tiptap.dev/experiments
  - [提供了类似块编辑器的drag示例](https://tiptap.dev/guide/node-views/examples)
# popular
- BlockNote /14Star/MPL.v2/202208/ts
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

- think /1kStar/MIT/202208/ts/nestjs
  - https://github.com/fantasticit/think
  - https://think.codingit.cn/
  - 依赖 MySQL/NextJS/nestjs/tiptap
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 前端依赖 @douyinfe/semi-ui、excalidraw、tiptap2、docx、katex、markdown-it、nextjs、react-pdf、react-query3、tippy.js、yjs
  - 后端依赖 nestjs、passport、typeorm、mysql、yjs
  - Think 是一款开源知识管理工具。通过独立的知识库空间，结构化地组织在线协作文档，实现知识的积累与沉淀，促进知识的复用与流通。同时支持多人协作文档。

- notesnook /2.8kStar/GPL.v3/202209/js+ts/tiptap
  - https://github.com/streetwriters/notesnook
  - https://notesnook.com/
  - open source & end-to-end encrypted note taking alternative to Evernote.
  - web编辑器和移动端编辑器都依赖tiptap2、zustand、unfurl.js(oembed)、re-resizable、katex
  - @notesnook/streamable-fs: Streaming interface around an IndexedDB based file system
  - Notesnook encrypts everything on your device using XChaCha20-Poly1305 & Argon2.
  - 服务端数据同步代码未找到
  - [A fully open-source and end-to-end encrypted note taking alternative to Evernote | Hacker News_202209](https://news.ycombinator.com/item?id=32708019)

- https://github.com/chenyuncai/tiptap-track-change-demo /vue
  - https://track-change.onrender.com/
  - [Implement new track changes in current document, just lice office review mode](https://discuss.prosemirror.net/t/implement-new-track-changes-in-current-document-just-lice-office-review-mode/4890)

- https://github.com/johnpuddephatt/gutentap
  - https://gutentap.letsdance.agency/
  - Tiptap based block editor
  - a UI for Tiptap, inspired by the Wordpress editor, Gutenberg. It uses a static floating toolbar as well as slash commands for inserting new blocks.

- novel /7.3kStar/MIT/202309/ts
  - https://github.com/steven-tey/novel
  - https://novel.sh/
  - a Notion-style WYSIWYG editor with AI-powered autocompletion. Built with [Tiptap](https://tiptap.dev/) + [Vercel AI SDK](https://sdk.vercel.ai).
  - 依赖tiptap、@vercel/kv/blob、nextjs、react-markdown.v8
  - [Show HN: I made an open-source Notion-style WYSYWIG editor | Hacker News_202306](https://news.ycombinator.com/item?id=36360789)

- better-virgool /9Star/MIT/NALic/202208/ts/tiptap
  - https://github.com/ahhshm/better-virgool
  - https://ahhshm.github.io/better-virgool/
  - An attempt to create a better rich text editor than virgool.io. Powered by Tiptap and ProseMirror
  - 实现了RTL国际化方向
  - 数据保存使用了 idb-keyval

- neeto-editor /10Star/MIT/202208/js/tiptap/提交多
  - https://github.com/bigbinary/neeto-editor
  - https://neeto-editor.onrender.com/
  - [editor demo with addons](https://neeto-editor.onrender.com/?path=/docs/examples-customize-options-addons--addons)
  - 支持定义变量
  - neetoEditor library drives the rich text experience in the neeto products built at BigBinary

- boring-editor /10Star/MIT/202205/ts/tiptap
  - https://github.com/gridaco/boring
  - A very boring text editor engine like notion.
  - 不支持block-ui
  - 支持斜杠菜单、协作
  - 依赖tiptap2、yjs

- markgh /6Star/NALic/202208/ts/提交多
  - https://github.com/EvitanRelta/markgh
  - https://evitanrelta.github.io/markgh/
  - 依赖 mui5、redux-toolkit、tiptap、dexie、highlight.js、markdown-it、quill

- typist /8Star/MIT/202211/ts
  - https://github.com/Doist/typist
  - https://typist.doist.dev/
  - Typist is the mighty Tiptap-based rich-text editor React component that powers Doist products
  - 提供了纯文本和富文本2种输入模式
  - Typist also supports a plain-text mode, and comes with HTML/Markdown serializers.

- linked-daily /561Star/GPL.v3/202208/js/vue/electron
  - https://github.com/lostdesign/linked
  - https://uselinked.com/
  - Daily journaling without distraction.
  - Search across all days
  - 依赖 vue2、highlight.js、electron-store
- https://github.com/m1911star/mermaid-editor-example
  - 依赖tiptap2、mermaid、react、electron
  - 代码少，适合入门

- gitlab-editor /3916Star/MIT/202208/js/vue2/tiptap2
  - https://gitlab.com/gitlab-org/gitlab/-/tree/master/app/assets/javascripts/content_editor
  - [WYSIWYG editor toolkit architecture proposal__2021](https://gitlab.com/gitlab-org/gitlab/-/issues/273238)
    - implementing support for all of md flavors is an unnecessary cost.
    - Solution 1: Traceability or file diffs
    - Solution 2: Relying on the Markdown preview endpoint
  - ref
    - https://github.com/gitlabhq/gitlabhq/tree/master/app/assets/javascripts/content_editor
# tiptap-editors
- dante3 /1.7kStar/MIT/202208/js
  - https://github.com/michelson/Dante
  - https://www.dante-editor.dev/
  - 依赖 emotion、polished、react-json-view、yjs
  - Just another medium clone built on top of ProseMirror/TipTap
  - Dante3(tiptap2): a Tiptap port of Dante2
  - Dante2(draftjs): Bad mobile support, big size(immutablejs), no realtime collab
  - Dante1(vanillajs): rely a lot on DOM manipulation

- wix-tiptap-editor /260Star/MIT/202008/ts
  - https://github.com/wix/ricos
  - https://wix-rich-content.herokuapp.com/
  - https://ricos.js.org/docs/ricos/ricos-intro
  - 每行前有加号，但每行不支持拖拽block修改顺序
  - A React-based rich content editor with an extensible plugin system
  - wix公司开源了自己的内容编辑器，公开了自己的json schema规范，提供了wix-rich-content-editor、wix-rich-content-viewer
  - 还支持在基于tiptap v2的编辑器中编辑内容，提供了draftToTiptap()转换方法，将ricos-draft的json格式转换成tiptap支持的json格式
  - 内部插件大多严重依赖自研ui库和基础库，如wix-rich-content-ui-components、ricos-content

- nextcloud-text /366Star/AGPLv3/202208/js/tiptap/php
  - https://github.com/nextcloud/text
  - Collaborative document editing using Markdown
  - 依赖tiptap.v2, @_ueberdosis/prosemirror-tables.v1.1.3, markdown-it、vue2、vuex3

- element-tiptap /825Star/MIT/202208/ts/vue/tiptap/inactive
  - https://github.com/Leecason/element-tiptap
  - https://element-tiptap.vercel.app/
  - WYSIWYG rich-text editor using tiptap and Element UI for Vue2 (tiptap2 and Vue3 is in alpha)
  - new version2 support Vue3, use tiptap2 and Element Plus

- https://github.com/lobbylabs/lobby-editor
  - https://lobby-editor-demo.vercel.app/
  - extendable rich text editor for Vercel's Next React framework, based on ProseMirror, built using TipTap. 
  - This project grew out of our internal usage at Lobby

- https://github.com/yuanzong/mui-editor
  - Rich text editor built on Material-ui.v5 and Tiptap

- https://github.com/essential-randomness/boba-editor-next
  - Next-generation editor for BobaBoard (and beyond). 
  - 代码量很少

- https://github.com/KonnorRogers/tip-tap-element
  - http://tip-tap-element.vercel.app/
  - WYSIWYG editing experience that can hook into Ruby on Rails ActionText backend. 

- @sensenet/editor-react
  - https://github.com/SenseNet/sn-client
  - Text editor library behind rich text editor is changed to tiptap@2.0
  - As a first step only those text editing features are implemented
  - More new things (managing tables, embedding, etc.) are coming in the following releases.

- https://github.com/pierre-lgb/slashwriter
  - 依赖tiptap.v2、redux-toolkit、supabase、express、yjs

- https://github.com/bcc-code/bcc-live-transcriber
  - 依赖tiptap.v2、yjs、vue3
  - A live transcribing app for sharing a meeting with deaf people.
  - The idea is to offer a simplistic keyboard only transcriber app with real time streaming and support for insterting bible verses.

- https://github.com/iojanis/Lity
  - 依赖tiptap.v2、yjs、vue3
  - Graph-based document editor with collaborative features
  - Create nodes by mouse, keyboard shortcuts or using markup (like @ and soon #)

- https://github.com/Young6118/dudu-editor
  - 基于 tiptap v2 的富文本编辑器

- https://github.com/shikimori/shiki-editor /js/vue/提交多/active
  - a wysiwyg editor based on prosemirror
  - highly inspired by tiptap source code. Many parts of the code are taken from there.

- https://github.com/bons-space/bons-editor
  - A WYSIWYG rich-text editor using tiptap and Element Plus for Vue3

- https://github.com/AventusKent/tiptap-react
  - Super light rich text editor based on TipTap and React

- https://github.com/g-bastianelli/tiptap-react-notion
  - Quick example of how we can make a 'Notion like' editor with Tiptap and react
# tiptap-utils
- https://github.com/troop-dev/tiptap-react-render
  - This library renders TipTap JSON payloads in React clients without embedding the editor.
  - We were inspired by Contentful's rich-text-react-renderer tool, so we built a similar one for TipTap payloads!

- https://github.com/sereneinserenade
  - https://github.com/sereneinserenade/tiptap-comment-extension-react
    - https://github.com/sereneinserenade/tiptap-comment-extension
    - https://sereneinserenade.github.io/tiptap-comment-extension/
    - Google-Docs like commenting solution for Tiptap 2
  - https://github.com/sereneinserenade/tiptap-search-n-replace-demo
  - https://github.com/sereneinserenade/tiptap-snippets-extension
    - drag-n-drop snippets into Tiptap. 
  - https://github.com/sereneinserenade/tiptap-extension-video
  - https://github.com/sereneinserenade/tiptap-media-resize
    - https://github.com/breakerh/tiptap-image-resize

- https://github.com/GoCapsule/tiptap-extensions
  - https://codesandbox.io/p/github/leonard-henriquez/column-extension/main
  - 支持选中文字后创建分栏，并将选中文字放在第一栏

- https://github.com/n8b8dy/tiptap-spoiler
  - React extension (actually two extensions) for TipTap to add spoilers to the editor.
  - http://zetamen.github.io/ckeditor-spoiler/ /ckeditor4

- https://github.com/yaskevich/extension-marker
  - Tiptap extension for setting custom class of the inline node (mark)

- https://github.com/benasher44/prosemirror-nodenext
  - Developer Ready: A comprehensive template.

- https://github.com/panGenerator/extension-small
  - `<small>` tag 小一号的字体
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/small

- https://github.com/farscrl/tiptap-extension-spellchecker
  - This is an extension to integrate a spellchecker into the tiptap editor.
  - The extension does not implement a spellchecker itself: you have to pass it a proofreader object implementing the IProofreaderInterface interface. 
  - That proofreader can work locallyin the browser, or it can call an online service, 
  - This extension is inspired by the tiptap-languagetool extension.

- [Tiptap CodeBlock Extension](https://gist.github.com/Itsnotaka/7eb107dcfe18225eeab66263339a8074)
  - Decided to ditch shiki and use highlightjs

## tiptap-ruby

- rhino-editor /26Star/MIT/202212/ts/ruby
  - https://github.com/KonnorRogers/rhino-editor
  - https://rhino-editor.vercel.app/
  - a grab and go WYSIWYG editing experience that can hook into Ruby on Rails ActionText backend.
  - Currently this package does so using TipTap but will most likely include another integration for ProseMirror to allow for both Markdown + WYSIWYG editing.

- https://github.com/afomera/richer-text.js /js
  - https://github.com/afomera/richer_text /ruby
  - A Richer Text Editor experience based on Tiptap
  - written in React, using the TipTap libraries and extensions, compiled into a web component
  - RicherText aims to provide a richer text editing experience than what comes out of the box with ActionText in Rails. 
  - It is however a separate thing from ActionText and is not backwards compatible.
  - 依赖@rails/activestorage、tiptap、react-to-webcomponent
  - Basic image uploading for ActiveStorage
  - not-yet
    - Support for disabling extensions/portions out of the library.
    - There is a hardcoded requirement for `ActionStorage` to be installed and setup for Image support to work. 

- https://github.com/decidim/decidim
  - Decidim is a participatory democracy framework, written in Ruby on Rails, originally developed for the Barcelona City government online and offline participation website
  - [To Trix or not to Trix · Discussion](https://github.com/decidim/decidim/discussions/7585)

- [Thoughts on Action Text](https://www.reddit.com/r/rails/comments/rt2qvo/thoughts_on_action_text/)
  - Action Text seems too coupled to Trix
# examples
- https://github.com/SkyGuardian42/piko.space /202212/ts
  - https://piko.space/
  - Collaborate at the speed of light and seamlessly sync offline work
  - tiptap的协作示例
  - redis、yjs、tiptap
  - 前端依赖tiptap、radix-ui、tan-query、yjs、zustand
  - 后端依赖trpc、express、yjs、zod

- rockeseat-ignite-rotion /1Star/ISC/202212/ts
  - https://github.com/wfl-junior/rockeseat-ignite-rotion
  - An alternative to Notion built with Electron
  - 依赖tiptap、electron、radix-ui、tanstack-query

- https://github.com/justinmoon/tiptap-markdown-demo
  - TipTap rich text editor doesn't support markdown, but this repo shows how to hack it in yourself.

- notes /4Star/GPL.v3/202208/js
  - https://github.com/keymorph/notes
  - https://notes.keymorph.com/
  - 依赖tiptap2、dnd-kit、mui、tanstack-query、nextjs、@azure/cosmos--db
  - A free web application for creating and editing notes.

- note-it /16Star/Apache2/202208/ts/tiptap
  - https://github.com/MuhametSmaili/note-it
  - https://www.youtube.com/watch?v=jxBAMwxbk78
  - NoteIt is a feature-packed, note-taking extension with OCR support for chrome.
  - 依赖React、Tiptap、tesseract.js、pdfmake、html-to-pdfmake
  - You can take notes, convert images to text, download notes to pdf, and more.

- FireFire /9Star/ISC/202208/js
  - https://github.com/coolerwu/FireFire
  - 一款着力于本地的笔记软件，支持Windows、Mac

- https://github.com/boxraiser/visual-editor
  - Edit your page block by block

- chirpy /328Star/Apache2/202208/ts
  - https://github.com/devrsi0n/chirpy
  - https://chirpy.dev/
  - a privacy-friendly and customizable Disqus(comment system) alternate. 
  - for analytics, we self-hosted a plausible instance to avoid sharing your customer's data with third-party companies
  - https://github.com/plausible/analytics
    - 基于elixir

- https://t.co/cSLL2bvRp6
  - using @tailwindcss @tiptap_editor @vuejs & @nuxt_js
# cms-like
- vrite /1kStar/AGPLv3/202307/ts
  - https://github.com/vriteio/vrite
  - https://vrite.io/
  - https://editor.vrite.io/
  - headless CMS intended for technical content like programming blogs or documentation
  - 后端依赖trpc-server/openapi、fastify、yjs、zod、open-graph-scraper
  - 协作依赖mongodb、hocuspocus
  - 前端依赖solid-js、solid-primitives、tiptap、trpc-client、yjs
  - editor包不依赖solid-js
  - Built-in Kanban dashboard for managing content production and delivery; 
  - Versitile API and Extension System for customizing your experience and delivering content to any frontend; 

- alinea /654Star/MIT/202301/ts
  - https://github.com/alineacms/alinea
  - https://alinea.sh/
  - an open source headless CMS written in Typescript.
  - 非wysiwyg，左侧编辑块数据，右侧预览
  - 依赖dnd-kit、yjs、react-query
  - Content is stored in flat files and committed to your repository
  - 👀 Content is easily queryable through an in-memory SQLite database
  - Content is fully typed
  - Alinea supports custom backends that can be hosted as a simple Node.js process or on serverless runtimes.

- https://github.com/primodotso/primo
  - https://primo.so/
  - ui基于svelte
  - Primo is a component-based CMS that makes it easy to build visually-editable static sites

- https://github.com/verbb/vizy /php
  - A flexible visual editor for Craft CMS
  - 依赖tiptap2、vue3、tippy.js、codemirror-editor-vue
# fans-tiptap
- https://github.com/xiaohanyu
  - Spent another two days to write a recursive descent evaluation to convert 
@tiptap_editor
 's JSON format to TeX snippet

# more
- https://github.com/ujw0712/editor-and-pdf
  - 依赖 vue3、jspdf, html2canvas、@tiptap/extension-collaboration, yjs, @hocuspocus/provider

- https://github.com/ParamagicDev/tip-tap-element /ruby
  - https://tip-tap-element.vercel.app/
  - A starter kit for tip-tap to get going

- https://github.com/ueberdosis/tiptap-php
  - A PHP package to work with Tiptap content. 
  - You can transform Tiptap-compatible JSON to HTML, and the other way around, sanitize your content, or just modify it.

- https://github.com/iqb-berlin/studio-lite
  - Authoring system for online assessments.
  - This project replaces the https://github.com/iqb-berlin/teststudio-lite-setup
    - backend is refactored in nestjs

- https://github.com/manifoldmarkets/manifold
  - Manifold Markets: A market for every question
  - Manifold's public API and web app are hosted by Vercel.
  - All data is stored in Firebase's database, Cloud Firestore. 

- https://github.com/nurullahhossain/resume-builder
  - http://resume-builder-xi.vercel.app/

- https://github.com/Leosouthey/Raphael
  - 开源的个人/团队知识库系统

- https://github.com/nanmenyu/inking
  - inking是个人开发的开源桌面码字软件，面向的群体主要是网文写手，包含写作（核心）和阅读（附带）两大模块
  - 内置关系图、灵感备忘、时间线、地图、webview等辅助模块
