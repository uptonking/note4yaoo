---
title: lib-state-redux-community-ajax
tags: [ajax, community, redux, rtk-query]
created: 2023-05-24T12:54:05.535Z
modified: 2023-05-24T12:54:32.960Z
---

# lib-state-redux-community-ajax

# guide

- dev-to

- getTable 为什么在 me-auth 之前请求
  - 原因未知
  - 一种解决方法是使用loadable-components拆分组件，异步加载
# discuss-websocket
- ## 

- ## 

- ## [Where should websockets and other persistent connections live? ](https://github.com/reduxjs/redux/blob/master/docs/faq/CodeStructure.md)
- We generally recommend that [most websocket usage in a Redux app should live inside a custom middleware]
- Middleware are the right place for persistent connections like websockets in a Redux app, for several reasons:
  - Middleware exist for the lifetime of the application
  - Like with the store itself, you probably only need a single instance of a given connection that the whole app can use
  - Middleware can see all dispatched actions and dispatch actions themselves. This means a middleware can take dispatched actions and turn those into messages sent over the websocket, and dispatch new actions when a message is received over the websocket.
- A websocket connection instance isn't serializable, so it doesn't belong in the store state itself
  - It's technically possible to insert non-serializable items into the store, but doing so can break the ability to persist and rehydrate the contents of a store, as well as interfere with time-travel debugging.
  - If you are okay with things like persistence and time-travel debugging potentially not working as intended, then you are totally welcome to put non-serializable items into your Redux store. Ultimately, it's your application, and how you implement it is up to you

# discuss-ajax
- ## 

- ## 

- ## 

- ## [RTKQ - Select data without hooks - Stack Overflow](https://stackoverflow.com/questions/72869959/rtkq-select-data-without-hooks)

```JS
export const selectUser = (state) => userApi.endpoints.getUser.select()(state);
```

- ## [how to Automated Re-fetching data in RTK query - Stack Overflow](https://stackoverflow.com/questions/72447522/how-to-automated-re-fetching-data-in-rtk-query)
- useGetuserdetailsQuery({}, { refetchOnMountOrArgChange: true })

- keepUnusedDataFor: 0

- invalidatesTags :['Userdetail']

- ## [Invalidate tags for another createApi](https://github.com/reduxjs/redux-toolkit/issues/1862)
- If I'm understanding you correctly... you can just use your own version of `api.util.invalidateTags` to do this. 
  - It's just a normal action, and the use case would look like this:

```JS
dispatch({
  type: `${reducerPath}/invalidateTags`,
  payload: ['SomeTag', 'AnotherTag'],
});

dispatch(api.utils.invalidateTags(...))
```

# discuss
- ## 

- ## 

- ## 

- ## [Moving business logic into a Web Worker · Issue #1841 · reduxjs/redux](https://github.com/reduxjs/redux/issues/1841)
- The state doesn't have to leave the Worker. The UI layer would only contain dumb components, sending event actions to the Worker. The Worker would send back to the UI only the change for the component/widget to update its view.
- I think this might be best left to an external library. One that can broker the communication of actions and state changes between the primary JS environment and the worker.

- ## [Style Guide: Ducks or Rails Style? · Issue #3639 · reduxjs/redux](https://github.com/reduxjs/redux/issues/3639)
- I actually did something very much like this in my "Practical Redux" tutorial series, which is directly based off the first real React+Redux project I built at work.
  - In that series, I had an entities feature that actually stored all the normalized items, with very generic action types like UPDATE_ENTITY. Meanwhile, I had specific "features" for the entities that had additional app-specific logic.
  - That particular work app really did have a lot of relations between the entities, so there was a strong benefit to keeping them in a single entities slice together (and using the Redux-ORM` lib.
