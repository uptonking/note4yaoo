---
title: lib-collab-logux-issues-not-yet
tags: [issues, logux, not-yet]
created: 2023-05-20T13:59:40.222Z
modified: 2023-05-20T14:00:05.623Z
---

# lib-collab-logux-issues-not-yet

# guide

# discuss
- ## 

- ## 

- ## [Glitches (Diamond problem)](https://github.com/nanostores/nanostores/issues/30)
- I do not have a solution for this problem yet
  - It is not a high priority task for now, since the main use case of Nano Stores (in contrast with RX) is to have big stores, not small atomic reactive steps.
- [fix: diamond problem](https://github.com/nanostores/nanostores/pull/58)
  - This pull request resolves the diamond dependency problem in 2 steps:
  - Listen to only writable stores
  - Bind callback with arguments (run function)

- ## [Action processing queues feature request](https://github.com/logux/logux/issues/54)
- Right now Logux Server process all actions “in parallel” (on one thread, just in async “parallel”). It could cause a problem when actions are related:
  - Client A created post with Optimistic UI
  - Client A rendered new post
  - Client A subscribed for new post, but action 1 was not finished yet. The server returned an error because there is no post yet.
- Solution:
  - Add the queue option to Server#type and Server#channel. By default, it will be main.
  - For every client and queue, we are creating action queue. The server will start action, resend, process, or load only if the previous action in the same queue was finally processed.

- This feature will require big action processing refactoring with proper queues.
