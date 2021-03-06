---
title: pm-office-products-solutions
tags: [office, pm, products, solutions]
created: '2021-07-11T08:30:12.375Z'
modified: '2021-07-11T08:31:00.660Z'
---

# pm-office-products-solutions

# guide

# office-online-products
- 选型参考
  - 既满足协作编辑需求，也满足Office功能的兼容性需求，支持 office open xml
  - 在线文档作为其他产品的基础功能，如网盘支持在线打开文档

- office软件厂商
  - 国内主流：金山文档，腾讯文档，钉钉文档，语雀
  - 国内其他：飞书，石墨
  - 国外主流：GSuite, MSOffice
  - 周边产品：Canva、Gravit

- 文字编辑器
  - 石墨：Quill
  - 腾讯：Etherpad转自研
  - 语雀：slate转自研
  - 美团学城：prosemirror

- 表格
  - 石墨：spreadjs
  - 腾讯：handsontable转自研 

- 多人协作冲突解决方案
  - OT算法，石墨和腾讯文档都是
  - [揭开在线协作的神秘面纱 – OT算法](http://www.alloyteam.com/2019/07/13659/)
  - [实现一个多人协作在线文档有哪些技术难点?](https://www.zhihu.com/question/274573543)

- [金山文档为什么没有腾讯和石墨火？](https://www.zhihu.com/question/439525789/answers/updated)
  - 金山全家桶你怕不怕
  - 在线文档这种东西，除非特别难用，否则火不火完全取决于用的人是否足够多。
    - 这在某种程度上跟社交软件很像，只要不是特别难用，最后就是用户最多的人取胜。
    - 在线文档这种东西，也是一个道理，你对接的人，他要用腾讯文档，你无非也就是顺手换一下的事情，用几次，你觉得腾讯文档也还行，那你就开始慢慢用了。
    - 在基础使用体验上，真的很难拉出明显的差距，最后就是用户最多的取胜，在这一点上，我依然觉得腾讯胜出的概率大。
# office-open-solutions
- [Cabbage Tree Labs](https://www.cabbagetreelabs.org/)
  - Cabbage Tree Labs is a home for publishing projects critical for the wider publishing ecosystem. 
- XSweet
  - https://gitlab.coko.foundation/XSweet/XSweet
  - tool for converting Microsoft Word documents (.docx) into HTML and beyond. 
  - Built as a series of XSL transformation steps, it’s designed to be modular and flexible.
  - A set of XSLT 2.0 stylesheets for extraction and refinement of data from MS Office Open XML (.docx) format, producing HTML for editorial workflows.
- Wax
  - https://gitlab.coko.foundation/wax/wax-prosemirror
  - http://wax-demo.coko.foundation/
  - https://waxjs.net/docs/wax/
  - 给出的文档例子包含批注形式
  - Wax depends on the following libraries.
    - React for the view(UI)
    - Styled-components for theming and styling.
    - Inversify.io as service containers，用的不多，剥离简单
- Paged.js
  - https://gitlab.pagedmedia.org/tools/pagedjs
  - library to display paginated content in the browser and to generate print books using web technology.

- PubSweet
  - https://gitlab.coko.foundation/pubsweet/pubsweet
  - The open toolkit for building publishing workflows
  - a server and client that work together, components that can modify or extend the functionality of the server and/or client, 

- [Fidus Writer](https://www.fiduswriter.org/how-it-works/)
  - https://github.com/fiduswriter/fiduswriter
    - /420Star/AGPLv3/202107/python
    - 依赖@vivliostyle/print、prosemirror、sortablejs、mathlive
    - 子项目很多，很复杂
  - Fidus Writer is an online collaborative editor especially made for academics who need to use citations and/or formulas.
  - The editor focuses on the content rather than the layout, so that with the same text, you can later on publish it in multiple ways: On a website, as a printed book, or as an ebook. 
  - Export as PDF, EPUB or HTML
  - In each case, you can choose from a number of layouts that are adequate for the medium of choice.

- bibliothecula
  - https://github.com/epilys/bibliothecula
  - https://epilys.github.io/bibliothecula/
  - document organizer with tags and full-text-search, in a simple and clean sqlite3 schema
  - Store plain text notes with automatic full-text search and back-reference indexing
