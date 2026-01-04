---
title: tool-office-pdf-xp
tags: [office, pdf, tool, xp]
created: 2020-09-23T03:00:38.971Z
modified: 2020-12-29T17:52:48.584Z
---

# tool-office-pdf-xp

# guide

- tips
  - pdf-editor参考: acrobat, libre-draw, scribus, inkscape, master, pdf-studio, pdf-sam, edge浏览器, os自带工具
  - pdf-viewer或标注参考: okular, foxit, canva, xournal, 各类电子书阅读器
  - 在浏览器查看markdown时使用print pdf功能，linux的效果比macos好很多，比如简历markdown

- pm-pdf
  - 为扫描版书本自动添加目录toc: 目录内容为手动复制或自动检测, 然后自动关联到正文位置
  - 对常见的多栏布局文本化适合较为固定的场景

- 双栏布局对pdf特别有用，一方面在屏幕展示更多内容， 另一方面是利用双栏ux实现同步滚动 原文 和 翻译/评论 2个独立但位置相关的内容
  - 多栏布局的场景: 类似markdown文本, overleaf富文本编辑, 文字版pdf, 图片版pdf
  - 实现思路1: editor-suggestion
  - 实现思路2: two-doc-scroll
  - ✨ pdf-viewer很少实现多个独立文档的共用导航目录的交互, 在翻译/校对场景很有用
- pdf-布局
  - overleaf的Visual Editor支持以富文本的形式编辑内容，但布局与右侧预览的pdf不同，是简化版的布局和样式
    - 仍显示latex文本形式的表示，而不是图形形式
    - 未显示分页
    - 表格更简单，但表格能可视化编辑内容

- 画板或批注类产品要参考规范 [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/)
# draft
- 基于 AI 的pdf review/suggestions

- ⚖️ 支持中国知网的 caj 格式

- 
- 

# pdf-studio
- 编辑功能强大

- bugs
  - 高亮后的颜色可能不同，在win平台或使用不同的pdf阅读软件如acrobat
# pdf-editor
- [JOPDF | Free & Fast PDF Editor for Windows, Mac & Linux](https://www.jopdf.com/)
# pdf-reader
- foxit-reader
  - ui阅读体验更好
  - bugs
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
- https://github.com/xournalpp/xournalpp /GPL/202502/cpp
  - https://xournalpp.github.io/
  - Xournal++ is a handwriting notetaking software with PDF annotation support. 
  - Written in C++ with GTK3, supporting Linux, macOS and Windows 10.
# discuss
- ## 

- ## 

- ## 

- ## 强烈推荐这篇文章：《深入探索：AI 驱动的 PDF 布局检测引擎源代码解析 [译]》
- https://twitter.com/dotey/status/1734129116167729596
  - 系统的分析了最近很火的 PDF 转 Markdown 开源程序 Marker 的工作原理，比我想象的要复杂不少，用了好几个开源库。
  - https://github.com/VikParuchuri/marker
  - [Inside Marker: A Guided Source Code Tour for an AI-powered PDF Layout Detection Engine_202312](https://journal.hexmos.com/marker-pdf-document-ai/)
- Marker 主要通过以下六个阶段来工作：
  1. 准备阶段： 利用 PyMuPDF 工具，可以把各种格式的文档转换成 PDF 文件。
  2. 文本识别（OCR）： 使用 Tesseract 或 OCRMyPDF 进行文字识别；也可以选择用 PyMuPDF 进行基本的文字抓取。
  3. 布局识别： 运用专门定制的 LayoutLMv3 模型 来识别文档中的表格、图表、标题、图说、页眉和页脚。
  4. 列的检测和排序： 再用一个定制的 LayoutLMv3 模型来识别文档中的列，并按照正确的顺序（上到下，左到右）进行排列。
  5. 公式/代码处理： 通过 Nougat 工具，把公式图片转换成对应的 latex 代码，并利用启发式方法准确识别和调整代码及表格内容。
  6. 文本清理与优化： 使用定制的 T5ForTextClassification 模型进行文本清理，比如去掉不必要的空格和奇怪的字符，确保以一种保守且保留原意的方式进行优化。
  - 借助这六个阶段，Marker 能够把任何文档转化为格式整洁的 Markdown 文件。

- 这跟我的企业知识库产品的处理流程几乎一样，看来大家殊途同归，没有高效的解决办法，只能搞这种缝合怪

- 试了下，效果也没这么好。
  - markdown格式下表格的不能太复杂，比如colspan和\n字符的问题，还是html稍微好些。
  - 识别pdf表格，Marker用的是Pymupdf，但是这个工具对表格的解析没有Camelot好。针对pdf表格里面的colspan，我没发现完美的解决方案，目前最好的是Camelot和Nougat
- 针对表格，Camelot和Pymupdf都是识别表格成二维list，转pandas DataFrame，再用pandas built-in方法转为markdown表或者html表格，自然无法处理colspan的问题。

- 用了呀，问题是这玩意也太慢了，在 macbook 上用 mps 也要十分钟左右

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
