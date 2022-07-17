---
title: lib-state-management
tags: [state]
created: 2020-10-31T19:09:23.017Z
modified: 2021-05-13T03:14:00.514Z
---

# lib-state-management

# faq

- 组件内的state如何管理，component/local state vs global state
  - 可以模糊组件状态和全局状态的界限
  - 对于复杂的state，组件内的state也可以使用单例的global state来管理，因为具体业务组件的数据是不同的，state的变化完全由开发者控制

- action或event如何设计能让debug更方便
  - 可以通过第三方日志工具打印出event信息
  - [Step over EventEmitter to the listeners in debugger](https://stackoverflow.com/questions/40469119/step-over-eventemitter-to-the-listeners-in-debugger)
    - 可以在浏览器控制台中设置blackboxing为事件源码文件，然后就可以调试跟踪到listener了
  - https://github.com/watson/event-debug
    - Log all events emitted by a Node.js EventEmitter object.
# guide
- 状态管理的主要任务
  - 读写状态，主要是更新：get/set/read/update
  - 状态变化后，通知应用程序变化的数据，通常会执行变化相关的回调函数
  - sharing：不同层级的组件如何共享状态
    - react采用的方式是状态提升，提升到最近公共祖先组件
  - persist
  - hot-reload, time-travel
  - 非UI类型State的处理，如身份验证、预设类型

- state分类
  - global/local: 根据状态的位置和影响范围
  - server-state: 与网络io相关的
  - router-state: 浏览器url相关的
  - style-state: 主题相关的

- 状态管理实验方案
  - 基于`data-`属性
  - 基于css variables

- css-vars pros
  - 浏览器直接支持，浏览器内置，符合标准
  - 实现简单theme切换非常方便，不用下载额外css文件，相关计算交给浏览器

- css-vars cons
  - 依赖浏览器，直接使用css variables的组件很难跨平台
  - 修改任何值时都会执行层叠覆盖，类似react context影响所有后代
    - 所以不适合用来实现通用的状态管理
  - css变量值必须是any valid CSS value
    - css的值的数据类型太单一，js的值可以函数、Map等，js更灵活
  - css内置的计算函数不够丰富，如比不过polish

- 对象间数据(消息)的传递，可以通过pub/sub event实现，很适合component内状态管理
  - 缺点：简单的pub/sub没有考虑缓存数据，每次要使用数据都必须发送事件再次传递数据
  - 不支持跨page传递数据
  - 不支持数据持久化
- SPA中只有跨页面的信息才进入Store。基于这个原则，对Store进行精简、降级

- ## The Modern Quadfecta of React State Management 
- https://twitter.com/flybayer/status/1337065452154089472
🏆 xstate  — simplifies complex logic (State machines)
🏆 zustand — simplifies flux principles (like Redux)
🏆 jotai   — simplifies atomic principles (like Recoil)
🏆 valtio  — simplifies proxy principles (like Mobx)
- Each of the four options are very powerful and can all mostly do the same things, but each one is better suited to different use cases.
  - NOTE: This does not include cached server state management which would be things like react-query, apollo, etc.
- zustand is a 100% redux compatible_ store = createStore().getState/setState/subscribe.
  - essentially bases on the same principles. 
  - it just doesn't force you to use providers, actions, action-types, reducers. 
  - the way it evaluates changes is the same.

- [State management solution 2021](https://www.reddit.com/r/reactjs/comments/nbh8ld/state_management_solution_2021/)
- for the last 2 years I’ve been working on 4 different, high quality and heavily used apps (mostly e-commerce). All of them only used Context API as a solution for state management and it worked very well.
- zustand is redux reduced to its fundamentals (flux state). 
  - jotai is recoil reduced (atom state) 
  - and valtio is like vue/svelte (proxy state). 
  - all three are on poimandres, and they all share the same philosophy: reduction without sacrifice.

- ## [web前端为什么很少用有限状态机设计框架？](https://www.zhihu.com/question/278938893)
- 我本身做游戏开发的，但是对前端有着很大的兴趣. 在游戏开发的时候处理不同的状态的切换避免过量的判断语句会使用有限状态机去实现.
  - 我觉得区别还是前端树状结构比较明显，所以整个问题可以用决策树（路由）或组件树（vDOM tree）+很简单的局部状态来建模，所以不会有游戏里那种 很大的有限状态机，局部状态用几个变量来存就行了
- 我之前的公司自己的前端框架还真是用了状态机，逻辑也全部用规则实现（规则引擎用的nools），写起规则，还真是可怕 ，尤其是调试和维护。有些不是很复杂的业务，用状态梳理好了挺简单，梳理不好的话，会特别复杂，要站在机器的角度，抽离状态，状态定义的要完全依赖开发者理解。状态定义，各种状态的切换，然后是规则的实现，调试，后期维护，一堆的东西，开发效率…你懂的
  - 太多的规则限制了 开发的灵活性 也会造成开发的时间归于漫长 但是规则也可以提高软件的健壮性 有些时间折中就好了.

- ## [Communicate Between Components](https://react-cn.github.io/react/tips/communicate-between-components.html)
- For parent-child communication, simply pass props.
- For child-parent communication: 
  - Say your GroceryList component has a list of items generated through an array
  - we're simply passing more arguments to `handleClick`. 
  - This is not a new React concept; it's just JavaScript.
- For communication between two components that don't have a parent-child relationship, you can set up your own global event system. 
  - Subscribe to events in `componentDidMount()`, unsubscribe in `componentWillUnmount()`, 
  - and call `setState()` when you receive an event. 
  - Flux pattern is one of the possible ways to arrange this.
- How about doing this so we can keep the benefit of type-safety?
- Works great for transitioning legacy non-React code. Another downside: we can't manipulate colors with polished.
- The only thing I don't like about CSS variables is that they are global, and we know what happens in large codebases with global stuff... Other than that, I too believe the Theme is perhaps more verbose and causes many rerenders, not an issue as long as they're cheap tho.
  - They're only as global as your scope for them (just like context).
- CSS variables are ultimate compilation target for CSS-in-JS!
  - It doesn't apply only to the theme, it applies to dynamic properties too.
- My only problem with css variables is that it makes sharing with react native more difficult. 
  - Still seems like the right workflow for 95% of use-cases
- I agree, especially the point about sharing CSS variables via a JS theme for static typing is really useful. 
  - The one thing I'm missing from CSS variables is to be able to use them in media queries
  - I guess there's no way around JS for now (if they depend on the theme).

- ## [Use CSS Variables instead of React Context](https://epicreact.dev/css-variables/)
- Turning to the CSS Variables approach, you'll notice the only component that re-rendered was our `ThemeToggler` component responsible for updating the `body`. And yet the user experience works perfectly! This is the magic behind CSS variables. 
  - With the `ThemeProvider` approach, we have to update the styles of every component, and then the browser paints those updates. 
  - But with the CSS Variables approach, we update the styles to a single component (the `body`) and then the browser paints those updates. 
  - The browser paint should theoretically take the same amount of work on the part of the browser, so **the only difference** is how much work we're making the browser do to have React re-render all our components and get emotion to update the styles of every component.
  - This can have negative performance implications as your app grows.

- https://twitter.com/kentcdodds/status/1324026743099781120
- We took a similar approach with @stitchesjs
  - Tokens are converted to CSS Custom Properties
  - Reference token in CSS value without prop-interpolation
  - Support nested and/or multiple themes on the same page
- My favorite is both. 
  - Favor CSS variables but still update a context so that you can switch out the components **for advanced use cases that have different rendering**.
  - Also update the CSS variables in useLayoutEffect so it happens at the same time as the context change.
# pieces
- event-pub/sub vs browser event
  - 目前CustomEvent的支持率达到了99.38%，几乎所有浏览器都支持，IE9-11部分支持
  - What your describing is the difference between
    - A custom event based message passing system
    - manually firing DOM events.
  - The former is a way to use events for message passing. 
    - An example would be creating an `EventEmitter`
  - The latter is simply a way to use the browsers built-in DOM event system manually. 
    - This is basically using the DOM 3 Event API which natively exists in (competent/modern) browsers.
  - Benchmark showing DOM 3 custom events is 98% slower
  - The DOM appears to have a huge overhead(管理费用). 
    - It does so because it supports event propagation and bubbling. 
    - It does because it supports binding events to a DOMElement.
  - If you do not need any of the features of DOM3 events, then use a pub/sub library of choice.
  - The most obvious "con" to using the DOM methods is that 
    - they're tied to browser-based deployments and involve the DOM in things even if it doesn't really make sense (e.g., the messaging isn't related to DOM objects), 
    - whereas a standard Observer-style implementation can be used in any environment, not just web browsers, and with any generic object you like.
  - The most obvious "con" to doing your own Observer implementation is that
    - you've done your own Observer implementation, 
    - rather than reusing something already present (tested, debugged, optimised, etc.) in the environment.
  - ref
    - [What is the difference between different ways of Custom event handling in JavaScript?](https://stackoverflow.com/questions/6570523/what-is-the-difference-between-different-ways-of-custom-event-handling-in-javasc)
    - [Custom Event emitter/consumers in Browser Javascript outside DOM](https://stackoverflow.com/questions/51110935/custom-event-emitter-consumers-in-browser-javascript-outside-dom)
      - 借助DOM通过自定义事件传递数据时，事件属性会继承所有基类属性，如bubble、detail等，而这些属性可能与业务数据无关

```JS
// 提供一个示例元素
let obj = document.body;
// add an appropriate event listener
obj.addEventListener("cat", function(e) { console.log('detail, ', e.detail) });

// create and dispatch the event
var event = new CustomEvent("cat", {
  detail: {
    evtContent: 'true'
  },
  // 默认值
  bubbles: false,
  cancelable: false,
  composed: false
});
// 本对象触发的事件，可以触发注册在本对象上的方法，这里提供了一种传递数据的新思路
obj.dispatchEvent(event);
```

- redux vs pub/sub
  - pub/sub没有直接考虑数据缓存
- [Is there a React (state related) event pub sub pattern when replacing Redux?](https://stackoverflow.com/questions/61533575/is-there-a-react-state-related-event-pub-sub-pattern-when-replacing-redux)
  - Redux is "an event pub/sub at the root level", and can specifically be beneficial in cases where widely separated components need to make use of the same data.
- [Explain Redux like I'm five](https://dev.to/hemanth/explain-redux-like-im-five)
  - Redux is a silly concept. Combination pubsub and global variable. 
  - But the author take it very seriously. 
  - Build as framework, has ability to customize and plug in. 
  - And also great tooling such as time travel.
  - In the end, the author prove good insight. Global variable is good for client application
  - My suggestion is use redux if you need time travel. If not, event emitter is much simpler
  - action creators with state objects do help time travel debug but they prevent proper typechecking, to get around JS problems. if using typescript they get in the way.
  - I also prefer event emitter because the pub/sub API is so much clearer.
    - but redux connect() does automate some processes you'd have to setup yourself otherwise
    - and mapStateToProps to filter which events you want to sub to.
  - All this could be done with a much simpler event emitter module though.
  - Usually when i adopt redux I'll wrap in my own TS code to hide the boilerplate in a single place.
- [React Application and Global Event Bus](https://www.reddit.com/r/reactjs/comments/7o6gz7/react_application_and_global_event_bus/)
  - I have a side project React application that exists alongside other javascript applications. 
    - I would like to have a two way communication pattern between "external" javascript and internal React events. 
    - An example of this might be passing "state" data between outside applications to the React app, 
    - or triggering specific behavior on the React application (or vice versa).
    - For example, it would be cool if the external JS could mount/unmount the application as needed, or "reset" the application state.
  - I have a few options:
    - Use custom browser window events. 
      - This is basically already supported, but worried I might run into browser specific issues or odd handling of events. 
      - It does seem well suited to this.
    - Some kind of pub sub library attached to the window, either something I write or an existing lib. 
      - This is more work, but might be a better long term solution. 
      - Thinking of this as housing or controlling callback functions.
    - Some kind of functional promise/callback system, maybe overlapping with #2. 
      - I've seen some interesting things related to Redux pub/sub
  - I dealt with something very similar recently. 
    - I work with a legacy codebase, and am developing a react codebase along-side it. 
    - Essentially the legacy codebase takes care of the site furniture, 
    - and react takes care of the core rendering of the page.
    - we already have a pub/sub AMD module in the legacy codebase, 
      - so I went with something similar to option #2 - 
      - Though the pub-sub module was re-written.
  - From a high level, the solution was to extract the pub-sub module into a shared resources area of the codebase, and code them with no dependencies (raw basic JS).
    - From there, update the legacy require config to alias the old location of the pub-sub module, to avoid reworking where it was previously used.
    - In React, I wrote a redux enhancer to listen to the pub-sub channel, and ingest the data object that was passed through as if it were a redux action.
  - I'm having a hard time understanding why you would roll your own pubsub system when the browser gives it to you for free. 
    - Overhead maybe? I've heard DOM events can be a performance drag.
    - A combination of cross-browser support and legacy layover.
      - We support IE9, which uses attachEvent instead of addEventListener. 
      - It would be silly to make that check every time you want to pub/sub, so a local module can just alias that and standardise it.

- [I was asked today if it is OK for an action to trigger multiple effects.](https://twitter.com/MikeRyanDev/status/1003737879930130435)
  - The answer is YES. 
    - That is why there is indirection between actions, reducers, and effects: 
    - actions may be the inputs to multiple state changes and side effects.
  - Why don't we just stick to Pub Sub design pattern
    - Pub Sub is too generic. Redux/flux is kind of a specialized form of pub sub. 
    - In JavaScript, we’ve been using pub sub since forever, but it was a mess usually.
    - Redux added structure to it.
  - Everywhere it's like use setState for local state and lift state if you want to share state. 
    - If lifting has to be done too much, then consider redux or mobx
- Does Redux follow the pub/sub pattern?
  - yeah. Each connected component subscribes to the store
  - any changes reach state and are mapped to props. The reducer handles all message traffic.

- ## [How do you manage 'state' with vanilla js?_2018](https://www.reddit.com/r/javascript/comments/9cdxwt/how_do_you_manage_state_with_vanilla_js/)
- Variables are not managed, nor trigger updates on changes. 
  - State management can be done with variables if you proxy them or overwrite object properties with getter/setters.
  - Everything else resorts to polling or updaters, which will turn your app upside down if it functions asynchronously.
- Hopefully you're using es6 at least so you have classes which can store their own state, 
  - then it's a matter of making the class objects talk to each other in a parent class as necessary的传递，可以通过pub
  - pub/sub
  - flux
  - observables(Observer pattern)
- To be honest, if your code becomes complex enough that you actively have to worry about state and a few variables clearly don't cut it, you either bring in a small state management helper or write your own.
# ref
- [A Very Basic State Management Library In Under 100 Lines Of JavaScript_2020](https://vijitail.dev/blog/basic-state-management-library-using-vanilla-javascript)
  - https://github.com/vijitail/Kel
  - This library is going to make use of the Pub/Sub pattern like most of the other libraries, so all the data will be passed around using events
  - [reddit discussion](https://www.reddit.com/r/javascript/comments/gbj8qm/i_created_a_very_simple_state_management_library/)
    - My thought process behind this was that the store should be the single point of truth for all the global data. 
    - Having multiple instances of the store would make it difficult for the consumer to keep track of the data.
    - On the other hand, having multiple stores will give the user liberty to manage data for each component independently.
    - both of those things make sense. It doesnt seem like the library should make that decision for the code consuming the library tho.
- https://github.com/maiavictor/purestate
  - small state management library that is supposed to cover every use case of complex solutions such as Flux/Reflux/etc without the overengineering. 
  - The 1% that isn't pure should be written as if it was. 
  - Then, when you do need to mutate that 1% - just do it. Not indirectly like you do.
- https://github.com/Anekenonso/Vanillajs-state-magement
  - a Vanillajs state management app with no library or framework.
- [More than 100 different counter applications](https://gist.github.com/srdjan/1d10cbd42a2d695f696dee6b47fdc5e0)
- [Binding User Interfaces and Application State with Vanilla JavaScript](https://matswainson.com/binding-user-interfaces-application-state-with-vanilla-javascript)
  - https://github.com/matswainson/todo-list-application-state-example
  - https://codepen.io/matswainson/pen/RMoGmj
  - In this article I would like to explain and show an example of how creating a centralised application state can help you handle and manage your application's User Interface.
  - For this example, we will be storing the data using localStorage.
  - The Store class will be used to save and load list items to localStorage when needed
- [What problems are state management libs solving? Can't you just create a singleton/static class and be done with it?](https://www.reddit.com/r/javascript/comments/d6lw4c/askjs_what_problems_are_state_management_libs/)
  - I think if you come from React, state management is ingrained(根深蒂固的；日久难改的) into you. 
    - I come from Angular, and I just use a service to hold an application-wide data model. Works great.
