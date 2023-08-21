---
title: thread-lang-js-ts-proposal
tags: [js, proposal, thread]
created: 2021-09-14T06:29:14.993Z
modified: 2021-09-14T06:29:41.503Z
---

# thread-lang-js-ts-proposal

# discuss

- ## 

- ## 

- ## 

- ## 

- ## I've taken the time to articulate all of my thoughts in a single space about the current pipeline proposal. (It's opinionated, sorry)
- https://twitter.com/BenLesh/status/1436890184449236994
  - [TC39 Pipeline Operator - Hack vs F#](https://benlesh.com/posts/tc39-pipeline-proposal-hack-vs-f-sharp/)
- What Is A "Pipeline Operator"?
  - Simply put, the pipeline is an operator, |> in this case, that allows a software developer to "pipe" the evaluated expression from the left-hand-side (LHS) to some function or expression on the right-hand-side (RHS).
  - There were many competing proposals, two stood out the most, the Hack pipeline — currently in stage 2, and the F# pipeline — skipped despite being very popular.

- I was an early advocate of pipe, but the longer I've used JS the more I've gravitated(被吸引，吸引而转向) towards explicitness: debuggability over brevity. 
  - I favor the hack version but honestly in my day job I'd probably bias towards neither and use let.
- One of the biggest advantages of the F# pipeline is that it allows for destructuring of arguments- this is something I use _loads_, as I prefer working with single arg object instead of multiple parameters (creates inflexible APIs). You should list it in the cons for Hack.
- Piping is such a crucial FP concept, it's really strange that the proposal doesn't take partial application, the other crucial FP concept, into account. 
- Is it not possible to have both options?
  - Yes you would have both options if F# and partial application both landed. In fact, that would give us all the most options.
- I don’t really get why the community didn’t go for the F# way since it’s definitely the way  (most) FP minded people tend to think imo. If you’re not using pipe/compose at this point, you won’t use the pipe operator anyway.
  - Counterpoint: I'm going to use hack pipes all the time when they come to JS and I'm not very FP minded (IMO having every bit of logic abstracted into a small function tends to cost too much flexibility). Hack pipes would be awesome for everyone and would quickly spread
- Partial application has much wider applicability anyway, and should get in first to reinforce the cowpaths that ACTUALLY need to be paved.
- I agree deeply with your conclusion. The F# + partial application proposal makes much more sense than the Hack proposal. The Hack proposal feels really bad. JS has been making progress by adding features that make sense and compose well together. The second proposal makes sense.
- Sad they skipped the F# pipe.
# discuss-js-features
- ## 

- ## 

- ## 

- ## 虽然我知道 JavaScript 的 number 在精度上和其他语言不匹配，没有 int32 int64 这种细分，但我也不喜欢 long.js ，很容易出 bug。
- https://twitter.com/ThaddeusJiang/status/1693578008601526470
  - 建议轻易不要使用 long.js， 除非，你也上了 #gRPC #protobuf 的破船
  - 代码能跑，但结果不符合期待

- 我知道js只支持到2**53 但是我之前记得在那看过 新特性解决了这个问题 还支持有无符号 难道是我记忆错位
