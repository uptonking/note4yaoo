---
title: lang-js-arch-async-callback-promise
tags: [architecture, async, js, lang, promise]
created: 2021-08-30T07:00:06.476Z
modified: 2021-08-30T07:01:09.493Z
---

# lang-js-arch-async-callback-promise

# guide

- tips
  - 部分浏览器支持scheduler和TaskController可用来取消task，但firefox和safari不支持

- [Learn Asynchronous Patterns in JavaScript with Kyle Simpson](https://frontendmasters.com/courses/rethinking-async-js/)

- [JavaScript Promises vs. RxJS Observables](https://auth0.com/blog/javascript-promises-vs-rxjs-observables/)
  - Promises are very eager(热切的，渴望的). If we had a callback function provided to a Promise, once the Promise is resolved, the `.then` gets executed.
  - Observables are very lazy. We create the Observable, and then it will wait to be subscribed to. We create the Observable, and then it will wait to be subscribed to.
# not-yet
- await是否没有让出cpu时间？ 
- 如何让一个function类型的参数支持await和非await调用，如何提高性能
# examples
- https://github.com/eldargab/load-script /js
  - load-script appends a `script` node to the `<head>` element in the dom.

- https://github.com/rumkin/pill /js
  - Pill adds dynamic content loading to static sites and makes content loading smooth for users.
  - Intercepts navigation attempts: links clicks and history navigation.
  - Loads requested url using fetch.
  - Grabs content from received HTML
  - Replaces current page content.

## dynamic-load

- https://github.com/systemjs/systemjs /js
  - Dynamic ES module loader

- https://github.com/microsoft/redux-dynamic-modules /202003/ts/inactive
  - aims to make Redux Reducers and middleware easy to modular-ize and add/remove dynamically.
  - In large Javascript applications, it is often desired to perform some kind of code-splitting, so that the initial script size is small. 
  - However, in Redux, you are required to define your reducers and middleware up-front; 
  - there is no good way to dynamically add/remove these constructs at runtime.
  - designed to make dynamically loading these constructs easier

## react-remote

- https://github.com/hupe1980/react-script-hook /ts
  - React hook to dynamically load an external script and know when its loaded

- https://github.com/Paciolan/remote-component /ts
  - Dynamically load a React Component from a URL

## async-utils

- https://github.com/abbr/deasync
  - DeAsync turns async function into sync, implemented with a blocking mechanism by calling Node.js event loop at JavaScript layer. 
  - The core of deasync is written in C++.

- https://github.com/dmaevsky/conclure /MIT/202211/js/NoDeps/inactive
  - Brings cancellation and testability to your async flows.
  - It is a tiny (core is < 200 lines of code), zero dependencies generator runner. 
  - Using generators instead of promises allows for a LOT more flexibility, including cancellation, sync resolution, and better testing. The API is strictly the same as `async/await`.
  - 🤼 You should avoid Promises for two major reasons:
    - Promises are greedy: once created, cannot be cancelled
    - `await promise` always inserts a tick into your async flow, even if the promise is already resolved or can be resolved synchronously.
  - You can see a Promise as a particular type of an iterator for which the JS VM provides a built-in runner, a quite poorly designed one nonetheless.
  - Conclure JS is a custom generator runner that
    - allows you to cancel your async flows
    - ensures that sync flows always resolve synchronously
    - delivers better testability through the use of effects as popularized by redux-saga.
# discuss-async-loading
- ## 

- ## 

- ## what are good usecases for _dynamic_ imports in js
- https://twitter.com/threepointone/status/1491467308065243148
  - i.e. `const something = await import(xyz);` where xyz is _not_ statically known / can _not_ be known ahead of runtime? 
  - looking for good usecases that don't have great workarounds.

- One of my pain points with authoring a lib with ES modules is that I _can't_ conditionally import something that's needed for sync startup in DEV mode.
  - We've got some stupid search/replace build shenanigans in redux-RTK related to that.
- Cant it be done with dynamic import?
  - No, and that was exactly the point. In our case, we have Redux middleware that only run in dev. But all the store setup is done synchronously during app setup / module loading. You can't dynamically import a middleware and add it to the store - it has to exist _now_.
- With export conditions u could do this but it probably would involve having to create an identity/noop/passthrough middleware for production
  - Those are still fairly new and some tools might not always support this in the same way

- a plugin system where the list of plugins is stored as user data in a db?
  - yeah, plugin/config systems looks like a very good usecase here

- Plugins...oh 'good' use cases..sorry that's on me I got nothing.
  - only thing worse is order dependent globally mutating middleware

- Loading i18n translations on demand?
  - the workaround here would be a map of keys to imports, like -  { "en-US" : () => import('./translations/en-us'), ... }

- One example that comes to mind is code that doesn't need to run until a user has scrolled to a certain point on a page (e.g., with IntersectionObserver). No need to statically bundle the dependencies if a user hasn't scrolled to that point yet (or a certain distance from it)
  - Actually, this is exactly what I’m doing. Page contains several React components, and each is imported only when needed/viewed. This: import(`components/${data.componentPath}/index.jsx`) .

1. Test runners that load your test files dynamically. 
2. Plugins that are loaded by (dev) tools (eslint, prettier, StrykerJS) 
3. A playground that lets you create and run multiple JS files

- Importing a module for a new feature behind a feature flag

- Remix uses this for importing the js for routes dynamically on client side transition 

- ## Performance tip: use dynamic imports to ensure JS is only downloaded when needed
- https://twitter.com/Steve8708/status/1502084919488495621
  - When used responsibly, they can greatly reduce your bundle sizes and boost page load times

- The code for dynamic `import` can be placed in the `head` of the file instead of inside the `onClick` function, two benefits: 
  - 1. maintain page performance (dynamic import will start loading after the static import), 
  - 2. no need to wait to use the function inside the onClick function
# discuss-queue/concurrency
- ## 

- ## 

- ## Every Node.js developer has lost a background job to a server restart.
- https://x.com/matteocollina/status/2028879094381686834
  - We just open-sourced @platformatic/job-queue, a new queue library built for reliability from day one.
  - Deduplication, retries, request/response, graceful shutdown. All out of the box.
- Most queue setups make you stitch together patterns yourself:
  - Deduplicate jobs? DIY.
  - Wait for a result? Build custom plumbing.
  - Recover stalled jobs? Hope for the best.
- We built these into the core API so you don't have to.
- Three storage backends for different stages:
  - MemoryStorage - dev & testing
  - FileStorage - simple single-node deploys
  - RedisStorage - production, horizontal scaling, leader election
- Start local, go distributed. No code changes.
- We've been testing this @platformatic , and it's been solid.

- Are there plans for concurrency management and group concurrency? (so that big tenants don't clog the pipe) pg-boss has very powerful and flexible concurrency configuration that can be used as a reference

- Did you build this because you ran into problems with BullMQ? Curious what you are solving for, given there is a _very_ mature tool in this space
  - I needed something that could work over the file system, and generically had a multi-provided interface.
  - It introduces a caching/deduplication layer too. So if the same job gets queued twice, it will only be processed once.
- Yeah, but easily enough done with explicit job ID creation/dedup with BullMQ. But nice you built it first-class!

- what does it have that bullmq doesnt or it does better
  - it’s multi-provider and it introduces a caching/deduplication layer too. So if the same job gets queued twice, it will only be processed once.

- ## [GCP: When to use PubSub vs Task Queues _201702](https://groups.google.com/g/google-appengine/c/IcIjLfgnNXs/m/-m_ik7h6DgAJ)
- Much of the answer is historical. Task Queues evolved as part of the App Engine developer libraries (back in 2009) and was (internally) slated for deprecation and replacement with release of Pub/Sub. As you observed: Pub/Sub does seem like a strong generalization of Task Queues. When Pub/Sub launched, however, we found that it did not meet the needs of a significant number of customers. A number of features that we thought weren’t particularly import (de-duplication, scheduled delivery, rate management, concurrency management, tagged tasks, configurable retries, etc) turned out to be critical and not supported in Pub/Sub.
  - In response to that feedback, we took a step back and tried to define the core differences. The conclusion we arrived at is that Pub/Sub is a networking and big data product. It is agnostic to both the content and the target and focuses on delivering very high throughput capabilities to arbitrary handlers. Task Queues is a managed execution product. It is intended for running and managing large numbers of explicit commands. We’re working to repackage Task Queues as Cloud Tasks and open it up for broader integration with the rest of GCP. For example, we want to make it possible to enqueue Datastore operations or Cloud Functions for asynchronous execution. The idea is to make it as easy as possible to spin up large distributed systems without needing to write handlers and managers. 

- Personal opinion:
  - Task queues are probably better to use from App Engine Standard. They've existing for a long time, and I suspect the RPC API that is used to call App Engine services is pretty efficient. Using Pub/Sub is likely to be slightly worse in terms of overhead per API call, since it will have to go through the HTTP API via URL Fetch.
  - Pub/Sub is probably better to be used from anywhere else. The API works from anywhere. A single Pub/Sub topic has nearly no limits, while task queues top out at around 500 messages / second. You can also "replicate" a topic to multiple subscribers, which is useful for some applications.

- ## [javascript - what is the difference events and tasks? - Stack Overflow](https://stackoverflow.com/questions/73185642/what-is-the-difference-events-and-tasks)
- Events are signals that tell the event loop that a task is now ready to run. They are not part of the event loop, they come from outside. Examples are DOM events (such as clicks, keyboard events etc), network events (readystatechange, progress), timer events (from setTimeout). 
  - Events are not tasks themselves. They may or may not be fired by another thread - often enough, the event loop polls for them.

- ## 🆚️ [Event Loops vs Queues? _201910](https://www.reddit.com/r/esp32/comments/dde864/event_loops_vs_queues/)
  - I'm doing a refactoring of some code and am looking to componentize things. As far as communication between components, is there any "best practice" as to when to use event loops vs queues? 
  - Its seems like you can get the same functionality, ie running a function on an event vs running a function when an item in a queue is received. 
  - I want to do things in an extendable, well maintainable, and "correct" way so does anyone have any advice or resources I can look into to better resolve this?

- ‘Queues’ provide a task-to-task, task-to-interrupt, and interrupt-to-task communicationmechanism.
  - Event groups are another feature of FreeRTOS that allow events to be communicated totasks. Unlike queues and semaphores: Event groups allow a task to wait in the Blocked state for a combination of one of moreevents to occur. Event groups unblock all the tasks that were waiting for the same event, or combinationof events, when the event occurs
- In Summary. 
  - Events are good if you want to wait to do something when the chip has reached a set of states. e.g. I have read the temperature and humidity and I'm connected = OK send the payload. All (or some) conditions must be met for the event to trigger
  - Queues are better for copying information from one task to another. e.g I have 2 tasks. One that handles reading the temperature and another that displays the information. A queue can be used to "notify" (copy) the information from the task that read the data to the other that displays it.
  - As far as Main is concerned, Its just another FreeRtos task. I like to organize my code so that all my tasks, semaphores, events, queues etc, are initialized in main and the tasks act like individual applications thereafter. but there is no hard and fast rule about that as long as you keep your eye on the available stack space

- My answer will be specific to ESP-IDF.
  - The best practice is this: use eventGroup to signalling, use Queue to transfer data between tasks.
  - ESP-IDF framework is oriented to asynchronous programming model i.e. Non-blocking. So the main function should only be used for init'ing and setup handler. It's okay to have small code in main function, but if you're working with a larger systems then you need to consider creating some FreeRTOS tasks from main func. This way you'll keep your project modular.

- ## 🆚️ [Message Queue vs Task Queue difference - Stack Overflow](https://stackoverflow.com/questions/10075817/message-queue-vs-task-queue-difference)
- below is my understanding:
  - Message queue is the message broker part - a queue data structure implementation, where you can: send/receive
  - Task queue, on the other hand, is to process tasks: At a desired pace, In an async way
  - As you can see, message queue and task queue focus on different aspects, they can overlap, but not necessarily.
  - An example for task queue but not message queue - if your tasks don't care about ordering - each task does not depend on one another - then you don't need a "queue", FIFO data structure. You can, but you don't have to. You just need a place to store the buffered tasks like a pool, a simple SQL/NoSQL database or even S3 might suffice.
  - An opposite example is push notification. You use message queue but not necessarily task queue. Server generates events/notifications and wants to deliver them to the client. The server will push notifications in the queue. The client consumes/pulls down notifications from the queue when they are ready to do so. Products like GCP PubSub, AWS SNS can be used for this.
- Tools like Celery are task queue + message queue baked into one. There aren't many tools like Celery as I know that do both, guess that's why it's so popular (alternatives are Bull or Bee in NodeJS, or if you know more please let me know!).

- ### 🆚️ [Difference between a task queue and worker threads? : r/node _202203](https://www.reddit.com/r/node/comments/tdrjq2/difference_between_a_task_queue_and_worker_threads/)
- A task queue lets you do things like persist, schedule, coordinate and retry jobs in a robust way.
  - A worker thread just spins up a new thread to do some work on. It doesn't help you with the other stuff I mentioned.
  - If you are looking for a lightweight queue and are using Postgres, you might want to check out pg-boss and @graphile/worker, as an alternative to the Redis-based queues like Bull.

- A worker thread is a primitive which gives you the ability to run code in parallel. 
  - A task queue is a pattern for distributing work across potentially many computers.
  - You could implement a task queue pattern on top of worker threads, but as others have pointed out, if your process dies due to an exception, the OOM killer, or even a deployment script, all the threads will be killed along with it.
  - Most of the time when you implement a task queue pattern, you'll want to distribute the work across multiple servers, and store the actual tasks externally (e.g. in a database or Redis).
  - This is why e.g. "worker threads don't automatically retry" like some task queues. They're low level and you can use them to build up many different high level architectures.
# discuss-stars
- ## 

- ## I can't tell how many times I have found bugs like this... Is there any way to prevent this somehow?
- https://x.com/zx_loro/status/1917517267476308381
  - return中的函数执行忘了写await
- You need typescript-eslint/no-unnecessary-condition

- ## Let's mess around with sync, async
- https://x.com/antfu7/status/1896474458086596811
  - [Async, Sync, in Between](https://antfu.me/posts/async-sync-in-between)
  - in JavaScript: An async function can call both sync and other async functions; A sync function, however, cannot directly call an async function without changing its own color to async.
  - We often discuss the async inflection problem, where a common solution is to make everything async since async functions can call both sync and async functions
  - While an async function requires all the callers to be async, a sync function also requires all the dependencies to be sync.
  - For example, the widely used library find-up provides two main APIs, findUp and findUpSync, to avoid dependents being trapped by the coloring problem
  - Another case demonstrating the coloring problem is a plugin system with async hooks.
- Trying to make the situation a bit better, SXZZ and I took inspiration from gensync by LOGANFSMYTH and made a package called quansync.
  - Generator is where the magic happens. It allows you to create a quansync function by using other quansync functions.
  - By leveraging generator fn, we can pause execution at each yield point. In an asynchronous context, we can wait for the async operation to complete before resuming execution. In a synchronous context, the next chunk runs immediately. This approach offloads the coloring problem to the caller, allowing them to decide whether the function should run synchronously or asynchronously.
  - Promise in JavaScript naturally a microtask that delays a tick. yield also introduce certain overhead (around ~120ns on M1 Max). In performance-sensitive scenarios, you might also want to avoid using either asyncor quansync.
  - Quansync functions still face the coloring problem, as wrapping a function to support both sync and async requires it to be a quansync function (or generator). However, the key advantage is that a quansync function can be "collapsed" to either sync or async as needed. 

- ## 🆚️ Let’s say `f()` returns a promise:
- https://twitter.com/shuding_/status/1766842504635134271
  - async function a() { return f() }
  - async function b() { return await f() }
  - function c() { return f() }
- A returns a promise like c, since no await is used with async. 
  - B unwraps the promise in f, and rewraps it since async and await are used. 
  - F directly returns the promise from f. Behavior is the same.

- it’s the matter of where you handle the result of Promise, and where the error or success should be handled imo
- The examples are identical unless you expect c() === c() and don't add more code in each function. Try/catch in a() and errors before the return in c() make it behave differently.
- Only b) will return a complete stack trace if the promise code errors

- ## 🆚️ [Events vs Streams vs Observables vs Async Iterators - Stack Overflow](https://stackoverflow.com/questions/39439653/events-vs-streams-vs-observables-vs-async-iterators)
- There are roughly two categories of APIs here: pull and push.
  - Push APIs are a good fit for when something is generating data, and the data being generated does not care about whether anyone wants it or not
  - Async pull APIs are a good fit for cases where data is pulled from a source. This source might be a file, or a network socket, or a directory listing, or anything else. The key is that work is done to pull or generate data from the source when asked.

- ## [Would it be a good idea to unify generators and async-await? : r/ProgrammingLanguages _202008](https://www.reddit.com/r/ProgrammingLanguages/comments/igy5jd/would_it_be_a_good_idea_to_unify_generators_and/)
  - Many languages, including C#, Python and JavaScript, support both generators via yield and concurrency via async-await.
  - C# (conceptually) uses source-code transformation to turn coroutine functions of both types into state machines. 
  - Python has the ability to suspend and resume individual stack frames.
  - Do you think it would be a good idea to offer a single coroutine feature, instead of separate generators and async-await?

- That’s what goroutines do in golang. Channels and channel-operations are used to model both concurrency and generators. The same is true for core.async in clojure.

- This is what Kotlin does. They offer a generic coroutine framework that lets you build “suspend” functionality
# discuss-setTimeout/setInterval
- ## 

- ## 

- ## [Is there memory leak issue if not calling clearTimout after calling setTimeout - Stack Overflow](https://stackoverflow.com/questions/4244309/is-there-memory-leak-issue-if-not-calling-cleartimout-after-calling-settimeout)
- No. clearTimeout only needs to be called if you want to stop a pending setTimeout from happening. After the setTimeout happens, the timer id is no longer valid but fortunately calling clearTimeout with an invalid timer id is harmless.

- [Will a setTimeout keep a function from being garbage collected? - Stack Overflow](https://stackoverflow.com/questions/31503110/will-a-settimeout-keep-a-function-from-being-garbage-collected)
  - In javascript scope of a function is created when the function is created. setTimeout takes a callback function which keeps a reference of scope of myFunction. So it wont be garbage collected till the callback function is called.

- ## in early versions of Bun we made setTimeout(cb, 0) append to the task queue without delay and it broke a lot of libraries that implicitly expected it to clamp to 1ms
- https://x.com/jarredsumner/status/1885104099307511953
  - Blink:  Intent to Ship: Remove clamping of setTimeout(...) to >= 1ms

- I thought setTimeout ran immediately unless the stack had X number of  setTimeouts, than clamped to 4ms
  - iirc none of the actual behavior is defined in spec, so it’s pretty flexible.

- ## Builtin timeout using AbortSignal
- https://x.com/hd_nvim/status/1882484934356664640

# discuss
- ## 

- ## 

- ## 

- ## 💡 [Is it an anti-pattern to use async/await inside of a new Promise() constructor? - Stack Overflow](https://stackoverflow.com/questions/43036229/is-it-an-anti-pattern-to-use-async-await-inside-of-a-new-promise-constructor)
- You're effectively using promises inside the promise constructor executor function, so this is the Promise constructor anti-pattern.
  - Your code is a good example of the main risk: not propagating all errors safely
  - In addition, the use of async/await can make the same traps even more surprising.
  - any immediate exception in a `Promise` constructor executor function conveniently rejects the newly constructed promise (but inside any `.then` you're on your own).
  - any immediate exception in an `async` function rejects the implicit promise returned by the async function itself.

- 
- 
- 
- 

- ## if you need a pretty simple Queue in JS/TS just use a `TransformStream` . 
- https://x.com/okikio_dev/status/1830083868596036095
  - With the web stream api supporting back pressure, `ReadableStream.tee()` for multiple reads over the Queued data and the fact that TransformStreams are transferable across Workers and the main thread

- ## 前端的发展还是很快的，对语言设计来说可以很快落地试验一些 feature, 
- https://twitter.com/codeworm96/status/1775764265695322438
  - Javascript以很快的速度走过了 callback -> promise -> async/await 的路（而 async rust 和 c++...）而且现在前端也足够工程化了，完全足以观察在大项目中的表现
- 别尬黑，我发现的前端大部分的问题，都是 JS 根上乱搞导致的.. 工程化的事情系统开发好早就明白了，前端得等到组件化以后，很多新技术也还在斗争，了解/兼容一堆村规想死..
- JS主要作为脚本语言，以文本形式分发，所以新版本至少不能在 parse 上 break 掉旧版本；于是就这么拖着屎山一路向前。 很难想象像 Python 3 那样搞语法不兼容会对 JS 产生什么后果。
- 我感觉async await跟手动内存管理相性不好
- 我觉得 async await 至少是符合 structured concurrency 的，但一些比较复杂的控制流表达不出来。 
  - 我觉得原文传达出来最主要的意思是 structured 的控制流（除了循环）基本是从上而下顺序的，而 goto (go) 是乱跳的；async await 是符合顺序的，而如果你试过用 callback 或者 Promise 实现循环，你就会发现代码的顺序很别扭。
- go 怎么类比goto 呢，go 有 waitgroup，感觉挺容易写成 structured concurrency 呀。我的疑问是，协程本身应该支持 structured concurrency，这是趋势，但是并不是 async/await 更容易写成 structured concurrency。像 go 和 java 这样不用勿扰代码的协程方式，同样很容易实现 structured concurrency
- 写说可以写的，JS 也有 await Promise.all() 。主要是多人协作的项目里意识的问题。你可以用 go 来实现 structured concurrency，但别人不一定会有这个意识；相比之下 async await 由于不支持像 go 这样跳，下限更低一点，不容易用出问题。goto 也可以实现所有的控制流。
  - 你说的没毛病。什么特性滥用都会导致预料外的事情。所以 java 在virtual thread基础上在实现 sc。 并鼓励使用最佳实践。go类似。 我想表达的是，核心是 sc，而不是 await/async 更容易 sc

- ## A common misunderstanding about `Promise.all` is that it cancels the remaining promises as soon as it rejects—this is NOT true! 
- https://twitter.com/hovhaDovah/status/1765763275545817427
  - It simply ensures that you don't have to *wait* for the remaining promises to resolve if a promise has already rejected. What do you think this code logs?
- In other words, Promise.all gives you fail-fast behavior, allowing you to handle the error case sooner than if you had waited for all of the promises to settle.
- very interesting, even if one promise fails it goes into the catch block, makes a ton of sense to do so.

- ## 🤔🆚 Have any JS lib maintainers switched back to using callbacks over promises and async/await?
- https://twitter.com/tantaman/status/1758828869530906748
  - The purpose being that by using callbacks you can preserve the task and event loops when the library is deployed with synchronous workloads and still be able to support async workloads.
  -  with promises and async functions, everything resolves asynchronously even if it is synchronous. That’s what I want to avoid since, with my lib, some ppl want it to be full synchronous and others full asynchronous. Callbacks allow that as you said. Promises don’t.

- If you create a promise that contains no async call, it will be synchronous, but listeners will be queued in the micro-tasks, which is rarely an issue but maybe it is for you ? You can also return a custom promise to mimic then(), but async stack trace become an issue :/
  - The micro task queueing for ‘then’ callers is an issue since it will cause interleaved execution of synchronous code.
  - As a concrete example— I have a library where users can provide a data source. That source could be synchronous or async.
  - If my library used promises to expose the synchronous sources then any call to get a result from those sources would resolve in a future micro task. 
  - The most obvious place this is a problem is react controlled inputs. The synchronous sources will cause cursor jumping when put behind a promise api. 
  - Other issues are code someone wants to run sequentially getting interleaved with other code since all ‘then’ calls are new tasks.

- pulumi is actually callback based and so the new version of sst is as well
- What did you take into account when deciding to make sst callback based?
  - we actually wanted to maximize parallelism whereas promises would require the end user to ensure they aren’t blocking unnecessarily
  - basically we never want them to await

- 🤔 I've ditched promises long time ago in favor of generators. Wrote a tiny generator runner http://github.com/dmaevsky/conclure that allows me to keep the async/await logic (spelled function*/yield in the iterator world), but sync tasks are still executed sync. And async tasks can be cancelled

- Too many people call await sequentially which kills perf, cause they don't know about parallel.

- I am curious if it possible to make own Promise implementation that will not be falling to microtasks

- Given I’m mostly writing code (both apps and libraries) using [Effect](https://effect.website/), most APIs are returning Effects - or sync if side-effect free. Effect uses callbacks to implement most operations where necessary.

- ## is there a way to wait for N promises on tests?
- https://twitter.com/sseraphini/status/1365297469911937025
  - I have a test that will receive N messages and process each of them using an async code
  - so I need to wait N process to be processed to do some assertion
- Promise.all() or Promise.allSettled() might be work.
- `await new Promise(setImmediate)` .
  - will this awaits a single promise or all the pending promises?
  - This awaits all promises that are to be resolved in the same event loop

- ## I think we should have an ESLint rule that stops you from `await` -ing in an inline `Promise.all` array
- https://twitter.com/karlhorky/status/1720194025695719503
- You can pass any value in the promise all array so nothing for TS to ‘catch’. Maybe a lint rule would be handy as you suggest

- ## [Why people still compare Observables as "better" than promise as a primitive?](https://www.reddit.com/r/angular/comments/w9ipf4/why_people_still_compare_observables_as_better/)
- Because observables are much more powerful.

- ## 🤔🔢 [Why the Microtask queued after chained promises are executed after the first promise resolution ignoring the chained ones? - Stack Overflow](https://stackoverflow.com/questions/75373806/why-the-microtask-queued-after-chained-promises-are-executed-after-the-first-pro)

```JS
function tasksAndMicroTasks() {
  const promise = Promise.resolve()

  console.log('#1st call')

  promise
    .then(() => console.log('#3rd call'))
    .then(() => console.log('#4th call'))
    .then(() => console.log('#5th call'))

  queueMicrotask(() => console.log(`I'm microtask from the custom Queue`))

  console.log('#2nd call')
}
tasksAndMicroTasks()

// #1st call
// #2nd call
// #3rd call
// I'm microtask from the custom Queue
// #4th call
// #5th call
```

- `promise.then(fn1).then(fn2);` is not the same as `promise.then(fn1); promise.then(fn2);`.
- For the purposes of your experiment,  `Promise.resolve().then(fn)` is doing the same thing as `queueMicrotask(fn)`. 
  - The Promise is already resolved, so the callback function is queued.
- When you chain .then() callbacks, you're adding callbacks to the returned Promises from the calls to .then(). Those Promise objects will not resolve until each .then() resolves in sequence.

- A promise returned by `.then()` is resolved with the result of the callback, so it fulfills only after the callback has been called. 
  - Only at this point, the promise handlers of the chained promise are scheduled on the microtask queue - after all the ones that had initially been scheduled on the already fulfilled promise or by `queueMicrotask`.

- ## [What are the advantages of async.js over native Promises](https://github.com/caolan/async/issues/1714)
- Promises add a caching layer for results and errors and state machine around your function calls which makes things more stateful and somewhat slower than necessary 
  - and they also allow passing the next point of execution around which breaks encapsulation. 
  - Async/await helps somewhat with the latter but you can get the best of both world with casync along with this library.
- I could do `Promise.all(ratings.map(processRating))` but this would overload my API. With `mapLimit` I can set a max of 25 calls at a time. Rather than 1000's. 

- ## [Node.js 异步api的本质和 libuv](https://zhuanlan.zhihu.com/p/402398815)
- Node.js 是一个 Javascript 的运行时，提供了系统能力的 api，主要是文件、网络相关的 IO api，而 IO api 的实现是在 libuv，提供了同步异步两种形式的 api。
- 本来就来探究下 libuv 的功能和提供的 api 的形式。
- cpu是顺序执行代码的，通过pc寄存器来存储着下一条指令的内存地址。代码的执行流程叫做控制流。
  - 但是对于一些IO操作来说，并不需要cpu做计算，而是在等待硬盘设备、网络设备的数据读取，
  - 这时候 cpu 是空闲的，所以一条控制流不行，会导致cpu利用率太低。
- 所以操作系统又提供了进程、线程的功能，进程是分配资源的单位，而执行代码主要是靠线程，
  - 一个线程就是一条控制流，它是cpu调度的基本单位，也就是说可以在多个控制流之间切换，当一个线程在做IO的时候就释放cpu，让其他线程去跑。
- 一个线程阻塞的等待IO的方式就是同步，会比较浪费 cpu，
  - 而多个线程切换，在做IO的时候让其他线程上 cpu 跑，执行完IO再申请cpu来继续后续处理，这种方式就是异步
- 异步最终是多线程来实现的，但是在 Node.js 里面又进一步通过 event loop 做了封装，
  - 比如执行文件读取、网络访问的时候并不需要开发者去创建线程，而是调用api，指定回调函数就可以了，这是对多线程的进一步封装。
- **异步的底层实现都是通过线程的切换，但是暴露给开发者的形式有两种**：
  - 第一种是开发者控制线程的创建和销毁，指定线程执行的内容，java是这种。
  - 第二种是提供事件循环机制，提供一系列异步api，这些异步api最终是由线程来执行的，但是开发者不需要手动管理线程。javascript是这种。​
- 在Node.js里面，实现 event loop 的就是 libuv，它是一个异步IO库，负责文件和网络的io，提供了事件形式的异步api。
  - libuv里有一个线程池负责维护一些线程用来执行异步api，这个线程池的大小是可以设置的，通过环境变量 UV_THREADPOOL_SIZE 可以设置。
- 就是说libuv是负责IO的 api 的异步实现的，基于更底层的操作系统 api。
  - 这些操作系统api有的是异步的，有的不是，对于不是异步api的那些，就要由libuv的线程池中的线程来执行，变成异步的形式。
- 这些 api 包括：
  - 所有的文件 fs api，除了 watch 的 api
  - 加密 crypto 的异步 api
  - 所有压缩的 zlib api
  - dns.loopup
  - 这些 api 共用一个线程池，那么肯定会相互影响，所以有的时候需要加大线程池的线程数量，默认是 4，当需要的时候可以设置这个环境变量来加大。
- 当面试问到Node.js性能调优的时候，可以答设置libuv的线程池大小，堆大小设置的这两个参数/环境变量。
- 看了文档之后，我们更确认了异步最底层的实现就是线程，只不过是通过libuv的线程池做了封装。

- 再来看下 Node.js 都怎么提供这两种 api 的
- 同步的 api 比较简单，就是调用函数，拿到返回值就行，很多 xxSync 的 api 都是同步的
- 而异步的 api 则分为了两种形式，callback 和 promise
  - 其中 promise 的版本只有两个模块有，fs 和 dns，是在 Node.js 10.x 引入的，方便使用 async、await 来组织代码

- 总结
- 程序在进行IO的时候， cpu是空闲的，为了更好的利用cpu，操作系统提供了进程、线程的功能，一个线程就是一条控制流。
  - 当在IO的时候，切换到别的线程，等IO结束之后再继续执行的方式就是异步，而相应的一个线程阻塞的等待的方式就是同步。
- 异步最终是由线程实现的，但是提供给开发者的有两种形式：
  - 一种是提供线程api，让开发者自己管理线程，
  - 另一种方式就是提供事件循环，对于异步api通过线程来实现。
  - 第二种方式对开发者更透明，不需要关心线程的创建和切换。
- Node.js 里面的 event loop 的实现是在 libuv，它提供了文件和网络的异步 IO 的 api，
  - 从文档中我们可以看到，libuv是基于操作系统的 api 实现的，而其中一些同步的api，则是由 libuv 的线程池来执行，达到异步的目的。
  - 但是线程池的大小默认是 4，有的时候需要加大，可以通过修改 UV_THREADPOOL_SIZE 的方式。
- Node.js 提供的 api 有3种形式，一种是同步的，一种是异步callback、一种是异步promise。
  - 其中异步 promises 的形式是推荐的写法，但是只有在 fs、dns 两个模块可用，并且要在 Node.js 10 以上才行。

- discussion

- 异步底层实现不一定是多线程吧，某些异步任务，如果 IO 任务直接交给硬件，然后等待系统事件通知
  - 是这样，比如 dma 就是，libuv 是通过多线程封装了一些同步系统 api，异步系统 api 的部分不一定是多线程
  - 限定在软件级别的异步就是靠线程了，软件的执行是靠cpu，也就是需要线程。硬件级别的异步是靠电路，就不用线程了。

- ## Are you using async/await safely in Node.js? @simonplend explains why Express is not a safe choice and why you should consider an alternative like Fastify instead.
- https://twitter.com/sebastienlorber/status/1374029709210701831
- [Are you using promises and async/await safely in Node.js?](https://simonplend.com/are-you-using-promises-and-async-await-safely-in-node-js/)

- ## I was chasing the race conditions today in the code that is using observers and async/await syntax. Oh, boy, a day full of fun.
- https://twitter.com/maciejadamczak/status/1374286061543718916
- I still need to fix the root problem

- ## Deleted a thread about async/await flows since I hadn’t realized that it made error-handling more complicated.
- https://twitter.com/JoshWComeau/status/1374056481524482054
- I still think it's a valuable tip. I use it all the time - it really helps to speed things up when you've got independent parallel requests.
- You can use try catch.
  - I think it doesn't work when you don't `await` the async function! And that's what Josh means.
- Now I'm interested in a thread about proper error-handling when working with async functions
  - imo async makes it _easier_ (you just use try/catch). I think the difficulty is when you're mixing async/await with raw promises.

- ## When you have a complex series of async functions to call, how do you manage them? 
- https://twitter.com/JoshWComeau/status/1374027384119263233
  - we'll look at 3 different ways, including an *awesome* way that isn't super well-known.
- First, though, let's look at the most straightforward way: serially, one at a time.
  - The beauty of `async/await` is that it lets us read the code in the order it executes. I love how easy it is to understand.
  - The trouble is that it can be quite slow, since none of these tasks can start until the previous one finishes.
- What about `Promise.all` ? Well, we can't dump all 5 into a single call, since there are dependencies.
- From a performance standpoint, this is quite a lot better, since we can let 3 operations run in parallel.
  - But we can make this even faster 
- This final way makes selective use of the `await` keyword. 
  - We can weave the promises together to create a tapestry without gaps. 
  - Each function starts as soon as possible! 
  - The key insight is that promises can be await-ed at any time, not just on creation!
- Which way is best? Well, it depends on the circumstances.
  - The third way is the fastest, but it's also (IMO) the hardest to follow. 
  - We're trading away some simplicity in order to gain some performance.

- ## I don't like much Promise.all
- https://twitter.com/sebastienlorber/status/1379731789707632640
  - Too sensitive to array destructuring typo
  - Code becomes verbose when input to transform is an object
  - Finally published this little utility: combine-promises
- Reminds me of `Promise.props` in Bluebird. 
  - I wonder why something like this wasn’t part of the Promise spec.
- Another big pain point with Promise.all and variations, is error handling IMO (ex: calling 3 APIs from diff providers). It would be awesome if you could solve this in the lib too. I'd love to help, got some ideas on how to go about doing it.

- ## Problem with `Promise.all()` : Once it encounters a rejection, it doesn’t wait until all Promises are settled (short-circuiting (*)). Consequence: Unexpected things can happen after error handling.
- https://twitter.com/rauschma/status/1405568325724291080
- Tentative idea: Promise.forkJoin(objOrArr). Once all Promises are settled:
  - All fulfilled: fulfill result with obj/arr of values
  - 1+ rejected: reject with AggregateError
  - This is what an implementation of forkJoin() could look like:
  - https://gist.github.com/rauschma/bdc56a046b18528959ad1db3eed05386
- What about `Promise.allSettled` ? I’ve taken to chaining the outcome to array filter and map (depending on intent, of course).
- There’s `Promise.allSettled` , combine it with `Promise.all`

- ## Async functions & microtasks
- https://whistlr.info/2021/async-and-tasks/
- When you invoke an `async` function, the function will run its synchronous prefix immediately, but whenever you `await` something, the rest of its code will be put into a microtask.

```JS
console.info('a');
const p = foo(); // call async and hold Promise in p
console.info('b');
p.then(() => {
  console.info('c');
});

async function foo() {
  console.info('1');
  await Promise.resolve(); // actually do something async
  console.info('2');
}
// a 1 b 2 c
```

- Any time we `.then()` a Promise, that callback is executed as a microtask—broadly, that code is queued to run "immediately", but after the current execution and other microtasks. (And, the same happens when we use `await` on them.) 

- ## With the rise of async-await, I've noticed more and more JS developers have less understanding of concurrency and how to work with async code flow
- https://twitter.com/dev__adi/status/1417554978130915328
- [How to escape from the async/await hell](https://devadi.netlify.app/blog/async-await-hell)
  - While working with Asynchronous JavaScript, people often write multiple statements one after the other and slap an await before a function call. 
  - **This causes performance issues, as many times one statement doesn’t depend on the previous one** — but you still have to wait for the previous one to complete.
  - One interesting property of promises is that you can get a promise in one line and wait for it to resolve in another. This is the key to escaping async/await hell.
- How to get out of async/await hell ?
  - Find statements which depend on the execution of other statements
  - Group-dependent statements in async functions
  - Execute these async functions concurrently: Two common patterns of doing this is returning promises early and the `Promise.all` method.

- ## setTimeout using an AbortController and Promise
- https://twitter.com/rikschennink/status/1691417576868380674

- ## Promise resolvers are one of my absolute favorite little programming tools
- https://twitter.com/aboodman/status/1619426079399350272

- I've been looking for a name for this pattern for years. IIRC I've used it mainly in tests

- I think some people call this "deferred"
  - https://github.com/ljharb/promise-deferred

```JS
// https://github.com/rocicorp/resolver

import { resolver } from '@rocicorp/resolver';

const { promise, resolve } = resolver();
resolve(42);
await promise; // 42

class LongRunning {
  async stop() {
    this._stopper = resolve();
    await this._stopper.promise;
  }

  async run() {
    while (!this._stopper) {
      // ...complex asynchronous process...
    }
    this._stopper.resolve();
  }
}
```

- ## 🤔🆚 I really wish there were Promises in JS that could be evaluated sync. It’s a complex problem. _202303
- https://twitter.com/trueadm/status/1630739165045194752
- For UI frameworks you want to allow the user to pass a promise, but ensure that if it is ready that you can render synchronously. But `T | Promise<T>` doesn’t compose the way promises do, so either you accept a perf/UX hit, create your own alternate async ecosystem, etc.
  - I use a WeakMap for this. Only pass promise. Lookup resolution value sync via weakmap where you want to do this. Still agree though: custom thenables are great and Promise.resolve using them is great, async/await not using them sucks
- This was discussed ad nauseum a decade ago. If you want sync promises try jQuery. Deferred.
- https://github.com/abbr/deasync
  - DeAsync turns async function into sync, implemented with a blocking mechanism by calling Node.js event loop at JavaScript layer. 
  - The core of deasync is written in C++.
- conclure js Using generators instead of promises allows for a LOT more flexibility, including cancellation, sync resolution, and better testing. The API is strictly the same as async/await

- I definitely want eager await that resolves sync if the promise resolves sync. That’s more in the style of callbacks, and allows you to write a single api for both sync and async interfaces.
  - I struggle with this issue in tuple-database. I want to write the same code that works for an async backend or a sync backend. I don’t want to create an intermediate query language…
- My problem is actually pretty specific:
  - For tuple-database, there's an async storage interface and a sync storage interface. 
  - The sync interface is important if you want to use it for application state management and stuff. Or maybe you just want to use local storage...
- Since the lowest level abstraction is either sync or async, it pollutes all the code above it which needs to be written to handle both cases.
  - I looked into coroutines, higher-kinded types, monkey-patching promise... 
  - My solution? Regex lol
- Replicache is designed to be used for application state and it is async. We are religious about 60fps. Promises that resolve immediately *are* slower than sync code but we’re taking microseconds. It works great for 60fps in our experience.
  - We have tons of customers in production using Replicache exactly this way (among them @vercel ) and it’s ~instant.
- Yeah, you can definitely get away with async state management most of the time...
  - I'm curious if that can get in the way of typing into an `<input>` if the input's value is updating async as you type...
- Yes you can. We do this while animating at 60fps.
  - We have many users who back input boxes by @replicache directly. It's a design goal of ours to enable this exactly. Try it out, I think it's an overlooked design pattern.
- 👉🏻 关于架构层sync或async api的设计 
  - The other nice thing about making the api to Replicache asynchronous is that it permits falling back to io as necessary. Many sync systems have this problem where these choose sync apis for perf but eventually data gets large and causes excessive gc.
  - If the core API is async it can be up to the sync system to dynamically manage cache size. Replicache does this, lazily caching data from IDB and paging it out after awhile.
- Getting into the weeds though: on iOS Safari, if you want to call focus() on an element to bring up the keyboard, it must be called synchronously in response to a user action event callback... Now, what if they press a button and you want to open a popup and focus the input?
  - https://twitter.com/ccorcos/status/1631159120043835392
  - In React, at least, you're going to want to update the state, synchronously re-render, and then call focus... This *could* work with a sync state update. Unfortunately, React's move towards async rendering throws a wrench in it. But the problem remains the same.
- I am pretty sure it only needs to be called in the same task (queueing a microtask is fine). So if your data is in memory it will still work.

```js
const foo = await Promise.resolve("foo");

// vs:

const foo = await new Promise((res, rej) => setTimeout(res, 0));
```

- The first runs in *same turn* of event loop as calling code, guaranteed. Second gets queued in event loop.
- Microtasks are crazy fast. All they are doing is delaying a function to run later in the turn of the event loop. No actual IO (to disk, network, whatever) can possibly get between the queuing of a microtask and its execution.
- `setImmediate` is not part of the spec or implemented by browsers, but was meant to queue a task. So shorthand for `setTimeout(fn, 0)`.
- A microtask enqueued from within another microtask would execute immediately I believe, but I bet React's whole rendering model probably has its own considerations for this.
  - I think they were also doing some weird stuff with unwrapping resolved promises.. somehow.. maybe an RFC.

- It’s important to understand that `async` does not mean “yield to event loop”. When the underlying promise resolves in same event loop task, the resolution will also run in same event loop task. This usually happens when the data needed is already in memory, because it’s cached.
  - Mutations don't need to go through useEffect or similar in the first place because they aren't an effect of render, but of some UI event. So the whole cycle should happen in one frame if your data is in memory, even if all the methods are `async`.

- Yeah, but my goal was to just have one system that can work either sync or async... Perhaps, that's not a great goal, but that's where I landed on these problems... If generators could have a typed yield (similar to  await), then my problem would be solved...
- It's worked really surprisingly well for us. I think UI developers have a phobia of `async` because it often means 'network activity' in classic web apps. But that isn't actually what `async` means to the browser. It just means >= microtask.

- This is good news. I’ve done cr-sqlite / vlcn as completely async (and had to part ways with collaborators over that decision) so this gives me some reassurance(肯定，保证).

- Gotta convince everyone to switch to generator-based effects.

- For UI frameworks you want to allow the user to pass a promise, but ensure that if it is ready that you can render synchronously. But `T | Promise<T>` doesn’t compose the way promises do, so either you accept a perf/UX hit, create your own alternate async ecosystem, etc. promises always incur a microtask
  - I use a `WeakMap` for this. Only pass promise. Lookup resolution value sync via weakmap where you want to do this. Still agree though: custom thenables are great and `Promise.resolve` using them is great, async/await not using them sucks

- Have you looked at @EffectTS_ from @MichaelArnaldi . I think he mentioned that Effect is faster than Promise as it is more sync.
  - Yeah effect only forces a micro task every 2048 suspensions of a fiber and a timer after 2048 microtasks have been executed in a row
  - ofc if you use the sync executor it runs fully sync without ever suspending
