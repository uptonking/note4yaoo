---
title: pm-noter-notable
tags: [note-taking, notion, office, pm]
favorited: true
created: 2020-11-24T07:44:16.296Z
modified: 2022-12-19T02:01:20.161Z
---

# pm-noter-notable

> easy to read， easy to write, content-centric notebook

# guide(for notable/noter/paper)
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

- editor
  - copy as markdown link
  - core-text-mode，整体页面突出文字，淡化链接样式
  - statistics-in-editor
    - 自动统计链接点击次数、图片分享次数、page或问题的访问次数

- headless/unstyled design
  - 基于场景预定义react组件接口，允许替换默认使用的各个组件
  - 因为允许替换，所以经常需要动态导入
# features

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

- marketplace
  - template/page
  - data/block

- markdown-table工具
  - 在本页面分析表格，filter/sort/group
  - 在新页面的平台分析表格

- observable-notebook默认不支持私有文档
  - 考虑2年后可私有或会员私有
# draft
- 功能或菜单太多容易使人迷茫，考虑设计多个版本的前端：lite、pro、customized

- unlocalizable
  - 移动本地文件时，自动更新其他文件中引用的链接
  - 图床

## search

- search-in-page
  - 跳到当前可见内或之后的第一个搜索结果，尽量减少页面滚动
  - 跳到页面第一个搜索结果

## page

- 保存各级标题、字体的样式为类似页面格式刷

## toc

- 传统toc
- 类似批注的大纲+小结简介

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
# experimental
- notion like block editor
- roam like editor with bidirectional links，国内思源笔记
- remotion

- 在文本加书签或标记
  - https://github.com/StarlaneStudios/vscode-comment-anchors

- 管理链接的多维表格
  - 链接添加tag
  - 链接导出markdown，tag放在下一行
# connections
- 支持mdx，内置开源组件
# knowledge-base
- 个人知识搜索引擎
  - 保存个人文档、笔记，浏览器书签
# ux
- 当视口宽度变窄时，tab页或宽卡片可以像tweetdeck一样折叠以缩小空间，折叠的过程可显示动画
# faq
- 如何不使用图床而将图片直接嵌入到笔记中
  - [MarkDown图片存储格式-Textbundle格式](https://zhuanlan.zhihu.com/p/368463926)

- 参考
  - jupytext: jupyter notebooks as readable, editable documents
  - executable document
# discuss
- ## [Notion编辑器原理分析](https://zhuanlan.zhihu.com/p/359122473)
- 先了解怎么设计一款编辑器，做下铺垫，参考 facebook draft-js 的介绍视频
  - 文章讲了做一款编辑器为什么不直接使用 contenteditable，但又不能完全抛弃 contenteditable 的原因。
- 文章所指的主要原因是 contenteditable 中 DOM = State ，这里的 State 指存储用户输入的内容，为 html 格式；
  - 从用户操作发起到数据修改整个过程都由浏览器控制，但是各浏览器存在实现差异，造成 State 的结果不一致，兼容性问题多。
  - contenteditable 又有很多原生能力，速度快且支持所有的浏览器、如光标与选区、输入法事件等；ipad 下 contenteditable 也提供较多有意思的能力，如左右分栏时可直接从其它应用拖动文字到 contenteditable 中
  - 最终 draft-js 通过自定义 State，抛弃掉原生提供的 html 形式的 State，通过 contenteditable 提供的能力负责文字排版与用户事件接收，定义一套 op(Operation) 来修改 State ，同时把数据模型通过 react 渲染到 html 中，达到 controlled contenteditable。
- notion 也自定义数据层，设计了基于 Block-tree 的数据模型；
  - 渲染层用 React 把数据渲染成 html；
  - 使用 React 提供的事件(onInput\onCopy\onCut)或者工具条接收用户的操作指令，用户指令转换成 op；
  - 操作经过执行并修改数据模型 ，op 也会实时提交到服务端中改变后端数据库中的数据；
  - 服务端通过协同把 op 传给其他用户，达到一起编辑同一篇文章目的。
- 所以整个notion可以分两层，数据层专门负责存储数据；
  - 渲染层负责把数据渲染成界面，接收用户的事件并转化成 op 操作交给数据层执行。

- ### 数据层
- 在notion里一切都为block，如表格、图片、文字段落等，
  - block 通过 parent_id 来指向父 block，以此表达层级，如文章下有段落、表格、表格下有行、分栏下又可以圈套表格等。
  - 通过这种层级关系，就形成一棵 block-tree。
- 一个 block 最基本的几个属性为：
  - block_id
  - properties: 属性值，如段落中用户输入的文字
  - parent_id: 指向父 block id，形成 block tree
  - type: block 的类型，如表格、行、列、图片、段落等
  - version：版本，用于协同
- block 和 dom 节点对比，反过来想，dom tree 可以表达所有的用户界面，理论上来说 block tree 也能完成大部份编辑器的需求
- 有了数据模型后，接下来是需要对这棵数据模型进行修改，
  - 在 dom api 里，浏览器提供了节点的删除、增加、修改(属性)、移动等功能 。
  - 在 notion 里也一样，数据层通过提供 op 的方式给到渲染层来修改数据，常规对树的操作可以有两类
  - 节点位置移动、增加、删除
  - 节点属性修改
- 总结
  - 数据存储基于 tree，称为 block-tree，类似于 dom-tree
  - 定义一套 op 来表达修改数据意图，通过执行 op 来修改 block-tree

- ### 表现层/view
- 在打开一篇文档时会通过 blockId 去服务端拿到前 50 个子 block ，本地把这 50 个 block 缓存到内存中。
  - 此时服务端传回的和存在本地 store 的 block 并没有树形概念，而扁平化存储在 map 中，block id 为 key，block 值为 value；
  - 树形的构建是在渲染期建立，通过 block id，去 map 中找出所有的子节点递归渲染。
- 表现层的渲染大致流程为，第一步从服务端取出当前页的子 block 存放在 block cache 内存中，第二步从最顶上的 block 依次递归到叶子节点进行渲染。

- notion在产品能力上很优秀，打破了传统的笔记软件固化思维，与其说提供给用户的是一套笔记工具，而不如说是一套设计笔记软件的系统。
  - 但通过 block 能力的增强，能力更多了，可以用来做日常工作管理，团队 wiki 等。
  - notion整个软件架构的基建能力是把 block 的渲染、block 的存储、数据修改等都处理好，后期功能的增加可快速迭代，在基础上增加更多的 block 类型。

- ref
  - [探索 Notion 的实现](https://zhuanlan.zhihu.com/p/152964640)
# more
