---
title: thread-dev-engineering-stars
tags: [engineering, thread]
created: '2021-08-10T03:50:40.299Z'
modified: '2021-08-10T03:51:01.891Z'
---

# thread-dev-engineering-stars

# discuss

- ## 

- ## 

- ## 

- ## 

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
