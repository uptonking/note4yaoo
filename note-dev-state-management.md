---
title: note-dev-state-management
tags: [state]
created: '2020-10-31T19:09:23.017Z'
modified: '2020-10-31T19:11:26.567Z'
---

# note-dev-state-management

## guide

## pieces

- ### [How do you manage 'state' with vanilla js?](https://www.reddit.com/r/javascript/comments/9cdxwt/how_do_you_manage_state_with_vanilla_js/)
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
