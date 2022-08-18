---
title: lib-editor-prosemirror-examples-plugins
tags: [examples, prosemirror, toc]
created: 2022-08-18T11:27:58.811Z
modified: 2022-08-18T11:28:22.623Z
---

# lib-editor-prosemirror-examples-plugins

# guide

# prosemirror-collab

# prosemirror-utils-markdown-remark
- milkdown /454Star/MIT/202106/ts
  - https://github.com/Saul-Mirone/milkdown
  - https://saul-mirone.github.io/milkdown/
  - 依赖prosemirror、remark、prism、katex，但不依赖prosemirror-markdown、react
  - A plugin-driven WYSIWYG markdown Editor, inspired by Typora, built on top of prosemirror and remark.
  - ⚠️️breaking: @milkdown/core@4.4.0(202107) migrate from markdown-it to remark

- rino /20Star/GPLv3/202201/ts
  - https://github.com/ocavue/rino
  - https://rino.app/
  - 依赖 remirror、codemirror6
  - A better way to write Markdown

- https://github.com/marionebl/prosemirror  /mdx
  -基于react重新实现了部分prosemirror-view的功能，视图层用了pm-EditorState但没用pm-EditorView
  - A personal experiment libraries over prosemirror project
  - prosemirror + remark demos
  - https://www.npmjs.com/package/@marduke182/prosemirror-react-view
    - This library is a full React implementation of the official prosemirror-view package. 
    - Aims to implement a simple React Component that uses ProseMirror Data Model to render the document and bind the right events to synchronize the user selection and created ProseMirror transaction based on user inputs.

- https://github.com/Novartis/mdx-utils  /mdx
  - 实现了将mdx ast转换成PMNode，视图层仍然使用prosemirror-view
  - This package contains utilities for working with MDX syntax.
  - Parses an MDX document and its frontmatter into an AST.
  - Create a custom Prosemirror schema. 
    - This extends the Prosemirror Markdown schema with your custom elements, allowing its AST to represent your MDX document.
  - transforms an MDX syntax tree into a Prosemirror syntax tree. 
    - This way, you can load it into a Prosemirror editor and allow rich-text editing with your custom components.

- https://github.com/rexxars/react-prosemirror-document
  - Render a ProseMirror document in JSON-format using React
  - 不使用prosemirror-view，直接转换PMNode然后用react渲染文档，实现过于简单

- https://github.com/ryaninvents/prosemirror-doc-tpl
  - jsx转PMNode，实现很简单
  - provides a concise way to create Prosemirror documents using a JSX-like syntax, for testing or content generation.
# prosemirror-utils-table

# prosemirror-utils-math

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
# prosemirror-examples-apps

# more-prosemirror-editor
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
