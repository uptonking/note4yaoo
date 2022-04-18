---
title: lib-state-machine
tags: [state, state-machine]
created: '2021-03-23T15:50:17.581Z'
modified: '2021-05-13T03:13:52.403Z'
---

# lib-state-machine

# guide

# discuss
- ## Who is using XState in production?
- https://twitter.com/DavidKPiano/status/1514944861341892612
  - And what kinds of features/tools would make it even more useful for you and your team?
- 1. Better syncing with external state (in the real world we’ll always have a redux store that needs syncing). Now we have to rely a lot on “always”.
  2. When a transition happens from A->C (without passing over B) is kind of hard to debug.
  - For 2. the plan is to make it easier to inspect microsteps in v5.
- XState has indeed made me so much more productive and the codebase easier to read. For now everything is perfect and the TS support keeps getting better and better. I just wish "sendParent" was just working for child -> parent communication.

- ## I break down a step-by-step process for how I model statecharts
- https://twitter.com/mpocock1/status/1493236276899815424
  - https://www.youtube.com/watch?v=wykDyFwr8Lk
1. List the events
2. List the side effects
3. Figure out the machine's lifecycle
4. Figure out the first state
5. Use the events as paths to create new states

- ## [statechart vs state-machine](https://stackoverflow.com/questions/37034913)
- A state machine is a mathematical model of computation that is less general purpose than a Turing Machine. 
  - Another common usage of the term "state machine" is the code that implements that model and runs on a computer.
- In contrast, a state chart is a description of a state machine, usually represented as a diagram or a table. 
  - The word "chart" is Latin for "paper", so it implies something written or drawn.

- [Difference between a statechart and a finite statemachine (FSM)?](https://stackoverflow.com/questions/8190385)
- A state machine is an abstract machine for parsing strings of input in a formal language, while a state diagram is a UML description of the different states a system (subsystem, etc) may assume and how it may transition between them.
- The state diagram on the other hand says (among other things) that some system may be in one of three main states; 
  - that it assumes state 1 upon startup; 
  - that it can transition from state 1 to state 2 or state 3; 
  - and that it can terminate from state 2 but not from state 3.

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

- 基于状态机实现解析器的示例
  - https://github.com/GeeLaw/bibtex-ts/blob/master/src/ObjectModel/ParseDatabase.ts
  - remark > micromark
