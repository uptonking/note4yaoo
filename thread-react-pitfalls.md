---
title: thread-react-pitfalls
tags: [pitfalls, react, thread]
created: 2024-04-13T12:45:49.657Z
modified: 2024-04-13T12:49:45.255Z
---

# thread-react-pitfalls

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 🤼🏻 Created an RFC for @getwebstudio to stop using React custom hooks in the application logic.
- https://twitter.com/oleg008/status/1779113663887991040
  - Hooks are not pure functions, they can be effectful.
  - Custom hooks are too powerful. Using custom hooks for application level logic inevitably leads to bad code.
  - Custom hooks are good for libraries
  - The right way to make readable code in react and simplify your abstractions is to use components. By extracting the shared logic into a component, changing open state doesn't cause MyTextField rerender.

- Anyone returning markup from a custom hook deserves all the pain they get.
