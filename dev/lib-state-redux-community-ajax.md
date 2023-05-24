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
# discuss
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
