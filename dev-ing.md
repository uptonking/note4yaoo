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
rm package-lock.json && find . -name 'node_modules' -type d -prune -exec rm -rf '{}' +

# npm i
  DEBUG=* npm i --no-audit --loglevel silly
DEBUG=* npm install --legacy-peer-deps --no-audit --loglevel silly

$$('[contenteditable]')

flatpak run com.discordapp.Discord --proxy-server="socks5://127.0.0.1:1080"
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
# dev-03-realworld-react-nodejs

## 031

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
# dev-02-hexo-eg-&-strapi-eg

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
