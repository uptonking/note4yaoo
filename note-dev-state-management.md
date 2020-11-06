---
title: note-dev-state-management
tags: [state]
created: '2020-10-31T19:09:23.017Z'
modified: '2020-10-31T19:11:26.567Z'
---

# note-dev-state-management

## faq

- 组件内的state如何管理，component state

## guide

- 对象间数据(消息)的传递，可以通过pub/sub event实现，很适合component内状态管理
  - 简单的pub/sub没有考虑缓存数据，每次要使用数据都必须发送事件再次传递数据
  - 不支持跨page传递数据
  - 不支持数据持久化
- SPA中只有跨页面的信息才进入Store。基于这个原则，对Store进行精简、降级

## pieces

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

``` JS
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

- ### [How do you manage 'state' with vanilla js?_2018](https://www.reddit.com/r/javascript/comments/9cdxwt/how_do_you_manage_state_with_vanilla_js/)
- Variables are not managed, nor trigger updates on changes. 
  - State management can be done with variables if you proxy them or overwrite object properties with getter/setters.
  - Everything else resorts to polling or updaters, which will turn your app upside down if it functions asynchronously.
- Hopefully you're using es6 at least so you have classes which can store their own state, 
  - then it's a matter of making the class objects talk to each other in a parent class as necessary的传递，可以通过pub
  - pub/sub
  - flux
  - observables(Observer pattern)
- To be honest, if your code becomes complex enough that you actively have to worry about state and a few variables clearly don't cut it, you either bring in a small state management helper or write your own.

## ref

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
