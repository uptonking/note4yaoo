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
  - [The Raindrop-Blue Book (Typst中文教程)](https://typst-doc-cn.github.io/tutorial/)
# popular
- https://github.com/YDX-2147483647/best-of-typst /CC-SA/202512/python/typst
  - https://ydx-2147483647.github.io/best-of-typst/
  - A ranked list of awesome projects related to Typst, or the charted dark matter in Typst Universe (TCDM)

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
  - https://github.com/typst-community/typst.js /apache2/202312/ts/inactive
    - Provides a typed JavaScript API so you can typst.compile()

- https://github.com/Mapaor/typst-online-editor /MIT/202512/ts
  - https://typst-online-editor.vercel.app/
  - Typst online editor, built with NextJS using Typst.ts (Typst WASM compiler)
  - A lightweight web-based Typst editor that compiles documents directly in your browser using WebAssembly
  - Everything is client-side thanks to Typst.ts (wasm file is from their CDN).
  - Portable. The UI may not be framework-agnostic but the compiler logic is
  - https://github.com/Mapaor4/simple-typst-editor /minimal
    - https://typst-nextjs.vercel.app/
  - https://github.com/Mapaor/typst-online-vite
    - https://typst-online-vite.vercel.app/
    - This website is built with Svelte 5, Typst.ts (@myriaddreamin), PDF.js and Vite.
  - https://github.com/Mapaor/typst-wasm-demo /202508/ts
    - https://mapaor.github.io/typst-wasm-demo/
    - Demo website using typst.ts and React.

- https://github.com/Cierra-Runis/caduceus /MIT/202512/rust/ts
  - open-source alternative to Typst App. 
  - This project aims to provide a simple, self-hostable alternative for writing and compiling Typst documents in your browser.
- https://github.com/ParaN3xus/tyraria /GPL/202511/ts/vue
  - https://tyraria.typs.town/
  - Recreate the online editing experience of typst.app based on tinymist and typst.ts
  - Monaco Editor basic editing functionality
  - 直接使用了vscode shell的交互，右侧预览是svg

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

- https://github.com/cosformula/mdxport /MIT/202512/ts/svelte
  - https://www.mdxport.com/
  - Markdown to PDF, Perfect Typesetting, Powered by Typst.
  - 左边文本可编辑，右边预览只读
  - Runs entirely client-side using WebAssembly.
  - Mermaid diagrams
  - Math formulas (LaTeX syntax)
  - Syntax Highlighting for code blocks
  - [Built a browser-based PDF exporter using Typst + WASM (No Pandoc/LaTeX setup required) : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1ppmoql/built_a_browserbased_pdf_exporter_using_typst/)
    - 100% Local (WASM): It uses the Typst engine compiled to WebAssembly. all rendering happens in your browser. No data is sent to any server
    - Better Pagination: unlike the standard HTML-to-PDF print (which Obsidian uses), Typst handles page breaks smartly. It keeps table rows together and handles footnotes/math ($E=mc2$) beautifully.

- https://github.com/arashatt/typsy /202511/ts
  - https://typeset.live/editor
  - typst in browser

- https://github.com/dereklei12/Typst-Editor /202510/js/inactive
  - A React-based WYSIWYG editor for Typst documents with real-time preview.
  - Rich Text Editing: Tiptap-based editor with toolbar
  - Real-time Preview: Live PDF preview
  - The editor requires a Typst compilation server running, Compile Typst to PDF

- https://github.com/Bzero/typstwriter /139Star/MIT/202511/python
  - An integrated editor for the typst typesetting system.
  - Integrated Document Viewer
  - Integrated File System viewer
  - typst CLI has to be available to compile typst documents

- https://github.com/Cubxity/typstudio /713Star/GPL/202403/rust/svelte/tauri/inactive
  - A W. I. P desktop application for a new markup-based typesetting language, typst. 
  - Typstudio is built using Tauri.
  - https://github.com/Ahdeyyy/typwriter /rust/ts/svelte
    - modern editor for Typst, built with Tauri and Svelte

- https://github.com/automataIA/wasm-typst-studio-rs /202510/rust/tauri
  - https://automataia.github.io/wasm-typst-studio-rs/  /典型双栏预览
  - A WASM-powered Typst Studio built with Rust and Leptos.
  - A modern Typst editor built entirely in Rust using WebAssembly. 
  - Available as both a web application and a native desktop app (via Tauri).
  - 100% Rust + WASM - No JavaScript required, fully compiled to WebAssembly
  - Multi-page Documents - Proper rendering of documents with multiple pages

- https://github.com/tyx-editor/TyX /144Star/MIT/202512/rust/ts/lexicaljs
  - https://tyx-editor.com/
  - https://app.tyx-editor.com/
  - A LyX-like experience rewritten for Typst and the modern era
  - 编辑器支持富文本编辑和markdown快捷键
  - 默认保存为 .tyx 后缀的文件, 里面内容是json
  - 👀 不支持读取 .typ 文件, 支持导出 .typ/.pdf
  - TyX uses `lexical` to build its wysiwyg editor. To convert typst documents into lexical format, TyX adopts a custom converter
  - TyX uses `MathLive` to make math formula editing easy by seeing the formula you're editing! This is currently LaTeX-based. We are working on a Typst-based editor
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
  - https://github.com/SoAp9035/cvforge
    - ATS-friendly CV/Resume builder using YAML and Typst

- https://github.com/KaiserY/mdbook-typst-pdf /MIT/202506/rust/inactive
  - A mdBook backend for generate pdf (through typst).
- https://github.com/LegNeato/mdbook-typst /rust
  - An mdBook backend to output Typst markup, pdf, png, or svg
- https://github.com/duskmoon314/mdbook-typst-math /rust
  - mdbook typst preprocessor

- https://github.com/leichaoL/typst-table-paste /MIT/202512/ts
  - VSCode extension that automatically converts RTF or CSV tables from the clipboard to Typst table syntax.

- https://github.com/TuringProblem/atoms /202512/typst
  - A typst ui library for computer science papers, research, and brainstorming
  - components: button, card(wip)

- https://github.com/oicana/oicana /polyform-nc/202512/rust
  - https://oicana.com/
  - Cross-Platform PDF templating based on Typst
  - Dynamic PDF Generation based on Typst
  - Define your templates in Typst, specify dynamic inputs, and generate high quality PDFs from any environment
  - Templates can use all of Typst's functionality, including its extensive package ecosystem.
  - Compile a PDF based on the template from either a
    - C# application using ASP.NET
    - Rust application with axum
    - Node.js application using NestJs
  - https://github.com/oicana/oicana-example-axum
    - Example project for using Oicana templates in Axum services
  - https://github.com/oicana/oicana-example-react
    - React app showcase for using Oicana templates in the browser

- https://github.com/slashformotion/typst-http-api /MIT/202504/python/inactive
  - Compile typst documents with a simple HTTP request.
  - a web server that allows users to compile typst markup remotely by a simple API call.
  - Currently, there is no way to compile a file that loads external resources (images or other .typ files for example).
  - https://github.com/a-musing-moose/django-typst-engine /BSD/202510/python
    - A Django template engine that uses Typst to render Portable Document Format (PDF) files.
- https://github.com/reportobello/server /AGPL/202505/python/inactive
  - https://reportobello.com/
  - Reportobello uses Typst, a blazing-fast Rust library, as it's templating engine.
  - Reportobello was built out of frusturation with existing PDF generators' lacking features, slow performance, poor SDK support, and so on.
  - JSON API

- https://github.com/typst-doc-cn/clreq /apache2/202512/ts/typst
  - [clreq-gap for typst](https://typst-doc-cn.github.io/clreq/)
  - Chinese Layout Gap Analysis for Typst. 分析 Typst 与中文排版的差距。
  - 这份文档描述了它在中文支持方面的差距，特别是排版和参考文献著录。本文会检查 typst 编译器是否支持所需功能，并介绍可能的临时解决方案
  - typst 目前连基础直排也难以实现
  - typst 的正文默认字体不含汉字。因此本地编译时，若不用#set text(font: …)配置字体就写中文，回落结果可能混合不同风格的字体（如 Figure 3），难以阅读，且无任何警告或提示。
  - 代码块内汉字回落的等宽字体不正常， 在正文之外，typst 对raw代码块预设了另一字体，同样不含汉字。该设置目前优先于你指定的正文字体，导致必须用#show raw: set text(font: …)再次指定中文字体
  - 对于引号（见 §4.2）等标点符号，中西文在Unicode中共用码位w3c/clreq#534，但要求不同形态，故必须分开设置字体。
  - 号数制是中文和日文排版中指定字号的系统。这种单位无法线性转换成点数：五号 = 10.5点，小四 = 12点，四号 = 14点……号数制在中国仍然普遍使用。普通人通常理解小四字多大，但可能对 12 pt 没有直观感受，除非查阅转换表。
  - 由于号数制当年在各地金属活字厂家并未统一（例如今日 CTeX、MS Word、WPS、Adobe 的四号是14点，但其它可能用13.75点），暂且算作 Advanced
  - 中文排版中，一行的行长应为文字尺寸的整数倍，不然容易触发 §5.2 中的若干对齐问题。因此通常“先确定版心，再余出空白”，而不是“先确定边距，再剩出版心”
  - 参考文献管理: GB/T 7714—2015 规定了以下三种标注方法。各方法采用不同的正文引注样式，末尾参考文献表的排布方式也不尽相同
  - 编译器暂不支持 CSL-M 标准，也不兼容 citeproc-js 的一些扩展。
  - https://github.com/HPDell/ctyp
    - 集成基础的 Typst 中文排版支持，提供快速的中文排版体验。
    - a Typst package providing basic Chinese typography support. 
- https://github.com/YDX-2147483647/typst-set-font /202512/ts/vue
  - https://ydx-2147483647.github.io/typst-set-font/
  - Setting Chinese font in Typst. 设置 Typst 中文字体。
  - 中西混排的文章可能用到许多字符。可目前鲜有字体覆盖并联合设计多个文种，典型情况如下。
  - 西文（Latin）字体：缺少中文字符，中文变成豆腐块；
  - 中文字体：虽基本覆盖 Latin 字符，但 Latin 部分的设计未必美观，甚至组成单词时难以阅读。
  - 然而，引号“”等中西共用标点不仅中西字体均提供，而且中西实际都会使用，并且中西习惯的形状、位置、大小还不相同。这导致选择字体比较复杂。
  - 中西共用标点的三种处理方法
  - 对于中文为主的文章，中西共用标点应采用中文字体渲染。
  - 对于西文为主的文章，中西共用标点应采用 Latin 字体渲染。
  - 对于代码等不含中文标点的特殊文段，也可采用另一特殊方法。

- https://github.com/forliage/Omni-Converter /202506/python/inactive
  - Web应用，旨在实现 Markdown (包括Jupyter Notebook), LaTeX, Typst, 和 HTML 之间的高保真、双向无缝转换。
  - 本项目完全独立实现所有核心转换逻辑，不依赖 Pandoc。
  - 本项目采用“星型”架构，以一个自定义的 中间表示 (Intermediate Representation, IR) 为核心。
  - 自研引擎: 所有解析器和渲染器均为从零开始构建，提供完全的控制力和透明度。
  - 解析器 (Parser): 将任何输入格式的文本（如 Markdown）解析成统一的 IR 结构。
  - 渲染器 (Renderer): 将 IR 结构渲染成任何目标格式的文本（如 LaTeX）。

- https://github.com/Lamkateh/richtext-typst /MIT/202509/python/inactive
  - Convert rich text JSON documents (from editors like ProseMirror, Quill, Slate) to Typst markup.
  - Supports multiple formats: ~~Quill, Slate~~, ProseMirror (extensible)
  - Custom parser support: Register your own parser for new formats
  - https://github.com/Lamkateh/outline-typst
    - Converts Outline's ProseMirror-based exports to Typst markup

- https://github.com/rkstgr/TypstBench /202505/python/inactive
  - LLM evaluation suite for Typst.
  - TypstBench is a dataset containing tasks and question around Typst, a modern typesetting language. It serves as a reference point for evaluating and enhancing LLMs' proficiency in Typst generation.
  - Preliminary Findings: claude-4 > gemini-2.5 > gpt-4.1
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

- https://github.com/lemueldls/mnemo /AGPL/202512/rust/ts/vue
  - https://mnemo.world/
  - A local-first, cross-platform note-taking app leveraging the Typst ecosystem.

- https://github.com/Snippyst/backend /202512/ts
  - https://github.com/Snippyst/frontend /AGPL/202512/ts
  - https://snippyst.com/
  - open-source snippet sharing platform for typst snippets
  - Live preview of Typst code rendering
  - Code syntax highlighting with Monaco editor
  - https://github.com/Snippyst/worker /ts
    - worker handles server-side rendering. 

- https://github.com/SuperMegaFort/TypstEdit /202512/swift
  - A lightweight, native macOS editor for Typst.
  - It combines a robust text editor with a live preview, leveraging the speed of the native Typst CLI.
  - Built with SwiftUI. 100% Native, fast, and lightweight.

- https://gitlab.com/gnoooo/typst_studio /ISC/202508/js/inactive
  - cross-platform desktop editor for Typst documents, built with Electron and designed for an intuitive writing experience.
  - Typst syntax support with CodeMirror 5 and custom files
  - Project Management: Create, open, and manage Typst projects

- https://codeberg.org/haydn/typesetter /GPL/202512/rust
  - lightweight desktop application for creating beautiful documents with Typst.

- https://gitlab.gnome.org/JanGernert/typewriter /GPL/202509/rust
  - Create documents with typst, the new markup-based typesetting system that is powerful and easy to learn.

- https://github.com/e-zz/MixTex-OCR-WebRebuild /AGPL/202509/python/vue
  - 文本+公式混合识别模型 MixTeX-Latex-OCR 的网站重构版，支持 Typst 转换
  - Convert LaTeX output to Typst format for modern document typesetting
  - https://github.com/OnHaiping/MixTex-OCR-WebRebuild /AGPL/202508/python/vue
    - 本项目由MixTeX-Latex-OCR修改而来，将原本的应用程序重构成了网站，功能基本上不变，模型用的原模型
    - 前端使用vue，后端使用Fastapi
  - https://github.com/RQLuo/MixTeX-Latex-OCR /1.6kStar/AGPL/202504/python/inactive
    - multimodal LaTeX recognition mini-program
    - It performs efficient CPU-based inference in a local offline environment. Whether it's LaTeX formulas, tables, or mixed text, MixTeX can easily recognize them all, supporting both Chinese and English processing.
    - LaTeX Formula Recognition: Accurately recognizes complex LaTeX mathematical formulas
    - Table Recognition: Efficiently processes and recognizes various tables, generating corresponding LaTeX table code.
    - Bilingual Support: Whether Chinese or English
    - Local Offline Inference: No internet connection required

## eg-templates

- https://github.com/henchoznoe/Typify /MIT/202512/typst
  - A modular, ready-to-use template for modern Typst documents.

- https://github.com/angelonazzaro/typxidian /MIT/202512/typst
  - A Typst template inspired by Obsidian good for note-taking an thesis writing
  - It is based, both on color palette and functionalities, on Obsidian and "Alice in a Differentiable Wonderland" by Simone Scardapane
  - A twin LaTeX version of TypXidian is available at: https://github.com/robertodr01/LaXidiaN

- https://github.com/Dawnfz-Lenfeng/easy-paper /MIT/202512/typst
  - 开箱即用的 Typst 中文写作模板
  - 一个基于 SimplePaper 改进的 Typst 模板，可用于日常报告/作业等。只需一个文件，无需外置库，使用 Windows 系统内置字体，即可开始创作。

- https://github.com/Mrered/GongWen-Tamplate-Lite /MIT/202512/lua
  - 一个公文格式的简单模板，并未完全适配国标，个人报告之用
  - 一个旨在快速生成公文格式 PDF 的简单模板，基于 Pandoc 和 Typst 

- https://github.com/vsheg/tufted /MIT/202512/typst
  - https://tufted.vsheg.com/
  - Responsive web layout with wide margins, elegant sidenotes, and restrained typography
  - A static website template built using Typst's experimental HTML export. Requires no external dependencies other than basic `make`.
  - [Tufte CSS](https://edwardtufte.github.io/tufte-css/) used for styling, loaded automatically from a CDN

- https://github.com/TimeTravelPenguin/mem /MIT/202510/typst
  - A Typst package for creating compact and tested cheat sheets/memory aids for exams.

- https://github.com/jiahaoxiang2000/typesetting /MIT/202510/typst
  - A professional document preparation and typesetting system based on Typst.
  - It's designed for academic papers, technical documentation, presentations, and other professional documents requiring precise formatting and layout.

- https://github.com/C4illin/typewind /MIT/202510/typst
  - tailwind colors in typst
# utils
- https://github.com/Myriad-Dreamin/tinymist /2.6kStar/apache2/202512/rust/ts
  - https://myriad-dreamin.github.io/tinymist
  - an integrated language service for Typst
  - [typlite ](https://crates.io/crates/typlite)
    - Converts a subset of typst to markdown/LaTeX/Word
    - Contents begin with `context` keyword will be rendered as svg output. The svg output will be embedded inline in the output file as base64 by default,

- https://github.com/destroyerOfOfficeChairs/dooc_embed_typst /202512/rust
  - A minimalist, self-contained wrapper for embedding Typst in Rust
  - self-contained wrapper for the Typst compiler
  - This library is designed for building Single Static Binary tools. It allows you to "bake" your Typst source code, fonts, images, and data directly into your Rust executable, creating a PDF generator that runs offline with zero external dependencies.
  - https://github.com/destroyerOfOfficeChairs/doocMath /python
    - a command-line tool designed to create customizable arithmetic worksheets in PDF format
- https://github.com/Relacibo/typst-as-lib /rust
  - Easily use typst from rust.
- https://github.com/xTeamStanly/typst-lib-wrapper /archived
  - Synchronous wrapper around 'typst' library
  - Typst version 0.13.1 is currently the last supported version as I lack resources to keep up with new releases.

- https://github.com/astrale-sharp/wasm-minimal-protocol /unlic/202511/rust
  - A minimal protocol to write typst plugins.
  - Note that plugins require typst version 0.8 or more.
  - A plugin can be written in Rust, C, Zig, Go, or any language than compiles to WebAssembly.
  - Rust plugins can use this crate to automatically implement the protocol with a macro
  - The runtime used by typst do not allow the plugin to import any function (beside the ones used by the protocol). In particular, if your plugin is compiled for WASI, it will not be able to be loaded by typst.
    - To get around that, you can use wasi-stub. It will detect all WASI-related imports, and replace them by stubs that do nothing.

- https://github.com/kxxt/codemirror-lang-typst /apache2/202508/ts/inactive
  - (Experimental) Typst language support for CodeMirror editor
  - WebAssembly support is required because this package implements the parser through wasm binding to the official typst-syntax crate.

- https://github.com/cetz-package/cetz /1.6kStar/LGPL/202512/typst/rust
  - https://cetz-package.github.io/
  - CeTZ (CeTZ, ein Typst Zeichenpaket) is a library for drawing with Typst with an API inspired by TikZ and Processing.
  - https://github.com/cetz-package/cetz-plot /LGPL/202509/typst
    - a library that adds plots and charts to CeTZ 
  - https://github.com/gbchu/ezchem
    - A typst lib draw atomic or ionic structures powered by ctez and single or double line bridge.

- https://github.com/lublak/typst-echarm-package /MIT/202512/js
  - A typst plugin to run echarts in typst with the use of CtxJS.

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

- https://github.com/kokic/kodama /GPL/202512/rust
  - https://kodama-community.github.io/
  - A Typst-friendly static Zettelkästen site generator
  - Typst support, which compiles via Typst installed on the user's device and embeds as SVG / HTML, thus all Typst features are available. 
  - Organize Markdown files in the manner of Jon Sterling's Forester.

- https://github.com/hanwenguo/weibian /GPL/202512/rust
  - https://hanwenguo.github.io/weibian/
  - 韦编: A Note System Powered by Typst
  - a software for taking scientific notes in the spirit of Forester, using Typst as the markup language.
  - It compiles Typst notes to HTML, then post-processes the HTML to resolve transclusion, internal links, and backmatter (backlinks/contexts/references/related notes).
  - Utilizes Typst HTML export: just use your templates/styles
  - Backmatter generation (backlinks, contexts, references, related notes)
  - 🆚 对比了同类产品 Forester, kodama, typesite
    - Forester uses its own markup language and LaTeX/KaTeX for math, and Weibian uses Typst for everything.
    - Kodama uses Markdown as the primary note format with good Typst support, while weibian uses Typst as the only note format.
    - Typsite aims to be a general purpose static site generator, and provides many features (e.g. schema, rewriting, etc.) for that. Weibian is more focused on being a tool for taking scientific notes, thus more opinionated and less flexible.

- https://github.com/tola-ssg/tola-ssg /MIT/202512/rust
  - static site generator for typst-based blog - keep your focus on the content
  - parallel compilation — Build pages and assets concurrently using rayon

- https://github.com/sihooleebd/noteworthy /MIT/202512/python/typst
  - https://noteworthy.benjaminlee.kr/
  - A powerful Typst framework for creating beautiful, themed educational documents.
  - an academic parser and framework for creating massive and complex documents in one go.
  - Interactive Editors: TUI-based editors for config, hierarchy, schemes, and snippets
  - Content Block Library: Pre-styled components for definitions, theorems, examples, proofs, and solutions
  - Plotting Engine: Advanced 2D/3D plotting, vector diagrams, and geometric constructions
  - Document Structure: Automated table of contents, chapter covers, and page headers
  - Configuration Layer: JSON-based settings in templates/config/
  - Build System: Incremental compilation with automatic PDF merging
  - https://github.com/sihooleebd/math-noteworthy

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
  - https://github.com/Mc-Zen/komet /rust
    - This package provides Rust implementations and a Typst wrapper for selected routines that are expensive to compute in pure Typst. In particular, this package supercharges the plotting package Lilaq by speeding up some essential computations.

- https://github.com/Jollywatt/typst-fletcher /MIT/202508/typst
  - A Typst package for drawing diagrams with arrows, built on top of CeTZ.
  - https://github.com/ivaquero/typst-consketcher
    - Draws Control Blocks using fletcher and CeTZ (still a toy)

- https://github.com/patrick-kidger/typst_pyimage /apache2/202512/python
  - Typst extension, adding support for generating figures using inline Python code
  - Usage is two steps. Write your content within the .typ file, and then run from the command line to build the content for Typst to actually import.

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
- https://github.com/Loewe1000/blockst
  - A Typst package for creating Scratch-style code blocks with pure curves and style.
- https://github.com/QuadnucYard/typst-hypraw /MIT/202512/typst
  - A lightweight package for creating headless code blocks optimized for HTML export. Inspired by zebraw.
  - Line numbers — expressive-code styled gutter with proper accessibility

- https://github.com/ludwig-austermann/typst-timetable /MIT/202509/typst
  - A typst template for timetables

- https://github.com/ntjess/typst-drafting /unlic/202505/typst/inactive
  - Margin notes cannot lay themselves out correctly until they know your page size and margins. 
  - By default, they occupy nearly the entirety of the left or right margin, but you can provide explicit left/right bounds if desired

- https://github.com/QuadnucYard/ourchat-typ /MIT/202512/typst
  - https://quadnucyard.github.io/ourchat-typ/
  - a Typst package for building chat UI mockups.

- https://github.com/Vanille-N/meander.typ /MIT/202512/typst/图文混排
  - provides a core function `reflow` to segment pages and wrap content around images
- https://github.com/jdpieck/oasis-align /MIT/202512/typst
  - A Typst package to cleanly place content side by side with equal heights using automatic content sizing.

- https://github.com/nleanba/typst-marginalia /unlic/202512/typst
  - Configurable margin-notes with smart positioning and matching wide blocks for Typst

- https://github.com/alexanderkoller/pergamon /MIT/202512/tex/typst
  - Typst bibliographies inspired by Biblatex
  - inspired by BibLaTeX, in that the way in which it typesets bibliographies can be easily customized through Typst code.
  - Like Typst's regular bibliography management model, Pergamon can be configured to use different styles for typesetting references and citations; unlike it, these styles are all defined through Typst code, rather than CSL.

- https://github.com/zyf722/typst-tabler-icons /MIT/202512/typst
  - A Typst library for Tabler Icons, a set of over 5800 free MIT-licensed high-quality SVG icons
  - Install the webfont file tabler-icons.ttf for Tabler Icons before using this library.
- https://github.com/cscnk52/simple-icons-typst /MIT/202512/rust/just
  - Typst Simple Icons Package
  - Since the compiled WASM module is relatively large (~5 MB), this package is only updated with new major releases of Simple Icons.
  - This package is under MIT LICENSE. Simple Icons is under CC0-1.0 and additional legal disclaimer

- https://github.com/hongjr03/typst-rexllent /MIT/202510/rust
  - https://hongjr03.github.io/excel-to-typst/
  - https://hongjr03.github.io/excel-to-typst/paste/
  - Convert xlsx/ods format tables to typst tables, powered by wasm.
  - You can also convert Spreet parsed tables to typst tables

- https://github.com/Acture/d2typ /202508/rust/inactive
  - Convert structured data (CSV/JSON/YAML/TOML/XLSX) into Typst syntax for embedding in documents.

- https://github.com/tilman151/pypst /MIT/202512/python
  - https://krokotsch.eu/pypst/
  - Declarative Typst in Python with Pandas data frame support.
  - Pypst helps you dynamically generate Typst code directly in Python.
  - Generating and styling Typst tables from Pandas data frames to be included in another Typst document
  - Pypst produces human-readable Typst code that you can modify and extend.
  - Pypst is not a Typst compiler. It doesn't check for syntax errors or compile Typst code into PDFs. Pypst interprets any string as a Typst literal

- https://github.com/typst-g7-32/typst-mdx-docs /MIT/202512/python
  - A tool for automated generation, conversion, and localization of Typst documentation
  - Multi-version Support: Automatically builds documentation for all Typst versions (starting from v0.11.0).
  - AI-Powered Translation: Context-aware translation pipeline that preserves terminology and style by using previous translations as a baseline.
  - MDX & Assets: Outputs production-ready MDX files and images that ready for web frameworks.

- https://github.com/lilBchii/tide /MPL/202512/rust
  - cross-platform IDE for Typst, written in Rust with Iced.

- https://github.com/IrregularPersona/TypTaps /202512/rust
  - A native Typst renderer made with iced-rs, and pdfium.

- https://github.com/An-314/scripst /MIT/202503/typst
  - A versatile scripting template for Typst typesetting
  - A customizable-named and colored block with a built-in counter that can be referenced anywhere in the document.

- https://github.com/PgBiel/elembic /MIT/202510/typst
  - Framework for custom elements and types in Typst. Supports Typst 0.11.0 or later.
  - Elembic lets you create custom elements, which are reusable and customizable document components, with support for typechecked fields, show and set rules 

- https://github.com/SillyFreak/typst-bullseye /MIT/202510/typst
  - Hit the target (HTML or paged/PDF) when styling your Typst document
  - This library helps you write target-dependent Typst code, particularly target-dependent content and show rules.
  -  allow package and document authors to easily write content and show rules that behave differently based on the target.

- https://gitlab.com/balping/typst-pdf-embedder /GPL/202409/python/inactive
  - provides a wrapper around the typst binary that enables embedding pdf files in documents.
  - Vector graphics and selectable and searchable text are preserved
  - Without this package, it is currently not possible to embed pdf files in documents using typst, you have to first convert the files to svg, thus compromising quality. It is possible that in the future embedding pdfs will be possible in plain typst
  - You will need Python 3.9+ and `PyMuPDF` 1.24+
  - typst-pdf.py calls typst compile. Now typst knows how large each pdf should be and generates placeholder rectangular frames
    - The placeholder frames are identified and replaced by the embedded pdfs using PyMuPDF
  - [Allow inserting PDFs as figures · Issue · typst/typst _202303](https://github.com/typst/typst/issues/145)
    - This would allow for workflows such as creating images in TikZ standalone mode and then inserting them into Typst documents. 
    - At the moment a workaround is to manually `pdf2svg a.pdf a.svg`.

- https://github.com/beibingyangliuying/python-typst /MIT/202510/python
  - a python package for generating executable typst codes. This package is written primarily in functional programming paradigm with some OOP contents. 
  - This package provides interfaces which are as close as possible to typst's native functions.

- https://github.com/typst-community/prequery /MIT/202510/typst
  - This package helps extracting metadata for preprocessing from a typst document, for example image URLs for download from the web. 
  - Typst compilations are sandboxed

- https://github.com/maxcrees/tbl.typ /MPL/202510/typst
  - https://maxre.es/tbl.typ/
  - This Typst library facilitates the creation of complex tables in Typst using a compact syntax based on the tbl preprocessor for the traditional UNIX TROFF typesetting system.

- https://github.com/NinZeige/Heyiwei /typst
  - 何呓谓 —— 用你最喜爱的无意义内容作为占位符来验证排版，由何意味驱动

- https://github.com/janosh/diagrams /MIT/202511
  - https://janosh.github.io/diagrams
  - Diagrams of concepts in physics/chemistry/ML
  - allows searching, sorting, opening in Overleaf and downloading figures (PDF/SVG/PNG) from this collection.
  - Have a TikZ/CeTZ diagram you'd like to share? Submit a PR with a .tex or .typ and a corresponding metadata .yml file in the assets/ directory

## format/markdown-typst

- https://github.com/RayZ3R0/typst-raster /MIT/202512/ts
  - Blazing-fast Typst → PNG/JPEG/WebP renderer for Node.js using native Rust compiler + Sharp
  - A fast, no-nonsense Node.js library for rendering Typst to PNG, JPEG, WebP, or PDF.
  - It uses the official Typst compiler through native Rust bindings (@myriaddreamin/typst-ts-node-compiler) and Sharp for rasterization
  - Comes with New Computer Modern fonts bundled, works out of the box on Lambda, Vercel, Docker, or anywhere else, no system font dependencies required.
  - SVG → raster pipeline with Sharp (sub-pixel accurate, any DPI)
  - SVG output support for vector graphics
  - Stream output for efficient HTTP responses

- https://github.com/SabrinaJewson/cmarker.typ /MIT/202512/rust
  - Transpile CommonMark Markdown to Typst, from within Typst

- https://github.com/nervosys/md2typ /apache2/202510/rust
  - Markdown → Typst (→ PDF) converter and CLI utility.
- https://github.com/forliage/Markst /202507/rust/inactive
  - Markdown与Typst的双向转换器
- https://github.com/rjnichols/mdtype /202511/ts
  - Convert Markdown documents with Mermaid diagrams to beautifully typeset Typst format.

- https://github.com/hongjr03/typst-oxdraw /MIT/202510/rust
  - A Typst plugin for visualizing Mermaid diagrams, built on top of oxdraw.
  - https://github.com/RohanAdwankar/oxdraw /MIT/202510/rust/ts
    - Diagram as Code Tool Written in Rust with Draggable Editing

- https://github.com/OrangeX4/typst-cheq /MIT/202509/typst/inactive
  - Write markdown-like checklist easily.
  - We can use the `cheq` package to achieve checklist syntax similar to GitHub Flavored Markdown and Minimal.
- https://github.com/OrangeX4/typst-tablem /MIT/202507/typst
  - Write markdown-like tables easily in Typst.
  - You can define a custom render function for advanced styling, such as a three-line table
  - Tablem supports both horizontal and vertical cell merging.

- https://github.com/Xecades/markdown-it-typst /MIT/202508/ts/inactive
  - Plugin to transform Typst code to SVG image for markdown-it markdown parser.
  - https://github.com/Lowmst/markdown-it-typst-math
    - adds Typst rendering for math equations.

- https://github.com/Quorafind/typst-toolbox /apache2/202512/ts/obsidian
  - Convert Markdown to Typst and then to DOCX/PDF. Supports real-time preview and editing.
  - https://github.com/k0src/Typst-for-Obsidian 
    - A Typst editor and renderer in Obsidian
  - https://github.com/fogsong233/Typsidian
    - A typst tool for obsidian

- https://github.com/sghng/typ2docx /MIT/202512/python
  - https://typ2docx.sgh.ng/
  - a command line tool that converts a Typst project to Microsoft Word .docx format, with tables, cross-references, most of the styles, and most importantly the math markups preserved
  - It combines the mature, comprehensive document conversion of standard PDF-to-Word tools with `Pandoc`'s high-quality mathematical formula export.

- https://github.com/Magi3r/md-typ-pdf /202511/rust
  - A simple command-line tool written in Rust that converts Markdown (.md) files into clean PDF documents using using typst and the cmarker package.
  - Converts Markdown files (.md) into PDFs (.pdf)
  - Math rendering with `mitex`

- https://github.com/aualbert/typst2latex /MIT/202512/rust
  - Convert Typst documents written using the unequivocal-ams template to human-friendly Latex.
  - This uses a custom Typst parser to produce a parse tree in which useful environements (e.g. theorem) are preserved. A backend (currently pandoc only) is then used to convert the leafs of the parse tree (typically math formulas). 

- https://github.com/nibsbin/quillmark /apache2/202512/rust
  - https://quillmark.readthedocs.io/
  - A template-first Markdown rendering system that converts Markdown with YAML frontmatter into PDF, SVG, and other output formats
  - Quill templates control structure and styling, Markdown provides content
  - YAML frontmatter support: Extended YAML metadata with inline sections
  - Multiple backends:
    - PDF and SVG output via Typst backend
    - PDF form filling via AcroForm backend
  - Dynamic asset loading: Fonts, images, and packages resolved at runtime
  - [TongueToQuill - Military Document Editor | Write Markdown, Export Professional Docs](https://www.tonguetoquill.com/)
    - 需要用这里的模版

- https://github.com/scipenai/tylax /71Star/apache2/202601/rust
  - https://convert.silkyai.cn/
  - bi-directional converter between Typst and LaTeX. 
  - Available as both a CLI tool and a Web interface.
  - A tool written in Rust that converts mathematical formulas and full documents between LaTeX and Typst formats.
  - [[开源] 给佬友们推个新轮子 Tylax：Rust 写的 LaTeX ↔ Typst 双向转换神器，全 AST 解析  _202601](https://linux.do/t/topic/1418819)
    - 跟市面上那些靠正则（Regex）硬替换的脚本不一样，Tylax 走了正道，基于 mitex 和 typst-syntax 搞了完整的 AST（抽象语法树）解析。这意味着处理嵌套结构、各种环境定义还有复杂的数学公式时，稳得一批，不会因为少个括号就原地爆炸。
    - 表格不乱：智能处理 \multicolumn 和 \multirow
    - 持把 LaTeX 的 TikZ 代码直接转成 CeTZ
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

- https://github.com/VMASPAD/text-latex /202512/ts
  - https://text-latex.vercel.app/
  - Write markdown, export latex
  - A modern rich text editor built with Next.js, Lexical, and KaTeX that supports LaTeX equation rendering and export.

- https://github.com/susam/texme /js
  - a lightweight JavaScript utility to create self-rendering Markdown + LaTeX documents.

- https://github.com/parpalak/upmath.me
  - Markdown and LaTeX online editor - create text for web with equations and diagrams
# math
- https://github.com/mitex-rs/mitex /apache2/202512/rust
  - https://mitex-rs.github.io/mitex/
  - https://mitex-rs.github.io/mitex/tools/underleaf.html
  - LaTeX support for Typst, powered by Rust and WASM

- https://github.com/dbccccccc/TypstPad /MIT/202512/ts/公式
  - https://typstpad.com/
  - A simple and elegant online Typst formula editor with real-time preview
  - SVG, PNG, JPG导出下载，支持将PNG复制到剪切板
  - SVG, HTML, typ代码文件下载&复制
  - 现在暂时还没有对移动端进行优化，后续版本可能会添加
  - Monaco Editor, Shiki, typst.ts
  - Generate shareable URLs with encoded formulas
  - [TypstPad: 一个在线Typst公式编辑器 ](https://linux.do/t/topic/1364899)

- https://github.com/qwinsi/tex2typst-webapp /GPL/202512/js/svelte
  - https://qwinsi.github.io/tex2typst-webapp/
  - Translate between LaTeX / TeX math markup and Typst in your browser.
  - https://github.com/qwinsi/tex2typst /apache2/202512/ts
    - conversion between TeX/LaTeX and Typst math code.
- https://github.com/continuous-foundation/tex-to-typst
  - Translate LaTeX or TeX math markup to typst

- https://github.com/ParaN3xus/typress /MIT/202503/python/js
  - Typst Mathematical Expression OCR based on TrOCR.

- https://github.com/paran3xus/tex2typ /MIT/202501/js/vue/archived
  - https://paran3xus.github.io/tex2typ/
  - A tool to rebuild Typst mathematical formulas from KaTeX syntax tree.
  - Convert LaTeX mathematical formulas to Typst mathematical formulas.
  - Differences from MiTeX
    - The generated formulas do not rely on any special Typst environments or packages and can be compiled directly with the standard Typst.
    - We didn't provide any Typst package.

- https://github.com//wypst /MIT/202406/rust/js/inactive
  - https://0xbolt.github.io/wypst/
  - Typst math typesetting for the web. Renders into the HTML element/string
  - There's still no conclusive roadmap for native HTML export in Typst
  - 测试用例: sum_(n >= 1) 1/n^2 = pi^2/6

- https://github.com/detypstify/typic /202408/rust/inactive
  - http://jachymp.me/typic/
  - Using OCR to convert images of formulas into Typst code
  - Using OCR to generate Typst code based on images of math formulas as a fully client-side webapp.

- https://github.com/xyy-cas/tex2typst-UI /GPL/202502/rust
  - https://xyy-cas.github.io/tex2typst-UI/
  - Convert TeX math to Typst with custom macros support.

- https://github.com/KaTeX/KaTeX /js/NoDeps
  - https://katex.org/
  - Fast math typesetting for the web.
  - KaTeX renders its math synchronously and doesn't need to reflow the page. See how it compares to a competitor in this speed test.
  - KaTeX's **layout** is based on **Donald Knuth's TeX**, the gold standard for math typesetting.
  - support ssr
  - KaTeX supports much (but not all) of LaTeX and many LaTeX packages.

- https://github.com/cortex-js/compute-engine /ts
  - https://cortexjs.io/
  - An engine for symbolic manipulation and numeric evaluation of math formulas expressed with MathJSON
  - MathJSON is a lightweight mathematical notation interchange format based on JSON.
  - The Cortex Compute Engine can parse LaTeX to MathJSON, serialize MathJSON to LaTeX, format, simplify and evaluate MathJSON expressions.

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
# typesetting-examples
- https://github.com/pagedjs/pagedjs /1.2kStar/MIT/202511/js
  - https://gitlab.coko.foundation/pagedjs/pagedjs
  - https://pagedjs.org/
  - https://controverses.org/mode-demploi/
  - Display paginated content in the browser and generate print books using web technology
  - It contains a set of handlers for CSS transformations and fragmented layout which polyfill the Paged Media and Generated Content CSS modules, along with hooks to create new handlers for custom properties.

- https://github.com/vivliostyle/vivliostyle.js /709Star/AGPL/202512/ts
  - https://vivliostyle.org/
  - https://vivliostyle.github.io/vivliostyle_doc/samples/gutenberg/Alice.html
    - 网页版不分页，但使用浏览器的打印预览时显示分页，每章的分页都正确
  - The power of CSS typesetting, right at your fingertips
  - offers HTML+CSS typesetting and rich paged viewing with EPUB/Web publications support

- https://github.com/mkpoli/hundouk /MIT/202512/typst
  - hundouk (訓讀) is a Typst package for rendering Kanbun Kundoku (漢文訓読) texts, by which Classical Chinese texts are rendered with annotations to be translated mechanically into Classical Japanese, which is still used in modern Japanese education.
  - https://github.com/untunt/kanbunHTML /AGPL/202206/js/inactive
    - https://phesoca.com/kanbun-html/
    - a kanbun kundoku (漢文訓読) HTML display solution (probably the best) supporting both fixed inter-character spacing setting (アキ組) and solid setting (ベタ組) setting. It converts annotated kanbun text to HTML and displays it.
    - ✨ 竖排文字， 每个文字可在右下角或右侧显示翻译
# more
