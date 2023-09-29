---
title: tool-office-pdf-xp
tags: [office, pdf, tool, xp]
created: 2020-09-23T03:00:38.971Z
modified: 2020-12-29T17:52:48.584Z
---

# tool-office-pdf-xp

# pdf-studio

- 编辑功能强大

- bugs
  - 高亮后的颜色可能不同，在win平台或使用不同的pdf阅读软件如acrobat

- tips
  - pdf-editor参考: acrobat, libre-draw, scribus, inkscape, master, pdf-studio, pdf-sam, edge浏览器, os自带工具
  - pdf-viewer或标注参考: okular, foxit, canva, xournal, 各类电子书阅读器

- 画板或批注类产品要参考规范 [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/)
# foxit-reader
- ui阅读体验更好

- bug
  - bookmarks在别的平台会消失，甚至导致pdf异常损坏，在别的平台打不开
# office-word

# usage-xp

- 普通视图方式 、页面视图方式 、打印预览方式 、大纲视图方式
- 普通视图方式 
  - 普通视图是Word最基本的视图方式，也是Word默认的视图方式，它可显示完整的文字格式，但简化了文档的页面布局（如对文档中嵌入的图形及**页眉、页脚等内容就不予显示**），其显示速度相对较快，因而非常适合于文字的录入阶段
- 页面视图方式 
  - Word的页面视图方式即直接按照用户设置的页面大小进行显示，此时的显示效果与打印效果完全一致，用户可从中看到各种对象（包括**页眉、页脚、水印和图形等**）在页面中的实际打印位置，这对于编辑页眉和页脚，调整页边距，以及处理边框、图形对象当分栏都是很有用的。
- 大纲视图方式 
  - 对于一个具有**多级标题**的文档而言，我们往往需要按照文档中标题的层次来查看文档（如只查看某重标题或查看所有文档等），此时采用前述几种视图方式就不太合适了，而大纲视图方式则正好可解决这一问题。
- 打印预览方式
  - 用于显示打印效果的打印预览（通称“模拟显示”）实际上也是Word文档视图方式中的一种，它在页面视图方式显示文档完整打印效果的基础上，增加了**同时显示文档多个页面内容**的功能，这就有助于用户检查文档的布局，并据此编辑或调整文档格式。注意，在打印预览方式下，用户无法修改文档中的文字信息。
# examples
- https://github.com/xournalpp/xournalpp /cpp
  - https://xournalpp.github.io/
  - Xournal++ is a handwriting notetaking software with PDF annotation support. 
  - Written in C++ with GTK3, supporting Linux, macOS and Windows 10.
# discuss
- ## 

- ## 

- ## 一个冷知识： 有些pdf文件加了密码限制编辑操作（就是你可以看不能改）， 
- https://twitter.com/syeerzy/status/1692413182202327198
  - 从pdf的文件格式标准来看，实际上“限制编辑”是不可能完成的， 因此这个功能其实是需要 “编辑软件” 和 “pdf文件” 串通一起完成，
  - 因此只需要一个不支持此特性的pdf工具就能完美绕过
- 最简单的不支持此特性的工具就是“打印机驱动” 
  - 无须安装，不管macOS还是Windows，你都很容易“打印”一个限制编辑的pdf文件， 在弹出的打印窗口里，你都可以选择“保存为pdf” （不同操作系统版本描述略不同） 
  - 这个新的pdf就是没有限制编辑的。

- ## [Why is There a Lack of Open-Source PDF Editor Options?](https://www.reddit.com/r/opensource/comments/uoxbmn/why_is_there_a_lack_of_opensource_pdf_editor/)
  - a few basic tasks: page manipulation, drawing, inserting text and images, filling out forms, and redactions. 
  - The general consensus from that thread is that there is no one free tool that does all of those, and several responders mentioned using a combination of tools.
  - I would imagine that such an editor would be low-hanging fruit for open-source development, especially when we have powerful open-source alternatives for things like Microsoft Office and the rest of the Adobe suite. Why does an open-source alternative to Adobe Acrobat Pro not exist

- PDF is a decent output format. 
  - It's not very great as a working format. 
  - PDF often uses proprietary things like fonts. Fonts are one of the most difficult things to "replicate" without licensing the real actual fonts. 
- PDF is also a container format. 
  - It can build a document from many types of underlying layers all the way from fully typeset text and vectorized images up to simple page scans of entire pages stitched(缝合，编结) together.
- If you want to explore PDFs, open them with Inkscape and check out what actually makes up the content. What looks like text is often bitmapped, graphics are often jigsaws of multiple images etc etc.

- Why would that be an issue for creating a PDF editor?
  - Because the output from the source material might do things like place individual glyphs on the page to get correct kerning/justification/object placement. You don't have a page of words in order, you have letters located on a page, and those letters may not be in order. Or it might be a mix of partial words and letters or letter combination glyphs.

- Most PDF output writers do use postscript programming routines (Postscript is also a type of programming language) to avoid that sort of behavior, but it isn't always the case. PDF editors need to be Postscript interpreters, and try to reduce some of that complexity into editable data.

- LibreOffice is great at creating PDFs, but I've found that when I try to open and manipulate existing PDFs, everything gets corrupted. LibreOffice doesn't seem to preserve fonts, layouts, spacing, etc.
  - Inkscape can only do one page at a time, and it has problems similar to LibreOffice.

- ## [Open-Source PDF viewer and editor](https://www.reddit.com/r/opensource/comments/dej32w/opensource_pdf_viewer_and_editor/)
- LibreOffice Draw allows you to view and edit PDFs. You can also use Firefox as a PDF(pdfjs) viewer

- LibreOffice can edit PDF files, but will often corrupt formatting in my experience. 
  - Xournal has a different approach, where it keeps the original document as-is and you can only add text/graphics on top of it. 
  - I don't believe there is anything open-source that will do *everything* Adobe Acrobat can do.

- Okular is the best I used so far.
  - It's developed by KDE but recently they made a release for Microsoft
  - Viewing and annotation only though.

- To make radical changes to a PDF I use Inkscape. And for viewing I use Okular on KDE and Evince on Gnome.
  - Inkscape only works on single-page PDFs. It now works on multipage PDFs - just tried it today (June 29, 2022)

- with PDFSAM you can merge, split, extract and do other things. It's open-source.
  - Worth noting you can't view a pdf with this tool. Only edit it

- LaTeX: Am I a joke to you?

- Sejda PDF Desktop it's really good
  - Sejda PDF Desktop is free to use with daily limits.
  - 3 tasks per day
