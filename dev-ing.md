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
  - 做完tailwind-table就面试

- dev-to 提炼核心`需求+产出`工作流，不能在产品中检验的技术不玩
# dev-03

## 030

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
[Nest] 44 - 02 / 25 / 2025, 9: 52: 16 PM ERROR[PlaygroundItem][mqName: paas - ide - server - 54 c68844fb - 6 hhwm][agentUserId: clacky][playgroundId: 740285278417498112] Error: ENOENT: no such file or directory, scandir '/app/data/codeZone/2024/1/12-16/@7ae1bce9-0562-4f50-b3e2-73709105f44f/dependency/home/app' + 1 ms
```

```
^(?!42\["resourceM).* 

update package @dao42/clacky-paas-front to next patch version, and add one-line changelog in changelog.md
update package @dao42/clacky-paas-front to next patch version, and run pnpm install

add an action to run "npm install -ddd" and another action to add datetime at top of readme.md
add action to create quickSort1.mjs and add 200 separate test cases with more than 200 lines of code in it, because i want to do performance test.
add action to create a route /nextjs with nextjs changelog content in it , and show nextjs link in home page, when clicking the link, jump to /nextjs route

add action to create quickSort1.mjs and add 3 test cases in it
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
  - terminal在follow时自动打开，在非follow时显示更新的红点
  - terminal放大缩小折叠展开后，光标自动聚焦在terminal
  - 编辑器行号宽度样式优化
  - 修复文件树将文件夹拖到文件夹不work的问题
  - 变更列表 accept-all, reject-all
  - ~~terminal在执行时需要自动滚到末尾，方便显示最新输出信息~~
  - ~~编辑器打开时自动跳到diff视图第一个变更块的位置~~
  - ~~action路径超出卡片宽度~~
  - ~~webview自动打开, 刷新时保持打开~~
  - ~~cmdk工具条无法触发，快捷键可以~~

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

## 0323

- 昨天
  - 清理sdk的浏览器组件，将未实现完的loading隐藏
  - 与茜茜确定revert后打开文件，diff视图的对比逻辑 和 revert/restore工具条 的需求变更，调整了一部份代码
- 今天
  - 继续调整 revert后打开文件自动定位到未被revert的action
  - 测试diff视图的逻辑，保证准确性

## 0321

- 昨天
  - 在thread close后，允许编辑文件
  - 设计webview刷新时的loading状态，今天会继续完善
- 今天
  - 进一步清理sdk的浏览器组件，减少rerender的次数，来减少白屏时间

## 0319

- 昨天
  - 完成子需求，创建root-thread时添加二次确认的指引
  - 测试和检查入职流程的整体需求，已经合到staging
- 今天
  - 进一步清理sdk的浏览器组件，减少rerender的次数，来减少白屏时间
  - 和佳路讨论优化场景，打开多个端口时，webview是否要自动切换到展示最新port

## 0318

- 昨天
  - 给thread列表添加了树形ui
  - 开始入职流程最后一个子需求，创建root-thread时添加二次确认的指引
- 今天
  - 完成子需求，创建root-thread时添加二次确认的指引
  - 测试和检查入职流程的整体需求，今天应该可以合到staging

## 0317

- [[Tooltip] tooltips are shown for disabled buttons but documentation says it shouldn't happen · Issue · radix-ui/primitives](https://github.com/radix-ui/primitives/issues/1914)
  - Indeed, setting `pointer-events: auto !important` (`!pointer-events-auto` in Tailwind) allows to show the tooltip even when disabled is true

- [margin - Spacing - Tailwind CSS](https://tailwindcss.com/docs/margin)
  - Use `space-x-<number> or space-y-<number>` utilities like space-x-4 and space-y-8 to control the space between elements

- 上周
  - 开发P0级的需求，入职流程引导，实现了6个子需求，还剩2个
  - 处理用户反馈的一些问题，如路由跳转、diff不一致、文件打不开等，花费时间较多，导致入职流程需求未按时完成
  - 清理了sdk的webview的一些废弃代码和逻辑
- 本周
  - 快速完成P0级的需求，入职流程引导
  - 大概花3天开发P0级的需求, webview减少白屏时间、增加loading反馈
- 今天
  - 继续完善入职流程子需求，给thread列表添加树形ui
  - 测试和检查入职流程的整体需求，尽快上线

## 0314

- how to create terminal, send input, get result  in linux , show me dev tips and  some code examples in nodejs
  - Use `child_process.spawn` for real-time interaction
  - Use `child_process.exec` for simple commands
  - Use `stdin, stdout, and stderr` streams: to interact with the child process programmatically.
  - Use asynchronous methods to avoid blocking the Node.js event loop.

- 昨天
  - 解决用户反馈的 requirements.txt打不开的问题，已合入develop
  - 排查了用户反馈的问题，ai-diff 与 github-pr的diff不一致的问题，是产品设计问题，已反馈给佳路
  - 排查了内部反馈的一些问题，如makePlan的数据是否是修改过的数据
- 今天
  - 继续处理onboarding入职项目流程的剩余2个半需求，树形ui需要花费较多时间

## 0313

- [What is the most efficient way to read only the first line of a file in Node JS? - Stack Overflow](https://stackoverflow.com/questions/28747719/what-is-the-most-efficient-way-to-read-only-the-first-line-of-a-file-in-node-js)

```JS
const fs = require('fs');
const readline = require('readline');

// 🚨 This won't work with zero length file. The promise will wait for resolve call forever.
// Seems to work fine with a zero length file, but may be due to an update. I'm running Node v16.2.0.
async function getFirstLine(pathToFile) {
  const readable = fs.createReadStream(pathToFile);
  const reader = readline.createInterface({ input: readable });
  const line = await new Promise((resolve) => {
    reader.on('line', (line) => {
      reader.close();
      resolve(line);
    });
  });
  readable.close();
  return line;
}
```

- 昨天
  - 提测了onboarding入职项目流程的5个半子需求，还剩2个半
  - 排查了用户反馈的 requirements.txt打不开的问题，原因是ide-server读取utf16文件时识别为二进制，昨天改了这一块的逻辑但打开后乱码，今天需要继续改读写文件的逻辑
- 今天
  - 继续处理onboarding入职项目流程的剩余2个半需求，手动关闭root thread需要陈越这边更新下后端的逻辑
  - 继续处理requirements.txt打不开的问题

## 0312

- 昨天
  - 实现了onboarding入职项目流程的4个issue，还剩2个优先级高的
  - 在状状的协助下，排查了用户反馈的路由跳转未生效的问题，是用户业务侧问题，不是clacky平台问题
- 今天
  - 处理onboarding入职项目流程的剩余2个高优先级issue，涉及树形ui要花费较多时间

- 排查ai执行action结束后，打开文件ai-diff没有红绿块的问题
  - 因为ai在用户执行前的thinking阶段就自己把文件改了，这是非预期的

## 0311

- 在html中显示同向斜引号
  - `{' '} <span className='font-["Inter_Variable",_"SF_Pro_Display",_-apple-system,_BlinkMacSystemFont,_sans-serif]'> “Root Thread” </span>{' '}`

```CSS
.quotes {
  font-family: "Inter Variable", "SF Pro Display", -apple-system, BlinkMacSystemFont, sans-serif;
}
```

- 昨天
  - 清理webview react组件的一些已废弃的逻辑，减少rerender的次数，优化白屏时间
  - 进行了onboarding入职项目流程的需求评审
- 今天
  - 根据设计稿调整webview的交互细节，提升体验
  - 优化webview的loading反馈

### 💊 排查记录0311

- 🐛 问题: 用户点击 "登陆聚合页" 时，没有自动跳转到登陆界面的ui
- 💡 原因: vite在从路由 https://5800-5af768f8d191-web.clackypaas.com/ais 跳转到 https://5800-5af768f8d191-web.clackypaas.com/ais/portal.html 时，由于proxy中的路径替换没有匹配到正确的 portal.html 文件，导致这个url下前端vue组件及vue-router都未执行
  - windows下路径替换用 `\\`, clacky的cde默认是linux环境，路径替换要用`\/`
  - 解决方案如下，修改文件 `proxy/common.js`

```diff
-        const module = dir.split('\\')[1]
+        const module = dir.split('\/')[1]
```

## 0310

- 上周
  - 上线了导入知识库的需求，并修复相关问题
  - 排查ai写代码相关问题，包括重复片段、打快照超时
  - 处理文件重命名时光标跳入编辑器的问题，增加重命名时支持ESC快捷键退出
- 本周
  - 大概花3天开发P0级的需求, webview减少白屏时间、增加loading反馈
  - 会开始另一个p0级需求，LSP的优化
  - 伟强讨论后，有调整为高优先级的需求和issue也会先处理
- 昨天
  - 测试文件重命名时光标跳入编辑器的问题，已合到staging
  - 清理webview react组件的一些已废弃的逻辑，减少rerender的次数，来减少白屏时间
- 今天
  - 继续优化webview的渲染逻辑
  - 开始给webview添加loading反馈

## 0309

- 昨天
  - 处理urgent紧急issue，文件重命名时光标跳入编辑器的问题，本地修改已完成，今天会合到staging
- 今天
  - terminal打开文件的diff视图选择非revert的action
  - 开始处理p0需求，给webview添加loading反馈

## 0308

- [Use Chrome's Developer Tools to Track Element Focus, by John Kavanagh](https://johnkavanagh.co.uk/articles/use-chrome-developer-tools-to-track-element-focus/)

## 0307

- 昨天
  - 花了点时间排查群里反馈的激活失败 DOCKER_INFO_LOST的问题
  - 处理urgent紧急issue，文件重命名时光标跳入编辑器的问题，分析代码逻辑后没有找到快速解决的方法
- 今天
  - 换其他方法解决文件重命名时光标跳入编辑器的问题
  - terminal打开文件的diff视图选择非revert的action
  - 处理git stash后文件树与文件系统的同步

## 0306

- 🐛 文件重命名时光标跳入编辑器的问题
  - contenteditable的事件触发顺序: onblur > onfocusout
  - 重命名时 react input的事件触发顺序:  onKeydown(旧值) > onInput(新值) > focus
  - input连续输入字符时正确的时序: onkeydown > oninput > renderTree > ref-cb x2
- 💡 不算完美的解决方案
  - ~~对于重命名非当前打开的文件，可以将文件设为editable=false~~(非重命名的打开文件支持edit)
  - 重写重命名的逻辑

- 昨天
  - 排查ai写的代码与diff展示的代码不一致的问题，定位到是用户特殊的操作流程导致的，不是bug
  - 排查ai写文件时打快照超时的问题，根据日志可判断打快照的逻辑并未超时，由于观测云agent日志缺失，再观察看能否复现
  - 处理urgent紧急issue，文件重命名时光标跳入编辑器的问题，ai给出修改方案不work，还需要分析代码逻辑
- 今天
  - 解决文件重命名时光标跳入编辑器的问题
  - terminal打开文件的diff视图选择非revert的action
  - 处理git stash后文件树与文件系统的同步

## 0305

- [Why doesn't the try catch block catch the promise exception? - Stack Overflow](https://stackoverflow.com/questions/66119982/why-doesnt-the-try-catch-block-catch-the-promise-exception)

```JS
const test = async function() {
  throw new Error('Just another error')
}

// ❌ error not caught
try {
  test().then()
} catch (err) {
  alert('error: ' + err.toString())
}

// ✅ the following 2 pattern works
test()
  .then(result => {
    // ...use `result` here...
  })
  .catch(error => {
    // ...handle/report error here...
  });

try {
  const result = await test();
  // ...use `result` here...
} catch (err) {
  // ...handle/report error here...
}
```

- 昨天
  - 排查ai写的代码包含重复片段的问题，定位到问题是ai生成的代码质量有待提高
  - 排查导入知识库在develop环境能工作，但在staging环境不工作的问题，可能是提示词不好
  - 处理urgent紧急issue，主要是文件树重命名输入框相关问题，ai给出修改方案不work，还需要分析代码逻辑
- 今天
  - 处理urgent紧急issue，主要是文件树重命名输入框相关问题
  - terminal打开文件的diff视图选择非revert的action
  - 处理git stash后文件树与文件系统的同步

## 0304

- 排查rename时编辑器`view.focus()`触发的原因和位置

- [Find and replace with a newline in Visual Studio Code - Stack Overflow](https://stackoverflow.com/questions/30351529/find-and-replace-with-a-newline-in-visual-studio-code)
  - when search in file, Check the regular exp icon `.*`

- 昨天
  - 导入知识库在本地与 @陈旭东 联调完毕，前端已合入develop，agent部分昨天还没合入develop，今天会推进合到staging
  - 添加一个文件树搜索同步调用形式的api，但不work
- 今天
  - 处理git stash后文件树与文件系统的同步
  - 处理urgent紧急issue，主要是文件树重命名输入框相关问题
  - webview的loading交互及其他优化

## 0303

- [CursorList - .cursorrule files and more for Cursor AI](https://cursorlist.com/)
  - [awesome-cursorrules/rules/react-typescript-nextjs-nodejs-cursorrules-prompt-/.cursorrules at main · PatrickJS/awesome-cursorrules](https://github.com/PatrickJS/awesome-cursorrules/blob/main/rules/react-typescript-nextjs-nodejs-cursorrules-prompt-/.cursorrules)

- 上周
  - 排查用户反馈的问题，主要包括，排查 Console 输出 Cannot write file 的异常， ai写代码后在编辑器显示重复代码的问题，花了较多时间但没有找到原因
  - 优化了cde的体验细节，包括terminal打开文件路径支持显示diff，减少webview和ports出现的频率
  - 处理ide-server在监控告警上的噪音日志
  - 开发P0级的需求-导入知识库，前端进度80%
- 本周
  - 推进需求-导入知识库上线
  - webview的loading交互及其他优化
  - LSP语法跳转的修复和增强
- 今天
  - 本地测试导入知识库的需求，尽快合入staging
  - 处理git stash后文件树与文件系统的同步
  - 确定下一个开发任务

- 迭代需求重点
  - webview关闭打开逻辑优化
  - 语法跳转 (LSP跳转)
  - 编辑器 - TS 项目支持 Lint
  - Tab代码补全 - 迭代一
# dev-02-logging-to-guance-&-fix-folder-crud-loading-&-user-issues-fixes-&-ai-rules-cursorrules

## 0228

- 昨天
  - 开发P0级的需求-导入知识库，与产品设计确定了交互细节，在clacky前端实现了导入知识库的cde tools
- 今天
  - 在paas实现了placeholder占位符，完成需求开发，与意如在develop环境核对交互，与 陈旭东 联调导入知识库的完整流程，合入staging

- [Difference between DOM parentNode and parentElement - Stack Overflow](https://stackoverflow.com/questions/8685739/difference-between-dom-parentnode-and-parentelement)
  - In most cases,  `parentElement` is the same as `parentNode`. The only difference comes when a node's `parentNode` is not an element. If so,  `parentElement` is null.

```JS
document.body.parentNode; // the <html> element
document.body.parentElement; // the <html> element

document.documentElement.parentNode; // the document node
document.documentElement.parentElement; // null 👈

(document.documentElement.parentNode === document); // true
(document.documentElement.parentElement === document); // false
```

- [Is there a CSS parent selector? - Stack Overflow](https://stackoverflow.com/questions/1014861/is-there-a-css-parent-selector)
  - The W3C's Selectors Level 4 Working Draft includes a :has() pseudo-class that provides this capability
  - The pseudo element `:focus-within` allows a parent to be selected if a descendent has focus.

- [VIM: how to go to exact line on Ubuntu - Stack Overflow](https://stackoverflow.com/questions/6380635/vim-how-to-go-to-exact-line-on-ubuntu)
  - :1500
  - try `150G` to get to line 150. which is less key strokes then `:150Enter`

## 0227

<!---

# Best Practices
  - Define Rule Objectives
  - Define coding Standards & Style
  - Avoid Rule Conflicts
  - Provide Examples
  - Key Conventions
  - Organize and Tag
-->

- 昨天
  - 处理了ide-server的监控告警噪音日志
  - 优化了cde的体验细节，包括terminal打开文件路径支持显示diff，减少webview和ports出现的频率
- 今天
  - 开发P0级的需求，开发导入知识库，与 陈旭东 联调和对接
  - 处理影响发版的问题

## 0226

- 昨天
  - 修复了暂停时只剩下一个action的场景下，无法开始执行的问题
  - 协助排查agent连接ide-server超时的问题，是ide-server cpu占用高导致的
  - 下午排查ai写代码后在编辑器显示重复代码的问题，通过回放确定是OT逻辑异常导致代码写入多次，今天会通过mongodb查询ot数据来进一步确认问题的原因
- 今天
  - 继续排查编辑器显示重复代码的问题
  - ide-server的噪音处理
  - 开始分析paas现有LSP的实现逻辑和梳理现有问题

- [What is the point of finally in a try..catch? - Stack Overflow](https://stackoverflow.com/questions/73813509/what-is-the-point-of-finally-in-a-try-catch#)
  - `finally` basically runs even if you have an early-return from try-catch or even if you don't handle the error in the try-catch. 

```JS
function myFunction() {
  try {
    console.log('inside "try"');
    return
  } finally {
    console.log('inside "finally"');
  }

  console.log("after try-finally");
}

myFunction()
// inside "try"
// inside "finally"
```

- [Error: ENOENT: no such file or directory, scandir '../commands' discord.js - Stack Overflow](https://stackoverflow.com/questions/71982181/error-enoent-no-such-file-or-directory-scandir-commands-discord-js)

## 0225

- 昨天
  - 上午排查通过ssh打开clacky-cde时，ports端口转发列表包含很多端口的问题，上午时间有限没什么结论
  - 下午排查ai写代码后在编辑器显示重复代码的问题，通过日志大致确定是OT逻辑异常导致代码写入多次，今天会通过回放和mongodb查询ot数据来进一步确认问题的原因
- 今天
  - 继续排查编辑器显示重复代码的问题
  - 开始分析paas现有LSP的实现逻辑和梳理现有问题

## 0224

- 上周
  - 集中处理用户反馈的issue
- 本周
  - 继续处理cde高优先级的issue
  - 开始ports端口转发和webview的优化
- 昨天
  - 排查用户反馈的问题, Console 输出 Cannot write file 错误, 在本地ubuntu系统和clacky-ubuntu系统能复现，在本地mac不能复现
  - 和 @刘天平 排查git stash后文件系统和文件树数据不同步相关的fileChange事件，文件操作的现有实现考虑非常不全面，要花时间继续改
- 今天
  - 快速开发近期反馈的2个小优化: ide server的断连与恢复提示ui、排查白屏问题
  - 修复完和 @廖伟强 确定下一个任务的优先级，先做 ports优化，还是其他的issue

```sh
run_command: npx concurrently "cd backend && npm run start:dev" "cd admin-frontend && pnpm dev:arco"
# 对于concurrently执行的命令如何stop
```

## 0223

- 掉线提示
  - terminal光标不要闪了
- 大白屏异常排查
- webview关闭按钮

- 昨天
  - 测试用户反馈的 Run button 一直 loading 的问题，分为3个子issue，解决了2/3，剩下的 @刘天平 进一步排查
  - 修复影响发版的问题
- 今天
  - 修复用户反馈的高优先级问题, 如Console 输出 Cannot write file 错误
  - git stash后文件系统和文件树数据不同步，需要配合 @刘天平 排查fileChange事件为什么缺失部分路径
  - 修复完和 @廖伟强 确定下一个任务的优先级，先做 ports优化，还是其他的issue

## 0221

- 昨天
  - 排查用户反馈的 Run button 一直 loading 的问题，分为3个子issue，解决了1/3，剩下的需要和 @刘天平 @胡状状 讨论
  - 修复了偶尔会出现的底部时光机多个 action 进度条同时loading的问题，昨晚合入了staging
- 今天
  - 修复用户反馈的高优先级问题, 如文件树数量限制，ide异常loading时任务没有restart按钮，Console 输出 Cannot write file 错误
  - 测试和修复fileChange事件和文件树的更新逻辑
  - 测试用户反馈的开关AI Diff后编辑器出现loading的问题，已合入staging

## 0220

- 昨天
  - 测试用户反馈的开关AI Diff后编辑器出现loading的问题，已合入staging
  - 排查用户反馈的webview每隔十几秒自动刷新的问题，定位到是旧版本vite的问题，已反馈给用户
  - 协助排查用户反馈的Run button一直loading的问题，发现主流程上出现异常的不停发送激活事件但manager激活不成功及心跳异常的问题，后面主要由天平在排查
- 今天
  - 修复用户反馈的高优先级问题, 如文件树数量限制，ide异常loading时任务没有restart按钮，Console 输出 Cannot write file 错误
  - 优化ports启动白屏时间过长的问题、loading反馈
  - 进一步测试和修复fileChange事件和文件树的更新逻辑

## 0219

- 昨天
  - 测试反馈 git stash 时文件树ui和文件系统不一致的问题经常出现，需要进一步测试和修复fileChange事件和文件树的更新逻辑
  - 和测试确定语法跳转的需求范围和实现方案
  - 修复用户反馈的开关AI Diff后编辑器出现loading的问题，待进一步测试
- 今天
  - 进一步测试和修复fileChange事件和文件树的更新逻辑
  - 修复用户反馈的高优先级问题
  - 优化ports启动白屏时间过长的问题、loading反馈

## 0218

- 昨天
  - 修复了用户反馈的文件树不显示文件的问题 
  - 修复过程中发现了文件树里移动操作的实现有很大缺陷，fileChange事件不包含移动的文件，修复完待测试
- 今天
  - 优化ports启动白屏时间过长的问题、loading反馈

- [`stat` command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/stat-command-in-linux-with-examples/)
  - stat -x aa.md
  - Birth: The time at which the file was created. 对于NFS系统，属性值为空
  - Change: The last time the at which file’s attribute or content was changed(the last time the file's metadata or contents were changed. Metadata includes file permissions, ownership, link count, etc.)
  - Modify: The last time at which file was modified(the last time the contents of the file were modified)
  - Access: The last time at which the file was accessed.
  - 在本地ubuntu系统，在vscode中拖拽移动文件时或通过mv移动文件时，只有ctime会变化
  - 在NFS系统，Birth一直为空, 通过mv移动文件时只有ctime会变化

## 0217

- 上周
  - 修复删除文件和新建文件夹类型的action时编辑器一直loading的问题
  - 编辑器支持.slim文件语法高亮
  - 修复cmd+p打开文件不显示diff视图的问题
  - 定位到用户反馈的文件树不显示文件的问题，原因是用户特殊的操作以及sdk文件树组件的更新逻辑异常，确定了解决方案
- 本周
  - 优化端口转发的实现细节、优化白屏时间
  - 处理未完成的cde细节优化的相关issues
- 今天
  - 快速解决文件树不显示文件的问题
  - 优化ports启动白屏时间过长的问题，增加loading的ui反馈

## 0214

- 昨天
  - 协助排查ports频繁自动断开连接且自动恢复的问题
  - 排查用户反馈的执行新建文件类型action时文件树不显示文件的问题，最后发现不是因为30个文件的限制，今天还需要继续画点时间分析日志
  - 根据反馈为了减少对服务端的影响，在playground status处于异常状态时，将每隔5s自动发动激活事件的事件间隔调整为15s-30s的随机数
  - 编辑器支持.slim文件语法高亮已上线develop环境，在develop环境测试能正常语法高亮和diff视图下正常编辑，但昨天提测的功能有点多测不过来，所以这个发版先不发这个
- 今天
  - 继续排查用户反馈的执行新建文件类型action时文件树不显示文件的问题
  - 优化ports启动白屏时间过长的问题，增加loading的ui反馈

## 0213

- 昨天
  - 在本地测试删除文件和新建文件夹类型的action，尽快合到staging
  - 修复cmd+p打开文件不显示diff视图的问题
- 今天
  - 排查ports频繁自动断开连接且自动恢复的问题
  - 执行新建文件类型action时，文件树不显示文件
  - 编辑器支持.slim文件语法高亮

## 0212

- 昨天
  - 🚧 修复执行新建文件夹类型的action时，编辑器一直loading的问题，基本修复完成还需要本地测试
  - 🚧 排查用户进入cde时卡在第3个进度条的问题，没有从底层定位到原因，在业务侧调整了发送激活事件的逻辑
- 今天
  - 在本地测试测试删除文件和新建文件夹类型的action，尽快合到staging
  - 修复cmd+p打开文件不显示diff视图的问题
  - ai执行时，ai和用户头像没有定位到文件树对应文件的问题

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
# dev-01-forwarded-ports-&-inner-testing-fixes-agentWriteFile-timeout-&-iframe-url-updates-&-cmdk-ux-close-btn

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
