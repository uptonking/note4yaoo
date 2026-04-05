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
- pdfgear [Extract PDF Pages Online Free](https://www.pdfgear.com/extract-pdf-pages/)

- [JOPDF | Free & Fast PDF Editor for Windows, Mac & Linux](https://www.jopdf.com/)

- [PenguinPDF](https://grojobil.github.io/PenguinPDF/)
  - https://github.com/grojobil/PenguinPDF /NonOpen
  - Local-first PDF toolbox — free, offline, no accounts.
# pdf-reader
- foxit-reader
  - ui阅读体验更好
  - bugs
    - bookmarks在别的平台会消失，甚至导致pdf异常损坏，在别的平台打不开
# office-word

# usage-xp

- 普通视图方式 、页面视图方式 、打印预览方式 、大纲视图方式
- 普通视图方式 
  - 普通视图是Word最基本的视图方式，也是Word默认的视图方式，它可显示完整的文字格式，但简化了文档的页面布局（如对文档中嵌入的图形及 **页眉、页脚等内容就不予显示** ），其显示速度相对较快，因而非常适合于文字的录入阶段
- 页面视图方式 
  - Word的页面视图方式即直接按照用户设置的页面大小进行显示，此时的显示效果与打印效果完全一致，用户可从中看到各种对象（包括 **页眉、页脚、水印和图形等** ）在页面中的实际打印位置，这对于编辑页眉和页脚，调整页边距，以及处理边框、图形对象当分栏都是很有用的。
- 大纲视图方式 
  - 对于一个具有 **多级标题** 的文档而言，我们往往需要按照文档中标题的层次来查看文档（如只查看某重标题或查看所有文档等），此时采用前述几种视图方式就不太合适了，而大纲视图方式则正好可解决这一问题。
- 打印预览方式
  - 用于显示打印效果的打印预览（通称“模拟显示”）实际上也是Word文档视图方式中的一种，它在页面视图方式显示文档完整打印效果的基础上，增加了 **同时显示文档多个页面内容** 的功能，这就有助于用户检查文档的布局，并据此编辑或调整文档格式。注意，在打印预览方式下，用户无法修改文档中的文字信息。
# examples
- https://github.com/xournalpp/xournalpp /GPL/202502/cpp
  - https://xournalpp.github.io/
  - Xournal++ is a handwriting notetaking software with PDF annotation support. 
  - Written in C++ with GTK3, supporting Linux, macOS and Windows 10.
