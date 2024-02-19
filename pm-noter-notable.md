---
title: pm-noter-notable
tags: [note-taking, notion-like, office, pm]
favorited: true
created: 2020-11-24T07:44:16.296Z
modified: 2023-11-28T14:48:45.910Z
---

# pm-noter-notable

> easy to read， easy to write, content-centric notebook

# guide(for notable/noter/paper)
- features
  - versioning and branching: 基于oplog/events实现, draft/public
  - collaboration-ready: 基于crdt
  - end-user database: 支持用户自定义数据和流程
  - github修改文档要提pr很繁琐; 可协作的workspace可直接改或用审阅修订模式
  - mobile-app-generator
  - local-first data storage with optional syncing: 兼容git的commits
  - markdown: hotkeys, table-builder
  - office viewer

- selling-point-knowledge-base
  - markdown support with git-like database
    - widely used, enterprise-loved(易盈利)
    - text files works well with existing tooling
    - 备选方案参考git，将文本与git工具绑定
    - sync: 本地文件自动生成delta
  - mdbook/gitbook
  - open folder as site
  - office editor
  - encrypted elements: 有权限的用户或有密码的用户才可看到的数据
  - 文章段落查重，也可用于论文查重、评论查重
  - paid-only paragraphs/sentences
  - 视频笔记
    - 针对视频的笔记，如历史片/纪录片
    - 针对视频的搜索
  - pdf chat
  - split-table
  - ActionText
  - cms+crdt
  - integrations
    - jupyter-notebook
    - whisper-editor

- 难点
  - 对于嵌入到note中的本地媒体资源如图片、视频、音频，如何解析、存储、渲染更好

- 主要功能模块
  - file-explorer
    - 复刻vscode的文件管理器
    - 支持多个sidebar
    - 支持多种排序，包括创建时间、修改时间、tag

- 特色功能点
  - localizable note file(not local-first)
  - keyboard shortcuts(accessible): 参考office、vscode、浏览器不冲突
  - api doc
    - 生成openapi/swagger ui风格的文档
  - hero block
    - 类似在一页ppt上只显示一个大号的单词/短语，以醒目突出
  - examples as notes
  - instant-preview
    - 类似typora的即时预览，可选择 行内/上下 两种结构
    - 类似observable-notebook的上下结构可减少页面reflow
  - dev-tools, instead of wrapper like react-ag-grid，需要大量时间，可跨平台

- interactive-doc
  - wysiwyg + codesandbox 编辑类
  - wysiwyg + code-editor 展示类
  - wysiwyg + table 展示类

- headless/unstyled design
  - 基于场景预定义react组件接口，允许替换默认使用的各个组件
  - 因为允许替换，所以经常需要动态导入
# features
- inspirations
  - 高频需求，网盘分享

## text-editing

- 选择一段文字，将其中的空格替换成`-`，方便区分比较双方，如 a-bvs c-d
- 选择多行文字，批量在行首添加`- `转换成列表显示，甚至`- [ ]`转换成待办列表
- 选择复制列表的多行文字，提供菜单，粘贴时用逗号拼接成一行文字

- 按键书写
  - `[ctrl]`+`[c]`

### list

- 每个list如何折叠
  - s1: 使用二级列表，然后将第一级列表的黑点改为折叠图标
  - s2: 使用标题+列表，借助标题进行折叠
  - s3: 列表块的判断基于前置符号+块级换行，这样可以将列表项前的段落作为折叠触发点

## image

- text on image, 类似支持编辑器卡片背景图片和文字

## export

- 文本优先版编辑器会丢失部分数据
- 标准版会导出所有编辑数据，以sqlite格式
# premium
- 针对table优化的notebook

- 作品默认使用系统预览图，允许vip上传自定义截图
- 剪藏扩展 web cliper
  - local-first pocket, any links
  - 支持批量导出

- multi-accounts
  - 支持新建账户(匿名)，然后临时操作

- 同步
  - 拼写检查cSpell、自定义短语、语法检查
  - 同步编辑器设置项，如缩进、特性启用

- subscription
  - 订阅知乎文章、博客园博客
  - 订阅某个用户的文章、资源，如hackernews用户、b站up主更新
  - 订阅股票数据

- marketplace
  - template/page
  - data/block

- image
  - copy text in image
  - ocr

- markdown-table工具
  - 在本页面分析表格，filter/sort/group
  - 在新页面的平台分析表格

- observable-notebook默认不支持私有文档
  - 考虑2年后可私有或会员私有
  - like jupyter but using js/ts

- docx
  - diff .docx and .doc
# draft
- 功能或菜单太多容易使人迷茫，考虑设计多个版本的前端：lite、pro、customized

- unlocalizable
  - 移动本地文件时，自动更新其他文件中引用的链接
  - 图床

- IIIF-spec + anno
  - 处理comment、高亮
  - 效果参考mirador

- editor
  - copy as markdown link
  - core-text-mode，整体页面突出文字，淡化链接样式
  - statistics-in-editor
    - 自动统计链接点击次数、图片分享次数、page或问题的访问次数

## search

- search-in-page
  - 跳到当前可见内或之后的第一个搜索结果，尽量减少页面滚动
  - 跳到页面第一个搜索结果

## page

- title
  - auto unique title by username-prefix

- 保存各级标题、字体的样式为类似页面格式刷

## toc

- 传统toc
- 类似批注的大纲+小结简介

- 另一种形式的文章浏览
  - 当前文章内的关键词词云图，或block关系网状图

## code-block

- [Update all code blocks to toggle between TS and JS syntax](https://github.com/reduxjs/redux/issues/4112)
  - The RTK docs currently use Lenz Weber's phryneas/remark-typescript-tools plugin to let us write TS syntax in code blocks, compile away the TS syntax to plain JS, and show both versions as a tab
  - https://github.com/phryneas/remark-typescript-tools
  - https://github.com/shikijs/twoslash
  - 两种方案需要选择取舍

## cloud-saas

- 类似ruby的ActionText

## sync

- 云同步提供商
  - 网盘：百度OAuth2.0, 腾讯文档/微云，onedrive
  - 云服务商：七牛
  - 非主流存储：github、gitee

## comment

- 页面底部的comment、侧边栏跟随内容的comment、侧边弹框的comment
# experimental
- notion like block editor
- roam like editor with bidirectional links，国内思源笔记
- remotion

- 在文本加书签或标记
  - https://github.com/StarlaneStudios/vscode-comment-anchors

- 管理链接的多维表格
  - 链接添加tag
  - 链接导出markdown，tag放在下一行

- animated-cards
# connections
- 支持mdx，内置开源组件
# knowledge-base
- 个人知识搜索引擎
  - 保存个人文档、笔记，浏览器书签

- cms
  - 以editor为基础的论坛，支持页面评论，页面统计，整体效果类似论坛
# ux
- 当视口宽度变窄时，tab页或宽卡片可以像tweetdeck一样折叠以缩小空间，折叠的过程可显示动画
# business-features
- ActionText

- 规避版权问题的内容讨论平台
  - 科技分享，类似hacker-news
  - 产品讨论，类似product-hunt
  - 打分评论，类似豆瓣电影与音乐
  - 论坛圈子，类似贴吧/reddit，支持一个url在不同板块重复讨论、多次讨论

- office开放集成
  - 支持wopi协议集成

- core免费，plugin收费
  - 类似vscode扩展市场
  - 非热门产品的特性插件是否该付费，参考nocodb，只将某些数据源收费，如oracledb

## pricing

- [ckeditor](https://ckeditor.com/pricing/)
  - free: GPLv2
  - paid/talk
  - ckbox/$50
  - export2pdf/$30
  - export2word/$40
  - import1word/$40

- [tinymce](https://www.tiny.cloud/pricing/)
  - free: MIT, 1, 000 editor loads per month
  - Essential/$80: 5, 000 editor loads per month, collab
  - Professional/$150: 20, 000 editor loads per month, PowerPaste, ai
  - Custom/talk: Unlimited editor loads, Self-hosted

- [tiptap](https://tiptap.dev/pricing)
  - free: MIT, Single developer, pro plugins, limited collab, forum support
  - starter/$150: 8members, ai, more plugins
  - business/$1000: Nmembers, sso
  - enterprise/talk: On premises solution, Dedicated support engineer

- [froala](https://cart.froala.com/)
  - free: trial, Watermark
  - Professional/$60: 1 Product, 3 Domains, no SaaS/Subscription
  - Enterprise/$133: Unlimited Products, Unlimited Domains, SaaS/Subscription

- [ag-grid](https://www.ag-grid.com/license-pricing/)
  - free: MIT
  - AG Grid Enterprise: $1000 Per Developer
  - AG Charts Enterprise: $200 Per Developer
  - Deployment License/$750: 单独售卖，每份

- [handsontable](https://handsontable.com/pricing)
  - free: for personal use only
  - Commercial/talk

- [jspreadsheet](https://jspreadsheet.com/pricing)
  - Standard/$41: 1dev, 1app, no saas
  - Enterprise/$166: 5dev, 2app, saas, limited-ext
  - Ultimate/$291: 10dev, 3app, saas, ext
  - Custom/talk: Ndev, Napp

- [sheetjs](https://sheetjs.com/pro/)
  - free: apache2
  - pro: $250/yr, basic, Image, Chart, Edit

- [SpreadJS 表格控件](https://www.grapecity.com.cn/developer/spreadjs/price)
  - 个人: 一年￥9800
  - 团队授权 I 型: 4人, ￥29, 400
  - 团队授权 II 型: 20人, ￥78, 400
  - 项目部署: 每个域名￥22, 000，透视表部署额外￥13, 800
  - SaaS部署/talk：包含 SpreadJS 的 SaaS 平台和服务。
- [spreadjs](https://developer.mescius.com/spreadjs/pricing)
  - paid/$1499: 每人每年
  - Designer Component: $500
  - Pivot Table Addon: $1000

- [outline wiki](https://www.getoutline.com/pricing)
  - free: BSL
  - vip1/$10: 10dev
  - vip2/$80: 100dev
  - vip3/$250: 200dev
  - vipN/talk

- [react-admin](https://marmelab.com/ra-enterprise/#pricing)
  - free: MIT
  - Team/135€: 2dev, pro-modules
  - Business/270€: 10dev
  - Corporate/540€: Ndev

- [craft-cms](https://craftcms.com/pricing)
  - free: self-hosted, 1dev
  - pro: $59/year, self-hosted, team, Unlimited user accounts 
  - cloud: $240/month, 3 environments, with 10GB asset storage each
  - enterprise/talk

- [Strapi](https://strapi.io/pricing-cloud)
  - free: MIT
  - pro/$99: 10dev, 100, 000 CMS Entries, Real-time logs
  - team/$499: 20dev, 1, 000, 000 CMS Entries, Audit logs (7 days), Review Workflows
  - Custom/talk: Ndev, SSO, Customer Success Manager

- [Directus](https://directus.io/pricing/cloud)
  - free: GPL/BSL
  - pro/$99: 1million API Requests/Month, 5 GB db, Unlimited Users & Roles, Unlimited Collections & Fields
  - enterprise/$599: Remote Database Access, SSO(Including LDAP & SAML)

- [react-admin](https://marmelab.com/ra-enterprise/#pricing)
  - free: MIT
  - team/$135: 2dev, Private modules
  - business/$270: 10dev
  - Corporate/$540: Ndev

- [wordpress](https://wordpress.com/pricing/)
- [wix](https://www.wix.com/premium-purchase-plan/dynamo)

- [Polaris Office: What are Basic, Smart, Pro, AI and AI-Plus accounts?](https://polarisofficehelp.zendesk.com/hc/en-us/articles/4408969904783-What-are-Basic-Smart-Pro-AI-and-AI-Plus-accounts-)
- [OfficeSuite OfficeSuite: Pricing of our Office Software](https://www.officesuite.com/en/plans/home)

- [Filmora - Compare All Plans](https://filmora.wondershare.com/shop/buy/buy-video-editor-us-pb.html)
# faq
- 如何不使用图床而将图片直接嵌入到笔记中
  - [MarkDown图片存储格式-Textbundle格式](https://zhuanlan.zhihu.com/p/368463926)

- 参考
  - jupytext: jupyter notebooks as readable, editable documents
  - executable document
# examples
- awesome-list
  - 将类似github上awesome-list的内容转换为多维表格
# more
