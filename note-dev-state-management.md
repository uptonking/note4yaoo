---
title: note-dev-state-management
tags: [state]
created: '2020-10-31T19:09:23.017Z'
modified: '2020-10-31T19:11:26.567Z'
---

# note-dev-state-management

## guide

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

- ### [Build a state management system with vanilla JavaScript_2018](https://css-tricks.com/build-a-state-management-system-with-vanilla-javascript/)
  - https://github.com/hankchizljaw/vanilla-js-state-management
  - Traditionally, we’d keep state within the DOM itself or even assign it to a global object in the window
  - Libraries like Redux, MobX and Vuex make managing cross-component state almost trivial(微不足道的，不重要的)
  - We’re creating the functionality that allows other parts of our application to subscribe to named events.
  - Another part of the application can then publish those events, often with some sort of relevant payload.
  - The PubSub pattern loops through all of the subscriptions and fires their callbacks with that payload.
  - Let’s take a look at how our Store object keeps track of all of the changes. We’re going to use a Proxy to do this
  - Usage of DOM Api will prevent possible SSR

- ### [State-based components with vanilla JS](https://gomakethings.com/state-based-components-with-vanilla-js/)
- State is data at a particular moment in time. It’s the present “state” of your data.
- If you’ve done simple DOM manipulation before, you’ve probably gone through the task of:
  - Getting an element from the DOM (using `querySelector()` or something similar), and then…
  - Adding content with `innerHTML`, or…
  - Using `classList` to add or remove classses, or…
  - Using `style` to update some styles.
- This works, but as your apps grow, it can be tedious to manage.
- Today’s more popular JavaScript frameworks, including React and Vue, use state and components to make managing the UI easier.
- With this approach, instead of targeting specific elements in the DOM and adjusting a class here or a style there, you treat your data, or state, as the single source of truth.
- Updated your state, render a fresh copy of the UI based on the new data, and move on. 
- You never have to think about which element in the DOM to target or how it needs to change.
- In the previous example, the state was a global object that any function can access.
- To give your code more structure, you might instead scope state to your component. 
  - This is how React, Vue, and other popular frameworks do things.
- The nice thing about scoping state to a component like this is that you get out of the business of targeting individual elements and manipulating specific things within them.
- With a scoped component, you update your state and then render your template. You don’t need to hunt for individual items.
- Your data is the single source of truth, and it makes updating the UI easier and more consistent.

## ref

- [A Very Basic State Management Library In Under 100 Lines Of JavaScript](https://vijitail.dev/blog/basic-state-management-library-using-vanilla-javascript)
  - https://github.com/vijitail/Kel
  - This library is going to make use of the Pub/Sub pattern like most of the other libraries, so all the data will be passed around using events
- https://github.com/maiavictor/purestate
  - small state management library that is supposed to cover every use case of complex solutions such as Flux/Reflux/etc without the overengineering. 
  - The 1% that isn't pure should be written as if it was. Then, when you do need to mutate that 1% - just do it. Not indirectly like you do.
- https://github.com/Anekenonso/Vanillajs-state-magement
  - a Vanillajs state management app with no library or framework.
- [More than 100 different counter applications](https://gist.github.com/srdjan/1d10cbd42a2d695f696dee6b47fdc5e0)
