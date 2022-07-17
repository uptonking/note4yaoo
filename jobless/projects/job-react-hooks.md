---
title: job-react-hooks
tags: [hooks, job, react]
created: 2021-09-23T05:19:27.323Z
modified: 2021-09-23T05:19:43.908Z
---

# job-react-hooks

# guide

# hooks原理
- rules
  - Only Call Hooks at the Top Level, not in if/loop
  - Only Call Hooks from React Functions

## [React Hooks: 没有魔法，只是数组](https://zhuanlan.zhihu.com/p/66923924)

- 在下面的实现里，state 是存放在被render的组件外面，并且这个state不会和其他组件共享，同时，在这个组件后续render中，能够通过特定的作用域方式，访问到这个state。
- 当首次render这个函数组件的时候。
  - 每一个 setter 函数，都关联了对应的指针位置。
  - 当调用某个 setter 函数式，就可以通过这个函数所关联的指针，找到对应的 state，修改state数组里对应位置的值
- 组件后续(非首次)每次render，指针都会重置为 0 ，每调用一次 useState，都会返回指针对应的两个数组里的 state 和 setter，然后将指针位置 +1。
- 每一个 setter 函数，都关联了对应的指针位置。当调用某个 setter 函数式，就可以通过这个函数所关联的指针，找到对应的 state，修改state数组里对应位置的值

- 为什么hooks的调用顺序不能变呢？
  - 将hooks的操作想象成数组的操作，如果顺序变了，那变化之后的hook就取不到正确的值了
- 因为调用hooks的过程中，我们是在操作数组上的指针，如果你在多次render中，改变了hooks的调用顺序，将导致数组上的指针和组件里的 useState 不匹配，从而返回错误的 state 以及 setter 。
# faq

## 

## 

## 

## 

## 使用 React Hooks 好处是什么

- motivation
  - It’s hard to reuse stateful logic between components; 
  - Complex components become hard to understand
  - Classes confuse both people and machines
- ~~函数式编程的风格~~

## React 加入 Hooks 的意义是什么？或者说一下为什么 React 要加入Hooks 这一特性？最后举例说一下 Hooks 的基本实现原理；

- 文档中的 “动机” 就很好的解释了为什么 React 要加入 Hooks 特性
  1：组件之间的逻辑状态难以复用；
  2：大型复杂的组件很难拆分；
  3：Class 语法的使用不友好；
- Rudi Yardley 在 2018 年的时候写过一篇文章 《React hooks: not magic, just arrays》，详细地阐释了它的设计原理
- 最重要的是，Hook 和现有代码可以同时工作，你可以渐进式地使用他们
