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

```shell
flatpak run com.discordapp.Discord --proxy-server="socks5://127.0.0.1:1080"

# delete all node_modules folders recursively
rm package-lock.json && find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +

# npm i
DEBUG=* npm i --no-audit --loglevel silly
DEBUG=* npm install --legacy-peer-deps --no-audit --loglevel silly

$$('[contenteditable]')
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

- deep into lib/fwk 书籍原理与代码实践要分开
  - 学习巩固: 实践练习 > 源码/示例 > 文档/论坛 > 社交媒体
  - src-code, issues, pr, forks, extensions/alternatives
  - storage, sync/partial, conflicts, concistency
  - 直接根据具体框架或产品搜索解决方案如airtable-database，不必拘泥于通用方案如event-sourcing/eav，在产品讨论中常有细节和ideas
  - 解决方案在npm也可以搜到，且更准确
  - 拆分核心内容和周边功能
    - split git-src and issues/pr/wiki, split txt/docx/xlsx and api
    - 将更多精力投入 core content 的创作，以及格式兼容、平台兼容、产品集成
  - 不必执着于vanillajs，常用模式早晚会抽象出工具库或框架，如reactive/effect/ajax/undo
# dev-2024-方向+方法+时间
- 👉🏻 output: 代码产出、产品落地、生态积累
- cms
  - outline, payloadcms, undb, nocobase
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
    - remove zustand
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
# dev-01

## 011

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
