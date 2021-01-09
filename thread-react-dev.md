---
title: thread-react-dev
tags: [react, thread]
created: '2020-12-25T15:22:27.224Z'
modified: '2021-01-06T14:40:11.360Z'
---

# thread-react-dev

# pieces

 

- ## How do you manage API calls in react
- https://twitter.com/_Adyasha8105_/status/1347978564251963392
  - Using a library like react-query 
  - or your own custom hooks 
  - or just plain fetch/Axios calls in components or inactions? 
  - What's the best way to go forward
- Short answer: react-query
  - Long answer: Axios was my base. 
  - I found state is kinda tricky when there’s too many request or components with CRUD operations (introduced xstate). 
  - then I realized a cache could help to improve UX (added react-query) 🙃. 
  - Start simple then build up
- I also created my own generic http class wrapper so if I want to swap between fetch, axios or something else, I won’t have to change in multiple places. 
  - have not tried React Query but it looks cool...
  - I just always am cautious of abstraction lib dependencies.
- I have not worked much in React But Axios did the work I needed

- ## JSX is an abomination(令人厌恶的事物).
- https://twitter.com/justinfagnani/status/1246514699341983744
  - You can't write a literal <, because that opens a tag, 
  - but you can't write &lt; either because JSX isn't HTML and doesn't support entities. 
  - You also can't write HTML comments, or use `<template>`.
  - JSX is clearly unsuitable as a general way to write HTML in JS.
- You can't event put a < inside of a string inside a JSX expression
- There are alternative ways of expressing DOM in JS though. For example: domz
- Recently ran into not being able to use `<template>` in React/Angular. 
  - Workaround is to use `dangerouslySetInnerHtml/[innerHTML]`. 
  - After that make sure that the sanitizer does not strip your Custom Elements
- JSX isn’t even made to “write HTML in JS”

- [My 5 Tips in Building a Design System](https://twitter.com/frostyweather/status/1087380930417840128):
  1. Build components without business logic, but hooks for data.
  2. Build UI components for/from products, not in the abstract
  3. Should be easy to onboard/understand
  4. Create code guidelines early on
  5. Strong processes involved = strong DS
  - I would add early and often 'collaboration' with the dev team to stay aligned.

- ## Unit testing a react component is a waste of time in 99% 
- https://twitter.com/oleg008/status/1235358013495676928
- here is why
  - React components are useless without React or a compatible runtime. 
    - You can see components also as "plugins" which together with the runtime make a framework and then an application.
  - React handles a lot of its side effects like hooks and rendering. 
    - Without all those things, most of the component code should be pretty dumb. 
    - If it's not, you should extract that logic into a separate function.
  - Once all your components are pretty dumb, there is no point in unit testing them, because it's like testing a configuration.
    - What you should be testing though if your component works as expected for an end-user.
    - which means you need functional or e2e tests. 
    - Depending on your use case it can be cypress and co, jest with JSDOM  or anything else that renders your component using React and validates the result same way a consumer would do.
  - Snapshot tests are rarely useful because they test only an HTML output of a component, 
    - which is ok if your user actually consumes HTML as a text, 
    - but most of the time this is not the case.
    - Your typical users in the browser see a DOM rendered presentation of your components, which includes all side effects, interactions and transitions and you are not testing those with snapshots.
- Unit tests are useless 99% of the time. It has nothing to do with react
  - I disagree with that. They are great for complicated functions.
    1. Making clear how they are supposed to be used
    2. Ensuring they work for the intended use cases.
  - Obviously no guaranties outside the unit bu thats expected. React components are a special case.
