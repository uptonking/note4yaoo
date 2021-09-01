---
title: lib-state-machine
tags: [state, state-machine]
created: '2021-03-23T15:50:17.581Z'
modified: '2021-05-13T03:13:52.403Z'
---

# lib-state-machine

# guide


# discuss
- ## 状态机 vs 正则
- https://www.zhihu.com/pin/1395368116139036672
- 用状态机的方式就是一个个接受字符，然后做状态流转，扩展状态很容易。
- 用正则的好处就是很容易提取token，但是case多的时候正则不好维护，而且扩展困难。
- 状态机是对每个字符做状态的判断和流转，正则是一次匹配一批字符。
- 词法分析还是状态机靠谱，但是简单场景用正则来做会比较简单，比如 vue template parser。
- 正则的方式会随着 case 的增多，复杂度越来越高，而状态机的方式只是加几个状态，复杂度会维持在低水平。
- 从架构来说，状态机适合大型的不断迭代的 parser，正则适合简单的不经常变动的 parser。
- 状态机能够很好的治理随迭代增加的复杂度，正则不行。
- 正则写起来简单，维护和迭代困难

- 谨慎使用正则，这东西可读性太差。
  - 我的原则是，如果你写了一个正则，不能在3s内肉眼parse出来语义的话，那就不要写正则了，换另外一种方式。

# ref
- [A reducer is a single-state state machine](https://erikras.com/blog/reducer-single-state-machine)

- https://github.com/statelyai/xstate-viz
  - https://stately.ai/viz
  - Visualize XState state machines and statecharts in real-time.
