---
title: dev-ing
tags: [dev-xp, dev，dev-log]
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

sudo find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + 

# 格式化当前包，注意在子文件夹执行命令也会从package.json目录开始格式化整个包
prettier --write '**/*.{js,jsx,ts,tsx,json}' --ignore-unknown
eslint --ext .js,.ts,.tsx --quiet --fix . 

# npm i
  DEBUG=* npm i --no-audit --loglevel silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel=silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel=silly --registry=https://registry.npmmirror.com

npm --registry=https://registry.npmmirror.com install   axios
yarn add axios --registry=https://registry.npmjs.org/  
pnpm install --registry=https://registry.npmmirror.com --loglevel=debug

export https_proxy=http://127.0.0.1:7890;export http_proxy=http://127.0.0.1:7890;export all_proxy=socks5://127.0.0.1:7890

$$('[contenteditable]')

flatpak run com.discordaspp.Discord --proxy-server="socks5://127.0.0.1:7897"
betterdiscordctl -i flatpak install

npx create-strapi@latest --ts --use-npm --git-init  --example --skip-cloud --skip-db    --quickstart ./emptyFolder

vite --host 0.0.0.0 --port 8080
serve -p 9000 --cors
HOST=0.0.0.0 PORT=8080 react-scripts start

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
  - ui: ariakit, zag/ark, radix-ui/base-ui, mantine
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
# dev-2025-方向+方法+时间
- 👉🏻 output: 代码产出、产品落地、生态积累

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
  - kanban view, specification
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

- [Scrum Poker Online - Free Tool for Planning Poker](https://www.scrumpoker-online.org/en/room/64881797/scrum-poker)

## ing

- yaoo-proj
  - codemirror-devtools

- not-yet
  - ~~elmesque-editor~~, 基于immutable思想实现的编辑器大多采用redux/elm风格
  - branching/versioned-doc
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav
  - todo remove hashId在编辑器model中有什么作用
  - 做完tailwind-table就面试

- dev-to 提炼核心`需求+产出`工作流，不能在产品中检验的技术不玩
# dev-02

## 02x

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

console.log(
  '📝 ide-file ',
  filePath,
  isFollow,
  selectedFilePath,
  store.file.latestRequestFilePath(),
  isOtherUserOpened,
  agentUserId,
  event,
);

console.trace(';; loadFile', path, loadType);

// apps/webapp/src/components/pull-request-box/commit/commit-message.tsx
```

```
^(?!42\["resourceM).*
```

- lsp支持的语言排查
  - 鼠标放上去就消失lint了
  - 让settings开关联动

- 文件树M标记的处理
  - 清理标记的时机， fork时和commit时，提供手动删除.1024feature-file的能力
    - goAgent去删，ideServer不关心git操作和文件操作
  - A/D标记不支持
  - goAgent触发的时机不太确定，计算资源占用大
  - gitignore的文件不应该显示M

- 🔲 🔜
  - terminal在执行时需要自动滚到末尾，方便显示最新输出信息
  - terminal在follow时自动打开，在非follow时显示更新的红点
  - terminal放大缩小折叠展开后，光标自动聚焦在terminal
  - 编辑器行号宽度样式优化
  - 编辑器打开时自动跳到diff视图第一个变更块的位置
  - action路径超出卡片宽度
  - 修复文件树将文件夹拖到文件夹不work的问题
  - 变更列表 accept-all, reject-all
  - ~~webview自动打开, 刷新时保持打开~~
  - cmdk工具条无法触发，快捷键可以

- 异常处理增强
  - 观测重要log: RESOURCE_NOT_ENOUGH

### 多标签设计与实现-快速方案

- limitations
  - 不支持超过2个分栏布局
  - 不支持一个分栏内创建tab-group
  - 支持将webview标签页自由拖拽到任意标签旁

- 单人多标签的场景，只需要在内存保存多个文件的数据，但要支持多个编辑器显示和编辑同一份数据

- 协同多标签的场景，
- 跟随模式下会自动切换标签页，
  - 大多数场景下，切换标签页时先save再切换
  - 特殊场景如用户处于cmdk或regenerate或search的输入框且修改了提示词但还没有点击send或执行，此时切换会造成用户数据丢失
    - 在cmdk未accept时切换的场景
- 更改布局的操作如浮动驾驶舱或split-editor-right是否要支持协同
  - vscode会将光标自动切换到新tab内容的对应位置
  - 标签页的其他数据如何协同，如image放大比例
- 非编辑器的页面如何协同如图片查看页、浏览器页
  - 在标签页头部显示用户头像？
  - 最好能同步光标位置，iframe内容上光标的位置难以准确确定

### 删除移动文件的设计与实现-快速方案

- action-删除文件
  - live模式显示弹窗
  - 回放模式显示红色背景的文件快照

## 0211

- 昨天
  - 测试跟随时打开已删除文件时遇到异常大弹窗的问题，今天会合到staging
  - 修复与上面类似的问题，执行新建文件夹时编辑器一直loading
- 今天
  - 修复执行新建文件夹时编辑器一直loading
  - ai执行时，ai和用户头像没有定位到文件树对应文件的问题

## 0210

- 上周
  - 调整前端日志接入观测云的方式，补充主要流程节点的日志，方便排查用户反馈
  - 处理近期反馈的高优先级issues，如扩容提示消息、cmdL改为cmdShiftL
- 本周
  - 继续处理近期反馈的高优先级issues
  - 开发本次迭代规划的需求
- 今天
  - 测试跟随时打开已删除文件时遇到异常大弹窗的问题
  - 最近又收到新建文件类型的action执行后在文件树不显示的反馈，找到了稳定复现的方法，今天会解决此问题
  - 处理近期反馈的高优先级issues

- [Feat/fix bugs 0116 time-machine action click enhancement by huisnotacouncillor · Pull Request #491 · clacky-ai/clacky-ai-frontend](https://github.com/clacky-ai/clacky-ai-frontend/pull/491)

- [get the second to last item of an array? - Stack Overflow](https://stackoverflow.com/questions/6499012/get-the-second-to-last-item-of-an-array)

```JS
array_fragment[array_fragment.length - 2]

path.split('/').slice(-2)[0];
path.split('/').slice(-2).reverse().pop()

path.split('/').reverse()[1];
```

## 0208

- 昨天
  - 和壮壮一起补充完善了前端关键流程节点的日志，方便排查用户反馈
  - 部分实现了自定义现有的toast提示消息组件，解决机器扩容时toast消息显示多条的问题
    - 使用现有组件逻辑不方便，因为每次都会创建新的toast
  - 又收到新建文件类型的action执行后在文件树不显示的反馈，并且找到了稳定复现的方法，排查了一部分日志发现没有触发fileTree事件，今天会尽快解决此问题
- 今天
  - 解决新建文件类型的action执行后在文件树不显示的问题
  - 处理近期反馈的高优先级issues

## 0207

- 昨天
  - 因为有些紧急issue无法复现也没有日志，在clacky前端给pass初始化流程和重要事件添加了日志
  - 将前端日志从rum迁移到和后端统一的查看位置，并在文档上记录了clacky日志的格式约定
- 今天
  - 处理cde高优先级的issues，解决影响近期发版的问题

- [Typescript: No index signature with a parameter of type 'string' was found on type '{ "A": string; } - Stack Overflow](https://stackoverflow.com/questions/56568423/typescript-no-index-signature-with-a-parameter-of-type-string-was-found-on-ty)
  - (this. DNATranscriber as any)[character]; 

## 0206

- 昨天
  - 优化了机器扩容时的异常提示消息体验，今天会尽快合到正式环境
  - 将业务侧paas sdk相关的异常接入观测云，后面会将更多的关键日志接入观测云
- 今天
  - 继续cde高优先级的issues
  - 处理删除移动文件相关的问题

- [How to override multiple console function? (console.log, console.info etc) - Stack Overflow](https://stackoverflow.com/questions/73232960/how-to-override-multiple-console-function-console-log-console-info-etc)
  - for-loop 逐个覆盖
  - new Proxy(console, { get(console, key){} })

- [Hijack console.log, console.warn, and console.error without breaking the default browser function.](https://gist.github.com/designbyadrian/2eb329c853516cef618a)

- [How to override the console methods in Javascript | Our Code World](https://ourcodeworld.com/articles/read/104/how-to-override-the-console-methods-in-javascript)

## 0205

- 年前
  - 根据反馈调整端口转发的交互细节
  - 在playground状态inactive时，添加自动重试发送激活消息的逻辑
- 本周
  - 修复年前规划的剩余issues
- 今天
  - 排查文件树在某些场景下未自动更新的问题
# dev-01-forwarded-ports-&-agentWriteFile-timeout-&-alpha-test-fix-&-iframe-url-updates-&-cmdk-ux

## 0124

- 昨天
  - 和佳路确定探测中端口的交互细节，并上线staging
  - 修复一些影响发版的issues
- 今天
  - 继续修复紧急优先级的issues
  - 设计删除文件的体验和实现方案

## 0123

- [How can I force a `span` to not wrap at the end of a line? - Stack Overflow](https://stackoverflow.com/questions/7015317/how-can-i-force-a-span-to-not-wrap-at-the-end-of-a-line)

```CSS
.span-nowrap {
  display: inline-block;
  width: max-content;
}
```

- 昨天
  - 优化cde的编辑体验，进一步还原cmdk的动效边框，优化了cmdk在ai返回大量内容时的超时问题
- 今天
  - 和佳路确定端口转发中探测中端口的交互细节，并上线
  - 设计删除文件的体验和实现方案

- cmdk卡片是否要自动隐藏，不方便复制粘贴提示词，不方便在异常后保持卡片位置和内容
- cmdk的accept/reject快捷键的样式确认
- cmdk的打字效果在大文件经常超时或卡死，需要讨论解决方案

## 0122

- 昨天
  - 优化cde的编辑体验，解决了点击浮动工具条没有唤起cmdk输入框的问题，还原了cmdk的ai工作动效
- 今天
  - 继续优化cde的编辑体验，还剩余2个紧急问题
  - 设计删除文件的体验和实现方案

## 0121

- 昨天
  - 讨论并梳理年前剩余issue的复杂度和优先级
  - 开始进一步优化cde的编辑器，解决了cmd-z有时会唤起cmdk输入框的问题
- 今天
  - 继续优化cde的编辑体验，集中解决cmdk相关的问题

## 0120

- 上周
  - 集中处理体验测试反馈的问题，主要是add-to-chat背景色挡住文字、webview宽度优化
  - 修复terminal经常不可用的问题
  - 开始实现当用户点击webview内的链接时自动更新上方的url的功能，访问iframe内的对象碰到跨域问题，需要讨论下解决方案
    - 一种思路是用户访问url前向网站注入自定义js脚本逻辑
- 本周
  - 优化webview的体验
  - 实现删除移动文件在live和回放模式的表现
  - 修复年前规划的剩余issues
- 今天
  - 继续优化webview面板的体验
  - 排查文件树在某些场景下未自动更新的问题

## 0119

- [Difference between DOMContentLoaded and load events - Stack Overflow](https://stackoverflow.com/questions/2414750/difference-between-domcontentloaded-and-load-events)
  - `DOMContentLoaded` event is fired when the document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading 
  - `load` event will do it when all the images and sub-frames have finished loading.

- [Detect DOMContentLoaded in iframe - Stack Overflow](https://stackoverflow.com/questions/16960829/detect-domcontentloaded-in-iframe)
  - If your page and the iframe are on the same domain, you have to wait for the original page to fire `DOMContentLoaded` first, then attach a `DOMContentLoaded` event listener on the iframe's Window (not Document).

- 周四
  - 协助排查点击action时显示的diff视图与ai实际修改内容不一致的问题
  - 尝试实现当用户点击webview内的链接时，自动更新上方的url，参考了codesandbox的实现，确定了方案
- 今天
  - 继续优化webview面板的体验
  - 排查文件树在某些场景下未自动更新的问题

## 0117

- [WindowProxy and Window objects? - Stack Overflow](https://stackoverflow.com/questions/16092835/windowproxy-and-window-objects)
  - iframe.contentWindow, or window.frames[0], or any other way of attempting to access a window, return a WindowProxy object, not a Window object. That WindowProxy object delegates to whatever the current Window is

## 0116

- 昨天
  - 集中处理体验测试反馈的问题，主要是add-to-chat背景色挡住文字、webview宽度优化
  - 将一些无法复现的问题移入了backlog，再观察一段时间能否复现
- 今天
  - 优化webview面板的操作体验
  - 排查ai写文件超时的问题
  - 修复年前规划的剩余问题

## 0115

- 昨天
  - 修复了terminal经常不可用的问题
  - 修复了文件树搜索的关键词包含特殊字符时导致页面崩溃的问题
- 今天
  - 集中修复体验测试反馈的问题

- 🤔 [innerWidth and outerWidth oddness on desktop - Stack Overflow](https://stackoverflow.com/questions/22468878/innerwidth-and-outerwidth-oddness-on-desktop)
  - One reason `innerWidth` could be larger than `outerWidth` is if your browser is zoomed

- [AWS EFS too slow when i use git & npm install - Stack Overflow](https://stackoverflow.com/questions/63768023/aws-efs-too-slow-when-i-use-git-npm-install)
  - EFS with git, regardless of config is not working very well. However, rsync works much better. 
  - As such a workaround for EFS+git repo that worked for me: Clone to an EBS. Rsync to the EFS

## 0114

- [regex - javascript syntax error: invalid regular expression - Stack Overflow](https://stackoverflow.com/questions/16168484/javascript-syntax-error-invalid-regular-expression)
  - In this case you didn't actually need regular expressions, but if you want to avoid invalid characters in your expression you should escape it:

```JS
RegExp.quote = function(str) {
  return str.replace(/([.?*+^$[\]\\(){}|-])/g, "\\$1");
};
var re = new RegExp(RegExp.quote(filter));

RegExp.quote = function allowSpecialSymbols(str) {
  return str.replace(/([.?*+^$[\]\\(){}|-])/g, '');
};
const regExp = new RegExp(RegExp.quote('some \ string'), 'i');
```

- 昨天
  - 继续排查刷新页面不显示编辑器和文件树的问题，初步结论是没什么思路
  - 尝试修复terminal经常不可用的问题，定位到了原因，修复方法还在尝试
- 今天
  - 继续修复terminal经常不可用的问题
  - 修复体验测试反馈的问题
  - 实现删除移动文件在live和回放模式的表现

[fromMQ] fileChange

```log

[Nest] 44  - 01/14/2025, 10:13:23 AM VERBOSE [RabbitmqService] [mqName:paas-ide-server-dev-6db6599549-c84mm][playgroundId:746966488363220992][rabbitmq.service.ts:129] <=[fromMQ] fileChange[750759531793043456]:{"messageId":"21c50acd-d21d-11ef-a5ca-0242ac110004","timestamp":1736820803,"replyMessageId":"","dockerId":"750759531843375104","fileChanges":[{"path":"venv/include/python3.11","change":1,"type":1},{"path":"venv/lib/python3.11","change":1,"type":1},{"path":"venv/lib/python3.11/site-packages","change":1,"type":1},{"path":"venv/bin","change":1,"type":1},{"path":"venv/include","change":1,"type":1},{"path":"venv/lib","change":1,"type":1},{"path":"venv/pyvenv.cfg","change":1,"type":0},{"path":"venv","change":1,"type":1}]} +9038ms

```

## 0113

```shell
curl -i -X POST -H 'Content-Type: application/json' -d  '{"name": "New1", "email": "yaoo@qq.com","password":"111111"}' http://rest-api.io/items
```

- 上周
  - 修复了重启容器后部分状态未更新的问题
  - 修复布局最大化和收起terminal有时不work的问题
  - 修复了一些紧急issues，如驾驶舱聊天框的光标经常跳到行尾
  - 修复了cde一些其他issue
  - 花了较多时间排查cde激活失败、ai写文件超时、刷新页面不显示编辑器文件树的问题
- 本周
  - 实现删除移动文件在live和回放模式的表现
  - 修复年前规划的剩余issues
- 今天
  - 继续排查刷新页面不显示编辑器文件树的问题
  - 修复一些urgent优先级的bug，特别是佳路反馈的terminal经常不可用的问题

## 0110

- 昨天
  - 继续排查了agentWriteFile超时问题，但staging环境昨天无法复现了，根据日志还是把问题定位在fs.writeFile, 我把排查日志在linear上记录了，这个问题再观察一段时间
  - 修复布局最大化按钮和terminal收起按钮有时不work的问题，已合入staging
  - 修复高优先级bug，在驾驶舱输入框文字中间输入时，光标经常跳到末尾
  - 开始修复昨天反馈的搜索关键词包含正则时，卡住不可用的问题
- 今天
  - 继续修复昨天反馈的搜索体验问题
  - 修复一些urgent优先级的bug，特别是佳路反馈的terminal经常不可用的问题

## 0109

- [node.js - Fs.writeFile callback not called - Stack Overflow](https://stackoverflow.com/questions/52225476/fs-writefile-callback-not-called)
  - I've temporarily fixed the issue by writing a synchronous version with fs.writeFileSync
  - If process is dead before the writing path is done, your callback will not be called because it is an asynchronous.

- 昨天
  - 修复布局最大化和收起terminal有时不work的问题，还剩一点工作
  - 排查佳路反馈的激活失败的问题，暂时没什么解决思路
  - 排查staging环境的agentWriteFile超时问题，已定位到问题出在是node fs.writeFile这一步
- 今天
  - 修复agentWriteFile超时问题
  - 测试和完善布局相关的功能，并合入staging
  - 修复一些urgent优先级的bug，特别是聊天框输入时光标自动跳到行尾

## 0108

```log
tempOTInfo before write file: true, {"revision":0,"locked":false,"currentDoc":""} 
```

- 昨天
  - 修复restart container后，部分playground status未更新的问题
  - 排查布局上的最大化按钮、terminal收起按钮有时不生效的问题，定位到是最近实现布局自动持久化和恢复导致的，与编辑器无关，已经修改了持久化相关的逻辑，还要再测试下
- 今天
  - 测试和完善布局相关的功能，并合入staging
  - 修复一些高优先级的bug，特别是聊天框输入时光标自动跳到行尾
  - 实现删除文件在live和回放模式的表现

## 0107

- 昨天
  - 端口转发增强的功能合入staging，并修复相关问题
  - 梳理了linear上删除移动文件相关的issues，分析了删除移动重命名文件在live和回放模式的主要交互
- 今天
  - 和产品确认删除移动重命名文件的需求和交互细节
  - 实现删除文件在live和回放模式的表现
- 风险
  - terminal上的restart按钮导致容器重启后，有一些ide-server上的数据没有及时清除，如开放的端口，需要讨论解决方案

## 0106

- restartServer后如何更新ports数据
  - S1: ~~在restartServer的逻辑中，加上获取ports的逻辑~~ 后端方案，调整restart成功的时机
  - S2: 在restartServer后， 在前端业务侧手动请求ports数据，缺点是sdk的demo不能正常使用
    - 此方案耦合度最低，易维护
  - ✅ S3: 在周边事件中添加ports数据或playgroundStatus数据，如在active事件后自动发送ports数据
  - S4: 纯前端的场景定制方案, 前端主动将webview设为空白

- 上周
  - 根据业务需求，与杨豪调整了端口转发事件相关的数据结构
  - 端口转发渲染层逻辑重构
  - 进一步优化了ai写字和显示动画的时序
  - 修复cde的一些issue，如action不显示描述，webview面板的自动打开和刷新页面恢复
- 本周
  - 快速完成删除移动文件在live和回放模式的表现
  - cde空间布局体验优化
- 今天
  - 端口转发增强的功能尽快合入staging
  - 快速完成删除移动文件在live和回放模式的表现

## 0103

- 昨天
  - 根据业务需求，与杨豪调整了端口转发事件返回的数据结构
  - 重构webview组件的渲染和更新逻辑，因为要兼容很多现有的状态计算，所以没调整完，internal server error的逻辑还在处理中
  - 修复action不显示描述的问题
- 今天
  - 调整完端口转发的逻辑和体验
  - 快速完成删除移动文件在live和回放模式的表现
- 风险
  - runningStatus的现有实现对于在命令行执行程序的场景几乎没有考虑，影响到了很多组件状态，如iframe的url选择逻辑

## 0102

- 昨天
  - 在ide-server调整了ai写字和显示动画的时序，解决打字动画有时不显示的问题
  - 联调端口转发的事件和逻辑，重构webview组件的渲染和更新逻辑
- 今天
  - 调整完端口转发的逻辑和体验
  - 快速完成删除移动文件在live和回放模式的表现
