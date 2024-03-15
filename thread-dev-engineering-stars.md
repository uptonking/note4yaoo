---
title: thread-dev-engineering-stars
tags: [engineering, thread]
created: 2021-08-10T03:50:40.299Z
modified: 2021-08-10T03:51:01.891Z
---

# thread-dev-engineering-stars

# guide

- 处理超多配置项，可参考 tsconfig/webpack/vscode
# discuss-stars
- ## 

- ## 

- ## The devil hides in long "Utils" classes.
- https://twitter.com/RaulJuncoV/status/1768623548703060460
1. Add your Tests before touching anything
   - You will understand behavior.
   - You will refactor with confidence.
   - They will serve as your new documentation until you have something better.

2. Data-Driven class design
Methods that operate on the same data should be within the same class.
Group data and behavior.

3. Struggling with finding a name means something (SRP)
If you struggle to find a name for a function or a class, you will likely need to split.
Every class should have only one reason to change and do one job.
If you find a class doing too much, it's time to break it down into more focused classes.

4. Encapsulation Through Composition
Prefer composition over inheritance where practical.
Use objects to represent behaviors or states you can compose into your classes rather than extending them through inheritance.
Use composition over inheritance to create flexible and loosely coupled systems.

5. Validate Input at Public Interfaces
When your methods need to accept input from other parts of your code, don't just trust that the input is correct.
Validate it to ensure it meets the method's requirements.

- Unfortunately, "Utils" classes are a common bad practice.  Someone creates a single util class to put a method not fitting in any other place. Then the new class quickly pollute with many other methods.

- ## 🆚️ which URL format we going with?
- https://twitter.com/Shpigford/status/1763318774336311731
  - param-in-url-path vs query-params
- My view on this: the path is the WHAT, the query is the HOW.
  - Excellent advice! Query parameters essentially serve as an additional filtering layer
  - 💡 注意顺序。Also it is easier to add more params when/if needed, and client wouldn’t care about the order of them.

- Query params are widely used to filter down the data you get from an endpoint. I don’t see the reason not to use them.

- I like 2nd since better support for languages query params to string concept. Lots of http libs out there handle key/value pairs to query string. W/o it you manually construct it, which is fine too but more readable as a dictionary in code IMO

- 2.  Clean URLs and clean configurable parameters.

- ## 🤼🏻 your codebase is a mess
- https://twitter.com/catalinmpit/status/1763178455750029710
- talk is cheap, send me patches

- ## Question for other library authors: how do you handle experimental code? 
- https://twitter.com/steveruizok/status/1763119013243007438
  - We have a feature flag system in tldraw but mainly for our dotcom/application layer. 
  - It makes me nervous to ship experimental code in the library releases.
- Follow the React model, e.g. `unstable_new_thing` ?
- for libraries, it could be a constructor option with a very explicit name like `UNSTABLE_<featureName>` .

- We do this in @getunleash : Feature flags are part of our code. 
  - In our cloud they are resolved using an internal Unleash Instance. 
  - For self-hosted, we have zero insights, so it's treated as static configuration, and the user can opt-in by setting the experimental flag.
- Our code is open, so you can inspect it yourself. For our cloud we simply provide the Unleash SDK as a dynamic flag resolver.

- Future flags from remix is an awesome concept

- ## 💡 I have a "give it 5 years" rule for assessing tech trends. It's not performant but reliable.
- https://twitter.com/rednafi/status/1761727361047835072
  - GraphQL, Prisma, and many other JS zeitgeists didn't pass the filter. 
  - Vue, Go, Django, RoR, Sqlite, FastAPI did. 
  - I'll treat ML & the movement to make programmers obsolete the same way.

- Where does Rust belong?

- ## Avoid Barrels (A barrel is a file that exports code from other files)
- https://twitter.com/housecor/status/1730993597862780976
- Barrel benefits:
  - ✅ Shorter import paths
  - ✅ Support importing many files via one import
  - ✅ "Hide" modules - Only export some modules for the "public" interface
- avoid barrels. Here's why:
  - 可能导致循环依赖问题
  - 🚫 Bloats the bundle. Inhibits tree shaking.
  - 🚫 Increases memory usage.
  - 🚫 Slows tooling (builds, tests, linting). Barrels create more modules to parse.
  - 🚫 Slows code navigation ("Find all references" finds the barrel instead of the actual source).
  - 🚫 Barrels shorten import paths and group related imports. Sounds nice, but it's an outdated benefit because I don't write imports anymore - my editor reliably auto-imports.

- People often put each component in a folder to group the files, and use a barrel to shorten the import. Instead, I suggest eliminating the needless parent folder.

- Thoughts on this for backend node apps? Still no to barrel files?
  - aside from tree shaking which mostly makes sense in frontend stacks… the benefits are far greater.

- Far too general, barrel files are useful in many scenarios including reducing circular dependencies. Tree shaking is totally OK, in every tool since about 5y
  - How does it reduce circular dependencies? I've found quite the opposite. For example, two utils A and B being exported from a barrel. B needs A so it imports A from the barrel, thus importing itself...
- Not sure, frameworks like NestJS advices against it precisely because of circular dependencies between modules. Same goes for TypeORM and a few others I've used.
- it generated circular deps only if you use the barrel in the sub-modules, which is an anti-pattern

- ## I told you barrel(桶) files were evil
- https://twitter.com/_developit/status/1712906859877629983
  - Barrel files are files that only export other files and contain no code themselves. 

- We are using index.ts only to export things, no other code than export is in there. It allows us to treat any folder like its a single module, if there is an index, we don't import directly. This gives us "private modules" and prevents stuffing everything into a single file.
- This i  s what a barrel file is... and they are to be avoided. @marvinhagemeist wrote about it sufficiently, I'm not going to bother repeating or quoting.
- that is a barrel file, and they are a very bad idea.
  - AOT bundling can apply tree-shaking to index.ts, but it doesn't work like folks think it does.
- Maybe opting in to the non-safe mode of dropping all unused imports might be a good compromise. It just means we have to explicitly add `import "specifier"` in addition to `import {x} from "specifier"` when importing for side effects, which seems like a good idea anyways.
  - is it a good idea? why not just write code in a way that expresses intent?

- ### [Speeding up the JavaScript ecosystem - The barrel file debacle](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-7/)
  - In such a setup a module very likely imports another barrel file which pulls in a bunch of other files
  - Get rid of all barrel files.

- ## You don’t like something? Fix it, instead of complaining.
- https://twitter.com/catalinmpit/status/1693165227183837429
- Complain, but be nice and provide suggestions.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🆚️ In many programming languages, there are two ways of a specifying a sort: a comparator function, and a sort key.
- https://twitter.com/julianhyde/status/1765135622451368386
  - From a theory-of-computation perspective, is the comparator function strictly more powerful? Or can you always devise a (infinite?) sort key to match it?
- The values being compared might only be parseable by a Turing Machine. memcmp() can be implemented by an NFA, and since languages recognized by Turing Machines are superset of languages recognized by NFAs, comparator function is strictly more powerful
  - Yes.  But we "can devise" (i.e. compute the key using any method) and all one has to do is produce a key that has the same effect.  All a comparator function can do is produce a list of choices.  A key can navigate any list of choices.

- ## A lot of library authors end up with generics requiring a crazy number of ordered parameters.
- https://twitter.com/ssalbdivad/status/1753880880110518629
  - This feels fine when you're defining them, but is awful to read and maintain.
  - Just use a single parameter with named keys!
- I would argue that if an interface takes more than 2 parameter (beside maybe context/Lifecycle control in some language) then you should split the interface into more specific use cases.
- I tend to agree with this. It’s what made React’s component props seem unique when it was introduced, but also clean.

- ## 🌰 sentry 现在居然已经这么复杂了，上一次部署的时候只需要 postgres + redis + worker + web 就可以了。
- https://twitter.com/laixintao/status/1719198693822431517
- 这个架构已经没有开源和self-host的必要了。引入的复杂度太高。超出了它能解决的复杂度。
- 我当专门找了很旧的版本装上。
- 毕竟 sentry 要为大团队服务，发展方向决定的
- 前段时间 部署过一次 组件奇多 我感觉是为了直接用云服务
- 可以让你放弃自己部署，选择花钱买它的服务，几年前就已经这样了，不少开源解决方案是这个套路，架构设计是为千万级用户设计的，然而自己部署实际用户只有一个人

- ## Stop making fun of code just because you think it's bad.  All code is bad.
- https://twitter.com/DavidKPiano/status/1718666356059471968
- Wrong. My code is _horrendous_, which is not the same thing as "bad"

- ## I'm a big fan of "build it yourself" because it gives you control over your own destiny.
- https://twitter.com/ccorcos/status/1714035814735487462
  - If there’s a bug or limitation in some third party framework you’re using, you’re stuck! 
  - But if you build it yourself, then the only thing holding you back is your own talent.

- And time
  - everything takes time though, even using a framework... 
  - People seem to underestimate how much time they spend learning a framework and then chasing down bugs and designing workarounds to get it to do what they need.
- I’d much rather use Quill than write a rich-text editor for web! You can always reach into the internals of a third party library and fork it
- Try building something like the Notion editor with Quill and you’ll rage-quit pretty fast
  - I’ve tried both ways. I’d rather just not build that. 

- ## 想问问大家，真的觉得这样好看吗？我宁愿多写几个 if else + for loop
- https://twitter.com/junairez/status/1710167177054355864
- 这种链式写法，自己写的爽了，可读性差，出问题调试麻烦，新手的代码总爱越写越复杂，老手的代码喜欢越写越简单，Python 之禅不是说么：简单胜于复杂，优美胜于丑陋，平铺胜于嵌套
  - 加上隐藏了不少中间值，出问题跟踪调试麻烦死你，特别那些还写成一行的，调试器又不支持按列下断点的时候
  - 中间想加行日志看看中间值都麻烦
- 让rust 社区自嗨吧
- 还是要保守一点，怕过段时间自己都看不懂的
- 这种写法其实扩展性不好，写的很精致，出现一些业务变化了，改着改着就成屎山了，一个方法只完成一个功能，其实是最好的
- 团队工作里在不是特别影响效率的地方，我觉得可读性的重要性是最高的。

- ## People often find it strange that I never use `console.log` to debug things when I'm coding in JavaScript.
- https://twitter.com/trueadm/status/1709361643535143316
  - Personally, using `debugger` statements and breakpoints work better for my mental mindset. I often want to inspect the call-stack, or check various values at their point in time. However, I can see why folks love using `console.log` too.
  - I don't think one is better than the other – stick with whatever works best for you!

- Console.log is mood anyway since the introduction of logpoints in Chrome (and likely others)

- I’ve started to often prefer console.warn to console.log for debugging. In many situations, it appears a good balance. It doesn’t interrupt the flow but shows a call stack

- I use console.log for time series data and “debugger” for things that’s don’t involve a time element. Plays to the strengths of both choices!

- ## So much of SaaS is: build an API to wrap your database so that I can parse the JSON and put it into my own database
- https://twitter.com/_swanson/status/1704703441338053020

- [Skip the API, Ship Your Database · The Fly Blog](https://fly.io/blog/skip-the-api/)

- And then send me a request when it changes so I can re-request it.

- JSON being a terrible transport format with it's 5 data types.
  - I think you’re forgetting null!
- [Steampipe | `select * from cloud;`](https://steampipe.io/)
- It's all strings over the network.
- and this is how a database schema becomes the API schema
- I dubbed this “enterprise crud”

- ## Without any subjective, measurable, and agreed on goals and metrics, striving for "clean code" is a waste of time. 
- https://twitter.com/gunnarmorling/status/1690685859140411394
  - People will just go forth and back pushing through their favorite patterns and idioms, without creating much value along the way.
- Just ask a successful person. That's the fastest xd

- ## Problem: You’re building a big feature that will require weeks of work. 
- https://twitter.com/housecor/status/1689656571570114560
  - Mistake: A long-lived feature branch.
  - Solution: Use a feature flag to hide the feature until it’s ready. Now you can merge daily.
  - Principle: Integrate *continuously*.
- What do you do if the new feature involves db schema changes that can affect the current app behavior?
  - Avoid breaking DB schema changes. 
  - Example: Instead of renaming a column, create a new column, then remove the old one once no one is using it.
- Is there a feature flag tool you would recommend?
  - You probably don’t need one. I typically use an env var, the URL, the user that’s logged in, or a simple checkbox in an admin UI.

- ## reuse logic in JS. I think this makes sense.
- https://twitter.com/tantaman/status/1687090113958797312
  - Business logic is less likely to change between platforms than your view
  - JS is the portable language
  - Why have we been focusing on view portability over model portability all these years? 🤣

- Exactly what I've been wondering lately. Particularly when:
  - You want to embrace the native feel of a platform (i.e. UI/UX) which differs across platforms
  - Business logic usually stays the same across platforms

- I'm trying not to sound bitter, but... do most frontend code bases really have a concept of 'business logic' that lives outside of a react component? In my experience they don't.
  - Thick(厚的；粗的) clients, in my experience, have pretty hefty(大的, 粗壮的) business logic.

- ## What types of app logic would you ideally move into your database layer (if you could)?
- https://twitter.com/calcsam/status/1682610083698728960
- Besides the usual (replication, mvcc, transactions, indices):
  - multiplayer / collaboration 
  - reactivity / live queries
  - paging out cold app state from mem to disk
  - paging out colder state from disk to cloud 
  - permissions / row level security 
  - incremental view maintenance

- outside of very tailored custom systems for massive volume, most teams I've seen come to **regret pushing stuff to the db** 
  - read write and search only imo
- Backup, usage tracking for main tables. Domain code is usually avoided.

- ## 🤔 以前我也很信“大佬们”说这些，直到我加入了Office团队，我终于发现这些乱七八糟的规则都是浮云。
- https://twitter.com/geniusvczh/status/1680029213695557632
  - 只要代码够多，什么都是难的，根本没有程度的区分。
  - 我在改的都是Office的共享代码，每次都小心翼翼地，因为一旦出了错误，十几个app和一千多个内部库加在一起，错误信息的log就会挤爆我2T的硬盘
  - 👉🏻 代码可读性更是无稽之谈，根本没有时间去读的。gpt4刚公开的时候最离谱，我被要求去把一个我完全不了解的模块集成进一个我从来没改过的程序里去，当然最后还是做出来了。一开始连怎么编译都没搞清楚，更别提debugger，完全靠不断的搜索代码然后在脑子里推理最后把东西做完，交给别人测试，居然能用
- 贵司的那几坨屎山代码能正常编译本身就是个奇迹了
  - 我们专门有个几十个人的build team在捣鼓这个，感觉是整个部门最牛逼的地方
- reviewer进来的时候代码已经这样了
- 让我想起 Bing 很多 owner 早已离职的 code，根本没人敢动…… 一般也就改改 config

- ## Weex 坟头草都几丈高啦，全指望开源社区驱动维护这么复杂的技术方案是不可行的
- https://twitter.com/Brooooook_lyn/status/1678226894158954497
  - 目前已知使用 Vue.js 手机 APP 的有 DCloud 的 UniApp 和来自社区维护的 Vue Native（基于 React Native）。
  - 但是，他们对于 Vue.js 官方的新技术的支持，并不是那么及时。甚至性能上，还会出很大的问题。

- ## 非核心业务，要尽量用别人的 API, 不要自己累死累活去重新研究和发明轮子。
- https://twitter.com/Svwang1/status/1646669244158066689
  - 反过来，自己的核心竞争力，要尽量变成一种类似 API 一样的东西，供更多外人使用，帮自己分摊成本。
- 应试教育可能会诞生这样的顽固惯性，那就是我所做的一切是为了证明我很厉害，而不是为了轻松快捷高效的出成果捕捉价值，有时甚至还会故意给自己增加难度，这大概是所谓"累赘效应"？
- 只有一个例外，自己的健康。假如你一直要依赖别人，那怕这个人是专家（甚至一批专家医生），大概率也要失败，尤其在中国. 一般人的想法就是生病找医生，我自己就别费什么心了

- ## Would be nice if I selectively could make sub dirs of my monorepo public while the overall repo stays private.
- https://twitter.com/schickling/status/1645729275268538370
  - Building apps within a monorepo is critical for my workflows however it's usually too much overhead for me to separately factor out (and maintain) library code.
- The pain is real. I might have to setup git submodules
- https://github.com/facebook/fbshipit
  - This is what we used to use at Facebook for shipping parts if the monorepo to GitHub.
- what you need is josh. i guess we are overdue for another coffee chat…. i use josh + cgit
- I think this is why Google used SVN (which evolved into an in-house solution)
- IIRC @marius built a tool for this use case exactly
  - Grit is a tool to mirror monorepo subtrees to Github

- ## Tech "influencers" posting about how writing tests and submitting PRs is a waste of time.
- https://twitter.com/aboodman/status/1645859025165365249
- I hate these kinds of online discussions because nobody can see that they are talking about different things.
- If you are building a user-visible app (primarily what @t3dotgg does I think) then several things happen:
  - you want to iterate fast
  - the main thing that matters is "feel"
  - it's much harder to test
  - it's much easier to know (in real time) whether something broke -- yay metrics
- If you are building libraries, like say React or Replicache or vlcn, then I think it's pretty clear none of these points apply:
  - pure iteration speed is important but less so
  - the main thing that matters is correctness and stability
  - it's much easier to exhaustively unit test
  - it's much harder to know without tests whether something broke
- In summary, the real world is complicated, software is used for many different things, and when somebody is successful doing something you *don't* that's a *learning opportunity* not a bad thing.

- Somewhere I saw a video years ago where someone on the uber team said that they don't test, they just launch stuff incrementally and let metrics tell them how it's working.
  - And at the time that was such a novel idea to me, and so - for lack of a better word - elegant.

- Your product can “make it” with very little testing. But you’ll spend a year being very slow once you hit 150 eng and now no one can move without breaking something
- For complex frontend apps, especially involving rich text editors, if you dont write tests, you will end up playing whack-a-mole and waste so much more time than if you had just spent a few days on coming up with a good e2e testing abstraction
  - I dont wanna sound too snarky, and everyone in this thread has more experience than me but damn i saw both ends of this spectrum, and switched camps so fast

- ## 按照我的经验，接受这种烂代码，可以通过几个步骤来改进完善。
- https://twitter.com/dotey/status/1631325201274220546
- 做事之前要先收集收据。两个目的：1. 帮助分析问题，找出大的严重的问题；2. 为将来邀功和吹牛逼准备好基础。
  - 常见的数据包括：构建时间、响应时间、部署频率、新功能开发时间、bug修复时间、服务故障恢复时间、单测覆盖率、部署后回滚频率、生产故障频率等一切对将来你解决问题和吹牛逼有帮助的数据
- 先根据数据找出那种能短期提升效果的任务。这可以让你很快建立威信，让同事和老板相信你能做好事，给你更多机会。那种要花很长时间的留在后面再做，不然体现不出来能力，老板还不知道你在忙什么
  - 比如够构建时间太长，你可以写一些自动化帮助提升效率，瞬间就可以将部署时间从30分钟提升到3分钟
- 做某事之前先一定请示老板，要alignment，至少要得到默许。无论是老板还是员工，工作中都不喜欢太多的surprise，无论是惊吓还是惊喜。并且和老板聊之前，带上数据和方案，让老板知道你的想法是基于数据的，而不是基于你的主观想法，带来的收益有都少，时间资源成本又是多少，让老板支持你去做。
- 每做成一件事之后，不要怕小，都要找机会去演示，展示你的数据提升。像demo会议all hands会议都是露脸的好机会，群发邮件也不错，能让老板帮你邮件是最好的，聪明的老板会主动帮你做这事，毕竟你做好了事情老板脸上也有光，普通的老板在一对一会议中提一下一般也会帮忙。
- 没做好也没关系，大方承认，然后尝试复盘找出问题，下一个任务可以吸取教训。

- 一般像这样的烂系统，有些常见的短期提升的任务：
  1. 自动化构建，提升构建和部署效率
  2. 增加自动化测试，提升测试覆盖率，为将来重构做准备
  3. 部分重构，提升代码质量，提升可维护性，提升性能
  4. 增加日志和监控，提升故障发现速度，提升故障恢复速度
  5. 缩短发布周期，提升部署频率

- 要老板资源支持可能更重要：1）让老板认同重构的价值，老板不懂技术的话，要花点心思，2）老板愿意为了这点价值投入多长时间，多少资源，这两点可能决定了成与败。

- ## 有同事问我，你觉得重构中最重要的点是什么？我想了一下，回答道，是老板的理解和支持。
- https://twitter.com/michaelwong666/status/1676257775557705728

- ## engineering上的好的决策是重构出来的。
- https://twitter.com/geniusvczh/status/1594452820459388929
  - 最近在升级自己的parser生成器，为了检验它的能力我决定用它来parse C++，发现了很多缺陷，加了一些feature。

- ## Auto Generating Code Demo via ASTs for ag-grid
- https://www.slideshare.net/StephenCooper95/auto-generating-code-demo-via-asts

- ## TanStack Query v5 Roadmap_20221001
- https://github.com/TanStack/query/discussions/4252
- 👉🏻 proposal: remove all overloads and only allow all functions to be called with a single signature - one object
  - We have actually tried this already for v4

- ## With colour palettes, they often use specific colours as a bridge between many different colours. This often comes in the form of neutral tones like greys.
- https://twitter.com/JungleSilicon/status/1518090012004618240
  - This same system can be used to reduce the amount of compatible tiles that are necessary in tile sets.
  - For example if you have grass, ice, dirt and water tile types, you would generally need to create transitions between each type. Instead you could treat the dirt as the bridging tile type and then you only need to create transitions between dirt and the other types.
  - 👉🏻️ This flattens the workload required to create new tiles from `O(n)` into `O(1)` .
  - This kind of algorithm has inspired my thinking around interoperability and distributed computing. Not everything needs to be compatible, just create bridges.
- it reminds me of pipelining different programs together in a shell, and how the unix philosophy regards text as the "universal interface"

- ## A fundamental truth of development: You will spend much more time reading code than you will creating it.
- https://twitter.com/codecapers/status/1533937511222784000
  - That's why frameworks & tools that get rid of "boilerplate" code are practically useless.
  - Don't optimize for code creation... optimize for code understanding
- To optimize anything, we first have to make it explicit.
- Why use Next.js, when plain react would be "better" by this fundamental truth?
  - Next.js is designed to sell Vercel. They make it easy for you to do certain things in the hope that you'll deploy your web page to their platform.
  - There's nothing you can't do in Next.js that you can't do fairly quickly with any old bundler, React, React Router and the knowledge to wire it up to a backend.
  - But it's certainly easier to use Next.js than it is to have to create a backend, frontend and SSR setup - if that's what you need.

- ## “Programming is mostly about reading previous code, researching what is needed and how it fits within the current system, and planning the writing of features with small, testable increments. The actual writing of lines of code is probably…” — @samerbuna
- https://twitter.com/Yi_Xpress/status/1396602143575056389

- ## 经常有人说国产数据库底层都是mysql/postgres没啥意思，其实他们大概率没有真的去开发过数据库。
- https://twitter.com/niyue/status/1525081487175217152
  - 真的数据库大佬也说现在没法从头开发数据库了，得用个部份现成的轮子再去改进，不然做都做不完，
  - 类似于现在的浏览器都得基于chrome搞了，连微软都没有足够资源维护一个有竞争力的浏览器
- 说这话的是外行，几百万行代码，每一行我都重头写么，WAL/read view/read version/B+tree/lock coupling/行锁/死锁检测/CATS这些都是经典设计，我能hold住，有需要的话我有设计的idea，并且能实现我的设计就可以。
  - “国产”的本质是研发能力，不会被人卡脖子，不是说我要把page slot的二分查找都实现一遍
- 其实MS SQL Server也是基于Sybase搞的，搞的时间长了，就长得完全不一样了
- 分布式 TiDB 说是很厉害的嘛
  - tiflash是在clickhouse上面改的，不过说清楚了就行，改的多了其实可能都很不一样了
- 所以各大厂商才能卷起来啊，底层都是开源的数据库，比谁周边模块做得好，比用户体验，比扩展性，比SQL兼容，比分布式事务，比RTO RPO，比可用性几个9，比价格，比谁家的小弟公司多，比谁家的商务会来事，比谁家的SA会哄客户，比谁家的SER盯得住

- ## 2021 年 5 月的想法：借助云平台的便利，爆速开发。
- https://twitter.com/ThaddeusJiang/status/1512369748772003842
  - 2022 年 4 月的想法：借助平台只能开发原型，项目初期节省的时间，在项目中后期全都会回来的。
  - “走捷径才是最远的路。” ～ TJ
- 不知道算不算坑，但是确实成本很高。
  - 举几个例子：
  - 1. firebase 提供发送邮件功能，MVP 够用。实际需求是根据用户角色、地区、语言等，给客户发送不同内容。
  - 2. firebase 提供基本的 SSO 登陆，MVP 够用。实际需求是根据客户已经在使用的服务集成 SSO，例如 Microsoft，okta，onelogin 等等
- 我之前挺喜欢这类产品。目前会区分产品的发展路线， 如果我就只做一个月，我会用这些。如果我要做很久。我会用传统的技术架构。
  - 我现在不接短期项目了，太浪费生命了。

- ## How to quickly find out when debugging if an array of objects has duplicates
- https://twitter.com/AndaristRake/status/1505169709657997314
  - arr.forEach((el, i) => (el.__i = i))
  - and just inspect arr if some elements share the __i after that
- new Set(arr).size === arr.length
  - ye, the set thing is useful too but in this case i specifically have wanted to know **which** item is the duplicate

- ## @replayio is an elegantly simple product, but I think it gets at some really deep ideas about the human psychology of debugging
- https://twitter.com/geoffreylitt/status/1438152748449636360
- A question that has always fascinated me: why is print debugging so popular? Like, there are nice fancy step-based debuggers, but most devs just use print statements most of the time. Why?
  - One idea could be: we don't need fancy tools! Print debugging is simple 

    - and it's good enough to get the job done. People don't want to bother learning fancy tools.
    - Maybe some truth to that, but I don't think it's the main reason...

  - IMO, a main reason is that print debugging is actually *better* than step-based debugging in one key area: *showing time in space*.

    - With print debugging, I see what my program did from start to end; 
    - I can "scrub through time" by just scrolling up and down in the terminal.

- In contrast, in a step-based debugger, I'm stuck at one moment in time. 
  - It's hard to have a sense of place: where am I in the execution of the code? Gotta be careful not to step forward too far..
  - For me this leads to a vague sense of unease, even if I'm not consciously aware.
- The sad thing is, step-based debuggers are better in so many ways! Interactively evaluate code at any point. Explore live, no need to add print statements ahead of time. Etc. 
  - But still, I choose print debugging because showing time in space is the killer feature...
- Finally, this brings us to Replay. 
  - Simple idea: Just get the best of both of these worlds.
  - Like print debugging, it shows time in space. 
  - But way way better: I can actually scrub a timeline, I can see what my UI looked like at any point...
  - But also has all the normal benefits of step debugging. 
  - I can rewind to any point in the running program and interactively debug.
  - Also allows absurd things, like edit a print statement and see the entire log instantly retroactively update 
- They have impressive tech under the hood making this possible, but the dev experience is straightforward. Once you've fully wrapped your head around this idea, normal debuggers just start to feel primitive... can't wait for record-replay to become the new normal

- ## Note to self: If you face complex problems and don’t know where to start, there are three simple things you can do.
- https://twitter.com/hanspagel/status/1438107649330008064
  - Go for a walk and think about the actual problem 🌲
  - Read a book and learn how others solve it 📚
  - Start with the tiniest thing you can do *now* 💪

- ## Poll: How does your team do daily app development?
- https://twitter.com/housecor/status/1426893559056240645
  1. Call a shared dev environment database
  2. Call a dedicated database for each developer
  3. Call mock APIs
- #1 is common and the obvious default. But it's rarely the right answer.
- Why #2 or #3 are worth setting up:
  ✅ Stability
  ✅ Autonomy
  ✅ Faster iteration and feedback
  ✅ Supports fast, reliable APIs, which leads to fast, reliable tests 
- I'm not surprised simply because 1 is the default. 2 and 3 require extra up-front work, so you've gotta sell management on the need.
- #2 and #3 have an ongoing maintenance cost to take into account (#3 more so than #2) to keep feature parity. But still worth considering as its likely offset by the advantages you mentioned
- I use SQLite locally and move to sql server for production.
- I prefer a static dataset since it’s stable and can be augmented as we find edge cases we need to cover via tests.

- ## How I pivoted from an object-oriented programming style to a functional programming style
- https://twitter.com/housecor/status/1426191017968119813
  1. I stopped attaching behavior to objects. My objects are merely data structures.
  2. I create pure functions.
  3. I pass primitives/plain objects (with no behaviors) to these functions.
- I also do this in conjunction with my shift to "vertical slice" type architecture (vs the old n-tier/onion approach).

- ## If I want to create animations for video (nothing too complex: animated diagrams, simple illustrations) should I go straight to After Effects or are there more scoped-down tools to learn instead?
- https://twitter.com/steveruizok/status/1424799618559320068
- https://github.com/remotion-dev/remotion
  - https://remotion.dev/
  - Remotion is a suite of libraries building a fundament for creating videos programmatically using React.
  - Leverage web technologies: Use all of CSS, Canvas, SVG, WebGL, etc.
  - Leverage programming: Use variables, functions, APIs, math and algorithms to create new effects
  - everage React: Reusable components, Powerful composition, Fast Refresh, Package ecosystem
- PPT -> Video ?
  - not a bad option
- Really depends on what you mean by complex... sometimes Keynote is enough for me
- Rive also exports video and png sequences.
