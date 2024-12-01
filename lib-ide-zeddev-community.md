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
# discuss
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
