---
title: thread-devtools-browser-chrome
tags: [browser, chrome, devtools]
created: 2023-02-20T19:40:49.993Z
modified: 2023-02-20T19:41:08.506Z
---

# thread-devtools-browser-chrome

# guide

# dev-xp
- 调试浮窗如tooltip/dialog的技巧， devtools > rendering > emulate a focused page
  - inspect浮窗元素时，ctrl+shift+p 搜索 disable javascript
# resources
- [Chrome DevTools Protocol](https://chromedevtools.github.io/devtools-protocol/)
  - The Chrome DevTools Protocol allows for tools to instrument, inspect, debug and profile Chromium, Chrome and other Blink-based browsers.
  - Instrumentation is divided into a number of domains (DOM, Debugger, Network etc.). Each domain defines a number of commands it supports and events it generates. 
  - Both commands and events are serialized JSON objects of a fixed structure.

- chrome://dino/
  - chrome://network-error/-106
# discuss-stars
- ## 

- ## 

- ## 

- ## [不允许打开开发者工具？我偏要 ](https://linux.do/t/topic/115760)
  - 首先发现网站屏蔽了 F12、右键等打开开发者工具的快捷键，使用浏览器的更多工具可破
  - 打开之后发现当前页面会跳转到另一个禁止打开 dev tool 的页面，然后原来页面的内容清空掉了。通过 Initiator 分析一下请求链，发现是通过 app-XXXX.js 调用的。
  - 通过浏览器直接请求 js 资源，拿到之后进行格式化，方便静态分析。
  - 通过搜索 devtool，发现有一段这样的代码，看到了一个 GitHub 相关的链接，点开看了一下，是个开源的禁用浏览器打开开发者工具的一个仓库。到这里的话其实可以搜一下这个项目看下怎么破解了，不过我选择简单暴力的方式：直接把这段注释了。
  - 这里通过浏览器的功能，直接重写响应，记得保存。改的时候发现还有一个清空控制台的设置项，一并注了

- https://github.com/theajack/disable-devtool /MIT/ts
  - Disable web developer tools from the f12 button, right-click and browser menu

- 尊重公益大佬，这贴的意思就只是说靠前端防不住这个，做好后端限制吧

- 安全方面还是得在后端做，前端能防的实在有限

- GoAmzAI 授权 2400 定制5000+

- 只禁止请求 disable-devtool/404.html 这个 url

- 一样的，先打开控制台，记得勾选上 Preserve log，就能看到是怎样跳转的白页了
  - 控制台勾一下 Preserve log，不然跳转新页面，原来页面的请求都会被清掉

- 首先 firefox 不好防护这个。 我有个想法，那油猴注入一遍，强制开
- firefox 拦截请求 简单快捷

- 可以先开一个空白页，并打开控制台，再输入地址。

- 在浏览器直接打开这个 js 地址，然后再重写, 因为原来的那个请求在跳转之后会被清空，直接打开 js 不会清空

- 有个工具叫抓包软件，直接挂代理抓包就完了，比这个省事多了

- 看看浏览器上面，地址栏下面是不是让你授权本地文件夹的访问权限。这个重写会保存一份 js 文件到本地，然后请求这个网站时候，不走网站返回的 js，直接取本地的 js。
- 无限 debugger 使用类似的方法 [JS 逆向：常见无限 Debugger 以及绕过方法 - 腾讯云开发者社区 - 腾讯云] （抓包过滤，重写内容，覆盖方法），js 代码混淆和控制流 都是 AST 转换后进行替换和修改实现。

- ## New in @ChromeDevTools : Accurately emulate CPU performance of a low/mid tier phone with Automatic CPU throttling calibration
- https://x.com/addyosmani/status/1893201558952911200
  - This feature calculates slow-downs for your specific device. Wanted this for years! We just shipped it.

- I’ve been fiddling around with emulators and more for years to build in scope of multiple browsers and device and bandwidth. Nice update ifykyk

- Cool. Now can you add memory limiting as well? It'd be a very cool feature
- cool for QA and testing

- ## 推荐一个可自托管的虚拟浏览器，可以直接部署到一个VPS上，然后就可以实现团队间共享一个持久化Session的浏览器。
- https://x.com/Stephen4171127/status/1883559372204491156
- 试过了，卡顿很厉害。还不如vpn加windows虚拟机
- 这种用类似于novnc实现的浏览器项目都不是很好用，带宽和延迟一旦不够就会让整个界面都很卡，甚至是完全不可用的地步
- aws的remote desktop考虑一下？

# discuss-net
- ## 

- ## We forked Chromium and bolted on a lock-free, zero-copy, low-latency shared memory ringbuffer written in Rust
- https://x.com/davidgu/status/2000608790836854925
  - We needed to IPC 100+ MB/s of raw video, and Chromium's WebSocket implementation is dreadfully inefficient
  - Recall is the API for meeting recording. We capture millions of hours of meetings per week, and process over 3 TiB/sec of raw video at our peak load.
  - We started out with a naive implementation using WebSockets on localhost, but our profile data showed that this was burning a ton of CPU cycles.
  - We read through the WebSocket RFC, and Chromium's WebSocket implementation, dug through our profile data, and discovered two primary causes of slowness:
- 1. Fragmentation
  - The WebSocket specification supports fragmenting messages. This is the process of splitting a large message across several WebSocket frames.
  - Looking into the Chromium WebSocket source code, messages larger than 131KB will be fragmented into multiple WebSocket frames.
  - A single 1080p raw video frame would be 1080 * 1920 * 1.5 = 3110.4 KB in size, and therefore Chromium's WebSocket implementation would fragment it into 24 separate WebSocket frames.
  - That's a lot of copying and duplicate work!
- 2. Masking
  - The WebSocket specification also mandates that data from client to server is masked.
  - This has security benefits, because it prevents a client from controlling the bytes that appear on the wire.
  - While this is great for security, the downside is masking the data means making an additional once-over pass over every byte sent over WebSocket -- insignificant for most web usages, but a meaningful amount of work when you're dealing with 100+ MB/s

- We knew we need to move away from WebSockets, so we began our quest to find a new mechanism to get data out of Chromium.
  - We realized pretty quickly that browser APIs are severely limited if we wanted something significantly more performant that WebSocket.
  - This meant we'd need to fork Chromium and implement something custom. But this also meant that the sky was the limit for how efficient we could get.
  - We considered 3 options: raw TCP/IP, Unix Domain Sockets, and Shared Memory.

- Could you bring that to puppeteer as well, they transmit screenshots from Chrome to the runner via websocket and it's a huge performance bottleneck in practice. I didn’t build any of the system, I just found out sending screenshots over was super slow.
  - That's really interesting. We previously ran puppeteer in the stack, too, and sent its screenshots to Rust over the FFI for telemetry.
- have you tried using the pipe transport (not sure specific terminology)
  - It uses stdout/in instead of websocket. It may still be a far cry from "highly performant". Playwright uses this by default, though it's usually slower (for other reasons)

- ## A web application can be choked by Chrome’s HTTP/1.1 six connection per host limit.
- https://x.com/hnasr/status/1886291288749908243
  - The browser creates a TCP connection to the HTTP server on port 443. As part of TLS, protocol negotiation happens which decides whether the communication should happen on HTTP/1.1 or HTTP/2, ( h1 or h2 for short). This is done through the ALPN TLS extension.
  - If the web server doesn’t support h2, (h2 isn’t not implemented or purposely disabled), the communication proceeds with h1.
  - Let us say an h1 frontend sending many concurrent requests. Each HTTP request is sent on a dedicated TCP h1 connection. 
  - No two concurrent h1 requests can use the same* TCP connection, the browser has to wait for the response to come back to send another request on the same connection.
  - Chrome and other browsers implemented an h1 connection pool per host and this limit is hard coded to 6.
  - With that limit, if the frontend sent 6 requests concurrently on 6 connections, the rest of subsequent requests get stalled and queued until a connection is available (a response was received). This leads to performance and latency issues.
  - Enabling h2 can of course help alleviate this because you essentially are no longer chocked by the h1 pool limit, you would have one TCP connection but create new stream for each request or reuse existing available streams. There is a max stream limit of course as well but its high (I think 250 is the default)
  - However enabling h2 isn’t free, it comes with an extra cost on the backend, especially that h2 processing is more cpu and memory intensive compared to simple h1 because of the additional h2 frame processing.

- ## [HTTP simultaneous connections per host limit... are per tab, browser instance or global? - Stack Overflow](https://stackoverflow.com/questions/22866552/http-simultaneous-connections-per-host-limit-are-per-tab-browser-instance-or)
- I use EVENTSOURCE API to open a persistent http connection.
  - HTTP/1.1: I could open 6 connections in one browser alone (by looping EVENTSOURCE 6 times) or by having 6 tabs open with one EVENTSOURCE I could open 6 new connections with incognito chrome on the same machine.
  - HTTP/2: more than 20 [in theory they say its 100] i did not try.

- I have read in various forums where people have problems with SSEs when more than x tabs are open (I think 6 in chrome), and this is because browsers limit the number of simultaneous connections to a single ip address.
  - This, however is not the same for Server Side Events (SSEs or eventsource() )

- ## 💡 [Max parallel HTTP connections in a browser? - Stack Overflow](https://stackoverflow.com/questions/985431/max-parallel-http-connections-in-a-browser)
- The first value is `ConnectionsPerHostname` and the second value is `MaxConnections` .
  - `ConnectionsPerHostname` is the maximum number of concurrent HTTP requests that browsers will make to the same domain.
  - To increase the number of concurrent connections, one can host resources (e.g. images) in different domains. However, you cannot exceed `MaxConnections` , the maximum number of connections a browser will open in total - across all domains.
- Host and domain are completely different. `ConnectionsPerHostname` means per subdomain. So if there are 2 sub domains it uses additional connections.if no subdomain then it means per domain.

# discuss-news
- ## 

- ## 

- ## 

- ## [What's new in DevTools, Chrome 139  |  Blog  |  Chrome for Developers _20250722](https://developer.chrome.com/blog/new-in-devtools-139)
- To provide additional visual context to your prompts, you can now not only take automatic screenshots but also upload arbitrary images to your chats with Gemini in the AI assistance panel.
  - 👀 注意大陆地区不支持此feature

- In the Network panel, you can now right-click a column name in the requests table and select multiple `request headers` to add them as columns.
# discuss-headless-browser
- ## 

- ## 

- ## 

- ## [服务器运行浏览器怎么优化内存占用 - LINUX DO _202606](https://linux.do/t/topic/2305122)
  - 我的服务器里跑了那个 Chromium。然后现在内存占用还是比较大，有什么优化的办法吗？是无头。或者是有没有什么替代的方案？因为我现在是需要，就是开一个浏览器来执行任务。或者是说能不能进行一些内存上的优化？现在动辄大几百 mb 小鸡吃不消 
  - 因为我在做一个自动化流程，纯协议过不了 cf 盾，如果开浏览器的话，自己就过了，所以说才让小鸡上跑浏览器
  - 有什么Chromium的简洁替代品，我用了以下两个，都无法正常运行：
  - Obscura（Rust 编写）：专为 AI agents 和 scraping 设计，声称 ~30-70MB 内存、80ms 左右加载，支持真实 V8 JS 执行和 Chrome DevTools Protocol (CDP)，可作为 Puppeteer/Playwright drop-in 替代（几乎零代码改动）。
  - Lightpanda（Zig 编写）：已有多组基准，25 并发任务时 ~123-215MB vs Chrome 2GB+（部分实测约 4x 优势，非总能达宣传的 16x）。同样 CDP 兼容，适合高并发 agent/自动化。仍在快速迭代，兼容性需验证。

- 那么其实不一定非要启动完整的浏览器引擎， 盾主要检测的是TLS指纹和HTTP/2指纹。如果你就是要保留现有的Chromium架构，可以通过追加启动参数来关闭非核心的一些功能。

```sh
--headless
--disable-gpu
--disable-software-rasterizer
--disable-dev-shm-usage
--no-sandbox
--disable-background-networking
--disable-extensions
--disable-sync
--mute-audio
--blink-settings=imagesEnabled=false
--js-flags="--max-old-space-size=128"
```

- WebSocket(WSS)升级失败报403，上下文断层问题。
  - 1、浏览器的真实行为，当你在Chromium中通过CF验证并建立会话后，随后的WSS连接大概率是复用了之前与CF边缘节点建立的那个底层的TCP/TLS连接
  - 2、你的在请求HTTP API时用了一个连接，而在发起WSS时，应该是发起了一个全新的TCP连接。对于CF，这个新连接没有经历过之前的上下文，所以即使你带上了Cookie和Token，依然会被判定为高风险机器行为直接403
  - 最简单的方法将过盾和长连接保持拆分开，使用FlareSolverr或远程代理，要不就小鸡纯协议直连。
  - 尝试Golang。使用cycletls（伪造 JA3）配合底层的连接池管理，强制WSS和之前的HTTP API 请求复用同一个底层的TCP/TLS Connection
  - 服务器装个codex，就给你搞定了哈哈，开玩笑

- 过cf盾关键在于 `cf_clearance` 这个cookie，其实你只要拿到能过盾的cookie, 后面就不需要浏览器了，request都替换成带这个cookie就行。当然这个cookie一段时间就会过期，不过那是之后的事情了。

- 我建议哈，既然NetLog⁠都在手里了，你可以直接把Chromium成功的WSS Client Hello⁠包和HTTP请求头跟你脚本发出的包进行字节级的对比，重点看一下密码套件、扩展和HTTP头顺序
  - 然后就是你现在发起WSS连接的是哪一个具体的库，判断一下是不是第一个TLS导致的割裂
# discuss-fingerprint/指纹浏览器
- ## 

- ## 

- ## 

- ## 

- ## [吐槽roxybrowser - LINUX DO _202606](https://linux.do/t/topic/2286343)
  - 开机自动启动
  - “强制”更新
- 还他妈的时不时要重新登录，也是醉了

- virtual browser挺好用的，roxy虽然功能挺多但是每次都更新太麻烦了

- ## [你敢信，浏览器需要实名认证 - LINUX DO _202605](https://linux.do/t/topic/2259725)
- 什么是指纹浏览器？对于Chrome来说的优势是什么？
  - 指纹浏览器就是多开呀，不被对方网站判定是一个人，电商可以开多个店之类的，不容易被封，底层基本也是谷歌浏览器开源版搞的

- 用这种指纹浏览器的，电商欺诈的比例比普通浏览器高几个数量级都不止。开发商不想担风险，触犯“帮信罪”。所以一刀切，先实名再说。

- Canvas指纹之类的隐私模式下面生成的还是同一个。 GPT没用这个策略，应该是风控等级还没那么高。一般是跟钱有关的银行、电商、广告、支付这类的会用。

- ## 🧩 [指纹浏览器全方案对比：10 款商业 + 7 款开源 - LINUX DO _202605](https://linux.do/t/topic/2271548)
  - [指纹浏览器全方案对比（2026.05） | Hanchen's Wiki _202605](https://docs.20020519.xyz/books/68554/page/202605)
- 指纹浏览器（Anti-Detect Browser）通过修改浏览器指纹参数（Canvas、WebGL、AudioContext、UA、时区、分辨率、字体等），为每个浏览器环境创建独立的"身份"，让网站认为是不同设备在访问。
- 核心用途：
  - 跨境电商多账号管理（Amazon、Shopify）
  - 海外社媒矩阵运营（Facebook、Google Ads）
  - AI 账号多开防降智（GPT Plus 共享）
  - 批量注册服务（Gmail、GitHub、Outlook）
  - Web3 空投/撸毛

- Donut Browser
  - 开源双引擎，免费无限本地 Profile；
  - CDP 需 Pro $29/月
  - 内核：Chromium（Wayfern，闭源）+ Firefox（Camoufox，开源）双引擎
  - 无限本地 Profile、指纹隔离（100+参数）、每 Profile 独立代理 + WireGuard VPN、Cookie/扩展管理、REST API + MCP 服务器
  - 优点：完全免费无限 Profile、双引擎（Chromium+Firefox）、零注册零遥测、MCP 支持可给 AI Agent 用、WireGuard per-Profile VPN 独一无二
  - 缺点：项目仅 1 年、单人维护、Wayfern 引擎闭源、指纹深度检测（pixelscan/iphey）不通过、L 站零用户反馈、CDP 需 Pro $29/月
  - [Is it anti-detect or just a profile manager · zhom/donutbrowser · Discussion _202511](https://github.com/zhom/donutbrowser/discussions/133)
    - Do you have any plans to extend the anti-detect features to at least one of the Chromium-based browsers? Maybe you could look into adryfish/fingerprint-chromium ultrafunkamsterdam/undetected-chromedriver
    - I do have plans to add support for a Chromium-based browser, but it is time-consuming. fingerprint-chromium is not really open source and the author does not provide binaries for all platforms that I support. undetected-chromedriver is only good for one chromium instance on one machine as it is only good for avoiding bot detection, not for changing the fingerprint.

- RoxyBrowser — 少数支持Linux的商业方案之一
  - 前身：LumiBrowser（2024），2025年初改名 Roxy 重新出发
  - 平台：Windows / macOS / Linux（2025.12 上线，AUR 有包）
  - 功能：指纹隔离、免费API（兼容 Selenium/Puppeteer）、代理管理、团队协作、Roxy AI Agent（自然语言驱动多窗口自动化）
  - 优点：少数支持 Linux 的商业方案、API 免费且好用（Python + DrissionPage 自动化丝滑）、同 IP 下比 AdsPower 更快、官方在 L 站活跃反馈响应快
  - 缺点：小团队、从免费转收费引发不满、2026.4 回收站“永久保留”改 30 天自动删除事件（官方道歉后恢复原政策）、内置代理合作商 PrivateProxy 质量差（谷歌撞人机）、多端登录互踢

- 等大佬vibe一个完整开源的指纹浏览器吧，闭源商业的说实话不敢用，密码还是很重要的

- 一直感觉除非是有多账号需要做隔离（比如批量注册新号，批量登陆账号，这种确实需要），否则没必要上指纹浏览器，自己的浏览器chrome/brave等就已经带有标准的浏览器指纹了，时区之类的也可以直接在系统里改。
  - 一般是那种电商、TikTok等等这些需要
# discuss
- ## 

- ## 

- ## 

- ## boss 直聘打开了F12，检测一会儿就把页面关了，也是牛逼
- https://x.com/0xdeusyu/status/2033403504514212073
- 现在web能爬很少，限制挺大。搞他Android端能搞的多。不多搞几个号，很容易限权。android端过掉yidun和geetest3风控层还有指纹层拿jd 3000左右会触发账号限权。这些都是有窗口上限，相对而言，安卓端窗口更大。

- 现在连复制都不让复制了

- ## 突然发现 Chrome 当中还有个测试水印的页面，各位知道这个页面有什么用吗？
- https://x.com/vikingmute/status/2022556076156293564
  - chrome://watermark/
- 这个功能对于个人用户没什么用，企业级使用场景，可以通过策略开启它，主要就是数据防止泄露和溯源用的。

- ## 原来在开发者工具里面勾选「仅限选定的上下文」就可以隐藏掉各种插件打印出来的日志，还你一个清爽的日志！
- https://x.com/luoling8192/status/1993686847663313195
- 怎么屏蔽插件的请求呢

- ## If you ever do UI debugging in Chromium go and enable this setting right away, it will make your life so much easier. 
- https://x.com/tommoor/status/1877390846665830867
  - Clicking into devtools will no longer cause the page to lose focus.
  - Also accessible via cmd+shift+p

- ## Tip: Chrome DevTools can override the content of Fetch/XHR requests! 
- https://x.com/addyosmani/status/1873479196829467123
  - Useful for mocking APIs without waiting on backend changes.
- I was looking into this a few weeks ago. It's a great feature! However, we ended up going with https://requestly.com. Mostly because of share-ability of mocks across the team.

- please… add server-side validations. Do not rely solely on the client. If your application is a Single Page Application (SPA) and does not use or implement any form of server-side rendering, users may experience unexpected behaviors using this new tool.

- I use this to activate chrome extensions that have failed API calls

- Does it works for any kind of requests? Like for CSS or JS
  - Yes! You can use Chrome DevTools’ Local Overrides to replace or modify CSS and JS files as well. Just enable overrides, make your edits, and reload the page to see the changes applied in real time. Super handy for front-end tweaks

- ## Uncaught (in promise) Error: Could not establish connection. Receiving end does not exist.
- 经排查是过期扩展的问题， 定位到是 z-context 导致的，disable掉就让异常信息消失了

- ## In Chrome/Firefox, when debugging memory leaks, you can click a “Collect Garbage” button to run a garbage collector. 
- https://twitter.com/iamakulov/status/1737065367657382118
  - (In Chrome, you do it in DevTools→Memory; in Firefox, in about:memory.)
  - I spent *a year* thinking Safari doesn’t have such button. It’s in the console

- ## TIL Safari DevTools have a “Type Profiler”, which shows types the engine inferred for each JS variable 
- https://twitter.com/iamakulov/status/1736702980374893040
  - Not sure why or when this can be useful in practice, but looks like a cool gimmick!

- ## Chrome 推出的 Record & Replay 的能力_202308
- https://twitter.com/Barret_China/status/1692077606567625086
  - 利用它可以将操作者在 Chrome 的行为路径 Record 下来，然后使用 Replay 进行浏览器层面的回放，记录包括页面跳转、内容输入、点击、鼠标移动等等。
  - 它的使用场景在于 UI Automation 测试，可以深度解耦质量和研发的工作，只需要在测试环节打开 Record 能力，就可以生成一个通过 JSON 来描述的用户操作路径文件，在业务后期发布时，再利用 Replay 进行回放
  - Chrome 自身可以根据每个 JSON 文件导出一个无头浏览器的自动化执行脚本，此外，Puppeteer 也推出了针对 Replay 的工具库

- ## [How To Inspect Interactions In The Browser](https://www.builder.io/blog/inspect-interactions-in-the-browser)

- I can't believe I just learnt that Chrome lets you:
  - Emulate focus so you can click freely in devtools
  - add debugging for when HTML subtrees change
  - https://twitter.com/samijaber_/status/1625258927888732161

- Solution #1: Emulate Focus Page
  - devtools > show rendering > emulate focus
  - 勾选后，需要在页面触发focus，比如输入下拉框
- Solution #2: Break On Subtree Modifications
