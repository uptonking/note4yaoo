---
title: toc-lib-format-read-ebook
tags: [ebook, format, reading, toc]
created: 2022-11-06T15:48:58.293Z
modified: 2023-09-19T07:26:04.103Z
---

# toc-lib-format-read-ebook

# guide

# popular
- https://github.com/GitbookIO/gitbook /25.8kStar/apache2/201610/js/inactive
  - https://www.gitbook.com/
  - Modern documentation format and toolchain using Git and Markdown
  - As the efforts of the GitBook team are focused on the GitBook.com platform, the CLI is no longer under active development.
- https://github.com/honkit/honkit /2.7kStar/apache2/202308/ts/gitbook
  - building beautiful books using Markdown - Fork of GitBook(legacy)
  - honkit is a command line tool (and Node.js lib) for building beautiful books using GitHub/Git and Markdown (or AsciiDoc).
  - 依赖immutable3.8、nunjucks、chokidar、commander、i18n-t、htmlparser2
  - GitBook is only free for open-source and non-profit teams.
  - [HonKit: A Fork of GitBook | Hacker News_202006](https://news.ycombinator.com/item?id=23659451)

- https://github.com/executablebooks/jupyter-book /3.6kStar/BSD/202312/python
  - http://jupyterbook.org/
  - open-source tool for building publication-quality books and documents from computational material.

- https://github.com/rstudio/bookdown /3.5kStar/GPLv3/202308/js/rlang
  - https://pkgs.rstudio.com/bookdown/
  - Authoring Books and Technical Documents with R Markdown

- https://github.com/lufengd3/htmlbook2pdf /202311/js
  - Generate PDF on Playwright Playground
  - [Show HN: Generate pdf with gitbook or mdbook url | Hacker News_202311](https://news.ycombinator.com/item?id=38230453)

- https://github.com/nota-lang/bene /202401/ts/rust/tauri
  - https://nota-lang.github.io/bene/
  - Bene is a reading system for documents written in the EPUB file format.
# mdbook
- https://github.com/rust-lang/mdBook /15.6kStar/MPLv2/202312/rust
  - https://rust-lang.github.io/mdBook/
  - Create book from markdown files. 
  - Like Gitbook but implemented in Rust
  - mdBook is a utility to create modern online books from Markdown files.
  - [MdBook – A command line tool to create books with Markdown | Hacker News_202306](https://news.ycombinator.com/item?id=36528984)

- https://github.com/Michael-F-Bryan/mdbook-epub /293Star/MPLv2/202311/rust
  - https://michael-f-bryan.github.io/mdbook-epub/
  - An experimental mdbook backend for creating EPUB documents.

- https://github.com/HollowMan6/mdbook-pdf /GPLv3/202312/rust/python
  - 用 Rust 编写的 mdBook 后端，基于headless chrome和Chrome开发工具协议生成PDF

- https://github.com/fastn-stack/fastn /BSD/202312/rust
  - https://fastn.com/
  - ftd is a programming language for building user interfaces and content centric websites.
  - fastn is a web-framework, a content management system, and an integrated development environment for ftd.

## preprocessor

- https://github.com/badboy/mdbook-toc /MPLv2/202312/rust
  - A preprocessor for mdbook to add inline Table of Contents support.

- https://github.com/badboy/mdbook-mermaid /MPLv2/202312/rust
  - A preprocessor for mdbook to add mermaid support

- https://github.com/lzanini/mdbook-katex /MIT/202311/rust
  - A preprocessor for mdBook, rendering LaTex equations to HTML at build time.
# examples

# parser-generator

# extension-superset

# ebook
- https://github.com/kovidgoyal/calibre /python
  - https://calibre-ebook.com/
  - an e-book manager. It can view, convert, edit and catalog e-books in all of the major e-book formats. 
- https://github.com/janeczku/calibre-web /GPLv3/202401/python/js
  - a web app that offers a clean and intuitive interface for browsing, reading, and downloading eBooks using a valid Calibre database
  - This software is a fork of calibreserver

- https://github.com/standardebooks/tools /python
  - https://standardebooks.org/
  - A collection of tools Standard Ebooks uses to produce its ebooks, including basic setup of ebooks, text processing, and build tools.

- koodo-reader /12kStar/AGPLv3/202401/ts
  - https://github.com/koodo-reader/koodo-reader
  - https://github.com/troyeguo/koodo-reader /renamed
  - https://koodo.960960.xyz/
  - A modern ebook manager and reader with sync and backup capacities for Windows, macOS, Linux and Web
  - 依赖electron-store、fs-extra、howler、react-hot-toast、webdav、marked、jszip
  - Save your data to Dropbox or Webdav
  - Single-column, two-column, or continuous scrolling layouts
  - Add bookmarks, notes, highlights to your books
  - [希望能够有编辑功能_202401](https://github.com/koodo-reader/koodo-reader/issues/1037)
    - 个人认为作为一个阅读器，编辑功能有点冗余，如果需要编辑可以用对应的各种强大产品

- https://github.com/edrlab/thorium-reader /1.4kStar/BSD/202402/ts
  - https://www.edrlab.org/software/thorium-reader/
  - A cross platform desktop reading app, based on the Readium Desktop toolkit
  - an easy to use EPUB reading application for Windows 10/10S, MacOS and Linux. 
  - 依赖redux、saga、electron

- https://github.com/koreader/koreader /AGPLv3/lua
  - http://koreader.rocks/
  - An ebook reader application supporting PDF, DjVu, EPUB, FB2 and many more formats, running on Cervantes, Kindle, Kobo, PocketBook and Android devices
  - https://github.com/koreader/koreader-sync-server
    - koreader is meant for kindle devices. It looks awful on Android.

- https://github.com/BookStackApp/BookStack /php
  - https://www.bookstackapp.com/
  - A platform to create documentation/wiki content built with PHP & Laravel

## epub

- https://github.com/futurepress/epub.js /bsd/202305/js
  - a JavaScript library for rendering ePub documents in the browser, across many devices.
  - provides an interface for common ebook functions (such as rendering, persistence and pagination) without the need to develop a dedicated application or plugin
  - https://github.com/futurepress/epubjs-reader /MIT/201805/js
    - https://futurepress.github.io/epubjs-reader/
    - You can change the ePub it opens by passing a link to bookPath in the url: ?bookPath=https://s3.amazonaws.com/epubjs/books/alice.epub
  - https://github.com/futurepress/epubjs-rn /201912/js

- https://github.com/Sigil-Ebook/Sigil /GPLv3/cpp
  - http://sigil-ebook.com/
  - open source, multi-platform ebook editor that uses Qt (and QtWebEngine). 
  - designed to edit books in ePub format (both ePub 2 and ePub 3).
  - [just to know why wysiwyg doesn't exist anymore](https://github.com/Sigil-Ebook/Sigil/issues/589)
    - welcome to use PageEdit Or any older version of Sigil that suits your needs. 
    - As to why it was removed ... WYSIWYG editing is live HTML (not XHTML) editing internal to the browser engine
    - It can and often does generate code that appears to work but is NOT valid xhtml required by epub and will not pass flightcrew
    - The illegal xhtml code generated by the old BookView was a constant source of pain that consumed much energy and took away from Sigil development itself.
  - https://github.com/Sigil-Ebook/PageEdit /cpp
    - An ePub visual XHTML editor based on Sigil's Deprecated BookView. 
    - It uses WebEngine instead of WebKit
    - PageEdit was originally designed as a replacement for the Book View feature found in older Sigil versions. However, it can also be used as a general purpose visual XHTML editor.
    - PageEdit is based on Sigil
# utils
- https://github.com/mindoc-org/mindoc /6.7kStar/apache2/202308/go
  - 基于beego框架的接口在线文档管理系统, 针对IT团队开发的简单好用的文档管理系统
  - 前身是 SmartWiki 文档系统。SmartWiki 是基于 PHP 框架 laravel 开发的一款文档管理系统。因 PHP 的部署对普通用户来说太复杂，所以改用 Golang 开发。可以方便用户部署和实用
  - 其功能和界面源于 kancloud
  - https://github.com/TruthHun/BookStack
    - 基于MinDoc，使用Beego开发的在线文档管理系统，功能类似Gitbook和看云

- https://github.com/michaelrsweet/htmldoc /cpp
  - https://www.msweet.org/htmldoc
  - HTMLDOC is a program that reads HTML and Markdown source files or web pages and generates corresponding EPUB, HTML, PostScript, or PDF files with an optional table of contents.
  - HTMLDOC was developed in the 1990's as a documentation generator 
  - However, it does not support many things in "the modern web", such as: css/table/form/emoji/encryption

- https://github.com/apache/xmlgraphics-fop /java
  - https://xmlgraphics.apache.org/fop/
  - FOP (Formatting Objects Processor) is a print formatter driven by XSL formatting objects (XSL-FO) and an output independent formatter. 
  - It is a Java application that reads a formatting object (FO) tree and renders the resulting pages to a specified output. 
  - Output formats currently supported include PDF, PS, PCL, AFP, XML (area tree representation), Print, AWT and PNG, and to a lesser extent, RTF and TXT. The primary output target is PDF.

- https://github.com/Symbitic/markbook /MIT/202002/js
  - https://symbitic.github.io/markbook/
  - Write books in CommonMark.

## docbook

- https://github.com/docbook/xslt10-stylesheets /xslt
  - XSLT 1.0 Stylesheets for DocBook

## asciidoc

- https://github.com/asciidoctor/asciidoctor.js /js
  - uses Opal to transpile Asciidoctor, a modern implementation of AsciiDoc, from Ruby to JavaScript to produce asciidoctor.js

- https://github.com/asciibook/asciibook /60Star/MIT/202308/ruby
  - https://asciibook.org/
  - An ebook generator from asciidoc to html/pdf/epub/mobi
# solutions/ssg
- https://github.com/softcover/softcover /MIT/202310/ruby
  - https://www.softcover.io/
  - CLI for book generation, building, and publishing to softcover.io
  - Softcover is an ebook typesetting system for technical authors. 
  - This is the main gem, softcover, which depends on `polytexnic` to convert Markdown or PolyTeX input to HTML and LaTeX, and thence to EPUB, MOBI, and PDF.

- https://gitlab.com/DaveJarvis/KeenWrite /BSD/202312/java
  - https://keenwrite.com/
  - open-source, cross-platform desktop Markdown editor that can produce beautifully typeset PDFs.
  - based on Markdown-Writer-FX
  - Typesetting to PDF files requires the following: Theme Pack ConTeXt

- https://github.com/retypeapp/retype /907Star/Free100Pages/202310/js
  - https://retype.com/
  - ultra-high-performance static site generator that builds a website based on simple text files.
  - [Retype: A self-hosted and free alternative to gitbook | Hacker News_202204](https://news.ycombinator.com/item?id=30938501)
# wikidata
- https://github.com/inventaire/inventaire /js
  - https://inventaire.io/
  - Its a collaborative resources mapper project, while yet only focused on exploring books mapping with wikidata and ISBNs
  - https://github.com/inventaire/inventaire-client
# more
