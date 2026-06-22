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
  - java

- 单独的src下文件夹
  - lexical
  - vscode

- 和源码放在一起
  - rust
# discuss-stars
- ## 

- ## 

- ## I learned this from @tan_stack query codebase: add a interface wrapper for builtin globals like setTimeout
- https://x.com/6onnykato/status/2003395932549972042
- You might like a concept called dependency injection. It is much straightforward and solider way than working with implicit dependencies.
  - +1 unfortunately, the dependency injection is largely overlooked in frontend development

- ## Some times you just gotta admit defeat. System tests -- the end-to-end variety that drive a headless browser -- just aren't worth the effort. 
- https://x.com/dhh/status/1892265453524803859
  - We'll bring back a minimal set for smoke testing, but rarely been happier to see 5, 000+ lines of code erased!
  - This was for Basecamp. We had already dropped them for HEY.
- We dropped our headless tests a while ago at @QuadraticHQ and moved to @QAWolfHQ they are awesome!
- Maintaining e2e tests was expensive in the pre-LLM era, but new frameworks like @octominddotdev promise to make it very cheap again

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [I’ve been auditing vibe-coded apps — here are the 8 things that break most often, all testable by you in an afternoon : r/vibecoding _202606](https://www.reddit.com/r/vibecoding/comments/1ub3yag/ive_been_auditing_vibecoded_apps_here_are_the_8/)
- If you built on Lovable, Bolt, Replit, or Base44 and you’re not technical, run these 8 checks before real users find the problems for you. None need a developer.
1. Open browser dev tools → Network tab, click around your app. If you see other users’ emails/IDs in the responses, anyone can read your whole user table. Most common issue I see.
2. Make two test users. Log in as A, copy a URL with their data, paste it while logged in as B. If B sees A’s stuff, your app has login but no ownership rules.
3. Trigger a Stripe refund. Does the user lose access? Usually not — most builds handle the checkout success path and ignore refunds, cancellations, and failed payments entirely. This is the #1 thing I end up fixing.
4. Kill your wifi mid-action and submit a form. White screen or infinite spinner = no error handling. Users in weak signal churn silently.
5. Search your AI chat history for “key” or “password.” Ever pasted a Stripe key or DB password to debug? Rotate every one — they’re sitting in a transcript.
6. Open it on an old Android. Works on your MacBook, chokes on a mid-range phone most of your users have.
7. Sort your workflows and look for duplicates. The reprompt loop creates two onboarding flows that double-fire emails.
8. Type /admin while logged out, then as a normal user. If anything loads, you have no role check.
- Pass all 8 and you’re ahead of ~90% of vibe-coded apps. 

- Claude is pretty good about recommendations to security and potential vulnerabilities as long as you prompt it properly

- ## ⚖️ Prediction: Deterministic Simulation Testing (DST) will completely change the way reliable software is written.
- https://x.com/LewisCTech/status/1916407192946938076
  - Given the same inputs, you get the same outputs, always. This part is deterministic.
  - TDD, manually writing example based tests on a hunch, is small and naive in comparison. DST is the future.

- Sounds like regular functional programming.
  - Definitely parallels. Some similarities to property based testing too. The difference is 1) local state manipulation is fine, because it's deterministic 2) you assert things internally 3) you make a program that drives the whole core, rather than testing individual functions

- ## Learn how to write end-to-end tests for AG Grid with Playwright
- https://x.com/ag_grid/status/1881357589633704223
  - Async data loading
  - Accessibility
  - [Writing E2E Tests for AG Grid React Tables with Playwright _202501](https://blog.ag-grid.com/writing-e2e-tests-for-ag-grid-react-tables-with-playwright/)

- ## 🔒 This is THE way to test any UI behind authentication. 
- https://x.com/kettanaito/status/1821828346780516619
  - Storing and loading any set of cookies in Playwright is so powerful. What we did in one of my previous projects was create a few different set of cookies based on different user roles, and used those as the input to the test suite.

- I have been using this feature for at least 2 years already. Impossible to do e2e without it

- Works great with auth! I wasn't able to make it work with 3rd party GDPR dialog, though, maybe because it's an `<iframe>` so perhaps not really possible… But storageState() is cool AF, I use it all around!

- ## Apisix looks pretty interesting. It builds on top of nginx and adds pretty much every feature you'd expect from a modern API gateway.
- https://twitter.com/ohmypy/status/1786687116937707703
  - And you can try it in the browser without installing anything!
  - Also, you'll definitely love it if you're into Lua

- ## it is interesting to watch how every project that adopts some form of simulation testing chooses to model the network using a completely different mental model (all equally valid)
- https://twitter.com/AlexMillerDB/status/1764136495429107729
  - FoundationDB: An RPC endpoint is just a stream of futures.
  - TigerBeetle: The network is just a bus of messages.
  - Cassandra: The network is a network.
  - Resonate: The network is actually a queue of requests and completions.

- ## Limitations of property based testing: wrote this transactional, in-memory index for looking up disk offsets. 
- https://x.com/LewisCTech/status/1802093559174353125
  - (think a multiplayer version of the KeyDir from bitcask).  Wrote it to have transaction semantics in mind. Tried to write a property test for it - either all writes succeed or the DB remains unchanged - and the test passed!
  - Except it only passed because I was unable to actually generate a valid key to be inserted. Meaning it never even gets modified. So I haven't actually tested the case I wanted to test - ie that nothing non-atomic happens.

- ## I may have been wrong about property based testing.
- https://twitter.com/LewisCTech/status/1752061962681553170
  - Love it in theory. But every library I've used has been complicated and confusing. Which  suggests it's just a complicated and confusing thing to implement.

- ## Is there a good utility for testing a project against multiple versions of its npm dependencies?
- https://twitter.com/justinfagnani/status/1736795878823014603
  - I know how to do this manually, but I want something more automatic. I should work locally, and so that I could import the package to vary under its default name.
  - I say local just because GitHub CI and others have matrix features that don't work locally.
  - Usually I want to test against multiple versions of a single package, like a bunch of typescript versions or rollup versions. I haven't had a need for a full matrix yet.

- @thoughtbot has something like this in Ruby land called "appraisal"

- Ember try is potentially generic enough

- ## 🆚️ Which type of automated test do you find most valuable?
- https://twitter.com/housecor/status/1729516522786226192
  - unit : integration : end2end = 0.31 : 0.29 : 0.4
- My answer? End-to-end. Why? Because it's the only type of test that proves the system works.
  - E2E tests are slower. 
  - They can be hard to write in a reliable manner.
  - They're often brittle due to data changes, network issues, environment churn, etc.
  - But E2E tests are the only type of test that gives me complete confidence that the feature actually works.

- Unit tests are more valuable for library authors to verify the full API
  - For production applications E2E instead

- Although it can be the slowest I think E2E tests provide the most comprehensive coverage. All three types are important, but if you make me pick I’ll go with E2E. Solutions like Cypress and Playwright have made the E2E journey more enjoyable nowadays.

- If you have good end-to-end tests you don't need the rest.

- e2e will kinda test both unit and integration. But you have to finish almost the whole system for this to implement. If you want to test while developing, unit and integration is better. But I would prefer e2e.

- ## Found out today that `userEvent.type` is pretty slow because it types each char separately, causing a rerender every time 
- https://twitter.com/tsirlucas/status/1718374050408333671
  - Depending on whats running on rerender, it can be slow 
  - Debounce is usually disabled on testing env for perf reasons 
  - This is local, can you imagine on CI?
- [Performance issues with `userEvent.type()` · testing-library/user-event](https://github.com/testing-library/user-event/issues/577)
  - Sometimes is till worth it for you to type each char, but most of times you should be fine with just pasting like I did

- ## 🗒️ Explaining 9 types of API testing. 
- https://twitter.com/alexxubyte/status/1718297723177402400
  - https://twitter.com/alexxubyte/status/1751265300446908506

- ## 💡 I dislike JSDOM. It runs in Node, pretends to be a browser, but is intentionally neither. It's a hack.
- https://twitter.com/kettanaito/status/1717085912545247557
  - Test browser things in the browser. There's no excuse not to use Playwright in 2023.
- Why do I say it's neither? Because it explicitly strips away Node.js globals, like TextEncoder or Fetch or Headers, and then manually re-adds them. That's the reason it still lacks global fetch although it's been more than a year that Node ships with it.
  - Here's what baffles me the most: when you run a test in Node.js 20, which has global fetch, JSDOM won't give it to you. It will throw. 

- How would you test a library with Playwright? I've come up with solutions before, but they are always hacky.
  - You create a test environment for it that resembles the library's usage and test it there. This approach composes 90% of MSW tests. Real browser, real usage example, a bit of testing setup to make it work with less noise in tests themselves.

- Agree, I've spent more time trying to figure out hidden quirks of JSDOM than writing the actual tests. Overall it's just the most hacky way to test UIs.

- https://twitter.com/mjackson/status/1717206924343869481
  - Strong agree. JSDOM was built for a world without playwright. But playwright is so good, there’s really no reason to use JSDOM anymore.

- ## You're testing the business logic of your database-backed application. 
- https://twitter.com/gunnarmorling/status/1705025130953580799
  - For your DAOs (if you have any), do you mock them (e.g. with Mockito), manually create fake implementations (e.g. based on collections), or keep them as-is (e.g. using Testcontainers to spin up a DB)?

- I avoid mocks. I try to implement the complex business logic in a functional style. If it heavily relies on the database I use a real database most often with Testcontainers
  - +1. with spring boot + postgresql I run tests on real database. one should not ignore existing data and it’s impact in test suite.

- All. 
  - Mocks for simple unit tests which test all the code flows combinations.
  - Integration tests with real db to check the main flows end to end. 
  - Testcontainers for something in between. Or when it is hard to make the mocks.

- IMHO the coolest thing about using Event Sourcing is exactly this: you have a write model with your business rules. 
  - And all you have to write to your database: events. 
  - So unit tests for your model (persistence agnostic) and integration/ e2e tests for the whole thing.

- Depends what do you need to test. If it is a DAO containing query and logic I will go for an integration test with these container
- Started with mocks, found that there are too many edge cases that get missed. Switched to an in-memory fake implementation that is fast and simulates the DB layer well enough to catch any serialization issues. Integration smoke tests that hit each API with real payload.

- ## 将本地开发的 localhost:3000 映射到一个具体网址(还要带 https)有什么办法
- https://twitter.com/vikingmute/status/1694539022125949393
  - 我之前都用的是 nginx，后来看到讨论中用的 Caddy
  - 自带 https，配置非常简单（比 nginx 简单多了）
- 其他的高赞一些方案：
  * Docker + Docker Compose + Traefik + Mkcert, 这里面的这个 mkcert，本地生成证书的， 可以收藏了
  * Localcan https://localcan.com，居然还有一个专门的 App，太神奇了
  * localtest, https://readme.localtest.me, 一个简单的小教程

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
