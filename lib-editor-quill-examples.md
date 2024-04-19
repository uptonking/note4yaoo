---
title: lib-editor-quill-examples
tags: [examples, quill, text-editor]
created: 2023-02-09T18:31:53.078Z
modified: 2023-02-09T18:32:06.240Z
---

# lib-editor-quill-examples

# guide

- tips
  - 核心模块: image, table, toolbar, mention
  - resize: image, table, video, iframe

- resources
  - https://github.com/quilljs/awesome-quill
  - search: mern + quill
  - 很多dashboard也包含quill
  - [Quill Diff - old/new/diff](https://codepen.io/belomm/pen/ebdbGy)
  - https://npmtrends.com/@tiptap/core-vs-draft-js-vs-lexical-vs-quill-vs-slate
# popular
- quill /37.5kStar/BSD/202311/ts
  - https://github.com/quilljs/quill
  - https://quilljs.com/
  - https://quilljs.com/playground/  /提供了vanillajs、react、form
  - a modern WYSIWYG editor built for compatibility and extensibility
  - https://github.com/quilljs/delta
  - https://github.com/quilljs/parchment
  - 🍴 forks
  - https://github.com/reedsy/quill /BSD/202404/ts
    - We need to use our own forked version of the Delta class, which adds support for complex attributes (which we need for tracked changes).
    - 依赖@reedsy/quill-delta、eventemitter3、parchment、rfdc
    - https://github.com/reedsy/delta
    - https://github.com/reedsy/parchment
    - https://github.com/reedsy/rich-text /Rich Text uses quill-delta
  - https://github.com/welkinwong/superdocs-quill /202311/ts/inactive
    - https://github.com/welkinwong/superdocs-rsuite
    - a fork of quill, inactive
  - https://github.com/revolist/quill

- https://github.com/DevExpress/devextreme-quill /BSD/202403/js
  - https://js.devexpress.com/React/Demos/WidgetsGallery/Demo/HtmlEditor/Tables/MaterialBlueLight/
  - a fork of Quill, based on the 2.0 branch
  - supports basic table operations and enhances lists rendering
  - https://github.com/DevExpress/DevExtreme/tree/24_1/packages/devextreme/js/ui/html_editor

- typewriter /347Star/MIT/202311/ts
  - https://github.com/typewriter-editor/typewriter
  - A rich text editor based off of Quill.js and Ultradom, and using Svelte for UI
  - 依赖 svelte、popperjs2、typewriter/delta
  - Built on the same data model as Quill.js, the Delta format, and using a tiny virtual DOM, Superfine, Typewriter aims to make custom rich text editors faster, easier, and more powerful
  - Typewriter modifies `Delta` to provide better memory usage with an immutable approach and adds a layer on top `TextDocument`, which splits a Delta document into lines to add even more memory benefits for large documents. It also paves the way for document virtualization 
  - It also paves the way for document virtualization 
  - Typewriter adds Decorations like ProseMirror which support changes to how the document is displayed without changing the document. This is used for features like highlighting find-replace words or inserting a collaborator's cursor.

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

- https://github.com/ludejun/quill-react-commercial /ISC/202404/ts/js
  - https://ludejun.github.io/quill-react-commercial/
  - 多功能的、可面向商业化的quill富文本编辑器，主要模块包括图片、表格、工具条
  - 使用最新的quill@2.0.0-rc.4，方便向后兼容
  - 使用React Hooks实现wrapper，大部分代码包括modules的实现都基于vanillajs
  - 微信小程序的富文本编辑器也使用的Quill底层和数据结构，可以和quill-react-commercial打通编辑和展示
  - 图片支持本地上传和图片Url插入，可以限制上传图片格式和大小
  - 参考quill-better-table

- https://github.com/AmeyVijeesh/ReactTextEditor /202404/js/单文件
  - https://atext.netlify.app/
  - Rich Text Editor made with React and Quill.js
  - 实现了简单工具条, 体验好, 但功能弱
  - Save the edited text locally or on a server.

- https://github.com/WindrunnerMax/QuillBlocks /202403/ts
  - Quill Editor Blocks Kit
  - delta数据结构diff算法。
  - 编辑器实时diff的虚拟图层实现。
  - delta to docx/html/pdf

- https://github.com/Alec-Aldrine-Lakra/Track-Changes-quill /202001/js/inactive
  - This is a demo version of track changes in quill, It is still incomplete and major features are missing
  - I am highlighting text changes for every user and storing all their highlighted text in web storage api.
  - https://github.com/openevocracy/quill-track-changes /202003/js/空文件

- https://github.com/TonyYu2015/GEditor /202309/js/inactive
  - https://g-editor-fawn.vercel.app/
  - rich-text base on Quill, 非react
  - 典型的单页文档编辑器, 功能丰富
  - 集成了sharedb

- https://github.com/BugCreators/ql-quill /MIT/202403/ts
  - 关于 Quill.js 一些公共配置的封装、支持使用 KityFormula 公式插件，供内部使用
  - 依赖quill.v1
  - PasteFromWord基于worker实现
  - `class QlQuill extends Quill` 大部分自定义逻辑放在子类上，项目结构模仿quill

- https://github.com/domilin/media-quill /202011/ts/inactive
  - Rich text editor based on Quill
  - Built in vanilla JS, typescript support, so it can be used on React, Vue, Angular as well
  - 功能较丰富
  - `class MediaQuill extends Quill`，模块不多

- https://github.com/coach-K/custom-quill-editor /202312/ts/实现简单
  - https://coach-k.github.io/custom-quill-editor/demo/
  - a WYSIWYG Editor build on top of the open source library Quill
  - To test the Video and Social Embed

- https://github.com/balmjs/balm-ui/blob/main/src/scripts/components/editor/quill/core/index.js /MIT/202309/js
  - https://material.balmjs.com/text-inputs/editor
  - const quill = new Quill(editorEl, options); 
  - 设计了自定义useExtension()
  - A modular and customizable UI library based on Material Design and vue3
  - BalmUI Pro is a front-end scaffolding. it introduces higher level components

- https://github.com/KID-1912/quill-js-editor /202312/js/实现简单
  - Custom JavaScript editor built on quill
  - 不依赖react, 提供了工具条，示例类似在线文档布局

- https://github.com/NSFI/ppfish-components /MIT/202208/ts/js/inactive
  - https://github.com/NSFI/ppfish-components/blob/master/source/components/RichEditor/src/editor.tsx
  - https://nsfi.github.io/ppfish-components/#/components/richEditor
  - 一种可内嵌于浏览器，所见即所得的文本编辑器。
  - 插入不可编辑的文本
  - 拖拽编辑器改变大小
  - 默认情况下，使用编辑器内置的插入、拖入/粘贴图片功能时，图片将以Data URL的形式嵌入到页面中，此时后端保存该图片将占用较大的空间，因此推荐使用自定义的方式将图片上传到服务器并设置图片的URL

- https://github.com/BobaBoard/boba-editor /MIT/202203/ts/deprecated
  - An advanced text editor based on QuillJS, vaguely inspired by Tumblr's
  - 依赖quill.v1.3、react-tiny-popover
  - used by boba-components to create posts and comments
  - 第三方的embed示例很多
  - 示例很多，包括spoiler
  - 支持ssr
  - https://github.com/FujoWebDev/astrolabe
    - 最新转向tiptap

- https://github.com/cloverhearts/quilljs-markdown /MIT/202207/js/inactive
  - https://cloverhearts.github.io/quilljs-markdown
  - Plugin for advanced Markdown. 书写时会自动转换成md样式
  - https://github.com/doc22940/quill.markdown
- https://github.com/patleeman/quill-markdown-shortcuts /201910/js
  - module that converts markdown to rich text formatting while typing.
  - https://github.com/sswatson/quill-markdown-shortcuts /202103/js
  - https://github.com/rogeriomq/quill-markdown-shortcuts /202208/js

- https://gitee.com/wfeng0/mpoe /apache2/202402/js/vue
  - 多人协同编辑器开发 MPOE（Multi person online edit）
  - node采用较强的模块化思想，每个单独的模块都会独立导出 index.js ，因此，node有很多的 index.js，注意区分; 
  - 使用Yjs、Quill、LuckySheet 等技术实现的markdown、txt、excel 等文件的多人在线协同编辑，支持以 websocket、webRTC、组合API等形式实现通信
  - [Yjs + Quill 实现文档多人协同编辑器开发（基础+实战） - 掘金 _202309](https://juejin.cn/post/7273432426772070457)
  - [Luckysheet 实现excel多人在线协同编辑 - 掘金](https://juejin.cn/post/7298170736480485376)

- https://github.com/shenmaxg/quill-imitate-shimo /202110/ts/inactive
  - 基于 quill 的富文本编辑器，react, 模仿石墨风格的富文本编辑器
  - [富文本编辑器是如何实现协同编辑的, 基于ot sharedb - 知乎 _202110](https://zhuanlan.zhihu.com/p/416018080)
  - [如何为富文本添加目录与评论 - 知乎](https://zhuanlan.zhihu.com/p/427555073)

- https://github.com/hubertnare/strapi4-wysiwyg-replacement /202202/js
  - change the default WYSIWYG to Quill Editor
  - [How to change the default WYSIWYG in Strapi v4 to Quill Editor_202203](https://strapi.io/blog/how-to-change-the-default-wysiwy-to-quill-editor)

- https://github.com/zenoamaro/react-quill /202208/ts/单文件
  - https://zenoamaro.github.io/react-quill/
  - https://codepen.io/alexkrolick/pen/xgyOXQ
  - A Quill component for React
  - ReactQuill 2 brings a full port to TypeScript and React 16+, a refactored build system, and a general tightening of the internal logic
    - it removes support for long-deprecated props, the ReactQuill Mixin, and the Toolbar component
  - If you frequently need to manipulate the DOM or use the Quill APIs imperatively, you might consider switching to fully uncontrolled mode.
  - If you instantiate ReactQuill without children, it will create a `<div>` for you, to be used as the editing area for Quill.
  - [React-Quill Custom Format w/Parchment Demo](https://gist.github.com/alexkrolick/8ec0de512c97b363c02a38db60623c29)
  - https://github.com/adrianhelvik/react-quill /202110/js/inactive
    - it can be used as a basis for the next version of react-quill
    - To use with katex, add a cdn script tag. The editor will not load if the formula module is used and window.katex is unavailable.
    - [I started rewriting using hooks and React 17 compatible APIs _201911](https://github.com/zenoamaro/react-quill/issues/547)
  - 🍴 forks
    - https://github.com/yata-corp/react-quill-patched
    - https://github.com/abrarhayat/react-quill-abrarhayat
    - https://github.com/shareefalis/react-quill
    - https://github.com/miketalbot/react-quill
    - https://github.com/Grewer/react-quill2 /202211/ts
      - 手动升级v2, 本文选择了 `quill-table-ui` 作为接入方案

- https://github.com/gtgalone/react-quilljs /MIT/202209/ts/单文件/inactive
  - React Hook Wrapper for Quill, powerful rich text editor.

- https://github.com/sciencenawaaz/Text-Editor /202309/js/inactive
  - https://text-editor-roan.vercel.app/
  - text editor using react-quill
- https://github.com/ha3158987/react-quill-editor-example /202306/js
  - http://react-quill-editor-example.s3-website.ap-northeast-2.amazonaws.com/
  - An example using React-quill editor library created for practice purpose.

- https://github.com/lovelysystems/lovely-editor /apache2/202210/js/inactive/多实例
  - https://lovely-editor.netlify.com/
  - react component which lets you use multiple editors (e.g Quill) for a single document.
  - Each editor will create an isolated HTML markup of its part.
  - LovelyEditor basically consists out of three main components: LovelyEditor, EditorBlock, Editors (eg. EditorQuill)
  - 支持添加Quill/ToastUI/CodeMirror5

- https://github.com/maxfahl/Quill-Edit-Multiple /202010/js
  - https://codesandbox.io/s/github/maxfahl/Quill-Edit-Multiple
  - A sample application showing how you can have multiple editable areas of your app using the Quill editor with only one toolbar, moving the editor around.
  - 用一个工具条控制3个textarea
  - I'm creating one instance of Quill, using a custom toolbar positioned at the top. The editor element is placed in a temporary, hidden, container. When the user double clicks any of the three text containers (Editables), the editor element will be transplanted from the temporary container to a new location inside the Editable

- https://github.com/tangien/quilljs-textarea /MIT/202202/js/inactive
  - https://tangien.github.io/quilljs-textarea/
  - A simple extended helper for quilljs to transform textarea into text editor
  - Works on both textarea and divs
  - Auto-initialize quilljs using data-quilljs selector

- https://github.com/vbobroff-app/quill-blot-resizer /202307/ts
  - How to resize image, video, table into Quill-editor

- https://github.com/mild-blue/quill-even-better-table /MIT/202306/js/inactive
  - https://codepen.io/soccerloway/pen/WWJowj
  - A module for better table in Quill, more useful features are supported
  - Using `DIV` to implement TableCellLine led a copy/paste issue
- https://github.com/seehar/quill-better-table-plus /MIT/202308/js/inactive
  - https://codepen.io/seehar/pen/yLQopvq
  - fork by quill-better-table, quill-even-better-table
  - 外部工具条按钮更多
- https://github.com/soccerloway/quill-better-table /MIT/202007/js/inactive
  - https://codepen.io/soccerloway/pen/WWJowj
  - Module for better table in Quill, more useful features are supported.
  - quilljs v2.0.0-dev.3
  - 支持 Merge/Unmerge table cells
  - Selects multiple table cells
  - codepen可以直接查看delta内容
  - table通过给\n添加attributes控制单元格内容
  - https://github.com/liuyisnake/quill-better-table
  - 🍴 forks
    - https://github.com/clool/quill-better-table /202306/js
      - support table cell vertical align
    - https://github.com/Scholar-6/quill-better-table /202106/js
    - https://github.com/ddunny/quill-better-table /202304/js
    - https://github.com/Tobias-Braun/quill-better-table /202007/js
      - Add support for background color in table cells 

- https://github.com/volser/quill-table-ui /202007/ts
  - https://codepen.io/volser/pen/QWWpOpr
  - A module for table UI in Quill
  - quilljs v2.0.0-dev.3
  - 功能太少, 每个单元格都有悬浮菜单

- https://github.com/zzxming/quill-table /202403/js
  - https://zzxming.github.io/quill-table/demo/index.html
  - A table module used in QuillJS@1.3.7
  - 实现了在工具条选择表格行列数

- https://github.com/dost/quilljs-table /201703/js/archived
  - Test lab for creating TABLE functionality in QuillJS using Containers.
  - https://github.com/Shatiger/quill-table /202305/js
  - https://github.com/dclement8/quill1-table /202309/js
- https://github.com/unzld/quill-better-table-picker /202110/js
  - An extension of the table module for Quill, with support for toolbar table picker.
  - v2.0.0-dev.3

- https://github.com/kagol/quill-table-list /202202/js
  - 在 Quill 表格中插入列表
  - quill-better-table@1.2.10

- https://github.com/tanvirraj/quill-notion-table-editor /202208/js
  - https://tanvirraj.github.io/quill-notion-table-editor/
  - a notion like menu and table editor based on quilljs
  - table功能简单，通过类似/菜单添加
  - table的delta通过给\n添加attributes为row来区分行
  - 不依赖react
  - https://github.com/uragirii/Notion-Clone /202012/js
  - https://codesandbox.io/p/sandbox/notion-clone-v3-g3pey
- https://github.com/tzhangchi/quill-menu-module /202201/ts
  - https://jsfiddle.net/zhangchi/2dyafg67/1/
  - Notion-like style quill menu module based on Quill.js
  - 斜杠菜单，非react

- https://github.com/denvudd/cypress /202404/ts
  - https://cypress-r2o0.onrender.com/
  - SaaS Notion Clone with Realtime cursors, Nextjs 13, Stripe, Drizzle ORM, Tailwind, Supabase, Sockets
  - Real-time cursors, text selection
  - Supabase Row level policy
  - 不支持斜杠菜单
  - 不支持拖拽block
  - https://github.com/Ulrich-Tonmoy/nextjs-web-apps/tree/main/notion
  - https://github.com/anjalipal2001/QuillSync
  - https://github.com/TobCraft3521/notion-clone

- https://github.com/imtiaz101325/quill-fold-example /202008/ts/archived
  - A simple quill.js base WYSIWYG editor with an added feature of collapsable bullet points

- https://github.com/Kibo/filemanager-js /202201/ts/vue
  - The JavaScript filemanager for CKEditor, Quill, TinyMCE.

- https://github.com/BrenoFariasdaSilva/TextSync /CC0/202306/js/仅同步未处理冲突/inactive
  - A Real-Time Distributed-Text-Editor Application with ReactJS, NodeJS, MongoDB and WebSockets.
  - 依赖react、quill、socket.io、mongoose

- https://github.com/exilednick/Bandersnatch /202009/js/ejs/inactive
  - 🤝🏻 A collaborative text editor
  - 依赖express、ejs、socket.io
  - 未实现协同，仅同步未处理冲突
  - 采用ssr，每次全量覆盖 `socket.on('take_data', data => editor.setText(data));`

- https://github.com/gentabazi2/simulQ /MIT/202312/ts/inactive
  - Real-time collaborative editing system with MERN
  - Its purpose is to serve as a reference project on how a real-time collaborative editing system should be developed.
  - Documents: Rich text editor used: Quill.
- https://github.com/promise-dash/Blogspot /202308/js
  - A Full Stack Blog App with all the CRUD functionality and user authentication. 
  - Built with Next 13, React, Tailwind, Nodejs and MongoDb.
  - https://github.com/Priyanshu88/MERN-Blog /202307/js

- https://github.com/Heisdalu/Dracora /202309/ts
  - https://dracora.vercel.app/
  - an admin dashboard with drag-and-drop capabilities, pagination, a text editor, as well as line, bar, and other entertaining charts.
  - 依赖Firebase、React-quill、Next.js、React-beautiful-dnd

- https://github.com/isaacsokari/simple-docs /202104/ts
  - Lightweight Google Docs clone made using Quill editor, Socket.io, and MongoDB.

- https://github.com/LittleWhitechun/chouxiang-converter /202208/ts
  - React16 hooks + css in js + Quill + ts *抽象话翻译器，可以把中文翻译成emoji，支持单字替换，文字位置对应跳转，一件翻译等

- https://github.com/joeldarl/quill-cms /202101/ts/pug
  - A publishing CMS developed using NodeJS, TypeScript and MongoDB. 
  - 不依赖quilljs，编辑器使用SimpleMDE

- https://github.com/scriptype/writ-cms /GPLv3/202404/js
  - https://enes.in/writ-cms
  - https://github.com/scriptype/writ-cms/blob/master/packages/expansion-content-editor/static/editor/quill.js
  - The timeless SSG + CMS
  - I should be able to just use GUI from start to end
  - I should get automated index pages, pagination, sitemap, rss, search etc. without touching code
  - 依赖jquery、quill

- https://github.com/netless-io/netless-app/tree/master/packages/app-quill /MIT/202312/ts/svelte
  - Netless App for rich-text collaborative editing, powered with Yjs (a CRDT implementation) and Quill.
  - https://github.com/netless-io/netless-app /MIT/202312/ts
    - https://netless-io.github.io/netless-app
    - Official Apps for the Agora Interactive Whiteboard.
  - https://github.com/netless-io/flat /MIT/202401/ts
    - https://flat.whiteboard.agora.io/
    - Project flat is the Web, Windows and macOS client of Agora Flat open source classroom.
  - https://github.com/netless-io/flat-server
    - Node.js server for the Agora Flat open source classroom.

- https://github.com/sjustintaylor/text-editor /202012/js
  - client + server
  - 依赖quill.v1、react-ace、pouchdb

- https://github.com/vtejuf/quill-pagination /202308/js/inactive
  - A CKEditor-like style component
  - Applicable version: Quill v1.3.7
  - 简单的分页效果
# quill-based-editors
- https://github.com/mostafizurhimself/admintoolkit-html /MIT/202403/js
  - https://getadmintoolkit.com/
  - https://www.getadmintoolkit.com/editor.html
  - Admin template based on TailwindCSS and Vanilla JavaScript
  - 典型的tailwind样式

- https://github.com/Uclusion/uclusion_web_ui/blob/master/src/components/TextEditors/QuillEditor2.js /202311/js
  - 依赖quill-table-ui、quill-image-resize-module

- https://github.com/immense/quill-drag-and-drop-module /MIT/201708/js
  - https://immense.js.org/quill-drag-and-drop-module/
  - module to add drag-and-drop support to the Quill container
  - You can specify a container to enable dragging and dropping

- https://github.com/asturgeon123/quill-drag-and-drop-demo /202401/js
  - Demo drag-and-droppable tokens into a Quill rich text editor
  - 类似拖拽变量
- https://github.com/millievn/quill-variable-demo /202312/js/vue
  - show variable text in quill and edit its value in antd-vue

- https://github.com/gywgithub/vue-quill-drag-drop /MIT/202009/js/vue
  - https://gywgithub.github.io/vue-quill-drag-drop/#/
  - Quill Drag-Drop Example
  - Based on quill, different types of data are dragged to the rich text input box. 
  - 类似页面编辑器，将左侧元素拖拽到quill编辑器中
  - It supports text drag, picture drag, canvas drag, table, HTML and other data drag formats.
  - quill-image-drop-module: v1.0.3

- https://github.com/takitakit/block-editor-vue /MIT/201906/js/vue
  - https://codepen.io/takitakit/pen/RmpVKL
  - a block editor that allows you to stack any combination of block elements, such as paragraphs, headings, lists, and so on.
  - 依赖quill.v1、vuex

- https://github.com/brsloan/warewoolf /MIT/202403/js
  - A minimalist novel-writing system/rich text editor designed to be usable without a mouse.
  - All-keyboard navigation designed for pleasant use without a mouse
  - 依赖quill.v1、docx、@electron/remote

- https://github.com/weblineindia/ReactJS-CK-Editor /MIT/202403/js
  - A simple, native and easy-to-use WYSIWYG / Rich Text editor built in Quill.js and React.js
  - inspired by react-quill

- https://github.com/wellspr/react-quill-editor /202402/ts
  - a react typescript wrapper for Quill JS

- https://github.com/opensquare-network/rich-text-editor /MIT/202402/ts
  - OpenSquare Team Rich Text Editor
  - 依赖react、quill、marked、prismjs
  - wysiwyg基于quill, markdown基于textarea

- https://github.com/yxy199399/react-quill-style /202401/ts
  - 将原有功能基于react-quill的基础，将所有（公式除外，公式用到其它依赖）转换成行内样式，在移动端等地方使用可不用单独引入样式 11种行内格式
  - 依赖quill.v1

- https://github.com/ChrisMayor/D365RichTextEditor /202012/ts
  - Dynamics 365 Rich text editor for Unified Interface / Based on PowerApps component framework, React and quill

- https://github.com/fgilde/MudExRichTextEditor /GPLv3/202403/js
  - Quill based RichEditor component for MudBlazor
  - easily consume Quill combining in a MudBlazor project Features with MudBlazor Theme Support.
  - Exports editor contents in Text, HTML, and Quill’s native Delta format
  - https://github.com/Spillgebees/Blazor.RichTextEditor

- https://github.com/NodeBB/nodebb-plugin-composer-quill /202311/js
  - WYSIWYG composer for NodeBB based off of Quill
  - This composer saves its data in a unique format that is only compatible with Quill. If you switch to Quill, any posts made with Quill cannot be migrated back to Markdow

- https://github.com/Wikia/post-editor /202203/js
  - Quill-based editor for posts and replies, currently used in Discussions
  - Preact as a renderer
  - wds-components/_drowdowns

- https://github.com/graasp/graasp-text-editor /202311/ts/实现简单
  - Quill text editor for Graasp using react

- https://github.com/innovatorved/Markdown-Editor /202212/ts/inactive
  - https://markdown-editor-six-mu.vercel.app/
  - A simple Nextjs, Quill based markdown Editor

- https://github.com/KillerCodeMonkey/stencil-quill /MIT/202402/ts
  - https://killercodemonkey.github.io/stencil-quill/
  - Native web components for the Quill Rich Text Editor
  - do not forget to install quill v2! and include it + theme css in your buildprocess, module or index.html

- https://github.com/moonshine-software/quill /MIT/202402/js
  - Quill field for MoonShine Laravel admin panel
# client-mobile
- https://github.com/cdcrft/quill-mobile-view /201909/js
  - module to add a button inside the toolbar that will allow you to change the editor width to adapt it to a mobile view

- https://github.com/kanso-team/typeskill-typer /MIT/202402/ts
  - Typeskill, the Operational-Transform Based (React) Native Rich Text Library.
  - No bloated/clumsy WebView ; this library only relies on (React) Native components; 
  - Fully controlled components
  - Based on the reliable Delta operational transform library from quilljs.
  - https://github.com/typeskill/typer /202002/ts/archived
  - https://github.com/meliorence/react-native-render-html /BSD/202306/ts
    - https://meliorence.github.io/react-native-render-html/
    - iOS/Android pure javascript react-native component that renders your HTML into 100% native views

- https://github.com/imnapo/react-native-cn-quill /202306/ts
  - a rich-text editor for react-native. 
  - We've created this library on top of Quill Api.
- https://github.com/LuudJanssen/react-native-webview-quill /201912/ts
  - Quill component for React Native built using `postMessage` communication and a WebView.

- https://github.com/YipitBeijing/RN-edison-editor /202305/ts/inactive
  - react-native quill rich-text-editor

- https://github.com/tonisantosbalbi/react-native-quill-editor /MIT/202208
  - React Native Quill Rich Text Editor Wrapper
  - Make sure you installed react-native-webview

- https://github.com/artiely/quill-vue-mobile /202004/js/vue
  - 一个 quill 的封装，用于移动端 webview 的跨平台富文本编辑器, 类似知乎移动端富文本
# client-pc
- https://github.com/abahmed/Deer /MIT/202002/js
  - beautiful note taking app, built on Electron and React
  - 依赖react-quill、redux、immutable.v4、pouchdb、electron-store、mui.v4
  - https://github.com/FilippoSecchi/Deer
    - Added italian language

- https://github.com/azure06/clips /202212/ts/vue
  - A universal clipboard app
  - Clips powered by Google Drive synchronize your clipboard with multiple devices, and allows you to quickly search throw your clipboard history.
  - 依赖rxdb.v9、quill、vue2
# plugins/modules
- https://github.com/quill-mention/quill-mention /635Star/MIT/202311/js/inactive
  - https://quill-mention.com/
  - a module to provide @mentions or #hashtag functionality for the Quill rich text editor.
  - https://github.com/devdcodes9/quill-mentionjs /202401/js

- https://github.com/xie392/quill-mention-react /MIT/202403/ts
  - https://quill-mention-react.vercel.app/
  - Quill 富文本编辑器的 @mentions

- https://github.com/raphaelM-sudo/quill-emoji-mart-picker /MIT/202006/ts
  - https://quill-emoji-mart-picker.netlify.com/
  - Module and Blot for Quill.js that supports Emoji Mart Picker and Emoji Mart.
  - converts unicode emojis, emoticons and emoji names into emoji images from Apple, Google, Twitter, EmojiOne, Facebook Messenger or Facebook.
  - https://github.com/mr04vv/quill-emoji-mart-picker /202108/ts

- https://github.com/benoitlahoz/quill-emoji-parser /MIT/202401/ts
  - https://benoitlahoz.github.io/quill-emoji-parser/
  - Checks for emojis shortcuts during typing and pasting and replace them by their visual counterpart.
  - inspired by quill-magic-url 
  - Default map is taken from Smile2Emoji

- https://github.com/artknight/quill-emoji /MIT/202310/ts
  - Module extension for Quill.js that handles emojis in the toolbar.
  - https://github.com/xingw-z/quill2-emoji /202305/ts
- https://github.com/devdcodes9/quill-emojijs /202402/js
  - Module extension for Quill.js version 2.0 that handles emojis in the toolbar

- https://github.com/contentco/quill-emoji /202111/js
  - Module extension for Quill.js that handles emojis in the toolbar.
  - you can add emojis through the toolbar at the top, or by typing the emoji code.
  - https://github.com/adtribute/quill-emoji /202402/js
    - remove the sprites, remove the css rules that use sprite
  - https://github.com/FuseDesk/quill-emoji /202310/js
    - dropped node-sass, moved to sass

- https://github.com/koffeinfrei/quill-task-list /201806/js
  - Adds a task/todo list to the quill editor. Includes a toolbar item.
  - Behaves as the built-in bullet list.
- https://github.com/yslyong/React-Quill-Improved-Listing /202303/ts
  - contain two fixes for React Quill Listing to make it have a similar feeling with .docx listing

- https://github.com/contentco/quill-inline-comment /201710/js
  - Module that handles inline comment like medium

- https://github.com/zaffnet/quill_spellcheck_demo /202101/js
  - https://zaffnet.github.io/quill_spellcheck_demo/
  - Spellcheck in a WYSIWYG Editor. I have modified the Tooltip provided by Quill to suggest words.

- https://github.com/mithya-team/rte-quill-plugin /MIT/202401/ts
  - a plugin for integrating Quill rich text editor with your form library
  - provides an easy-to-use interface for creating rich text content within forms handled by popular form libraries like React Hook Form, Formik, or Redux Form.

- https://github.com/mindroute/quill-form /201809/js
  - Module for form bindings and input fields in Quill
  - Automatically creates hidden input fields for a form and adds submit handling and submit by key (⌘/Ctrl+S). 
  - It creates fields for text, html and delta.

- https://github.com/lukevp/quill-fire /202305/ts
  - Extend Quill JS editor to fire events as soon as matching text is entered
- https://github.com/mindroute/quill-autoformat /201903/js
  - Module for formatting and transforming text as you type in Quill
  - Using RegExp to find and trigger transformations for text such as links, mentions, hashtags or emojis. 
  - Requires Quill 2.0

- https://github.com/T-vK/DynamicQuillTools /201911/js
  - https://t-vk.github.io/DynamicQuillTools/example.html
  - allows you to dynamically add or remove new custom elements to/from a Quill Editor's toolbar

- https://github.com/rain0002009/quill-divider /202207/ts
  - Module extension for Quill.js that handles divider in the toolbar.

- https://github.com/HimasRafeek/quilljs-floating-toolbar /202402/js
  - plugin adds a floating toolbar to the Quill editor. 
  - When text is selected within the Quill editor, a custom floating toolbar appears above the selection
  - Make sure to include this plugin after jQuery and Quill scripts.

- https://github.com/machengqi/quill-clipboard-plugin /202207/ts
  - module plugin for clipboard pasted files, it can help you filter clipboard file size and mimetypes, and provides a hook to help you substituted error files

- https://github.com/MuhammedAlkhudiry/quill-find-replace-module /201909/js
  - https://codepen.io/muhammedalkhudiry/pen/VoMxeK
  - A module for Quill rich text editor to allow searching/finding words and replacing them.
- https://github.com/Lmangoxx/quill-find-replace-module /202201/ts
  - quill富文本编辑器”搜索查找“扩展模块

- https://github.com/CHere/quill-find-and-replace /GPL/202302/js
  - adds find and replace functionality to the quill rich text editor

- https://github.com/gocodebox/lifterlms/tree/trunk/packages/quill-wordcount-module /202208/js
  - Word count module for Quill.
  - Uses words-count to perform word counting in multiple languages and character sets.

- https://github.com/rain0002009/quill-position-placeholder /201907/ts
  - 一个Quill.js的插件，用来添加一个使用百分比高度的占位元素。
- https://github.com/jspaine/quill-placeholder-module /201807/ts
  - https://codepen.io/jspaine/pen/MozyNp
  - Quill module for adding placeholders
  - https://github.com/kathirr007/quill-placeholder-module-forked /202312/ts
- https://github.com/Datananas/quill-placeholder-autocomplete /201809/js
  - brings autocomplete to quill-placeholder-module

- https://github.com/jmquigley/quill-markup /201912/ts
  - A markup highlighting module for the Quill text editor

- https://github.com/visualjerk/quill-magic-url /MIT/202208/ts/inactive
  - Automatically convert URLs to links in Quill
- https://github.com/juyeong1260/quill-auto-detect-url /202105/ts
  - transform the url of the url as the user types.
  - based on quill-magic-url
- https://github.com/kyoncy/quill-linkify /202209/ts
  - plugin that converts URL, mail address, phone number to link.

- https://github.com/brettimus/quill-local-storage /201506/js
  - a local storage module for restoring "drafted" text to the quilljs editor

- https://github.com/benwinding/quill-html-edit-button /202311/ts
  - https://benwinding.github.io/quill-html-edit-button/script-tags/demo-quill-1.x.html
  - Module which allows you to quickly view/edit the HTML in the editor

- https://github.com/Artem-Schander/quill-paste-smart /202307/js
  - module to paste only supported HTML
  - extends the default clipboard module of Quill.js to prevent users from pasting HTML that does not belong into the editor.

- https://github.com/qvarts/quill-toggle-fullscreen-button /202310/ts
  - module which adds a toggle fullscreen button to the Quill editor toolbar.

- https://github.com/CHNB128/quill-attachments /202109/js
  - Attachments plugin for Quill rich text editor
  - https://github.com/Shatiger/quill-attachments /202310/js

- https://github.com/nvt-ak/quill-upload /202403/js
  - A plugin for uploading image, video, attachment in Quill 
  - upload a image, video, attachment when it is inserted, and then replace the base64-url with a http-url
  - preview the image, video, attachment which is uploading with a loading animation

- https://github.com/lw1995/quill-video-image-module /202008/js
  - 整合视频上传，图片上传到服务器模块，用video标签替换iframe，中文提示框，中文描述

- https://github.com/NoelOConnell/quill-image-uploader /218Star/MIT/202305/js/inactive
  - allow images to be uploaded to a server instead of being base64 encoded
  - Adds a button to the toolbar for users to click, also handles drag, dropped and pasted images
  - https://github.com/fxmontigny/quill-image-upload /201812/js
  - https://github.com/dragonwong/quill-plugin-image-upload /201811/js
  - https://github.com/xiangchuifeng/quill-image-upload-v2 /202304/js

- https://github.com/xeger/quill-image /202310/ts
  - provide resizable, floatable images that cleanly "round trip" between HTML and JSON.
  - a fork and rewrite of quill-blot-formatter
  - https://github.com/redTreeOnWall/quill-image
  - https://github.com/UMN-LATIS/quill-better-image-module

- https://github.com/portive/quill-images /202311/ts
  - https://codepen.io/scottward/pen/RwvjOVJ
  - Add image uploads with click to upload, drag and drop and paste support.
  - Includes upload progress bar, quick image preview, server side image resizing, presets, support for higher DPI devices with srcset.

- https://github.com/chenjuneking/quill-image-drop-and-paste /ISC/202304/ts/inactive
  - module for drop and paste image, with a callback hook before insert image into the editor
  - by default, it would insert a image with a base64 url
  - 提供了多个框架的demo
- https://github.com/x-cold/quill2-image-drop-and-paste /202112/ts
  - https://x-cold.github.io/quill2-image-drop-and-paste/
  - module for drop and paste image, with a callback hook before insert image into the editor

- https://github.com/Nelwhix/quill-image-uploader /202303/ts
  - plugin that uploads images inserted, drag/dropped or pasted into the quill editor to a server instead of being base64 encoded.

- https://github.com/kensnyder/quill-image-drop-module /201703/js
  - A module for Quill rich text editor to allow images to be pasted and drag/dropped into the editor.

- https://github.com/benwinding/quill-image-compress /MIT/202402/ts
  - https://benwinding.github.io/quill-image-compress/src/demo.html
  - compresses images that are uploaded to the editor

- https://github.com/phamquyetthang/react-quill-image-upload /202307/ts
  - Image upload in quill editer, React-quill + cloudinary
  - https://github.com/krishnawaghmode/reactjs-quilljs-image-upload-server

- https://github.com/EthanYan6/quill-image-super-solution-module /202103/js
  - vue-quill-editor 的专用插件，为其提供了自定义上传图片到服务器、粘贴图片上传至服务器、拖拽图片上传至服务器的功能

- https://github.com/scrapooo/quill-resize-module /202209/ts
  - A module for Quill rich text editor to allow images to be resized.
  - enables resize for image/iframe/video.
  - https://github.com/arnauddrain/quill-media-resize /ts
- https://github.com/hunghg255/quill-resize-image /202308/ts
  - https://quill-resize-image.vercel.app/
  - A plugin resize image for Quilljs

- https://github.com/kensnyder/quill-image-resize-module /201807/js
  - A module for Quill rich text editor to allow images to be resized.
  - https://github.com/kensnyder/quill-image-resize-module /202311/js
- https://github.com/mild-blue/even-better-quill /202402/ts
  - imageResize - originaly based on quill-image-resize-module
  - https://github.com/mild-blue/quill-even-better-image /202307/ts

- https://github.com/CracKerMe/quill-format-img /202305/js/inactive
  - a module for the Quill text editor to allow blots to be reformatted. 
  - Built in formatters: resize and realign. 
  - Built in blot support: images. and add image open link
  - Heavily inspired by quill-image-resize-module. 

- https://github.com/agendaedu/quill-image-resize-module-react-mobile /202101/js
  - A module for Quill rich text editor to allow images to be resized.
  - https://github.com/LucasAnitelli/quill-image-resize-module-react-mobile

- https://github.com/mudoo/quill-resize-module /202003/js
  - allow images/iframe/video and custom elements(convert to placeholder) to be resized.
  - original forked from https://github.com/whatcould/quill-image-resize-module.

- https://github.com/Fandom-OSS/quill-blot-formatter /201803/js
  - https://codesandbox.io/s/4wnwllnnl9
  - A module for Quill that allows editor elements to be resized, repositioned, etc
  - 支持缩放image/video
  - module to format document blots. Heavily inspired by quill-image-resize-module.
  - supports resizing and realigning images and iframe videos, but can be easily extended using BlotSpec and Action.
  - 🍴 forks
  - https://github.com/lidessen/quill-blot-formatter-es /202401/ts
    - es6 module format. Forked from quill-blot-formatter
  - https://github.com/juandjara/quill-blot-formatter-mobile /202103/js
    - a fork of quill-blot-formatter that adds support for touch screen on mobile devices
  - https://github.com/time-loop/quill-blot-formatter /202304/js
    - Publish as es6
  - https://github.com/acatec/quill-blot-formatter-extended /201912/js
    - remove video support becouse it was very bad and for video it is enough to be 100% width anytime
  - https://github.com/badrazizi/quill-blot-formatter-new /202101/js
    - disable user text selection while resizing images
  - https://github.com/devhus/quill-blot-formatter-vite /202209/js

- https://github.com/simialbi/quill-smart-break /202004/js
  - Support shift + enter in Quill WYSIWYG editor

- https://github.com/mathquill/mathquill /2.5kStar/MPLv2/202201/ts/NoDeps
  - http://mathquill.com/
  - a web formula editor designed to make typing math easy and beautiful.
  - 不依赖quill
- https://github.com/drlippman/MathQuillEditor /201906/js
  - experiments with adapting an entry palette to work with MathQuill 0.10

- https://github.com/c-w/mathquill4quill /202311/js
  - https://justamouse.com/mathquill4quill
  - adds support for rich math authoring to the Quill editor.
  - depends on MathQuill, Quill and KaTeX

- https://github.com/vieyama/quill-editor-math /202304/ts/inactive
  - Rich text editor with react quill, mathquill4quill, katex, and image resizer. you can use formula with this.

- https://github.com/manaragr/mathTextEditor /202307/js
  - https://math-text-editor.vercel.app/
  - combines the power of ReactQuill for text editing, MathLive for mathematical typesetting , and KaTeX for rendering math expressions.

- https://github.com/JonathanTreffler/Quill-mathLive-blot /202107/js
  - A Blot/Extension for Quill.js to embed editable formulas with mathLive.
- https://github.com/JonathanTreffler/Quill-mathQuill-blot
  - A Blot/Extension for Quill.js to embed editable formulas with mathQuill.

- https://github.com/digabi/rich-text-editor /67Star/MIT/202311/js
  - http://digabi.github.io/rich-text-editor/
  - Math editor
  - Rich text editor with math support for Finnish Matriculation Examination Board
  - allow candidates to attach screenshots and write equations as part of their submissions.
  - by MathJax and MathQuill, jquery

- https://github.com/reedsy/quill-cursors /202301/ts
  - A multi cursor module for Quill text editor.
  - https://github.com/welkinwong/superdocs-quill-cursors

- https://github.com/devaman/quill-selection /202403/js
  - a module to provide selection and show dropdown functionality for the Quill rich text editor.
  - Disabled items are shown but not selectable with the mouse or keyboard.

- https://github.com/amiller-gh/quill-hr /202004/js
  - module for horizontal rules.

- https://github.com/MeccaMedialight/quillwrap /201912/js
  - Module for converting textareas into Quill-powered editors
  - https://github.com/luke-mml/quillwrap-demo

- https://github.com/vantezzen/quill-languagetool /202312/ts
  - https://vantezzen.github.io/quill-languagetool
  - LanguageTool integration for Quill.js editors
- https://github.com/anderneath/react-quill-spell-checker /MIT/202310/ts
  - Integrate any spell checker on Quill.js editor
  - Custom server support
  - Using this module will change the contents of the editor to add control elements for spell checking and grammar checking.
# starter
- https://github.com/darriwil/quill-delta-generator /MIT/202402/ts
  - https://quill-delta-generator.netlify.app/
  - 单文件编辑器示例

- https://github.com/quilljs/webpack-example /202403/ts/单文件
  - A working example of building Quill as part of a larger application build pipeline using Webpack.

- https://stackblitz.com/edit/quill-editor-demo
  - [Render React Component inside Quill without losing context_202004](https://culture.kissflow.com/render-react-component-inside-quill-without-losing-context-151eac4eda08)
# examples
- https://github.com/jotform/dnd-builder /43Star/MIT/202402/js
  - https://www.jotform.com/open-source/dnd-builder/
  - accessible drag and drop page builder with React
  - 依赖use-gesture、fuse.js、react-dnd-cjs、react-quill、react-sortable-hoc、react-zoom-pan-pinch、react-window、recharts
  - 示例丰富，支持preview/ppt/print

- https://github.com/form-js/forms.js /MIT/202404/ts
  - https://formsjs.io/
  - Fully featured javascript form builder
  - core依赖tom-select、filepond、flatpickr
  - 其他依赖quill.v1
  - Field Types: Includes text, file, date/time, rich text, and more
  - Conditional Logic & Validation
  - Simplified event management for dynamic user experiences
  - Deigned for customization and extension.
  - Clean API: ease of use for developers and accessibility for users

- https://github.com/jado66/reactive-site-creator /CC-BY-NC/202303/js/inactive
  - https://jado66.github.io/reactive-site-creator-live/
  - A website creator for React.
  - 依赖dnd-kit、react-quill、react-reveal、bootstrap5

- https://github.com/devat-youtuber/MERN-Typescript-Blogdev /202207/ts
  - MERN Stack Build a blog app using MERN + Typescript + Redux + Bootstrap 5 + ReactQuill + Socket.io + Twilio
- https://github.com/RyanPPitts/React-Blog-Editor /202001/js
  - Blog built with the MERN stack, Quill Editor Tool & MongoDB
- https://github.com/weilyuwang/react-quill-blog /202103/js
  - A quill editor with custom media files upload functionalities, integrated with AWS S3.

- https://github.com/sharvdalal/Mern-Blog /202312/js
  - This project is a blog website built using the MERN stack - MongoDB, Express.js, React, and Node.js. 
  - It serves as a platform for users to create, publish, and manage their blog posts.

- https://github.com/j-berman/hush-docs /MIT/202102/js
  - https://hushdocs.com/
  - offline-first, private Google Docs alternative.
  - using IndexedDB/Dexie.js
  - Docs stay in sync using CRDTs (Automerge)
  - 依赖userbase-js、automerge.v0.14、dexie.v3、jquery、quill、workbox
  - https://github.com/smallbets/userbase /js
    - Userbase is the easiest way to add user accounts and user data persistence to your static site.

- https://github.com/AChiabodo/SimpleCMS /202403/js/fe+be
  - A simple Blog implemented in React.js and Node.js

- https://github.com/mushfiqweb/mybl-cms /202311/ts/仅前端/样式友好/inactive
  - MyBL CMS React Template
  - 依赖redux-toolkit、tanstack-table、fullcalendar、apexcharts、quill、formik

- https://github.com/aniruddha-jafa/notes-app /202110/js/inactive
  - A fullstack web app based around the open-source quill.js text editor
  - back-end uses Express & mongoDB、ejs

- https://github.com/lisnyaknikita/mini-notion /202305/ts/inactive
  - https://mi-notion.netlify.app/
  - Redux Toolkit, RTK Query; React quill(editor for notes and journaling); 
  - 不支持拖拽

- https://github.com/vuquangpham/boilcms-ec /MIT/202311/js
  - A CMS that has been built with Node.js and Express.js
  - 依赖express、ejs、mongoose、quill
  - https://github.com/vuquangpham/boilcms-ec
    - https://boilcms-ec.vercel.app/
    - Boilcms with Ecommerce

- https://github.com/plsrd/hark /MIT/202212/js
  - a tiny CMS for authoring blog content

- https://github.com/klaudsol/klaudsol-cms /MIT/202307/js
  - https://cms-demo.klaudsol.app/
  - a Headless and Serverless CMS (Content Management System). 
  - A great alternative to WordPress and Strapi.
  - 依赖@coreui/react、nivo、nextjs、react-redux、react-bootstrap、react-quill
  - Deploys seamlessly to AWS Amplify Hosting + AWS Aurora Serverless

- https://github.com/johnpolacek/bucket-cms /202311/ts
  - https://bucket-cms.com/
  - lightweight CMS around – ready for you to drop into your Next.js project.
  - no database necessary
  - 依赖react-quill、next-auth、radix-ui

- https://github.com/ProtoDigitalUK/proto_headless /202404/ts
  - headless CMS offering a delightful developer experience.
  - 依赖fastify、pg、sharp、solidjs、quill

- https://github.com/folkloreinc/panneau-js /201909/js/inactive
  - https://folkloreinc.github.io/panneau-js/storybook/index.html
  - React components to build forms and administration panels
  - 依赖ckeditor5-react、react-quill，实现了可切换的版本

- https://github.com/origami-cms/cms /201902/ts/inactive
  - http://www.origami.so/
  - flexible and open-source CMS built for Node.js
  - built on Node.js and Express with flexibility as it's primary value.
  - Use any database, any templating language
  - admin依赖lit-html

- https://github.com/vapid/vapid /MIT/202101/js/archived
  - https://github.com/vapid/vapid
  - simple content management system built on the idea that you can create a custom dashboard without ever leaving the HTML.
  - 依赖 ace、jquery、quill、turbolinks、koa、sequelize.v5
  - 🍴 forks
  - https://github.com/universe/vapid

- https://github.com/webpoint-solutions-llc/easy-blog-cms /202309/ts
  - The API is designed to be consumed by any client, be it a web application (React, Vue, Angular)
  - 前端依赖tanstack-query、quill、localforage
  - 后端依赖nestjs

- https://github.com/entando/entando-cms /LGPLv3/202110/js
  - This project contains the App Builder screens for the CMS app of Entando.
  - https://github.com/entando/app-engine /java

- https://github.com/LargeNFT/large-nft /202401/ts
  - decentralized CMS for Ethereum & IPFS that runs offline-first in the browser.
  - Publish content as a collection of Ethereum NFTs.
  - 依赖ethers、framework7、ipfs、level-js.v6、inversify、memfs、pouchdb、quill、workbox

- https://github.com/WebDevSimplified/google-docs-clone /ISC/202104/js
  - 最简单的示例，几乎单文件
  - 依赖quill, react、mongoose、socket.io

- https://github.com/luanpanno/google-docs-clone /202105/ts
  - Google Docs Clone with Node, React, Socket.io and Quill
  - https://github.com/seifeldeen92/google-docs-texteditor-clone
  - https://github.com/Chondan/google-doc-clone
  - https://github.com/Khusheel26/Google-docs-clone
  - https://github.com/Danitilahun/SmallGoogleDocClone
  - https://github.com/klublin/google-docs-clone /202212/js/4milestones

- https://github.com/NickMandylas/noogle-docs /202106/ts
  - Google Docs clone built with Typescript, inspired by Web Dev Simplified
  - Front-end: Built with ReactJS (utilising Create React App). The TextEditor used is QuillJS.
  - Back-end: Fastify (with Fastify-WebSockets), PostgreSQL and Redis.

- https://github.com/realsnipc/OG-Docx-Editor /MIT/202401/js/fe+be
  - Google Docs inspired awesome docs editor. 
  - Built with React, Quill, Tailwind, Socket.io and MongoDB

- https://github.com/bryanakitchen/google-docs-clone-server /202105/js
  - uses Socket.io, Quill, and Mongoose to generate a text editor that will allow for simultaneous edits.
  - https://github.com/bryanakitchen/google-docs-clone-front
  - https://github.com/bryanakitchen/google-docs-clone /client+server

- https://github.com/Bunty9/Google-docs-backend /202104/js
  - Backend of the Google docs clone , based on socket.io , express and mongoDb
  - https://github.com/Bunty9/Google-docs-frontend

- https://github.com/ajCastiglione/google-docs-clone /202306/js
  - https://google-docs-clone-mwd.netlify.app/
  - Built to replicate the live document editing experience of Google docs.
  - Saves every 2 seconds to instance based on URL ID
  - https://github.com/ahzamir/google-docs-clone
  - https://github.com/Nukealbert/google-doc-editor-clone
  - https://github.com/WinnardArthur/google-docs-clone
  - https://github.com/ramyatrouny/GoogleDocs-Clone
  - https://github.com/ayushjha952/Google_docs_clone

- https://github.com/Braysen/EvernoteClone /202011/js
  - Build a Evernote Clone with REACT JS
  - https://github.com/Wellers0n/evernote-clone /202001/js

- https://github.com/westhyun/all-notes-app /202307/ts
  - https://all-notes-app.vercel.app/
  - Redux-toolkit, react-quill, LocalStorage

- https://github.com/urbanogardun/monte-note /GPLv3/201804/ts
  - Note taking application with a rich set of editing and management features
  - 依赖electron-store、nedb、jquery、quill、react-redux

- https://www.npmjs.com/package/@nocobase/client
  - 依赖react-quill.v1

- ddd-forum /1.8kStar/ISC/202306/ts
  - https://github.com/stemmlerjs/ddd-forum
  - https://dddforum.com/
  - Hacker news-inspired forum app built with TypeScript using DDD practices from solidbook.io.
  - 后端依赖 express、sequelize、redis
  - 前端依赖 react、redux、react-quill
  - https://github.com/dyarleniber/typescript-ddd-forum

- https://github.com/izkshitiz/natforums /202303/js
  - https://natforums.netlify.app/
  - Community forums management system
  - 依赖quill、graphql、express

- https://github.com/oldboyxx/jira_clone /202001/前端js+后端ts
  - https://jira.ivorreic.com/project/board
  - A simplified Jira clone built with React/Babel (Client), and Node/TypeScript (API). 
  - 前端依赖 react-router、formik、history、jwt、moment、quill(Editor)、react-beautiful-dnd、styled-components、sweet-pubsub
  - 后端依赖 express、jsonwebtoken、faker、pg、typeorm

- https://github.com/vedant-3010/WiredSapien /202310/js
  - A Blogging platform using MERN Stack and quill WYSIWYG editor.
- https://github.com/AhmedAli9991/Document-CVS-Centralized-Verion-Control-System-Full-stack-APP /202205/js
  - manages various documents a user creates as repositories user can make versions and also add other users as collaborators in the project it has been made using the MERN stack

- https://github.com/bridgerbrown/daynotes /202311/ts
  - https://daynotes-ebon.vercel.app/
  - A calendar-based note taking platform that uses web sockets for seamless synchronization between browser tabs.
  - save notes made with the Quill.js text editor to a MongoDB database. 
  - Built with Node.js, Express.js, Socket.io, React, TypeScript, MongoDB, Quill.js, Date-fns, HTTP, BCrypt, TailwindCSS, and NextJS

- https://github.com/rrecalo/ONote /202311/ts
  - A single-page note taking web app in React powered by the Quill JS library, Auth0, and MongoDB 
  - hosted using Netlify, AWS EC2, and AWS Route53

- https://github.com/Noelzak03/quill-frontend /202311/js
  - https://quill-teal-omega.vercel.app/
  - a multiplayer drawing and guessing platform.
  - 不支持协作，但交互已搭建
  - 依赖excalidraw、nextjs

- https://github.com/ErcouldnT/code-together /202106/js
  - An Express, Socket.io, React project to work together on a single webpage simultaneously.

- https://github.com/marchetti2/kanban-reactjs /202202/ts
  - Firebase Firestore/Auth, react-beautiful-dnd, Chakra-ui

- https://github.com/LogicalAnt/live-doc /ts
  - a small live editor using React-Quill editor and Socket.io

- https://github.com/yangzongzhuan/RuoYi-Vue /202311/java/vue
  - http://ruoyi.vip/
  - 基于SpringBoot，Spring Security，JWT，Vue & Element 的前后端分离权限管理系统，同时提供了 Vue3 的版本
  - https://github.com/yangzongzhuan/RuoYi-Vue-fast

- https://github.com/omzeton/notnik /202202/ts/vue
  - Notebook app (Vue - Quill - Express - MongoDB)

- https://github.com/Kibo/filemanager-js /202201/ts/vue
  - JavaScript filemanager for CKEditor4, Quill, TinyMCE5.

- https://github.com/joduplessis/weekday /202309/js
  - https://weekday.work/
  - Weekday is a messaging-first collaboration platform that gives your team superpowers. 
  - 依赖pouchdb、react-quill、redux、rxjs、graphql、apollo

- https://github.com/huygamcha/Ecommerce /202404/ts
  - https://ecommerce-huygamcha.vercel.app/
  - client + server

- https://github.com/pandeyrochak/quillpages /202403/ts
  - https://quillpages.vercel.app/
  - This is the official repository for Penit, a blog application.
  - 依赖next-auth、swr、react-quill、firebase、@prisma/client

- https://github.com/VedanthB/bloggingly-frontend /202210/ts/inactive
  - https://github.com/VedanthB/bloggingly-backend
  - a blogging platform, where you can upload and view blogs and create your own blog page
  - Client: TypeScript, React, Redux Toolkit, TailwindCSS, React Quill Markdown Editor
  - Server: Node, Express, TypeScript

- https://github.com/Top-Ranger/writergo /202403/go/js
  - A simple collaborative editing software

- https://github.com/y8nju/QuillTextEditor /202303/ts
  - https://text-editor-one.vercel.app/
  - react-quill

- https://github.com/relatedcode/Messenger /202208/ts/swift/inactive
  - https://relatedcode.com/
  - RelatedChat is an open-source alternative communication platform. 
  - Both iOS (Swift), Android (React Native), and Web (React) version source codes are available.
  - Single backend server (using GraphQLite-swift)
# collab/ot
- https://github.com/WindrunnerMax/Collab /202308/ts
  - 初探富文本之OT协同实例 sharedb+quill
  - 初探富文本之CRDT协同实例 yjs+quill

- https://github.com/kindone/text-versioncontrol /MIT/202208/ts/inactive
  - provides version and concurrency control for text editing based on OT(Operational Transformation) and CRDT(Conflict-free Replicated Data Type) ideas
  - Text-VersionControl utilizes Quill's Delta representation in JSON. 
  - Text-VersionControl borrows Quill Delta's representation and many of its method names but does not behave the same in a few cases.

- https://github.com/Kannndev/Collaborative-rich-text-editor /202010/js
  - https://github.com/Kannndev/Collaborative-rich-text-editor-server
  - Collaborative rich text editor using react and quill js
  - 依赖sharedb、quill.v1、ws
  - https://github.com/arus-archive/collaborative-rich-text-editor
  - https://github.com/baegmon/React-ShareDB-Example
  - https://github.com/danfuzz/bayou
- https://github.com/rohitrp/collaborative-editor-sharedb-quilljs /201806/js
  - a modified version of collaborative rich text editor using Quill and the rich-text OT type
  - In this demo, data is not persisted

- https://github.com/pedrosanta/quill-sharedb-cursors /201801/js
  - An attempt at multi cursors sync in a collaborative editing scenario using Quill, a ShareDB backend, and the reedsy/quill-cursors Quill module

- https://github.com/CJEnright/quill-ot.js /201812/js
  - An Operational Transformation implementation for use with the web based rich text editor Quill. 
  - This library was based on Operational-Transformation created by Tim Baumann. 
- https://github.com/Dev1an/Quill-Operational-Transform /201706/js
  - A demo on how to transform Deltas obtained from the Quill text editor to resolve conflicts in text documents. 
  - The demonstration uses meteor's minimongo database: an in-browser version of the popular MongoDB database.

- https://github.com/we-miks/collaborative-editor /202108/js/inactive
  - A collaborative editor that supports authorship display, image uploading placeholder and CJK characters composition based on Quill and ShareDB.

- https://github.com/Zeekg-zk/Collaborative-Platform /202210/ts/inactive
  - https://github.com/zach-xing/Collaborative-Platform
  - 团队协作与管理平台，具有在线多人聊天、消息实时推送、协同编辑等功能
  - 前端使用 NextJS 12.2.0，后端使用 NestJS 8.0
  - 后台管理界面使用 Ant Design Pro
  - 支持多人协作文档（使用 Quill 富文本编辑器）

- https://github.com/anjalipal2001/QuillSync /202403/ts
  - Real time Collaborating App
  - 依赖radix-ui、@supabase/supabase-js、drizzle-orm、quill.v1、socket.io
  - https://github.com/EduardStroescu/QuillScribe
# collab-crdt
- https://github.com/mweidner037/list-demos/tree/master/triplit-quill /202401/ts
  - Basic collaborative rich-text editor that synchronizes using the Triplit fullstack database. 
  - The editor is Quill.

- https://github.com/WindrunnerMax/Collab /202308/ts/inactive
  - 初探富文本之OT协同实例 sharedb+quill
  - 初探富文本之CRDT协同实例 yjs+quill

- https://github.com/F-star/yjs-quill-simple-demo /202310/ts/inactive
  - HOST=localhost PORT=1234 npx y-websocket

- https://github.com/jaredly/local-first/tree/master/packages/text-crdt /202104/js/inactive
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.
  - Your approach seems to resemble RGASplit which I believe is bases for

- https://github.com/arusikgrigorian/Rich_Editors_Socket_Integration /202404/ts
  - Integration of Quill and Slate with y-websocket

- https://github.com/loro-dev/crdt-richtext /169Star/MIT/202305/rust
  - https://crdt-richtext-quill-demo.vercel.app/
  - Rich text CRDT that implements Peritext and Fugue
  - This CRDT lib combines Peritext and Fugue's power, delivering impressive performance specifically tailored for rich text. 
  - It leverages the `generic-btree` library to boost speed, and the `serde-columnar` simplifies the implementation of efficient columnar encoding.
  - loro-wasm and fugue only support plain text for now

- https://github.com/phedkvist/crdt-woot /202204/ts
  - Implementation of collaborative editing algorithm CRDT WOOT.
  - 示例使用react-quill
  - https://github.com/phedkvist/crdt-server
- https://github.com/PHedkvist/crdt-sequence
  - 自己实现了 history、activeUsers
  - quill的功能使用得很少
  - dev-to
    - 多人光标待改进
  - https://github.com/PHedkvist/crdt-server

- https://github.com/automerge/pushpin /BSD/202101/ts/inactive
  - a mixed media canvas workspace similar to Miro or Milanote.
  - A local-first collaborative corkboard app. 
  - Built with Electron, React, automerge and hypermerge.
  - 依赖automerge、quill

- https://github.com/pedrogao/co-editor /202212/ts/vue/inactive
  - 协同 markdown 编辑器
  - 还未开发完成，目前仅仅是一个 demo

- https://github.com/yjs/y-quill /MIT/202205/js/inactive
  - https://demos.yjs.dev/quill/quill.html
  - This binding maps a Y. Text to a Quill instance. 
  - It optionally supports shared cursors via the quill-cursors module.
- https://github.com/sameer1612/quilly /202205/ts
  - Collaborative editing using Quill.js and Y.js

- https://github.com/ethanryan/textedit-app /201807/js
  - Collaborative text editing app, built with React, Express, Quill, and Yjs.

- https://github.com/peer-base/peer-pad /MIT/201907/js
  - Online editor providing collaborative editing in really real-time using CRDTs and IPFS.
  - 依赖codemirror5、quill.v1、remark.v10、delta-crdts
  - https://github.com/peer-base/js-delta-crdts /201910/js

- https://github.com/widmogrod/js-crdt /ts/201711
  - explore applications of data structure called CRDT in context of real time collaboration 
  - https://github.com/widmogrod/notepad-app /201710/ts
    - Collaborative notepad app (demo).
    - 依赖quill

- https://github.com/mweidner037/firebase-text-editor
  - Collaborative plain text editor using CRDTs on top of Firebase (Realtime Database).
  - 依赖position-strings，不依赖quill
  - https://github.com/mweidner037/firebase-rich-text-editor
    - 依赖quill.v1

- https://github.com/jeremysamuel13/cse356-google-docs /202211/ts
  - client + server + elasticsearch
- https://github.com/kazijamal/collaborative-doc-editor /202301/ts/yjs
  - A collaborative document editor similar to Google Docs capable of handling 3000 requests per second with a 95th percentile latency of 30ms

- https://github.com/Glissen/StarDocs2 /202212/ts/yjs
  - client + server
# delta
- https://github.com/vincentdchan/delta-es /BSD/202311/ts
  - a forked version to quill-delta
  - es module for tree shaking.
  - unit tests are rewritten using Vitest.
  - `lodash` is removed from the dependencies.

- https://github.com/mundo-68/quill-delta-rs /MIT/202402/rust
  - A rust re-implementation of the quill delta format
  - https://github.com/mundo-68/quill-core-rs /202402/rust
    - A Rust re-implementation of the well known Quill HTML editor.
    - Translate a Delta document to a HTML DOM
    - Translate the current DOM state back to a Delta document
    - Edit the Delta document using operational transform commands
    - Provide a set of formats that translate Delta operations to HTML DOM
- https://github.com/amantoux/quill-delta-rs /MIT/202404/rust
  - Implementation of Quill editor Delta format in Rust
- https://gitlab.com/SimVet/quill-delta /MIT/201808/rust
  - Delta impelmentation of quill delta

- https://github.com/thuanthe81/quill-delta-diff /202207/ts
  - an enhancement of quill-delta

- https://github.com/andrewanthro/quilljs-parser /202304/ts
  - Transform your QuillJS contents into an easier-to-use paragraph format.
  - parseQuillDelta() function will return an easier-to-use paragraph version of the Delta

- https://github.com/mbb10324/quill-json-converter /apache2/202312/js
  - https://mbb10324.github.io/quill-json-converter/
  - Convert a quill editor to a quill delta, and vice-versa

- https://github.com/workiom/delta-md-converter /202312/ts
  - Convert from Quill Delta to Markdown and from Markdown to Quill Delta.
- https://github.com/buu700/quill-markdown /202301/ts/inactive
  - Converts between Quill deltas and Markdown

- https://github.com/frysztak/markdown-to-quill-delta /202205/ts
  - Converts Markdown to Quill Delta using remark.
- https://github.com/volser/md-to-quill-delta /201911/ts
  - `import { MarkdownToQuill } from 'md-to-quill-delta';`

- https://github.com/yucheng-Li/quill-converter-xp /202308/js
  - Convert HTML to a Quill Delta or a Quill Delta to HTML
  - 去掉 fs 模块
  - https://github.com/joelcolucci/node-quill-converter /202001/js
    - Convert HTML to a Quill Delta or a Quill Delta to HTML

- https://github.com/nozer/quill-delta-to-html /MIT/202204/ts/inactive
  - Converts Quill's delta ops to HTML
  - https://github.com/wirechunk/quill-delta-to-react /202404/ts
    - Render Quill's Delta ops in React
    - we take performance seriously. You can have many instances of a RenderDelta component on a page, and it will render quickly and efficiently.
    - In addition to providing custom HTML element tags, classes, styles, and any other attribute, you can define custom Op types and provide a rendering function for these types with a `customRenderer` prop.
  - https://github.com/sudowrite/quill-delta-to-html-fork
    - Although it's open source, it's not intended for general use
  - https://github.com/microcmsio/quill-delta-to-object
    - Not Supported: Image, Video, Table, Nested List

- https://github.com/xeger/quill-deltacvt /202306/ts
  - Converts Quill Delta to HTML (or other formats) without depending on quill, parchment or quill-delta

- https://github.com/mastito03/render-quill /201704/js
  - render quill delta to html string on server

- https://github.com/UmbraEngineering/quilljs-renderer /201503/js
  - Renders an insert-only Quilljs delta into various format like HTML and Markdown
- https://github.com/casetext/quill-render /201510/js
  - Renders a sequence of quill insert-only deltas (operational transforms) into HTML with no browser dependencies.
  - using cheerio to build a DOM from the delta sequence.

- https://github.com/FPG-Alan/quill-delta-parser /202210/rust/inactive
  - parse delta of quill to html(only insert)

- https://github.com/forgeworks/quill-delta-python /202010/python/js
  - Python port of the Quill-JS Delta library - Has support for HTML Rendering

- https://github.com/Orange-Murker/quill_delta_pdf 202403/rust
  - Parse and convert Quill's Deltas to PDF documents.

- https://github.com/slab/delta-elixir /BSD/202312/elixir
  - Simple yet expressive format to describe contents and changes 
# utils
- https://github.com/andrewanthro/quilljs-parser /202101/ts
  - Parse a QuillJS delta
  - Transform your QuillJS contents into an easier-to-use paragraph format

- https://github.com/boomanaiden154/quillgethtml /MIT/202311/js
  - https://boomanaiden154.github.io/quillgethtml/example.html
  - allows you to pull HTML out of the editor for rendering elsewhere
  - It takes the delta format that quill provides natively and transforms it into HTML that can be used just about anywhere.

- https://github.com/andrewanthro/quill-to-pdf /202102/ts
  - Create a PDF from a QuillJS delta object
  - Convert a QuillJS delta object into a `.pdf` BLOB
  - https://github.com/thebadge/quill-to-pdf /202307/ts
- https://github.com/andrewanthro/quill-to-word /202101/ts
  - Convert a QuillJS delta object into a `.docx` file

- https://github.com/TheProgramMaster/MSU-Provost-Office-PDF-Generator-Module /202404/js
  - PDF Generator Module using Quill WYSIWYG editor for Murray State University Provost Office

- https://github.com/gzzhanghao/quill2docx /201707/js
  - Convert Quill Delta to DocX

- https://github.com/cotype/core /paid/202302/ts
  - Cotype manages structured content that can accessed via APIs. 
  - The system itself is not concerned with the actual rendering of the data
  - THe content API is read-only. Modifying content is only possible via the management API that is used by the UI.

- https://github.com/jobsta/reportbro-designer /js
  - https://www.reportbro.com/demo/invoice
  - A javascript plugin to create PDF and XLSX report templates.
  - Everyone can design & edit document templates, and preview them directly in the browser
  - The reports can be generated with ReportBro Lib (a Python package) on the server.
  - 依赖quill.v1、jsbarcode、qrcode
  - https://github.com/jobsta/reportbro-lib

- https://github.com/12Ahn22/quill-multer /202205/js
  - react-quill, multer

- https://github.com/angelaki/quill-get-text /MIT/202311/js
  - Quill module to control how contents get serialized in Quill's getText()-method

- https://github.com/payz0/quill-base64-to-file-location /202104/js
  - Method untuk merubah base64 ke file upload dalam quill editor
# non-js
- https://github.com/plato-messaging/quill-delta /apache2/202312/java
  - A java implementation of QuillJS delta
- https://github.com/volser/android-quill-delta /201809/java/kotlin
  - A kotlin implementation of Delta format

- https://github.com/singerdmx/flutter-quill /2.2kStar/MIT/202311/dart
  - a rich text editor and a Quill component for Flutter.
  - editor built for the modern Android, iOS, web and desktop platforms

- https://github.com/visual-space/visual-editor /245Star/MIT/202402/dart
  - a Rich Text editor for Flutter originally forked from Flutter Quill.
  - The editor is built around the powerful Quilljs Delta document format originally developed by QuillJs
# more
- https://github.com/amamov/smart-editor-dev-playground /202107/ts/inactive
  - realtime collabo editor and rich editor - quill, draft-js, toast-ui
  - nextjs, socket.io, mongoDB

- https://github.com/jamiekieranmartin/quiller /202205/ts/inactive
  - https://quiller.vercel.app/
  - Offline personal note-taking simplified.
  - All notes are stored locally on the device. All pages are static files, there simply is no backend.
  - 依赖next、react-hook-form

- https://github.com/rwth-acis/syncmeta /202311/js
  - Near real-time collaborative modeling framework
