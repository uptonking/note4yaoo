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
# ref
