---
title: spec-office-pdf-ofd
tags: [format, ofd, office, pdf, spec]
created: 2026-04-05T18:13:02.564Z
modified: 2026-04-05T18:34:12.403Z
---

# spec-office-pdf-ofd

# guide

- pros
  - ?

- cons
  - ?

- features
  - ?

- tips
  - ?
# faq

- 
- 
- 
- 
- ## for any arbitary pdf file, how to check if it is text pdf or scanned image pdf?
- 
- 
- 
- 

# summary

- 

# dev-tips

- 
- 
- 

- PDF uses bottom-left origin, but browsers use top-left

- 
- 
- 
- 

# spec

- 

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
# spec-ofd
- [中国人自己的“PDF”版式文档格式：OFD （哪些软件能打开这种格式？） - 知乎](https://zhuanlan.zhihu.com/p/1932328214493115870)
  - WPS, 福昕阅读器, 永中OFD版式软件, 友虹可信版式阅读软件, 数科阅读器, 点聚OFD
# discuss-pm-pdf
- ## 

- ## 

- ## 

- ## 

- ## [So you want to parse a PDF? | Hacker News _202508](https://news.ycombinator.com/item?id=44780353)
  - The author of the blog works on PdfPig, a framework to parse PDFs. For its document understanding APIs, it uses a hybrid approach that combines basic image understanding algorithms with PDF metadata .  https://github.com/UglyToad/PdfPig/wiki/Document-Layout-Analysis
- Great rundown. One thing you didn't mention that I thought was interesting to note is incremental-save chains: the first startxref offset is fine, but the /Prev links that Acrobat appends on successive edits may point a few bytes short of the next xref. Most viewers (PDF.js, MuPDF, even Adobe Reader in "repair" mode) fall back to a brute-force scan for obj tokens and reconstruct a fresh table so they work fine while a spec-accurate parser explodes. Building a similar salvage path is pretty much necessary if you want to work with real-world documents that have been edited multiple times by different applications.
  - You're right, this was a fairly common failure state seen in the sample set. The previous reference or one in the reference chain would point to offset of 0 or outside the bounds of the file, or just be plain wrong.
  - What prompted this post was trying to rewrite the initial parse logic for my project PdfPig. I had originally ported the Java PDFBox code but felt like it should be 'simple' to rewrite more performantly. The new logic falls back to a brute-force scan of the entire file if a single xref table or stream is missed and just relies on those offsets in the recovery path. However it is considerably slower than the code before it and it's hard to have confidence in the changes. I'm currently running through a 10, 000 file test-set trying to identify edge-cases.

- As someone who has written a PDF parser - it's definitely one of the weirdest formats I've seen, and IMHO much of it is caused by attempting to be a mix of both binary and text; and I suspect at least some of these weird cases of bad "incorrect but close" xref offsets may be caused by buggy code that's dealing with LF/CR conversions. What the article doesn't mention is a lot of newer PDFs (v1.5+) don't even have a regular textual xref table, but the xref table is itself inside an "xref stream", and I believe v1.6+ can have the option of putting objects inside "object streams" too.
  - Yeah I was a little surprised that this didn't go beyond the simplest xref table and get into streams and compression. Things don't seem that bad until you realize the object you want is inside a stream that's using a weird riff on PNG compression and its offset is in an xref stream that's flate compressed that's a later addition to the document so you need to start with a plain one at the end of the file and then consider which versions of which objects are where. Then there's that you can find documentation on 1.7 pretty easily, but up until 2 years ago, 2.0 doc was pay-walled.
- Yeah, I was really surprised to learn that Paeth prediction really improves the compression ratio of xref tables a lot!

- Yeah, PDF didn't anticipate streaming. That pesky trailer dictionary at the end means you have to wait for the file to fully load to parse it.
  - there are Linearized PDFs which are organized to enable parsing and display of the first page(s) without having to download the full file. I skipped those from the summary for now because they have a whole chunk of an appendix to themselves.
- Streaming with a footer should still be possible if your website is capable of processing range requests and sets the content length header. A streaming PDF reader can start with a HEAD request, send a second request for the last few hundred bytes to get the pointers and another request to get the tables, and then continue parsing the rest as normal.
  - Not great for PDFs generated at request time, but any file stored on a competent web server made after 2000 should permit streaming with only 1-2 RTT of additional overhead.
  - Unfortunately, nobody seems to care for file type specific streaming parsers using ranged requests, but I don't believe there's a strong technical boundary with footers.

- Founder of Tensorlake, we built a Document Parsing API for developers. 
  - This is exactly the reason why Computer Vision approaches for parsing PDFs works so well in the real world. Relying on metadata in files just doesn't scale across different source of PDFs.
  - We convert PDFs to images, run a layout understanding model on them first, and then apply specialized models like text recognition and table recognition models on them, stitch them back together to get acceptable results for domains where accuracy is table stakes.
- PDFs are intended to produce an output that is consumed by humans and not by computers, the format seems to be focused on how to display some data so that a human can (hopefully) easily read them. It is sad though that in 30+ years we didn't manage to add a consistent way to include a way to make a PDF readable by a machine. I wonder what incentives were missing that didn't make this possible. Does anyone maybe have some insight here?
  - 1. It's extra work to add an annotation or "internal data format" inside the PDF.
  - 2. By the time the PDF is generated in a real system, the original data source and meaning may be very far off in the data pipeline. It may require incredible cross team and/or cross vendor cooperation.
  - 3. Chicken and egg. There are very few if any machine parseable PDFs out there, so there is little demand for such.
  - I'm actually much more optimistic of embedding meta data "in-band" with the human readable data, such as a dense QR code or similar.
- Probably for the same reason, images were not readable by machines. Except PDFs dangle(悬挂; 诱惑) hope of maybe being machine-readable because they can contain unicode text, while images don't offer this hope.
- PDF supports all the necessary features, like structure tags. You can create a PDF with the basically the same structural information as an HTML document. The problem is that most PDF-generating workflows don’t bother with it, because it requires care and is more work.
  - And yes, PDF was originally created as an input format for printing. The “portable” in “PDF” refers to the fact that, unlike PostScript files of the time (1980s), they are not tied to a specific printer make or model.

- Almost every place I've worked at has complained about the parsability of PDF files until I showed them LibreOffice's PDF export feature, that supports PDF/A (arciveable), PDF/UA (Universal Accessibility), and embedding the original .odt file in the PDF itself. That combo format has saved so many people so much headache, I don't know why it is not more widely known.

- PDFs are primarily a way to describe print data. So to a certain extent the essence of PDF is a hybrid vector-raster image format. Sure, these days text is almost always encoded as or overlaid with actual machine-readable text, but this isn't really necessary and wasn't always done, especially for older PDFs. 15 years ago you couldn't copy (legible) text out of most PDFs made with latex.

- One of the biggest benefits of PDFs though is that they can contain invisible data. E.g. the spec allows me to embed cryptographic proof that I've worked at the companies I claim to have worked at within my resume. But a vision-based approach obviously isn't going to be able to capture that.

- There's a huge difference between parsing a PDF and parsing the contents of a PDF. Parsing PDF files is its own hell, but because PDFs are basically "stuff at a given position" and often not "well-formed text within boundary boxes", you have to guess what letters belong together if you want to parse the text as a word.

- An alternative approach would be to adopt a very simple 'machine first', or 'content first' format - for example, based on JSON, XML, even HTML - with minimum metadata to support strurcture, intra-document links, and embedding of images. 
  - For human comsumption, a simple viewer app would reconstitute the file into something more readable; for machine consumption, the content is already directly available. 
  - I'm well aware that such formats already exist - HTML/browsers, or EPUB/readers, for example - the issue is to take the rational step towards adopting such a format in place of the legacy alternatives.
- is docx really that bad in practice? I have not implemented a parser for it so I’m not pushing one answer to that. But it seems like it’s an XML-based format that isn’t about absolutely positioning everything unless you explicitly decide to, and intuitively it seems like it should be like an 80 on the parsing easiness scale if a JPEG is a 0, a PDF is a 15, and a markdown is 100.
- Extracting text from DOCX is easy. Anything related to layout is non-trivial and extremely brittle. To get the layout correct, you need to reverse engineer details down to Word's numerical accuracy so that content appears at the correct position in more complex cases. People like creating brittle documents where a pixel of difference can break the layout and cause content to misalign and appear on separate pages.

- Tagged PDF can represent document structure with a decent variety of elements, including alternative text for objects. Proper text encoding can give a good representation of all the ligatures and such. All of this is a part of the spec since 2001. The fact that modern software produces PDFs that are barely any better than a series of vector images is totally on the producers of that software.

- I think a PDF 2.0 would just be an extension of a single file HTML page with a fixed viewport

- you can "just" enforce pdf/a
  - ...well there is like 50 different pdf/a versions; just pick one of them
# discuss-tools/conversions
- ## 

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

- ## [Html to Pdf library suggestions : r/Python _202601](https://www.reddit.com/r/Python/comments/1q74ivt/html_to_pdf_library_suggestions/)
- playwright is probably the best one even though it's heavier since it needs to run a browser in headless mode
  - for css and images you are gonna have the same problem independently on the library you are using
  - if these styles and images are just static files that don't require authentication you can just use the full url in the template

- Personally, I've given up trying to tame these HTML->PDF beasts. I rather create a Word-file which the user later can print/convert to PDF if they so require. It's so much easier (imho).

- I actually usually write a tiny wrapper around a statically compiled wkhtml2pdf binary. Works great, gives some control, and is VERY simple and easy. 

- If your html is not too complicated, wkhtmltopdf.
  - I think that if you want reliable rendering your best option is always going to be a headless browser. In which case you should look at pyppeteer.

- [Html to Pdf library suggestions : r/django](https://www.reddit.com/r/django/comments/1q74j4u/html_to_pdf_library_suggestions/)
  - I think that if you want reliable rendering your best option is always going to be a headless browser. In which case you should look at pyppeteer.
# discuss-ofd
- ## 

- ## 

- ## 

- ## 

- ## [国家去年(2016)发布了中国版式文件标准（OFD），并且开始在党政军开始推广，市场前景如何？ - 知乎](https://www.zhihu.com/question/65579070)

- 国家版式文档格式 即 开放固定版式文档（Open Fixed-layout Documents，OFD），是依照中国国家标准自主研发的一种电子文件格式。OFD标准基于XML对版式进行描述，与OOXML、ODF及UOF采用的为同一种框架；支持使用商用密码进行加密，与便携式文档格式（PDF）为竞争关系。与PDF相比，OFD格式较为简单，易于实现。
- 国家版式文档格式从2011年开始立项，历时五年完成最终标准。2016年10月14日，中国国家标准化管理委员会正式发布：GB/T 33190-2016《电子文件存储与交换格式 版式文档》。
- OFD类似微软的OpenXPS，都是静态文档格式。
  - OpenXPS全称“ Open XML Paper Specification ” (开放式XML文件规范)，它是微软公司开发的一种文档保存与查看的规范。OpenXPS是一个静态文档格式，其本身不包括类似于PDF所具有的动态
- OFD的前景可以参照UOF： 统一办公文档格式（英语：Uniform Office Format，中文简称“标文通”）是一种基于XML语言的中文办公软件文档格式，支持文字处理、电子表格和演示文稿等应用。
  - 2002年，由红旗中文2000、金山、永中、中标等中国办公软件企业以及中国科学院软件研究所等科研院所组成了中文办公软件工作组，推出中国标准UOF。
  - 2007年4月，UOF获批成为中国国家标准GB/T20916-2007，即由中国国家电子政务总体组所属的中文办公软件基础标准工作组组织制定的《中文办公软件文档格式规范》标准。

- 先不评价格式本身。 看看网上找到一个 绿色、无广告、无木马，不诱导消费、不捆绑其他程序的 OFD文件查看工具 难度有多大吧。 我的直观感受，这里面的利益关系，不输文件的加密算法

- 应该大力推广各客户端兼容OFD预览，比如微信、邮件客户端、WPS、浏览器等这些客户端，先解决能预览的问题，慢慢的用的人就多了

- 本质上OFD跟XLSX是一样的底层，但厂家不愿做。

- 
- 
- 
- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

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
