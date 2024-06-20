---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# guide
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-summary
- dev-starter
  - css: open-props, glass-ui, 渐变字体
  - patterns: react, typescript
- list-grid-starter
  - no sort/filter/group
  - no reorder
  - no column width resize
  - custom cell renderer
  - searchable
  - virtualizable
- list-grid-solutions
  - checkbox
  - draggable/reorder list
  - fields menu - filter/groupable
  - inline editing
  - orm integration
  - sortable-filterable-groupable-table
  - dropdown-menu & tabs switcher
- 产品日历组件: headless-date-picker
- module/fwk/server: 灵活的tag/bookmark系统, cms, tables, bi
- 编辑器参考
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
  - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
  - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
  - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - more-editor
    - https://demo.grammarly.com/
# dev-review
- 解释代码
  - https://denigma.app/#demo
  - https://code-mentor.ai/

```shell
# delete all node_modules folders recursively
rm package-lock.json && find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + && find . -name 'dist' -type d -prune -exec rm -rf '{}' +

find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + 

# 格式化当前包，注意在子文件夹执行命令也会从package.json目录开始格式化整个包
prettier --write '**/*.{js,jsx,ts,tsx,json}' --ignore-unknown
# npm i
  DEBUG=* npm i --no-audit --loglevel silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel silly

$$('[contenteditable]')

flatpak run com.discordapp.Discord --proxy-server="socks5://127.0.0.1:7897"
betterdiscordctl -i flatpak install
```

- dev-goals 不能在产品中检验的技术不玩，注意产品化
  - rich-editor: text/block, vanillajs
  - pivot-table: editable
  - collaboration, local-first database
  - flowchart/whiteboard/pdf/annotation/comment
  - 事项--截止日期(0730+休整)--重要性(hml/s1-s3)
  - apps-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901
  - ui: ariakit, zag/ark, radix-ui, mantine
  - apps: cms+crdt

- deep into lib/fwk 书籍原理与代码实践要分开, 寻找深入debug的状态
  - 学习巩固: 实践练习 > 源码/示例 > 文档/论坛 > 社交分享
  - 不要从一个想法开始，而是从一个真正的问题开始
  - src-code, issues, pr, forks, extensions/alternatives
  - storage, sync/partial, conflicts, concistency
  - 直接根据具体框架或产品搜索解决方案如airtable-database，不必拘泥于通用方案如event-sourcing/eav，在产品讨论中常有细节和ideas
  - 解决方案在npm/docker也可以搜到，且更准确; 多关注包管理器上的最新的包
  - github package.json 也能搜索示例
  - 拆分核心内容和周边功能
    - split git-src and issues/pr/wiki, split txt/docx/xlsx and api
    - 将更多精力投入 core content 的创作，以及格式兼容、平台兼容、产品集成
  - 不必执着于vanillajs，常用模式早晚会抽象出工具库或框架，如reactive/effect/ajax/undo
# dev-2024-方向+方法+时间
- 👉🏻 output: 代码产出、产品落地、生态积累

- log2024 表格编辑、版本协作、cms
  - 01-pouchdb-idb-rspack, ethercalc-ot
  - 02-hexo-ssg, strapi-v5, realworld-fe-react
  - 03-realworld-be-sequelize/knex, airtable-like

- cms 功能融合及模块化
  - outline, strapi, undb, nocobase, 将undb的多维表格加入strapi-admin
  - business-features, 盈利支持自身
  - 不必执着于engine如db/excel-dataflow, 产品的形式大多cms
- slate-wangeditor
  - model, view, sync, collab
  - slate-docs-examples
  - general-editing-backend: ActionText, cms-payload
- eg-pivot-views/focalboard
  - table view
  - kanban view
  - **结合tanstack-table的pivot和ospreadsheet的edit/architecture**
- eg-tanstack-table-v8
  - [ ] 方便接入已有的外部数据源
  - [x] 内存数据: nedb, blinkdb
  - [x] 流式数据: linvodb, tingodb; 可参考kappa架构
  - 支持内存和持久化: tupledb, tinybase, tiddlywiki
- db-sync/collab
  - db+crdt的参考: piratedb, evolu, triplitdb, mithic
    - 不必执着于基于indexeddb的实现，只是作为一种持久化的方式
  - base: level/rocksdb/foundationdb, hypercore, ipfs, kappa-db
  - sqlite: rust_sqlite, extension
  - pouchdb: doc-db, incremental view
  - crsqlite, hypermerge: crdt + db
  - triplitdb: crdt + tupledb + eav
  - fireproof: ipld, live-sync, replication, branching-prolly-tree
  - tinybase: reactive
  - kappa + lsm => kdtree/r-tree
  - 基于oplog的研发方向, 架构设计时考虑放在数据库层解决还是应用层解决
    - 实现db，还是sourcing based framework
    - 基于log能提升write性能，基于materialized-view能提升read性能
  - pijul: crdt + vcs

- long-term-support
  - cms, airtable, lowcode
- techstacks-to
  - async/generator, stream, buffer, binary, scheduler, arrow
  - 样式片段也可在线尝试: codepen, w3schools.com 

- separate storage compute example
  - Lovefield uses a plug-in architecture for data stores. All data stores implement `lf.BackStore` interface so that query engine can be decoupled from actual storage technology.

- cache/stream for web storage
  - 参考 tanstack-query, localforage

- 🤔 支持切换内存和异步数据源的示例
  - tanstack-table external data; ag-grid server-side row model
  - abstract-level, localforage
  - tupledb, tinybase
  - tiddlywiki, react-admin
  - falcor
  - service worker

- collab-sync, partial-sync
  - string-crdt: ? list-crdt
  - logux
    - sqlite-persistor
    - collab-data-structure: lww-with-hlc
  - verdant/lo-fi: hlc + websocket, no-merkle
  - harika: hlc + sqlite + absurd-sql, no-merkle
  - jaredly/local-first: hlc + rga
  - evolu: hlc + merkle + worker
  - automerge: hypermerge
  - remoteStorage: google-drive、网盘、七牛对象存储
  - 使用hlc: idbsidesync, verdant, harika
  - 结合hlc+crdt: idbsidesync, evolu, rga-crdt
  - 结合hlc+db: piratedb, tinybase, kappa-db-stream, linvodb
  - hypercore: partial-sync
- event-sourcing

- undo/redo与branching可拆分实现
  - undo与versioning/history基于persistent data structure
  - branching与merge可在应用层实现
  - 多个branching可通过structural sharing共享数据结构

- sqlite-web
  - evolu(hlc+worker)
  - absurd-sql-ts: read ArrayBuffer
  - kikko

- ui: headless-architecture
  - state + action: 参考autocomplete、search-ui
- headless组件是否表明react将view与logic耦合在一起封装为component的思路是错误的?
  - 与view视图无关的component本身就是个简单的函数或eventemitter-pattern

- 若slate-model层采用扁平化Node(扁平化的思路可参考event-sourcing/orm/tinybase)
  - 如何保持path和key同步，参考 getKeysToPathsTable, getByKey实现上基于getByPath
  - 优化方向可参考tree的crud及协作
  - 协作时还应该考虑 json patch + last-write-win
  - Node定义采用unist
  - lww的字符串改为针对crdt优化的类型
- flat-data-model的示例
  - frontend/in-memory database，如rxdb/pouchdb/tupledb
  - 还可以参考indexeddb相关示例，如dexie
  - sqlite-react: vlcn-orm
  - ast如何扁平化
  - 参考案例: tree、react-admin

- 内容的存储与更新如何与数据库集成
  - 编辑器内容自动保存一般通过在onChange方法中执行saveToDB
    - 也可以在onChange方法中创建内存db、更新索引，通过索引提高计算效率
    - 应该避免维护2份数据
  - 将编辑器的计算密集部分的数据模型不使用普通json对象，而直接用类似数据库模型的设计
  - 为了性能，尽量不要直接读写持久化数据源，要使用缓存object pool

- log2023 编辑器、表格、协作、cms
  - 01-pouchdb

- why use es6 class
  - 运行时类型检查，instanceof
  - 既包含类型定义，又包含逻辑工具方法
    - 注意class有时也采用先定义interface再实现，此时ts type也合理了
    - 但应用层业务代码一般不需要定义单独interface
  - 方便调试，可直接log到对象及方法，函数里面的闭包变量更新难以定位
    - 也可以提前将需要调试的属性或方法添加到闭包暴露的对象上

- dev-xp-editor
  - 不仅要保持编辑器内容和视图同步，还要保持选区和内容同步

- dev-later
  - crdt tutorials
  - 默认 last-write-win, 出现冲突时，提示用户选择版本
  - 离屏渲染, keep-alive
  - 分层渲染

## ing

- not-yet
  - elmesque-editor
  - branching/versioned-doc
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav
  - todo remove hashId在编辑器model中有什么作用
  - 处理初试
  - 做完tailwind-table就面试

- dev-to 提炼核心`需求+产出`工作流，不能在产品中检验的技术不玩
  - headless-comp: sidebar
  - replace forceUpdate with useSyncExternalStore
  - slate-docs-examples
  - dnd-kit preset-tree
    - 参考react-sortable-tree
  - noseditor-docs
  - unit-tests
    - test in firefox
  - drag
    - rewrite dndkit by use-gesture
    - dnd-kit tree performance
      - 自定义冲突解决
      - 拖拽指示线
    - 拖拽到页面顶部或底部时，自动滚动
    - 拖拽时原布局不变，只显示预期位置的指示线
    - [x] 支持向左拖动更新层级
    - [x] 支持方向键向左更新层级
  - toolbar
    - [ ] dropdown 组件样式、active值
    - [x] 工具条按钮处理跨选区的情况
    - [x] 当前 block type 指示与转换
    - [x] 点击按钮时保存选区，逻辑+视觉
    - [x] 高亮当前光标对应的格式按钮
    - [x] 字体大小、颜色
    - [x] 按钮按功能分组
  - image
    - 上传图片时，默认图片原大小
    - upload by drag-drop
    - paste
    - [x] upload by filePicker
  - table to tanstack
    - 删除表格
    - 删除行时，若只有一行，则应该删除表格
    - [x] 隐藏浏览器selection
    - 优化model
    - copy from word
  - list
    - [x] rename todoList to checkboxList
  - scss to linaria
    - list-item
  - callout 高亮块
  - keyboard-shortcuts
  - copy-paste
    - images
  - 去掉依赖
    - plate-serializer
    - zustand
  - emoji
  - embeds
    - video
    - iframe
    - notion
    - apitable
  - formats
    - 清除格式
  - link
    - 粘贴图片url时提示显示为图片
  - 高亮块
  - 格式刷
  - 斜杠菜单
  - resume with noseditor
  - editor-features-playground
    - rewrite lexical for slate
    - with devtools

- dev-to-collab
  - 🐛 每次刷新页面，空白行会多一行
    - 每次刷新，observeDeep会执行
  - 🐛 yOffset out of bounds
    - 位置：getSlatePath > yOffsetToSlateOffsets
    - 复现方法，在一个浏览器输入，在另一个浏览器全选+删除

- dev-later
  - realworld - test
  - 悬浮工具条
  - merge-cells 逻辑优化
  - cell-floating-menu 右上角
  - list
    - 第一个列表项无法向左拖实现提升到父级
      - 列表项A的兄弟项B无法拖到A的位置，即无法替换A，B会自动变成A的子级
    - 列表折叠图标在item内容多行时，会竖直居中
    - 将无序列表项拖进数字列表项时，数字列表项会增加？数字编号或自动变动
    - 数字列表跟在符号列表后时，数字不会从0开始，需要在前面插入一个空行
    - 列表组件设置面板，设置折叠、可拖动
    - 拖拽时，不相关的列表项也会抖动
    - checkboxList完成后可选变灰
    - bulletList支持emoji
  - initialDataLong示例，无法删除首行列表项
  - drag
    - paragraph的drag handle有时无法选中
  - collab
    - 2个编辑器同一页面协同的示例未完成
    - cursor光标位置经常对不上
  - [x] streaming infinite-list/tree
# dev-06-dockview-floating-&-progressbar-animation-&-cm-diff-&-cm-typewriter
- architecture
  - 实现了偏静态的ui交互，优化cde集成、状态管理、单元测试
  - websocket chat/room, progress
  - refactor-cde-state-to-zustand
  - cde页面不稳定复线的内存泄漏
- CDE集成
  - lift layout state up to global
- diff-view
  - red + green
  - cursor
- time-machine
  - workflow progress
  - playback
- chat ui
  - typewriter
  - 分开处理 dock和float 的场景
- ui
  - editor: typewriter
  - dark theme for dockview
  - tailwind child selector
  - steps-tree: deprecate id in favor of content
  - 处理floating的滚动条

- not-yet
  - ide滚动失败
  - 删除未使用的 workbench2 组件失败，会导致样式混乱
  - trpc请求过多的问题

## 061

- dev-log
  - 
- dev-to
  - 

## 0620



- 导入仓库进度问题
  - 等github-repo导入完了，后端才返回结果

- dev-log
  - 导入github仓库的逻辑更新到了新的api，但还ui上还不work
- dev-to
  - run按钮运行前需要激活
  - 明天需要演示驾驶舱交互功能的话，今晚就将mock的制定计划数据、执行计划集成下

## 0619

- template表的env存放项目自身配置和系统配置.1024code
- 进入cde的代码拉取流程
  - importRepo > codezone_id
  - playground > playgroundId
  - ticket > ticketId
  - jssdk > serverUrl

- [Environment to disable NxCloud · nrwl/nx _202209](https://github.com/nrwl/nx/issues/12319)
  - `--skip-nx-cache` now prevents the task runner from connecting to Nx Cloud at all, as of @nrwl/nx-cloud@15.2.0.
  - This has been released in Nx Cloud 16.0.2 with the env variable `NX_NO_CLOUD=true`.

- [GitHub action failing when disconnected from Nx cloud · nrwl/nx _202403](https://github.com/nrwl/nx/issues/22444)
  - You can add set the `NX_NO_CLOUD` environment variable to true in your pipelines, to disable Nx Cloud.
  - You can add `--no-cloud` to your Nx Commands, to disable Nx Cloud.

## 0618

- 👥👥 sharing20240618-ai金融需求
  - 需求在业务各方传递时会丢失上下文
  - all-in-one的知识库产品，会保存上下文，减少重复工作
  - all-in-one的产品存在权限问题，还涉及利益问题、信息隔离，市场上的公司大多都自己给自己建立了信息隔离
  - 解决方法之一是内容转化，如将figma的图像转换为文字
  - 信息浓缩，类似figma/jira这样的抽象，大模型就可以理解，类似人的理解过程
  - ai会话的历史会保存，甚至ai能模拟公司中的人(根据记录、日志)
  - 产品、研发、销售一起积累数据，解决问题更快； 非研发也可以积累数据
  - 先尝试新技术，方便成熟时上手
  - 对ai的需求: ai能不能将需求直接生成代码
  - 💰 通义千问做了私有化部署，但chatgpt没做私有化部署； 客户会短暂采购私有版本，当效果匹配得上商用版时就会加大采购范围
  - 敏感数据的隐私安全问题
    - 敏感数据清洗过吗
    - 可以通过私有化部署解决信息隔离的问题，开源模型效果差一点
    - 通用场景、特定场景的问题，定制的模型

## 0617

- [How to access all the direct children of a div in tailwindcss? - Stack Overflow](https://stackoverflow.com/questions/67119992/how-to-access-all-the-direct-children-of-a-div-in-tailwindcss)

```HTML
<!-- Since 4th of july 2022, Tailwind added an ad-hoc approach to target specific elements.  -->
<div class="[&>*]:text-gray-200 [&>*:hover]:text-blue-500">...</div>

<!-- Since 19th of december 2023, Tailwind added child selectors -->
<div class="*:text-gray-200 hover:*:text-blue-500">...</div>
```

## 0616

- [gvm安装及go版本管理 - 逢生博客 - 博客园](https://www.cnblogs.com/wufengsheng/p/17755310.html)

- ERROR: Invalid or corrupt Go version
  - 原因：gvm未指定默认环境。
  - gvm use go1.19 --default
  - [gvm 安装教程及 终端出现ERROR: Invalid or corrupt Go version解决方案-CSDN博客](https://blog.csdn.net/IT_admin/article/details/136263880)

- dev-log
  - 优化了cde的交互细节图标菜单宽度，实现了执行计划在前端的进度条效果
- dev-to
  - cde-tools 集成paas现有功能
  - ai自然对话
  - layout状态优化
  - 尝试单个action对应文件的 diff视图-静态版、持久化数据库层
  - 业务staging分支使用paas的staging

## 0614

- https://almanac.io/  这个文档产品，用的也是 Prosemirror，看着设计挺不错的
  - 可以通过它的 DOM 显示和文档交互，窥一下它对于一些交互的处理逻辑
  - 前端不就这点好，没有秘密

- [Next.js attempted import error: 'useLayoutEffect' is not exported from 'react' (imported as 'React') - Stack Overflow](https://stackoverflow.com/questions/77885952/next-js-attempted-import-error-uselayouteffect-is-not-exported-from-react)
  - 需要在引用第三方可疑组件(特别是使用了useLayoutEffect)时，在使用位置加上 'use client'

- dev-log
  - 优化了cde的交互细节，分析了获取paas中op状态数据的方法
- dev-to
  - 尝试单个action对应文件的 diff视图-静态版

## 0613

- dev-log
  - 整理了执行计划的代码，在ui层mock计划op做了简单实现，提交了pr
- dev-to
  - 尝试将执行计划的op转换到paas中对编辑器的操作

- 每周分享-大数据中台 /黄茂俊/20240613
  - 从你的经历中，处理过的大数据的数据量有多大tb级别，文本、二进制数据
  - 运营商的书仓，pb级别的数据，日常的日志是1-2tb
    - 数据源较复杂，使用了第三方工具和平台
    - 还有些excel文件，使用python解析入库
  - 数据清理的工作量大
    - 主动对接和采集几百家停车场的数据，提供api和文档
    - 对不同业务域建模

## 0612

- 系统状态管理如何支持同时执行多个任务

- [React setInterval and useState - Stack Overflow](https://stackoverflow.com/questions/71172632/react-setinterval-and-usestate)
  - What if you want to start, stop, reset timer using functions ?
  - Make sure you use `useRef()`, because `useState()` will cause render.

```css
// 简单无分段的进度条动画效果

.grad {
  width: 10rem;
  height: 4rem;
  color: #fff;
  background: linear-gradient(to right, red, blue);
  background: linear-gradient(to left, #3F3F46 50%, #047857 50%);
  background-size: 200% 100%;
  background-position: right;
  transition: background-position 200ms ease-in-out;
}

.grad:hover {
  background-position: left
}
```

- [Why you don't need every CSS pseudo-selector in Tailwind CSS - DEV Community](https://dev.to/wheelmaker24/why-you-don-t-need-every-css-pseudo-selector-in-tailwind-css-3kn1)

- dev-log
  - 根据prd更新时光机进度条的实现，实现了一个最小版的验证，在ui层实现简单暂停和继续
- dev-to
  - 继续cde的集成，在前端模拟ai的对文件树的操作action

## 0611

- 制定计划、执行计划
  - ai-server
  - 制定计划agent与执行计划agent不是同一个角色
  - 驾驶舱聊天数据持久化
  - cde中回放数据持久化
- diff-view
  - 模型
  - 视图
  - 选区光标

- dev-log
  - cde新布局的发布
- dev-to
  - 继续完善cde的布局和交互逻辑
  - 根据linear的任务拆分，推进clacky的发布，主要包括 制定计划、diff-view的逻辑、驾驶舱ai对话的ui(不包括逻辑)

## 0608

- [B站11年，这 10 个技巧还有很多人不知道！ - 哔哩哔哩](https://www.bilibili.com/read/cv7767304/)
  - 将视频的链接复制到视频的评论区，接着在链接后面加上 `/?t=0h1m59s` ，这里的英文字母 h、m、s 分别代表 时、分、秒 ，字母前面的数字对应跳转到的时间点，即跳转到视频的 1 分 59 秒处。 

## 0606

- [NPM stuck giving the same error EISDIR: Illegal operation on a directory, read at error (native) - Stack Overflow](https://stackoverflow.com/questions/34959038/npm-stuck-giving-the-same-error-eisdir-illegal-operation-on-a-directory-read-a)
  - EISDIR stands for "Error, Is Directory". This means that NPM is trying to do something to a file but it is a directory. In your case, NPM is trying to "read" a file which is a directory (Line: 4). Since the operation cannot be done the error is thrown.
  - 解决方法是 将import的路径从 cm/file-up 改为 cm/file-up/index.js

- [tsc with allowJs reports TS9005 error for anonymous constructor functions · Issue #55172 · microsoft/TypeScript](https://github.com/microsoft/TypeScript/issues/55172)

## 0605

- dev-log
  - 事件风暴 制定计划、时光机
- dev-to
  - 调整cde的交互

## 0603

- dev-log
  - 优化cde
- dev-to
  - mock执行计划的前端数据
  - 登陆 > 授权仓库 > 导入仓库数据 > 创建thread > 初始化环境

## 0602

- [How to set DOM element as first child? - Stack Overflow](https://stackoverflow.com/questions/2007357/how-to-set-dom-element-as-first-child)
  - parent.prepend(newChild)  // [newChild, child1, child2]
  - parent.append(newChild)  // [child1, child2, newChild]

## 0601

- [unicode - Text encoding in ID3v2.3 tags - Stack Overflow](https://stackoverflow.com/questions/9857727/text-encoding-in-id3v2-3-tags)
  - for the text encoding code:
  - 00 – ISO-8859-1 (ASCII).
  - 01 – UCS-2 (UTF-16 encoded Unicode with BOM), in ID3v2.2 and ID3v2.3.
  - 02 – UTF-16BE encoded Unicode without BOM, in ID3v2.4.
  - 03 – UTF-8 encoded Unicode, in ID3v2.4.
# dev-05-codemirror-docs-&-cde-pm-&-replay-&-dockview-views

## 0531

- cde整体布局
  - 左侧可隐藏
  - 中间可max
  - 右侧可浮动

- 获取文件树数据的websocket事件名是 syncPlaygroundInfo
  - fileRootId
  - fileRootPath
  - fileTree

## 0530

- cde标签页结构(从上到下)
  - header: icon、title、pin、close；new-tab、max
  - breadcum
  - editor

- dev-log
  - 参与了制定计划、执行计划、时光机回放、cde编辑器细节的需求评审，优化了cde的界面交互
- dev-to
  - 测试github仓库的数据的拉取和编辑保存

## 0529

- dev-to
  - ~~在sdk仓库新建分支开发clacky功能，保留合并到main分支的可能~~
  - 在clacky业务侧实现cde的分屏交互

## 0528

- 为什么需要 RAG？
    - 私有数据只能用 RAG
    - 动态上下文构建：不同 task 看到不同的内容
    - long context 为什么还需要 RAG？ 始终需要从外界获取信息

- 难以提出通用方案
    - 推荐系统可以自我闭环
    - 但 RAG 是基于文本的概率选择

## 0527

- 待确认
  - 对于clacky新产品, ide-server的数据库和api的部署和1024/showmebug是分开的吗
  - 获取github仓库数据的api和sdk的逻辑

- dev-log
  - 参与了2个需求评审, thread创建流程和cde主要界面交互
  - 优化了cde的初始化为懒加载
- dev-to
  - 还原cde界面交互的细节
  - 导入github仓库的流程

## 0526

- dev-log
  - 升级了paas-sdk的状态管理zustood，暂时不改变
  - cde演示demo
- dev-to
  - 现在sdk的实现方式过于随意, 拆分为 editor/workbench/extension 三部分
  - sdk的api设计，参考vscode/theia，设计workbench界面布局的api

## 0524

- dev-log
  - 修改sdk的CodeEditor组件，支持多标签页
- dev-to
  - 驾驶舱、制订计划ui还原
  - 继续完善cde的功能，完善任务执行和回放的ui交互逻辑

## 0523

- [Tasks — Airflow Documentation](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/tasks.html)
- The possible states for a Task Instance are:
  - none: The Task has not yet been queued for execution (its dependencies are not yet met)
  - scheduled: The scheduler has determined the Task’s dependencies are met and it should run
  - queued: The task has been assigned to an Executor and is awaiting a worker
  - running: The task is running on a worker (or on a local/synchronous executor)
  - success: The task finished running without errors
  - restarting: The task was externally requested to restart when it was running
  - failed: The task had an error during execution and failed to run
  - skipped: The task was skipped due to branching, LatestOnly, or similar.
  - upstream_failed: An upstream task failed and the Trigger Rule says we needed it
  - up_for_retry: The task failed, but has retry attempts left and will be rescheduled.
  - up_for_reschedule: The task is a Sensor that is in reschedule mode
  - deferred: The task has been deferred to a trigger
  - removed: The task has vanished from the DAG since the run started

- dev-log
  - repo初始化逻辑
  - 修改sdk的CodeEditor组件，支持多标签页
  - 回放逻辑有了新的修改思路
- dev-to
  - 继续完善cde的功能，完善任务执行和回放的ui交互逻辑

- [css - Center a position:fixed element - Stack Overflow](https://stackoverflow.com/questions/2005954/center-a-positionfixed-element)
  - if your div has a dynamic/undefined width and/or height, then instead of the `margin`, set the `transform` to the negative half of the div's relative width and height.

## 0522

- [前端权限开发——设计到实践（保姆级） - 掘金](https://juejin.cn/post/7259210874446692411)

- [Differences between GitHub Apps and OAuth apps - GitHub Docs](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/differences-between-github-apps-and-oauth-apps)
  - In general, GitHub Apps are preferred to OAuth apps because they use fine-grained permissions, give more control over which repositories the app can access, and use short-lived tokens.
  - app 强在权限管理，OAuth 强在功能齐全
  - Similar to OAuth apps, GitHub Apps can still use OAuth 2.0 and generate a type of OAuth token (called a user access token) and take actions on behalf of a user. 
  - However, GitHub Apps can also act independently of a user. This is beneficial for automations that do not require user input.
  - GitHub Apps have built-in, centralized webhooks. GitHub Apps can receive webhook events for all repositories and organizations the app can access. Conversely, OAuth apps must configure webhooks individually for each repository and organization.

- dev-log
  - 和产品和设计确认cde的交互细节，确定了多标签页的技术方案和修改paas-sdk的思路，但为了支持回放暂时disable多标签
- dev-to
  - 多标签页分三阶段实现: 阶段B多标签但不支持回放，阶段C多标签且支持回放

## 0521

- cde多标签页的功能写在webapp好，还是写在sdk好
  - 写在webapp，优点是实现简单，缺点是可复用性低
  - 写在sdk，缺点是切换标签页的回放没实现，但可后期实现
- 用文件树拖文件到编辑器的场景
  - 多用于演示

- zustood有些用法不合理，比如初始化2次

## 0520

- dev-log
  - 修改paas的时光机的播放逻辑，支持修改编辑文件
  - 是否支持每个用户仅回放自己的操作
- dev-to
  - 本周目标: 时光机可用版，cde集成

## 0516

- dev-log
  - paas的录制和回放的实现，与时光机结合的方式
- dev-to
  - 执行和暂停

## 0514

- [node.js - opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ] - Stack Overflow](https://stackoverflow.com/questions/74726224/opensslerrorstack-error03000086digital-envelope-routinesinitialization-e)
  - Try to uninstall Node.js version 17+ and reinstall Node.js version 16+

- [Next.js Issue: useEffect Hook Running Twice in Client | by Rishabh Sharma | Medium _202401](https://rishabhsharma.bio/next-js-issue-useeffect-hook-running-twice-in-client-9fb6712f6362)
  - When using React’s useEffect hook in a Next.js application, you might encounter a behavior where the useEffect function runs twice during the initial render in development mode. 

- 测试
  - 注意 fixture/snapshot

- dev-log
  - paas sdk精简版示例已在本地测试通过
- dev-to
  - 在playground测试codemirror的diff视图

## 0513

```shell
# sdk-local
https://develop.1024paas.com/demo/api/v1/tickets?playgroundId=661625642386874368&specialNameFromQueue=king
# sdk-online
https://www.1024paas.com/demo/api/v1/tickets?playgroundId=661631957259927552

# 🐛 一直提示校验失败，且此api只在文档中提到，业务中并未使用
https://develop.1024paas.com/api/v1/sdk/environments
```

- [How to set header and options in axios? - Stack Overflow](https://stackoverflow.com/questions/45578844/how-to-set-header-and-options-in-axios)

- dev-log
  - 迁移paas平台的功能未完成
- dev-to
  - 继续迁移paas平台，尝试实现业务

- ddd开发
  - domain-entity-value
- 事件风暴
  - 用户主要流程的事件时间顺序
  - 事件、操作、用户

## 0511

```shell
# 1024paas init log 日志
https://develop.1024paas.com passDomain from demo
Start to init SDK,with version:0.9.211
{paasDomain: 'https://develop.1024paas.com'}

closeLspServer: null null
[messageLinstener][addMessageListener]0-1
[messageLinstener][addErrorListener]0-1
[messageLinstener][addMessageListener]1-2

findAvailableAgentUser: 63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea
Start to get ticket: M3w2NjA5ODIzODczNzg5MDUw

[canVisit]
[messageLinstener][addMessageListener]2-3
[messageLinstener][addMessageListener]3-4
[messageLinstener][addMessageListener]4-5
[Editor]freezeCode:false,showHiddenCode:true
[messageLinstener][addMessageListener]9-10

Reciver ticket:  
{
  "status": "success",
  "data": {
    "url": "ws://localhost:3012",
    "userId": "659227293847281664",
    "socketParser": ""
  }
}

findAvailableAgentUser:  true 63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea

🔁 Start to connect WS  ws://localhost:3012

>>>registerVisiblityChangeEvent
Connect  WS  successfully

[canVisit] undefined

移除message监听
[messageLinstener][removeMessageListener]12

payload:  {debugSupport: false}

{terminalUpdate: true}

[canVisit] 
[messageLinstener][trigger]followingFocusComponentUpdate-12
```

```shell
# 运行js项目
{ consoleUpdate: true }
[canVisit] RUNNING
[messageLinstener][removeMessageListener] 11[messageLinstener][addMessageListener] 11 - 12 { consoleUpdate: true }
[canVisit] RUNNING[OutputBrowser] reload: https: //5afbc1d37ef0fb2b7257947fee0a9571-app.develop.1024paas.com
[messageLinstener][trigger]message-12
hello world!
```

```JS
{
  "paasDomain": "https://develop.1024paas.com",
  "tenantId": "3",
  "ticket": "M3w2NjA5ODIzOD=",
  "defaultLspLang": [
    "html",
    "css",
    "less",
    "sass"
  ],
  "openLspDiagnostic": true,
  "showModifyIcon": true,
  "focusEditorPosition": "BOTTOM",
  "isSplitCode": true,
  "isInsertCrdt": true,
  "isLegacyMarkdownMath": false,
  "userInfo": {
    "username": "king",
    "avatarUrl": "https://ui-avatars.com/api/?background=3A3C40&color=fff&rounded=true&uppercase=true&bold=true&length=1&name=king"
  },
  "xtermStyle": {},
  "enableSentry": false,
  "isOpenDebugMode": false,
  "defaultOpenFiles": [
    "README.md",
    "CHANGELOG.md"
  ],
  "specialFileHighlight": [{
      "fileName": "paas_test",
      "languageType": "typescript"
    },
    {
      "fileName": ".java.answer",
      "languageType": "java"
    },
    {
      "fileName": "paas_test.java.answer",
      "languageType": "yaml"
    }
  ],
  "recordBrowser": false,
  "persistenceWebData": false,
  "customFileTreeAction": false,
  "contextMenu": [
    [{
        "text": {
          "ZH": "剪切",
          "EN": "Cut"
        },
        "shortcutKey": "Ctrl/Cmd+X",
        "actionName": "cut",
        "className": "contextmenu-cut",
        "textClassName": "d42 dao42__icon--create",
        "shortcutClassName": ""
      },
      {
        "text": {
          "ZH": "复制",
          "EN": "Copy"
        },
        "shortcutKey": "Ctrl/Cmd+C",
        "actionName": "copy"
      },
      {
        "text": {
          "ZH": "粘贴",
          "EN": "Paste"
        },
        "shortcutKey": "Ctrl/Cmd+V",
        "actionName": "paste"
      }
    ],
    [{
        "text": {
          "ZH": "撤销",
          "EN": "Undo"
        },
        "shortcutKey": "Ctrl/Cmd+Z",
        "actionName": "undo"
      },
      {
        "text": {
          "ZH": "注释代码",
          "EN": "Comment Block"
        },
        "shortcutKey": "Mod-/",
        "actionShortcutKey": "Mod-/"
      },
      {
        "text": {
          "ZH": "全选",
          "EN": "Select All"
        },
        "shortcutKey": "Ctrl/Cmd+A",
        "actionName": "selectAll"
      },
      {
        "text": {
          "ZH": "选中整行",
          "EN": "Select Line"
        },
        "shortcutKey": "Ctrl/Cmd+R",
        "actionName": "selectLine"
      },
      {
        "text": {
          "ZH": "格式化代码",
          "EN": "Format Document"
        },
        "shortcutKey": "Mod-Alt-f",
        "actionShortcutKey": "Mod-Alt-f"
      },
      {
        "text": {
          "ZH": "插入代码(自定义快捷键)",
          "EN": "Insert Code"
        },
        "shortcutKey": "Mod-j",
        "actionShortcutKey": "Mod-j"
      }
    ]
  ],
  "aiCodeMenu": [
    [{
        "text": {
          "ZH": "清空内容",
          "EN": "Cut"
        },
        "actionName": "remove",
        "shortcutClassName": "",
        "withCodeFlag": true
      },
      {
        "text": {
          "ZH": "复制代码",
          "EN": "Copy"
        },
        "shortcutKey": "Ctrl/Cmd+C",
        "actionName": "copy"
      },
      {
        "text": {
          "ZH": "取消标识",
          "EN": "Paste"
        },
        "shortcutKey": "Ctrl/Cmd+V",
        "actionName": "removeFlag"
      }
    ],
    [{
        "text": {
          "ZH": "解释代码",
          "EN": "Cut(Custom)"
        },
        "shortcutKey": "Ctrl/Cmd+X"
      },
      {
        "text": {
          "ZH": "生成代码",
          "EN": "Cut(Custom)"
        },
        "shortcutKey": "Ctrl/Cmd+X"
      },
      {
        "text": {
          "ZH": "交换代码",
          "EN": "Cut(Custom)"
        },
        "shortcutKey": "Ctrl/Cmd+X"
      }
    ]
  ],
  "editorBlankContent": "\n      <div class=\"blank_container\"\n      <div class=\"item\">\n        <div class=\"item-title\">Show All Commands</div>\n        <div class=\"item-shortCut\">\n          <div class=\"item-shortCut-item\">⇧1</div>\n          <div class=\"item-shortCut-item\">⌘</div>\n          <div class=\"item-shortCut-item\">P</div>\n        </div>\n      </div>\n    </div>\n    <div class=\"blank_container\"\n      <div class=\"item\">\n        <div class=\"item-title\">Open File or Folder</div>\n        <div class=\"item-shortCut\">\n          <div class=\"item-shortCut-item\">⌘</div>\n          <div class=\"item-shortCut-item\">O</div>\n        </div>\n      </div>\n\n    </div>\n  <div class=\"blank_container\"\n    <div class=\"item\">\n      <div class=\"item-title\">Open Recent</div>\n      <div class=\"item-shortCut\">\n        <div class=\"item-shortCut-item\">⌃</div>\n        <div class=\"item-shortCut-item\">R</div>\n      </div>\n    </div>\n </div>\n<div class=\"blank_container\"\n  <div class=\"item\">\n    <div class=\"item-title\">New Untitled Text File</div>\n    <div class=\"item-shortCut\">\n      <div class=\"item-shortCut-item\">⌘</div>\n      <div class=\"item-shortCut-item\">N</div>\n    </div>\n  </div>\n</div>\n<div class=\"blank_container\"\n<div class=\"item\">\n  <div class=\"item-title\">Show All Commands</div>\n  <div class=\"item-shortCut\">\n    <div class=\"item-shortCut-item\">⇧</div>\n    <div class=\"item-shortCut-item\">⌘</div>\n    <div class=\"item-shortCut-item\">P</div>\n  </div>\n</div>\n</div>\n<div class=\"blank_container\"\n</div>\n      ",
  "globalConfig": {
    "fontSize": "16px"
  }
}
```

- dev-log
  - 迁移了编辑器的部分功能，但paas的预览功能需要一个后端
- dev-to
  - 将paas的server也迁移过来?

- [What is RPA (Robotic Process Automation)? | Microsoft Power Automate](https://powerautomate.microsoft.com/en-us/what-is-rpa/)
  - How robotic process automation streamlines business processes
  - By using RPA tools as part of a larger business process automation strategy, software “robots” can easily be configured to trigger responses, manipulate data, and communicate with other digital systems
  - When exploring RPA as a workflow automation solution, it’s helpful to consider the two different categories—attended and unattended automation—before deciding which is right for your organization.

## 0510

- [ENOSPC: System limit for number of file watchers reached - Stack Overflow](https://stackoverflow.com/questions/55763428/react-native-error-enospc-system-limit-for-number-of-file-watchers-reached)

```sh
sudo gedit /etc/sysctl.conf
fs.inotify.max_user_watches=524288
sudo sysctl -p
```

- dev-log
  - 熟悉了1024code的整体架构
  - 熟悉编辑器的插件
- dev-to
  - 1024code的代码如何复用到新产品中

## 0509

- dev-log
  - 从sdk到paas
- dev-to
  - 将1024code的代码抽象出可复用的模块

- turborepo的问题，默认使用cache，想重新构建较繁琐
  - [Caching – Turborepo](https://turbo.build/repo/docs/core-concepts/caching)
  - 可手动删除cache， `./node_modules/.cache/turbo`

- [配置VSCode的Dev Container - 知乎](https://zhuanlan.zhihu.com/p/627102373)

## 0508

- dev-to
  - withSSR的if逻辑似乎有问题，都会提前返回

- [Can there be multiple request interceptors defined with axiosInstance? · Issue #4861 · axios/axios](https://github.com/axios/axios/issues/4861)
  - Please refer to Multiple interceptors

- [node.js - Logging axios request and response headers - Stack Overflow](https://stackoverflow.com/questions/70704988/logging-axios-request-and-response-headers)
  - Here's what I usually do: In the request interceptor, I use some UUID library (or maybe the crypto core module of node) to generate a UUID, then attach it to the config object as a request ID, say config.reqId. Same config object should be accessible in response.config

- https://github.com/Gerhut/axios-debug-log
  - Axios interceptor of logging request & response with debug library.
- https://github.com/hg-pyun/axios-logger
  - When you send a request in nodejs, you need to show the log to the console. This library display the necessary information while communicating with the server.
  - This package is working as Axios's interceptors.

- [NEXT. JS redirect not working in getServerSideProps · vercel/next.js ](https://github.com/vercel/next.js/discussions/42405)
  - your service worker is using the incorrect strategy. Refer to this answer. 
  - All you gotta do is, if you are using next-pwa

- [pnpm link | pnpm](https://pnpm.io/cli/link)

```JS
console.log(';; ajax-req ', config.url, isBackendURL(config.url), JSON.stringify(Token), window);

console.log(';; ajax-res ', path, JSON.stringify(error));
```

## 0505

- Resolve error: Can't resolve '@datalking/codemirror-react'
  - 方法是移除package.json中的`exports`字段

## 0502

# dev-04-strapi-preview-versions-&-yjs-quill-codebase

## 0423

- [How do I make Git ignore file mode (chmod) changes? - Stack Overflow](https://stackoverflow.com/questions/1580596/how-do-i-make-git-ignore-file-mode-chmod-changes)
  - git config core.fileMode false
  - git config --global core.filemode false

## 0421

- [max-height - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/max-height)
  - `max-height` overrides `height`, but `min-height` overrides `max-height`.

- [max-width - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width)
  - `max-width` overrides `width`, but `min-width` overrides `max-width`.

## 0419

- [How can I clear an HTML file input with JavaScript? - Stack Overflow](https://stackoverflow.com/questions/1703228/how-can-i-clear-an-html-file-input-with-javascript)
  - input.value = '' or input.value = null; 

- [Make some properties optional in a TypeScript type - Stack Overflow](https://stackoverflow.com/questions/52703321/make-some-properties-optional-in-a-typescript-type)

```ts
type OptionalExceptFor<T, TRequired extends keyof T> = Partial<T> & Pick<T, TRequired>

// F - the fields that should be made optional
export type PartialPick<T, F extends keyof T> = Omit<T, F> & Partial<Pick<T, F>>;

// make some properties required 
type RequiredPick<T, F extends keyof T> = Omit<T, F> & Required<Pick<T, F>>;

```

## 0418

- [TS 2540: Cannot assign to style because it is a read-only property - Stack Overflow](https://stackoverflow.com/questions/64243292/ts-2540-cannot-assign-to-style-because-it-is-a-read-only-property)
  - `style` property is immutable, use `setProperty` method
  - `element.style.setProperty(propName, propValue)`

- [Remove all child elements of a DOM node in JavaScript - Stack Overflow](https://stackoverflow.com/questions/3955229/remove-all-child-elements-of-a-dom-node-in-javascript)
  - container.replaceChildren(); 

## 0417

- [TypeScript "Not a constructor function type" error after casting - Stack Overflow](https://stackoverflow.com/questions/59583659/typescript-not-a-constructor-function-type-error-after-casting)

```ts
class ClassA {
  field1: any;
}

const SomeClassAsA = diContainer.get('SomeClass') as ClassA;

class ClassB extends ClassA {} // works
class ClassB extends SomeClassAsA {} // error: Type ClassA is not a constructor function type

const SomeClassAsA = diContainer.get('SomeClass') as typeof ClassA; // ✅
```

- [How to assert a type of an HTMLElement in TypeScript? - Stack Overflow](https://stackoverflow.com/questions/12686927/how-to-assert-a-type-of-an-htmlelement-in-typescript)
  - Do not type cast. Never. Use type guards `if ((e instanceof HTMLScriptElement)) `; 
  - Rather than using a type assertion, type guard, or any to work around the issue, a more elegant solution would be to use generics to indicate the type of element you're selecting.
  - Unfortunately,  `getElementsByName` is not generic, but `querySelector` and `querySelectorAll` are. (querySelector and querySelectorAll are also far more flexible, and so might be preferable in most cases.)

## 0416

- [Prohibition against prefixing interfaces with "I" ](https://github.com/microsoft/TypeScript-Handbook/issues/121)
  - I-prefix violates encapsulation principle. Let's assume you get some black-box. You get some type reference that allows you to interact with that box. You should not care if it is an interface or a class. You just use its interface part (I from SOLID principle). Demanding to know what is it (interface, specific implementation or abstract class) is a violation of encapsulation.
  - Conformance. When in Rome principle. Major ts-based frameworks like Angular discorage using I prefix for interfaces. Rxjs also do not use I prefix.
  - I think thats because in TypeScript the interface is not just an pure object interface but it can be used to define interface to ctors, call signatures, indexable objects and maybe more I can't imaigine right now

- [Confused about the Interface and Class coding guidelines for TypeScript - Stack Overflow](https://stackoverflow.com/questions/31876947/confused-about-the-interface-and-class-coding-guidelines-for-typescript)
  - Protection from bad naming: you should not not define an ICar interface and an associated Car class. Car is an abstraction and it should be the one used for the contract. Implementations should have descriptive, distinctive names e.g. SportsCar, SuvCar, HollowCar.
  - If not, maybe the Java style of `SomeThing` (interface) with `SomeThingImpl` (implementation) then by all means use that.
  - I personally quite like the idea of turning a noun into an adjective by adding the `-able` suffix. It sounds very impropper, but I love it!

- [Width of stroke in an SVG icon - User Experience Stack Exchange](https://ux.stackexchange.com/questions/126020/width-of-stroke-in-an-svg-icon)
  - I'd like to use the "material" icons. Their design guidelines say, for outlined icons, To maintain legibility, the recommended stroke weight is 2dp for most icons. 2dp outlined icons remain readable across sizes and applications.

- [Icon Sizes and why SVG is not the Solution – Part 3/3 – SGrottel.de](https://www.sgrottel.de/?p=2079&lang=en)
  - we should go the extra mile also optimizing the graphics for exactly those sizes we aim for: 16×16, 24×24, 32×32, 48×48, and 64×64, traditionally.
  - 16×16 is very very small, and as written above looses it’s importance in the age of high resolution displays. Similar to the abstraction from a logo to and icon, as written in my first article of this series, many icons simplify and remove details when they go down from 32×32 pixel sized versions to the 16×16 pixel sized versions
  - the second reason are the in between sizes, infamously the 24×24 pixels. It’s a scaling factor of 1.5x from the 16×16 version. Any line might end up again in between pixels and blurry if you just scale up.
  - Personally, I usually try to design icons at 32×32 pixels. The 64×64 pixel and 256×256 pixel versions are then automatic upscales

## 0415

- [HTML : Is there any way to show images in a textarea? - Stack Overflow](https://stackoverflow.com/questions/3793090/html-is-there-any-way-to-show-images-in-a-textarea)
  - Use a div with contentEditable attribute which acts like a textarea. That's how wysiwyg editors are created.
  - you can use css to set an background image for textarea, and js to set the text

## 0414

- [react-dnd 16.0.0 is causing "Module not found: Error: Can't resolve 'react/jsx-runtime'" · Issue #3423 · react-dnd/react-dnd](https://github.com/react-dnd/react-dnd/issues/3423)
  - With Webpack and React 17, you can add this Webpack config so it knows where to find those files if they dont exist:

```JS
{
  resolve: {
    fallback: {
      'react/jsx-runtime': 'react/jsx-runtime.js',
      'react/jsx-dev-runtime': 'react/jsx-dev-runtime.js',
    },
  }
}
```

## 0411

- [Is there any difference between a GUID and a UUID? - Stack Overflow](https://stackoverflow.com/questions/246930/is-there-any-difference-between-a-guid-and-a-uuid)
  - The simple answer is: no difference, they are the same thing.
  - For most practical purposes, treat them as 16 byte (128 bits) values that are used as a unique identifier. In Microsoft-speak they are called GUIDs, but call them UUIDs when not using Microsoft-speak.
  - GUID is Microsoft's implementation of the UUID standard.
  - RFC 4122 itself states that UUIDs "are also known as GUIDs". All this suggests that "GUID", while originally referring to a variant of UUID used by Microsoft, has become simply an alternative name for UUID…
  - One difference between GUID in SQL Server and UUID in PostgreSQL is letter case; SQL Server outputs upper while PostgreSQL outputs lower.

## 0407

- [NodeJS - setTimeout(fn, 0) vs setImmediate(fn) - Stack Overflow](https://stackoverflow.com/questions/24117267/nodejs-settimeoutfn-0-vs-setimmediatefn)
  - `setImmediate()` is to schedule the immediate execution of callback after I/O events callbacks and before `setTimeout` and `setInterval` .

- [OnsenUI : uncaught ReferenceError: setImmediate is not defined - Stack Overflow](https://stackoverflow.com/questions/52164025/onsenui-uncaught-referenceerror-setimmediate-is-not-defined)
  - `window.setImmediate = window.setTimeout; `

- [Type safety in JavaScript with JSDoc and VSCode - DEV Community](https://dev.to/t7yang/type-safety-in-javascript-with-jsdoc-and-vscode-1a28)

## 0406

```JS
// Number.prototype.toLocaleString()
3500. toLocaleString() // Uncaught SyntaxError: Invalid or unexpected token
3500..toLocaleString() // 3,500
```

## 0405

- [Can we add a `<span>` inside an `<h1>` tag? - Stack Overflow](https://stackoverflow.com/questions/7524185/can-we-add-a-span-inside-an-h1-tag)
  - Yes, it's typically fine to use a span inside of an h1. span is an inline element, so it's typically okay to use it inside anything

- [Can I createPortal from an onClick handler? - Stack Overflow](https://stackoverflow.com/questions/69324046/can-i-createportal-from-an-onclick-handler)
  - A better method to do it would be having the portaled element in a separate component and having a state in your `MyPage` component that renders the modal conditionally

```JSX
const MyPortaledModal = () => createPortal(<MyModalDialog />, document.body)

const MyPage = () => {
  const [shouldShowModal, setShouldShowModal] = useState(false);

  const toggleModal = () => setShowModal(prevValue => !prevValue)

  return (
    <div>
      <button onClick={toggleModal}>Click me</button>
      {shouldShowModal && <MyPortaledModal/>}
    </div>
  )
}
```

## 0404

- [Does TypeScript Interface have anonymous and named function? - Stack Overflow](https://stackoverflow.com/questions/41082804/does-typescript-interface-have-anonymous-and-named-function)
  - An "unnamed" member in a TypeScript interface does not refer to an anonymous member, but declares the function signature of the interfaced class itself

## 0403

- [How do I reload a page with react-router? - Stack Overflow](https://stackoverflow.com/questions/46820682/how-do-i-reload-a-page-with-react-router)

```JS
// react-router v6
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();

const refreshPage = () => {
  navigate(0);
}
```

## 0402

- 🆚️ [Is it fine to use JSON.stringify for deep comparisons and cloning? - Stack Overflow](https://stackoverflow.com/questions/15376185/is-it-fine-to-use-json-stringify-for-deep-comparisons-and-cloning)
  - JavaScript does not guarantee the order of keys.
  - If they are entered in the same order, this approach would work most of the time, but it would not be reliable.

```JS
JSON.stringify(NaN) === JSON.stringify(null)
// => true

JSON.stringify(Infinity) === JSON.stringify(null)
// => true
```

# dev-03-realworld-react-sequelize-knex-&-strapi-version-history

## 0324

```JS
import * as TOML from 'https://jspm.dev/@ltd/j-toml@1.29';
```

## 0323

- [Using the Compiler API · microsoft/TypeScript Wiki](https://github.com/Microsoft/TypeScript/wiki/Using-the-Compiler-API)

```ts
import * as ts from "typescript";

function compile(fileNames: string[], options: ts.CompilerOptions): void {
  let program = ts.createProgram(fileNames, options);
  let emitResult = program.emit();
  }
```

## 0322

- [Failed to resolve import. Does the file exist? since 5.1.0-beta.4 (5.1.0-beta.3 was fine) · vitejs/vite](https://github.com/vitejs/vite/issues/15784)
  - I guess it may be related to the path cache.  server: { fs: { cachedChecks: false } }
  - 实测需要重启dev-server

## 0319

- [Remove leftover `unstable_` prefix from `Blocker`/`BlockerFunction` types by brophdawg11 · Pull Request #11187 · remix-run/react-router](https://github.com/remix-run/react-router/pull/11187)
  - This pull request first appeared in react-router@6.21.3-pre.0

- [MIME type ('text/html') is not executable, and strict MIME type checking is enabled - Stack Overflow](https://stackoverflow.com/questions/49617440/mime-type-text-html-is-not-executable-and-strict-mime-type-checking-is-enab)
  - Try changing `webpack.config.js` add `publicPath`.
  - `publicPath: '/'`

- [通用唯一识别码 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E5%94%AF%E4%B8%80%E8%AF%86%E5%88%AB%E7%A0%81)
  - UUID是用于计算机体系中以识别信息的一个128位标识符。
  - UUID按照标准方法生成时，在实际应用中具有唯一性，且不依赖中央机构的注册和分配。UUID重复的概率接近零，可以忽略不计
  - UUID 的 16 个 8 位字节表示为 32 个十六进制数字，由连字符 '-' 分隔成五组显示，形式为“8-4-4-4-12”总共 36 个字符（32 个十六进制数字和 4 个连字符）。
  - xxxxxxxx-xxxx-Mxxx-Nxxx-xxxxxxxxxxxx
  - M表示 UUID 版本，数字 N的一至三个最高有效位表示 UUID 变体
  - UUID的变体1是目前世界最常见的UUID，完全以大端序（big-endian）二进制存储与传输 UUID 。

## 0318

- [ReferenceError: Cannot access x before initialization _202008](https://github.com/pmmmwh/react-refresh-webpack-plugin/issues/190)
  - 由 react-refresh webpack热加载插件导致的异常
  - To be clear, this is not a problem that only exists on our side - it is a limitation of HMR of Webpack (or potentially any other bundlers that creates a module graph). 
  - When a graph needs to be created and there exists cyclic references, the order of which node is created first can be nondeterministic, which means while your app could work in production, it will not work in development with HMR enabled.
  - Generally, I think the Webpack maintainers hold a similar stance as I do - cyclic dependencies are bad.you should try eliminate them
- This is really an unexpected meeting. We have seen the same problem and come out with a way to solve it In Rspack.
  - The problem is caused by eagerly accessing some un-initialized variables declared by const. The accessing is done due to the react-refresh need to access each export of modules. By making accessing laziness, we solved the problem

- [run-p: command not found - Stack Overflow](https://stackoverflow.com/questions/53252424/run-p-command-not-found)
  - npm i npm-run-all --save-dev

- [2024 年，该如何写一个全面兼容的 NPM 库 - 静かな森](https://innei.in/posts/tech/write-a-universally-compatible-js-library-with-fully-types)

## 0317

- [Assignment (=) - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment)
  - The assignment (=) operator is used to assign a value to a variable or property. 
  - 💡 The assignment expression itself has a value, which is the assigned value. This allows multiple assignments to be chained in order to assign a single value to multiple variables

## 0316

- [Why use parentheses when returning in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/20824558/why-use-parentheses-when-returning-in-javascript)
  - Using parentheses when returning is necessary if you want to write your return statement over several lines.

- TypeError: Illegal invocation
  - 创建函数别名时记得bind
  - const qs = document.querySelector.bind('document'); 

- Cannot find name 'DocumentAndElementEventHandlers'
  - [HTMLElement definition in typescript.lib/lib.dom.d.ts was overridden by @types/react/global.d.ts - Stack Overflow](https://stackoverflow.com/questions/54167595/htmlelement-definition-in-typescript-lib-lib-dom-d-ts-was-overridden-by-types-r)
  - ts类型定义更新快，查找同名interface的extends或属性名称的变化

## 0313

- [How to Create a Custom API Endpoint in Strapi? - DEV Community](https://dev.to/strapi/how-to-create-a-custom-api-endpoint-in-strapi-2pa4)
  - go to the Setting > Roles > Public in the Strapi dashboard. 
  - Please, check the final for the pages-report route and hit the save button.

- [How to Create a Custom API Endpoint in Strapi](https://strapi.io/blog/how-to-create-a-custom-api-endpoint-in-strapi)
  - In order to make the end-point accessible only to the authenticated users, go to the Settings > Roles > Authenticated

- [Puppeteer国产镜像地址不能用了？ - 知乎](https://zhuanlan.zhihu.com/p/637107614)
  - 对于Puppeteer20.1以上的版本，可以 
  - puppeteer-download-base-url="https://cdn.npmmirror.com/binaries/chrome-for-testing"
  - 19以下版本还是原来的方式
  - puppeteer-download-host="https://cdn.npmmirror.com/binaries"

## 0312

- [Postgresql GROUP_CONCAT equivalent? - Stack Overflow](https://stackoverflow.com/questions/2560946/postgresql-group-concat-equivalent)
  - `select string_agg(distinct column1, ', ') as tagList from tags`; 
  - If column type is integer, don't forget to convert or use `concat(column, '')` for implicit conversion

- [sql - must appear in the GROUP BY clause or be used in an aggregate function - Stack Overflow](https://stackoverflow.com/questions/19601948/must-appear-in-the-group-by-clause-or-be-used-in-an-aggregate-function?answertab=scoredesc#tab-top)
  - 实测的解决方法是，将异常中必需的字段手动添加到group by

- ["message":"Error: TypeError: (intermediate value) is not iterable" - Stack Overflow](https://stackoverflow.com/questions/75157742/messageerror-typeerror-intermediate-value-is-not-iterable)
  - you can't use destructuring on undefined.

- [knex.js: combination of orWhere followed by multiple where - Stack Overflow](https://stackoverflow.com/questions/64912025/knex-js-combination-of-orwhere-followed-by-multiple-where)
  - `.where(function () { this.orWhere({'Project.productType': 1}).orWhere({'Project.productType': 2}) });`

## 0310

- [golang pq sql driver: pq: invalid input syntax for type uuid error type - Stack Overflow](https://stackoverflow.com/questions/69305845/golang-pq-sql-driver-pq-invalid-input-syntax-for-type-uuid-error-type)
  - In the query you can cast the uuid column to text

- [Postgres SELECT where the WHERE is UUID or string - Stack Overflow](https://stackoverflow.com/questions/46433459/postgres-select-where-the-where-is-uuid-or-string)
  - Casting the UUID column to ::text stops the error.

```SQL
SELECT * FROM user
WHERE id::text = '33bb9554-c616-42e6-a9c6-88d3bba4221c' 
  OR uid = '33bb9554-c616-42e6-a9c6-88d3bba4221c';
```

## 0309

- [What is the difference between “rethink” and “think again”? - English Language & Usage Stack Exchange](https://english.stackexchange.com/questions/444690/what-is-the-difference-between-rethink-and-think-again)
  - ‘think again’ is the simple long-established English way of expressing the idea.
  - 'Think Again" carries the certainty that the other person is wrong, whereas 'please rethink' is simply a request that they reconsider.

- [Is it "twice more" or "twice again" ? : r/ENGLISH](https://www.reddit.com/r/ENGLISH/comments/14wsisp/is_it_twice_more_or_twice_again/)
  - "two times" is replaced by "twice".
  - “Two more times” is correct. “Twice more” sounds wrong.
  - "twice more" = the amount of times that it happened goes up by two.
  - "twice again" = it happened two times, and then it happened two times after that.

## 0307

- [Sequelize error - "model.get is not a function" - Stack Overflow](https://stackoverflow.com/questions/46475953/sequelize-error-model-get-is-not-a-function)

- [css - What is the difference between :focus and :active? - Stack Overflow](https://stackoverflow.com/questions/1677990/what-is-the-difference-between-focus-and-active)
  - `:focus` represents the state when the element is currently selected to receive input
  - `:active` represents the state when the element is currently being activated by the user.
  - when you click on an element, you give it focus, which also cultivates the illusion that :focus and :active are the same. They are not the same. When clicked the button is in `:focus:active` state.

## 0305

- [Extend Express Request object using Typescript - Stack Overflow](https://stackoverflow.com/questions/37377731/extend-express-request-object-using-typescript)
  - Solving this with .d.ts declarations is hack. Accept the fact that express' middleware system is not for typescript. I suggest not to use them.

```typescript
// 在 src/types.ts 添加自定义覆盖类型
declare namespace Express {
   export interface Request {
      tenant?: string
   }
}

```

- [Express middleware with TS: void' is not assignable to parameter of type 'PathParams' - Stack Overflow](https://stackoverflow.com/questions/73505586/express-middleware-with-ts-void-is-not-assignable-to-parameter-of-type-pathpa)
# dev-02-airtable-db-dash-&-hexo-eg-&-strapi-eg

## 0228

- [reactjs - How to use Private route in react-router-dom@v6 - Stack Overflow](https://stackoverflow.com/questions/69923420/how-to-use-private-route-in-react-router-domv6)

```JSX
import { Navigate, type RouteProps } from 'react-router-dom'; 

export function PrivateRoute({ children }: RouteProps) {
  const isLoggedIn = checkUser() // check cookie or local storage etc
  return (
     isLoggedIn
        ? children
        : <Navigate to="/sign-in"/>
  );
}

// <Route path="/" element={ <PrivateRoute> <AdminPage /> </PrivateRoute> } />
```

- [node.js - Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './lib/tokenize' is not defined by "exports" in the package.json of a module in node\_modules - Stack Overflow](https://stackoverflow.com/questions/69693907/error-err-package-path-not-exported-package-subpath-lib-tokenize-is-not-d)
  - Remove node_modules folder and .lock file and re-install your packages (yarn or npm). It worked for me with last 17.0.1 of nodejs, I can npm (or yarn) start my app again.

- [Disable ESLint that create-react-app provides - Stack Overflow](https://stackoverflow.com/questions/55821078/disable-eslint-that-create-react-app-provides)
  - `DISABLE_ESLINT_PLUGIN=true react-scripts start`

- [How can I disable all typescript type checking? - Stack Overflow](https://stackoverflow.com/questions/54506744/how-can-i-disable-all-typescript-type-checking)
  - `TSC_COMPILE_ON_ERROR=true`

## 0225

- [Attach Authorization header for all axios requests - Stack Overflow](https://stackoverflow.com/questions/43051291/attach-authorization-header-for-all-axios-requests)
  - I have explained the two most common approaches.
  - you can use axios interceptors to intercept any requests and add authorization headers.
    - config.headers.Authorization =  token;
  - there is a mechanism available which allows you to set default header which will be sent with every request you make.
    - axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
  - A minor gotcha: You will have to set default headers for each instance of Axios in your application separately if you are following second method. This took me a while to figure out
  - Sometimes you get a case where some of the requests made with axios are pointed to endpoints that do not accept authorization headers. Thus, alternative way to set authorization header only on allowed domain is as in the example below
- never store token in localStorage
  - the most secure way would be that server sets cookie with token. Important thing - cookie should have attributes "httpOnly" and "secure". And axios should not worry about token, because that cookie would be attached to request header. 
  - The other approach (which usually is used by third party auth libraries, for example MSAL) - to store in session storage (and not in local storage). In this case would be necessary to define `Authorization` header as in Your example. 

- [A neat little trick with JavaScript's indexOf() - DEV Community](https://dev.to/werninator/a-neat-little-trick-with-javascripts-indexof-4dj5)
  - The Bitwise NOT-Operator ~ It flips all bits of a number
  - 按位非 ~num 等价于 -num -1, 只有num为-1时为0(falsy)，其余值的~num都为truthy
  - Unless one will reuse the index in other places, I like to recommend `includes` instead of `indexOf`. I think it's more readable.

```JS
var arr = [1, 2, 3, 'foo'];

// old way
if (arr.indexOf('foo') > -1) {
  console.log('"foo" is in "arr"!');
}

// new way
if (~arr.indexOf('foo')) {
  console.log('"foo" is in "arr"!');
}
```

## 0224

- [Remove all subfolders in Node using globs with the help of rimraf package? - Stack Overflow](https://stackoverflow.com/questions/58056804/remove-all-subfolders-in-node-using-globs-with-the-help-of-rimraf-package)
  - You can simply use `rimraf dist/*/` to remove all the subfolders within a particular folder.
  - This will remove subfolders and will preserve all the other extensions file.

## 0206

- [How to restore MySQL dump from host to Docker container - Stack Overflow](https://stackoverflow.com/questions/46579381/how-to-restore-mysql-dump-from-host-to-docker-container)
  - docker exec containerid mysqldump -u root --password=pass portal-db > lower-portal-db.sql
  - cat lower-portal-db.sql | docker exec -i containerid mysql -u root --password=pass portal-db

- [Flutter App stuck at "Running Gradle task 'assembleDebug'... " - Stack Overflow](https://stackoverflow.com/questions/59516408/flutter-app-stuck-at-running-gradle-task-assembledebug)

- [AS Gradle镜像配置 - 掘金](https://juejin.cn/post/7213138784810991677)
  - 全局； 局部项目

## 0205

- 💡🔁 postgresql将docker数据库迁移到本地数据库 /#devlog
  - pg_dump支持连接到remote后再dump，导出sql格式是最通用的，还可以手动修改
  - remote的pg可能启用了插件，此时要先在本地启用插件如uuid
  - 对着error一个个处理，可能github-issues已经说明了
  - dbeaver的tools-dump导出后，不能通过tools-restore恢复，是已知的bug

- su: Authentication failure
  - 使用 sudo su - postgres

- [postgresql - COPY FROM STDIN does not work in liquibase - Stack Overflow](https://stackoverflow.com/questions/59214217/copy-from-stdin-does-not-work-in-liquibase)
  - Mixing the `COPY` statement and the data in the same file only works in `psql` scripts.
  - You should use `INSERT` statements in your script. If you want to load a pg_dump with the JDBC driver, use `pg_dump --inserts` (but expect slower performance).

- [pg_restore: [archiver] input file appears to be a text format dump. Please use psql. · dbeaver/dbeaver](https://github.com/dbeaver/dbeaver/issues/3972)
  - pg_restore can't import plain SQL files. Its a job for psql. Also it is possible to run SQL dump as script in DBeaver.

- pg_restore: error: could not execute query: ERROR:  function public.uuid_generate_v4() does not exist
- [How to deal with : Function uuid_generate_v4() does not exist on PostgreSQL - DEV Community](https://dev.to/wteja/how-to-deal-with-function-uuidgeneratev4-does-not-exist-on-postgresql-3fb4)
  - CREATE EXTENSION IF NOT EXISTS "uuid-ossp"; 

- [How to backup and restore a PostgreSQL database via DBeaver - Databases - Pyramid Analytics Community Forum](https://community.pyramidanalytics.com/t/h7hk07w/how-to-backup-and-restore-a-postgresql-database-via-dbeaver)

- [postgresql 9.5 - Can't backup db: libpq.so.5: cannot open shared object file: No such file or directory - Stack Overflow](https://stackoverflow.com/questions/74463039/cant-backup-db-libpq-so-5-cannot-open-shared-object-file-no-such-file-or-dir)
  - Make sure you are not using the flatpak version, I had the same problem with this version, if you are using it, uninstall and download the .deb package and install from there.

- [DBeaver Documentation - backup](https://dbeaver.com/docs/dbeaver/Backup-Restore/#backup-postgresql-database)
  - When performing a Global PostgreSQL database Backup, the entire database is dumped, including roles and tablespaces. 
  - This differs from standard backup procedures where only specific schemas and their contents can be selected. 
  - Additionally, multiple databases can be chosen for backup at once in the global method.

- ### 🐘 [PostgreSQL的模式、表、空间、用户间的关系 - 掘金](https://juejin.cn/post/6844903987762692103)
- 一个数据库包含一个或多个已命名的模式schema，模式又包含表table。
  - 模式还可以包含其它对象， 包括数据类型、函数、操作符等。同一个对象名可以在不同的模式里使用而不会导致冲突； 比如，herschema和myschema都可以包含一个名为mytable的表。 
- 和数据库不同，模式不是严格分离的：只要有权限，一个用户可以访问他所连接的数据库中的任意模式中的对象。
- 需要模式的原因有好多：
  - 允许多个用户使用一个数据库而不会干扰其它用户。
  - 把数据库对象组织成逻辑组，让它们更便于管理。
  - 第三方的应用可以放在不同的模式中，这样它们就不会和其它对象的名字冲突。
- 模式类似于操作系统层次的目录，只不过模式不能嵌套。

- 模式(schema)是对数据库(database)逻辑分割。
  - 在数据库创建的同时，就已经默认为数据库创建了一个模式--public，这也是该数据库的默认模式。所有为此数据库创建的对象(表、函数、试图、索引、序列等)都是创建在这个模式中的
  - 一个数据库至少有一个模式，所有数据库内部的对象(object)是被创建于模式的。用户登录到系统，连接到一个数据库后，是通过该数据库的search_path来寻找schema的搜索顺序，可以通过命令SHOW search_path；
  - 官方建议是这样的：在管理员创建一个具体数据库后，应该为所有可以连接到该数据库的用户分别创建一个与用户名相同的模式，然后，将search_path设置为$user，即默认的模式是与用户名相同的模式。

- 表空间是实际的数据存储的地方。
  - 一个数据库schema可能存在于多个表空间，相似地，一个表空间也可以为多个schema服务。
  - 通过使用表空间，管理员可以控制磁盘的布局。表空间的最常用的作用是优化性能，例如，一个最常用的索引可以建立在非常快的硬盘上，而不太常用的表可以建立在便宜的硬盘上，比如用来存储用于进行归档文件的表。

- 默认的数据库所有者是当前创建数据库的角色，默认的表空间是系统的默认表空间`pg_default`。
  - 在PostgreSQL中，数据的创建是通过克隆数据库模板来实现的，这与SQL SERVER是同样的机制。由于CREATE DATABASE dbname并没有指明数据库模板，所以系统将默认克隆template1数据库，得到新的数据库dbname。(By default, the new database will be created by cloning the standard system database template1)
  - template1数据库的默认表空间是pg_default，这个表空间是在数据库初始化时创建的，所以所有template1中的对象将被同步克隆到新的数据库中。
  - 在PostgreSQL中，表空间是一个目录，里面存储的是它所包含的数据库的各种物理文件。

- 表空间是一个存储区域，在一个表空间中可以存储多个数据库，尽管PostgreSQL不建议这么做，但我们这么做完全可行。
  - 一个数据库并不知直接存储表结构等对象的，而是在数据库中逻辑创建了至少一个模式，在模式中创建了表等对象，将不同的模式指派该不同的角色，可以实现权限分离，又可以通过授权，实现模式间对象的共享，public模式可以存储大家都需要访问的对象。
- 表空间用于定义数据库对象在物理存储设备上的位置，不特定于某个单独的数据库。
  - 数据库是数据库对象的物理集合，而schema则是数据库内部用于组织管理数据库对象的逻辑集合，schema名字空间之下则是各种应用程序会接触到的对象，比如表、索引、数据类型、函数、操作符等。

## 0202

- [How to get the measurementId from the Firebase config? - Stack Overflow](https://stackoverflow.com/questions/60804074/how-to-get-the-measurementid-from-the-firebase-config)
  - it is displayed when you enable Google analytics first time for the project.
# dev-01-pouchdb-idb-rspack-rebuilt-&-ethercalc-ot-&-joplin-note

## 0131

- [Error: error:0308010C:digital envelope routines::unsupported (Node.js v19.4.0) - Stack Overflow](https://stackoverflow.com/questions/75167770/error-error0308010cdigital-envelope-routinesunsupported-node-js-v19-4-0)

```shell
# linux
export NODE_OPTIONS=--openssl-legacy-provider
# win
set NODE_OPTIONS=--openssl-legacy-provider

npm start
```

## 0117

- [ERR_IMPORT_ASSERTION_TYPE_MISSING for import of json file - Stack Overflow](https://stackoverflow.com/questions/70106880/err-import-assertion-type-missing-for-import-of-json-file)

```JS
import { createRequire } from 'node:module';
const require = createRequire(
  import.meta.url);

const countryTable = require('./data/countries.json');
```

- [Error: require() of ES modules is not supported when importing node-fetch - Stack Overflow](https://stackoverflow.com/questions/69041454/error-require-of-es-modules-is-not-supported-when-importing-node-fetch)

```typescript
import { RequestInfo, RequestInit, Response } from 'node-fetch'

const _importDynamic = new Function('modulePath', 'return import(modulePath)')

export const nodeFetch = async function (url: URL | RequestInfo, init?: RequestInit): Promise<Response> {
  const { default: fetch } = await _importDynamic('node-fetch')
  return fetch(url, init)
}
```

- [How do I use “require” and ESM “import” in the same project? - Stack Overflow](https://stackoverflow.com/questions/71884616/how-do-i-use-require-and-esm-import-in-the-same-project)

```JS
import Module from "node:module";
const require = Module.createRequire(
  import.meta.url);
```

## 0116

- [shell中冒号 : 用途说明 - nowgood - 博客园](https://www.cnblogs.com/nowgood/p/shellmaohao.html)
  - 在Linux系统中，冒号(:)常用来做路径的分隔符（PATH），数据字段的分隔符（/etc/passwd）等。
  - 其实，冒号(:)在Bash中也是一个内建命令，它啥也不做，是个空命令、只起到占一个位置的作用
  - No effect; the command does nothing beyond expanding arguments and performing any specified redirections. A zero exit code is returned.
  - 没有想好或完成相应的代码，这时就可以用: 来做占位符
  - 单行注释 : your comment # your comment
  - 清空文件file的内容 : >file
  - 默认参数 : ${VAR:=DEFAULT}

- [bash - Explanation of colon operator in `: ${foo=value}` - Stack Overflow](https://stackoverflow.com/questions/7444504/explanation-of-colon-operator-in-foo-value)
  - it also returns the assigned value
  - if you simply executed `${SOMETHING='value'}`, then your shell would try to invoke the command value. This might or might not do something unwanted; 
  - the no-op :, which evaluates its argument and then throws it away, rather than executing it. 

## 0112

- [Instead change the require of index.js, to a dynamic import() which is available in all CommonJS modules - Stack Overflow](https://stackoverflow.com/questions/70541068/instead-change-the-require-of-index-js-to-a-dynamic-import-which-is-available)
  - const fetch = (...args) => import('node-fetch').then(({default: fetch}) => fetch(...args)); 

- [How to use dynamic import from a dependency in Node.js? - Stack Overflow](https://stackoverflow.com/questions/71432755/how-to-use-dynamic-import-from-a-dependency-in-node-js)
  - await import("my-plugin")	
  - await import("/parent/node_modules/my-plugin/dist/index.js")	

## 0111

- [babel plugin 的 loose 模式是什么](https://github.com/fengzilong/pso/issues/7)
  - 开启：会生成更贴近 ES5 风格的代码
  - 关闭：会生成尽可能严格遵循 ES next 语法的代码
  - 优点：代码更易读，在一些浏览器上可能兼容性更好，运行更快
  - 缺点：当你想切换回 native ES 语法时，这个过程可能会出现不兼容的情况，因为你的代码使用了编译后的不严格的代码，存在风险
  - 所以大部分情况下，不建议开启 loose 模式

- [详解利用webpack的splitChunk拆分打包文件 - 掘金](https://juejin.cn/post/7101555050194927624)
  - splitChunks的配置项都是作用于cacheGroup上的，也就是cacheGroups缓存组可以继承和覆盖来自 splitChunks.* 的任何选项

- [webpack 拆包：关于 splitChunks 的几个重点属性解析 - 掘金](https://juejin.cn/post/7118953143475372039)
  - 对于异步导入，splitChunks 分离出 chunks 形成单独文件来重用，而对于同步导入的相同模块没有处理，这就是 chunks: 'async' 的默认行为
  - initial 与 async 的区别：同步导入的模块也会被选中分离出来。
  - 在 initial 设置下，就算导入的是同一个模块，但是同步导入和异步导入是不能复用的。
  - 把 chunks 设置为 all，不管是同步导入还是异步导入，m3.js 都分离并重用了。

- [webpack and yarn magic against duplicates in bundles](https://www.developerway.com/posts/webpack-and-yarn-magic-against-duplicates-in-bundles)
  - https://github.com/atlassian-labs/webpack-deduplication-plugin
  - NormalModuleReplacementPlugin — it gives the ability to replace one file with another file during build time based on a regular expression

## 0110

- [Module not found: Can't resolve '@swc/helpers/src/_class_private_field_init.mjs' using NextUI with Next.js 13 - Stack Overflow](https://stackoverflow.com/questions/76083438/module-not-found-cant-resolve-swc-helpers-src-class-private-field-init-mjs)
  - npm install @swc/helpers

## 0104

- [Project must list all files or use an 'include' pattern - Stack Overflow](https://stackoverflow.com/questions/60029058/project-must-list-all-files-or-use-an-include-pattern)
  - In my case I was building a monorepo and referencing one of the packages into another package.
  - All I had to do was remove `composite: true` from tsconfig.json and it worked.

## 0103

- [How to specify registry while doing npm install with git remote url? - Stack Overflow](https://stackoverflow.com/questions/35622933/how-to-specify-registry-while-doing-npm-install-with-git-remote-url)
  - `npm install pkg11 --registry=https://registry.npmjs.org`
