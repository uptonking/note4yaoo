---
title: toc-office-pdf
tags: [doc, pdf, toc]
created: 2020-09-26T17:53:26.962Z
modified: 2021-01-04T17:26:43.784Z
---

# toc-office-pdf

# guide

- tips
  - 支持导出pdf是大多数产品的基本功能，如drawio/jsreport/thorium-reader/notesnook
  - pdf-editor 可参考 ppt-editor 的实现，都包含自由文本、标注
    - 💡 可参考 overleaf, 支持典型的latex文本编辑、富文本编辑
  - pdf标注可参考 office-drawing, 还可参考: okular, foxit, canva, xournal, 各类电子书阅读器

- https://printcss.live/
  - 渲染pdf的多种js示例
# popular
- pdf.js /52.4kStar/apache2/202512/js
  - https://github.com/mozilla/pdf.js
  - https://mozilla.github.io/pdf.js/
  - PDF.js is a Portable Document Format (PDF) viewer that is built with HTML5.
  - Our goal is to create a general-purpose, web standards-based platform for parsing and rendering PDFs.
- https://github.com/Osiris-Team/pdf.js-utils /MIT/202408/js
  - A collection of utility functions for pdf.js to make the lives of developers easier.

- jsPDF /30.9kStar/MIT/202511/js
  - https://github.com/parallax/jsPDF
  - https://parall.ax/products/jspdf
  - A library to generate PDFs in JavaScript.
  - 支持web和node
  - https://github.com/AaronClaes/jspdf-editor
    - https://jspdf-editor.vercel.app/
    - *WIP* Design pdfs and generate code for jspdf
  - https://github.com/simonbengtsson/jsPDF-AutoTable
    - adds the ability to generate PDF tables either by parsing HTML tables or by using Javascript data directly. 

- pdfkit /10.5kStar/MIT/202512/js
  - https://github.com/foliojs/pdfkit
  - http://pdfkit.org/
  - http://pdfkit.org/demo/browser.html
  - A JavaScript PDF generation library for Node and the browser.

- https://github.com/unjs/unpdf /950Star/MIT/202512/ts
  - Utilities to work with PDFs in Node.js, browser and workers
  - unpdf ships with a serverless build/redistribution of Mozilla's PDF.js for serverless environments. 
  - This library is also intended as a modern alternative to the unmaintained but still popular `pdf-parse`.

- https://github.com/diegomura/react-pdf /16.2kStar/MIT/202509/ts
  - React renderer for creating PDF files on the browser and server
  - This package is used to create PDFs using React. 
    - If you wish to display existing PDFs, you may be looking for https://github.com/wojtekmaj/react-pdf
  - https://github.com/ag-media/react-pdf-table /MIT/202501/ts
    - a declarative table generator for @react-pdf/renderer
  - https://github.com/enescang/react-pdf-table /202210/js/inactive
    - Simple table generator for @react-pdf/renderer

- https://github.com/wojtekmaj/react-pdf /10.7kStar/MIT/202512/ts
  - https://projects.wojtekmaj.pl/react-pdf
  - Display PDFs in your React app as easily as if they were images.
  - For React-PDF to work,  `PDF.js` worker needs to be provided.
  - https://x.com/xiaohanyu1988/status/1905077853785567258 🆚️

- https://github.com/Alpovka/EasyPDF-React /24Star/MIT/202501/ts/inactive
  - https://easypdf.vercel.app/
  - open source React library for generating beautiful PDFs from React components
  - [I built an open-source package 6 months ago to easily turn React components into PDFs _202510](https://www.reddit.com/r/reactjs/comments/1nun17d/i_built_an_opensource_package_6_months_ago_to/)

- https://github.com/pdfslick/pdfslick /771Star/MIT/202511/ts
  - https://pdfslick.dev/
  - PDFSlick is a library that enables viewing of and interaction with PDF documents in React, SolidJS, Svelte and JavaScript apps. 
  - It's build on top of Mozilla's `PDF.js`, and utilises `Zustand` to provide a reactive store for the loaded documents.
  - @pdfslick/core package wraps PDF.js's functionality and links it to the store.
    - you can learn more about using PDFSlick's @pdfslick/core package with Vanilla JS apps and with libraries other than React and SolidJS

- https://github.com/jkgenser/react-pdf-headless /50Star/MIT/202509/ts
  - a React component for efficiently rendering and navigating PDF documents.
  - It leverages virtualization to handle large documents smoothly and provides APIs for client-side interactions such as jumping to specific pages or highlighted areas.
  - [Don't use this package, and a good mostly FREE alternative · Issue · react-pdf-viewer/react-pdf-viewer](https://github.com/react-pdf-viewer/react-pdf-viewer/issues/1858)
    - I re-wrote it from scratch on top of wojtekmaj/react-pdf and tanstack.com/virtual
    - My use case involves lazily rendering large PDFs, scrubbing to particular pages or offsets within a page, showing bounding boxes or highlights overlaid on the pages and more!
  - https://github.com/react-pdf-viewer/react-pdf-viewer /paid/202408/ts/deprecated
    - https://react-pdf-viewer.dev/
    - React component to view a PDF document
    - https://github.com/react-pdf-viewer/starter /js/electron
    - [WARNING: Project no longer maintained - Do not use in virtual solutions _202406](https://github.com/react-pdf-viewer/react-pdf-viewer/issues/1768)

- https://github.com/Hopding/pdf-lib /8.1kStar/MIT/202111/ts/inactive
  - Create and modify PDF documents in any JavaScript environment.
  - Designed to work in any modern JavaScript runtime. Tested in Node, Browser, Deno, and React Native environments.
  - [Is this thing still on?](https://github.com/Hopding/pdf-lib/issues/1423)
  - 🍴 forks
  - https://github.com/cantoo-scribe/pdf-lib
    - This fork adds the support for svg to the pdf-lib project.

- https://github.com/anaralabs/lector /355Star/MIT/202510/ts
  - https://lector-weld.vercel.app/
  - A composable, headless PDF viewer toolkit for React applications, powered by PDF.js
  - Page thumbnails and outline navigation
  - Text selection and search functionality
  - Responsive and mobile-friendly
  - Form filling support
  - Internal and external link handling

- https://github.com/OnedocLabs/pdfreader /MIT/202411/ts
  - https://pdfreader.fileforge.com/
  - Easy Radix-Style PDF Viewer for React.

- https://github.com/pdfme/pdfme /3.9kStar/MIT/202512/ts
  - https://pdfme.com/
  - https://playground.pdfme.com/
  - Open-source PDF generation library built with TypeScript and React. 
  - Features a WYSIWYG template designer, PDF viewer, and powerful generation capabilities. 
  - Fast PDF Generator: Works on Node and in the browser. Use templates to generate PDFs
  - Easy PDF Template Design: easily create templates using the designer.
  - Templates are JSON data that is easy to understand
  - pdfme will always remain open source. The cloud service is an optional offering for those who prefer a managed solution.

- https://github.com/agentcooper/react-pdf-highlighter /1.2kStar/MIT/202409/ts
  - https://agentcooper.github.io/react-pdf-highlighter
  - a React library that provides annotation experience for PDF documents on web.
  - built on top of PDF.js by Mozilla. 
  - Text and rectangular highlights are supported. 
  - Highlight data format is independent of the viewport, making it suitable for saving on the server.
  - `react-pdf` and react-pdfjs only provide React wrappers for PDF.js and do not have built-in annotation functionality.
  - `pdfjs-annotate` does not provide text highlights out of the box.
  - https://github.com/velvetfs/v-pdf-highlighter

- https://github.com/bfritscher/pdf-stamp /MIT/202405/js/inactive
  - https://bfritscher.github.io/pdf-stamp/
  - PDF Stamp is a web application that allows users to add stamps or signatures to PDF files directly from their browsers. 
  - pdfjs-dist for rendering PDF files to image.
  - signature_pad for signature creation.
  - fabric.js for handling canvas and stamps.
  - pdf-lib for PDF manipulation.
  - Stamps are stored in the browser's localStorage under the key pdf-stamps-srcStamps. This allows you to reuse them even after refreshing the page.

- https://github.com/aexol-studio/react-pdf-editor /MIT/202205/ts/inactive
  - Pdf editor react component
  - 依赖@react-pdf/rendere
  - [Refactor 2022](https://github.com/aexol-studio/react-pdf-editor/issues/69)
- https://github.com/snamoah/react-pdf-editor /202009/js/inactive
  - PDF Editor built with react
  - This project is a react port of the svelte version here so most of the pdf generation and editing logic was lifted from there.

- https://github.com/neslxzhen/pdf-editor /202201/ts/inactive
  - No Server, No Install PDF Editor with React
  - https://github.com/oren-l/PdfEditor /js
  - https://github.com/pgarciacamou/pdf-editor /js

- https://github.com/jeetiss/react-pdf-repl
  - https://react-pdf-repl.vercel.app/
  - REPL for `@react-pdf/renderer` with interactive debugger

- https://github.com/bpampuch/pdfmake /11kStar/MIT/202311/js
  - http://pdfmake.org/
  - https://pdfmake.github.io/docs/
  - PDF document generation library for server-side and client-side in pure JavaScript.
  - 依赖pdfkit、xmldoc
  - images and vector graphics
  - tables and columns
  - page headers and footers

- https://gitlab.coko.foundation/pagedjs/pagedjs
  - Paged.js is a free and open-source library that paginates any HTML content to produce beautiful print-ready PDF. 
  - The library fragments the content, reads your CSS print declarations and presents a paginated preview in your browser that you can save as PDF.

- https://github.com/PDFMathTranslate-next/PDFMathTranslate-next /2kStar/AGPLv3/202512/python
  - https://pdf2zh-next.com/zh/index.html
  - PDF 科学论文翻译与双语对照。基于 BabelDOC
  - 🐛 翻译图片pdf的异常 'Translation error: Babeldoc translation error: The document contains no paragraphs 
  - [关于扫描版PDF & 图片的说明 _202508](https://github.com/PDFMathTranslate-next/PDFMathTranslate-next/issues/166)
    - 目前 BabelDOC 技术路线 暂无计划支持扫描版 PDF
    - 位图：方案仍在探索中，大概率会依赖闭源服务，优先级较低。
    - 矢量图：最新版本的 BabelDOC 已经可以识别并翻译图中的文字。
    - 不同 OCR 服务的输出格式差异较大，需要大量适配工作。
  - [接入paddleocr vl呀 _202511](https://github.com/PDFMathTranslate-next/PDFMathTranslate-next/issues/285)
    - 要吃饭的，基于OCR翻译闭源搞了
  - https://github.com/PDFMathTranslate/PDFMathTranslate-next /AGPLv3
    - pdf2zh 2.0 does not currently provide an online demo
- https://github.com/PDFMathTranslate/PDFMathTranslate /29.8kStar/AGPLv3/202511/python 
  - https://pdf2zh.com/
  - 基于 AI 完整保留排版的 PDF 文档全文双语翻译，支持 Google/DeepL/Ollama/OpenAI 等服务，提供 CLI/GUI/MCP/Docker/Zotero
  - Preserve formulas, charts, table of contents, and annotations
  - Support multiple languages, and diverse translation services.
  - ✨ 可参考翻译后pdf布局不变的实现方式, 特别是表格中英文变中文但布局不变
  - 支持双栏布局显示原文和翻译，体验非常好
  - 🐛 [supports ocr on scanned document ](https://github.com/PDFMathTranslate/PDFMathTranslate/issues/19)
    - 图片型的 PDF 文档暂时还没办法翻译，目前主要还是在优化电子书和论文的翻译效果
    - 对于扫描版的pdf文件的翻译效果咋样呢？ 压根不支持
    - sayura 就是 marker 的作者做的开源多国语言和表格的 OCR 模型，我只测试了 PaddleOCR 高精度模型，Sayura 效果比它好很多，而且支持多国语言效果很好。缺点就是 Sayura 对 GPU 显存要求有点高，头疼，不太会量化模型
    - 💡 扫描件可以直接理解为图片，实际上是保持排版的图片翻译功能，可以参考微信的实现，长按图片点翻译可以自动翻译
    - 👷 202505: 遇到此问题时，请尝试使用 2.0 预览版 并启用高级选项中的 OCR Workaround 来翻译。
  - [为什么会出现完全重影？ ](https://github.com/PDFMathTranslate/PDFMathTranslate/issues/942)
    - 重影用2.0，开ocr workaround就行
  - 🎯 [pdf2zh 2.0 _202502](https://github.com/PDFMathTranslate/PDFMathTranslate/issues/586)
    - Core: I am completely rewriting it, related code is at funstory-ai/BabelDOC
  - https://github.com/funstory-ai/BabelDOC /6.2kStar/AGPL/202512/python
    - https://funstory-ai.github.io/BabelDOC/
    - Yet Another Document Translator
    - Provides a simple command line interface.
    - Provides a Python API.
    - Mainly designed to be embedded into other programs, but can also be used directly for simple translation tasks.
    - This project hopes to promote a standard pipeline and interface to solve the problem.
      - We offer an intermediate representation of the results from parser and can be rendered into a new pdf or other format. The pipeline is also a plugin-based system which everybody can add their new model, ocr, renderer, etc.
    - [部署 Babel DOC 到家用 NAS，PDF 自动翻译 _202504](https://zhuanlan.zhihu.com/p/1899886272828379973)
    - [科研论文翻译神器！BabelDOC：开源AI工具让PDF论文秒变双语对照，公式图表全保留 - 知乎](https://zhuanlan.zhihu.com/p/1892003359227089736)

- https://github.com/CBIhalsen/PolyglotPDF /2.1kStar/GPL/202509/python/js
  - A multilingual eBook processing tool supporting all eBook formats. 
  - Features online and offline translation while preserving original layouts.
  - Compatible with both scanned and digital PDFs. 
  - 目前效果，对于基于文本的pdf, polyglotpdf的解析方式依旧是最优解。 ocr和布局分析并不总是完美。
  - 对于报告型表格文档，polyglotpdf效果相当完美，当然表格中的复杂矢量数学公式依旧无法正确处理
  - 本项目采用与 Adobe Acrobat DC 编辑 PDF 类似的基本原理，基于 PyMuPDF 识别和处理 PDF 文本块, 这种方式直接处理 PDF 文本块，保持原有布局不变，实现高效的文本提取和修改
  - 🛝
    - 实测图片pdf在ocr后底部是原文, 文字散乱排布在上方, 视觉上是重影, 但分栏布局可以还原, 且识别后的每行文本和原文位置基本都一致
    - 💡🤔 更合理的流程是生成2个pdf image > text-pdf > translated-pdf, 这样就能既保持原有布局，又能无重影展示干净的译文pdf
  - [关于·ocr识别 ](https://github.com/CBIhalsen/PolyglotPDF/issues/6)
    - 请问考虑·添加·paddle作为OCR模型吗？ 文字PDF的翻译速度是我用过最快的，比pdfmathtran快几倍
# pdf-editor
- https://github.com/BDenizKoca/Tideflow-md-to-pdf /MIT/202511/ts/tuari
  - https://bdenizkoca.studio/projects/tideflow/
  - Turn Markdown into beautiful PDFs with Tideflow instantly - offline, portable desktop app
  - offline-first Markdown → PDF desktop app powered by Typst. Write on the left, get a beautifully typeset PDF on the right – instantly.
  - Typst (bundled binary) for PDF: Tideflow bundles the official Typst CLI (currently v0.13.1) for macOS, Windows, and Linux so the app works offline out of the box.
  - Zustand store (single slice: editor state, preferences, UI flags)
  - Export Formats: Primarily PDF, but also exports to PNG, SVG, and clean Markdown. No HTML export yet.
  - two-way scroll sync between editor & PDF preview (Has around %70 accuracy)
  - Clean, distraction‑lite editor (CodeMirror 6)
  - I wanted a dead-simple, elegant writing tool that outputs print‑ready PDFs without relying on a web service, LaTeX toolchains, or heavy exports. 
  - [Why Markdown at All?](https://bdenizkoca.studio/notes/creating-tideflow/)
  - [I created a free Markdown to PDF editor with true pagination and live preview. : r/Markdown _202511](https://www.reddit.com/r/Markdown/comments/1oq644g/i_created_a_free_markdown_to_pdf_editor_with_true/)
    - A lot of the elements are similar to KeenWrite (themes, real-time preview panel, synchronized scrolling, automatic ToC).
    - KeenWrite's architecture is as you describe in your blog post: Markdown to XHTML to TeX to PDF, which affords the possibility of a wide variety of themes.
    - Tideflow is positioned a bit differently. I built it to be dead simple for everyday use cases. The goal was: open the app, write Markdown, get a beautiful PDF instantly. No configuration complexity, no TeX knowledge needed, no giant toolchain to manage.
    - does KeenWrite support rowspan and colspan In tables?
      - No, is the short answer. The longer answer is more involved.
      - KeenWrite uses `flexmark-java` to convert Markdown into XHTML. The Tables Extension for flexmark-java supports column spans. So, technically, you could use its column span syntax to generate XHTML with colspans.

- https://github.com/luke-browning/pdf-web-edit /MIT/202309/ts/c#/ng/inactive
  - a web-based application for manipulating PDF files. 
  - It's main purpose is to pre-process documents before they are imported into a Document Management System (DMS) such as Paperless (-ng and -ngx) or stored in a directory based structure.

- https://github.com/jichang/unionpdf /MIT/202502/ts
  - https://jichang.github.io/unionpdf/
  - A universal pdf rendering/editing library
  - model, engine, react

- https://github.com/oomol-lab/pdf-craft /3.7kStar/AGPL > MIT/202512/python
  - convert PDF files into various other formats. This project will focus on processing PDF files of scanned books. 
  - This project can read PDF pages one by one, and use `DocLayout-YOLO` mixed with an algorithm I wrote to extract the text from the book pages 
  - 超过100页的，可转为EPUB，结合了本地OCR和云端LLM处理，兼顾效率和功能性，最终生成带目录分章节的EPUB
  - Starting from the official v1.0.0 release, pdf-craft fully embraces DeepSeek OCR and no longer relies on LLM for text correction.
    - removing the previous AGPL-3.0 dependency, allowing the entire project to be released under the more permissive MIT license
    - Note that pdf-craft has a transitive dependency on easydict (LGPLv3) via DeepSeek OCR.
  - [PDF Craft：一个更懂技术的开源 PDF 转换工具 _202512](https://linux.do/t/topic/1322118)
    - 我们基于 DeepSeek-OCR 重写了一个转换引擎：pdf-craft
    - 更智能的布局还原：特别优化了双栏和图文混排，目标是转成 Markdown 或 EPUB 后，还能有接近纸质书的阅读体验。
    - 更完美的 LaTeX 公式支持：无论是行内公式还是独立公式，都能精准识别并还原
    - 本地免费跑（我们最推荐的）
  - https://github.com/oomol-lab/epub-translator
    - uses AI large language models to automatically translate EPUB e-books while 100% preserving the original book's format, illustrations, table of contents, and layout. 

- https://github.com/cosformula/mdxport /MIT/202512/ts/svelte
  - https://www.mdxport.com/
  - 左边文本可编辑，右边预览只读
  - [Built a browser-based PDF exporter using Typst + WASM (No Pandoc/LaTeX setup required) : r/ObsidianMD _202512](https://www.reddit.com/r/ObsidianMD/comments/1ppmoql/built_a_browserbased_pdf_exporter_using_typst/)
    - 100% Local (WASM): It uses the Typst engine compiled to WebAssembly. all rendering happens in your browser. No data is sent to any server
    - Better Pagination: unlike the standard HTML-to-PDF print (which Obsidian uses), Typst handles page breaks smartly. It keeps table rows together and handles footnotes/math ($E=mc2$) beautifully.

- https://github.com/awesome-yasin/PDF-Verse /MIT/202312/js/ejs/inactive
  - https://pdf-verse.vercel.app/
  - a powerful web based PDF Editor with tools fexamplesor editing, converting, and manipulating PDFs.
  - Merge, compress, add or remove pages, or extract text using OCR technology. 

- https://github.com/ShizukuIchi/pdf-editor /202011/js/inactive
  - https://pdf-editor.now.sh/
  - Offline PDF editor. Add images, signatures, text to PDF in your browser

- https://github.com/gr2m/pdf-editor /201504/js/inactive/单文件
  - WYSIWYG PDF-Editor, plugin-free, using pdfkit and pdf.js

- https://github.com/xinglie/report-designer
  - https://xinglie.github.io/report-designer/
  - 打印设计、可视化、标签打印、编辑器、设计器、数据分析、报表设计、组件化、表单设计、h5页面、调查问卷、pdf生成、流程图、试卷、SVG、图形元素、物联网、标签纸
  - https://github.com/xinglie/magix5-playground

- https://github.com/rylog/pdf-editor-electron
  - /ts

- https://github.com/yashu2001/PDF-Generator-Electron-App /js
  - an electron app used to generate pdf documents with some text for making labels

- https://github.com/fraserxu/electron-pdf /202010/js
  - A command line tool to generate PDF from URL, HTML or Markdown files with electron.

- https://github.com/thinreports/thinreports
  - Thinreports is a PDF generation tool that provides Thinreports Basic Editor and Thinreports Section Editor, a design tool for editing templates, and Thinreports Generator, a Ruby library for generating PDFs.

- https://github.com/GoDinRyu/editor.md-electron /js
  - 基于Editor.md的markdown编辑客户端，支持docx转化md，导出到pdf文档。
# generator
- https://github.com/rkusa/pdfjs /MIT/202312/js
  - A Portable Document Format (PDF) generation library targeting both the server- and client-side.

- https://github.com/carboneio/carbone /CCL/202305/js
  - https://carbone.io/
  - simple report generator, from JSON to pdf, xslx, docx, odt...
  - Powerful report generator in any format PDF, DOCX, XLSX, ODT, PPTX, ODS, XML, CSV using templates and your JSON data as input

- https://github.com/betterwrite/pdfeasy /ts
  - JavaScript Client/Server Side PDF-Generator based in PDFKit
  - Plugins Ready!

- https://github.com/eKoopmans/html2pdf.js /3.6kStar/MIT/202109/js/inactive
  - Client-side HTML-to-PDF rendering using pure JS.
  - html2pdf.js converts any webpage or element into a printable PDF entirely client-side using `html2canvas` and `jsPDF`.

- https://github.com/PejmanNik/jikji /ts
  - report generator with React and NodeJS
  - Unlike the puppeteer-report, this library uses its layout engine instead of the browser layout engine for pagination, so it is 100% customizable. 
  - It supports both Client-side rendering and server-side generation.
  - Jikji provides all the necessary components to creates reach reports; you can build sections and pages with the header, footer, watermarks, etc. And give you the power to use thousands of JS libraries to create beautiful charts and distinguished reports and export it to PDF, Image ot HTML.

- https://github.com/isneezy/pdf-generator-service /MIT/202301/ts
  - simple express service that generates a pdf based on the submitted HTML using Chromium and Puppeteer.

- https://github.com/tuanpham-dev/react-invoice-generator /ts
  - allows you quickly make invoices and export them as PDF

- https://github.com/baptistejamin/node-microinvoice /js
  - elegant PDF invoice generator for Node using PDFKit. No Puppeteer
- https://github.com/Astrocoders/node-pdf-invoice /js
  - A Phantom free PDF invoice generator built with PDFKit

- https://github.com/rimiti/invoice-it /js
  - Generate your orders or your invoices and export them in html, pdf or buffer easily.  

- https://github.com/AmirTugi/tea-school
  - Simplified `HTML + CSS --> PDF` Generator for Nodejs
  - just a method combining PugJS, Node-Sass, and Puppeteer

- https://github.com/bleek42/pdf-generator /js
  - PDF file creation tool, using React, MaterialUI, JSPDF & html2canvas

- https://github.com/johnuberbacher/invoice-generator /js
  - An Invoice creator project built with React. 
  - Uses jspdf-react to capture the data from the modal and convert it from canvas -> pdf.

- https://github.com/IonicaBizau/nodeice /js
  - Another PDF invoice generator

- https://github.com/sschandi/create-resume /ts
  - Client Side, Private, PDF Resume Generator

- https://github.com/Kozea/WeasyPrint /8.4kStar/BSD/202512/python
  - https://weasyprint.org/
  - WeasyPrint is a visual rendering engine for HTML and CSS that can export to PDF. 
  - It aims to support web standards for printing. 
  - It is based on various libraries but not on a full rendering engine like WebKit or Gecko. The CSS layout engine is written in Python, designed for pagination, and meant to be easy to hack on.

- https://github.com/pdsuwwz/puppeteer-server
  - 基于 Puppeteer + Koa + Rollup + TypeScript, 将任意网页快速转换为 PDF, 图像, 支持将多个网页合并生成为一个 PDF 文件，支持 Cookie 的注入、PDF 水印和页眉页脚的插入

- https://github.com/kevalbhatt/puppeteer-pdf-generator /js
  - Internally server starts a headless browser and opens http://localhost:3000 application and creates the pdf (i.e print layout).
  - Note: Server-side pdf generator code is hardcoded so you will get same pdf every time.
# reader/viewer
- https://github.com/embedpdf/embed-pdf-viewer /1.8kStar/MIT/202508/ts
  - https://www.embedpdf.com/
  - https://app.embedpdf.com/
  - EmbedPDF is a framework‑agnostic, MIT‑licensed PDF viewer that drops into any JavaScript project.
  - Annotations (highlight, sticky notes, free text, ink) + comment
  - True redaction (content is actually removed)
  - Pluggable architecture & tree-shakable plugins
  - Smooth, virtualized scrolling
  - [PDF viewer using PDFium + WebAssembly — would love your input : r/opensource](https://www.reddit.com/r/opensource/comments/1kydm90/pdf_viewer_using_pdfium_webassembly_would_love/)
  - open source PDF viewer called EmbedPDF, based on PDFium (the same rendering engine used in Chrome) compiled to WebAssembly.
  - It’s meant to be an alternative to PDF.js, with a focus on rendering accuracy and customizability. You can use it with a full UI out of the box, or headless for full control.
  - It’s MIT-licensed and framework-agnostic.

- https://github.com/Stirling-Tools/Stirling-PDF /20.4kStar/GPL > MIT/202403/java/js
  - https://www.pdfdrills.com/
  - locally hosted web application that allows you to perform various operations on PDF files
  - locally hosted web based PDF manipulation tool using docker that allows you to perform various operations on PDF files
  - 依赖 Spring Boot + Thymeleaf、pdfbox、itext7、libreoffice转换格式、ocrMyPdf
  - 除了能给PDF打水印之外，还可以轻松批量给扫描的PDF文件瘦身，1秒钟搞定，太好用了
  - [New Browser-based PDF Editor (github link) : selfhosted](https://www.reddit.com/r/selfhosted/comments/10pexhn/new_browserbased_pdf_editor_github_link/)
  - https://twitter.com/dotey/status/1739426777091408207
    - 一个本地的处理 PDF 的工具，界面是 Web UI，可以支持 Docker 部署。
  - https://twitter.com/geekbb/status/1739627252701450251
    - Docker 真是方便，刚刚在 NAS 上弄了一个本地 PDF 工具 ：Stirling PDF，并通过 Cloudflare Tunnels 建立连接方便自己外网访问，再也不用担心 PDF 资料泄漏的问题了
  - [Fat VS Lite?  _202507](https://github.com/Stirling-Tools/Stirling-PDF/discussions/3940)
    - Lite: Only Java code, no external dependencies (features that rely on them are disabled). Affected endpoints: Compress, File to PDF, Repair, etc.,
    - Standard: Java + external dependencies (e.g., GhostScript, LibreOffice, qpdf), with this you have access to everything.
    - Fat: Standard Java + external dependencies + a large set of fonts.
  - [Editor needs a LOT of work _202512](https://github.com/Stirling-Tools/Stirling-PDF/discussions/5222)
    - It messes up the fonts...puts random spaces in between words, it drops paragraphs on top of each other, and you can't scroll the whole document - you have to click on each page at the top (?) On a 300+ page book, this is impossible. The UI is horrible.
    - we are working in it! As you mention it's not even beta but an alpha release as a concept to build on. We will get this improved! This is a top priority for us

- https://github.com/TheWebDevel/electron-pdf-conversion-article-proj /js
  - [Converting an Electron view content to PDF - DEV Community](https://dev.to/sathish/converting-an-electron-view-content-to-pdf-caa)
  - simple electron app to demonstrate the conversion of view into PDF.

- https://github.com/ikuokuo/electron-pdf-viewer
  - Demo for using PDF.js in Electron, with antd
- https://github.com/ZeroX-DG/EasyPDF /js
  - A simple library that use PDF.js for rendering pdf file on electron

- https://github.com/HeiSir2014/URL2PDF /js
  - An electron app that can convert HTML into pdf file. url 网页 转 pdf服务
  - 通过 Session WebRequest API 监控页面请求，当所有请求完成时，数据加载完毕后，开始执行printPDF功能，完整的打印所有页面内容。
  - Windows 用户需要确保Windows服务中的Spooler服务处于开启的状态，否则会打印失败
  - https://github.com/zeay/pdfmaker
    - Pdf maker electron and phantomjs

- https://github.com/CMOISDEAD/next-library /GPLv3/202307/js/inactive
  - Next Library is an innovative virtual library application that offers a seamless and personalized way to manage your book collection
  - Custom PDF Viewer Tool: Open and view PDF files directly within the virtual library program using a customized PDF viewer tool.

- https://github.com/PSPDFKit/pspdfkit-electron-example /JS
  - PSPDFKit for Electron Example Application

- https://github.com/nikensss/sign_here /js
  - Small electron app to add hand signature image to PDF

- https://github.com/praharshjain/Electron-PDF-Viewer /MIT/202302/java/js/inactive
  - PDF viewer created using Electron framework and PDF.js
  - https://github.com/praharshjain/Vudit-Desktop
    - cross-platform desktop file viewer

- https://github.com/ollm/OpenComic /JS
  - Comic and Manga reader, written with Node.js and using Electron

- pdf viewer
  - https://github.com/AlexRogalskiy/electron-pdfviewer
  - https://github.com/chastain1337/pdf_toolbox
    - An electron-react app for manipulating PDFs.

- https://github.com/scribusproject/scribus /cpp
  - open source page layout program which produces commercial grade output in PDF and Postscript, primarily, though not exclusively, for Linux.

- https://github.com/sagargurtu/lector /201908/js
  - PDF Reader built using Electron and PDF.js

- https://github.com/PDFTron/webviewer-mendix-sample
  - WebViewer is a powerful JavaScript-based PDF Library that's part of the Apryse PDF SDK. 
  - It provides a slick out-of-the-box responsive UI that interacts with the core library to view, annotate and manipulate PDFs that can be embedded into any web project.

- https://github.com/slotDumpling/multibility /202310/ts/inactive
  - https://slotdumpling.github.io/multibility/
  - Collaborative notes and PDF annotations
  - 协同笔记与PDF批注
  - 依赖draft-pad(基于paperjs-canvas)、antd.v4、antd-mobile.v5、immutable.v4、pdfjs、react-beautiful-dnd、socket.io

- https://github.com/davidbstein/pdf-tools /MIT/202202/js/inactive
  - A set of tools for really basic highlighting and reading PDFs because every tool I tried to use couldn't just act like an handful of highlighters

- https://github.com/algorithmx/electron-react-pdf-viewer /202502/ts
  - An electron app for viewing PDF files, written in Typescript-React
- https://github.com/ikuokuo/electron-pdf-viewer /MIT/202201/js/inactive
  - Demo for using PDF.js in Electron.

- https://github.com/koreader/koreader /lua
  - http://koreader.rocks/
  - An ebook reader application supporting PDF, DjVu, EPUB, FB2 and many more formats, running on Cervantes, Kindle, Kobo, PocketBook and Android devices

- https://github.com/Cimbali/pympress /GPLv2/202312/python
  - https://cimbali.github.io/pympress/
  - Pympress is a simple yet powerful PDF reader designed for dual-screen presentations

- https://github.com/pdfjs-express/pdfjs-viewer
  - Building a PDF.js viewer from the ground up
  - https://github.com/pdfjs-express/pdfjs-express-react-sample
    - PDF.js Express is a powerful JavaScript-based PDF Library that leverages PDF.js and adds additional features such as annotations, form support, and digitial signatures

- https://github.com/pdf-tools/pdf-web-viewer-samples /202502/js
  - PDF Web Viewer by Pdftools, Switzerland, is a JavaScript component for viewing and annotating PDFs.
# utils
- https://github.com/YuHuaOu/electron-print
  - 支持直接传PDF、图片的资源地址(将资源地址传到桌面端打印程序的接口中)，完成打印。electron、PDF、PNG
  - 支持直接传PDF、图片的资源地址到打印服务的接口中，完成打印
  - pdf打印目前仅支持windows平台
  - 应用接口收到内容后，包装一层数据，将其传进写好的打印队列调度器中进行打印任务处理

- https://github.com/RelaxedJS/ReLaXed
  - creates PDF documents interactively using HTML or Pug (a shorthand for HTML). 
  - It allows complex layouts to be defined with CSS and JavaScript, while writing the content in a friendly, minimal syntax close to Markdown or LaTeX.

- https://github.com/USEPA/pdf-data-extraction /js
  - The purpose of this project is to further the research and development of tools that NCEA can use in their creation of machine-readable datasets and machine learning research. 

- https://github.com/Cimorexave/desktop-document-manager /js
  - a desktop ElectronJS app to extract and edit data and tables from pdf to other formats

- https://github.com/ifnoelse/pdf-bookmark /java
  - pdf bookmark generator 目录 书签 大纲
  - 本项目用来给pdf书籍自动打上书签方便阅读

- https://github.com/stimulsoft/Samples-Reports.JS-for-Node.js
  - examples of usage Stimulsoft Reports. JS reporting tool in the Node.js applications, using JavaScript report engine. 

- https://github.com/plainlab/plainmerge /ts
  - PDF mail merge (PDF data merge / PDF generator using Excel files)

- https://github.com/kkdai/pdf_online_editor /python
  - a simple web application that allows users to upload a PDF file and display its pages as images. 
  - Users can select a page from the uploaded PDF and view its content as text.
  - 依赖streamlit、pdf2image、pypdf2、pillow

- https://github.com/chromium/pdfium /apache2/202509/cpp/chromium
  - https://pdfium.googlesource.com/pdfium/
  - The PDF library used by the Chromium project
  - PDFium uses the same build tooling as Chromium. PDFium is located in` third_party/pdfium` in Chromium's source code.
  - PDFium uses GN to generate the build files and Ninja to execute the build files.
  - PDFium may be built either with or without JavaScript support, and with or without XFA forms support. Both of these features are enabled by default.
  - By default, the entire project builds with C++20.
  - https://github.com/embedpdf/embed-pdf-viewer /MIT/202511/ts
    - [PDF viewer using PDFium + WebAssembly — would love your input : r/opensource](https://www.reddit.com/r/opensource/comments/1kydm90/pdf_viewer_using_pdfium_webassembly_would_love/)
    - open source PDF viewer called EmbedPDF, based on PDFium (the same rendering engine used in Chrome) compiled to WebAssembly.
    - It’s meant to be an alternative to PDF.js, with a focus on rendering accuracy and customizability. You can use it with a full UI out of the box, or headless for full control.
    - It’s MIT-licensed and framework-agnostic.

- https://github.com/pdfarranger/pdfarranger /GPL/202502/python
  - PDF Arranger is a small python-gtk application, which helps the user to merge or split PDF documents and rotate, crop and rearrange their pages using an interactive and intuitive graphical interface. 
  - It is a front end for pikepdf.
  - PDF Arranger is a fork of Konstantinos Poulios’s PDF-Shuffler
  - https://github.com/pikepdf/pikepdf /MPL/202502/cpp/python
    - https://pikepdf.readthedocs.io/
    - A Python library for reading and writing PDF, powered by QPDF

- https://github.com/hkdb/Densify /python
  - A GTK+ GUI Application written in Python that simplifies compressing PDF files with Ghostscript

- https://github.com/plainlab/plainprinter /GPLv3/202309/ts
  - Take multiple screenshots and convert them into a PDF file
# examples
- https://github.com/AnsellMaximilian/electron-excel-to-pdf-invoice-generator /ts
  - A desktop invoice generator that turns excel files (with a specifically formatted workbook) into pdf invoices for every customer.
  - 依赖xlsx、pdfkit

- https://github.com/tithanayut/pagepdf-rendering-server /js
  - a service for generating PDF file from HTML (via URL) on server. It integrates electron-pdf with express and lowdb to serve client as a REST API.
  - https://github.com/fraserxu/electron-pdf

- https://github.com/85599/Desktop-PDF-Generator-Electron /js
  - an electron app used to generate pdf documents with some text for making labels

- https://github.com/tani/yomu /js/pdfjs/简单渲染pdf
  - 英和辞書付きPDF閲覧ソフト

- https://github.com/bjrmatos/jsreport-electron-pdf /js
  - jsreport recipe which renders pdf from html using electron 

- https://github.com/surveyjs/survey-pdf
  - Supplementary component to the SurveyJS Form Library to download surveys as PDF files and generate editable PDF forms.
# office
- databyss /39Star/AGPLv3/202409/ts/js/inactive
  - https://github.com/databyss-org/databyss
  - https://databyss.org/
  - Write and cite, research and re-search, and never get lost in Databyss. Welcome to your new word processor.
  - Drag highlighted and/or annotated PDF files into any Page. Databyss will extract all your margin notes and highlighted passages so you can easily edit and search them.
  - 依赖pouchdb

- https://github.com/SpiderStrategies/pdf-officegen /js
  - A NPM module that accepts one or more PDF files and converts them into pptx/docs
  - This module is the successor of pdf-powerpoint
  - A rendering engine is used to transform each page of a PDF into a PNG image.
# sign
- https://github.com/open-pdf-sign/open-pdf-sign /java
  - Digitally sign PDF files from your commandline
# pdf4j
- OpenPDF /1.7kStar/LGPLv2||MPLv2/202009
  - https://github.com/LibrePDF/OpenPDF
  - OpenPDF is the LGPL/MPL open source successor of iText
  - based on a fork of iText 4.2.0 svn tag. 
  - changelog
    - 1.2.21 - 201906
- iText /7774Star/AGPL||Commercial/202009
  - https://github.com/itext/itext7
  - changelog
    - iText 0.x (2000-2006)
    - iText 1.x-2.x / iTextSharp 3.x-4.x (2006-2009)
      - The last release dates from 2009 (iText 2.1.7 / iTextSharp 4.1.6.0)
    - iText 5.x and iTextSharp 5.x (2009-2016)
      - In 2009, the license changed from the LGPL/MPL to the AGPL
      - iTextSharp was designed as the .NET port of the library 
      - and the release numbers were synchronized at the moment iText 5.0.0/iTextSharp 5.0.0 was released.
      - In Java, the library moved to Java 5.
    - iText 7.x (2016-present)
      - A complete rewrite, focusing on extensibility and modularity.
      - We no longer talk about iTextSharp, but iText for Java and for .Net (C#)
      - The Java version moved to Java 7.
      - iText 7 is dual licensed as AGPL/Commercial software.
      - Buying a license is mandatory as soon as you develop commercial activities distributing the iText software inside your product or deploying it on a network without disclosing the source code
- pdfbox /1.3kStar/Apache2/202009
  - https://github.com/apache/pdfbox
  - https://pdfbox.apache.org/
  - Java tool for working with PDF documents
  - allows creation of new PDF documents, manipulation of existing documents and the ability to extract content from documents.
  - changelog
    - 2.0.16 - 201906

## pdf viewer

- JPedal PDF library /11Star/LGPL/202009
  - https://github.com/Lonzak/JPedal
  - a fork of the last official [JPedal PDF library] 

- PDFrenderer  /162Star/LGPLv2/201912
  - https://github.com/katjas/PDFrenderer
  - It uses an improved version of JPedal's JBig2 decoder API.

- MuPDF /295Star/AGPLv3/202009/c
  - https://github.com/ArtifexSoftware/mupdf
  - https://github.com/muennich/mupdf
  - written in C, providing Java JNI
  - https://github.com/ArtifexSoftware/mupdf.js /AGPL
  - https://github.com/ArtifexSoftware/pdf2docx /AGPL
- https://github.com/pymupdf/PyMuPDF /8.6kStar/AGPLv3/202511/python
  - a high performance Python library for data extraction, analysis, conversion & manipulation of PDF (and other) documents.
  - PyMuPDF adds Python bindings and abstractions to MuPDF, a lightweight PDF, XPS, and eBook viewer, renderer, and toolkit. Both PyMuPDF and MuPDF are maintained and developed by Artifex Software, Inc.
- https://github.com/andytango/mupdf-js /AGPLv3/202406/ts/c/inactive
  - another Webassembly PDF renderer for node and the browser
  - This is a port of MuPDF to javascript and webassembly

- OpenViewerFX  /LGPL/
  - https://github.com/qwertme/OpenViewerFX
  - now part of JDeli

- https://github.com/sumatrapdfreader/sumatrapdf /14.7kStar/GPL/202505/C
  - http://www.sumatrapdfreader.org/
  - SumatraPDF reader for windows only
# pdf-doc/rag 👾
- https://github.com/docling-project/docling /39.3kStar/MIT/202509/python
  - https://docling-project.github.io/docling
  - Docling simplifies document processing, parsing diverse formats
  - Transform PDF to JSON or Markdown with ease and speed
  - Parsing of multiple document formats incl. PDF, DOCX, PPTX, XLSX, HTML, WAV, MP3, images (PNG, TIFF, JPEG, ...), and more
  - 模块化设计，集成 Unstructured、LayoutParser 等库，支持本地化处理
  - ~~需 CUDA 环境，部分功能依赖商业模型~~
  - Advanced PDF understanding incl. page layout, reading order, table structure, code, formulas, image classification, and more
  - Unified, expressive DoclingDocument representation format
  - export formats: Markdown, HTML, DocTags and lossless JSON
  - Plug-and-play integrations incl. LangChain, LlamaIndex, Crew AI & Haystack for agentic AI
  - Optionally applies OCR, Extensive OCR support for scanned PDFs and images
  - Support of Visual Language Models (SmolDocling)
  - Works on macOS, Linux and Windows environments. Both x86_64 and arm64 architectures.
  - https://huggingface.co/ibm-granite/granite-docling-258M /apache2
    - a multimodal Image-Text-to-Text model engineered for efficient document conversion

- https://github.com/opendatalab/PDF-Extract-Kit /8.6kStar/apache2 > AGPL/202501/python/inactive
  - https://pdf-extract-kit.readthedocs.io/zh-cn/latest/index.html
  - 布局检测：使用LayoutLMv3模型进行区域检测，如图像，表格, 标题, 文本等；
  - 公式检测：使用YOLOv8进行公式检测，包含行内公式和行间公式；
  - 公式识别：使用UniMERNet进行公式识别；
  - 光学字符识别：使用PaddleOCR进行文本识别
  - [Update license from Apache 2.0 to AGPL-3.0 _20240914](https://github.com/opendatalab/PDF-Extract-Kit/commit/1471e22384d4b02e1357926e4908296ed31dac51)

- https://github.com/py-pdf/pypdf /9.6kStar/BSD/202511/python
  - https://pypdf.readthedocs.io/en/latest/
  - A pure-python PDF library capable of splitting, merging, cropping, and transforming the pages of PDF files
  - It can also add custom data, viewing options, and passwords to PDF files. 
  - pypdf can retrieve text and metadata from PDFs as well.
  - [Reading the PDF metadata on large files _202507](https://github.com/py-pdf/pypdf/discussions/3390)
    - Is there a way to get the PDF attributes like Creation Date without loading the whole file into memory? We have large multi-gigabyte files and are trying to process them on a fleet of smaller ECS instances. The streaming features of pypdf have been great, but would love to get the same metadata without loading the whole file into memory.
    - Have you tried to pass a buffered file stream as stream argument ?
  - [Implementation of get_contents ](https://github.com/py-pdf/pypdf/discussions/3352)
    - `get_data()` is accessing the (decoded) byte data of the corresponding content stream, thus this only relevant when reading from the original PDF file.
    - skimming through the usages of self.pdf in ContentStream seems to indicate that this is used to avoid cloning if the content streams are both targeting the same PDF reference

- https://github.com/pdfminer/pdfminer.six /6.8kStar/MIT/202511/python
  - https://pdfminersix.readthedocs.io/
  - Community maintained fork of pdfminer
  - a tool for extracting information from PDF documents. It focuses on getting and analyzing text data. 
  - Pdfminer.six extracts the text from a page directly from the sourcecode of the PDF. 
  - It can also be used to get the exact location, font or color of the text.
  - It is built in a modular way such that each component of pdfminer.six can be replaced easily. You can implement your own interpreter or rendering device that uses the power of pdfminer.six for other purposes than text analysis.
  - Written entirely in Python.
  - Support for PDF-1.7 specification (well, almost).
  - Support for CJK languages and vertical writing.
  - Automatic layout analysis.
  - [For optimization of extracting text page by page  ](https://github.com/pdfminer/pdfminer.six/issues/533)
    - I get that using `StringIO` is a bit cumbersome. But using input and output streams in the way it was setup and its difficult to change. Anyway, besides being cumbersome it doesn't give any performance penalty.
  - https://github.com/euske/pdfminer /MIT/202001/archived
- https://github.com/dhdaines/playa /MIT/202511/python
  - The purpose of PLAYA is to provide a robust, efficent, parallel and parallelizable, pure-Python and Pythonic (for its author's definition of the term), lazy interface to the internals of PDF files.
  - PLAYA allows you to take advantage of multiple CPUs. This parallelism currently operates at the page level since this is the most logical way to split up a PDF
  - [Playa PDF: A strong pdfminer successor : r/Python](https://www.reddit.com/r/Python/comments/1jfk466/playa_pdf_a_strong_pdfminer_successor/)
  - This library is similar in scope to pdfminer and its fork pdfminer.six
  - It handles a broader range of PDFs and PDF issues, being very close to the (horrible) specification. For example, the author of the library (dhaines) has recently added an enormous test suite from PDF.js
  - it is faster than the other Python libs by a factor of at least two, if not three, and not only when parallelizing.
  - complete metadata extraction - this part is what got me into this since I am integrating this with Kreuzberg now 
  - It uses modern and full-type hints and exports, proper dataclasses.
  - https://github.com/dhdaines/paves /MIT/202511/python
    - PLAYA is intended to get objects out of PDF, with no dependencies or further analysis. 
    - The primary goal of PLAYA-PDF is to give access to all the objects and particularly the metadata in a PDF. 
    - One goal of PAVÉS (because there are a few) is to give an easy way to visualise these objects and metadata.

- https://github.com/jsvine/pdfplumber /9.2kStar/MIT/202511/python 
  - Plumb a PDF for detailed information about each text character, rectangle, and line. Plus: Table extraction and visual debugging.
  - Works best on machine-generated, rather than scanned, PDFs. 
  - Built on pdfminer.six.

- https://github.com/opendatalab/MinerU /44.2kStar/AGPLv3/202509/python
  - https://opendatalab.github.io/MinerU/
  - 一站式开源高质量数据提取工具，将PDF转换成Markdown和JSON格式
  - Magic-PDF 是一款将 PDF 转化为 markdown 格式的工具。支持转换本地文档或者位于支持S3协议对象存储上的文件。
  - Magic-Doc 是一款支持将网页或多格式电子书转换为 markdown 格式的工具。
    - 支持176种语言的准确识别
  - 集成 LayoutLMv3、YOLOv8 等模型，支持多模态解析（表格/公式/图像）
  - 支持 API 和图形界面
  - 依赖 GPU，表格处理速度较慢，配置复杂
  - MinerU2.5: currently the most powerful multimodal large model for document parsing. With only 1.2B parameters
  - Output text in human-readable order, suitable for single-column, multi-column, and complex layouts.
  - Extract images, image descriptions, tables, table titles, and footnotes.
  - Automatically recognize and convert formulas in the document to LaTeX format.
  - Automatically recognize and convert tables in the document to HTML format.
  - Automatically detect scanned PDFs and garbled PDFs and enable OCR functionality.
  - Remove headers, footers, footnotes, page numbers, etc., to ensure semantic coherence
  - Supports running in a pure CPU environment, and also supports GPU(CUDA)/NPU(CANN)/MPS acceleration
  - Compatible with Windows, Linux, and Mac platforms
  - https://huggingface.co/spaces/opendatalab/MinerU

- https://github.com/datalab-to/marker /27.3kStar/GPLv3/202508/python
  - https://www.datalab.to/
  - Marker converts documents to markdown, JSON, chunks, and HTML quickly and accurately.
  - Converts PDF, image, PPTX, DOCX, XLSX, HTML, EPUB files in all languages
  - Does structured extraction, given a JSON schema (beta)
  - Extensible with your own formatting and logic
  - 基于 PyMuPDF 和 Tesseract OCR，支持 GPU 加速（Surya OCR 引擎），开源轻量化
  - 处理速度快（比同类快 4 倍）
  - 缺乏复杂布局解析能力，依赖本地 GPU 资源
  - Removes headers/footers/other artifacts
  - Works on GPU, CPU, or MPS
  - Optionally boost accuracy with LLMs (and your own prompt)
  - For the highest accuracy, pass the `--use_llm` flag to use an LLM alongside marker. This will do things like merge tables across pages, handle inline math, format tables properly, and extract values from forms. 
  - It can use any gemini or ollama model. 
  - [Ingesting PDFs and why Gemini 2.0 changes everything | Hacker News](https://news.ycombinator.com/item?id=42952605)
    - Marker output will be higher quality than docling output across most doc types, especially with the `--use_llm` flag. A few specific things we do differently:
    - We have hybrid mode with gemini that merges tables across pages, improves quality on forms, etc.
    - we run an ordering model, so ordering is better for docs where the PDF order is bad
    - OCR is a lot better, we train our own model, surya
    - References and links
    - Better equation conversion (soon including inline)

- https://github.com/lumina-ai-inc/chunkr /AGPLv3/202410/python/ts/rust
  - https://chunkr.ai/
  - Vision model based PDF chunking.
  - We have temporarily switched to Textract for OCR from PaddleOCR. Textract is provided for free until we resolve PaddleOCR issues.
  - Lumina的一款基于视觉模型的PDF分块处理工具：Chunkr，速度每秒可处理约5页
  - 基于视觉模型进行段落提取和OCR，通过 Rust Actix 服务器统一输出，可实现单个NVIDIA L4 GPU上达到每秒约5页速度
  - 支持自托管部署，兼容GPU和CPU，提供用户界面

- https://github.com/CatchTheTornado/pdf-extract-api 
  - 一款可本地运行去除个人信息的PDF解析工具：pdf-extract-api，文档匿名化处理，可以识别表格数据、数字、数学公式，适合隐私性较强的处理需求，企事业单位、医疗机构等
  - 集成marker、surya-ocr、tessereact多种OCR策略，用LLM提高识别准确度, 支持输出JSON和Markdown

- https://github.com/pymupdf/pymupdf4llm /1.2kStar/AGPL/202511/python
  - https://pymupdf.readthedocs.io/en/latest/pymupdf4llm
  - a specialized extension of PyMuPDF designed specifically for extracting content from PDFs in a format that's optimized for Large Language Models (LLMs).
  - Converts PDFs to clean, structured Markdown format
  - Automatically identifies headers, paragraphs, tables, and images
  - Extracts images from PDFs
  - [Build a Multimodal RAG using — PyMuPDF4LLM-llamaindex-Qdrant _202411](https://ai.gopubby.com/build-a-multimodal-rag-using-pymupdf4llm-llamaindex-qdrant-e9d23a4409cc)
# pdf-video
- [PDF to Brainrot | MemenomeLM](https://www.memenome.gg/)
  - 把 PDF 转化为易上瘾的视频
  - 通过 AI 技术将传统的 PDF 学习材料转换为更生动有趣的视频形式, 既保留了学习内容的专业性, 又强调提高效率、改善学习体验和趣味性, 网站显示已经有超过 10w 学生使用
  - 用 AI 改造成交互式学习的过程, 交互视频、AI 和真人交互都可以
  - https://x.com/0xPaulius/status/1852697757124845684
    - Been using this to post automated tiktoks on the latest research papers, its actually getting pretty good traction
# more-pdf
