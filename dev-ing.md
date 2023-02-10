---
title: dev-ing
tags: [dev]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# dev-2023
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发

金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-xp
- ui-starter
  - css-only: open-props, glass-ui, nextui, 渐变字体
  - react: spectrum, zigzag, ariakit
- dev-starter
  - patterns: react, typescript
- list-grid-starter
  - plain
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
- 产品日历组件
  - headless-date-picker
- module/fwk/server
  - 灵活的tag/bookmark系统
  - cms, tables, bi
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

```shell
DEBUG=* npm install --legacy-peer-deps --loglevel silly
```

# dev-review
- dev-goals
  - rich-editor: text/code/block
  - pivot-table
  - collaboration
  - local-first-database
  - annotation/comment/whiteboard/pdf
  - 事项--截止日期(0730+休整)--重要性(hml/s1-s3)
  - *mirror-based-editor-vanillajs
  - pivot-table/grid--0828--h
    - dropdown-menu vs tabs
  - app-wiki-knowledge-base--0904
  - dashboard/webapp-template--0901

- dev-to/log/xp
  - deep into lib: src-code, issues, pr, forks, extensions/alternatives

- later
  - crdt-hlc 
    - merkle 如何在op-log中找到上次相等的timestamp
  - idb-side-sync
    - storage adapter: indexeddb/memory/sqlite-opfs
    - 系统预置数据如待办类型合并时可能出现名称相同的情况，用户添加数据时也可能出现
  - url-as-state-management
  - docker打包前端
# dev-2023-方向+方法+时间
- eg-prosemirror-examples+collab
  - 重写collab示例的交互，参考blocky-editor在一个页面展示多个编辑器且支持实时协作
  - [x] 用websocket替换轮询，可基于socket.io
  - 参考atlaskit-editor实现collab，服务端未开源，但yjs提供了示例，支持切换docs
  - 分析协作时官方的undo-redo和yjs的undo-redo
- eg-tiptap-examples
  - 重写atlaskit或ckeditor的丰富示例
  - tiptap-yjs-server-src
- eg-migrate-atlaskit-examples
- eg-BlockNote
- eg-focalboard
  - olap-cube-js
- 👉🏻 eg-tanstack-table-v8
  - tuple-database
  - [x] 数据全内存: nedb, blinkdb
  - [x] 数据全持久: linvodb, tingodb
  - [ ] 方便接入已有的外部数据源

- collab-sync
  - ddp/ejson/minimongo
  - collab-data-structure: lww-with-hlc
  - undo/redo
  - remoteStorage: google-drive、网盘、七牛对象存储
  - lo-fi-sync-server

- sqlite-web
  - evolu
  - kikko
  - absurd-sql-ts: read ArrayBuffer

- products
  - airtable, cms, lowcode

- 内容的存储与更新如何与数据库集成
  - 编辑器内容自动保存一般通过在onChange方法中执行saveToDB
    - ❌ 也可以在onChange方法中创建内存db、更新索引，通过索引提高计算效率； 应该避免维护2份数据
  - 将编辑器的计算密集部分的数据模型不使用普通json对象，而用类似数据库模型的设计

- log2022 数据同步、冲突处理、本地存储
  - 07-focalboard-views
  - 08-block-editor-tiny-write
  - 09-prosemirror-examples
  - 10-prosemirror-collab - otjs - crdt
  - 11-idb-sync
  - 12-nedb-linvodb
- log2023
  - 01-linvo-search+sync-hlc-wip

- dev-to
  - crdt tutorials
  - 腰包掉到床头版与墙的夹缝中了
# dev-02

## 0208

- [Wechaty 实现微信机器人的原理 - 知乎](https://zhuanlan.zhihu.com/p/567250559)

- [各类期刊的区别 | J. Xu](https://xujinzh.github.io/2020/10/09/journal-or-transactions/)
  - Journal学报最典型的叫法， 刊登关于某特殊主题的文章的期刊。要求有很大的创新点，比较详细的公式推导。因 Journal 面向的读者较广泛，因此发表在其上的文章需要对背景知识有更加全面的介绍。
  - Transactions 本意为商业交易和谈判，引申为公开发表的大会记录。后来有汇刊的意思。 其具体到一个相对较细的专业方向上，发表在 transactions 上的文章需要有很大的创新和详细的公式推导。
  - Proceedings 表示某行动，或行动过程或方式，引申意之一是学术团体或其他正规团体会议所讨论问题的记录，进一步有会议论文集的意思。有会刊、记录、会议录的意思。但是 IEEE 的 Proceedings 也变成了期刊 (出版周期相对长)，并没有会议支撑。

## 0210

- [rg process taking up all my CPU 100% · Issue #98594 · microsoft/vscode](https://github.com/microsoft/vscode/issues/98594)
  - `"search.followSymlinks": false` solved my issue too

## 0205

- npm ERR! Invalid comparator: github:thecodrr/htmlparser2
  - [[BUG] \`overrides\` in \`package.json\` do not allow file paths of any kind (including fake ones) · Issue #5843 · npm/cli](https://github.com/npm/cli/issues/5843)
  - I really hope this can be fixed. Overrides otherwise only fully work in npm v8.
  - npm v9 最新版已修复
# dev-01

## 0126

- SyntaxError: Named export 'WebSocketServer' not found. The requested module 'ws' is a CommonJS module, which may not support all module.exports as named exports.
  - 原因是 ws 不在dependencies列表里

- ### [Why is there no same-origin policy for WebSockets? Why can I connect to ws://localhost? - Stack Overflow](https://stackoverflow.com/questions/23674199)
- WebSockets can cross domain communication, and they are not limited by the SOP (Same Origin Policy).
- The same security issue you described can happen without WebSockets.
- The evil JS can:
  - Create a script/image tag with a URL to evil.tld and put data in the query string.
  - Create a form tag, put the data in the fields, and invoke the "submit" action of the form, doing an HTTP POST, that can be cross domain. AJAX is limited by the SOP, but normal HTTP POST is not. Check the XSRF web security issue.
- If something injects javascript in your page, or you get malicious javascript, your security is already broken.

- SOP/CORS does not apply to WebSocket, but browsers will send an `origin` header that contains the hostname of the server that served the HTML with the JS that opened the WebSocket connection. A WebSocket server can then restrict access by checking `origin`.

## 0123

- [node.js - Difference between process.nextTick and queueMicrotask - Stack Overflow](https://stackoverflow.com/questions/55467033/difference-between-process-nexttick-and-queuemicrotask)
  - It is the same, in the way of both of them are to execute a task just after the execution of the current function or script.
  - They have different queues. The nextTick's queue is managed by node and the microtask one is managed by v8.
  - The nextTick queue is checked first after the current function/script execution, and then the microTask one.
  - There is no performance gain, the difference is that the nextTick queue will be checked first after the function/script execution 

## 0119

- 💡 a global event emitter (could be replaced by redis, etc)

## 0121

- Downloading ripgrep failed: TypeError [ERR_INVALID_PROTOCOL]: Protocol "https:" not supported. Expected "http:"
  - https://github.com/microsoft/vscode-ripgrep/issues/26#issuecomment-1187663914

```
1. Clone ripgrep locally: git clone git@github.com:microsoft/vscode-ripgrep ~/vscode-ripgrep
2. run yarn in that folder (this seems to work even behind proxy)
3. cp bin/rg ~/vscode-repo-path/node_modules/@vscode/ripgrep
4. run yarn in your vscode repo path again
```

## 0118

### [既然有 HTTP 请求，为什么还要用 RPC 调用？ - 知乎](https://www.zhihu.com/question/41609070)

- rpc是远端过程调用，其调用协议通常包含传输协议和序列化协议。
  - 传输协议包含: 如著名的 [gRPC](grpc / grpc.io) 使用的 http2 协议，也有如dubbo一类的自定义报文的tcp协议。
  - 序列化协议包含: 如基于文本编码的 xml json，也有二进制编码的 protobuf hessian等
- 为什么要使用自定义 tcp 协议的 rpc 做后端进程通信？
  - 要解决这个问题就应该搞清楚 http 使用的 tcp 协议，和我们自定义的 tcp 协议在报文上的区别。
  - 首先要否认一点 http 协议相较于自定义tcp报文协议，增加的开销在于连接的建立与断开。http协议是支持连接池复用的，也就是建立一定数量的连接不断开，并不会频繁的创建和销毁连接。
  - 二要说的是http也可以使用protobuf这种二进制编码协议对内容进行编码，因此二者最大的区别还是在传输协议上。
- 通用定义的http1.1协议的tcp报文包含太多废信息，
  - 即使编码协议也就是body是使用二进制编码协议，报文元数据也就是header头的键值对却用了文本编码，非常占字节数。

- 所谓的效率优势是针对http1.1协议来讲的，http2.0协议已经优化编码效率问题，像grpc这种rpc库使用的就是http2.0协议。这么来说吧http容器的性能测试单位通常是kqps，自定义tpc协议则通常是以10kqps到100kqps为基准
- 简单来说成熟的rpc库相对http容器，更多的是封装了“服务发现”，"负载均衡"，“熔断降级”一类面向服务的高级特性。可以这么理解，rpc框架是面向服务的更高级的封装。如果把一个http servlet容器上封装一层服务发现和函数代理调用，那它就已经可以做一个rpc框架了。

- 用rpc和http跟业务需求有关系，其实rpc可以用http协议实现

## 0116

- 加减乘除表示运算：plus minus multiply divide
- 和差积商表示运算结果：sum difference product quotient

```JS
new Date('1970-01-01T00:00:00').getTime() // local时间， -280000

new Date('1970-01-01').getTime() // 0
```

- ⭐️ new Date().getTime() 总是13位

- [Deterministic length of JS new Date().getTime() string in the modern era: Unix Epoch Time - Stack Overflow](https://stackoverflow.com/questions/69995741/deterministic-length-of-js-new-date-gettime-string-in-the-modern-era-unix-e)
  - The timestamp is milliseconds since 1970-01-01 00:00:00 UTC (the same as the Unix epoch).
  - if it overflows to 14 digits, the , which is 8, 362, 906, 319, 000
  - 10000000000000/1000/3600/24/365 = 317 年

- [encryption - Hashing a string to a specific length - Stack Overflow](https://stackoverflow.com/questions/45221412/hashing-a-string-to-a-specific-length)
  - Non-cryptographic hashes usually have a wider range of sizes available. For a non-crypto hash I often suggest the FNV hash, which is easy to implement and offers a wide range of output sizes: 32 bits to 1024 bits.
  - 自定义编码解码即可，无需加密

## 0115

- [Typescript generic type parameters: `T` vs `T extends {}` - Stack Overflow](https://stackoverflow.com/questions/61648189/typescript-generic-type-parameters-t-vs-t-extends)
  - in TypeScript 3.5 a change was made so that generic type parameters are implicitly constrained by `unknown` instead of the empty object type `{}`
  - If you don't explicitly constrain a generic type parameter via `extends XXX`, then it will implicitly be constrained by `unknown`, the "top type" to which all types are assignable. So in practice that means the `T in funcA<T>()` could be absolutely any type you want.
  - the empty object type `{}`, is a type to which nearly all types are assignable, except for `null` and `undefined`. Even primitive types like string and number are assignable to {}.

## 0113

### [深入理解Vite核心原理 - 知乎](https://zhuanlan.zhihu.com/p/467325485)

- Vite主要利用浏览器ESM特性导入组织代码，在服务器端按需编译返回，完全跳过了打包这个概念，服务器随起随用。
  - 快速的冷启动: No Bundle + esbuild 预构建
  - 真正的按需加载: 利用浏览器ESM支持，实现真正的按需加载
- Vite相比于Webpack而言，没有打包的过程，而是直接启动了一个开发服务器devServer。
  - Vite劫持浏览器的HTTP请求，在后端进行相应的处理将项目中使用的文件通过简单的分解与整合，然后再返回给浏览器(整个过程没有对文件进行打包编译)。所以编译速度很快。
- Snowpack 首次提出利用浏览器原生ESM能力的打包工具，其理念就是减少或避免整个bundle的打包。默认在 dev 和 production 环境都使用 unbundle 的方式来部署应用。但是它的构建时却是交给用户自己选择，整体的打包体验显得有点支离破碎。

- ESM提供了更原生以及更动态的模块加载方案，最重要的就是它是浏览器原生支持的
  - 👉🏻 我们可以直接在浏览器中去执行import，动态引入我们需要的模块，而不是把所有模块打包在一起。
- ESM的执行可以分为三个步骤：
  - 构建: 确定从哪里下载该模块文件、下载并将所有的文件解析为模块记录
  - 实例化: 将模块记录转换为一个模块实例，为所有的模块分配内存空间，依照导出、导入语句把模块指向对应的内存地址。
  - 运行：运行代码，将内存空间填充
- 从上面实例化的过程可以看出，ESM使用实时绑定的模式，导出和导入的模块都指向相同的内存地址，也就是值引用。而CJS采用的是值拷贝，即所有导出值都是拷贝值。

- vite核心原理
  - 当声明一个 script标签类型为 module 时,                             `<script type="module" src="/src/main.js"></script>`; 
  - 当浏览器解析资源时，会往当前域名发起一个GET请求main.js文件
  - 请求到了main.js文件，会检测到内部含有import引入的包，又会import 引用发起HTTP请求获取模块的内容文件，如App.vue、vue文件
- Vite其核心原理是利用浏览器现在已经支持ES6的import, 碰见import就会发送一个HTTP请求去加载文件，
  - Vite启动一个 koa 服务器拦截这些请求，并在后端进行相应的处理将项目中使用的文件通过简单的分解与整合，然后再以ESM格式返回返回给浏览器。
  - Vite整个过程中没有对文件进行打包编译，做到了真正的按需加载，所以其运行速度比原始的webpack开发编译速度快出许多！

- 在Vite出来之前，传统的打包工具如Webpack是先解析依赖、打包构建再启动开发服务器，Dev Server 必须等待所有模块构建完成，当我们修改了 bundle模块中的一个子模块， 整个 bundle 文件都会重新打包然后输出。项目应用越大，启动时间越长。

- 而Vite利用浏览器对ESM的支持，当 import 模块时，浏览器就会下载被导入的模块。先启动开发服务器，当代码执行到模块加载时再请求对应模块的文件, 本质上实现了动态加载。灰色部分是暂时没有用到的路由，所有这部分不会参与构建过程。随着项目里的应用越来越多，增加route，也不会影响其构建速度。

- 目前所有的打包工具实现热更新的思路都大同小异：主要是通过WebSocket创建浏览器和服务器的通信监听文件的改变，当文件被修改时，服务端发送消息通知客户端修改相应的代码，客户端对应不同的文件进行不同的操作的更新。

- 基于esbuild的依赖预编译优化，为什么需要预构建？
  - 支持commonJS依赖，将commonJs的文件提前处理，转化成 ESM 模块并缓存入
  - 减少模块和请求数量
  - Vite预编译之后，将文件缓存在node_modules/.vite/文件夹下。

## 0111

- [--es-module-specifier-resolution=node not working from v13.0.1 · Issue #30520 · nodejs/node](https://github.com/nodejs/node/issues/30520)
  - we have renamed the flag, but we continue to support `--es-module-specifier-resolution=node` which silently aliases to `--experimental-specifier-resolution`

## 0109

- [Feature: Documenting Promises · Issue · jsdoc/jsdoc](https://github.com/jsdoc/jsdoc/issues/509)
  - jsdoc对promise，暂不支持

- [Summary of `process.env.NODE_ENV` and its use with Webpack by markerikson(redux)](https://gist.github.com/markerikson/6776848172c33aaa4db882627c689e18)

- [Can I mark code blocks as production or development only with webpack? - Stack Overflow](https://stackoverflow.com/questions/50997670/can-i-mark-code-blocks-as-production-or-development-only-with-webpack)
  - emphasize again: The code really disappears if the condition is not met. Only an empty if statement appears on the output. 

```JS
var environment = process.env.NODE_ENV || 'development';

if (process.env.NODE_ENV === 'production') {
  // Code will only appear in production build.
}

if (process.env.NODE_ENV !== 'production') {
  // Code will be removed from production build.
  console.log("Looks like you're a developer.");
}

// process.env is a reference to your environment, so you have to set the variable.
// on windows:
SET NODE_ENV = development
// on macOS / OS X or Linux:
export NODE_ENV = development
// cross-env NODE_ENV=development node server.js
```

## 0112

- [exports is not defined in ES module scope - Stack Overflow](https://stackoverflow.com/questions/71478604/exports-is-not-defined-in-es-module-scope)
  - 使用ts-node执行ts却忘了拷贝 tsconfig.json

## 0108

- 测试mocha时，不能稳定复现 Database is not open/closed
  - db.clear: Delete all entries or a range. Not guaranteed to be atomic. 
  - 解决方法不是写多遍，而是使用 `try-catch`

```JS
// ❌
await d.store.close();
await d.store.close();

// ✅
try {
  await d.store.close();
} catch (e) {
  await d.store.close();
}
```

## 0107

- mocha的异步测试异常
  - Error: Timeout of 2000ms exceeded. For async tests and hooks, ensure "done()" is called; if returning a Promise, ensure it resolves.
  - 对于async的callback方法cb1，若cb1内部有await，可尝试在await后expect断言前使用`setTimeout(done, 50)`，让done方法异步被执行

- [Correct way to use done() while testing asyc/await with mocha - Stack Overflow](https://stackoverflow.com/questions/52449202/correct-way-to-use-done-while-testing-asyc-await-with-mocha)
  - The correct way is to not use `done` with `async..await`. 
  - Mocha supports promises and is able to chain a promise that is returned from `it`, etc. functions.
  - `done` is needed only for testing asynchronous APIs than don't involve promises. Even then, converting to promises often results in cleaner control flow.

```JS
it('Testing insertDocumentWithIndex', async () => {
  var data = await db.insertDocumentWithIndex('inspections', {
    "inspectorId": 1,
    "curStatus": 1,
    "lastUpdatedTS": 1535222623216,
    "entryTS": 1535222623216,
    "venueTypeId": 1,
    "location": [
      45.5891279,
      -45.0446183
    ]
  })
  expect(data.result.n).to.equal(1);
  expect(data.result.ok).to.equal(1);
})
```

- [Describe block with async function behaving weirdly · mochajs/mocha](https://github.com/mochajs/mocha/issues/2975)
  - Mocha's describe blocks do not support (as in waiting for resolution of) returned promises. 

## 0105

- [Import '.json' extension in ES6 Node.js throws an error](https://stackoverflow.com/questions/60205891/import-json-extension-in-es6-node-js-throws-an-error)
- `node --experimental-json-modules ./your-file.js`

```JS
import packageFile from "../../package.json"
assert { type: "json" };

const {
  name,
  version
} = packageFile;

// The dynamic import version looks like this:

const {
  default: {
    name,
    version
  }
} = await import("../../package.json", {
  assert: {
    type: "json"
  }
});
```

- [ShopifyQL Notebooks · Shopify Help Center](https://help.shopify.com/en/manual/reports-and-analytics/shopifyql-notebooks)
  - ShopifyQL Notebooks is an app that enables you to query, explore, and visualize your business’ data.

## 0104

- Each time you're introducing a Boolean field in a Database schema, use a timestamp instead. Future You will thank you. 

```JS
isPublished = true;
if (isPublished) console.log(';; true');

isPublished = new Date();
if (isPublished) console.log(';; true');
```
