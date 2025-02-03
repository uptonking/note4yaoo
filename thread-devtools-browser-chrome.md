---
title: thread-devtools-browser-chrome
tags: [browser, chrome, devtools]
created: 2023-02-20T19:40:49.993Z
modified: 2023-02-20T19:41:08.506Z
---

# thread-devtools-browser-chrome

# guide

# discuss-stars
- ## 

- ## 推荐一个可自托管的虚拟浏览器，可以直接部署到一个VPS上，然后就可以实现团队间共享一个持久化Session的浏览器。
- https://x.com/Stephen4171127/status/1883559372204491156
- 试过了，卡顿很厉害。还不如vpn加windows虚拟机
- 这种用类似于novnc实现的浏览器项目都不是很好用，带宽和延迟一旦不够就会让整个界面都很卡，甚至是完全不可用的地步
- aws的remote desktop考虑一下？
# discuss-net
- ## 

- ## 

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

# discuss
- ## 

- ## 

- ## 

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
