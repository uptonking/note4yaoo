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
# discuss-opencode
- ## 

- ## 

- ## 

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
