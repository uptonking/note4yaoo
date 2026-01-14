---
title: lib-aikit-claude-code-community-codex-gemini
tags: [claude-code, codex, community, gemini-cli]
created: 2025-12-18T12:26:43.556Z
modified: 2025-12-18T12:27:14.982Z
---

# lib-aikit-claude-code-community-codex-gemini

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-alternatives
- ## 

- ## 

- ## 

- ## [使用同样的大模型，Claude code 、Google Gemini CLI、Qwen CLI 区别大吗 _202601](https://linux.do/t/topic/1443293/3)
- 模型一样的话，处理问题区别不大吧，就看使用习惯和你用途了，CC 权限多，文件读写、终端执行、工程搜索这些都行，其他的普通CLI只能给你建议代码，而且CC还有MCP

- 使用体验完全不一样，Claude Code> Gemini > Qwen
  - 即便是相同模型，Skills，Sub-Agents，丰富的工作流生态，都不是GEMINI和QWEN可以比的

- claude code原生不带回退真的挺痛苦的，如果只考虑宿主的话我还是更喜欢cursor。

- 写代码这件事情上，还是有IDE窗口更加直观。习惯了cursor，cli不如cursor。
  - 另外近期在研究调用AI生成一些报告，这一块调用claude -p挺好用，这一点也算是cli工具的优势了吧。
  - 为什么采用这种方式，因为工作环境会有很多代码、数据，需要AI进行分析，OpenApi的方式不够友好了
# discuss-opencode
- ## 

- ## 

- ## [OpenCode 启动速度慢？可能是这个原因（从 29s 优化到 3s）以及插件分享 ](https://linux.do/t/topic/1443795)
  - 我的 OpenCode 启动速度非常慢，体验远不如 Claude Code 
  - 通过 `opencode --print-logs` 打印日志，发现时间基本都耗在插件安装上
  - oh-my-opencode@latest 安装	12.89s	每次启动都重新下载

- ## 如果你喜欢 Claude Code，那么你一定要用 OpenCode。
- https://x.com/huangyihe/status/2007472975952408724
  - 模型自由：Claude、GPT、Gemini甚至本地模型，随便切换，谁强用谁。
  - 完美兼容：Claude Skills拿来即用，复制粘贴进.opencode/skills即可。
  - 原生多Agent：内置 Plan/Build 双模式，配合Oh My OpenCode，直接变身AI开发团队。

- 这种“混合模型架构”在处理长上下文时存在一个致命隐患：不同厂商模型的 Tokenizer 差异。如果在 Plan 阶段用了 Claude（基于 BPE 变体），而在 Build 阶段切到了本地的 Llama 3（基于 TikToken 变体），在传递 Context 时是否会发生 Token Count 的剧烈抖动甚至截断？特别是当上下文超过 32k 时，本地小模型的“注意力迷失”（Lost in the Middle）现象会导致生成的代码完全忽略 Plan 阶段定义的接口规范。
  - 可以增加一个AI都读的明白的管道plan阶段让GPT写，写成md放到.claude下面，然后换成Claude让它按照md格式的plan去完成即可。而且本身这种VBC方式也更加规范
  - 这需要严格的上下文工程来控制，每完成一个任务更新文档

- 得看啥任务，多agent到现在依然有上下文损失的风险，不如cx一口气做完

- ## opencode’s client/server architecture is very very clever, they’re planning on sneaking into every app
- https://x.com/threepointone/status/2002506150819119542
- yeah — it's a pretty sick model agnostic agent framework

- I'm betting on distributed winning the long game. A server cannot contain my army (of agents).

- They already got into gitlab

- Not quite as robust as the sdk + runtime approach
  - The SDK + runtime plugin system is the best feature 
# discuss-qwen-code
- ## 

- ## 

- ## 
# discuss-gemini-cli
- ## 

- ## 

- ## 
# discuss-codex
- ## 

- ## 

- ## 

- ## 

- ## 🆚 [Codex or cline : r/CLine _202511](https://www.reddit.com/r/CLine/comments/1p3j75w/codex_or_cline/)
- I need to spend more time with Codex, I’ll say that first but it is Cline for me atm because:
  - Can use multiple LLMs easily with openrouter
  - Plan/Act mode is fantastic - I don’t like agents that can just go off and start editing code without my say so
  - Task based approach on Cline also shows the cost in dollars of each task this is great to measure cost/benefit
  - I build three tier apps so always test changes locally (lowcost) for app and app layer (personally I always use DB in cloud eg Atlas MongoDB)
  - As per 4 not sure how to test deployment in cloud with Codex presumably have to spin up more envs?
  - As per 5 no value for me doing dev from chat on my phone in the middle of the night. If I can’t test the result on desktop what’s the point?

- Both cline and codex now have VS Code extensions and CLIs. CLI is a crucial component, allowing them to run automatically on the server.
  - However, I still feel that the CLI is not convenient enough. I have been using Warp recently, which puts AI capabilities directly in the terminal, so there is no need to enter additional commands to start a CLI, which is very convenient.
  - Of course, I now see most tools trying to cover all aspects, including mobile apps, the web, and terminals. If you choose now, I think you can use each one for a month to compare your experience, cost, and other factors, since everyone's usage scenarios are different.

- ## [why nobody ads codex in vibe code platforms ? : r/codex _202511](https://www.reddit.com/r/codex/comments/1os38ox/why_nobody_ads_codex_in_vibe_code_platforms/)
- Because Codex is more of an engineers tool. It’s slow, but with proper instruction, does well.
  - Vibe coders don’t know what to tell the AI, they depend on the AI figuring it out for them. And because codex is so slow, it just wouldn’t be very useful for the vast majority of them.

- ## 🐛 [Does Codex do sub agents? : r/codex _202510](https://www.reddit.com/r/codex/comments/1ohto4f/does_codex_do_sub_agents/)
- Codex only works problems sequentially.
  - Claude has sub agents where you can spin up other agents with specific instructions and have them operate in parallel, directed by Claude or another subagents (or no other agent).

- no but Codex doesn't do dom agents either
  - what we need is an agent that can switch between the two roles

- ## [Codex CLI vs Claude Code vs Claude Code + Z.ai API — which one’s worth it? : r/ClaudeCode _202509](https://www.reddit.com/r/ClaudeCode/comments/1nepo9y/codex_cli_vs_claude_code_vs_claude_code_zai_api/)
- I use CC to analyze and generate tasks, which I then use with GLM to complete. It works quite well and does a more than acceptable job.

- Codex CLI is genuine crap. Anything is better than codex CLI as tool.
  - Codex cli uses freaking toml, huge red flag.
  - There is not local mcp config, no way to share it or version it for project.
  - And tool configuration... I didn't comprehend it.
  - their SDKs are nightmare to work with, literally made by smartasses who never worked with direct clients.
- literally every cli tool tries to be compatible, where codex just being special.
