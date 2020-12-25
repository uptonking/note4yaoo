---
title: thread-react-dev
tags: [react]
created: '2020-12-25T15:22:27.224Z'
modified: '2020-12-25T15:22:49.750Z'
---

# thread-react-dev

## guide

## pieces

 

- ### Unit testing a react component is a waste of time in 99% 
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
