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

- https://printcss.live/
  - 渲染pdf的多种js示例
# popular
- pdf.js /40.9kStar/Apache2/202212/js
  - https://github.com/mozilla/pdf.js
  - https://mozilla.github.io/pdf.js/
  - PDF.js is a Portable Document Format (PDF) viewer that is built with HTML5.
  - Our goal is to create a general-purpose, web standards-based platform for parsing and rendering PDFs.

- jsPDF /25.7kStar/MIT/202202/js/inactive
  - https://github.com/parallax/jsPDF
  - https://parall.ax/products/jspdf
  - A library to generate PDFs in JavaScript.
  - 支持web和node
  - https://github.com/AaronClaes/jspdf-editor
    - https://jspdf-editor.vercel.app/
    - *WIP* Design pdfs and generate code for jspdf

- pdfkit /8.5kStar/MIT/202311/js
  - https://github.com/foliojs/pdfkit
  - http://pdfkit.org/
  - http://pdfkit.org/demo/browser.html
  - A JavaScript PDF generation library for Node and the browser.

- https://github.com/unjs/unpdf /ts
  - Utilities to work with PDFs in Node.js, browser and workers
  - unpdf ships with a serverless build/redistribution of Mozilla's PDF.js for serverless environments. 
  - This library is also intended as a modern alternative to the unmaintained but still popular pdf-parse.

- https://github.com/diegomura/react-pdf
  - React renderer for creating PDF files on the browser and server
  - This package is used to create PDFs using React. 
    - If you wish to display existing PDFs, you may be looking for https://github.com/wojtekmaj/react-pdf
  - https://github.com/enescang/react-pdf-table
    - Simple table generator for @react-pdf/renderer

- https://github.com/wojtekmaj/react-pdf /js
  - Display PDFs in your React app as easily as if they were images.
  - For React-PDF to work,  `PDF.js` worker needs to be provided.

- https://github.com/react-pdf-viewer/react-pdf-viewer /ts
  - https://react-pdf-viewer.dev/
  - React component to view a PDF document

- https://github.com/aexol-studio/react-pdf-editor /ts
  - Pdf editor react component
  - [Refactor 2022](https://github.com/aexol-studio/react-pdf-editor/issues/69)
- https://github.com/snamoah/react-pdf-editor /js
  - PDF Editor built with react
  - This project is a react port of the svelte version here so most of the pdf generation and editing logic was lifted from there.

- https://github.com/neslxzhen/pdf-editor /ts
  - No Server, No Install PDF Editor with React
  - https://github.com/oren-l/PdfEditor /js
  - https://github.com/pgarciacamou/pdf-editor /js

- https://github.com/pdfme/pdfme /MIT/ts
  - https://pdfme.com/
  - A TypeScript based PDF generator library, made with React.

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

- https://github.com/Hopding/pdf-lib /202111/ts/inactive
  - Create and modify PDF documents in any JavaScript environment.
  - Designed to work in any modern JavaScript runtime. Tested in Node, Browser, Deno, and React Native environments.
  - [Is this thing still on?](https://github.com/Hopding/pdf-lib/issues/1423)
  - 🍴 forks
  - https://github.com/cantoo-scribe/pdf-lib
    - This fork adds the support for svg to the pdf-lib project.

- https://gitlab.coko.foundation/pagedjs/pagedjs
  - Paged.js is a free and open-source library that paginates any HTML content to produce beautiful print-ready PDF. 
  - The library fragments the content, reads your CSS print declarations and presents a paginated preview in your browser that you can save as PDF.
# pdf-editor
- https://github.com/luke-browning/pdf-web-edit /ts/c#/ng
  - a web-based application for manipulating PDF files. 
  - It's main purpose is to pre-process documents before they are imported into a Document Management System (DMS) such as Paperless (-ng and -ngx) or stored in a directory based structure.

- https://github.com/jichang/unionpdf /MIT/202401/ts
  - https://jichang.github.io/unionpdf/
  - A universal pdf rendering/editing library
  - model, engine, react

- https://github.com/awesome-yasin/PDF-Verse /MIT/202312/js/ejs
  - https://pdf-verse.vercel.app/
  - a powerful web based PDF Editor with tools fexamplesor editing, converting, and manipulating PDFs.
  - Merge, compress, add or remove pages, or extract text using OCR technology. 

- https://github.com/ShizukuIchi/pdf-editor /202011/js/inactive
  - https://pdf-editor.now.sh/
  - Offline PDF editor. Add images, signatures, text to PDF in your browser

- https://github.com/gr2m/pdf-editor
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

- https://github.com/isneezy/pdf-generator-service /ts
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

- https://github.com/pdsuwwz/puppeteer-server
  - 基于 Puppeteer + Koa + Rollup + TypeScript, 将任意网页快速转换为 PDF, 图像, 支持将多个网页合并生成为一个 PDF 文件，支持 Cookie 的注入、PDF 水印和页眉页脚的插入

- https://github.com/kevalbhatt/puppeteer-pdf-generator /js
  - Internally server starts a headless browser and opens http://localhost:3000 application and creates the pdf (i.e print layout).
  - Note: Server-side pdf generator code is hardcoded so you will get same pdf every time.
# reader/viewer
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

- https://github.com/CMOISDEAD/next-library /js
  - Next Library is an innovative virtual library application that offers a seamless and personalized way to manage your book collection
  - Custom PDF Viewer Tool: Open and view PDF files directly within the virtual library program using a customized PDF viewer tool.

- https://github.com/PSPDFKit/pspdfkit-electron-example /JS
  - PSPDFKit for Electron Example Application

- https://github.com/nikensss/sign_here /js
  - Small electron app to add hand signature image to PDF

- https://github.com/praharshjain/Electron-PDF-Viewer /js
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

- https://github.com/koreader/koreader /lua
  - http://koreader.rocks/
  - An ebook reader application supporting PDF, DjVu, EPUB, FB2 and many more formats, running on Cervantes, Kindle, Kobo, PocketBook and Android devices

- https://github.com/Cimbali/pympress /GPLv2/202312/python
  - https://cimbali.github.io/pympress/
  - Pympress is a simple yet powerful PDF reader designed for dual-screen presentations
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

- https://github.com/FanQinFred/OCRmyPDF-Desktop
  - 在OCRmyPDF的基础上，集成了所需环境，并使用Electron开发了桌面端

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

- https://github.com/pdfarranger/pdfarranger /python
  - Small python-gtk application, which helps the user to merge or split PDF documents and rotate, crop and rearrange their pages using an interactive and intuitive graphical interface.

- https://github.com/hkdb/Densify /python
  - A GTK+ GUI Application written in Python that simplifies compressing PDF files with Ghostscript
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
- databyss /39Star/AGPLv3/202312/js
  - https://github.com/databyss-org/databyss
  - https://databyss.org/
  - Write and cite, research and re-search, and never get lost in Databyss. Welcome to your new word processor.
  - Drag highlighted and/or annotated PDF files into any Page. Databyss will extract all your margin notes and highlighted passages so you can easily edit and search them.
  - 依赖pouchdb

- https://github.com/agentcooper/react-pdf-highlighter /MIT/202307/ts
  - https://agentcooper.github.io/react-pdf-highlighter
  - a React library that provides annotation experience for PDF documents on web.
  - built on top of PDF.js by Mozilla. 
  - Text and rectangular highlights are supported. 
  - Highlight data format is independent of the viewport, making it suitable for saving on the server.
  - `react-pdf` and react-pdfjs only provide React wrappers for PDF.js and do not have built-in annotation functionality.
  - `pdfjs-annotate` does not provide text highlights out of the box.
  - https://github.com/velvetfs/v-pdf-highlighter

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
- https://github.com/andytango/mupdf-js /AGPLv3/202209/ts/c
  - another Webassembly PDF renderer for node and the browser
  - This is a port of MuPDF to javascript and webassembly

- OpenViewerFX  /LGPL/
  - https://github.com/qwertme/OpenViewerFX
  - now part of JDeli
