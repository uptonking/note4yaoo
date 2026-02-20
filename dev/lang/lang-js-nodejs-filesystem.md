---
title: lang-js-nodejs-filesystem
tags: [filesystem, nodejs]
created: 2026-02-19T06:10:20.863Z
modified: 2026-02-19T06:10:41.718Z
---

# lang-js-nodejs-filesystem

# guide

# dev-xp

# docs

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-web-fs
- ## 

- ## 

- ## 

- ## 
# discuss-fs-runtime/compatibility
- ## 

- ## 

- ## 

- ## we have a tedious task of moving off of bun file apis _202602
- https://x.com/thdxr/status/2024147745024495794
  - we had opencode analyze all usage and come up with a plan for how things should be mapped
  - and now it's running in a loop opening one PR per file - each of which can be reviewed and safely merged independently
  - entirely done with kimi k2.5

- why?
  - at our scale we're exposed to so many different OS's and CPUs that cause crashes which node has already dealt with - probably years worth of work
  - given how much help cc needs with the basics unlikely these become prioritized anytime soon
- we decided to make opencode work in nodejs because this gives us a few options
  - node is way more stable on windows and we have a lot of pain there currently
  - electron desktop app can easily embed it without spawning another process
  - we're not certain about the future of bun for a few different reasons
  - gives us the option of freely exploring deno
  - lets people embed opencode in their own applications more easily
  - we've benchmarked things and we're not really benefiting from bun's slight performance advantage
- I believe opencode has a client/server architecture. when would someone feel the need to embed opencode v/s just call the API ?
  - it's a bit easier in lambda environments to call it as a library
- "slight performance advantage" Huh...? All the charts that get bandied around are showing like 2x speeds at least.
  - some of the benchmarks we ran showed even like 14x! but our use case isn't a server receiving a ton of requests so in practice it makes little difference. we're using it as a very very very low traffic server so less of a gap
  - we could even switch to nodejs sync apis and be faster than bun

- Are you moving off Bun for package management as well? Will you still be using bun for the tooling/package management? Or migrating off of that too?
  - NO
  - for us developing opencode, yeah no reason to move off
  - just everything at runtime should be agnostic

- bun files are like tech debt's passive-aggressive cousin - they dont yell, they just make everything slower until you finally move out

- My experience as someone who just built a little runtime-agnostic library is that Deno’s nAPI compatibility for file operations still isn’t quite there, so watch out for that.

- isn't oc desktop app is on tauri?
  - it's moving to electron
- we're moving off from tauri specifically for performance reasons too lol
  - The limit of what you can with Tauri’s webview was going to eventually lure you to Electron. Tauri just ain’t it for in app browser views.
- I’m just happy because it means I don’t have to learn rust to contribute

- Tauri feels like dogshit on Linux

- I was a big support Deno, still hope they do great things but switched to bun for better node_modules compatability. Deno was just doing some weird things and we kept having bugs.
- Deno works well on Windows + stable but you might run into other frustrating issues.

- Nice. And 1 more benefit is that maybe it can run on Android termux. Currently bun cannot run on termux so any Bun API based thing cannot run.

- opentui's goal is to support everything bun/deno/node
# discuss
- ## 

- ## 

- ## 

- ## 
