---
title: pattern-arch-flux-elm
tags: [architecture, elm, flux, redux]
created: 2023-11-17T10:25:45.016Z
modified: 2023-11-18T09:48:30.897Z
---

# pattern-arch-flux-elm

# guide

- flux with event-sourcing

- redux [数据流](https://redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow)
  - action -> state -> view
- flux [数据流](http://fluxxor.com/what-is-flux.html)
  - action -> dispatcher -> store -> view
- elm [数据流](https://elmbridge.github.io/curriculum/The%20Elm%20Architecture.html)
  - message -> update -> model -> view (-> native-ui)
# faq

## 🆚️ redux vs flux

- flux的action是普通js对象
  - redux的action可以是function

- flux只有一个dispatcher
  - redux没有单独的dispatcher，store提供dispatch api

- 💡 flux支持多store，state可mutate
  - redux推荐单store，immutable，每次会返回整个store对象

- flux的计算逻辑在store，data transform
  - redux的计算逻辑在reducer

- ref
  - [The difference between Flux and Redux_201701](https://medium.com/edge-coders/the-difference-between-flux-and-redux-71d31b118c1)
  - [Why use Redux over Facebook Flux? - Stack Overflow](https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux)

## 🆚️ redux/flux vs elm

- redux开发的样板代码太多，redux-toolkit过于opinionated，代码复杂
  - elm的设计侧重简单易理解，如单store、mvu、去掉effect/signal

- redux action是js对象或函数
  - elm的message是函数

- effects的处理不同
  - Redux middleware were designed to enable writing logic that has side effects.
    - 参考方案有thunk/saga/observable/listener/rtk-query
  - elm的effects通过command/subscription处理

- 开发模式不同
  - react app由组件组成，组件通过connect从单store读取所需的state
  - elm app由单store驱动，state在全局顶层，开发者自己传递整个或部分store到view，可能包含复杂的数据传递逻辑

- flux不强调component和compose, redux推荐reducer compose
  - elm不推荐component，但model/view/update都可compose

- ref
  - [what is the difference between Elm and redux architecture : elm_201706](https://www.reddit.com/r/elm/comments/6jkt6c/what_is_the_difference_between_elm_and_redux/)
  - [Comparing Elm to React/Redux - DEV Community_201907](https://dev.to/rametta/comparing-elm-to-react-redux-2emo)
# dev
- 基于event实现undo的两种思路
  - 每个event的op同时保存inverse-op，每次undo时执行inverse-op
  - 每个event保存op，undo时从头开始计算一遍
# more
