---
title: page-js-event-loop
tags: [js, lang]
created: 2020-09-04T06:46:52.946Z
modified: 2020-09-04T06:47:12.681Z
---

# page-js-event-loop

# guide

- ref
# [w3c-spec: event loop processing model](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)
- Let oldestTask and taskStartTime be null.
- If the event loop has a task queue with at least one runnable task, then:
  - Set taskStartTime to the unsafe shared current time.
  - Set oldestTask to the first runnable task in taskQueue, and remove it from taskQueue.
  - Set the event loop's currently running task to oldestTask.
  - Perform oldestTask's steps.
  - Set the event loop's currently running task back to null.
- Perform a microtask checkpoint.
- Update the rendering: if this is a window event loop 
- this event loop's microtask queue is empty

- If this is a worker event loop, then:
  - Run the animation frame callbacks for that DedicatedWorkerGlobalScope, passing in now as the timestamp.
  - Update the rendering of that dedicated worker to reflect the current state.
# [Why dont long running javascript promises block?](https://stackoverflow.com/questions/63356992/why-dont-long-running-javascript-promises-block)
- It does block, for instance you may get blocked in a microtask checkpoint.

```JS
const block_loop = () => Promise.resolve().then(block_loop);

document.getElementById('btn').onclick = evt => {
  if (confirm("this will block this page")) {
    block_loop();
  }
};
```

- This example won't block the task from where it came from, but since microtasks queued from the microtask endpoint will get queued inside the same microtask queue that is being emptied, you'll actually end up in an endless loop and the event loop won't be able to process any future task.
- Also microtask are tasks, and their processing itself will also block the event loop like any other task

# [Event loop: microtasks and macrotasks](https://javascript.info/event-loop)
- Browser JavaScript execution flow, as well as in Node.js, is based on an event loop.
- The event loop concept is very simple. There’s an endless loop, where the JavaScript engine waits for tasks, executes them and then sleeps, waiting for more tasks.
- The general algorithm of the engine:
  - While there are tasks:
    - execute them, starting with the oldest task.
  - Sleep until a task appears, then go to 1.
- Examples of tasks:
  - When an external script `<script src="...">` loads, the task is to execute it.
  - When a user moves their mouse, the task is to dispatch `mousemove` event and execute handlers.
  - When the time is due for a scheduled `setTimeout`, the task is to run its callback.
- The tasks form a queue, so-called “macrotask queue” (v8 term)
  - Tasks from the queue are processed on “first come – first served” basis
- Rendering never happens while the engine executes a task. 
  - It doesn’t matter if the task takes a long time. 
  - Changes to the DOM are painted only after the task is complete.
- If a task takes too long, the browser can’t do other tasks, such as processing user events. 
  - So after a time, it raises an alert like “Page Unresponsive”, suggesting killing the task with the whole page. That happens when there are a lot of complex calculations or a programming error leading to an infinite loop.

## Use-case 1: splitting CPU-hungry tasks

- For example, syntax-highlighting (used to colorize code examples on this page) is quite CPU-heavy.
  - To highlight the code, it performs the analysis, creates many colored elements, adds them to the document – for a large amount of text that takes a lot of time.
- We can avoid problems by splitting the big task into pieces. Highlight first 100 lines, then schedule setTimeout (with zero-delay) for the next 100 lines, and so on.

```JS
let i = 0;
let start = Date.now();

// A single run of count does a part of the job (*), and then re-schedules itself (**) if needed:
function count() {

  // do a piece of the heavy job (*)
  do {
    i++;
  } while (i % 1e6 != 0);

  if (i == 1e9) {
    alert("Done in " + (Date.now() - start) + 'ms');
  } else {
    setTimeout(count); // schedule the new call (**)
  }

}

count();
```

```JS
let i = 0;
let start = Date.now();

// it takes significantly less time.
function count() {

  // move the scheduling to the beginning
  if (i < 1e9 - 1e6) {
    setTimeout(count); // schedule the new call
  }

  do {
    i++;
  } while (i % 1e6 != 0);

  if (i == 1e9) {
    alert("Done in " + (Date.now() - start) + 'ms');
  }

}

count();
```

- there’s the in-browser minimal delay of 4ms for many nested setTimeout calls. Even if we set 0, it’s 4ms (or a bit more). So the earlier we schedule it – the faster it runs.

## Use case 2: progress indication

- changes to DOM are painted only after the currently running task is completed, irrespective of how long it takes.
- If we split the heavy task into pieces using setTimeout, then changes are painted out in-between them.

## Use case 3: doing something after the event

- In an event handler we may decide to postpone some actions until the event bubbled up and was handled on all levels. We can do that by wrapping the code in zero delay setTimeout.
- 💡 Immediately after every macrotask, the engine executes all tasks from microtask queue, prior to running any other macrotasks or rendering or anything else.
  - order: macrotask > microtasks (~~> macrotask~~) > render > macrotask
  - Only one of macrotasks will get executed per event-loop iteration, selected at the first step
- All microtasks are completed before any other event handling or rendering or any other macrotask takes place.
  - That’s important, as it guarantees that the application environment is basically the same **(no mouse coordinate changes, no new network data, etc) between microtasks**.
- There’s no UI or network event handling between microtasks: they run immediately one after another.

- event loop algorithm
  1. Dequeue and run the oldest task from the macrotask queue (e.g. “script”).
  2. Execute all microtasks: While the microtask queue is not empty: Dequeue and run the oldest microtask.
  3. Render changes if any.
  4. If the macrotask queue is empty, wait till a macrotask appears.
  5. Go to step 1.

- For long heavy calculations that shouldn’t block the event loop, we can use Web Workers.
# [mdn: Concurrency model and the event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- JavaScript has a concurrency model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks. 
  - This model is quite different from models in other languages like C and Java.
- Function calls form a stack of frames.
  - When calling `bar` , a first frame is created containing `bar` 's arguments and local variables.
  - When `bar` calls `foo` , a second frame is created and pushed on top of the first one containing `foo` 's arguments and local variables. 
  - When `foo` returns, the top frame element is popped out of the stack (leaving only `bar` 's call frame). 
  - When `bar` returns, the stack is empty.
- Objects are allocated in a heap which is just a name to denote a large (mostly unstructured) region of memory.
- A JavaScript runtime uses a message queue, which is a list of messages to be processed. 
  - Each message has an associated function which gets called in order to handle the message.
- At some point during the event loop, the runtime starts handling the messages on the queue, starting with the oldest one. 
  - To do so, the message is removed from the queue and its corresponding function is called with the message as an input parameter. 
  - As always, calling a function creates a new stack frame for that function's use.
  - The processing of functions continues until the stack is once again empty. 
  - Then, the event loop will process the next message in the queue (if there is one).
- Each message is processed completely before any other message is processed.
  - This offers some nice properties when reasoning about your program, including the fact that whenever a function runs, it cannot be pre-empted(预先制止、防止、避免) and will run entirely before any other code runs (and can modify data the function manipulates). 
  - This differs from C, for instance, where if a function runs in a thread, it may be stopped at any point by the runtime system to run some other code in another thread.
  - A downside of this model is that if a message takes too long to complete, the web application is unable to process user interactions like click or scroll. 
    - The browser mitigates this with the "a script is taking too long to run" dialog. 
    - A good practice to follow is to make message processing short and if possible cut down one message into several messages.

- In web browsers, messages are added anytime an event occurs and there is an event listener attached to it. 
  - If there is no listener, the event is lost. 
  - So a click on an element with a click event handler will add a message—likewise with any other event.
- If there is no other message in the queue, and the stack is empty, the message is processed right after the delay. 
  - However, if there are messages, the `setTimeout` message will have to wait for other messages to be processed. 
  - For this reason, the second argument indicates a minimum time—not a guaranteed time.
  - setTimeout指定的延迟时间与实际的执行实际不一定精确相等
  - Calling setTimeout with a delay of 0 (zero) milliseconds doesn't execute the callback function after the given interval.
  - The execution depends on the number of waiting tasks in the queue.

- A web worker or a cross-origin `iframe` has its own stack, heap, and message queue. 
  - Two distinct runtimes can only communicate through sending messages via the `postMessage` method. 
  - This method adds a message to the other runtime if the latter listens to message events.

- A very interesting property of the event loop model is that JavaScript, unlike a lot of other languages, never blocks. 
  - Handling I/O is typically performed via events and callbacks, so when the application is waiting for an `IndexedDB` query to return or an `XHR` request to return, it can still process other things like user input.
