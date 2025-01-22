---
title: dev-ing-log-debug
tags: [debug, dev, xp]
created: 2021-04-28T20:54:34.301Z
modified: 2023-06-14T00:53:15.226Z
---

# dev-ing-log-debug

# guide

# not-yet
- ❓ hover的tooltip/popover如何调试
# tips
- 后端有没有收到请求以及请求执行是否成功/超时，需要开发时在业务逻辑的现场位置提前添加日志记录并判断，否则排查时需要靠猜或缺少信息
  - 添加日志的重要场景: http请求， 文件io， 文件格式解析异常(易漏)

- nextjs或react组件如何在浏览器devtools中调试或获取业务变量/对象
  - 有时在devtools中直接source代码不会生效
  - 可尝试在onClick等event handler的逻辑中间直接设置breakpoint，这样可在source面板看到调用栈及闭包对象，再通过 store as global variable 拿到重要对象

- 前端页面有时无法捕获鼠标事件，可尝试先F12关闭devtools控制台，再重启服务，然后页面可能就能正常交互了，再F12打开控制台调试异常
# issues-sketch/figma

## 

## figma渲染和浏览器渲染的区别

- 字体渲染的影响因素
  - 使用dom渲染文字时，不同浏览器渲染字体时能匹配到的fallback字体，比如mono字体常用 monaco > consolas > courier new > monospace
    - 💡 要让不同浏览器渲染的文字宽度相同，首先要让不同浏览器能匹配到相同字体的相同字号
  - 检查浏览器渲染字体的渲染实现基于dom，还是canvas/webgl自定义渲染逻辑
- 特殊字体在figma渲染得更友好，如roboto-mono在figma更好看，特别是针对keycode键盘符号元素的渲染
# issues-architecture

## 

## 

## 

## 大量用户同时调用github的api来clone仓库，可能导致后端崩溃

- 前端每次刷新页面都会发起一个新的clone请求，这个设计不好
  - 前端每次刷新页面应该去查询上次clone请求的结果
  - 后端使用同步处理的逻辑容易导致资源被占满
# issues

## 

## 

## editor的工具条点击相关事件，注意点击的同时要阻止事件冒泡 event.stopPropagation()

- 注意场景
  - 点击工具条undo, 有时会先执行blur使工具条消失，然后就不会执行undo逻辑了
  - clickOutside的场景下，有时先执行undo/showCmdk，然后执行outside逻辑隐藏掉，视觉上就是没执行

- `event.stopPropagation()`通常是比`setTimeout`更好的方案

## ai工作时写文件超时，agent_write_file call timeout(7s)

- NFS在staging下使用v4的文件问题

- 目前发现，相同的命令（time cat 1），在文件系统，nfs挂载目录，docker容器内执行都为0.001s，在cde terminal中执行延时显著增加，需要进一步排查
  - 已知 aws efs 有问题，其他问题待查

- 项目实测，nfs+btrfs更稳定， nfs+bcachefs在git-status不稳定
  - 特别是 find / 命令很容易导致文件系统崩溃，类似地，如果多个进程在执行ai写文件，也容易导致系统cpu爆满而崩溃
  - 考虑多个docker容器同时挂载同一个文件系统时，文件系统崩溃会导致多个docker不可用

## python socketio用的aiohttp客户端设了个4MB的限制

- ide server重连问题，nodejs和goagent没问题，和python有问题，看了下是socketio用的aiohttp客户端设了个4MB的限制

## 通过git fetch拉取代码失败，导致数据不一致的问题

- 多人git fetch会导致其中有人git fetch失败，所以导致数据不一致，解决方案是fetch失败后重试

- root thread会丢失node_modules数据的问题
  - 原因是使用第三方go-sdk操作git仓库文件导致丢失， 使用原生shell-git命令操作git仓库不会丢失文件

## codemirror打开大文件如package-lock.json时卡顿

- 原因定位到是 readOnlyRanges 扩展让每次 editorState 更新都会逐行计算readOnly范围
  - 减少计算的方式是使用自定义memo方法，不用WeakMap的原因是codemirror的editorState是不可变数据结构，更新次数过多，用字符串反而能解决问题

- [javascript - How to create a memoize function - Stack Overflow](https://stackoverflow.com/questions/30386943/how-to-create-a-memoize-function)

```JS
var myMemoizeFunc = function(passedFunc) {
  var cache = {};
  return function(x) {
    if (x in cache) return cache[x];
    return cache[x] = passedFunc(x);
  };
};

const memoize = (func) => {
  const results = {};
  return (...args) => {
    const argsKey = JSON.stringify(args);
    if (!results[argsKey]) {
      results[argsKey] = func(...args);
    }
    return results[argsKey];
  };
};
```

## clacky的.go文件的diff-view在编辑时抛出异常

- rangeError

- 原因是paas用的legacy-modes里面go语法高亮
  - 2024年官方发布了新版实现的go语法高亮，且需要 "@codemirror/language": "^6.6.0", 
  - 但paas里面锁定了版本  "@codemirror/language": "6.5.0", 
  - 6.6.0 (2023-02-13)： Syntax-driven language data queries now support sublanguages, which make it possible to return different data for specific parts of the tree produced by a single language. 

## codemirror的stateField扩展不能使用工厂方法创建, 否则tooltip的dom元素会显示后立即消失

- 原因是state变化时tooltip的dom创建后会立即销毁

- toolbar上按钮的click事件会后于editor的blur事件执行，若在editor的blur事件中已经将toolbar所在的dom销毁了，toolbar上按钮的事件也不会触发
  - blur事件中的timeout设置要考虑低性能的浏览器和设备，调试时设为60ms会在windows上出bug，设为120ms会在windows上正常

## innerHTML=\ `内容\` 内容中若有换行时，会占用元素高度

- 注意内容使用反引号包裹和使用双引号包裹时内部换行符的区别

- 下面的示例中 Reject span元素的高度为100px左右

```HTML
<div class="cm-ai-prompt-input-actions">
  <button id="cm-ai-prompt-btn-accept" class="cmdk-accept-btn">
    <span style> Accept </span>
    <span class="hotkey-text">
      ⌘↩
    </span>
  </button>
  <button id="cm-ai-prompt-btn-discard" class="cmdk-reject-btn">
    <span>
      Reject
    </span>
    <span class="hotkey-text">
      ⌘⌫
    </span>
  </button>
  <!-- <button id="cm-ai-prompt-btn-gen">Regenerate</button>  -->
</div>
```

## 监听文件系统变化然后通知

- 网络文件系统 NFS/SMB 的文件变化可能有的文件监听库如chokidar监听不到, 有的实现库可以监听到
  - 这会导致代码在本地文件系统运行没问题，但在aws或其他云主机上监听不到文件变化

## clacky在多用户同时clone/fork时出现并发问题

- 通过github api拉取项目，分为 校验阶段+拉取阶段
- 若clone depth设为N来只拉取部分数据, github那边校验阶段耗时可能很长，比拉取全量数据的耗时更长
  - depth为1时很快，为100时可能很慢
  - 实现时可以先拉取depth为1，再在空闲时fetch剩余的历史记录

- 系统的性能受第三方资源如github的限制，设计初期要想办法避免

## cmdk的弹出框的右上角关闭按钮位置错误

- 输入卡片容器是 relative定位， flex-column布局
  - 关闭按钮 display-block, absolute定位
    - 按钮图标svg， 默认display-block
- 问题上svg显示在按钮的下方，而不是在button里面
  - 🤔 解决方案是将关闭按钮调整为 display-flex，这样svg就会显示在button里面
  - 又debug了几小时，发现现在的布局实现会让关闭按钮被overflow-hidden挡住，需要调整元素的位置和层次来显示完整的关闭按钮，也变向解决了问题

## figma的sparkling-fill icon无法在驾驶舱渲染

- 但在页面header部分渲染icon后，驾驶舱groupHeader的图标也能正常渲染
  - 在groupHeader先隐藏再通过条件变为true也能让它渲染

## nextjs项目集成clerk后无法正常打开页面

- 因为刷新页面需要获取clerk的token，对网络要求很高
  - 解决方法是开启代理的增强模式，然后使用全局代理而不是rule

## codemirror打字机动画

- 为什么先dispatch(scrollIntoView)再typing-line的执行结果是先动态打字，再滚动
- 在setInterval中更新操作行号，那么自动滚动到dom需要~~在下次渲染前触发，先滚动到下一块再打字机  ~~

## 🎨 flex-col布局，切换底部时光机面板时要保持底部面板内容高度变化时始终可见

- 上中下布局中间是`flex-1`的场景，有时底部高度变大时中间高度不变且底部下面会被遮挡(预期是底部可见中间变短)
  - 解决方法是 `flex-1`的元素加上 ~~`overflow-hidden`~~ `min-height:0px`

- ~~底部面板的dom元素使用同一个，然后根据状态切换内容dom~~
  - ~~不能根据状态渲染2个不同的dom，比如div和footer，这样底部面板内容可能看不见~~

- [Why is overflow hidden required to make this flex layout work properly? - Stack Overflow](https://stackoverflow.com/questions/66907438/why-is-overflow-hidden-required-to-make-this-flex-layout-work-properly)
  - to be more accurate, you need `min-height:0` but `overflow:hidden` is doing the same

- [min-height: 0 or min-width: 0](https://x.com/argyleink/status/1354467081878560780?lang=en)
  - my least favorite (easiest to forget because they're unintuitive) CSS "solutions" to layout issues
  - the minimum width of a grid and flex children is `auto`. setting it explicitly to 0 removes the intrinsic size, unlocking various things

- ### 💡 [Why don't flex items shrink past content size? - Stack Overflow](https://stackoverflow.com/questions/36247140/why-dont-flex-items-shrink-past-content-size)
- A flex item cannot be smaller than the size of its content along the main axis. 
  - The defaults are `min-width: auto` or `min-height: auto` for flex items in row-direction and column-direction, respectively.
  - You can override these defaults by setting flex items to: `min-width: 0` or `min-height: 0` or `overflow: hidden` (or any other value, except visible)

- To provide a more reasonable default minimum size for flex items, this specification introduces a new `auto` value as the initial value of the min-width and min-height properties defined in CSS 2.1.
  - The `min-width: auto and min-height: auto` defaults apply only when `overflow` is `visible`.
  - If the overflow value is not visible, the value of the min-size property is 0.
  - Hence, overflow: hidden can be a substitute for min-width: 0 and min-height: 0.
- You've applied min-width: 0 and the item still doesn't shrink?
  - Basically, a higher level flex item with `min-width: auto` can prevent shrinking on items nested below with `min-width: 0`.
  - If you're dealing with flex items on multiple levels of the HTML structure, it may be necessary to override the default min-width: auto / min-height: auto on items at higher levels.
- I'm finding this has bitten me repeatedly over the years for both flex and grid, so I'm going to suggest the following: `* { min-width: 0; min-height: 0; }`

## 调试cde的跟随模式渲染编辑器异常，即无法渲染

- 一开始以为是通信过程中事件处理逻辑的问题，参考1024code和showmebug后不是此问题
  - 调试多层编辑器的渲染，找到触发unmount的条件添加限制来解决问题

- [fix: following ai ui and switch files by uptonking · Pull Request · clacky-ai/clacky-ai-frontend](https://github.com/clacky-ai/clacky-ai-frontend/pull/107/files)

## 调试idepaas的编辑器不能正常渲染，调试了一晚上加第二天整天 _20240714

- 原因是 用户跳转路由的方式有很多种，如浏览器back、页面link、手敲url，某些情况下zustandx的状态会在页面跳转后保持旧的
- 解决方法是 进页面后先尝试清空state对象，再初始化业务逻辑更新state

- api请求响应因为梯子不稳定导致更烦躁
  - 请求慢的原因，是其他api的请求header需要clerk的token，这个前置请求很慢

## 🤔 是否要将socket连接方法放在全局state里面

- ai-agent的socket连接与state结合的问题
  - 💡 不要直接暴露socket连接对象， 暴露socket的on/emit方法即可
  - 创建连接conn的逻辑是effect，若使用全局工具方法获取conn对象，则effect范围太大
  - 考虑 依赖注入取值 vs 全局工具方法取值

- pros
  - 可在状态更新方法中直接发送socket消息
  - state持有socket操作方法，就不存在类似fetch的外部依赖
- cons
  - 状态中的socket方法无法持久化

- 现有方案
  - redux将socket放在middleware
  - zustand

## 20240617: nextjs react strictMode 导致的问题

- 计划执行进度条的动画播放速度变为2倍
  - 基于setInterval实现的进度条

- 🤔 ai-plan-steps-tree的折叠效果失败
  - debug调试时，nextjs在严格模式下，onClick的handleCollapse里面setState后计算最新数据第一次为最新可折叠数据，紧连着的第二次为旧数据
  - 💡 原因是strict模式下执行2次render导致 `setState(v=>!v)` 执行2次，由于setState的参数没有close over原始值，所有boolean会复原
  - 🧐 逐步仔细分析异常的位置

## 20240527: Warning: Each child in a list should have a unique "key" prop.

- [Unable to see key value in React or Chrome devtools - Stack Overflow](https://stackoverflow.com/questions/65552907/unable-to-see-key-value-in-react-or-chrome-devtools)
  - Solved by changing settings. In React devtools: Components tab -> settings symbol -> components -> remove or disable the filter type equals host (e.g. `<div>`)
- 可以在react devtools里面查看基本dom元素，上面就可以看到具体dom元素的key值冲突

- 🔂 可能是找错了异常发生的位置，查看error的调用链，真实的异常位置不在第一层的render方法，而是在前面组件的render方法

## /code/fork 创建playgroundId的api一直显示 cancelled

- 变通方法是用 staging环境 的api，而不是 dev环境 的api

## 旧代码1024paas试了很多遍不能注册和创建sandbox

- 最后注册个新帐号解决了

- 尝试过不使用axios，直接在getServerSideProps用fetch，也可以定位问题
  - 但node环境下调试req和res的headers和参数很不方便

## Module '"parchment"' has no exported member 'Bolt'

- 排查了很久，import名称错误，是 Blot, 而不是 Bolt

- [typescript - Module has no exported member error in angular module - Stack Overflow](https://stackoverflow.com/questions/57234220/module-has-no-exported-member-error-in-angular-module)
  - Make sure the names are matching.

## [rspack serve 热加载慢到200s，若执行rspack build会慢到70s, ，，我还用webpack试了都没有这么慢](https://discord.com/channels/977448667919286283/1219528136543440988/1219619268987977770)

- 看了下 newTreeshaking 关闭的情况下是快的，建议 production build 的时候再开 newTreeshaking, 现在 dev 下开 newTreeshaking 会有点慢 

## sharp安装问题

- 可尝试修改 node_modules dist 目录下的源码，绕过sharp

## express router 无法触发的问题

- 一步步调试，定位到问题是 middleware 是高阶函数，route使用时不能直接用，要用 userRouter.get('/', [authorize()], userController.me); 
  - 而不是 userRouter.get('/', [authorize], userController.me); 

## monorepo多包项目的bundle

- 若打包各包默认的 dist/index.js， 会产生大量的重复代码
- 若使用tsc编译多包，tsc无法输出单文件且没有transpile-only
- 临时方案，使用rspack编译各包源码，通过 resolve.alias 直接编译src/index.ts，而不是 dist/index.js，注意要同时支持browser和node

## react-starter-rspack自动部署到github-pages

- 不要执着于旧项目模版，github actions/workflow/token/pages支持的部署方式已有很大变化
  - 最新的部署不需要token
- 反复理解官方文档和官方示例，修改尝试
- 官方文档更新过快，marketplace里面很多action都失效了
- yaml的语法检查

## list item前的黑点大小不一致，黑点基于 `::before` 伪元素实现

- 因为before伪元素的父元素的font-family会影响伪元素的渲染，字体不同时渲染出的黑点大小不一致
  - 还需考虑基于`::marker`实现的伪元素的默认样式

- inline元素设置margin-top/bottom不会生效，可转换为inline-block

## type 'getRowModel' is not assignable to type 'keyof TablePlugin'

- 调试浪费了很多时间
  - 原因是之前改名了，getRowModel > getTableRowModel

## watarble-snabbdom渲染细节

- 首次渲染需要 vnode的顶层节点 与 已存在的domNode 匹配，所以一般要先创建domNode或修改vnode顶层节点的选择器

- useReactTable的实现，每次执行该hook时，会执行setOptions更新table实例的配置，手动更新state
  - 自己封装时，也要在createTable后立即setOptions

## vscode里面调试mocha测试的命令调了很久

- 先在控制台调通，再修改launch.json

- 原因是 --experimental-loader 误写成了 --loader
  - nodejs v12 renamed from --loader to --experimental-loader.
  - This flag is discouraged and may be removed in a future version of Node.js. Please use `--import` with register() instead.

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

## webpack: ReferenceError: Cannot access x before initialization

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
