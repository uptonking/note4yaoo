---
title: spec-office-word-docx
tags: [docx, office, spec]
created: 2026-04-05T18:28:54.433Z
modified: 2026-04-05T18:29:33.553Z
---

# spec-office-word-docx

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

# summary

- 

# dev-tips

- 

# spec

- 

# discuss-tools/conversions
- ## 

- ## 

- ## 

- ## 

- ## [word文档怎样免费无损的，高效的转换成PDF文档呢  - LINUX DO _202603](https://linux.do/t/topic/1793546)
  - 在word文档转PDF文档时遇到了困难，在word中选项-高级中选了高保真分辨率，打印或者导出来的pdf中图片比word中更模糊。
- 图片用矢量图的话好点

# discuss-odt
- ## 

- ## 

- ## 

- ## [Why do scientific journals not accept manuscripts in .odt format? : r/libreoffice _202605](https://www.reddit.com/r/libreoffice/comments/1t4qiab/why_do_scientific_journals_not_accept_manuscripts/)
- docx is also an open format (a shitty one, but still). OOXML sucks, and the standardization process was fucky as hell, but that's mainly why. They "do" allow for submissions in an open format, technically.

- Calling docx an open format is technically correct. Comparing it with odt is disingenuous. Docx remains under Microsoft's control.

- Because learning latex is a rite of passage. 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [吐槽docx格式 - LINUX DO _202606](https://linux.do/t/topic/2461415/21)
  - 帮忙将一份PDF文件转成Word文档（docx格式），要求需要百分百还原源PDF的排版。
  - 免费的、付费的，都无法很好地转换出能否还原排版的Word文档。
  - 浪费了2个小时之后我终于还是放弃了。究其原因，有两个：
  - 1. PDF的排版和Word排版根本无法用简单程序一对一映射还原；
  - 2. Word文档实在是太不利于程序处理了。
  - 不利于程序处理的东西，也不利于AI处理，未来难免会没落和被淘汰。诚然有些人很精通Word，并且精心调整出来的排版让人感觉非常舒适，但是成本实在太大了。
  - 这个过程中倒是发现了两个还原度还可以的工具，但是做不到百分百还原，而且还是通过取巧的方式进行的，例如通过大量换行来还原文字的分布，但是这种从本质上不符合甲方（例如老师）的要求

- 特别是有大量公式的PDF文档, 想直接转换获得可编辑的公式格式(在保持原版式的情况下), 目前还没发现有好的处理方法

- 是的，网上看到的大部分是通过pandoc转成文本格式然后就可以diff了，但是每提交一次还是会存储一份docx，提交的多了.git肯定很大

- 这套东西对agent来说真的不友好，即便是让agent去操作ooxml这种底层的，依旧没办法很好的控制排版。比如图片这种插入docx，agent没办法知道大小，因为要走docx那套渲染引擎，agent就必须导出pdf或者截图才能看到视觉效果，太难受了。

- 微软从来没有保证过同一份docx在不同的设备上显示效果完全一致，光字体这一点就是屎山了。你就算在自己电脑上1:1 port成功了也不能保证换台电脑不出问题。
  - 我说写docx和写代码一样，有没有懂的：这段代码明明在我的电脑上能跑

- ## 文档基金会 (LibreOffice) 再次发文抨击微软，称微软的 OOXML 文档格式极其荒谬，Excel 甚至都不能很好的处理日期。
- https://x.com/landiantech/status/2057643105935859998
  - 文档基金会致力于推动开源格式 ODF 成为主流，微软则主要使用自己的专有标准 OOXML，文档基金会认为除非实现 ODF 成为默认选项，否则无法实现真正的数字主
  - [文档基金会(开源LibreOffice开发商)再次发文抨击微软的OOXML专有格式 - 蓝点网 _202605](https://www.landian.news/archives/113046.html)
- libreoffice對ooxml的兼容性慘不忍睹 尤其是中文
- libreoffice在编辑PDF的时候非常渣, 这东西甚至不如wps
