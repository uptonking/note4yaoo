---
title: log-dev-pieces-pattern
tags: [cs, dev, log, pattern]
created: '2021-01-01T20:38:51.480Z'
modified: '2021-01-01T20:40:14.733Z'
---

# log-dev-pieces-pattern

- about algorithms, data structures, design pattern

## logging

 

- [有限状态机通常在什么地方被用到？](https://www.zhihu.com/question/31634405)
  - 说一些我知道的：
    - 处理程序语言或者自然语言的tokenizer, 
    - 自底向上解析语法的parser各种通信协议发送方和接受方传递数据时
    - 升级版，如果状态之间的转换是有概率的，就是markov模型
      - 在markov模型基础上，如果每个状态时可观察到的所有现象都是按某种概率分布的，就是Hidden Markov Model (HMM)。
      - HMM在语音识别里用到的非常多。
    - 另外从软件工程角度说，如果你想实现状态机，可以看看设计模式里的 State Pattern
  - 工业自动化行业的顺序控制，理论基础就是有限状态机。
    - 如乙烯装置裂解炉的清焦程序，闭锁料斗的控制程序，煤化工行业气化炉紧急安全系统顺控程序
  - 处理各类输入的时候，比如编程语言的解释、正则匹配、图形界面上的按钮文本框等等
  - 我觉得FSM适合用在如下场景:
    - 状态跳转逻辑明确，特别是能够将一个问题的处理拆分成几个独立的逻辑状态，
    - 这时候在这些状态之间添加状态转移的连线，并附加跳转条件，这时候，FSM能够帮上大忙。
    - 另外，FSM的难点不在编程，在于理清楚状态转移图！
