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
    - 尝试用atlassian editor重写outline，抽象出替换可编辑器的接口，考虑可替换的协作同步方案
    - react indexeddb， 编辑器数据频繁的更新可参考编辑器实时协作的更新

- 💡 vanillajs-first
  - tiptap/dante/wix, bangle.dev, tui.editor.v3, stacks-editor(StackOverflow)
  - guardian-prosemirror-typerighter/elements/invisibles/noting
  - milkdown(Typora), syllepsis(字节), pubpub-editor(202003)
  - start-editor, jcmnunes-bc-editor(md), zeditor, emirror, NotionEditor(toy)

- 💡 react-first
  - remirror, rich-markdown-editor/keyboardnotes, @atlaskit/editor-core
  - wax-prosemirror(coko editor), curvenote-editor(redux), czi/licit(word), perry-white(newspaper)
  - smartblock(202003), xen-editor，nib-edit(高级功能未开源如comment/collab)

- more-prosemirror
  - pageboard/client(页面搭建), noteworthy(solidjs)
  - 建站编辑器应该参考gutenberg、wix
# prosemirror-popular
- tiptap /16.1kStar/MIT/202208/ts/prosemirror
  - https://github.com/ueberdosis/tiptap
  - https://tiptap.dev/
  - https://tiptap.dev/examples/default
  - A headless, framework-agnostic and extendable rich text editor, based on ProseMirror.
  - It’s headless and comes without any CSS. You are in full control over markup, styling and behaviour.
  - ref
    - https://github.com/ueberdosis/awesome-tiptap

- remirror /1.8kStar/MIT/202208/ts
  - https://github.com/remirror/remirror
  - https://remirror.io/
  - https://remirror.vercel.app/?path=/story/editors-wysiwyg--basic
  - A React toolkit for building cross-platform text editors, based on ProseMirror.
  - I18n support via lingui.
  - Great support for mobile devices.
  - Out-of-the-box editors, or create own by composing extensions.
  - Collaborative editing with yjs or prosemirror-collab.

- @atlaskit/editor-core /Apache2/ts
  - https://bitbucket.org/atlassian/atlassian-frontend-mirror/src/master/editor/
  - [kitchen-sink-example](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - A package contains Atlassian editor core functionality
  - 基于react class组件实现
  - 提供了针对image/file的图文混排工具
  - 还提供了多列布局工具，包括两栏、三栏、按比例、居中
  - 提供了语法树ADF显示
- https://github.com/TeemuKoivisto/prosemirror-react-typescript-example
  - copy the approach by Atlassian editor_v20201205
  - https://github.com/TeemuKoivisto/prosemirror-track-changes-example

- bangle-editor /527Star/MIT/202208/ts
  - https://github.com/bangle-io/bangle.dev
  - https://bangle.dev/docs/examples/markdown-editor
  - Collection of higher level rich text editing tools. It powers the local only note taking app https://bangle.io
- bangle.io /711Star/AGPL.v3/202208/ts
  - https://github.com/bangle-io/bangle-io
  - https://bangle.io/
  - A web only WYSIWYG note taking app that saves notes locally in markdown format

- wax-prosemirror /9Star/MIT/202208/js
  - https://gitlab.coko.foundation/wax/wax-prosemirror
  - http://wax-demo.coko.foundation/
  - https://waxjs.net/docs/wax/
  - Wax depends on the following libraries.
    - React for the view(UI)
    - Styled-components for theming and styling.
    - Inversify.io as service containers，用的不多，可剥离
  - 依赖注入使用了很多class
  - 大量使用react组件
  - ref
    - https://github.com/christos8333/wax-prosemirror
    - licit也是适合论文的编辑器

- curvenote-editor /140Star/MIT/202208/ts
  - https://github.com/curvenote/editor
  - https://curvenote.com/
  - 依赖 redux-toolkit、codemirror.v5、material-ui.v4、date-fns
  - 支持 footnote、comment、latex
  - interactive scientific editor built with ProseMirror, React and Redux
  - A collaborative, rich text editor for interactive technical & scientific content., implementing the MyST standard, and integrating with JupyterLab, JupyterBook and Sphinx. 
  - We aim to lower the barriers to writing computational narratives.
    - Today, narrative is often moved out of computational notebooks into static document creation tools (Microsoft Word, Google Docs, LaTeX, Slides/PPT).

- tui.editor.v3 /11.8kStar/MIT/202009/popular
  - https://github.com/nhn/tui.editor
  - http://ui.toast.com/tui-editor
  - 👀 v3新版本迁移到了prosemirror
  - core只依赖 codemirror5，另外提供了react/vue-editor
  - 只依赖prosemirror，mark解析自己实现了toastmark，公司还自研了很多ui组件
  - 全都是vanillajs，react的封装很薄，只有3文件
  - 代码复杂度高
  - 支持通过代码块中的图表配置信息生成图表
    - [example: Editor with Chart Plugin](https://nhn.github.io/tui.editor/latest/tutorial-example07-editor-with-chart-plugin)
    - Markdown WYSIWYG Editor. 
    - GFM Standard + Chart & UML Extensible.
    - 编辑器支持：chart、uml、语法高亮、合并单元格、自定义toolbar、i18n、theming

- syllepsis /187Star/MIT/202208/ts/字节
  - https://github.com/bytedance/syllepsis
  - https://bytedance.github.io/syllepsis/#/
  - rich text editor compatible with mainstream modern browsers.
  - We re-encapsulate Prosemirror to provide more concise APIs, a large number of basic plugins
  - https://github.com/lastnigtic/syllepsis-collab
    - Example of `Syllepsis` collaborative editing using `prosemirror-collab`

- gitlab editor /js/vue2/tiptap.v2
  - https://gitlab.com/gitlab-org/gitlab/-/tree/master/app/assets/javascripts/content_editor
  - [WYSIWYG editor toolkit architecture proposal__2021](https://gitlab.com/gitlab-org/gitlab/-/issues/273238)
    - implementing support for all of md flavors is an unnecessary cost.
    - Solution 1: Traceability or file diffs
    - Solution 2: Relying on the Markdown preview endpoint

- guardian-prosemirror-elements /21Star/MIT/202208/ts
  - https://github.com/guardian/prosemirror-elements
  - This Prosemirror plugin adds the ability to add custom 'elements' to a document.
    - Modelling non-text content in Prosemirror can be tricky. 
    - it provides an abstraction that makes it easy to write custom elements
  - A ProseMirror plugin for adding user-defined 'elements' containing arbitrary fields to a document.
  - renderer-agnostic (we use React as a default)

- Stacks-Editor /218Star/MIT/202208/ts
  - https://github.com/StackExchange/Stacks-Editor
  - https://editor.stackoverflow.design/
  - Stacks-Editor is a combination rich text/markdown editor that powers Stack Overflow's post editing experience.
  - 依赖prosemirror, hightlight.js、markdown-it、@lezer/markdown、stacks-ui，不依赖react
  - 全部基于es6 class，[new EditorView()](https://github.com/StackExchange/Stacks-Editor/blob/481492297f680472c51e57c981f050133681edc6/src/rich-text/editor.ts#L76)的过程非常标准，无封装

- noteworthy /166Star/AGPL.v3/202207/ts
  - https://github.com/benrbray/noteworthy
  - https://noteworthy.ink/
  - Markdown editor with bidirectional links and excellent math support
  - 依赖solid-js、remark13、prosemirror、electron-window-state、remark
  - 参考了prosemirror、zettlr、vscode、notable
    - Thanks to Fabio Spampinato for releasing the source to an early version Notable!
  - https://github.com/benrbray/prosemirror-math

- taleweaver(织书) /71Star/MIT/202007/ts
  - https://github.com/yuzhenmi/taleweaver
  - https://yuzhenmi.github.io/taleweaver/
  - Web word processor for 2Tale Writer's Portal.
  - feature
    - 基于dom实现，且支持显示分页
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
  - https://wode.vercel.app/
  - TipTap based Google Doc
  - google采用canval好象是为了解决浏览器兼容性方面的问题。因为在dom在不同浏览器上表现差别确实大，大到它都不再维护直接换成canvas了。

- smartblock /249Star/MIT/202003/ts/inactive/prosemirror
  - https://github.com/appleple/smartblock
  - https://appleple.github.io/smartblock/
  - 依赖prosemirror、codemirror5、react-highlight.js、react-svg、styled-components
  - 支持跨block选择部分文字
  - 不支持拖拽block修改顺序，但有上下箭头按钮
  - intuitive block based wysiwyg editor built with React and ProseMirror

- NotionEditor /30Star/GPL.v2/202103/ts/inactive
  - https://github.com/Xheldon/NotionEditor
  - A Notion's editor implement based on ProseMirror, just for feasibility studies.
  - 不允许跨 block 选择部分文本内容
  - 基础 schema 是两个 doc 和 text, 这是 Prosemirror 默认的两个最大和最小可编辑 schema. 而设计 schema 的时候我使用的最小编辑单元是 textblock, 表现形式是一个 div 中包含着 text
  - 所有的元素都是使用 div 进行模拟, 而不是使用语义化的 p/ul/ol 等进行, 这是为了摆脱浏览器的限制, 如段落嵌套段落的时候, p 标签无法嵌套块级元素等.
  - 使用了 React 构建界面的有: Slash

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

- https://github.com/shobokshy/rpm-editor /1Star/MIT/202201/ts
  - A React renderless rich text editor component.
  - 只依赖prosemirror、react
  - 没有提供使用示例

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
    - https://github.com/luke-john-atlassian/prosemirror-devtools
# tiptap/remirror/milkdown
- better-virgool /9Star/MIT/NALic/202208/ts
  - https://github.com/ahhshm/better-virgool
  - https://ahhshm.github.io/better-virgool/
  - An attempt to create a better rich text editor than virgool.io. Powered by Tiptap and ProseMirror
  - 实现了RTL国际化方向

- element-tiptap /825Star/MIT/202208/ts/vue/inactive
  - https://github.com/Leecason/element-tiptap
  - https://element-tiptap.vercel.app/
  - WYSIWYG rich-text editor using tiptap and Element UI for Vue2 (tiptap2 and Vue3 is in alpha)
  - new version2 support Vue3, use tiptap2 and Element Plus

- https://github.com/ueberdosis/tiptap-php
  - A PHP package to work with Tiptap content. 
  - You can transform Tiptap-compatible JSON to HTML, and the other way around, sanitize your content, or just modify it.

- nextcloud-text /366Star/AGPL.v3/202208/js/php
  - https://github.com/nextcloud/text
  - Collaborative document editing using Markdown
  - 依赖tiptap.v2, @_ueberdosis/prosemirror-tables.v1.1.3, markdown-it、vue2、vuex3

- standardnotes.markdown-visual-editor /4Star/AGPL.v3/202208/ts
  - https://github.com/standardnotes/app/tree/main/packages/components/src/Packages/Editors/org.standardnotes.markdown-visual-editor
  - https://github.com/standardnotes/markdown-visual
  - A lightweight WYSIWYG markdown editor, derivated from Milkdown editor
  - https://github.com/dec0dOS/standard-notes-ultimate-editor
    - A mobile-friendly and high-performance editor for s-notes

- https://github.com/Collaborne/remirror-react-beautiful-dnd-poc
  - https://collaborne.github.io/remirror-react-beautiful-dnd-poc/
  - Drag and drop the quotes (powered by react-beautiful-dnd) onto this Remirror editor
  - whilst Remirror does support native drag-n-drop events, it doesn't support react-beautiful-dnds Draggables.
  - Our react-beautiful-dnd based solution requires lots of workarounds, that could be confusing to maintain.
    - If your use case for drag-n-drop behaviour is simple, it may be more worthwhile to remove react-beautiful-dnd's abstraction layer, and use the native implementation instead.
# prosemirror-editor-collection
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

- jcmnunes-editor /5Star/MIT/202203/ts
  - https://github.com/jcmnunes/editor
  - https://editor.binarycapsule.tech/
  - 功能简单，短小精悍
  - Prosemirror based text editor with markdown shortcuts and serialization
  - It is highly inspired by rich-markdown-editor, linear-app-editor

- gem /10Star/MIT/202205/ts/代码量少
  - https://github.com/tanishqkancharla/gem
  - Gem (previously called Editor) is a performant and simple plain text editor, 
  - The design is very inpsired by Paco Coursey's [Writer](https://github.com/pacocoursey/writer).
  - 只依赖prosemirror，不依赖react

- BrianHung-editor /202110/ts/inactive
  - https://github.com/BrianHung/editor
  - https://editor-brianhung.vercel.app/
  - 依赖prosemirror-markdown、codemirror6、katex，不依赖react、tiptap、rich-markdown-editor
  - a rich text editor built upon the ProseMirror framework. 
  - It is based off tiptap and rich-markdown-editor, but tries to stay agnostic to Vue and React.

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

- react-tinacms-editor
  - https://github.com/tinacms/tinacms/blob/main/packages/react-tinacms-editor
  - 基于ts

- https://github.com/humhub/humhub-prosemirror /202205/js
  - 打包使用grunt

- pubpub-editor /100Star/GPL.v2/202003/js/inactive
  - https://github.com/pubpub/pubpub-editor
  - A stand alone, extensible WSIWYG editor based on ProseMirror.
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

- https://gitlab.com/smoores/ode /inactive
  - A self-hosted collaborative rich text editor.
  - It's based on Parse Platform, an open source, self-hosted "Complete Application Stack, " and Prosemirror, a rich text editor toolkit.

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

- pubsweet/xpub-edit /inactive
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
