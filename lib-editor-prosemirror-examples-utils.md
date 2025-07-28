---
title: lib-editor-prosemirror-examples-utils
tags: [examples, prosemirror, toc]
created: 2022-08-18T11:27:58.811Z
modified: 2022-08-18T16:57:29.058Z
---

# lib-editor-prosemirror-examples-utils

# guide

# model-data-structure
- amat-react /1Star/MIT/202207/js/提交多
  - https://github.com/APMG/amat-react
  - Amat React renders ProseMirror JSON Documents as HTML
  - This component is able to take in a ProseMirror endpoint and compose the correct HTML from it

- https://bitbucket.org/jstleger/prosemirror-composer
  - A useful way to keep complex prosemirror projects tidy, maintainable and testable.
  - complex Prosemirror project: [how we structured our code](https://discuss.prosemirror.net/t/prosemirror-composer-wip/3887)
  - Modifier - A modifier function takes a `transaction` and returns a `transaction`.
  - Handler - A handler function takes the `editorView` and composes the modifier functions and `dispatches` them.

- https://github.com/atlassian/prosemirror-utils /apache2/202307/ts
  - Utils library for ProseMirror

- https://github.com/rexxars/react-prosemirror-document
  - Render a ProseMirror document in JSON-format using React
  - 不使用prosemirror-view，直接转换PMNode然后用react渲染文档，实现过于简单

- https://github.com/jw176/md-viz
  - https://md-viz.netlify.app/
  - Visualise a Markdown/Rich Text document as an interactive force-directed node link diagram.
  - 文档节点视图切换：tree/radial/network
  - 可视化依赖  d3.v7

- https://github.com/ryaninvents/prosemirror-doc-tpl
  - jsx转PMNode，代码量很少
  - provides a concise way to create Prosemirror documents using a JSX-like syntax, for testing or content generation.

- https://github.com/pubpub/prosemirror-pandoc
  - Utilities for converting between Prosemirror schemas and the Pandoc JSON format

- https://github.com/OrkhanAlikhanov/prosemirror-replaceattrs
  - The missing ReplaceAttrsStep for prosemirror
  - In prosemirror, in order to update attributes of a node, you must delete it and replace with a new node with updated attributes.
  - While this works perfectly, during collaboration it does not go well with undo history. 

- https://github.com/sueddeutsche/prosemirror-recreate-transform
  - This module allows recreating the steps needed to go from document A to B
  - it allows merging two different Transforms (sets of steps) whose steps may be conflicting.
  - Recreating steps can be interesting for example in order to show the changes between two document versions without having access to the original steps.
- https://gitlab.com/mpapp-public/manuscripts-manuscript-transform
  - It provides a way to import/export Manuscript JSON Schema formatted data from and to other formats such as (JATS XML, STS XML, HTML, ProseMirror Model)
- https://gitlab.com/mpapp-public/prosemirror-recreate-steps /js
  - This module allows recreating the steps needed to go from document A to B should these not be available otherwise, and it allows merging two different Transforms (sets of steps) whose steps may be conflicting.

- https://github.com/ProseMirror/prosemirror-changeset
  - a helper module that can turn a sequence of document changes into a set of insertions and deletions, for example to display them in a change-tracking interface

- https://github.com/hamflx/prosemirror-diff /202207/js/inactive
  - 支持保留新版本状态的标记
- https://github.com/pubpub/prosemirror-diff /201907/ts/inactive
- https://codesandbox.io/p/sandbox/prosemirror-diff-forked-9trmjq

- https://github.com/davvidbaker/prosemirror-position-debugger
  - I wouldn't say the code in here is exemplary by any means. Lots of mutation, no tests (yet), no strong typing

- https://github.com/ccorcos/prosemirror-decouple-plugins
  - Problem: Prosemirror plugins couple both schema and view.
  - [Separating state and view plugins](https://discuss.prosemirror.net/t/separating-state-and-view-plugins/3970)
  - [Generalized State Architecture](https://discuss.prosemirror.net/t/generalized-state-architecture/3908)

- https://github.com/ccorcos/prosemirror-architecture
  - Since I'm already using ProseMirror, what if we were to model an entire application with a similar style for state management a'la Elm Architecture.

- https://github.com/BlueMona/prosemirror-react-renderer /201710/ts
  - An alternative to ProseMirror's DOMSerializer that converts documents into React elements instead of DOM fragments.
# table
- https://github.com/skiff-org/prosemirror-tables /MIT/202308/js/fork
  - This module defines a schema extension to support tables with rowspan/colspan support, a custom selection class for cell selections in such a table, a plugin to manage such selections and enforce invariants on such tables, and a number of commands to work with tables.
  - https://github.com/medistream-team/prosemirror-tables /ts

- prosemirror-datagrid /3Star/MIT/202109/ts
  - https://github.com/hedgerwang/prosemirror-datagrid
  - https://hedgerwang.github.io/prosemirror-datagrid/dist/demo.html
  - This module defines a schema extension to support datagrid with virtual scrolling and editing support.
# elements-node
- https://github.com/ocavue/prosemirror-flat-list
  - https://prosemirror-flat-list.netlify.app/
  - https://remirror-extension-flat-list.netlify.app/
  - Powerful list for ProseMirror and Remirror
  - This project introduces a new ProseMirror(opens in a new tab) list design different from the prosemirror-schema-list.
  - This project simplifies the list design in ProseMirror(opens in a new tab) by providing only one node type: list. You can add any block nodes as a children of a list node, including another list node. The first child can also be any block type, not just a paragraph.
  - [ProseMirror Flat list (Alpha)](https://discuss.prosemirror.net/t/prosemirror-flat-list-alpha/5191)
    - Some wrapper framework of prosemirror may want to limit the schema groups. For example, in Milkdown, I expect everything under doc should be block.

- https://github.com/emergence-engineering/prosemirror-slash-menu
  - A ProseMirror plugin to handle the state of a slash menu. 
  - It is intended to be opened inline with /, searched and navigated by keyboard. 
  - https://github.com/emergence-engineering/prosemirror-slash-menu-react
    - provide a UI element for the plugin, or you could write your own.
  - [Slash menu for ProseMirror](https://discuss.prosemirror.net/t/prosemirror-slash-menu-prosemirror-slash-menu-react-slash-menu-for-prosemirror/5629)
  - [Emergence Engineering - prosemirror-slash-menu](https://emergence-engineering.com/blog/prosemirror-slash-menu)

- https://gitlab.com/emergence-engineering/prosemirror-codemirror-block /202310/ts
  - https://emergence-engineering.com/blog/prosemirror-codemirror-block
  - CodeMirror 6 code_block in ProseMirror
    - Legacy ( CodeMirror 5 ) language support trough @codemirror/legacy-modes
  - Customizable language selector
  - Lazy-loaded language support

- https://github.com/emergence-engineering/prosemirror-link-preview
  - [Link preview for prosemirror!](https://emergence-engineering.com/blog/prosemirror-link-preview)
  - Because of CORS you can't fetch the link preview from the client directly. 
  - You need to have a custom backend that will fetch the link preview for you. 
  - You either use payed OpenGraph fetcher API or use `link-preview-js` library on your backend to do this. 
  - In this article we will use link-preview-js with Next.js API to do this.

- https://gitlab.com/emergence-engineering/prosemirror-image-plugin
  - Upload images to endpoints, showing placeholder until the upload finishes
  - Customizable overlay for alignment 
  - Image resizing with body resize listeners, so the image always fits the editor ( inspired by czi-prosemirror )

- https://github.com/MH4GF/prosemirror-details-list
  - https://prosemirror-details-list.vercel.app/
  - an open/closeable details element that works with rich text editor based on ProseMirror.
# code-block
- https://github.com/ocavue/prosemirror-highlight /24Star/MIT/202506/ts
  - https://prosemirror-highlight.pages.dev/
  - Highlight your ProseMirror code blocks with any syntax highlighter you like
  - 支持 lowlight(highlightjs), refactor(prism), shiki, sugar-high

- https://github.com/b-kelly/prosemirror-lezer
  - Experimental ProseMirror syntax highlighting plugin that uses Lezer grammars
  - an experimental plugin forked from b-kelly/prosemirror-highlightjs

- https://github.com/StackExchange/prosemirror-highlightjs /19Star/MIT/202207/ts/inactive
  - Or import just the decoration parser and write your own plugin
  - Due to how ProseMirror renders decorations, some existing highlight.js themes might not work as expected. ProseMirror collapses all nested/overlapping decoration structures

- https://github.com/b-kelly/prosemirror-highlightjs
  - Due to how ProseMirror renders decorations, some existing highlight.js themes might not work as expected.
  - ProseMirror collapses all nested/overlapping decoration structures
# form
- https://github.com/kameojs/kameo /23Star/MIT/202507/js
  - https://kameo.dev/
  - Web form editor framework powered by ProseMirror
  - Kameo is a toolkit for creating and rendering interactive web forms in rich text. Based on ProseMirror.
  - Import/export forms - Save and load forms as JSON
  - Dynamic form creation - Build forms programmatically with commands
  - Extensible and customizable - Create your own custom extensions and form fields
  - Framework agnostic - Works seamlessly across different frontend frameworks
# media/embed
- https://github.com/OrkhanAlikhanov/prosemirror-image-uploader
  - The necessary image uploader for prosemirror based editors like (tiptap, remirror).
- https://github.com/shoobyban/prosemirror-dropimage
  - File upload by dragging the images onto the Prosemirror editor. No upload form, no hassle. 
  - Accepts svg, png, jpg and gif.
# port-lang
- https://github.com/fellowapp/prosemirror-py /50Star/BSD/202503/python
  - Python implementation of core ProseMirror modules
  - Until now, the only option for manipulating and working with ProseMirror documents from Python was to embed a JS runtime. 
  - With this translation, you can now define schemas, parse documents, and apply transforms directly via a native Python API.
- https://github.com/fiduswriter/prosemirror-python
  - Python translation of prosemirror parts needed to modify a document in Python

- https://github.com/cozy/prosemirror-go /47Star/AGPLv3/202501/go
  - A port in Go of ProseMirror for writing a collaborative editing server
  - This repository contains a port in Go of `prosemirror-model` and `prosemirror-transform` in order to have the server part of the collaborative editing in Go.

- https://github.com/Xiphoseer/prosemirror-rs
  - Implementation of the https://prosemirror.net model/transform API in Rust

- https://github.com/atlassian-labs/prosemirror-kotlin /29Star/apache2/202506/kotlin
  - Java/Kotlin implementation of Prosemirror
  - collab, history, model, state, test-builder, transform

- https://github.com/Holoon/ProseMirror.Model /c#
  - C# definitions of ProseMirror's content model, the data structures used to represent and work with documents.
  - https://github.com/stepwisehq/prosemirror-dotnet
# utils/extensions
- https://github.com/marekdedic/prosemirror-unified /MIT/202507/ts
  - This package provides support for using the unified ecosystem of parsers and other packages (for example, remark, the markdown parser) in ProseMirror.
  - Currently, there is only the prosemirror-remark package to support markdown parsing and serialization
  - https://github.com/marekdedic/prosemirror-remark

- https://github.com/ueberdosis/prosemirror-to-html
  - Takes ProseMirror JSON and outputs HTML. 基于php实现
- https://github.com/enVolt/prosemirror-to-html
  - 基于js实现
- https://github.com/mailbean/pm2html /202310/ts
  - ProseMirror JSON to HTML

- https://github.com/ueberdosis/html-to-prosemirror /php
  - Takes HTML and outputs ProseMirror compatible JSON. 基于php实现
- https://github.com/enVolt/html-to-prosemirror
  - Takes HTML and outputs ProseMirror compatible JSON. originally written for PHP

- https://github.com/SebastianPodgajny/prosemirror-html-to-json
  - This library is used to convert HTML to prosemirror JSON format on backend

- https://github.com/ShreyRavi/prosemirror-toc
  - An implementation of a table of contents using prosemirror within React.

- https://github.com/ocavue/prosemirror-virtual-cursor /83Star/MIT/202408/ts/inactive
  - https://prosemirror-virtual-cursor.vercel.app/
  - a plugin that adds a virtual cursor (or caret) to your editor. 
  - It implements the bike-style cursor, which shows a tail under the cursor between mark boundary.
  - 在光标竖线的底部显示向左或向右的短横，来表名行内marker的边界
  - Under the hood, I hide the native cursor and use `Decoration.widget` to insert a `<span>` element to the cursor position
    - 👉🏻 I refactored prosemirror-virtual-cursor and overlay the cursor over the editor.

- https://github.com/curvenote/editor/tree/main/packages/prosemirror-autocomplete
  - can be used to create suggestions similar to Notion, Google Docs or Confluence; it is created and used by Curvenote. 
  - The library does not provide a user interface beyond the demo code.
  - 仅依赖pm-state/view

- https://github.com/ccorcos/prosemirror-examples/blob/master/src/app/components/Autocomplete.tsx
  - https://ccorcos.github.io/prosemirror-examples/

- https://github.com/joelewis/prosemirror-mentions /js
  - https://star-drug.glitch.me/
  - A ProseMirror plugin that enables @mentions and #hashtags in a prosemirror view.
  - https://github.com/quartzy/prosemirror-suggestions

- https://github.com/sereneinserenade/tiptap-inline-suggestion /69Star/MIT/202308/ts/inactive
  - https://sereneinserenade.github.io/tiptap-inline-suggestion/
  - A tiptap extension that allows you to add inline suggestions to your editor

- https://github.com/lukesmurray/prosemirror-async-query
  - A simple declarative API for using promises in prosemirror plugin state.

- https://github.com/thomasgafner/prosemirror-br-encoded-hierarchy-base
  - Use this module to interpret leading and trailing line breaks (br) in paragraphs as a hint for levels of a hierarchy. 
  - Two line breaks in the middle of a paragraph indicate, that the content at a given position is split into two groups

- https://github.com/toba/editor-model
  - TypeScript fork of ProseMirror WYSIWYG editor model
  - https://github.com/toba/editor-commands
  - https://github.com/toba/editor-test
    - 只转换了2个模块到ts就放弃了

- https://github.com/curvenote/prosemirror-docx /140Star/MIT/202506/ts
  - Export a prosemirror document to a Microsoft Word file, using docx.
  - https://github.com/dxc111/prosemirror-docx
    - Export a prosemirror document to a Microsoft Word file, using docx.
  - https://github.com/dolanmiu/docx /MIT/202401/ts
    - Easily generate .docx files with JS/TS with a nice declarative API. 
    - Works for Node and on the Browser.

- https://github.com/iFixit/prosemirror-wikitext
  - taking a Prosemirror document and serializing it into iFixit's custom wiki text syntax.

- https://github.com/evolvedbinary/jdita
  - generates Prosemirror documents from JDita objects. 
  - It also provides Schema Definition for proper display and editing of JDita data.
  - https://github.com/evolvedbinary/jdita
    - converting LwDITA XDITA format to JSON

- https://github.com/artcompiler/L123
  - A language for writing ProseMirror editors

- https://github.com/todorstoev/prosemirror-pagination /88Star/MIT/202412/ts/inactive
  - Plugin for ProseMirror emulating A4 pages

- https://github.com/guardian/prosemirror-invisibles
  - https://guardian.github.io/prosemirror-invisibles/
  - A simple implementation of invisible characters in ProseMirror.
  - A plugin that uses decorations to show invisible characters in ProseMirror

- https://github.com/guardian/prosemirror-noting
  - https://guardian.github.io/prosemirror-noting/
  - This plugin allows you to add notes as marks to prosemirror. 支持 toggle note

- https://github.com/xylk/prosemirror-compress /201805/js
  - ProseMirror data compression

- https://github.com/prowriting/beyondgrammar-prosemirror /28Star/MIT/202008/ts/inactive
  - Bring real-time spelling, grammar and style checking into your ProseMirror editor.
  - You will need to register to get a API key first (FREE for Individuals)

- https://github.com/amirhhashemi/tiptap-text-direction /202304/ts
  - This extension automatically detects the direction of a configurable list of nodes and adds dir="ltr" or dir="rtl" to them.
  - Why not dir="auto"? dir="auto" changes the text direction based on the element's content too

- https://github.com/kongdivin/prosemirror-scroll2cursor
  - a prosemirror plugin. It makes sure the cursor is always visible and at the position that is comfortable for typing, not too low at the bottom or too high at the top.

- https://github.com/sereneinserenade/vimirror
  - VIM bindings for ProseMirror/Tiptap.

- https://github.com/benrbray/prosemirror-math /288Star/MIT/202404/ts/katex/inactive
  - https://benrbray.com/prosemirror-math/
  - provides schema and plugins for comfortably writing mathematics with ProseMirror.
  - math rendering handled by KaTeX

- https://github.com/mattberkowitz/prosemirror-find-replace /MIT/201606/js/inactive
  - Find & Replace plugin for ProseMirror
# selection
- https://github.com/xnimorz/selection-range-enhancer /202010/ts
  - A project, which enhances abilities of selectionRange. It allows to track changes, works with carets and so on

- https://github.com/retentioneering/retentioneering-dom-observer /202111/ts
  - tools for parsing DOM data, observing DOM and tracking changes
  - a wrapper over MutationObservers, allowing you to observe changes even of those nodes that are not already in the DOM.
# mobile
- https://github.com/amjadbouhouch/rn-text-editor /22Star/MIT/202405/ts/inactive
  - an evolving and feature-rich text editor package for React Native 
# more-utils
- https://github.com/remirror/prosemirror-migration
  - a tool for migrating ProseMirror documents when you have breaking changes to your document schema.
  - It takes a JSON encoded ProseMirror document, and recursively descends through each node, executing a migration strategy for a node type.

- https://github.com/evolvedbinary/prosemirror-jdita
  - This tool generates Prosemirror documents from JDita objects. 
  - It also provides Schema Definition for proper display and editing of JDita data.
  - https://github.com/evolvedbinary/jdita
    - This tool generates JSON data from XDita files
    - 在使用 XML 开发这种信息管理系统时，IBM 开发了 Darwin Information Typing Architecture (DITA) [OASIS 标准]。
    - DITA 是“一种基于 XML 的端对端架构，可用于编写、生成并交付技术信息”。
    - 它使用 DTD 将文档组织为可重用的模块（称为“主题(topics)”）并表示该主题的内容。
    - 它还提供了一种系统实现主题的元数据注释，因此用户可以便捷地搜索、过滤和处理内容。

- https://github.com/KamenRider41/Prosemirror-cli
  - 一个基于webpack的ProseMirror脚手架！
  - 运行后可以得到一个简单的编辑器，可以在这个基础上进行进一步的开发！
