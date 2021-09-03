---
title: dev-ing-pieces-xp
tags: [dev, xp]
created: '2021-04-28T20:54:34.301Z'
modified: '2021-04-28T20:54:58.126Z'
---

# dev-ing-pieces-xp

# pieces

- ## 

- ## 少使用 `auth && <Routes />` 的形式
- auth为null时，右边也会悄悄执行

- ## 开发时setState没有触发rerender
- 可能是因为 react-refresh 热加载插件，保留了页面内组件的状态
- 刷新页面即可看到

- ## react-router 在界面中使用 Link 可以正常跳转，但在地址栏address bar输入url回车时不能直接跳转到指定url
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

- ## 使用 `<a href='#!'> icon </a>` 模拟button
- 优点是button自身样式过多，anchor更简洁，但也有自身样式
- 缺点是 可能造成所有组件rerender，注意观察highlight updates的闪烁绿框的范围
- 还可考虑直接用 `<span style={{cursor:'pointer'}}> icon </span>` ；此时闪烁绿框范围较小

- ## react.lazy 批量动态导入pages文件夹下的所有react组件

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

- ## react onClick中如何访问旧的state
- 全部通过setState(prev=> { doSth(prev); return newState; })
  - 不要部分使用oldState，部分使用prev

```JS
   setState((prev) =>
     prev.has(curItem) ?
     new Set(Array.from(prev).filter((i) => i !== curItem)) :
     new Set(prev.add(curItem)),
   );
```

- ## 实现mdx文档编辑后自动更新的思路
- (在当前app界面)编辑内容后直接渲染最新内容到dom，都在内存无需本地
- (在3方编辑器界面)编辑内容后保存到本地文件，然后app扫描目录，渲染内容
- ssg: 首次全面渲染，然后在后台监听新文件的添加，并立即构建
- ssr: 每次点击url，都重新请求mdx的内容

- ## 文件编辑浏览的实现思路
- edit > ~~save(内存或本地)~~ > render
- usecase
  - webpack的热加载

- ## 调试component-docs的文档示例
- npm workspaces的不同子包，可以使用不同版本的react，不会冲突
- 异常信息是 `mini css extract plugin loader has been initialized using an options object that does not match the api schema.` .
  - 修改版本后测试发现，深层原因不是mini-css-extract-plugin的版本问题
  - 查看component-docs项目的issues，有人已经提交了最新版样式错乱broken的bug，所以应该降级component-docs，而不是降级mini-css-extract-plugin
  - 容易看花眼: ^0.20.4，^0.24.0
