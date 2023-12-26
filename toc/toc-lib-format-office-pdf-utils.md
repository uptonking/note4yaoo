---
title: toc-lib-format-office-pdf-utils
tags: [format, pdf, toc]
created: 2022-11-11T10:44:44.054Z
modified: 2022-11-11T10:46:41.519Z
---

# toc-lib-format-office-pdf-utils

# guide

# popular
- https://github.com/Frooodle/Stirling-PDF /GPLv3/202312/java
  - locally hosted web application that allows you to perform various operations on PDF files
  - locally hosted web based PDF manipulation tool using docker that allows you to perform various operations on PDF files
  - 依赖 Spring Boot + Thymeleaf、pdfbox、itext7、libreoffice转换格式、ocrMyPdf
  - [New Browser-based PDF Editor (github link) : selfhosted](https://www.reddit.com/r/selfhosted/comments/10pexhn/new_browserbased_pdf_editor_github_link/)
  - https://twitter.com/dotey/status/1739426777091408207
    - 一个本地的处理 PDF 的工具，界面是 Web UI，可以支持 Docker 部署。
  - https://twitter.com/geekbb/status/1739627252701450251
    - Docker 真是方便，刚刚在 NAS 上弄了一个本地 PDF 工具 ：Stirling PDF，并通过 Cloudflare Tunnels 建立连接方便自己外网访问，再也不用担心 PDF 资料泄漏的问题了

- https://github.com/SimplePDF/simplepdf-embed /MIT/ts
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
- https://github.com/yWorks/svg2pdf.js /MIT/202308/ts
  - A javascript-only SVG to PDF conversion utility that runs in the browser leveraging jsPDF.

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
# utils
- https://github.com/RussCoder/djvujs /js
  - https://djvu.js.org/
  - library for working with .djvu files online without any connection with the server. 
  - DjVu.js Viewer is a widget that allows viewing .djvu files right in the browser
  - .djvu is a computer file format designed primarily to store scanned documents
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
# more
- [PDF to JSON (by PDFLite.co)](https://chrome.google.com/webstore/detail/pdf-to-json-by-pdfliteco/aapoejhdejkncgnbpngckmddecnfjiob)
  - Extract PDF To JSON with 100% privacy for your files and no uploads to Internet, works offline.
