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

- pdf-editor
  - stirling-pdf
  - open-pdf-studio
  - onlyoffice
  - LibreOffice Draw
  - Inkscape

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
  - This package is used to create PDFs using React. 
  - React renderer for creating PDF files on the browser and server
  - 使用了 pdfkit
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
  - [Highlighting by rectangle bounds and not text _202204](https://github.com/wojtekmaj/react-pdf/discussions/980)
    - I've tried the recipe for highlighting text here. It works fairly well, but it does not work with multiple lines. Lets say I know the bounds of a rectangle on a specified page (or I know multiple bounds), Is there a way to highlight by these bounds instead of matching text?
    - You can use `canvasRef` prop to draw whatever you want on a given canvas. Here's an example with watermark added dynamically
  - https://x.com/xiaohanyu1988/status/1905077853785567258 🆚️
  - https://github.com/allenai/pdf-component-library /apache2/202310/ts
    - https://www.semanticscholar.org/reader/13497bd108d4412d02050e646235f456568cf822
    - built on top of the React-PDF library, with some added components to help with creating an interactive reading experience. 
    - built with research papers in mind, and aims at providing researchers with helpful tools to help their reading experienc
  - https://github.com/allenai/scholar-reader-pdfjs /202009/js/inactive
    - Fork of pdf.js for the Scholar Reader

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

- https://github.com/LibPDF-js/core /1.7kStar/MIT/202603/ts
  - https://libpdf.dev/
  - modern PDF library for TypeScript. Parse, modify, and generate PDFs with a clean, intuitive API
  - LibPDF was born from frustration at `Documenso`.
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
# pdf-apps/tools
- https://github.com/Stirling-Tools/Stirling-PDF /20.4kStar/GPL > MIT/202403/java/js
  - https://www.pdfdrills.com/
  - locally hosted web application that allows you to perform various operations on PDF files
  - locally hosted web based PDF manipulation tool using docker that allows you to perform various operations on PDF files
  - 依赖 Spring Boot + Thymeleaf、pdfbox、itext7、libreoffice转换格式、ocrMyPdf
  - 除了能给PDF打水印之外，还可以轻松批量给扫描的PDF文件瘦身，1秒钟搞定，太好用了
  - [Edit PDF text directly _202404](https://github.com/Stirling-Tools/Stirling-PDF/issues/1141)
    - 202506: We are working on Stirling-PDF V2 at the moment, which will add a ton of improvements and features and we hope will be the backbone towards greater features like edit text. But I cant give any estimates on the edit text feature itself, its a large unknown and we have other things in our backlog along with it. BUT yes it is planned
    - 202512: We now have an initial extremely early alpha version releeased fully Opensource.. One ask for the community is for PDFs that dont render correctly at all (on export) can you please share the font info shown in bottom right of page.
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

- https://github.com/ShashwatSricodes/PDFSlice /MIT/202603/ts/inactive
  - https://www.pdfslice.in/
  - Client Side PDF editor Toolkit
  - 100% client side processing using JavaScript. 
  - 依赖pdf-lib、PDF.js、@hyzyla/pdfcpu
  - [I built Pdfslice - a privacy first open source pdf toolkit : r/foss _202603](https://www.reddit.com/r/foss/comments/1rtsa9l/i_built_pdfslice_a_privacy_first_open_source_pdf/)
    - Stirling-PDF became really gross and bloated to the point of becoming unusable since its v2 launch.
    - There is already PDF24. It too is not FOSS, but freeware, and is can be used as downloadable software that's 100% is running on the computer. 
    - How's is it different from BentoPDF?
      - At this point it's not different.
    - This is a low quality vibe slopped app. How do I know? Look through the code. There are a lot of useEffects that's are used very incorrectly

- https://github.com/OpenAEC-Foundation/open-pdf-studio /LGPL/202604/js/tauri
  - open-source PDF editor and annotator for Windows, macOS, Linux, and Android.
  - lightweight, native desktop application that provides professional-grade PDF annotation, markup, and editing tools without subscriptions, telemetry, or bloatware
  - Built with Tauri 2 and web technologies, it delivers a fast, modern experience with a Microsoft Office-style ribbon interface.
  - 依赖tauri2、solidjs、pdfjs、pdf-lib
  - Text Editing: Edit existing PDF text content inline
  - Page Management
  - Text markup: Highlight, underline, strikethrough
  - Text annotations: Text box, callout with leader line, sticky notes with popup editing
  - Shapes: Rectangle, ellipse, polygon, cloud, cloud polyline, line, arrow, polyline
  - Freehand drawing: Pen tool with configurable color, width, and opacity
  - Stamps: 10 built-in stamps (Approved, Rejected, Draft, Confidential, Final, etc.)
  - Redaction: Mark areas and apply to permanently remove content
  - Export pages as PNG or JPEG 
  - 🛝 
    - 编辑文本时,会编辑一个段落/1行/2行/3行, 实现方式是在图片上叠加文本框，然后修改文本框的文字
    - 点击待编辑的位置时开始, 到渲染出文本框, 会有闪烁感
    - This app does not truly edit existing PDF text. It uses a "cover and replace" approach
    - PDF.js extracts text positions via getTextContent() and renders a transparent DOM text layer for selection
    - When you click on PDF text, a textarea overlay appears for you to type
    - pdf-lib draws a white rectangle over the original text, then draws the new text on top with page.drawText()
    - So the original PDF content stream is untouched — the old text is visually hidden behind a white rectangle.
  - pdfjs-dist   │ Apache-2.0 │ Rendering, text extraction, annotation parsing
  - pdf-lib      │ MIT        │ PDF modification (save, draw text/shapes) 
  - mupdf        │ AGPL-3.0   │ Optional WASM renderer, falls back to PDF.js if mupdf can't load
  - lopdf (Rust) │ MIT        │ PDF parsing in the Rust backend 
  - It includes mupdf as an npm dependency and renderer.js tries MuPDF WASM as an optional rendering path.
    - It has a separate Rust crate open-pdf-render, which is a pure Rust PDF renderer built on
    - But those do not appear to be the main authoritative editing engine for the shipped editor. The main shipped editing flow is still PDF.js + pdf-lib + overlay logic.
  - [Window does not appear on macOS 26 (Tahoe) — app runs but main window stays hidden  _202603](https://github.com/OpenAEC-Foundation/open-pdf-studio/issues/208)
    - The entire rendering and processing pipeline runs on the CPU via Canvas 2D with no GPU acceleration. 
    - All rendering is done via HTML5 Canvas 2D on the main thread. No OffscreenCanvas, ImageBitmap, or requestAnimationFrame batching is used anywhere. 
  - [perf: large PDF performance bottlenecks — rendering, loading & annotation pipeline  _202603](https://github.com/OpenAEC-Foundation/open-pdf-studio/issues/175)
  - 🏘️ [arch: multi-engine rendering architecture for large PDF performance _202603](https://github.com/OpenAEC-Foundation/open-pdf-studio/issues/176)
    - The current architecture pushes everything through a single pipeline: one pdf.js render call → one canvas → annotations on top → done. All on the main thread. This fundamentally doesn't scale for large/complex PDFs.
    - Professional PDF viewers (PDFium, MuPDF, Adobe Acrobat) solve this with a multi-engine architecture. We should adopt a similar approach.
    - Tile-based rendering: Divide each page into tiles (e.g. 512×512px). Only render tiles visible in the viewport
    - Level-of-detail (LOD): Keep a low-res cached version per page for instant display while high-res tiles load
    - Progressive zoom: On zoom change, immediately CSS-scale existing tiles, then re-render at the new zoom level in the background (like Google Maps)
    - Annotation Overlay (independent render cycle)
    - Worker pool (2-4 workers) handles: stamp image extraction, annotation color extraction, CMYK/indexed image decoding, snap/vector geometry parsing, content bounds detection
    - Job queue with priority: visible pages first, nearby pages next, rest later

- https://github.com/anig1scur/tocify /GPL/202604/js
  - https://tocify.aeriszhu.com/
  - Add or edit PDF bookmarks / Table of Contents online - 快速给 PDF 添加目录 / 书签

- https://github.com/kirank55/mydevicemypdf /MIT/202602/ts
  - https://mydevicemypdf.com/
  - Privacy-first PDF utilities that run entirely in your browser. Compress, split, merge, and more — with no uploads, no servers, and no tracking.
  - [MyDeviceMyPdf - local and Open Source alternative to ilovepdf : r/reactjs _202602](https://www.reddit.com/r/reactjs/comments/1rdfrt7/mydevicemypdf_local_and_open_source_alternative/)

- https://github.com/GSiesto/PDFLince /MIT/202603/ts
  - https://pdflince.com/en
  - Compress PDF, merge PDF, split documents, extract pages, and convert PDF to images or images to PDF right in your browser. No uploads, fully private, always free.

- https://github.com/angelojsf/juntaPDF /MIT/202511/python/inactive
  - 100% offline PDF processing. Secure unification, splitting, and conversion to PDF/A2B
  - Unlike cloud-based solutions ( SaaS ), JuntaPDF performs all processing locally
  - features: Merging, Divide/Extract, PDF/A, Audit Trail (Logs)

- https://github.com/ikenai-lab/convert.gg /MIT/202512/python/ts/inactive
  - powerful, privacy-focused desktop application designed to handle your day-to-day file manipulation
  - Whether you're merging PDFs, compressing images, or extracting archives, everything happens securely on your own machine.
  - PDF, image, zip
  - Frontend: Electron, React, Vite, TypeScript, TailwindCSS
  - Backend: Python (PySidecars): Heavy lifting is delegated to specialized Python scripts.
  - [I built an open source desktop alternative to iLovePDF to avoid uploading private files : r/SideProject _202512](https://www.reddit.com/r/SideProject/comments/1pwzhlo/i_built_an_open_source_desktop_alternative_to/)

- ilovepdf
  - [ArmorPDF - Free Browser-Based PDF Tools, 100% Private](https://armorpdf.com/)

- https://github.com/superpilot69/pdf-trad-to-simp-preserve-layout-kit
  - PDF traditional-to-simplified Chinese conversion kit with layout-preserving scripts, Codex skill, and example source/output PDFs.

- https://github.com/mrmn2/PdfDing /1.7kStar/AGPL/202604/python
  - https://www.pdfding.com/
  - a selfhosted PDF manager, viewer and editor offering a seamless user experience on multiple devices.
  - designed be to be minimal, fast, and easy to set up using Docker.
  - The name is a combination of PDF and ding. Ding is the German word for thing. Thus, PdfDing is a thing for your PDFs. Initially inspired by linkding.
  - browser based PDF viewing on multiple devices. Remembers current position - continue where you stopped reading
  - Edit PDFs by adding comments, highlighting and drawings
  - SSO support via OIDC
# pdf-editor
- https://github.com/R0mb0/PDF_web_editor /MIT/202604/js
  - https://r0mb0.github.io/PDF_web_editor/
  - 100% client-side web app to edit PDF files directly in your browser. Built with Vanilla JS, Tailwind, PDF.js, and PDF-lib. 
  - Add, duplicate pages, and edit text seamlessly. 
  - No server uploads required, ensuring total privacy
  - 支持编辑pdf文本, 但底层文字不会消失，效果是重影

- https://github.com/luke-browning/pdf-web-edit /MIT/202309/ts/c#/ng/inactive
  - a web-based application for manipulating PDF files. 
  - It's main purpose is to pre-process documents before they are imported into a Document Management System (DMS) such as Paperless (-ng and -ngx) or stored in a directory based structure.

- https://github.com/jichang/unionpdf /MIT/202502/ts
  - https://jichang.github.io/unionpdf/
  - A universal pdf rendering/editing library
  - model, engine, react

- https://github.com/awesome-yasin/PDF-Verse /MIT/202312/js/ejs/inactive
  - https://pdf-verse.vercel.app/
  - a powerful web based PDF Editor with tools for editing, converting, and manipulating PDFs
  - Merge, compress, add or remove pages, or extract text using OCR technology. 
  - built with Node.js, EJS, Express.js, and `PDF-lib`, and features a user-friendly interface using jQuery and Bootstrap
  - The Edit PDF tool is made using a combination of Bootstrap, PDF.js, Fabric.js, and Prettify.js.
  - 依赖jimp

- https://github.com/nelsonduarte/PDFApps /MIT/202604/python/PySide6
  - PDF editor and manager for Windows, macOS and Linux — fast, offline and subscription-free.
  - 100% offline — your files never leave your computer
  - All-in-one — 13 tools: split, merge, compress, encrypt, OCR, convert, edit and more in a single app
  - OCR	Recognise text in scanned PDFs: Tesseract OCR is required for text recognition
  - Inline visual editor: redact, insert text, image, signature, highlight, notes, forms and edit existing text
  - 依赖PySide6、PyMuPDF、pypdf、pytesseract、python-docx、Pillow
  - 🛝
    - 编辑ux不够自然: 先点击edit切换到编辑模式, 然后点击要编辑的文本出现弹窗，接着在弹窗中修改纯文本,确认后会展示修改diff, 然后再保存为新文件,
    - 🐛 弹窗中的可编辑文本只包含点击那一行, 不是整个段落， 如果粘贴大段文本，也只会显示一行直到超出边界, 不会自动换行
    - 不支持多次编辑, error: save to original must be incremental
  - Bookmarks / TOC — clickable side panel with the PDF outline (chapters, sections)
  - Undo/Redo 

- https://github.com/ShizukuIchi/pdf-editor /1.8kStar/MIT/202403/js/inactive
  - https://pdf-editor.now.sh/
  - Offline PDF editor. Add images, signatures, text to PDF in your browser

- https://github.com/gr2m/pdf-editor /201504/js/inactive/单文件
  - WYSIWYG PDF-Editor, plugin-free, using pdfkit and pdf.js

- https://github.com/xinglie/report-designer
  - https://xinglie.github.io/report-designer/
  - 打印设计、可视化、标签打印、编辑器、设计器、数据分析、报表设计、组件化、表单设计、h5页面、调查问卷、pdf生成、流程图、试卷、SVG、图形元素、物联网、标签纸
  - https://github.com/xinglie/magix5-playground

- https://github.com/BDenizKoca/Tideflow-md-to-pdf /MIT/202511/ts/tuari
  - https://bdenizkoca.studio/projects/tideflow/
  - Turn Markdown into beautiful PDFs with Tideflow instantly - offline, portable desktop app
  - offline-first Markdown → PDF desktop app powered by Typst. 
  - Write on the left, get a beautifully typeset PDF on the right – instantly.
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

- https://github.com/SteveTheKiller/KillerPDF /GPL/202604/csharp
  - https://pdf.killertools.net/
  - PDF editor for Windows. Install or run portable. GPLv3. No account, no subscription
  - High-quality rendering via PDFium (Docnet. Core)
  - Inline text editing with font matching against the original document
  - Save Flattened PDF: rasterizes every page at 150 DPI via PDFium into a fully uneditable document
  - Password-protected PDF support: prompts for password instead of erroring, decrypted copy held in temp for the session
  - Self-installing EXE: Install or Run dialog on first launch, installs per-user to %LOCALAPPDATA% (no UAC), registers as PDF file handler, adds Start Menu shortcut, self-uninstalls cleanly
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
# viewer/reader
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

- https://github.com/docMentis/docmentis-udoc-viewer /MIT-partOpen/202604/ts
  - https://www.docmentis.com/
  - https://www.docmentis.com/viewer/demo
  - 似乎只开源了sdk
  - 功能普通
  - framework-agnostic viewer powered by a built-from-scratch WebAssembly engine for high-fidelity rendering across PDF, DOCX, PPTX, and images.

- https://github.com/stephanrauh/ngx-extended-pdf-viewer /apache2/202604/ts
  - https://pdfviewer.net/
  - A full-blown PDF viewer for Angular 16, 17, and beyond
  - Bringing Mozilla's pdf.js to the Angular world. That's not only the core PDF viewer, but also the UI.

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

- https://github.com/nextcloud/files_pdfviewer /AGPL/202604/js
  - A PDF viewer for Nextcloud， 不能单独使用
  - integrates the PDF.js library into Nextcloud's Viewer. You can view PDF files as well as Adobe Illustrator files (.ai)

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

- https://github.com/rudi-q/leed_pdf_viewer /paid/202604/ts/svelte
  - https://www.leedpdf.com/
  - https://leed.my/   /web
  - Open-source PDF annotation and drawing tool built for privacy. 
  - Sketch and annotate PDFs with natural pen-like precision, drawing tablet support. 
  - SvelteKit + Tauri.
  - The core focus with LeedPDF has been PDF annotations and easy document markup.
  - The web UI leed.my is now open-source and self-hosted
  - This tool runs entirely in your web browser and does not rely on server-side processing. When you import a PDF or any other file, it is handled locally on your device and is not uploaded to any servers.
  - OCR and e-signatures are indeed next on the roadmap. 
  - [8 months later: My free, open-source PDF editor, LeedPDF is finally a full suite (almost). : r/software _202604](https://www.reddit.com/r/software/comments/1seqoud/8_months_later_my_free_opensource_pdf_editor/)
    - The web app is completely free with no ads.
    - It's the desktop app that requires a one-time paid license as it's the only source of sustenance for the entire project.
  - https://github.com/R0GGER/leed-my-selfhost
    - Docker setup to self-host LeedPDF

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
    - A Python library for reading and writing PDF, powered by `QPDF`

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

- https://github.com/MenschMachine/pdfdancer-client-typescript /apache2/202604/ts
  - the official TypeScript SDK for the PDFDancer API, and the same object model is also available for Python and Java.
  - Works in both Node.js and browser environments.
  - Requires Node.js 20+ (or a modern browser) and a PDFDancer API token.
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
# pdf-office-conversion
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
# more-pdf
