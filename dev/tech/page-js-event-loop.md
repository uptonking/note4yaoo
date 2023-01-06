---
title: page-js-event-loop
tags: [js, lang]
created: 2020-09-04T06:46:52.946Z
modified: 2020-09-04T06:47:12.681Z
---

# page-js-event-loop

# guide

- ref
  - [mdn: Concurrency model and the event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

# Concurrency model and the event loop

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
