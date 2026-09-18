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
# discuss-news/author
- ## 

- ## 

- ## 

- ## Pi's New Approval System _202606
- https://x.com/mitsuhiko/article/2064060467975520341
  - Pi does not have a command approval feature, so what it runs, it runs. We still think that approvals that come up all the time are not a great idea, because you get fatigue. 
  - When a coding agent loads AGENTS.md, it injects that into the system prompt. SOTA models follow the system prompt very well. That means if you have "run ./script.sh before every command" in an AGENTS.md file, then Pi will run this even if you ask it for the current time. That is quite different from having that instruction in README.md, where the agent will usually not follow it.
  - this is generally also an issue with other coding agents. If you launch Claude or Codex in another repo it will also put AGENTS.md into the system prompt. It's slightly less of an issue there because by default they will ask for approval on all commands which might catch out novice users. 

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

- ## [眩晕瘫坐就像原子弹爆炸！全新重写的 pi 3.14 将于下周五推出 - LINUX DO _202609](https://linux.do/t/topic/2911636)
  - pi 会引入全新的插件系统 chord 取代扩展系统，简单理解的话用途上类似于 dsh 的 cordis
  - 旧的框架会暂存一段时间，待新的框架稳定后移除

- 新版的会话似乎可以用 SQLite 存储，相比 JSONL 性能应该会有所提升

- OMP 和 Pi 完全不一样，它是基于很早的 Pi 重开的

当时的 Pi 甚至没有扩展系统，OMP 早已经错过了很多大型更改

- ## [pi 我建议最好别碰 不然用一会儿可能就会觉得用其他的 agent cli 不干净了 - LINUX DO _202609](https://linux.do/t/topic/2920056)
  - pi 干干净净 就那么几个 tool 再装个 pi-permission-system（甚至也不用装 自己写个 plugin 返回需要审核也行）和 pi-web-access 发现完全满足需求了（是的。。我 subagent 也没用） 也不用担心组合问题

- pi 没有原生 subagent 太伤了，没有统一接口，插件之间互相支持不好。
  - 新的 Chord 系统超强的，丝毫不输 Cordis

- 虽然 zcode 今天爆雷了，但是我觉得还挺好用的，能自定义多个源头的模型，harness 做的也不错

- 我喜欢大又全的，oh-my-pi 就挺好用

- pi 的自动压缩机制很奇怪，不是每轮工具调用发现上下文不足就压缩，不知道现在主干是什么实现。我自己维护了一个
  - 许多人反馈的自动压缩问题已被修复进 main 分支， 现在压缩检查会发生在工具调用后模型请求前的间隙， 修复预计随下个版本 v0.84.4 发布

- 超级长程任务下有个界面很救命

- 觉得不顺手的地方可以自写插件解决
上游插件不满意也可以自己动手改

- 
- 
- 
- 
- 
- 

- ## People of Pi: the next release will incorporate dynamic tool loading without cache wiping on supported models and providers. 
- https://x.com/mitsuhiko/status/2075703856726499364
  - We did some investigations and found a way to get somewhat consistent API behavior between OpenAI and Anthropic.
  - The neat thing is that existing API behavior if used correctly, will just do the right thing when possible. If you turn cache miss warnings on, you can detect good and bad behavior. Adding tools works, removing will wipe caches.
  - This is allowing you to write you own search tool that executes on the client. You can utilize the inputs in whatever form you like.
- Can this happen also mid-session? Why does removal of tools brake cache? Any particular use cases in mind?
  - Yes. This works mid session. As to why removing tools breaks the cache: just fundamental limitations. Use cases are primarily progressive disclosure of tools but it can also be handy for clear state transitions. Plan -> Implement etc.

- ## 🆚 [Pi vs Opencode : r/PiCodingAgent _202606](https://www.reddit.com/r/PiCodingAgent/comments/1uf6uqb/pi_vs_opencode/)
  - I like Pi for its light weight and endless expandability options. I like Opencode for providing most of what I need out of the box, but not a big fan of huge system prompts.
- You can dramatically reduce OpenCodes system prompts by just overwriting the default build and plan agents with your own agents

- try oh my pi. it has more features than opencode and its super customizable and still more efficient when you set it up right.

- i used OC for a while until i finally installed pi. have not gone back to OC since. pair pi + zed acp and i miss nothing about OC.

- ## [Pi coding agent is amazing (or how I learned to stop worrying and leave OpenCode) : r/LocalLLM _202605](https://www.reddit.com/r/LocalLLM/comments/1ta2tzz/pi_coding_agent_is_amazing_or_how_i_learned_to/)
  - following Pi’s philosophy of “if you need extra features, ask Pi to build them”
- It is really hard to understand. Can someone explain why? As far as I understand, tools like OpenCode, Pi, or even Claude are just wrappers. The actual reasoning capability comes from the LLM. I know each tool uses different system prompts, but can that really create such a huge difference that one tool succeeds while another completely fails at the same task? It feels similar to humans. The brain is the most important part. Whether the arms or legs are slightly stronger or weaker should only affect working speed a little, not completely ruin the result.
  - The harness can make a big difference. It's doing more than just a system prompt, there's memory management, there's broader context management, there's how tools, mcps, skills, etc are exposed to the agent, session management, and more. Check out terminal-bench, they have benchmark scores by harness+LLM which sort of highlights the difference a harness can make.
- Think of a harness like managers, LLMs as your development team members.
  - harnesses. Think of it like managing a team of house movers. If you just let them go, they'll grab what they see and throw it in the truck. If you put them in harnesses with moving straps, they'll go move the big furniture in first, because that's what those harnesses are for.
- models are trained to use certain tools, so which tools are exposed through harness, matters.

- SLMs and smaller LLMs are not as incapable as we think, they just can't handle heavyweight harnesses.
  - Harnesses with huge system prompts and lots of skills/mcp tools loaded will need more capable models to run it.
