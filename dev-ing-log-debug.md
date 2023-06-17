---
title: dev-ing-log-debug
tags: [debug, dev, xp]
created: 2021-04-28T20:54:34.301Z
modified: 2023-06-14T00:53:15.226Z
---

# dev-ing-log-debug

# dev-2023

# issues

## 

## 

## 

## watarble-snabbdom渲染细节

- 首次渲染需要 vnode的顶层节点 与 已存在的domNode 匹配，所以一般要先创建domNode或修改vnode顶层节点的选择器

- useReactTable的实现，每次执行改hook时，会执行setOptions更新table实例的配置
  - 自己封装时，也要在createTable后立即setOptions

## vscode里面调试mocha测试的命令调了很久

- 先在控制台调通，再修改launch.json

- 原因是 --experimental-loader 误写成了 --loader

## 更新logux后ts-node server无法运行

> Error: Debug Failure. False expression: Output generation failed

- 不要一次性更新全部包再检查能否运行
  - 在能正常运行时，逐个替换，逐个检查，便能轻松发送问题
  - 一次性全替换后，bug不知从哪个包开始查

- 尝试ts-node的替代品tsm，也能够解决问题

- 调试时复现问题，问题出在 `export * from './index.d';`，注释即可
  - index.d.ts文件中包含部分函数声明

## webpack circular dependencies 打包失败

- 尝试借助 dpdm/circular-plugin 分析问题deps并解决
- 尝试借助eslint自动添加import type

- 解决方法是将@babel/preset-typescript的 `onlyRemoveTypeImports`保持默认值false

- [@babel/plugin-transform-typescript · Babel](https://babeljs.io/docs/babel-plugin-transform-typescript)
  - `onlyRemoveTypeImports: true` is equivalent to `importsNotUsedAsValues: preserve`, while `onlyRemoveTypeImports: false` is equivalent to `importsNotUsedAsValues: remove`. 

- 变通方法是，tsc支持build含有循环依赖的源码
  - 但verbatimModuleSyntax不能为true，否则运行会异常

## 刷新页面自动登录用户帐号

- 需求
  - 登录时，/login(添加token) > /userMe > /data
  - 刷新时，/userMe > /data

- 每次刷新会请求类似`/userMe`的接口
  - 但在注册登录页不会请求，注册登录页在userMe的children中，
  - 若已登录，会自动跳转数据页
  - 若未登录，则无token，也不会发起useMe

## fetch的response在await后仍然是promise，调试了很久

- [Why fetch returns promise pending? - Stack Overflow](https://stackoverflow.com/questions/59394620/why-fetch-returns-promise-pending)

- `res.json()` is a promise too

- 自定义fetch和rtk-query的fetch执行顺序难以确定
  - 就算使用redux支持的自定义query，顺序仍然难确定
  - 从devtools里面的actions顺序分析

## cors问题

- [ajax - CORS: Cannot use wildcard in Access-Control-Allow-Origin when credentials flag is true - Stack Overflow](https://stackoverflow.com/questions/19743396/cors-cannot-use-wildcard-in-access-control-allow-origin-when-credentials-flag-i)

- 原因是server代码需要rebuild，因为执行的是 node dist/server.js，而不是src/server.ts

## tanstack-virtual+query的无限滚动只能滚动一页

- 对照原示例跑了很多次，没发现代码上的问题，反而在css-in-js上花费过多时间
- 原因是使用vscode的自动补全依赖，将useEffect依赖中的`rowVirtualizer.getVirtualItems()`自动改成了`rowVirtualizer`; 
  - 修改自己或别人的依赖时一定要注意
  - ide或lint的auto fix慎用，出问题也要往这方面排查

## virtual-list在devtools中width或height为0，导致元素不显示_202305

- flex-item 的 flex-basis 默认auto，宽度由item自身width/height决定
  - 而flex-item内的div宽度为width:100%时，相对于item自身width
  - 两处计算有点依赖和冲突，所以item自身with在devtools中显示为0

- 虚拟列表容器为position-relative，列表项为position-absolute
  - position-absolute会脱离文档流，不会填充父容器宽高
  - 需要手动设置父容器宽高
  - 一旦设置容器宽高，flex-item的宽高可以确定

## slate的link元素使用floating-ui无法显示弹出框的原因_202203

- 一直在floating-ui源码的useFloating/useHover排查，方向错误
- 原因是slate元素渲染时`{...attributes}`的属性attributes.ref.current=null，而floating-ui需要的 `ref={refs.setReference}`
  - 注意传递props的书写顺序

## 在slate中文输入法的问题定位花费过多时间

- slate的Editable组件存在会在model数据更新前渲染的问题
  - 在onCompositionStart中setIsComposing导致渲染
  - 在onCompositionEnd中setIsComposing导致渲染，此时slate的model未更新其他组件不会更新，但渲染时renderElements却能拿到最新输入值，就导致了异常

- 可以在应用层的其他组件手动遍历model数据计算来获取最新值
  - 但这可能导致应用层存在过多重复计算，因为其他组件从context获取的editor更新时又会计算一遍

## 在搜索crdt rga上花费了过多时间

- 对于问题比较明确和具体的场景，可直接在github搜code，而不是搜repository

## mongoose modelInstance.save无法保存数据

- 其实数据已经保存了，但使用的是自动创建的表名
- 刷新compass，reload data

- 检查mongoose和mongodb的兼容性

## ts重构场景，Namespace N1名和type名相同

> 需求，既需要T1.m1()工具方法，又需要类型T1

- 方法1: 若将Namespace改为 export const N1 = ，则会 
  - 'Op' refers to a value, but is being used as a type here. Did you mean 'typeof Op'?

- 方法2: 若将Namespace去掉namepace，重命名为N1Utils，则api会变化

- ✅ 方法3: 若将Namespace改为 static class
  - 仍存在问题，静态方法名无法使用js内置名称
  - I don't think the properties name, caller and length are doable. They are read-only properties and can't be overridden. All assignments to them will be ignored.

## sequelize-rest-api调试很久，fetch api在浏览器控制台的返回异常

```
violates the following Content Security Policy directive: "connect-src 'self' 
```

- 跨域问题调试的基础就错了，应该在新标签页打开http://localhost:3000/api/courses然后在此标签页的控制台发送请求
  - 不要在其他域名标签页的控制台调试

## 测试mocha时，不能稳定复现 Database is not open

- 测试时要以terminal信息为准，测试面板可能会隐藏部分冲突提示
  - 表面通过测试，但terminal会提示id冲突

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

## yjs的源码，各子文件夹都使用import顶层./internals文件中的导出，极易导致循环依赖

- 很难解决循环依赖问题，耗费时间过多，对A文件import B, B文件又import A，解决需要资源过多
  - 临时方案是直接使用npm打包分发的.mjs文件，可能会丢失注释

- 可借助webpack circular-dependency-plugin插件尽早发现和解决问题

- 手动补充ts类型有时就是方向错了不该做，工具根据jsdoc自动打包出来的类型定义比手写的更好

## ide总是添加过多的分号 semicolon

- 排查的方向一开始就错了，不是eslint造成的
  - 因为关闭ide后执行eslint fix 是通过的，这也可作为一种变通方案
- 确定原因是prettier
# webpack: ReferenceError: Cannot access x before initialization
- 临时方案，禁用webpack hmr热加载
  - 使用插件提前检查并处理 https://github.com/aackerman/circular-dependency-plugin

- https://github.com/pmmmwh/react-refresh-webpack-plugin/issues/190

- To be clear, this is not a problem that only exists on our side - it is a limitation of HMR of Webpack (or potentially any other bundlers that creates a module graph). When a graph needs to be created and there exists cyclic references, the order of which node is created first can be nondeterministic, which means while your app could work in production, it will not work in development with HMR enabled.

## npm idealTree 很慢 

```shell
DEBUG=* npm install --legacy-peer-deps --loglevel silly
```

```shell
--noproxy 127.0.0.1:8889
--noproxy registry.npmmirror.com
```

## prosemirror官方示例，footnote弹框打开后，其中所有文本出现浏览器默认选区蓝色背景色

- 首先分析父编辑器而不是子编辑器选区范围，确实存在
- 发现是设置弹框内`::selection`的css规则未生效

- 结果是由于以前调整prosemirror的源码不细心导致，Selection的默认visible是true，但NodeSelection的默认visible是false

## prosemirror官方示例，图片上传完成后，点击图片会很卡，但点击编辑器其他位置文字时光标正常

> 官网线上却无此问题

- 在实现上传图片demo时，发现图片上传完成后，从点击图片到点击的图片出现蓝框即选中状态，耗时很长，体验很卡
  - 通过浏览器perf面板分析调用栈定位到问题
  - mouseup > selectClickedLeaf > updateSelection > dispatch > appendNewHistoryEntry(来自prosemirror-dev-toolkit)
  - `appendNewHistoryEntry`并不来自prosemirror源码，而是开发者工具引入的，这也解释了官网案例不卡的原因

## 排查webpack一直热更新的问题花了很多时间，搜索也没人碰到过

- [webpack-dev-server] App updated. Recompiling...
- 其他同事没碰到的原因是只pull了最新代码，但没有执行 pnpm i
- 解决方式是将代码回退，找到没问题的版本，原因大致是monorepo其他地方修改了配置
  - 其他同事也是这么解决的

- 后来其他同事通过打印webpack提供的import.meta，确定问题来自style9

## slate设置文本对齐的方式示例在官方示例rich-text，自己却在其他地方找了很久，浪费时间

## block-editor拖动鼠标形成选区后快捷键如加粗失效，但双击自动形成选取后快捷键仍可用

- 使用多编辑器实例实现block-editor时，跨block的选区实现很困难，还要考虑键盘、滚动等事件

> 自研实现选区的方案都要考虑此问题

## slate编辑器的悬浮工具条做了一个月没做完，如何在编辑器组件外部操作编辑器数据

- 思路💡️： slate-text和其他组件都从外部如database获取数据，这样更新database数据的方法就在外部了，到处都可以拿到

- 思路1: 在全局创建eventmitter，在组件外其他地方emit事件，通知注册了监听函数的slate-text组件更新自身
  - 缺点是在其他位置获取slate-text组件的数据很复杂，因为普通eventemitter很难获取emit事件的结果

- 思路2-变通: 将slate-text组件的ref保存到全局，然后就可以在组件外其他地方通过拿到ref来操作slate-text组件通过useImperativeHandle暴露的方法，从而更新slate-text组件

## overleaf的pdf

- 基于mozilla开源的pdf.js实现
- 一个神奇的问题，pdf的蓝色链接使用开发工具定位到a标签元素后，a标签的css样式颜色值不是真实值(把这个颜色应用到设计软件后这个文字颜色明显不是pdf上的文字颜色)
  - 原因是，要考虑pdf的渲染基于canvas实现，下层是canvas图片，上层是文字
  - 当光标点击或悬浮在文字之上时，文字元素才会出现，否则要手动给该元素设置颜色和位移才能显示出来
  - 当手动删掉div.canvasWrapper元素后，pdf上的文字就会消失，但pdf的页面容器还存在

## 手写Promise

  - `then`()方法可以注册回调函数
- 对于static resolve/reject方法的实现，可以用setTimeout，创建promise对象时阻塞，然后给机会让then方法执行注册回调函数

- 复制相似的代码注意修改必需项
  - 复制 this.resolveList.push 到 this.rejectList.push
  - 忘记修改排查了好久才找到原因

## 调试深拷贝的实现碰到各种问题

- 必须使用`Map`或双数组或元素为键值对的数组，不能用`{}`; 
  - The keys of an Object must be either a String or a Symbol.
  - 如果使用object对象作为键，会产生覆盖问题

```JS
aa = { a: 1 };
bb = { b: 1 };
cc = {};

// 使用对象作为key时，类型会转换成string，所以默认都是  [object Object]
// 因为属性名相同，所以属性值会覆盖

cc[aa] = 'cc11'; // {[object Object]: 'cc11'}
cc[bb] = 'cc22'; // {[object Object]: 'cc22'}
```

- 特殊内置类型对象属性值创建拷贝后可立即返回，不用遍历拷贝Date/RegExp的属性了

- `new Date(dateObj); new RegExp(reObj)` 可以方便地创建对象，
  - 但mozilla的文档没有提供说明，各浏览器底层的实现也可能不一样

## js `arr.sort()` 不传递比较函数参数时，会先转换为字符串再比较

- 所以使用官方的arr.sort()建议必须写比较函数

> The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values.

- 所以 `[1,2,100].sort()` 的结果是 [1, 100, 2]

## 递归有时会依赖其返回值

- 不要漏写return

## arr.forEach 遍历 action reducer 函数时，return无法立即结束forEach 

- 可改用传统for循环

## 少使用 `auth && <Routes />` 的形式

- auth为null时，右边也会悄悄执行

## 开发时setState没有触发rerender

- 可能是因为 react-refresh 热加载插件，保留了页面内组件的状态
- 刷新页面即可看到

## react-router 在界面中使用 Link 可以正常跳转，但在地址栏address bar输入url回车时不能直接跳转到指定url

- 要理解client-side routing的原理
  - 在页面内通过Link组件跳转url是利用页面已下载且正在执行的js修改浏览器的url的值，没有发生服务器请求
  - 在地址栏输入或粘贴url按回车，会立即发送服务器请求，因为服务器只有index.html/bundle.js等少数资源，所以服务器会返回找不到资源的404异常

- [React-router urls don't work when refreshing or writing manually](https://stackoverflow.com/questions/27928372)
  - Those same URLs work fine on the client-side, because there React Router is doing the routing for you, but they fail on the server-side unless you make your server understand them.
  - If you want the http://example.com/about URL to work on both the server- and the client-side, you need to set up routes for it on both the server- and the client-side. 
- With Hash History instead of Browser History, your URL for the about page would look something like this: `http://example.com/#/about`. 
  - The part after the hash (#) symbol is not sent to the server. 
  - So the server only sees http://example.com/ and sends the index page as expected. 
  - React-Router will pick up the #/about part and show the correct page.
  - Downsides:
    - 'ugly' URLs
    - Server-side rendering is not possible with this approach. As far as Search Engine Optimization (SEO) is concerned, your website consists of a single page with hardly any content on it.

## 使用 `<a href='#!'> icon </a>` 模拟button

- 优点是button自身样式过多，anchor更简洁，但也有自身样式
- 缺点是 可能造成所有组件rerender，注意观察highlight updates的闪烁绿框的范围
- 还可考虑直接用 `<span style={{cursor:'pointer'}}> icon </span>` ；此时闪烁绿框范围较小

## react.lazy 批量动态导入pages文件夹下的所有react组件

> 20210904 又碰到此问题

- 原因是数据的属性数量与预期的不同
  - error信息里面给出了错误链路，可以倒着分析出来

> 20210821又碰到此问题

- 原因是文件名写错了，默认拼接成的组件地址为 index.tsx，而不是index.ts
- 一个文件组件动态导入出错，导致了Suspense的RoutingPagesErrorBoundary错误在其他路由也占据页面，影响判断

------

- 使用ErrorBoundary组件包裹Suspense，可以显示其他正常组件，在动态导入失败的位置显示ErrorBoundary的fallback组件
- 原因是以异步方式定义的变量，不能直接马上使用它的值，实际执行时的数据类型也可能是异步返回值的类型
  - 动态导入每个组件后，不能马上 `route.component = LazyLoadedComp`

  - 可以放在Route定义处导入

```

Error: Cannot find module './[object Object].tsx'

 componentStack: "\n    at Lazy\n    at D (webpack-internal:///../../n…/./src/store/global-context.tsx:89:21)
```

- 抛出的异常却是导入另外一个文件夹下的react组件失败
  - 变通的方法，在每个`Route`组件定义的定义动态导入，而不是在其他其他统一动态导入

## react onClick中如何访问旧的state

- 全部通过setState(prev=> { doSth(prev); return newState; })
  - 不要部分使用oldState，部分使用prev

```JS
   setState((prev) =>
     prev.has(curItem) ?
     new Set(Array.from(prev).filter((i) => i !== curItem)) :
     new Set(prev.add(curItem)),
   );
```

## 实现mdx文档编辑后自动更新的思路

- (在当前app界面)编辑内容后直接渲染最新内容到dom，都在内存无需本地
- (在3方编辑器界面)编辑内容后保存到本地文件，然后app扫描目录，渲染内容
- ssg: 首次全面渲染，然后在后台监听新文件的添加，并立即构建
- ssr: 每次点击url，都重新请求mdx的内容

## 文件编辑浏览的实现思路

- edit > ~~save(内存或本地)~~ > render
- usecase
  - webpack的热加载

## 调试component-docs的文档示例

- npm workspaces的不同子包，可以使用不同版本的react，不会冲突
- 异常信息是 `mini css extract plugin loader has been initialized using an options object that does not match the api schema.` .
  - 修改版本后测试发现，深层原因不是mini-css-extract-plugin的版本问题
  - 查看component-docs项目的issues，有人已经提交了最新版样式错乱broken的bug，所以应该降级component-docs，而不是降级mini-css-extract-plugin
  - 容易看花眼: ^0.20.4，^0.24.0
