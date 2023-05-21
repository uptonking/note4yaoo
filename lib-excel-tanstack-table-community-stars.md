---
title: lib-excel-tanstack-table-community-stars
created: 2023-05-08T23:37:59.784Z
modified: 2023-05-08T23:38:02.593Z
---

# lib-excel-tanstack-table-community-stars

# guide

# discuss
- ## 

- ## I love this article from @ag_grid talking about their learnings in data grid perf (which is hard) over the years.
- https://twitter.com/tannerlinsley/status/1507080909735940126
- #ReactTable lends itself well to some of these points (like implementing virtualization), but luckily by using React as the rendering engine, we did not have to write our own dom-manipulation work-queue.

- Since then we(ag-grid) now use React for Rendering when using AG Grid in React, so the rendering points don't apply now when using AG Grid in React.

- ## After a lot of research and even implementation, I found requestIdleCallback scheduling is not the right performance tradeoff for the CPU/Memory load of #ReactTable. 
- https://twitter.com/tannerlinsley/status/1524128427229335552
  - Web workers could be more promising, but for now, async table-ing is on hold. #tabbit-hole
- The problem is that when you break up a memory-heavy block of synchronous work into chunks, that shared memory has to be stored across tasks. I'm not super familiar with the low-level memory strategies/thresholds for JS engines, but I'm assuming this chunking has negative effects
  - Totally, super agree with the problem of serialization as well. Once we can pass large amounts of structured data around its over for other platforms. Here's the API I was thinking of. Not sure if it fits this use case but could be fun to noodle on

- Y'know, this actually mirrors what the React team found with using `requestIdleCallback` for scheduling

- I found this web worker demo interesting. No performance time improvement, but leaves the main thread unblocked, just like you are looking for.
  - https://afshinm.github.io/50k/
  - Exactly. We don't necessarily need to make things faster. We're doing that already. We just need a way to unblock the UI for large tasks in a framework agnostic way.

- I would suggest looking at how @Microsoft did for excel cloud, it s unbelievable what they did there, full porting of excel.

- ## So far, I've been unpleasantly surprised at how much longer the *total* time of a long-running task is when you break it out into multiple scheduled tasks (via `requestIdleCallback` ) vs just running the task synchronously.
- https://twitter.com/tannerlinsley/status/1524100159176511488
  - Am I wielding `useIdleCallback` wrong?
- I used to work on a 3D modeling program where we did some long running tasks. Breaking it up did indeed make it way slower. Ended up doing it in a webworker and using transferable objects.
  - This could very well be a solution. The tasks I'm performing are not necessarily as CPU intensive as they are memory intensive. Instead of a single op never leaving something like lower level hardware caches, they probably get moved out to RAM between the tasks.
  - Maybe idle callback fits a CPU intensive task set better than a very CPU + large memory intensive task?  My experience has had results of like 5-7x time when dealing with constructing/manipulating large data structures (~1million)
- that's expected with `requestIdleCallback` . Overall time will be bigger, the advantage is that your browser will not freeze while doing the calculation as it can take some breaks to do something else every now and then. You can try to play with the **timeout** or switch to **workers**
- Do you provide the timeout option? It's highly recommended, as without it can take several seconds before the callback gets fired.

- ## Finally got #ReactTable working well with React's strict effects.
- https://twitter.com/tannerlinsley/status/1523719550381944832
  - Turns out having your own scheduler can make that pretty easy... did I mention that the core has its own scheduler?
  - TLDR: I have built my own scheduling and memoization system into the ReactTable core
- Then you are using refs and controlled rerenders, I know, well, I guess
  - Indeed
- I wouldn't say "easy", but the strict effect have a purpose: idempotency. Strict effects act on effects by running them multiple times, the design of the library should follow then (just execute the cleanup, and next time rexecute).
  - Yep
- Niiice, @ScriptedAlchemy and I have been writing some of our own as well. Using the event loop to schedule main thread work is awesome. Assuming you are using the event loop, ha!
