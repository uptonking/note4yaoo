---
title: toc-lib-editor-text-code-prosemirror-codemirror
tags: [code-editor, codemirror, prosemirror, text-editor, toc]
created: 2021-05-14T10:28:05.856Z
modified: 2021-07-08T12:37:23.562Z
---

# toc-lib-editor-text-code-prosemirror-codemirror

# guide

- monaco-editor-pros
  - 来自vscode，代码编辑功能强大，有大公司支持
  - 支持 language server protocol

- monaco-editor-cons
  - 体积大、复杂度高
  - 设计目标是ide，而不是纯粹的代码编辑器
  - 不支持mobile
  - 引入项目比较麻烦，不能直接简单的import，webpack要使用专门的plugin，如cra无法直接使用

- top-dependents-of-prosemirror
  - prosemirror-collab
  - @tiptap/core v2
  - @atlaskit/editor-core
  - rich-markdown-editor
  - @remirror/core

- top-dependents-of-codemirror.v5
  - react-codemirror
  - @toast-ui/editor
  - tui-editor
  - admin-lte
  - @jupyterlab/codemirror
  - grapesjs
  - @uiw/react-codemirror
  - playroom

- top-dependents-of-codemirror.v6
  - @codemirror/collab
  - @eldonlabs/autocomplete: 也是官方扩展
  - @codesandbox/sandpack-react: 依赖的sandpack-client(不依赖codemirror)
  - react-tools-codemirror: codemirror6的react组件封装
  - @writewithocto/ink: 原地预览样式的编辑器
  - markword: A WYSIWYG markdown syntax set for Codemirror 6

- ref
  - [html editors](https://gist.github.com/manigandham/65543a0bc2bf7006a487)
  - [codemirror6 vs prosemirror vs editorjs](https://www.npmtrends.com/@editorjs/editorjs-vs-@codemirror/state-vs-prosemirror-state-vs-monaco-editor-vs-codemirror)
  - https://bangle.io/ 编辑器的折叠体验很好，链接编辑也好
  - Abstracted Editors
    - These use separate document structures instead of HTML, 
    - some are more modular libraries than full editors
  - Dom-Based Editors
    - eg, tinymce,medium-editor,froala
# text-editor
- https://github.com/ProseMirror/prosemirror
  - http://prosemirror.net/
  - /5.1kStar/MIT/202002/js
  - rich semantic content editor based on contentEditable, with support for collaborative editing and custom document schemas.
  - ProseMirror library consists of a number of separate modules.

- https://github.com/ianstormtaylor/slate
  - https://docs.slatejs.org/general/changelog
  - /18.6kStar/MIT/202009/ts/react
  - a completely customizable framework for building rich text editors.
  - since v0.50.0(201911), slate codebase has had a complete overhaul(彻底检修)
    - The data model is now comprised of simple JSON objects.(old: Immutable.js data structures)
    - The codebase now uses TypeScript. 
    - Plugins are now plain functions that augment the Editor object they receive and return it again.

- https://github.com/tbhuabi/textbus
  - /150Star/GPL/202011/ts
  - 依赖prismjs、rxjs、reflect-metadata、@tanbo/di, @tanbo/css-themes, @tanbo/color
  - 基于数据驱动的富文本编辑器
  - 为什么我还要另起炉灶呢？
    - 目前大多数富文本内容都太脏了，比如，加粗一段文字，可能是一个 strong 标签，也有可能是多个，如果这段文字同时还有其它格式，那么就更热闹了
    - 较新的编辑器，基本都有自己的一套抽象数据结构来描述富文本，这同时又引起了另一个问题，即这一数据结构对有的富文本内容描述不了，导致要扩展特定的格式不能实现。
    - 部分富文本编辑器依赖特定的框架或库，造成使用上的限制
    - 实时的代码高亮，这个对程序员写文档来说，比较重要
    - 对于粘贴进来的内容，要么粗爆的只是提取文本内容，导致格式丢失。要么就直接扔进页面，产生非常多的脏数据（如粘贴 word 的内容）
  - TextBus 解决如下
    - 输出非常干净，没有冗余的标签及样式。
    - 没有定义一个标准的数据结构，只抽象出了 Formatter（格式） 和 Component（组件）两个维度的数据来格式化富文本的 Content（内容）
    - 不依赖特定的库
    - 实时代码高亮
    - 由于TextBus的架构设计天然的支持过滤脏内容，所以，当粘贴进 TextBus 不认识的数据时，会自动忽略掉
    - 粘贴进来的资源上传，目前正在开发中
# code-editor
- https://github.com/codemirror/CodeMirror
  - /21.3kStar/MIT/202010/js
  - In-browser code editor
  - CodeMirror 6 is a rewrite of the CodeMirror code editor. 
  - The new system provides solid accessibility, touchscreen support, better content analysis
  - It is not API-compatible with the old code.
- https://github.com/writewithocto/ink
  - https://octo.app/tags/examples
  - A plain-text javascript markdown editor library that renders formatting live and in-place without the need for a preview pane. 
  - Built on CodeMirror 6. Powers https://octo.app/
# prosemirror-examples
- 研发方向：markdown、collab协作、data-grid、codeblock
- **vanillajs-first**
  - tiptap/dante, tui.editor.v3, remirror, emirror
  - guardian-prosemirror-typerighter/elements/invisibles/noting, stacks-editor(StackOverflow)
  - milkdown(Typora), bangle.dev, pubpub-editor(202003)
  - start-editor, jcmnunes-bc-editor(md), zeditor
  - y-prosemirror, NotionEditor(toy)
- **react-first**
  - rich-markdown-editor/keyboardnotes, @atlaskit/editor-core, wax-prosemirror, xkeditor-next(r-m-e)
  - curvenote-editor(redux), czi-prosemirror(201906), licit(word), perry-white(newspaper)
  - Aditor, smartblock(202003), xen-editor(vanillajs为主，代码不多)，nib-edit(高级功能未开源如comment/collab)
- more-editor
  - pageboard/client(页面搭建), noteworthy(solidjs)

- https://github.com/jcmnunes/editor
  - https://editor.binarycapsule.tech/
  - 功能简单，短小精悍
  - Prosemirror based text editor with markdown shortcuts and serialization
  - It is highly inspired by rich-markdown-editor, linear-app-editor

- https://github.com/benrbray/noteworthy
  - Markdown editor with bidirectional links and excellent math support
  - 参考了prosemirror、zettlr、vscode、notable
  - 依赖solid-js、remark13、prosemirror、electron-window-state

- https://github.com/StackExchange/Stacks-Editor
  - Stack Overflow's Combination Rich Text/Markdown Editor
  - 依赖prosemirror, hightlight.js，不依赖react
  - 全部基于es6 class，[new EditorView()](https://github.com/StackExchange/Stacks-Editor/blob/481492297f680472c51e57c981f050133681edc6/src/rich-text/editor.ts#L76)的过程非常标准，无封装

- https://github.com/openstax/perry-white
  - https://openstax.github.io/perry-white/
  - 只依赖prosemirror、mathlive
  - a fork of licit
  - newspaper editor for Clark Kent in SuperMan.
    - The base editor is ProseMirror.
    - CZI-Prosemirror built on top of that and added React rendering
    - That was extended further by the Licit Editor
    - This fork converts from flow to Typescript, adds a few plugins

- https://github.com/bvanjoi/emirror
  - 渲染自定义组件基于`plugin.props.nodeViews`配置
  - EMirror, which based on ProseMirror, designed to provide a free framework

- https://gitlab.com/smoores/ode
  - A self-hosted collaborative rich text editor.
  - It's based on Parse Platform, an open source, self-hosted "Complete Application Stack, " and Prosemirror, a rich text editor toolkit.

- https://github.com/li-yechao/paper-editor
  - Write everything in your life
  - 整体架构和tiptap/rich-markdown-editor类似
  - 渲染自定义组件基于editorView.props.nodeViews，ReactNodeView的update方法定义在父类，基于ReactDOM.render()
  - CodeBlock.tsx基于MonacoEditor

- https://github.com/curvenote/editor
  - interactive scientific editor built with ProseMirror, React and Redux
  - A collaborative, rich text editor for interactive technical & scientific content., implementing the MyST standard, and integrating with JupyterLab, JupyterBook and Sphinx. 

- https://github.com/shobokshy/rpm-editor/tree/dev
  - A React renderless rich text editor component.
  - 只依赖prosemirror、react
  - 没有提供使用示例

- https://github.com/Collaborne/mwc-markdown-editor
  - A markdown editor following Material Design spec
  - 基于lit-element、@material/mwc-textfield

- https://github.com/alihesari/prosemirror-demo
  - a demo of a ProseMirror editor that was made collaborative with Yjs & y-prosemirror.
  - We use the y-websocket provider to share document updates through a server. 

- https://github.com/grauwoelfchen/vergil
  - An editor written with Inferno + ProseMirror

- more-prosemirror
  - [xpub-edit (pubsweet-edit)](https://gitlab.coko.foundation/pubsweet/pubsweet/-/tree/master/components/client/xpub-edit)
# prosemirror-utils-extensions
- https://github.com/ShreyRavi/prosemirror-toc
  - An implementation of a table of contents using prosemirror within React.

- https://github.com/thomasgafner/prosemirror-br-encoded-hierarchy-base
  - Use this module to interpret leading and trailing line breaks (br) in paragraphs as a hint for levels of a hierarchy. 
  - Two line breaks in the middle of a paragraph indicate, that the content at a given position is split into two groups

- https://github.com/toba/editor-model
  - TypeScript fork of ProseMirror WYSIWYG editor model
  - https://github.com/toba/editor-commands
  - https://github.com/toba/editor-test
    - 只转换了2个模块到ts就放弃了

- https://github.com/sueddeutsche/prosemirror-recreate-transform
  - This module allows recreating the steps needed to go from document A to B
  - it allows merging two different Transforms (sets of steps) whose steps may be conflicting.
  - Recreating steps can be interesting for example in order to show the changes between two document versions without having access to the original steps.

- https://github.com/iFixit/prosemirror-wikitext
  - taking a Prosemirror document and serializing it into iFixit's custom wiki text syntax.

- https://github.com/evolvedbinary/jdita
  - generates Prosemirror documents from JDita objects. 
  - It also provides Schema Definition for proper display and editing of JDita data.
  - https://github.com/evolvedbinary/jdita
    - converting LwDITA XDITA format to JSON

- https://github.com/artcompiler/L123
  - A language for writing ProseMirror editors
# more-prosemirror-codemirror
