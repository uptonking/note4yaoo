---
title: lib-office-gitbook-docbook
tags: [docbook, format, gitbook, office, spec]
created: 2023-09-19T07:53:30.188Z
modified: 2023-09-19T07:53:59.349Z
---

# lib-office-gitbook-docbook

# guide

- 需求分析和优先级
  - 渲染的一致性, pdf/fop
  - 自定义排版, canvas/latex/DonaldKnuth
  - 数据导出的格式, docx/markdown
  - 搜索与查询

- 纯文本的缺点
  - 不方便引用文本块或其他块
  - 不方便自定义格式，比如内嵌表格、画板

- 文件格式的实现可理解为数据库序列化导出的一种场景

- tips
  - DocBook is a semantic markup language for doc, 并不是一种具体的文件格式
  - docbook/docx描述了数据模型层， HTML/EPUB/PDF/man-pages描述了视图层，侧重点不同
  - docx大多是单篇文档，而不是整本书，但编辑工具很多，docx/xlsx/pptx都属于ooxml
  - **epub不方便实现编辑，不适合作为知识库的编辑层，参考sigil将editor分离出去了**
  - 用hexo作为ssg生成重展示型的网站，可替代部分reader/cms产品

- 结合纯文本编辑和数据库同步的方案
  - 分离文本的方案使用非常广泛，如ooxml/epub/textbundle，常用来处理只读/读多写少的场景
  - 参考git，文本文件更新由用户编辑，commit更新数据由git生成并放在`.git`文件夹
    - `markdown + database`的方案也可以有类似实现，但也会与类似git的工具绑定

- docbook vs ooxml
  - docx格式使用广泛得多，docbook格式古老，docx/odf格式新一点
  - 格式可相互转换
  - docbook使用类似css的方式设置样式, ooxml使用类似富文本编辑器的方式存储样式
  - 对大文件的支持
    - .docx的元数据和样式在多个小文件，但主体内容在`document.xml`这一个大文件
    - .epub的元数据和样式在多个小文件，但主体内容在text文件夹下多个`.xhtml`小文件
    - 懒加载、虚拟渲染

- book-formats，只读/readonly的工具较多
  - epub
  - docbook
  - markdown/asciidoc/reStructuredText-sphinx
  - gnu-texinfo
  - emacs-orgmode
  - wikipedia zim: 高压缩，为只读设计
  - O'Reilly HTMLBook Specification: rarely
  - 主流notebook: jupyter

- who is using #markdown-markup
  - gitbook, rust-docs
  - nixos

- who is using #asciidoc
  - FreeBSD has recently switched from DocBook to AsciiDoc

- who is using #reStructuredText
  - sphinx-docs-python
  - Linux kernel project decided to transition from DocBook based documentation to reStructuredText and the Sphinx toolchain in 2016

- who is using #epub-html/css
  - kobo ereader
  - apple books, google play books, kindle fire
  - Adobe Digital Editions uses .epub format for its e-books, with digital rights management (DRM) protection provided through their proprietary ADEPT mechanism.

- resources
  - [Comparison of Office Open XML and OpenDocument - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Office_Open_XML_and_OpenDocument)
# blogs
- 👉🏻 **asciidoc has first class support for blocks and references/attributes**.

- [Lightweight Markup: Markdown, reStructuredText, MediaWiki, AsciiDoc, Org-mode - Hyperpolyglot](https://hyperpolyglot.org/lightweight-markup)

## ⚖️ [DocBook - Wikipedia](https://en.wikipedia.org/wiki/DocBook)

- DocBook is a semantic markup language for technical documentation. 
- As a semantic language, DocBook enables its users to create document content in a presentation-neutral form that captures the logical structure of the content; 
  - that content can then be published in a variety of formats, including HTML, XHTML, EPUB, PDF, man pages, WebHelp and HTML Help, without requiring users to make any changes to the source
- DocBook files are used to prepare output files in a wide variety of formats. 
  - Nearly always, this is accomplished using DocBook XSL stylesheets. 
  - These are XSLT stylesheets that transform DocBook documents into a number of formats (HTML, XSL-FO for later conversion into PDF, etc.). 
  - These stylesheets can be sophisticated enough to generate tables of contents, glossaries, and indexes.
- Norman Walsh and the DocBook Project development team maintain the key application for producing output from DocBook source documents: A set of XSLT stylesheets (as well as a legacy set of DSSSL stylesheets) that can generate high-quality HTML and print (FO/PDF) output, as well as output in other formats, including RTF, man pages and HTML Help.

- The major features are its fully CSS-based page layout, search of the help content, and a table of contents in collapsible-tree form. 

- DBpedia data is served as Linked Data, which is revolutionizing the way applications interact with the Web. 

## [DBpedia](https://www.dbpedia.org/about/)

- DBpedia is a crowd-sourced community effort to extract structured content from the information created in various Wikimedia projects
  - This structured information resembles an open knowledge graph (OKG) which is available for everyone on the Web. 
- The DBpedia RDF Data Set is hosted and published using OpenLink Virtuoso. 
  - The Virtuoso infrastructure provides access to DBpedia’s RDF data via a SPARQL endpoint, alongside HTTP support for any Web client’s standard GETs for HTML or RDF representations of DBpedia resources.
  - As the project gained traction, the HTTP demands on Pubby’s out-of-process Linked Data Publishing services increased, and the natural option was to take advantage of Virtuoso’s SPASQL (SPARQL inside SQL) and other Linked Data Deployment features, by moving these services in-process with Virtuoso.

- https://github.com/dbpedia/databus /js
  - Databus is a transformative platform for agile data integration, collaboration, and automation via a structured metadata Knowledge Graph

- [On the Mutually Beneficial Nature of DBpedia and Wikidata_201702](https://medium.com/virtuoso-blog/on-the-mutually-beneficial-nature-of-dbpedia-and-wikidata-5fb2b9f22ada)
  - DBpedia’s focus is on generating Linked Open Data from Wikipedia documents.
  - Wikidata’s focus is on creating Linked Open (meta)Data to supplement Wikipedia documents.
  - Both projects provide access to their respective Linked Open Data via SPARQL Query Service endpoints.

- [A Preliminary Study on Wikipedia, DBpedia and Wikidata_201506](http://andrea-index.blogspot.com/2015/06/wikipedia-dbpedia-wikidata.html)
  - 提供了比较表格

### [What are the differences between Wikidata and Dbpedia? | ResearchGate](https://www.researchgate.net/post/What_are_the_differences_between_Wikidata_and_Dbpedia)

- DBpedia extracts structured data from the infoboxes in Wikipedia, and publishes them in RDF and a few other formats.
- Wikidata  provide a secondary and tertiary database of structured data that everyone can edit.  it will allow infoboxes to be created from structured data.

- DBpedia is a project to create a graph from Wikipedia data. 
  - That is not the goal of Wikidata. Wikidata aims to provide a free knowledge base that anyone can edit.
- 
- 
- 
- 
- 
- 

## 💡 [Comparison of e-book formats - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_e-book_formats)

- The EPUB format is the most widely supported e-book format
  - Most e-book readers also support the PDF and plain text formats

- Open eBook (OEB), or formally, the Open eBook Publication Structure (OEBPS), is a legacy e-book format which has been superseded by the EPUB format. 
  - Open eBook is a ZIP file plus a Manifest file
  - The default file extension is .opf (OEB Package Format).

- [Write a Book with Markdown | Hacker News](https://news.ycombinator.com/item?id=36582208)
  - Being built on DocBook is a great insurance policy for Asciidoc, as DocBook has been around approximately forever and opens lots of doors to other XML specifications via XSL or something more sane.

## [DocBook: The Definitive Guide - online](https://tdg.docbook.org/)

- [homepage for DocBook 5: The Definitive Guide](https://docbook.org/)

- DocBook is more than 15 years old. It began in 1991 as a joint project of HaL Computer Systems and O’Reilly
- DocBook’s roots are in SGML, where it was defined with a Document Type Definition, or DTD. 
  - DocBook was released as both an SGML and an XML vocabulary starting with V4.1. 
- Starting with DocBook V5.0, DocBook is exclusively an XML vocabulary defined with RELAX NG and Schematron.
  - In V5.0, DocBook has been rewritten as a native RELAX NG grammar (“An introduction to the RELAX NG schema language” is an excellent introduction to the grammar).

- [业界有哪些结构化文档写作软件包？](https://www.zhihu.com/question/55048996)
  - Arbortext是写作工具，dita是一种写作标准。
  - 书写结构化文档工具目前有 PTC的Arbortext，以及Syncro Soft的Oxygen xml

## [DITA 与 DOCBOOK 对比](https://www.ossez.com/t/dita-docbook/10050)

- DITA和DocBook是数字出版领域的两种标准，通过定义规范化的文档描述规则，来解决文档交付过程中遇到的问题
- DITA解决了出版物的结构化描述和内容重组问题，且支持多语言版本制作，适用于对格式有严格限定的技术手册类出版物。但DITA不能实现很完美的样式渲染，且对于内容与格式一体化的复杂出版物，DITA很难进行主题和界定与划分。所以使用DITA进行书籍出版的成本和难度较高。
- DocBook适用于通用出版物，文档易于组织和排版。但DocBook内容以Section段落组织，不具备DITA的内容映射机制，无法做到类似Topic这样粒度的内容划分与重组。且对于内容需要频繁修改的文档排版，Docbook略显力不从心。 
- DITA和DocBook专注于交付技术信息，但DITA侧重于交付主题，而DocBook侧重于交付书籍。
- DITA提供基于主题级粒度的信息分类，允许作者组织并描述特定信息领域。在生成多种文档格式的信息重用过程中，能够保持内容的高度一致性。在最终交付物的输出格式方面，DITA能够生成 PDF、CHM、HTML等大部分的出版交付类型。
- DocBook常用的交付格式为PDF和HTML，其他输出格式需要借助相关的功能插件。

- [DITA 已死](https://zhuanlan.zhihu.com/p/345260365)
  - DITA作为文档交付应该已经是日薄西山了。应该没有什么人通过写 XML 的方式来写文档了。
  - 相反，MD 和 AsciiDoc 格式的文档却大行其道。主要原因是能够随意部署，并且文档结构少，约束少，更加容易写作和阅读。
  - DITA，编译太复杂，PDF生成问题太多，CHM 格式的文档很多时候大家都
- dita是底层文件格式的方案，word内部也是xml格式，但是没有有人创建word从xml开始的。dita需要专门写dita的工具和工具集，上下游都是厂商去自行设计的。大型航空公司都用dita
# blogs-epub

## ⚖️ [EPUB - Wikipedia](https://en.wikipedia.org/wiki/EPUB)

- The .epub or OEBPS format is a technical standard for e-books 
- The EPUB format has gained some popularity as a vendor-independent XML-based e-book format.
- The EPUB format is implemented as an archive file consisting of `XHTML` files carrying the content, along with images and other supporting files. 
- EPUB is the most widely supported vendor-independent XML-based e-book format; that is, it is supported by almost all hardware readers
- An EPUB file is an archive that contains, in effect, a website. 
  - It includes HTML files, images, CSS style sheets, and other assets. It also contains metadata.

## ⚖️ [Portable EPUBs _202401](https://willcrichton.net/notes/portable-epubs/)

- https://github.com/nota-lang/bene /202401/ts/rust/tauri
  - https://nota-lang.github.io/bene/
  - Bene is a reading system for documents written in the EPUB file format.

- modern document formats like HTML have yet to provide a competitive alternative to PDF. This post explores what prevents HTML documents from being portable, and I propose a way forward based on the EPUB format.
  - To demonstrate my ideas, this post is presented using a prototype EPUB reading system.
- PDF is the de facto file format for reading and sharing digital documents like papers, textbooks, and flyers.
- 🌹 pros-pdf
  - PDFs are self-contained. A PDF is a single file that contains all the images, fonts, and other data needed to render it. 
  - PDFs are rendered consistently. A PDF specifies precisely how it should be rendered
  - PDFs are stable over time. PDFs from decades ago still render the same today. PDFs have a relatively stable standard
- 🐛 cons-pdf
  - PDFs cannot easily adapt to different screen sizes. Most PDFs are designed to mimic 8.5x11" paper (or worse, 145, 161 km2). These PDFs are readable on a computer monitor, but they are less readable on a tablet or phone.
  - PDFs cannot be easily understood by programs. A plain PDF is just a scattered sequence of lines and characters. For accessibility, screen readers may not know which order to read through the text. For data extraction, scraping tables out of a PDF is an open area of research.
  - PDFs cannot easily express interaction. PDFs were primarily designed as static documents that cannot react to user input beyond filling in forms.
- These pros and cons can be traced back to one key fact: the PDF representation of a document is fundamentally unstructured. 
  - PDF commands are unstructured because a document's organization is only clear to a person looking at the rendered document, and not clear from the commands themselves. 
  - Reflowing, accessibility, data extraction, and interaction all rely on programmatically understanding the structure of a document. Hence, these aspects are not easy to integrate with PDFs.

- how can we design digital documents with the benefits of PDFs but without the limitations?
- PDFs can be annotated with their logical structure to create a tagged PDF
  - In theory, these issues could be fixed. If the world's PDF exporters could be modified to include logical structure.

- we already have a structured document format which can be flexibly and interactively rendered: HTML (and CSS and Javascript, but here just collectively referred to as HTML). 
  - The HTML format provides almost exactly the inverse advantages and disadvantages of PDF.
- 🌹 pros-html
  - HTML can more easily adapt to different screen sizes.
  - HTML can be more easily understood by a program.
  - HTML can more easily express interaction
- 🐛 cons-html
  - HTML is not self-contained. HTML files may contain URL references to external files that may be hosted on a server.
  - HTML is not always rendered consistently. HTML's dynamic layout means that an author may not see the same document as a reader.
  - HTML is not fully stable over time. Browsers try to maintain backwards compatibility 

- how can we design HTML documents to gain the benefits of PDFs without losing the key strengths of HTML?
  - Self-Contained HTML with EPUB

- how can we make HTML documents self-contained? 
  - This is an old problem with many potential solutions. 
  - WARC, webarchive, and MHTML are all file formats designed to contain all the resources needed to render a web page. 
  - But these formats are more designed for snapshotting an existing website, rather than serving as a single source of truth for a web document. 
- From my research, the most sensible format for this purpose is EPUB.
- an EPUB is a ZIP archive of web files: HTML, CSS, JS, and assets like images and fonts. 
  - On a technical level, what distinguishes EPUB from archival formats is that EPUB includes well-specified files that describe metadata about a document. 
- The EPUB format optimizes for machine-readable content and metadata. 
  - HTML content is required to be in XML format (hence, XHTML). 
  - Document metadata like the title and author is provided in structured form in the package document. 
  - The navigation document has a carefully prescribed tag structure so the TOC can be consistently extracted.
- Overall, EPUB's structured format makes it a solid candidate for a single-file HTML document container. 
- However, EPUB is not a silver bullet. EPUB is quite permissive in what kinds of content can be put into a content document.
  - a major issue for self-containment is that EPUB content can embed external assets. A content document can legally include an image or font file whose src is a URL to a hosted server. 
  - Google Doc's EPUB exporter will emit CSS that will @include external Google Fonts files. The problem is that such an EPUB will not render correctly without an internet connection, nor will it render correctly if Google changes the URLs of its font files

- Hence, I will propose a new format which I call a portable EPUB, which is an EPUB with additional requirements and recommendations to improve PDF-like portability

- The first requirement is local asset requirement
  - All assets (like images, scripts, and fonts) embedded in a content document of a portable EPUB must refer to local files included in the EPUB. 
  - Hyperlinks to external files are permissible.
- I think the core solution for consistently rendering EPUBs comes down to this:
  - The document format (i.e., portable EPUB) needs to establish a subset of HTML (call it portable HTML) which could represent most, but not all, documents.
  - Reading systems need to guarantee that a document within the subset will always look reasonable under all reading conditions.
  - If a document uses features outside this subset, then the document author is responsible for ensuring the readability of the document.
- Portable HTML rendering requirement: if a document only uses features in the portable HTML subset, then a portable EPUB reading system must guarantee that the document will render reasonably.
- Portable HTML generation principle: when possible, systems that generate portable EPUBs should output portable HTML.
- Fixed-layout fallback principle: systems that generate portable EPUBs can consider providing both a reflowable and fixed-layout rendition of a document.
- Cascading styles principle: both documents and reading systems should express stylistic preferences (such as font face, font size, and document width) as CSS styles which can be overriden (e.g., do not use !important). The reading system should load the CSS rules such that the priority order is reading system styles < document styles < reader styles.

- I decided to build a lighter EPUB reading system, Bene. 
  - The styling and icons are mostly borrowed from pdf.js. 
  - Bene is implemented in Tauri
  - The general design goal of Bene is to embody my ideals for a portable EPUB reader. 

- Encapsulated scripts principle: interactive components should be implemented as web components when possible, or otherwise be carefully designed to avoid conflicting with the base document or other components.
- Components fallback requirement: interactive components must provide a fallback mechanism for rendering a reasonable substitute if Javascript is disabled.

- My short-term goal is to implement a few more documents in the portable EPUB format, such as my PLDI paper. 
- My long-term goal is to design a document language that makes it easy to generate portable EPUBs. Writing XHTML by hand is not reasonable. I designed Nota before I was thinking about EPUBs, so its next iteration will be targeted at this new format

### 👥 [I wrote some ideas for how to actually make HTML documents a viable replacement for PDFs.](https://twitter.com/tonofcrates/status/1750591889391378796)

- PDF continues to exist on the web primarily because we don't have a format that hermetically packs html with all its resources into one file that can be seamlessly loaded in a browser. 
- My answer is basically:
  - Use EPUB to package an HTML document into a single file.
  - Build a better EPUB reading system.

- I think the "aesthetics" point is a lot broader than line-breaking. You can control layout and rendering more in TeX and more in PDF than in HTML and that seems hard to change.
  - line-breaking is just a prominent example. Besides typography, I think HTML provides pretty expressive layout/render controls? The main problem is using these controls such that a document is still responsive, accessible, etc
# docbook-docs

# more

# discuss-ebook/epub
- ## 

- ## 

- ## 

- ## [Digital books wear out faster than physical books | Hacker News](https://news.ycombinator.com/item?id=33616593)
- HTML isn't immune from broken backwards compatibility.
  - The frame element has been completely removed, the hgroup element is gone, and so is the dir element. acronym is deprecated in favour of abbr. isindex, plaintext, xmp, and listing are all dead.
  - The attributes border, clear, background and bgcolor have all been removed by HTML, and shifted to be CSS' responsibility instead.
- Just moving between EPUB 2 and EPUB 3, you lose the DAISY format support, and external resources. 
  - (EPUB2 let you use full URLs to specify parts hosted externally, like webpages, but EPUB3 requires itself to be self-contained. Not a bad change, but still a breaking change.) 
  - NCX replaces just using a HTML5 nav element, and a few more things.

- ## [Sigil – A free, open-source, multi-platform eBook editor | Hacker News_202008](https://news.ycombinator.com/item?id=24140752)
- It appears to be largely equivalent to the Calibre editor.

- I prefer markdown -> pandoc -> epub. That way I can use whatever editor I like, and I'm not stuck editing HTML by hand.

- I haven't played much with any of this stuff, but one thing that I'm curious about is what is the advantage of having a container format like this, rather than just having a single giant HTML file (with embedded CSS & data: uri images)?
  - For editing this would be ridiculous, but for transport and presentation it seems much more compact and useful. It is easy to target as an output format for a variety of tools, without understanding a bunch of quirks of the format. It would be easier to render, since the application has to make all the decisions about where to place content and support reflowing anyway.
- An .epub is already what you describe; it's a .zip of .xhtml, images, and supporting files you edit directly seen in the sidepanel
  - An ebook editor just entails helping you edit those .xhtml files in a slightly more domain specific way, generating a few extra files (like table of contents), and producing the distributable zip.
- One big file is hard to handle. Ereaders choke on them just like the browser does.
  - They do; probably xhtml/XML is not really an ideal format because it isn't easily linearalizable, but if ereaders are using a reduced set of the functionality, then they can probably safely assume that they can just split the file at a `<p> or <mpb:chapter>` tag without loss of fidelity, and just consider that all style-related content needs to occur in `<head>`.
- For long books or books containing large images or videos, that giant HTML file would be so gigantic that many e-readers would be slow at loading them or even fall over (the average e-reader doesn’t have a fast CPU or loads of memory).
  - I also expect data URIs for images would make the HTML file, even if gzipped, larger than the equivalent ePub.
  - HTML also isn’t good at doing the book-like things such as pagination, tables of content and on-page footnotes.

- What's the value of your tool over using asciidoc tools
  - It's WYSIWYG, and I can edit existing EPUB files, which is always nifty.
  - I believe the WYSIWYG part of sigil was forked into PageEdit?

- 
- 
- 
- 
- 
- 

- ## [Alexandria: A minimalistic cross-platform eBook reader | Hacker News](https://news.ycombinator.com/item?id=37303960)
- One fun thing about Calibre is that the library is stored in a SQLite database. So, if you write a wrapper to parse that data, you don’t even need Calibre’s content server running!
  - I have the library stored on my NAS and am running a fairly simple NodeJS + Express + React web app on my Raspberry Pi that reads the database and provides web access this content.
- Koreader does awesome stats tracking into a SQLite database of every page you’ve read. You even get a calendar view for months showing what you’ve been reading.

- ## 💡 [Today I learned Epub is just HTML/CSS | Hacker News_202104](https://news.ycombinator.com/item?id=26739124)

- You might be surprised to learn just how many files are zip files.
  - Java software (jar, war): zip files
  - Android packages (apk): zip files
  - OpenDocument Format (odt, ods, odp): zip files
  - Quake 3 / OpenArena / Urban Terror / etc. (pk3): zip files
  - Firefox/Thunderbird/Chromium extensions (xpi, crx): zip files
  - EPUB: 
  - numpy's npz is also zip.
- Yeah, it is surprising at first, but after you think about it, maybe not so much. If you need to cram a bunch of files into one package, zip is the obvious candidate. There are well-tested libraries and apps for dealing with zips for essentially every language and operating system.

- It actually goes deeper than that: Epub is basically a specific implementation of DocBook, which is itself a specific XML specification derived from the grand daddy of markup languages SGML.

- 👉🏻 It's pretty easy to write code that generates and displays **EPUB2**.
  - **EPUB3** is a dog's breakfast -- it's hard to think of a better example of "second system effect". As far as I know, **there's still not even one reference implementation that supports the full standard**, even though it's been out for nearly 10 years. 
  - It gains you very little over EPUB2 for standard novels written in western scripts. 
  - **EPUB3 is only needed if you require embedded scripting**, support for non-alphabetical or bidirectional scripts, etc. 
  - I believe that most commercial "EPUB3" files still have an EPUB2 `toc.ncx` file and are designed to fall back to EPUB2 if the reader doesn't support EPUB3 (there are a lot of readers like this).
  - Something that's easy to overlook(忽视): "The mimetype file must be a text document in ASCII that contains the string `application/epub+zip`. It must also be uncompressed, unencrypted, and the first file in the ZIP archive". What this means in practice is that **uncompressing an EPUB is easy** (just rename it to .zip, if necessary, and run unzip), but **recompressing it requires some care**.
- EPUB 3 Reading Systems may optionally support scripting, which was explicitly discouraged in EPUB 2.

- Books should be immutable much like a true real website. Anyone using javascript in a book should not be writing a book. If you're writing javascript then go write an app.
  - I can see some useful cases. For example, in a computer science book, you could update a caption space that gets its data from the web. This would allow you to display an "obsolete sample code" warning below the examples. When the user is not connected to the internet, you could display "Get online to know code snippet status". And so on.
  - A better idea: include the "obsolete sample code" warning in the book and ask the user check for the latest practices at a URL also included in the book.

- I've worked on a ePub parser and renderer and the issues you're describing sound pretty familiar.
  - The three main components of the ePub (aside from the actual pages) are the TOC, the spine(书脊) and the manifest. 
  - The manifest basically tells you where everything is, the TOC is the table of contents which can link to various pages and the spine gives you the traversal order.
  - Some mistakes I've seen are using the TOC to traverse the book. Using the spine to traverse the book but not handling hidden pages properly. Not handling two page spread properly.
  - We ended up writing our own parser because we kept finding issues with the main open source ones.

- Epub can do all sort of homecalling / user tracking using HTML or CSS or javascript. 
  - What's even worse - almost all Epub readers don't do proper sandboxing.
  - Browsers don't block any homecalling either.

- One of the benefit of EPUB is that text can be reflowed, so the display size doesn't matter much, unlike PDF which sets a specific page size. I'm not sure about the MOBI format, but I assume it has similar features to EPUB?
  - Mobi is very similar to EPub. It’s almost a 0.9 version of EPub. The main differences are in the container.

- sounds like the kindle format (actually mostly .mobi) is moving towards html/css too
  - When I checked, years ago, it seemed that .mobi included an embedded EPUB file. 
  - It's actually always used XHTML. Both .mobi and .epub is based on the Open Ebook format

- Yes it's "just" HTML/CSS, but given the wide range of ePub reader capabilities, it's not like you can just take any web page and put it in an .epub. 
  - You have be conservative, and use only basic stuff. Also JavaScript is not supported by most ePub readers, so many of the modern web "dynamic" niceties are not available.
  - For example, rendering math on the web has been a solved problem for many years thanks to MathJax and KaTeX, but these require JS, so cannot be used in ePubs (unless you know the reader supports scripting).

- One of the possible reasons Chromium is a bad for EPUB is its lack of MathML support. But then it's not like all EPUB readers have it, and it's not like MathJax can't be used for rendering.
- epub supports MathML. are you saying Chrome doesn't support MathML?
  - Sadly yes. There are solutions such as MathJax, however this is obviously not as nice as having it built into a lower level.
# discuss-docbook
- ## 

- ## 

- ## 

- ## [未来有没有可能使用HTML完全替代Word，Latex等文档格式? - 知乎](https://www.zhihu.com/question/479921969)
- Office的流行，在一定程度上等于把排版的工作转嫁给写作者

- ## [DocBook 5.1: The Definitive Guide (2020) | Hacker News_202203](https://news.ycombinator.com/item?id=30550354)

- DocBook was SGML for most of its lifetime, and only became XML-only with the newest version 5, I believe. 
  - So you can use custom Wiki syntax if your concern is XML's verbosity and unfriendliness as an authoring format.
  - Other than that, I don't have a particular bad experience using DocBook for the one conference paper where I used it. Especially compared to LaTeX' limited options for rendering copies to HTML, I'd say DocBook is far better, like you say.
  - Also, DocBook is supported by pandoc.
  - I thought DocBook was for technical books whereas Sphinx + ReStructuredText was for technical documentation?

- For software and technical documentation, I recently rediscovered **GNU Texinfo**. It perfectly fills the gap that the others have left open.
  - Consistent, fairly easy syntax, exports to DocBook, PDF, HTML and can be read interactively from terminal as well.
  - In contrast to markdown|asciidoc|reStructuredText|… and LaTeX, it handles more complex, non-linear documentation very well.
- I wonder if Texinfo became a victim to naming that is easy to misunderstand. 
  - "Texinfo" is basically a structured document format, somewhat similar to DocBook, except instead of XML it uses a more compact and (IMO) easier to read and write syntax that `@looks{ like this }`. 
  - It is largely meant for full manuals, guides, etc. 
  - There are a bunch of conversion tools (AFAIK written in Perl) to convert Texinfo documents to other formats, like TeX, HTML and of course info.
  - "info" is a hypertext document format, similar to CHM, though it predates it (and HTML) by many years. It is quite primitive though it has some neat indexing functionality which improves searching it
  - One of its biggest issues is that it is a preformatted document and image support is "hacked in"..
  - "GNU info" is GNU's viewer for info documents which uses some Emacs-like shortcuts which trips people.
- Note that Texinfo was originally meant to generate output for the info file format (viewed by the GNU info viewer as well as GNU emacs and a few other less used viewers) alongside TeX, which is probably where it got its name (tex+info output). The info format is essentially a primitive hypertext format with support for hierarchical nodes and keyword indices packaged in a single file (essentially a primitive text-only form of CHM, though later versions of info also support external image references). The HTML and other output formats were added much later.

- I feel like DocBook is in a bad place compared to alternatives - it's to esoteric(只有内行才懂的; 难懂的), too hard to write, and then there's the fact that it's XML.
  - TeX and friends are first class for paper docs and publication, but given their **pre-web** origins don't work well in that medium.
  - Markdown is just **too limited** and primitive for anything more than a blog post or basic README file - no captions on figures, hyperlinking to headings/sections isn't formalized, etc.
  - I tend to think that Sphinx + ReStructuredText makes the right balance in terms of publishing targets, and with all of Python, ReadTheDocs, and the Linux Kernel making the same decision, it seems like the right one. Intersphinx is pretty sweet if you have to link multiple sites together.
  - MS Word and Wikis can go die in a fire.

- I have seen some places that use asciidoc as the interface, and then transpile asciidoc to docbook by using custom transformations. This works really well.
  - It's a huge PITA to write anything but basic markdown for books or long articles (30+ pages) that you need to output in multiple formats (e.g. one source to PDF, epub, and html) to be honest.
- What I'd love to see is a general-purpose human readable format for documents. 
  - Markdown is handicapped by being (effectively) an HTML pre-processor for a tiny subset of HTML. Poor support for math, no captions, but more importantly very little semantics. 
    - On the other hand, if you think of Markdown as just being a preprocessor, not a format that has to have everything built in, it's really not that bad if your renderer is good. For example: python-markdown has built-in plugins that make everything much nicer: meta, extra, and smarty are the one's I'd recommend. 'yafg' is a plugin that solves the figure support problem. 'markdown_vidify' allows embedding HTML5 videos.
  - RST strikes me as rather domain specific with its emphasis on technical writing, and IMO it also suffers from being intended as a preprocessor (the ugly link syntax for example).
  - I'm probably asking for too much, but what I'm looking for is something semantic enough to write a book in, but with viewing as plain text as the primary intended output. Gemini's gemtext format has very different goals, but it captures what I mean by "text as the primary intended output" very well.

- There are dozens of Markdowns flavors:
  - Github Flavored Markdown, Stack Exchange Flavored Markdown, Markdown Extra LiaScript MultiMarkdown, LeanPub Flavored Markdown, Markua Python-Markdown, Kramdown
  - Even that is enough to show that Markdown is bad by design. But when you actually use it for any serious document, you face the bad design and struggle with the "easy" tool 

- Creating books with Jupyterbook gives creating books in markdown endless options. It’s simple but you can create complex interactive books as well. All browser based powered by JupyterLab and building on sphinx.

- DocBook has served me very well.
  - Unfortunately, the tooling, although very capable and very well documented is very difficult to use unless you're an XML expert already. XSLT really isn't a good choice for this sort of thing. That's what I had to use because CSS-styling wasn't mature enough. These days I'd **start with CSS instead of XSLT**.
  - Crucially, I would use a commercial FO processor. I spent a lot of time with Apache FOP
  - You're not meant to write XML by hand, but there aren't that many great editors out there. I use OxygenXML, which is all right. It's expensive. T
  - To sum up: Do use DocBook. Use OxygenXML to write your books and collaborate with your coauthors and editors.

- Asciidoc and Asciidoctor can produce DocBook, and from DocBook you can do most formats.
  - Working with the DocBook toolchain is rather unpleasant and brittle (depends a lot on the versions), so my company ended up packaging everything in a Docker container https://github.com/l3nz/dockbooker - this has worked pretty well for many years 
  - but now we mostly use Asciidoctor by itself.
- I've the same experience. Soem years ago I tried DocBook to render HTML and PDF documents, but the whole setup was so unpleasant that I gave up. Writing the syntax is not overly hard, but also not pleasant. I ended up with AsciiDoc, what is nice to read and write and which has a rich set of features. 
- AsciiDoctor has been designed so that its syntax elements map well to Docbook. You can use pretty much every feature of Docbook with the much nicer AsciiDoctor syntax on top.

- I find DocBook (and XML in general) too cumbersome. I've been using Asciidoc in conjunction with Pandoc to create Word documents, Asciidoctor-PDF to generate PDF documents, and Antora to generate websites. This combination works well for me, anyway.
- Asciidoctor could be perfect for my use case, but as of now it does not support end of page footnotes, but end of chapter or end of article ones.

- Is there anyone who enjoys writing XML?
  - It's a document interchange format, and the code that persists it does not have feelings.
  - Use it to write out (externalize) the model structure of your document to persistent storage.
  - The structure reflected in the XML form of a document could either be hidden below a near-WYSIWYG GUI layer, or it may be more exposed in an XML editor: XML editors let you edit XML in a way that "normal" text editors don't (e.g. show markup and text directly together while still protecting mark-up tags instead of treating them as character-wise editable text).

- ## [Docbook | Hacker News_201911](https://news.ycombinator.com/item?id=21436245)
- When I was at O'Reilly Media, we worked on an HTML replacement to Docbook called HTMLBook.
  - I built the Atlas system that O'Reilly uses to produce books, along with a Markdown and Asciidoc converter to HTMLBook. So **even though you write in Asciidoc or Markdown, it gets converted to HTMLBook** since that's what the entire toolchain understands. But those formats are great for the authors wanting to write in a plain-text alternative.
  - Behind the scenes, you're actually getting well-formed HTML5—specifically, HTMLBook, our new open standard for writing books (or book-like projects) in HTML.

- Today I'm using AsciiDoc with AsciiDoctor. The AsciiDoc syntax is as pleasant as MarkDown, but much more powerful and more consistent. AsciiDoc can be converted to DocBook if needed, but I've never needed this possibility, because all I need is PDF and HTML output.

- Does anyone else have the feeling that Docbook was killed by XML?
  - the whole world apparently decided that SGML is bad and XML is good, and started over. Markup became annoying, DSSSL was replaced with XSLT
  - It took a few years until xsltproc finally made XSLT usable (but still not pretty to look at), and Apache FOP could format to PDF 
  - But nobody wrote their documentation in Docbook or Linuxdoc anymore. Because markdown and asciidoc and a bazillion similar ad-hoc languages may not have been as theoretically clean, but at least the tools worked, even on a cheap workstation.

- Don’t use Tex if you’re aiming for web formats. There’s technically ways to do it but I’ve never found it effective.
  - Sphinx is probably the best for what you’re looking for though

- 👉🏻 TeX is a document typesetting language, not a file format. It's really, really awesome for making documents that are typeset in a very specific way. LaTeX gives you a set of macros on top of TeX that allows you to abstract some of that stuff to a certain degree, but the underlying engine is for typesetting.
  - TeX is a real programming language, though with a truly bizarre syntax and grammar (I still love it, though ; -) ). Trying to execute TeX and output HTML is incredibly difficult to do with any kind of quality. You could take LaTeX documents and then write a completely different formatting system that output HTML, but at that point, you would be better off using a system that is intended to output HTML: like docbook
- I think you're misunderstanding what typesetting means. LaTex is for producing output to send to a typesetter to generate a printed document. What Tex produces is essentially a document page image. It was never intended for producing documents for user consumption on electronic devices. The least worst approach would be to use it to generate a PDF.
- The thing is ePubs and such aren't all that easy to consume. They don't provide standardised predictable layout, so you can't control how it will be presented to the reader. 
  - **HTML and ePub only provide layout hints to the device or reader app**. 
  - Even the reader doesn't have much control how the document is displayed. 
  - In contrast PDF provides complete, precise control over presentation. 
- HTML is too vague and imprecise a format to express one anyway.
  - HTML does not have the concept of a deterministic page size and length or predictable pagination. In academic papers references, figures, footnotes and titles need to be presented in a deterministic way so that when text refers to a figure, or a footnote is referenced, etc, they exist in a predictable and know relationship to each other. 
  - HTML can't even guarantee that a given image will be displayed at all. have you never been to a web page where some images were not shown or just appeared as placeholder boxes?
  - Information that belongs together, that the author intends and needs to be together, had better be together. None of this can be guaranteed by HTML or ebook formats. These formats can't guarantee what fonts information will be represented in, they can't even guarantee whether text will he shown in italics, bold, what relative font sizes they will have, etc. Reference formats are very precisely specified, but these formats simply don't support that level of precision.
- figures, footnotes and titles need to be presented in a deterministic way so that when text refers to a figure, or a footnote is referenced, etc, they exist in a predictable and know relationship to each other
  - Solved with references to the structure, e.g. ‘Figure 1.1‘ or ‘Section 2.4.‘
- have you never been to a web page where some images were not shown or just appeared as placeholder boxes?
  - Solved with a format that ships the page and images together, like Epub does. It's a basic requirement for sane personal storage-for-reference anyway.

- **TeX is special in that it has perfect algorithms for doing things like line breaking, kerning, etc, etc, etc**. 
  - The output of TeX is dramatically better than just about any other piece of software. It's insanely better than any word processor will output and there are probably only a handful of desktop publishing packages that are even close. 
  - If you need absolutely perfect print output, then TeX (and LaTeX) are a really good fit.
  - Because Donald Knuth.

- Is this still used ?
  - It's not used directly in a lot of places. However, it's still used in a lot of publishing toolchains as an intermediate format, usually compiled from asciidoc via asciidoctor. 
  - O'Reilly books, for example, are all written in asciidoc and then run through a publishing toolchain that goes through asciidoctor to docbook, to eventually get rendered into printable formats as well as PDFs.

- We still use it a lot within KDE, for all the documentation.

- I started using it recently since the manual and all the documentation of Nix, NixOS and nixpkgs are written in Docbook.
  - > nix migrate to markdown in 2020

- ## 🤔 [Documentation format - NixOS Discourse_201910](https://discourse.nixos.org/t/documentation-format/4650)

- [[RFC 0064] New Documentation Format for nixpkgs and NixOS_202007](https://github.com/NixOS/rfcs/pull/64)
  - This RFC proposes to convert the documentation for the Nix, Nixpkgs and NixOS projects from Docbook to CommonMark Markdown.

- There are actually **2 objections to Docbook** which we want to address: rarely anybody knows it and GitHub doesn’t render XML nicely in Github web UI
- There are 3 candidates to move from Docbook: markdown, asciidoc and RST. The last one has least supporters, but some do know it.
- Asciidoc(tor) is the most obvious choice to switch from Docbook:
  - designed from start as XML-less docbook
  - consistency check out of box
  - GitHub rendering, it has editor support 
  - machine-processable (using Ruby)
- I think Markdown is the best option because it is the most popular. The only drawback is the awkward table syntax

- I’m also a fan of Markdown: in a head-to-head comparison, it’s inferior to more structured XML-based formats, but everyone knows it, it’s dead simple to edit, it renders nicely on GitHub, it renders nicely in git diff and is therefore easy to code review
  - Aside from Google using markdown everywhere, all of Amazon’s public AWS documentation is in it, and most open source projects write docs in it – for example, all of the Rust docs
  - Another consideration is that the NixPkgs manual already has quite a bit of Markdown in it, so there’s prior art here

- I’m skeptical of Markdown and other almost-plain-text markup languages.
  - I think that they encourage writers to care about how things look, rather than what they mean, and make it a bit too easy to add formatting.
  - Markdown is also not nearly as easy to write as it might appear to be at first. The list syntax is objectively extremely confusing
  - On the contrary, a well-defined language like DocBook or even HTML makes you think about formatting and semantic meaning, and it’s difficult to do it wrong.
