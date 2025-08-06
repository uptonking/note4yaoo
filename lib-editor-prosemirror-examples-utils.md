---
title: lib-editor-prosemirror-examples-utils
tags: [examples, prosemirror, toc]
created: 2022-08-18T11:27:58.811Z
modified: 2022-08-18T16:57:29.058Z
---

# lib-editor-prosemirror-examples-utils

# guide

# popular
- https://github.com/mizuka-wu/prose-typed /202505/ts
  - https://mizuka-wu.github.io/prose-typed/
  - ProseTyped is a streaming text animation library for ProseMirror editors, leveraging the prosemirror-model to create typewriter effects

- https://github.com/GYHHAHA/prosemirror-columns /MIT/202505/ts
  - plugin that allows you to create multiple columns in the editor. 
  - It also supports resizing columns and add/remove single column. 
  - The implementation is largely inspired from prosemirror-tables.

- https://github.com/topo-io/tiptap-extensions /202302/ts/inactive
  - Column extension for tiptap v2

- https://github.com/vueditor/tiptap-extension-handle /MIT/202501/ts
  - https://vueditor.litingyes.top/
  - A tiptap extension to support drag handle and custom view
  - https://github.com/vueditor/rich-text-editor /MIT/202409/ts/vue/inactive
    - https://vueditor-rich-text.netlify.app/
    - As a playground for rich text editors with Tiptap, committed to exploring and incubating various practical extensions.

- https://github.com/NiclasDev63/tiptap-extension-global-drag-handle /MIT/202502/ts
  - In order to enjoy all the advantages of the drag handle, it is recommended to install the AutoJoiner extension as well, which allows you to automatically join various nodes such as 2 lists that are next to each other
  - https://github.com/NiclasDev63/tiptap-extension-auto-joiner /MIT/202405/ts
    - This extension provides the expected behavior for lists, e.g. joining two adjacent lists to one. It can be extended to join not only lists, but all types of nodes that are next to each other, such as paragraphs or custom nodes.

- https://github.com/vueditor/tiptap-extension-handle /MIT/202409/ts
  - A tiptap extension to support drag handle and custom view

- https://github.com/todorstoev/prosemirror-pagination /88Star/MIT/202412/ts/inactive
  - Plugin for ProseMirror emulating A4 pages

- https://github.com/RomikMakavana/tiptap-pagination /MIT/202505/ts
  - http://romikmakavana.me/tiptap-pagination/
  - A TipTap extension that adds pagination support to your editor with table handling capabilities.
  - https://github.com/RomikMakavana/tiptap-pagination-plus
    - adds pagination support to your editor with table handling capabilities.
  - https://github.com/Nanomagicos/tiptap-extension-pagination-mod
  - [Feature Request: Pagination extension (A4 format content) _202410](https://github.com/ueberdosis/tiptap/discussions/5719)

- https://github.com/adityayaduvanshi/tiptap-pagination-breaks /MIT/202504/ts
  - a Tiptap extension that enables automatic pagination and page breaks within your Tiptap editor. 
  - Perfect for applications that require document-like editing features with defined page heights and visual page breaks.
  - Automatic Pagination: Handles content overflow by adding page breaks based on defined page dimensions.
  - Customizable Page Settings: Configure page height, width, and margin to control how content is paginated.
  - Visual Page Breaks: Inserts dashed lines to represent page boundaries in the editor.
  - Page Numbering: Allows optional page numbering.

- https://github.com/Cassielxd/tiptap-pagination-demo /202507/ts
  - 一个基于 Vue 3 + TypeScript + Vite + Element Plus + Tiptap + Tailwind CSS 构建的现代化富文本编辑器。
  - https://github.com/Cassielxd/umo-enhance
    - tiptap prosemirror Paging use cases

- https://github.com/hugs7/tiptap-extension-pagination /MIT/202503/ts
  - An extension for the Tiptap editor allowing for pagination

- https://github.com/ramu-narasinga/tiptap-extension-pagination-changesets-playground /MIT/202503/ts/inactive
  - An extension for the Tiptap editor allowing for pagination
  - Improved from clemente-xyz's comment [Feature Request: Pagination extension (A4 format content) _202410](https://github.com/ueberdosis/tiptap/discussions/5719)

- https://github.com/emergence-engineering/prosemirror-vs-lexical-performance-comparison /202410/ts
  - ProseMirror vs. Lexical Performance Comparison

- https://github.com/sereneinserenade/tiptap-search-and-replace /MIT/202401/ts
  - https://sereneinserenade.github.io/tiptap-search-and-replace/
  - Search and Replace extension for Tiptap 2.

- https://github.com/luccalb/tiptap-annotation-magic /MIT/202309/ts/inactive
  - An extension for the Tiptap editor, enabling the annotation of text. 
  - render overlapping annotations as fragments. Annotations are rendered as Decorations and are therefore not a part of the Prosemirror Document.
  - https://github.com/bashitoy/annotationMagic-tiptap

- https://github.com/b310-digital/tiptap-extension-comment-collaboration /MIT/202503/ts
  - TipTap Extension which brings proper support for collaborative comments
  - It is used actively within GroupWriter.
  - Comments get a calculated position so it is possible to place them next to the text where they belong

- https://github.com/Manas1820/extension-table-of-contents /MIT/202505/ts
  - A Tiptap extension that generates a customizable and dynamic Table of Contents from your editor content.
  - A TipTap extension that automatically generates and manages a table of contents from document headings.
  - Note: This extension is fully compatible with the official TipTap Table of Contents extension.
  - Provides scroll position tracking
  - Customizable heading ID generation
# model-data-structure
- https://bitbucket.org/jstleger/prosemirror-composer
  - A useful way to keep complex prosemirror projects tidy, maintainable and testable.
  - complex Prosemirror project: [how we structured our code](https://discuss.prosemirror.net/t/prosemirror-composer-wip/3887)
  - Modifier - A modifier function takes a `transaction` and returns a `transaction`.
  - Handler - A handler function takes the `editorView` and composes the modifier functions and `dispatches` them.

- https://github.com/atlassian/prosemirror-utils /apache2/202307/ts
  - Utils library for ProseMirror

- amat-react /1Star/MIT/202507/js/提交多
  - https://github.com/APMG/amat-react
  - Amat React renders ProseMirror JSON Documents as HTML
  - This component is able to take in a ProseMirror endpoint and compose the correct HTML from it

- https://github.com/rexxars/react-prosemirror-document
  - Render a ProseMirror document in JSON-format using React
  - 不使用prosemirror-view，直接转换PMNode然后用react渲染文档，实现过于简单

- https://github.com/measurlabs/prosemirror-react-renderer /202310/ts/inactive
  - Customizable and lightweight library for rendering ProseMirror compatible JSON schema as React components.

- https://github.com/gbicou/prosemirror-render /202507/ts/vue
  - https://gbicou.github.io/prosemirror-render/
  - Monorepo for rendering ProseMirror JSON data with Vue and Nuxt
  - Vue plugin providing a component that translates ProseMirror nodes and marks to customizable Vue components or HTML elements.

- https://github.com/jw176/md-viz
  - https://md-viz.netlify.app/
  - Visualise a Markdown/Rich Text document as an interactive force-directed node link diagram.
  - 文档节点视图切换：tree/radial/network
  - 可视化依赖  d3.v7

- https://github.com/ryaninvents/prosemirror-doc-tpl /202106/ts/inactive
  - jsx转PMNode，代码量很少
  - provides a concise way to create Prosemirror documents using a JSX-like syntax, for testing or content generation.

- https://github.com/pubpub/prosemirror-pandoc /MIT/202207/ts/inactive
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
  - https://github.com/chanzuckerberg/prosemirror-recreate-steps-timeout-patch /apache2/202202/js/inactive
  - https://github.com/banaoa/prosemirror-recreate-steps /202305/js/inactive

- https://github.com/ProseMirror/prosemirror-changeset
  - a helper module that can turn a sequence of document changes into a set of insertions and deletions, for example to display them in a change-tracking interface

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

- https://github.com/chatwoot/prosemirror-schema /MIT/202507/js
  - Schema setup for using prosemirror in chatwoot. 
  - Based on https://github.com/ProseMirror/prosemirror-example-setup/

- https://github.com/ekkolon/prosemirror-autopairs /MIT/202506/ts
  - Smart auto-pairing of brackets and quotes for ProseMirror editors.
  - Auto-inserts matching characters like (), {}, "", etc.

- https://github.com/emergence-engineering/prosemirror-text-map /MIT/202407/ts
  - A library for manipulating ProseMirror documents in text format.
  - Convert a ProseMirror document to text, do the work, then map back positions in the text to the ProseMirror document.
  - This lib is mostly helpful for situations where you use other libraries whose working on texts only (like diffing, parsing, etc.) and you need to map back the results to the ProseMirror document (like adding marks based on text change).

- https://github.com/ocavue/prosemirror-splittable /MIT/202406/ts
  - Extends ProseMirror's `AttributeSpec` to allow for `splittable` property. 
  - splittable is a boolean that, when true, enables the inheritance of the attribute when splitting a node using the `splitSplittableBlock` command.

- https://github.com/dylanonelson/pm-collab-clipboard /201909/js/inactive
  - This module is an experiment with making a “collaborative clipboard” in ProseMirror.
  - This module changes that behavior by introducing a MoveStep, which, instead of serializing the pasted content directly into the step, records only the positions of the moved content and its destination. Thus, the second user’s rebased cut-and-paste will in fact include the first user’s changes when they fall within the slice that was cut and then pasted.
# table
- https://github.com/skiff-org/prosemirror-tables /MIT/202308/js/fork
  - This module defines a schema extension to support tables with rowspan/colspan support, a custom selection class for cell selections in such a table, a plugin to manage such selections and enforce invariants on such tables, and a number of commands to work with tables.
  - https://github.com/medistream-team/prosemirror-tables /ts

- prosemirror-datagrid /3Star/MIT/202109/ts
  - https://github.com/hedgerwang/prosemirror-datagrid
  - https://hedgerwang.github.io/prosemirror-datagrid/dist/demo.html
  - This module defines a schema extension to support datagrid with virtual scrolling and editing support.

- https://github.com/ProseMirror/prosemirror-tables /MIT/202504/ts
  - This module defines a schema extension to support tables with rowspan/colspan support, a custom selection class for cell selections in such a table, a plugin to manage such selections and enforce invariants on such tables, and a number of commands to work with tables.
- https://github.com/Ultra317/ProseMirror-tables-forked /202503/ts
  - pm-tables修改版，允许设置表格不超出特定范围
  - 允许设置表格像腾讯文档一样，不超出编辑区域边界 （对编辑器元素和内边距的处理较为粗糙，可以自行前往columnresizing.ts文件做更精细的适配）

- https://github.com/massifrg/prosemirror-tables-sections /MIT/202403/ts
  - prosemirror-tables derived component to support tables with caption/thead/tbody/tfoot
  - This module defines a schema extension to support tables with table caption, head, bodies and foot, rowspan/colspan support, a custom selection class for cell selections in such a table, a plugin to manage such selections and enforce invariants on such tables, and a number of commands to work with tables.
  - It's a fork of prosemirror-tables.
  - The goal of this module is a Prosemirror Node rendering the tables of Pandoc's internal model, but it's generic enough to support any table with an optional caption, an optional head (thead), one or more table bodies (tbody) and an optional foot (tfoot).

- https://github.com/RomikMakavana/tiptap-table-plus /202503/js
  - extends the table functionality of the Tiptap editor by adding two new commands: `duplicateColumn` and `duplicateRow`.
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

- https://github.com/emergence-engineering/prosemirror-link-preview
  - [Link preview for prosemirror!](https://emergence-engineering.com/blog/prosemirror-link-preview)
  - Because of CORS you can't fetch the link preview from the client directly. 
  - You need to have a custom backend that will fetch the link preview for you. 
  - You either use payed OpenGraph fetcher API or use `link-preview-js` library on your backend to do this. 
  - In this article we will use link-preview-js with Next.js API to do this.

- https://github.com/HMarzban/extension-hyperlink /MIT/202401/ts/inactive
  - A powerful and customizable hyperlink extension for Tiptap Editor, offering enhanced functionality similar to Google Docs link plugin.

- https://github.com/sadn1ck/prosemirror-extras
  - Personal collection of ProseMirror plugins and utilities
  - @sadn1ck/prosemirror-link-paste-plugin
    - Plugin that allows users to paste links into the editor and have it converted to a link mark per the schema.

- https://gitlab.com/emergence-engineering/prosemirror-image-plugin
  - Upload images to endpoints, showing placeholder until the upload finishes
  - Customizable overlay for alignment 
  - Image resizing with body resize listeners, so the image always fits the editor ( inspired by czi-prosemirror )
  - https://github.com/dkulchenko/prosemirror-image-plugin

- https://github.com/bae-sh/tiptap-extension-resize-image /MIT/202507/ts
  - a suite of open source content editing and real-time collaboration tools for developers
- https://github.com/breakerh/tiptap-image-resize /MIT/202304/ts/inactive
  - https://breakerh.github.io/tiptap-image-resize/
  - Simple React image resizer

- https://github.com/HoHieuLuc/tiptap-resizable-image /MIT/202507/ts
  - https://tiptap-resizable-image.vercel.app/
  - Resizable image extension for Tiptap

- https://github.com/MH4GF/prosemirror-details-list
  - https://prosemirror-details-list.vercel.app/
  - an open/closeable details element that works with rich text editor based on ProseMirror.

- https://github.com/rbell6/emoji-picker-poc /202503/ts
  - emoji-picker/prosemirror poc
- https://github.com/reactjseditor255/reactjs-tiptap-editor-emoji /202408/ts
  - https://tiptap-emoji.surge.sh/
  - Tiptap extension emoji

- https://github.com/raihan-ramadhan/tiptap-extension-twemoji /202507/ts
  - shadcn/ui monorepo
- https://github.com/satyajeetjadhav/tiptap-emoji-picker
  - The official tiptap emoji picker extension is a pro extension.
  - It is easy enought to build this extension by extending the existing Mention plugin 

- https://github.com/buttondown/tiptap-footnotes /MIT/202507/ts
  - A footnotes extension for Tiptap
- https://github.com/LAbigael/tiptap-extension-footnote /202312/js/inactive
  - Tiptap extension that allows you to add footnote to your document

- https://github.com/talqui-oss/tiptap-extension-variable /202504/ts
  - Variable extension for tiptap 

- https://github.com/danejorgensen/tiptap-extension-variable /202404/ts
  - https://github.com/haiml123/tip-tap-variable-node-view

- https://github.com/tanushri0804/Text-Editor /202503/ts
  - https://syntaxbit.netlify.app/
  - a React-based Rich Text Editor built using TipTap. 
  - The editor supports custom variables, formatting options, and interactive features like fallback values for variables.
  - Custom Variables: Insert variables with `{{ variable }}` syntax
# code/highlight/annotation
- https://gitlab.com/emergence-engineering/prosemirror-codemirror-block /202310/ts
  - https://emergence-engineering.com/blog/prosemirror-codemirror-block
  - CodeMirror 6 code_block in ProseMirror
    - Legacy ( CodeMirror 5 ) language support trough @codemirror/legacy-modes
  - Customizable language selector
  - Lazy-loaded language support

- https://github.com/sibiraj-s/prosemirror-codemirror-6 /MIT/202206/ts
  - https://sibiraj-s.github.io/prosemirror-codemirror-6/
  - Based on the example from https://prosemirror.net/examples/codemirror/. This is just an example setup and might not be very reusable.

- https://github.com/ocavue/prosemirror-highlight /24Star/MIT/202506/ts
  - https://prosemirror-highlight.pages.dev/
  - Highlight your ProseMirror code blocks with any syntax highlighter you like
  - 支持 lowlight(highlightjs), refactor(prism), shiki, sugar-high

- https://github.com/timomeh/tiptap-extension-code-block-shiki /MIT/202503/ts
  - Use Shiki syntax highlighting for codeblocks in TipTap
  - https://github.com/vphventures/tiptap-code-block-shiki

- https://github.com/b-kelly/prosemirror-lezer
  - Experimental ProseMirror syntax highlighting plugin that uses Lezer grammars
  - an experimental plugin forked from b-kelly/prosemirror-highlightjs

- https://github.com/StackExchange/prosemirror-highlightjs /19Star/MIT/202207/ts/inactive
  - Or import just the decoration parser and write your own plugin
  - Due to how ProseMirror renders decorations, some existing highlight.js themes might not work as expected. ProseMirror collapses all nested/overlapping decoration structures

- https://github.com/b-kelly/prosemirror-highlightjs
  - Due to how ProseMirror renders decorations, some existing highlight.js themes might not work as expected.
  - ProseMirror collapses all nested/overlapping decoration structures

- https://github.com/Jorge-Antonio-Gomez/quantum-highlighter-pro-chrome-extension /CC-4.0/202507/js/tiptap
  - open-source web annotation extension for Chrome, inspired by Zotero's annotation system. 
  - Highlight, underline, and manage annotations with rich-text comments on any webpage.
  - Vanilla JavaScript: No heavy frameworks for the core logic
  - Floating UI: A powerful library for intelligently positioning floating elements like context menus.
  - Custom i18n System: A dependency-free internationalization system.
  - Two Annotation Types: Choose between highlighting text with a background color or underlining it.
  - Annotations persist reliably, even on dynamic websites like YouTube, thanks to a MutationObserver-based re-application system.

- https://github.com/nartix/tiptap-inline-code-highlight /MIT/202506/js
  - Inline live code highlighting extension for Tiptap editor using lowlight and highlight.js

- https://github.com/prowriting/beyondgrammar-prosemirror /28Star/MIT/202008/ts/inactive
  - Bring real-time spelling, grammar and style checking into your ProseMirror editor.
  - You will need to register to get a API key first (FREE for Individuals)

- https://github.com/nullpointerexceptionkek/prosemirror-proofread /MIT/202412/ts
  - https://nullpointerexceptionkek.github.io/prosemirror-proofread/
  - a plugin for adding spell-check and grammar-checking capabilities to your ProseMirror editor.
  - Handles integration of spell-checking and proofreading services into ProseMirror
  - This library helps you integrate a variety of spell-check services, including LanguageTool. 
  - This library is designed to handle caching, ignore, and pop-ups. It is up to the developer's responsibility to implement UI and spell-checking services.
  - The main difficulty of creating a spell-checking library for ProseMirror, which handles ProseMirror's particular index. Most spell-checking services are designed to handle plain text, and mapping between a rich ProseMirror document to plain text and vice versa is complex. To do so, the library checks each node individually and caches the results.
  - https://github.com/sereneinserenade/tiptap-languagetool

- https://github.com/farscrl/tiptap-extension-spellchecker /MIT/202502/ts
  - extension to integrate a spellchecker into the tiptap editor.
  - The extension does not implement a spellchecker itself: you have to pass it a proofreader object implementing the IProofreaderInterface interface
  - This extension is inspired by the tiptap-languagetool extension.
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
- https://github.com/SachikoNitta/IconFlow /202507/ts
  - https://icon-flow.vercel.app/
  - A proof-of-concept showcasing how to integrate inline SVG icons within a ProseMirror-based editor, providing seamless icon insertion and rendering capabilities.
  - Customization: Easy to modify colors, styles, and properties via CSS
  - Performance: Inline SVGs reduce HTTP requests and can be cached efficiently

- https://github.com/OrkhanAlikhanov/prosemirror-image-uploader
  - The necessary image uploader for prosemirror based editors like (tiptap, remirror).
- https://github.com/shoobyban/prosemirror-dropimage
  - File upload by dragging the images onto the Prosemirror editor. No upload form, no hassle. 
  - Accepts svg, png, jpg and gif.

- https://github.com/PentestPad/tiptap-extension-figure /202506/ts
  - An extension for Tiptap that allows you to add and edit captions for images as well as align and resize them.

- https://github.com/sereneinserenade/tiptap-extension-video /MIT/202412/ts
  - https://sereneinserenade.github.io/tiptap-extension-video
  - Tiptap 2 Extension for adding videos.

- https://github.com/carlosvaldesweb/tiptap-extension-upload-image /MIT/202405/ts
  - image upload feature with real-time preview. 
  - https://github.com/coolswitch/tiptap-extension-image-upload

- https://github.com/HMarzban/extension-hypermultimedia /202501/ts
  - A powerful and customizable HyperMultimedia extension for Tiptap Editor
  - We designed the HyperMultimedia extension as a headless UI.
  - Note: By default, the Image, YouTube, Vimeo, SoundCloud, and Twitter are active.
  - This extension is primarily built for the docs.plus project

- https://github.com/haydenbleasel/tiptap-extension-figma /MIT/202408/ts/inactive
  - A Tiptap extension for hydrating Figma designs in a TipTap document. 
  - It uses Figma's Live Embed Kit to take matching URLs and render them in the editor as an iframe.
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

- https://github.com/Cassielxd/moduforge-rs /paid/202507/rust
  - http://mf.vv-xj.com/
  - 一个基于 Rust 的状态管理和数据转换框架，专注于不可变数据结构和事件驱动架构。
  - 它提供了无业务绑定的编辑器核心实现，可以通过扩展进行定制和扩展，支持任何业务场景的需求。
  - 灵感来自prosemirror , deno
  - 工作方式: 定义基础节点、标记和约束，然后定义扩展添加行为。
  - 使用 im-rs 进行基础数据定义，保证数据的不可变性。
  - zen: 规则引擎管理，解除业务硬编码耦合（如果使用）。
  - 可扩展性: ModuForge 设计为高度可扩展，允许开发者根据需求自定义编辑器的功能和行为。这包括插件系统，使得添加新功能变得简单，任何功能都可以扩展。例如：历史记录，撤销，重做。
  - 模块化: 整个框架被分解成多个独立的模块，每个模块负责编辑器的一个特定方面，如模型、状态管理、命令执行等。
  - https://github.com/Cassielxd/moduforge-demo

- https://github.com/atlassian-labs/prosemirror-kotlin /29Star/apache2/202506/kotlin
  - Java/Kotlin implementation of Prosemirror
  - collab, history, model, state, test-builder, transform

- https://github.com/Holoon/ProseMirror.Model /c#
  - C# definitions of ProseMirror's content model, the data structures used to represent and work with documents.
  - https://github.com/stepwisehq/prosemirror-dotnet
- https://github.com/myblueprint-spaces/papiermirror
  - This package is intended for server applications written in . NET to interface with frontend applications that use ProseMirror.
# tooltip/autocomplete/ai
- https://github.com/emergence-engineering/prosemirror-suggestcat-plugin-react /202412/ts
  - Basic UI for prosemirror-suggestcat-plugin in React.
  - https://github.com/emergence-engineering/prosemirror-suggestcat-plugin /MIT/202410/ts
    - Adds AI features to your ProseMirror editor

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

- https://github.com/Letterboxd/prosemirror-selection-menu /202401/ts
  - A plugin for displaying prosemirror-menu items in a floating menu above a selection.
  - This is sometimes referred to as a Medium-style floating menu

- https://github.com/owardlaw/Autocomplete /202407/js/inactive
  - https://autocomplete-engine-gold.vercel.app/
  - An autocomplete engine written in JS using TipTap.
# utils/extensions
- https://github.com/handlewithcarecollective/remark-prosemirror /MIT/202505/ts
  - A remark plugin for converting between markdown and ProseMirror
  - A set of plugins and utils for integrating remark, mdast, and ProseMirror. 
  - Can be used to convert ProseMirror documents to Markdown, and vice versa
  - This library exports tools for converting back and forth between Markdown and ProseMirror documents. It’s part of the unified ecosystem.

- https://github.com/marekdedic/prosemirror-unified /23Star/MIT/202507/ts
  - This package provides support for using the unified ecosystem of parsers and other packages (for example, remark, the markdown parser) in ProseMirror.
  - Currently, there is only the `prosemirror-remark` package to support markdown parsing and serialization
  - https://github.com/marekdedic/prosemirror-remark
  - https://github.com/marekdedic/prosemirror-remark-example

- https://github.com/riccardoperra/prosemirror-processor /apache2/202505/ts
  - Process ProseMirror documents via unified AST.

- https://github.com/domgdsman/prosemirror-placeholder /MIT/202507/ts
  - Minimal prosemirror plugin that displays a placeholder text. 
  - Useful for search bars and text fields.

- https://github.com/ueberdosis/prosemirror-to-html
  - Takes ProseMirror JSON and outputs HTML. 基于php实现
- https://github.com/enVolt/prosemirror-to-html
  - 基于js实现
- https://github.com/ShivamJoker/Prosemirror-to-HTML-NodeJS /202402/ts
  - Convert Prosemirror AST JSON back to HTML in NodeJS with Happy-DOM
- https://github.com/mailbean/pm2html /202310/ts
  - ProseMirror JSON to HTML

- https://github.com/ueberdosis/html-to-prosemirror /php
  - Takes HTML and outputs ProseMirror compatible JSON. 基于php实现
- https://github.com/enVolt/html-to-prosemirror
  - Takes HTML and outputs ProseMirror compatible JSON. originally written for PHP

- https://github.com/SebastianPodgajny/prosemirror-html-to-json
  - This library is used to convert HTML to prosemirror JSON format on backend

- https://github.com/tiavina-mika/tiptap-parser /202410/ts
  - HTML parser for Tiptap editor build on the of html-react-parser with code syntax highlighting.

- https://github.com/ShreyRavi/prosemirror-toc
  - An implementation of a table of contents using prosemirror within React.

- https://github.com/ocavue/prosemirror-virtual-cursor /83Star/MIT/202408/ts/inactive
  - https://prosemirror-virtual-cursor.vercel.app/
  - a plugin that adds a virtual cursor (or caret) to your editor. 
  - It implements the bike-style cursor, which shows a tail under the cursor between mark boundary.
  - 在光标竖线的底部显示向左或向右的短横，来表名行内marker的边界
  - Under the hood, I hide the native cursor and use `Decoration.widget` to insert a `<span>` element to the cursor position
    - 👉🏻 I refactored prosemirror-virtual-cursor and overlay the cursor over the editor.

- https://github.com/lukesmurray/prosemirror-async-query /MIT/202112/ts/inactive
  - A simple declarative API for using promises in prosemirror plugin state.

- https://github.com/alexzavgorodnii/tiptap-trailing-paragraph /202506/ts
  - https://alexzavgorodnii.github.io/tiptap-trailing-paragraph/
  - A Tiptap extension that ensures there's always a trailing paragraph at the end of your document, making it easy for users to continue typing after any content block.

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
  - https://github.com/evolvedbinary/prosemirror-lwdita
    - LwDITA and ProseMirror Integration

- https://github.com/artcompiler/L123
  - A language for writing ProseMirror editors

- https://github.com/guardian/prosemirror-invisibles
  - https://guardian.github.io/prosemirror-invisibles/
  - A simple implementation of invisible characters in ProseMirror.
  - A plugin that uses decorations to show invisible characters in ProseMirror

- https://github.com/guardian/prosemirror-noting
  - https://guardian.github.io/prosemirror-noting/
  - This plugin allows you to add notes as marks to prosemirror. 支持 toggle note

- https://github.com/xylk/prosemirror-compress /201805/js
  - ProseMirror data compression

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

- https://github.com/buttondown/tiptap-math /MIT/202406/ts
  - https://codesandbox.io/p/devbox/tiptap-math-example-777xhm
  - A LaTeX extension for Tiptap

- https://github.com/aarkue/tiptap-math-extension /MIT/202504/ts
  - https://aarkue.github.io/tiptap-math-extension/
  - Math Extension for the TipTap Editor
  - Use inline math expression / LaTeX directly in your editor
  - To correctly render the LaTeX expressions, you will also need to include the KaTeX CSS
  - KaTeX: A LaTeX rendering engine for the web, used to render LaTeX expressions.

- https://github.com/mattberkowitz/prosemirror-find-replace /MIT/201606/js/inactive
  - Find & Replace plugin for ProseMirror

- https://github.com/uniwebcms/semantic-parser /apache2/202502/js
  - A semantic parser for ProseMirror/TipTap content structures that helps bridge the gap between natural content writing and component-based web development.

- https://github.com/mizuka-wu/styled-textarea /202501/ts
  - https://mizuka-wu.github.io/styled-textarea/
  - 一个基于 Web Components 的自定义文本编辑器组件，支持对文本应用自定义样式标记。
  - 底层使用 ProseMirror 实现，提供了与原生 textarea 相似的使用体验。
  - 与原生 textarea 行为一致
  - 基于 Web Components，易于集成

- https://github.com/gavwuorg/prosemirror-character-count /202304/ts
  - plugin to counting the characters in the editor

- https://github.com/gfrancine/screenplay /202112/ts/inactive
  - A screenwriting toolkit based on Prosemirror
  - https://github.com/AmmariAbdelmounaim/screenplay-tiptap-editor

- https://github.com/itsarnaud/tiptap-fontsize-extension /MIT/202504/js
  - extension for adjusting font size in text editors.
# selection
- https://github.com/xnimorz/selection-range-enhancer /202010/ts
  - A project, which enhances abilities of selectionRange. It allows to track changes, works with carets and so on

- https://github.com/retentioneering/retentioneering-dom-observer /202111/ts
  - tools for parsing DOM data, observing DOM and tracking changes
  - a wrapper over MutationObservers, allowing you to observe changes even of those nodes that are not already in the DOM.

- https://github.com/fourwaves/tiptap-extension-selection-decoration /202410/ts
  - a selection decoration extension for Tiptap. 
  - It allows text to remain visibly selected, even when you focus out of the editor, offering a more flexible and customizable selection behavior.
  - This is especially useful in cases where native selections disappear when the editor loses focus, such as when interacting with other elements (e.g., dropdowns) in the editor interface.
# hotkeys/input
- https://github.com/juliankrispel/prosemirror-better-backspace /202507/ts
  - https://jkrsp.com/blog/prosemirror-backspace-problem/
  - plugin that provides better backspace behavior for list items and empty paragraphs
  - Empty paragraphs are merged with previous text containers when backspacing
  - Schema Agnostic: Works with any ProseMirror schema that includes list items and paragraphs

- https://github.com/ocavue/prosemirror-safari-ime-span /202407/ts
  - This module exports a ProseMirror plugin to work around the bug in Safari where IME text replacement removes empty nodes when the composition finishes.
# mobile
- https://github.com/amjadbouhouch/rn-text-editor /22Star/MIT/202405/ts/inactive
  - an evolving and feature-rich text editor package for React Native 

- https://github.com/nstfkc/tiptap-react-native-example /202308/ts/inactive
  - An example project that shows how to implement a rich text editor with tiptap.dev and react native
# import/export
- https://github.com/Intevation/tiptap-extension-office-paste /MIT/202507/ts
  - This extension fixes format of text copied from MS Office and pasted into the Tiptap editor.

- https://github.com/unicscode/tiptap-clean-paste /202408/ts
  - a plugin for Tiptap that provides a clean paste functionality for your editor. 
  - It allows you to strip unwanted content from pasted text, such as formatting, styles, or non-printable characters.

- https://github.com/vovanushka/ProseMirror2PDF /202410/go/inactive
  - send JSON data to the server and receive a PDF in response

- https://github.com/remirror/prosemirror-migration /202203/ts/inactive
  - a tool for migrating ProseMirror documents when you have breaking changes to your document schema.
  - It takes a JSON encoded ProseMirror document, and recursively descends through each node, executing a migration strategy for a node type.
# integrations
- https://github.com/haydenbleasel/tiptap-extension-jira /MIT/202412/ts
  - A collection of Tiptap extensions that enable bidirectional sync with Jira. 
  - It works by introducing a series of Nodes and Marks unique to the Atlassian Document Format (ADF) that can be used to render Jira content in a TipTap document.
# more-utils
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
