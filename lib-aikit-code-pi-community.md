---
title: lib-aikit-code-pi-community
tags: [community, pi]
created: 2026-08-14T21:43:35.305Z
modified: 2026-08-14T21:43:42.546Z
---

# lib-aikit-code-pi-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## Pi 两位作者的见解： _202608
- https://x.com/dotey/status/2089127369596383363
  - On memory: code is the ground truth. code itself is evolving.
  - Bash is all you need: llm are trained to use bash.
  - Build context efficient tools, tools better than mcp
- ask llm to pull the data, and build tools

- 我在实践k8e-sandbox的时候发现mcp比cli处理好慢，所以把mcp去掉了

- MCP 更适合多人共用或者复用把，一套skill 每个人都要装
  - 没有 skill 好复用，如果有 token 还得每个地方都配，cli 登录一次就够了，skill 也可以 link 到其他 agent skills 目录

- Great point regarding Skills vs MCPs. One of the things I dislike with MCP is that it always forces you their own rules and formatting. + You never need 100% of MCP capabilities, even though your Context eats it each time it launches.

- Use embeddings does make a difference at scale, if your are working on enterprise architecture comprising hundreds of repos then I found it did make a difference across my own personal evals.

- 不赞同 “代码即真相，代码不需要记忆系统，不需要 RAG，模型很擅长理解代码结构”。 模型很擅长理解代码，不代表能找到对应的代码。古法写过代码的人都知道，难的不是写代码，是找到写代码的地方
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
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 这篇 Pi 压缩的文章，太过于朴实无华，就真的只是写个 prompt 让 LLM 把上下文总结一下，然后保留前面的system prompt 和工具调用，在摘要后可能还会保留最近几次对话。
- https://x.com/dotey/status/2088330456022311109
  - 这种压缩是有损的，不知道是不是有机制会去历史会话检索上下文？
  - 当然这确实是压缩上下文的最简单有效方案。
  - [How Compaction Works in Pi  _202608](https://earendil.com/posts/compaction-in-pi/)

- 看下来确实过于朴实，但用户能通过插件自定义自己的压缩行为，也可以在 jsonl 文件中检索完整历史

- 尽管这种方式的压缩是有损的，但是可以保留压缩后访问过的以及tool call path，这样检索的时候有更高的概率去reproduce。AdaL也是这样做的。
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [switching from opencode to pi any advice? : r/PiCodingAgent _202608](https://www.reddit.com/r/PiCodingAgent/comments/1vp3cn7/switching_from_opencode_to_pi_any_advice/)
- I use vanilla pi for quite some months already and I coded a bunch of stuff without using any extensions
- I ran pi for 2 months with noting on it just fine, web fetch tool was QoL improvement, that’s it, probably.

- Have these extensions installed. I have got all these and it's more than enough for me:
  - I run these in my setup which provides pi with a proper knowledge graph on Github. It's more than efficient even in token usage

pi-web-access - Fetches real-time web documentation, API references, and clones GitHub repositories directly into your workspace.

pi-mcp-adapter - Connects Pi to the entire Model Context Protocol ecosystem, allowing seamless integration with external databases and enterprise tools.

protected-paths - Prevents accidental deletions or overwrites of critical project directories like .git, .env, and node_modules.

confirm-destructive - Pauses execution and asks for manual confirmation before Pi can run high-risk, destructive terminal commands.

pi-subagents - Spawns specialized background agents to handle isolated debugging tasks or multi-file refactoring without bloating your main session context.

todo-tracker - Maintains a persistent, file-based list of development tasks so Pi remembers project goals across terminal restarts.

format-on-save - Automatically runs linters and prettier formatting hooks immediately after Pi edits or writes a new source file.

- Web search tool, subagent tool, and ponytail skill. That’s the simplest winning combo:
  - send agents to investigate, the where and the how
  - do smart fetching stop bloating context window with css and meta data, just content
  - And ponytail is a nice addition to keep changes under control. Do the bare minimum that meets the criteria.
# discuss
- ## 

- ## 

- ## 

- ## 
