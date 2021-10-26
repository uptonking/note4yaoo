---
title: job-react-faq-open
tags: [faq, job, react]
created: '2021-09-22T16:26:39.726Z'
modified: '2021-09-22T16:27:34.992Z'
---

# job-react-faq-open
# doing

- 介绍一下你用React做过的东西，为什么当时那么设计？
- 不废话了，来用React写code实现一个组件吧，比如Counter或者Todo。
  - 这两个例子太简单了，我面试的时候考的是写个文件树组件。



- 了解virtual dom的原理 ， 能不能手写一个virtual dom功能？


- 了解几种react的状态管理方法？（flux/redux/mobx）了解他们之间的区别么？用过那一种？
- 明白redux的工作原理么？能不能手写一个简单的redux
- 如何根据业务逻辑合理构建应用数据结构，进而定制 状态机制 ？
- 如何设计state、store


- 网络请求时如何处理race condition

- react组件系统有什么特点？在实际开发中，有没有自己封装过一些常用的组件。
- 使用react开发带给你哪些开发模式上的变化？
- react组件中，数据如何在子父/兄弟节点中传输？
- 对于react通用组件设计中，如何设计能增加组件的通用性和灵活性？
- 基于react开发的项目，怎么做性能优化？用过light house吗？（怎么避免大量的dom渲染）


- 如何做react的工程化和自动化测试？


- 觉得React体系（包括周边生态）有什么地方用着不大舒服吗？感觉可以用什么办法来改进？有自己的实现吗？
- React有什么可以向其他一些库或者框架借鉴的吗？
# open

- 怎么理解react传达组件的概念，react是view么，怎么看 state 的设计
- 兄弟组件的状态怎么互传，有哪些方法
- state的设计为什么是异步的，同步设计有没有问题
- ssr会有什么性能问题，哪些会引起内存泄露，引入 redux 后怎么处理请求的逻辑

- 怎么抽象一个带搜索，单多选复合，有请求的 Selector，区分 smart 和 dumped。如果我再往上加功能，比如 autocomplete 等
- 怎么实现对表单的抽象，数据验证怎么统一处理
- 用react来实现一个可视化编辑器的引擎，怎么设计，怎么抽象与model的交互，再引入redux呢，怎么支持第三方组件热插拔
- 用 react 和 redux 模拟多人协作的 Todo，node 作为后端，怎么设计

- 按需加载实现




# discuss

- 会用redux就完事，你还奢望其他的，10个react 8个半路的，不用单向流，2凑合用其中一个半还被卡学历啥的。现实里只要会用redux全家桶，store设计上能答出来 app store, domain store, state store我基本上就不往后问了。ssr我基本摒弃（有前提），不是说不好，坑太多，如果要集成第三方东西就要处理好多东西。用前置或程序判断下是不是爬虫，是的话丢PhantomJS或者之类的里面渲染。其他的泄露，就查吧webstorm 开个监控往死了点，看log重现现场吧。其实真觉得ssr少用的好，在受到业务制约的前提下，team里面积累又少，感觉真心没那么好，至少不伦不类。
