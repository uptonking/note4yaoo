---
title: pattern-arch-flux-elm
tags: [architecture, elm, flux, redux]
created: 2023-11-17T10:25:45.016Z
modified: 2023-11-18T09:48:30.897Z
---

# pattern-arch-flux-elm

# guide

- flux with event-sourcing
- functional 插件架构

- 自定义view层(state + presentation)的实现参考
  - 主流开源组件的渲染层实现，如 typewriter/tanstack-table/odoo-spreadsheet
  - https://github.com/matthewp/views-the-hard-way
  - https://github.com/nolanlawson/emoji-picker-element

- 
- 

- redux [数据流](https://redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow)
  - action -> state -> view
- flux [数据流](http://fluxxor.com/what-is-flux.html)
  - action -> dispatcher -> store -> view
- elm [数据流](https://elmbridge.github.io/curriculum/The%20Elm%20Architecture.html)
  - message -> update -> model -> view (-> native-ui)

- 渲染层的架构和实现可参考flutter
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
- 👉🏻 基于op/event实现undo的两种思路
  - 每个event的op同时保存inverse-op，每次undo时执行inverse-op
  - 每个event保存op，undo时从头开始计算一遍
  - 缺点是异步op要特殊处理，可能部分要忽略; 复杂度较高
  - 优化方案是定期snapshot
- 👉🏻 基于delta-state实现undo
  - 优点是数据量小，replay状态时无需考虑异步op/effects
  - 缺点是多人协作时不方便撤销他人的中间op
- 👉🏻 基于全量state实现undo
  - 优点是实现简单，replay状态时无需考虑异步op/effects
  - 缺点是每次保存全量数据可能导致性能问题和空间浪费，多人协作时不方便撤销他人的中间op
# elm-dev

# hyperapp-dev
- undo/redo因为action是fn实现较麻烦
- 实现undo可参考devtools https://github.com/mrozbarry/hyperapp-debug
# [changelog-elm](https://elm-lang.org/news)
- v0.19_201808
  - 🚨 Removal of custom operators and native modules
  - Smaller assets, faster builds
- v0.18_201611
  - New debugger with import/export
- v0.17_201605
  - Add subscriptions, remove signals
- v0.14_201412
  - Package manager, parallel builds, JSON
- v0.3_201206
  - Modules
- v0.1_201204
  - Elm was initially designed by Evan Czaplicki as his thesis in 2012
  - The first release of Elm came with many examples and an online editor that made it easy to try out in a web browser
  - The initial implementation of the Elm compiler targeted HTML, CSS, and JavaScript
# more
