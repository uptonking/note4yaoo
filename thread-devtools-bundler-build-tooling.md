---
title: thread-devtools-bundler-build-tooling
tags: [compiler, devtools, thread, tool]
created: 2021-07-07T07:14:21.190Z
modified: 2021-09-22T05:47:54.470Z
---

# thread-devtools-bundler-build-tooling

# discuss

- ## 

- ## 

- ## https://github.com/wclr/yalc
- When developing and authoring multiple packages (private or public), you often find yourself in need of using the latest/WIP versions in other projects that you are working on in your local environment without publishing those packages to the remote registry. 
  - NPM and Yarn address this issue with a similar approach of symlinked packages (npm/yarn link). Though this may work in many cases, it often brings nasty constraints and problems with dependency resolution, symlink interoperability between file systems, etc.
- yalc acts as very simple local repository for your locally developed packages that you want to share across your local environment.

- ## For checking if a codepoint is possibly a JS identifier, using a gigantic switch statement seems 3.5x faster than binary search 
- https://twitter.com/jarredsumner/status/1451355843857768452
  - at least in Zig, which is an LLVM frontend
  - V8, esbuild and TypeScript use binary search
- Turns out, the microbenchmark was flawed. The inline while in main() made it inconsistent with real code. 
- Here’re updated numbers that are consistent with real code
  - Using a bitset is 3x faster with Unicode-heavy text, but only slightly faster for ascii text.
  - By “Unicode-heavy” I mean lots of emoji

- ## Also easy to forget: JS/Node is FANTASTIC at orchestrating IO. **Moving compute out of JS but keeping data flow in JS** is the best of both worlds, IMO
- https://twitter.com/FredKSchott/status/1440508008245514246
- I’m thoroughly convinced Go & Rust are great choices for core compute functions like compilers, bundlers, and the like. 
  - But I also still see the value in a larger JS ecosystem. In my experience, this is where most contributions to a project happen anyway
  - Agree. Core in Rust, plugins in JS seems like the right balance. And maybe _also_ plugins in Rust for those who want to optimize.
- Yep, that’s exactly what we do in Parcel right now. I think over time more of the core data structures will move too though (eg to enable better multi threading).
- Node is not great as orchestrating processes though. Which I have yet to see a build tool in this space not need to eventually do (unless it’s purely single threaded). I hope we can add better structured shared memory and make JS threads a real thing but we’re so far from that

- ## One of the reasons Vite is fast (and one that I often forget to mention) is that we manage to do 0 full AST parses by default during dev. 
- https://twitter.com/youyuxi/status/1440513631381123072
  - All dev server code rewrites are lexer-based (and initial lex by es-module-lexer which is written in C).
  - This of course excludes plugins that have to do full AST parses, but those can be fast too (e.g. TS transpiling via esbuild)
- Wait, so esbuild is not even used in simple cases? Wow, I thought it was the magic that powered Vite
  - esbuild does help when you have large dependencies that need pre-bundling. Plain JS source files are by default never fully parsed.
- One thing I’d really love to be able to do in vite is have more control over the HTML when doing SSR. The ssr-outlet is ok for body content, but it’d be nice to be able to render `<head>` (title, meta, etc) based on the page’s data as well.

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
