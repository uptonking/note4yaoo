---
title: lib-editor-prosemirror-examples-utils-markdown
tags: [examples, markdown, prosemirror, toc, utils]
created: 2022-11-08T21:14:34.789Z
modified: 2022-11-08T21:14:54.399Z
---

# lib-editor-prosemirror-examples-utils-markdown

# guide

# markdown-editor
- milkdown /6.5kStar/MIT/202208/ts/remark
  - https://github.com/Saul-Mirone/milkdown
  - https://milkdown.dev/
  - https://milkdown.dev/online-demo
  - 依赖prosemirror、remark、prism、katex，但不依赖prosemirror-markdown、react
  - A plugin-driven WYSIWYG markdown Editor, inspired by Typora, built on top of prosemirror and remark.
  - 不同于其他prosemirror项目，可配置支持的markdown特性
  - ⚠️️breaking: @milkdown/core@4.4.0(date202107) migrate from markdown-it to remark
  - https://github.com/alexwkleung/Iris
    - Iris is a WYSIWYG Markdown note-taking app. 
    - Created with TypeScript and Tauri.
    - Mode switching. Switch between WYSIWYG, Markdown, and Reading mode views.
    - Milkdown (ProseMirror) and CodeMirror as the editors.

- rich-markdown-editor /2.7kStar/BSD/202112/ts/markdown-it/archived
  - https://github.com/outline/rich-markdown-editor
  - https://www.getoutline.com/
  - 依赖react、styled-components、prosemirror-markdown、markdown-it、prism-refractor
  - v11.0.0_202009: styled-components is now a peer dependency
  - [v10.0.0_202005: a complete rewrite of the editor from slate to prosemirror](https://github.com/outline/rich-markdown-editor/releases/tag/v10.0.0)
  - A React and Prosemirror based editor that powers Outline

- yfm-editor /3Star/MIT/202211/ts/md-it
  - https://github.com/yandex-cloud/yfm-editor
  - https://ydocs.tech/en/
  - https://preview.yandexcloud.dev/yfm-editor/
  - 依赖prosemirror、markdown-it、react-use、gravity-ui
  - Yandex Flavored Markdown (YFM) is a Markdown dialect and a set of tools for transforming Markdown to HTML in real time and building complete documentation projects.
  - Expandable: you can add any plugin for markdown-it or write your own.

- Stacks-Editor /218Star/MIT/202208/ts
  - https://github.com/StackExchange/Stacks-Editor
  - https://editor.stackoverflow.design/
  - Stacks-Editor is a combination rich text/markdown editor that powers Stack Overflow's post editing experience.
  - 依赖prosemirror, hightlight.js、markdown-it、@lezer/markdown、stacks-ui，不依赖react
  - 全部基于es6 class，[new EditorView()](https://github.com/StackExchange/Stacks-Editor/blob/481492297f680472c51e57c981f050133681edc6/src/rich-text/editor.ts#L76)的过程非常标准，无封装

- https://github.com/Xiphoseer/padington
  - Padington is a tiny collaborative markdown editor that combines a ProseMirror text-editor with a channel based collaborative editing backend written in Rust.
  - https://github.com/xiphoseer/prosemirror-rs 
    - for Rust types for ProseMirror JSON messages
  - https://github.com/xiphoseer/padington-server 
    - for the backend service
  - https://github.com/xiphoseer/padington-client 
    - for the HTML frontend
# markdown-apps
- tiny-write /4Star/NALic/202208/ts/prosemirror/markdown-it/web版+桌面版
  - https://github.com/dennis84/tiny-write
  - https://tiny-write.pages.dev/
  - 支持跨block选择部分文字
  - 支持拖拽block修改顺序，但不支持拖入拖出list item
  - 不支持/斜杠菜单  
  - 依赖solid-js、codemirror6、idb-keyval、date-fns、markdown-it、y-prosemirror
  - Just a little writing tool with markdown shortcuts that saves every change to local indexeddb.
  - 跨平台客户端基于tauri实现，tauri部分使用rust实现

- rino /26Star/GPL.v3/202208/ts/remirror/markdown-it
  - https://github.com/ocavue/rino
  - https://rino-editor.vercel.app/
  - https://rino.app/
  - 提供了类似typora的行内实时编辑预览
  - editor依赖 remirror、unstated-next、codemirror.v6、mui5、floating-ui、markdown-it、mdast-util-from-markdown
  - A better way to write Markdown

- blank /23Star/MIT/202208/ts
  - https://github.com/FPurchess/blank
  - A minimalist, opinionated markdown editor made for writing
  - available for Linux, macOS and Windows， 基于tauri

- https://github.com/Bistard/nota
  - open-sourced note-taking desktop application / markdown editor that provides WYSIWYG and noteTaking-like user experience.
  - 依赖toast-ui-editor
# markdown-utils
- https://github.com/marionebl/prosemirror  /mdx
  -基于react重新实现了部分prosemirror-view的功能，视图层用了pm-EditorState但没用pm-EditorView
  - A personal experiment libraries over prosemirror project
  - prosemirror + remark demos
  - https://www.npmjs.com/package/@marduke182/prosemirror-react-view
    - This library is a full React implementation of the official `prosemirror-view` package. 
    - Aims to implement a simple React Component that uses ProseMirror Data Model to render the document and bind the right events to synchronize the user selection and created ProseMirror transaction based on user inputs.

- https://github.com/Novartis/mdx-utils  /mdx
  - 实现了将mdx ast转换成PMNode，视图层仍然使用prosemirror-view
  - This package contains utilities for working with MDX syntax.
  - Parses an MDX document and its frontmatter into an AST.
  - Create a custom Prosemirror schema. 
    - This extends the Prosemirror Markdown schema with your custom elements, allowing its AST to represent your MDX document.
  - transforms an MDX syntax tree into a Prosemirror syntax tree. 
    - This way, you can load it into a Prosemirror editor and allow rich-text editing with your custom components.

- https://github.com/Sats365/ProsemirrorMarkdownParser
  - /提交多
# more
- prosemirror-markdown /210Star/MIT/202208/ts
  - https://github.com/ProseMirror/prosemirror-markdown
  - 依赖markdown-it.v13
  - This module implements a ProseMirror schema that corresponds to the document schema used by CommonMark, and a parser and serializer to convert between ProseMirror documents in that schema and CommonMark/Markdown text.
  - This is a (non-core) module for ProseMirror.
