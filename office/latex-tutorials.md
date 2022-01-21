---
title: latex-tutorials
tags: [latex]
created: '2021-10-25T00:05:49.275Z'
modified: '2021-10-25T00:20:04.009Z'
---

# latex-tutorials

# guide

# latex

## [LaTeX入门指南|新手速进](https://www.zhihu.com/zvideo/1421078748670566400)

- 编辑器
  - 侧边菜单栏：文件、图片
  - 编辑区
  - 预览区

- latex方便制作模版

- 命令[可选参数]{必选参数}
- \newenvironment{自定义环境}开始代码
  - 方便分离格式排版和内容

- 论文基本结构
  - 导言部分
  - 正文部分
  - 参考文献

- 空行会另起一段，多个空行不会增加行间距
- 换行不会另起一段
- 中文间的空格不会渲染，英文间空格会渲染出来

- 图片和表格属于浮动体，是为了不合理的分页

- 数学公式
  - 行内公式
  - 行间公式

- 参考文献 
  - 方法1： 新建.bib输入参考文献信息，然后在.tex文件中使用\bibliography
    - 如何将参考文献加入目录
    - BIBTEX程序在生成参考文献列表的时候，通常只列出用了\cite 命令引用的那些。
    - 如果需要列出未被引用的文献，则需要 \nocite{ ⟨ citation ⟩ } 命令； 而 \nocite{*} 则让所有未被引用的文献都列出。
  - 方法2： 手动输入bib信息

- 交叉引用
# bibtex
- 关于中文参考文献格式
  - https://github.com/zepinglee/gbt7714-bibtex-style
    - 支持“顺序编码制”和“著者-出版年制”两种风格。
    - 提供了 2005 版的 .bst 文件。
  - https://github.com/hushidong/biblatex-gb7714-2015
    - A biblatex implementation of the GB/T7714-2015 bibliography style
    - biblatex-gb7714-2015 宏包是中文参考文献著录/标注标准 GB/T 7714-2015 的 biblatex 实现
    - 它本质上是一个样式包，提供了顺序编码制和著者年份制样式，在 tex 文档中配合 biblatex 宏包使用

## [使用 BibTeX 生成参考文献列表](https://liam.page/2016/01/23/using-bibtex-to-generate-reference/)

- BibTeX 是一个参考文献格式化工具，它会根据需要，按照（bst文件规定的）某种格式，将（bib文件中包含的）参考文献信息，格式化为 LaTeX 能够使用的列表信息。
- BibTeX 涉及到两种特有的辅助的文件格式：bst 和 bib。
  - bst 是 (B)ibliography (ST)yle 的缩写。 bst 文件控制着参考文献列表的格式。
    - 在这里说的「格式」，主要指参考文献列表中的编号、排序规则、对人名的处理（是否缩写）、月份的处理（是否缩写）、期刊名称的缩写等。
  - bib 是 BibTeX 定义的「参考文献数据库」。通常，我们会按照 BibTeX 规定的格式，向 bib 文件写入多条文献信息。
    - 实际排版出来的参考文献列表中有多少条文献，实际是哪几条，具体由文中使用的 \cite 命令（以及 \nocite 命令）指定。
- BibTeX 不是用来排版参考文献的，更不是个排版工具，
  - 它只是根据需要，按照（bst文件规定的）某种格式，将（bib文件中包含的）参考文献信息，格式化为 LaTeX 能够使用的列表信息。
  - 正确使用 BibTeX 处理参考文献，需要先用 (Xe/PDF)LaTeX 编译 tex 文件，生成 aux 辅助文件。
  - BibTeX 正是通过读取 aux 文件中的 \citation{} 标记，来确定用户需要哪些参考文献的。
  - 当 BibTeX 读入 aux 文件的时候，它就会记录下所有 \citation 命令中的内容（即文献标记——label），这样就知道了用户需要哪些参考文献信息。
  - LaTeX 需要 aux 文件中的 \bibcite 命令，将参考文献标记与参考文献编号关联起来，从而在 tex 文件中的 \cite 命令位置填上正确的参考文献编号
  - \bibliography 命令则用 \bibdata 在 aux 文件中记录了参考文献数据库的名字（不含扩展名）
  - tex 文件中的 \bibliographystyle 指定了用户期待的参考文献列表格式文件，并将其写入 aux 文件备用，通过 \bibstyle 标记
- .bbl就是 BibTeX 格式化输出的结果，LaTeX 只需要将该文件的内容读入，就能在相应的位置输出格式化之后的参考文献列表了。
  - thebibliography 环境正是 LaTeX 中手工编排参考文献时使用的环境
  - .blg 实际是 BibTeX Log 的缩写，即这是一个日志文件
- BibTeX 可能支持两个或更多的 bib 数据库共同工作
# ref
- https://bithesis.bitnp.net/
  - BIThesis 是针对北京理工大学本科同学毕业设计、毕业论文制作的一个非官方的 LaTeX 模板，BIThesis 同时也包括其他本科学习中涉及到的文献综述、实验报告等的 LaTeX 模板。

- [BibTeX Format Description](http://www.bibtex.org/Format/)
  - [A complete guide to the BibTeX format](https://www.bibtex.com/g/bibtex-format/)

- repo
  - https://github.com/ORCID/bibtexParseJs
  - https://github.com/retorquere/bibtex-parser
    - A node/npm package for parsing bibtex (.bib) files. This is the parser that drives Better BibTeX for Zotero bib(la)tex imports.

- [A summary of BibTex](https://maverick.inria.fr/~Xavier.Decoret/resources/xdkbibtex/bibtex_summary.html)
  - you can have a valid BibTex file that is correctly parsed but produce no output with the standard style files (e.g. alpha.bst) 
    - because this styles expects standards field names such as author, title for example.
  - When two ore more entries have the same key, only the first is retained, the other ones are skipped. 
    - Same thing if there are several fields with the same name. 
    - In both situations, equality is case insensitive.
  - BibTeX splits the file in two areas: inside an entry and outside an entry, the delimitation being indicated by the presence of a `@` sign. 
    - When this character is met, BibTex expects to find an entry as described above. 
    - Before that sign, and after an entry, everything is considered a comment! 
    - The advantage of this definition of comment is that you can quickly "comment" an entry by simply removing the `@` at the beginning.
  - BibTeX actually offers another way to comment a part of the file. 
    - If the entry type is `@Comment`, is is not considered to be the start of an entry. 
    - (Actually, the rule is that everything from the `@Comment` and to the end of line is ignored.
  - A side effect of the very strong meaning of the `@` sign in the file format is that when BibTex encounters an error in an entry (as a missing coma between two fields, or an unbalanced braced expression), it is able to recover rather well by skipping everything until the next `@` sign.

- https://github.com/CTeX-org/zhlipsum
  - 本宏包提供了中文乱数假文的功能，可用于测试中文LaTeX文档， 支持UTF-8、GBK和Big5编码。
