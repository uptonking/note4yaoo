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
  - 提取pdf中插图/图表的思路是分步执行, vlm返回bbox, 然后通过pymupdf裁剪

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
  - https://github.com/Lulzx/tinypdf /MIT/202512/ts
    - Minimal PDF creation library. <400 LOC, zero dependencies, makes real PDFs.

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
  - https://react-pdf.org/repl /示例渲染的页面内容为dom元素
    - 示例效果是左边是react jsx代码， 右边是pdf预览， 感觉不如markdown/typst的预览
  - React renderer for creating PDF files on the browser and server
  - 使用了 pdfkit
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
  - [Mismatching worker version with pdfjs-dist as a direct dependency _202306](https://github.com/wojtekmaj/react-pdf/discussions/1520)
    - If you've installed pdfjs-dist as a direct dependency and the version is not matching the pdfjs-dist that react-pdf depends on, you may get an error
    - In this case I have this "pdfjs-dist": "3.7.107" in my package.json, but react-pdf depends on "pdfjs-dist": "3.6.172". To solve this, make sure to use the worker provided by the pdfjs-dist version that react-pdf specifically depends on
    - Unfortunately you have to change this back to "pdfjs-dist/build/pdf.worker.min.js" if the direct dependency version matches react-pdf's version
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

- https://github.com/LibPDF-js/core /440Star/MIT/202601/ts
  - https://libpdf.dev/
  - modern PDF library for TypeScript. Parse, modify, and generate PDFs with a clean, intuitive API
  - LibPDF was born from frustration at Documenso
    - PDF.js is excellent for rendering and even has annotation editing — but it requires a browser
    - pdf-lib has a great API, but chokes on slightly malformed documents
    - pdfkit only generates, no parsing at all
    - We kept adding workarounds. Eventually, we decided to build what we actually needed
  - [Introducing LibPDF: The PDF Library TypeScript Deserves - Documenso _202601](https://documenso.com/blog/introducing-libpdf-the-pdf-library-typescript-deserves)
  - https://x.com/lxunos/status/2014805777551392968  _202601
    - Introducing LibPDF the library that we’ve always wanted for PDF parsing, manipulation and signing (MIT)
    - It does text/line/word extraction but won't do OCR, so if you're dealing with a scanned document you would need other tooling.
      - For a multi column layout I'm not sure, we parse all the text operators we can find and do glyph mapping.
      - Then using the font metrics we get everything onto a baseline and aggregate that into lines/words.
    - @documenso has embeddable signing, works with any framework, is customizable, and open source.
    - LibPDF handles the low-level PDF work. Documenso handles the signing UX. Use both.
    - how would you compare this to reducto
      - I'd say they're more focused on document extraction, for a rasterised document they'd be way better if that's your sole focus.
    - just wrap pdfium.. wont beat its performance
    - Pdf nightmares
      - layering citation bounding boxes
      - free text search
      - resizing

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

- https://github.com/agentcooper/react-pdf-highlighter /1.4kStar/MIT/202409/ts/inactive
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

- https://github.com/gavrielc/Nano-PDF /903Star/MIT/202512/python
  - A CLI tool to edit PDF slides using natural language prompts, powered by Google's Gemini 3 Pro Image ("Nano Banana") model.
  - Natural Language Editing: "Update the graph to include data from 2025", "Change the chart to a bar graph".
  - Add New Slides: Generate entirely new slides that match your deck's visual style.
  - Non-Destructive: Preserves the searchable text layer of your PDF using OCR re-hydration.
  - Multi-page & Parallel: Edit multiple pages in a single command with concurrent processing.
    - The tool processes multiple pages in parallel for speed, with configurable resolution (4K/2K/1K) to balance quality vs. cost.
  - 💡 How It Works
    - Converts target PDF pages to images using Poppler
    - Style References: Optionally includes style reference pages with generation request to understand visual style (fonts, colors, layout)
    - Sends images + prompts to Gemini 3 Pro Image, which generates edited versions
    - OCR Re-hydration: Uses Tesseract to restore searchable text layer to generated images
    - PDF Stitching: Replaces original pages with AI-edited versions while preserving document structure
  - https://x.com/GithubProjects/status/1995953642772500850
    - Most PDFs can be converted to an editable formats. This feels like over engineering lowkey
  - [Show HN: Nano PDF – A CLI Tool to Edit PDFs with Gemini's Nano Banana | Hacker News _202511](https://news.ycombinator.com/item?id=46090619)
    - Does this mean the text only pdf page is transformed into an image that covers the full page, but the text is still under there. So, any machine based extraction would still get the text, but would probably loose all the bounding box information and regular users cannot just use their mouse to select text anymore?
    - So you convert the PDF into image, edit the image, then convert the image back into a PDF.
      - This is the usual workflow dealing with pdfs (unfortunately)
    - A side effect of replacing entire pages with images is that the file size will expand dramatically. Most PDFs only contain a couple of images
    - Interesting approach. I've spent a lot of time wrangling PDF internals recently, and the issue is usually maintaining the xref table integrity when you inject new content streams.
    - Does this approach rewrite the entire file structure on save, or are you appending incremental updates to the EOF? Incremental is safer for corruption, but file size bloats quickly with AI-generated diffs.

- https://github.com/yeahhe365/LongImg-Splitter /MIT/202512/ts
  - [网页工具：长图转多页 PDF 文件工具，方便 AI 分析  ](https://linux.do/t/topic/1360957)

- https://github.com/DDULDDUCK/every-pdf /1kStar/MIT/202601/python
  - all-in-one desktop PDF toolkit to edit, convert, merge, and secure your documents. Built with Electron, Next.js, and Python.
  - PDF Editor (New!): Add text, signatures, images, and checkboxes to complete your documents.
  - Converting PDFs to different formats and converting different formats to PDFs 
  - split, merge, Watermark
  - Framework: Nextron (Next.js + Electron)
  - Backend: Python, FastAPI
  - Build/Deployment: Electron Builder
  - [My free, open-source PDF Editor is ready. Edit, sign, and merge PDFs without paying a dime. : r/macapps _202508](https://www.reddit.com/r/macapps/comments/1miyrty/my_free_opensource_pdf_editor_is_ready_edit_sign/)
    - Can it edit text? That’s the one feature I’m missing from preview.
    - There is no function to change text within PDF yet, but there is a function to add text separately
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

- https://github.com/awesome-yasin/PDF-Verse /MIT/202312/js/ejs/inactive
  - https://pdf-verse.vercel.app/
  - a powerful web based PDF Editor with tools for editing, converting, and manipulating PDFs
  - Merge, compress, add or remove pages, or extract text using OCR technology. 
  - built with Node.js, EJS, Express.js, and `PDF-lib`, and features a user-friendly interface using jQuery and Bootstrap
  - The Edit PDF tool is made using a combination of Bootstrap, PDF.js, Fabric.js, and Prettify.js.
  - 依赖jimp

- https://github.com/ShizukuIchi/pdf-editor /1.8kStar/MIT/202403/js/inactive
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

- https://github.com/JakubMelka/PDF4QT /1.2kStar/LGPLv3 > MIT/202512/cpp
  - https://jakubmelka.github.io/
  - Open source PDF editor.
  - This software is consisting of PDF rendering library, and several applications, such as advanced document viewer, command line tool, and document page manipulator application. 
  - Software is implementing PDF functionality based on PDF Reference 2.0. 
  - Software works on Microsoft Windows / Linux.
  - As of April 27, 2025, The change to the MIT License was made to provide greater freedom and flexibility for both open-source and commercial use
  - qt LGPL
  - libjpeg, OpenJPEG, Blend2D
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
  - [Browser-based PDF Editor and PDF Toobox Stirling-PDF : r/selfhosted _202305](https://www.reddit.com/r/selfhosted/comments/13glhyr/browserbased_pdf_editor_and_pdf_toobox_stirlingpdf/)

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

- https://github.com/ollm/OpenComic /GPL/202511/js
  - https://opencomic.app/
  - Comic and Manga reader, written with Node.js and using Electron

- pdf viewer
  - https://github.com/AlexRogalskiy/electron-pdfviewer
  - https://github.com/chastain1337/pdf_toolbox
    - An electron-react app for manipulating PDFs.

- https://github.com/scribusproject/scribus /542Star/GPLv2/202512/cpp
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

- https://github.com/MarkPDFdown/markpdfdown /apache2/202509/python
  - 一款基于大模型视觉识别的高质量PDF转Markdown工具
  - Supports OpenAI and OpenRouter through LiteLLM
  - Flexible CLI: Both file-based and pipe-based usage modes
  - Modular Architecture: Clean, maintainable codebase with separation of concerns

- https://github.com/USEPA/pdf-data-extraction /js
  - The purpose of this project is to further the research and development of tools that NCEA can use in their creation of machine-readable datasets and machine learning research. 

- https://github.com/camelot-dev/camelot /MIT/202508/python/inactive
  - https://camelot-py.readthedocs.io/
  - A Python library to extract tabular data from PDFs
  - https://github.com/camelot-dev/excalibur /1.8kStar/MIT/202501/python/js
    - https://excalibur-py.readthedocs.io/
    - A web interface to extract tabular data from PDFs. powered by Camelot.
    - Note: Excalibur only works with text-based PDFs and not scanned documents
    - control over your data. All file storage and processing happens on your own local or remote machine.
    - Excalibur can be configured with MySQL and Celery for parallel and distributed workloads. By default, sqlite and multiprocessing are used for sequential workloads.
    - Upload a PDF and enter the page numbers you want to extract tables from.
    - Go to each page and select the table by drawing a box around it. (You can choose to skip this step since Excalibur can automatically detect tables on its own. )
    - Click on "View and download data" to see the extracted tables.

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

- https://github.com/pi-dal/ebook-toc /202511/python
  - a Python CLI that extracts a book’s Table of Contents (TOC) from PDFs using a Vision-Language Model (VLM), then optionally embeds the TOC back into the PDF as bookmarks. 
  - The current implementation integrates SiliconFlow’s Qwen3‑VL‑32B‑Instruct for TOC detection and printed‑page offset estimation. 
  - It supports scanned PDFs by falling back to page images when text is unavailable.
  - Powered by `PyMuPDF` for PDF parsing and bookmark embedding.
  - Input handling (ebooktoc/cli.py): validates local files or downloads remote PDFs
  - Page extraction (ebooktoc/vlm_api.py): extracts per‑page text (or renders JPEG when text is empty), batches VLM requests, and parses JSON robustly.
  - TOC parsing (ebooktoc/toc_parser.py): normalizes entries, deduplicates, filters, and infers missing trailing numeric targets.
  - Offset and mapping (ebooktoc/fingerprints.py, ebooktoc/cli.py): computes dominant dimensions, builds a canonical index map (logical → PDF), and estimates printed‑page offsets by sampling pages with the VLM; stores toc, page_offset, fingerprints, and page_map in JSON.
  - Apply phase (ebooktoc/pdf_writer.py, ebooktoc/cli.py): rebuilds the canonical map, refines the offset, resolves target pages, and writes bookmarks.

- https://github.com/jiangnan1224/pdf-toc-editor /202601/python/js
  - 智能 PDF 目录编辑器
  - 智能目录提取：内置高精度算法，一键扫描文档前 20 页并自动识别潜在层级结构。
  - 自由拖拽排序：支持通过手柄直接拖拽调整目录顺序，所见即所得
  - 支持三级目录结构（章、节、点），轻松应对复杂文档。
  - 自适应纸质页码与电子页码的偏差，确保跳转精准无误。
  - 后端: Python (Flask), pypdf
  - 前端: HTML5, Vanilla JavaScript, Tailwind CSS
  - [【开源自荐】pdf目录生成工具 _202601](https://linux.do/t/topic/1480789)

- https://github.com/zjm18023/pdf-watermark-remover /MIT/202601/python/tinker
  - [做了一个PDF去除水印的工具，可视化操作界面，支持区域删除和文字删除两种模式 ](https://linux.do/t/topic/1408892)
  - PyMuPDF (fitz) - PDF 文件处理和渲染
  - 枕头 (PIL) - 图像处理
  - CustomTkinter - 现代化 GUI 框架
  - CTkMessagebox - 消息框组件

- https://github.com/YiYoYiYoYiYo-Web3/PDF-Text-Remover /AGPL/202512/python
  - 用AI搓了个把PDF文字去除的工具 
  - 主要思路是把PDF分页后用大香蕉:banana: 重新生成一个一样但是无文字的图片，然后再拼成PPT/PDF，后续自己把文字拼上去。
  - 后来想加入文字识别，用了tesseract + AI 合并文字块 + 坐标映射，但是有伪文字不太好识别，基本上搞出来的文字最后都得重新编辑==。实在没办法了，丢上来看哪位大佬有兴趣的话解决一下 
  - [一个没啥用的PDF去文字工具  ](https://linux.do/t/topic/1257896)
# examples
- https://github.com/AnsellMaximilian/electron-excel-to-pdf-invoice-generator /ts
  - A desktop invoice generator that turns excel files (with a specifically formatted workbook) into pdf invoices for every customer.
  - 依赖xlsx、pdfkit

- https://github.com/tithanayut/pagepdf-rendering-server /js
  - a service for generating PDF file from HTML (via URL) on server. It integrates electron-pdf with express and lowdb to serve client as a REST API.
  - https://github.com/fraserxu/electron-pdf

- https://github.com/RyotaUshio/obsidian-pdf-plus /MIT/202508/ts
  - https://ryotaushio.github.io/obsidian-pdf-plus/
  - the most Obsidian-native PDF annotation & viewing tool ever.

- https://github.com/85599/Desktop-PDF-Generator-Electron /js
  - an electron app used to generate pdf documents with some text for making labels

- https://github.com/tani/yomu /js/pdfjs/简单渲染pdf
  - 英和辞書付きPDF閲覧ソフト

- https://github.com/bjrmatos/jsreport-electron-pdf /js
  - jsreport recipe which renders pdf from html using electron 

- https://github.com/surveyjs/survey-pdf
  - Supplementary component to the SurveyJS Form Library to download surveys as PDF files and generate editable PDF forms.

- https://github.com/seanpedrick-case/doc_redaction /34Star/AGPL/202603/python
  - https://seanpedrick-case.github.io/doc_redaction/
  - https://huggingface.co/spaces/seanpedrickcase/document_redaction_vlm
  - Redact PDF/image-based documents, Word, or CSV/XLSX files using a graphical user interface.
  - To extract text from documents, the 'Local' options are `PikePDF` for PDFs with selectable text, and OCR with Tesseract. 
    - Use AWS Textract to extract more complex elements e.g. handwriting, signatures, or unclear text. 
    - `PaddleOCR` and VLM support is also provided 
  - For PII(personally identifiable information) identification, 'Local' (based on `spaCy`) gives good results if you are looking for common names or terms, or a custom list of terms to redact 
  - sudo apt-get install -y tesseract-ocr poppler-utils
  - 依赖gradio、pdfminer.six、pymupdf、pikepdf、pdf2image、opencv、presidio-image-redactor
  - [Local VLMs (Qwen 3 VL) for document OCR with bounding box detection for PII detection/redaction workflows (blog post and open source app) : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r8smbk/local_vlms_qwen_3_vl_for_document_ocr_with/)
    - I have now implemented OCR with bounding box detection into the Document redaction app 

- https://github.com/leedrake5/unredact /GPL/202512/python
  - This repository contains a Python utility for extracting selectable (but visually redacted) text from PDF files and presenting it in a clear, human-readable format while preserving pagination and layout as closely as possible.

- https://gitlab.com/Nystik/inkheart /apache2/202512/rust/js/svelte
  - A self-hosted PDF library indexer and reader, written in Rust for the backend and Svelte for the frontend SPA.
  - Direct linking to specific pages
  - [Inkheart - Self-hosted PDF organisation and reader : r/selfhosted _202601](https://www.reddit.com/r/selfhosted/comments/1q11s7a/inkheart_selfhosted_pdf_organisation_and_reader/)
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

- https://github.com/yfedoseev/pdf_oxide /MIT/202603/rust/ts
  - https://oxide.fyi/
  - The fastest PDF library for Python and Rust. 
  - written in Rust with Python bindings
  - [Open-source PDF text extraction library (100% pass rate on 3, 830 test documents, MIT licensed) : r/pdf _202602](https://www.reddit.com/r/pdf/comments/1rdhuae/opensource_pdf_text_extraction_library_100_pass/)
    - I tested this against 3,830 PDFs across three major suites: veraPDF (conformance), Mozilla pdf.js (real-world), and DARPA SafeDocs (adversarial/broken files).
  - [PDF Oxide -- Fast PDF library for Python with engine in Rust (0.8ms mean, MIT/Apache license) : r/Python](https://www.reddit.com/r/Python/comments/1rjsq84/pdf_oxide_fast_pdf_library_for_python_with_engine/)

- OpenViewerFX  /LGPL/
  - https://github.com/qwertme/OpenViewerFX
  - now part of JDeli

- https://github.com/sumatrapdfreader/sumatrapdf /14.7kStar/GPL/202505/C
  - http://www.sumatrapdfreader.org/
  - SumatraPDF reader for windows only
# pdf-ai 👾
- https://github.com/yeahhe365/InsightPDF /MIT/202601/ts
  - https://insightpdf.pages.dev/
  - 基于 AI 的 PDF 智能助手，支持见解提取、内容总结和智能文档搜索
  - 基于 Google Gemini 多模态模型构建的智能文档助手，支持精确的视觉定位与边框高亮。
  - 视觉定位 (Visual Grounding) AI 不仅回答问题，还会自动跳转到 PDF 对应页面，并用红框高亮显示答案来源（支持文本段落、图表、数据表格）
  - 聊天记录和设置均存储在浏览器本地（LocalStorage/IndexedDB），只需配置 Key，无需担心数据泄露。
  - PDF 渲染: React-PDF

- https://github.com/MrAMS/Smart-Search-PDFs /MIT/202601/python/qt5
  - 🔍 智能 PDF 搜索引擎 - 基于语义向量(embeddings)和 BM25 的混合搜索系统，可用于开卷考试离线搜索PDF课件
    - 一个基于语义向量（Embeddings）和 BM25 算法的本地化 PDF 混合搜索工具。
  - 全部在本地运行，无需 API Key，保护隐私。
    - 本地端侧：无需 GPU/API，使用 FastEmbed 和轻量级模型，CPU 也能流畅运行，无需 OpenAI API Key。
  - ux交互是双栏布局，左侧是文本，右侧是pdf原文，左侧搜索出的文本，右侧不会高亮
  - 混合搜索（智能推荐）： 结合了语义理解和关键词匹配。不仅能搜到字面一样的，还能搜到意思相近的。结果自动按相关度排序。
    - 语义搜索： 哪怕你输入的词文中没出现，只要意思对，就能搜到。（基于 Jina AI 的 Embeddings 模型）。
    - BM25 关键词： 经典的倒排索引算法，不仅是精确匹配，还能处理词频权重。
    - 大文件支持：动态加载机制，几百页的文档滚动流畅不卡顿。
  - [[开源自荐] 开卷考试/论文搜索神器 - 基于语义向量和BM25的PDF文件搜索软件 ](https://linux.do/t/topic/1408107)
    - 不管是开卷考试需要在几百页的 PPT 里瞬间定位知识点，还是写论文时需要在几十篇参考文献中寻找佐证，传统的 Ctrl+F 往往力不从心
# pdf-doc/rag 🔗
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
    - Since this project uses YOLO code and PyMuPDF for file processing, these components require compliance with the AGPL-3.0 license

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
  - https://github.com/RapidAI/RapidDoc /apache2/202512/python/非VLM
    - RapidDoc 是一个轻量级、专注于文档解析的开源框架，支持 OCR、版面分析、公式识别、表格识别和阅读顺序恢复 等多种功能。
    - 框架基于 `Mineru` 二次开发，移除 VLM，专注于 Pipeline 产线下的高效文档解析，在 CPU 上也能保持不错的解析速度。
    - 基于 MinerU 改造而来，已移除原项目中的 YOLO 模型，并替换为 PP-StructureV3 系列 ONNX 模型。 由于已移除 AGPL 授权的 YOLO 模型部分，本项目整体不再受 AGPL 约束。
    - 项目所使用的核心模型主要来源于 PaddleOCR 的 PP-StructureV3 系列（OCR、版面分析、公式识别、阅读顺序恢复，以及部分表格识别模型），并已全部转换为 ONNX 格式，支持在 CPU/GPU 上高效推理。
    - 基于gradio开发的webui，界面简洁，仅包含核心解析功能，免登录
  - [MinerU商业化二开 _202505](https://linux.do/t/topic/640019)
    - 官方版本问题：包含禁止非商业的排序模型layoutreader，
    - 使用规则排序替换排序模型layoutreader
    - 优化Dockerfile（在项目根目录下）：集成libreoffice到容器，支持直接解析docx、ppt等文件
    - 解决libreoffice转码和MinerU识别中文乱码问题
    - 使用fastapi开发了api服务，部署后无需再次做接口开发（在web_service目录下）

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
- https://github.com/datalab-to/pdftext /644Star/apache2/202506/python
  - Text extraction like `PyMuPDF`, but without the AGPL license. PDFText extracts plain text or structured blocks and lines. 
  - It's built on `pypdfium2`, so it's fast, accurate, and Apache licensed.
  - It first uses pypdfium2 to extract characters in order, along with font and other information. Then it uses a simple decision tree algorithm to group characters into lines and blocks. It does some simple postprocessing to clean up the text.
  - built on some amazing open source work, including:  pypdfium2, scikit-learn

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

- https://github.com/QuivrHQ/MegaParse /apache2/202408/python/inactive
  - https://pypi.org/project/megaparse/
  - a powerful and versatile parser that can handle various types of documents with ease
  - Parse PDFs, Docx, PPTx in a format that is ideal for LLMs
  - Files: ✅ PDF ✅ Powerpoint ✅ Word
  - Content: ✅ Tables ✅ TOC ✅ Headers ✅ Footers ✅ Images

## pdf-extraction

- https://github.com/quest-bih/quest-pdf-tools /AGPL/202512/python
  - FastAPI-based web application and API service for processing PDF documents
  - The service can be deployed either as a full web application with an intuitive interface or as a standalone API.
  - PDF Layout Analysis: Detects and annotates different document elements including titles, text blocks, figures, tables, and formulas
  - Automatically identifies and removes headers, footers, and other irrelevant content from PDFs
  - 🖼️ Figure Extraction: Extracts and exports figures from PDFs into separate image files
    - The bounding box computation happens in `src/doc_layout.py` during `YOLO` detection. YOLO runs inference on the rendered image (internally resized to 1024x1024). 
    - Each cropped figure is saved as a PNG file with a naming convention like {pdf_name}_page{N}_figure{M}.png 
    - the cropped figures are saved to the filesystem
    - the figure extraction uses `PyMuPDF`'s `get_pixmap()` method. This method renders the PDF page as an image at 300 DPI, regardless of the original PDF format
    - PyMuPDF handles the conversion internally - you get the same rendered image output for both types
  - Table Extraction: Identifies and exports tables from PDFs into separate files
  - Text Extraction: Extracts plain text content from PDFs with preserved formatting
  - YOLO-based Detection: Utilizes DocLayout-YOLO model for accurate document layout analysis
  - https://github.com/huridocs/pdf-document-layout-analysis /1.1kStar/apache2/202601/python
    - A Docker-powered microservice for intelligent PDF document layout analysis, OCR, and content extraction
    - The service offers both a user-friendly Gradio web interface for interactive use and a comprehensive REST API
    - Export to JSON, Markdown, HTML, and visualize PDF segmentations
    - Extract tables as HTML and formulas as LaTeX
    - Apply OCR to scanned documents: uses Tesseract OCR with support for 150+ languages
    - Visual & Fast Models - Choose between VGT (Vision Grid Transformer) for accuracy or LightGBM for speed
    - Translate documents to multiple languages using Ollama models
  - https://github.com/huridocs/pdf-table-of-contents-extractor
    - extract Table of Contents (TOC) information from PDF files using the outputs generated by the pdf-document-layout-analysis service
  - https://github.com/huridocs/pdf-text-extraction
    - extract text from PDF files

- https://github.com/Flopsky/MarkThat /MIT/202601/python
  - A Python library for converting images and PDFs to Markdown or generating rich image descriptions using state-of-the-art multimodal LLMs.
  - Multiple Provider Support: OpenAI, Anthropic, Google Gemini, Mistral, and OpenRouter
  - Advanced Figure Extraction: Automatically detect, extract, and process figures from PDFs
    - 💡 可参考插图提取的流程逻辑 👇 
    - Detection: Analyzes document content to identify pages with figures
    - Coordinate Mapping: Overlays coordinate grids and identifies figure boundaries
    - Extraction: Crops figures using precise coordinate mapping
    - Integration: Embeds figure paths into the final markdown output
  - Robust Retry Logic: Intelligent retry with fallback models and failure feedback
  - Async Support: Concurrent processing for improved performance
  - Clean architecture: Type-safe, well-documented, and thoroughly tested
  - 实测可运行的模型包括, gpt-4o-mini, mistral-medium, nemotron-12b-vl, 🤔 但效果都很差

- https://github.com/tatevik-t/pdf_visual_extraction /MIT/202509/python/inactive
  - A Python library for extracting text and visual elements (tables, figures) from PDF document
  - Use OpenAI's GPT-4o-mini to detect and extract tables and figures
    - 🧊 返回bbox数据, 需要手动裁剪图片
  - Convert extracted tables to CSV format using LLM

- https://github.com/AdemBoukhris457/Doctra /apache2/202511/python
  - https://ademboukhris457.github.io/Doctra/
  - Parse, extract, and analyze documents with ease
  - Doctra requires `Poppler` for PDF processing
  - `StructuredPDFParser` is a comprehensive PDF parser that extracts all types of content from PDF documents
    - Uses `PaddleOCR` for accurate document layout analysis
    - Supports both `PyTesseract` (default) and `PaddleOCR` PP-OCRv5_server for text extraction
    - Visual Element Extraction: Saves figures, charts, and tables as images
    - VLM Integration: Optional conversion of visual elements to structured data
    - Multiple Output Formats: Generates Markdown, Excel, and structured JSON
  - https://github.com/AdemBoukhris457/Documents-Parsing-Lab /202511/jupyter
    - Jupyter notebooks testing different OCR models for document parsing (Dolphin, MonkeyOCR, Marker, Nanonets, ...)
    - This repository enables easy benchmarking and practical usage of the latest open-source and cloud-based solutions for document image processing.
    - a quick start guide for getting started with Doctra, a powerful tool for structured document parsing without Vision Language Models (VLM).

- https://github.com/aitomatic/ai-vision-capture /apache2/202601/python
  - A Python library for extracting and analyzing content from PDF, Image, and Video files using VLM
  - Supports multiple providers including OpenAI, Anthropic Claude, Google Gemini, and Azure OpenAI.
  - Async Processing: Configurable concurrency for batch operations
  - Structured Output: Template-based data extraction to JSON
  - Pluggable Architecture: Provider abstraction with auto-detection
  - PDF-to-image conversion using PyMuPDF (fitz)
  - VisionCapture: Used for extracting specific fields from documents (e.g., forms, technical diagrams)
    - 似乎只提取字段, 不提取插图

- https://github.com/iamarunbrahma/vision-parse /457Star/MIT/202509/python
  - Parse PDFs into markdown using Vision LLMs
    - 实测本地模型不好用, 很多小图片
  - Intelligently identifies and extracts text, tables, and LaTeX equations from scanned documents into markdown-formatted content with high precision
  - Multi-LLM Support: Seamlessly integrates with multiple Vision LLM providers such as OpenAI, Gemini, and Llama for optimal accuracy and speed
  - Supports local model hosting with Ollama for secure, no-cost, private, and offline document processing
  - 🛝
    - VisionParserError: Failed to convert page 1 to base64-encoded PNG: Ollama Model processing failed: timed out

- https://github.com/EsmaeilNarimissa/SciDOCX /MIT/202511/python/inactive
  - scientific document conversion and multimodal RAG pipeline powered by DeepSeek-OCR and Qwen2-VL.
  - DeepSeek-OCR: pdf > markdown > pandoc > docx
  - Dual Output:
    - Markdown and DOCX for editing and publishing.
    - JSONL elements (paragraphs, tables, figures) for multimodal retrieval.
  - Embedded Figures: Extracts, deduplicates, and embeds figures with correct captions in both DOCX and JSONL outputs.
  - optionally use Qwen2-VL-2B-Instruct to generate concise, factual figure descriptions.
  - PyMuPDF for PDF processing

- https://github.com/gsmatheus/pdf-image-extractor /202511/python
  - a Python script designed to process PDF files, specifically extracting and saving images embedded within the pages of the document. 
  - Automatically resizes the extracted images to 60% of their original size, ensuring consistent output and potentially reducing file size.
  - Text Extraction: For each processed page, the script also extracts and prints the textual content.
  - pdfplumber, fitz (PyMuPDF), PIL (Pillow)

- https://github.com/linjc16/PDF-Extraction /MIT/202303/python
  - A tool for extracting tables and figures from PDF files.
  - Pipeline for Table and Figure Extraction from Papers
  - First, use `PaddleOCR` to extract text, tables and figures from each paper.
    - We first convert PDF to images page by page by using `PyMuPDF`. To improve the performance of the following OCR operation, these images are unpsamped 8x to get high resolution inputs.
    - Then, use the results from the last step to output the final extracted samples.

- https://github.com/EvilFreelancer/img2md-vlm-ocr /MIT/202509/python/js
  - service for extracting document structure and content from images using advanced computer vision and vision-language models (VLM). 
  - The system combines YOLO-based document layout segmentation with OpenAI-compatible VLM models to accurately detect, classify, and extract text content from document images, converting them to structured Markdown format
  - Document Layout Segmentation: Uses YOLOv8-based models to detect and classify document elements (text blocks, tables, images, headers, etc.)
  - Vision-Language Model Integration: Leverages OpenAI-compatible VLM models (default: Qwen2.5-VL) for intelligent text extraction
  - CLI Tools: Command-line utilities for batch PDF processing and document analysis
  - Image Processing: Drag-and-drop upload, real-time preview, and bounding box visualization
    - Overlay detected elements on the original image
    - Cropped image extraction for tables and images
  - Core: FastAPI, Uvicorn, Pydantic, Pydantic-settings
  - Computer Vision: Pillow, OpenCV, Ultralytics (YOLO)
  - Document Processing: pdf2image
  - uv run python process_pdf.py -i /Users/yaoo/Documents/01files/testpdf/html5canvas1pages-pic-figure.pdf -o output

- https://github.com/emcf/thepipe /1.5kStar/MIT/202510/python/inactive
  - a package that can scrape clean markdown, multimodal media, and structured data from complex documents.
  - It can extract well-formatted data from a wide range of sources, including PDFs, URLs, Word docs, Powerpoints, Python notebooks, videos, audio, and more.
  - Uses VLM for OCR in text-only mode
  - Accepts a wide range of sources, including PDFs, URLs, Word docs, Powerpoints, Python notebooks, GitHub repos, videos, audio, and more
  - The default install only pulls in CPU-friendly dependencies so it is suitable for constrained environments and CI systems. 
    - GPU-enabled libraries such as PyTorch and Triton are left as optional extras.
  - 👾 By default, thepipe uses the OpenAI API, so VLM features will work out-of-the-box provided you pass in an OpenAI client.
    - If you wish to use a local vision-language model or a different cloud provider, you can provide a custom OpenAI client
  - structured extraction is being deprecated and will be removed in future releases. The current implementation is a simple wrapper around OpenAI's chat API, which is not ideal for structured data extraction. We recommend OpenAI's structured outputs for structured data extraction, or using Trellis AI for automated workflows with structured data.

- https://github.com/katanaml/sparrow /5.1kStar/GPL/202601/python
  - https://sparrow.katanaml.io/
  - Structured data extraction and instruction calling with ML, LLM and Vision LLM
  - Pluggable Architecture: Mix and match different pipelines (Sparrow Parse, Instructor, Agents)
  - Multiple Backends: MLX (Apple Silicon), Ollama, vLLM, Docker, Hugging Face Cloud GPU
  - Multi-format Support: Images (PNG, JPG) and multi-page PDFs
  - API-First Design: RESTful APIs for easy integration
  - Built-in dashboard and agent workflow tracking
  - Local Vision LLMs: Mistral, QwenVL, DeepSeek OCR, etc.
  - Usage Analytics: Track API calls, success rates, performance
  - Real-time Monitoring: Live processing statistics
  - Pipeline Comparison
    - Sparrow Parse: Use for structured data extraction from documents
    - Sparrow Instructor: Use for text analysis, summarization, Q&A
    - Sparrow Agents: Use for complex multi-step document processing workflows
  - 💰 Licensed under GPL 3.0. Free for open source projects and organizations under $5M revenue.

- https://github.com/Tro-fish/ChartEye-all_in_one-figure-VQA /202407/pythoh/js/inactive
  - ChartEye: Multi Modal QA Chatbot for Scientific Figure Images
  - This repository contains the code for ChartEye, including its implementation and execution instructions, for the Figure-to-Caption and QA Chatbot for Chemistry and Materials Science documents.
  - Extract Chart(figure) image from PDF, PPTX, WORD files --> Image Extraction
    - ❓ 似乎不支持图片版pdf
    - PDF: Extracting images with pymupdf
    - WORD: Extracting images with python-docx
    - PPTX: Extracting images with python-pptx
  - Convert Chart(figure) image to text explanation --> Chart Captioning
  - Convert imformation in a Chart(figure) image to a number --> Chart Derendering
  - Answer Question about the information in a Chart(figure) imge --> Question Answering

- https://github.com/lkk688/VisionLangAnnotate /MIT/202511/python/inactive
  - an advanced vision-language annotation framework that enables dynamic object detection and annotation based on natural language prompts.
  - VisionLangAnnotate consists of two main components:
    - Traditional Object Detection Pipeline: Multiple object detection models (DETR, YOLO, RT-DETR)
    - Vision-Language Models (VLM) Backend: llava, Qwen2.5-VL
  - Detect objects based on natural language descriptions
  - Combines traditional object detectors with Vision-Language Models
  - Unified API: Simple interface for various detection and annotation tasks
  - Generate annotations on-the-fly based on user requests
  - Support for both image and video inputs
  - Zero-Shot Capabilities: Detect novel objects without prior training
  - Export detection results to Label Studio compatible JSON format
  - Complete Annotation Loop: End-to-end pipeline from user requests to data pre-processing, object detection, vision annotation, and human validation

- https://github.com/pengyuanli/PDFigCapX /apache2/202411/python/inactive
  - https://www.eecis.udel.edu/~compbio/PDFigCapX
  - For each document in the input_path, the main function will generate a corresponding folder with the same name as the original document in the output_path. All extracted figures (in jpg format), captions (in text format) and their coordinate information (in json format) will be saved in the corresponding folder.
  - PDF parsing using xpdf 

- https://github.com/morkev/vlm-yolo-detector /MIT/202601/python
  - VLM-powered image extraction and semantic search for equipment manuals. This repository provides the image data pipeline for the agentic-rag system.
  - Extract images from PDF documents (embedded images + rendered pages with diagrams)
  - Generate VLM descriptions for each image using LLaVA via Ollama
  - Create semantic embeddings for intelligent image search
  - Integrate with agentic-rag for visual content retrieval
  - PyMuPDF (for PDF processing)
  - sentence-transformers (for embeddings)
  - Pillow (for image processing)
  - Optional Dependencies (for YOLO training): ultralytics, torch, torchvision
  - 🛝 
    - uv sync时 there are no versions of yologen[vlm]
  - https://github.com/ahmetkumass/yolo-gen /MIT/202601/python
    - Train YOLO + VLM with one command. No extra labeling
    - Train object detection and natural language description models from a standard YOLO dataset. VLM training data is auto-generated from YOLO labels.
    - Why YOLO + VLM?
      - YOLO alone: Fast but not enough for production-level accuracy
      - VLM alone: Smart but too slow for production
      - YOLO + VLM: Fast detection + VLM adds detailed descriptions, classification, and false positive filtering

- https://github.com/longhoag/vlm-prototype /MIT/202601/python
  - Simple VLM pipeline prototype for object detection with proprietary model
  - The system processes traffic images, identifies vehicles (cars, motorcycles, mopeds, trucks, buses), and outputs annotated images with green bounding boxes.
  - Images are analyzed via API, vehicle coordinates are extracted, and bounding boxes are rendered on the output images.
  - Opens input images using Pillow (PIL), Draws green (#00FF00) bounding boxes

- https://github.com/getomni-ai/zerox /MIT/202505/python/ts/inactive
  - OCR & Document Extraction using vision models
  - Convert that file into a series of images, Pass each image to GPT and ask nicely for Markdown
  - [Research: Add bounding boxes to response _202407](https://github.com/getomni-ai/zerox/issues/7)
    - I would love to have some bounding boxes come back with the text response. Primarily for highlighting locations in the original document where the text got pulled. Not sure exactly how I would proceed with this one

- https://github.com/landing-ai/vision-agent /5.3kStar/apache2/202508/python/deprecated
  - VisionAgent is the Visual AI pilot from LandingAI. Give it a prompt and an image, and it automatically picks the right vision models and outputs ready‑to‑run code—letting you build vision‑enabled apps in minutes. 
  - The VisionAgent library includes a set of tools, which are standalone models or functions that complete specific tasks. When you prompt VisionAgent, VisionAgent selects one or more of these tools to complete the tasks outlined in your prompt.
  - This tool has been deprecated. Use Agentic Document Extraction instead.
  - https://github.com/landing-ai/ade-python
    - A Python library for interacting with the LandingAI Agentic Document Extraction REST API, designed for flexibility, reliability, clarity, and performance.
# pdf-video
- [PDF to Brainrot | MemenomeLM](https://www.memenome.gg/)
  - 把 PDF 转化为易上瘾的视频
  - 通过 AI 技术将传统的 PDF 学习材料转换为更生动有趣的视频形式, 既保留了学习内容的专业性, 又强调提高效率、改善学习体验和趣味性, 网站显示已经有超过 10w 学生使用
  - 用 AI 改造成交互式学习的过程, 交互视频、AI 和真人交互都可以
  - https://x.com/0xPaulius/status/1852697757124845684
    - Been using this to post automated tiktoks on the latest research papers, its actually getting pretty good traction
# more-pdf
