---
tags: [dev/office]
title: note-dev-office
created: '2019-07-08T04:55:46.940Z'
modified: '2020-06-22T09:10:21.668Z'
---

# note-dev-office

## tips
- pdf阅读器/编辑器可参考已有解决方案
- excel阅读器/编辑器可以自己动手实现，基本数据格式比较固定

## excel

### poi  /Apache2.0
- A Java library for reading and writing Microsoft Office binary and OOXML file formats.
- 4.1.0 - 201904
- 4.0.0 - 201808
- 3.17 - 201709

## pdf

### OpenPDF /LGPL3.0/MPL2.0
- https://github.com/LibrePDF/OpenPDF
- OpenPDF is the LGPL/MPL open source successor of iText, and is based on a fork, of a fork, of iText 4.2.0 svn tag. 
- 1.2.21 - 201906

### iText - dual licensed as AGPL/Commercial software.
- iText 0.x (2000-2006)
- iText 1.x-2.x / iTextSharp 3.x-4.x (2006-2009)
  - The last release dates from 2009 (iText 2.1.7 / iTextSharp 4.1.6.0)
- iText 5.x and iTextSharp 5.x (2009-2016)
  - In 2009, the license changed from the LGPL/MPL to the AGPL
  - iTextSharp was designed as the .NET port of the library and the release numbers were synchronized at the moment iText 5.0.0 / iTextSharp 5.0.0.0 was released.
  - In Java, the library moved to Java 5.
- iText 7.x (2016-present)
  - A complete rewrite, focusing on extensibility and modularity.
  - We no longer talk about iTextSharp, but iText for Java and for .Net (C#)
  - The Java version moved to Java 7.
  - iText 7 is dual licensed as AGPL/Commercial software.
  - Buying a license is mandatory as soon as you develop commercial activities distributing the iText software inside your product or deploying it on a network without disclosing the source code

### pdfbox  /Apache2.0
- https://github.com/apache/pdfbox
- https://pdfbox.apache.org/
- 2.0.16 - 201906

### pdf viewer
- JPedal PDF library /LGPL/NOUPDATE
  - https://github.com/Lonzak/JPedal
- OpenViewerFX  /LGPL/NOUPDATE
  - https://github.com/qwertme/OpenViewerFX
  - now part of JDeli
- PDFrenderer  /LGPL/201901
  - https://github.com/katjas/PDFrenderer
  - It uses an improved version of JPedal's JBig2 decoder API.
- MuPDF  /AGPL/201909
  - https://github.com/ArtifexSoftware/mupdf
  - https://github.com/muennich/mupdf
  - written in C, providing Java JNI

## office-dev
- Apache OpenOffice
- LibreOffice
- JODConverter  /Apache2.0
  - automates document conversions using LibreOffice or Apache OpenOffice
