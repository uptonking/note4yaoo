---
title: lib-collab-logux-issues-not-yet
tags: [issues, logux, not-yet]
created: 2023-05-20T13:59:40.222Z
modified: 2023-05-20T14:00:05.623Z
---

# lib-collab-logux-issues-not-yet

# guide

- [Add Todo app examples](https://github.com/logux/logux/issues/5)
# discuss
- ## 

- ## 

- ## [Action processing queues feature request](https://github.com/logux/logux/issues/54)
  - [Add action queues pr](https://github.com/logux/server/pull/140)

- Right now Logux Server process all actions “in parallel” (on one thread, just in async “parallel”). It could cause a problem when actions are related:
  - Client A created post with Optimistic UI
  - Client A rendered new post
  - Client A subscribed for new post, but action 1 was not finished yet. The server returned an error because there is no post yet.
- Solution:
  - Add the queue option to Server#type and Server#channel. By default, it will be main.
  - For every client and queue, we are creating action queue. The server will start action, resend, process, or load only if the previous action in the same queue was finally processed.

- This feature will require big action processing refactoring with proper queues.

- ## [Glitches (Diamond problem)](https://github.com/nanostores/nanostores/issues/30)
- I do not have a solution for this problem yet
  - It is not a high priority task for now, since the main use case of Nano Stores (in contrast with RX) is to have big stores, not small atomic reactive steps.
- [fix: diamond problem](https://github.com/nanostores/nanostores/pull/58)
  - This pull request resolves the diamond dependency problem in 2 steps:
  - Listen to only writable stores
  - Bind callback with arguments (run function)

- ## [Context](https://github.com/nanostores/nanostores/issues/171)
- Problem 1: Cache API
- Problem 2: SSR
  - In SSR, Node.js will render HTML for multiple users in the same time (in the same Node.js environment). If you just export store from a file, all users will share the same store. It could be a very dangerous.
  - the best solutions is to export store creators and not stores themselves. And then create a single instance in application root.
- Problem 3: Mocks
- Problem 4: DevTools
