---
title: toc-lib-editor-text
tags: [lib, text-editor, toc]
created: 2021-07-27T15:11:58.769Z
modified: 2021-07-27T15:12:39.959Z
---

# toc-lib-editor-text

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

- https://github.com/inokawa/rich-textarea
  - https://inokawa.github.io/rich-textarea/
  - A small customizable textarea for React to colorize, highlight, decorate texts, offer autocomplete and much more.
  - designed to behave as native textarea as much as possible. Supports formik and react-hook-form. 
  - IME composition handling: IME related events have some cross browser problems. This library handles them for easy to use.

- https://github.com/TheNocoder/ncSimpleHtmlEditor  /js
  - 偏向页面编辑器
  - smallest WYSIWYG web content editor, entire document, body and head, no dependencies.
  - Allows you to edit the content of previously created templates or designs, it does not have options to change the design.
  - Unlike other editors, it allows you to edit the entire document, body and head, also does not use deprecated execCommand().

- https://github.com/cnuebred/octapus
  - modular WYSIWYG rich text editor
  - 代码量很少
# markdown-editor
- yfm-editor /3Star/MIT/202211/ts/md-it
  - https://github.com/yandex-cloud/yfm-editor
  - https://ydocs.tech/en/
  - https://preview.yandexcloud.dev/yfm-editor/
  - 依赖prosemirror、markdown-it、react-use、gravity-ui
  - Yandex Flavored Markdown (YFM) is a Markdown dialect and a set of tools for transforming Markdown to HTML in real time and building complete documentation projects.
  - Expandable: you can add any plugin for markdown-it or write your own.

- https://github.com/Resetand/textarea-markdown-editor  /ts
  - UI headless simple markdown editor using only textarea
  - 依赖react
  - You can choose any markdown parser, create your own layout, and use your own textarea component that is styled and behaves however you like

- https://github.com/kumachan-mis/react-realtime-markup-editor
  - A text document editor which is syntactically formattable in real time
  - 类似typora的即时渲染
  - 依赖react、katex、emotion
  - 组件采用atoms/molecules/organisms结构

- https://github.com/GDUcrash/write
  - https://writeapp.vercel.app/
  - Extremely minimalistic text editor
  - 依赖react-markdown

- https://github.com/donny-chan/qingshu
  - A modern, minimalistic Markdown editor for Windows, implemented in Vue + Electron + TypeScript.
  - Support GitHub Flavored Markdown + LaTeX (including inline math).

- https://github.com/Eroxl/Note-Rack
  - An inline WYSIWYG markdown editor built for students to manage school work
# mobile-editor
- zx-editor /319Star/MIT/202209/ts
  - https://github.com/capricorncd/zx-editor
  - https://capricorncd.github.io/zx-editor/
  - 移动端HTML文档（富文本）编辑器，支持图文混排、引用、大标题、无序列表，字体颜色、加粗、斜体

- medit /160Star/MIT/201708/js
  - https://github.com/echosoar/medit
  - https://medit.js.org/demo.html
  - 专注做一个更具价值和体验的移动端富文本编辑器，所以Medit目前不支持Pc端使用，仅支持移动端

- https://github.com/deadlyjack/Acode
  - powerful text/code editor for android
  - You can use this editor for editing HTML, CSS, JavaScript, text files etc.

- https://github.com/siposdani87/expo-rich-text-editor
  - This rich text editor written in TypeScript and use React Hooks structure. 
  - This component use the HTML ContentEditable div feature and React communicate and send data to native JavaScript via WebView.

- https://github.com/imgly/catalog-react-native
  - customizable photo and video editor for your app.
# more-editor
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
