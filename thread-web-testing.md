---
title: thread-web-testing-debug
tags: [debug, testing, thread, web]
created: 2021-08-28T11:48:45.381Z
modified: 2021-08-28T11:49:05.730Z
---

# thread-web-testing-debug

# guide

## 测试文件的位置

- 单独的顶层文件夹
  - prosemirror
  - tiptap

- 单独的src下文件夹
  - lexical
  - vscode

- 和源码放在一起
# discuss
- ## 

- ## 

- ## Tip: @ChromeDevTools can now override the content of Fetch/XHR requests! Great for mocking APIs without waiting on backend changes!
- https://twitter.com/addyosmani/status/1691833832817967315
  - more in Chrome 117_202308

- ## 发现 zod-mock 很好用，我以前都是手动维护 mock-data，虽然有 GitHub Copilot 帮助也不算麻烦，但是还是会造成代码量增加。
- https://twitter.com/uptonking2/status/1681561542377230336
  - 我是一个坚信 less code less bug 的开发者，zod-mock 通过 zod schema 自动生成模拟数据的解决方案对于我来说很优雅

- ## would it be useful to replace all trivial random numbers in an app with seeded randomness instead, and then replace the seed with a random seed?
- https://twitter.com/steveruizok/status/1658736018063872001
- It's useful for replicating bugs found in testing, but it's a bad idea to actually test against the randomised value even if it's now deterministic, because that introduces a hidden dependency on test order
- automerge does that; can't tell if only for testing or has other utility
  - could be useful in tldraw too, since it lets developers pick which way new record ids e.g. right now i'm patching nanoid with uuid since my schema only accepts the latter for ids

- ## Nested `describe` blocks are bad!
- https://twitter.com/TkDodo/status/1619998044317192192
  - I've read this on Twitter some time ago already, but I only now get that it's true. 
  - Most devs want to append a test at the end, they don't look for existing describe blocks, so it becomes a mess for no reason. 
- The tests are already grouped by file. If you need extra context, just add it to the test name

- ## Chrome can dynamically insert console.logs without touching your code.
- https://twitter.com/marvinhagemeist/status/1527356830757933058
  - Just right-click on the line and choose "logpoint", enter the variables you want to log and hit Enter
- 💡 Pro-tip: instead of a logpoint for say `node` you can also use a conditional breakpoint with `console.trace(node)` as condition to achieve a logpoint that also includes the stack trace in the log message.

- ## Use npm pack to test your packages locally
- https://dev.to/scooperdev/use-npm-pack-to-test-your-packages-locally-486e
- First: Build your Package
  - Before you can use npm pack you must first build your package.
- Second: Locate your Build Artifacts package.json
  - The important part of this step is to run npm pack in the correct folder location where the build artifact package.json is located.
- Third: Pack you artifacts
  - npm pack --pack-destination ~
  - Now it is time to package our build artifacts to enable us to produce a package that mimic what would be published to npm. We tell npm to pack it to our user folder ~ for ease.
- Fourth: Point package.json to your file
  - "dependencies": {   "@ag-grid-community/angular": "file:~/ag-grid-community-angular-27.0.0.tgz" }
  - npm install
- Fifth: Test you package in your application

- ## One of the best ways a web developer can truly help make websites work the same in every browser is to help create more tests for WPT(Web Platform Tests). 
- https://twitter.com/TerribleMia/status/1431381473421049858
  - We all want interoperability. 
  - Testing is a way to get there, and not regress. 
  - But we need more tests written to check on more things.
- http://wpt.live has all the tests, live, in your browser
- http://wpt.fyi has a dashboard of the results in various browsers
