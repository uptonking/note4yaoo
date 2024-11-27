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
- coding-tools
  - https://denigma.app/#demo
  - https://code-mentor.ai/
  - [TypeScript to plain JavaScript](https://transform.tools/typescript-to-javascript)

```shell
# delete all node_modules folders recursively
rm package-lock.json && find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + && find . -name 'dist' -type d -prune -exec rm -rf '{}' + && find . -name '.next' -type d -prune -exec rm -rf '{}' +

find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + 

# 格式化当前包，注意在子文件夹执行命令也会从package.json目录开始格式化整个包
prettier --write '**/*.{js,jsx,ts,tsx,json}' --ignore-unknown
eslint --ext .js,.ts,.tsx --quiet --fix . 

# npm i
  DEBUG=* npm i --no-audit --loglevel silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel=silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel=silly --registry=https://registry.npmmirror.com

npm --registry=https://registry.npmmirror.com install   axios
yarn add axios --registry=https://registry.npmjs.org/  
pnpm install --registry=https://registry.npmmirror.com  

export https_proxy=http://127.0.0.1:7890;export http_proxy=http://127.0.0.1:7890;export all_proxy=socks5://127.0.0.1:7890

$$('[contenteditable]')

flatpak run com.discordaspp.Discord --proxy-server="socks5://127.0.0.1:7897"
betterdiscordctl -i flatpak install

npx create-strapi@rc strapi5-play-202408 --use-npm --quickstart --ts --skip-cloud

npx create-strapi@latest --ts --use-npm --git-init  --example --skip-cloud --skip-db    --quickstart ./emptyFolder

stt.message.channel().send('uResetTask')
stt.message.channel().send('uCmdK', 'script.mjs',1,1,'write a quick sort algorithm')
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
    - 基于oplog实现partial-sync
  - pijul: crdt + vcs

- long-term-support
  - cms, airtable, lowcode
- techstacks-to
  - async/generator, stream, buffer, binary, scheduler, arrow
  - 样式片段也可在线尝试: codepen, w3schools.com 

- separate storage compute example
  - `Lovefield` uses a plug-in architecture for data stores. All data stores implement `lf.BackStore` interface so that query engine can be decoupled from actual storage technology.

- cache/stream for web storage
  - 参考 tanstack-query, falcor, localforage

- 🤔 支持切换内存和异步数据源的示例
  - tanstack-table external data; ag-grid server-side row model
  - abstract-level, localforage
  - tupledb, tinybase
  - tiddlywiki, react-admin
  - service worker, falcor

- collab-sync, partial-sync
  - string-crdt: ? list-crdt
  - logux: sqlite-persistor, lww-with-hlc
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
  - Node定义采用ast, 如 unist
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

- functional-codebase: slate, tanstack-table, feathersjs
- why use es6 class
  - 运行时类型检查，instanceof
  - 既包含类型定义，又包含逻辑工具方法
    - 注意class有时也采用先定义interface再实现，此时ts type也合理了
    - 但应用层业务代码一般不需要定义单独interface
  - 方便调试，可直接log到对象及方法，函数里面的闭包变量更新难以定位
    - 也可提前将需要调试的属性或方法添加到闭包暴露的对象或window上
    - 闭包实现的私有属性更安全

- dev-xp-editor
  - 不仅要保持编辑器内容和视图同步，还要保持选区和内容同步
  - 编辑器外部相关面板的协同产品较少，如评论

- dev-later
  - crdt tutorials
  - 默认 last-write-win, 出现冲突时，提示用户选择版本
  - 离屏渲染, keep-alive
  - 分层渲染
  - 测试文档系统未登录的流程和mock

## ing

- not-yet
  - ~~elmesque-editor~~, 基于immutable思想实现的编辑器大多采用redux/elm风格
  - branching/versioned-doc
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav
  - todo remove hashId在编辑器model中有什么作用
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
    - ✨ 2个编辑器同一页面协同的示例未完成
    - cursor光标位置经常对不上
  - [x] streaming infinite-list/tree

- [Scrum Poker Online - Free Tool for Planning Poker](https://www.scrumpoker-online.org/en/room/64881797/scrum-poker)
# dev-11
- yaoo-proj
  - codemirror-devtools

- editor
  - tab自动补全
  - 打字动画优化，先对行数多的按行输出，再对行数少的按字符输出
  - 通过minimap快速定位diff视图位置
  - ~~readonly属性不生效~~

- diffView
  - 🚨 关闭diff视图显示打字动画后，无法使用cmdk，且cmdk-undo交互异常
  - diff-view的开关只在需要时显示，[ ] 开启关闭diff无需刷新编辑器
  - ✅ 关闭diff后也支持显示打字动画
  - ✅ 在行数多时按行打字，在行数少时按字符打字
  - ✅ 重构打字动画css，不会从下向上
  - 流式更新的文档内容，需要流式更新diff-view
  - ~~隐藏绿色部分后，红色部分是否显示行号~~，打字太快了，不用看行号

- cde
  - 变更文件列表在fork仓库时需要清空M标记
  - 重写驾驶舱侧边栏的header，让置顶卡片位置水平居中
  - changed-files-list
  - cde页面无法区分自己和其他用户
  - ~~快照文件编辑器的提示条~~

- agent
  - 系统token达到上限后，不能再制定计划，但现有计划也无法显示
  - 计划终止后，如何清理action，需要agent提供api

- animation
  - time machine show/hide
  - ~~action bar working/replaying~~

- time-machine
  - ❓ 追加step，同一cde内，用户A在回放，用户B追加完点执行，
    - 则用户A的的时光机处于什么状态
    - 若用户A取消跟随且自己执行回放，是否执行B追加过的已执行完的action
  - 文件树上文件路径变化后(如移动)，action信息显示的路径要变化吗，支持打开吗
  - 🚨 对于单action的任务，执行时openFile(带打字)，执行完会立即再次openFile(无打字)，体验不好
  - 在action执行rerun后，时光机回放模式取快照的逻辑需要根据action的快照次数确定
  - ~~回放模式点击第一个action，然后点击播放，没有播放~~
  - ~~终止后未执行的action在进度条仍然显示，状态是cancelled~~
  - ~~关闭machine再打开时，会强制再次打开editor~~
  - ~~时光机终止后，驾驶舱如何反馈，终止状态如何清理~~
  - ~~时光机在计划执行完后，追加action修改之前的文件并执行，此时点击后面的action打开文件时会一直显示loading~~
  - ~~终止需要二次确认~~
  - ~~live模式下暂停时支持终止~~
  - ~~machine组件unmount要手动清理时光机的定时器~~
- 回放模式
  - .pnpm-store文件夹应该默认隐藏，被ignore的文件不要显示，不要出现在changedFiles
    - 文件树打不开.pnpm-store文件夹
  - ~~最后一个action播放时进度条未显示loading~~
  - ~~.gitignore文件无法显示，需要在ideServer放开~~
  - 只读编辑器光标改为禁用箭头
  - diff效果有时显示不出来
  - 新增文件未显示A图标，显示的是M

- 🚧 cmdk实现计划 
  - [x] 工具条或快捷键唤起、隐藏
  - [x] 输入提示词，agent返回时显示diff
  - [x] undo: cmd+z回到diff, 恢复提示词和选区
  - [-] 部分stop/cancel， 注意agent返回内容的时机
  - [ ] followup
  - [ ] 部分accept
  - [x] diff工具条
  - [ ] agent写代码时的输入框显示动画边框
  - [ ] 🚨 悬浮输入框，第一行时唤起的输入框改为悬浮输入框(或将input显示在第2行)，全选也改为悬浮输入框
  - explain an elegant word in one sentence
    - rename to an elegant variable name
    - implement quick sort algorithm and add 2 test cases
    - show me how to implement quick sort algorithm using recursive and non-recursive approach separately, then add 5 test cases
  - bugs
    - 🚨 diff视图开关只在需要时显示
    - 🚨 测试恢复提示词
    - 🚨 多次cmdk后能正确恢复diff、原文
    - 🚨 cmd+del在input执行时会多执行一个del
    - cmdk针对选中全文的场景进行优化, ai会返回空{}
    - migrate to StateField
    - 等待ai返回结果时，禁止send，允许esc键取消输入框和丢弃ai返回结果
    - 若在ai写代码时或写完后但未accept时刷新页面，是否会丢失状态数据
    - 输入框无法在ctrl+a+DEL时删除
    - ✅ cmdk input输入框在undo后有时位置没有正确恢复，显示在diff视图中间而不是上面，在内容变化后选区位置也应变化
      - 一种思路是显示和隐藏前都保存pos
    - ~~键盘ac/rj~~
    - ~~输入框位置在修改内容如加减行后如何保持正确的位置~~
    - ~~reject后的diff视图 undo~~
    - ~~显示输入框时高亮原选区，undo时能恢复原选区~~
    - ~~处理esc隐藏输入框的undo/redo~~
    - ~~disable cmdk in readonly and diff-view~~
    - ~~cmdk + esc + cmd-z会显示diff~~
    - ~~sdk如何不使用sleep来获取chunk返回完成时的数据~~
    - ~~replace initial lines on ai responses~~
    - ~~diff anime gray bg~~
    - ~~disable cmd+k in diff-view(cursor支持多次cmdk唤起多个输入框)~~
    - ~~if input box is visible, cursor cannot be put in editor~~
  - 🤼🏻 dev-discuss
    - 🤔 ~~agent返回chunkMsg的时机是确定的吗，测试是在ok消息后等6s才返回chunkMsg且chunkMsg会在1s(或2s)内快速流式返回完~~
      - 为了让sdk编辑器及时获取更新内容，需要sleep大于6s才能开始打字动画
    - 👾 对同一选区第一次cmdk后reject, 第二次cmdk会保留第一次的修改
      - 就算第一次reject了点击光标到其他位置再将光标回到原位置，cmdk也会返回对旧内容的修改
    - cmdk后直接编辑，是否立即更新文档，特别是多人协作的场景是否支持diff-view协作
      - 用户ua在cmdk后显示doc2(与原文档doc1进行diff)，编辑在doc2；用户ub仍显示和编辑doc1
      - cursor支持直接编辑最新doc2
      - 用户ua在cmdk后未accept时，若用户ub删除了选区行，那么内容如何变化，输入框显示在哪里
    - 大多数cmdk的变更块只有1个，此时diff-view的实现可采用简化版实现单红单绿
      - 若cmdk的变更块超过1个，上下布局的diff-view方便确定范围，agent返回不是多个范围
    - 在undo时恢复编辑器内容之外的数据，如cmdk的输入框的内容，思路是将自定义stateField的数据也加入history
    - message chunk stop
      - 多人cmdk的返回代码会冲突吗
    - more
      - 输入框与editor绑定，这样能支持多editor
      - 输入框内容很多时，是否支持换行  => 不换行
      - 💡 悬浮状态的指令输入框实现时应该使用单独的dom，这样可以减少reflow, 还可以解决输入框因文档长导致输入框元素未被viewport渲染时不能作为sticky元素
      - 指令输入框与diff-view无关，在diff下触发cmdk~~会聚焦到输入框~~会提示关闭diff
    - impl
      - input出现后且发送prompt到ai前，若用户光标位置变化然后再发送prompt到ai，生成代码的位置仍在原选区的位置且在input输入框之下
    - 🌰 cursor的cmdk实现细节
      - cmdk后先修改绿色代码再accept后再修改，连续undo的表现是，先正常undo，然后undo到diff-view，然后保持在diff-view下undo，然后undo到原代码和输入框
      - 多次cmdk后连续undo，能恢复上一次cmdk的提示词prompt
      - 📌 cursor的指令输入框不能被del键删掉, cmdk后按backspace时输入框会显示在上一行之上
      - cursor的空行会显示cmd+k/l的指令提示
      - cmdk后，用户点击accept后，cmd+z会恢复diff-view；用户点击reject后，cmd+z会恢复diff-view吗(cursor会)
- cmdk-undo的难点
  - cmdk的输入框在redo时要恢复到正确的选区位置
  - 如何确定undo显示diff的条件，若用stateField, diff恢复后再次消失前的编辑也要支持undo
  - 输入指令内容prompt的存储和还原，不在编辑器的内容中，是保存在编辑器state之外还是之中
    - 可以将prompt内容保存在编辑器外(因为不需要reactivity)，prompt id保存在编辑器的state

- not-yet
  - ~~cmdk整体功能~~
  - ~~追加步骤、回放重构~~
  - 🤔 时光机获取快照使用uuid, ~~cancelled的action无法打开快照~~
  - 🚨 ai写代码打字效果的时机优化和样式优化
  - 同一step里追加步骤不能选择之前修改过的文件
  - ~~diff视图开关只在需要时显示~~
  - ~~支持撤销ai写的代码, diff工具条~~
  - tab-key; chat-apply
  - 防抖: cmdk， chat
  - 驾驶舱action列表支持打开文件
    - 🚨 打开已删除的文件未实现， 同时处理undo工具条的位置
    - 点击actionBar打开文件时，文件树对应文件应该被选中
    - 在文件树ui创建文件夹和命令行mkdir创建文件夹的permission不同
  - 驾驶舱聊天后直接apply代码到编辑器
  - regenerate plan/task/action
  - zustandx如何在一个store里面使用另一个store的值, 或重新架构store的内容
  - ~~演示之前测试cpu、内存~~
  - ~~私有项目的导入~~
  - ~~多标签打开同一个cde，文件树的头像会显示2个~~

## 110

- dev-log
  - ?
- dev-to
  - ?

 

```JS
stt.message.channel().send('uCmdK', 'README.md', 2, 2, 'explain an elegant word in one sentence')
stt.message.channel().send('message', '@@user_context[file://README.md:12-42, file://XXX]@@')
stt.message.channel().send('message', '@user_context[file://README.md:7-24]')

console.log(';; task ', taskState, runningTaskAction, task?.task_steps)

console.log(';; act-file-o ', currentOpenedActionId, shouldForceOpenFile, actionPath, currentFilePath)

console.log(';; taskActions', currentActionId, path, store.cdePlay.enableDiffView(), taskActions)
console.log(';; open-diff ', enableDiffAnimation, store.cdePlay.enableDiffView(), store.cdeReplay.isMachinePaused())
console.log(';; qryDiffSnap ', snapshotFrameResult)
```

```
^(?!42\["res).*
```

- ~~为什么ai执行同一个action期间会打开2次编辑器，且第2次的path是最新的~~
- 为什么 onTaskUpdated 事件会触发2次，中间刚好隔2s，然后 有时中间也会打开文件
  - action状态变化: wip-action1 > 2s > completed > 2s > wip-action2

- 📌 🔜
  - file-tree search input 支持快捷键隐藏搜索
  - 隐藏browser面板箭头跟随图标
  - 将快捷键在win下由cmd改为ctrl
  - .breakpoints的配置文件改为.1024breakpoint

- 快捷键改进
  - cmd+shift+f 的描述不包含docs/commands

## 1127

- [How can I make a div not larger than its contents? - Stack Overflow](https://stackoverflow.com/questions/450903/how-can-i-make-a-div-not-larger-than-its-contents)
  - display: inline-block
  - display: table
  - width: fit-content
  - width: intrinsic
  - 让子元素宽度相同的方法： flex: 1 1 0

- 昨天
  - 进行了regenerate重试和revert撤销的需求评审
  - 实现了快捷键展示说明的主要ui，核对了需求文档中的一部份快捷键，还剩一部份
  - 修复了ideServer未更新rgaStatus的问题
- 今天
  - 核对并交付快捷键pr
  - 修复cde高优先级的bug，特别是文件树容易达到1000个文件的限制而无法查看
  - 实现cde打开已删除文件失败的feature

## 1126

- ideServer收到manager的playgroundInfo事件时，会替换当前

- 昨天
  - 实现了clacky需求的重点快捷键，包括布局、时光机、编辑器3个方面
  - 实现了快捷键展示说明的主要ui
- 今天
  - 核对文档并在ui上隐藏一些未实现的快捷键，提交快捷键feature的pr
  - 修复体验测试相关的bug，特别是文件树容易达到1000个文件的限制而无法查看
  - 实现cde打开已删除文件失败的feature

## 1125

- 上周
    - 修复部分体验测试反馈的issue
    - 上线 add to chat
- 本周
    - 交付快捷键pr
    - 实现多个快照切换的feature
    - 修复cde相关issue
- 昨天
  - 实现了部分时光机操作相关快捷键
  - 在showmebug业务侧，解决了切换编程题时编辑器无法显示的问题，体验还有待改进
- 今天
  - 交付快捷键feature的pr
  - 修复体验测试相关的高优先级bug

- 不在文件树ui而通过api打开文件时，文件树上对应文件没显示选中状态
  - 方案1: daoPaas提供新api setFileSelected, 让前端手动设置文件选中的状态
  - 方案2: 在执行daoPaas.openFile时自动更新文件树的选中状态

## 1124

- [node.js - Yarn local packages dependencies - Stack Overflow](https://stackoverflow.com/questions/48686053/yarn-local-packages-dependencies)
  - yarn unlink 在原link的文件夹A执行，就会让使用方文件夹B下的node_modules的a包失效

## 1123

昨天
- 修复一些cde相关的bug
- 实现了布局切换相关快捷键

今天
- 实现编辑器和时光机操作相关快捷键

## 1122

- 昨天
  - 修复cde中文件树相关的多个bug，比较大的调整是默认显示隐藏文件
  - 实现一部分布局切换相关的快捷键
- 今天
  - 实现布局切换和编辑器相关的快捷键
  - 修复一些cde布局相关的bug

## 1121

- 昨天
  - 配合后端排查文件丢失的问题
  - 修复体验测试反馈的打开.sql文件卡顿的问题，也解决了打开普通大文件如package-lock.json卡顿的问题
- 今天
  - 修复cde高优先级bugs，特别是体验测试反馈相关的
  - 开始实现全局布局切换相关的快捷键，解决一些浏览器内置的快捷键冲突

## 1120

- 昨天
  - 给部分issue添加了关联标签
  - 可用性测试尝试了2个项目
- 今天
  - 修复cde高优先级bugs，特别是打开.sql文件卡顿或打不开
  - 开始实现全局布局切换相关的快捷键，解决一些浏览器内置的快捷键冲突

## 1119

- 昨天
    - 解决 add to chat 在前端的循环引用问题
    - 分别review add to chat在paas和clacky前端的pr，上午合入staging
- 今天
    - 梳理linear上的100多个issues，将相关的issue添加关联，有疑问的和测试、产品、老板确认
    - 完成clacky的体验报告
    - 开始实现clacky的重点快捷键

## 1118

- 上周
  - 交付了fileTree-search的功能
  - 实现了大部分add-to-chat的功能
- 本周
  - 交付clacky的重点快捷键的功能
  - 修复cde高优先级的issues
- 今天
  - 分别review add to chat在paas和clacky前端的pr，上午合入staging
  - 开始实现clacky的重点快捷键

## 1115

- 昨天
  - 完善代码引用在历史消息列表的交互细节
  - 联合paas/clacky/ai测试add to chat的功能
- 今天
  - 提交一版add to chat的pr，下午可以演示主流程
  - 准备下午的演示，修复相关的issue

## 1114

- [ multiple condition in ternary operator in jsx - Stack Overflow](https://stackoverflow.com/questions/46408983/multiple-condition-in-ternary-operator-in-jsx)
  - I would suggest using functions if your conditions get complicated, to not degrade your code readability.

- [javascript - Is it possible to put a switch statement inside of a Conditional (ternary)? - Stack Overflow](https://stackoverflow.com/questions/47488109/is-it-possible-to-put-a-switch-statement-inside-of-a-conditional-ternary)

```JS
// tl;dr: kind of, but you shouldn't do it since it is not that readable.
// It is better to use a verbose coding style. In your case something like this would be cleaner and more readable:

const a = 20;
const condition = a > 100;
const result = condition ? true : (() => {
  switch (a) {
    case 11:
      return 22;
    case 20:
      return 21;
    default:
      return 100;
  }
})();

console.log(result);
```

- 昨天
  - 在paas完善了add to chat按钮的消失隐藏条件
  - 在聊天输入框实现了添加代码引用的基本交互
- 今天
  - 完善取消代码引用的交互和渲染细节
  - 提交一版add to chat的pr
  - 开始clacky重点快捷键的实现

## 1113

- 昨天
  - 合并文件树搜索的pr, 今天会发到staging
  - 在编辑器实现代码工具条add to chat的按钮
- 今天
  - 在驾驶舱实现add to chat的聊天交互

- ui交互
  - 产品设计上，add to chat 最多支持引用几个代码块
  - 聊天框有最大高度吗

## 1112

- 昨天
  - 和产品设计讨论并调整了文件树搜索的显示隐藏条件和筛选过滤交互
- 今天
  - 合并文件树搜索的pr
  - 实现代码工具条add to chat

## 1111

- [css - How to increase cursor caret thickness in HTML? - Stack Overflow](https://stackoverflow.com/questions/67417961/how-to-increase-cursor-caret-thickness-in-html)
  - You can't change the way the cursor caret looks in a textarea. The most you can do is change the color
  - There a way, you can change the font-size of the textarea to bigger or smaller, the caret size will change according to it, its not the best way but its a solution

- [iframe嵌套其他网站提示连接被拒绝 - 明月南楼 - 博客园](https://www.cnblogs.com/mynl/p/16065589.html)
  - 最近开发项目中遇到了客户iframe嵌套我们项目，遇到了域名提示... 拒绝了您的访问。
  - 然后百度了一下 `X-Frame-Options`： HTTP 响应头是用来给浏览器 指示允许一个页面 可否在`<frame>, <iframe>, <embed> 或者 <object>` 中展现的标记。站点可以通过确保网站没有被嵌入到别人的站点里面，从而避免 点击劫持 攻击。

- 搜索框一直显示的设计不符合ide
  - 显示变更文件的checkbox的条件是什么

上周
- 重构打字动画的实现
- 修复cde相关issues，修复了20多个
- 根据clacky的需求在paas调整了文件树及搜索的功能，完成了80%

本周
- 交付文件树搜索
- 代码工具条实现add to chat
- 全局快捷键

今天
- 合并文件树搜索的pr
- 实现add to chat的交互和通信

风险
- 文件树搜索的实现依赖goAgent的grep命令，需要在docker镜像中预安装这个包
- 和意如确定文件树搜索输入框的显示条件

## 1110

- 昨天
  - 根据clacky需求进一步完善文件树的搜索功能
- 今天
  - 提交文件树搜索的pr
  - 对接ai的add to chat通信逻辑

## 1108

- 昨天
  - 提交了打字动画的pr，还有改进的空间，以后抽时间再优化
  - 修复驾驶舱变更文件列表打开时不显示diff视图的问题
  - 接入paas的文件树搜索功能，根据设计稿进行调整
- 今天
  - 根据clacky需求进一步完善文件树的搜索功能
  - add to chat

## 1107

- 昨天
  - 优化打字动画的效果
- 今天
  - 文件树搜索
  - add to chat

## 1106

- 昨天
  - 调整打字动画的逻辑，实现在修改行数较多时按行打字，在修改行数较少时按字符
- 风险
  - ai打字的等待时间希望根据新增行数等待，而不是默认等2s
    - action对象的result属性的diff描述内容中包含新增文件的行数
  - 某些类型的action如新增文件，ai工作时跟随延迟的问题，前端难以解决
    - 希望ai先打开一个空白文件，然后再开始写
  - 某些类型的action，回放时应该如何交互产品定义不清晰，rename/move/文件夹操作
    - 对于文件路径不存在的场景，默认打开只读的快照文件

## 1105

- [Create dummy text using javascript - Stack Overflow](https://stackoverflow.com/questions/34123706/create-dummy-text-using-javascript)
  - 可将随机文本问题转换为在固定数组中获取有效下标元素的问题

- 昨天
  - 修复时光机快照相关pr合到staging
  - 调整打字动画的实现，关闭diff视图时也支持打字
- 今天
  - 调整打字动画的逻辑，在修改行数较多时按行打字，在修改行数较少时按字符
- 风险
  - ai工作时跟随延迟的问题，前端难以解决
  - 某些类型的action，回放时应该如何交互产品定义不清晰，rename/move/文件夹操作

## 1104

- 上周
  - 集中修复时光机终止、追加、回放、快照相关的issues，修复快照相关pr还没合到staging
  - 简单调整了打字动画的时机，避免多次打开文件多次渲染
- 本周
  - 花2天时间修复打字动画的效果和时机
  - 花1天时间修复ui、动效相关issues
  - 花2天时间完成本次迭代的feature，包括addToChat/fileTree-search
- 今天
  - 调整打字动画的逻辑，在修改行数较多时按行打字，在修改行数较少时按字符
    - 思路是设计diff视图的option支持几种模式 auto | byLine | byChar
  - 调整打字动画的实现，关闭diff视图时也支持打字
    - 关闭diff一定不刷新编辑器，打开diff可能刷新

## 1101

- ~~d42-tree-root-container  去掉 tansition 样式~~

昨天：
- 排查并解决了cde的编辑器编辑go语言文件卡顿的问题
- 修复显示快照action时不能切换文件的问题

今天：
- 修复快照action剩下的issue
- 打字动画优化
# dev-10-cmdk-reject-undo-&-cm-tooltip

## 1031

- paas
  - ~~agent新建文件后文件树未显示~~
  - ~~openFile处理异常 File does not exist~~
  - ~~显示部分隐藏文件，如 .gitignore~~

- frontend
  - think卡片打开文件，滚动到文件的行数
  - 🎨 计划画布展示、修改及对话
  - 付费订阅和积分扣减
  - ai控制台前端
  - 前端未控制member/owner的按钮、路由访问权限

昨天：
- 合并重构时光机回放的pr并上线staging，解决现有问题和产品需求变化
- 重构快照action的快照提示条的逻辑
- 排查clacky cde的编辑器几乎不能编辑go语言文件的问题

今天：
- 重构快照action的快照提示条的逻辑
- 排查clacky cde的编辑器几乎不能编辑go语言文件的问题
- 打字动画优化

## 1029

昨天：
- paas的browser组件支持配置logo，不会显示showmebug了
- 调整了时光机的追加步骤和播放逻辑，使得与驾驶舱保持一致

今天：
- 调整时光机的回放逻辑，执行完计划会自动回到第一个action并打开对应文件，使得live和playback模式的播放逻辑保持一致
- 处理快照action的快照提示条导致的多个issue

## 1028

上周：
- 重构右上角diff-view开关的显示隐藏时机，解决了此问题导致的多个issue
- 修复了diff工具条undo的在windows系统兼容性问题
- 修复了时光机的样式和终止计划、部分逻辑issue

本周：
- 先集中修复时光机追加步骤、回放相关issue
- 优化编辑器打字动画的时机和效果
- 处理本次迭代cde相关研发

今天：
- 重构时光机回放相关的逻辑，解决相关的多个issue

## 1025

- nx配置执行自定义命令的方法

```JS
// apps/webapp/project.json
// npx nx run webapp:dev1
{
  "targets": {
    "dev1": {
      "executor": "nx:run-commands",
      "options": {
        "cwd": "apps/webapp",
        "command": "next dev -H 0.0.0.0 -p 3000"
      }
    }
  }
}
```

- [How to host NextJS app on 0.0.0.0:3000 with nrwl/next (not localhost:3000) - Stack Overflow](https://stackoverflow.com/questions/70079560/how-to-host-nextjs-app-on-0-0-0-03000-with-nrwl-next-not-localhost3000)
  - `npx next dev -H 0.0.0.0 -p 3000`

## 1024

- 现在有个需求，前端需要获取当前打开的文件路径
  - 现有的fileOpenDone事件不能满足，因为关闭文件的时候没有发送事件

## 1023

- dev-to
  - AI在会话栏输出内容时，切换文件，无法将文件打开，只能等 AI 回复完毕才可以

昨天：
- 修复编辑器右上角的diff-view开关的显示时机
- 修复测试反馈的cmdk先关问题， 包括reject快捷键
- 修复时光机终止任务的action异常

今天：
- 集中修复追加步骤、回放相关问题

## 1022

昨天：
- 处理编辑器右上角diff开关显示时机的问题
- 处理时光机终止后action状态的issues

今天：
- 集中处理时光机终止和追加步骤、回放的逻辑
- 处理cmdk反馈的相关issue

## 1018

- [css - What's the difference between :focus-within and :has(:focus)? - Stack Overflow](https://stackoverflow.com/questions/78652185/whats-the-difference-between-focus-within-and-hasfocus)
  - So why to use :focus-within instead of &:focus, &:has(:focus), which depends entirely on your use-case (leaving the slight performance differences aside), you can see :focus-within as a shorthand like logical properties or that you can just write border: 1px solid red instead of writing border-color, border-width, ...

昨天：
- cmdk undo在clacky测试，修复影响体验的问题，比如undo后输入框位置有时不能正确恢复的问题
- 代码整理，提交pr

今天：
- 很明显的体验问题没有了，代码整理，code review和合并pr，让产品体验undo
- 修复时光机相关bug和高优先级bug

## 1017

昨天：
- 在clacky前端测试了cmdk undo的功能，修复了样式主题相关问题
- 整理代码，已提交pr

今天：
- 在clacky前端再测试一下，进行code review，将undo合入develop环境，很多实现细节产品文档没有描述，先让产品体验，根据产品反馈修改后再合入staging
- 修复linear上的高优先级bug

## 1015

昨天：
- 基本实现了代码工具条和diff工具条，分别用来唤起cmdk和undo，完成70%
- 协助排查rootThread有时编辑器显示的内容和文件实际内容不一致的问题，需要天平抽时间排查manager在执行修改文件命令后通知ideServer的逻辑

今天：
- 限制工具条的显示场景，只在业务需要时显示
- 修复linear上cmdk相关的bug，测试cmdk的完整功能并提pr
- 修复linear上的高优先级bug

风险 🤼   
- 解决数据不一致的思路待讨论，茂俊的思路是前端在进入cde时由前端通知manager先更新文件树和文件内容，我的思路是在通过api修改文件的call site立即由manager/goAgent通知更新
- [https://linear.app/clackyai/issue/C-1131/【cde】创建-thread-获取的文件列表代码内容，并不是最新的数据，导致需求无法实现](https://linear.app/clackyai/issue/C-1131/%E3%80%90cde%E3%80%91%E5%88%9B%E5%BB%BA-thread-%E8%8E%B7%E5%8F%96%E7%9A%84%E6%96%87%E4%BB%B6%E5%88%97%E8%A1%A8%E4%BB%A3%E7%A0%81%E5%86%85%E5%AE%B9%EF%BC%8C%E5%B9%B6%E4%B8%8D%E6%98%AF%E6%9C%80%E6%96%B0%E7%9A%84%E6%95%B0%E6%8D%AE%EF%BC%8C%E5%AF%BC%E8%87%B4%E9%9C%80%E6%B1%82%E6%97%A0%E6%B3%95%E5%AE%9E%E7%8E%B0#comment-3ef33df4)

## 1012

昨天：
- 完善cmdk undo的细节，输入框显示隐藏也支持undo
- 实现代码工具条唤起cmdk

今天：
- 检查linear上cmdk相关的bug
- 测试cmdk的整体功能，体验测试

## 1011

- cmdk需求沟通
  - cmdk的输入框必须支持undo撤销，否则会出现多个输入框
  - undo的效果采用4阶段还是3阶段: originalDoc > inputBox > inputBox提示词+showDiff > newDoc+hideDiff
  - 每次undo光标都会在编辑器内，不会撤销输入框的输入，只undo编辑器内容
  - 选中代码就会触发cmdk+chat工具条，未选中代码就会消失
  - ai计划内的文件默认自动打开diff视图(原文件vs最新文件)， 
    - 在无选区时的第一个变更块显示diff工具条，undo会撤销所有变更块恢复到原文件，
    - diff工具条的隐藏条件，不能手动隐藏而在关闭diff视图时隐藏，在有选区时不显示diff工具条而显示code工具条
    - regenerate执行的操作是什么 (重新执行ai计划最新的action，还是cmdk提示词)

昨天：
- 修复paas的i18n
- 完善了cmdk undo/redo的逻辑
- 开始实现工具条

今天：
- 实现cmdk的唤起工具条、diff工具条

## 1010

昨天：
- cmdk 多次undo的逻辑优化，探索了2种方法

今天：
- 采用比较hack的方法优化多次undo的逻辑
- 实现唤起cmdk的工具条

## 1009

- cmdk并接受代码的状态变化
  - original > new > showDiff > hideDiff

## 1008

- aws加速营的ai分享
  - 国内融资金额小一个数量级
  - ai的创业与学术相关
  - 国内外大厂都投入了大量资源
  - 小公司的toc机会不多，大厂也会做
  - ai创业，topc面向专业消费者的机会更大
- 十一分享
  - 泰国曼谷，脏乱差，很热，再也不想去了
# dev-09-cursorai-cmdk-pm-&-cm-block-widget-&-promise-socket-&-cm-undo-yet

## 0930

- 昨天：
0001. 将cmdk undo的实现方案从transactionFilter迁移到invertedEffects, 能更准确的确定diff显示隐藏的时机

- 今天：
0001. 继续实现基于invertedEffects的undo/redo, 测试普通模式下的undo/redo不受影响
0002. undo时恢复对应的提示词

## 0927

- ideServer-events
  - previous: followingAgentUser, followingFocusComponent, editorScroll, unFollowingAgentUser

昨天：
- 排查测试反馈的文件树不显示action创建文件的bug
- cmdk的undo实现完善
今天：
- 测试undo并提pr

## 0926

- 在paas的文件树创建文件时，ideServer会返回fileTree事件和fileOp事件数据用来更新文件树
  - FileTree组件会根据fileOp数据更新文件列表视图

```JS
["fileTree", { "eventName": "fileTree", "agentUesrId": "shell", "playgroundId": "711049437866319872", "dockerId": "711049437891485696", "data": { "action": "CREATE", "files": [{ "type": "FILE", "name": "aa3.js" }], "result": true }, "timestamp": 1727354351292 }]
```

## 0923

- 🤔 如何让一个clacky thread的playground里面的多个用户都能够在vscode打开cde的文件
  - 需要有一个thread是否已添加ssh密钥的api让前端直接获取
  - 👥💡 讨论后不需要后端添加api或新开发，前端若能在刷新页面后能展示ssh-key，就已添加

- team-to
  - 确定本次迭代的最后一天及demoday是周五还是放假前最后一天9月30号
    - 27号

## 0919

- [Resolving a promise inside a callback - Stack Overflow](https://stackoverflow.com/questions/55185103/resolving-a-promise-inside-a-callback)
  - Never mix up callback/promise.

## 0917

- [Fatal error in, line 0 -- Fatal JavaScript invalid size error 171211145 - Stack Overflow](https://stackoverflow.com/questions/76587029/fatal-error-in-line-0-fatal-javascript-invalid-size-error-171211145)
  - There could be several reasons why the error occurs.
  - Node version. Ask friends what version they are on, and try to use the same
  - Broken node_modules. Delete the node_modules directory and run npm install (or yarn install or pnpm install)
  - Broken git. Delete the local project directory and clone it again. Remember to save all your changes (i.e. git branch -b stage && git add . && git commit -m "stage changes" && git push -u origin stage)
  - One cure for all diseases - restart your computer

## 0915

- [Overriding shortcut keys in Firefox and Chrome - Stack Overflow](https://stackoverflow.com/questions/15911785/overriding-shortcut-keys-in-firefox-and-chrome)
  - `if (event.ctrlKey && event.key === 'k') event.preventDefault()`

## 0913

- Got an error from agent event, Failed to find the prompt when use ctrl +c command

昨日：
- 修复develop/staging新环境相关的问题
- 处理cmd+k的diff视图的undo/redo，包括初次生成和用户accept后 (60%)
- 整理了一下cmd+k相关的extension

今日：
- 处理cmd+k与agent通信与状态，测试cmd+k主流程
- 继续处理undo/redo

## 0912

昨日：
- 修复developer环境下ideServer连接相关问题
- cmd+k的undo (40%)

今日：
- 修复新环境下现有功能的问题
- cmd+k的undo/redo

## 0911

昨日：
- 继续实现cmd+k，处理agent的返回，并渲染diff视图
- 排查clacky在新环境下部分功能不work的问题

今日：
- 继续处理clacky在新环境下部分功能不work的问题
- 实现cmd+k的undo

## 0910

- 刚我排查了点击时光机已执行成功的action打开编辑器一直显示骨架屏未显示diff视图的问题
  - 原因是staging.app.clackyai.com环境下queryCustomizeFrameData没有返回快照数据，staging.app.clacky.ai环境下能正常返回快照数据因而不存在这个问题
  - 明天需要检查下ideServer的部署，我之后会在前端补充打开文件时的异常处理

昨天：
- 解决cmd+k指令输入框无法获取focus的问题
- 处理agent的返回，并渲染diff视图 (40%)

今天：
- 实现并测试cmd+k主流程的逻辑，并提交pr
- 开始实现部分accept

## 0909

上周：
- 修复时光机的播放控制，暂停和恢复
- 修复时光机进度条和驾驶舱action状态的一致性
- 基本实现了cmd+k快捷键的唤起隐藏

本周：
- 交付cmd+k的主要功能和打字效果，尽量对齐cursor的cmd+k的体验
- action的rerun
- 实现diff工具条

今日：
- 交付cmd+k的主要功能，并提pr

## 0907

- 昨日：
  1、讨论了cmd+k和diff工具条的需求细节，确认了clacky cmd+k与cursor的差异
  2、探索嵌入到代码中间的卡片元素的实现方式
- 今日：
  1、实现cmd+k输入框的唤起与隐藏
  2、输入指令后，先显示静态版diff-view

## 0906

- taskState的append状态
  - 追加步骤时，agent后端自动设置append状态
  - 进入回放模式，从哪个action开始播放
    - 默认最后一个追加的

- dev-log
  - 改进cde的功能与体验，修复时光机状态变化时底部action和驾驶舱action状态不一致的问题
  - 讨论了agent工作时打字动画优化的方案，以后会转向动态更新编辑器的配置而不是强制刷新文件
  - 尝试cmd+k的弹窗实现，探索 paas和agent通信的架构
- dev-to
  - 需要和agent、产品、设计确认cmd+k及diff工具条的功能细节和交互细节
  - 如何让paas和agent通信

```JS
// uRemakeFile request parameters, 'uRemakeFile'
{
  prompt,
  filePath,
  // { lines, offset }, lines是1-based行号如[4,5]/[4,4], offset是光标位置
  selectedRange,
  // meta可包含用于生成代码的其他信息如代码注释/当前行变量或方法的声明或引用
  meta = {},
  selectedContent = '',
  isFollowUp,
  // isRegenerate
}
// uRemakeFile response
{
  filePath: '',
  remakeContent: '',
  // alternatives: []
}

// uStopRemakingFile request
{
  filePath: '',
}
// uStopRemakingFile response
{
  stopped: true
}
```

## 0905

- agent工作时的diff动画问题
  - 有时写字的文件会错乱，action依次是a3/a4, 先写a4，再写a3，不能稳定复现
  - 会意外打开.gitignore文件

## 0904

- Error: onCancelTask error, "Can't trigger event cancel_task from state PAUSE_STATE!"

## 0903

- [Composition – Radix Primitives](https://www.radix-ui.com/primitives/docs/guides/composition)

```JSX
// dialog和tooltip的trigger顺序
<Dialog.Root>
  <Tooltip.Root>
    <Tooltip.Trigger asChild>
      <Dialog.Trigger asChild>
        <MyButton>Open dialog</MyButton>
      </Dialog.Trigger>
    </Tooltip.Trigger>
    <Tooltip.Portal>…</Tooltip.Portal>
  </Tooltip.Root>

  <Dialog.Portal>...</Dialog.Portal>
</Dialog.Root>
```

```JS
// resourceMonitoring
{
  "memoryCurrent": 370,
  "memoryMax": 1024,
  "cpuPercent": 0.22
}
```

- [What is the difference between parseInt() and Number()? - Stack Overflow](https://stackoverflow.com/questions/4090518/what-is-the-difference-between-parseint-and-number)
  - they are semantically different, the Number constructor called as a function performs type conversion and parseInt performs parsing

## 0902

- dev-log
  - 交付了时光机的主要功能和ui设计稿还原
  - 设计了cmd+k的主要状态和实现流程
- dev-to
  - 本周前2天，修复agent和clacky前端的状态，agent工作时没有预留打字动画的时间，agent暂停后action状态的改变
  - 本周后3天，实现cmd+k的主要功能，唤起和accept/reject
  - .gitignore 文件在文件树无法显示

- 👥 aws创业论坛分享
  - ai产品: coding大概3个，视频几个
  - ai ppt及操作word/excel的效果很好
  - 业内融资，cursor的A轮60m，codeium的C轮0.12b
  - 大厂不容易垄断，大厂会与私有agent绑定，代码privacy问题
# dev-08-diff-view-with-animation-&-codemirror-typewriter-&-stepped-progressbar

## 0830

- dev-log
  - 实现diff-view显示快照文件时编辑器显示不可编辑的提示条
- dev-to
  - 使用hack修复时光机的暂停继续问题

- 时光机暂停event时不需要参数
  - 时光机恢复时，旧的数据不会更新

- dev-to-demo
  - ~~editor: typewriter~~
  - ~~时光机回放模式~~
  - paas的断线恢复问题
  - paas激活的时机要修改
  - ~~LSP补全~~
  - ~~cde的 push/commit/pr~~
  - ~~cde的 分享、邀请、进入权限~~
  - ~~cde设置页面~~
  - ~~cde环境变量、中间件~~
  - ~~userStatusUpdated~~
  - ~~paas异常处理~~
  - ~~删除废弃的代码~~
  - ~~带着issue进入cde~~
  - ~~异常toast弹窗, 异常处理~~

- 跟随模式
  - ~~followUser时会自动打开console面板~~
  - ~~ai工作时自动打开面板状态~~
  - ~~同一个用户在不同浏览器打开同一个playground的cde时，用户头像显示几个~~
  - ~~刷新完页面恢复面板显示隐藏状态~~
  - ~~ai头像的位置顺序~~, 按进入room的顺序
  - ~~文件树 keydown事件传到了编辑器~~
  - ~~浏览器panel滚动禁用~~
  - ~~修复文件树无法创建文件和文件夹的问题~~
  - ~~测试跟随ai~~
  - ~~发送readfile指令或切换文件，渲染editor失败~~
  - ~~`/playground`路由页面不需要知道issue信息~~

- 时光机
  - ~~打字机效果~~
  - ~~上下布局diff视图~~
  - ~~播放控制逻辑，op的内容和时机~~
  - ~~回放模式支持编辑，内容和光标选区的变化~~
  - ~~处理打开已删除文件、新增文件~~

## 0829

- dev-log
  - 实现了时光机的terminate，review并且合并了时光机主要功能的pr，时光机可以开始测试
- dev-to
  - 解决paas的openFile处理异常 File does not exist
  - 实现diff-view显示快照文件时编辑器显示不可编辑的提示条
  - 开始设计cmd+k功能的状态和逻辑

## 0828

- dev-log
  - action bar点击时显示三角形指针
- dev-to
  - 测试时光机的new/delete-file， terminate

## 0827

- dev-log
  - 驾驶舱置顶卡片还原设计稿
- dev-to
  - 测试时光机的live/playback模式的播放控制和动画播放逻辑

## 0826

- 计划终止后
  - 未执行的action是否会丢失，因为默认进入playback模式且无法回到live模式
  - 如何彻底删除actions

- ✨ 用户介入action的实现思路
  - 确认需求: 只要最后一个action有介入，同一文件都会介入
  - 思路1: agent修改内容后也插入自定义帧fAfterAgent，查询快照action的fAfterAgent与最新内容做比较
  - 思路2: 查询path对应的op，计算op执行compose后是否变化

- 置顶卡片
  - 执行完成后立即进入playback模式，是否显示还置顶卡片，该显示什么action

- dev-log
  - 修复了diff视图的只读编辑器的功能，时光机进度条还原设计稿
- dev-to
  - 驾驶舱置顶卡片还原设计稿， 测试时光机的live/playback模式的播放控制和动画播放逻辑

- 🔡 code-review-layout
  - 设计系统更新后，cde的颜色如header/gutter更新了嘛
  - bg-background 的亮暗色有吗，比如圆点
  - primary-sidebar-container 的实现变成什么样了
  - mainEditor expandable需要改名maximizable
  - 切换terminal和console时，不能rerender

## 0825

- action进度条的动画
  - live模式working可以循环loading
  - playback模式动画只放一遍，类似播放视频

## 0822

- diff-animation-to-do
  - 不用写右侧空白部分

- diff-animation-issues
  - agent删除文字是什么效果
  - 按行写代码时，一行代码的时间间隔

- [How to catch dynamic import error in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/75295514/how-to-catch-dynamic-import-error-in-javascript)
  - `await import('path-to-module').catch(reason => { })`

## 0821

- 在setInterval中更新操作行号，那么自动滚动到dom需要~~在下次渲染前触发，不能在setInterval触发~~

```shell
# fileTreeIgnore
.git/;.1024.nix;.1024feature*;.nfs*;*.dll;*.swp;.paas-unit-*;core.*;.breakpoints;.idea/;.vscode/;node_modules/
```

- [Can a number returned by setTimeout() in javascript be negative? - Stack Overflow](https://stackoverflow.com/questions/52179772/can-a-number-returned-by-settimeout-in-javascript-be-negative)
  - The returned `timeoutID` is a positive integer value which identifies the timer created by the call to setTimeout(). This value can be passed to clearTimeout() to cancel the timeout.
  - The returned `intervalID` is a numeric, non-zero value which identifies the timer created by the call to setInterval(); this value can be passed to clearInterval() to cancel the interval.

- [Is calling setTimeout with a negative delay ok? - Stack Overflow](https://stackoverflow.com/questions/8430966/is-calling-settimeout-with-a-negative-delay-ok)
  - the specification requires that there is a minimum timeout.
  - If you provide something less than this (HTML5 spec says 4ms) then the browser will just ignore your delay and use the minimum.
  - So negatives should be fine, since it'll just be less than the minimum.

## 0820

- dev-log
  - 本次cycle的需求评审
  - 隐藏diffView中的绿色部分，探索动画的实现方式
- dev-to
  - 初步实现diff视图的打字机效果

## 0819

- dev-log
  - 时光机基本的播放控制
- dev-to
  - 进一步测试 播放控制、追加步骤
  - 动态diff
  - cmd+k
  - 时光机还原设计稿
  - undo/redo

- 🔡 requirements-review-v20240819
- 代码工具条的出现场景
  - 光标在diffView里面就出现
  - 光标在非diffView代码块需要选中代码才出现，只有edit和chat
- action的修改操作
  - 只支持删除不支持添加，不支持细粒度修改
  - 每修改一个action都发送消息给agent，不是修改完后一起发送
- 代码索引的功能和交互
  - thread全局的索引进度
- cmd+k
  - 重做代码块，参数是action的id
  - 只在第一个变更代码块出现
  - 选中代码后出现edit+chat悬浮工具条，选中后cmd+k直接出现聊天窗口
- self-debug/auto-detect
  - agent自动检测terminal的异常信息
  - 代码异常，先由agent捕获并处理异常，再由前端显示suggest卡片
- 追加步骤
  - 从追加的第一个action开始执行
  - 时光机回放从追加的步骤开始播放
  - 第4次plan由agent返回拒绝执行
- 制定计划过程中，用户触发auto-detect-debug，不会触发新计划

## 0815

- 优化了打开文件的逻辑

## 0814

- 插入自定义帧并搜索

```JS
// 自定义帧的内容
{
  path: 'src/index.ts',
  content: 'export const vv = 11',
  actionType: 'delete_file',
  // 存储时数据来源于打开文件时file事件的响应内容， 用来获取追加步骤场景下的文件快照，
  fileTime: 1723635429480
}
```

```JS
// task_steps
[{
    "id": "1",
    "title": "Set the run_command in the .1024 configuration file",
    "task_actions": [{
      "id": "1-1",
      "title": "Set run_command with HOST and PORT",
      "action": "modify_file",
      "path": ".1024",
      "target": "",
      "status": "inited",
      "detailed_requirement": "The run_command in the .1024 file should be set to HOST=0.0.0.0 PORT=8080 npm run dev. This ensures that the web service runs on the correct host and port.",
      "result": ""
    }]
  },
  {
    "id": "2",
    "title": "Install necessary dependencies",
    "task_actions": [{
      "id": "2-1",
      "title": "Run npm install to install project dependencies",
      "action": "run_command",
      "path": "",
      "target": "npm install",
      "status": "inited",
      "detailed_requirement": "",
      "result": ""
    }]
  }
]
```

## 0813

- cde设计稿背景色
  - header是   #18181B
  - panel是    #27272A   bg-background-subtle
  - machine是  background: linear-gradient(270deg, #18181B 0%, #27272A 50%, #18181B 100%); 
- tailwind
  - bg-background #09090b
- machine
  - border-radius: 12px 12px 0 0

## 0812

- [How to have multiple CSS transitions on an element? - Stack Overflow](https://stackoverflow.com/questions/7048313/how-to-have-multiple-css-transitions-on-an-element)
  - Transition properties are comma delimited 
  - transition: color .2s, text-shadow .2s; 

- [CSS animation to make div appear smoothly from bottom - Stack Overflow](https://stackoverflow.com/questions/74165073/css-animation-to-make-div-appear-smoothly-from-bottom)

- [How can I transition height: 0; to height: auto; using CSS? - Stack Overflow](https://stackoverflow.com/questions/3508605/how-can-i-transition-height-0-to-height-auto-using-css)

- [Make HTML element disappear with CSS animation - Stack Overflow](https://stackoverflow.com/questions/39513705/make-html-element-disappear-with-css-animation)

- [CSS border bottom animation - YouTube](https://www.youtube.com/watch?v=lvS8KDTo67k)
  - 从单词正中间向两个划线

- [Animation using Keyframes in tailwind css | Medium](https://medium.com/@sandhyasrinivasan.1502/animation-using-keyframes-in-tailwind-css-9003a7a62c33)
  - theme: { extend: { keyframes: { rubberband: {
  - animation: { "rubber-band": "rubberband 1s linear 1 ", 
  - className='animate-rubber-band'

## 0811

- 💬🎨 [`<u>`: The Unarticulated Annotation (Underline) element - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/u)
  - To underline text, you should instead apply a style that includes the CSS `text-decoration` property set to `underline`
  - the original HTML Underline (`<u>`) element was deprecated in HTML 4; however,  `<u>` was restored in HTML 5 with a new, semantic, meaning: to mark text as having some form of non-textual annotation applied.
  - Valid use cases for the `<u>` element include annotating spelling errors, applying a proper name mark to denote proper names in Chinese text, and other forms of annotation.
  - You should not use `<u>` to underline text for presentation purposes, or to denote titles of books.

- [Zed is not opening _202403](https://github.com/zed-industries/zed/issues/9623)
  - try to give permission to your user to the folder ~/.cache/zed
  - `sudo chmod 700 ~/.cache/zed`

## 0809

- dev-log
  - 从message-store的状态渲染时光机进度条
- dev-to
  - 时光机执行打开文件

- 测试集成-dev-to
  - 前端未控制member/owner的按钮、路由访问权限
  - agent生成thread名称限制长度
  - think流程支持stop，设计稿有设计
  - 在驾驶舱的plan文件列表打开文件，think/plan, 聊天时的
  - think卡片打开文件，滚动到文件的行数
  - 聊天搜索 未实现
  - 驾驶舱还原设计稿
  - agent计划只给到文件名，暂时没做到方法粒度
  - 追加步骤的上限控制
  - 驾驶舱里面的think流程与外面有不同，补充表单
  - 插入代码块到文件中，未实现
  - 引用历史聊天的内容，未实现
  - 引用terminal的异常信息
  - 聊天上传图片未上传，暂时先关闭
  - 聊天点赞，先隐藏
  - 重新生成内容， 前端再调一次
  - 计划agent和聊天agent不是一个
  - ❓ 执行计划时，其他人能看到进度吗
  - 终止二次确认前ai还会继续执行
  - ai执行计划后，用户将文件删了，action显示异常
  - 取消置顶的按钮，待确认，人工可以取消置顶吗
    - 暂停时切换action，置顶也要变
  - 回放时，也会置顶卡片
  - 任务执行时，多人的暂停与恢复
  - 人工删除ai需要的文件，ai会执行异常，整个计划失败
  - ai修改后的文件，人工再修改，然后撤销人工修改，进度条从绿色变成黄色吗？
  - 执行过程中澄清补充需求，暂时不做
  - 回放模式可以删除文件吗？  待确认。 确认修改文件
  - 回放模式取消diff时，直接展示最新代码

### 时光机执行与回放的细节确认

- diff视图显示的场景
  - ✅ 计划首次执行或回放时，首次执行action时显示动画
  - ✖️ 计划执行或回放时，切换已执行完action的文件不显示动画
  - ✖️ 当前文件执行完后，上下滚动不显示动画
  - ❓ 暂停状态下

## 0808

- 自由对话code-review
  - ~~create pr的task和其他task如创建thread的流程有结构设计和ui设计吗~~
  - 分析需求时需求规模的获取有方案了吗

## 0807

- ai-coding的动画编码效果

## 0806

- [GnuTLS recv error (-110): The TLS connection was non-properly terminated ](https://github.com/argoproj/argo-cd/issues/3994)
  - apt-get install gnutls-bin
  - git config --global http.sslVerify false

## 0805

- dev-log
  - 调研及研发diffView
- dev-to
  - 交付diffView, cmd+k的代码生成部分, 对接agent的播放控制

- 需求评审
- 时光机进度条点击到中间位置，会自动吸附到进度条小节的开始位置
  - 第一期只做点击，不做拖拽
- 终止计划后，ai的变更文件列表暂时不做，暂时使用文件变更列表

- agent侧使用goal/detail, 业务侧使用issue/desc

## 0802

- demoDay240802
  - 自动跟随ai工作

## 0801

- [How to set background color on terminal · xtermjs/xterm.js](https://github.com/xtermjs/xterm.js/issues/1719)
  - term.setOption('theme', { background: '#fdf6e3' }); 
- [Release 5.0.0 · xtermjs/xterm.js](https://github.com/xtermjs/xterm.js/releases/tag/5.0.0)
  - The deprecated getOption and setOption APIs have been removed in favor of options assignment
  - term.options.scrollback = 1000; 
  - term.options.theme = { background: '#ccc' } 注意这里更新是replace而不是merge

- dev-log
  - 讨论了diffView接入使用场景的状态数据流，以及产品细节
  - 修改paas的编辑器，增加了diffView相关api
- dev-to
  - 实现与agent无关的上下布局的diff编辑器
# dev-07-dockview-ephemeral-panel-&-init-thread-playground-&-paas-custom-frame

## 0731

- paas的事件监听，缺少 resourceMonitoring

## 0730

- dev-log
  - 确认回放的实现细节
  - 尝试添加自定义帧的事件到ideServer

## 0729

- idepaas提供了打字机效果的参考实现
  - 1024code的ai编辑几乎都使用paas的能力

- dev-log
  - nbdime diff
  - idepaas的打字机效果实现, 支持一次性将ai的修改全撤销
  - 合并了迁移paas的pr，提供了本地调试的文档放在clacky仓库，迁移测试不充分，有问题反馈
- dev-to
  - 交付上下布局的diff视图，暂时可能是只读版，编辑相关的问题看能处理到什么程度
  - 探索一个可支撑业务的前端持久化数据结构

## 0728

- ai分析任务描述用plan，ai分析任务的结果用task

## 0726

- diff数据流
  - agent > ideServer > paas-sdk > fe
  - diff接口: 输入新的全文，渲染上下格式的diff视图

## 0725

- [npm run build is failing due to typescript or lodash uncompatibility - Stack Overflow](https://stackoverflow.com/questions/78682996/npm-run-build-is-failing-due-to-typescript-or-lodash-uncompatibility)

- 是否要发布新的单独的npm包，还是沿用旧的包名增加版本号
- 什么操作逻辑会持久化到mongodb

- dev-log
  - 修复了跟随模式下切换文件渲染编辑器异常的问题
- dev-to
  - 迁移paas-sdk到单独的仓库
  - 梳理时光机和diff视图的实现细节，明天和产品确认业务细节

## 0724

- dev-log
  - 尝试修复跟随模式下切换文件渲染编辑器异常的问题
- dev-to
  - 继续修复这个问题
  - ai邀请跟随

## 0723

- [How to remove all duplicates from an array of objects? - Stack Overflow](https://stackoverflow.com/questions/2218999/how-to-remove-all-duplicates-from-an-array-of-objects)
  - One liners with filter() (Preserves order)
  - myArr.filter((obj1, i, arr) => arr.findIndex(obj2 => (obj2.id === obj1.id)) === i )

- [What would be the Unicode character for big bullet in the middle of the character? - Stack Overflow](https://stackoverflow.com/questions/12971187/what-would-be-the-unicode-character-for-big-bullet-in-the-middle-of-the-characte)
  - You can use a span/div with 50% border radius. I like this solution, slower but you can control position and size or color more directly.
  - 考虑a11y

- dev-log
  - 研发任务分解
  - 跟随模式的样式优化
- dev-to
  - ai执行shell时，自动打开面板
  - ai邀请

## 0722

- 需求分解
  - 游客也是member，游客是member的一种身份
  - 游客也走clerk用户系统

- agent是每个用户一个，还是每个playground一个
  - 目前是一个playground一个agent

- dev-log
  - 修复了跟随模式用户异常的问题
  - 与后端和agent联调发送issue
- dev-to
  - 先修复演示反馈的明显问题
  - LSP补全
  - 时光机

### demo-feedback0714

- 操作流程：
  0001. 访问官网
  0002. 展示 [进入控制台] 按钮 -> 点击后有登录进入dashboard ，没登录进入登录页
  0003. 登录后  -> 进入Workspace - project列表页面 （不应进入个人中心）
  0004. 仓库连接 -> 创建项目 -> 初始化环境（项目支持Next）
  0005. 进入 CDE （运行、Terminal、Console、浏览器、文件树 OK）
  0006. 驾驶舱：自由对话 OK
  0007. 提出需求 -> 需求分析 -> 制定计划 -> AI 执行计划写入代码
  0008. 创建Thread - 连接Issue - 设置Thread名称和分支（默认代入初始值）

- 问题 及 未完成功能：
  0001. 连接仓库 - 报500问题
  0002. 项目列表 - 假数据（项目类型、协同者、Thread数量）
  0003. 初始化环境：仅支持Next项目
  0004. CDE假数据（协同者、邀请、Thread状态、CPU、内存）
  0005. CDE 窗口布局问题
  0006. 驾驶舱 - 内部滚动
  0007. plan 内容和格式
  0008. Thread已执行计划后， 无法继续执行下一计划（追加步骤应能继续启动任务）
  0009. Thread中返回Dashboard 报500
  0010. agent IDE server 连接问题
  0011. GIthub 仓库授权 限制数量 ???
  0012. 多人协同
  0013. 视角跟随
  0014. 执行计划中 - AI 流式输出
  0015. 推分支
  0016. 需求识别：确认issue是否可行
  0017. diff
  0018. command + K

### 公测就绪条件（草稿）

- 产品故事就绪范围
  - [ ] 连接并获取 issue 详情
  - [ ] 基于issue生成计划与canvas预览
  - [ ] NextJS项目初始化过程清晰、可用
  - [ ] CDE 环境文件树、编辑器、shell 及浏览器，运行正常
  - [ ] 时光机过程100%顺畅，主动跟随 AI 工作
  - [ ] 中断工作时，Cmd+K
  - [ ] 结束工作后，直接修改代码、Cmd+K
  - [ ] 生成 commit 或 PR

- 其他不强求
  - 布局灵活性（窗口拖拽、开关等）
  - 计划 canvas 调整
  - 多用户协作协同（邀请用户协作、分享链接等）
  - 自由会话质量和能力（快捷指令、RAG配置等）

- 质量要求
  - NextJS 限制、清晰的需求描述（人类直接可理解，没有歧义）的前提下：
    - S需求一次性成功率达到 70%，不成功的修改步骤不超过 30%
    - M需求一次性成功率达到 30%，不成功的修改步骤不超过 50%
  - 内测匿名反馈（含内外部、最后20个投票）
    - 获得平均 7 分以上评价
    - 50% 的用户能有效提出 aha moment
  - 主流程无P0、P1级别问题

- 前端开发任务
  - cde基础功能， browser/terminal
  - 时光机计划
  - 环境配置
  - 提交pr
  - cmd+k, 自动补全
  - 快捷键
  - cde loading
  - 基础交互、首次加载

## 0719

- 第二个thread创建后, 是否要调用 api通知clacky后端
  - 是的

- dev-log
  - 与后端联调获取threadIssue的api，简单实现了发送issue给agent，缺少测试ui
  - 修复cde-tools拖拽的问题、移除空白区域
- dev-to
  - 配合演示修复问题
  - 测试跟随ai

- dev-done-cde布局开发
  - 紧急: 拖动改变浏览器宽度时，布局会混乱
    - ~~console/terminal的内容高度有时异常，有时布局混乱的原因是shell的宽度高度过大~~
  - ~~难点: 隐藏侧边栏的头部~~
  - ~~难点: disable tab页拖动，有时不work有时work~~
  - ~~驾驶舱添加滚动css， SecondarySidebarContainer overflow-auto~~
  - ~~run前端项目才需要打开浏览器，其他项目不需要，前端项目执行时上方是editor+browser下方是console~~
  - ~~cde-tools需要点2次才生效~~
  - ~~editor默认提示文本 删除~~
  - ~~cde tools 最小高度~~
  - later: 布局持久化和刷新页面恢复

## 0718

- dev-log
  - disable cde布局的大部分拖拽问题
  - 切换console/shell
- dev-to
  - 开始时光机的回放模式
  - terminal组件 重复渲染和无法使用
  - cde-tools状态联动
  - ~~CDE Tools 不用支持拖~~
  - ~~CDE Tools 下方空白~~
  - 编辑器有时候出不来
  - 获取thread对应的issue，提供给agent

## 0717

- [[🐛 Bug]: Using Clerk on Cloudflare Pages: Unhandled ‘default’ Property TypeError Leading to HTTP 500 · cloudflare/next-on-pages _202406](https://github.com/cloudflare/next-on-pages/issues/800)
  - If I understand correctly, issue is happening when navigating between routes which have client components being rendered, with Clerk installed and hosted on Pages.

- dev-log
  - code review 跟随模式代码，已合并pr
  - 讨论邀请跟随的实现，跟随链接不是cde页面的url，跟随者不是使用guest身份而是使用member身份
  - 删除废弃代码
- dev-to
  - 优化布局，下午提pr
  - 开始时光机的回放模式，先复习一下codemirror的文档，尝试
  - 创建git分支，放在第一个loading

## 0716

- dev-log
  - cde页面基本的异常处理
  - 跟随其他用户测试通过
- dev-to
  - 测试跟随ai的功能

## 0715

- [node.js - try/catch blocks with async/await - Stack Overflow](https://stackoverflow.com/questions/40884153/try-catch-blocks-with-async-await)
  - Due to the fact that every async function is technically a promise
  - You can add catches to functions when calling them with await
  - No need for try catch, as all promises errors are handled, and you have no code errors, you can omit that in the parent

- dev-log
  - code review cde页面内的组件和逻辑的pr
  - 添加跟随模式相关状态

## 0714

- dev-log
  - 重构cde初始化流程到paas-api, 重构cde页面的状态管理技术栈并迁移现有组件
  - 目前cde基本可以运行项目代码，我的测试以前端项目为主
  - cde面板优化交互
  - cde初始化的准备repo和激活paas 2个loading状态

- dev-done
  - ~~将tenantCode代码放在state, 放在环境变量~~
  - ~~playgroundId可能取旧值~~, 通过reset+当前组件的useState解决
  - ~~repo隔一段时间会自动失活~~
  - ~~cde初始化迁移到paas-api~~
  - ~~dynamic add panel for plans/steps~~

- 有时thread无法打开文件, 临时方案是~~ready后才渲染~~
  - 可能是上个页面的组件及状态未清空导致
  - ~~原因是cm-editor-dom的container渲染多次, 且dom值不一样，setContainer~~
  - ~~解决方法是，限制cm-editor-dom的更新~~

## 0712

- dev-to
  - 迁移组件和状态
  - 增加loading页面

## 0711

- 👥👥 sharing-how-to-use-ai-agent-in-work
  - Dify自动流程
  - rpa
  - 使用场景: 测试用例， 技术文档， 产品介绍

- dev-log
  - cde面板去掉一些暂时没用的button，存储了各个面板的宽度
  - 实现了简单的添加新tab页面的api
- dev-to
  - 将paas相关状态再整理下，今天先提交一版pr

- 支持添加新tab页，如settings/hotkeys/search/plugin-details/preview-web/problems-or-warnings
  - 添加的通常是临时页面，不需要alwaysVisible
  - 思路1，先让使用方注册comp1，再根据DefaultPanel组件中的type渲染comp1
    - 优点是不需要改动comp1，方便接入
    - 缺点是使用分2步，且注册的位置不好选，一般放在顶层组件的props
  - 思路2，直接将comp1放在state中，~~comp1无法rerender更新，除非做成纯展示组件~~
    - 优点是使用只有1步，`setState({comp1: ()=><Comp1 />, props} )` 立即work
    - 缺点是comp放入state不是最佳实践，comp1的内部的全局state要单独处理(在多实例的场景，思路1也存在此问题)

## 0710

- [reactjs - Is it a good idea to store components in state? - Stack Overflow](https://stackoverflow.com/questions/66919014/is-it-a-good-idea-to-store-components-in-state)
  - I would not recommend it. But not for the reason that those instances would somehow add too much size to the state (which I don't think they would).
  - The strongest argument in my opinion is: the instantiated components are stale; their properties will only have those values that were assigned when they were instantiated.

- dev-log
  - code review并调整了重构cde初始化的pr
  - 将cde tools面板布局组件的实现调整了下，又提取了一些state
- dev-to
  - cde-tools面板宽度持久化到localStorage
  - 重构paas初始化的逻辑，提取paas相关状态并注册事件

## 0705

- [Error: The externalDependency 'webpack-cli' for 'server:build' could not be found · Issue · nrwl/nx](https://github.com/nrwl/nx/issues/22871)
  - Issue has nothing to do with pnpm. it also reproduced with npm, when using nx 19.0.1. After downgrade to 18.3.4, issue goes away.
  - Nx doesn't support pnpm 9 yet

- dev-done
  - ~~ide滚动条失败~~
  - ~~trpc请求过多的问题~~
  - ~~删除未使用的 workbench2 组件失败，会导致样式混乱~~
  - ~~threadName variable~~
  - ~~clacky read_file TODO.md~~

## 0704

- [Migrate to @xterm org on npm · xtermjs/xterm.js _](https://github.com/xtermjs/xterm.js/issues/4859)
  - Publish 5.4 to new scope

- 根据thread状态优化cde启动速度
  - ~~每次打开cde都会重新import，要实现skip~~
  - 若是empty，则需要import仓库
  - 若是initialized，则直接创建playgroundId
  - 若是inProgress, 则直接创建ticket

- dev-log
  - 重构了workbench布局相关的状态
  - 更新了cde的初始化逻辑到最新api，但最后一步请求ide-server url失败
  - cde-tools分屏面板添加
- dev-to
  - 分别优化第一个thread/普通thread的cde初始化逻辑
  - cde-tools面板按钮隐藏及调整

- 如何获取clerk的cookie，传到header的Authorization

- [What is the shortest function for reading a cookie by name in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/5639346/what-is-the-shortest-function-for-reading-a-cookie-by-name-in-javascript)
  - await cookieStore.get('cookieName'); 
  - It's 2022, everything except Internet Explorer supports the URLSearchParams API (^1) and String.prototype.replaceAll API (^2), so we can horribly (ab)use them

```JS
const cookies = new URLSearchParams(document.cookie.replaceAll('&', '%26').replaceAll('; ', '&'));
cookies.get('cookie name'); // returns undefined if not set, string otherwise

const getCookieValue = (name) => (
  document.cookie.match('(^|;)\\s*' + name + '\\s*=\\s*([^;]+)')?.pop() || ''
)
```

## 0703

- dev-log
  - 熟悉codemirror的文档和源码， 探索切换diff视图的插件化实现方式
- dev-to
  - 静态版diff视图编辑器

## 0702

- dev-log
  - 尝试复用paas编辑器的插件和逻辑，实现一个最小的diff编辑器组件，思路可行，但不符合产品需求
- dev-to
  - 将最小diff编辑器完善下，尝试将diff逻辑抽象为codemirror插件

## 0701

- dev-log
  - 上周重构cde状态管理与对接agent
  - 熟悉了codemirror官方diff示例的原理，尝试从视图层提取出编辑op
- dev-to
  - 最小可用版的时光机播放和回放
  - 完善agent相关的制定计划/执行计划的实现细节
# dev-06-dockview-floating-&-progressbar-animation-&-trpc-thread-id-&-zustand-socketio

## 0630

- dev-log
  - 重构cde-state，对接agent通信
- dev-to
  - 先mock时光机的编辑op，再对接agent的编辑

## 0628

- [React Custom Hooks fetch data globally and share across components? - Stack Overflow](https://stackoverflow.com/questions/57602715/react-custom-hooks-fetch-data-globally-and-share-across-components)
  - Whenever you use a custom hook, there will be separate instances of the hook within your App and they won't share the data unless you are using context API within them

- dev-log
  - cde state的 get/set/socket通信 的架构及代码实现
  - 优化了事件注册的设计
- dev-to
  - 新增api: 获取回放所需的operations，获取变更文件列表，fileChangeLogs的变更列表无法区别修改删除

## 0627

- 👥👥 sharing-how-to-get-rich-slowly 💰
- 美股的优势
  - 持续几十年的增长
  - 最好的公司
  - 监管体系
  - 每年的淘汰率
  - 非美国不需要资本税，国内印花税
- 二级市场
  - 上市 nasdaq， s&p
- 股票走势案例
  - Nvidia在23年gpt发布后持续走高
- 临近期货交割时，利润会很大
  - 币安新币种有机会， old money进场后机会就变少
- 期权非线性市场
- 期权公式 c+k = p+f
  - 公式不成立时，就是赚钱的机会
  - 期权内幕交易在股价变动结束后才会体现，更隐蔽
- 赌财报
  - 传统行业的波动更少
- 交易习惯：观察周四周五的收盘价，周一买入
- 基金是把资产交给别人打理
  - 美国国债基金比较稳健，但需要探索发现
- 不必盯着暂时的热股，多年的涨势和趋势更有参考性
- trading和invest不同
  - 开奶茶店的收益也是有的

## 0626

- state与socket的初始化逻辑
  - state的set方法需要socket，不可以delay
  - ✅ socket的初始化需要state的set方法，但可以delay
  - > 结论: 先初始化socket，再初始化state，然后注册state更新事件到socket.on

- dev-log
  - cde的状态重构
- dev-to
  - 将部分现有状态提升到全局
  - 时光机回放模式的状态在全局的存储

## 0625

- [Add a prefix to each type in a string union type - Stack Overflow](https://stackoverflow.com/questions/73135992/add-a-prefix-to-each-type-in-a-string-union-type)

```JS
type Prefix < P extends string, S extends string > = `${P}${S}`;

type Prefix < K > = K extends string ? `on${K}` : K;
```

- [const enum in Typescript - Stack Overflow](https://stackoverflow.com/questions/40227401/const-enum-in-typescript)
  - const in an enum means the enum is fully erased during compilation. Const enum members are inlined at use sites. You can't index it by an arbitrary value.

## 0624

- cde状态设计

- 时光机的用户编辑, 每个action对应的文件是否一定不同，是否存在多个action对应同一个文件
  - 追加步骤的action可能会与前面的action对应同一文件，对于此场景，前面action对应的文件默认不可编辑，点击时跳到最新文件进行编辑

- 测试cde
  - http://localhost:3000/thread?tid=019039f0-20f4-74c0-b3cd-3060ea57f4d3

```JS
// 获取变更文件列表数据的api
// stt.dao.get.playgroundInfo().fileChangeLogs
// stt.dao.store.getState().playgroundInfo.fileChangeLogs
// 🐛 不包含修改的内容/行号，被删除的文件不包含在返回的数组
['README.md', 'package.json', 'src/app.tsx']
```

- 前端cde的研发功能拆分
  - cde的初始化流程优化
  - 制定计划、执行计划: 时光会产生新action吗机回放
  - ai对话
  - pr提交

## 0621

- [Why is there no same-origin policy for WebSockets? Why can I connect to ws://localhost? - Stack Overflow](https://stackoverflow.com/questions/23674199/why-is-there-no-same-origin-policy-for-websockets-why-can-i-connect-to-ws-loc)
  - WebSockets can cross domain communication, and they are not limited by the SOP (Same Origin Policy).

- [Is it possible to chain pseudo classes using Tailwind CSS? - Stack Overflow](https://stackoverflow.com/questions/70855897/is-it-possible-to-chain-pseudo-classes-using-tailwind-css)
  - `focus:hover:bg-black`

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

- 👥👥 sharing-ai金融需求
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
- diffView
  - 模型
  - 视图
  - 选区光标

- dev-log
  - cde新布局的发布
- dev-to
  - 继续完善cde的布局和交互逻辑
  - 根据linear的任务拆分，推进clacky的发布，主要包括 制定计划、diffView的逻辑、驾驶舱ai对话的ui(不包括逻辑)

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
