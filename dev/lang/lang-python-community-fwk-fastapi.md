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
