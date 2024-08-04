---
title: thread-dev-engineering-refactor
tags: [engineering, refactor]
created: 2023-11-15T08:20:29.241Z
modified: 2023-11-15T08:20:46.678Z
---

# thread-dev-engineering-refactor

# guide
- refactor
  - before adding a new feature
  - before fixing a bug
  - before doing an improvement
# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 对一个curd 的部分进行 batch  化改造，原理很简单，过程很麻烦，最后还要写一篇设计文档
- https://x.com/suohawking/status/1800096913997660317
- batch 后再并行，并行后再分布式并行，分布式并行后再并发，并发后再限制并发，限制并发后再动态调整并行度和并发度，这辈子的工作量有了
- 我在对一个 polling 实现的 batch 的 curd，用 message queue 进行实时化改造

- ## 今天看到有人转发一个关于维护 Oracle database 💩山代码的文章
- https://twitter.com/beihuo/status/1729624234585108518
  - 我意外发现我从中学到了东西，那就是不要重构。
  - 通过 flag 的方式将 bug 修好，或者将新功能塞进去，反而是正确的一种做法。重构这种系统，得不偿失。
- 前提是巨量的自动化测试
- 代码基数达到一定规模是没办法重构的，没有这个选项
- 重构的前提是代码量要小、维护的人要少、重构要频繁和坚决；同时要坚信，任何具体的特定事情都不应该基于大规模的代码才能完成，也就是，不要写大程序。

- ## 人人知道好代码长啥样，知道事后要重构对自己和团队的价值
- https://twitter.com/tison1096/status/1724458303701618709
- 这不只是员工的问题，尤其是如果只是公司内部闭源代码，写好了有什么意义呢？团队有一致的追求，不只是说个人素养，也是说做好了确实有肉吃。 另一个例子就是公司 HR 说大家都是家人.. 终身雇佣制可以考虑，合同一年一签三年一签，动不动开除裁员，谁跟你家人啊

- 重构只有在需求变更（增加）的时候才合适呀，如果一块需求没有变更，测试通过就不需要变动。频繁重构需要很“重”的单体做支撑，而且是一个负循环，重构越频繁，单体滚的越大。所以，最优解就是代码一遍完成，不挨打就不动手重构
- 昨天1-1老板还让我没事别提重构，“有用户需求才能考虑重构”，我听得都傻了，现在准备赶紧跑路…

- 曾经顶着非常大的压力重构了一个六七年的老项目，自己加班搞了半年多，搞完后内部开发提效了不少，对产品和老板并没有什么效益，反而给测试找了不少麻烦。现在我的做法是把屎山尽可能的去包起来，而不是去在里面洗澡

- 为什么开源项目才能比较自由的追求代码之美？因为只有纯种技术人员才能不计得失得追求完美啊。

- 一个功能设计加实现需要一周，糊一个能用的功能可能一天二天，进度有了效率有了，至于后面花三周修bug成本就被均摊了，况且交付使用不一定触发bug。再放长点，三年做个产品，还没做完公司倒闭了，政策转向了等等…所以设计啊质量啊都会被降优先级。不过我始终觉得技术人应该理解但不该轻易妥协这种情况

- ## I've wished that *ALL* of @nozzleio was written in TypeScript. 
- https://twitter.com/tannerlinsley/status/1382435100449591296
  - In true @getsentry style, expect a lengthy post-mortem(事后反思) about the imminent(即将发生的) transition/rewrite.
- Please tell me how you attack this because there's a 200k+ line codebase I'd like to do this for
  - First step is likely setting up tooling to let TS and JS files build and coexist.
  - From there, it's about how you want to tackle converting files. I opted for hand-converting one at a time. Tried a couple different auto-migrate tools but wasn't impressed with the output.
  - First file should probably be some tiny utils file, just so you know that TS is compiling anything at all and the app still loads.
  - From there, pick a few key core files, convert, start writing types for critical data structures. Branch out from there.
- I've read several of these "we migrated our whole codebase to TS" posts, and the common themes are usually:
  - A few key folks driving the effort
  - Get buy-in by socializing with other devs
  - Long-term process
  - Have to interop JS+TS
  - Track progress over time
- In my case, we have a typical Express CRUD server, plus about 20K lines of pure business logic.
  - I set up `ts-node` for dev, and just call `tsc` to build for prod. 
  - I have it outputting JS files in the original folders vs a separate build folder.
  - [best practices for refactoring 60k LoC JS project to TS?](https://www.reddit.com/r/typescript/comments/j512sf/2020_best_practices_for_refactoring_60k_loc_js/g7q6hvw/)
