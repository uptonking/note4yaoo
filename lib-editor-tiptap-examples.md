---
title: lib-editor-tiptap-examples
tags: [examples, prosemirror, tiptap-editor, toc]
created: 2022-08-19T23:00:04.811Z
modified: 2023-02-05T19:03:27.730Z
---

# lib-editor-tiptap-examples

# guide

- resources
  - https://tiptap.dev/experiments
  - [提供了类似块编辑器的drag示例](https://tiptap.dev/guide/node-views/examples)
# popular
- https://github.com/ueberdosis/awesome-tiptap
  - Delightful Tiptap packages and resources

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

- think /1kStar/MIT/202208/ts/nestjs
  - https://github.com/fantasticit/think
  - https://think.codingit.cn/
  - 依赖 MySQL/NextJS/nestjs/tiptap
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - 前端依赖 @douyinfe/semi-ui、excalidraw、tiptap2、docx、katex、markdown-it、nextjs、react-pdf、react-query3、tippy.js、yjs
  - 后端依赖 nestjs、passport、typeorm、mysql、yjs
  - Think 是一款开源知识管理工具。通过独立的知识库空间，结构化地组织在线协作文档，实现知识的积累与沉淀，促进知识的复用与流通。同时支持多人协作文档。
  - https://github.com/fantasticit/magic-editor /202301/ts
  - https://github.com/fantasticit/sailkit /202407/ts/inactive
    - A toolkit editor suite based on tiptap and prosemirror.

- https://github.com/xun082/DocFlow /MIT/202507/ts
  - https://www.codecrack.cn/
  - 一个基于 Tiptap 和 Next.js 构建的现代化协同文档编辑器，集成了丰富的编辑能力与多人实时协作功能，支持插件扩展、主题切换与持久化存储。
  - 适合团队写作、教育笔记、在线文档平台等场景。
  - 实时协作：使用 Yjs + @hocuspocus/provider 实现高效协同
  - 插件丰富：基于 Tiptap Pro 多种增强功能（如表情、详情组件等）
  - 后端依赖nestjs、fastify、hocuspocus、prisma、minio、ioredis

- https://github.com/docs-plus/docs.plus /78Star/MIT/202507/ts
  - http://docs.plus/
  - a real-time community collaboration platform
  - 依赖Supabase、tiptap、hocuspocus/yjs、next、react-query、zustand

- notesnook /2.8kStar/GPLv3/202209/js+ts/tiptap
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
  - https://github.com/chenyuncai/tiptap-track-change-extension /MIT/202308/ts/inactive

- https://github.com/johnpuddephatt/gutentap
  - https://gutentap.letsdance.agency/
  - Tiptap based block editor
  - a UI for Tiptap, inspired by the Wordpress editor, Gutenberg. 
  - It uses a static floating toolbar as well as slash commands for inserting new blocks.

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

- https://github.com/osuresearch/annotator /MIT/202305/ts/inactive
  - https://osuresearch.github.io/annotator
  - React components for annotating forms and documents
  - 依赖tiptap2、@osuresearch/ui、mantine-hooks、iframe-resizer、react-aria、react-hook-form
  - https://github.com/osuresearch/ui
    - https://osuresearch.github.io/ui/v5
    - Research UI is The Ohio State University's Office of Research component library, based on Ohio State's design system - BUX.
    - 依赖react-aria
  - https://github.com/osuresearch/electron-example
    - Electron React Boilerplate uses Electron, React, React Router, Webpack and React Fast Refresh.

- https://github.com/Seedsa/echo-editor /583Star/MIT/202507/ts/vue
  - https://echo-editor.jzcloud.site/
  - A modern AI-powered WYSIWYG rich-text editor for Vue, based on Tiptap and shadcn-vue
  - Markdown support with real-time preview

- neeto-editor /12Star/MIT/202311/js/tiptap/提交多
  - https://github.com/neetozone/neeto-editor
  - https://github.com/bigbinary/neeto-editor
  - https://neeto-editor.onrender.com/
  - https://neeto-editor.neeto.com/
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
  - Online WYSIWYG GFM editor. Same look as Github's markdown. Supports HTML-in-Markdown

- typist /8Star/MIT/202211/ts
  - https://github.com/Doist/typist
  - https://typist.doist.dev/
  - Typist is the mighty Tiptap-based rich-text editor React component that powers Doist products
  - 提供了纯文本和富文本2种输入模式
  - Typist also supports a plain-text mode, and comes with HTML/Markdown serializers.

- linked-daily /561Star/GPLv3/202208/js/vue/electron
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
  - [WYSIWYG editor toolkit architecture proposal__202010](https://gitlab.com/gitlab-org/gitlab/-/issues/273238)
    - implementing support for all of md flavors is an unnecessary cost.
    - Solution 1: Traceability or file diffs
    - Solution 2: Relying on the Markdown preview endpoint
  - https://github.com/gitlabhq/gitlabhq/tree/master/app/assets/javascripts/content_editor
  - [Research and evaluate editor options against UX and technical requirements · GitLab.org / GitLab_202007](https://gitlab.com/gitlab-org/gitlab/-/issues/231725)

- https://github.com/isboyjc/isle-editor /MIT/202501/js
  - https://editor.islenote.com/
  - an open-source web editor that supports rich text, block-based, and markdown editing. 
  - It's efficient and ready to use out of the box, built on top of prosemirror and tiptap.
  - We leverage tiptap's core implementation for its reliability while providing UI views and additional core extensions that enable out-of-the-box functionality through configuration.
  - isle-editor's `core` extensions are fully compatible with `tiptap`. If you're developing a project using tiptap, you can seamlessly use our core extensions. You can also reference the isle-editor source code, as we aim for it to be a best practice implementation of tiptap.

- https://github.com/amjadbouhouch/markup /202210/ts
  - https://mark-up.netlify.app/
  - mobile first markdow editor for web & desktop with tiptap plugins and more

- https://github.com/Okramjimmy/docx-editor /202412/ts
  - https://docx-editor-six.vercel.app/
  - DOCX Editor with Tiptap (Next.js) is a powerful, web-based editor that allows users to create, edit, and format DOCX documents directly in their browser.

- https://github.com/raulereno/tiptap-example-integration /202507/ts
  - https://tiptapexample.netlify.app/
  - A minimal, fully-commented example showing how to use Tiptap 3 with DOCX import/export functionality.
  - Multiple Document Sources
  - Get a token from Tiptap Cloud

- https://github.com/Tzng/allahbin-tiptap /MIT/202507/ts
  - 基于tiptap配置的一个用于国内公文的编辑器
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

- https://github.com/thematters/matters-editor /apache2/202404/ts/react
  - https://thematters.github.io/matters-editor/
  - Rich editor for matters.town, built on top of Tiptap/ProseMirror

- nextcloud-text /366Star/AGPLv3/202208/js/tiptap/php
  - https://github.com/nextcloud/text
  - Collaborative document editing using Markdown
  - 依赖tiptap.v2, yjs, @ueberdosis/prosemirror-tables.v1.1.3, markdown-it、vue2、vuex3

- element-tiptap /825Star/MIT/202208/ts/vue/tiptap/inactive
  - https://github.com/Leecason/element-tiptap
  - https://element-tiptap.vercel.app/
  - WYSIWYG rich-text editor using tiptap and Element UI for Vue2 (tiptap2 and Vue3 is in alpha)
  - new version2 support Vue3, use tiptap2 and Element Plus

- https://github.com/yiitap/yiitap /MIT/202505/ts
  - https://yiitap.pileax.ai/
  - https://yiitap.pileax.ai/demo/vue
  - an AI powered, Notion-style WYSIWYG rich-text block-based editor, built on top of tiptap.
  - Supports Vue & React – Seamless integration with both frameworks.

- https://github.com/Sachin-chaurasiya/BlockEditor /14Star/MIT/202406/ts
  - A notion like editor built with TipTap and Prosemirror
  - https://github.com/huewilliams/notion-clone

- https://github.com/lobbylabs/lobby-editor /MIT/202309/ts
  - https://lobby-editor-demo.vercel.app/
  - extendable rich text editor for Vercel's Next React framework, based on ProseMirror, built using TipTap. 
  - This project grew out of our internal usage at Lobby

- https://github.com/yuanzong/mui-editor
  - Rich text editor built on Material-ui.v5 and Tiptap

- https://github.com/essential-randomness/boba-editor-next
  - Next-generation editor for BobaBoard (and beyond). 
  - 代码量很少

- https://github.com/KuaiYu95/ct-tiptap-editor /MIT/202507/ts/提交多
  - 基于 Tiptap 二次开发的编辑器组件

- https://github.com/KonnorRogers/tip-tap-element
  - http://tip-tap-element.vercel.app/
  - WYSIWYG editing experience that can hook into Ruby on Rails ActionText backend. 

- https://github.com/SenseNet/sn-client
  - @sensenet/editor-react
  - Text editor library behind rich text editor is changed to tiptap@2.0
  - As a first step only those text editing features are implemented
  - More new things (managing tables, embedding, etc.) are coming in the following releases.

- https://github.com/pierre-lgb/slashwriter /NALic/202312/ts
  - https://slashwriter.fly.dev/
  - 依赖tiptap.v2、redux-toolkit、supabase、express、yjs、hocuspocus、mui5
  - App for editing and sharing documents online, with a Notion-like block-based collaborative editor.

- https://github.com/bcc-code/bcc-live-transcriber
  - 依赖tiptap.v2、yjs、vue3
  - A live transcribing app for sharing a meeting with deaf people.
  - The idea is to offer a simplistic keyboard only transcriber app with real time streaming and support for insterting bible verses.

- https://github.com/iojanis/Lity
  - Graph-based document editor with collaborative features
  - 依赖tiptap.v2、yjs、vue3
  - Create nodes by mouse, keyboard shortcuts or using markup (like @ and soon #)

- https://github.com/Young6118/dudu-editor
  - 基于 tiptap v2 的富文本编辑器

- https://github.com/zjz1993/easy-editor /202505/ts
  - 基于tiptap的富文本编辑器

- https://github.com/shikimori/shiki-editor /js/vue/提交多/active
  - a wysiwyg editor based on prosemirror
  - highly inspired by tiptap source code. Many parts of the code are taken from there.

- https://github.com/bons-space/bons-editor
  - A WYSIWYG rich-text editor using tiptap and Element Plus for Vue3

- https://github.com/AventusKent/tiptap-react
  - Super light rich text editor based on TipTap and React

- https://github.com/g-bastianelli/tiptap-react-notion
  - Quick example of how we can make a 'Notion like' editor with Tiptap and react

- https://github.com/clevertask/scribe /MIT/202507/ts
  - A Tiptap-based rich text editor with a Notion-style block interface for viewing and creating content. 
  - Easily integrate @clevertask/scribe into any project requiring rich text editing.

- https://github.com/Cassielxd/CassieEditor /apache2/202506/ts/vue/inactive
  - http://cassie.vv-xj.com/
  - 基于prosemirror和tiptap开发的富文本编辑器项目
  - 本项目主要用于 电子病历的预研

- https://github.com/pagevamp/tapwrite /202503/ts
  - a robust WYSIWYG rich text editor component for React built on top of Tiptap designed to integrate seamlessly into your projects. 
  - This component supports image and PDF file handling within the text editor
# utils
- https://github.com/l1m2e/tiptap-print-designer /MIT/202507/ts/vue
  - https://l1m2e.github.io/tiptap-print-designer/
  - 一个开箱即用的富文本打印设计器，基于 tiptap 和 Vue3 开发。让开发者可以像写文档一样设计打印模板
  - 它提供了一个可视化模板设计系统，允许用户创建具有数据绑定功能的打印模板，然后使用实际数据呈现这些模板以进行打印。
  - 它提供了两个重要组件：设计器 Designer 渲染器Render

- https://github.com/namesakefyi/tiptap-extensions /MIT/202507/ts
  - A collection of extensions for Tiptap, including step-by-step guides and disclosures.

- https://github.com/Aslam97/shadcn-minimal-tiptap /1.5kStar/MIT/202507/ts
  - https://shadcn-minimal-tiptap.vercel.app/
  - a lightweight, customizable rich text editor component designed for integration with Shadcn UI.

- https://github.com/NiazMorshed2007/shadcn-tiptap /MIT/202410/ts
  - https://tiptap.niazmorshed.dev/
  - Sets of custom extensions & toolbars for tiptap editor. 
  - Install with shadcn/cli.
  - https://github.com/ehtisham-afzal/tiptap-shadcn

- https://github.com/hunghg255/reactjs-tiptap-editor /MIT/202507/ts
  - https://reactjs-tiptap-editor.vercel.app/
  - A modern WYSIWYG rich text editor based on tiptap and shadcn ui for Reactjs
  - https://github.com/hunghg255/reactjs-tiptap-editor-demo

- https://github.com/sjdemartini/mui-tiptap /MIT/202507/ts
  - A Material UI (MUI) styled WYSIWYG rich text editor, using Tiptap

- https://github.com/troop-dev/tiptap-react-render /202306/ts
  - This library renders TipTap JSON payloads in React clients without embedding the editor.
  - We were inspired by Contentful's rich-text-react-renderer tool, so we built a similar one for TipTap payloads

- https://github.com/formfcw/tiptap-render-view /GPL/202503/ts
  - Serialize Tiptap JSON content with interactive components.
  - this package only provides a Vue component to render your JSONContent. 
  - But it also provides types and tools to build components for your preferred JavaScript framework.

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

- https://github.com/aguingand/tiptap-markdown /MIT/202401/js/inactive
  - The Markdown extension for Tiptap editor.
  - As Tiptap have now a solution for markdown (paid Conversion extension and more markdown handling announced for v3). I don't plan to release v1. Feel free to fork 

- https://github.com/n8b8dy/tiptap-spoiler
  - React extension (actually two extensions) for TipTap to add spoilers to the editor.
  - http://zetamen.github.io/ckeditor-spoiler/ /ckeditor4

- https://github.com/amirhhashemi/tiptap-text-direction /202304/ts
  - This extension automatically detects the direction of a configurable list of nodes and adds dir="ltr" or dir="rtl" to them.
  - Why not dir="auto"? dir="auto" changes the text direction based on the element's content too

- https://github.com/yaskevich/extension-marker
  - Tiptap extension for setting custom class of the inline node (mark)

- https://github.com/sereneinserenade/tiptap-inline-suggestion /69Star/MIT/202308/ts/inactive
  - https://sereneinserenade.github.io/tiptap-inline-suggestion/
  - A tiptap extension that allows you to add inline suggestions to your editor

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

- https://github.com/harshtalks/tiptap-plugins /202502/ts
  - https://tiptap-plugins.vercel.app/
  - Tiptap React extensions and headless components for image nodes and a slash command for React.js

- https://github.com/arnau01/tiptap-templates /202405/ts/inactive
  - exemplary UI templates for those looking to get a headstart with the Tiptap Editor in a React 

## tiptap-ruby

- rhino-editor /322Star/MIT/202506/ts/ruby
  - https://github.com/KonnorRogers/rhino-editor
  - https://rhino-editor.vercel.app/
  - a grab and go WYSIWYG editing experience that can hook into Ruby on Rails ActionText backend.
  - Currently this package does so using `TipTap` but will most likely include another integration for ProseMirror to allow for both Markdown + WYSIWYG editing.
  - A drop-in Trix replacement which creates ActionText compatible HTML and can parse your existing Trix views allowing a seamless migration without updating any existing db columns
  - Getting up and running locally is hopefully quite painless. We have a test suite using Ruby on Rails and is intended to provide a good demonstration of how this package can hook into ActionText.

- https://github.com/afomera/richer-text.js /MIT/202406/js
  - https://www.richer-text.com/
  - ✨ open-source text editor based on TipTap and ProseMirror for the modern age
  - ~~written in React, using the TipTap libraries and extensions, compiled into a web component~~
  - written with Lit, using the TipTap libraries and extensions with a few of our own added
  - RicherText aims to provide a richer text editing experience than what comes out of the box with ActionText in Rails. 
  - It is however a separate thing from ActionText and is not backwards compatible.
  - 依赖@rails/activestorage、tiptap、react-to-webcomponent
  - Basic image uploading for ActiveStorage
  - not-yet
    - Support for disabling extensions/portions out of the library.
    - There is a hardcoded requirement for `ActionStorage` to be installed and setup for Image support to work. 
  - https://github.com/afomera/richer_text /ruby
    - provide a richer text editing experience than what comes out of the box with ActionText in Rails
    - there's currently a hard requirement for ActiveStorage
  - https://x.com/afomera/status/1799103684791746684
    - RicherText.js v2.0.0-beta.1 is out 
    - It's not ActionText compatible, but the backend solution is very similar to ActionText so you'll feel at home.
    - If you need an ActionText compatible solution, look at Rhino Editor
  - [Announcing Richer Text v2 _202406](https://www.richer-text.com/2024/06/28/announcing-version-two)

- https://github.com/decidim/decidim
  - a participatory democracy framework, written in Ruby on Rails, originally developed for the Barcelona City government online and offline participation website
  - [To Trix or not to Trix · Discussion](https://github.com/decidim/decidim/discussions/7585)

- [Thoughts on Action Text](https://www.reddit.com/r/rails/comments/rt2qvo/thoughts_on_action_text/)
  - Action Text seems too coupled to Trix
# examples
- https://github.com/tanlucvn/miniwrit /202506/ts
  - https://miniwrit.vercel.app/
  - A clean, minimal, local-first writing app — designed for focused writing and seamless syncing.
  - Tag-based organization
  - Local-first sync (Dexie + Turso)
  - Daily writing goals and statistics
  - Soft delete & trash recovery
  - Settings with full control over appearance, storage & sync

- https://github.com/ueberdosis/ai-agent-custom-llm-demos /MIT/202507/ts
  - https://tiptap.dev/docs/content-ai/capabilities/agent/custom-llms/overview
  - Integrate the Tiptap AI Agent extension with a custom backend and AI model provider.
  - This repository contains 12 complete demos demonstrating different integration patterns and capabilities.

- https://github.com/chenxiaoyao6228/idea-forge /MIT/202504/ts
  - Idea Forge is an AI-powered tool for writing and collaboration, enhancing creativity, productivity, and seamless teamwork
  - AI-powered writing assistance
  - Backend: NestJS, PostgreSQL, Redis, Hocuspocus, Prisma, S3
  - Frontend: React, TypeScript, TailwindCSS, Shadcn UI, Tiptap
  - AI Integration: OpenAI API

- https://github.com/volagold/beenote /MIT/202503/ts
  - https://beenote-ai.netlify.app/
  - Full stack AI web application for languge learning built with Next.js and ChatGPT

- https://github.com/imberZsk/editor /202507/ts
  - 基于 TipTap 的 block-editor，支持 MD、AI、协同

- https://github.com/artificialcitizens/acai.so /MIT/202401/ts/inactive
  - ACAI is a collection of AI powered tools to help you manage your digital world

- https://github.com/Damonbodine/wordwise-ai /202507/ts
  - https://wordwise-ai-sigma.vercel.app/
  - Modern Next.js app with TipTap editor, document management, and real-time features
  - 依赖nextjs、tiptap、zustand、supabase
  - Real-time Grammar Analysis - AI-powered grammar and spell checking using Groq API
  - Smart Suggestions - Accept/dismiss grammar corrections with one click
  - Overall writing quality assessment with detailed metrics
  - Three-column Layout - Document list, editor, and suggestions panel
  - AI: Groq API (llama-3.1-8b-instant model)

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

- notes /4Star/GPLv3/202208/js
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

- https://github.com/OpenSlides/OpenSlides /555Star/MIT/202507/python
  - https://openslides.com/
  - OpenSlides is a free, web based presentation and assembly system for managing and projecting agenda, motions and elections of an assembly.
  - OpenSlides is a powerful and modern, web-based software for the digital organization of your meetings and committees. All user access their committees and meetings via one central URL.

- https://github.com/sturepo/onotes
  - https://onotes.onotes.workers.dev/
  - using @tailwindcss @tiptap_editor @vuejs & @nuxt_js

- https://github.com/yesmore/inke /apache2/202311/ts
  - https://inke.app/
  - 一个所见即所得的Markdown笔记本，支持AI辅助写作和多人协作，支持自部署，使用IndexedDB存储笔记。

- https://github.com/arikchakma/maily.to /MIT/202507/ts
  - https://maily.to/
  - Craft beautiful emails effortlessly with Maily, the powerful email editor that ensures impeccable communication across all major clients.

- https://github.com/Davronov-Alimardon/google-docs /202412/ts
  - A full-stack Google Docs clone with real-time collaboration, commenting, advanced text editing (Tiptap), and a template gallery. Next.js 15, React 19
  - https://github.com/Sunanda-05/papergate-docs-editor

- https://github.com/RajdeepDs/coordinize /AGPL/202507/ts
  - Coordinize is a modern communication platform designed specifically for asynchronous team
  - Asynchronous Collaboration: Coordinize is built for asynchronous teams, allowing members to work independently and communicate asynchronously.
  - Integration-Friendly: Works with tools like GitHub, Linear, and other platforms for issue tracking and project management.
  - 依赖nextjs、shadcn、prisma

- https://github.com/UmarAurangzeb/tiptap-ppt /202507/ts
  - ppt-export added

- https://github.com/iamrohanshrestha/form-builder /202407/ts/inactive
  - A Full Stack MERN app for building dynamic forms with drag and drop interface & to track and view the responses received in the created form.
  - You can use Brevo for free SMTP server and MongoDB Atlas for database.
  - Frontend: React, TypeScript, Tailwind, React Hook Form, Zod, ShadcnUI, React Router, DND Kit, Tanstack Query, Tanstack Table, Tiptap, React Dropzone, React Easy Crop, Zustand
  - Backend: Node, Express, TypeScript, Nodemailer, Multer, JWT
  - Database: MongoDB, Mongoose
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
  - [Show HN: An open-source, collaborative, WYSIWYG Markdown editor | Hacker News_202306](https://news.ycombinator.com/item?id=36446045)

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

- https://github.com/elegantframework/elegant-cli /210Star/MIT/202411/ts/inactive
  - https://www.elegantframework.com/
  - Build SEO-friendly websites, super fast full-stack web applications
  - Built with Next.js, TipTap, Tailwind CSS, and more
  - An all-in-one web application and blogging solution. All the features you need are included right out of the box.
  - Seamless integration with PostgreSQL and Prisma
  - Elegant is perfect for blogging, documentation websites, or just about any type of web application.

- https://github.com/primodotso/primo
  - https://primo.so/
  - ui基于svelte
  - Primo is a component-based CMS that makes it easy to build visually-editable static sites

- https://github.com/verbb/vizy /php
  - A flexible visual editor for Craft CMS
  - 依赖tiptap2、vue3、tippy.js、codemirror-editor-vue
# more
- https://github.com/ujw0712/editor-and-pdf
  - 依赖 vue3、jspdf, html2canvas、@tiptap/extension-collaboration, yjs, @hocuspocus/provider

- https://github.com/ParamagicDev/tip-tap-element /ruby
  - https://tip-tap-element.vercel.app/
  - A starter kit for tip-tap to get going

- https://github.com/stckme/tiptapy /MIT/202506/ts
  - Library that generates HTML output from JSON export of tiptap editor

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

- https://github.com/nabedkhan/multistep-job-application-form /202505/ts
  - https://multistep-job-application-form.vercel.app/
  - This is a AI powered multi-steps form built with TypeScript, Redux Toolkit, TipTap editor, and OpenAI integration. 
  - The project uses modern development tools and practices including Tailwind CSS for styling and React Hook Form for form management

- https://github.com/Leosouthey/Raphael
  - 开源的个人/团队知识库系统

- https://github.com/nanmenyu/inking
  - inking是个人开发的开源桌面码字软件，面向的群体主要是网文写手，包含写作（核心）和阅读（附带）两大模块
  - 内置关系图、灵感备忘、时间线、地图、webview等辅助模块

- https://github.com/xiaohanyu
  - Spent another two days to write a recursive descent evaluation to convert @tiptap_editor 's JSON format to TeX snippet
