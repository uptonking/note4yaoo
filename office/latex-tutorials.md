---
title: latex-tutorials
tags: [latex]
created: 2021-10-25T00:05:49.275Z
modified: 2021-10-25T00:20:04.009Z
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

## [使用Latex写论文](https://xsliulab.github.io/Workshop/week36/%E4%BD%BF%E7%94%A8Latex%E5%86%99%E8%AE%BA%E6%96%87.html)

- LaTex的基本框架：整个代码内容分两块
  1. Preamble。写在最前面的引导语，用来定义基本设置，如页面大小，页边距，字体和大小，页眉页脚，章节和段落格式，参考文献的格式，Figure和Table的标题格式，还有主程序需要用的程序包。标题和作者信息也可以用maketitle代码写在preamble里，设置好字体格式，然后在主程序里直接引用和maketitle即可。几乎所有重要设置和命令模块化都在preamble里完成。
  2. 主程序从\begin{document}到\end{document}，所有manuscript内容将写入里面。内容又分各章节，引用preamble里设置好的章节标题格式，再接着写正文即可。后面设置Figure和Table。每个Figure和Table是一个模块。主程序主要用于写入正文，以及通过一些命令的调用，来调整格式。

- 在LaTex中，所有在document内容之前的都称为preamble, 
  - 在preamble中可以定义整个文档的格式、使用的语言、你需要使用到的宏包、以及其他的元素。

- [自学Latex——Manuscript排版入门](https://zhuanlan.zhihu.com/p/66937047)

- [latex中cls和sty文件](https://www.jianshu.com/p/12b4a4b3afce)
  - .cls 和 .sty 文件都是增加 LaTeX 功能的补足文件。它们在我们排版文章是时对应的使用 \documentclass{} 和 \usepackage{} 加载，在包内部则对应的使用 \LoadClass, \LoadClassWithOptions 和 \RequirePackage, \RequirePackageWithOptions 加载。我们通常将 .cls 文件称之为类（classes）文件，将 .sty 文件称之为风格（style）文件或者包（package）。
  - 虽然它们都可以包含任意的 TeX 和 LaTeX 代码，但是它们的使用方式不同。我们必须通过 \documentclass 加载一个类文件，并且在一个 LaTeX 文件中只能出现一次，通常也是第一个出现的命令。而另一方面，包是一个可选项，它可以根据我们的需求加载任意多个（在开始文档之前）。
  - 如果一个命令是用来控制文档结构的，则应该放到类文件中；否则应该放到包文件中。

## [参考文献那些事 BibTeX、Natbib、BiblateX、biber、Better Bib(La)TeX、bst、bbl、bib、ris、csl、sty、cls…](https://yufree.cn/cn/2018/10/22/reference/)

- 严格说csl跟pandoc没啥关系，是一套基于xml的引文与列举文献样式的定义，现在主流期刊的定义都能查到，也被 Zotero、 Mendelay 与 papers 这三大文献管理工具所支持。只不过pandoc在处理格式转换时用了csl。
  - 当然，需要事先说明的是，pandoc可以进行基于natbib与biblatex的LaTeX相关格式转换的。
  - 但很明显csl更简单明了，需要什么期刊就用对应csl编译就可以了，Rmarkdown 就支持这个转换的，在Yaml里写好用什么csl文件就可以了

- 总结一下：
  - 参考文献的排版需要考虑引用格式与文末文献排列格式
  - BibLatex 同时支持 bibtex 与 biber 后端，natbib 只支持 bibtex 后端
  - 建议使用 biblatex 而不是 bibtex 来排版 tex 文档
  - csl 可以实现参考文献的轻量级排版，可配合 pandoc 使用
  - Rstudio + citr + Zotero + rticles 是个不错一站式 Rmarkdown 论文写作方案
  - 超轻量级的文献排版可以直接考虑DOI与超链接
# bibtex
- 关于中文参考文献格式
  - https://github.com/zepinglee/gbt7714-bibtex-style
    - 支持“顺序编码制”和“著者-出版年制”两种风格。
    - 提供了 2005 版的 .bst 文件。
  - https://github.com/hushidong/biblatex-gb7714-2015
    - A biblatex implementation of the GB/T7714-2015 bibliography style
    - biblatex-gb7714-2015 宏包是中文参考文献著录/标注标准 GB/T 7714-2015 的 biblatex 实现
    - 它本质上是一个样式包，提供了顺序编码制和著者年份制样式，在 tex 文档中配合 biblatex 宏包使用

- [在博客中使用 BibTeX](https://geelaw.blog/entries/bibtex-for-blog/)
  - https://github.com/GeeLaw/bibtex-ts 实现说明

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

## [BibTeX的使用方法](https://www.cnblogs.com/parrynee/archive/2010/03/02/1676369.html)

- 默认bst模板
  - plain，按字母的顺序排列，比较次序为作者、年度和标题
  - unsrt，样式同plain，只是按照引用的先后排序
  - alpha，用作者名首字母+年份后两位作标号，以字母顺序排序
  - abbrv，类似plain，将月份全拼改为缩写，更显紧凑
  - ieeetr，国际电气电子工程师协会期刊样式
  - acm，美国计算机学会期刊样式
  - siam，美国工业和应用数学学会期刊样式
  - apalike，美国心理学学会期刊样式

- https://github.com/Mezek/Bst_generator
  - https://mezek.github.io/Bst_generator/generator.html
  - 生成bst，但下一步的选项太多了，估计有30多个下一步选项
# Citation Style Language (CSL)
- [手把手教你如何使用Zotero自定义参考文献格式（csl）](https://codeantenna.com/a/xOZGExJP1L)
  - 样式分为两个部分：1）文中引用（IN-TEXT CITATION）；2）参考文献（BIBLIOGRAPHIC ENTRY）

## [四步实现自定义 Zotero 参考文献格式](https://zhuanlan.zhihu.com/p/31326415)

- "流行的"指的是以 Citation Style Language (CSL) 为基础的一类参考文献软件，相对经典的EndNote 而言，Zotero, Mendeley, Docear 等软件均属于此类。
  - Citation Style Language 是一种基于XML的广泛使用的开源语言，用于定义 citation 和 bibliography 的格式。
- 称 citation 为参考文献索引，或简称索引。它就是正文中的 [1~3, 5] 或者 somebody (year) 这样的东西。
  - 常见索引只有两种格式：数字 (number) 与作者年代 (author-year)
- 称 bibliography 为参考文献书目，或简称书目。
# ref
- https://bithesis.bitnp.net/
  - BIThesis 是针对北京理工大学本科同学毕业设计、毕业论文制作的一个非官方的 LaTeX 模板，BIThesis 同时也包括其他本科学习中涉及到的文献综述、实验报告等的 LaTeX 模板。

- [BibTeX Format Description](http://www.bibtex.org/Format/)
  - [A complete guide to the BibTeX format](https://www.bibtex.com/g/bibtex-format/)

- repo
  - https://github.com/retorquere/bibtex-parser
    - A node/npm package for parsing bibtex (.bib) files. This is the parser that drives Better BibTeX for Zotero bib(la)tex imports.
  - https://github.com/ORCID/bibtexParseJs
  - https://github.com/GeeLaw/bibtex-ts

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

- Zotero 文献标题「首字母大小写」，修改秘诀！
  - 一些期刊对参考文献标题（title）的{字母大小写}有一定规定，常见的两种情况有
    - 仅标题首字母大写，其他单词首字母均小写。比如：Flexible triboelectric nanogenerator for human
    - 标题中所有单词（介词除外）的首字母均大写。比如：Flexible Triboelectric Nanogenerator for
  - 可是很多时候，我们抓取或导入到Zotero的文献的标题大小写不一定符合上述要求。
  - 最简单粗暴的方法是手动修改每个单词，但是效率低下
  - 今天要分享的是另一种简单实用的方法，而且是Zotero自带的功能，在其右侧信息面板中，我们鼠标右击标题。会弹出三个菜单项
    - Title Case：首字母大写。即每个单词的首字母均大写。
    - Sentence case：句首大写。即标题首字母大写，其他单词首字母小写。
    - BBT sentence case：与Sentence case有细微差别。符号;?:.!后的字母不进行小写处理。
      - 主要用于标题中存在「子标题」，且有;?:.!符号的情况。
      - 即BBT sentence case不会对冒号:后的字母A进行小写处理

- [Is it possible to convert a citation style language (csl) style file to a bibtext (bst) style file?](https://tex.stackexchange.com/questions/261023)
  - no

- [How do I use APA-style citations with BibTeX? ](https://tex.stackexchange.com/questions/35809/how-do-i-use-apa-style-citations-with-bibtex)
  - \usepackage{apacite}

- [LaTeX 第七课：排版参考文献](https://zhuanlan.zhihu.com/p/25013341)
  - \bibliographystyle{apacite}
