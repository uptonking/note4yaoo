---
title: note-dev-state-management
tags: [state]
created: '2020-10-31T19:09:23.017Z'
modified: '2020-10-31T19:11:26.567Z'
---

# note-dev-state-management

## faq

- 组件内的state如何管理

## guide

- SPA中只有跨页面的信息才进入Store。基于这个原则，对Store进行精简、降级

## pieces

- ### [How do you manage 'state' with vanilla js?_2018](https://www.reddit.com/r/javascript/comments/9cdxwt/how_do_you_manage_state_with_vanilla_js/)
- Variables are not managed, nor trigger updates on changes. 
  - State management can be done with variables if you proxy them or overwrite object properties with getter/setters.
  - Everything else resorts to polling or updaters, which will turn your app upside down if it functions asynchronously.
- Hopefully you're using es6 at least so you have classes which can store their own state, 
  - then it's a matter of making the class objects talk to each other in a parent class as necessary
- Honestly, something like redux is already far more basic than what you're going for here. 
  - State is the single most important aspect of the application and hard to get right, if there's any place to use a well-established and tested lib it's for state. 
  - Doing this with a OO monstrosity(巨大而丑陋之物) with setter/getters and event subscriptions will work, 
  - but it'll grow, it'll be messy unless you add actions, demands will increase, you'll want to log, send error reports to a remote, etc. 
  - Like always when people are trying to avoid libs for no reason, in the end they'll write a bad one themselves with little to no benefit.
- What does vanilla mean to you? Are you rolling everything yourself? A couple patterns are:
  - pub/sub
  - flux
  - observables(Observer pattern)
- To be honest, if your code becomes complex enough that you actively have to worry about state and a few variables clearly don't cut it, you either bring in a small state management helper or write your own.

- ### [redux 有什么缺点？](https://www.zhihu.com/question/263928256)
- 需要写大量的 Action Creator 代码
- 需要写大量 switch case 分支判断
- Action 和 Reducer 分开书写，维护起来麻烦
- 异步操作，通常可以使用 thunk 中间件来做异步
- store里面的数据必须都是可以序列化的，比如普通文本，数组，不支持Map，Set等数据结构

- 模板代码太多，使用不方便，属性要一个一个 pick，对 ts 也不友好
- 触发更新的效率也比较差，connect 的组件的 listener 必须一个一个遍历，再靠浅比较去拦截不必要的更新
- store 的推荐数据结构是 json object
  - 这对于我们的业务来说也不太合适，我们的数据结构是图状，互相有复杂的关联关系
  - 适合用面向对象来描述模型，描述切面，需要多实例隔离，显然用 json 或者 normalizr 强行做只会增加复杂度，和已有的代码也完全无法小成本适配
- 基于 snapshot 的 time travel 内存占用高，性能差，并且没有配套的暂停、重启、切换、清空、事务等机制
- 无法做关联更新，每一次的所有变更必须由用户触发，既是优点又是缺点
- 非class的设计在ts下得主动写interface并在调用方声明，而 class 的好处是在于本身就能作为 type，并且可以利用 IDE做反向依赖查找
  - 在复杂业务中，函数式很难落地，包括类似游戏开发中的ECS架构，其实都很难实践，那一点点利用分级缓存提升的性能远远不如面向对象带来的优势更多，还是看业务场景和团队成员的。
- 对于自定义的class实例、引用类型、各个不同命名空间属性之间的互相引用似乎是不支持的，仍然需要设计成扁平化，通过 id 来关联，查找的时候显然是不如链式结构快的，并且很难用

## ref

- [A Very Basic State Management Library In Under 100 Lines Of JavaScript_2020](https://vijitail.dev/blog/basic-state-management-library-using-vanilla-javascript)
  - https://github.com/vijitail/Kel
  - This library is going to make use of the Pub/Sub pattern like most of the other libraries, so all the data will be passed around using events
- https://github.com/maiavictor/purestate
  - small state management library that is supposed to cover every use case of complex solutions such as Flux/Reflux/etc without the overengineering. 
  - The 1% that isn't pure should be written as if it was. Then, when you do need to mutate that 1% - just do it. Not indirectly like you do.
- https://github.com/Anekenonso/Vanillajs-state-magement
  - a Vanillajs state management app with no library or framework.
- [More than 100 different counter applications](https://gist.github.com/srdjan/1d10cbd42a2d695f696dee6b47fdc5e0)
- [Binding User Interfaces and Application State with Vanilla JavaScript](https://matswainson.com/binding-user-interfaces-application-state-with-vanilla-javascript)
  - https://github.com/matswainson/todo-list-application-state-example
  - https://codepen.io/matswainson/pen/RMoGmj
