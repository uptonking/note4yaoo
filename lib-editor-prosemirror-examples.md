---
title: lib-editor-prosemirror-examples
tags: [editor, examples, prosemirror, toc]
created: 2021-07-20T02:14:55.679Z
modified: 2022-08-18T16:57:46.405Z
---

# lib-editor-prosemirror-examples

# guide

- 编辑器的架构模块: model(包含selection)/view/commands

- prosemirror-futuristic
  - 方向：collab、markdown、pivot-table、math/formula、media/embed、cms
  - 大部分的方案是以vanillajs为core，react为wrapper
  - toys
    - 尝试保留rich-markdown-editor的api，将core用 ~~tiptap~~ 重写
    - 尝试用atlassian editor重写outline，抽象出可替换编辑器的接口，考虑可替换的协作同步方案
    - react indexeddb， 编辑器数据频繁的更新可参考编辑器实时协作的更新

- vanillajs-first
  - tiptap/blocknote/novel/dante/wix, guardian, tui.editor.v3, stacks-editor, bangle.dev
  - milkdown(Typora), jcmnunes-bc-editor(md)
- react-first
  - nytimes, remirror, @atlaskit/editor-core, yandex-yfm, syllepsis(字节)
  - wax-prosemirror(coko), manuscript-editor, curvenote-editor(redux), rich-markdown-editor

- more-prosemirror
  - pageboard/client(页面搭建), noteworthy(solidjs)
  - 建站编辑器应该参考gutenberg、wix
  - [npmtrends for pme](https://npmtrends.com/@remirror/react-vs-@tiptap/core-vs-lexical-vs-prosemirror-view-vs-remirror-vs-slate)

- examples
  - https://prosekit.dev/examples/drop-cursor
  - https://code.haverbeke.berlin/prosemirror/prosemirror
  - https://code.haverbeke.berlin/prosemirror/prosemirror-view

- fans-prosemirror
  - https://github.com/sereneinserenade/tiptap-comment-extension
  - https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
  - https://github.com/emergence-engineering/prosemirror-slash-menu-ui
# popular
- tiptap /28.5kStar/MIT/202501/ts
  - https://github.com/ueberdosis/tiptap
  - https://tiptap.dev/
  - https://tiptap.dev/examples/default
    - 文档中的示例基于iframe预览
  - A headless, framework-agnostic and extendable rich text editor, based on ProseMirror.
  - It’s headless and comes without any CSS. You are in full control over markup, styling and behaviour.
  - 优点: 🔁 协同后端实现hocuspocus, 示例丰富(drawing), RAG生成示例
    - 编辑器内嵌入iframe
    - 支持多层嵌套拖拽
  - 缺点: 很多扩展未开源

- BlockNote /8.4kStar/MPLv2+AGPL/202508/ts/tiptap
  - https://github.com/TypeCellOS/BlockNote
  - https://www.blocknotejs.org/
  - A "Notion-style" block-based extensible text editor built on top of Prosemirror and Tiptap.
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，特别是支持将list item拖入拖出列表
  - 支持斜杠菜单、悬浮菜单修改标题层级、多级列表、顺滑动画
  - ✨❤️️ 支持multi-column布局, 支持拖拽生成多列布局 (AGPL)
  - ✨ 支持editor多实例，且支持将block从一个editor拖到另一个editor
  - 📱 支持mobile优化
  - 示例丰富: 嵌入pdf
  - 依赖tiptap.v2、tippyjs、styled-components
  - core+react-slashMenu/toolbar
  - bugs
    - 复制粘贴多行文本
  - Collaboration提供了多种实现: y-sweet, liveblocks, partykit
  - also works with vanilla JS for use with other frameworks
  - 100% of BlockNote is open source. While the library is free, we offer paid consultancy and support services
  - "BlockNote Pro" is not an additional library, but instead a subscription service built around the open-source BlockNote library.
  - BlockNote is open source software licensed under the MPL 2.0 license, which allows you to use BlockNote in commercial (and closed-source) applications - even without a subscription
    - The XL packages are dual-licensed and available under AGPL-3.0 or a commercial license as part of the BlockNote Business subscription or above.

- milkdown /9.1kStar/MIT/202501/ts/remark
  - https://github.com/Milkdown/milkdown
  - https://github.com/Saul-Mirone/milkdown
  - https://milkdown.dev/
  - https://milkdown.dev/playground
  - 依赖prosemirror、remark、prism、katex，但不依赖prosemirror-markdown、react
  - A plugin-driven WYSIWYG markdown Editor, inspired by Typora, built on top of `prosemirror` and `remark`.
  - ✨ 主要特性是自定义markdown、支持plugin
  - Plugin Driven: Everything in Milkdown are plugins
  - Collaborative with yjs
  - Headless: comes without any CSS
  - Math - LaTeX math equations support via math plugin
  - 不同于其他prosemirror项目，可配置支持的markdown特性
  - ⚠️️breaking: @milkdown/core@4.4.0(date202107) migrate from markdown-it to remark
  - Milkdown is a headless editor, which means it doesn't come with any default styles. 
    - Crepe theme uses CSS variables for consistent styling. 
    - provides default class names for each node and mark. 
  - Crepe is a powerful, feature-rich Markdown editor built on top of Milkdown. It provides a complete editing experience with a beautiful UI and extensive customization options.
  - https://github.com/Milkdown/vscode /MIT/202501/ts
    - vscode-ext: Edit markdown in a WYSIWYG way, powered by milkdown

- https://github.com/prosekit/prosekit /720Star/MIT/202507/ts
  - https://github.com/ocavue/prosekit
  - https://prosekit.dev/
  - https://prosekit.dev/guide/integrations/react
  - Framework agnostic and headless rich text editor based on ProseMirror
  - 整体采用ContextProvider模式，`<ProseKit editor={editor}>` 编辑器实例放在顶层
  - 支持多个前端框架react/vue/solid/svelte
  - 支持多层嵌套拖拽
  - https://prosekit.dev/examples/change-tracking
    - 示例较简单，偏向纯文本的diff
  - https://prosekit.dev/components/block-handle/
    - reorder, and insert blocks in your editor through drag-and-drop.
  - Cross-Framework Support: Use with React, Vue, Preact, Svelte, Solid, or vanilla JavaScript.
  - Modular & Extensible: Easily add or modify features.
  - Headless: Full control over the editor's appearance.
  - Tailwind CSS Components: Quickly build beautiful editors with copy-paste components in your app.
  - supports multiple content formats: json, html
  - ProseKit can run in Node.js environments for background processing, CLI applications, and Server-Side Rendering (SSR). The primary limitation is that DOM-dependent APIs are unavailable unless you provide a DOM implementation.
  - 🆚️ [how is it different from Remirror, Prosemirror or Tiptap? _202412](https://github.com/prosekit/prosekit/discussions/857)
    - Remirror and TipTap share some similar designs. One of them is that every extension is a class (e.g., BoldExtension). If you want to add more features based on an existing extension, you extend it (e.g., class MyBoldExtension extends BoldExtension) and add/override methods in the subclass.
    - I found this design makes it harder to use in complex scenarios. Using the principle of "composition over inheritance," I redesigned the extension system in ProseKit, where every extension is just a function that calls one or more other extensions.
    - I also made some other improvements, like simpler lifecycle management and more UI library (Svelte, SolidJS, etc.) support.
    - Sadly, these changes are so significant that I won't be able to publish them as a new major version of the existing Remirror project, so I created ProseKit.
- prosemirror-adapter /65Star/MIT/202402/ts
  - https://github.com/prosekit/prosemirror-adapter
  - https://github.com/Saul-Mirone/prosemirror-adapter
  - Universal adapter to create prosemirror nodeview from modern UI frameworks.
  - 支持react/vue/lit/svelte
  - 支持node-view, plugin-view, widget-decoration
  - not on the plan: no ui, no hotkeys, no schema

- remirror /2.9kStar/MIT/202504/ts
  - https://github.com/remirror/remirror
  - https://remirror.io/
  - https://remirror.vercel.app/
  - [basic editor demo](https://remirror.vercel.app/?path=/story/editors-wysiwyg--basic)
  - A React toolkit for building cross-platform text editors, based on ProseMirror.
  - I18n support via lingui.
  - Great support for mobile devices.
  - Out-of-the-box editors, or create own by composing extensions.
  - Collaborative editing with yjs or prosemirror-collab.
  - 缺点: ui组件依赖material-ui, api设计依赖装饰器
  - [Introducing Remirror v3 _202407](https://www.remirror.io/blog/announcement-v3)
    - This version aims to make it easier to use Remirror in existing applications, by not imposing our architectural decisions on to you.
    - The core of Remirror v2 relied on packages such as `@mui/material` to power our menus and toolbars, and @lingui/core to provide internationalisation (i18n) support.
    - we have removed these features from the core, and moved them into optional packages.

- wax-prosemirror /9Star/MIT/202411/js/react
  - https://github.com/Coko-Foundation/wax-prosemirror
  - https://gitlab.coko.foundation/wax/wax-prosemirror
  - https://waxjs.net/docs/wax/
  - http://wax-demo.coko.foundation/
  - https://waxjs.net/features/
  - 提供了丰富示例，包括编辑器内带下拉框的表单、脚注面板浮层、Track changes
  - 支持评论，评论卡片可与编辑器内容水平对齐，但被评论文本不支持部分重叠
  - ✨ 实现了suggestion mode
  - The Word Processor for the Web
  - Wax depends on the following libraries.
    - React for the view(UI)
    - Styled-components for theming and styling.
    - Inversify.io as service containers，用的不多，可剥离
  - 依赖注入使用了很多class
  - 大量使用react组件
  - ref
    - https://github.com/christos8333/wax-prosemirror
    - licit也是适合论文的编辑器
    - Wax, a [Cabbage Tree Labs](https://www.cabbagetreelabs.org/) project
    - The Cabbage Tree Method and Book Sprints and led the development of open source software for publishing such as PubSweet, Editoria, Kotahi, PagedJS, Wax, BookType and many more
  - https://github.com/uday-ament/wax-prosemirror-services /202403/js
    - An extension of wax-prosemirror-services with additional services

- @atlaskit/editor-core /8Star/Apache2/202208/ts
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - [kitchen-sink-example](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - A package contains Atlassian editor core functionality
  - 基于react class组件实现
  - 提供了针对image/file的图文混排工具
  - 还提供了多列布局工具，包括两栏、三栏、按比例、居中
  - 提供了语法树ADF显示
  - 样式写法在2022年抛弃styled转向css工具方法
  - https://github.com/TeemuKoivisto/prosemirror-react-typescript-example /MIT/202210/inactive
    - copy the approach by Atlassian editor_v20201205
  - ref
    - https://github.com/TeemuKoivisto/prosemirror-track-changes-example
    - https://github.com/pioug/atlassian-frontend-mirror

- guardian-prosemirror-editor /2Star/MIT/202311/ts/react/inactive
  - https://github.com/guardian/prosemirror-editor
  - provide a re-usable ProseMirror editor for use across our tools
  - it aims to replace Scribe-based rich text editors with a React-based prosemirror editor in: tagmanager, atom-workshop
- guardian-prosemirror-elements /37Star/MIT/202311/ts
  - https://github.com/guardian/prosemirror-elements
  - This Prosemirror plugin adds the ability to add custom 'elements' to a document.
  - 使用prosemirror编辑器作为NodeViews，嵌套多实例编辑器
  - Prosemirror-elements provides a way of expressing an Element and its Fields in the UI framework of your choice, and we provide React bindings as a default.
  - What is an Element?
    - Modelling non-text content in Prosemirror can be tricky. 
    - Elements contain user-defined Fields that can model many different kinds of content, including rich text fields and arbitrary data.
    - Each Element is made up of Fields, which represent a data type – for example, text, rich text, or custom data types.
  - [How prosemirror-elements works](https://github.com/guardian/prosemirror-elements/blob/main/docs/how-it-works.md)

- https://github.com/handlewithcarecollective/react-prosemirror /apache2/202501/ts
  - A fully featured library for safely integrating ProseMirror and React.
  - On Jan. 17, 2025, the maintainers of the @nytimes/react-prosemirror library decided fork the v2 release into its own project. It had been developed entirely by one developer, @smoores-dev, who had not worked for NYT in years
  - It's also challenging to effectively use React to define node views for ProseMirror documents. Both ProseMirror and React expect to have full control over their respective parts of the DOM. They both modify and destroy DOM nodes as needed. Previous solutions (including previous iterations of this library) have attempted to work around this power struggle by producing wrapper elements to hand to ProseMirror, and then mounting React nodes within these (usually with React Portals).
    - This approach works, but tenuously. Having additional nodes in the document that ProseMirror isn't strictly aware of can cause issues with its change detection system, leading to challenging edge cases. [Deleting the last node view can throw errors · Issue · nytimes/react-prosemirror _202306](https://github.com/nytimes/react-prosemirror/issues/42)
  - 💡 This library provides an alternate implementation of ProseMirror's `EditorView`. It uses React as the rendering engine, rather than ProseMirror's home-brewed DOM update system. This allows us to provide a more comfortable integration with ProseMirror's powerful data model, transformations, and event management systems.
    - the new release moves rendering responsibility entirely into React. We disabled the EditorView's DOM update cycle, and implemented the same update algorithm that prosemirror-view uses with React components. The result is a more idiomatic, React-based library, which doesn't have any of the issues of the original implementation.
- nytimes-react-prosemirror /314Star/apache2/202311/ts/migrated
  - https://github.com/nytimes/react-prosemirror
  - A fully featured library for safely integrating ProseMirror and React
  - React separates updates into render and commit phases so that it can process updates in batches
  - [Announcing React ProseMirror_202303](https://discuss.prosemirror.net/t/announcing-react-prosemirror/5328)
  - 📡 [The Future of @nytimes/react-prosemirror_202309](https://discuss.prosemirror.net/t/the-future-of-nytimes-react-prosemirror/5855)
    - For the past several months, I’ve been hard at work on a very different approach to integrate React and ProseMirror. 
    - The summary is this: the new approach completely replaces ProseMirror’s DOM management system with one built in React. 
    - We’re still using `prosemirror-view` for everything outside of change detection and DOM updates, which means we are exposing exactly the same API. 
    - In fact, I’ve ported over most of the unit tests from prosemirror-view to ensure that behavior matches the default library.
  - ProseMirror View library renders ProseMirror documents in a single-phase update. 
  - The first phase of a React update should be free of side effects, which requires that updates to the ProseMirror View happen in the second phase.
    - during the first phase, React components actually have access to a different (newer) version of the EditorState than the one in the Editorview. 
    - As a result code that dispatches transactions may dispatch transactions based on incorrect state. 
  - 💡 There are two different directions to integrate ProseMirror and React: 
    - you can render a ProseMirror EditorView inside of a React component, 
    - and you can use React components to render ProseMirror NodeViews. 
    - This library provides tools for accomplishing both of these goals.
  - https://github.com/nytimes/oak-byo-react-prosemirror-redux
    - https://nytimes.github.io/oak-byo-react-prosemirror-redux/
    - This repository contains learning materials originally sourced and written for the Oak team at The New York Times.
    - The courses within focus on developing an understanding of how the three tools that the Oak collaborative rich text editor relies on, React, ProseMirror, and Redux, actually work.
    - [Build Your Own: ProseMirror View](https://nytimes.github.io/oak-byo-react-prosemirror-redux/post/build-your-own-pm-view/)
      - demonstrate how to build the core components of a ProseMirror view library.
      - https://github.com/mlhiter/mini-prosemirror
    - [Build Your Own: React, ProseMirror, and Redux : javascript](https://www.reddit.com/r/javascript/comments/10swhle/build_your_own_react_prosemirror_and_redux/)
    - 🤔 [Why I rebuilt ProseMirror’s renderer in React _202502](https://smoores.dev/post/why_i_rebuilt_prosemirror_view/)
      - For almost five years, I worked on the New York Times’ rich text editor, Oak.
      - The Times’ website is written with React, which is one of the big reasons that Oak was written in React. We were able to author React components that could be used by both the reader-facing website and Oak
      - React and ProseMirror do not play nicely together. 
      - React and ProseMirror actually have very similar philosophies about how to manage the DOM. Both libraries maintain a sort of “virtual DOM”, a tree structure that’s very efficient to update, which maps to the actual DOM that the browser uses to render the web page. Both libraries also separate state from the view, and use that state to drive the view unidirectionally. The differences between how they implement these philosophies are small, but they’re very important

- manuscript-editor /7Star/apache2>CPAL/202208/ts/react
  - https://github.com/Atypon-OpenSource/manuscripts-article-editor
  - the editor package of Manuscripts app to be used in a react application.
  - 数据保存支持 pouchdb-adapter-idb
  - https://github.com/Atypon-OpenSource/manuscripts-article-editor/blob/master/src/lib/comparison/compare-table-element.ts
    - 使用了 diff-match-patch 比较文档字符串
  - https://github.com/Atypon-OpenSource/manuscripts-body-editor
    - A React + ProseMirror editor for manuscripts.
  - https://gitlab.com/mpapp-public/manuscripts-manuscript-editor
  - https://gitlab.com/mpapp-public/manuscripts-frontend
    - /CPAL-1.0; 类似MPL
  - A React + ProseMirror editor for manuscripts.
  - 编辑器依赖prosemirror、@jupyterlab/services、codemirror5、popperjs、react-dnd
  - 编辑器样式采用论文简洁风格，支持 摘要、脚注、交叉引用、评论
  - Manuscripts.io web frontend which makes API calls to manuscripts-api and manuscripts-sync
  - This repository contains the browser client for the Manuscripts collaborative authoring environment, in a single-page React app (desktop and mobile app embeddable using cocos).
  - https://github.com/Atypon-OpenSource/manuscripts-data
    - https://github.com/Atypon-OpenSource/manuscripts-examples
    - source data for use by Manuscripts client applications
  - ref
    - https://gitlab.com/mpapp-public/manuscripts-api
    - https://gitlab.com/mpapp-public/manuscripts-sync
    - https://gitlab.com/mpapp-public/manuscripts-data
  - [Manuscripts.io is a ProseMirror-based editor in a React application _202011](https://discuss.prosemirror.net/t/manuscripts-io/3299), 
    - served as a PWA that works offline and can be installed as a desktop application via Chrome.
    - instead of using ProseMirror’s standard collaboration plugin, 👉🏻 Manuscripts serializes each block of the document to a JSON object with an id, which is stored in the browser’s local storage (IndexedDB) using RxDB/PouchDB and then synced with Couchbase via Sync Gateway, which handles permissions and validates each object according to a defined schema. 
    - Manuscripts.io is built by a team within Atypon; Atypon成立于1996年，是一家为全球期刊发展服务的软件系统公司，Atypon旗下出版平台Literatum为全球近100000本期刊和919家出版商网站、45%的英文同行评审学术期刊和其他语种的出版物提供服务。
    - Conflict resolution is handled in each client, with any conflicting changes in the document’s content presented to the user for them to choose the most appropriate resolution.
    - Collaboration in Manuscripts.io works at the project level — each project can contain several manuscripts — and collaborators can either be responsible for editing parts of the document or can simply comment by adding annotations to blocks or ranges of the manuscript.
    - Manuscripts.io includes some innovations: figures that can be (re)generated dynamically by evaluating code in a hosted Jupyter kernel; built-in searching of online reference databases; configurable paragraph, section and inline styles, and output to multiple formats (DOCX, PDF, JATS XML, HTML, and others).

- notitap /39Star/MIT/202209/ts
  - https://github.com/sereneinserenade/notitap
  - https://sereneinserenade.github.io/notitap/
  - 依赖daisyui、tippyjs、floating-ui、fuzzysort
  - Notion like editor built on top of tiptap.
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但list item不支持拖入拖出

- tui.editor.v3 /15.1kStar/MIT/202302/ts/inactive/几乎无依赖/生态丰富
  - https://github.com/nhn/tui.editor
  - https://ui.toast.com/tui-editor
  - https://nhn.github.io/tui.editor/latest/tutorial-example01-editor-basic
  - ✨ v3新版本迁移到了prosemirror
  - 只依赖prosemirror，mark解析自己实现了toastmark，公司还自研了很多ui组件
  - core只依赖 codemirror5，另外提供了react/vue-editor
  - 全都是vanillajs，react的封装很薄，只有3文件
  - 编辑器支持分屏查看、双屏同步滚动、配置图表chart、uml、语法高亮、合并单元格、自定义toolbar、i18n、theming
  - 代码复杂度高
  - 支持通过代码块中的图表配置信息生成图表
  - The Editor allows you to edit your Markdown documents using text or WYSIWYG and comes with Syntax Highlighting, Scroll-Sync, Live Preview, and Chart features.
  - ref
    - [example: Editor with Chart Plugin](https://nhn.github.io/tui.editor/latest/tutorial-example07-editor-with-chart-plugin)
    - https://github.com/QinHongZhe/hongzhe-tui.editor

- bangle.dev-editor /667Star/MIT/202503/ts
  - https://github.com/bangle-io/banger-editor
  - https://github.com/bangle-io/bangle-editor
  - https://github.com/bangle-io/bangle.dev
  - https://bangle.dev/docs/examples/markdown-editor
  - https://app.bangle.io/
  - 支持拖拽标题section，但不支持拖拽section内的段落
  - 使用了浏览器文件系统api来支持打开本地文件
  - Collection of higher level rich text editing tools. It powers the local only note taking app https://bangle.io
  - Bangle is written in a framework agnostic way, we have support for React and I have plans to add Vue support
  - bangle.io /909Star/AGPLv3/202310/ts/react
    - https://github.com/bangle-io/bangle-io
    - https://bangle.io/
    - 提供了 indexed-db-storage-provider, fs
    - A web only WYSIWYG note taking app that saves notes locally in markdown format

- curvenote-editor /140Star/MIT/202309/ts/inactive
  - https://github.com/curvenote/editor
  - https://curvenote.github.io/editor/
  - https://curvenote.com/
  - 依赖 redux-toolkit、codemirror.v5、material-ui.v4、date-fns
  - 支持 footnote、comment、很多latex特性
    - 评论与block顶部对齐，不与评论位置水平对齐
  - 👀 支持在编辑器内定义变量和滑块
  - 支持同步，基于prosemirror-collab+firebase+redux
  - 支持斜杠菜单，并且表格单元格内的斜杠菜单解决了插入上下行的问题
  - interactive scientific editor built with ProseMirror, React and Redux
  - A collaborative, rich text editor for interactive technical & scientific content., implementing the MyST standard, and integrating with JupyterLab, JupyterBook and Sphinx. 
  - We aim to lower the barriers to writing computational narratives.
    - Today, narrative is often moved out of computational notebooks into static document creation tools (Microsoft Word, Google Docs, LaTeX, Slides/PPT).
  - https://github.com/curvenote/curvenote /7Star/MIT/202208/ts
    - curvenote is an open source library and command line interface (CLI) to create share and publish technical documents.
    - https://github.com/curvenote/blocks
      - Schemas, types and utilities for Curvenote APIs and DTOs.
    - [Curvenote - scientific editor, explorable explanations & floating comments__202102](https://discuss.prosemirror.net/t/curvenote-scientific-editor-explorable-explanations-floating-comments/3503)

- yfm-editor /3Star/MIT/202211/ts/md-it
  - https://github.com/yandex-cloud/yfm-editor
  - https://preview.yandexcloud.dev/yfm-editor/
  - https://ydocs.tech/en/
  - 依赖prosemirror、markdown-it、react-use、gravity-ui
  - Yandex Flavored Markdown (YFM) is a Markdown dialect and a set of tools for transforming Markdown to HTML in real time and building complete documentation projects.
  - 支持显示tab
  - Expandable: you can add any plugin for markdown-it or write your own.

- Stacks-Editor /218Star/MIT/202208/ts
  - https://github.com/StackExchange/Stacks-Editor
  - https://editor.stackoverflow.design/
  - a combination rich text/markdown editor that powers Stack Overflow's post editing experience.
  - 依赖prosemirror, hightlight.js、markdown-it、@lezer/markdown、stacks-ui，不依赖react
  - 全部基于es6 class，[new EditorView()](https://github.com/StackExchange/Stacks-Editor/blob/main/src/rich-text/editor.ts#L105)的过程非常标准，无封装

- https://github.com/alphagov/govspeak-visual-editor /MIT/202507/js
  - https://govspeak-preview.publishing.service.gov.uk/editor
  - A visual editor for Govspeak built using ProseMirror
  - Govspeak is a flavour of Markdown used for publishing content on GOV. UK.

- syllepsis /187Star/MIT/202304/ts/字节/inactive/参考中文支持
  - https://github.com/bytedance/syllepsis
  - https://bytedance.github.io/syllepsis/#/zh-cn/about
  - [编辑器在线例子](https://bytedance.github.io/syllepsis/#/zh-cn/playground)
  - 支持格式刷、调整文字间距、段落间距
  - 大多vanillajs，不依赖react
  - 支持[Card或Block插件](https://bytedance.github.io/syllepsis/#/zh-cn/chapters/card-plugin)，但不支持拖拽，块比卡片拥有更广的定义，但我们无意增加开发者的心智负担，也可以认为卡片是一种块
  - 设计了占位插件，可实现左侧加号按钮
  - rich text editor compatible with mainstream modern browsers.
  - We re-encapsulate Prosemirror to provide more concise APIs, a large number of basic plugins
  - https://github.com/lastnigtic/syllepsis-collab
    - Example of `Syllepsis` collaborative editing using `prosemirror-collab`

- zotero-note-editor /16Star/AGPLv3/202404/js
  - https://github.com/zotero/note-editor
  - 依赖 prosemirror、katex、react、react-intl
  - Note editor for Zotero 6
  - 提供了 web/ios 两个ui入口

- gitlab-editor /3916Star/MIT/202208/js/vue2/tiptap2
  - https://gitlab.com/gitlab-org/gitlab/-/tree/master/app/assets/javascripts/content_editor
  - [WYSIWYG editor toolkit architecture proposal__2021](https://gitlab.com/gitlab-org/gitlab/-/issues/273238)
    - implementing support for all of md flavors is an unnecessary cost.
    - Solution 1: Traceability or file diffs
    - Solution 2: Relying on the Markdown preview endpoint
  - ref
    - https://github.com/gitlabhq/gitlabhq/tree/master/app/assets/javascripts/content_editor

- https://github.com/WaiSiuKei/neditor /MIT/202308/ts/inactive
  - https://waisiukei.github.io/neditor/
  - rich text editor aimed at running in Canvas.
  - 在事件模型和 DOM 模型都准备好之后，移植 ProseMirror 就非常容易了。
  - [从浏览器源码开始实现 Canvas 富文本编辑器 - 知乎 _202307](https://zhuanlan.zhihu.com/p/642703113)

- taleweaver(织书✨) /90Star/MIT/202008/ts
  - https://github.com/yuzhenmi/taleweaver
  - https://yuzhenmi.github.io/taleweaver/
  - Web word processor for 2Tale Writer's Portal.
  - ✨ 未使用contenteditable，基于dom实现排版，支持显示分页； 
    - 自定义排版还可参考 dropflow，但输出canvas
  - core无依赖，react封装很少(只有2个文件)，不依赖prosemirror
  - 大量使用es6 class
  - 自己实现了依赖注入，设计了model/service/component
  - 该项目是作为2Tale Writer's Portal的核心编辑器来开发的。
  - 项目的目标是保持编辑器核心的最小化和可扩展性，覆盖必要的功能以便有机会将其扩展到更具体的用例中。
  - 目前有相当多的开源所见即所得（WYSIWYG）的编辑器，使用ContentEditable特性提供编辑界面。这些编辑器同时可以充分利用CSS和浏览器的布局引擎去渲染和修饰文档的样式。
  - 因为浏览器关注的是布局和渲染，所以这些编辑器不清楚内容会渲染在什么地方，这在大多数场景下是可以接受的。然而，当你开发一个依赖布局信息的功能的时候，你可能会遇到一个不能跨越的障碍。
  - 一个很常见的场景就是目前这些开源编辑器不能对文字进行分页处理。要实现这一特性，需要在确定何处分页之前就知道文档是如何被拆分成一行一行的，并且知道每行的尺寸和位置。像谷歌Doc这种有分页功能的商业的云服务文字处理是通过研发自有排版引擎来达到目标的。
  - Taleweaver 拥有排版引擎同时提供了一套API来访问排版信息。它的目标就是把word那种风格的文字编辑体验带到开源社区。
  - Taleweaver的工作原理是获取文档状态并将其呈现到屏幕上。当状态发生变化时，这些更改将通过一系列步骤传播到屏幕。
    - [State] -> [Model Tree] -> [Render Tree] -> [Layout Tree] -> [View Tree]
    - [状态] -> [模型树] -> [呈现树] -> [布局树] -> [视图树]
  - [Page node data-id unnecessarily updates on keydown](https://github.com/yuzhenmi/taleweaver/issues/73)
    - I wanted paginated documents, which requires breaking up pages at equal heights. This cannot be done efficiently with editors like ProseMirror because we need to know the position and height of each line in order to produce pages.
    - I don't have prior experience with building word processors, much of the project's design has been trial and error.
    - There are 2 features that I'm still trying to figure out, with no satisfactory solution so far: Pasting, Text formatting 

- https://github.com/oschina/tide /MIT/202306/ts/react/inactive
  - https://oschina.gitee.io/tide
  - 开箱即用、扩展性强、支持 Markdown 语法、基础功能完善的 React 富文本编辑器

- wode /3Star/MIT/202206/ts
  - https://github.com/wenerme/wode
  - https://wode.vercel.app/tiptap
  - TipTap based Google Doc
  - 实现了预定义2/3多栏布局，但不work
  - google采用canvas好象是为了解决浏览器兼容性方面的问题。因为在dom在不同浏览器上表现差别确实大，大到它都不再维护直接换成canvas了。

- jcmnunes-editor /5Star/MIT/202203/ts
  - https://github.com/jcmnunes/editor
  - https://editor.binarycapsule.tech/
  - 功能简单，短小精悍
  - Prosemirror based text editor with markdown shortcuts and serialization
  - It is highly inspired by rich-markdown-editor, linear-app-editor

- gem /10Star/MIT/202205/ts/inactive/代码量少
  - https://github.com/tanishqkancharla/gem
  - https://gem.tanishqkancharla.dev/
  - 只依赖prosemirror，不依赖react
  - Gem (previously called Editor) is a performant and simple plain text editor 
  - The design is very inspired by Paco Coursey's [Writer]().
  - [Gem, a plain-text editor based on prosemirror_202111](https://discuss.prosemirror.net/t/gem-a-plain-text-editor-based-on-prosemirror/4231)
    - I worked on moving to codemirror 6 
    - https://github.com/tanishqkancharla/gem/tree/codemirror /202112/cm6.v0.19
  - https://github.com/pacocoursey/writer /291Star/NALic/202110/js/inactive
    - https://writer.paco.sh/
    - Plain text editor from scratch, made for the web. Drag and drop files to open them.
    - Buffer is an array of array of lines
    - Text is manually measured and wrapped with canvas
    - Lines are virtualized on scroll and drawn as divs

- smartblock /249Star/MIT/202003/ts/inactive/prosemirror
  - https://github.com/appleple/smartblock
  - https://appleple.github.io/smartblock/
  - 依赖prosemirror、codemirror5、react-highlight.js、react-svg、styled-components
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序，但有上下箭头按钮
  - intuitive block based wysiwyg editor built with React and ProseMirror

- Xheldon/NotionEditor /30Star/GPLv2/202103/ts/inactive
  - https://github.com/Xheldon/NotionEditor
  - A Notion's editor implement based on ProseMirror, just for feasibility studies.
  - 不允许跨 block 选择部分文本内容
  - 依赖 redux、lodash
  - 基础 schema 是两个 doc 和 text, 这是 Prosemirror 默认的两个最大和最小可编辑 schema. 而设计 schema 的时候我使用的最小编辑单元是 textblock, 表现形式是一个 div 中包含着 text
  - 所有的元素都是使用 div 进行模拟, 而不是使用语义化的 p/ul/ol 等进行, 这是为了摆脱浏览器的限制, 如段落嵌套段落的时候, p 标签无法嵌套块级元素等.
  - 使用了 React 构建界面的有: Slash

- use-prosemirror /321Star/MIT/202201/ts/inactive
  - https://github.com/ponymessenger/use-prosemirror
  - ProseMirror + React made easy
  - Separates state and presentation so you can keep your state as high up as necessary.
  - Allows using `EditorView` props as React props.
  - This library is in production at Pony Messenger.

- react-prosemirror /223Star/MIT/202104/ts
  - https://github.com/hubgit/react-prosemirror
  - https://ow1qi.csb.app/
  - A React component for ProseMirror.
  - provides a solution for efficiently integrating ProseMirror with React, without creating a new API.
- https://github.com/rebecca-thompson/prosemirror-react
  - A React app implementation of the Prosemirror rich text editor

- reprose /2Star/MIT/202109/ts
  - https://github.com/riboseinc/reprose
  - Configurable ProseMirror instance as a React component
  - Provides tools and patterns that simplify rendering a document to HTML
  - 渲染自定义组件基于`plugin.props.nodeViews`配置
  - 将插件的功能分为编写author和显示schema两部分
  - Reprose’s functionality is contained in features. 
  - A feature can provide schema aspects (nodes, marks), and authoring aspects (key bindings, menu items, ProseMirror plugins).

- https://github.com/KhushilMistry/prosemirror-react /202408/ts/inactive
  - https://prosemirror-react.vercel.app/
  - a powerful library for building rich-text editors on the web
  - In early 2021, few libraries offered React integration with ProseMirror. 
    - Inspired by these libraries and `prosemirror-react-nodeviews`, we developed our own toolkit.
    - We recently revisited our decision and explored other libraries. if we were to start anew, we might choose Tiptap instead of building a toolkit from scratch.

- Aditor /9Star/MIT/202104/js
  - https://github.com/YacheLee/Aditor
  - https://yachelee.github.io/Aditor/
  - A React component made by ProseMirror
  - nodes和marks的自定义渲染执行发生在pm-plugin的new Plugin()过程中，没有使用NodeView

- rpm-editor /1Star/MIT/202201/ts
  - https://github.com/shobokshy/rpm-editor
  - A React renderless rich text editor component.
  - 只依赖prosemirror、react
  - 没有提供使用示例

- https://github.com/littlemyx/ProseMirrorReactWrapper
  - Autocomplete words by hitting the Tab key in the end of the word by the local dictionary

- https://github.com/johnkueh/prosemirror-react-nodeviews /202003/ts
  - An example of how to use React components as NodeViews for ProseMirror
  - 原理是`ReactDOM.createPortal(<Component />, container, shortid.generate())`; 
  - 事件传播会根据组件在react tree中的位置，而不是根据在真实dom tree中的位置

- prosemirror-dev-toolkit /40Star/MIT/202208/ts/svelte
  - https://github.com/TeemuKoivisto/prosemirror-dev-toolkit
  - https://teemukoivisto.github.io/prosemirror-dev-toolkit/
  - This is a rewrite of prosemirror-dev-tools
  - I took it to my own hands to rewrite it in Svelte.
- prosemirror-dev-tools /241Star/MIT/202402/ts
  - https://github.com/d4rkr00t/prosemirror-dev-tools
  - Developer Tools for ProseMirror
  - Inspect document – all nodes and marks
  - Inspect selection – position, head, anchor and etc.
  - Inspect active marks
  - See document stats – size, child count
  - ref
    - https://github.com/NovelAI/prosemirror-dev-tools /提交多
      - a monkey patched fork which fixed the wrong indexing problem
      - 合并了其他人的修复 https://github.com/kepta/prosemirror-dev-tools
    - https://github.com/luke-john-atlassian/prosemirror-devtools /单独app或extension/inactive
    - [Is there a good way to understand the “pos” that is used all over?](https://discuss.prosemirror.net/t/is-there-a-good-way-to-understand-the-pos-that-is-used-all-over/3458)
# tiptap/milkdown/remirror/atlassian
- https://github.com/NiazMorshed2007/shadcn-tiptap /MIT/202410/ts
  - https://tiptap.niazmorshed.dev/
  - Sets of custom extensions & toolbars for tiptap editor. 
  - Install with shadcn/cli.

- typist /8Star/MIT/202211/ts
  - https://github.com/Doist/typist
  - https://typist.doist.dev/
  - Tiptap-based rich-text editor React component that powers Doist products
  - 提供了纯文本和富文本2种输入模式
  - Typist also supports a plain-text mode, and comes with HTML/Markdown serializers.

- better-virgool /9Star/MIT/NALic/202208/ts/tiptap
  - https://github.com/ahhshm/better-virgool
  - https://ahhshm.github.io/better-virgool/
  - An attempt to create a better rich text editor than virgool.io. Powered by Tiptap and ProseMirror
  - 实现了RTL国际化方向
  - 数据保存使用了 idb-keyval

- https://github.com/fantasticit/magic-editor /202301/ts/inactive
  - http://magic-editor.vercel.app/
  - rich text editor built on top of Prosemirror and Tiptap

- element-tiptap /825Star/MIT/202208/ts/vue/tiptap/inactive
  - https://github.com/Leecason/element-tiptap
  - https://element-tiptap.vercel.app/
  - WYSIWYG rich-text editor using tiptap and Element UI for Vue2 (tiptap2 and Vue3 is in alpha)
  - new version2 support Vue3, use tiptap2 and Element Plus

- nextcloud-text /591Star/AGPLv3/202507/js/vue/tiptap/php
  - https://github.com/nextcloud/text
  - Collaborative document editing using Markdown
  - 依赖tiptap.v2, yjs, @_ueberdosis/prosemirror-tables.v1.1.3, markdown-it、vue2、vuex3
  - Nextcloud Text is the default text editor since Nextcloud 17. 

- standardnotes.markdown-visual-editor /4Star/AGPLv3/202208/ts/milkdown
  - https://github.com/standardnotes/app/tree/main/packages/components/src/Packages/Editors/org.standardnotes.markdown-visual-editor
  - https://github.com/standardnotes/markdown-visual
  - A lightweight WYSIWYG markdown editor, derivated from Milkdown editor
  - https://github.com/dec0dOS/standard-notes-ultimate-editor
    - A mobile-friendly and high-performance editor for s-notes

- remirror-react-beautiful-dnd-poc /remirror
  - https://github.com/Collaborne/remirror-react-beautiful-dnd-poc
  - https://collaborne.github.io/remirror-react-beautiful-dnd-poc/
  - Drag and drop the quotes (powered by react-beautiful-dnd) onto this Remirror editor
  - whilst Remirror does support native drag-n-drop events, it doesn't support react-beautiful-dnds Draggables.
  - Our react-beautiful-dnd based solution requires lots of workarounds, that could be confusing to maintain.
    - If your use case for drag-n-drop behaviour is simple, it may be more worthwhile to remove react-beautiful-dnd's abstraction layer, and use the native implementation instead.
# for-design-system
- https://github.com/cultureamp/rich-text-toolkit
  - https://cultureamp.design/storybook/?path=/story/components-rich-text-editor-rich-text-editor--default
  - helpers for building a rich text editor (WYSIWYG) with ProseMirror.
  - If you only need basic rich text editing functions (bold, italics, lists, links)—take a look at the Kaizen Rich Text Editor, which uses these helpers to create a plug-and-play component.
  - https://github.com/cultureamp/kaizen-design-system/tree/master/packages/rich-text-editor

- https://github.com/equinor/fusion-components/tree/master/src/customElements/components/markdown-editor
  - https://equinor.github.io/fusion-components/?path=/story/general-markdown-editor--default
  - 依赖prosemirror、prosemirror-markdown、lit

- https://github.com/gravity-ui/markdown-editor /MIT/202407/ts/设计系统中的一个组件
  - https://preview.gravity-ui.com/md-editor/
  - a powerful tool for working with Markdown, which combines WYSIWYG and Markup modes
  - Support for the basic Markdown and YFM syntax.
  - Extensibility through the use of ProseMirror and CodeMirror engines.
  - 依赖 prosemirror, @diplodoc/transform, react, react-dom, @gravity-ui/uikit, @gravity-ui/components 
# ai-editor(可参考vscode ai)
- novel /13.7kStar/apache2/202501/ts/inactive
  - https://github.com/steven-tey/novel
  - https://novel.sh/
  - Notion-style WYSIWYG editor with AI-powered autocompletion. 
  - 依赖tiptap、@vercel/kv/blob、nextjs、Vercel AI SDK、react-markdown.v8、tailwindcss
  - Slash menu & bubble menu
  - 核心的ai功能: improve writing, shorter/longer, fix-grammer, agi
  - 不支持图片生成， 不支持ask ai
  - Mathematical symbols with LaTeX expression
  - [feat: IS THIS REPO BEING MAINTAINED? _202412](https://github.com/steven-tey/novel/issues/469)
    - No, it is not.
  - [Here’s how AI-powered autocompletion is implemented in Novel, an open-source text editor - DEV Community _202412](https://dev.to/ramunarasinga-11/heres-how-ai-powered-autocompletion-is-implemented-in-novel-an-open-source-text-editor-44oh)

- https://github.com/aieditor-team/AiEditor /1.5kStar/LGPLv2/202506/ts
  - https://gitee.com/aieditor-team/aieditor
  - https://aieditor.dev/
  - https://aieditor.dev/versions.html
  - http://doc.aieditor.com.cn 现代风格（类腾讯文档）
  - https://aieditor.com.cn/zh/demo 经典/传统风格
  - a next-generation rich text editor for AI
  - AI 驱动的开源富文本编辑器， 开箱即用、支持所有前端框架、支持 Markdown 书写模式
  - 目标是打造一个完全由 AI 驱动的富文本编辑器，同时支持对接任意大模型，包括私有的大模型，允许用户使用自己私有的大模型 ApiKey
  - 所有的 AI 功能，都允许用户自定义自己的 prompt，以及扩展的 AI 菜单。
  - 基于 Web Component，因此支持 Layui、Vue、React、Angular 等几乎任何前端框架
  - pro: 还提供了功能更加强大的商业，商业版不限制用户量、不限制应用数量
    - 类 Notion 内容块拖拽， Word 导入/导出， PDF 导出，团队协作编辑， 批注评论功能
  - https://aieditor.dev/price
    - paid: Can remove the logo, collab, word import, local llm

- https://github.com/numerique-gouv/blocknote-llm /202406/ts/inactive
  - https://numerique-gouv.github.io/blocknote-llm/
  - A proof of concept of what can be done with the BlockNote editor based on ProseMirror and an LLM running in the browser
  - Works offline: No data ever leaves your computer
  - This tool is built on top of `WebLLM`, a package that brings language model inference directly onto web browsers with hardware acceleration.
    - To run this, you need a modern browser with support for WebGPU. 
    - We use Llama3, a 8B language model. it takes up 5.2 Gb of storage in the browser's cache.

- https://github.com/taranek/prosemirror-ai-completion /202508/ts
  - https://prosemirror-ai-completion.vercel.app/
  - Prosemirror AI-completion demo
  - 灰色显示修改文字，有打字机效果

- https://github.com/khyamay/prosemirror-speech-to-text /202407/ts
  - https://prosemirror-speech-to-text.vercel.app/
  - basic text to speech menu for prosemirror

- https://github.com/phyohtetarkar/tiptap-block-editor /MIT/202507/ts
  - https://tiptap-block-editor.web.app/
  - Notion style AI-powered block editor build with Tiptap + Vercel AI SDK + Shadcn + Tailwindcss.
  - This template used Gemini as AI model provider. You can change any provider supported by Vercel AI SDK models.

- https://github.com/will-lp1/snowleopard /apache2/202507/ts
  - https://www.cursorforwrit.ing/
  - Cursor for Writing
  - Drizzle schema & migrations, Next.js (App Router)
  - apps/snow-leopard/lib/editor/diff.js: Modified from https://github.com/hamflx/prosemirror-diff/blob/master/src/diff.js

- https://github.com/yyjhao/wrait /202503/ts/inactive
  - https://demo-ai-editor.combini.app/
  - Wrait is a text editor that uses local, in-browser AI with the WebLLM technology.
  - It depends on support for WebGPU in the browser, so e.g., it doesn't work on Safari.
  - 在 src/app/components/ProseMIrror
/proofReadPlugin.ts 使用 diff-match-patch计算差异

- https://github.com/mastra-ai/mastra/blob/main/examples/crypto-chatbot/lib/editor/diff.js
  - 使用diff_match_patch计算差异

## streaming

- https://github.com/gjc14/tiptap-streaming-preview /MIT/202410/ts/inactive
  - A compact demo of streaming Markdown from Google AI Gemini and save to Tiptap Extension demo
  - `/app/extensions/stream/markdown-component.tsx` handling ai call and streaming markdown
  - Dataflow
    - [Tiptap] Send prompt to Streaming Preview extension
    - [StreamingPreview] Get prompt from attributes (node.attrs.prompt)
    - [StreamingPreview] Call Gemini @ai/api/completions with ai-sdk
    - [StreamingPreview] Rendering completion stream
    - [StreamingPreview] Choosing to discard or save the response
    - [StreamingPreview] Transform data and execute editor's api (commands)
    - [Tiptap] Tiptap get's HTML and automatically transform it to visible format

## ai-pattern

- https://github.com/ueberdosis/ai-agent-custom-llm-demos /MIT/202507/ts
  - https://tiptap.dev/docs/content-ai/capabilities/agent/custom-llms/overview
  - Integrate the Tiptap AI Agent extension with a custom backend and AI model provider.
  - 🌰 示例包括: generate, autocomplete(tab), suggest(lint-like), review(diff), agent-sidebar

- https://github.com/continuedev/continue /21.3kStar/apache2/202508/ts
  - https://docs.continue.dev/
  - Continue is the leading open-source AI code assistant. You can connect any models and any context to build custom autocomplete and chat experiences inside VS Code and JetBrains
  - Tab to autocomplete code suggestions
  - [Continue 实现原理 · Pines-Cheng/blog _202505](https://github.com/Pines-Cheng/blog/issues/108)

- https://github.com/gjc14/tiptap-streaming-preview /MIT/202410/ts/Remix
  - A compact demo of streaming Markdown from Google AI Gemini and save to Tiptap Extension demo

## ai-chat

- https://github.com/vercel/ai-chatbot /17.4kStar/apache2/202507/ts/inactive
  - https://github.com/vercel/ai-chatbot/blob/main/lib/editor/diff.js
  - Modified from https://github.com/hamflx/prosemirror-diff/blob/master/src/diff.js

- https://github.com/trendy-design/llmchat /782Star/MIT/202504/ts/inactive
  - https://llmchat.co/
  - Unified interface for AI chat, Agentic workflows and more ...
  - LLMChat.co is a sophisticated AI-powered chatbot platform that prioritizes privacy 
  - LLMChat.co stands out with its workflow orchestration system and focus on privacy, storing all user data locally in the browser using IndexedDB
  - Multiple LLM Provider Support

- https://github.com/RyanLisse/rra-v2 /202506/ts
  - Production-grade RAG Chat Application v2 - Built with Next.js 15, Vercel AI SDK, TailwindCSS v4, and comprehensive testing
  - 使用 diff-match-patch计算差异

- https://github.com/mayneyao/eidos /AGPL/202507/ts
  - https://github.com/mayneyao/eidos/blob/dev/packages/lib/editor/diff.js
  - Modified from https://github.com/hamflx/prosemirror-diff/blob/master/src/diff.js
# editors-collection
- https://github.com/Harbour-Enterprises/SuperDoc /37Star/AGPL/202507/js/vue
  - https://superdoc.dev/
  - open source document editor bringing Microsoft Word capabilities to the web with real-time collaboration, 
  - Self-hostable with Vanilla JS, React, Vue, and more
  - uses: Yjs, FontAwesome, JSZip, and Vite
  - Extensible architecture: Modular design makes it easy to extend, brand, and customize
  - Microsoft Word compatible: View and edit DOCX documents with great import/export, advanced formatting, comments, and tracked changes
  - seamlessly integrates with React, Vue, vanilla JavaScript, and more
  - Real-time collaboration: Features multiplayer editing, live updates, commenting, sharing, and revision history

- licit /37Star/MIT/202507/js
  - https://github.com/MO-Movia/licit
  - http://greathints.com/licit/
  - a feature rich editor based on ProseMirror and an initial foundation of CZI code
  - 典型的适合学术论文的文档
  - 依赖express4、jquery、katex、react
  - 服务端依赖python，实现了协作编辑、图片上传

- czi-prosemirror /304Star/MIT/201906/js/inactive
  - https://github.com/chanzuckerberg/czi-prosemirror
  - Drop-In WYSIWYG editor based on ProseMirror & React

- perry-white /5Star/MIT/202101/ts/inactive
  - https://github.com/openstax/perry-white
  - https://openstax.github.io/perry-white/
  - 只依赖prosemirror、mathlive
  - a fork of licit
  - Perry White was the newspaper editor for Clark Kent in SuperMan.
  - The base editor is ProseMirror.
    - CZI-Prosemirror built on top of that and added React rendering
    - That was extended further by the Licit Editor
    - This fork converts from flow to Typescript, adds a few plugins

- https://github.com/tiptiz/editor /MIT/202503/ts/svelte
  - https://tiptiz.github.io/editor/
  - HTML5 & Email friendly WYSIWYG rich text editor by Tiptap & web comonents (WIP)
  - 基于Svelte和Tiptap实现一个WYSIWYG富文本编辑器，项目的目标是实现一个HTML5 Copy/Paste友好 & Email格式友好 & Markdown友好的WYSIWYG富文本编辑器。 
  - 编辑器将用于个人博客、邮件编辑器、博客文章快速复制粘贴到微信公众号、掘金、知乎等平台发布。

- https://github.com/KID-1912/tiptap-appmsg-editor /202501/js/inactive
  - 基于 tiptap 搭建的微信公众号编辑器示例，支持排版后复制到微信公众平台，支持开发者自己开发样式库、模板库作为内容插入

- https://github.com/alin995/wechat-tiptap /MIT/202311/ts/inactive
  - 一个基于 Tiptap 的 WYSIWYG 编辑器。界面和操作采用微信文档风格，同时提供了AI能力。
  - OpenAI - AI completions

- nib /215Star/GPLv3/202205/ts/inactive
  - https://github.com/nib-edit/nib
  - https://nib-edit.github.io/nib/
  - 高级功能未开源如comment/collab
  - Nib not only has good rich text editing capabilities but also addresses complex editing requirements like tracking changes made to a document, adding comments in document, collaborative editing and more...

- https://github.com/tautastic/ltx /MIT/202504/ts
  - https://ltx.st/
  - efficient and minimalist LaTeX editor. 
  - Creating, saving and sharing LaTeX documents has never been so effortless.

- https://github.com/abdulrahman-mh/textrix /26Star/MIT/202506/ts
  - https://textrix.vercel.app/
  - a rich-text publishing editor inspired by Medium 
  - Unlike most editors, Textrix lets you write, edit, and publish in one place!, Generate a static HTML article or blog post from document that look exactly like they did in the editor
  - Framework-Agnostic: use it with React, Vue, Svelte, Vanilla JS, and more.

- https://github.com/neetozone/neeto-editor /MIT/202507/js
  - https://neeto-editor.neeto.com/
  - The neetoEditor library drives the rich text experience in the neeto products built at BigBinary.

- humhub-prosemirror /17Star/apache2/202505/js
  - https://github.com/humhub/humhub-prosemirror
  - Prosemirror based richtext implementation for the humhub social network
  - 依赖 prosemirror-example-setup、markdown-it

- https://github.com/lynhan318/nextlint /MIT/202404/ts/svelte/inactive
  - https://nextlint-editor.vercel.app/
  - Rich text editor (WYSIWYG) written in Svelte, build on top of tiptap, prosemirror, AI prompt integrated.
  - written in Svelte, using MeltUI headless UI and tailwindcss 
  - The theme tokens are inherited from Svelte Shadcn.

- kangxi-editor /2Star/MIT/202312/ts
  - https://github.com/mgenware/kangxi-editor
  - https://mgenware.github.io/kangxi-editor/
  - Another web-based rich text editor.
  - 只依赖prosemirror，不依赖react
  - 编辑器功能简单

- BrianHung-editor /10Star/NALic/202110/ts/inactive
  - https://github.com/BrianHung/editor
  - https://editor-brianhung.vercel.app/
  - 依赖prosemirror-markdown、codemirror6、katex
  - a rich text editor built upon the ProseMirror framework. 
  - It is based off tiptap and rich-markdown-editor, but tries to stay agnostic to Vue and React.
    - 其实不依赖react、tiptap、rich-markdown-editor

- https://github.com/PeopleWhoListenToStories/sanxi-kit /202507/ts
  - https://sanxi.xulai.fun/
  - A toolkit editor suite based on tiptap and prosemirror.

- https://github.com/ahsanu123/litsi /202501/ts
  - Litsi is an extended markdown editor based on Prosemirror and Lit, with easy to add custom component, inputrules, and dragable element (notion like).

- https://github.com/IsaacAderogba/pine /1Star/MIT/202208/ts
  - https://www.craft.do/s/yE0O3cmWP35qHQ
  - An extensible and headless text-editor framework.
  - Pine is an extensible text-editor framework that prioritizes modularity and performance.
  - Pine adopts an extension system, similar to other prosemirror-based frameworks such as TipTap.

- https://github.com/cesardeazevedo/nostr-editor /MIT/202506/ts
  - nostr-editor is a collection of Tiptap extensions designed to enhance the user experience when creating and editing nostr notes. 
  - It also provides tools for parsing existing notes into a structured content schema.
  - Parse existing nostr events, including imeta tags

- xen-editor /4Star/MIT/202112/ts
  - https://github.com/specup/xen-editor
  - https://specup.github.io/xen-editor
  - Yet another React editor based on Prosemirror

- https://github.com/Mo2men-dev/noqta-editor /MIT/202508/ts
  - https://mo2men-dev.github.io/noqta
  - customizable rich text editor for React. 
  - Clean UI, extensible plugins, and built for modern web apps.
  - WYSIWYG editing with semantic HTML output

- start-editor /4Star/lic/202105/ts
  - https://github.com/NewBuilding/start-editor
  - A rich editor which base on ProseMirror
  - jsx使用jsx-dom转换

- emirror /1Star/MIT/202111/ts
  - https://github.com/bvanjoi/emirror
  - https://emirror.dev/
  - A rich editor toolkit based on ProseMirror.
  - 渲染自定义组件基于`plugin.props.nodeViews`配置

- pubpub-editor /100Star/GPLv2/202003/js/inactive
  - https://github.com/pubpub/pubpub-editor
  - A stand alone, extensible WSIWYG editor based on ProseMirror.
  - https://github.com/pubpub/pubpub/tree/master/client/components/Editor
    - Collaborative Community Publishing
    - 最新的编辑器
  - https://github.com/pubpub/prosemirror-reactive /MIT/202301/ts/NoDeps
    - Reactive documents for Prosemirror
    - This package provides an API modeled on React Hooks for dynamically computing ProseMirror node attributes.
    - This library allows you to define "reactive attributes" on a Node schema that are automatically recomputed as necessary and passed into toDOM (or a NodeView). A "reactive node" is just one that has one or more reactiveAttrs.

- paper-editor /2Star/Apache2/202108/ts/inactive
  - https://github.com/li-yechao/paper-editor
  - A rich editor powered by prosemirror.
  - 整体架构和tiptap/rich-markdown-editor类似
  - 渲染自定义组件基于editorView.props.nodeViews，ReactNodeView的update方法定义在父类，基于ReactDOM.render()
  - CodeBlock.tsx基于MonacoEditor
  - Collaborative powered by prosemirror-collab and Socket. IO
  - Video powered by dashjs and ffmpeg.wasm
  - https://github.com/li-yechao/paper
    - https://paper.yechao.xyz/
    - Paper powered by jsipfs and ProseMirror
  - https://github.com/li-yechao/paper-collab

- https://github.com/tinyrack94/edybara /202504/ts
  - https://edybara.com/
  - Powerfull rich text library for browser, based on ProseMirror

- react-tinacms-editor /ts
  - https://github.com/tinacms/tinacms/blob/main/packages/react-tinacms-editor

- https://github.com/Musery/report_system
  - rjx-wysiwyg 基于 prosemirror和mdast及其相关扩展插件实现的可视化 markdown 语法报表在线编辑和支持docx, pdf格式报表导出

- https://github.com/SeogJongYu/editor-demo
  - Django Backend / React Frontend ，使用@toast-ui/editor.v3

- the-grid-ed /56Star/MIT/201702/js/inactive
  - https://github.com/the-grid/ed
  - https://the-grid.github.io/ed/#fixture
  - Using ProseMirror with data from the Grid API
  - The demo shows translating from ProseMirror to the the Grid API JSON and back.

- https://github.com/RobinJadoul/nuboard
  - A collaborative minimalist latex/math editor, inspired by muboard.
  - 代码量很少

- https://github.com/binary-is/prosearea /202005/js/inactive
  - ProseArea is a drop-in replacement for HTML textareas, providing WYSIWYG editing of markdown, based on the ProseMirror web library.

- https://github.com/adrianheine/ProsePad /25Star/AGPLv3/201909/js/inactive
  - ProsePad is a real-time collaborative text editor like Etherpad, but based on ProseMirror

- https://gitlab.com/smoores/ode /202101/ts/inactive
  - A self-hosted collaborative rich text editor.
  - It's based on Parse Platform, an open source, self-hosted "Complete Application Stack, " and Prosemirror.

- https://github.com/Collaborne/mwc-markdown-editor /202006/inactive
  - A markdown editor following Material Design spec
  - 基于lit-element、@material/mwc-textfield

- https://github.com/grauwoelfchen/vergil /201803/js/inactive
  - An editor written with Inferno + ProseMirror

- https://github.com/rzuppur/rvpe /5Star/MIT/202206/ts/vue3
  - https://rvpe.netlify.app/
  - Minimal rich text editor for Vue 3 based on ProseMirror

- https://github.com/lkiarest/zeditor /2Star/202101/js/inactive
  - https://lkiarest.github.io/zeditor/
  - ProseMirro based Rich Text Editor

- pubsweet/xpub-edit /202111/js/inactive
  - https://gitlab.coko.foundation/pubsweet/pubsweet/-/tree/master/components/client/xpub-edit

- https://github.com/vuau/simplemirror /2Star/MIT/202102/js/inactive
  - A simple and easy to use WYSIWYWG editor based on ProseMirror

- https://github.com/paperbits/paperbits-prosemirror /28Star/MIT/202507/ts
  - Paperbits HTML editor based on ProseMirror.
  - 代码过于简单

- https://github.com/dxos/editor  /1Star/AGPLv3/202101/js/archived
  - Collaborative editor
  - 依赖 react、material-ui、remark-rehype、yjs、prosemirror、hightlight.js

- https://github.com/ubavic/marble-edit 
  - Rich text editor with Latex math support
  - Based on ProseMirror and prosemirror-math
  - 代码过于简单
