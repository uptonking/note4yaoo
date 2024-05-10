---
title: lib-utils-codesandbox-community
tags: [codesandbox, community]
created: 2024-01-25T13:28:03.358Z
modified: 2024-01-25T13:33:23.267Z
---

# lib-utils-codesandbox-community

# guide

# discuss-stars
- ## 

- ## The fastest way to restore an environment is to take a memory snapshot and restore it. 
- https://twitter.com/Vjeux/status/1777721284345930088
  - It’s pretty wild that CodeSandbox made it happen at scale!

- ## 🐛 If I could remove one thing from JavaScript it would be `eval()` .
- https://twitter.com/awesomekling/status/1758775888647188567
  1. Calling eval() may change the set of bindings in the existing environment. This prevents a lot of optimizations based on static knowledge of environment layout (although engines can still optimize anyway in scopes where eval is not called.
  2. It forces us to plumb the “completion” value around in a million finicky ways so that eval() can return it. (This is what’s bugging me today
  3. Running arbitrary strings as code at runtime in the first place is a pretty goofy API!
- how do you feel about new Function()? #3 applies but iirc 1 and 2 should be much less
  - Yeah, it’s a lesser evil and much less annoying to support than eval() 

- #3. is still important for me. I compile HTML templates (a PHP lookalike, containing <? js() ?>) using `new Function()` at runtime. Doing my best to avoid that pesky build step

- ## 🐘 Most sandboxes in CodeSandbox are stored in a Postgres database.
- https://twitter.com/CompuIves/status/1667148424389566465
  - 40M+ sandboxes and 400M+ files stored in Postgres, and we still have performant load times.
  - When going with Postgres, I thought "this is the first thing we'll have to replace". Still didn't happen after 6 years
- Generally, the three technologies that exceeded my expectations in scale and performance:
  - Postgres
  - Elixir
  - Rust
- Now we're seeing that the database is growing very big (leading to long & big backups), so we started archiving sandboxes to GCP to save space. We're considering moving our DB from k8s to a managed instance. But still, Postgres has exceeded all my expectations.
- Curious, which components are written in Rust vs Elixir? Did you find that Elixir was better suited for some tasks than Rust?
  - Yah, Elixir is doing everything with the API (including websocket message handling).
  - Rust is doing computationally expensive things, or things that require a lot of string manipulation.
  - For example, we use Elixir to handle WS OT messages, but we use Rust then to apply the OT operations on the string. We first did this with Elixir, but (partly because of my implementation) it started to eat a lot of memory as every mutation created a new string.
  - Elixir + Rust interop is fantastic, so it's nice if you can pull out Rust for these kind of things while maintaining the concurrency/robustness of Elixir for the server.
- Erlang/Elixir under load is just amazing. Incredibly resilient. One of the many reasons I became a fanboy of CouchDB. Still love Postgres but there is something beautiful about storing everything in a giant B-tree

- 🤔 How is the Postgres DB structured.  Is it single node or shareded across multiple nodes?  And do you store files in Postgres as blobs?
  - Single DB (with a R/O replica). Files are stored as text, binary files are uploaded to GCP and we store a link in the db.
- Wow, just single DB for such huge workload!  Must be a huge machine.
  - It's not huge! 4 cores and 24GiB RAM (actually I believe 16GiB would be fine too). Plus we also store sandbox pageviews (hourly, daily, weekly, monthly)/users/teams etc...
- Incredible!  I am using a little bigger machine for a much lesser scale application.  Likely I am doing something wrong.
# discuss-iframe
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

- If you want to embed Google into an iframe you can do what sudopeople suggested in a comment above and use a Google custom search link like the following. 
  - `<iframe id="if1" width="100%" height="254" style="visibility:visible" src="http://www.google.com/custom?q=&btnG=Search"></iframe>`

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
# discuss-author
- ## 

- ## [devpod: Codespaces but open-source, client-only, and unopinionated | Hacker News _202306](https://news.ycombinator.com/item?id=36407477)
- At CodeSandbox we're also working on this! Main focus of us is that we're running the environment in Firecracker microVMs, which allows us to snapshot and clone environments very quickly. 
  - This enables us to create a VM for every branch, which comes with the added advantage that every branch automatically has a snapshotted preview environment that can resume in ~2 seconds.

- ## 🌰 [Codemirror 6 and Typescript LSP - v6 - discuss. CodeMirror _202107](https://discuss.codemirror.net/t/codemirror-6-and-typescript-lsp/3398?page=2)

- Did https://codesandbox.io/ 4 switch away from CodeMirror to Monaco for it’s TypeScript/LSP editor? If so, is there a discussion somewhere of why? _202212
  - 💡 Actually, CodeSandbox has always used Monaco as the default editor, except for a specific mobile version where we defaulted it to CodeMirror.

- ## [Vscode.dev: Local Development with Cloud Tools | Hacker News _202307](https://news.ycombinator.com/item?id=36855517)
- The editor on CodeSandbox runs web VSCode, and in that version we emulate Node.js in the browser to run local extensions.
- I'm curious about the technical details. Could you elaborate on how CodeSandbox runs Node.js in the browser? Does it use a Linux VM like Alpine compiled to WASM?
  - Nodebox is a runtime for executing Node.js modules in the browser

- ## [Codesandbox open sources their execution environment: Sandpack | Hacker News _202112](https://news.ycombinator.com/item?id=29417937)
- Does it download the dependencies on the client side, and compile the JS on the client side as well?
  - Yep, it downloads and compiles dependencies on the client side. However, it does this on a different domain for security reasons.
  - Also, while it uses the CodeSandbox bundler, you can self host it so it's not dependent on our servers
- Is there an API to get the compiled and bundled sources into one output/result?
  - Yes, after every compilation we send the full bundler state. This is saved on the context so you can use that to analyze the output. In one of the examples in the blog post we show the transpiled code for example.
  - A hidden "feature" is that we automatically run tests defined (e.g. index.test.js) using jest, and dispatch the test results. So you can listen to that as well.

- I'd like to see storybook with support for this.
# discuss-csb-editor
- ## 

- ## [Feature request: Monaco Editor integration option? · codesandbox/sandpack _202201](https://github.com/codesandbox/sandpack/issues/305)
  - Codesandbox website uses Monaco, so it would be nice to have a similar experience when cross over between the sandpack version and the codesanbox website
- I'm curious, are there any pros & con's that come to mind when it comes to choosing codemirror vs monaco-editor? Was also curious about why you chose codemirror over vscode for prisma/text-editors 
  - Just to add a little bit of context, the current difficulties we had facing is a little bit out of scope, the main trouble we had is the setup of typescript's language server.
  - The Monaco editor is able to generate autocomplete based on the provided and customized d.ts files relatively easy but not for .tsx | .ts files, 
  - so for those packages written in `.tsx` by default, I cannot find an easy way to auto generate d.ts files and bundle them for the Monaco editor.
  - In term of UI/UX, as long as we are able to setup the environment and get the hint from the typescript server stably, it's just a matter of time to improve them gradually.
  - In fact, using CodeMirror in this case leave a lot of flexibilities to users to craft their own hint UI
- Although I wasn't here when this decision of CodeMirror over Monaco was made, I think I can understand some of the reasons and highlight them here:
  - Mobile support: Monaco doesn't have great mobile support, and this is crucial for Sandpack to deliver a uniform experience throughout all types of devices; 
  - Final bundle size: CodeMirror provides an easy way to load only the modules/extensions we want to, which gives us the possibility to lazy-loading and code-splitting the CodeEditor component. Meanwhile, Monaco is a heavy package, and that's why CodeSandbox.io/CodeSandbox Embeds also defaults to CodeMirror in the mobile version (due to the previous reason too
  - Extensibility: TBH, I haven't had many experiences with Monaco before, but I can tell what I've heard, and Monaco makes it hard to customize and extend some configuration - and Monaco provides a great API to extensions, which pretty much solved many of our problems; 
  - Plus, Sandpack is designed to be extensible and provide a basic (but powerful) development experience, so the initial goal was never to support any language server by default but to provide ways (API, documentation, support) for the application consumer (you) implement it by yourself.
  - In fact, you can easily switch from CodeMirror to Monaco at your end, as Sandpack exposes all the APIs needed to implement it. 

- I think Danilo nailed the reasons I also considered when I picked CodeMirror over Monaco. For me personally, the biggest one was extensibility, because we had very specific interactions in mind, and I wasn't very confident that Monaco would let me build some of them. This is more of a matter of taste, but I also preferred CodeMirror's API over Monaco's (plus CodeMirror's source code seemed a lot more approachable), so I went with it for prisma/text-editors.
# discuss-alternatives-stackblitz/replit
- ## 

- ## 

- ## [Repl from Repo | Hacker News _201912](https://news.ycombinator.com/item?id=21765872)
- Gitpod is awesome and a really bright team behind it. However, Repl.it is different in that we're focused on speed and minimal configuration. You don't even need to login to clone a repo and start it.

- Will this change the pricing model at all? Or add a new tier? 
  - No, not at all. Our infra costs are a lot less than most people expect.
# discuss-news-csb
- ## 

- ## 

- ## We've hit the point that more than 150 thousand new MicroVMs get created on a monthly basis!
- https://twitter.com/CompuIves/status/1788888447119225192
  - The cost stays low thanks to VM cloning & snapshot/resume. 
  - I'm writing a new post about how our memory (de)compression works, might as well become a series now

- ## We’re thrilled to announce our Storybook add-on: making every story come to life 
- https://twitter.com/codesandbox/status/1788205375189025090
  - Open any story as a Sandbox with a click

- ## Over the past months we've received a lot of feedback about our pricing, and today we're updating the pricing of CodeSandbox to make public sandboxes free again!
- https://twitter.com/CompuIves/status/1788596561032937720
  - From today, our free plans will include:
  - Unlimited public sandboxes
  - 5 private sandboxes
  - Private npm support
  - Our most important goal is to make coding more accessible, so we decided to remove that friction.

- ## Introducing CodeSandbox CDE: instant cloud development environments _202401
- https://twitter.com/codesandbox/status/1752368702878527776
  - Run every branch in a powerful VM
  - Resume & fork in 2 seconds
  - Collaborative 24/7
  - Available now with usage-based billing
  - DevContainer support
  - VS Code, AI code auto-complete, automated git flow & more
  - [Introducing CodeSandbox CDE - CodeSandbox _202401](https://codesandbox.io/blog/introducing-codesandbox-cde)
- I think you guys are changing the game with this one, it is a step towards remote programming and who knows maybe sooner than later your service will play a huge role in the big playing field.

# discuss
- ## 

- ## 

- ## wrote about @ValDotTown 's runtime, which we've rewritten three times in the last year because sandboxing untrusted code is a hard problem
- https://twitter.com/tmcw/status/1755616125474504960
  - [The first four Val Town runtimes _202402](https://blog.val.town/blog/first-four-val-town-runtimes/)
  - Val Town is a social website to write and deploy TypeScript. Build APIs and schedule functions from your browser.
- Nice overview! For https://skybear.net (runs user-provided Hurl/cUrl scripts) I ended up using AWS Lambda without IAM permissions given to it. Isolation from my application servers, no credentials issue and they can break whatever they want there.

- ## my course platform has a custom sandbox (built using Sandpack) that automatically persists any edits to my database, and restores them when the lesson is revisited.
- https://twitter.com/JoshWComeau/status/1749075678379626683
  - I just saw that the DB contains 285, 000 saved snippets, over 1GB of code!
  - originally, saved edits were stored in localStorage. Migrated to this solution maybe a year ago, since people noticed that their work wasn't following them from device to device.

- ## Are there any good sandboxes for Rails apps that let you also run docker containers?
- https://twitter.com/RogersKonnor/status/1747415376768487822
  - Why docker containers (more specifically docker-compose)? Because I use it to start a MinIO container to be able to simulate direct uploads locally.
- You could accomplish that with Codespaces for sure. Everyone gets a free amount of Codespaces usage every month, so this would be available to everyone with a GitHub account.
- gitpod can handle docker/rails pretty easily

- ## I don't really understand this upcoming @codesandbox pricing/plans updates _20240116
- https://twitter.com/tomlienard/status/1747267455767150641
  - Sandboxes runs in the browser, they're not using any cloud RAM/CPU resources (these are Devboxes), why limit them to 20?

- I want to like CodeSandbox because I know how hard they’re working and innovating. But this change might require me to move away from them, and I’m not happy about that
