---
title: toc-lib-format-office-pdf-utils
tags: [format, pdf, toc]
created: 2022-11-11T10:44:44.054Z
modified: 2022-11-11T10:46:41.519Z
---

# toc-lib-format-office-pdf-utils

# guide

# popular
- https://github.com/pdf-association/pdf-cos-syntax /apache2/202503/ts
  - VSCode extension for understanding and learning PDF syntax. 
  - This extension will NEVER render PDF pages or provide support like an interactive PDF viewer. There are other VSCode extensions and external applications which do this
  - Implementers with suitable PDF rendering and viewing technologies are encouraged to create their own VSCode extensions to render PDF pages to work along side this extension.
  - PDF COS syntax and content stream operator syntax highlighting
  - Technically all PDF files are binary files and should never be arbitrarily edited in, or saved from, text-based editors such as VSCode as this will break them
    - PDF files use precise byte offsets for locating objects and data, and can contain compressed or encrypted data. 
    - PDFs are NOT UTF-8
  - https://github.com/pdf-association/pdf-differences /apache2/202502
    - The PDF files in this repository are targeted test files highlighting specific issues seen across multiple widely-used implementations.

- https://github.com/alam00000/bentopdf /14Star/apache2 > AGPL/202510/ts/vanillajs
  - https://bentopdf.com/
  - privacy-first, client-side PDF toolkit that allows you to manipulate, edit, merge, and process PDF files directly in your browser. No server-side processing is required
  - 依赖qpdf-wasm、pdfjs、jspdf、pdf-lib、pdfkit、tesseract.js、tiff
  - Merge PDFs	Combine multiple PDF files into one.
  - Split PDFs	Extract specific pages or divide a document into smaller files.
  - Extract Pages	Save a specific range of pages as a new PDF.
  - Organize Pages	Reorder, duplicate, or delete pages with a simple drag-and-drop interface.
  - N-Up PDF	Combine multiple pages onto a single page.
  - BentoPDF was originally built using HTML, CSS, and vanilla JavaScript
    - As the project grew, it was migrated to a modern stack: ts,vite, tailwindcss
    - Some parts of the codebase still use legacy structures from the original implementation
  - thanks
    - PDFLib.js – For enabling powerful client-side PDF manipulation.
    - PDF.js – For the robust PDF rendering engine in the browser.
    - PDFKit – For creating and editing PDFs with ease.
    - EmbedPDF – For seamless PDF embedding in web pages.
    - Cropper.js – For intuitive image cropping functionality.
  - 📡 Roadmap
    - Edit PDF Content: Directly edit text and other content within your PDF.
    - HTML to PDF
    - Markdown to PDF
    - Convert to PDF/A
    - Linearize PDF: Optimize PDFs for fast web viewing.
  - ⚖️ [Change Licence to AGPL v3 _20251025](https://github.com/alam00000/bentopdf/commit/e0a253be83af58325273de309f56589b31d52b92)
  - [BentoPDF is now open sourced : r/webdev _202510](https://www.reddit.com/r/webdev/comments/1o6lkwf/bentopdf_is_now_open_sourced/)
  - What does it do better / different compared to Stirling pdf?
    - Runs fully client side
    - You can merge pdf with ranges
    - You can crop each pdf page differently
    - You can fill and create form
  - i wonder if you can add "sign" feature using both imported signature or digital signature like in FoxitPDF. 
    - As a Linux user it's very difficult to find a decent application for digital signatures/certificates.
  - 🍴 forks
  - https://github.com/GTEC-PUC-Rio/puc-pdf /i18n/AGPL
  - https://github.com/tommyvange/bentopdf /AGPL
  - https://github.com/xiongfh2008/pdf.ToolkitLife
  - https://github.com/Han-Anonymous/bentopdf
  - https://github.com/IT-BAER/bentopdf

- https://github.com/Stirling-Tools/Stirling-PDF /20.4kStar/MIT(core)+GPL/202403/java/js
  - https://www.pdfdrills.com/
  - locally hosted web application that allows you to perform various operations on PDF files
  - locally hosted web based PDF manipulation tool using docker that allows you to perform various operations on PDF files
  - 依赖 Spring Boot + Thymeleaf、pdfbox、itext7、libreoffice转换格式、ocrMyPdf
  - 除了能给PDF打水印之外，还可以轻松批量给扫描的PDF文件瘦身，1秒钟搞定，太好用了
  - [refactor: move modules under app/ directory and update file paths _202507](https://github.com/Stirling-Tools/Stirling-PDF/pull/3938)

- https://github.com/mrmn2/PdfDing /1.4kStar/AGPL/202511/python
  - https://www.pdfding.com/
  - a selfhosted PDF manager, viewer and editor offering a seamless user experience on multiple devices.
  - designed be to be minimal, fast, and easy to set up using Docker.
  - The name is a combination of PDF and ding. Ding is the German word for thing. Thus, PdfDing is a thing for your PDFs. Initially inspired by linkding.
  - browser based PDF viewing on multiple devices. Remembers current position - continue where you stopped reading
  - Edit PDFs by adding comments, highlighting and drawings
  - SSO support via OIDC

- https://github.com/SimplePDF/simplepdf-embed /280Star/NonOpen/202502/ts
  - https://simplepdf.eu/embed
  - PDF editor in the browser – add text, checkboxes, pictures, signatures to PDF files. 
  - Merge, rotate PDF pages – iframe, script and React component
  - Client-based: the document and data filled in does not leave the browser
  - The library is a simple wrapper around an Iframe that loads SimplePDF on-demand (whenever the user clicks the wrapped link), as such the footprint for this "opening an Iframe" mechanism is very tiny
  - As for the editor itself, it's not open-source
    - The generation part is done using **PDF-lib**
  - [I made a free PDF editor that works in your browser](https://www.reddit.com/r/InternetIsBeautiful/comments/zxdz3e/i_made_a_free_pdf_editor_that_works_in_your/)
    - The PDF editor is completely free and does not require an account to be used.
    - I want to keep it for free for individuals, but there's a paid service for companies
    - I am resting on the shoulders of giants: I used every possible help (read open source work from others) and combined them into the result you're able to use. So I haven't luckily had to spend a lot of time dealing with the complexity of PDFs.

- https://github.com/tabulapdf/tabula /MIT/201802/js/inactive
  - http://tabula.technology/
  - Tabula is a tool for liberating data tables trapped inside PDF files
  - Tabula only works on text-based PDFs, not scanned documents
  - Tabula allows you to extract that data in CSV format, through a simple web interface.
# examples
- https://github.com/xitanggg/open-resume /AGPLv3/202308/ts
  - https://open-resume.com/
  - powerful open-source resume builder and resume parser
  - 依赖@react-pdf/renderer、pdfjs、@reduxjs/toolkit

## viewer

- https://github.com/rwv/lookscanned.io /ts/vue
  - https://lookscanned.io/
  - a pure frontend site that makes your PDFs look scanned
  - 预览效果是图片
  - Based on WebAssembly, No waiting for your PDF to be scanned. Just click the button and your PDF will be scanned in a second
  - offline-capable. It works even if you don't have a network connection.
  - Tweak the settings to make your PDF look better. See the preview in real time.
# parser-generator
- https://github.com/py-pdf/pypdf /9.6kStar/BSD/202511/python
  - https://pypdf.readthedocs.io/en/latest/
  - A pure-python PDF library capable of splitting, merging, cropping, and transforming the pages of PDF files
  - It can also add custom data, viewing options, and passwords to PDF files. 
  - pypdf can retrieve text and metadata from PDFs as well.
  - [How pypdf parses PDF files ](https://pypdf.readthedocs.io/en/latest/dev/pypdf-parsing.html)
    - Finding and reading the cross-reference tables / trailer: The cross-reference table (xref table) is a table of byte offsets that indicate the locations of objects within the file
    - After locating the xref table and the trailer, pypdf proceeds to parse the objects in the PDF. 
    - Decoding content streams: The content of a PDF is typically stored in content streams, which are sequences of PDF operators and operands. 
  - [Reading the PDF metadata on large files _202507](https://github.com/py-pdf/pypdf/discussions/3390)
    - Is there a way to get the PDF attributes like Creation Date without loading the whole file into memory? We have large multi-gigabyte files and are trying to process them on a fleet of smaller ECS instances. The streaming features of pypdf have been great, but would love to get the same metadata without loading the whole file into memory.
    - Have you tried to pass a buffered file stream as stream argument ?
  - [Implementation of get_contents ](https://github.com/py-pdf/pypdf/discussions/3352)
    - `get_data()` is accessing the (decoded) byte data of the corresponding content stream, thus this only relevant when reading from the original PDF file.
    - skimming through the usages of self.pdf in ContentStream seems to indicate that this is used to avoid cloning if the content streams are both targeting the same PDF reference

- https://github.com/chromium/pdfium /apache2/202509/cpp/chromium
  - https://pdfium.googlesource.com/pdfium/
  - https://pdfium.googlesource.com/pdfium/+/HEAD/docs/getting-started.md
  - The PDF library used by the Chromium project
  - PDFium uses the same build tooling as Chromium. PDFium is located in` third_party/pdfium` in Chromium's source code.
  - PDFium uses GN to generate the build files and Ninja to execute the build files.
  - PDFium may be built either with or without JavaScript support, and with or without XFA forms support. Both of these features are enabled by default.
  - By default, the entire project builds with C++20.
  - https://github.com/bblanchon/pdfium-binaries /MIT
    - Binary distribution of PDFium
  - https://github.com/embedpdf/embed-pdf-viewer /MIT/202511/ts
    - [PDF viewer using PDFium + WebAssembly — would love your input : r/opensource](https://www.reddit.com/r/opensource/comments/1kydm90/pdf_viewer_using_pdfium_webassembly_would_love/)
    - open source PDF viewer called EmbedPDF, based on PDFium (the same rendering engine used in Chrome) compiled to WebAssembly.
    - It’s meant to be an alternative to PDF.js, with a focus on rendering accuracy and customizability. You can use it with a full UI out of the box, or headless for full control.
    - It’s MIT-licensed and framework-agnostic.

- https://github.com/tradle/pdf-parse /js
  - Pure javascript cross-platform module to extract texts from PDFs.

- https://github.com/mehmet-kozan/pdf-parse /109Star/apache2/202512/ts
  - https://mehmet-kozan.github.io/pdf-parse/
  - Pure TypeScript, cross-platform module for extracting text, images, and tabular data from PDFs. 
  - Run directly in your browser or in Node.js
  - Can be integrated with React, Vue, Angular, or any other web framework.
  - Supports: Next.js + Vercel, Netlify, AWS Lambda, Cloudflare Workers.
  - [Not able to parse PDFs created with https://github.com/itext · Issue _202511](https://github.com/mehmet-kozan/pdf-parse/issues/50)
    - Capture a screenshot for each page using getScreenshot(), then pass the buffer to Tesseract.js.
  - https://github.com/dryor/translate-app /MIT/202409/ts/inactive
    - Translate App using TypeScript, Tailwind CSS, NextJS, Bun, shadcn/ui, AI-SDK/OpenAI, Zod, Vercel Analytics, pdf-parse.

- https://github.com/esbenp/pdf-bot /js
  - A Node queue API for generating PDFs using headless Chrome. 
  - Comes with a CLI, S3 storage and webhooks for notifying subscribers about generated PDFs

- https://github.com/jbaiter/pdiiif /ts/svelte
  - https://pdiiif.jbaiter.de/
  - a JavaScript library to create PDFs from IIIF Manifests, completely client-side (with server-based fallback for unsupported browsers)
  -  PDF Page for every single-image Canvas in a Manifest

- https://github.com/HarvestProfit/DocFlux /202009/js
  - https://harvestprofit.github.io/DocFlux/
  - Flux/React framework for creating any document, just define a few DOM components to transform into the document.
  - You will define a few document metadata options and specify which component it will render. 
  - 实现了react style Component class, 不依赖react
  - https://github.com/HarvestProfit/DocFlux-Spreadsheets
    - XLSX Spreadsheets parser for DocFlux
  - https://github.com/humphreyja/sample-doc-flux-spreadsheets
    - https://humphreyja.github.io/sample-doc-flux-spreadsheets/
    - Example of using DocFlux to generate spreadsheets with xlsx lib
  - https://github.com/HarvestProfit/DocFlux-PDFs
    - Allows you to create pdfMake pdfs using DocFlux.
    - 依赖pdfmake
# extension-superset

# converters

- https://github.com/yWorks/svg2pdf.js /MIT/202503/ts
  - https://raw.githack.com/yWorks/svg2pdf.js/master/
  - A javascript-only SVG to PDF conversion utility that runs in the browser leveraging jsPDF.
  - Since version 2.x, this repository no longer depends on a forked jsPDF but can be used with original MrRio/jsPDF.

- https://github.com/VikParuchuri/marker /GPLv3/202312/python
  - converts PDF, EPUB, and MOBI to markdown. 
  - 依赖PyMuPDF/GPL、Nougat/cc、LayoutLMv3/cc
  - It's 10x faster than nougat, more accurate on most documents, and has low hallucination risk.
  - Converts most equations to latex
  - Due to the licensing of the underlying models like layoutlmv3 and nougat, this is only suitable for noncommercial usage.

- https://github.com/pdf2htmlEX/pdf2htmlEX /GPLv3
  - https://pdf2htmlex.github.io/pdf2htmlEX/
  - Convert PDF to HTML without losing text or format.
  - This is my branch of pdf2htmlEX 
  - Rewritten handling of obscured/partially obscured text - now much more accurate
  - Some support for transparent text
  - Supporting links, outlines (bookmarks), printing, SVG background, Type 3 fonts and more...
  - 利用的Chrome Headless，让Chrome渲染PDF，再导出成HTML，甚至图片都转成了 base64 字符，所以一个网页就可以包含完整的文本、字体和图片等内容

- https://github.com/PDFTron/web-to-pdf
  - Convert any web technology to PDF (HTML to PDF, html2pdf)
  - 依赖chokidar、live-server、passport、puppeteer、react
  - Please note that React components are not required for web-to-pdf to work. It supports all frameworks, and even vanilla JS/HTML/CSS.

- https://github.com/ArtifexSoftware/pdf2docx /3.2kStar/AGPL/202409/python/mupdf/inactive
  - Extract data from PDF with `PyMuPDF`, e.g. text, images and drawings
  - Generate docx with python-docx
  - https://github.com/sw3do/pdf-to-docx
    - Built with PyPDF2 for PDF reading
    - Built with python-docx for DOCX generation
  -  https://github.com/python-fan/pdf2word /202407/python/inactive
    - 60行代码实现多线程PDF转Word
    - 基于pdf2docx实现
  - https://github.com/fhaelmarinho/PDFtoDOCX
- https://github.com/LianjiaTech/bella-domify /GPL/202511/python
  - 一个贝壳开源的文档解析Python库。使用Python lib包形式引入，也可以服务化方式运行，支持多种文档格式的解析和转换。
  - Markdown转换：将解析结果转换为Markdown格式
  - 基于 pdf2docx 进行二次开发，基于 PyMuPDF 提取文本、图片、矢量等原始数据。并基于规则解析章节、段落、表格、图片、文本等布局及样式
  - https://github.com/LianjiaTech/bella-rag /MIT/202512/python
    - 基于llama-index框架的 RAG 最佳实践，通过业界领先的PDF结构化文档解析能力、混合检索、small2big、Contextual rag等策略实现了高精度的传统rag模式问答效果
  - https://github.com/LianjiaTech/bella-knowledge /MIT/202512/java/ts
    - Bella 体系内的知识管理中心，提供文件、数据集在内多类数据源的统一存储、管理能力
    - 系统完全对标 OpenAI File API，在标准化接口的基础上，扩展了企业级的数据管理和知识处理功能

- https://github.com/tmzncty/dots_ocr_suite /202512/python/js
  - 基于 DotsOCR 库开发的 OCR（光学字符识别）处理工具箱，包含 PDF 转 Word (DOCX) 的完整应用
  - 将 PDF 文档或图片转换为可编辑的 Word 文档或 Markdown 格式，支持复杂的版面分析（如表格、公式、图片等）。
  - 批量转换：在“批量处理”标签页，您可以一次性拖入多个 PDF 文件。

- https://github.com/rubensbraz/LogicPaper /CC-NC/202512/python
  - https://rubensbraz.github.io/LogicPaper/
  - LogicPaper is a high-performance document generation engine designed to automate complex reporting and contract workflows. 
  - It merges structured data (Excel/JSON) with Microsoft Office templates (.docx, .pptx) or text-based files (.md, .txt) using an advanced Jinja2-based strategy system.
  - Asynchronous Batch Processing: Handles large datasets via background workers to prevent request timeouts.
  - State Persistence: Job tracking and session management powered by Redis.
  - Multi-Format Support: Native rendering for Word, PowerPoint, Markdown, and Plain Text.
  - PDF Engine: Integrated LibreOffice for high-fidelity conversion of Office documents to PDF.

- https://github.com/NativeDocuments/docx-wasm-client-side /201902/js/inactive
  - doc/docx to PDF conversion, client-side in-browser, using docx-wasm

- https://github.com/Quorafind/typst-toolbox /apache2/202512/ts/obsidian
  - Convert Markdown to Typst and then to DOCX/PDF. Supports real-time preview and editing.

- https://github.com/Prosperis/Resumier /apache2/202512/ts
  - https://resumier.vercel.app/
  - https://prosperis.github.io/Resumier/
  - Modern resume/CV builder with themes, block editing, and PDF/DOCX export
  - A modern, feature-rich resume builder application built with React, TypeScript, and TanStack Router.
  - 依赖tanstack-router, zustand, jspdf, docx
  - https://github.com/thomascrha/resume
    - Anyone's personal resume pipeline; edit one markdown file and produce a release with a PDF and docx and publish the resulting HTML 
  - https://github.com/hadishah123/resume-analyzer-ai
    - Backend (FastAPI + NLP) A backend service that analyzes resumes and matches them with job descriptions using AI

- https://github.com/adityadomle/ResearchX /202512/ts
  - ResearchX is an AI-powered research document generator built with Next.js and TypeScript. 
  - It uses modern UI (Tailwind + shadcn UI) and integrates AI (Gemini-style) to create complete research papers from customizable outlines, with export support to DOCX or PDF.

- https://github.com/LeanerCloud/invoicr /MIT/202512/ts
  - Tool that generates DOCX and PDF invoices from JSON configuration files
  - Desktop GUI application (Tauri/React)
  - LibreOffice (for PDF conversion)

- https://github.com/pekrau/writethatbook /MIT/202512/python
  - Web app for writing books using Markdown files allowing references and indexing, creating DOCX or PDF.

- https://github.com/beladevo/libreoffice-docx-to-pdf /python
  - Converting docx files to pdf using libreoffice engine, flask and docker

- https://github.com/TrialAndErrorOrg/parsers /GPL/202512/ts
  - https://convert.centeroftrialanderror.com/
  - Monorepo for a suite of `unified`-compatible converters for converting between, from, and to .docx, JATS XML, LaTeX, and PDF
  - Monorepo for a suite of parsers used in the Journal of Trial and Error.
  - The goal is to automate the process of converting a manuscript from a word processor to a JATS XML file, which can then be used to generate a PDF and HTML version of the manuscript

- https://github.com/cherfia/chromiumly /ts
  - A lightweight Typescript library that interacts with Gotenberg's different modules to convert a variety of document formats to PDF files.

- https://github.com/ChipiKaf/html-to-document /ISC/202512/ts
  - https://html-to-document.vercel.app/
  - A modular, open source library for converting HTML content into professional document formats. Initially focused on HTML-to-DOCX conversion, with planned support for PDF and XLSX.
  - it features a core HTML parsing engine and separate format-specific modules, offering a unified API for seamless integration

- https://github.com/tumbati/bukajs /MIT/202512/ts
  - A document viewer library supporting PDF, DOCX, Images, XLSX, and PowerPoint files.
  - Framework Agnostic: Works with React, Vue, Angular, or vanilla JS
  - Advanced Image Editing: Professional-grade cropping, filtering, and aspect ratio controls
  - Annotations: Highlights, notes, drawings with import/export
  - Performance: Canvas rendering with text layer for PDFs
  - Caching: Optional offline caching with LocalForage

- https://github.com/Belval/pdf2image /1.9kStar/MIT/202401/python/inactive
  - A python (3.7+) module that wraps pdftoppm and pdftocairo to convert PDF to a PIL Image object
  - Windows users will have to build or download `poppler` for Windows
  - [Is there a way to skip disk r/w operations, and we can directly use the image object without saving it on disk _201903](https://github.com/Belval/pdf2image/issues/58)
    - The most optimized workflow I can think of would be to use `tesserocr` with pdf2image without and output_folder or with a ramdisk.
    - Tesserocr is a Python/Pillow friendly library that uses libtesseract.
  - [Licensing _202002](https://github.com/Belval/pdf2image/issues/124)
    - you're using MIT license while poppler is under GPL license. Could you please dispel my doubts?
      - Poppler is distributed under a copyleft license, namely GPL 2.0. If in your commercial application you modify Poppler and/or do static/dynamic linking on Poppler, you can be infringing(违反/侵犯) on their license by not releasing your source code.
      - That being said, it is by design that pdf2image does not in any way or form, link directly to poppler. All it does is call an already existing CLI utility that comes pre-installed on most Linux installation. As such, my code is distributed under MIT 
    - I'm reopening this since it's not clear to me if running pdf2image inside a docker container can still be considered as MIT compatible ?
      - TLDR: The container is not considered anything as it is not code, but GPL code can "live" with MIT code in a container without any issue.

- https://github.com/Gary-zy/imageConversion /202601/ts/vue
  - https://gary-zy.github.io/imageConversion/
  - 免费在线图片格式转换工具，支持多种图片格式互转、OFD文档处理。
  - 所有转换在浏览器本地完成，保护隐私，无需上传服务器。
  - 图片处理	Canvas API、Pica（高质量缩放）
  - PDF 生成	jsPDF
  - OFD 解析	ofd.js（自定义实现）
  - 国密算法	sm-crypto（SM2/SM3/SM4）、jsrsasign
  - 文件处理	JSZip、file-saver
# utils
- https://github.com/RussCoder/djvujs /js
  - https://djvu.js.org/
  - library for working with .djvu files online without any connection with the server. 
  - DjVu.js Viewer is a widget that allows viewing .djvu files right in the browser
  - .djvu is a computer file format designed primarily to store scanned documents

- https://github.com/typst/pdf-writer /MIT/202402/rust
  - A step-by-step PDF writer.

- https://github.com/wuxue107/bookjs-eazy /MIT/202310/js/inactive
  - HTML自动分页插件。用于生成PDF, 前端WEB打印生成PDF或后端wkhtmltopdf、chrome headless生成
  - 主要解决，HTML生成PDF，分页可控的问题
  - 依赖 jquery、lodash、bookjs-eazy

- https://github.com/lukaszliniewicz/PyCropPDF /MIT/202511/python
  - A GUI application to crop PDF files. It is primarily designed for documents where multiple pages need the same cropping, such as removing headers, footers, or margins.

- https://github.com/Drakonis96/notypdf /GPL/202507/ts
  - NotyPDF helps you read pdf, extract and save quotes (or their translation) from PDF documents to your Notion database
  - A built-in document manager keeps everything organized while backups ensure your configuration is safe.

- https://github.com/vslavik/diff-pdf /4.1kStar/GPL/202409/cpp/inactive
  - http://vslavik.github.io/diff-pdf
  - A simple tool for visually comparing two PDF files
  - produces a PDF file with visually highlighted differences:
    - pdf上显示红绿色文字表示2个pdf的差异, 以浮层文字显示，视觉效果类似重影
# latex
- https://github.com/dginev/ar5iv /MIT/rust
  - https://ar5iv.org/
  - A web service offering HTML5 articles from arXiv.org as converted with latexml
  - Authors can reproduce locally using ar5ivist.
  - Not a live preview service.
  - Goal: incremental improvement until worthy of native arXiv adoption.
  - View any arXiv article URL by changing the X to a 5

- https://github.com/arxiv-vanity/arxiv-vanity /1.6kStar/apache2/202201/python/inactive
  - https://www.arxiv-vanity.com/
  - Renders papers from arXiv as responsive web pages so you don't have to squint(眯着眼看) at a PDF.
  - This is the web interface for viewing papers. 
  - The actual LaTeX to HTML conversion (the interesting bit) is done by Engrafo.
  - https://github.com/arxiv-vanity/engrafo
    - Convert LaTeX documents into beautiful responsive web pages using LaTeXML.
# pdf-datasets
- https://huggingface.co/datasets/HuggingFaceFW/finepdfs
  - https://github.com/huggingface/finepdfs /AGPL
  - FinePDFs is the largest publicly available corpus(资料，文集，语料库) sourced exclusively from PDFs, containing about 3 trillion tokens across 475 million documents in 1733 languages.
  - The data was sourced from 105 CommonCrawl snapshots, spanning the summer of 2013 to February 2025
  - the dataset is fully reproducible and released under the ODC-By 1.0 license
  - https://huggingface.co/datasets/HuggingFaceFW/finepdfs-edu
    - FinePDFs-Edu dataset consists of 350B+ tokens of educational PDFs filtered from FinePDFs dataset covering 69 languages.
    - FinePDFs was created using the formula inspired from FineWeb-Edu
    - we developed an educational quality classifier using annotations generated by Qwen3-235B-A22B-Instruct-2507 to retain only the most educational web pages. 
# more
- [PDF to JSON (by PDFLite.co)](https://chrome.google.com/webstore/detail/pdf-to-json-by-pdfliteco/aapoejhdejkncgnbpngckmddecnfjiob)
  - Extract PDF To JSON with 100% privacy for your files and no uploads to Internet, works offline.
