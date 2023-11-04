---
title: toc-lib-format-office-pdf-utils
tags: [format, pdf, toc]
created: 2022-11-11T10:44:44.054Z
modified: 2022-11-11T10:46:41.519Z
---

# toc-lib-format-office-pdf-utils

# guide

# popular
- https://github.com/Frooodle/Stirling-PDF /GPLv3/java
  - locally hosted web application that allows you to perform various operations on PDF files
  - locally hosted web based PDF manipulation tool using docker that allows you to perform various operations on PDF files
  - 依赖 Spring Boot + Thymeleaf、pdfbox、itext7、libreoffice转换格式、ocrMyPdf
  - [New Browser-based PDF Editor (github link) : selfhosted](https://www.reddit.com/r/selfhosted/comments/10pexhn/new_browserbased_pdf_editor_github_link/)

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

## viewer

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
# extension-superset

# converters
- https://github.com/yWorks/svg2pdf.js /MIT/202308/ts
  - A javascript-only SVG to PDF conversion utility that runs in the browser leveraging jsPDF.

- https://github.com/pdf2htmlEX/pdf2htmlEX /GPLv3
  - https://pdf2htmlex.github.io/pdf2htmlEX/
  - Convert PDF to HTML without losing text or format.
  - This is my branch of pdf2htmlEX 
  - Rewritten handling of obscured/partially obscured text - now much more accurate
  - Some support for transparent text
  - Supporting links, outlines (bookmarks), printing, SVG background, Type 3 fonts and more...
  - 利用的Chrome Headless，让Chrome渲染PDF，再导出成HTML，甚至图片都转成了 base64 字符，所以一个网页就可以包含完整的文本、字体和图片等内容
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
