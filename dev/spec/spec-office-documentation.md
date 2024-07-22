---
title: spec-office-documentation
tags: [documentation, format, office, spec]
created: 2020-12-16T12:41:16.245Z
modified: 2021-09-30T07:44:05.964Z
---

# spec-office-documentation

# office-formats

- open office xml
  - .docx
  - .xlsx
  - .pptx

- markdown
- rst
- asciidoc

- [Why OpenDoc failed, and then failed 3 more times?_202105](https://instadeq.com/blog/posts/why-opendoc-failed-and-then-failed-3-more-times/)
# RTF: Rich Text Format

## [.rtf文件, .doc文件，和.docx有何异同？ - 知乎](https://www.zhihu.com/question/31945498/answers/updated)

- 有了RTF，又想加增强的功能旧的也得兼容啊，新创建个格式叫DOC吧。
  - DOC也不够华丽了，跟不上时代了啊，再做个DOC加强版叫DOCX吧！

- RTF是富文本格式，又称为多文本格式，是由微软公司开发的跨平台文档格式，一种类似DOC格式的文件。
  - 它能够保存各种格式信息，如文字粗体，斜体，不同的字体和字体大小以及各种选项设置，也支持保存在文本文件中的对象和图像，例如JPG和PNG文件。
- 优势
  - 通用兼容性是RTF的最大优点，它可以实现多平台的信息兼容。在不同的操作系统下创建的RTF文件可以在多种操作系统和应用程序之间互相传送、查看，大多数的文字处理软件都能读取和保存RTF文档。
- 劣势
  - 文件一般相对较大，WORD等应用软件特有的格式可能无法正常保存
- RTF 是一种类似 TeX 的宏格式，貌似是收到 TeX 启发以后撸的。你用记事本打开看看就知道了

- DOC是微软出品的Word98、Word2000、WordXP、Word2003等默认保存的后缀格式名称。
  - 软件适配的word版本更多，能打开DOCX格式就一定能够打开DOC，并且默认不进行图片压缩
  - DOC文件以**二进制**格式储存文档，文件过大响应速度慢

- DOCX文件是Microsoft Office 2007之后版本使用的，是用新的基于**Open XML**压缩文件格式创建，取代了原来使用二进制文件格式存储数据的DOC文件。
  - 这意味着DOCX 基本上是一个 zip 文件，其中包含与文档相关的所有XML文件。
  - 如果将 DOCX 扩展名替换为 ZIP，则可以使用任何 zip 压缩软件轻松打开它并查看或更改 XML 文档。
  - DOCX和DOC相比，同样的文件体积更小，对复杂对象的处理也更好
  - Microsoft Word 2007之前的版本不支持打开阅读，在共享文件方面具有劣势，需要安装微软推出的Office兼容性补丁包
# pdf

## [PDF - Wikipedia](https://en.wikipedia.org/wiki/PDF)

- Portable Document Format (PDF), standardized as ISO 32000, is a file format developed by Adobe in 1992 to present documents, including text formatting and images, in a manner independent of application software, hardware, and operating systems.
  - Based on the PostScript language, each PDF file encapsulates a complete description of a fixed-layout flat document, including the text, fonts, vector graphics, raster images and other information needed to display it.
  - PDF was a proprietary format controlled by Adobe until it was released as an open standard on July 1, 2008
  - A PDF file is often a combination of vector graphics, text, and bitmap graphics. 
  - In later PDF revisions, a PDF document can also support links (inside document or web page), forms, JavaScript (initially available as a plugin for Acrobat 3.0), or any other types of embedded contents that can be handled using plug-ins.
  - PostScript is a page description language run in an interpreter to generate an image.
    - PDF is a subset of PostScript, simplified to remove such control flow features, while graphics commands remain.
- A PDF file is organized using ASCII characters, except for certain elements that may have binary content. The file starts with a header containing a magic number (as a readable string) and the version of the format, for example %PDF-1.7. 
- There are two layouts to the PDF files: non-linearized (not "optimized") and linearized ("optimized"). 

## [The Structure of a PDF File. Introduction | by Jay Berkenbilt | Medium](https://medium.com/@jberkenbilt/the-structure-of-a-pdf-file-6f08114a58f6)

- A PDF file is an indexed collection of objects. A PDF object is a chunk of structured data
  - A PDF file consists of a header, a bunch of object definitions, a cross-reference table, and a trailer. The cross-reference table is a lookup-table that provides the location of each numbered object as a byte offset within the file. The trailer provides information about the root object, or document catalog, which is the starting point for interpreting the PDF file. At the end of the file, there is a byte offset to the cross reference table.

- a PDF file must be seekable — that is, the reader must be able to read a portion of the file starting from a given byte offset into the file. The PDF file format is designed such that you can immediately display the part of the file you’re interested in without having to read the parts you’re not interested. This is one of the most important goals of the PDF format.

- When a PDF viewer interprets a PDF file, it starts by going to the end of the file. The last thing in the PDF file is the byte offset to the cross-reference table. The cross-reference table contains the location in the file of each object along with the trailer dictionary
# ref
