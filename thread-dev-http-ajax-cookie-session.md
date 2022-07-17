---
title: thread-dev-http-ajax-cookie-session
tags: [ajax, cookie, http, jwt, session]
created: 2021-08-06T08:30:13.653Z
modified: 2021-08-06T08:32:26.142Z
---

# thread-dev-http-ajax-cookie-session

# discuss
- ## 

- ## 

- ## 

- ## After 3 years, I still love that data fetching hooks maximize the concurrency automatically. Which has been something tricky with awaits/Promises.
- https://twitter.com/shuding_/status/1529264553900531712
  - Data dependency is a directed acyclic graph. We used to describe that graph using `Promise.all` s, but in many cases it's still not optimized enough.
  - With Dependent Fetching, we can walk through it as parallelized as possible (no extra code needed).

- ## Thunks are great for "run some code now and dispatch eventually" logic, but they can't _listen_ for other actions.
- https://twitter.com/acemarke/status/1440494692836069392
  - Sagas and observables are widely used for that, but they're heavyweight syntactically and conceptually.
- Would love to have folks try out the "action listener callback middleware" we've got as an upcoming RTK API
  - It lets you add listeners ahead of time (statically), but also dynamically add listeners at runtime. Listeners can call `dispatch` and `getState` , unsubscribe, etc.

```JS
let mw = createActionListenerMiddleware()

mw.addListener(todoAdded, (action, listenerApi) => {
      console.log(`Text was: ${action.payload}, new num todos: ${listenerApi.getState().todos.length})
})
```

- ## JWT shouldn't be the default way of storing session data - because it doesn't allow logging out a user. 
- https://twitter.com/francoisz/status/1394258658641514514
  - Good old session cookies do the job fine, but yes, you'll have to keep track of sessions in a shared server-side storage. 
- You can store server side JWT and have logout
- But if you are going to have a shared server-side storage it's trivial to invalidate a JWT token on logout. And then your non-HTTP services don't need to understand cookies.
