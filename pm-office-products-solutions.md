---
title: pm-office-products-solutions
tags: [office, pm, products, solutions]
created: 2021-07-11T08:30:12.375Z
modified: 2021-07-11T08:31:00.660Z
---

# pm-office-products-solutions

# guide

- 偏向文本编辑
  - almanac
  - coda
  - cloverapp

- 偏向任务管理
  - airtable
  - monday
  - taskade
  - asana
  - clickup
  - trello
  - focalboard

- 产品形式
  - 桌面端以编辑器为主
  - 移动端以多维表格为主

- pm-business
  - 直播卖课用的编辑器，专注于知识付费的方向
  - carbon-like screenshot for doc/table/markdown
    - [其他预览效果，类似渐变色背景上的卡片](https://twitter.com/hashnode/status/1597902218606149632?s=20&t=QD2NjvJuc-5zOZt6lBrViA)

- [2022年协作文档的发展趋势与技术选型](https://juejin.cn/post/7049275631774728199)

- L0
  - 几乎完全依赖浏览器特性 contenteditable，execCommand
- L1
  - 部分依赖浏览器，光标，选区，文本换行、方向，字体渲染
  - 数据和渲染分离的架构，内容更新一般抽象成MVC
- L2
  - 大部分完全自研实现，自定义程度最高
    - 自己实现光标、选区，文字换行、方向，字体渲染

- 文本编辑器
  - 自研：ms-word, google-docs, wps
  - 腾讯：Etherpad转自研
  - 飞书：Etherpad转自研
  - 语雀：slate转自研
  - 石墨：quill
  - 美团学城：prosemirror

- 表格编辑器
  - 自研canva：ms-excel, google-spreadsheets, wps
  - 腾讯：handsontable转自研
  - 飞书：spreadjs
  - 石墨：spreadjs

- office软件厂商
  - 国内主流：金山文档，腾讯文档，钉钉文档，语雀
  - 国内其他：飞书，石墨
  - 国外主流：GSuite, MSOffice
  - 周边产品：Canva、Gravit、Framer

- [效率软件综合测评 知乎专栏](https://www.zhihu.com/column/c_1486707752840425473)

- [【译】深度解析 Roam 数据结构 —— 为什么 Roam 远不只是一个笔记应用 - 知乎](https://zhuanlan.zhihu.com/p/355844756)
# trending-office-products

## office-doc-whiteboard

- [Whimsical - Work Better, Faster, Together](https://whimsical.com/)
  - The hub for visual collaboration

- [Fabrie 设计师的在线协作平台](https://www.fabrie.cn/home)

## Notion竞品分析

- [我来](https://www.wolai.com/)

- [从Notion到wolai，这些中文细节优化真是让人心动](https://zhuanlan.zhihu.com/p/346197555)
  - 中文排版优化
    - 会自动在中英文内容插入间隔，插入的间隔并非实际空格，只是样式上的限定
    - 一旦将文字复制或者导出为本地文件，却是没有空格的。
  - 直接粘贴markdown图片格式或者粘贴markdown全部图文，图片都会自动加载
  - wolai的编辑体验最让我印象深刻的是对全角字符的兼容
    - 无论是Notion的快捷输入还是markdown格式，一般都是需要在英文输入状态下支持，因此导致在中文输入中需要频繁切换输入法，
    - 但在wolai中则省事多了，如1。也可以识别为有序列表
  - 对拼音的支持非常好，如[/img], [/tupian], [/tp]
  - 支持右侧显示悬浮目录，在窄屏会显示小黑条
  - 多媒体内容与国内服务商结合紧密，特别是视频、地图
  - 表头提供了免费授权的背景图

- [interactive notebooks](https://nteract.io/)
  - We build SDKs, applications, and libraries that help you and your team make the most of interactive (particularly Jupyter) notebooks and REPL.

- [Top 12 Notion Alternatives 2022 (Free & Paid Competitors)](https://clickup.com/blog/notion-alternatives/)
  - 点评了最新的notion竞品，总结了features和pros
  - 大多给出了特性比较表
  - clickup的官方博客给出了很多竞品调研报告
    - [Monday.com Review 2022 (Features, Pros, Cons, Pricing)](https://clickup.com/blog/monday-com-review/)
- [16 Best Notion Alternatives In 2022 (Free & Paid)](https://marketsplash.com/notion-alternatives/)
- [Best Notion Alternatives in 2022: Review and Comparison](https://www.nuclino.com/alternatives/notion-alternatives)
- [8 Notion Alternatives To Change Your Project Management Game](https://hive.com/blog/notion-alternatives/)
- [11 Best Notion Alternatives for Your Company Home](https://friday.app/p/notion-alternatives)
- [16 Best Notion Alternatives to Use in 2022](https://www.ntaskmanager.com/blog/best-notion-alternatives/)
- [18 Best Notion Alternatives to Boost Your Productivity](https://everhour.com/blog/notion-alternatives/)

## [almanac](https://almanac.io/features)

- features-selling-points
  - modern editor
    - real-time collaboration, track changes, version history, templates...
  - os for documents
    - organize docs in handbooks, folders, groups or nested docs
    - 双链引用，助力分析，操作更方便
    - 文档小册，wiki风格的文档浏览，左侧目录，右侧文档内容，便于整理
  - living documentation
    - enable anyone to suggest changes, without disturbing the original doc
  - collaborative workflows
    - use structured workflows to ask for feedback or approval on documents
    - 文档、任务、审批、反馈集中化管理
    - 透明工作流
  - version control
    - use branches to draft, ideate, and revise high-risk work
    - 支持创建分支文档，然后将分支文档的修改合并回原文档

- features
  - everything remote teams need to create, organize, collaborate, and share
  - create
    - an easy-to-use yet powerful document editor
    - save templates or content to quickly reuse.
    - realtime collaboration
    - keyboard friendly; command panel
    - dynamic elements: insert checklists, tables, embed videos, figma files
  - organize
    - curate docs into wiki-style handbooks
    - git-like version control to branch and merge ideas, drafts, and revisions
    - create bidirectional links to other docs
    - nested folders: organize docs in a simple folder system
    - fast search
  - collaborate
    - get feedback on documents in a way that is structured and transparent
    - assign, manage, and review tasks in the doc editor; not in another trello
    - approval (and an audit trail) without another meeting
    - comments on the doc with auto-threading
    - track changes: see exactly what edits have been made
    - crowd-source improvements:let anyone suggest changes
    - message inbox: respond to comments from across all your docs, in one place
  - share
    - share docs with read receipts
    - publish docs with a link with edit/comment/copy permissions
    - home for community-focused documentation
    - password protect for docs
    - adjust permissions for dozens of documents at once
    - easily share folders and docs with multiple people

## craft

- features
  - 移动端的动画和设计是最大亮点
  - 每个block可以自定义样式，类似主题
  - 完整的离线功能
    - logseq是markdown，只存了数据，没存样式
    - 导出的数据，可以是定期导出，而不是实时导出

- cons
  - 异步协作，如mention
    - 协作功能大多是 coming soon
  - 实时协作不支持
  - 不支持目录

- details
  - 折叠列表时，不是显示三点省略号
    - 显示二级图标、菜单文字
    - 简单点时，可直接放一个代表block类型的icon
  - 可在编辑器页面添加手绘页面/白板

- 知识库功能和任务管理经常分为2个软件
  - Notion将两个功能融合在一起了

- TextBundle是一种文件格式，将图片和markdown一起导出，不再是难题

- craft: We’ve raised $8m Series A funding led by @creandum_202104

## 飞书文档

- 从 etherpad 迁移到 block-editor

## [Google Sheets vs. Excel: Complete Overview](https://sada.com/insights/blog/google-sheets-for-microsoft-excel-users-5-key-differences/)

1. Google Sheets is entirely cloud-based
2. Google Sheets automatically saves all files to Google Drive
3. Google Sheets makes collaboration simple
4. Easily view and revert back to previous versions of Sheets spreadsheets
5. Google Sheets seamlessly integrates with AppSheet
# products-excel
- [Subset - A remarkably simple way to create a spreadsheet](https://subset.so/)

- [Ultorg: General-Purpose, User-Friendly Database Software](https://www.ultorg.com/)

- [CloudTables](https://cloudtables.com/)
# latest-office-products
- [黑客说，类twitter/知乎的社交与内容平台](https://hackertalk.net/)
# office-online-products
- 选型参考
  - 既满足协作编辑需求，也满足Office功能的兼容性需求，支持 office open xml
  - 在线文档作为其他产品的基础功能，如网盘支持在线打开文档

- 基于canvas
  - google docs

- 基于svg
  - wps online kdocs

- 基于dom
  - microsoft office word online
  - 轻雀文档

- [飞书 云文档功能更新](https://www.feishu.cn/hc/zh-CN/articles/360049067483)
- [语雀 更新日志](https://www.yuque.com/yuque/changelog)
- [Confluence Release Notes](https://confluence.atlassian.com/doc/confluence-release-notes-327.html)
- [Notion What's New](https://www.notion.so/What-s-New-157765353f2c4705bd45474e5ba8b46c)
- [腾讯文档 功能更新日志](https://docs.qq.com/doc/p/435191b004cbb16236da93588e128f87949c2646)
- [Microsoft Office updates](https://docs.microsoft.com/en-us/officeupdates/)

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

- [富文本调研](https://juejin.cn/post/6844904068847140877)
- 字节 飞书
  - etherpad
- 阿里 语雀
  - slate转自研
- 金山 wps
  - 自研
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
  - a server and client that work together, components that can modify or extend the functionality of the server and/or client

# docs/journals
- [AsPoem | 现代化诗词学习网站](https://aspoem.com/zh-Hans)
# more-products
- [Diffchecker - Compare text online to find the difference between two text files](https://www.diffchecker.com/)

- [9 products you can build with TinyMCE](https://www.tiny.cloud/blog/tinymce-examples-products-you-can-build-wysiwyg-editor/)
  1. Blogging platforms
  2. Real-time chat apps
  3. Design tools
  4. Document processors
  5. Note-taking apps
  6. Email service providers
  7. Collaborative workspaces
  8. Comments apps
  9. Form builders

## teamind

teamind的新手引导里就已经出现了一些惊喜的元素，比如他们做了目录。
他们的新手引导真不错。
teamind在不同的frame切换时动画很不错。
teamind的多个元素组合成复杂图形时，block的嵌套蛮丝滑的，逻辑似乎也比较清晰。
teamind已经支持了聊天，留言，音视频，演示模式等有意思的东西。
为了解决地图和无限大白板的定位问题，他们限制了拖动时候的地图边界，除非你画了东西或者拖了已经有的元素，否则画布不是无限大的。
teamind似乎也基于dom而不是canvas

- 工具产品，向内容平台扩展；让我想起了快手，从GIF工具到内容生态的跨越
  - 和用户一起发展
