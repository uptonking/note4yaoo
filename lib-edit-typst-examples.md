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
- https://github.com/Myriad-Dreamin/typst.ts /907Star/apache2/202512/rust/ts
  - https://myriad-dreamin.github.io/typst.ts
    - 示例渲染为html元素，文字可选择，但没有视觉上的分页线
  - a project dedicated to bring the power of typst to the world of JavaScript
  - 效果类似付费版 [Typst: The new foundation for documents](https://typst.app/play)
    - 此示例右侧预览pdf渲染为`<canvas>`元素
  - https://github.com/tfachmann/typst-as-library /apache2/202511/rust
    - Simple demo that demonstrates how to use typst as a library in Rust
  - [Use typst as library in browser? · Issue · typst/typst _202304](https://github.com/typst/typst/issues/909)
    - Typst can be compiled to WASM, but no JS glue is available, you'd have to write that yourself. It's not as simple as compile(string) because you also need to provide fonts, and if you want a multi-file setup of course also files.
  - https://github.com/Myriad-Dreamin/shiroa /590Star/apache2/202512/rust
    - https://myriad-dreamin.github.io/shiroa/
    - a simple tool for creating modern online books in pure typst
    - heavily inspired by mdBook, but it is considered to be more adapted to Typst style, hence no guarantee of compatibility with mdBook

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

- https://github.com/Bzero/typstwriter /139Star/MIT/202511/python
  - An integrated editor for the typst typesetting system.
  - Integrated Document Viewer
  - Integrated File System viewer

- https://github.com/Cubxity/typstudio /713Star/GPL/202403/rust/svelte/tauri/inactive
  - A W. I. P desktop application for a new markup-based typesetting language, typst. 
  - Typstudio is built using Tauri.

- https://github.com/tyx-editor/TyX /144Star/MIT/202512/rust/ts/lexicaljs
  - https://tyx-editor.com/
  - https://app.tyx-editor.com/
  - A LyX-like experience rewritten for Typst and the modern era
  - 编辑器支持富文本编辑和markdown快捷键
  - TyX uses `MathLive` to make math formula editing easy by seeing the formula you're editing! This is currently LaTeX-based. We are working on a Typst-based editor
  - 默认保存为 .tyx 后缀的文件, 里面内容是json
  - 👀 不支持读取 .typ 文件, 支持导出 .typ/.pdf
  - you can open .typ files into TyX
  - still a work in progress. Many Typst features are currently not imported correctly.
  - [Announcing TyX - A LyX-like experience rewritten for Typst and the modern era _202505](https://forum.typst.app/t/announcing-tyx-a-lyx-like-experience-rewritten-for-typst-and-the-modern-era/3976)
  - [Change from tyx to typ extension _202505](https://github.com/tyx-editor/TyX/issues/17)
    - The TyX file stores what's seen in the WYSIWYG editor - it's TipTap JSON. There's no use using the .typ extension because it's not Typst.
    - When compiling, a .typ file is generated, see main/src/compilers/tyx2typst.ts
    - I think we could develop a tiptap `typst-math` node step by step
    - The editor is now Lexical instead of TipTap - sadly sort-of schema-less. There is a JSON Schema tho, and generating Rust from this specification may already have some library?
    -  typlite has conversion path typst document -> AST -> markdown, and the typst-tiptap was converting to tiptap based on the AST rather than markdown, i.e. before markdown conversion rather than after markdown conversion.

- https://github.com/rendercv/rendercv /12.3kStar/MIT/202512/python
  - https://docs.rendercv.com/
  - CV/resume generator for academics and engineers, YAML to PDF
  - Version-control your CV — it's just text.

- https://github.com/KaiserY/mdbook-typst-pdf /MIT/202506/rust/inactive
  - A mdBook backend for generate pdf (through typst).

- https://github.com/leichaoL/typst-table-paste /MIT/202512/ts
  - VSCode extension that automatically converts RTF or CSV tables from the clipboard to Typst table syntax.
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

- https://github.com/ra-jeev/write-assist-ai /MIT/202511/ts
  - OpenAI-powered Text Rewriter for VS Code. 
  - Works with Markdown, LaTeX, quarto, typst and text files.
# utils
- https://github.com/Myriad-Dreamin/tinymist /2.6kStar/apache2/202512/rust/ts
  - https://myriad-dreamin.github.io/tinymist
  - an integrated language service for Typst

- https://github.com/qwinsi/tex2typst-webapp /GPL/202512/js/svelte
  - https://qwinsi.github.io/tex2typst-webapp/
  - Translate between LaTeX / TeX math markup and Typst in your browser.
  - https://github.com/qwinsi/tex2typst /apache2/202512/ts
    - conversion between TeX/LaTeX and Typst math code.

- https://github.com/cetz-package/cetz /1.6kStar/LGPL/202512/typst/rust
  - https://cetz-package.github.io/
  - CeTZ (CeTZ, ein Typst Zeichenpaket) is a library for drawing with Typst with an API inspired by TikZ and Processing.
  - https://github.com/cetz-package/cetz-plot /LGPL/202509/typst
    - a library that adds plots and charts to CeTZ 

- https://github.com/touying-typ/touying /1.8kStar/MIT/202511/typst
  - https://touying-typ.github.io/
  - Touying (投影 in chinese, /tóuyǐng/, meaning projection) is a user-friendly, powerful and efficient package for creating presentation slides in Typst.
  - Touying does not rely on counter and context to implement #pause, resulting in better performance.
  - https://github.com/touying-typ/touying-exporter
    - Export presentation slides in various formats
- https://github.com/polylux-typ/polylux /MIT/202510/rust
  - A package for creating slides in Typst
- https://github.com/glambrechts/slydst /MIT/202511/typst
  - Create simple static slides with Typst
- https://github.com/OrangeX4/typst-pinit /MIT/202505/typst/inactive
  - Relative positioning by pins, especially useful for making slides in typst.
  - Pinit works with Touying or Polylux animations.
  - The idea of pinit is pinning pins on the normal flow of the text, and then placing the content on the page by absolute-place function.
  - 效果类似画箭头 ?
- https://github.com/skriptum/diatypst /MIT/202512/typst
  - http://mdwm.org/diatypst/
  - easy slides in typst
  - easy delimiter for slides and sections (just use headings)

- https://github.com/Glomzzz/typsite /MIT/202509/rust
  - https://typ.rowlib.com/en/
  - a static site generator (SSG) that uses pure Typst for content creation. 
  - It processes these Typst files to generate a complete static website.
  - Typst math -> Mathml （auto detected math-font)
  - Typst introduced HTML export functionality in version 0.13. This includes an `html-export` mode and two core functions: html.elem and html.frame. These allow us to write content in Typst that targets HTML+CSS output.

- https://github.com/clysto/typst-vscode /MIT/202511/js
  - A lightweight VS Code extension for Typst.
  - This is an extremely minimal Typst extension. It only connects VS Code to your own Tinymist executable and omits many client‑side features.
  - All features are powered by Tinymist.

- https://github.com/SadmanKibria/tailvia-pdf-engine /MIT/202506/js/inactive
  - A simple API that takes a Typst template with `{{placeholders}}` and JSON data, fills it in, compiles the Typst code to PDF and returns the result as a downloadable file.

- https://github.com/OI-wiki/OI-Wiki-export/tree/master/remark-typst /MIT/202508/js/inactive
  - 为 OI Wiki 的 Typst PDF 自动化导出工具开发的 Markdown 到 Typst 编译器。
  - https://github.com/OI-wiki/OI-Wiki-export/tree/master/oi-wiki-export-typst
    - Markdown 源文档到 Typst 的转换通过 remark-typst 完成。
    - TeX 公式到 Typst 的转换通过 mitex完成。
    - 二维码的生成通过 tiaoma 插件完成；插件的二进制文件已包含在根目录当中。

- https://github.com/observerw/typst-oxide-vscode /MIT/202507/ts/inactive
  - PKM for typst
  - A comprehensive VS Code extension for Typst that brings wiki-style bidirectional linking, smart autocompletion, and powerful navigation features to your Typst documents.

- https://github.com/ffy6511/Adjust-heading-in-tree /MIT/202512/ts
  - 针对 Markdown 与 Typst 文档的 VS Code 扩展，提供导航树、拖拽重排、批量层级调整与块级标签机制，帮助你像操作“块”一样管理整段内容。
  - 块级标签：使用Tag来组织管理您的文件! 为标题块添加标签，支持全局/当前文件切换、搜索、多选, 并可在 Tag 管理面板中自定义颜色、图标等；
  - 拖拽与同级重排：拖动标题即可连同子树迁移位置，同级内可用内联按钮或快捷键快速上/下移，保持结构一致；
  - 子树导出：将选中的标题子树导出为 PDF 或 PNG（需 Tinymist），便于分享或后续处理。

- https://github.com/CFiggers/typst-companion /MIT/202406/ts/inactive
  - A VS Code extension that adds Markdown-like editing niceties for typst (.typ) files on top of and in addition to to Nathan Varner's Typst LSP(deprecated).
  - Intuitive handling of Ordered and Unordered lists in .typ files.
  - Keyboard Shortcuts for: Toggle Bold, Italics, and Underline
  - The core logic of this extension is adapted, with attribution and gratitude, from [Markdown All in One](https://github.com/yzhang-gh/vscode-markdown) 

- https://github.com/lilaq-project/lilaq /563Star/MIT/202512/typst
  - https://lilaq.org/
  - a powerful plotting library for Typst.
  - Consistent styling and interoperability with Zero.

- https://github.com/Jollywatt/typst-fletcher /MIT/202508/typst
  - A Typst package for drawing diagrams with arrows, built on top of CeTZ.

- https://github.com/patrick-kidger/typst_pyimage /apache2/202512/python
  - Typst extension, adding support for generating figures using inline Python code
  - Usage is two steps. Write your content within the .typ file, and then run from the command line to build the content for Typst to actually import.

- https://github.com/mitex-rs/mitex /apache2/202512/rust
  - https://mitex-rs.github.io/mitex/
  - https://mitex-rs.github.io/mitex/tools/underleaf.html
  - LaTeX support for Typst, powered by Rust and WASM

- https://github.com/Mc-Zen/zero /MIT/202512/typst
  - Advanced scientific number formatting for Typst.
  - A number in scientific notation consists of three parts: the mantissa, an optional uncertainty, and an optional power (exponent). 

- https://github.com/lkoehl/typst-boxes /MIT/202504/typst
  - a Typst package for adding colorful, customizable boxes to your documents.
  - 类似callout/alert

- https://github.com/hongjr03/typst-zebraw /MIT/202512/typst
  - https://hongjr03.github.io/typst-zebraw/
  - a lightweight and fast package for displaying code blocks with line numbers in Typst, supporting code line highlighting.
  - 支持插入块元素

- https://github.com/Dherse/codly /MIT/202508/typst
  - package for even better code blocks
  - It allows you to add annotations, skip lines, customize numberings, add language icons, and much more.

- https://github.com/ludwig-austermann/typst-timetable /MIT/202509/typst
  - A typst template for timetables

- https://github.com/ntjess/typst-drafting /unlic/202505/typst/inactive
  - Margin notes cannot lay themselves out correctly until they know your page size and margins. 
  - By default, they occupy nearly the entirety of the left or right margin, but you can provide explicit left/right bounds if desired

- https://github.com/ParaN3xus/typress /MIT/202503/python/js
  - Typst Mathematical Expression OCR based on TrOCR.

- https://github.com/QuadnucYard/ourchat-typ /MIT/202512/typst
  - https://quadnucyard.github.io/ourchat-typ/
  - a Typst package for building chat UI mockups.

- https://github.com/Vanille-N/meander.typ /MIT/202512/typst/图文混排
  - provides a core function `reflow` to segment pages and wrap content around images

- https://github.com//wypst /MIT/202406/rust/js/inactive
  - https://0xbolt.github.io/wypst/
  - Typst math typesetting for the web. Renders into the HTML element/string
  - There's still no conclusive roadmap for native HTML export in Typst
  - 测试用例: sum_(n >= 1) 1/n^2 = pi^2/6

## markdown-typst

- https://github.com/SabrinaJewson/cmarker.typ /MIT/202512/rust
  - Transpile CommonMark Markdown to Typst, from within Typst
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
