---
title: toc-lib-editor-text-typesetting
tags: [editor, layout, typesetting]
created: 2024-11-16T08:23:15.537Z
modified: 2024-11-16T08:23:40.617Z
---

# toc-lib-editor-text-typesetting

# guide

- 经典排版系统
  - html/css: yogo, flex
  - latex
  - pdf
# popular
- https://github.com/samwillis/premirror /MIT/202603/ts
  - https://samwillis.uk/premirror/
  - Premirror is a library for building Word-class page-layout editors on the web. 
  - It layers deterministic pagination and composition on top of ProseMirror, giving you paper-style page breaks, widow/orphan control, and fragment-level text positioning — all while keeping ProseMirror as the single source of truth for document content and editing.
  - ProseMirror owns the document model and all editing operations. Premirror's composer takes a measured snapshot of the document and produces a deterministic layout: pages, frames, line boxes, and placed runs. A React rendering layer then projects those fragments into absolute positions inside page-chrome viewports, producing a word-processor-style paged view with a single contenteditable surface.
  - Text measurement is handled by @chenglou/pretext, which provides segment-aware width calculation and line fitting.
  - https://x.com/samwillis/status/2038209756268048771
    - Document layout with page breaks

- https://github.com/chenglou/pretext /5.5kStar/MIT/202603/ts
  - https://pretextbreaker.com/
  - https://chenglou.me/pretext/
  - https://somnai-dreams.github.io/pretext-demos/
  - Pure JavaScript/TypeScript library for multiline text measurement & layout. 
  - Fast, accurate & supports all the languages you didn't even know about. 
  - Allows rendering to DOM, Canvas, SVG and soon, server-side.
  - Pretext side-steps the need for DOM measurements (e.g. getBoundingClientRect, offsetHeight), which trigger layout reflow, one of the most expensive operations in the browser. It implements its own text measurement logic, using the browsers' own font engine as ground truth (very AI-friendly iteration method).
  - [Pretext — Under the Hood _202603](https://tools.simonwillison.net/pretext-explainer)
    - An interactive exploration of how pure-JS text measurement works using a simplified version of Pretext — from raw string to pixel-accurate line heights, without ever touching the DOM.

- https://github.com/BaselAshraf81/layout-sans /MIT/202603/ts
  - Pure TypeScript 2D layout engine powered by Pretext. 
  - CSS Flex/Grid layout without the browser. No DOM. No WASM bloat.
  - Flex, Grid, Magazine multi-column, and Absolute layouts — with zero DOM and zero WASM bloat. 
  - Pretext measures text. LayoutSans positions everything. 
    - LayoutSans is designed as the natural next layer after Pretext.
  - Give it a tree of boxes with flex/grid rules; get back exact pixel positions for every box. 
  - Works everywhere: Browser, Node, Bun, Deno, Workers. The natural next primitive after Pretext.
  - yoga flexbox engine that inspired LayoutSans's API design. Yoga's WASM approach informed what we decided not to do.
  - https://x.com/Basel_Ashraf812/status/2038466644842791100

- https://github.com/razroo/textura /MIT/202603/ts
  - https://razroo.github.io/textura
  - DOM-free layout engine for the web
  - Combines Yoga (flexbox) with Pretext (text measurement) to compute complete UI geometry — positions, sizes, and text line breaks — without ever touching the DOM.
    - Yoga solves box layout (flexbox) in pure JS/WASM, but punts on text — it requires you to supply a MeasureFunction callback externally. 
    - Pretext solves text measurement with canvas measureText, but doesn't do box layout. 
    - Textura joins them: declare a tree of flex containers and text nodes, get back exact pixel geometry for everything.
  - Worker-thread UI layout — compute layout off the main thread, send only coordinates for painting
  - Zero-estimation virtualization — know exact heights for 100K items before mounting a single DOM node
  - Canvas/WebGL/SVG rendering — full layout engine for non-DOM renderers
  - Server-side layout — generate pixel positions server-side (once Pretext gets server canvas)
  - https://x.com/charliegreenman/status/2038382414037123438
    - Could it support orphan text?  Alas text-wrap: pretty/balance;

- https://github.com/alerque/polytype /202408
  - https://polytype.dev/
  - A Rosetta stone for typesetting engines.
  - This project's goal is to provide a chrestomathy for typesetting similar to what Rosetta Code does for programming languages. 
  - 🆚️ SILE, Typst, LaTeX, paged.js, WeasyPrint, Speedata, groff, Patoline, SATySFi
  - The samples here are designed to compare and/or contrast the approaches taken to various typesetting situations by different typesetting engines.
  - The emphasis is less on document markup languages, programming languages, or actual content and more on the way layout and orthographic features are achieved. 
  - 📝🆚️ [On Typesetting Engines: A Programmer's Perspective _202410](https://blog.ppresume.com/posts/on-typesetting-engines)

- https://github.com/typst/typst /50kStar/apache2/202512/rust
  - https://typst.app/
  - Typst is a new markup-based typesetting system that is designed to be as powerful as LaTeX while being much easier to learn and use.
  - This repository contains the Typst compiler and its CLI 
  - Built-in markup for the most common formatting tasks
  - Flexible functions for everything else
  - A tightly integrated scripting system
  - Math typesetting, bibliography management, and more
  - Fast compile times thanks to incremental compilation

- https://github.com/yamlresume/yamlresume /MIT/202505/ts
  - https://yamlresume.dev/
  - YAMLResume allows you to manage and version control your resumes using YAML and generate professional looking PDFs with beautiful typesetting in a breeze.
  - This project was started as the core typesetting engine for PPResume, a LaTeX based, pixel perfect resume builder. 
  - YAMLResume adopts `LaTeX` as the default typesetting engine, which is the state of the art typesetting system in the academic and technical publishing industry.
    - In the future we may support other typesetting engines like Typst, HTML/CSS, etc.
  - the resume content is drafted in plain text as YAML
  - the YAML plain text is then rendered into a PDF with a pluggable typesetting engine
  - the layout can be adjusted with options like font sizes, page margins, etc.
  - https://x.com/PPResumeX/status/1920294577497387493
    - This project is inspired by JSON Resume with many enhancements like rich text, layout and i18n, etc.
  - [Introducing YAMLResume _202505](https://yamlresume.dev/blog/introducing-yamlresume)
  - YAMLResume works like a mini compiler, i.e, it takes an input, parses it to an AST and then generates an output.
  - The core design principle of YAMLResume is separation of concerns. One of the most famous examples that follows this principle is HTML & CSS
  - YAML is better than JSON because it is more human-readable and human-writable
    - markdown is a general-purpose markup language for creating formatted text, while resumes only use a very limited set of markdown features.
    - markdown is far too flexible, often giving users more freedom than they need. It would be pretty hard to reliably parse a generic markdown document as a resume.
    - Third, features like templates switching, precise layout control (like \hfill and \hspace in LaTeX) is very hard to implement in markdown.
  - LaTeX is a very mature and stable typesetting engine that can produce extremely high-quality PDFs. 
    - YAMLResume is designed to support multi languages with the best possible typesetting quality, however, `typst` CJK support is still unstable and lacking.
    - Later on I may add a new renderer backend to support typst.
  - Although we have decided not to use markdown as the resume input format, we do support a limited set of markdown rich text syntax for the `summary` field in various sections.
# typesetting-layout
- https://github.com/chearon/dropflow /MIT/202412/ts
  - https://chearon.github.io/dropflow/
  - Dropflow is a CSS layout engine created to explore the reaches of the foundational CSS standards (that is: inlines, blocks, floats, positioning and eventually tables, **but not flexbox or grid** ).
  - You can use it to generate PDFs or images on the backend with Node and node-canvas or render rich, wrapped text to a canvas in the browser.
  - 🧐 最后渲染的元素是canvas
  - Bidirectional and RTL text
  - Hyperscript (h()) API with styles as objects in addition to accepting HTML and CSS
  - Any OpenType/TrueType buffer can (and must) be registered
  - Desirable line breaking (e.g. carries starting padding to the next line)
  - Inherited and cascaded styles are never calculated twice
  - Dropflow works off of a DOM with inherited and calculated styles, the same way that browsers do. You create the DOM with the familiar h() function, and specify styles as plain objects.
  - [Show HN: Dropflow, a CSS layout engine for node or <canvas> | Hacker News _202403](https://news.ycombinator.com/item?id=39778570)
    - For the last 5 years I've been working on a layout engine that targets CSS2 and some more modern properties.
    - We currently use it in CellEngine for our new canvas-based spreadsheet library to layout text in hundreds of thousands of cells, and will be using it soon to render PDFs with thousands of pages in a few seconds.

- https://github.com/DioxusLabs/taffy /2.2kStar/MIT/202412/rust
  - https://docs.rs/taffy
  - a flexible, high-performance, cross-platform UI layout library written in Rust.
  - It currently implements the CSS Block, Flexbox and CSS Grid layout algorithms.
  - designed to be used as a dependency for other UI and GUI libraries. Right now, it powers: zed-GPUI, Bevy, Dioxus, Lapce
  - This library was forked from the `stretch` crate
  - 🆚 性能测试表明多数场景比yoga更快

- https://github.com/iamgio/quarkdown /9.1kStar/GPLv3/202509/kotlin
  - https://quarkdown.com/
  - a modern Markdown-based typesetting system, designed around the key concept of versatility, by seamlessly compiling a project into a print-ready book or an interactive presentation. 
  - All through an incredibly powerful Turing-complete extension of Markdown
  - Born as an extension of CommonMark and GFM, the Quarkdown Flavor brings functions to Markdown, along with many other syntax extensions.
  - standard library offers layout builders, I/O, math, conditional statements and loops.
  - [Quarkdown, a modern, Turing-complete, Markdown-based typesetting system, now finally supports exporting to PDF : r/programming _202508](https://www.reddit.com/r/programming/comments/1joyi4l/quarkdown_a_modern_turingcomplete_markdownbased/)

- https://github.com/litehtml/litehtml /BSD/202412/cpp
  - http://www.litehtml.com/
  - lightweight HTML rendering engine with CSS2/CSS3 support. 
  - Note that litehtml itself does not draw any text, pictures or other graphics and that litehtml does not depend on any image/draw/font library
  - litehtml just parses HTML/CSS and places the HTML elements into the correct positions (renders HTML). To draw the HTML elements you have to implement the simple callback interface document_container. 
  - litehtml uses the gumbo-parser to parse HTML. Gumbo is an implementation of the HTML5 parsing algorithm implemented as a pure C99 library with no outside dependencies

- https://github.com/youtube/cobalt /BSD/202501/cpp
  - https://cobalt.dev/
  - https://developers.google.com/youtube/cobalt
  - Cobalt is a lightweight HTML5/CSS/JS application container that is designed to provide a rich application development environment with minimal resource consumption (deployment size, RAM, CPU, GPU). 
  - 为在极少资源条件下播放视频而设计，支持audio/video标签，不支持img/p，对文本排版支持有限
  - Cobalt is a single-process application and does not rely on the ability to spawn multiple processes.
  - Cobalt is optimized to run on single-core CPUs, resulting in better input latency since the renderer and resource loader do not compete with layout operations.
  - Cobalt produces consistent 60FPS animations by only supporting animation of properties that don't affect layout, like transform, and always running animations on a separate thread.
  - On platforms that support GLES2, Cobalt avoids CPU painting by performing almost all rendering operations on the GPU.
# latex
- https://github.com/EvolvingLMMs-Lab/lmms-lab-writer /MIT/202602/rust/ts/Tauri
  - https://writer.lmms-lab.com/
  - Agentic LaTeX Writer - Local-first editor for AI-assisted academic writing
  - automatically detects and installs a lightweight LaTeX distribution. If a package is missing, it’s installed on the fly during compilation. 
  - Supports TinyTeX, MiKTeX, MacTeX, and TeX Live—with streamlined, one-click management.
  - English, Chinese, Japanese, Korean, Arabic, or any other language. XeLaTeX and LuaLaTeX are supported out of the box with full Unicode and system font compatibility
  - It also pairs perfectly with Claude Code, Cursor, Codex CLI, Aider, and other tools.
  - Cross-Platform: Built with Tauri 
  - 🆚 Overleaf vs. LMMs-Lab Writer
  - https://x.com/Brian_Bo_Li/status/2020853665196617796
    - 天下苦 Overleaf 久矣，赶 paper 在 chatgpt 和编辑器之间反复横跳真的会疯。prism 出来后又感觉太繁重且不支持中文
    - 一个内置 AI Agent 的终极 LaTeX 本地编辑器 LMMs-Lab Writer。
    - 一键环境配置，自动下载管理 LaTeX，开箱即用。
    - 原生 Git 集成：侧边栏直接可视化管理版本控制。
    - 我想要的是，可以在本地跟着代码一起写，做事实核查，可以在vscode，cursor里面写的，这样就能用deep research或者任何github整的skills，还可以随时同步云端的overleaf，how can we achieve this
# more
