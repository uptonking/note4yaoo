---
title: thread-dev-engineering
tags: [dev, engineering, thread]
created: '2021-01-21T17:51:54.496Z'
modified: '2021-01-21T17:52:13.333Z'
---

# thread-dev-engineering

# guide

- ## 

- ## 

- ## 

- ## 

- ## 提高编程水平的一个高效的方式: 
- https://twitter.com/ivyliner/status/1519472859239923712
  01. 自己先写一个中等复杂度的项目(在写的时候自己会知道哪些地方写得不够好, 当然也会有不知道的地方) 
  02. 开始学习相关的知识, 看别人的代码
  03. 这时候你会意识到哦原来还能这样用,  嗯用这个 API 看起来更优雅, 我去还能这样写. ..
  整个过程自我会感觉到不断精进.

- 我个人最难的是代码边界控制。如何做到适当的业务上可扩展性和尽量缩小业务变更所带来的代码变更问题。

- ## peg.js 真不错，写各种parser很方便，语法的设计很简单而且非常符合直觉。 
- https://twitter.com/TooooooBug/status/1519158038883880960
  - 试了一下，从零基础开始，1个多小时就能写出简单的SQL parser了
- 可惜不维护了，不支持左递归

- ## This is the flowchart of how slack decides to send a notification. 
- https://twitter.com/alexxubyte/status/1514993500709863425

- ## One of my go-to software development tricks: Have 2 clones of the repo side by side
- https://twitter.com/andy_kelley/status/1504657645172449284
  - Implement the a feature the "safe" way in one of them without touching too much code
  - Simultaneously implement the same feature more daringly, refactoring aggressively in a fit of rage
  - Often you can ping-pong between the clones while waiting for builds or tests to run. And there's not really a context switch since it's the same feature.
  - And if the aggro one ends up being too deep of a rabbit hole, often you can still salvage *some* of the diff in your "safer" implementation.

- ## developers at different levels
- https://twitter.com/ZainRzv/status/1502550200396750851
- Junior engineer:
  - Take this tightly defined feature & build it
- Mid-level engineer:
  - Take this vaguely defined feature & build it
- Senior engineer:
  - Take this known problem & figure out how to solve it
- Staff engineer:
  - Take this goal & find the problems we should be solving

- ## TIL you can use "it.only" to run only one test at a time
- https://twitter.com/steveruizok/status/1496052781945397252

- ## One fact that was unknown to me before becoming an open source maintainer is: You have to really understand a contribution before accepting it, as _you_ have to maintain it.
- https://twitter.com/TkDodo/status/1487804403356680201
  - If I'm getting issues for a contribution made by someone else who is now unavailable, what am I gonna do?

- ## 代码中 state 和 status 区别：
- https://twitter.com/ThaddeusJiang/status/1444133176352247810
  * 有状态迁移关系：state，交通灯状态： red -> green -> yellow
  * 没有状态迁移关系：status，付款结果：success、failure
- Search vs. Query
  - Search：在未知的领域查找，比如搜索引擎的搜索 
  - Query：在已经确定的领域内超出某些特例，比如数据库的查询。

- ##  `<num value={123} />` vs `<num>123</num>` which style do you prefer?
- https://twitter.com/jarredsumner/status/1441923089382535173
- my opinion as a developer: `<number value={123} />` is better because it's clearer and there's no ambiguity of what the type is going to be

- ## XSS cheat sheet only with stuff that works in 2021!
- https://twitter.com/SamuelAnttila/status/1358822910526320640
  - [Cheatsheet: XSS that works in 2021](https://netsec.expert/posts/xss-in-2021/)
* Tons of  XSS filter bypasses!
* mXSS Sanitizer bypasses
* URL Schema filter tips
* MIME type exploitation
* Too much stuff to fit here!

- ## 以前经历过的编程模式有：
- https://www.v2ex.com/t/795043
  - Salary Oriented Programming
  - Lingdao Oriented Programming
  - Hongbao Oriented Programming

- ## The danger of open redirects!
- https://scotthelme.co.uk/the-danger-of-open-redirects/
  - 要防止被利用钓鱼
- The absolute first thing I do when I come across any phishing page is report it to Safe Browsing here, as you should too: https://safebrowsing.google.com/safebrowsing/report_general/
- The problem with having an open redirect like the one above is that it can, and will, be abused by attackers in scenarios like this. 
  - The reason these open redirects are useful is that they add legitimacy to the URL in the email itself which helps it to bypass spam filters.
- If an email provider were to check the domain reputation of homes4wiltshire.co.uk then it would come back as quite positive. It hasn't been flagged as being involved in any phishing/malware activity, it doesn't appear on any block lists
- This is what the attackers want to hide and is why the open redirect on a 'good' domain is so useful.

- ## the most valuable thing I've learned in my career isn't a specific skill, but instead the knowledge that "this will eventually work"
- https://twitter.com/Wattenberger/status/1433880202086600704
  - Projects can be seriously overwhelming when you're in the middle of them, but they almost always come together, and usually faster than you think!

- ## Working on open source while also having a full time job is exhausting and unsustainable. 
- https://twitter.com/devongovett/status/1389635869628256259
  - No wonder people are starting companies around this stuff!
- People expect so much for free and it’s not always easy to let that go and not feel bad about it.
- The open source, unfortunately, is on the verge of being broken by the big companies.
  - There has never been a better time for open source companies than now. Elastic is a billion dollar company.
  - the most popular ones are being bought by a limited number of companies. A very limited number.
  - Thankfully those projects maintainers have the ability to choose not to sell. But it begs the question: why do they?
- I've got some news for you. If you quit your job, you just have new problems and need to spend even more time doing things which are not coding.
- The problem is that the github platform promoted open source as free (non paid). 
  - And now everyone expects oss to be free labor, big corps are using software without funding or contributing while making millions. 
  - Getting paid shouldn't be an after thought.

# pieces
- ## 

- ## There is tension between fast startup times (AOT) and peak performance (JIT).
- https://twitter.com/jerrinot/status/1430165270631534602
  - Historically the peak performance was more important for server-side applications.
  - Cloud is changing it, at least partially, and people go a long way to improve startup times. 
- Some examples:
  01. Design brand new frameworks with great startup times as an explicit design goal.
  02. Give-up on some language/VM features we used to take for granted.
  03. Maintain a bunch of descriptors for the sake of a specific compiler.
  04. Extract JIT compiler into a separate process and run it as a network server.
  05. Switch to an entirely different language/ecosystem.
- Given all of the above, I wonder how come I don't hear about process snapshotting/checkpointing more.
- Something like Criu sounds like a good fit for "stateless business logic" - That's precisely the place where the fast startup times are most relevant. 
  - The idea is simple: Run a regular JVM, with JIT and everything. 
  - When you need to scale-out then do not start a new process from scratch. 
  - Instead, take a snapshot of an already running/warmed-up process/container and start its clone. 
  - Sure, there'll be many state-related issues.
- https://criu.org/Main_Page
  - Checkpoint/Restore In Userspace, or CRIU is a Linux software. 
  - It can freeze a running container (or an individual application) and checkpoint its state to disk. 
  - The data saved can be used to restore the application and run it exactly as it was during the time of the freeze.
- Yet I don't hear this approach to be discussed too much. I only saw one FOSDEM talk. What am I missing?
  - Native image tool in GraalVM is thought of AOT compiler for Java, but it has snapshotting capabilites. **You have to adapt your code to work with this** well, but maybe that's inherent requirement. Most code bases do not expect that they can be snapshotted.
- [Call for Discussion: New Project: CRaC](https://mail.openjdk.java.net/pipermail/discuss/2021-August/005941.html)

- ## App: Has 83 feature flags.
- https://twitter.com/markdalgleish/status/1429005039452835845
- I often like to think about feature flags in terms of “how many possible versions of this app exist”
  - 2^83 is well, not maintainable

- ## JavaScript build tools measure performance wrong. Roundtrip time — not build time — is what people feel.
- https://twitter.com/jarredsumner/status/1427891371797454851
- What is your definition of round-trip here?
  - For frontend development, that’s ideally how long from saving in your editor to the code refreshing in the page (either through hot reloading or the script loading) — a broader scope than transpilation time
- That makes sense. Incremental changes generally require fewer files to be rebuilt. So the build plays less of a role in that scenario.

- ## Oh God, I've worked with people who made the one function to rule them all. 
- https://twitter.com/BenLesh/status/1424379521525035010
  - The one component to rule them all. The one service to rule them all. Etc. 
  - And then when you finally break it up into tiny pieces, they're like "oh. yeah I guess that's simpler"
- I think the coolest thing about hooks is they get developers thinking like framework developers. Which is sort of weird but cool. "When this component renders, how do I trick it to wiring things up?" ... That's framework developer thinking, normally.

- ## After experimenting with multiple caching solutions and application frameworks to scale our inventory read layer, 
- https://twitter.com/dinquisitively/status/1419145128497737731
  - we finally proceeded to use Hazelcast with near cache support 
  - and Vert. X as this combination offered maximum performance for our use case.
  - [Scaling our inventory cache reads to 1000X](https://t.co/91nSO7NOtU?amp=1)

- ##  Always use profilers to identify performance issues in code. 
- https://twitter.com/d__raptis/status/1419611806557945859
  - I'd never find the problem otherwise.
- It's quite simple (for React at least) : 
  01. Use this Chrome plugin react-developer-tools 
  02. Click record
  03. Reproduce a laggy action
  04. Check which components/actions are time-consuming
- Now, you've located the issue and you need to check the code to find the real issue

- ## Syncing sign-in state
- https://www.tommoor.com/posts/syncing-signin-state
- Because Outline is primarily for writing documents, we see a use case where users keep many Outline tabs open containing different docs. 
  - Outline is built using MobX for state management. 
  - Local client state is split into multiple stores in the app, for example users, documents, auth. 
  - The auth store contains data related to authentication such as the current user and team – it also manages the persistence and subscriptions. 
- There are essentially three parts to this feature:
  - Syncing auth in MobX state to localStorage
  - Listening to localStorage changes
  - Updating local MobX state from received events

- ## TypeScript/VS Code tip: If you don’t see external type updates in your editor, try opening the changed .d.ts file. That usually refreshes things for me.
- https://twitter.com/rauschma/status/1417285626836160512
- There's also a "TypeScript: Restart TS Server" command that should work too.

- ## Is there a good CI/CD service that provides "visual diffs" of HTML? (and can plug into GitHub CI/CD checks?)
- https://twitter.com/choldgraf/status/1417385474272944152
- https://github.com/cburgmer/csscritic
  - CSS Critic closes the gap in front end testing and makes HTML & CSS testable

- ## Just curious: which package manager/CLI do you use? npm vs yarn vs yarn2 _202105
- https://twitter.com/JoshWComeau/status/1395044829013368846
- [Yarn 1 vs Yarn 2 vs NPM](https://shift.infinite.red/yarn-1-vs-yarn-2-vs-npm-a69ccf0229cd)
- pnpm is supposed to be very good, but since we focus on React Native, it's not an option for us.
  - Yarn 2 is almost an entirely different CLI altogether. I wish they'd just name it Berry (which is its code name) v1.
- I feel your article is misleading in two important aspects:
  01. Yarn 2+ supports React Native well with node_modules install scheme
  02. Yarn 2+ perfs are better or comparable to perfs of Yarn 1, both with default PnP installs and with node_modules installs
- I used to use yarn 1. After the acquisition of npm by GitHub I switched back to npm
- I use whatever the project already uses but use npm for anything I start. No real reason though

- ## Test accessibility with more than 1 tool and more than 1 method.
- https://twitter.com/jackdomleo7/status/1414468761860587520
- Accessibility testing tools:
  - Axe
  - Pa11y
  - WAVE
  - Tota11y
  - Chrome's Lighthouse
  - Firefox accessibility devtools
  - jest-a11y
  - Checka11y.css
- Accessibility testing methods:
  - Use a11y testing tools (see above)
  - Unplug mouse
  - Install a screenreader
  - Install a plugin/extension to mock colour blindness
  - Turn on high contrast mode
  - Turn off images
  - Turn off CSS (very useful for HTML structure)
  - Video captions

- ## I feel TDD is focused on backend/business logic, too dogmatic, and lack of clarity on how to test UIs/DOM.
- https://twitter.com/sebastienlorber/status/1414210224001622018
  - You are not allowed to write any production code unless it is to make a failing unit test pass
  - Visual diff tools like Chromatic are much more pragmatic.
  - I don't want to draw a png as my failing test.
  - Nor I want to manually edit a video of the desired animation.
  - testing frontend state/Redux/FSM is only a small part of all the things that can go wrong in a frontend app.
  - TDD should clarify when it can be applied successfully. In my opinion it's not 100% of the time
- I think TDD is more useful when interpreted as "write tests alongside production code code" and not as "write tests before production code".
  - Having a falling test gives you confidence the test is not a false positive, but you can make it fail after writing the production code.

- ## When I do a big refactor to a data structure I like to start by changing the type definitions. Then I fix the red squiggles until they're gone.
- https://twitter.com/kentcdodds/status/1413326124969459714
  - The joy of things *just working* when I finally run the code will never get old.
- This! I have done a few big retractors (~2000-5000 lines of code each) on my current project over the past 9 months without batting an eye. There's a correlation between the red squiggles being gone and the tests passing. TypeScript is the bomb! 
- This is the red-green-refactor cycle with typescript.
- With ts I have no problem on refactors covering tens of files, thousands of lines. 
  - It saved us from having to write a lot of test cases. 
  - More than that I find writing the interface first, I have a clear mental model of what I’m developing and all goes faster

- ## Polishing up a project for release is so much work. I feel like I’ve been working on “finishing” Parcel 2 for the last 6 months. Getting close though!
- https://twitter.com/devongovett/status/1412865291315417089
- Some recent things I've been working on:
  - Automatic module/nomodule
  - Support for reading tsconfig.json to configure JSX settings
  - API consistency
  - TypeScript definitions for public API
  - Improvements for web workers
  - Cache portability
  - Improved diagnostics
  - Lots of bugs
- The last 10% is always the longest half of the project

- ## how to adapt faster in a new squad and a new codebase?
- https://twitter.com/luizpn_/status/1412431905924993030
  - this is my first week working with a new squad and I feel so slow 
- Play with the features, once you understand how the product works you start to make more sense of the code. The rest like architectural decisions made you will pick up on the fly when doing tasks.
- In the beginning, it's normal to be slow. If your teammates help, you'll also learn faster. I'd put emphasis on learning the domain
  - Another great way to get familiar with some codebase is to write automated tests for it.
- Don't worry it's normal
  - First, demonstrate an interest in the project, be proactive, and ask questions. There will be someone that will value your energy and will want to help you
  - Do pair programming, read tests, read the whole code base, and try to understand the big picture

- ## What is the best approaches to provide an uniform API (it could be a function, endpoint or something else) when you have APIs that do the same thing but has different inputs and outputs?
- https://twitter.com/sseraphini/status/1412483649564561408
- I think doing this will just add more complexity, so I'd avoid this if users are devs. Else if they're clients, I'd do a good enough wrapper over the whole thing returning a Frankenstein
  - How would u do instead? Expose 100 different formats to end user?
  - I think a wrapper could work. Enforce the inputs and return an unified output if possible
- A wrapper that receives the "eigen inputs, " a switch case that calls those APIs, and a mapper to return the "eigen outputs."

- ## Open API
- https://twitter.com/peduarte/status/1407710813247389700
  · Flexible, composed, extensible 
  · Can still be abstracted at the app side
  · Use it when wanting to give users more control
- Closed API
  · Opinionated, strict, prop-driven
  · Can be simpler to learn
  · Use it when wanting to limit what users can do
- **They're both good**!
- I use both on a daily basis, I mean the second (UI preset) can be a shortcut for using the first (design system)

- ## I ported Chrome DevTools' inspector to Node.js
- https://twitter.com/privatenumbr/status/1407976142892580867
  - Just run `await inspect(object)` to inspect any value with an inline interactive CLI
  - Great for working with large & complex objects in Node without having to spin up a Chrome debugger

- ## Note: you can't write a test that depends on dynamic import in Jest because Jest runs your code in a vm and dynamic imports don't work in vm due to a Node bug.
- https://twitter.com/matthewcp/status/1407724050638594050
  - Another reason not to have your testing library be a runtime.
- I've used test-framework free solutions quite a few times. Generally they just involve a tiny assertions module, then each test is just a module that exports a test. The actual "test runner" would often just be a simple loop that goes through each test file and runs it.
  - The fact the test modules know nothing about how they'll be run does offer some nice flexibility, in particular it's very easy to whip up versions that run tests in browsers, in workers, or under other constraints.
  - The main drawback I've found is it can be kinda annoying to associate descriptions with tests, especially given it can be a lot easier to have multiple tests in a file. e.g. One thing I've done in the past is have object property names as test descriptions, which isn't ideal.

- ## As someone who ends up building a lot of architectural and infrastructure code, there's one thing I cannot emphasize enough: do the simplest thing that works. 
- https://twitter.com/promit_roy/status/1405912880663433223
  - Do not try to imagine future requirements, or support ill-defined potential use cases. 
  - It will always change later.
  - The problem is that the simplest thing that will work is dependent on how well you already understand the setting. 
  - There’s no single simplest possible approach, and they all differ on how easily they can be extended in different vectors.
- I used to do a lot of planning, and it always turned out to be a waste of time, and I'd have to rewrite large chunks anyway - either because the requirements changed, or because I didn't understand the problem until I actually wrote the code.
- I don't agree, trying the simplest solution will make it harder for you or anyone to extend
  - Yes, do simple things, but not the simplest. 

- ## One driver behind the 'lots of small packages' trend in JavaScript has been the desire to ship the minimal amount of code in web pages.
- https://twitter.com/MarijnJH/status/1397127566503419904
  - Have tree-shaking tools mooted that? Is there still a good point to be made against packages that include a bunch of stuff that many people won't need, as long as it's in a shape where unused code is easy to eliminate?
- Since tree-shaking has been adopted by @RollupJS, I've been shovelling(铲起；挖出) all utility functions that I use across projects into a single monorepo. 
  - Creating yet another package would mean that I'd abandon it at some point.
  - A monorepo forces me to keep it up to date
- I think another advantage of small packages is that all the relevant documentation can easily fit into the README. This makes it pretty straightforward for new contributors to properly document the stuff they add or change, which in turn leads to better documentation overall.
- No. I have found tree shaking to be unreliable when many exports are included in one module, and it is still best to have many small modules to get the best out of the shaker.

- ## has anyone tried both esbuild (or meta build systems like Vite that use it) side by side with Rome?
- https://twitter.com/devongovett/status/1390023696782221312
  - Does/can Rome approach esbuild's speed?
- https://github.com/alangpierce/sucrase
  - Sucrase is an alternative to Babel that allows super-fast development builds.
- vs
  - babel - mutable ast, plugins can mutate the ast, slow af
  - esbuild - immutable ast, filter/link file plugins, very fast
  - sucrase - immutable ast, no plugins, silly fast
- Sucrase doesn’t even have an AST at all. 
  - It manipulates the token stream as it parses. 
  - Much less flexible but skips full parse, ast pass, and codegen.
  - Also mutation itself isn’t the problem. 
  - It’s revisiting mutated nodes that increases complexity from linear to quadratic.
- Rome can get there for sure. sucrase (babel alternative written in TypeScript) is already faster than esbuild for some things.
  - The real bottleneck is multi-threading. 
  - Sucrase only wins slightly in single-threaded mode PLUS the trade-off of non-extensible AST treatment (by design).
  - Future dev machines likely come with 8+ cores and a flexible AST is required for Rome's intended scope.
  - Which is to say... using Sucrase as an example for "JS compilers can be fast if you design it right" isn't particularly accurate because (1) Sucrase is designed to take shortcuts by drastically reducing its scope. Sucrase and Babel are like apples and oranges.
  - And (2) you can't solve JS' inherent problem at multi-threading with compiler design.
- To be fair, ESBuild also takes a lot of the same shortcuts. 
  - No custom transform plugins means it reduces the number of AST passes but wouldn’t be scalable to something with the scope of Rome. 
  - Nothing wrong with being focused one one thing, but they are different approaches.
- Does swc take shortcuts too? If it is comparable to babel and still beats esbuild in performance benchmark, I am even more impressed.
  - It is very similar to babel. Everything is built in separate passes. Does not have quadratic behavior like Babel though.
- Parcel switches to swc (written in Rust) for massive perf boosts

- ## If you do integration tests you don't need to know if the app is using react, redux, redux-saga, or something else
- https://twitter.com/sseraphini/status/1389584078790352902
  - render the app to the DOM
  - interact with the DOM
  - assert the final state of the DOM
- if you refactor from redux to pure react, the test would still pass

- ## I don’t use fake data generators for testing. I prefer using a static dataset instead.
- https://twitter.com/housecor/status/1389386557648482308
  - Tests using local static data are reliable and fast.
  - I can enhance the dataset when I find edge cases.
  - I use the static dataset in mock APIs, unit/integration tests, and Storybook.
- Fake data can be useful for “Fuzz” testing (feeding the app a bunch of random data to see if it bombs), but that’s a separate conversation.
- I would use a faker library to generate useful datasets. Then store that json in a static, committed file.
- Overall I agree with the sentiment: tests should be deterministic. I don't want them to sometimes fail (or falsely pass) depending on randomly generated data; the code either works or it doesn't.
  - We sometimes use static data and sometimes a Faker generator, but with a static seed. Precisely to give us predictable tests. I find that the two versions behave the same in practice.
- For integration tests of components, I prefer to generate fake data 
  - and override parts of fake data with static data  when testing a particular scenario, so the focus on the data remains clear.

- ## If you do code split for each page of your application, you are denying the benefits of building a SPA.
- https://twitter.com/danieljpgo/status/1387149559315550211
- With webpack you can have an SPA with chunk splits dynamically imported to improve performance, and with react you can use suspense
  - Yes, but you will still have to download the bundle for each page, which will not deliver smooth navigation when using your application, which is one of the main features that the SPA brought.
  - render as you fetch solves this
- I would agree that many of us focus on code splitting routes over code splitting features. The latter thinking is more SPA like imo

- ## creating a javascript package is easy
- https://twitter.com/sseraphini/status/1094358825417797633
  - it should run on all node versions
  - it should run both on node and browser
  - it should works on SSR
  - it should works on pure js, typescript and so on
  - it should have lint, prettier setup
  - it should have autorelease process
  - it should work on both react web and react native
  - it should work across frameworks: angular/react/vue
  - it should provide hooks api
  - it should work with webpack, parcel, metro bundler
  - it should cover 100% of edge cases
  - it should have docs and a good readme
  - it should be blazing fast
  - it should have blog posts
  - it should be incrementally adopted
  - it should have tests
  - it should have/provide types
  - it should work on npm, yarn
  - it should have a great logo
  - it should have a changelog

- ## How can I generate a tree, starting from a component to see where it is being used? like A is used in B and C, and D uses B and C
- https://twitter.com/lucasleandrodev/status/1385617694653882370
- [How to easily visualize a project's dependency graph with dependency-cruiser](https://www.netlify.com/blog/2018/08/23/how-to-easily-visualize-a-projects-dependency-graph-with-dependency-cruiser/)
- https://github.com/pahen/madge
  - Create graphs from your CommonJS, AMD or ES6 module dependencies

- ## avoid pages/screens vs components folder structure 
- https://twitter.com/sseraphini/status/1385574397998637058
  - folder-by-type vs folder-by-feature
  - keep components and routes colocated based on their feature example: 
- `<feature>` .
  - all routes of this `<feature>` .
  - all components of this `<feature>` .
  - like sub apps that you can compose
- for both pages and features folder (for a multi-page app)
  - one thing to notice is that a page can use multiple features, so having the page component inside a specific features folder is something that breaks this logic colocation.
- But take next for example
  - Since it's routing is based on the file system, won't that put components to be considered as pages, when they shouldn't be?

- ## AsyncAPI is the OpenAPI for Event Driven architecture 
- https://twitter.com/sseraphini/status/1384490726168227843
  - You can document all your events and payloads, internal and external ones
  - https://www.asyncapi.com/
  - https://github.com/asyncapi/spec
  - https://github.com/asyncapi/asyncapi-react
  - AsyncAPI正在成为定义异步、事件驱动的API的行业标准；您可以将其视为异步世界的OpenAPI
  - 它既提供了以机器可读格式描述和记录异步应用程序的规范，也提供了工具(如代码生成器)来简化负责实现这些应用程序的开发人员的工作
  - 很多框架都支持从代码直接生成OpenAPI，比如SpringDoc等

- ## Forget DRY. It's okay to repeat code sometimes. 
- https://twitter.com/renatorib_/status/1384159371593060357
  - Abstract it when you are sure that it will more help than harm.
  - Repeat first, abstract later.

- ## Request: point me to some good examples of JS libraries that show the TS types for their APIs in the API reference pages? 
- https://twitter.com/acemarke/status/1383503585812508684
  - I'd like to see how other libs organize presenting descriptions vs typedefs in the reference docs.
  - How to present potentially complex and nested typedefs
  - How to maybe hand-wave some of those complex types for readability
  - How to split arg/return value display from the written descriptions
- We dynamically replace the generic type parameters in the docs for generic types with a concrete type where necessary. 
  - No `IEnumerable<T>` but `IEnumerable<INode>` .
  - why not just name the generic parameter something readable (rather than abstract T)? that way you wouldn't have to replace anything - like probably you could just grab the name from `Node extends INode`

- ## Unpopular opinion: you should write E2E/integration tests *first*, always. 
- https://twitter.com/DavidKPiano/status/1180497113341468677
  - (This mainly applies to applications. For libraries used by developers, the unit tests *are* the E2E tests, a lot of the time.)
  - They should be directly related to business logic (user) requirements. 
  - Only when an E2E/integration test fails should you even think about writing unit tests. 
  - And be willing to delete those unit tests.
- Speaking strictly from the point of view of a library author, it’s the failing unit tests that can give you an instant idea of why the e2e tests are failing, rather than having to go spelunking(洞穴攀爬运动)
- When we first started React Training, we had only one test for the whole website: make sure someone can buy a ticket. As long as that worked, everything else was negotiable

- ## The largest misconception about @webpack is: 
- https://twitter.com/TheLarkInn/status/1017052742039326721
  - Not treeshaking or making vendorbundles is the cause of their web perf issues. 
  - Rather, in _most cases_, the main cause is not leveraging code splitting enough. 
  - You should prioritize code-splitting above the aforementioned.
- The irony here is that to code split, you don't need to configure anything for webpack. 
  - Just use `import()` . 
- I think code-splitting will be more efficient at making your app faster, whether code is tree-shaken or not.
- We use webpack dynamic imports to also lazy load features into our app that only apply in certain config e.g. /config endpoint -> {features:[]} -> for each feature -> import. Works well for us
- Any recommendation or best practices articles  
  - The key is this, if the code you `import` is not needed to produce the initial render of your application (routes, modals, tooltips, dialogues, event handlers, etc.)， then you should use `import()` instead.

- ## Why I code against a mock API:
- https://twitter.com/housecor/status/1256242384075198472

1 I control the speed
2 It's never down
3 No internet required
4 No cross-team dependency
5 I can force it to throw errors to simulate server errors
6 I can write fast, reliable app tests
7 When I find a bug, I can enhance mock data and test it

- ## What challenges have you faced adopting serverless technologies?
- https://twitter.com/flybayer/status/1381743417391255559
- Simulating the environment "locally" for testing/debugging.
  - use case: complex business logic breaking, like a bunch of calculations, how to simulate and debug that to find the error 
  - arc.codes solves that part w a local sandbox
- Realtime, 
  - Connection pools, 
  - Stateful assets(dynamic images et al), 
  - Complex setup (or lose of control)
  - inability to use some tools I love(e.g. mongodb is just poor in serverless)

- ## Don't forget to consider an option to scale horizontally rather than vertically. 
- https://twitter.com/kettanaito/status/1381604735304806403
  - Horizontal scaling is far more sustainable and prone to refactoring.
- let's say when we need to extend an existing function to handle two different scenarios - request in browser or nodejs.
  - instead of pushing the logic through one function `handleRequest` , consider treating each scenario as a standalone implementation, potentially reusing the internal logic that repeats.
- Treating those as two independent scenarios also contributes to much more scoped tests. 
  - That, in turn, allows to reason about similarities and difference and makes it easier to alter logic on a per-scenario basis.

- ## I'd really like to have a thing that wraps every function in my codebase at compile time, it profiles samples of them with minimal overhead, 
- https://twitter.com/fabiospampinato/status/1381569380203573257 
  - it's always on, and over time it tells you interesting things. 
  - Potentially it could work across an entire user base too, that'd be super.
- Different domain and technology, but this idea reminds me very much of pira
  - https://github.com/tudasc/pira
  - Except we don't instrument / wrap every function. We Actually try to minimize the instrumentation to only "relevant" parts -- for different aspects of relevant.

- ## to repeat my favorite software development mantra: "make it work. make it right. make it fast."
- https://twitter.com/acemarke/status/1376969090552725506
- I hate perfectionism, I rather create something initially janky but a really cool thing/idea THEN work on improving it and optimizing it.

- ## I don't use TDD This is what I do instead: code -> test -> docs (CTD)
- https://twitter.com/sseraphini/status/1376636172080922629
- CPT - code > production > test
- Tdd is great but it usually it is not so practical while you are still exploring the implementation space
- I do the opposite: docs code test, DCT
- TDD is interesting for pure functions that you know the expected result and use the test as a tool to automatically check if you are doing it right. Test functions manually are boring if it's not trivial.

- ## it never ceases to amaze me how much some people will resist showing their code after asking a question and saying "this doesn't work".
- https://twitter.com/acemarke/status/1376656948926496768
  - Sometimes I can provide an answer after just hearing a description.
  - but most of the time, I need to see the _real code_ to debug the issue.

- ## Is there any kind of a utility lib that will scan a JS file and identify code that doesn't match a given set of features supported by a target browser?
- https://twitter.com/acemarke/status/1376703719669182471
  - I'm basically looking for something like (notional): `is-browser-safe ie11 my-file.js` .
- eslint-plugin-compat
- eslint-ie11-compat

- ## What's the right process for a library to drop support for IE11/ES5-only environments in its published artifacts? 
- https://twitter.com/acemarke/status/1376381894279987209
  - Should that be a new major, or a minor?
  - Right now our CJS/ESM files are back-compiled to ES5 syntax for IE11 support.
- So "major" seems to be the consensus answer so far, which is reasonable.
- We're planning for RTK Query to be released in RTK 1.6. It's additive only, so that doesn't require a new major.
  - I really want to keep RTK and the new RTK Query features accessible to as many devs as possible. On the other hand... IE11. Ew.
  - Maybe put these out in 1.6, and then begin planning RTK 2.0 that drops ES5-only support?

- ## Where do you put tests and why? same folder vs separate tests/ folder
- https://twitter.com/claviska/status/1375071253753647118
- Separate “tests” folder because clutter etc. 
  - Also if you are concerned that things aren’t getting test, you can also setup code coverage and know for sure.
- Framework's default
  - It's configurable, but I'm looking at one with a tests folder. My concern is, if tests are independent of the things they're testing, it's easy to forget to add/update them (particularly for contributors and large codebase)

- ## If you deploy your app to serverless platforms (Vercel and friends) but you use services (Postgres, Redis, etc) that don’t have auto scaling, then your app is not serverless at all. It’s only an illusion.
- https://twitter.com/flybayer/status/1373824547506511873
- We just shift the bottleneck. Classic manufacturing efficiency optimization problem

- ## I always wondered about Google, how do you push through the internal competition? Android, PWA, Flutter. 
- https://twitter.com/sebmarkbage/status/1373775862219292674
  - I sit here with an amazing community, team, org and management support. 
  - Yet all I can think of before every Monday is the people that don’t believe in me or what we’re doing.
- You have to lead and stand by your decision: Think of Steve Jobs coming back to Apple and bring all that Objective-C guys from Next.
  - It was the better technology - but heck it was unpopular at that time. And despite all the lows he denied all alternatives (Java, Flash).
- I worked at companies where such competition is a norm. 
  - In my experience, that's what helped to avoid such feeling. 
  - Helpful competition promotes stuff that works, kills stuff that does not; 
  - it allows people to focus on the objectivism of the tech not the subjectivism of feelings.

- ## Wondering sometimes if, instead of more libs, we shouldn't offer more first-class copy-and-paste solutions.
- https://twitter.com/mpocock1/status/1372986732354883588
  - Copy and paste an entire component lib and then tweak to your heart's content
- I'm absolutely against this: the good thing about libs is that they are documented and tested configurable blocks. All code should be libs, even our own. Coding for open source enforces code quality (at least at the boundaries).
  - Libs are wonderful, invaluable. But choosing libs for _all_ solutions is perhaps too dogmatic. There should also be space for when you want to grab something pre-built and modify it.
- What you described is the basic idea behind the architecture of Crown. You “install” packages within the framework by cloning with git subrepo. You own the code but can still pull changes from upstream

- ## For tools that don't have multi-versioned docs sites: what are good techniques for how they indicate a particular API or option was added/modified in a specific lib version?
- https://twitter.com/acemarke/status/1373102543371390979
- just a line at the top of the page/section mentioning the version works fine. I think I've seen that pattern in a bunch of pages on Next.js and some other docs.
- api.jquery.com/blur/ Of course that's how things were done back in the day I guess 
  - The version added for a method is always specified, also there are always notes about the differences between versions.
- Kotlin docs show you which version APIs were added in and if they are supported in JavaScript, JVM and/or native

- ## Developers that can't or don't write good comments aren't great developers yet.
- https://twitter.com/BenLesh/status/1372562839475470336
  - Add comments about WHY code exists, not what it does.
- Comments cannot be tested and should therefore be assumed to be wrong.

- ## What's the coolest open source project in the JS or Wasm ecosystems you've seen that's *new* within the last year?
- https://twitter.com/_jayphelps/status/1372249383291457540
- esbuild
- We just finished a show on Remotion and @JNYBGR - how to programmatically make videos with React. It's really excellent and empowering technology.
- css-in-js: SnackUI - the final React style library
  - The smart SwiftUI-inspired UI kit for React Native & Web.

- ## I don't actually show much of my coding work in public, largely because I do most of my coding at my day job.
- https://twitter.com/acemarke/status/1372374988762779649
  - Even then, teammates normally only see "final" code in my PRs, and don't often see how many mistakes I made along the way to get to that final result.
- A couple nights ago I decided I'd see if I could try writing a faster implementation of the RTK mutation detection logic. I did get it passing all our tests.
  - It appears to be like 15x _slower_ than the original.
  - I guess the point here is, consider this your semi-inspirational reminder that everyone screws up - you just don't always see that happening visibly.
  - I am now trying to figure out _why_ my implementation is slow.
  - today I deployed a new build of our app to prod. small app, single server, half-automated deploy process.

- ## What are some times you've needed to keep data synced between two SaaS products? (eg: keep a Trello board synced w/ a Notion table)
- https://twitter.com/geoffreylitt/status/1371509957779148802
  - Looking for example use cases for a sync tool I'm working on
  - Could also be things like "needed to keep this Salesforce data updated in a Google Sheet"
- In design-engineering teams:
  - Figma Comments <> Trello Cards <> GitLab Issues
  - Trello being the middle ground for managers who‘re afraid of Figma/ GitLab
- Personally: Airtable <> Google Sheets

- ## The #1 tech skill to have is comfort in coding, on the fly, in front of other people.
- https://twitter.com/AdamRackis/status/1370875384812740610
  - Expect to be given some silly use case, ie, "write a class that take two strings, and tracks which is longer"
  - Be comfortable talking through the requirements, asking questions, etc.
- Expect to iterate on it, over and over, with requirements being added. Ie, "now optionally take an array of strings, and, if an array was passed, track the shortest string. If just two strings were passed, like before, then ..."
- Most important tip I can give: **think out loud**. Always. Turn the voice in your head you normally think with, off, and think out loud.
  - If you get stuck, talk it through, out loud. Explain why you're stuck. Ask questions. Your interviewer is there to help you. Seriously.
- The worst thing you can do is stop coding, and freeze up, panicking in your mind. Talk it through.
- Expect to be asked questions in your domain to test how deeply you know it. I was asked about everything from arrow functions, to Promises, to web sockets.
  - The deeper you know your stuff, and can demonstrate it, the better.
- If you're asked about arrow functions, don't just say they're shorter syntax sugar.
  - Mention lexical this.
  - Mention lexical arguments.
  - Mention lack of a Prototype and [[Construct]] slot.
  - Show them you're someone who knows their shit.
- You know what I was never, ever asked about, even once? JS Frameworks
  - Oh, you've written apps in React, Svelte, Vue and also Angular? Nobody gives a shit.
  - Companies care a lot more that you have deep language mastery, vs having played with a bunch of different frameworks.
- You know what else I was never asked about? CSS Frameworks.
  - Tailwind seems really, really cool. But maybe learn the fundamentals of CSS before you dive in, there.

- ## friendly reminder that http-only cookies don't protect you from XSS
- https://twitter.com/benawad/status/1370532233698770947
  - if someone can inject code they don't need your token, they can just make fetch calls on that users behalf
- The solution to this is using CSP, right?
  - The solution is "don't trust user input"
  - Yep but not all browsers respect the policy. And if you parse malicious code comming for user inputs it doesn't matter if the browser respect the CSP especially if that code can be rendered by other users too
- Very true. If you've an XSS you're actually flawed and a local jwt should be the least of your worries

- ## Webpack have achieved production server Hot Module Reloading between apps using module federation
- https://twitter.com/ScriptedAlchemy/status/1370555543136301060
  - No cold start, no downtime, no new process. I've seen the future, and its got zero-downtime

- ## Preemptive Pluralization is (Probably) Not Evil
- https://www.swyx.io/preemptive-pluralization/
- What if we just assumed we might have two of everything?
- Before you write any code — ask if you could ever possibly want multiple kinds of the thing you are coding. If yes, just do it. Now, not later.
- But I think Preemptive Pluralization(先发制人多元化) — projecting forward into hypothetical situations when you need N types of a thing — is exempt, even though you are literally optimizing for a future you don't currently live in.
- It is a LOT easier to scale code from a cardinality of 2 to 3 than it is to refactor from a cardinality of 1 to 2. 
- Robust code is optimized for change (more in a future blogpost).
- Let's address two obvious criticisms of Preemptive Pluralization:
  - Increased code complexity: Functional languages and other abstractions can help make array or matrix operations almost as easy to work with as regular operations.
  - Slow performance from doing extra loops: Loops only cost significantly when you have lots of N. By definition, if you are pluralizing prematurely, N = 1.
- Listen up, this is sound advice that I can attest to after years of experience. 
  - You will almost always need two or more. 
  - If you end up not needing 2 or more, the risk/reward is worth it in almost every situation.
  - Just Pluralize It.
- I've made this type of refactor more times than I care to count, and it's always a pain. Absolutely good advice.

- ## 3rd party integrations today are like:
- https://twitter.com/ryanflorence/status/1370405429189046278
  - First, add our 100kb browser SDK
  - Now fetch to your "api route"
  - Now use our server side sdk
  - Now back in the browser use our browser SDK
  - A little config on the third-party dashboard + `<form> ` would have been way simpler.
- But you know that A in JAM is for API and you can make a `<form method=post>` , right?
  - Yes indeed, but so many services require browser javascript and you can't actually process that post on the server.
- `<form method=post>` .
  - automatically serializes data
  - automatically fetches an "api route"
  - automatically changes the page state when complete
  - automatically adds pending indication to the user interface
  - works cross origin if needed
  - This is how you communicate a mutation.
- use `<form>` , Then use `<Form>` , when you've got the time/energy/skill to implement a nice pending/optimistic UI. 
  - Remix doesn't care which one you use, it's all the same!

- ## For a long time, I was always unhappy with my code. I never trusted it, never liked it.
- https://twitter.com/eveporcello/status/1369678978827493376
  - Then I discovered: Testing, Refactoring
  - With both, I worry much less about getting code right initially—I can always improve it later. 
  - Testing also lets me trust my code.

- ## My problem with types added to every function and object is that they occupy my brain when I scan the code when I don't need them. 
- https://twitter.com/oleg008/status/1369956575964782594
  - They are just cluttering the code most of the time. 
  - I want to go back to clean JS code but still have the types hints when I want them.

- ## TIL: passing multiple `-m` options to `git commit` creates paragraphs in the message.

- ## How to identify mistakes in a code structure to learn from:
- https://twitter.com/cse_as/status/1369281929162285063
  - When you go back to a part in the project your team worked on earlier & it takes you more than 10 seconds to pinpoint where the needed code is, it probably wasn't structured in a way that made sense.

- ## A list of basic Linux commands every developer should know:
- https://twitter.com/iamdevloper/status/1368866110951596032
01. Open your browser
02. Head to your favourite search engine
03. Type "how to copy a file to another directory"
04. Click the first Stack Overflow link
05. Copy the top voted answer
06. Blindly paste it into your terminal

- ## When should I (not) use mocks in testing?
- https://dev.to/kettanaito/when-should-i-not-use-mocks-in-testing-544e
- Depending on the software that is being tested, there are multiple things that can be mocked:
  - Environment and context.
  - API communication
  - External dependencies.

- ## Writing software is basically a 2 step process: 
- https://twitter.com/housecor/status/1368569429202792448
  - Ask the computer to do something
  - Verify its response
  - That’s why I believe in creating fast feedback loops. The faster I get a response, the more productive I can be.
- Feedback loops also involve CI, designer-developer collaboration, automated tests, among others. Any improvement that you do in any of those increases your productivity!
- You missed the 3rd step. Swear at the computer when the response is wrong and you can't see the problem.
- What are your favorite techniques for this?
  - Mock APIs
  - Small tickets so I get teammate and user feedback faster
  - Automated unit tests and TDD
  - Build and test small components in isolation
  - Create custom dev tools
  - Use Cypress to avoid interacting with the app manually while coding
- In all seriousness though, this is why I love to write my code using TDD.

- ## is there a "modern" UI for OpenAPI? built with @reactjs that could be very customizable?
- https://twitter.com/sseraphini/status/1367851096421568512
  - I'm like to embed my API inside @docusaurus
  - but redoc takes the full page and swagger UI has some dark mode issues

- ## You can't mock cloud semantics locally but you can mock the API surface. AWS is very stable. 
- https://twitter.com/brianleroux/status/1367851230785990663
  - Folks say you shouldn't use local emulation because of this but I respectfully disagree. It's slower. 
  - Tighten those feedback loops. Test locally AND in an identical staging stack.
- Fwiw, same discussion happened in mobile a decade ago. You can't use an emulator they said. Mostly ppl said that because the emulators sucked. 
  - Ppl don't say that about mobile dev anymore. Cloud will have the same cycle.
- I was firmly in the “don’t emulate AWS” camp until I actually tried using localstack. 
  - If the bits you need to emulate are supported, it works quite well.
  - It's additive too. Work local and then test in a staging stack. Makes step 2 shorter which has higher latency anyhow. 
  - I'm fairly certain this meme happens every new platform because vendors and frameworks add emulation later. It's an excuse while they get their shit together.

- ## 99% of what I do in a large codebase is find pre-existing examples, copy-paste structure, fill in the holes and clean up. That's it.
- https://twitter.com/deech/status/1366859264732635148
  - Relevant skills: find pre-existing examples, copy-paste structure, fill in holes, clean up
  - Irrelevant skills: category theory, able to whiteboard delete for a red-black tree
- This is definitely how big company code works! Sometimes to a surprising effect. 
  - You might check in some random pattern you haven’t given much thought to while filling in some hole. 
  - Then a year later you find your code in a 1, 000 places with tiny changes. Hope it was good code.

- ## Is Webpack's code-splitting just garbage or are there more tricks to implement?
- https://twitter.com/mattgperry/status/1366344701964648450
- Why do you think it is garbage?
  - Because moving a single enum into its own file yielded a 11kb/89% saving.
  - This is incredibly delicate and has implications about how a project should be structured (no more than one export per file). As far as I can tell, for no good reason. It isn't the case with Rollup.
- nope, webpack just offloads more to Terser whereas Rollup do a lot more work on its own, this can make a big diff for some projects, 
  - also - Rollup makes some pragmatic choices sometimes whereas webpack tries to be super strict and safe, which also can make a big diff
  - So do you personally tend towards single-export files?
  - This is a good advice if u want to keep things as treeshakeable as possible - ive thought about creating a rollup plugin that would chunk a project this way automatically. I dont want to split files manually. Never got to it though

- ## As a CS prof, I use binary search practically every day to figure out which part of the paper is crashing LaTeX.
- https://twitter.com/bradreaves/status/1365061879744315398
- I take quadratic computer time to avoid the logarithmic human time for the binary search (a.k.a. re-compile every few keystrokes).
- This is how I used to teach kids to debug. 
  - When a problem is really hard to find, try and reduce code in half, recursively, until the program works
- Divide and comment 😋

- ## Want to find a perf problem? Throw something big at it.
- https://twitter.com/kuvos/status/1364929672652464132
  - 88mb of js will probably do

- ## Integration testing tip: Avoid creating many small tests. Instead, create a few big tests. 
- https://twitter.com/housecor/status/1364584436755480578
  - Here’s why: There’s a lot of overhead in starting each integration test. 
  - So to build a fast integration test suite, favor “big” tests over “small” tests.
  - Example: Imagine I have a todo app. I don’t write separate tests for create, update, and delete. Instead, I create a single test that checks all three. I name the test “should support adding, editing, and deleting todos”.
- And when the test fails, you don't know why.
  - In Cypress that’s clear. It shows what line. And even records and screenshots.

- ## Best CSS debugger: `border: 1px red solid;` .
- https://twitter.com/kyleshevlin/status/1363901000948408320
- I have to say this every time: This is close, but it's NOT the best.
  - It's better to use `outline` than to use `border` . Why?
  - Because `border` affects layout, changing the width and height of its element. `outline` has no affect on layout, whatsoever.
- It's especially important to use `outline` instead of `border` when testing the cumulative layout shifts
- Good call. Its also useful to keep in mind when trying optimize for a better Cumulative Layout Score, if there are larger shifts in elements that could alter the CLS.  Though something as small as a border may not be enough for the algorithm to catch, I am not sure.
- Sometimes, I do prefer using backgrounds, like: `background-color: rgba(0,0,0,0.1)` , I can see how much an element takes, and how they stack
  - But most of the time, outline is the way to go

- ## Imagine if tools like Sketch and Figma let you write expressions the way Excel does.
- https://twitter.com/markdalgleish/status/1363703556109312007
  - e.g. calculating a background based on another element: `=darken(getBackground($ELEMENT_NAME, 10%))` .
- Transpile to CSS vars and ship as code
- Figma could expose the API in editor in addition to using it for plugins. That’d be sweet!
  - It's already done. You can use it in the console.
  - Good point. I think a part of writing “expressions”, not code is making it more approachable. For example, a small thing excel does when writing expression’s is letting you click to select fields and inserting them into the expression.
- It's really clever that Excel doesn't refer to writing expressions as "writing code." More tools should let you "write expressions" rather than underestimating their users' intelligence.

- [Excel is visual programming because you're placing data, labels, variables and calculations in physical space.](https://twitter.com/markdalgleish/status/1363727357169704963) 
- This makes VBA is the javascript of the spreadsheet world
- arent all programming languages like this as well? only difference is that it’s not bound by y and x axis

- ## Sometimes it’s overwhelming to change some complex feature in the existing code.
- https://twitter.com/BenLesh/status/1362762796501401601
- I used to do this. But it's often dangerous. I try to take a more measured approach now.
  01. Make a couple of PoCs off to the side to see what I learn.
  02. Carefully improve the code and add tests in the parts of the code I'll be touching, and see what I learn.
  03. Add the feature.
- I find that after part 2 above, often the approach I take is different and better than what I did in some of my PoC work.
- The main difference between the new code and deleted code: The deleted code has been tested and hardened, if only by users. 
  - It already has behaviors that are expected. 
  - Depending on complexity, a "big bang" rewrite has little hope of recapturing all of that.
- Even when I've had insane test coverage, there were missing corners. 
  - I've found big bang rewrites have a higher probability of regression. 
  - Better to push existing code around until it looks like a rewrite. But this is my experience.

- ## The reason Vite requires .jsx extension for JSX processing is because in most cases plain .js files shouldn't need full AST transforms to work in the browser.
- https://twitter.com/RyanCarniato/status/1362178225493839874
  -  Allowing JSX in .js files means every served file must be full-AST-processed just in case it contains JSX.
- We have been struggling about enforcing this because it makes so much sense, but figured there wouldn't be enough community backing. 
  - But if major tools like Vite go this way that is amazing. It never should have been just .js when you consider compilation

- ## Introducing Blazepack - a super fast dev server powered by @codesandbox sandpack bundler.
- https://twitter.com/ameerthehacker/status/1361615692294852613
  - Supports @reactjs, @vuejs, @angular
-  It is a thin wrapper around the sandpack bundler, so it support React fast refresh, HMR and all the cool stuffs that sandbox supports

- ## How are some of you actually working on _side tech projects_? I'm struggling to even maintain energy for day-job projects lately.
- https://twitter.com/brian_d_vaughn/status/1361520253604421634
- I get anxious without side project. It’s how I relax.
  - When the brain is full of errant(错误的、行为不当的) thoughts and ideas, only way to get anything done at work is to regularly clean the brain.
- don't believe everyone on twitter. Specially in the Dev community.
  -  I have experienced it a lot that people try to talk them selfs better than they actually are. Per se it is not a problem. 
  -  But it promotes a bad reputation for devs. We don't code 24/7

- ## Offline support has been part of the PWA installability criteria since the beginning. 
- https://twitter.com/ChromiumDev/status/1358817467661967365
  - In Chrome 89, we'll warn you if your PWA doesn't have an offline experience. 
  - In Chrome 93, we'll start enforcing the updated install criteria for new PWAs.
- If all you need is a baseline offline fallback page without actually delivering a true offline experience (which, acknowledgedly, many apps don’t need or can’t), then give my article a read
  - [Create an offline fallback page](https://web.dev/offline-fallback-page/)

- ## When learning something new, it’s easy to fall in to the trap of comparing your work to seasoned professionals and think everything you’re doing is wrong. 
- https://twitter.com/steveschoger/status/1358588140328538115
  - Lately I’ve been trying to embrace this learning period because it’s a small window of great discoveries.
- Constant learning from seasoned profs, using my previous dev knowledge mixed with theirs, change code as I find better or more efficient solutions, seasoned profs's solutions are not always right or appropriate for the current app.  Having a blast and always learning.

- ## which companies are using @GraphQL in production nowadays?
- https://twitter.com/mxstbr/status/1358351658078634014
- Frontend teams at Danske Bank use GraphQL, mostly driven through Apollo. 
  - Microservices are still on REST so there's redundancy maintaining a mid-tier just for conversion.
  - GraphQL has most significant advantages when adopted by backend teams which isn't the case at most places.
- Using it in production at @skillshare . 
  - Running Apollo Gateway as API composition layer to allow frontend decoupled monolith -> microservices migration.
- @OrbitalChat uses it for admin-based stuff. 
  - The more interactive part is done with Firebase Real-time database and Firestore direct from the client. 
  - Also @SketchADay is 98% GraphQL and a couple of little plain JSON-over-HTTP bits
- GitHub and Contentful
- @AirbnbEng uses it quite a lot

- ## If you don't know which code is calling your function, use console.trance()
- https://twitter.com/sseraphini/status/1356654950198239233
- I used `console.log(new Error)`

- I usually also do “console.log = console.trace” to locate and remove some console.log

- ## Hyphens are pretty. Underscores are ugly and don’t belong in URLs
- https://twitter.com/mscccc/status/1355525419152384002
- What about emojis in URLs? 
- [URL as UI](https://www.nngroup.com/articles/url-as-ui/)

- ## "The DOM is bad for apps" makes me laugh pretty hard. 
- https://twitter.com/_developit/status/1355670204366393347
  - It's effectively the same type of abstraction as a scene graph, but because we use it poorly it must be bad!
- I think the dom is very much bad for apps, who in their right mind would say otherwise. 
  - Why else do we have frameworks abstracting it. 
  - Most people don't know or see a dom when they make apps and that is a good thing.
  - That is the same reason why we have rejected a component model built on that pile of perpetual backward compat which is the dom.
- The browsers dom is virtual, bc it's faster. 
  - Every GUI system is split into a logical/virtual & a visual tree, otherwise you wouldn't be able to schedule, or, well, virtualize. 
  - Ever used a virtual list, I suppose you did. 
  - FBs "vdom" has better scheduling than the "dom", facts. 
- aren't some of the most popular apps just app shells with a web-view?
  - that, or react-native which uses a tree abstraction very similar to the DOM anyway
- Well, if we just used fixed height for everything and there was never a need to refresh layout I think most html apps would be as fast as 'native' - as if running apps in a JVM/runtime is native anyway - if it's not assembly writing directly to a framebuffer it's trash

- ## Software tradeoffs
- https://twitter.com/housecor/status/1355144710185230336
  - Build vs Buy
  - Reuse vs Copy
  - Sync vs Async
  - Serial vs Parallel
  - Dynamic vs Static
  - Concise vs Explicit
  - Unified vs Separate
  - Secure vs Convenient
  - Simple vs Configurable
  - Centralized vs Distributed
  - Convention vs Configuration
  - **Avoid picking sides. Think tradeoffs.**
- I am not sure you want to trade off security for convenient
  - Perhaps, but companies do so everyday. 
  - Using other people’s software is convenient, but adds security risk by trusting other people’s code.

- ## Will Vite replace vue-cli? 
- https://twitter.com/youyuxi/status/1354584410482499585
  - Initially I wasn't sure, but at this stage I believe it will eventually be the case.
  - The main disparity(不同；差异，悬殊) now is just test runner integrations.
- Check out uvu by @lukeed05 . 
  - Native ESM support, very much in the spirit of Vite. 
  - No test compilation step by default, no special integration needed.
  -  When I need to test in the browser, I just start my Vite dev server and use puppeteer in uvu tests. It's refreshingly simple
- We could make a plugin for web test runner
  - It should be relatively straightforward if we can proxy browser requests to some transform API or middleware. 
  - We already have a plugin for snowpack
- There was discussion in vue-cli about letting plugins replace webpack as the builder
- after a few years of running large enterprise apps on vue-cli, I've had to break out of the test runner integrations to avoid the lag time between test runner updates, and vue-cli updates. 
  - vue-cli is still a great tool... 
  - But would love to see a more decoupled approach in vite

- ##  what are your team’s package.json script naming conventions for development mode, your build stage, and potentially running the built thing?
- https://twitter.com/jaredpalmer/status/1353083840424763392
  - I used to be in the ‘start, build, start:prod’ team 
  - but now I’m actually leaning toward ‘dev, build, start’

- ## A little technique we use all the time to audit the layout shifts and avoid performance issues.
- https://twitter.com/smashingmag/status/1352185650091581441
01. Add * { outline: 3px solid red } to your CSS.
02. Record the loading of your site/app.
03. Review it by exploring what happens in slow motion.
04. Adjust and minimize shifts.

- Great tip, thanks! This one's less visual and more programmatic from the 'Performance' tab in Chrome.
  - You can hover over the 'Moved from' keys and this will visualise the movement in the browser window.
  - And using this method you can even see down to the shift caused by web fonts loading.
- We can also use a `PerformanceObserver` to log elements causing layout shift to the console
- Remember this trick from when i started to learn css.
  - Always use to troubleshoot when some problem arises while postioning elements..
