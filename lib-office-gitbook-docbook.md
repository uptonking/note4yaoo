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
  - 导出格式, docx/markdown
  - 搜索与查询

- tips
  - docbook/docx描述了数据模型层， HTML/EPUB/PDF/man-pages描述了视图层，侧重点不同
  - epub不方便实现编辑

- book-formats
  - epub
  - docbook
  - markdown/asciidoc/reStructuredText-sphinx
  - gnu-texinfo
  - emacs-orgmode
  - O'Reilly HTMLBook Specification: rarely

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
  - [DocBook - Wikipedia](https://en.wikipedia.org/wiki/DocBook)
# blogs
- [Lightweight Markup: Markdown, reStructuredText, MediaWiki, AsciiDoc, Org-mode - Hyperpolyglot](https://hyperpolyglot.org/lightweight-markup)

## 💡 [Comparison of e-book formats - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_e-book_formats)

- The EPUB format is the most widely supported e-book format
  - Most e-book readers also support the PDF and plain text formats

- Open eBook (OEB), or formally, the Open eBook Publication Structure (OEBPS), is a legacy e-book format which has been superseded by the EPUB format. 
  - Open eBook is a ZIP file plus a Manifest file
  - The default file extension is .opf (OEB Package Format).

- [Write a Book with Markdown | Hacker News](https://news.ycombinator.com/item?id=36582208)
  - Being built on DocBook is a great insurance policy for Asciidoc, as DocBook has been around approximately forever and opens lots of doors to other XML specifications via XSL or something more sane.
# docbook-docs

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
# more

# discuss-epub
- ## 

- ## 

- ## 
# discuss-docbook
- ## 

- ## 

- ## 

- ## [未来有没有可能使用HTML完全替代Word，Latex等文档格式? - 知乎](https://www.zhihu.com/question/479921969)
- Office的流行，在一定程度上等于把排版的工作转嫁给写作者
- 
- 
- 
- 

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
