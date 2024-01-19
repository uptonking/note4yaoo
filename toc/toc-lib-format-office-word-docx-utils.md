---
title: toc-lib-format-office-word-docx-utils
tags: [docx, format, microsoft-word, ooxml]
created: 2022-11-06T15:56:39.587Z
modified: 2023-01-09T11:03:32.533Z
---

# toc-lib-format-office-word-docx-utils

# guide

# popular
- https://github.com/SheetJS/js-word /apache2/202007/js
  - Parser and writer for various word processing doc formats. 
  - Pure-JS cleanroom implementation from official specifications, related documents, and test files

- https://github.com/dolanmiu/docx /MIT/202401/ts
  - Easily generate .docx files with JS/TS with a nice declarative API. 
  - Works for Node and on the Browser.
  - 依赖xml-js、jszip
  - https://github.com/naskio/docx-viewer /MIT/202111/js
    - Live Preview the generated word document (docx) in your browser while using docx

- https://github.com/TrialAndErrorOrg/parsers /GPLv3/202309/ts
  - https://convert.centeroftrialanderror.com/
  - Monorepo for a suite of `unified`-compatible converters for converting between, from, and to .docx, JATS XML, LaTeX, and PDF
  - The goal is to automate the process of converting a manuscript from a word processor to a JATS XML file, which can then be used to generate a PDF and HTML version of the manuscript.

- https://github.com/byoungd/editor-to-word /ts
  - Export HTML to word (.docx) only by browser 

- https://github.com/nod-engineering/docx
  - Easily generate .docx files with JS/TS. 
  - Works for Node and on the Browser.

- https://github.com/open-xml-templating/docxtemplater /MIT/js/excel收费
  - a library to generate docx/pptx documents from a docx/pptx template.
  - Functionality can be added with the following paid modules
# examples

# viewer
- https://github.com/VolodymyrBaydalka/docxjs /apache2/202312/ts
  - https://volodymyrbaydalka.github.io/docxjs/
  - render/convert DOCX document into HTML document with keeping HTML semantic as much as possible
# parser-generator
- https://github.com/Ziv-Barber/officegen /MIT/202103/js
  - Standalone Office Open XML files (Microsoft Office 2007 and later) generator for Word (docx), PowerPoint (pptx) and Excell (xlsx) in javascript. 
  - The output is a stream.
  - officegen should work on any environment that supports Node.js including Linux, OSX and Windows. 
  - officegen also supporting PowerPoint native charts objects with embedded data.
# converter
- https://github.com/mwilliamson/mammoth.js /BSD/202307/js
  - designed to convert .docx documents, such as those created by Microsoft Word, Google Docs and LibreOffice, and convert them to HTML.
  - aims to produce simple and clean HTML by using semantic information in the document, and ignoring other details
  - Mammoth works best if you only use styles to semantically mark up your document.

- https://github.com/privateOmega/html-to-docx /MIT/202303/js
  - converting HTML documents to DOCX format supported by Microsoft Word 2007+, LibreOffice Writer, Google Docs, WPS Writer etc.
  - inspired by html-docx-js project but mitigates the problem of documents generated being non-compatiable with word processors like Google Docs and libreOffice Writer that doesn't support `altchunks` feature.

- https://github.com/evidenceprime/html-docx-js /201605/js
  - small library that is capable of converting HTML documents to DOCX format 

## wasm

- https://github.com/bokuweb/docx-rs
  - A .docx file writer with Rust/WebAssembly.
# extension-superset

# utils
- https://github.com/axa-group/Parsr
  - a minimal-footprint document (image, pdf, docx, eml) cleaning, parsing and extraction toolchain which generates readily available, organized and usable data in JSON, Markdown (MD), CSV/Pandas DF or TXT formats.

- https://github.com/tomashubelbauer/modern-office-git-diff /js
  - It is a pre-commit script which unpacks Office XML into text contents and tracks that alongside the source file. This way you can consider the binary to be a source of truth, but with each commit you also get a textual diff showing what changed content-wise. More or less
  - This is achieved using a PowerShell script which unpacks the ZIP file to a tracked directory, formats the XML files for nice diff and tracks the formatted files as well.

- https://github.com/ForNeVeR/ExtDiff /powershell
  - This is a small command line script that will compare two files using Microsoft Word file comparison tool. 
  - Microsoft Word will be started using COM automation.
# more
