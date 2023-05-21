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

- ## [Action processing queues feature request](https://github.com/logux/logux/issues/54)
- Right now Logux Server process all actions “in parallel” (on one thread, just in async “parallel”). It could cause a problem when actions are related:
  - Client A created post with Optimistic UI
  - Client A rendered new post
  - Client A subscribed for new post, but action 1 was not finished yet. The server returned an error because there is no post yet.
- Solution:
  - Add the queue option to Server#type and Server#channel. By default, it will be main.
  - For every client and queue, we are creating action queue. The server will start action, resend, process, or load only if the previous action in the same queue was finally processed.

- This feature will require big action processing refactoring with proper queues.
