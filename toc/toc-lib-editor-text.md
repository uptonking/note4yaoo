---
title: toc-lib-editor-text
tags: [lib, text-editor, toc]
created: 2021-07-27T15:11:58.769Z
modified: 2021-07-27T15:12:39.959Z
---

# toc-lib-editor-text

# guide

- 编辑器的复杂度很大一部分来自跨平台的兼容性，而这不是靠rust能够解决的
# editor-starter
- pell /11.8kStar/MIT/201812/js/单文件
  - https://github.com/jaredreich/pell
  - https://jaredreich.com/pell/
  - smallest WYSIWYG text editor with no dependencies

- https://github.com/victrme/pocket-editor /ts/NoDeps/块级选区
  - https://pocketeditor.vercel.app/
  - fast block style wysiwyg editor that returns markdown
  - Reliable markdown output

- modern-editor-core /3Star/MIT/202210/ts/代码少
  - https://github.com/qq15725/modern-editor-core
  - A modern rich text editor core.
  - 只依赖immer
  - 未实现undo-redo，定义了模型和op

- Trumbowyg /3.8kStar/MIT/202210/js/单文件
  - https://github.com/Alex-D/Trumbowyg
  - https://alex-d.github.io/Trumbowyg
  - a simple and lightweight WYSIWYG editor, weight only 20kB minifed (8kB gzip) for faster page loading.
  - You can create your own plugins 

- https://github.com/tzhangchi/docs
  - https://tzhangchi.github.io/docs/
  - Docs editor - the design idea is based on Google Docs.

- stylo /603Star/MIT/202211/ts/NoDeps
  - https://github.com/papyrs/stylo
  - https://stylojs.com/
  - 代码不多，结构清晰
  - WYSIWYG interactive editor for JavaScript. 
  - Its goal is to bring great user experience and interactivity to the web, with no dependencies. 
  - Framework agnostic
  - Stylo controls what happens on every mutation. 
    - While a handful of actions in the alpha version still rely on `execCommand` to apply styles (e.g. bold, italic) - the core of the library does not. 
  - To keep track of the changes for a custom "undo redo" stack and to forward the information to your application, the component mainly uses the `MutationObserver` API.

- Squire /4.4kStar/MIT/202111/js
  - https://github.com/neilj/Squire
  - http://neilj.github.io/Squire/
  - Squire is an HTML5 rich text editor, with no dependencies
  - It was designed to handle email composition for the Fastmail web app. 
    - it must handle arbitrary HTML, because it may be used to forward or quote emails from third-parties and must be able to preserve their HTML without breaking the formatting. 
    - This means that it can't use a more structured (but limited) internal data model (as most other modern HTML editors do) and the HTML remains the source-of-truth.

- tiny-editor /58Star/MIT/202202/js
  - https://github.com/fvilers/tiny-editor
  - https://fvilers.github.io/tiny-editor
  - A tiny HTML rich text editor written in vanilla JavaScript

- https://github.com/TheNocoder/ncSimpleHtmlEditor  /js
  - 偏向页面编辑器
  - smallest WYSIWYG web content editor, entire document, body and head, no dependencies.
  - Allows you to edit the content of previously created templates or designs, it does not have options to change the design.
  - Unlike other editors, it allows you to edit the entire document, body and head, also does not use deprecated execCommand().

- https://github.com/cnuebred/octapus
  - modular WYSIWYG rich text editor
  - 代码量很少

- https://github.com/shredx/editor-vanillsjs
  - Editor completely made in Vanillajs. 
  - We are using plugin architecture.

- https://github.com/juliankrispel/zettel
  - Javascript framework for writing rich text applications

- https://github.com/joaomelo/textorama /202301/js/vue
  - https://github.com/joaomelo/textorama
  - a web editor that works with plain text files in your local system
  - 依赖codemirror6、vue3、vuestic-ui
  - The content is in your disk in a universal open format, and the browser ensures the editor only accesses the files you permit
  - Support for the markdown syntax. It is still portable plain text but visually enriched
# markdown-editor
- web-editor-markdown /90Star/MIT/202211/ts
  - https://github.com/Ben-love-zy/web-editor-markdown
  - 基于 Web 浏览器，即时渲染的 Markdown 编辑器。它基于 TypeScript 和 vanillajs 打造，并且不依赖任何第三方框架，对中文支持友好
  - 提供源码模式、双屏渲染模式、实时编辑模式和只读模式四种渲染模式。
  - 如果有需要，它的底层同时也支持了协同编辑的能力，提供了原子操作 Operation 用于扩展协同编辑。

- https://github.com/youking-lib/marktion
  - https://editor.marktion.io/
  - 可切换阅读和文本，阅读模式可编辑
  - 依赖immer

- https://github.com/imzbf/md-editor-rt
  - Markdown editor for react, developed in jsx and typescript.
  - https://github.com/imzbf/md-editor-v3 /vue3

- https://github.com/test-it-edu/notebook-dev /ts
  - Notebook is a simple Markdown and LaTeX Math editor build in React. 
  - The goal of this project is to create a modular / extensible editor for the web

- https://github.com/sofish/pen /201809/js/inactive
  - https://sofish.github.io/pen
  - enjoy live editing (+markdown)
  - used by Teambition
# editor-electron
- https://github.com/pulsar-edit/pulsar /MIT/202401/js
  - https://pulsar-edit.dev/
  - A Community-led Hyper-Hackable Text Editor, Forked from Atom, built on Electron.
  - Designed to be deeply customizable, but still approachable using the default configuration.
  - [Porting Teletype from Atom repo a.k.a Collaboration tool_202305](https://github.com/pulsar-edit/pulsar/issues/536)
    - The main issue is that Teletype runs on a server and we simply might not be able to justify running such a service without charging a maintenance cost for access.
  - https://github.com/atom-community/atom
    - Community build of the hackable text editor
# desktop-editor
- https://github.com/lapce/lapce
  - written in pure Rust with a UI in Druid (which is also written in Rust). 
  - It is designed with Rope Science from the Xi-Editor which makes for lightning-fast computation, and leverages OpenGL for rendering.

- https://github.com/jkhaui/rxeditor-2
  - an attempt at creating an open-source, web-based and lightweight alternative to word processors like Google Docs or Microsoft Word. 
  - It is built on Draft.js, ReactiveX (RxJS) and MobX.
  - Most features are currently not implemented; the main purpose of this demo currently is to show how pagination can be achieved in a web-based word processor. 
# editor-server

## non-js

- https://github.com/huacnlee/actiontext-lite /202002/ruby/inactive
  - [我终于受不了 ActionText，做了一个 Lite 版本 · Ruby China](https://ruby-china.org/topics/39130)
  - ActionText 默认高度集成了 Trix，但实际情况是 Trix 在 90% 的项目情况下都不符合实际的需求，我们的用户、后台编辑人员不喜欢它
  - Active Storage 为默认的附件存储，也是高度集成，难以清理干净，可它往往也不符合我们的需求，我们正文的附件、图片往往是需要公开的 URL 地址（Active Storage 目前不支持）
  - Action Text 带有默认的 HTML sanitize 规则，但那个规则过于严苛
  - 类似 ActiveText 的存储 API，兼容 ActionText 的 Model API，你可以保持那个好的东西
  - 数据存储依然保持在 ActionText 那个 action_text_rich_texts 表里面，所以引入它，只是会让 ActionText 没了 Trix 和 ActiveStorage 的集成
  - 你存什么进去，就拿什么出来，不做任何 sanitize 处理，把规则交给你自己处理

- https://github.com/helix-editor/helix /MPLv2/202402/rust
  - https://helix-editor.com/
  - A Kakoune/Neovim inspired editor, written in Rust.
  - [Plugin system](https://github.com/helix-editor/helix/discussions/3806)
  - [WebAssembly plugins system](https://github.com/helix-editor/helix/issues/122)
# editor-utils
- https://github.com/juliankrispel/react-text-selection-popover
  - https://juliankrispel.github.io/react-text-selection-popover
  - A react component that lets you render a popover in relation to the current text selection.

- https://github.com/ktsn/selective-undo-text
  - https://codepen.io/ktsn/pen/qZxdaY
  - A Selective Undo library for text editing
  - [Undo for selection/emacs · Issue · microsoft/vscode](https://github.com/microsoft/vscode/issues/108098)
    - When there is an active region, any use of undo performs selective undo: 
    - it undoes the most recent change within the region, instead of the entire buffer.

- [Cross-Browser Selection Utilities](https://gist.github.com/tcr/1022198/2dd0aefdc17c77b0997a09efa10247e511a4f92a)
# more-editor
- hypertext-editor /28Star/MIT/202211/js/tinymce
  - https://github.com/russellbeattie/hypertext-editor
  - https://www.hypertext.plus/
  - a new rich-text editor for creating documents using HTML instead of using an 18 year old text format or complex word processor files.
  - Hypertext is both a web app for creating and editing these documents, as well as a proposal for a new `.htmd` document format. 
  - The vision is to create a specification for a standard, safe, guaranteed-editable document using a strict-subset of HTML and CSS which replaces the variety of Markdown, AsciiText, Office file formats, etc. 

- https://github.com/digabi/rich-text-editor /67Star/MIT/202311/js
  - http://digabi.github.io/rich-text-editor/
  - Math editor
  - Rich text editor with math support for Finnish Matriculation Examination Board
  - allow candidates to attach screenshots and write equations as part of their submissions.
  - by MathJax and MathQuill, jquery

- https://github.com/liferay/alloy-editor /ckeditor.v4
  - http://alloyeditor.com/
  - WYSIWYG editor based on CKEditor with completely rewritten UI
  - [Switch to CKEditor5 因为许可协议问题已放弃升级](https://github.com/liferay/alloy-editor/issues/618)

- https://github.com/meta-explore/explore-editor /js
  - https://meta-explore.github.io/explore-editor/
  - A powerful WYSIWYG rich text web editor by pure javascript

- akilli-editor /14Star/MIT/202211/js
  - https://github.com/akilli/editor
  - https://akilli.github.io/editor/demo
  - A HTML standards-compliant and dependency-free rich text editor.
  - The editor consists of a main toolbar, a formatbar, a focusbar and a content area.
- lyove-editor /4Star/MIT/202211/js
  - https://github.com/lyove/editor
  - https://lyove.github.io/editor
  - A HTML standards-compliant and dependency-free rich text editor.

- https://github.com/pacocoursey/writer /291Star/NALic/202110/js/inactive
  - https://writer.paco.sh/
  - Plain text editor from scratch, made for the web. Drag and drop files to open them.
  - Buffer is an array of array of lines
  - Text is manually measured and wrapped with canvas
  - Lines are virtualized on scroll and drawn as divs

- https://github.com/artuntun/recursive-text-editor
  - a text editor akin to the ones used by Roam Research, Logseq, Athens..
  - 依赖react-contenteditable

- https://github.com/Cotter45/proof_of_concept
  - little proof of concept for a type of wysiwyg editor #messycode
  - 前后端2个文件夹

- https://github.com/oidoid/linear-text
  - Linear Text is a graphical line-oriented text editor

- https://github.com/benjamn/kix-standalone /201007/js/archived
  - A standalone version of Google's new rich text editor, Kix
