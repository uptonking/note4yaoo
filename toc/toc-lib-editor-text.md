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

- modern-editor-core /3Star/MIT/202210/ts/代码少
  - https://github.com/qq15725/modern-editor-core
  - A modern rich text editor core.
  - 只依赖immer
  - 未实现undo-redo，定义了模型和op

- Trumbowyg /3.8kStar/MIT/202210/js/单文件
  - https://github.com/Alex-D/Trumbowyg
  - https://alex-d.github.io/Trumbowyg
  - a simple and lightweight WYSIWYG editor, weight only 20kB minifed (8kB gzip) for faster page loading.

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
# desktop-editor
- https://github.com/lapce/lapce
  - written in pure Rust with a UI in Druid (which is also written in Rust). 
  - It is designed with Rope Science from the Xi-Editor which makes for lightning-fast computation, and leverages OpenGL for rendering.

- https://github.com/jkhaui/rxeditor-2
  - an attempt at creating an open-source, web-based and lightweight alternative to word processors like Google Docs or Microsoft Word. 
  - It is built on Draft.js, ReactiveX (RxJS) and MobX.
  - Most features are currently not implemented; the main purpose of this demo currently is to show how pagination can be achieved in a web-based word processor. 
# editor-utils
- [Cross-Browser Selection Utilities](https://gist.github.com/tcr/1022198/2dd0aefdc17c77b0997a09efa10247e511a4f92a)
# more-editor
- hypertext-editor /28Star/MIT/202211/js/tinymce
  - https://github.com/russellbeattie/hypertext-editor
  - https://www.hypertext.plus/
  - a new rich-text editor for creating documents using HTML instead of using an 18 year old text format or complex word processor files.
  - Hypertext is both a web app for creating and editing these documents, as well as a proposal for a new `.htmd` document format. 
  - The vision is to create a specification for a standard, safe, guaranteed-editable document using a strict-subset of HTML and CSS which replaces the variety of Markdown, AsciiText, Office file formats, etc. 

- https://github.com/digabi/rich-text-editor
  - http://digabi.github.io/rich-text-editor/
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
