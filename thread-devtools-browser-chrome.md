---
title: thread-devtools-browser-chrome
tags: [browser, chrome, devtools]
created: 2023-02-20T19:40:49.993Z
modified: 2023-02-20T19:41:08.506Z
---

# thread-devtools-browser-chrome

# guide

# discuss
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
