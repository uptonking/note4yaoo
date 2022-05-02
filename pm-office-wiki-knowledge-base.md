---
title: pm-office-wiki-knowledge-base
tags: [knowledge-base, office, pm, wiki]
created: '2021-07-27T11:27:02.160Z'
modified: '2021-07-27T11:27:37.050Z'
---

# pm-office-wiki-knowledge-base

# guide

- 知识库的设计一般分2部分
  - *笔记/随笔/速记 note/snippet/draft*
    - 对于临时书写的文章或难以分类的文章，不需要创建文件夹
    - 底层实现是由系统自动创建了一个名为「随记」的**知识库**
    - 特殊之处在于每篇随记文章很可能会使用不同文档模版
  - **知识库 library**
    - 重点是编辑和展示内容紧密相关的多个页面
    - 类似单个github repository
    - 文件树和目录树
    - 主页要提供最大的灵活性
    - 可执行批量操作、添加标签/水印、背景、追更
    - 大量社交功能，批注、评论、投票等
    - 支持拆分一个知识库为的新创作空间下的多个小知识库
    - ？支持导入markdown.zip来创建新知识库，一个知识库其实就是一个按规则组织的文件夹；不会丢失快捷入口的配置，因为计算得来
  - **创作空间 spaces**
    - 重点是展示某个主题相关的多个知识库，主要用来降低复杂度和嵌套深度
    - 类似npm workspaces、monorepo、github org，可包含多个库
    - 还可以作为类似多语言、多版本文档的入口页
    - 设计可参考dashboard工作台，可放置快捷入口、动态流
    - 可执行批量操作、添加标签/水印、收藏
    - 可查看扁平化的多个文档
    - 支持合并多个知识库为新的知识库
    - ？支持导入markdown.zip来创建新空间，一个空间就是多个知识库文件夹，**空间提供批量操作的入口，但不额外存储信息**

- 设计导致的局限 limitations
  - 要不要独立文档优先？observablehq优先文章，github优先仓库
  - 尽量不要嵌入embed跨页面的或第三方大段文字内容，不利于本地离线查看
    - 解决方案是embedBySnapshot，嵌入时复制一次内容
  - 不支持在一个知识库中引用其他知识库的资源，如图片
  - 主推编辑，还是主推查看？github主推查看，但github codespaces支持强大在线编辑功能

- 多级页面
  - 语雀的上级目录项可以无对应页面只用来折叠，也可以存在对应页面
  - 飞书的上级目录项必须有对应的页面

- 社交功能的设计
  - 社交和创作结合的较好的是github，能离线下载编辑，能通过issues评论
# features
- core
  - local first, easy to migrate
    - 不支持跨知识库顶层文件夹引用资源，不利于维护和迁移
  - markdown based text format
    - 不需要庞大的office软件，普通文本编辑器即可编辑
  - 统一管理各类资源 easy to batch organization
    - 批量替换、快速拆分合并文章
  - collaborative

- optional
  - 双向链接
  - standalone article first
  - 批量修改多个文件的内容，如更新链接url
  - 统一管理assets，如替换图片
  - 默认以日期年份作为分类标签
# templates 流行模版
- 飞书知识空间模版
  - 研发部门、产品部们、市场营销、商业化
- 语雀模版
  - 文档、表格、演示文稿、画板、数据表
- [Confluence templates](https://www.atlassian.com/software/confluence/templates)
- [Notion Template Gallery](https://www.notion.so/Notion-Template-Gallery-181e961aeb5c4ee6915307c0dfd5156d)
- [Microsoft Office Templates](https://templates.office.com/)
- [明道企业数字化Saas 模版库](ht tps://www2.mingdao.com/library.htm)
- [腾讯文档 模版](https://docs.qq.com/mall/index)
# products-solutions

## logseq

- [有什么 Roam Research 的替代方案？](https://www.zhihu.com/question/409872334/answer/1372000024)
- 前端代码已经全部开源
- Logseq 已经支持编辑和保存本地文件系统, 可以当完全离线文件的桌面端用了。
- 完全离线，无需登录的桌面端已经发布

- Logseq 和 Roam 或者其他工具的主要区别是:
- 1. 服务端不存储用户 notes, notes 存在本地浏览器 IndexedDB, 目前可以通过 GitHub 同步。
- 2. 支持 Markdown 和 Org mode。
- 3. Logseq 使用了一个内存数据库叫 Datascript, 支持 Datalog 查询，据我们所知目前我们是第一个做到能双向同步 Datascript 数据库和 Markdown 文本内容(或者 Org Mode 或者将来支持的其他格式)，其实最主要是没几个人干这事儿, :) 
  - 比如用户在 Outliner 模式下编辑，需要同时保存在 Datascript DB 和对应的文件中，同时如果有文件的改动，比如 Git pull，也需要对 Datascript DB 做增量索引。
  - 这个是为什么 Roam Research 的作者 Conaws 不单在推上说 "Thrilled to check this out."，而且他也在 Logseq 的 discord 群组讨论一些具体技术细节。
- 4. Markdown 从 Org mode 那边借鉴了很多好东西，比如 Heading properties, priorities, todo keywords 等等。而这些东西都可以自定义查询，并且支持自定义渲染。

- Datalog是Prolog的一种适应于知识库的改进形式语言。
  - Datalog是一种数据查询语言语法与Prolog相似

## [飞书](https://www.feishu.cn/hc/zh-CN/articles/134238909902)

- features
  - 多人协作
  - 多种类型：文档、表格、脑图
  - 支持多种文档类型，方便迁移，如传统office文档、confluence
  - 权限管控，精细安全

- 知识库作为云文档的一个部分，在功能上和ui上都是如何设计的

- **知识库由多个知识空间构成**，**知识空间由多个文档页面构成**。
- 知识库是一个面向企业的内容管理系统。
  - 通过多人共建、集思广益的方式，提升企业知识溯源、传播和分享效率，减少人员流动影响，降低内部知识的流转成本。
- 知识空间是知识库的基本组成单位，是企业根据需要搭建的不同类别的知识体系，
  - 由多个具有层级和所属关系的文档页面构成。

- 文档编辑体验-pros
  - 可切换显示的当前文章目录
  - 可按标题级别折叠当前标题下的内容，支持多级折叠，如先折叠内层二级标题，再折叠外层三级标题
  - 飞书多维表格

- 文档编辑体验-cons
  - 点击多级目录中的上级目录项时，会懒加载转圈请求对应页面，点击叶节点的目录项也会执行没必要的请求
  - 一篇文档必须指定类型，文档、表格、脑图

- 左边侧边栏
  - 收藏书签
  - 文件树(注意不包含文章内的标题目录)
  - 回收站
  - 设置
- 知识空间设置
  - 基本配置
  - 成员管理
  - 权限安全
- 协作
  - 评论
  - 分段编写

- 知识库的权限
  - 知识空间管理员
    - 拥有空间管理权限，以及空间内所有页面的所有权限 
  - ​知识空间成员
    - 视权限设置，可拥有页面的所有权限、编辑权限或阅读权限 
  - 权限管理
    - 申请、修改、扩张收缩、交接
  - 页面操作
    - 复制粘贴、查看、编辑、删除、收藏、评论、分享、打印
    - 发起协作、接受协作邀请
    - 创建子页面、移动页面
    - 创建快捷方式、创建副本
    - 导入本地文件、导出
    - 转移知识库

- [飞书管理后台](https://dataplayer.feishu.cn/admin/index)
  - 成员组织
  - 安全隐私
  - 数据统计
  - 查看全部设置：弹出全屏modal选择设置项目
- 后台统一进行功能管理
  - 日历
  - 邮箱
  - 文档管理：文档操作记录

- [如何将 Confluence 数据迁移至飞书知识库](https://www.feishu.cn/hc/zh-CN/articles/612602911143)
  - 内容工具 > 导出。在导出格式中勾选 HTML

## [语雀](https://www.yuque.com/yuque)

- features
  - 核心功能：知识库、小记、协作空间
  - 数据安全：数据加密、权限管理、安全水印、防删找回
  - 四大文稿：文档、表格、演示文稿、思维导图mindmap

- 个人页
  - 小记
  - 收藏
  - 个人知识库
  - 协作知识库
  - 团队与知识小组(类似github org)

- 知识库体验
  - 知识库的功能类似增强版的文件夹+特殊显示规则
  - 模版会影响首页显示的内容
  - 知识库首页默认会显示目录，但博客模版会依次显示最新的文章
  - 可以通过创建多个知识库减少嵌套层级和目录层级

- 语雀空间/知识协同核心能力
  - 结构化知识沉淀：四大文稿
  - 高效知识协同
  - 强力安全防护

- 创建知识库
  - 文档知识库：创作在线文档、表格
  - 资源知识库：上传并预览本地文件
  - 画板知识库：上传并预览设计稿
  - 话题知识库：基于话题的多人协同交流
  - 导入：本地内容
- 知识库模版
  - 学习笔记、博客专栏、旅行攻略
- 知识库管理
  - 文档管理、成员管理、统计、回收站、设置、讨论区

- 工作台
  - 工作台是用户登陆以后自己的首页，它可以帮助你快速到达语雀上任何地方，同时在工作台上你也可以找到你最近的参与的内容以及动态。
  - 可直接添加url地址作为快捷入口

## [gitbook](https://docs.gitbook.com/)

- features
  - spaces
  - organizations

- In GitBook, a space is a project where you can start organizing your ideas. 
  - Imagine it as a virtual book where you can start writing pages simultaneously with other members or individually with rich-content and rich-text.

## Confluence

- features
  - Turn conversations into action 记录行动
    - Built for lasting knowledge so you never lose great ideas or context in a transient notification or chat.
  - Organize everything in one place 各种格式统一管理
    - From quarterly planning docs to new hire blogs
  - Break down team silos 结构规范
    - An open, connected structure allows information to flow freely among everyone at the organization.
  - Build a culture of open teamwork 积极反馈
    - With social features, employees at every level have a voice to contribute, share, and receive feedback.
  - extensions from atlassian marketplace
  - best-practice templates
  - 60, 000+ customers use Confluence to rethink the way they work.

- space体验
  - 提供了可关闭的模版页占位符，类似README.md、blog
  - 可将url添加到快捷入口

- conflucence dashboard
  - discover:  what's happening
  - Your work: recent, all
  - customize: homepage, go to settings page

- space directory(知识库)
  - Spaces(知识空间) are places to collect pages with a common theme – you can create as many spaces as you like – and you can find them all in the space directory.

- space bar(侧边栏)
  - shortcuts: 快速链接到其他页面或外部页面
  - page tree

- [Confluence use-cases](https://confluence.atlassian.com/doc/confluence-use-cases-283641068.html)
  - Using Confluence for technical documentation
  - Setting up a knowledge base
  - Setting up an intranet
  - Confluence for software teams

- who is using /demos
  - [Atlassian Documentation](https://confluence.atlassian.com/alldoc/atlassian-documentation-32243719.html)
  - [IGEL Knowledge Base](https://kb.igel.com/)
  - [Comala Workflows](https://wiki.comalatech.com/display/CWL)
  - [BMC docs](https://docs.bmc.com/docs/)

- ref
  - [confluence 6中文文档](https://www.cwiki.us/display/CONFLUENCEWIKI/About+Confluence)
  - [Confluence Documentation Directory 7.12__202107](https://confluence.atlassian.com/doc/get-started-777010817.html)

## [Documize](https://www.documize.com/product/)

- Flexible organization strategies
  - labels, spaces and categories
- Bring along existing assets
  - We all have mountains of Word documents sitting in search-less locations.
- Reusable templates and snippets
  - helps establish your best practices library
- Compose top-to-bottom for a more natural reading and editing experience.
- Compose content with various section types — Rich Text, Code, Markdown, Jira, Trello & more.
  - Forcing everything through WYSIWYG editing hinders content creation.
- Define change control workflows to request, approve and publish changes.
  - Renegade changes, email tennis and review meetings detract from the job in hand.
- Let lifecycle reduce clutter
  - Archive the old stuff and keep new content in draft till ready for publication.
- version management to support different versions of the same content
- Put automation inside
  - Request contributions, reviews and feedback from within the document
- Be guided by intelligence/stats
  - See what content is being consumed, ignored or is completely missing.
- One place for everyone
  - Centralize internal and external documentation and invite employees, partners and customers.
- Secure external customers
  - Invite and collaborate with external users whilst protecting internal documentation.
- Endgame is your knowledge backbone
  - Provide the means to capture and centralize everything you absolutely need to know.

## Notion

- features
  - One tool for your whole team: wiki, docs, notes, tasks, design, sales, hr
  - connect the whole company
  - collabrate in real time
  - integrations: embed 500+ other apps inside Notion pages. 

- [Notion Official Documentation](https://www.notion.so/Notion-Official-83715d7703ee4b8699b5e659a4712dd8)
- [Notion: What's New?](https://www.notion.so/What-s-New-157765353f2c4705bd45474e5ba8b46c)

## [MrDoc 觅道文档](https://github.com/zmister2016/MrDoc/blob/master/README-zh.md)

- features
  - 便捷书写：markdown、WYSIWYG、table
  - 沉浸阅读：左栏大纲
  - 扩展丰富：md、pdf、简悦
  - 管理强大：文档、文集、附件、站点

- 服务体验
  - 支持打开和切换多个tab

- 个人控制台
  - 仪表盘工作台：文档统计 + 操作动态
  - 我的文集(类似文件夹)
    - crud、排序、批量水印/标签
    - 我的协作
    - 导入文集：语雀api、markdown.zip、gitbook.zip
  - 我的文档(类似单个文件/单个文档)
    - crud、历史版本、修改发布状态
    - 模版crud
    - 标签管理
    - 分享管理
    - 回收站
  - 我的素材资源
    - 图片
    - 附件
  - 我的收藏
  - 设置：编辑器、token等

- **站点管理**
  - 图片管理、附件管理、文档管理、文集管理、
  - 用户注册、用户登录、用户管理、
  - 注册邀请码配置、全站关闭注册开关、全站强制登录开关；
  - 广告代码配置、统计代码配置、站点信息配置；
  - 附件格式配置、附件大小配置、图片大小配置；

- **个人管理**
  - 文集管理：新建、删除、权限控制、转让、协作、导出、生成电子书格式文件
  - 文档管理：新建、删除、回收站、历史版本
  - 文档模板管理：新建、删除
  - 图片管理：上传、分组、删除
  - 附件管理：上传、删除
  - Token管理：借助Token高效新建和获取文档；
  - 个人信息管理：修改昵称、修改电子邮箱、切换文档编辑器；

- **文档书写**
  - 文本文档、表格文档两种文档类型，`Markdown` 、富文本两种编辑模式，`Editor.md`、`Vditor`、`iceEditor`三种编辑器加持，自由选择、自由切换；
  - 图片、附件、科学公式、音视频、思维导图、流程图、Echart图表；
  - 文档排序、文档上级设置、文档模板插入；
  - 文档标签设置；

- **文档阅读**
  - 两栏式布局，三级目录层级显示，左侧文集大纲，右侧文档正文；
  - 文档阅读字体缩放、字体类型切换、页面社交分享、移动端阅读优化；
  - 文集EPUB、PDF文件下载，文档Markdown文件下载；
  - 标签关系网络图；
  - 文档全文搜索；
  - 私密文档分享码分享

## Outline

- features
  - fast response and instantly searchable
  - intuitive editor with markdown support
  - structured nestable documents with backlinks
  - 20+ integrations like slack/figma/loom
  - security & permissions
  - customizable
  - i18n
  - open source

- collections
- groups
- auth
  - api policies: by id, custom
- attachments
- views
# more-wikis
- github
- gitbook
- wordpress
- salesforce

- teambition thoughts
