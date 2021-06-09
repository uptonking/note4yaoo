---
title: note-react-issues
tags: [issues, react]
created: '2021-06-09T00:46:09.221Z'
modified: '2021-06-09T00:46:34.611Z'
---

# note-react-issues

# pieces

- ## 

- ## 

- ## 

- ## 

- ## Order of Redux Provider and Router in React app
- https://stackoverflow.com/questions/49120583
- It does not matter.
  - They don’t depend on each other.
  - Take a look at their implementations, specifically at their render methods.


- [How to access Redux store using React Router?](https://stackoverflow.com/questions/56701584)
- It's a good practice to follow the connect pattern. 
  - You can create containers for components and do the connection there.
  - NOTE: This approach is usually used for more complex logic. In your case the LoginPage itself can be a container, so you don't need separate component.
