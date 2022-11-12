---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# dev-2022
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-xp
- my-next
  - dev-starter
    - react patterns
    - typescript patterns
    - mvc dev pattern(for app/data-grid)
  - readonly-list-grid
    - plain
      - no sort/filter/group
      - no reorder
      - no column width resize
      - custom cell renderer
    - searchable
    - virtualizable
  - crud-list-grid
    - checkbox
    - draggable/reorder list
    - fields menu - filter/groupable
    - inline editing
    - orm integration
  - sortable-filterable-groupable-table
- 产品日历组件
  - headless-date-picker
- module/fwk/server
  - 灵活的tag/bookmark系统
- 编辑器参考
  - atlassian-editor
    - https://atlaskit.atlassian.com/packages/editor/editor-core
    - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
    - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
    - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - more-editor
    - https://demo.grammarly.com/

```JS
console.log(';; r1-user-spaces ', pathname, user, userSpaces, currentSpaceId);
```

# dev-review
- dev-goals
  - rich-editor: text/code/block
  - pivot-table
  - collaboration
  - local-database
  - annotation/comment/whiteboard
- dev-to/log/xp
  - 事项--截止日期(0730+休整)--重要性(ll/ml/hl)
  - *mirror-based-editor-vanillajs--0825--hl
  - pivot-table/grid--0828--hl
    - dropdown-menu vs tabs
  - app-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901

- not-yet
  - crdt-hlc merkle 如何在op-log中找到上次相等的timestamp
    - make indexeddb optional
  - url-as-state-management
  - 灵活的tag/bookmark系统
# dev-11
- eg-prosemirror-examples+collab
  - 重写collab示例的交互，参考blocky-editor在一个页面展示多个编辑器且支持实时协作
  - [x] 用websocket替换轮询，可基于socket.io
  - 参考atlaskit-editor实现collab，服务端未开源，但yjs提供了示例，支持切换docs
  - 分析协作时官方的undo-redo和yjs的undo-redo
- eg-tiptap-examples
  - 重写atlaskit或ckeditor的丰富示例
  - tiptap-yjs-server-src
- eg-BlockNote
- eg-focalboard
- eg-tanstack-table-v8
- sync-service: google-drive、网盘、七牛

## 1112

- [bbcode这种格式是否还有存在的必要性？ - 知乎](https://www.zhihu.com/question/20296125)
  - 在国内目前很多的网站是由phpwind和discuz论坛程序建成，而他们采用的还是很多年前开始流行的bbcode编辑器。bbcode转换出来的html过于简单和不标准，但是在处理xss攻击上确有它的好处。

- [How to install Microsoft Edge extension (addon) in Chrome](https://superuser.com/questions/1630300)
  - With browser extensions today being built using the WebExtensions API, extensions should for the most part be cross-browser compatible between Chrome, Edge, Opera and even Firefox
  - Microsoft will not give you the option to.

- [Make a desktop shortcut of Chrome Extensions - Ask Ubuntu](https://askubuntu.com/questions/1301710/make-a-desktop-shortcut-of-chrome-extensions)
  - All you really would have to do is get the Chrome Extension ID of the app and then add it to a `.desktop` file.
  - Exec=google-chrome --app="chrome-extension://ophjlpahpchlmihnnnihgmmeilfjmjjc/index.html"

- [Extending Chrome App Support on Chrome OS_202110](https://blog.chromium.org/2021/10/extending-chrome-app-support-on-chrome.html)
  - we have made the decision to extend Chrome app support for those users on Chrome OS until at least January 2025. 
  - We continue to invest and have made significant progress in rich new capabilities on the Web platform with Progressive Web Apps (PWA), 
  - 👉🏻 and we recommend that Chrome app developers migrate to PWAs as soon as possible

- ### [Chrome Extension and IndexDB Integration](https://stackoverflow.com/questions/55147450)
- You can store tons of data in any HTML5 storage (including IndexedDB or localStorage) and `chrome.storage.local` with "unlimitedStorage" permission.
- HTML5 data is stored per URL origin and each extension has its own one that looks like `chrome-extension://id` where id is a 32-character string that is the extension's id. In Firefox the origin looks like `moz-extension://id`.
- Extension's own HTML5 storage:
  - can be accessed in any extension page (popup, options, background) just like you would do it in a web page, there are no differences.
  - cannot be accessed in a content script as it runs in a web page and thus can only access HTML5 storage of the web page's URL origin.
- `chrome.storage.local` can be accessed in any extension page and in a content script.

## 1110

- [Command-line "code ." not available with flatpak app](https://github.com/flathub/com.visualstudio.code/issues/19)
  - You can add `/var/lib/flatpak/exports/bin` to PATH though and you'll get `com.visualstudio.code`
  - Yeah, flathub doesn't export arbitary names for security reasons (it'd be too easy for malicious apps to takeover your system) so I'll have to close it noting the workarounds.

## 1109

- [Kubernetes中的JSON patch](https://juejin.cn/post/6993618347904466957)
  - JSON Merge Patch和JSON Patch很像，但是他描述了JSON文档更改的版本。
  - 与上文提到的方式相比，这种方式更像git中的差异文件，而JSON PATH更像操作数据库。
  - 这种方式不包含操作，只包含文档的节点。

## 1108

- [AttributeError: module ‘collections‘ has no attribute ‘MutableMapping‘](https://blog.csdn.net/lishuaigell/article/details/125221750)
  - `collections.MutableMapping`  改成  `collections.abc.MutableMapping`

## 1107

- [pjax使用小结](https://zhuanlan.zhihu.com/p/498415741)
  - 虽然传统的 ajax 方式可以异步无刷新改变页面内容，但无法改变页面 URL，
    - 因此有种方案是在内容发生改变后通过改变 URL 的 hash 的方式获得更好的可访问性，但是 hash 的方式有时候不能很好的处理浏览器的前进、后退，而且常规代码要切换到这种方式还要做不少额外的处理。
  - 而 pjax 的出现就是为了解决这些问题，简单的说就是对 ajax 的加强。
  - pjax 结合 pushState 和 ajax 技术， 不需要重新加载整个页面就能从服务器加载 Html 到你当前页面，这个 ajax 请求会有永久链接、title 并支持浏览器的回退/前进按钮。

## 1106

- [diff 算法深入一下？](https://zhuanlan.zhihu.com/p/401340016)
  - diff 算法是 vue2.x/vue3.x 以及 react 中关键核心点，理解 diff 算法，更有助于理解各个框架本质。
  - Dom 是多叉树结构，如果需要完整的对比两棵树的差异，那么算法的时间复杂度 O(n^3)，这个复杂度很难让人接收，尤其在 n 很大的情况下，于是 React 团队优化了算法，实现了 O(n) 的复杂度来对比差异。
  - 实现 O(n) 复杂度的关键就是只对比同层的节点，而不是跨层对比，这也是考虑到在实际业务中很少会去跨层的移动 DOM 元素。

## 1105

- [前端本地存储IndexedDB数据库最新教程 视频教程](https://www.bilibili.com/video/BV1T3411874j)
  - [前端本地存储数据库IndexedDB完整教程](https://www.bilibili.com/video/BV1T3411874j)
- 使用场景
  - im聊天消息存储在本地
- 创建索引后，key
- crud
  - add添加
  - put会添加或更新数据
  - delete删除单条主键，cursor.delete可删除多条

- [Google PageSpeed vs Lighthouse: How Are They Different?](https://medium.com/@OPTASY.com/google-pagespeed-vs-lighthouse-how-are-they-different-and-which-tool-should-you-use-3f03270c674)
  - Lighthouse is now incorporated into PageSpeed Insights. It is PageSpeed’s integrated analysis engine
  - PageSpeed Insights measures the performance metric only, whereas Lighthouse audits other aspects of a website, as well (SEO, accessibility, progressive web app, etc.)

- [Chrome Developer Tools console $](https://stackoverflow.com/questions/35682890/)
  - `$()` Returns the first element that matches the specified CSS selector. It is a shortcut for document.querySelector().
  - `$$()` Returns an array of all the elements that match the specified CSS selector. This is an alias for document.querySelectorAll()
  - `$x()` Returns an array of elements that match the specified XPath.

## 1103

- searched-tech-stacks
  - nodejs-backend：优先express+orm，框架可选trpc
  - nodejs-forum: orca、mbbs
  - local-first-storage: minimongo、dexie.js、nedb

- [Electron应用数据库选型暨indexedDB扫盲](https://shenlvmeng.github.io/blog/2019/03/12/indexeddb-introduction/)

- crdt-local-first
  - https://github.com/evoluhq/evolu
  - https://github.com/clintharris/IDBSideSync

## 1101

- 分析浏览器环境下多个async方法的执行顺序
  - 在async方法`initSync/initUser/initTodoTypes`内都存在await的异步逻辑，然后分别在await逻辑前后打印1、2

```JS
setTimeout(initSync, 1000);
initUser();
initTodoTypes();

// ;; init-user  1
// ;; init-todo-type  1
// [IDBSideSync] init() 初始化indexeddb
// ;; init-user  2
// ;; init-todo-type  2
// ;; init-sync  1
// ;; init-sync  2
```

- google-drive-api-query
  - 查询结构：`query_term operator values`，注意最前面可以加not

- [Store application-specific data](https://developers.google.com/drive/api/guides/appdata)
  - `appDataFolder` 在ui上始终不可见

## 1031

- dev-to
  - state/operation-based crdt: tiny-merge; hlc

- google-drive-api-model
- folder
  - id
  - name
  - kind
  - mimeType
- file
  - id
  - name
  - kind
  - mimeType
  - owners
  - createdTime
  - modifiedTime
  - starred
  - version
  - shared
  - webContentLink/webViewLink
- remove的文件使用list api仍会存在，只有在回收站删除后才能去掉

- google-drive-api
  - [Google Workspace > Google Drive for Developers > Drive API  > Guides](https://developers.google.com/drive/api/quickstart/js)
- guide
  - https://developers.google.com/drive/api/guides/folder
  - https://developers.google.com/drive/api/guides/search-files
- api
  - https://developers.google.com/drive/api/v3/reference
  - https://developers.google.com/drive/api/v3/reference/files/list
  - https://developers.google.com/identity/oauth2/web/guides/use-token-model
    - https://developers.google.com/identity/oauth2/web/reference/js-reference
  - https://github.com/google/google-api-javascript-client/blob/master/docs/reference.md

## 1030

- dev-log
  - crdt-hlc merkle 如何在op-log中找到上次相等的timestamp

- electron和react-native-webview都支持加载local html file
  - html中的link js文件路径可能要特殊处理

- [计算机的时钟（二）：Lamport逻辑时钟](http://yang.observer/2020/07/26/time-lamport-logical-time/)
- 既然物理时钟不可靠，那就人为构造一个递增的序列来为事件排序，这就是Lamport逻辑时钟的基本思想。
- 首先需要定义先后关系(happened before)，我把事件 a 发生在 b 之前定义为 a → b。
  - 如果a和b没有先后关系，则称两个事件是并发的，记作 a || b。
- a → b 除了可以表示两个事件的先后关系，也可以理解为两个事件的因果关系，a事件导致了b事件的发生，或者说a事件影响了b事件，
  - 而 a || b 也可以理解成两个事件没有因果关系
- 我们引入逻辑时钟算法：分布式系统中每个进程Pi保存一个本地逻辑时钟值Ci，Ci (a) 表示进程Pi发生事件a时的逻辑时钟值，Ci的更新算法
- 对于任意两个事件a和b，如果 a → b，那么 C (a) < C (b)。
  - 如果 C (a) < C (b)，那么可以得出 a → b 吗？
  - 答案是不能，举个反例，图二中C (e) = 2，C (d) = 3，虽然 C (e) < C (d)，但并不能得出 e → d

- [计算机的时钟（三）：向量时钟](https://yang.observer/2020/09/12/vector-clock/)
- 在《计算机的时钟（二）：Lamport逻辑时钟》中，我们介绍过对于任意两个事件a和b，如果 a → b，那么 C (a) < C (b)，但是反向并不成立，C(a) < C(b)推不出来a→b。本文介绍的向量时钟(Vector Clocks)可以保证反向也能成立
- 向量时钟可以解决这两个问题，它的思想是进程间通信的时候，不光同步本进程的时钟值，还同步自己知道的其他进程的时钟值。

- [分布式系统：向量时钟 vector clock](https://blog.xiaohansong.com/vertor-clock.html)
  - 本文中的因果关系指的是时序关系，即时间的前后，并不是逻辑上的原因和结果
    - 本文中提及的时间戳如无特别说明，都指的是逻辑时钟的时间戳，不是物理时钟的时间戳
  - Lamport 逻辑时钟帮助我们得到了分布式系统中的事件全序关系，但是对于同时发生的关系却不能很好的描述，导致无法描述事件的因果关系。
    - Lamport 逻辑时钟算法，它提供了一种判断分布式系统中事件全序关系的方法：如果 a -> b，那么 C(a) < C(b)，但是 C(a) < C(b) 并不能说明 a -> b。也就是说C(a) < C(b) 是 a -> b 的必要不充分条件，我们不能通过 Lamport 时间戳对事件 a、b 的因果关系进行判断。
    - Lamport 逻辑时钟算法中每个进程只拥有自己的本地时间，没有其他进程的时间，导致无法描述事件的因果关系。
  - 向量时钟是在 Lamport 时间戳基础上演进的另一种逻辑时钟方法，它通过向量结构不但记录本节点的 Lamport 时间戳，同时也记录了其他节点的 Lamport 时间戳，因此能够很好描述同时发生关系以及事件的因果关系。

- [XOR — 神奇的按位运算符](https://segmentfault.com/a/1190000021519228)
3.1 使某些特定的位翻转
3.2 不用额外变量交换两个整数的值
3.3 只出现一次的数字
3.4 确定将整数 A 转换为整数 B 所需翻转的位数
3.5 判断一个二进制数中 1 的数量是奇数还是偶数
3.6 序列加密，只要选择一个合适的B，仅仅使用XOR就可以实现一个高强度的密码

- [优秀数据结构--默克尔树 go语言实现](https://blog.hujm.net/post/%E4%BC%98%E7%A7%80%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84-%E9%BB%98%E5%85%8B%E5%B0%94%E6%A0%91/)

- [Merkle Tree学习](https://www.cnblogs.com/fengzhiwu/p/5524324.html)
  - 创建Merkle Tree是O(n)复杂度(这里指O(n)次hash运算)，n是数据块的大小。得到Merkle Tree的树高是log(n)+1。
  - 检索数据块 - O(log(n))
  - 更新操作其实是很简单的，更新完数据块，然后接着更新其到树根路径上的Hash值就可以了，更新所有的hash实际上可以在O(lgn)时间内完成，因为要改变的所有节点都是相关联的
  - 插入和删除操作肯定会改变Merkle Tree的结构，插入和删除操作其实是一个工程上的问题，不同问题会有不同的插入方法。
  - 实际上Merkle Tree的结构(是否平衡，树高限制多少)在大多数应用中并不重要，而且保持数据块的顺序也在大多数应用中也不需要。因此，可以根据具体应用的情况，设计自己的插入和删除操作。一个通用的Merkle Tree插入删除操作是没有意义的。

- [区块链技术架构分析（3）-默克尔树（merkle tree）](https://zhuanlan.zhihu.com/p/39271872)
- 应用场景
  - 快速比较大量数据：当两个默克尔树根相同时，则意味着所代表的数据必然相同（哈希算法决定的）
  - 快速定位修改
  - 零知识证明：例如如何证明某个数据（D0……D3）中包括给定内容 D0，很简单，构造一个默克尔树，公布 N0，N1，N4，Root，D0拥有者可以很容易检测 D0 存在，但不知道其它内容。
  - 在分布式存储系统中的应用原理
    - 为了保持数据一致，分布系统间数据需要同步，如果对机器上所有数据都进行比对的话，数据传输量就会很大，从而造成“网络拥挤”。
    - 为了解决这个问题，可以在每台机器上构造一棵Merkle Tree，这样，在两台机器间进行数据比对时，从Merkle Tree的根节点开始进行比对，
    - 如果根节点一样，则表示两个副本目前是一致的，不再需要任何处理；
    - 如果不一样，则沿着hash值不同的节点路径查询，很快就能定位到数据不一致的叶节点，只用把不一致的数据同步即可，这样大大节省了比对时间以及数据的传输量。
  - 比特币区块链系统中的采用的是Merkle二叉树，
    - 它的作用主要是快速归纳和校验区块数据的完整性，它会将区块链中的数据分组进行哈希运算，向上不断递归运算产生新的哈希节点，最终只剩下一个Merkle根存入区块头中，每个哈希节点总是包含两个相邻的数据块或其哈希值。
    - 区块头只需包含根哈希值而不必封装所有底层数据，这使得哈希运算可以高效地运行在智能手机甚至物联网设备上
    - Merkle树可支持“简化支付验证协议”（SPV），即在不运行完整区块链网络节点的情况下，也能够对交易数据进行检验。所以，在区块链中使用Merkle树这种数据结构是非常具有意义的。

## 1029

- dev-log
  - crdt-hlc hlc

- [How to "import" a typedef from one file to another in JSDoc using Node.js?](https://stackoverflow.com/questions/49836644)

```JS
/**
 * @typedef {import('./File1.js').MyObject1} MyObject1
 */
class File2 {}
```

- [Describing an array of objects in JSDoc](https://stackoverflow.com/questions/39942884)

```JS
/**
 * @typedef AwesomeObject
 * @type {Object}
 * @property {string} name
 * @property {boolean} next
 * @property {string} test
 */

/**
 * @param {Array.<AwesomeObject>} awesomeObjects Awesome objects.
 */
myAwesomeFunction(awesomeObjects) { ... }
```

## 1028

- [vscode断点调试配置-结合nodemon自动重启](https://juejin.cn/post/6988035414586032158)

- [node调试工具对比](https://juejin.cn/post/6987396078848966663)
  - 首推 ndb，因为最起码是谷歌在维护的项目，network 面板看情况也快了
  - 第二推荐. devtool，同为 Chromium 的控制台，热更新的速度和支持插件这点真的无敌
  - 第三推荐. vscode，vscode 对调试这块非常友好，加上nodemon热更新加持，只可惜看打印的对象真的太难受了
  - 第四推荐 nodemon，因为 --inspect 体验感实在是太差了，nodemon 还不至于最后

- [Getting SQLite to delete all records in a table](https://stackoverflow.com/questions/38297873)
  - `DELETE FROM TABLE_NAME`  语句
  - When the WHERE is omitted from a DELETE statement and the table being deleted has no triggers, SQLite uses an optimization to erase the entire table content without having to visit each row of the table individually. This "truncate" optimization makes the delete run much faster.

- [MySQL 正则表达式：NOT LIKE 操作符](https://learnku.com/mysql/wikis/36430)
  - Not like 是 MySQL 用于模式匹配的运算符。
  - 它将列与给定值进行比较，并返回与模式不同的列。

```SQL
select field from table_name where column_name not like 'pattern';

SELECT word FROM table WHERE word NOT LIKE '%a%' AND word NOT LIKE '%b%'

```

## 1026

- dev-log
  - crdt-hlc server

- `HTMLFormElement.elements` 在form元素的提交事件中可以获取到`event.target.elements`
  - returns an `HTMLFormControlsCollection` listing all the form controls contained in the `<form>` element.
  - In JS it's not only Object, Array, Map & Set

## 1025

- document.createDocumentFragment() vs document.createElement('template')
  - A `DocumentFragment` is not a valid target for various events, as such it is often preferable to clone or refer to the elements within it.
  - firstClone is a DocumentFragment instance, so while it gets appended inside the container as expected, clicking on it does not trigger the click event. 
  - secondClone is an HTMLDivElement instance, clicking on it works as one would expect.

## 1024

- sqlite-常用命令
  - sudo apt install -y sqlite3 
  - sqlite3 new.db
  - .databases
  - .tables
  - .read test.sql
  - .mode list/column/line
  - [sqlite3 常用命令](https://www.jianshu.com/p/590607baa0db)

- [Prevent ESModules from being deferred when imported with script tag](https://stackoverflow.com/questions/56823415)
  - es-module里面挂载变量v1到window会被延迟，所以后面的es5脚本访问不到v1
  - Module scripts behave like defer by default – there's no way to make a module script block the HTML parser while it fetches.

- [Error [ERR_MODULE_NOT_FOUND]: Cannot find module](https://stackoverflow.com/questions/65384754)
  - When you are using ECMAScript modules you are forced to provide the file extension
  - You can also create a script in your package.json
  - NODE_OPTIONS="--experimental-specifier-resolution=node" node server.js

## 1023

- [MurmurHash算法](https://www.cnblogs.com/july-sunny/p/15880549.html)
- Murmur哈希是一种非加密散列函数，适用于一般的基于散列的查找
  - 该名称来自两个基本操作，乘法（MU）和旋转（R），在其内部循环中使用。
  - 与加密散列函数不同，它不是专门设计为难以被对手逆转，因此不适用于加密目的。　
- 使用的场景有以下特点
　　1. 要求随机分布特征表现好，不容易被猜测，例如相比于自增ID，出于安全考虑，不会暴露增长量等相关敏感的业务；
　　2. 生成性能要好(该算法的性能强于MD5)；
　　3. 函数产生的数据量大  MurmurHash2（产⽣32位或64位值）, MurmurHash3（产⽣32位或128位值), MurmurHash的 32 bit 能表示的最⼤值近 43 亿的10进制；

- 例如，在短链生成，MurmurHash这里比较好的适用于该场景
  - MurmurHash生成得到的是一个long类型的10进制数，通常我们为了缩短短链的位数，可以适用Base62将结果转换为62进制数

- [MurmurHash算法简单介绍](https://www.cnblogs.com/strongmore/p/14493705.html)
  - 哈希算法简单来说就是将一个元素映射成另一个元素，可以简单分类两类，
  - 加密哈希，如MD5，SHA256等，
  - 非加密哈希，如MurMurHash，CRC32，DJB等。
  - MurMurHash由Austin Appleby在2008年发明，与其它流行的哈希函数相比，对于规律性较强的key，MurMurHash的随机分布特征表现更良好，Redis，Memcached，Cassandra，HBase，Lucene中都使用到了这种hash算法

- [Generate random string/characters in JavaScript](https://stackoverflow.com/questions/1349404)

```JS
Math.random().toString(36).substring(7);
// If random returns 0, 0.5, 0.25, 0.125... will result in empty or short string. 
(1.25).toString(36).substr(2, 5) // 9

('0000' + Math.random().toString(36).replace('.', '')).substr(-5);

(Date.now() * Math.random()).toString(36).substring(0, 5);
```

## 1017

- The global property `Infinity` is a numeric value representing infinity.
  - The initial value of Infinity is Number. POSITIVE_INFINITY. 
  - The value Infinity (positive infinity) is greater than any other number.
  - `1/Infinity`  // 0
  - `Infinity + 1 === Infinity ` // true

- [codemirror inputRead](https://github.com/codemirror/codemirror5/issues/3162)
  - inputRead intentionally has a different name from input. The two are not supposed to be equivalent.
  - Only the code that takes typed text from the hidden textarea fires inputRead.

- [for two-element array like `[ 1, "message" ]`, How would I define this in TypeScript?](https://stackoverflow.com/questions/29382389)
  - If you are sure that there are always only two elements [number, string] then you can declare it as a tuple
  - `const foo: [number, string] = [ 1, "message" ];`

## 1016

- [socket.io Emit cheatsheet](https://socket.io/docs/v4/emit-cheatsheet)
- [io.emit vs socket.emit](https://stackoverflow.com/questions/32674391)

- [are socket io rooms automatically destroyed if empty?](https://stackoverflow.com/questions/44523007)
  - The room is automatically removed from the array and the nodeJSs' V8 Garbage Collector finishes the job of completely removing the room from ram. You don't have to worry about any of that.
  - Remember that all users are automatically put on a room on joining the server ( the socket.id named room ). 
  - `io.emit` should be used when you want to send a message from the server to anyone and 
  - `socket.emit` should be used when you want to send a message only to the sender.

- [ES6 Class Multiple inheritance](https://stackoverflow.com/questions/29879267)
  - a very clean (imho) way to compose multiple classes into one using the fact that in ES2015, classes can be created with class expressions.

- you can solve this by creating A and B not directly as classes, but as class factories (using arrow functions for brevity)

```JS
class MyClass {} // class declaration
var MyClass = class {} // class expression

class A {}
class B extends A {}
class C extends B {} // C extends both A and B
// The problem with this is that it's very static. 
// If you later decide you want to make a class D that extends B but not A, you have a problem.

class Base {} // some base class to keep the arrow functions simple
var A = (superclass) => class A extends superclass
var B = (superclass) => class B extends superclass
var C = B(A(Base))
var D = B(Base)
```

## 1014

```JS
// 注意zIndex的类型是字符串，而不是数字
ele.style.zIndex = "2"
```

- [CSS force image resize and keep aspect ratio](https://stackoverflow.com/questions/12991351)

```CSS
.img-element.style {
  object-fit: cover;
  width: 50%;
  height: 50%;
}
```

- [程序员看过来，日本IT互联网公司现状_202005](https://www.zai.tokyo/2020/05/it_12.html)

## 1011

- [How to export variables from functions in Javascript?](https://stackoverflow.com/questions/34457171)
- You can do it two ways:
  - Declare var globally so that variable can be used from anywhere(inside or outside of java script) like.. `var nombre;` declared at top of javascript, and can be initialize and used within a javascript and from other java script as well. You need to just import the source js.
  - Create a function which return the var itself. like `var myFunction = function(){return nombre;}`
    - When you need the nombre variable, just call the function as, `var newNombre = myFunction();`

- [passing an array of arrow functions](https://stackoverflow.com/questions/27156264)

```typescript

private _tasks :Array<(x: T) => boolean>;

class Foo<T>{
  // 👇🏻 注意函数数组的类型用的{ fn }，而不是(fn)
    private _tasks: { ( x: T ): boolean }[];

    constructor( ...tasks: { ( x: T ): boolean }[] ) {
        this._tasks = tasks;
    }
}
```

## 1010

- yjs-src 循环import，难以手动解决所有循环依赖
  - 临时方案是直接使用npm打包的 yjs.mjs 单文件

```JS
import { splitItem } from '../structs/Item'
import { findIndexSS, getState, iterateStructs } from './StructStore'
import { UpdateEncoderV2 } from './UpdateEncoder'
```

# dev-09

## 0930

- [how to delete all node_modules from all packages in npm 7 workspace monorepo](https://stackoverflow.com/questions/70030643)
  - npm exec --workspaces -- npx rimraf node_modules && npx rimraf node_modules
  - npx rimraf ./**/node_modules
  - npx npkill
    - List any node_modules directories in your system, as well as the space they take up. 
    - You can then select which ones you want to erase to free up space.

## 0927

- ### [How to allow CORS with Node.js (without using Express)](https://stackoverflow.com/questions/44405448)

```JS
const http = require('http');
const port = 8080;
http.createServer((req, res) => {
  const headers = {
    'Access-Control-Allow-Origin': '*', // dev First, read about security
    'Access-Control-Allow-Methods': 'OPTIONS, POST, GET',
    'Access-Control-Max-Age': 2592000, // 30 days
    'Access-Control-Allow-Headers': 'Access-Control-Allow-Headers, Origin,Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers',
    /** add other headers as per requirement */
  };
  if (req.method === 'OPTIONS') {
    // /👉🏻 cors时，post前会先发options，所以需要单独处理
    res.writeHead(204, headers);
    res.end();
    return;
  }
  if (['GET', 'POST'].indexOf(req.method) > -1) {
    res.writeHead(200, headers);
    res.end('Hello World');
    return;
  }
  res.writeHead(405, headers);
  res.end(`${req.method} is not allowed for the request.`);
}).listen(port);
```

- ### [XMLHttpRequest changes POST to OPTION](https://stackoverflow.com/questions/8153832)
- Yes, this is a "problem with same-origin policy". You are making your request either to a different server or to a different port, meaning that it is a cross-site HTTP request. Here is what the documentation has to say about such requests:
  - Additionally, for HTTP request methods that can cause side-effects on server's data (in particular, for HTTP methods other than GET, or for POST usage with certain MIME types), the specification 👉🏻 mandates that browsers "preflight" the request, soliciting supported methods from the server with an HTTP OPTIONS request method, and then, upon "approval" from the server, sending the actual request with the actual HTTP request method.
- I was having this exact problem from a JavaScript code that sent an ajax content.
  - In order to allow the Cross-Origin Request with Preflight I had to do this in the . ASPX that was receiving the petition:

```JS
//Check the petition Method
if (Request.HttpMethod == "OPTIONS") {
  //In case of an OPTIONS, we allow the access to the origin of the petition
  string vlsOrigin = Request.Headers["ORIGIN"];
  Response.AddHeader("Access-Control-Allow-Origin", vlsOrigin);
  Response.AddHeader("Access-Control-Allow-Methods", "POST");
  Response.AddHeader("Access-Control-Allow-Headers", "accept, content-type");
  Response.AddHeader("Access-Control-Max-Age", "1728000");
}
```

## 0925

- `Content-Disposition` response header is a header indicating if the content is expected to be displayed inline in the browser, that is, as a Web page or as part of a Web page, or as an attachment, that is downloaded and saved locally.

```
Content-Disposition: inline
Content-Disposition: attachment
Content-Disposition: attachment; filename="filename.jpg"
```

- [screenkey: Missing support for wayland](https://gitlab.com/screenkey/screenkey/-/issues/61)
  - GDK_BACKEND=x11
  - https://github.com/AlynxZhou/showmethekey
  - https://github.com/WhiredPlanck/showmethekey-rs
- [Wayland 下使用腾讯会议](https://icooper.cc/archives/445)
  - sudo vim /etc/gdm3/custom.conf
  - WaylandEnable=false
  - sudo service gdm3 restart

```shell
export XDG_SESSION_TYPE=x11
export QT_QPA_PLATFORM=xcb
unset WAYLAND_DISPLAY
# 上面设置变量位置要找对
if [ "$XDG_SESSION_TYPE" = "wayland" ]
```

## 0924

- [Button type "button" vs. "submit" ](https://stackoverflow.com/questions/37736056)
- submit: 
  - The button submits the form data to the server. 
  - This is the default if the attribute is not specified, or if the attribute is dynamically changed to an empty or invalid value.
- reset: 
  - The button resets all the controls to their initial values.
- button: 
  - The button has no default behavior. 
  - It can have client-side scripts associated with the element's events, which are triggered when the events occur.
- As for the difference between button and input:
- A `button` can have a separate value as data, while for an `input` the data and button text are always the same

```html
<input type="button" value="Button Text"> <!-- Form data will be "Button Text" -->
<button type="button" value="Data">Button Text</button>
```

- A button can have HTML content (e.g. images), while an input can only have text.
- 
- [Property 'value' does not exist on type 'EventTarget'](https://stackoverflow.com/questions/42066421)

```JS
const element = event.currentTarget as HTMLInputElement;
const value = element.value;
// if you are using checkboxes too this is a good solution: 
e.currentTarget.type === 'checkbox' ? 'a' : 'b';
// add type argument
const handleOnChange = (e: ChangeEvent < HTMLInputElement > ) => {
  doSomething(e.target.value);
}
```

## 0923

- [Reversing order of ordered list counter in CSS](https://stackoverflow.com/questions/15844387)
  - https://codepen.io/uptonking/pen/jOxGLZK

```html
<ol style="counter-reset: my-list-items 5;">
  <li>An element</li>
  <li>An element</li>
  <li>Another element</li>
  <li>A third element</li>
</ol>
```

```CSS
ol {
  list-style-type: none;
  list-style-position: inside;
}

li:before {
  content: counter(my-list-items) '. ';
  counter-increment: my-list-items -1;
}
```

## 0922

- [How to use radio buttons in ReactJS?](https://stackoverflow.com/questions/27784212)

```JS
class App extends React.Component {
  setGender(event) {
    console.log(event.target.value);
  }
  render() {
    return (
      <div onChange={this.setGender.bind(this)}>
        <input type="radio" value="MALE" name="gender"/> Male
        <input type="radio" value="FEMALE" name="gender"/> Female
      </div>
    )
  }
}
```

- [currentTarget VS target](https://juejin.cn/post/6844904047913205767)
  - target在事件流的目标阶段；
  - currentTarget在事件流的捕获，目标及冒泡阶段。只有当事件流处在目标阶段的时候，两个的指向才是一样的， 而当处于捕获和冒泡阶段的时候，
  - target指向被单击的对象
  - currentTarget指向当前事件活动的对象（一般为父级）。
- [React Profiler 的使用](https://juejin.cn/post/7008337341634854942)
  - 虽然 Display 在 React.memo 的比较函数之下，已经不再重新 render。但是 Display 的渲染时间和应用的渲染时间相比改写之前都变大了，这说明 memo 函数的比较时间大于组件自身的渲染时间，在当前这个简单的应用程序下，以 React.memo 来 "优化" 应用是得不偿失的。
- ### [Chrome Dev Tools 性能分析&调试技巧](https://juejin.cn/post/7076277971392135176)
- Main中展示的是火焰图，也就是函数调用的堆栈火焰图 
  - x轴表示时间，最上面的第一条名为Task就是事件触发的地方，直到结束，这条线是最长的 
  - y轴表示调用的函数，函数中还包含依次调用的函数，越到下面数量越少
- 在火焰图中选择Task时，统计区域显示与事件相关的其他信息
  - Summary：统计报表，展示各个事件阶段耗费的时间。
  - Bottom-Up: 事件时长排序，可以看到各个事件消耗事件的排序。（self-time: 事件本身耗时。 total-time: 包含子事件，从开始到结束的耗时。）
  - Call-Tree: 调用栈，在Main选中一个事件，可以看到整个事件的调用栈（从最顶层到最底层，而不是只有当前事件）
  - Event Log: 事件日志。（多了一个start time, 指事件在多少毫秒开始触发。右边有事件描述信息）
- 面板中会有很多的 Task，如果是耗时长的 Task，其右上角会有红色三角号，这是chrome自动帮助识别出有问题的部分，图中没有，说明页面首屏的逻辑处理分配得还不错。点任一任务，都可在下面统计区域里看其具体的信息

## 0921

- [Argument of type 'EventTarget' is not assignable to parameter of type 'Node'.](https://stackoverflow.com/questions/71193818)
  - 在使用前先判断类型  `e.target instanceof HTMLElement && doSth(e.target)`
- [TSX: Property does not exist on type 'JSX. IntrinsicElements'](https://github.com/microsoft/TypeScript/issues/15449)
  - 处理html自定义标签的方法

```typescript
import * as React from 'react';
declare global {
    namespace JSX {
        interface IntrinsicElements {
            'my-html-custom-tag': React.DetailedHTMLProps<React.HTMLAttributes<HTMLElement>, HTMLElement>;
        }
    }
}
```

## 0920

```JS
document instanceof HTMLElement // false
document.body instanceof HTMLElement // true
document.documentElement instanceof HTMLElement // true
document.body.parentElement === document.documentElement // true
document.body.parentElement === document.body.parentNode // true
```

- [How do you check if a JavaScript Object is a DOM Object?](https://stackoverflow.com/questions/384286)
  - obj instanceof HTMLElement
  - Using W3 DOM2 (works for FF, Opera and Chrome)

## 0919

- eclipse che vs theia
- https://github.com/eclipse-che/che-theia
  - Eclipse Che provides a default web IDE for the workspaces which is based on the Theia project. 
  - It’s a subtle different version than a plain Theia as there are functionalities that have been added based on the nature of the Eclipse Che workspaces. 
  - We are calling this version of Eclipse Theia for Che: Che-Theia.
  - So, Che-Theia is the default Che editor provided with developer workspaces created in Eclipse Che 7
  - Che-Theia contains additional extensions and plugins which have been added based on the nature of Eclipse Che workspaces and to provide the best IDE experience of Theia within Che.
- https://github.com/eclipse-theia/theia
  - Theia is a cloud & desktop IDE framework implemented in TypeScript.
  - Eclipse Theia is an extensible framework to develop full-fledged multi-language Cloud & Desktop IDE-like products with state-of-the-art web technologies.
  - Support VS Code Extension protocol

## 0918

- 在Node.js中, Punycode是一种编码语法, 用于将Unicode(UTF-8)字符串转换为基本的ASCII字符串。这很重要, 因为主机名只能理解ASCII字符。
- Punycode是一个根据RFC 3492标准而制定的编码系统, 主要用于把域名从地方语言所采用的Unicode编码转换成为可用于DNS系统的编码。Punycode可以防止IDN欺骗。

## 0917

- 华侨指的是生在中国且为中国籍的人，但目前旅居国外，用英语可以表达为Overseas Chinese
- 华人指的是生在中国，但已经加入外国国籍的人，从国际上看他们已经是外国公民了。
- 华裔则指的是先辈是华人，而本人出生在国外。
  - 华人和华裔都可以用Ethnic Chinese来表示。
  - 具体而言，比如如果是美籍华人，英语可以说Chinese American。

## 0916

- 原型链的理解
  - class的实例属性会屏蔽class.prototype上定义的同名属性
  - When trying to access a property of an object, the property will not only be sought on the object but on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.
- [How can I add a property to a class dynamically in typescript?](https://stackoverflow.com/questions/44882416)
  - You can add index signature to your class
  - Yet note that thereby you are loosing the strict typechecks and introduce potential bugs that a prone to happen in weakly typed languages.

```JS
export class UserInfo {
  [index: string]: any;
  public name: string;
  public age: number;
}
```

- [Declare dynamically added class properties in TypeScript](https://stackoverflow.com/questions/41038812)

```JS
class Augmentable {
  constructor(augment: any = {}) {
    Object.assign(this, augment)
  }
  static create < T extends typeof Augmentable, U > (this: T, augment ? : U) {
    return new this(augment) as InstanceType < T > & U
  }
}
```

## 0914

- 💡 prosemirror交互流程： DOMObserver更新state > 更新viewDesc-vdom > 更新dom
- [Textarea Auto height](https://stackoverflow.com/questions/17772260)
  - contenteditable元素里面回车可以换行，且元素高度自动增加
  - textarea里面回车元素高度不会增加，可能出现滚动条，需要手动 `<textarea oninput="auto_grow(this)"></textarea>`

### [这几个高级前端常用的API，你用到了吗？](https://segmentfault.com/a/1190000040942225)

- 💡 MutationObserver 是一个可以监听 DOM 结构变化的接口。
  - 当 DOM 对象树发生任何变动时，MutationObserver 会得到通知。
- MutationObserver 有以下特点：
  - 它等待所有脚本任务完成后才会运行，即采用异步方式
  - 它把DOM变动记录封装成一个数组进行处理，而不是一条条地个别处理 DOM 变动。
  - 它既可以观察发生在DOM节点的所有变动，也可以观察某一类变动
- MutationObserver 与事件有一个本质不同：事件是同步触发，也就是说 DOM 发生变动立刻会触发相应的事件；
  - MutationObserver 则是异步触发，DOM 发生变动以后，并不会马上触发，而是要等到当前所有 DOM 操作都结束后才触发。
  - 举例来说，如果在文档中连续插入 1000 个段落（p 元素），会连续触发 1000 个插入事件，执行每个事件的回调函数，这很可能造成浏览器的卡顿；而 MutationObserver 完全不同，只在 1000 个段落都插入结束后才会触发，而且只触发一次，大大有利于性能。
- 💡 IntersectionObserver
  - 网页开发时，常常需要了解某个元素是否进入了"视口"（viewport），即用户能不能看到它。
- 传统的实现方法是，监听到 scroll 事件后，调用目标元素的 getBoundingClientRect()方法，得到它对应于视口左上角的坐标，再判断是否在视口之内。
  - 这种方法的缺点是，由于 scroll 事件密集发生，计算量很大，容易造成性能问题。
- 新的 IntersectionObserver API，可以自动"观察"元素是否可见，Chrome 51+ 已经支持。由于可见（visible）的本质是，目标元素与视口产生一个交叉区，所以这个 API 叫做"交叉观察器"。
- 相比于 getBoundingClientRect，它的优点是不会引起重绘回流
  - 图片懒加载的原理主要是判断当前图片是否到了可视区域这一核心逻辑实现的。这样可以节省带宽，提高网页性能。
  - 传统的突破懒加载是通过监听 scroll 事件实现的，但是 scroll 事件会在很短的时间内触发很多次，严重影响页面性能。
  - 为提高页面性能，我们可以使用 IntersectionObserver 来实现图片懒加载。
- 无限滚动（infinite scroll）的实现也很简单
- 💡 window.getComputedStyle(element[, pseudo-element])
  - 返回一个 CSSStyleDeclaration 对象（与 style 属性的类型一样），包含元素的计算样式。
- getComputedStyle 和 element.style 的相同点就是二者返回的都是 CSSStyleDeclaration 对象。而不同点就是：
  - element.style 读取的只是元素的内联样式，即写在元素的 style 属性上的样式；而 getComputedStyle 读取的样式是最终样式，包括了内联样式、嵌入样式和外部样式。
  - element.style 既支持读也支持写，我们通过 element.style 即可改写元素的样式。而 getComputedStyle 仅支持读并不支持写入。我们可以通过使用 getComputedStyle 读取样式，通过 element.style 修改样式
- 💡 Element.getBoundingClientRect()
  - 返回元素的大小及其相对于视口的位置。
  - 返回值是一个 DOMRect 对象，这个对象是由该元素的 getClientRects() 方法返回的一组矩形的集合，就是该元素的 CSS 边框大小。返回的结果是包含完整元素的最小矩形
- 获取 dom 元素相对于网页左上角定位的距离
- 判断元素是否在可视区域内
- 💡 requestAnimationFrame(cb)
  - 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。
  - 与 setTimeout 相比，requestAnimationFrame 最大的优势是由系统来决定回调函数的执行时机
  - 保证回调函数在屏幕每一次的刷新间隔中只被执行一次
- 监听 scroll 函数
- 大量数据渲染

### [MutationObserver用法总结( 监听DOM变化 )](https://juejin.cn/post/7016956024561074213)

- Mutation Observer是在DOM4中定义的，用于代替Mutation events作为观察DOM树结构发生变化时，做出相应处理的API
- Mutation Events是在DOM3中定义的，用于监听DOM树结构变化的事件；
  - IE9不支持Mutation Events； Webkit内核不支持DOMAttrModified特性；  DOMElementNameChanged和DOMAttributeNameChanged在Firefox上不被支持；
  - Mutation Events是同步执行的：它的每次调用，都需要从事件队列中取出事件并执行，然后事件队列中移除，期间需要移动队列元素；如果事件触发的较为频繁的话，每一次都需要执行上面的这些步骤，那么浏览器会被拖慢；
  - Mutation Events本身是事件，所以捕获是采用的是事件冒泡的形式；如果冒泡捕获期间又触发了其他的Mutation Events的话，很有可能就会导致阻塞Javascript线程，甚至导致浏览器崩溃；
- 如果目标节点为characterData节点(一种抽象接口，具体可以为文本节点、注释节点，以及处理指令节点)时，也要观察该节点的文本内容是否发生变化；
- 这是因为在new MutationObserver传入的函数并不会监听到修改了就立即执行，而是等到同步代码都执行完了，才会去调用我们传入的回调函数；
- 在观察者对象上调用takeRecords会返回其观察节点上的变化记录(MutationRecord)数组
  - 其中MutationRecord数组也会作为观察者初始化时的回调函数的第一个参数；
  - 同时也会从MutationObserver的通知队列中删除所有待处理的通知；
  - takeRecords方法是同步执行，可以即时获取；
- [MutationObserver 监听 DOM 树变化](https://segmentfault.com/a/1190000017804945)
  - 给出了开发编辑器的简单示例

### [DOM MutationObserver – reacting to DOM changes without killing browser performance.](https://hacks.mozilla.org/2012/05/dom-mutationobserver-reacting-to-dom-changes-without-killing-browser-performance/)

- DOM Mutation Events were a major performance and stability issue and have been deprecated 
  - Google and Mozilla engineers announced a new proposal that would offer similar functionality with improved performance: DOM MutationObserver. 
- The key advantage to this new specification over the deprecated DOM Mutation Events spec is one of efficiency. 
  - 👉🏻 If you are observing a node for changes, your callback will not be fired until the DOM has finished changing. 
  - When the callback is triggered, it is supplied a list of the changes to the DOM, which you can then loop through and choose to react to.
- This is an important distinction to be made from other techniques such as binding events to key presses or more common events like ‘click’. 
  - 👉🏻 MutationObservers work differently from these techniques because they are triggered by changes in the DOM itself, not by events generated either via JS or user interaction.
- Another use case would be situations where you are using frameworks that manipulate the DOM and need to react to these modifications efficiently ( and without `setTimeout` hacks! ).

## 0913

- `document.activeElement` focus vs selection
  - activeElement returns the Element within the DOM that currently has focus.
  - Typically a user can press the tab key to move the focus around the page among focusable elements, and use the space bar to activate one
  - 👉🏻 Focus (which element is receiving user input events) is not the same thing as selection (the currently highlighted part of the document).
- [How to allow bolding, underlining and italics in textarea](https://stackoverflow.com/questions/19074391)
  - It is not possible to format text in text area. You may try using div and then ContentEditable
- [调查如何实现Web页面的Minimap（缩略图）](https://marvinsblog.net/post/2022-04-16-web-minimap/)

## 0912

- `caretRangeFromPoint(x,y)`只有firefox浏览器不支持，其他浏览器都支持，是非标准属性
  - `caretPositionFromPoint(x,y)`只有firefox浏览器支持，是标准属性
  - 返回光标所在节点及光标在该节点内的offset
  - 两个方法参数完全相同，都是 x/y position within the current viewport，即clientX/Y
- `elementFromPoint(x,y)` 不包含offset
  - returns the topmost `Element` at the specified coordinates (relative to the viewport)
- ts变量类型声明时， : vs as
  - [What is the difference between using the colon and as syntax for declaring type?](https://stackoverflow.com/questions/54684886)
  - You should always prefer a type annotation to an assertion.
  - assertation forces Typescript to think that it will always return a number (even that it could be not true).
  - annotation, Typescript will verify and ensure that there could not be another case (Even that it could never happen).

## 0906

- 导入css文件到一个限定的范围，推荐用类styled-components的运行时方案
- [How to make React CSS import component-scoped?](https://stackoverflow.com/questions/47090574)

```JSX
// ❌ 以下方式不可行，className值为 [object Object]
import styles from './index.module.scss';
const MyPage = () => {
    return (
        <div className={styles}>
            <h1>My Page</h1>
        </div>
    );
};
```

## 0905

- [CodeSandbox为创建好的项目增加terminal](https://lipanpanx.com/codesandboxwei-chuang-jian-hao-de-xiang-mu-zeng-jia-terminal/)
  - 有些人在创建的时候会出现报错 比如: 502: Bad Gateway, 一般情况下 按照报错提示修改下配置文件之类的
  - 👉🏻 碰到502时，直接新建terminal执行npm start命令，就能看到异常详细信息
  - 建议直接参考公开的项目示例
- 在codesandbox配置webpack和热加载很难work，直接用官方create-react-app模版更方便

## 0904

- [为什么 APNG 图像格式没有被广泛应用？](https://www.zhihu.com/question/20030489)
  - GIF格式的图像只支持8位颜色，即256中颜色，不能呈现真彩色画面。所以这种算法对于图像的边缘处理与整体渲染都还停留在上个世纪。
  - APNG（Animated PNG）。从字面上理解，这种格式的图像就是一个“会动”的PNG图像。这个最早是由Mozilla的两名程序员设计出来的，当时Mozilla放弃了MNG图像格式，转而自己开发了APNG用以存储动态多图文件。
  - 首先缺乏浏览器支持，这就让APNG很难普及。
  - 其次，没有PNG发开组的支持。目前，支持MNG的PNG开发组与支持APNG的Mozilla在动态图标准上已经形成了对立。
  - 从另一个角度讲，GIF这么低劣的画质之所以能“横行”网络二十多年，就是因为人们对于动态图画质的需求并不高。

## 0901

- [Can I have an element with an ID that starts with a number?](https://stackoverflow.com/questions/5672903)
- From the HTML 4.01 specs, no
  - 👉🏻 From the HTML 5 specs, yes
- Yes you can, but selecting/styling it with a CSS selector will be a pain.
  - id values that consist solely of digits are perfectly valid in HTML; anything but a space is okay. 
  - And although earlier HTML specs were more restrictive (ref, ref), requiring a small set of chars and starting with a letter, browsers never cared, which is a big part of why the HTML5 specification opens things up.
  - If you're going to use those ids with CSS selectors (e.g, style them with CSS, or locate them with `querySelector`,                                                                                                                                                                                                                                                                                                                                                                                                                      `querySelectorAll`, or a library like `jQuery` that uses CSS selectors), be aware that it can be a pain and you're probably better off staring the `id` with a letter, because you can't use an id starting with a digit in a CSS id selector literally; you have to escape it. 
  - (For instance,  `#12` is an invalid CSS selector; you have to write it `#\31\32`.) 
# dev-08

## 0829

- [how to delete extra space between buttons?](https://stackoverflow.com/questions/17365017)
  - Any whitespace between tags in HTML is collapsed into a single space character, which is why you have that gap.

## 0828

- [TypeScript `React.FC<Props>` confusion](https://stackoverflow.com/questions/59988667)
- React Function components can be written as normal functions that take a props argument and return a JSX element.
- `React.FC` why:
  - It provides an implicit definition of `children`  - however there are some issues with the implicit `children` type 
    - 👉🏻 React v18已移除children定义
    - [React 18 TypeScript children FC](https://stackoverflow.com/questions/71788254)
    - children prop was removed from `React.FunctionComponent (React.FC)` so you have to declare it explicitly.
    - children is a regular prop and is not something special. 
  - It provides typechecking and autocomplete for static properties like `displayName`,                                                                      `propTypes`, and `defaultProps`; 
    - However, there are currently known issues using defaultProps with `React.FunctionComponent`. 
  - It is explicit about the return type, while the normal function version is implicit

## 0826

- [k8s 1.20版本为什么不推荐docker？](https://www.zhihu.com/question/433124795/answer/2144110676)
  - Containerd 调用链更短，组件更少，占用节点资源也比较少。
- docker公司在云原生时代，已然成为打工仔，在容器领域的话语权已经被云计算厂商挤压
  - 对于桌面端，docker也有了可以竞争者，那就是redhat的podman，你可以alise podman=docker，docker有的基础功能podman都有
- [被k8s弃用的docker还值得学吗？](https://juejin.cn/post/7031472527725559816)
  - 首先抛出答案：Docker依然值得学习。
  - 为什么k8s会弃用Docker作为其容器运行时？ Docker在设计之初，并不是为了运行在k8s上的，它是一个功能完备的开发者工具，实际上k8s运行时依赖的是Docker中的containerd组件，即然如此把containerd单独拿出来就可以了，而不需要Docker额外的组件，虽然containerd被集成在Docker中，但是k8无法直接调用Docker中的containerd，而是需要通过一个叫Dockershim的组件，这个组件也是需要额外的开发维护成本的
  - 为什么用Docker打包的镜像依然可以在k8s上使用？ 我们在上面说到Docker的核心利用了存在已久的Namespace和Cgroup技术，这并不是Docker的创新，但镜像绝对是Docker的一项重要创新， Docker镜像解决了应用程序的分发问题，并制定了统一的镜像标准：opencontainers.org/ 所以依据此标准制作的镜像，都可以在k8s上使用。
- [Are networks now faster than disks?](https://serverfault.com/questions/238417)
  - 要考虑的因素过多，要具体情况具体分析
  - 机房内网通信比公网数据传输要快，公网还存在不稳定的问题
  - 固态硬盘+顺序读写 比机械硬盘/raid磁盘阵列随机读写要快
- I used to work on the following rule for speed
  - cache memory > memory > disk > network
- Sometimes yes, sometimes no. What network? What disk?

```text
L1 cache reference                             0.5 ns
Branch mispredict                              5 ns
L2 cache reference                             7 ns
Mutex lock/unlock                            100 ns (25)
Main memory reference                        100 ns
Compress 1K bytes with Zippy              10,000 ns (3,000)
Send 2K bytes over 1 Gbps network         20,000 ns
Read 1 MB sequentially from memory       250,000 ns
Round trip within same datacenter        500,000 ns
Disk seek                             10,000,000 ns
Read 1 MB sequentially from network   10,000,000 ns
Read 1 MB sequentially from disk      30,000,000 ns (20,000,000)
Send packet CA->Netherlands->CA      150,000,000 ns
```

- There are a lot of variables when it comes to network vs. disk, but in general, disk is faster.
  - if you are transporting over the network is going to or coming from disk anyway...so.......again, disk is faster

## 0824

- 基于hooks模仿redux的api
  - [State Management with React Hooks and Context API](https://devsmitra.medium.com/state-management-with-react-hooks-and-context-api-2968a5cf5c83)
  - [React doesn't need state management tool, I said](https://dev.to/tolgee_i18n/react-doesnt-need-state-management-tool-i-said-31l4)
    - https://github.com/tolgee/tolgee-platform/blob/main/webapp/src/fixtures/createProvider.tsx

## 0822

- lesson-luckiikawayii-js基础 - 数组、对象、函数
- 数组常用方法

```JS
arr1 = [11, 22, 33];
arr2 = new Array();
arr2.push(11, 22, 33)
```

- 对象理解
  - 内置对象
  - 创建可复用的对象不要使用构造函数 new FuncName 的形式

```JS
obj1 = { p1: 11, p2: 22 };
obj2 = new Object();
obj2.p1 = 11;
obj2.p2 = 22;

function createObj(name, age) {
  return {
    name: name,
    age: age
  }
}
```

- 函数理解
  - 函数里面不要用this，

```JS
function fn1(text) {
  console.log('; 打印', text);
  return text;
}
const fn2 = function(text) {
  console.log('; 打印', text);
  return text;
}
const fn3 = (text) => {
  console.log('; 打印', text);
  return text;
}
let sum = (a, b) => a + b;
// 等价于
let sum = function(a, b) {
  return a + b;
};
fn1('hello');
fn2('hello');
```

### [略微探究React StrictMode两次渲染的问题](https://juejin.cn/post/7009189602506309640)

- 👉🏻 严格模式下，组件mount时，effect逻辑会执行2次；通常state更新触发rerender会导致，render执行2次，effect还是只执行1次
  - mount时，就算useEffect第二个参数是`[]`，也会按照以下顺序执行，先执行2次render，再执行effect > effect-cleanup > effect
  - 可以通过useRef变量来控制effect的执行次数
- strict mode的开发模式下确实会渲染两次
  - 在App组件里面debugger之后也发现了确实是走了两遍的render阶段。
  - 为了验证App被调用了两次，很自然的想到了用console来验证
- 第二次渲染中console会经历修改和还原，这导致第二次渲染的console不会输出; 
  - Starting with React 17, React automatically modifies the console methods like `console.log()` to silence the logs in the second call to lifecycle functions.
  - Starting from React 18, React does not suppress any logs. 
    - However, if you have React DevTools installed, the logs from the second call will appear slightly dimmed. 
    - React DevTools also offers a setting (off by default) to suppress them completely.
  - Apparently, it doesn't do so when the console.log is called from Promise callback. But it does so when it is called from render. 
  - There is a second run of your render function when strict mode is enabled (only in development mode), but as discussed here, React will monkey patch console methods (calling disableLogs(); ) for the duration of that second (synchronous) run, so that it does not output.
  - In my opinion, this log-suppression is a really bad design choice
  - 如果把APP中的console换成alert，或者把原生的console引用起来使用，就应该能得到预期的结果
- intentionally double-invoking the following functions:
  - Class component constructor, render, and shouldComponentUpdate methods
  - Class component static getDerivedStateFromProps method
  - Function component bodies 👈🏻 函数体内render逻辑和effect逻辑都会执行2次
  - State updater functions (the first argument to `setState`)
  - Functions passed to useState, useMemo, or useReducer
- React 18 introduces a new development-only check to Strict Mode. 
  - This new check will automatically unmount and remount every component, whenever a component mounts for the first time, restoring the previous state on the second mount.
  - On the second mount, React will restore the state from the first mount.

### [React 18 - Avoiding Use Effect Getting Called Twice](https://dev.to/ag-grid/react-18-avoiding-use-effect-getting-called-twice-4i9e)

- This happens only in development mode not in production mode . So should we change the code to handle behaviour only for the development mode.

```typescript
/** 👀 只能用在挂载时只执行一次的场景，后续state变化参数里的effect逻辑也不会执行 */
export const useEffectOnce = (effect: () => void | (() => void)) => {
  const destroyFn = useRef<void | (() => void)>();
  const effectCalled = useRef(false);
  const renderAfterCalled = useRef(false);
  const [, setVal] = useState<number>(0);
  if (effectCalled.current) {
    renderAfterCalled.current = true;
  }
  useEffect(() => {
    // only execute the effect first time around
    if (!effectCalled.current) {
      destroyFn.current = effect();
      effectCalled.current = true;
    }
    // this forces one render after the effect is run
    // 执行完effect后，触发修改 renderAfterCalled
    setVal((val) => val + 1);
    return () => {
      // if the comp didn't render since the useEffect was called,
      // we know it's the dummy React cycle
      if (!renderAfterCalled.current) {
        return;
      }
      if (destroyFn.current) {
        destroyFn.current();
      }
    };
  }, []);
};
```

- [React 18, useEffect is getting called two times on mount](https://stackoverflow.com/questions/72238175)

## 0821

- log202011
  - 完全俩东西，streamlit是基于tornado的，应该拿flask和tornado比较。flask活的比tornado滋润
  - Streamlit does not support the WSGI protocol at this time, so deploying Streamlit with (for example) gunicorn is not currently possible.

## 0818

- RESTFul 架构下的两个缺点：
  - 在一个 RESTful 架构下，因为后端开发人员定义在各个 URL 的资源上返回的数据，而不是前端开发人员来提出数据需求，使得按需获取数据会非常困难。经常前端需要请求一个资源中所有的信息，即便只需要其中的一部分数据。这个问题被称之为过度获取（overfetching）。
  - 最恶劣的场景下，一个客户端应用不得不请求多个而不是一个资源，这通常会发起多个网络请求。这不仅会造成过度获取的问题，也会造成瀑布式的网络请求（waterfall network requests）。
- GraphQL最初就是为了解决上述两个问题设计的
  - GraphQL schema提供了一个所有可用数据检索的源头，通常会在服务端定义，客户端可以基于 schema 读取（query）和写入（mutation）数据
  - 但是呢，因为GraphQL获取数据是动态的，随机的，所以肯定会有人对数据的缓存提出较大的疑问

## 0815

- js基础 数据类型、运算符operator、表达式、流程控制
  - 新的数据类型，bigint
  - typeof
  - 流程控制：顺序、条件、循环
  - if使用场景，切换主题
    - https://codepen.io/uptonking/pen/xxWzYJq
  - 循环使用场景，批量生成html元素
    - https://codepen.io/uptonking/pen/LYdpPBW

## 0812

- dev-to
  - [x] search notion like block editor for recursive rendering
- 百度网盘倍速播放的扩展
  - global speed

## 0810

- [Redux DevTools 扩展的使用说明](https://juejin.cn/post/6998924455984496671)
  - [使用 redux-devtools-extension 查看 Redux 中状态变化](https://lufanfan.github.io/20190109/redux-devtools/)
  - `const store = createStore(reducer, composeWithDevTools());`

## 0807

- 视图公共的 addCard 的逻辑分析
  - createCard 创建一个业务层对象
  - mutator 执行持久化数据操作
- 👉🏻 action都被mutator和undoManager封装过了，需要进一步理清思路

## 0805

- [What is the difference between dpkg and aptitude/apt-get?](https://askubuntu.com/questions/309113)
- `dpkg -i packageName.deb` will only install this Deb package, and will notify you of any dependencies that need to be installed, 
  - but it will not install them, and 
  - it will not configure the packageName.deb because well...the dependencies are not there.
- `apt-get` is basically dpkg (I like to think of it as apt-get being a front-end for dpkg), but a clever one that will look for the dependencies and install them. 
  - It even looks at the currently installed dependencies and determines ones that are not being used by any other packages, and will inform you that you can remove them.
- `aptitude` then came along. It uses the libraries apt-get uses and actually has an interactive UI (user interface). 
  - aptitude will automatically remove eligible packages, while apt-get needs a separate command to do so. 
  - aptitude provides the functionality of dselect and apt-get as well as many additional features not found in either program.
# dev-07

## 0730

- replace mutator with reduxStore

## 0729

- [fedora flatpak.. sudo or not sudo?](https://forums.fedoraforum.org/showthread.php?327857-fedora-flatpak-sudo-or-not-sudo&p=1855999)
  - 无一致答案
  - It's not a "SAFER" thing! As I see it, it's rather about if you're installing for yourself, or for all users. If for yourself, then you won't need sudo.
  - 参考apt安装命令用了sudo

### [http请求方式： post put patch 总结](https://blog.csdn.net/qianxing111/article/details/79791499)

- idempotent 幂等的
  - 如果一个方法重复执行多次，产生的效果是一样的，那就是idempotent的；
  - idempotent的意思是如果相同的操作再執行第二遍第三遍，結果還是一樣。
  - “Methods can also have the property of ‘idempotence’ in that (aside from error or expiration issues) the side-effects of N > 0 identical requests is the same as for a single request.”
- POST方法不是幂等的，多次执行，将导致多条相同的用户被创建（users/1，users/2)
- PUT比較正確的定義是 Replace (Create or Update)，
  - 例如 PUT /items/1 的意思是替換 /items/1 ，如果已經存在就替換，沒有就新增；
  - 因此，PUT方法一般会用来更新一个已知资源，除非在创建前，你完全知道自己要创建的对象的URI
- PATCH方法是新引入的，是对PUT方法的补充，用来对已知资源进行局部更新
  - HTTP PATCH method require a feature to do partial resource modification.
  - The existing HTTP PUT method only allows a complete replacement of a document.

## 0728

- 对于多维表格，一般将数据更新的方法定义在所有视图渲染的上层
  - 添加 card/row 时，状态如何变化？
  - 调用同一个 addCard 方法，但不同视图下传入的参数不同

## 0727

- Cannot read properties of null (reading 'pickAlgorithm')
  - ~~npm cache clear --force~~
    - 多看一眼，异常上一行就是导致问题的依赖包名称
  - 解决方法应该是将 .npmrc 里面的自定义npm镜像源注释掉，然后重新 npm i

## 0726

- shop-iot-外接显示器
  - 对显示器不太了解，请教了一下大佬，跟我说直接买他的那款就行。于是我买了两台，一台在家一台在公司，直到昨天我才知道这个显示器除了可以 65W 反向充电外，还可以直接插 USB 连键盘鼠标，不用再在电脑上接转接线连了...
  - VX2780-4K-HDU 经济又便宜
  - [优派 VX2780-4K-HDU 27"UHD三边微边框IPS技术HDR400支持PD65W充电滤蓝光不闪屏HDMI/DP/TypeC显示器](https://www.viewsonic.com.cn/products/lcd/VX2780-4K-HDU.php)

## 0725

- innerText vs textContent
  - `innerText` is aware of things like `<br>` elements, and ignores hidden elements
  - `innerText` is aware of styling and won't return the text of "hidden" elements.
  - `textContent` gets the content of all elements, including `<script>` and `<style>` elements. In contrast,  `innerText` only shows "human-readable" elements.
- [Is it possible to calculate the Viewport Width (vw) without scrollbar?](https://stackoverflow.com/questions/33606565)
  - the viewport relative length units do not take scrollbars into account (and in fact, assume that they don't exist).
  - According to the [specs](https://drafts.csswg.org/css-values-3/#viewport-relative-lengths),  `vw` does take scrollbar width away UNLESS the overflow is on auto, then it works like "hidden" for the vw value. So if the page must overflow, set it to "scroll". With overflow-x & overflow-y you choose which scrollbar to display
- 100vw会在超长内容时出现水平滚动条的问题
  - 具体宽度需要实测，很多资料的信息是过时的
    - https://codepen.io/uptonking/pen/zYWdRLO
  - chrome-linux 
    - window.innerWidth  625
    - document.documentElement.clientWidth  610
    - 100vw.div.clientWidth  625
    - 给容器设置100vw时，若出现竖直滚动条，因为vw默认没考虑滚动条，此时总宽度是100vw+竖直滚动条宽度，就会导致出现水平滚动条
- [解决 100vw 下滚动条引发的问题](https://juejin.cn/post/6844904062702321672)
  - 通过js工具函数计算滚动条宽度
  - 解决100vw出现水平滚动条的问题
    - .container  { width: calc(100vw - var(--scrollbar)); }
  - 解决出现滚动条时右边距和上边距不相同的问题
    - right: calc(40px + var(--scrollbar));
- [深入浅出 Viewport 设计原理](https://www.cnblogs.com/onepixel/p/12144364.html)
- css 中写的 px 指的就是逻辑像素，而不是物理像素，一个逻辑像素可以代表一个或多个物理像素
- 简单来说：viewport 是屏幕背后的一张画布。
- 浏览器会先把页面内容绘制到画布上，然后再通过屏幕窗口呈现出来。
- 如果没有在 html 中加 viewport 的设置，画布其实也是存在的，浏览器会给画布设置一个默认宽度 ，不同平台的默认值
- width=device-width 就是把画布的宽度设置为可视窗口的宽度，让画布上的内容完全呈现出来。
- 在没有给页面设置 viewport 的情况下，当画布宽度大于可视窗口的时候，浏览器会自动对画布进行缩放，以适配可视窗口大小。这样页面在不滚动的情况下也能呈现全部内容。

### [Viewport concepts](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts)

- 小结
  - vw单位未考虑滚动条宽度，容易造成出现滚动条
  - 100vw  === innerWidth
  - layout viewport 是innerWidth/Height内区域
  - visual viewport是layout viewport去掉不可见部分，一般是 键盘
- [Visual Viewport API](https://developer.mozilla.org/en-US/docs/Web/API/Visual_Viewport_API)
  - The visual viewport is the visual portion of a screen excluding on-screen keyboards, areas outside of a pinch-zoom area, or any other on-screen artifact that doesn't scale with the dimensions of a page.
- What happens when a web page element needs to be visible on screen regardless of the visible portion of a web page? 
  - For example, what if you need a set of image controls to remain on screen regardless of the pinch zoom level of the device? Current browsers vary in how they handle this. 
  - The visual viewport lets web developers solve this by positioning elements relative to what's shown on screen.
- A viewport represents the area in computer graphics being currently viewed. 
  - In web browser terms, it is generally the same as the browser window, excluding the UI, menu bar, etc. 
  - That is the part of the document you are viewing.
- Your viewport is everything that is currently visible
  - The size of the viewport depends on the size of the screen, whether the browser is in fullscreen mode or not, and whether or not the user zoomed in. 
  - On larger monitors where applications aren't necessarily full screen, the viewport is the size of the browser window.
  - On most mobile devices and when the browser is in fullscreen mode, the viewport is the entire screen.
  - In fullscreen mode, the viewport is the device screen, the window is the browser window, which can be as big as the viewport or smaller, and the document is the website, which can be much taller or wider than the viewport.
  - To recap, the viewport is basically the part of the document that is currently visible.
- The width of the viewport is not always the width of the window.
  - The document element's `Element.clientWidth` is the inner width of a document in CSS pixels, including padding (but not borders, margins, or vertical scrollbars, if present). This is the viewport width. 不包含 border/margin/竖直滚动条宽度
  - The `Window.innerWidth` is the width, in CSS pixels, of the browser window viewport including, if rendered, the vertical scrollbar. 包含竖直滚动条宽度
  - The `Window.outerWidth` is the width of the outside of the browser window including all the window chrome.
- The web contains two viewports, the layout viewport and the visual viewport. 
  - The **area within the `innerHeight` and `innerWidth` is generally considered the layout viewport**. The browser chrome is not considered part of the viewport.
  - The visual viewport is the part of the web page that is currently visible in the browser and can change. When the user pinch-zooms(双指缩放) the page, pops open a dynamic keyboard, or when a previously hidden address bar becomes visible, the visual viewport shrinks but the layout viewport is unchanged.
- The visual viewport is the currently visible portion of the layout viewport. 
  - The **visual viewport** is the visual portion of a screen **not including** on-screen keyboards, areas outside of a pinch-zoom area, or other feature that doesn't scale with the dimensions of a page. 
  - The visual viewport is the same size as the layout viewport or smaller.
- Sticky headers or footers, as discussed above, stick to the top and bottom of the layout viewport, and therefore remain in view when we zoom in with the keyboard. 
  - If you pinch-zoom, the layout viewport may not be fully visible. 
  - If you magnify from the middle of the layout viewport, the content will expand in all four directions. 
  - If you have a sticky header or footer, they will still be stuck to the top or bottom of the layout viewport, but they may not be visible at the top and bottom of the device's screen — which is the visual viewport. 
  - The visual viewport is the currently visible portion of the layout viewport.
  - If you scroll down, you are changing the contents of the visual viewport and bringing the bottom of the layout viewport into view, displaying the sticky footer, which will then stay stuck at the bottom.
- 现代桌面浏览器有两种缩放操作。
  - 你在菜单栏上的缩放是改变像素大小（同时缩放layout viewport和visual viewport），
  - 用触摸板双指操作才是只缩放visual viewport。
  - （古代浏览器如IE还有另一种缩放，缩放字体大小，类似于改变rem的值）

## 0724

- [Does adding too many event listeners affect performance?](https://stackoverflow.com/questions/28627606)
  - dding additional event handlers to an element DOES decrease performance. 
  - Keep in mind that those tests are done with an empty function. When adding a real function that performs some additional tasks, the performance will slow down even further.
- [git error: failed to push some refs to remote](https://stackoverflow.com/questions/24114676)
  - 修改git仓库地址后，其他分支无法push
  - 简单的解决办法是直接重命名无法push的分支
  - git branch -m old-name new-name

## 0723

- 产品设计
  - 需求列表
  - 细分客户，定位准确

## 0722

- display: list-item 默认在内容前加上列表黑点
- display: inline 行内元素设置width/height默认无效，行内元素宽高默认由内容决定
  - flex item弹性项目默认都是 display: block，所以弹性容器内的span弹性项目设置width/height有效
- [`<span>` element refuses to go inline in flexbox](https://stackoverflow.com/questions/20363441)
  - by the flexbox spec -- children of a flex container are forced to have a block-flavored display type.
  - If you don't want this behavior, just wrap your `<span>` in a `<div>`, and then the `<div>` will play the role of the flex item so that the `<span>` can keep its display type.
- [css flex-item default height issue](https://stackoverflow.com/questions/47106934)
  - All items in a flex row will take the largest height of them by default.
  - After calling container as display:flex, may i consider all its contained items will behave like inline-block elements?

### [python 字符串转列表出现\ufeff的解决方法](https://www.cnblogs.com/mjiang2017/p/8431977.html)

- 在Windows下用文本编辑器创建的文本文件，如果选择以UTF-8等Unicode格式保存，会在文件头（第一个字符）加入一个BOM标识。
  - BOM = Byte Order Mark
  - BOM是Unicode规范中推荐的标记字节顺序的方法。比如说对于UTF-16，如果接收者收到的BOM是FEFF，表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little-Endian的。
  - UTF-8不需要BOM来表明字节顺序，但可以用BOM来表明“我是UTF-8编码”。BOM的UTF-8编码是EF BB BF（用UltraEdit打开文本、切换到16进制可以看到）。所以如果接收者收到以EF BB BF开头的字节流，就知道这是UTF-8编码了。
- [Python 读取文件首行多了"\ufeff"字符串](https://blog.csdn.net/chenmozhe22/article/details/89472790)
- [json字符串头部出现非法字符“\ufeff”的问题处理](https://segmentfault.com/a/1190000010292346)
  - 今天在处理将数组转为json 字符串后，然后获取到解析时，出现解析的json字符串为空的现象，首先看了下，我的json转换脚本之前没有任何输出，但还是出现json转化乱码，后来查了下，原来是脚本编码格式的问题。
  - 其实解决方法很简单，就是涉及json转换的脚本文件的UTF-8格式编码 改成 UTF-8无BOM格式编码即可。

### [什么零宽度字符，以及零宽度字符在JavaScript中的应用](https://juejin.cn/post/6844904164057677831)

- 一种不可打印的Unicode字符, 在浏览器等环境不可见, 但是真是存在, 获取字符串长度时也会占位置, 表示某一种控制功能的字符.
- 常见的零宽字符有哪些
- 零宽空格（zero-width space, ZWSP）用于可能需要换行处。
  - Unicode: U+200B  HTML: &#8203; 
- 零宽不连字 (zero-width non-joiner，ZWNJ)放在电子文本的两个字符之间，抑制本来会发生的连字，而是以这两个字符原本的字形来绘制。
  - Unicode: U+200C  HTML: &#8204; 
- 零宽连字（zero-width joiner，ZWJ）是一个控制字符，放在某些需要复杂排版语言（如阿拉伯语、印地语）的两个字符之间，使得这两个本不会发生连字的字符产生了连字效果。
  - Unicode: U+200D  HTML: &#8205; 
- 左至右符号（Left-to-right mark，LRM）是一种控制字符，用于计算机的双向文稿排版中。
  - Unicode: U+200E  HTML: &lrm; &#x200E; 或&#8206; 
- 右至左符号（Right-to-left mark，RLM）是一种控制字符，用于计算机的双向文稿排版中。
  - Unicode: U+200F  HTML: &rlm; &#x200F; 或&#8207; 
- 字节顺序标记（byte-order mark，BOM）常被用来当做标示文件是以UTF-8、UTF-16或UTF-32编码的标记。
  - Unicode: U+FEFF
- 零宽度字符在JavaScript的应用
- 数据防爬
  - 将零宽度字符插入文本中, 干扰关键字匹配。
  - 爬虫得到的带有零宽度字符的数据会影响他们的分析，但不会影响用户的阅读数据。
- 信息传递
  - 将自定义组合的零宽度字符插入文本中，用户复制后会携带不可见信息，达到传递作用。
- 使用零宽度字符加密解密
  - 信息加密解密的思路是, 把字符串转成二进制0和1, 并用空格把字符隔开, 然后用三种零宽表示0、1、空格, 然后用第四种零宽字符拼起来; 解密反向操作即可.
- excel表格 中经常出现零宽字符 \u202c \u202d, 上传后解析或复制到 input 就会有问题, 
  - 在 excel表格 中获取到的数据一般需要先过滤.

## 0721

### [How to use throttle or debounce with React Hook?](https://stackoverflow.com/questions/54666401)

- After some time passed I'm sure it's much easier to handle things by your own with setTimeout/clearTimeout(and moving that into separate custom hook) than working with functional helpers.

```JS
const App = () => {
  const [value, setValue] = useState(0)
  const throttled = useRef(throttle((newValue) => console.log(newValue), 1000))
  useEffect(() => throttled.current(value), [value])
  return (
    <button onClick={() => setValue(value + 1)}>{value}</button>
  )
}
// It may work too
const throttled = useCallback(throttle(newValue => console.log(newValue), 1000), []);
```

### [How to autosave small changes to big settings file without lag?](https://stackoverflow.com/questions/41232606)

- Provided that you want to keep the model with a multi-MB settings file, the most reasonable solution would be to use **atomic writes** to avoid the problem of the app being quit in the middle of a save.
- Assuming your file is called `settings.json`, atomic writes would work something like this:
  - App decides to update settings, starts writing to a temporary file (to avoid overwriting the existing file halfway), say `settings.json.tmp-1482198169` (1482198169 being current unix timestamp).
  - Once writing to `settings.json.tmp-1482198169` is complete, copy the current `settings.json` to `settings.json.bak`.
  - Rename `settings.json.tmp-1482198169` to `settings.json`, overwriting the old one.
- The basic idea is to construct a process where you always have a valid copy of `settings.json`, so it's only replaced with a complete copy.
- npm has a number of implementations of this, like this one. I'd recommend you try one of those instead of writing your own, since any bugs in the implementation of the atomic write dance could cause you data loss, and it's tricky to get everything right when dealing with asynchronous code.
  - https://github.com/npm/write-file-atomic
  - Write files in an atomic fashion w/configurable ownership
  - This is an extension for node's fs.writeFile that makes its operation atomic and allows you set ownership (uid/gid of the file).

### [Is any solution to do localstorage setItem in asynchronous way](https://stackoverflow.com/questions/42921220)

```JS
const asyncLocalStorage = {
  setItem: function(key, value) {
    return Promise.resolve().then(function() {
      localStorage.setItem(key, value);
    });
  },
  getItem: function(key) {
    return Promise.resolve().then(function() {
      return localStorage.getItem(key);
    });
  }
};
const asyncLocalStorage2 = {
  setItem: async function(key, value) {
    await null;
    return localStorage.setItem(key, value);
  },
  getItem: async function(key) {
    await null;
    return localStorage.getItem(key);
  }
};
```
