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

- https://github.com/alam00000/bentopdf /14Star/apache2/202510/ts
  - https://bentopdf.com/
  - privacy-first, client-side PDF toolkit that allows you to manipulate, edit, merge, and process PDF files directly in your browser. No server-side processing is required
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
  - [BentoPDF is now open sourced : r/webdev _202510](https://www.reddit.com/r/webdev/comments/1o6lkwf/bentopdf_is_now_open_sourced/)
  - What does it do better / different compared to Stirling pdf?
    - Runs fully client side
    - You can merge pdf with ranges
    - You can crop each pdf page differently
    - You can fill and create form
  - i wonder if you can add "sign" feature using both imported signature or digital signature like in FoxitPDF. 
    - As a Linux user it's very difficult to find a decent application for digital signatures/certificates.

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

- https://github.com/tabulapdf/tabula /js
  - http://tabula.technology/
  - Tabula is a tool for liberating data tables trapped inside PDF files
  - Tabula only works on text-based PDFs, not scanned documents
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
- https://github.com/tradle/pdf-parse /js
  - Pure javascript cross-platform module to extract texts from PDFs.

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

- https://github.com/oomol-lab/pdf-craft /AGPL/202503/python
  - PDF craft can convert PDF files into various other formats. This project will focus on processing PDF files of scanned books. 
  - This project can read PDF pages one by one, and use `DocLayout-YOLO` mixed with an algorithm I wrote to extract the text from the book pages 
  - 超过100页的，可转为EPUB，结合了本地OCR和云端LLM处理，兼顾效率和功能性，最终生成带目录分章节的EPUB

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
# ocr-pdf
- https://github.com/ocrmypdf/OCRmyPDF /22.6kStar/MPLv2/202503/python
  - http://ocrmypdf.readthedocs.io/
  - OCRmyPDF adds an OCR text layer to scanned PDF files, allowing them to be searched or copy-pasted.
  - Generates a searchable PDF/A file from a regular PDF
  - Distributes work across all available CPU cores
  - Uses Tesseract OCR engine to recognize more than 100 languages
  - Battle-tested on millions of PDFs.
- https://github.com/FanQinFred/OCRmyPDF-Desktop /apache2/202312/js/vue/inactive
  - 在OCRmyPDF的基础上，集成了所需环境，并使用Electron开发了桌面端
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
# latex
- https://github.com/dginev/ar5iv /MIT/rust
  - https://ar5iv.org/
  - A web service offering HTML5 articles from arXiv.org as converted with latexml
  - Authors can reproduce locally using ar5ivist.
  - Not a live preview service.
  - Goal: incremental improvement until worthy of native arXiv adoption.
  - View any arXiv article URL by changing the X to a 5

- https://github.com/arxiv-vanity/arxiv-vanity /apache2/python
  - https://www.arxiv-vanity.com/
  - Renders papers from arXiv as responsive web pages so you don't have to squint(眯着眼看) at a PDF.
  - This is the web interface for viewing papers. 
  - The actual LaTeX to HTML conversion (the interesting bit) is done by Engrafo.
  - https://github.com/arxiv-vanity/engrafo
    - Convert LaTeX documents into beautiful responsive web pages using LaTeXML.
# doc-parser-ai-llm
- https://github.com/QuivrHQ/MegaParse /apache2/202408/python
  - https://pypi.org/project/megaparse/
  - a powerful and versatile parser that can handle various types of documents with ease
  - Parse PDFs, Docx, PPTx in a format that is ideal for LLMs
  - Files: ✅ PDF ✅ Powerpoint ✅ Word
  - Content: ✅ Tables ✅ TOC ✅ Headers ✅ Footers ✅ Images
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
