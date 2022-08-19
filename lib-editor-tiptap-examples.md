---
title: lib-editor-tiptap-examples
tags: [examples, prosemirror, tiptap, toc]
created: 2022-08-19T23:00:04.811Z
modified: 2022-08-19T23:00:22.162Z
---

# lib-editor-tiptap-examples

# guide

# popular

# editors-collection
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

- think /1kStar/MIT/202208/ts/nestjs/tiptap
  - https://github.com/fantasticit/think
  - https://think.codingit.cn/
  - 依赖 MySQL/NextJS/nestjs/tiptap
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序
  - Think 是一款开源知识管理工具。通过独立的知识库空间，结构化地组织在线协作文档，实现知识的积累与沉淀，促进知识的复用与流通。同时支持多人协作文档。

- nextcloud-text /366Star/AGPL.v3/202208/js/tiptap/php
  - https://github.com/nextcloud/text
  - Collaborative document editing using Markdown
  - 依赖tiptap.v2, @_ueberdosis/prosemirror-tables.v1.1.3, markdown-it、vue2、vuex3

- better-virgool /9Star/MIT/NALic/202208/ts/tiptap
  - https://github.com/ahhshm/better-virgool
  - https://ahhshm.github.io/better-virgool/
  - An attempt to create a better rich text editor than virgool.io. Powered by Tiptap and ProseMirror
  - 实现了RTL国际化方向

- element-tiptap /825Star/MIT/202208/ts/vue/tiptap/inactive
  - https://github.com/Leecason/element-tiptap
  - https://element-tiptap.vercel.app/
  - WYSIWYG rich-text editor using tiptap and Element UI for Vue2 (tiptap2 and Vue3 is in alpha)
  - new version2 support Vue3, use tiptap2 and Element Plus

- @sensenet/editor-react
  - https://github.com/SenseNet/sn-client
  - Text editor library behind rich text editor is changed to tiptap@2.0
  - As a first step only those text editing features are implemented
  - More new things (managing tables, embedding, etc.) are coming in the following releases.

- https://github.com/primo-af/primo
  - https://primo.af/
  - /76Star/AGPLv3/202106/svelte
  - an all-in-one ide, cms, component library, and static site generator
  - a next-gen, dev-friendly alternative to WordPress.
- https://github.com/shikimori/shiki-editor /vue/提交多/active
  - a wysiwyg editor based on prosemirror
  - highly inspired by tiptap source code. Many parts of the code are taken from there.
# tiptap-utils
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

- https://github.com/GoCapsule/tiptap-extensions
  - https://codesandbox.io/p/github/leonard-henriquez/column-extension/main
  - 支持选中文字后创建分栏，并将选中文字放在第一栏
# examples
- https://github.com/lostdesign/linked
  - https://uselinked.com/
  - Daily journaling without distraction.

- https://github.com/justinmoon/tiptap-markdown-demo
  - TipTap rich text editor doesn't support markdown, but this repo shows how to hack it in yourself.
# more
- https://github.com/ujw0712/editor-and-pdf
  - 依赖 vue3、jspdf, html2canvas、@tiptap/extension-collaboration, yjs, @hocuspocus/provider

- https://github.com/ParamagicDev/tip-tap-element
  - https://tip-tap-element.vercel.app/
  - A starter kit for tip-tap to get going

- https://github.com/ueberdosis/tiptap-php
  - A PHP package to work with Tiptap content. 
  - You can transform Tiptap-compatible JSON to HTML, and the other way around, sanitize your content, or just modify it.
