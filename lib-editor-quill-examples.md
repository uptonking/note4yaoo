---
title: lib-editor-quill-examples
tags: [examples, quill, text-editor]
created: 2023-02-09T18:31:53.078Z
modified: 2023-02-09T18:32:06.240Z
---

# lib-editor-quill-examples

# guide

- resources
  - https://github.com/quilljs/awesome-quill
# popular
- quill /37.5kStar/BSD/202311/ts
  - https://github.com/quilljs/quill
  - https://quilljs.com/
  - https://quilljs.com/playground/
  - a modern WYSIWYG editor built for compatibility and extensibility
  - forks
  - https://github.com/reedsy/quill /202308/ts
    - We need to use our own forked version of the Delta class, which adds support for complex attributes (which we need for tracked changes).
    - 依赖@reedsy/quill-delta、eventemitter3、parchment、rfdc
    - https://github.com/reedsy/delta
    - https://github.com/reedsy/parchment
  - https://github.com/reedsy/rich-text
    - Rich Text uses quill-delta on the back end.

- typewriter /347Star/MIT/202311/ts
  - https://github.com/typewriter-editor/typewriter
  - A rich text editor based off of Quill.js and Ultradom, and using Svelte for UI.
  - 依赖 svelte、popperjs2、typewriter/delta
  - Built on the same data model as Quill.js, the Delta format, and using a tiny virtual DOM, Superfine, Typewriter aims to make custom rich text editors faster, easier, and more powerful

- https://github.com/ludejun/quill-react-commercial /202311/ts/js
  - https://ludejun.github.io/quill-react-commercial/
  - 多功能的、可面向商业化的quill富文本编辑器
  - Use the latest quill@2.0.0-dev.4. Implement using React Hooks

- https://github.com/shenmaxg/quill-imitate-shimo /202110/ts
  - 基于 quill 的富文本编辑器

- https://github.com/hubertnare/strapi4-wysiwyg-replacement /202202/js
  - change the default WYSIWYG to Quill Editor
  - [How to change the default WYSIWYG in Strapi v4 to Quill Editor_202203](https://strapi.io/blog/how-to-change-the-default-wysiwy-to-quill-editor)

- https://github.com/zenoamaro/react-quill /202208/ts/单文件
  - A Quill component for React.

- https://github.com/gtgalone/react-quilljs /202209/ts/单文件
  - React Hook Wrapper for Quill, powerful rich text editor.

- https://github.com/sciencenawaaz/Text-Editor /202309/js
  - https://text-editor-roan.vercel.app/
  - text editor using react-quill

- https://github.com/lovelysystems/lovely-editor /202210/js
  - react component which lets you use multiple editors (e.g Quill) for a single document.
  - Each editor will create an isolated HTML markup of its part.
  - https://github.com/ha3158987/react-quill-editor-example /202306/js
  - https://github.com/maxfahl/Quill-Edit-Multiple

- https://github.com/tangien/quilljs-textarea /202202/js
  - https://tangien.github.io/quilljs-textarea/
  - A simple extended helper for quilljs to transform textarea into text editor
  - Works on both textarea and divs
  - Auto-initialize quilljs using data-quilljs selector

- https://stackblitz.com/edit/quill-editor-demo
  - [Render React Component inside Quill without losing context_202004](https://culture.kissflow.com/render-react-component-inside-quill-without-losing-context-151eac4eda08)

- https://github.com/mild-blue/quill-even-better-table /202306/js
  - https://codepen.io/soccerloway/pen/WWJowj
  - A module for better table in Quill, more useful features are supported
- https://github.com/seehar/quill-better-table-plus /202308/js
  - fork by quill-better-table
- https://github.com/soccerloway/quill-better-table /202007/js
  - https://codepen.io/soccerloway/pen/WWJowj
  - Module for better table in Quill, more useful features are supported.
  - quilljs v2.0.0-dev.3
  - 支持 Merge/Unmerge table cells
  - Selects multiple table cells
  - codepen可以直接查看delta内容
  - table通过给\n添加attributes控制单元格内容

- https://github.com/volser/quill-table-ui /202007/ts
  - https://codepen.io/volser/pen/QWWpOpr
  - A module for table UI in Quill
  - quilljs v2.0.0-dev.3
  - 功能太少

- https://github.com/dost/quilljs-table /201703/js
  - Test lab for creating TABLE functionality in QuillJS using Containers.
- https://github.com/unzld/quill-better-table-picker /202110/js
  - An extension of the table module for Quill, with support for toolbar table picker.

- https://github.com/tanvirraj/quill-notion-table-editor /202208/js
  - https://tanvirraj.github.io/quill-notion-table-editor/
  - a notion like menu and table editor based on quilljs
  - table功能简单，通过类似/菜单添加
  - table的delta通过给\n添加attributes为row来区分行
  - https://github.com/uragirii/Notion-Clone /202012/js
- https://github.com/tzhangchi/quill-menu-module /202201/ts
  - Notion-like style quill menu module based on Quill.js

- https://github.com/imtiaz101325/quill-fold-example /202008/ts
  - feature of collapsable bullet points

- https://github.com/Kibo/filemanager-js /202201/ts/vue
  - The JavaScript filemanager for CKEditor, Quill, TinyMCE.

- https://github.com/BrenoFariasdaSilva/TextSync /202309/js/仅同步未处理冲突
  - A Real-Time Distributed-Text-Editor Application with ReactJS, NodeJS, MongoDB and WebSockets.
  - 依赖react、quill、socket.io、mongoose

- https://github.com/isaacsokari/simple-docs /202104/ts
  - Lightweight Google Docs clone made using Quill editor, Socket.io, and MongoDB.

- https://github.com/LittleWhitechun/chouxiang-converter /202208/ts
  - React16 hooks + css in js + Quill + ts *抽象话翻译器，可以把中文翻译成emoji，支持单字替换，文字位置对应跳转，一件翻译等

- https://github.com/jamiekieranmartin/quiller /202205/ts
  - https://quiller.vercel.app/
  - Offline personal note-taking simplified.
  - All notes are stored locally on the device. All pages are static files, there simply is no backend.

- https://github.com/joeldarl/quill-cms /202101/ts/pug
  - A publishing CMS developed using NodeJS, TypeScript and MongoDB. 
  - 不依赖quilljs，编辑器使用SimpleMDE

- https://github.com/amamov/smart-editor-dev-playground /202107/ts
  - realtime collabo editor and rich editor demo - quill, draft-js, toast-ui
# quill-based-editors
- https://github.com/imnapo/react-native-cn-quill /202306/ts
  - a rich-text editor for react-native. 
  - We've created this library on top of Quill Api.
- https://github.com/LuudJanssen/react-native-webview-quill /201912/ts
  - Quill component for React Native built using `postMessage` communication and a WebView.

- https://github.com/brsloan/warewoolf /202306/js
  - A minimalist novel-writing system/rich text editor designed to be usable without a mouse.
  - All-keyboard navigation designed for pleasant use without a mouse
  - 依赖quill.v1、docx、@electron/remote

- https://github.com/innovatorved/Markdown-Editor /202212/ts
  - https://markdown-editor-six-mu.vercel.app/
  - A simple Nextjs , Quill based markdown Editor

- https://github.com/ChrisMayor/D365RichTextEditor /202012/ts
  - Dynamics 365 Rich text editor for Unified Interface / Based on PowerApps component framework, React and quill

- https://github.com/TonyYu2015/GEditor /202309/js
  - https://g-editor-fawn.vercel.app/
  - rich-text base on Quill

- https://github.com/NodeBB/nodebb-plugin-composer-quill /202311/js
  - WYSIWYG composer for NodeBB based off of Quill
  - This composer saves its data in a unique format that is only compatible with Quill. If you switch to Quill, any posts made with Quill cannot be migrated back to Markdow

- https://github.com/Wikia/post-editor /202203/js
  - Quill-based editor for posts and replies, currently used in Discussions
  - Preact as a renderer
  - wds-components/_drowdowns

- https://github.com/domilin/media-quill /202011/ts
  - Rich text editor based on Quill
  - Built in vanilla JS, typescript support, so it can be used on React, Vue, Angular as well
# plugins/modules
- https://github.com/quill-mention/quill-mention /635Star/MIT/202311/js
  - https://quill-mention.com/
  - a module to provide @mentions or #hashtag functionality for the Quill rich text editor.

- https://github.com/raphaelM-sudo/quill-emoji-mart-picker /202006/ts
  - https://quill-emoji-mart-picker.netlify.com/
  - Module and Blot for Quill.js that supports Emoji Mart Picker and Emoji Mart.
  - converts unicode emojis, emoticons and emoji names into emoji images from Apple, Google, Twitter, EmojiOne, Facebook Messenger or Facebook.

- https://github.com/contentco/quill-emoji /202111/js
  - Module extension for Quill.js that handles emojis in the toolbar.
  - you can add emojis through the toolbar at the top, or by typing the emoji code.

- https://github.com/yslyong/React-Quill-Improved-Listing /202303/ts
  - contain two fixes for React Quill Listing to make it have a similar feeling with .docx listing
- https://github.com/koffeinfrei/quill-task-list /201806/js
  - Adds a task/todo list to the quill editor. Includes a toolbar item.
  - Behaves as the built-in bullet list.

- https://github.com/contentco/quill-inline-comment /201710/js
  - Module that handles inline comment like medium

- https://github.com/zaffnet/quill_spellcheck_demo /202101/js
  - https://zaffnet.github.io/quill_spellcheck_demo/
  - Spellcheck in a WYSIWYG Editor. I have modified the Tooltip provided by Quill to suggest words.

- https://github.com/cloverhearts/quilljs-markdown /202207/js
  - https://cloverhearts.github.io/quilljs-markdown
  - support markdown. 书写时会自动转换成md样式
  - https://github.com/doc22940/quill.markdown
- https://github.com/patleeman/quill-markdown-shortcuts /201910/js
  - module that converts markdown to rich text formatting while typing.

- https://github.com/lukevp/quill-fire /202305/ts
  - Extend Quill JS editor to fire events as soon as matching text is entered
- https://github.com/mindroute/quill-autoformat /201903/js
  - Module for formatting and transforming text as you type in Quill
  - Using RegExp to find and trigger transformations for text such as links, mentions, hashtags or emojis. 
  - Requires Quill 2.0

- https://github.com/T-vK/DynamicQuillTools /201911/js
  - allows you to dynamically add or remove new custom elements to/from a Quill Editor's toolbar

- https://github.com/machengqi/quill-clipboard-plugin /202207/ts
  - module plugin for clipboard pasted files, it can help you filter clipboard file size and mimetypes, and provides a hook to help you substituted error files

- https://github.com/MuhammedAlkhudiry/quill-find-replace-module /201909/js
  - https://codepen.io/muhammedalkhudiry/pen/VoMxeK
  - A module for Quill rich text editor to allow searching/finding words and replacing them.
- https://github.com/Lmangoxx/quill-find-replace-module /202201/ts
  - quill富文本编辑器”搜索查找“扩展模块

- https://github.com/gocodebox/lifterlms/tree/trunk/packages/quill-wordcount-module /202208/js
  - Word count module for Quill.
  - Uses words-count to perform word counting in multiple languages and character sets.

- https://github.com/rain0002009/quill-position-placeholder /201907/ts
  - 一个Quill.js的插件，用来添加一个使用百分比高度的占位元素。
- https://github.com/jspaine/quill-placeholder-module /201807/ts
  - https://codepen.io/jspaine/pen/MozyNp
  - Quill module for adding placeholders
- https://github.com/Datananas/quill-placeholder-autocomplete /201809/js
  - brings autocomplete to quill-placeholder-module

- https://github.com/jmquigley/quill-markup /201912/ts
  - A markup highlighting module for the Quill text editor

- https://github.com/visualjerk/quill-magic-url /202208/ts
  - Automatically convert URLs to links in Quill
- https://github.com/juyeong1260/quill-auto-detect-url /202105/ts
  - transform the url of the url as the user types.
  - based on quill-magic-url
- https://github.com/kyoncy/quill-linkify /202209/ts
  - plugin that converts URL, mail address, phone number to link.

- https://github.com/rain0002009/quill-divider /202207/ts
  - Module extension for Quill.js that handles divider in the toolbar.

- https://github.com/mindroute/quill-form /201809/js
  - Module for form bindings and input fields in Quill
  - Automatically creates hidden input fields for a form and adds submit handling and submit by key (⌘/Ctrl+S). 
  - It creates fields for text, html and delta.

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

- https://github.com/nvt-ak/quill-upload /202301/js
  - A plugin for uploading image, video, attachment in Quill 
  - upload a image, video, attachment when it is inserted, and then replace the base64-url with a http-url
  - preview the image, video, attachment which is uploading with a loading animation

- https://github.com/lw1995/quill-video-image-module /202008/js
  - 整合视频上传，图片上传到服务器模块，用video标签替换iframe，中文提示框，中文描述

- https://github.com/xeger/quill-image /202310/ts
  - provide resizable, floatable images that cleanly "round trip" between HTML and JSON.
  - a fork and rewrite of quill-blot-formatter
  - https://github.com/UMN-LATIS/quill-better-image-module
- https://github.com/portive/quill-images /202311/ts
  - https://codepen.io/scottward/pen/RwvjOVJ
  - Add image uploads with click to upload, drag and drop and paste support.

- https://github.com/chenjuneking/quill-image-drop-and-paste /202304/ts
  - module for drop and paste image, with a callback hook before insert image into the editor
  - 提供了多个框架的demo
- https://github.com/x-cold/quill2-image-drop-and-paste /202112/ts
  - https://x-cold.github.io/quill2-image-drop-and-paste/
  - module for drop and paste image, with a callback hook before insert image into the editor

- https://github.com/Nelwhix/quill-image-uploader /202303/ts
  - plugin that uploads images inserted, drag/dropped or pasted into the quill editor to a server instead of being base64 encoded.

- https://github.com/NoelOConnell/quill-image-uploader /202305/js
  - allow images to be uploaded to a server instead of being base64 encoded
  - Adds a button to the toolbar for users to click, also handles drag, dropped and pasted images
  - https://github.com/fxmontigny/quill-image-upload /201812/js
  - https://github.com/dragonwong/quill-plugin-image-upload /201811/js

- https://github.com/kensnyder/quill-image-drop-module /201703/js
  - A module for Quill rich text editor to allow images to be pasted and drag/dropped into the editor.

- https://github.com/benwinding/quill-image-compress /202307/ts
  - https://benwinding.github.io/quill-image-compress/src/demo.html
  - compresses images that are uploaded to the editor

- https://github.com/phamquyetthang/react-quill-image-upload /202307/ts
  - Image upload in quill editer, React-quill + cloudinary
  - https://github.com/krishnawaghmode/reactjs-quilljs-image-upload-server

- https://github.com/EthanYan6/quill-image-super-solution-module /202103/js
  - vue-quill-editor 的专用插件，为其提供了自定义上传图片到服务器、粘贴图片上传至服务器、拖拽图片上传至服务器的功能

- https://github.com/scrapooo/quill-resize-module /202209/ts
  - A module for Quill rich text editor to allow images to be resized.
  - https://github.com/arnauddrain/quill-media-resize /ts
- https://github.com/hunghg255/quill-resize-image /202308/ts
  - https://quill-resize-image.vercel.app/
  - A plugin resize image for Quilljs

- https://github.com/kensnyder/quill-image-resize-module /201807/js
  - A module for Quill rich text editor to allow images to be resized.

- https://github.com/mudoo/quill-resize-module /202003/js
  - allow images/iframe/video and custom elements(convert to placeholder) to be resized.
  - original forked from https://github.com/whatcould/quill-image-resize-module.

- https://github.com/Fandom-OSS/quill-blot-formatter /201803/js
  - A module for Quill that allows editor elements to be resized, repositioned, etc
  - module to format document blots. Heavily inspired by quill-image-resize-module.
  - supports resizing and realigning images and iframe videos, but can be easily extended using BlotSpec and Action.

- https://github.com/simialbi/quill-smart-break /202004/js
  - Support shift + enter in Quill WYSIWYG editor

- https://github.com/mathquill/mathquill /2.5kStar/MPLv2/202201/ts
  - http://mathquill.com/
  - a web formula editor designed to make typing math easy and beautiful.

- https://github.com/c-w/mathquill4quill /202311/js
  - https://justamouse.com/mathquill4quill
  - adds support for rich math authoring to the Quill editor.
  - depends on MathQuill, Quill and KaTeX

- https://github.com/vieyama/quill-editor-math /202304/ts
  - Rich text editor with react quill, mathquill4quill, katex, and image resizer. you can use formula with this.

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
# examples
- https://github.com/jotform/dnd-builder /43Star/MIT/202305/js
  - https://www.jotform.com/open-source/dnd-builder/
  - accessible drag and drop page builder with React
  - 依赖use-gesture、fuse.js、react-dnd-cjs、react-quill、recharts
  - 示例友好

- https://github.com/jado66/reactive-site-creator /202303/js
  - https://jado66.github.io/reactive-site-creator-live/
  - A website creator for React.
  - 依赖dnd-kit、react-quill、react-reveal、bootstrap5

- https://github.com/folkloreinc/panneau-js/tree/v0.8
  - https://folkloreinc.github.io/panneau-js/storybook/index.html
  - React components to build forms and administration panels
  - 依赖ckeditor5-react、react-quill，实现了可切换的版本
  - /v0.8/fields/html/package.json

- https://github.com/luanpanno/google-docs-clone /202105/ts
  - Google Docs Clone with Node, React, Socket.io and Quill
  - https://github.com/seifeldeen92/google-docs-texteditor-clone
  - https://github.com/Chondan/google-doc-clone

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

- https://www.npmjs.com/package/@nocobase/client
  - 依赖react-quill.v1

- ddd-forum /1.8kStar/ISC/202306/ts/hacker-news
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
  - save notes made with the Quill.js text editor to a MongoDB database. 

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
# collab-ot
- https://github.com/WindrunnerMax/Collab
  - 初探富文本之OT协同实例 sharedb+quill
  - 初探富文本之CRDT协同实例 yjs+quill

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
  - 团队协作与管理平台，具有在线多人聊天、消息实时推送、协同编辑等功能
  - 前端使用 NextJS 12.2.0，后端使用 NestJS 8.0
  - 后台管理界面使用 Ant Design Pro
  - 支持多人协作文档（使用 Quill 富文本编辑器）
# collab-crdt
- https://github.com/jaredly/local-first/tree/master/packages/text-crdt
  - This algorithm is largely based on RGA, with support for rich-text formatting added, along with a number of optimizations.
  - integrate with Quill.
  - Your approach seems to resemble RGASplit which I believe is bases for

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

- https://github.com/yjs/y-quill /202205/js
  - https://demos.yjs.dev/quill/quill.html
  - This binding maps a Y. Text to a Quill instance. 
  - It optionally supports shared cursors via the quill-cursors module.
- https://github.com/sameer1612/quilly /202205/ts
  - Collaborative editing using Quill.js and Y.js

- https://github.com/ethanryan/textedit-app /201807/js
  - Collaborative text editing app, built with React, Express, Quill, and Yjs.

- https://github.com/peer-base/peer-pad /201907/js
  - Online editor providing collaborative editing in really real-time using CRDTs and IPFS.
  - 依赖codemirror5、quill.v1、remark.v10

- https://github.com/widmogrod/js-crdt /ts/201711
  - explore applications of data structure called CRDT in context of real time collaboration 
  - https://github.com/widmogrod/notepad-app
    - Collaborative notepad app (demo).
    - 依赖quill

- https://github.com/mweidner037/firebase-text-editor
  - Collaborative plain text editor using CRDTs on top of Firebase (Realtime Database).
  - 依赖position-strings，不依赖quill
  - https://github.com/mweidner037/firebase-rich-text-editor
    - 依赖quill.v1
# delta
- https://github.com/joelcolucci/node-quill-converter /202001/js
  - Convert HTML to a Quill Delta or a Quill Delta to HTML

- https://github.com/nozer/quill-delta-to-html /202204/ts
  - Converts Quill's delta ops to HTML

- https://github.com/xeger/quill-deltacvt /202306/ts
  - Converts Quill Delta to HTML (or other formats) without depending on quill, parchment or quill-delta

- https://github.com/mastito03/render-quill /201704/js
  - render quill delta to html string on server

- https://github.com/UmbraEngineering/quilljs-renderer /201503/js
  - Renders an insert-only Quilljs delta into various format like HTML and Markdown
- https://github.com/casetext/quill-render /201510/js
  - Renders a sequence of quill insert-only deltas (operational transforms) into HTML with no browser dependencies.
  - using cheerio to build a DOM from the delta sequence.

- https://github.com/frysztak/markdown-to-quill-delta /202205/ts
  - Converts Markdown to Quill Delta using remark.
- https://github.com/volser/md-to-quill-delta /201911/ts
  - `import { MarkdownToQuill } from 'md-to-quill-delta';`

- https://github.com/forgeworks/quill-delta-python /202010/python/js
  - Python port of the Quill-JS Delta library - Has support for HTML Rendering
# utils
- https://github.com/andrewanthro/quilljs-parser /202101/ts
  - Parse a QuillJS delta
  - Transform your QuillJS contents into an easier-to-use paragraph format

- https://github.com/boomanaiden154/quillgethtml /202311/js
  - allows you to pull HTML out of the editor for rendering elsewhere
  - It takes the delta format that quill provides natively and transforms it into HTML that can be used just about anywhere.

- https://github.com/andrewanthro/quill-to-pdf /202102/ts
  - Create a PDF from a QuillJS delta object
  - Convert a QuillJS delta object into a `.pdf` BLOB
- https://github.com/andrewanthro/quill-to-word /202101/ts
  - Convert a QuillJS delta object into a `.docx` file

- https://github.com/gzzhanghao/quill2docx /201707/js
  - Convert Quill Delta to DocX

- https://github.com/jobsta/reportbro-designer /js
  - https://www.reportbro.com/demo/invoice
  - A javascript plugin to create PDF and XLSX report templates.
  - Everyone can design & edit document templates, and preview them directly in the browser
  - The reports can be generated with ReportBro Lib (a Python package) on the server.
  - 依赖quill.v1、jsbarcode、qrcode
  - https://github.com/jobsta/reportbro-lib

- https://github.com/12Ahn22/quill-multer /202205/js
  - react-quill, multer

- https://github.com/payz0/quill-base64-to-file-location /202104/js
  - Method untuk merubah base64 ke file upload dalam quill editor
# non-js
- https://github.com/volser/android-quill-delta /201809/java/kotlin
  - A kotlin implementation of Delta format

- https://github.com/singerdmx/flutter-quill /2.2kStar/MIT/202311/dart
  - a rich text editor and a Quill component for Flutter.
  - editor built for the modern Android, iOS, web and desktop platforms

- https://github.com/visual-space/visual-editor /245Star/MIT/202311/dart
  - a Rich Text editor for Flutter originally forked from Flutter Quill.
  - The editor is built around the powerful Quilljs Delta document format originally developed by QuillJs
# more
