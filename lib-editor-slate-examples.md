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
  - [slate discussion: Add Collaboration Example and Documentation](https://github.com/ianstormtaylor/slate/issues/3715)
  - [Collaborative editing](https://github.com/ianstormtaylor/slate/issues/259)

- more-slate
  - 建站编辑器应该参考gutenberg、wix
  - search: mern + slate

- slate-fans
  - https://github.com/williamstein
# popular
- plate /1.6kStar/MIT/202208/ts/block-style
  - https://github.com/udecode/plate
  - https://plate.udecode.io/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但list内所有item不支持拖拽
  - core依赖jotai、react-hotkeys-hook
  - code-block自研实现，不依赖第三方代码编辑器
  - A plugin framework for building rich text editors with slate.
  - [Plate 17: Replace zustand by jotai_202209](https://github.com/udecode/plate/pull/1871)
    - 已从代码中移除zustand，zustood相关代码只有一处
    - jotai.v1
  - dev-xp
    - 表格方向键存在跳跃感，但总体正常
  - https://github.com/udecode/plate-template /202310/ts
    - https://template.platejs.org/
    - minimal template for building rich-text editors with Plate and Next.js 13

- https://github.com/discord/slate-react-package-fork /202311/ts
  - React-specific logic for Slate
  - 提供了android-input-manager

- editablejs /17Star/apache2/202208/ts/自绘光标/模型层block
  - https://github.com/editablejs/editable
  - https://github.com/editablejs/editable/blob/main/README.zh-CN.md
  - https://docs.editablejs.com/playground
  - 依赖slate、zustand
  - 只依赖slate不依赖slate-react，但实现是类似的，react组件逻辑并不多
  - 基于yjs实现协作
  - 一个可扩展的富文本编辑器框架，专注于稳定性、可控性和性能
    - 为此，我们没有使用原生的可编辑属性contenteditable，而是使用了一个自定义的渲染器
    - canvas的开发体验不佳，需要编写更多代码
  - 完全自绘和自定义选区，浏览器的selection始终是caret
  - 不再依赖 contenteditable 属性，使用slatejs数据模型，借助 react 使用自绘光标的模式渲染
  - dev-xp
    - 表格方向键异常
  - [修改license为GPL_20220204](https://github.com/editablejs/editable/commits/main?after=d61da6caa411139cddb0ae0e8eeeeaee05893610+69&branch=main&qualified_name=refs%2Fheads%2Fmain)
  - unicode-trie主要对一些 unicode 字符进行索引的计算。因为有些字符占位所占的字节数不确定，造成某些字符拆分后的索引不准确

- wangEditor.v5 /14.3kStar/MIT/202212/ts/vanillajs/inactive
  - https://github.com/wangeditor-team/wangEditor
  - https://www.wangeditor.com/
  - https://www.wangeditor.com/demo/index.html
  - core依赖slate、snabbdom、dom7、is-hotkey、lodash、uppy(file uploader)、event-emitter、i18next
  - 源码是函数式风格
  - 开箱即用，配置简单。
  - 视图层框架无关，支持 JS Vue React，可参考taleweaver
  - L1级编辑器，弃用了 document.execCommand，使用 slate.js（但不依赖 React）为内核
  - 使用vdom（基于 snabbdom.js）做视图更新，model 和 view 分离，增加稳定性
  - 扩展性
    - 使用扩展插件和模块的机制，保证扩展性
    - 现在wangEditor内置的各个功能，也都是通过扩展插件和模块的形式搭建起来的
  - dev-xp
    - 表格方向键未实现
  - https://github.com/wangfupeng1988/slate-dom-view /202105/ts
    - 💡 slate.js for DOM, without React.
  - [有计划整合slate-yjs插件吗？ _202204](https://github.com/wangeditor-team/wangEditor/issues/4033)
    - 暂时没有开发多人协同功能的计划。多人协同是一个非常复杂的工程，不是集成一个插件就可以解决的，还需要服务端做很多配合。

- rich-block-editor /2Star/ISC/202306/ts
  - https://github.com/rgbui/rich
  - https://shy.live/
  - 诗云富文本编辑器
  - 依赖wangeditor、codemirror6、katex、marked、remark-gfm、mobx-react、prismjs、react-loadable、react-markdown
  - https://github.com/rgbui/shy
    - 诗云应用程序，包括web、mobile
    - 依赖dexie、mobx、ethers(Ethereum library and wallet implementation)
  - https://github.com/rgbui/api
    - 诗云api

- prezly-slate /31Star/MIT/202208/ts/提交多
  - https://github.com/prezly/slate 
  - 依赖`plate`的工具方法而不依赖编辑器、popperjs2、@prezly/sdk、react-bootstrap
  - Prezly software built upon Slate
  - 悬浮工具条使用卡片的形式
  - dev-xp
    - 表格支持方向键
    - 单元格内容有时不会自动换行，只显示一行
    - 表格不支持单元格选区
    - 代码层支持合并单元格，没有示例
  - https://www.prezly.com/
    - Successful businesses need a fanbase. Use Prezly to build yours.
    - With Prezly, you can publish and share your content with your audience, directly. No algorithms, no middlemen, no BS.

- tripdocs /52Star/MIT/202303/ts/feature多/直接fork源码修改
  - https://github.com/ctripcorp/tripdocs
  - https://ctripcorp.github.io/tripdocs/
  - https://ctripcorp.github.io/tripdocs/apiDocs.html
  - TripDocsSDK是基于携程内部在线文档编辑器内核，提炼的一款通用的，现代的、稳定的、支持协同的、可用于生产环境的在线文档编辑器
  - 支持内容评论和底部评论，comment图标锚定在内容右侧水平对齐
  - 支持历史版本
  - 支持Markdown编辑和word解析
  - 支持toc、斜杠菜单
  - TripDocsSDK依赖slatejs、yjs、reactjs。并在slatejs基础上，进行了二次的开发
  - 通过在 `validation.worker.js` 中对 Slate 的 `value` 对象进行全量递归校验，对不满足的结构返回 `invalidNode` 的响应，并且全局使用 `Editor.normalize(editor, {force: true})` 对页面结构进行强制重刷。这样就能够保证即使使用了 `defaultValue` 直接渲染的数据，也能够被自动修复。
  - 直接在slate源码的基础上修改的，[源码修改记录](https://github.com/ctripcorp/tripdocs/blob/main/src/components/slate-packages/README.md)
  - faq
    - 如何协作，改哪个页面的socketUrl
    - webpack.native/prod.js 使用的是 indexDemo.html

- https://github.com/JokerLHF/mini-slate /202304/ts
  - 使用 ts 实现 slate 富文本

- https://github.com/Darginec05/Yopta-Editor /MIT/202310/ts
  - https://yopta-editor.vercel.app/basic
  - Notion-like editor with similar behaviour
  - 几乎无依赖
  - 支持跨block选择部分文字
  - list不支持多级
  - list item暂不支持拖出去
  - Offline ready mode, 离线基于localStorage
  - [plans for v2](https://yopage.co/blog/0zntIA46L4/5iK8VNiBI8)

- https://github.com/dsvgit/slatesbox /202203/ts
  - https://dsvgit.github.io/slatesbox/
  - Slate editor plugins system. 
  - Drag and drop, folding implementation.
  - 依赖dnd-kit、zustand，依赖plate的工具方法并不依赖编辑器
  - [Slate.js + dnd-kit = 🔥. Improving Rich Text Editor UX by adding Drag and Drop. - DEV Community](https://dev.to/devterminal/slatejs-dnd-kit-improving-rich-text-editor-ux-by-adding-drag-and-drop-23d3)
  - https://github.com/dsvgit/mide
    - https://dsvgit.github.io/mide/
    - Slate.js code editor extension

- https://github.com/WindrunnerMax/DocEditor /202311/ts
  - https://windrunnermax.github.io/DocEditor
  - 基于slate构建文档编辑器
  - 依赖 ahooks、arco-react
  - 效果类似飞书，不支持拖拽

- https://github.com/objectlegal/slate-snippets /js
  - Slate snippets
  - Convert data from v0.47 to v.0.50+
  - https://github.com/horacioh/slate-snippets /js

- https://github.com/juliankrispel/slate-patterns /202203/ts/slate.v0.61
  - Patterns for slate.js
  - 提供了示例 iframe、autocomplete
  - 依赖zustand
  - https://github.com/juliankrispel/slate-js-boilerplate

- https://github.com/techexpert0119/slate-app-mern /202308/ts
  - customizable framework for building rich text editors.

- https://github.com/jasonhoo95/slatejs /202311/js
  - 依赖slate、prosemirror、quill.v1

- https://github.com/mattiaz9/slate-jsx /202311/ts
  - A typesafe slate implementation for possibly any jsx framework
  - 测试了vue、solidjs

- react-editor-kit /22Star/MIT/202012/ts/inactive
  - https://github.com/mpkelly/react-editor-kit
  - https://mpkelly.github.io/react-editor-kit/
  - https://github.com/mpkelly/react-editor-kit-examples
  - Compose a React-based text editor using a suite of standard plugins
  - 依赖slate.v0.50+
  - https://github.com/mpkelly/journal
    - https://mpkelly.github.io/journal
    - Embeddable Wiki available as Chrome extension, PWA or React component.
    - 依赖slate二开、dexie3
    - 应用编辑器支持创建分栏，但底层react-editor-kit未直接提供
    - 示例体验友好、功能丰富

- https://github.com/TheGuardianWolf/treepack
  - Pack tree nodes into a flat object and unpack them again!
  - The original use case is to allow path based trees (such as the one used by Slate) to be stored in NoSQL based storage and be able to update them partially without sending the full tree.
  - v1 of changing the index of an object causes a lot of adding and deleting. This is a limitation of the path based scheme.
- https://github.com/paularmstrong/normalizr
  - Normalizr is a small, but powerful utility for taking JSON with a schema definition and returning nested entities with their IDs, gathered in dictionaries.
  - https://github.com/anseal/normalizr
    - The main point of difference from the original - performance
    - API is the same as in the original

- https://github.com/nivekithan/slate-devtools
  - devtool for slatejs which will assist you in debugging the code
  - 依赖slate.v0.59, jotai
  - [I created a devtool to assist in debugging](https://github.com/ianstormtaylor/slate/issues/4112)

- https://github.com/usunil0/slate-paged /202010/ts
  - https://slate-paged-demo.vercel.app/
  - 依赖slate.v0.59, nextjs, docx, theme-ui
  - 支持导出docx
  - A paged editor rather than a continuous block. built using slate js.
  - done: basic editor setup basic functionalities figure out the nodes length and paging
  - https://github.com/tobischw/slate-paged /201905/js/inactive
    - A buggy attempt at paginating the Slate editor

- quadrats /5Star/MIT/202311/ts
  - https://github.com/Quadrats/quadrats
  - https://quadrats.github.io/quadrats
  - A complete rich text editor. Currently based on Slate framework.
  - storybook示例非常丰富，但和artibox一样
  - 依赖 slate.v0.75.0
  - https://github.com/React-Artibox/artibox /202011/ts
    - https://react-artibox.github.io/artibox
    - A complete rich text editor based on Slate framework

- whim-notion-like /6Star/MIT/202108/ts
  - https://github.com/coniel/whim-editor
  - A highly customisable block based rich text editor inspired by Notion.
  - core依赖 slate.v0.65.3, fuse.js(fuzzy-search)
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
  - 代码量不大，思路清晰
- https://github.com/masnormen/noshon /202301/ts
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
  - 依赖zustand

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

- payloadcms /9.1kStar/MIT/202301/ts/slate
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

- https://github.com/seafileltd/seafile-editor /RepoNA
  - 项目是基于 react-slate 组件库的二次封装, 用于满足公司富文本编辑器的使用需求

- slate portive
  - https://github.com/portive/wysimark
    - Wysiwyg Editor for Markdown: 100% CommonMark + GFM with Uploads and Image Resizing
    - 依赖slate-react
  - https://github.com/thesunny/slate-experiments
    - 依赖slate.v0.63
  - https://slate-portive.docs.portive.com/
    - Plate Cloud is a partnership between Ziad Beyens and Portive to add cloud based Attachment and Image Uploading support with server-side image resizing to the Plate editor.
  - https://github.com/portive/slate-plugin
    - Upload Images and Attachments Plugin for Slate
    - Add beautiful and intuitive images and attachments to Slate with support for paste, drag and drop and `<input type="file">` uploads.

- https://github.com/react-page/react-page /8.3kStar/MIT/202304/ts/redux
  - https://react-page.github.io/
  - 依赖react-redux、redux-undo、mui.v5、react-dnd、uniforms
  - 使用redux作为状态管理
  - 提供了 @react-page/plugins-slate
  - 提供了集成react-admin的例子
  - react-page comes preconfigured with Slate as a ‘cellPlugin’ to be used as the rich text editor.

- edtr-io /696Star/MIT/202206/ts/page-editor
  - https://github.com/edtr-io/edtr-io
  - https://edtr.io/
  - a WYSIWYG in-line web editor written in React.
  - 支持拖拽block修改顺序
  - 不支持跨block选择部分文字
  - text-plugin依赖slate.v0.8
  - 依赖 prezly/slate-lists
  - 示例样式友好
  - 依赖redux、react-dnd
  - [Show HN: Edtr.io – Intuitive web editor, open source and fully adaptable | Hacker News_202002](https://news.ycombinator.com/item?id=22451568)

- onlyoffice-sdkjs /190Star/AGPLv3/202302/js
  - https://github.com/ONLYOFFICE/sdkjs
  - https://personal.onlyoffice.com/
  - https://api.onlyoffice.com/docbuilder/spreadsheetapi
  - 💡 word/excel/ppt都基于canvas实现
  - Contains API for all the included components client-side interaction.
  - sdk的设计可参考 notion-sdk-js
  - 通过TypedArray，将表格数据以二进制格式存储，通过字段压缩+共享字符串表来优化内存空间
  - [精读onlyoffice在线表格存储设计](https://juejin.cn/post/7202252704978386999)
  - repos
    - https://github.com/ONLYOFFICE/document-editor-react-samples
      - 示例依赖server api，本地无法运行
    - https://github.com/ONLYOFFICE/document-editor-react
      - 示例依赖server api，本地无法运行

- https://github.com/froala/wysiwyg-editor-node-sdk
  - Node. JS SDK to ease the integration of Froala WYSIWYG Editor on server side.

- https://github.com/payloadcms/payload/tree/main/packages/richtext-slate
  - Slate Rich Text Editor for Payload.

- oak /4Star/MIT/202208/js/提交多/page-builder
  - https://github.com/p3ol/oak
  - 整体上是一个可切换文本编辑器的页面编辑器
  - 页面从上到下由块构成，内容文字默认不可编辑，需要点击悬浮编辑按钮
  - Modern, lightweight & modulable page builder
  - @poool/oak-addon-richtext-field: WYSIWYG text field using Slate
  - @poool/oak-addon-richtext-field-prosemirror: WYSIWYG text field using ProseMirror

- https://github.com/hygraph/rich-text /MIT/201312/ts
  - A set of companion packages for Hygraph's Rich Text Field
  - rich-text-html-renderer: Framework agnostic Rich Text renderer.
  - rich-text-react-renderer: Out of the box Rich Text renderer for React; 
  - html-to-slate-ast: HTML to Slate AST converter for the Hygraph's RichTextAST format.
  - https://github.com/hygraph/gatsby-source-graphcms /202207/js/inactive
    - The official Gatsby source plugin for GraphCMS projects

- https://github.com/datocms/structured-text /202401/ts
  - Monorepo with Typescript libraries for handling and rendering DatoCMS Structured Text documents.
  - helpers to convert Structured Text dast to Slate structures.

- dmeditor /14Star/GPL/202306/ts
  - https://github.com/dmeditor/dmeditor
  - https://dmeditor.io/
  - https://demo.dmeditor.io/editor?d=demo
  - a block-based visual editor, written in React.
  - 不支持跨block选择部分文字
  - 可切换设备尺寸查看效果
  - 依赖mui、react-bootstrap、slate
  - https://github.com/dmeditor/dmeditor-sample

- https://github.com/uimix-editor/uimix /类似figma的设计工具
  - UIMix is a WYSIWYG editor for React components that offers a Figma or Framer-like experience for creating and maintaining React components.
  - 图形基于iframe里面的dom
  - ？ 是否依赖slate，deps有但代码无
# slate-based-editors
- https://github.com/raralabs/rara-rte /MIT/202311/ts
  - https://rte.raralabs.live/
  - A rich text editor built on top of slate.js
  - 依赖prismjs

- https://github.com/webkom/lego-editor /ts
  - A React rich text editor written in TS with Slate.js for lego-webapp
  - 代码量少，适合入门，支持上传图片

- boatproject-editor /1Star/MIT/202208/ts/plate/提交多/inactive
  - https://github.com/boatproject/editor
  - 依赖 plate、slate、styled-components
  - Rich text editor component for React. Built with Plate and MUI

- https://github.com/sodenn/react-fluent-edit /202306/ts
  - https://react-fluent-edit.vercel.app/
  - Brings easy-to-use mentions, markdown and DnD (WIP) features to Slate.
  - 非典型编辑器，更偏向输入框

- https://github.com/accordproject/web-components/tree/master/packages/ui-markdown-editor
  - https://ap-web-components.netlify.app/
  - a WYSIWYG editor for markdown that conforms to the CommonMark specification
  - 依赖markdown-it、slate、semantic-ui-react

- https://github.com/bipboy/rich-slate-editor /202305/ts
  - A small react implementation of a text editor based on Slate and Baseweb(css-in-js)


- https://github.com/ncqwer/lla-editor /202403/ts
  - 本项目使用 Slate 作为基础。旨在打造 React 友好的富文本编辑器

- https://github.com/pietrop/slate-transcript-editor /202110/js
  - https://pietrop.github.io/slate-transcript-editor
  - A React component to make correcting automated transcriptions of audio and video easier and faster. 
  - 适合视频播放器
  - 依赖slate.v0.59、mui.v4、docx、smpte-timecode
  - Building on the success and lessons learned from @bbc/react-transcript-editor. Mostly to be used in the context of autoEdit 3(digital paper edit)

- https://github.com/mbehr1/json-editor
  - slate.js based json editor to embed into webpages

- https://github.com/dictyBase/dicty-components-page-editor /202107/ts/inactive
  - https://dictybase.github.io/dicty-components-page-editor/
  - Reusable page editor built using Slate

- dslate /6Star/MIT/202207/ts/antd
  - https://github.com/rojer95/dslate
  - https://rojer95.github.io/dslate/
  - https://rojer95.github.io/dslate/#/docs/getting-started
  - 基于 Slate 构建的 Ant Design | Semi Design 风格的富文本编辑器。你可以通过插件的方式轻松自定义节点、工具等元素。
  - core依赖slate-react

- https://github.com/qirong77/SlatePad
  - 所见即所得的文本编辑器

- https://github.com/ls19930101/slate_editor
  - slate框架开发的富文本工具, 核心为contenteditable
  - 支持超大文档 word、excel 列表复制粘贴, 进行了一些性能优化处理; 
  - 依赖slate.v0.59, antd.v3

- https://github.com/xeajs/slate-react-editor
  - 基于 slatejs 的高度可定制的富文本编辑器

- slatejsx /48Star/Apache2/202203/js/antd
  - https://github.com/slatejsx/slatejsx
  - http://seditor.open.heyphp.com/
  - 项目基于slate.js框架开发，项目内所有图标，组件使用antd

- https://github.com/slatable/slate /202006
  - 基于 slatejs 封装富文本编辑器

- https://github.com/casperiv0/full-slate-editor-example /202308/ts
  - http://full-slate-editor-example.vercel.app/
  - A full Slate editor example with many features such as text formatting, block formatting (quotes, headers, lists) and text alignment

- https://github.com/alexichepura/slate-html-mui /202007/ts
  - WYSIWYG editor based on React, TypeScript, Slate >=0.57 and Material-UI.
  - https://github.com/alexichepura/slate-pen /202006/ts
    - Custom plugin engine for Slate editors framework. Written in TypeScript.
- https://github.com/nareshbhatia/react-force/tree/master/packages/slate-editor /202104/ts/inactive
  - https://nareshbhatia.github.io/react-force/
  - 依赖slate.v0.58、formik、material-ui.v4

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

- https://github.com/tiddly-gittly/slate-write /32Star/MIT/202310/ts
  - https://tiddly-gittly.github.io/slate-write/
  - WYSIWYG editor for TiddlyWiki. (WIP)
  - 一个用于 太微TiddlyWiki 的所见即所得编辑器
  - [Demo of a new WYSIWYG editor: slate-write (unstable alpha stage) - Plugins - Talk TW_202203](https://talk.tiddlywiki.org/t/demo-of-a-new-wysiwyg-editor-slate-write-unstable-alpha-stage/2788)
    - It is based on tw-react plugin, and use the powerful SlateJS editor and tons of keyboard shortcut plugins from udecode/plate
    - And I write some transformers to convert wikitext from/to SlateJS state JSON on saving, every 1s.

- https://github.com/ahmedosama7450/rich-slate
  - Opinionated rich text editor on top of slate (Under development)

- https://github.com/getweek/week-editor
  - Allows to reorder blocks.

- volto-slate /23Star/MIT/202203/js/依赖后端
  - https://github.com/eea/volto-slate
  - https://6.demo.plone.org/
  - An alternative text editor for Volto, capable of completely replacing the default richtext editor
  - Some of the main reasons that drove us to create volto-slate instead of enhancing Volto's draftjs implementation
  - 样式陈旧，编辑器和业务代码有联系
  - https://github.com/plone/volto
    - React-based frontend for the Plone Content Management System
    - plone后端依赖python
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
  - [Provide a (real) self hosted version](https://github.com/sanity-io/sanity/issues/3258)
    - Sanity Studio is only the editor interface, though. Sanity's hosted content backend, the Sanity Content Lake, on the other hand, is not open-source.

- https://github.com/contentful/field-editors/tree/master/packages/rich-text
  - https://contentful-field-editors.netlify.app/rich-text
  - This package contains a React RichTextEditor component that is used as default for RichText field type in the Contentful web application.
  - Since these are developed using the App SDK, this will allow you to understand how each editor works, fork existing apps or create your own apps based on existing Contentful components' source rather than starting from scratch.

- https://github.com/Yan-Boogie/highlighter
  - A complete rich text editor based on Slate framework with extended 'Highlighting' functionality.

- https://github.com/sympto-health/slate-rte /202310/ts
  - Pre-built rich text editor for Slate in React.
  - 基于ts，但所有源码都放在src文件夹，看起来较乱
  - https://github.com/sympto-health/slate-rte-demo  /js

- https://github.com/lingjieee/fantasy-editor /202006/ts/slate.v0.58
  - https://fantasy-editor.jieee.dev/
  - A React Rich Text Editor Based On Slate

- https://github.com/gwwyn/react-editor
  - https://gwwyn.github.io/react-editor/
  - Rich-text editor build with React and Slate
  - 支持 add column，但看起来乱

- https://github.com/rs-pro/rocket-slate /202008/inactive
  - A rich text editor based on SlateJS framework and slate-plugin-next
  - Supports slate 0.57 only

- https://github.com/farbenmeer/editor /202310/ts
  - farbenmeer's custom rich text editor based on slate

- https://github.com/quillforms/quillforms /php/ts/slate-react
  - https://www.quillforms.com/
  - Open Source TypeForm Alternative Based on React JS and Typescript | Best Typeform Clone

- https://github.com/kledk/react-chief-editor
  - https://kledk.github.io/react-chief-editor/
  - A rich-text editor for React, built ontop of Slate.js with an hooks-based addon architecture.

- https://github.com/eniolajayi/easy-writer /202108/js/inactive
  - A document editor built with React and Slate.js. with multi-edit feature

- https://github.com/uptoo/slate-editor /202308/js
  - 只依赖slate-react

- https://github.com/marsprince/slate-vue /202104/ts
  - slate.js implement for Vue2 and Vue3
  - Most of the slate-react's components can be easily migrated by no code change.

- deprecated
  - https://github.com/roast-cms/french-press-editor /slate.v0.36
  - https://github.com/Canner/canner-slate-editor
  - https://github.com/chatterbugapp/chatterslate
  - https://github.com/nossas/slate-editor

- https://github.com/naufaldi/slate-js-editor
  - Framer Motion, NextJS and Chakra UI

## mobile

- https://github.com/wleroux/slate-android-plugin /202011/ts/slate.v0.55
  - Android support for rich text editors based on Slate

- https://github.com/juliankrispel/slate-in-react-native
  - Proof of concept - Slate in react-native Webview

## slate-view-layer

- https://github.com/minheq/stela
  - Rich Text Editor Slate port in Flutter.

- https://github.com/nathanfaucett/svelte-slate /ts
  - https://nathanfaucett.github.io/svelte-slate/
  - tries to mimic the react api from slate-react as much as possible

## slate-v0.47

- https://github.com/372623460jh/sand-slate /js
  - fork slate 0.47.9 修复中文输入法问题
  - https://github.com/372623460jh/sand-editor

- https://github.com/kanweiwei/slatets /ts
  - slate.v0.37源码解读
  - https://github.com/kanweiwei/easy-editor

- https://github.com/grafana/grafana
  - ui依赖slate.v0.47.8

- https://github.com/wowlusitong/re-editor /201908/js
  - 一个开箱即用的React富文本编辑器

- https://github.com/concord-consortium/slate-editor
  - Rich text editor based on Slate 0.47
# slate-plugins
- https://github.com/newsiberian/slate-plugins /202306/ts
  - plugins
  - slate-gallery, slate-gallery-read-only, slate-linkify, slate-video

- https://github.com/imdbsd/slate-plugin /202106/ts/inactive
  - Rich text editor plugin for slate.js
  - https://github.com/imdbsd/slate-devtools

- https://github.com/alexichepura/slate-pen /202006/ts
  - Custom plugin engine for Slate editors framework. Written in TypeScript.

## markdown

- https://github.com/inokawa/remark-slate-transformer /76Star/MIT/202303/ts
  - remark plugin to transform remark syntax tree (mdast) to Slate document tree, and vice versa. 
  - 支持slate.v0.47和v0.50+
  - Made for WYSIWYG markdown editor.
  - All nodes in mdast syntax tree are supported, including nodes created with remark-gfm
  - And also have experimental support for custom AST.

- https://github.com/hanford/remark-slate /115Star/MIT/202211/ts
  - Transform the contents of a slate 0.50+ editor into markdown and back again.

- https://github.com/accordproject/markdown-transform /202311/js
  - A transformation and parsing framework for converting markdown content to HTML, Slate (for rich-text editing) and other structured document object models (DOMs).
  - 提供了很多子包，本身类似于remark

- https://github.com/zhangyu836/docx-slate /js
  - https://zhangyu836.github.io/docx-slate/
  - slatejs-based docx editor for demonstration of docxjs.
  - 打开docx后分页符显示为横杠
  - https://github.com/zhangyu836/docxjs
    - Javascript port of python-docx.

- https://github.com/orbiting/mdast /201907/js/inactive
  - utilities we've used to combine mdast and Slate in our CMS—Publikator.

## table

- https://github.com/nlulic/slate-table /MIT/202312/ts
  - https://slate-table.org/
  - utilities for flexible and straightforward table editing in your Slate editor
  - Easily add, merge, split cells, and insert rows or columns for more flexibility. 
  - 不支持调整列宽

- https://github.com/lqs469/slate-table /202003/ts
  - https://slate-table.vercel.app/
  - A pretty Slate.js table plugin (Slate.js version > 0.5)
  - 支持合并、拆分单元格
  - 支持调整列宽、行高
  - cons
    - 单元格内双击无法选中单词，已有单元格的选区在点击其他单元格后选区不会消失
- https://github.com/daibin0809/slate-table-demo /202204/ts
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

- https://github.com/jasonphillips/slate-deep-table /201910/js/v0.44
  - https://jasonphillips.github.io/slate-deep-table/
  - 支持table in table
  - Forked from the slate-edit-table implementation, allowing for creation of tables with nested content
  - https://github.com/George-A-Payne/slate-tables /ts/202003
    - https://george-a-payne.github.io/slate-tables/
    - Forked from slate-deep-tables
    - 不支持单元格级别的自绘选区
  - https://github.com/GitbookIO/slate-edit-table
    - archived and has moved to GitBook's private fork
- https://github.com/whatever-company/slate-tables /js/依赖v0.47
  - https://whatever-company.github.io/slate-tables/
  - A Slate plugin to handle table edition.
  - The plugin supports nested tables natively.
  - Colspan and Rowspan are supported. All operations create a matrix containing all cells' positions.

- https://github.com/1build/leyden /10Star/MIT/202203/ts/inactive
  - https://1build-org.gitbook.io/leyden/
  - a data table framework powered by Slate.
  - Leyden builds upon Slate's schema definition system, providing an interface for users to define table-shaped schemas with powerfully customization cells.
  - Leyden's coordinate system is simple and fully interoperable with Slate's Path system.
  - Cells can access data from other cells using absolute coordinates and relative positions.
  - Leyden exposes several pre-built validators (such as numeric and integer) for your cell data
  - Slate requires users to define complicated render functions to detect different types of elements. Leyden handles this automatically

- https://github.com/shrutikachawla/slateTables /js
  - 依赖material-ui.v4、antd

## image/file-upload

- test-image
  - [baidu logo](https://www.baidu.com/img/bd_logo1.png)

- [How to customise Slate js — Part 2 (adding Image upload functionality)](https://sushilkbansal.medium.com/how-to-customise-slate-js-part-2-adding-image-upload-functionality-3320a7260966)
  - [SlateImage.tsx](https://gist.github.com/sushilbansal/10243ac4592a93a9289ae9430ad23544)
  - 基于 FileReader readAsDataURL

- https://github.com/petelc/SlateEditorWithImages
  - 只支持添加url，不支持选择本地文件

- https://github.com/jasjeev4/slate-images
  - This is a version of the slate rich text editor with the ability to add images added in
  - [SlateJS: Adding Images and Links - DEV Community](https://dev.to/koralarts/slatejs-adding-images-and-links-2g93)
  - 依赖django
  - https://github.com/reillymcbride/react_work

## plugins

- https://github.com/openstax-poland/slate-persistence /202309/ts
  - 将IDBDatabase封装成了DocumentDB

- https://github.com/lukesmurray/use-slate-with-extensions /202110/ts/slate.v0.66/inactive
  - https://use-slate-with-extensions.netlify.app/
  - a simple, powerful, and tiny (< 2KB) hook which helps you build self contained and composable extensions for Slate. 

- https://github.com/productboard/slate-edit-list /js/v0.57
  - https://gitbookio.github.io/slate-edit-list/
  - A Slate plugin to handle keyboard events in lists.
  - 支持增加或取消缩进
  - 支持list与paragraph转换

- https://github.com/Simplicity-Tech/sim-slate-types
  - Common typings & helper functions for all slate related Simplicity projects.

- https://github.com/afeiship/next-slate-plugin
  - Slate plugin manager.

- https://github.com/enzoferey/slate-instant-replace /201911/js/slate.v0.44
  - A Slate plugin that gives you full power on the last word your user typed.
  - This package is compatible with <= slate@0.47

- https://github.com/palerdot/react-slite /202305/ts/代码过于简单
  - This react component provides a slack like rich text editing experience powered by slate.js
  - Starting v0.2.0, react-slite is powered by lexical.
# utils
- https://github.com/pubuzhixing8/slate-diff /202107/ts/js/inactive
  - 基于ot、diff-match-patch

- https://github.com/komkanit/slate-auto-save /202307/js/不依赖slate
  - A Slate plugin to handle onChange event on silence without event stack. Useful for implementing auto save Editor.

- https://github.com/thompsonsj/slate-serializers /202310/ts
  - A collection of serializers to convert Slate JSON objects to various formats and vice versa. 
  - Define rules to modify the end result.
  - Designed to work in both Node.js and browser environments.
  - Include top-level custom components with slateToTemplate. Framework agnostic - e.g. return Astro, React or Vue components alongside regular HTML nodes.
  - https://github.com/thompsonsj/slate-serializers-demo

- https://github.com/mdmjg/slate-docx-deserializer /202008/js
  - Microsoft Word deserializer for Slatejs
  - when pasting Microsoft Word content into Slate, the formatting is lost. The mythical html format of Wordx has limited the creation of an accurate deserializer. 
  - this plugin will meet your basic needs when pasting content from Word and maintaining its formatting.
  - 依赖slate-react.v0.58、blob-util

- https://github.com/mwood23/slate-test-utils
  - A toolkit to test Slate rich text editors with Jest, React Testing Library, and hyperscript! 
  - There's so many user input mechanisms, edge cases, selection, state, normalization, and more to keep in mind when developing.
  - It's an abstraction that uses hyperscript to generate editor states that can be tested in a JSDOM environment with a bit of black magic.
  - It's well documented that JSDOM does not support `contenteditable`.
  - https://github.com/AsterMiha/slate-editor-tests

- https://github.com/blockprotocol/blockprotocol
  - The open Block Protocol

- https://github.com/streamich/json-joy/blob/master/src/json-cli/docs/json-patch-test.md
  - 支持slate split、merge、extend

## render-only

- tips
  - 甚至可参考notion-render

- https://github.com/rockettomatooo/slate-react-presentation /MIT/202311/ts
  - a small package that lets you render a slate.js document without the overhead of the actual editor.

- https://github.com/dxiaoqi/slate-render-tool /ts
  - slate render tool

- https://github.com/octet-stream/slate-to-react
  - React component and utilities to transform Slate nodes to React
  - render Slate nodes using SlateView component
  - You can define and use custom transforms to control the output for each node
  - by default slate-to-react will generate a unique id for each node using nanoid to use it as key property of each rendered React component

- https://github.com/logmannn/slate-editor-renderer
  - js
- https://github.com/GitbookIO/slate-lite-renderer
  - Fast renderer for read-only Slate documents

- https://github.com/arrizalamin/slate-fast-renderer /201911/js
  - small renderer for read-only slate.js document for web and react-native
# examples
- https://github.com/fredrikj31/google-docs-clone /202108/js
  - google docs clone, which is built on top of Slate.js

- https://github.com/Kffhi/flomo-react /202304/ts
  - https://www.kffhi.com/flomo/
  - 大约1:1复刻的Flomo网页（旧）版的单纯练习玩具，主要复刻编辑器
  - 依赖reduxjs/toolkit、antd.v4
  - 富文本写着逐渐无聊了起来，后面可能会去做一个类似VitePress的之类的玩意给自己建站用
  - https://github.com/Kffhi/flomo-server /js
    - 后端实现简单，仅依赖express，数据库使用本地json文件
  - https://github.com/Kffhi/flomo-editor
    - 用react+slate写一个青春版的flomo文本编辑器，基本上实现了Flomo编辑器的大部分功能

- https://github.com/sodenn/2do-txt
  - https://2do-txt-sodenn.vercel.app/
  - 2do.txt is a task management that uses the todo.txt format
  - https://github.com/todotxt/todo.txt
    - todo.txt format

- https://github.com/fakob/plug-and-play
  - https://plugandplayground.dev/
  - A visual toolkit for creative prototyping to explore, transform or visualise data.
  - 交互以画板为主，文本为辅

- https://github.com/republik/plattform /55Star/MIT/202311/ts
  - 依赖slate.v0.31、immutable、graphql
  - The platform that powers republik.ch. A tailored solution for a membership based online magazine.

- https://github.com/Thinkmill/keystatic /ts
  - First-class CMS experience, TypeScript API, Markdown & YAML/JSON based, no DB.
  - Built with DNA from Keystone, connects directly to GitHub and doesn’t mess with your source code. 
  - Conceived(构想；设想) for modern front-end frameworks like Next.js, Remix and Astro, designed to fit into your workflow.

- https://github.com/stefancosquer/camas
  - Simple Git based CMS

- https://github.com/wwsalmon/postulate
  - http://postulate.us/
  - Postulate is an all-in-one tool for collecting and publishing your knowledge.
  - Built on Next.js and MongoDB.

- https://github.com/inthelamp/book-reviewer /202111/js
  - a learning project to obtain knowledge and skills about the MERN stack
  - Redux, Redux Thunk, axios, Slate, Lodash
  - Sign-in with JWT token

- https://github.com/mkoskim/mawejs /MIT/202401/js
  - Mawe writer's editor with ElectronJS, React and NodeJS. 
  - Third generation of the editors I have written for my own use.
  - I needed a tool for myself, that's why I wrote Mawe with Python/GTK, and now with ElectronJS, Javascript and React.

- https://github.com/sagemathinc/cocalc /1.1kStar/AGPL3+NonCommercial/202311/ts/python
  - https://cocalc.com/
  - https://github.com/sagemathinc/cocalc/tree/master/src/packages/frontend/editors/slate
  - CoCalc is web-based software that enables collaboration in research, teaching, and scientific publishing.
  - It includes Jupyter Notebooks, Sage Worksheets, a LaTeX Editor and a Linux Terminal to help people work together in real time
  - 前端依赖antd5、dnd-kit、slate-core.v.90、d3、react-redux
  - 后端依赖express-session、passport
  - 基于slate-core实现了virtualized-render, 魔改后的slate-react协议是MIT，EditableMarkdown协议是AGPLv3
  - selectionToText的实现just directly using DOM API, not slatejs, so could run into a subtle problem e.g., due to windowing.
    - we use it here usually for small snippets of visible text, so it tends to be OK
  - It is also possible to run CoCalc on your own infrastructure.
  - You can easily use CoCalc on your own computer for free by running a Docker image.
  - [202107: I ended up forking only the React part of Slate, and massively rewriting it to support virtualized windowing, so we can work with very large possibly complicated to render documents](https://news.ycombinator.com/item?id=28003677)
    - I have no plans to switch from Slate to Prosemirror. Getting virtualized windowing to work with Slate was quite difficult, but it's really table stakes for what I plan on doing longterm, and I don't even know where to begin to do virtualized windowing in Prosemirror.
  - https://github.com/sagemathinc/cocalc/tree/master/src/packages/sync /ts
    - [Collaborative Editing › CoCalc Blog_201810](https://blog.cocalc.com/2018/10/11/collaborative-editing.html)
    - This is an implementation of realtime synchronization. 
    - It has been used heavily in production on https://CoCalc.com for over 5 years. 
    - This is a Javascript library that helps provide collaborative multiuser editing for text files, Jupyter notebooks, and much more.
    - In particular, does this use CRDT or OT?
    - No. This is a realtime sync algorithm for document editing that does not use the same algorithm as literally all the other realtime sync projects. I made up with a different -- vastly simpler -- algorithm, inspired a little by "differential sync" and lot by how distributed databases work
    - This approach works for any document with a notion of "diff" and "patch".
    - I've used it heavily for everything from plain text, to Jupyter notebook, to WYSIWYG markdown editing (on top of Slate).
    - The algorithm itself is ridiculously easy to understand.Each user contributes a stream of patches to a big ordered list. The definition of the current state of the document is the result of applying all the patches in order on a "best effort" basis.

- https://github.com/RealRong/Rendevoz
  - open-source knowledge management application built with React and TypeScript
  - 依赖slate、yjs、rxjs
  - WYSIWYG Block Editor built upon Slate.js, with drag & drop, custom block rendering, etc.
  - Cross platform powered by Electron.

- https://github.com/madmaxmehdi44/platforms-slate-supabase
  - Build a blogging platform based on Slate.js, Supabase and Vercel.
  - Skip the PlanetScale installation and instead create a database on Supabase
  - [Platforms Starter Kit: a template for site builders, multi-tenant platforms, and low-code tools.](https://demo.vercel.pub/platforms-starter-kit)
  - [How to Build a Multi-Tenant App with Custom Domains Using Next.js](https://vercel.com/guides/nextjs-multi-tenant-application)

- https://github.com/grammarly/grammarly-for-developers
  - Grammarly Text Editor SDK

- https://github.com/Delavalom/clone-notion-ai
  - A Notion clone with AI integration

- https://github.com/NDLANO/editorial-frontend
  - CMS for NDLA

- https://github.com/johnsonandjohnson/bodiless-js
  - Framework for building editable websites on the JAMStack

- https://github.com/makeswift/makeswift
  - Setup a new Next.js app with Makeswift in less than 5 minutes.

- https://github.com/dittofeed/dittofeed
  - https://dittofeed.com/
  - Open-source customer engagement platform built for devs
  - 依赖prisma、fastify、codemirror6、mui5、next、slate、d3-dag(流程图/dag)

- https://github.com/neolace-dev/neolace
  - https://www.neolace.com/
  - The next-generation knowledge graph platform.
  - Neolace uses the Neo4j Graph Database as its primary datastore.

- https://github.com/JoogleDocs/JoogleDocs /202303/ts
  - Source code of the JoogleDocs application.
  - This is a T3 Stack project bootstrapped with create-t3-app

- https://github.com/srijeetpatil/bloggr /202110/js
  - a blog web app created with MERN stack
  - uses Slate JS for editing
# collab
- https://github.com/yomorun/react-cursor-chat /slate无关/仅参考
  - React Component helps bring Figma's Cursor Chat to your web applications
  - making real-time collaboration anywhere based on Presencejs.

- https://github.com/typewriter-editor/json-patch
  - Immutable JSON Patch implementation based on RFC 6902 which adds operational transformation (OT) and last-writer-wins (LWW) support for syncing between client and server. 
  - Does not support the full OT algorithm because `copy` and `move` operations cannot be transformed correctly in all cases, so operations must always be applied in correct order. 
    - This means a central server is required to determine order.
  - 👉🏻 json-patch provides a utility that will help sync an object field-by-field using the Last-Writer-Wins (LWW) algorithm. 
    - This sync method is not as robust as operational transformation, but it only stores a little data in addition to the object and is much simpler
    - It does not handle adding/removing array items, though entire arrays can be set. 
    - It should work great for documents that don't need merging text like Figma

- https://github.com/4molybdenum2/Metanoia
  - Metanoia is a Real-time Collaborative Text Editor made with the help of Slate JS and Socket. IO
  - onChange直接发送op，未使用冲突处理算法

- https://github.com/Regloom/slatesyncedit
  - 每次同步全量数据，未使用冲突处理算法
  - 注意测试时要用相同url代表在一个房间里面

- https://github.com/bugbakery/slate-automerge-doc /AGPLv3/202312/ts
  - Syncs slate with an automerge document. Bring your own transport.
  - 依赖automerge2
  - https://github.com/transcribee/slate-automerge-doc /ts
  - https://github.com/transcribee/slate-collaborative
  - https://github.com/transcribee/automerge-py

- https://github.com/BitPhinix/slate-yjs /463Star/MIT/202307/ts
  - https://docs.slate-yjs.dev/
  - Slate-yjs aims to be the goto collaboration solution for slate. 
  - Slate-yjs will overwrite the current editor value with the state contained in the shared type.
  - [Linearising document content](https://github.com/BitPhinix/slate-yjs/issues/296)
  - https://github.com/saadiqbal10/slate-yjs-react-compiled
  - https://github.com/BitPhinix/slate-yjs-example
    - Minimal example project for slate-yjs
  - 🍴 forks
  - https://github.com/sennpang/slate-yjs

- https://github.com/BangKk/slate-crdt-editor /MIT/202310/ts/inactive
  - https://slate-crdt-editor-editor.vercel.app/
  - demo use slatejs and yjs for collaborative editing
- https://github.com/6thfdwp/crdt-editor
  - A collaborating editor based on Slate and Yjs
  - 不依赖slate-yjs

- https://github.com/itoumlilt/crdt-md-editor /202209/ts/slate/未实现功能/仅模版代码
  - https://github.com/concordant/c-markdown-editor
  - React Typescript CRDT based Collaborative Markdown Editor
  - 依赖slate.v0.59、tippyjs，依赖少
  - 代码中未找到协同代码
    - 参考同作者项目 https://github.com/itoumlilt/CRDT-Spreasheet
    - https://gitlab.inria.fr/concordant/software/c-slate-collaborative-markdown-editor /未实现
  - This app aims to show a collaborative text editing application using two eventual consitency backends: revision-based and CRDT-based.
  - This demo shows that with a revision based approach, the user loses updates, either if updates are executed concurrently online, or if multiple users edit the document offline. 
  - With the CRDT-based backend, update convergence is available out-of-the-box.
  - The current demo is implemented on top of PouchDB which offers replication and offline support, but can be easily ported on other equivalent backends. 
  - If you want to run with cross-replica synchronization, just run a CouchDB Server

- https://github.com/geoffreylitt/automerge-slate-playground /202106/ts/v0.59
  - Playing with Automerge + Slate
  - Automerge doc is the source of truth. 
  - The entire text content is stored as a single Automerge. Text string. 
  - Comments and rich text formatting are stored as an array of annotations, per the OAFS idea; also similar to atjson.
  - Doesn't meaningfully use Slate's tree representation. Just treats the doc as a single text node.
  - Intercepts insert/delete operations from the Slate editor, and converts to corresponding Automerge Text ops to edit

- https://github.com/cudr/slate-collaborative /MIT/202101/ts/inactive/automerge
  - A example of a collaborative editor using Slate and Automerge
  - 依赖slate.v0.59、automerge.v0.14、socket.io
  - Based on idea of https://github.com/humandx/slate-automerge /201809/js
  - https://github.com/mms-gianni/slate-collaborationserver

- https://github.com/ahixon/slate-sync-bridge /201906
  - slate-automerge

- https://github.com/anantraghuvanshi/SyncSlate /202309/ts
  - fe + be

- https://github.com/Fronsto/Note-Taking-App /202207/ts
  - minimalistic webapp designed for fast collaborative note taking, created with Javascript/Typescript, Reactjs, Nodejs, Socket.io and runs on a GraphQL Server.

## slate-ot

- https://github.com/cchaonie/collaborative-editor /202401/ts/slate+sharedb
  - Learn collaborative softwares by creating a collaborative editor
  - The slate handles the UI part, and the sharedb handles the collaborative part.

- https://github.com/onechunlin/collaborative-docs /202304/ts/inactive
  - 基于 Slate 和 ShareDb 实现的基于 OT 算法的协同文档

- https://github.com/solidoc/slate-ot /ts/202006
  - Operation Transformations for slate 0.5x.
  - 依赖sharedb

- https://github.com/pubuzhixing8/ottype-slate
  - 基于 Slate 编辑器数据模型的 OTType, 基于标准的 ottypes 实现。
  - 基于原子操作的类型转换还在开发中
  - 示例基于sharedb、slate.v0.65

- https://github.com/Immortalin/slate-operational-transform
  - Slate JS Editor Operational Transform Example using ShareDB (used in production at Narration Box)
  - 依赖slate.v0.57、sharedb、json0-ot-diff
  - Invoking JSON0-ot-diff on every edit is not very efficient.
  - A debounce would trade off between granularity (important for good UX) versus performance. 
  - If you paste a large body of text there is a second or two of lag as diff function has to catch up.

- https://github.com/timbuckley/slate-collaborative
  - A collaborative implementation for the slatejs editor using operational transform
  - 依赖很少

- https://github.com/grimmer0125/slatejs-exp /201807/js
  - use socket.io to sync & show other people's cursors (carets) when collaborating to edit the same content by slatejs editor

- https://github.com/qqwee/slate-ottype
  - 依赖slate.v0.44、sharedb
# more-slate
- https://github.com/vip-git/universal-json-schema
  - https://react-jsonschema-form-material-ui.github56.now.sh/
  - Universal JSON Schema Form - Currently Support for React - Material UI components for building Web forms from JSON Schema.
  - A Material UI port of jsonschema-form. (mui5)

- https://github.com/commercetools/ui-kit
  - Component library based on our design system

- https://github.com/Mirrorgo/slatejs
  - 基于slate.js实现一个富文本编辑器, 用以学习富文本编辑器相关知识

- https://github.com/gwwyn/react-editor
  - Rich-text editor build with React and Slate

- https://github.com/ccjr1120/story-editor_slate
  - 基于slate的文本编辑器

- https://github.com/bouquetrender/slate-panel /202309/js
  - https://slatepanel.netlify.app/
  - rich text editor demo developed with Slate.js
