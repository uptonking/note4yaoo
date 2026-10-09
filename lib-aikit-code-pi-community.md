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

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Pi v0.99.0 is out! _20260930
- https://x.com/PiChangelog/status/2104986274730029265
  - Codemode runs model-written JavaScript in a QuickJS sandbox that calls pi's tools in parallel; MCP servers are now built-in via mcp.json or pi.registerMcpServer().
  - Codemode runs model-written JavaScript in a QuickJS sandbox that calls pi's tools; enable with defaultTools or --tools, configure with codemode.mode and codemode.inlineBudget. tool_search finds undeclared tools and declares them on demand.
  - MCP servers over stdio or streamable HTTP with OAuth come from mcp.json (global or per-project once trusted) or pi.registerMcpServer(); managed with /mcp and pi mcp add|remove|list|login|logout.
  - Sign in with ChatGPT is now available in /login 

- ### Pi 1.0 shipped with codemode _202610
- https://x.com/lucataco/status/2105829482741301696
  - Instead of 50 tool calls dumping raw output into context, the agent writes one script that does the work and returns only the answer
  - it's off by default, update settings to always have it or call it directly for one offs:  "pi --tools read, bash, edit, write, codemode"

- https://x.com/mitsuhiko/status/2105005860673954272
  - mcp and codemode are just shipped extensions. If you turn off tools, they are gone and you can disable those with "pi config" btw.

- https://x.com/chasen_liao/status/2105137326938878198
  - 新版本 Pi 如何开启 code mode
  - 在 ~/.pi/agent/settings.json 加一行就行：  "defaultTools": ["+codemode"]
  - 单次临时开：  pi --tools read, bash, edit, write, codemode

- [Code Mode: the better way to use MCP | Cloudflare Blog _202509](https://blog.cloudflare.com/code-mode/)

- ### Pi 新东西MCP + Codemode，一分钟给你讲清楚
- https://x.com/xiaomovps/status/2105919712727367821
  - MCP 负责告诉 Pi“我有哪些工具”，Codemode 负责决定“这些工具怎么一起干活”。
1、最直接影响的是上下文

以前一个 MCP 有几十个 Tool，Tool Schema 很可能从第一轮就全部塞给模型。

现在 Pi 默认不会这么干了。

模型只知道这里有 GitHub、Linear 这些能力，真正需要的时候再通过 Tool Search 去找具体工具。

也就是说：

工具可以越来越多，但 Context 不需要跟着一起变胖。

2、多个 Tool 可以一次一起跑

比如查 20 个 Issue，再筛出最严重的 5 个。

以前可能是：

调用 Tool → 返回结果 → 模型继续想 → 再调用下一个 Tool。

Codemode 则可以直接写一段 JS，在里面并行调多个 Tool、过滤结果，最后只把真正需要的内容交给模型。

中间那些几十 KB 的原始数据甚至不用全部进入 Context。

3、 PI 的 token 和响应速度

MCP 装得越多，以前越容易出现：

Prompt 越来越大、Cache 容易变化、每轮都带一堆根本用不到的 Tool。

现在更像按需加载。

你装 5 个、10 个 MCP，不代表每一轮模型都要背着它们一起跑。

这其实又回到了 Pi 一直在做的事情：

不是限制 Agent 能力，而是让它只在需要的时候看到需要的东西。

但是我具体测试下来的话 会有一些影响，还不是很稳定，所以在使用 MCP 的时候 我会默认把这个模式关掉

现在这个模式是 MCP 的默认模式，等后续官方的调整，不然你在正常使用的时候会出现一些问题

- Claude Code 现在也这样，工具先只有名字，用到再拉 schema。我一个会话里几十个工具都是这么挂着的

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
# discuss-pi-alternatives
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [DeepSeek Harness developer preview | Hacker News _202608](https://news.ycombinator.com/item?id=49285244)
- How is that different from what Pi already does?
  - Pi can only log what the model shows it. Many models keep their thinking traces hidden and only provide a hash or something to recover it on subsequent resumes. DeepSeek shows CoT traces, and is maybe the best model that does so, I think? Kimi stopped providing CoT traces a little while ago in their subscription service via Kimi Code, I believe. I haven't checked GLM or Qwen 3.8 Max, though I guess if you're hosting the open models yourself or using an alternative inference provider there's probably got to be some way to get at that data.
  - Anyway, this particular harness isn't doing anything unique, but the combination of an official agent intentionally keeping the data and making it accessible to the user and a model API that provides all the information is unusual and worth calling out. It used to be common, most APIs and models and agents showed the reasoning, or could be configured to do so. Most no longer offer it.
- pi also happily shows and stores deepseek CoT traces.

- I have read the underlying paper, and found it may be useful, but not that useful.
For those who want to know what it achieves: it adds hot-reload and dynamic enable/dispose capabilities to a plugin system, like the one in Pi agents, though they push the boundaries further, to the UI components and so on.

- 👷(pi): just read the paper, and there aee definitely some interesting ideas in it.
a plugin's registrations returning individual cleanup handlers is nice. in pi, you clean up all registrations in one go in the session-shutdown handler.

i also like the use of generator to to clean up partial registrations nicely.

the cross-plugin dependency injection and resolution i'm not so sure about. it comes with a lot of footguns and limitations as pointed out in the paper.

works ok within a single compilation unit, i.e. a plugin with many modules. does not help with typing of cross-plugin dependencies.

most plugins do not have dependencies on each other, so this more complex system doesn't win you much, e.g. with load order and conflicting registrations (i.e. two plugins registering the same tool).

being able to reload a single plugin on change while letting the others not in its dependents list jug along is neat. but that also only works if plugins actually declare dependencies (see last paragraph), and also has a lot of limitations. and the simple case, a plugin with no dependencies or dependents, which i'd say is the 90% case, does 't need that complexity either.

definitely cool stuff tho! remains to be seen how well it works in a real plugin ecosystem.

> they push the boundaries further, to the UI components

can you elaborate on this? pi extensions support contributions to the UI. in pi v1, they are limited to in-process UI. v2 splits server and client, and with that UI.

- If you run the `dsh`, you can go to the Settings -> Plugins, and you can find that they just write all UI components as plugins(maybe not all, I don't check). Also, you may ask the harness to write a UI plugin for you, I just read some neat examples somewhere.
  - ah. you can also ask pi to write a ui plugin for you. internals haven't migrated to plugin architecture yet tho.

- Based on what I've read today, DeepSeek Harness seems to be similar to Pi Coding Agent in design. Both are barebones to start out and rely heavily on plugins. However, 3 things make DSH stand out. 
  - 1. Plugins in DSH are required to have cleanup handlers, so I guess you could clean up plugins that are no longer used mid-session and prevent it from interfering with the current task? (unsure about this) 
  - 2. DeepSeek V4 models are post-trained on DSH. Given how cheap DS V4 is compared to OpenAI and Anthropic models, running DS V4 in DSH could be much more cost-effective while barely losing performance. 
  - 3. It's utilized and maintained by a large lab dedicated to open source AI. It's always nice to get new open source tools from large labs so that we are not always relying on small teams doing the heavy lifting.

- ## [DeepSeek Harness vs Pi Agent are they converging on the same philosophy? : r/PiCodingAgent _202608](https://www.reddit.com/r/PiCodingAgent/comments/1vnzn48/deepseek_harness_vs_pi_agent_are_they_converging/)
  - Looking at it alongside Pi, it feels like there’s a similar philosophy:
  - keep the core/harness small, and make capabilities composable at the session/plugin level.
  - Pi has extensions, skills, tools, prompts, etc., while DeepSeek Harness takes the plugin approach even further.
  - Is this essentially the same architectural direction?

- Pi's killer feature is that you can request it to extend itself. It knows where its documentation is.
  - there's a "creator mode" that works similarly to pi where you can ask the coding harness itself to create plugins for dsh

- I just checked and looks like One of its dependency was pi. I guess it is built on top of it.
  - It is not built on top of it, it can be integrated with it
- I think you are correct. its not built on top of it, just using pi as one of its llm adapters

- They seem similar to me with an interesting distinction regarding how they manage the extensions/plugins. The deepseek harness is built on a framework extended from earlier chatbot work where loading and unloading of plugins is done in a rigorously controlled way so that it can be done live within the session. Pi sidesteps this altogether by making session reload trivial to do. 
  - For single user environments, the rapid reload seems like the cleanest fix to me but there might be reasons why hot swapping plugins has material benefit. 
- Yeah, that’s a good distinction. I also wonder whether Pi’s trivial session reload is the simpler abstraction, unless true hot-swapping provides a meaningful benefit for long-running agents.

- This is definitely the direction as extra harness kind of get in the way as model capability increases. So you need to adjust external harness by model you use, which requires a pluggable/extensible architecture.

- It's code is very bloated. Seems vibecoded as hell

- They have a paper, of which I understand nothing!
  - True!!  From what I understood The paper is about making software components “Lego-like.” Instead of restarting an agent whenever you change its capabilities, let it safely reconfigure its own runtime while it's running and be able to roll those changes back.

- ## DSH（DeepSeek Harness）和 Pi Agent，架构哲学其实是两条相反的路，越看越觉得值得拆开聊聊。
- https://x.com/limbopeng/status/2087932451243041142
- Pi 的哲学是做减法。Mario Zechner 做 Pi 就是烦透了 Claude Code 这类工具越堆越重，于是把核心砍到只剩 read/write/edit/bash 四个工具，系统提示词不到一千 token，没有 plan mode、没有 subagent、没有 MCP，甚至默认不做权限校验。这是一种克制的极简主义——核心足够薄，剩下的全交给外部扩展去做，让你自己决定要不要加回这些复杂度。
- DSH 的哲学是做加法后再拆碎。它不是精简出一个薄核心，而是把整个 agent 系统的每一层——模型、工具、文件系统、Shell、沙箱、会话存储、Subagent，甚至 Agent Loop 本身——全部做成可替换的插件。官方那套 Coding Agent 只是 “用这些插件拼出来的一个默认答案”，不是唯一答案。这个模块化的颗粒度比 Pi 深了一层：Pi 是核心不变、外围可插拔，DSH 是没有不可替换的核心。
- 再往底层看，两者对 “谁该拥有系统控制权” 的答案也完全不同。Pi 的答案是开发者：极简是为了让你把每一步都看得清楚、改得动，它信任的是写代码的人，而不是运行时的 agent 本身——所以宁可不做的事就不做，也不让核心替你做决定。
- DSH 的答案更像是把控制权逐步下放给运行时本身：连 Agent Loop 这种最核心的调度逻辑都能被换掉，意味着系统本身没有预设 “应该怎么跑” 的立场，一切规则都可以在运行时被重新定义。这其实是两种对复杂度截然不同的态度：Pi 认为复杂度是负担，要主动砍掉；DSH 认为复杂度应该被结构化、装进插件里，而不是消灭，因为消灭了就没法长出新东西。
- 真正拉开差距的是自进化这件事。
  - DSH 已经能让 agent 在运行时检查自己的能力边界，现场写一个插件挂载上去，然后在后续任务里直接调用这个刚获得的能力——虽然现在还很实验性，动态插件只存在内存里，重启就没了，也不能自动沉淀成永久插件，但这个方向已经打开了。
  - Pi 的扩展机制目前还是人写 TypeScript 扩展、显式安装，是静态的，agent 自己不会在任务执行中主动发现能力缺口然后现场造工具再用上。这也呼应了架构哲学上的分野：Pi 把 “谁来扩展系统” 这件事留给人，DSH 在尝试把这件事也交还给 agent 自己。

- pi can extend itself.just fine when it finds a gap. i know of no single extension that was written by a human.
  - I can attest to this. Previously for an experiment I swapped out pi's edit tool, AI writing the glue. So even 1 of Pi's "core 4" can be replaced.

- 我记得 Pi 也是支持动态扩展的，不过确实应该是人来指定触发，而不是自我进化出来的。
  - 感谢纠正，是的，Pi 是有运行时动态注册能力。
- pi也想让模型自己写扩展自进化，自带这方面skill，x上宣传过这方面的能力。但是具体还是要看模型本身能力的适配才行。

- 不是简单的“可以加载插件”，而是把动态装卸后的依赖传播、资源撤销、局部隔离和失败回滚一起纳入内核

Agent 发现能力缺口
  → 生成/安装新插件
  → 在隔离 Context 中挂载
  → 运行评测或 shadow traffic
  → 通过则提升为正式 provider
  → 失败则卸载并恢复旧 provider

- 其实两者没有什么根本性的区别，都是以插件为中心，让用户去自由组装，每个人可以按照自己的品味打造专属Agent！

- ## [和 PI Agent 什么区别？ · deepseek-ai/deepseek-harness _202608](https://github.com/deepseek-ai/deepseek-harness/discussions/888)
- 我认为是比pi更自由，但是开发起来也会更复杂一些

- 不是简单的“DeepSeek Harness 比 Pi 更好”，两者的抽象层级不同：

Pi 的扩展 API 更直接：extension 注册 tools、commands、prompts、skills、hooks，开发和复用成本低。
DeepSeek Harness 把模型、工具、session、subprocess、credentials、MCP 等拆成 Cordis service/provider，宿主组合边界更细。
现在两者已经可以直接连接：pi2dsh 把 Pi 的公共扩展面实现成一套通用 Host ABI，Pi 包不需要改源码，也不需要先生成转换 bundle

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
