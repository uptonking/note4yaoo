---
title: lib-ide-zeddev-community
tags: [community, ide, vscode, zed, zeddev]
created: 2024-08-24T16:07:05.125Z
modified: 2024-08-24T16:14:33.275Z
---

# lib-ide-zeddev-community

# guide

# discuss-stars
- ##

- ##

- ##
# discuss-collab 🔀
- ##

- ##

- ##
# discuss-storage 💾
- ##

- ##

- ##
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Zed 1.0 is a complete code editor _20260429
- https://x.com/zeddotdev/status/2049498864093184045
  - 1.0 doesn't mean done, and it doesn't mean perfect. It means most developers can quickly feel at home in Zed. 
  - We'll keep shipping every week, the way we always have.
  - [Zed is 1.0 — Zed's Blog _202604](https://zed.dev/blog/zed-1-0)

- WSL support is my favorite feature. That said, git integration still has a long way to go. Separate staged and unstaged diffs would be a great addition!

- ## 🆚 We just shipped v0.216.0! Word-level diffing just landed.
- https://x.com/zeddotdev/status/1998804461909639384
  - You can now view the git commit history of any file. Select the `File History` option in the right-click editor context menu to open it.

- Character diff when though? @code to @zeddotd here. The character diff makes things much more clear.
  - There's currently a PR for AST-based diffing up for review

- Split diff
  - We're working on it
# discuss-gpui
- ## 

- ## 

- ## 

- ## 💥 [Why is Zed's binary size comparable to VS Code/Electron despite the GPUI architecture? : r/ZedEditor _202602](https://www.reddit.com/r/ZedEditor/comments/1r537ux/why_is_zeds_binary_size_comparable_to_vs/)
  - the Zed binary is still hovering around 70MB+.
  - Since Zed isn't shipping a full Chromium instance, what is taking up that space?

- Here it is 350mb.. I'm running zed-preview-bin from AUR
  - It should print the 20 largest crates in the binary, where a crate is like a library. Only thing is that if crate A calls a generic function defined by crate B (or, the optimizer makes crate A inlines a function defined in B, etc), this gets counted in A's budget.
  - It's possible that the zed binary includes large assets such as whole wasm binaries inside its binary (Zed uses wasm for its plugins). This will make the .text section to be very large (or even other linker sections, depending on where the asset is stored)

- Rust statically links all of its dependencies. And 70mb is pretty small, at least when it comes to Rust UI libraries

- Are binary sizes a big concern these days? Especially when we’re talking about something like 70MB? My own main concern is performance and reliability and how much memory it uses.

- 70 MB is actually pretty small when you consider that Rust statically links all its dependencies so the binary includes everything it needs to run.
  - Rust’s compiler also does dead code elimination, so it only includes what’s actually used. This keeps the binary smaller than the sum of the binary plus it's libraries would.

- I am more concerned about HOW are they developing ui? Coming from frontend, I can’t imagine not having hot module reloading, instant feedback and so on. I tried doing it in rust and every change you do - you need to wait for compilations, which is quite long…
  - You get used to keeping track of changes in your head 😜 we had some other tricks as well. component preview, our custom storybook-style bin for building smaller pieces in isolation…
  - Someone in the community did get subsecond working for gpui but only for single crates (Zed is split across hundreds? of crates at this point.)
  - When we rewrote gpui (`gpui2`) we move to a tailwind-esque method chaining approach to styling that makes prototyping pretty quick and manageable despite no live reload.
  - Fun fact: `gpui1` had hot reloading, because the entire ui used to be styled via one giant 50k+ line json file…
# discuss-architecture
- ## 

- ## 

- ## 

- ## Zed 的插件 都是 WASM，rust 里面 wasmtime 编译成实例后基本上没有冷启动时间，注意到这个 ondemand 插件启用机制，真的太舒服了
- https://x.com/Canmi21/status/2031921302983135452
- 好像Wasm只能写一些桥接业务逻辑，LSP很多还是外部的需要一些启动时间。

- 还要启动单独的lsp的, 还有一个node.js
# discuss-internals
- ## 

- ## 

- ## 

- ## 

# discuss
- ##

- ##

- ##

- ##

- ## 🚀 [Zed, a collaborative code editor, is now open source | Hacker News _20240124](https://news.ycombinator.com/item?id=39119835)
- GPL for the editor, AGPL for server-side components). GPUI, the UI framework that powers Zed, will be distributed under the Apache 2 license

- I am confused why the install is over 350mb, including a 300mb binary. I thought Electron-based stuff was big but this is even somehow more!?
  - It comes with quite a few language servers built-in.
  - The core app itself is 100% Rust, but it supports integration via Microsoft's Language Server Protocol. In practice, this means you will be running daemons locally for each language, which may be written in any language. Often these daemons are written in NodeJS since the reference implementation is in NodeJS.
- Zed developer here. Indeed we do not bundle the LSP binaries into the final binary for the reasons you've stated; and I do agree that the binary is kind of big, though at present .dmg compression gets us a long way (as the .dmg itself is ~115Mb). Right now we ship an universal binary, so half of that size is essentially unused

- Interesting to see how they are gonna approach integrating plugins/extensions system, because this is likely gonna be one of the major factors affecting adoption and ecosystem growth. 
  - Helix devs, for instance, lean towards a Scheme-like implementation.

- 
- 
- 
- 
- 
