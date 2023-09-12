---
title: lib-utils-codesandbox-plugin
tags: [codesandbox, extensions, plugin-system, scripts, utils]
created: 2023-09-02T09:15:34.289Z
modified: 2023-09-02T09:16:30.412Z
---

# lib-utils-codesandbox-plugin

# guide

- tips
  - 简单场景考虑基于eval/Function的方案
  - 复杂场景可参考 microsoft-excel-addon script-lab
# iframe
- iframe页面没有自己的历史记录，使用的是基座(父页面)的浏览历史
  - 当iframe页在内部进行跳转时，浏览器地址栏无变化，基座中加载的src资源也无变化
  - 当浏览器刷新时，无法停留在iframe内部跳转后的页面上，需要用户重新走一遍操作
# blogs

## [浅析 JavaScript 沙箱 - 掘金](https://juejin.cn/post/7148335784431468551)

- [浅析 JavaScript 沙箱机制 - 知乎](https://zhuanlan.zhihu.com/p/428039764)
  - 沙箱（Sandbox）是一种用于隔离正在运行程序的安全机制，通常用于执行未经测试或不受信任的程序或代码，它会为待执行的程序创建一个独立的执行环境，内部程序的执行不会影响到外部程序的运行。
  - 最直接的想法就是程序中访问的所有变量均来自可靠或自主实现的上下文环境而不会从全局的执行环境中取值
  - 非常简陋的沙箱（with）
    - with 会在作用域链的顶端添加一个新的作用域，该作用域的变量对象会加入 with 传入的对象
    - 问题来了，在提供的上下文对象中没有找到某个变量时，代码仍会沿着作用域链一层一层向上查找，这样的一个沙箱仍然无法控制内部代码的执行
  - 没那么简陋的沙箱（With + Proxy）
    - Proxy 中的 get 和 set 方法只能拦截已存在于代理对象中的属性，对于代理对象中不存在的属性这两个钩子是无感知的。
    - 因此这里我们使用 Proxy.has() 来拦截 with 代码块中的任意变量的访问，并设置一个白名单，在白名单内的变量可以正常走作用域链的访问方式，不在白名单内的变量会继续判断是否存在沙箱自行维护的上下文对象中，存在则正常访问，不存在则直接报错
    - 较为简单的场景就可以覆盖了, eg: Vue 的模板字符串
  - 天然的优质沙箱（iframe）
    - iframe 标签可以创造一个独立的浏览器原生级别的运行环境，这个环境由浏览器实现了与主环境的隔离。
    - 在 iframe 中运行的脚本程序访问到的全局对象均是当前 iframe 执行上下文提供的，不会影响其父页面的主体功能，因此使用 iframe 来实现一个沙箱是目前最方便、简单、安全的方法。
    - 虽然浏览器为主页面和 iframe 之间提供了 postMessage 等方式进行通信，但单单使用 iframe 来实现多沙箱通信这个场景是比较困难且不易维护的。
  - 应该能用的沙箱（With + Proxy + iframe）
    - 利用 iframe 对全局对象的天然隔离性，将 iframe.contentWindow 取出作为当前沙箱执行的全局对象
    - 将上述沙箱全局对象作为 with 的参数限制内部执行程序的访问，同时使用 Proxy 监听程序内部的访问。
    - 维护一个共享状态列表，列出需要与外部共享的全局状态，在 Proxy 内部实现访问控制。
  - 沙箱逃逸（Sandbox Escape）
    - 访问沙箱执行上下文中某个对象内部属性时，Proxy无法捕获到这个属性的访问操作。
    - 通过访问原型链实现逃逸，JS 可以直接声明一个字面量，沿着该字面量的原型链向上查找原型对象即可访问到外层的全局对象，这种行为亦是无法感知的
  - “无瑕疵”的沙箱（Customize Interpreter）
    - 有不少开源库已经在做这样一件事情，也就是分析源程序结构从而手动控制每一条语句的执行逻辑，通过这样一种方式无论是指定程序运行时的上下文环境还是捕获妄想逃脱沙箱控制的操作都是在掌控范围内的。
    - 实现这样一个沙箱本质上就是实现一个自定义的解释器。
    - myInterpreter(code, ctx, illegalOperations) // 自定义解释器

## [【微前端】JS沙箱的基本实现 - 知乎](https://zhuanlan.zhihu.com/p/450103808)

- 微前端中，为了保证应用之间js环境（主要是window全局变量）的独立，需要使用JS沙箱来对各应用的执行环境进行隔离。
- qiankun中使用了两种方案来实现这一隔离，分别是：快照沙箱、代理沙箱Proxy
- 对于支持Proxy的浏览器使用代理沙箱，不支持的浏览器降级使用快照沙箱。
- 快照沙箱的基本思路是记录差异并存储。
  - 沙箱激活前，当前window对象一定为纯粹的window对象；沙箱激活后至沙箱失活前，当前的window对象一定为当前应用使用的window（即纯粹的window对象+当前应用对window对象做出的修改）
  - 快照沙箱即对两个状态的window对象进行一次快照，然后比对两次快照的不同，存储不同内容和原始内容，达到差异重置的目的。
- 代理沙箱运用了proxy，保证了window对象的纯净，不被污染。
  - 代理沙箱运用了proxy，保证了window对象的纯净，不被污染。
  - 每个 ProxySandbox 都拥有其独立的代理对象，并不会污染真正的window对象，而快照沙箱会污染真正的window对象，所以需要在激活失活时去进行恢复/重置操作

## [30 行代码实现 JS 沙箱 - 知乎](https://zhuanlan.zhihu.com/p/589341143)

- 在 JavaScript 中，动态执行代码的方法有 Function 和 eval

```JS
eval('console.log("aaa:", aaa)');

Function('str', 'console.log(str, aaa)')('aaa:');
```

- `eval` 是在**当前作用域**直接执行代码，代码可以直接访问当前作用域。
  - 而 `Function` 创建的函数只会在**全局作用域**中运行（除主动修改作用域：bind，call 等），所以 Function 相对安全。
- 因为使用 `Function` 相当于定义一个函数，会进行分词和解析等编译工作，如果 Funcion 中执行的内容有语法错误，还是会报错 Uncaught SyntaxError 语法错误。
  - 但 `eval` 是直接对执行代码进行机器码的转译，缺少引擎编译带来的性能优化。所以 Function 比 eval 性能更优。
- 选择 Function 函数来动态执行代码后，我们可以 const createSandbox = () => code => Function(code)()
- 可以使用 Object.create() 来创建一个全局对象的副本，然后使用 with 让沙箱代码访问这个副本对象，从而达到隔离的效果。
  - with 语句可以将某个对象添加到作用域链的顶部。
  - 使用 with 的方式还存在一个问题，就是当访问全局对象不存在的字段时，还是能够访问到全局对象，比如新增字段。
- 避免沙箱代码中使用 this 访问全局对象，使用 bind 方法修改作用域。

## [使用 WebAssembly 打造定制 JS Runtime - 掘金](https://juejin.cn/post/7146939939786063885)

- 起因是在 lightdm-webkit2-greeter 这个 lightdm 插件中看到了自定义 JS Runtime的魔力，它支持在显示管理器中使用 web 技术去自定义登录界面，与操作系统的交互是通过 Runtime 中的一组 JS API来实现登录、关机、睡眠等功能

- 把 webkit 搬过来渲染系统界面，然后通过定制的 JS Runtime 与操作系统交互，相当于对浏览器本身进行了改造，关键的实现点是把系统调用封装成了Native函数，并在JS Runtime中进行绑定，以实现浏览器界面控制操作系统。

- 这种方式和 Electron 的本质区别在于，无需让浏览器与另外一个进程通信，它直接拓展了 JS 的运行时环境，与 Node 的做法十分相像，不过这次我们越过中间商赚差价，自己实现 Runtime ，可以做的更小巧和定制化。

- 这里选择了 Figma 曾经的方案 - Duktape
  - Duktape是一个嵌入式Javascript引擎，专注于可移植性和低空间占用。
  - 易于集成到C/C++项目中：将duktape.c, duktape.h，和duk_config.h添加到的构建项目中，然后使用Duktape API实现 C 代码与 Ecmascript 函数的双向调用。
# discuss-iframe
- https://github.com/niutech/x-frame-bypass /js
  - https://niutech.github.io/x-frame-bypass/
  - Web Component extending IFrame to bypass X-Frame-Options: deny/sameorigin
  - X-Frame-Bypass is using a CORS proxy to allow this

- ## 

- ## 

- ## [Alternative to iFrames with HTML5 - Stack Overflow](https://stackoverflow.com/questions/8702704/alternative-to-iframes-with-html5)
- You can use object and embed
  - Keep in mind that most modern browsers have deprecated and removed support for browser plug-ins, so relying upon `<embed>` is generally not wise if you want your site to be operable on the average user's browser.
- There is one alternative to `<iframe>` and that's the `<object>` tag. It can display content from different sources as well. The pro is it being conform to the **xhtml-standards** and encouraged to use but there's not such a broad / usable support in older browsers (you have to mess with it to get it right in IE).

- As others have mentioned you can also use the embed tag and the object tag but that's not necessarily more advanced or newer than the iframe.
  - HTML5 has gone more in the direction of adopting web APIs to get information from cross domains. **Usually web APIs just return data though and not HTML**.

- ## [How to show google.com in an iframe? - Stack Overflow](https://stackoverflow.com/questions/8700636/how-to-show-google-com-in-an-iframe)
  - Why does google.com not load in an iFrame 

- The reason for this is, that Google is sending an `X-Frame-Options: SAMEORIGIN` response header. 
  - This option prevents the browser from displaying iFrames that are not hosted on the same domain as the parent page.

- Because it has `X-Frame-Options` Header policy and browsers tend to respect those policies.
  - The "X-Frame-Options" allows a secure web page from host B to declare that its content (for example a button, links, text, etc.) must not be displayed in a frame of another page (e.g. from host A). 
  - In principle this is done by a policy declared in the HTTP header and obeyed by conform browser implementations.

- You can use this URL in an iframe
  - `https://www.google.com/webhp?igu=1` this url works
  - it's Google itself leaves the hole. I don't say it's a Loophole, just maybe Google think it's necessary under some circumstances.

- f you want to embed Google into an iframe you can do what sudopeople suggested in a comment above and use a Google custom search link like the following. 
  - `<iframe id="if1" width="100%" height="254" style="visibility:visible" src="http://www.google.com/custom?q=&btnG=Search"></iframe>`

- 
- 
- 

- ## [how to resolve iframe cross domain issue - Stack Overflow](https://stackoverflow.com/questions/40866219/how-to-resolve-iframe-cross-domain-issue)
  - I'm making web page that has to show another domain's web page.
  - `<iframe src="http://stackoverflow.com"></iframe>` usecase
  - My web page can't show stackoverflow.com. Because, stackoverflow denies this

- You need control over the domain you want to embed to remove/amend its CORS policy.
  - If the domain has explicitly blocked Cross-Origin requests, there's nothing you can do about it.
  - This is used to avoid anyone hijacking any site you want (you could have a full screen Google in an iframe running with your ads on top on bettergoogle.com, things like that).

- CORS does not apply when attempting to programmatically access content from a cross-origin iframe. 
  - If you want to access content from an iframe on a different domain, you will need to make use of the Web Messaging API (window.postMessage & the onmessage event) to communicate between your page and the iframe.

- It's also possible to access an iframe's content from another domain using Window.postMessage().
  - yes, but not here : because its iframe will not answer to the message. The question was "can they access the content of the iframe without my permission", and the answer is no.

- ## [iframe有什么好处，有什么坏处？](https://www.zhihu.com/question/20653055)
- 浏览器兼容性特别好
- iframe原本的用法在现在看来是不合时宜的，问题太多了但是它的其他功能却是不错的黑魔法，这里列举一些
  - 用来实现长连接，在websocket不可用的时候作为一种替代，最开始由google发明。Comet：基于 HTTP 长连接的“服务器推”技术
  - 跨域通信。JavaScript跨域总结与解决办法 ，类似的还有浏览器多页面通信，比如音乐播放器，用户如果打开了多个tab页，应该只有一个在播放
  - 历史记录管理，解决ajax化网站响应浏览器前进后退按钮的方案，在html5的history api不可用时作为一种替代。
  - 纯前端的utf8和gbk编码互转。

    - 比如在utf8页面需要生成一个gbk的encodeURIComponent字符串，可以通过页面加载一个gbk的iframe，
    - 然后主页面与子页面通信的方式实现转换，这样就不用在页面上插入一个非常巨大的编码映射表文件了

  - 用iframe实现无刷新文件上传，在FormData不可用时作为替代方案
  - 在移动端用于从网页调起客户端应用
  - 创建一个全新的独立的宿主环境。

    - iframe还可以用于创建新的宿主环境，用于隔离或者访问原始接口及对象，
    - 比如有些前端安全的防范会覆盖一些原生的方法防止恶意调用，那我们就能通过创建一个iframe，然后从iframe中取回原始对象和方法来破解这种防范。

- 可以用于单页面项目强制更新title
- 可以做委托提交，使页面不刷新、不跳转

- ## [为什么前端尽量少用iframe？](https://www.zhihu.com/question/23683645/answers/updated)
- 因为iframe等于打开一个新的网页，所有的JS/CSS全部加载一遍，内存会*2，无法释放，典型的内存泄露
  - 最近一个vue项目，一个组件用到了iframe，每次切换路由，会销毁这个组件，再重新加载，

    - 在火狐浏览器下，切换几十次内存占用暴增，最后浏览器崩溃，但是在谷歌浏览器下一切正常，
    - 通过各种方法最终定位到是iframe导致的内存泄漏，就是因为每次组件销毁但是iframe的内存在火狐下不会被释放，谷歌没有这种问题。
    - 解决方法是：把iframe提取到上一层组件，只加载一次，切换路由不会重新加载iframe，就一切正常了。

- 移动端对iframe不友好
  - 最近有个项目在移动端使用iframe，解决了安卓IOS又出问题，解决完ios安卓又出问题
- iframe是(几乎)不能访问外部数据的，js的作用域也会很奇怪
- iframe会阻塞主页面的Onload事件；
  - 动态创建iframe利用src来进行异步加载就可以避免上面的问题了
- iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
- 当时是基于iframe实现布局方便考虑的，没成想这是一个巨大的坑，
  - 内容区域iframe高度自适应可把我们坑苦了，然后布局上出现各种怪异的问题

- ## [Why Not Iframe](https://www.yuque.com/kuitos/gky7yw/gesexv)
- 为什么不用 iframe，这几乎是所有微前端方案第一个会被 challenge 的问题
- iframe 最大的特性就是提供了浏览器原生的硬隔离方案，不论是样式隔离、js 隔离这类问题统统都能被完美解决。但他的最大问题也在于他的隔离性无法被突破，导致应用间上下文无法被共享，随之带来的开发体验、产品体验的问题。
1. url 不同步。浏览器刷新 iframe url 状态丢失、后退前进按钮无法使用。
2. UI 不同步，DOM 结构不共享。想象一下屏幕右下角 1/4 的 iframe 里来一个带遮罩层的弹框，同时我们要求这个弹框要浏览器居中显示，还要浏览器 resize 时自动居中..
3. 全局上下文完全隔离，内存变量不共享。iframe 内外系统的通信、数据同步等需求，主应用的 cookie 要透传到根域名都不同的子应用中实现免登效果。
4. 慢。每次子应用进入都是一次浏览器上下文重建、资源重新加载的过程。
- 其中有的问题比较好解决(问题1)，有的问题我们可以睁一只眼闭一只眼(问题4)，但有的问题我们则很难解决(问题3)甚至无法解决(问题2)，而这些无法解决的问题恰恰又会给产品带来非常严重的体验问题， 最终导致我们舍弃了 iframe 方案。

- 慢的问题：慢的问题可以使用单例的iframe，不销毁，而且可以预加载
- 路由问题：主应用和iframe的路由做个映射关系，这样iframe就可以实时响应url变化了
- 弹框遮罩、通讯问题：可以在创建iframe的时候把topwindow的对象挂在到子应用的window上，这样子应用就能直接调用topwindow的方法了，比如使用topwindow的弹框，而且这种方式主应用可以往iframe中注入脚本和样式等，通讯也可以通过管理“事件中心实现” （这个方案还在探索中）

- 另外某些情况下，比如网页截屏，iframe 就不被支持
- 事件处理也是个问题，比如实现顶层菜单展开时，需要点击空白处收起，如果点到ifram则无法触发

- iframe 还有一个问题就是不能改变其在 DOM 树中的位置，否则也会导致重新加载 iframe。而在以 VDOM + Router 的场景中  iframe 都会被重新加载
# more
- [比 eval 和 iframe 更强的新一代 JavaScript 沙箱 - JavaScript 提案：ShadowRealm](https://zhuanlan.zhihu.com/p/549547458)

- [iframe接班人-微前端框架qiankun在中后台系统实践](https://zhuanlan.zhihu.com/p/259209543)
