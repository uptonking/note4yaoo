---
title: lib-edit-typst-examples
tags: [examples, typst]
created: 2025-12-25T19:55:00.820Z
modified: 2025-12-25T19:55:10.911Z
---

# lib-edit-typst-examples

# guide

- resources
  - https://github.com/search?type=code&q=typst++++path%3Apackage.json+NOT+is%3Afork
# popular
- https://github.com/TeXlyre/texlyre /537Star/AGPLv3/202512/ts
  - https://texlyre.github.io/
  - https://texlyre.github.io/texlyre
  - A local-first LaTeX & Typst web editor with real-time collaboration & offline support
  - Built with React, TypeScript, and Yjs
  - 依赖codemirror6、@lezer/highlight、typstyle-wasm-bundler、wasm-latex-tools、pdfjs、react-pdf
  - TeXlyre provides comment and chat features for real-time exchanges, reviews, and discussions among collaborators.
  - The platform integrates `SwiftLaTeX` WASM engines to provide in-browser LaTeX compilation without server dependencies. 
    - Currently supports `pdfTeX` and `XeTeX` engines for document processing. 
    - TeXlyre supports real-time syntax highlighting and error detection, with an integrated PDF viewer that offers zoom, navigation, and side-by-side editing capabilities.
  - The platform integrates `typst.ts` to provide in-browser Typst compilation without server dependencies. 
    - Currently supports PDF, SVG, and canvas compilation, however, SVG and HTML compilation are experimental, and are not guaranteed to work as expected at the time being.
  - Local-first Architecture
    - All documents are stored locally using IndexedDB, enabling full offline editing with automatic synchronization when connectivity returns. 
    - The File System Access API provides direct folder synchronization for external backup solutions
  - The plugin system allows extensibility through custom viewers, renderers, and backup providers. 
    - Core plugins handle PDF rendering, LaTeX and Typst log visualization, and file system backup operations. Theme plugins provide customizable layouts and visual styles.
  - TeXlyre is licensed under AGPL-3.0 due to our dependency on SwiftLaTeX's AGPL-licensed LaTeX engine (WASM) for in-browser LaTeX compilation.
  - https://github.com/SwiftLaTeX/SwiftLaTeX /2.2kStar/AGPL/202406/cpp/c/inactive
    - SwiftLaTeX, LaTeX Engines in Browsers with optional WYSIWYG support. We are a big fan of WebAssembly and all computation is done locally.
- https://github.com/TeXlyre/codemirror-latex-visual /MIT/202509/ts
  - https://texlyre.github.io/codemirror-latex-visual/
  - This package provides WYSIWYM visual editing for LaTeX documents in CodeMirror 6, designed to work with academic writing workflows and document preparation
  - 依赖codemirror6、mathlive
  - 已移除prosemirror依赖
  - 不支持分页
  - Real-time bidirectional synchronization between source and visual editors
  - Visual representation of LaTeX structures (sections, math blocks, environments)
  - Mathlive rendering and editing for math content

- https://github.com/dereklei12/Typst-Editor /202510/js/inactive
  - A React-based WYSIWYG editor for Typst documents with real-time preview.
  - Rich Text Editing: Tiptap-based editor with toolbar
  - Real-time Preview: Live PDF preview
  - The editor requires a Typst compilation server running, Compile Typst to PDF
# examples
- https://github.com/EMOAIRX/ppt-agent /202510/ts/vue/inactive
  - https://emoairx.github.io/ppt-agent/
  - 一个基于 Vue 3 和 TypeScript 的AI驱动演示文稿编辑器，支持 Typst 格式的幻灯片创建和编辑。
  - 使用强大的Typst标记语言编写专业演示文稿
  - 实时预览：即时编译和渲染Typst内容，所见即所得
  - 一键导出整个演示文稿为PDF格式
  - 用户手动编辑和AI自动编辑可能产生冲突, 实现简单而有效的编辑锁机制, AI编辑时锁定用户界面

- https://github.com/wflixu/typster /54Star/MIT/202512/rust/ts/vue
  - 现代化的 Typst 可视化编辑器 - 提供 Typora 风格的所见即所得编辑体验
  - 基于 Tauri 2.0 + Vue 3 + TypeScript 构建的现代化桌面应用，专注于为 Typst 标记语言提供直观、高效的编辑体验。
  - 核心目标: 通过"混合编辑模式"，将 Typst 的强大功能与 简单的编辑体验相结合
  - 核心对标: Typora (Markdown 编辑器) + Typst (现代化排版系统)
  - 似乎只支持mac?
  - 功能实现有问题, 最近的pr在调整目标和大修改代码 [next version ](https://github.com/wflixu/typster/pull/15)
# utils
- https://github.com/Myriad-Dreamin/tinymist /2.6kStar/apache2/202512/rust/ts
  - https://myriad-dreamin.github.io/tinymist
  - an integrated language service for Typst

- https://github.com/SadmanKibria/tailvia-pdf-engine /MIT/202506/js/inactive
  - A simple API that takes a Typst template with `{{placeholders}}` and JSON data, fills it in, compiles the Typst code to PDF and returns the result as a downloadable file.

- https://github.com/OI-wiki/OI-Wiki-export/tree/master/remark-typst /MIT/202508/js/inactive
  - 为 OI Wiki 的 Typst PDF 自动化导出工具开发的 Markdown 到 Typst 编译器。
  - https://github.com/OI-wiki/OI-Wiki-export/tree/master/oi-wiki-export-typst
    - Markdown 源文档到 Typst 的转换通过 remark-typst 完成。
    - TeX 公式到 Typst 的转换通过 mitex完成。
    - 二维码的生成通过 tiaoma 插件完成；插件的二进制文件已包含在根目录当中。
# latex
- overleaf /10.5kStar/AGPLv3/202211/js/latex/ace>codemirror
  - https://github.com/overleaf/overleaf
  - https://github.com/overleaf/overleaf/wiki
  - https://github.com/overleaf/overleaf/tree/main/services/web/frontend/js/features/source-editor
  - A web-based collaborative LaTeX editor
  - source-editor支持codemirror6、ace
  - https://github.com/overleaf/ace /Ajax.org Cloud9 Editor
  - [Compile Error and PDF Download Notifications](https://github.com/overleaf/overleaf/issues/1031)
    - migrate from ACE to CodeMirror 6. Yes, the CM6 work will be coming to CE soon._202206

  - https://github.com/overleaf/ace
  - https://github.com/amitness/open-in-overleaf
    - Open latex of any arxiv.org paper on overleaf

- https://github.com/fiduswriter/fiduswriter /js/python
  - https://fiduswriter.org/
  - an online collaborative editor especially made for academics who need to use citations and/or formulas.

- https://github.com/michael-brade/LaTeX.js /858Star/MIT/202304/livescript/inactive
  - https://latex.js.org/
  - https://latex.js.org/playground.html
    - 在线示例渲染的文档没有分页效果
  - a LaTeX to HTML5 translator written in JavaScript using PEG.js. 
  - LaTeX.js tries to be absolutely and uncompromisingly exact and compatible with LaTeX. 
  - If you need a LaTeX to HTML translator that also understands TeX to some extent, take a look at: tex4ht、latex2html

- https://github.com/manuels/texlive.js /inactive
  - http://manuels.github.com/texlive.js/
  - Compiling LaTeX (TeX live) in your browser
  - This is a port of TeX live 2016 to Javascript. It is based on the port of the pdftex TeX compiler to Javascript using emscripten. It creates PDF files from LaTeX code and supports packages.

- https://github.com/SaswatPadhi/pseudocode.js /js
  - https://saswatpadhi.github.io/pseudocode.js
  - a JavaScript library that typesets pseudocode beautifully to HTML.
  - Pseudocode.js takes a LaTeX-style input that supports the algorithmic constructs from LaTeX's algorithm packages
  - The HTML output produced by pseudocode.js is (almost) identical with the pretty algorithms printed on publications that are typeset by LaTeX.
  - pseudocode.js can render math formulas using either KaTeX, or MathJax.

- https://github.com/James-Yu/LaTeX-Workshop
  - an extension for Visual Studio Code, aiming to provide core features for LaTeX typesetting with Visual Studio Code.

## tex-markdown

- https://github.com/susam/texme /js
  - a lightweight JavaScript utility to create self-rendering Markdown + LaTeX documents.

- https://github.com/parpalak/upmath.me
  - Markdown and LaTeX online editor - create text for web with equations and diagrams
# math
- https://github.com/dbccccccc/TypstPad /MIT/202512/ts
  - https://typstpad.com/
  - A simple and elegant online Typst formula editor with real-time preview
  - SVG, PNG, JPG导出下载，支持将PNG复制到剪切板
  - SVG, HTML, typ代码文件下载&复制
  - 现在暂时还没有对移动端进行优化，后续版本可能会添加
  - [TypstPad: 一个在线Typst公式编辑器 ](https://linux.do/t/topic/1364899)

- https://github.com/cortex-js/compute-engine /ts
  - https://cortexjs.io/
  - An engine for symbolic manipulation and numeric evaluation of math formulas expressed with MathJSON
  - MathJSON is a lightweight mathematical notation interchange format based on JSON.
  - The Cortex Compute Engine can parse LaTeX to MathJSON, serialize MathJSON to LaTeX, format, simplify and evaluate MathJSON expressions.

- https://github.com/KaTeX/KaTeX /js/NoDeps
  - https://katex.org/
  - Fast math typesetting for the web.
  - KaTeX renders its math synchronously and doesn't need to reflow the page. See how it compares to a competitor in this speed test.
  - KaTeX's **layout** is based on **Donald Knuth's TeX**, the gold standard for math typesetting.
  - support ssr
  - KaTeX supports much (but not all) of LaTeX and many LaTeX packages.

- https://github.com/pyramation/LaTeX2JS /js
  - Author interactive math equations and diagrams online using LaTeX and PSTricks
  - thanks to MathJax
# word/wps
- https://github.com/moon-like-gray-cat/WordFormatter /202512/python
  - 用于 自动整理 Word 文档标题编号与段落格式的桌面轻量级工具。
  - 它能帮助用户一键格式化word文档，方便生成目录、规范论文或课程报告的排版。
  - 根据用户设置的标题的格式（例如 1. （一））, 识别每级标题和正文，并应用用户规定的字体, 字号与是否加粗
  - 具备段落统一缩进的功能，会将所有的段落都顶格，并首行缩进两个字符 所有的标题也会左对齐
  - 要求>win7操作系统
# more
