---
title: pm-noter-notable
tags: [note-taking, notion-like, office, pm]
favorited: true
created: 2020-11-24T07:44:16.296Z
modified: 2023-11-28T14:48:45.910Z
---

# pm-noter-notable

> make something people want to pay for futuristically. ~~easy to read， easy to write, content-centric notebook~~

# guide(for notable/noter/paper)
- features
  - 💰 market: lowcode(editor/automation), playground(preview+code+pdf)
  - ⏳ versioning and branching (reproducible/traceable): git-timeline, diff, draft/public
    - replay
    - 基于oplog/events的方案
  - 🤝 collaboration-ready (accessible): multiplayer, sharing, offlineable, crdt
  - ⛓️ automation/workflow/rpa (automatable): 结合lowcode, 基于dag?, scheduler, ai-hitl
  - 📱 mobile-editor: phone/pad, 自定义编辑器可以是主特性，也可以是锦上添花
    - mobile-app-generator
  - 📈 end-user database: 支持用户自定义数据和流程, multi views, ob-bases
  - 💫 animated-text/code sharing: playback with different speed
  - markdown: hotkeys, table-builder
  - github修改文档要提pr很繁琐; 可协作的workspace可直接改或用审阅修订模式
  - local-first storage with optional sync: 兼容git-commits, 浏览器多tab在断网时sync
  - office viewer
  - 👾 产品设计阶段可将 AI 作为用户，用来onboarding引导操作及问答，还可以在系统内预置数据并将owner设为AI，可用来提供模版及引导用户测试

- selling-point-knowledge-base
  - 通用或单一的builder价值不大，但针对业务平台特别是app-store的builder对平台方和开发者的价值都很大
  - ⌛️ version history
    - git-timeline
    - diff
    - 快照文件的协同，已删除文件的协同
    - 基于代码的回放能解决视频难以实时更新的问题, video-but-auto-update, 回放时显示问卷结果
    - replay: 探索rrweb结合的场景
      - 可调倍速
      - 回放时的表现可以和操作时不同，在回放模式下显示diff-view🆚更直观清晰，最好是流式diff
      - 快速定位到指定位置，快速分享链接和截图
      - 另一种思路: agent执行action后，整个repo都能回到指定action的时刻，类似git回到某个commit的状态
      - rrweb + editor-diff
  - 🪟 table
    - diff
    - 基于文本的table格式: gfm, front-matter-yaml; + diff
    - ✨ markdown-table的wysiwyg是一个痛点和卖点
    - split-table
    - export: copy-md-table, copy-list
  - 🔡 coding  + 🛝 playground
    - 针对用户问题给出代码参考和可运行可操作的在线交互示例，特别针对css
    - instant-preview: codesandbox的方案仍然太慢
    - code + table 适合重数据的业务场景，符合toB的需求，可参考jupyter
  - ⚖️ markdown support with git-like database
    - widely used, enterprise-loved(易盈利)
    - hotkeys
    - table-builder
    - text files works well with existing tooling
    - 备选方案参考git，将文本与git工具绑定
    - sync: 本地文件自动生成delta
    - 标题也支持富文本，特别是最顶层标题支持code/link
    - rust-mdBook
    - code block 也能支持纯前端的 autocomplete/lint/可折叠函数或花括号
  - 🔍 search: rag, code-search, ai-chat
    - 针对代码优化的搜索可作为技术卖点和产品卖点，可参考github-code-search/algolia
    - 文档和代码同步更新、搜索
    - repomap/manifest for repo
    - search the web
  - 💫 animation
    - editor + dom-motion + video-playback + 🛝 playground
    - 低代码工具吸引用户的方式一定会加入动画，类似 webflow收购GSAP/Framer开源motion
    - 适合使用动画的场景: ppt
    - 动画效果类别: 自动变速(时快时慢)
  - 🎞️ video: 自动生成视频，方便回放、教学
    - pdf/ppt > video
    - video templates for tiktok/bilibili
    - motion/live photo for doc
  - 🖼️ image
    - edit-image: 虽然不是编辑器的核心，但很实用且难做好
  - mdbook/gitbook: text + actions/workflows
  - office editor
    - pagable
    - pdf anno
  - encryption: 有权限的用户或有密码的用户才可看到的数据
    - paid-only elements: paragraphs/sentences
    - 只对部分段落或部分文字加密
    - 处理类似`.env`文件时，对secretKey加密或移除，类似上传或同步文档时自动加密或脱敏
  - 视频笔记
    - 针对视频的笔记，如历史片/纪录片, 快速添加时间戳/标签
    - 针对视频的搜索
  - pdf chat
  - ActionText for nodejs: hocuspocus
  - editor无法成为主营业务，但ide可以
  - cms+crdt
  - interoperable/sharing
    - MCP/LSP/backlink
  - drag between windows
  - integrations
    - jupyter-notebook
    - whisper-editor
  - ~~open folder as site~~, 通常发布的站点都会多次处理内容，任意文件夹无意义, 只是toc显示不同内容而已

- 特色功能点
  - localizable note file(not local-first)
  - keyboard shortcuts(accessible): 参考office、vscode、浏览器不冲突
  - blocks-store/templates
    - hero block，类似在一页ppt上只显示一个大号的单词/短语，以醒目突出
    - 对内容的块级抽象，可参考colanode
  - instant-preview
    - 类似typora的即时预览，可选择 行内/上下 两种结构
    - 类似observable-notebook的上下结构可减少页面reflow
  - dev-tools, instead of wrapper like react-ag-grid，需要大量时间，可跨平台
  - 文章段落查重，也可用于论文查重、评论查重
  - examples as notes
  - api doc，生成openapi/swagger ui风格的文档
    - 针对开发者的文档也有市场和融资，支持swagger/postman

- 难点
  - 对于嵌入到note中的本地媒体资源如图片、视频、音频，如何解析、存储、渲染更好

- 主要功能模块
  - file-explorer
    - 复刻vscode的文件管理器
    - 支持多个sidebar
    - 支持多种排序，包括创建时间、修改时间、tag

- interactive-doc
  - wysiwyg + codesandbox 编辑类
  - wysiwyg + code-editor 展示类
  - wysiwyg + table 展示类

- headless/unstyled design
  - 基于场景预定义react组件接口，允许替换默认使用的各个组件
  - 因为允许替换，所以经常需要动态导入
# business-apps
- 成功的产品，大多可以不断更新换代
  - 如大模型、支持最新大模型的comfyui
  - 能为其他产品提供infra或tools，如nvidia
  - 能为其他用户用户提供二创素材，如视频、图片

- 知识库的市场 (🤔 toB or toC)
  - 客服系统自动回复，并显示相关历史
  - classic 多文件知识库(ide)
  - mobile-first + markdown 知识库

- naming
  - mandroid (from android+manus)

## inspirations

- obsidian-mobile, notion-mobile
  - obsidian-open-rewrite compatible with obsidian plugin, 主流插件已达到百万下载
  - obsidian bases database

- git-statistics ui， 可参考 pingcap/ossinsight
  - auto generate cover by content/fields
  - files sorted by commits count

- github
  - github readme.md viewer: 参考obsdian的插件/vscode扩展/npm包可直接显示github-readme
  - reusable workflow actions as files
  - permlink for old docs

- linear
  - 问题描述中添加的 长日志 或 长文本 ， 在code block中显示时不会换行而需要水平滚动很长，临时方案是用 list item显示

## saas/cloud

- cloud-pros
  - unattended
  - parallel
  - collaborative
  - automation
  - history
  - data slice/subfolder
  - consistent environment and pre-installed tools

- pros-云桌面/云浏览器
  - ~~启动速度快~~, vnc打开chrome也挺慢
  - 方便服务端api操作
  - 云端环境方便打开类似本地的url如 http://localhost:3000, 且能绕过iframe的cors/cookie问题
  - 最新版chrome逐渐限制cdp调试的能力，在云桌面固定版本可绕过此问题

- cons-云桌面/云浏览器
  - 🐛 复制、粘贴、拖拽上传 不如本地环境方便
  - 用户刷新自己环境的浏览器需要手动触发刷新VNC的浏览器, 需要自己处理很多操作逻辑，如滚动页面
  - 云桌面的截图不能像本地一样滚动截长图
  - 需要在云环境/容器中安装 输入法、语言包、字体
  - 部分应用启动时不会显示全屏窗口，可能会显示全黑色背景， 窗口只占一部份屏幕
  - 需要透传声音
  - 需要设置vpn/防火墙/屏蔽占用带宽或流量的网站
  - 多人协作时的安全问题，直接读取浏览器密码、剪切板、容器文件
  - linux环境对GPU支持较差，最新版chrome内置的ai功能依赖gpu

- 类似ruby的ActionText
# features
- inspirations
  - 高频需求，网盘分享

## editor-feats

- doc-views
  - preview/text/text+blame, 类似github的网页版查看文件的tabs

- markdown
  - frontend LSP/autoFormat/autocomplete/twoslash
  - cloudflare markdown conversion open source alternative
- markdown code block 的优化
  - 支持语法高亮
  - 支持注释快捷键
  - 支持自动format
  - 支持基本语法autocomplete/lint/definition，基于webworker-lsp
  - markdown diff block 格式扩展和优化

- backlink
  - 在代码领域，双向链接通常对应import, 方便应用本地lib或远程lib
  - 在文档领域，双向链接方便引用和复用已有资源，需要在runtime层面支持解析和更新，甚至LSP

- vscode-inspired
  - search inside folder11

- git
  - search commit message
  - statistics (for team)

- image
  - 系统提供默认的图片placeholder需要样式友好

## diff

- special diff elements
  - table
  - code-block

## statistics/insights

- 统计以 github.com 开头的链接次数

- git-repo-insights

## text-editing

- web-editor在编辑器卡死(如打开超大文件)时，容易造成整个页面不可用，应该在架构上处理极端场景

- 选择一段文字，将其中的空格替换成`-`，方便区分比较双方，如 a-bvs c-d
- 选择多行文字，批量在行首添加`- `转换成列表显示，甚至`- [ ]`转换成待办列表
- 选择复制列表的多行文字，提供菜单，粘贴时用逗号拼接成一行文字

- 按键书写
  - `[ctrl]`+`[c]`

### list

- ✨ list 可多列对齐，类似分组table的list

- 每个list如何折叠
  - s1: 使用二级列表，然后将第一级列表的黑点改为折叠图标
  - s2: 使用标题+列表，借助标题进行折叠
  - s3: 列表块的判断基于前置符号+块级换行，这样可以将列表项前的段落作为折叠触发点

- toggle-list，支持设置初始折叠状态

## image

- text on image, 类似支持编辑器卡片背景图片和文字

- searchable-image
  - ocr

## export

- 文本优先版编辑器会丢失部分数据
- 标准版会导出所有编辑数据，以sqlite格式
# mobile
- 移动端的缩放
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
  - like jupyter but using js/ts
  - 考虑2年后可私有或会员私有

- ✨ 图文转视频
  - 视频的体验更生动有趣
  - 市场空白

- 自动生成头图、缩略图

- docx
  - diff .docx and .doc

- optimization(参考git的问题)
  - 针对二进制文件
  - 针对大项目
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

- editor/ide-settings sync/store/sharing

- excel
  - apache-arrow

## search

- search-in-page
  - 跳到当前可见内或之后的第一个搜索结果，尽量减少页面滚动
  - 跳到页面第一个搜索结果

- search时是否支持搜索侧边栏的评论

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

- parser
  - 以3个反引号开头，但结尾不一定是3个反引号，以增强解析容错

- [Update all code blocks to toggle between TS and JS syntax](https://github.com/reduxjs/redux/issues/4112)
  - The RTK docs currently use Lenz Weber's phryneas/remark-typescript-tools plugin to let us write TS syntax in code blocks, compile away the TS syntax to plain JS, and show both versions as a tab
  - https://github.com/phryneas/remark-typescript-tools
  - https://github.com/shikijs/twoslash
  - 两种方案需要选择取舍

## sync

- 云同步提供商
  - 网盘：百度OAuth2.0, 腾讯文档/微云，onedrive
  - 云服务商：七牛
  - 非主流存储：github、gitee

## comment

- 页面底部的comment、侧边栏跟随内容的comment、侧边弹框的comment

- comments
  - 编辑态评论
  - 阅读态评论
  - 分享态评论
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

- github非常强大的branching和历史版本功能在交互上隐藏太深
  - 可与timeseries时序数据库结合尝试

- 不那么成功的项目 wikidata
# gitbook-like
- 提供类似github的自动部署能力
- 支持mdx，支持部分js组件库
# versions/history
- 文档级、文件夹级、workspace级
# integretions
- 支持mdx，内置开源组件
# knowledge-base
- 个人知识搜索引擎
  - 保存个人文档、笔记，浏览器书签

- cms
  - 以editor为基础的论坛，支持页面评论，页面统计，整体效果类似论坛
# ux
- 当视口宽度变窄时，tab页或宽卡片可以像tweetdeck一样折叠以缩小空间，折叠的过程可显示动画
# business-features
- 提供相同的功能，但
  - 需要点击更多的确认按钮
  - 非高级的动画效果

- ActionText

- office开放集成
  - 支持wopi协议集成

- core免费，plugin收费
  - 类似vscode扩展市场
  - 非热门产品的特性插件是否该付费，参考nocodb，只将某些数据源收费，如oracle-db

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
# business-app-store/marketplace
- popular
  - ios, google-play
  - chrome-web-store, edge

- latest
  - ModelScope魔搭社区，主打中文的 AI 模型开源社区

- [Atlassian Marketplace](https://mar ketplace.atlassian.com/)
  - 支持jira, confluence, bitbucket, bamboo, crowd
  - Atlassian has a market cap or net worth of $53.92 billion

- [Microsoft AppSource marketplace](https://appsource.microsoft.com/en-us/marketplace/apps)
  - 支持word, excel, ppt, outlook, teams, powerbi

- [Google Workspace Marketplace](https://workspace.google.com/marketplace)
  - 支持google docs/sheets/slide/calendar/drive

- [Zoho Marketplace](https://marketplace.zoho.com/home)
  - 支持writer/mail/crm/analytics
  - estimated market value of between $5 billion – $15 billion
  - [How Zoho became a $1B company without a dime of external investment… | TechCrunch _202209](https://techcrunch.com/2022/09/10/how-zoho-became-1b-company-without-a-dime-of-external-investment/)

- [飞书 应用目录](https://app.feishu.cn/)
- [钉钉应用中心](https://appcenter.dingtalk.com/)

- [有赞应用市场-有赞营销插件-有赞私域场景解决方案](https://yingyong.youzan.com/)

- [Odoo Apps Store](https://apps.odoo.com/apps)
  - [Marketplace | Odoo Apps Store](https://apps.odoo.com/apps/modules/category/Marketplace/browse)
- [Salesforce AppExchange | Leading Enterprise Cloud Marketplace](https://appexchange.salesforce.com/)

- [GPTStore](https://gptstore.ai/)

- [Notion Integrations & Marketplace](https://www.notion-marketplace.com/)
  - The estimated value of Notion is $10 billion. 
  - Notion is estimated to make $67.2 million each year.

- [Coda Templates](https://www.codaplace.com/all-categories)

- [Airtable Marketplace](https://airtable.com/marketplace)
  - recently valued at $11.7 billion

- [Monday App Marketplace](https://monday.com/marketplace)
  - monday.com has a market cap or net worth of $10.76 billion

- [figma community](https://www.figma.com/community)
  - 支持figma/figjam/plugins/files
  - As of December 2023, CB Insights estimates that Figma is worth between $8.3 billion and $9 billion, a haircut to the $20B Adobe offered

- [Canva Apps Marketplace](https://www.canva.com/apps/)
  - from 2023, Canva's valuation may have dropped from $40bn to $26bn in just two years

- [Nextcloud - App Store](https://apps.nextcloud.com/)
  - 支持files, games, dashboard
- [ownCloud Marketplace](https://marketplace.owncloud.com/)

- [Mattermost Marketplace](https://mattermost.com/marketplace/)
  - 到2019年series-b共融资 70m

- [ClickApps in ClickUp™](https://clickup.com/clickapps)
  - Clickup Hits $4b Valuation 

- [Visual Studio Marketplace](https://marketplace.visualstudio.com/VSCode)
- [Unofficial Jupyter Notebook Extensions](https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/)
  - https://github.com/ipython-contrib/jupyter_contrib_nbextensions
    - [jupyter_contrib_nbextenions appears to be incompatible with Jupyter Notebook v7](https://github.com/ipython-contrib/jupyter_contrib_nbextensions/issues/1647)
  - [Extending the Notebook — Jupyter Notebook 7.1.0](https://jupyter-notebook.readthedocs.io/en/stable/extending/index.html)
    - Please note that the extension system for Notebook 7 is radically different from the one used in Notebook 6.5.x and earlier.
    - With Notebook 7 being developed on top of JupyterLab and Jupyter Server, the frontend extension system is now based on the same extension system used by JupyterLab.

- [JetBrains Marketplace](https://plugins.jetbrains.com/)
  - valuation. $7.0b (Public information from Dec 2020)

- [Eclipse Marketplace](https://marketplace.eclipse.org/)

- [AWS Marketplace](https://aws.amazon.com/marketplace)

- [Liferay App Marketplace](https://marketplace.liferay.com/home)

- [LibreOffice Extensions](https://extensions.libreoffice.org/)

- [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/home)

- [Zendesk App Marketplace](https://www.zendesk.com/marketplace/apps/)

- [zoom App Marketplace](https://marketplace.zoom.us/)
- [Motive App Marketplace](https://marketplace.gomotive.com/)
  - integrations help improve efficiencies, reduce operating costs, and deliver satisfying fleet and driver experiences

- [Shopify App Store](https://apps.shopify.com/)

- more-valuation
  - [Businesses based on open source software](https://www.factoftheday1.com/p/july-15-businesses-based-on-open)
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
