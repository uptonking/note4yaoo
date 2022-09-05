---
title: lib-editor-prosemirror-examples
tags: [editor, examples, prosemirror, toc]
created: 2021-07-20T02:14:55.679Z
modified: 2022-08-18T16:57:46.405Z
---

# lib-editor-prosemirror-examples

# guide

- prosemirror-futuristic
  - 方向：collab、markdown、pivot-table、math/formula、media/embed
  - 大部分的方案是以vanillajs为core，react为wrapper
  - toys
    - 尝试保留rich-markdown-editor的api，将core用~~tiptap~~重写
    - 尝试用atlassian editor重写outline，抽象出可替换编辑器的接口，考虑可替换的协作同步方案
    - react indexeddb， 编辑器数据频繁的更新可参考编辑器实时协作的更新

- 💡 vanillajs-first
  - tiptap/dante/wix, bangle.dev, tui.editor.v3
  - guardian-prosemirror-elements/typerighter/invisibles/noting
  - stacks-editor(StackOverflow), syllepsis(字节)
  - milkdown(Typora), jcmnunes-bc-editor(md)
  - start-editor, zeditor, emirror, NotionEditor(toy)

- 💡 react-first
  - remirror, @atlaskit/editor-core, rich-markdown-editor/keyboardnotes
  - wax-prosemirror(coko editor), curvenote-editor(redux), czi/licit(word), perry-white(newspaper)
  - smartblock(202003), xen-editor，nib-edit(高级功能未开源如comment/collab)

- more-prosemirror
  - pageboard/client(页面搭建), noteworthy(solidjs)
  - 建站编辑器应该参考gutenberg、wix
# prosemirror-popular
- tiptap /16.1kStar/MIT/202208/ts
  - https://github.com/ueberdosis/tiptap
  - https://tiptap.dev/
  - https://tiptap.dev/examples/default
  - A headless, framework-agnostic and extendable rich text editor, based on ProseMirror.
  - It’s headless and comes without any CSS. You are in full control over markup, styling and behaviour.

- remirror /1.8kStar/MIT/202208/ts
  - https://github.com/remirror/remirror
  - https://remirror.io/
  - [basic editor demo](https://remirror.vercel.app/?path=/story/editors-wysiwyg--basic)
  - A React toolkit for building cross-platform text editors, based on ProseMirror.
  - I18n support via lingui.
  - Great support for mobile devices.
  - Out-of-the-box editors, or create own by composing extensions.
  - Collaborative editing with yjs or prosemirror-collab.

- @atlaskit/editor-core /8Star/Apache2/202208/ts
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - [kitchen-sink-example](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - A package contains Atlassian editor core functionality
  - 基于react class组件实现
  - 提供了针对image/file的图文混排工具
  - 还提供了多列布局工具，包括两栏、三栏、按比例、居中
  - 提供了语法树ADF显示
  - https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
    - copy the approach by Atlassian editor_v20201205
  - ref
    - https://github.com/TeemuKoivisto/prosemirror-track-changes-example
    - https://github.com/pioug/atlassian-frontend-mirror

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

- notitap /39Star/MIT/202209/ts
  - https://github.com/sereneinserenade/notitap
  - https://sereneinserenade.github.io/notitap/
  - 依赖daisyui、tippyjs、floating-ui、fuzzysort
  - Notion like editor built on top of tiptap.
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但list item不支持拖入拖出

- bangle.dev-editor /527Star/MIT/202208/ts
  - https://github.com/bangle-io/bangle.dev
  - https://bangle.dev/docs/examples/markdown-editor
  - https://app.bangle.io/
  - 支持拖拽标题section，但不支持拖拽section内的段落
  - 使用了浏览器文件系统api来支持打开本地文件
  - Collection of higher level rich text editing tools. It powers the local only note taking app https://bangle.io
  - bangle.io /711Star/AGPL.v3/202208/ts
    - https://github.com/bangle-io/bangle-io
    - https://bangle.io/
    - A web only WYSIWYG note taking app that saves notes locally in markdown format

- tui.editor.v3 /15.1kStar/MIT/202208/ts/popular
  - https://github.com/nhn/tui.editor
  - http://ui.toast.com/tui-editor
  - 👀 v3新版本迁移到了prosemirror
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

- wax-prosemirror /9Star/MIT/202208/js
  - https://gitlab.coko.foundation/wax/wax-prosemirror
  - https://waxjs.net/docs/wax/
  - http://wax-demo.coko.foundation/
  - https://waxjs.net/features/
  - 提供了丰富示例，包括编辑器内带下拉框的表单、脚注面板浮层、Track changes
  - 👀 支持评论，评论卡片可与编辑器内容水平对齐，但被评论文本不支持部分重叠
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

- curvenote-editor /140Star/MIT/202208/ts
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

- guardian-prosemirror-elements /21Star/MIT/202208/ts
  - https://github.com/guardian/prosemirror-elements
  - This Prosemirror plugin adds the ability to add custom 'elements' to a document.
  - 使用prosemirror编辑器作为NodeViews，嵌套多实例编辑器
  - Prosemirror-elements provides a way of expressing an Element and its Fields in the UI framework of your choice, and we provide React bindings as a default.
  - What is an Element?
    - Modelling non-text content in Prosemirror can be tricky. 
    - Elements contain user-defined Fields that can model many different kinds of content, including rich text fields and arbitrary data.
    - Each Element is made up of Fields, which represent a data type – for example, text, rich text, or custom data types.

- Stacks-Editor /218Star/MIT/202208/ts
  - https://github.com/StackExchange/Stacks-Editor
  - https://editor.stackoverflow.design/
  - Stacks-Editor is a combination rich text/markdown editor that powers Stack Overflow's post editing experience.
  - 依赖prosemirror, hightlight.js、markdown-it、@lezer/markdown、stacks-ui，不依赖react
  - 全部基于es6 class，[new EditorView()](https://github.com/StackExchange/Stacks-Editor/blob/481492297f680472c51e57c981f050133681edc6/src/rich-text/editor.ts#L76)的过程非常标准，无封装

- syllepsis /187Star/MIT/202208/ts/字节/参考中文支持
  - https://github.com/bytedance/syllepsis
  - https://bytedance.github.io/syllepsis/#/zh-cn/about
  - [编辑器在线例子](https://bytedance.github.io/syllepsis/#/zh-cn/playground)
  - 支持格式刷、调整文字间距、段落间距
  - 支持[Card或Block插件](https://bytedance.github.io/syllepsis/#/zh-cn/chapters/card-plugin)，但不支持拖拽
  - 设计了占位插件，可实现左侧加号按钮
  - rich text editor compatible with mainstream modern browsers.
  - We re-encapsulate Prosemirror to provide more concise APIs, a large number of basic plugins
  - https://github.com/lastnigtic/syllepsis-collab
    - Example of `Syllepsis` collaborative editing using `prosemirror-collab`

- zotero-note-editor /16Star/AGPL.v3/202208/js
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

- taleweaver(织书) /90Star/MIT/202008/ts
  - https://github.com/yuzhenmi/taleweaver
  - https://yuzhenmi.github.io/taleweaver/
  - Web word processor for 2Tale Writer's Portal.
  - 👀 基于dom实现，且支持显示分页
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

- wode /3Star/MIT/202206/ts
  - https://github.com/wenerme/wode
  - https://wode.vercel.app/tiptap
  - TipTap based Google Doc
  - 实现了预定义2/3多栏布局，但不work
  - google采用canval好象是为了解决浏览器兼容性方面的问题。因为在dom在不同浏览器上表现差别确实大，大到它都不再维护直接换成canvas了。

- jcmnunes-editor /5Star/MIT/202203/ts
  - https://github.com/jcmnunes/editor
  - https://editor.binarycapsule.tech/
  - 功能简单，短小精悍
  - Prosemirror based text editor with markdown shortcuts and serialization
  - It is highly inspired by rich-markdown-editor, linear-app-editor

- gem /10Star/MIT/202205/ts/代码量少
  - https://github.com/tanishqkancharla/gem
  - https://gem.tanishqkancharla.dev/
  - 只依赖prosemirror，不依赖react
  - Gem (previously called Editor) is a performant and simple plain text editor, 
  - The design is very inpsired by Paco Coursey's [Writer]().
  - [Gem, a plain-text editor based on prosemirror_202111](https://discuss.prosemirror.net/t/gem-a-plain-text-editor-based-on-prosemirror/4231)
    - I worked on moving to codemirror 6 
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

- Xheldon/NotionEditor /30Star/GPL.v2/202103/ts/inactive
  - https://github.com/Xheldon/NotionEditor
  - A Notion's editor implement based on ProseMirror, just for feasibility studies.
  - 不允许跨 block 选择部分文本内容
  - 依赖 redux、lodash
  - 基础 schema 是两个 doc 和 text, 这是 Prosemirror 默认的两个最大和最小可编辑 schema. 而设计 schema 的时候我使用的最小编辑单元是 textblock, 表现形式是一个 div 中包含着 text
  - 所有的元素都是使用 div 进行模拟, 而不是使用语义化的 p/ul/ol 等进行, 这是为了摆脱浏览器的限制, 如段落嵌套段落的时候, p 标签无法嵌套块级元素等.
  - 使用了 React 构建界面的有: Slash

- manuscript-editor /7Star/apache2/202208/ts
  - https://gitlab.com/mpapp-public/manuscripts-manuscript-editor
  - https://gitlab.com/mpapp-public/manuscripts-frontend
    - /CPAL-1.0; 类似MPL
  - A React + ProseMirror editor for manuscripts.
  - 编辑器依赖prosemirror、@jupyterlab/services、codemirror5、popperjs、react-dnd
  - 编辑器样式采用论文简洁风格，支持 摘要、脚注、交叉引用、评论
  - Manuscripts.io web frontend which makes API calls to manuscripts-api and manuscripts-sync
  - This repository contains the browser client for the Manuscripts collaborative authoring environment, in a single-page React app (desktop and mobile app embeddable using cocos).
  - ref
    - https://gitlab.com/mpapp-public/manuscripts-api
    - https://gitlab.com/mpapp-public/manuscripts-sync
    - https://gitlab.com/mpapp-public/manuscripts-data
    - https://gitlab.com/mpapp-public/manuscripts-examples
  - [Manuscripts.io is a ProseMirror-based editor in a React application_202011](https://discuss.prosemirror.net/t/manuscripts-io/3299), 
    - served as a PWA that works offline and can be installed as a desktop application via Chrome.
    - instead of using ProseMirror’s standard collaboration plugin, 👉🏻 Manuscripts serializes each block of the document to a JSON object with an id, which is stored in the browser’s local storage (IndexedDB) using RxDB/PouchDB and then synced with Couchbase via Sync Gateway, which handles permissions and validates each object according to a defined schema. 
    - Manuscripts.io 64 is built by a team within Atypon; Atypon成立于1996年，是一家为全球期刊发展服务的软件系统公司，Atypon旗下出版平台Literatum为全球近100000本期刊和919家出版商网站、45%的英文同行评审学术期刊和其他语种的出版物提供服务。
    - Conflict resolution is handled in each client, with any conflicting changes in the document’s content presented to the user for them to choose the most appropriate resolution.
    - Collaboration in Manuscripts.io 64 works at the project level — each project can contain several manuscripts — and collaborators can either be responsible for editing parts of the document or can simply comment by adding annotations to blocks or ranges of the manuscript.
    - Manuscripts.io 64 includes some innovations: figures that can be (re)generated dynamically by evaluating code in a hosted Jupyter kernel; built-in searching of online reference databases; configurable paragraph, section and inline styles, and output to multiple formats (DOCX, PDF, JATS XML, HTML, and others).

- use-prosemirror /321Star/MIT/202201/ts
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

- reprose /2Star/MIT/202109/ts
  - https://github.com/riboseinc/reprose
  - Configurable ProseMirror instance as a React component
  - Provides tools and patterns that simplify rendering a document to HTML
  - 渲染自定义组件基于`plugin.props.nodeViews`配置
  - 将插件的功能分为编写author和显示schema两部分
  - Reprose’s functionality is contained in features. 
  - A feature can provide schema aspects (nodes, marks), and authoring aspects (key bindings, menu items, ProseMirror plugins).

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
- prosemirror-dev-tools /241Star/MIT/202106/js
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
# tiptap/milkdown/remirror/atlassian/wax
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

- nextcloud-text /366Star/AGPL.v3/202208/js/vue/tiptap/php
  - https://github.com/nextcloud/text
  - Collaborative document editing using Markdown
  - 依赖tiptap.v2, @_ueberdosis/prosemirror-tables.v1.1.3, markdown-it、vue2、vuex3

- standardnotes.markdown-visual-editor /4Star/AGPL.v3/202208/ts/milkdown
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
# prosemirror-editors-for-design-system
- https://github.com/cultureamp/rich-text-toolkit
  - helpers for building a rich text editor (WYSIWYG) with ProseMirror.
  - If you only need basic rich text editing functions (bold, italics, lists, links)—take a look at the Kaizen Rich Text Editor, which uses these helpers to create a plug-and-play component.
  - https://github.com/cultureamp/kaizen-design-system/tree/master/packages/rich-text-editor
  - https://cultureamp.design/storybook/?path=/story/components-rich-text-editor-rich-text-editor--default

- https://github.com/equinor/fusion-components/tree/master/src/customElements/components/markdown-editor
  - https://equinor.github.io/fusion-components/?path=/story/general-markdown-editor--default
# prosemirror-editors-collection
- licit /33Star/MIT/202208/js
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

- nib /215Star/GPL.v3/202205/ts
  - https://github.com/nib-edit/nib
  - https://nib-edit.github.io/nib/
  - 高级功能未开源如comment/collab
  - Nib not only has good rich text editing capabilities but also addresses complex editing requirements like tracking changes made to a document, adding comments in document, collaborative editing and more...

- humhub-prosemirror /15Star/Apache2/202108/js
  - https://github.com/humhub/humhub-prosemirror
  - Prosemirror based richtext implementation for the humhub social network
  - 依赖 prosemirror-example-setup、markdown-it

- kangxi-editor /2Star/MIT/202208/ts
  - https://github.com/mgenware/kangxi-editor
  - https://mgenware.github.io/kangxi-editor/
  - Another web-based rich text editor.
  - 只依赖prosemirror，不依赖react
  - 编辑器功能简单

- BrianHung-editor /10Star/NALic/202110/ts/inactive
  - https://github.com/BrianHung/editor
  - https://editor-brianhung.vercel.app/
  - 依赖prosemirror-markdown、codemirror6、katex，不依赖react、tiptap、rich-markdown-editor
  - a rich text editor built upon the ProseMirror framework. 
  - It is based off tiptap and rich-markdown-editor, but tries to stay agnostic to Vue and React.

- https://github.com/IsaacAderogba/pine /1Star/MIT/202208/ts
  - https://www.craft.do/s/yE0O3cmWP35qHQ
  - An extensible and headless text-editor framework.
  - Pine is an extensible text-editor framework that prioritizes modularity and performance.
  - Pine adopts an extension system, similar to other prosemirror-based frameworks such as TipTap.

- xen-editor /4Star/MIT/202112/ts
  - https://github.com/specup/xen-editor
  - https://specup.github.io/xen-editor
  - Yet another React editor based on Prosemirror

- start-editor /4Star/lic/202105/ts
  - https://github.com/NewBuilding/start-editor
  - A rich editor which base on ProseMirror
  - jsx使用jsx-dom转换

- emirror /1Star/MIT/202111/ts
  - https://github.com/bvanjoi/emirror
  - https://emirror.dev/
  - A rich editor toolkit based on ProseMirror.
  - 渲染自定义组件基于`plugin.props.nodeViews`配置

- paper-editor /2Star/Apache2/202108/ts/inactive
  - https://github.com/li-yechao/paper-editor
  - A rich editor powered by prosemirror.
  - 整体架构和tiptap/rich-markdown-editor类似
  - 渲染自定义组件基于editorView.props.nodeViews，ReactNodeView的update方法定义在父类，基于ReactDOM.render()
  - CodeBlock.tsx基于MonacoEditor
  - Collaborative powered by prosemirror-collab and Socket. IO
  - Video powered by dashjs and ffmpeg.wasm
  - ref
    - https://github.com/li-yechao/paper
      - https://paper.yechao.xyz/
      - Paper powered by jsipfs and ProseMirror
    - https://github.com/li-yechao/paper-collab

- react-tinacms-editor /ts
  - https://github.com/tinacms/tinacms/blob/main/packages/react-tinacms-editor

- https://github.com/humhub/humhub-prosemirror /202205/js
  - 打包使用grunt

- https://github.com/Musery/report_system
  - rjx-wysiwyg 基于 prosemirror和mdast及其相关扩展插件实现的可视化 markdown 语法报表在线编辑和支持docx, pdf格式报表导出

- https://github.com/SeogJongYu/editor-demo
  - Django Backend / React Frontend ，使用@toast-ui/editor.v3

- pubpub-editor /100Star/GPL.v2/202003/js/inactive
  - https://github.com/pubpub/pubpub-editor
  - A stand alone, extensible WSIWYG editor based on ProseMirror.
  - https://github.com/pubpub/pubpub/tree/master/client/components/Editor
    - Collaborative Community Publishing
    - 最新的编辑器
  - https://github.com/pubpub/prosemirror-reactive /NoDeps
    - Reactive documents for Prosemirror

- the-grid-ed /56Star/MIT/201702/js/inactive
  - https://github.com/the-grid/ed
  - https://the-grid.github.io/ed/#fixture
  - Using ProseMirror with data from the Grid API
  - The demo shows translating from ProseMirror to the the Grid API JSON and back.

- https://github.com/binary-is/prosearea /202005/js/inactive
  - ProseArea is a drop-in replacement for HTML textareas, providing WYSIWYG editing of markdown, based on the ProseMirror web library.

- https://github.com/adrianheine/ProsePad /25Star/AGPL.v3/201909/js/inactive
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

- https://github.com/paperbits/paperbits-prosemirror
  - Paperbits HTML editor based on ProseMirror.
  - 代码过于简单

- https://github.com/dxos/editor  /1Star/AGPLv3/202101/js/archived
  - Collaborative editor
  - 依赖 react、material-ui、remark-rehype、yjs、prosemirror、hightlight.js

- https://github.com/ubavic/marble-edit 
  - Rich text editor with Latex math support
  - Based on ProseMiror and prosemirror-math
  - 代码过于简单
