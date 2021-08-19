---
title: thread-devtools-bundler
tags: [compiler, devtools, thread, tool]
created: '2021-07-07T07:14:21.190Z'
modified: '2021-08-05T07:05:04.558Z'
---

# thread-devtools-bundler

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Just learned about SWC, a Babel alternative. Next.js is transitioning to use it instead of Babel. 
- https://twitter.com/housecor/status/1428101124343615495
  - Why? It's 20x faster than Babel. How? It's written in Rust (Babel is written in JS).
  - Rust seems to be the new language of choice for building web tools!
- Big moves happening in the js tooling space. Between rome, swc, and esbuild things are going to look much different in the next couple years. In a very good way I think.
- Question can you build a SPA with Rust?
  - Good question - swc from what I can see is a Rust transpiler from modern JavaScript (taking over from Babel) and/or TypeScript (taking over from tsc)
  - In the end it produces JS so it definitely can build a SPA, just much faster JS production times!
  - If you were doing wasm, Rust is quite popular there too natively, but that’s a different topic IMO
- Too bad it doesn't support Babel plugins or macros
- Incidentally, Vite and Snowpack use esbuild, written in Go, under the hood. 
- the trend to write transpilers, compilers and whatever kind of supporting tools in rust or go instead of JS is not exactly a new one (started already around 2019), but definitely a step in the right direction

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
