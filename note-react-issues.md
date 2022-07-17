---
title: note-react-issues
tags: [issues, react]
created: 2021-06-09T00:46:09.221Z
modified: 2021-06-09T00:46:34.611Z
---

# note-react-issues

# pieces

- ## 

- ## 

- ## Is dispatch asynchronous or synchronous? How do I know when it has finished affecting the state? with setState I have a callback
- https://github.com/facebook/react/issues/15344
  - 要避免此问题，reducer中不要执行side effects
- In Concurrent Rendering, React can and will start rendering components, only to pause and throw away the results. Because of that, React expects that the rendering process truly is "pure" with no side effects.
  - React calls your reducers at a couple points in the lifecycle and rendering process. It apparently does sometimes try to call it immediately when the update is queued to see if there's a chance of bailing out early. Assuming it keeps going, then it will normally get called during the rendering phase.
  - So, if you start putting side effects in reducers, you will almost definitely see unexpected behavior because those effects are running even if the component isn't getting updated at that point.

- ## React useReducer async data fetch
- https://stackoverflow.com/questions/53146795
- Fetch data before dispatch (simple)
- Use middleware for dispatch (generic)

- ## Order of Redux Provider and Router in React app
- https://stackoverflow.com/questions/49120583
- It does not matter.
  - They don’t depend on each other.
  - Take a look at their implementations, specifically at their render methods.

- [How to access Redux store using React Router?](https://stackoverflow.com/questions/56701584)
- It's a good practice to follow the connect pattern. 
  - You can create containers for components and do the connection there.
  - NOTE: This approach is usually used for more complex logic. In your case the LoginPage itself can be a container, so you don't need separate component.
