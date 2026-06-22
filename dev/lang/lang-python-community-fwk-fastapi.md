---
title: lang-python-community-fwk-fastapi
tags: [community, fastapi, python]
created: 2026-03-05T19:32:07.221Z
modified: 2026-03-05T19:32:19.303Z
---

# lang-python-community-fwk-fastapi

# guide

- pros
  - ?

- cons
  - ?

- features
  - ?

- tips
  - ?

- resources
  - ?
# discuss-stars
- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## 

- ## FastAPI can now serve your frontend app: With support for client-side routing _202606
- https://x.com/FastAPI/status/2068141463506935843
  - Great for React with TanStack Router, Astro static builds, Vite-based apps, etc. 
  - version 0.138.0
  - [Frontend - FastAPI ](https://fastapi.tiangolo.com/tutorial/frontend/)
- Main advantage of this approach than the normal build?
  - You still build as normally, this is only for serving the already built frontend app, respecting client-site routing while also respecting your API path operations.
- how it's diff from normal static files serving?
  - It supports client-side routing, serving the index.html as a fallback.

- I'm guessing next js is not supported since it was not mentioned?
  - Only with a static build output. But not in SSR mode as that requires executing Node.js in the backend.

- How do we do it before?
  - Maybe with StaticFiles, losing client-side routing, or with some good amount of custom logic to get close to something like this, maybe with an additional external static file server like Nginx, handling separation of API and frontend by path in a termination proxy, or by domain.
- StaticFiles didn't support client-side routing by default, as it's common in React and other frameworks.

- 
- 
- 
- 
- 

# discuss-internals
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🆚 [Transitioning from Node.js to FastAPI: Does the non-blocking mental model still apply? : r/FastAPI _202606](https://www.reddit.com/r/FastAPI/comments/1ubkph8/transitioning_from_nodejs_to_fastapi_does_the/)
  - I’m an experienced Node.js developer who recently picked up Python and is now diving into FastAPI.
  - In Node.js (and Express), my mental model revolves around a single-threaded, non-blocking, event-driven architecture.

- A lot of your experience regarding writing async code will carry over, but Python and JavaScript have very different concurrency models. There are potential footguns here.
  - In JS, you perform an async operation and get a Promise that will be resolved eventually. The async operation runs regardless of whether you await the Promise. The event loop is part of the JS runtime. There are generally no blocking operations in JS (you have to go out of your way to use blocking Node-specific APIs). Cancellation is managed via AbortController/AbortSignal objects.
  - In Python, blocking operations are the default. The Asyncio event loop is a library that can manage explicitly-async tasks on the current thread. Calling an async function will not actually execute the coroutine unless you await it (or explicitly spawn a separate task). Tasks may be garbage-collected without completing unless you hold a reference – there are no real fire-and-forget background tasks, you should always use the TaskGroup feature. Tasks (but not individual coroutines) may be cancelled, this raises a CancelledError the next time a Task awaits something. You can delegate blocking operations to a background thread (e.g. using await asyncio.to_thread(blocking_function, *args, ** kwargs)), but you must remember to do that yourself. Background thread work cannot be cancelled.
  - Importantly, Python makes it easy to accidentally block the event loop thread, and thus all in-progress async tasks. E.g. if you call time.sleep(5) in an async function, all pending tasks will be blocked as well for 5s. For FastAPI, this means no other request can make progress.
  - In FastAPI, you can declare path operations either via def handler() or async def handler(). The async def form will be executed as usual on the event loop thread, and you're responsible for not blocking the thread. The def form without async will automatically get scheduled on a background thread, but this will only work fine if your code is actually threadsafe.
  - 💡 So my main tip is to be on the lookout for potentially-blocking operations, and to send them to a background thread if possible. Prefer async-native libraries where possible, as they manage all of this for you (e.g. sending HTTP requests via `HTTPX` rather than using the blocking `Requests` library). The standard library (outside of the `asyncio` module) is generally not async-aware.
- On top of all this: Most FastAPI servers are using Uvicorn as the runtime, which ideally is running uvloop to handle all the async concurrency, which is written on top of libuv. The same libuv that node uses to handle non-blocking async. That is one major reason FastAPI scores so well on speed, it is using the highly optimized core of NodeJS.

- When using async functions in fastAPI, it uses the same event-loop concepts as nodejs even though the implementation is different.
  - Note: writing synchronous functions endpoints in fastAPI will run them in a thread pool executor which changes the concepts again (If I remember correctly, it's been a while I used nodejs, but there was a concept of child processes or something that could be used the same way)

- the major trap you can run into is modules or functions that don't support async. for example built in file operations (open). and of course these can hide inside innocent looking functions, like logging or loading configuration or templates. there are ways to handle this, like thread pools. but this is where the GIL comes in to ruin your day.

- the key difference is that javascript's async functions are eager (when called returns a promise that begins executing immediately), while python's async functions are lazy (when called returns a coroutine, only starts running when you await it or schedule it)
  - but when you are writing a request handler in fastapi and express, the framework hides this distinction; the incoming request handler invoked is already being awaited on by the framework, you mostly write code in the same way in both langs
# discuss-examples/showcase 🌰
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🧭 [I built an interactive FastAPI playground that runs entirely in your browser - just shipped a major update (38 basics + 10 advanced lessons) : r/FastAPI _202603](https://www.reddit.com/r/FastAPI/comments/1rjpjcz/i_built_an_interactive_fastapi_playground_that/)
  - [FastAPI Interactive Tutorials - Learn FastAPI with Hands-on Coding](https://www.fastapiinteractive.com/)
  - I've been working on an interactive learning platform for FastAPI where you write and run real Python code directly in your browser. 
  - No installs, no Docker, no backend - it uses Pyodide + a custom ASGI server to run FastAPI in WebAssembly.

# discuss
- ## 

- ## 

- ## 
