---
title: lib-aikit-code-opencode-community
tags: [community, opencode]
created: 2026-01-17T22:41:11.548Z
modified: 2026-01-17T22:41:25.867Z
---

# lib-aikit-code-opencode-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## [What's the point of Opencode's built-in clipboard? : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1qquefr/whats_the_point_of_opencodes_builtin_clipboard/)
  - Why does Opencode have a built-in clipboard that overrides your terminal's clipboard, and doesn't let you paste out of it? It's very frustrating.
  - Even for simple things, like copying a block of a conversation for documentation seems impossible with Opencode, outside of a clunky screenshot. So I assume I'm missing something and Opencode's documentation is horrible.

- Have you tried ctrl-shift-c and ctrl-shift-v? There's also ctrl-ins and shift-ins
  - Supposedly you can run 'opencode export' from the command line too for a raw text dump (saw a GitHub issue yesterday, haven't tried it yet).
  - And finally there's tmux's copy mode (albeit opencode's scrolling behaviour limits its usefulness to only what's on the screen, and adds some indentation)

- OpenCode has a text entry box, a sidebar, and a header that you PROBABLY don't want to copy. You may also want to be able to copy more than is visible on the screen, so you need OpenCode to be able to scroll back to let you select more stuff. It feels a little screen or tmux adjacent.

- I have been using Linux for months and copy and paste are completely and utterly broken anyway.

- ## opencode’s client/server architecture is very very clever, they’re planning on sneaking into every app _202512
- https://x.com/threepointone/status/2002506150819119542
- yeah — it's a pretty sick model agnostic agent framework

- I'm betting on distributed winning the long game. A server cannot contain my army (of agents).

- They already got into gitlab

- Not quite as robust as the sdk + runtime approach
  - The SDK + runtime plugin system is the best feature 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What would be the best memory-bank in Opencode, coming from Roo Code with MemoryBank injected in the prompts. : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1qe28fd/what_would_be_the_best_memorybank_in_opencode/)
- Simple Memory Plugin from @knikolovx. It is a very simple plugin, but also very effective. And it was created with programming in mind. https://github.com/cnicolov/opencode-plugin-simple-memory

- Ive written my own. I've used a meta tool pattern to keep tools down to three and got various connectivity guides/templates but I always encourage people to try and adapt something or build something suited to their workflow. https://github.com/ScottRBK/forgetful
