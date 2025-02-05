---
title: lib-ide-vscode-community-internals
tags: [codebase, community, internals, vscode]
created: 2025-02-04T17:20:35.702Z
modified: 2025-02-04T17:21:02.875Z
---

# lib-ide-vscode-community-internals

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Copilot Internals | Hacker News _202212](https://news.ycombinator.com/item?id=34032872)
- Why does “cushman-ml” suggest a 12B model instead of the 175B model?
- This is about the VSCode extension, which is obfuscated (maybe compiled) JS.
  - Their JetBrains plugin is written in Kotlin / Java but it spins up a agent server written in node.js which handles the business logic (building the prompt, caching, making completion requests to their API). I assume most of the code is shared between the VSCode extension and this javascript agent.

- Free idea for GitHub: a huge bit of missing context for the model right now is the last few edits made by the user. If you move your cursor to a different part of a long file, Copilot immediately forgets about that part of the file. If it knew the last few edits you did then it would be able to make much more intelligent suggestions based on the task you're working on, rather than just current cursor position.
  - This is a pretty cool idea even for just engineering the prompt! It's a complicated tradeoff to decide what should go into the context and what should be selected from other files (2000 tokens is a lot but sometimes not long enough for the longest files). Previous cursor location is a great signal directly from the user, compared to metrics like Jaccard similarity. I'd actually like to try this out for our next release of Codeium.
