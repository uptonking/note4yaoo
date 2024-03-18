---
title: thread-lang-js-toolchain
tags: [lang-js, thread, toolchain]
created: 2024-03-17T15:24:08.363Z
modified: 2024-03-17T15:24:20.824Z
---

# thread-lang-js-toolchain

# guide

# discuss-stars
- ## 

- ## 

- ## 你混淆过的JS代码将和“开源代码”没区别，ChatGPT可以轻松将你混淆后的代码还原。
- https://twitter.com/HeySophiaHong/status/1769238857286086886
  - 编译过后的代码也不安全，现在已经有研究能反编译二进制了

- js的混淆并不是主要为了安全
- 如果是前端，做什么加密混淆都意义不大
- The purpose of Uglyfying is just to minify the size of the js file.

- 想靠“加密”前端代码来获得安全方面的保护，本来就是自欺欺人的做法。 拆穿这个假把式有益帮地球省点能源。

- 这星期刚试过，真的看起来可行，虽然也可能存在一定幻觉，但是可信度不低，拿来还原80-90%的逻辑能节省不少工作量

- 反编译这项工作的确适合AI做，各种混淆器再厉害也架不住AI的大数据训练。
# discuss-testing
- ## 

- ## 

- ## [Best test framework for Node in 2022? : r/node _202209](https://www.reddit.com/r/node/comments/xhb4bi/best_test_framework_for_node_in_2022/)  
- We use Mocha with Chai for tests - works perfectly. 
  - We use c8 for coverage, which is a drop-in replacement for nyc which doesn't (or didn't when we switch) support `import` . 
  - We then use husky for managing git hooks, such as ensuring all tests pass to allow a push (which can be forced through if needed).

- Mocha and Chai are a terrific mixture. Chai offers a plugin system which may help with testing. I think it's worth mentioning.

- One thing that Jest has — both for better and for worse — is a module mocking mechanism. With your mocha + chai setup, do you ever find that you need to mock out a dependency of the module that you are testing? If yes, how do you do it?
  - Sinon if you have to. Restructuring your code so you don't have to mess with imports when you need mocks is a better move, though.

- Chai is an assertion library; it is meant to facilitate writing assertions. You want to use Sinon for anything spy related.
- Jest is okay but still very FB and React-oriented. On the front end, with a React project, I would use Jest only if required. Jest is not better than these three.
- The combination (Mocha, Chai, Sinon) covers all types of tests. You are never let down.

- We use node-tap at work which is similar to the new experimental nodejs test runner. There is also AVA which is also popular. I tend to lean more towards test runners that don’t pollute the globe namespace, that have a reduced api and rely less on mocking. If you write pure functions, then testing becomes much simpler and not much need for mocks.

- I maintained Mocha for 5 years and added parallel execution support.
  - Jest has certain limitations that you should be aware of when testing Node.js code or ESM in particular.
  - You can test just about anything with Mocha, but not out-of-the-box. Module mocks can be handled by something like rewiremock. Snapshots with other plugins; often these are plugins for assertion libs. OTOH if you’re using ESM w/o transpilation, mocking modules is much more painful due to limitations of the spec.
  - node-tap and ava work great. node-tap is especially well-written.

- ## [Jest or Mocha for testing Nodejs Application : r/node _202110](https://www.reddit.com/r/node/comments/q55mh2/jest_or_mocha_for_testing_nodejs_application/)
- A thousand times jest, because it gets coverage right, which mocha doesn't.

- The only reason to use jest is to support React component testing, and that's still not a great reason because there are solutions to this problem now that use mocha. Mocha is soo much faster and less complicated. The testing support that Jest provides that Mocha does not can be added in through the use of Sinon and other packages if needed. Jest tries to support too many test needs and does none of them well. I'll never use jest in a project again. Mocha is always the right choice.

- mocha and native assert
# discuss
- ## 

- ## 

- ## 
