---
title: thread-devtools-bundler
tags: [compiler, devtools, thread, tool]
created: '2021-07-07T07:14:21.190Z'
modified: '2021-08-05T07:05:04.558Z'
---

# thread-devtools-bundler

# discuss

- ## JS engines don't expose an API for hot reloading. It works by loading new code on top of old code, and leaking the memory.
- https://twitter.com/jarredsumner/status/1423156334564843523
  - This is part of why JS dev servers get slower each reload. 
  - I haven't solved this yet for the JS runtime, but it's on my mind.

- ## http://transform.tools is so incredible.
- https://twitter.com/leeerob/status/1412456314278584328
  ◾️CSS → Tailwind
  ◾️SVG → JSX
  ◾️HTML → JSX
  ◾️JSON → GraphQL
  ◾️JSON → TypeScript
  ◾️Mardown → HTML
  - And more! Built with Next.js and @vercel
- https://github.com/ritz078/transform
  - https://transform.tools/
  - A polyglot web converter.
