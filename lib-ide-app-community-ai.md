---
title: lib-ide-app-community-ai
tags: [ai, community, ide, pm]
created: 2024-05-10T06:17:15.244Z
modified: 2024-08-24T16:28:20.515Z
---

# lib-ide-app-community-ai

# guide
- pm-ai-coding
  - ai编程类热门产品可以在各大ide的插件市场搜索排序

- products
  - [Top 6 Devin AI Alternatives for Developer to Automate Codings](https://analyticsindiamag.com/top-6-devin-alternatives-to-automate-your-coding-tasks/)
# codellama
- https://github.com/meta-llama/codellama /202401/python
  - Code Llama is a family of large language models for code based on Llama 2 providing state-of-the-art performance among open models, infilling capabilities, support for large input contexts, and zero-shot instruction following ability for programming tasks.
  - We provide multiple flavors to cover a wide range of applications: foundation models (Code Llama), Python specializations (Code Llama - Python), and instruction-following models (Code Llama - Instruct) with 7B, 13B and 34B parameters each.
  - Code Llama was developed by fine-tuning Llama 2 using a higher sampling of code.
  - Our model and weights are licensed for both researchers and commercial entities, upholding(维护，支持) the principles of openness.

- [Introducing Code Llama, a state-of-the-art large language model for coding _202308](https://ai.meta.com/blog/code-llama-large-language-model-coding/)

- [codellama](https://ollama.com/library/codellama)
  - instruct	Fine-tuned to generate helpful and safe answers in natural language
  - python	A specialized variation of Code Llama further fine-tuned on 100B tokens of Python code
  - code	Base model for code completion
  - Fill-in-the-middle (FIM) is a special prompt format supported by the code completion model can complete code between two already written code blocks.

- [codellama (Code Llama) huggingface](https://huggingface.co/codellama)
  - This is an unofficial organization for the Code Llama models in the Hugging Face Transformers format.
  - https://huggingface.co/spaces/codellama/codellama-playground
  - https://huggingface.co/spaces/codellama/codellama-13b-chat
  - Code Llama in Hugging Chat: This is an end-to-end application in which you can use the 34B Instruct-tuned model.
- [CodeLlama huggingface](https://huggingface.co/docs/transformers/en/model_doc/code_llama)
  - The Llama2 family models, on which Code Llama is based, were trained using bfloat16, but the original inference uses float16
# code-ai
- https://github.com/princeton-nlp/SWE-bench /MIT/202405/jupyter
  - https://www.swebench.com/
  - [ICLR 2024] SWE-Bench: Can Language Models Resolve Real-world Github Issues?
  - SWE-bench is a benchmark for evaluating large language models on real world software issues collected from GitHub.
    - Given a codebase and an issue, a language model is tasked with generating a patch that resolves the described problem.
  - We have released SWE-agent, which sets the state-of-the-art on the full SWE-bench test set
  - https://x.com/jyangballin/status/1775114444370051582 /20240402
    - SWE-agent is our new system for autonomously solving issues in GitHub repos. It gets similar accuracy to Devin on SWE-bench, takes 93 seconds on avg + it's open source
    - We designed a new agent-computer interface to make it easy for GPT-4 to edit+run code
    - SWE-agent works by interacting with a specialized terminal, which allows it to: Open, scroll and search through files; Edit specific lines w/ automatic syntax check; Write and execute tests
  - https://github.com/princeton-nlp/SWE-agent /MIT/202405/python
    - https://swe-agent.com/
    - SWE-agent takes a GitHub issue and tries to automatically fix it, using GPT-4, or your LM of choice.
    - It solves 12.29% of bugs in the SWE-bench evaluation set and takes just 1.5 minutes to run.
# discuss-stars
- ## 

- ## Cursor 创始人自述ai编程正在走向第三时代：
- https://x.com/cryptonerdcn/status/2026839653849202788
1. 三个时代演进
   - 第一时代：Tab 自动补全（逐键输入 → 智能补全），持续近两年，极大提升低熵重复工作效率。  
   - 第二时代：同步 Agent（实时提示-回应循环），开发者仍深度参与每步，持续时间很短（可能不到一年）。  
   - 第三时代：自主云端 Agent，能独立处理大任务、长时间运行（数小时甚至数周）、极少人类干预。重点从“写代码”转向“构建由 Agent 组成的软件工厂”。
2. 核心变化
   - 开发者角色：从逐行指导 → 定义问题 + 设定评审标准 + 审阅产物（日志、视频录屏、预览）。  
   - Agent 运行方式：云端独立虚拟机，支持并行运行多个 Agent，互不干扰。  
   - 产物形式：易审阅的 artifacts（而非海量 diff）。
3. Cursor 内部真实数据
   - >35% 的 PR 由自主云端 Agent 创建。  
   - Agent 用户数已反超 Tab 用户（从 1:2.5 变为 2:1）。 
   - Agent 使用量过去一年增长 15倍。  
 - 采用第三时代工作方式的开发者特征：  
   - Agent 写几乎 100% 代码  
   - 时间主要用于拆问题、审产物、给反馈  
   - 同时启动多个 Agent 而非手把手带一个
4. 未来展望与挑战
   - 预计 1 年内，绝大部分开发工作将由这类自主 Agent 完成。  
   - 仍需解决工业级痛点：flaky 测试、环境稳定性、工具/上下文完备性等。  
   - 昨天的发布（指云端长时自主 Agent 相关更新）是重要一步。

- 自主云端不就是manus那种吗？感觉未来不应该仅仅是这样子？
  - 不完全是，manus其实应该叫放在沙盒里，云不云端倒是无所谓，因为还是面对人类同步交流。
  - cursor这次说的coding agent放在云端是为了和其他agent共同协作而不需要人类指挥。

- 第三时代真的来了，但大多数人还在第一时代的思维里。最难的转变不是工具，是心态：从「我在写代码」到「我在设计软件工厂」。

- 注定失败，non deterministic 系统永远都不可能在prod自主iterate

- ## wish cursor, windsurf, jetbrains junie, and all the ai vibe coders editors out there could just agree on one .rules file format
- https://x.com/enunomaduro/status/1918373761381752871
- Next project idea! Make a global .rules format compiler to all vibe coding editor.

- ## 📌 AI辅助编程的几类产品
- https://x.com/idoubicc/status/1888042418446139837
  1. AI代码编辑器，面向职业程序员，辅助写代码，debug，设计技术方案。代表产品：cursor, windsurf, trae
  2. 一句话生成项目，面向产品经理，输入 idea，快速实现一个 MVP，支持在线发布，快速验证需求，能实现简单的交互功能。代表产品：bolt, lovable, v0
  3. 指定品牌名生成落地页，面向电商卖家 / 独立创作者，快速为自己的商品或品牌生成一个 landing page , 支持在线编辑，一键发布。代表产品：pagen, wegic
  4. 输入 URL 或上传截图，快速复刻项目/组件，面向开发者，参考目标网站写页面的场景。代表产品：screenshottocode, copycoder 
  5. 其他辅助场景：一句话生成桌面/移动 App， 一句话生成管理后台，一句话生成 SQL 语句，一句话生成 API

- 尝试了一下落地页 AI 辅助工具，真心不错。

- 还有一类openhands，devin

- 几乎都在用

- ## 🤔 How Cline works 这两天一直在看 Cline 的源码，探究当前 AI Coding 编辑器背后的神秘技术。 _202501
- https://x.com/xiaokedada/status/1882697004670992774
  - [AI Coding 编辑器没有那么神秘 - How Cline works _202501](https://www.nazha.co/posts/how-cline-works)
  - Cline 的核心是依赖系统提示词以及大语言模型的指令遵循能力。在编程任务启动的时，收集系统提示词、用户自定义提示、用户的输入、以及所在项目的环境信息（哪些文件、打开的 Tab 等等），提交给 LLM。
  - LLM 按照指令输出解决方案和操作。
  - Cline 通过解析返回的操作指令（比如 `<execute_command />、<read_file />` ），调用编写好的 Tool Use 能力进行处理，并将处理结果再次交给 LLM 处理。
  - 也分析了为啥 Cline 会如此消耗 token，它是如何摆脱大语言模型的窗口限制的，@ 操作为啥起作用了...

- https://github.com/caicongyang/mini-cline
  - [Cline AI Agent 核心实现分析](https://github.com/caicongyang/mini-cline/blob/main/docs/core-implementation-analysis.md)

- cline非常棒，经典的react agent模式
  - cline一个很大的缺点就是system prompt实在太长了，例如MCP在我的场景里根本不需要，但是它也携带了，浪费很多token(不知道新版本优化了没有？)。

- cline能用本地的deepseek R1，例如7B，32B直接参与编程么？
  - 可以，他是开源的，你甚至可以自己修改相关的处理逻辑

- cline没有用tool calling吗？而是用解析特殊标识来实现调用工具的？
  - xml, 类似这样的格式。我自己写的agent就是几乎照搬了cline的格式。
  - function calling
- 我个人认为function call并不合适复杂处理过程。当然，cline目前这种系统提示词里all in one的模式似乎也不是很优雅
# discuss-autocomplete/ai
- ## 

- ## Introducing the next evolution of completions in GitHub Copilot: Next Edit Suggestions (preview). _20250213
- https://x.com/code/status/1889742273572737247
  - Also called, "NES" for short.

- GitHub Co-Pilot is the new internet explorer

- ## 💡 [LSP-AI: open-source language server serving as back end for AI code assistance | Hacker News _202406](https://news.ycombinator.com/item?id=40617082)
  - LSP-AI abstracts complex implementation details like maintaining document / context parity and providing different LLM backends.
  - Most editors should let you use multiple language severs at once, they merge the results together which can be annoying.

- Currently, whether multiple language servers can be active in one buffer is up to the language client. In Emacs for example, Eglot (built-in) doesn’t support this but LSP-mode (bolt-on) does.

- It would be very interesting to leverage this to edit documents as much as code. Obviously editor-dependent due to the language server.
- Isn't the entire point behind "language server" (guess it's referring to LSP - Language Server Protocol) that it gets rid of editor-dependent stuff?

- 🤔 Are there any text editors that use LSPs for non-coding tasks?
  - It's not really about the editor. The editor (the LSP client) just provides support for telling the server what the user wants a definition for, and how to display that back to the user.
  - Other non-coding uses of LSP that I'm aware of are spell-checking and grammar suggestions (LSP clients can display diagnostics), semantic syntax highlighting (e.g. for highlighting a markdown document), and projects like the one discussed here which just integrate more general-purpose AI.

- Very interesting approach. The folks at rift worked on LSP as an integration point for AI coding. But I think they are focusing on other things now.
  - My project aider provides a pair-programming UX, which allows complex interactions like asking for a change that will modify multiple files. Could LSP servers support more general AI coding like this?
- The problem with aider for me is that it works in the terminal, where as coding happens in the editor, where I most likely already have the file open I want to transform with LLM. I probably even have my cursor on the thing or can at least easily select the function etc. that needs to be changed.
  - CopilotChat.nvim solves this somewhat elegantly for neovim, providing a streamlined UI to interact with an LLM in a way that allows accepting suggested diffs to your currently open buffer. The problem however is that it only works with GitHub's Copilot chat, as the name suggests. Not sure how well Copilot stacks up against gpt-4o for example but I'd imagine not that well.
  - This is pretty much the kind of UI I'd want for interacting with LLMs, aside from the typical Copilot style ghost autocomplete.

- I want an LLM which uses an LSP to gather more context.
  - Aider uses Treesitter to improve code generation.
# discuss-ai-coding-free 💰
- ## 

- ## 

- ## You get 2, 000 free Qwen Code runs every day! `npx @​qwen-code/qwen-code@latest` Hit Enter, and that’s it! _20250808
- https://x.com/Alibaba_Qwen/status/1953835877555151134
  - 2, 000 requests per day with no token limits
  - 60 requests per minute rate limit
  - 2000 is for china users, 1000 for everyone else

- You kind of get the same deal with Gemini cli too. Just that it's 1000 requests per day, not 2000 like Qwen. You sign up through your personal Google account, not AI Studio API keys. And all requests go to Gemini 2.5 pro, which is better than Qwen3 coder?
  - It’s not 1000 Gemini 2.5 Pro requests per day. You only get 40-50 requests per day for 2.5 Pro and then it switches to Flash.
- 2.5 pro is bad at tool calling though

- Do you log/train/retain code written with Qwen Code free tier?  Didn’t see info on that on GitHub.
- almost all providers that allow free usage like google gemini cli, qwen code, the horizon beta model on open router etc use the data for training.

- I notice this is a Gemini-CLI fork. Is anybody else having trouble with the google_web_search tool?

- Is this the full qwen coder or qwen coder flash? Big regardless but if this is for the full coder then its game over.
  - the 480b version. full.
# discuss-terminal-ai
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Gemini is so far behind : r/GeminiCLI _202509](https://www.reddit.com/r/GeminiCLI/comments/1n7q049/gemini_is_so_far_behind/)
- totally agree. I tested the CLI and the "improved" Gemini agent, and ohh boy, what a nightmare. I gave it a simple task, and it ended up in a loop and wasn't able to fix anything. It was over and over, "I make it worse" or "I make a mistake, " and so on.
- I feel this. It's crazy because 2.5 Pro is an incredible model, but Gemini CLI is a mess.

- Gemini CLI is unusable for me. Qwen code is way better than Gemini CLI, though still not comparable to Claude or Codex.

- I wonder how much of the drop is due to your prompts (and configs) being optimized for Claude. I think somebody switching from Gemini to Claude runs into similar issues.

- ## [Qwen Code > Gemini CLI : r/Qwen_AI _202509](https://www.reddit.com/r/Qwen_AI/comments/1nk0wzj/qwen_code_gemini_cli/)
  - Compared to Gemini CLI, Qwen is a much better experience. Although Gemini 2.5 Pro can be very intelligent, it almost always fails a tool call once or twice, or formats the code it's adding wrong and apologizes over and over again. Qwen Code using Qwen 3 Coder Plus almost never fails tool calls and over all seems to understand the codebase better. I know Gemini 2.5 Pro tops benchmarks often but Qwen Coder has been much better to use in my experience. I use them both on the free tier.

- I agree Qwen seems better. Gemini-CLI honestly seems to function better when you use 2.5 Flash (In my opinion anyhow).
  - For features that need multiple files and lots of code to be written, Flash is not very good compared to Pro. Flash will also often dismiss instructions and execute a previous task that was cancelled. 
  - I feel that codex gpt5-medium > gemini 2.5 pro > qwen > flash 2.5 overall. Flash needs very specific prompts with small changes to work well, in m'y experience.

- Qwen CLI is extremely slow for me after a few messages. 

- ## 🆚 [Qwen3 Coder vs. Kimi K2 vs. Sonnet 4 Coding Comparison (Tested on Qwen CLI) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mi8lbl/qwen3_coder_vs_kimi_k2_vs_sonnet_4_coding/)
  - Claude Sonnet 4 was the most reliable across all tasks, with complete, production-ready outputs. It was also the fastest, usually taking 5–7 minutes.
  - Qwen3-Coder surprised me with solid results, much faster than Kimi, though not quite on Claude’s level.
  - Kimi K2 writes good UI and follows standards well, but it is slow (20+ minutes on some tasks) and sometimes non-functional.
  - On tool-heavy prompts like MCP + Composio, Claude was the only one to get it right in one try.
  - Qwen3-Coder feels like the best middle ground if you want budget-friendly coding without massive compromises. 

- I am absolutely baffled by all of these posts that claim Qwen3-Coder is better than kimi-k2. I've used both for weeks at Q4_K_XL and I keep returning to kimi-k2 every time. It's smarter and solves more problems than Qwen3-Coder in my experience.

- I just tried qwen-code + llama.cpp (unsloth's last update seems to have fixed tool calls?) + 30B-A3B on a real task. Based on my query, it did a SearchText tool call, after which qwen-code tried a 1.8M token API request, which of course immediately errored out. I am not impressed.

- I rotate between all of these. R1-0528 is still usually what fixes my code.
  - I'll use Qwen3-Coder when a task is simple and when there are cheap providers, but otherwise asking V3-0324 and R1-0528 still feel like asking the adult in the room

- I've tried 480b qwen, but GLM-4.5 Air 8bit blows that away. Its miles ahead in quality and speed.

- I think qwen-coder will have an advantage since they most likely did RL through it. Since the GLM team recommended Claude Code Router I have a feeling they may have done the same. So I would assume to see GLM perform better in Claude Code vs Qwen Code.

- ## [Let’s sync on CLI agents! What’s actually working for you? : r/ChatGPTCoding _202507](https://www.reddit.com/r/ChatGPTCoding/comments/1m73qb8/lets_sync_on_cli_agents_whats_actually_working/)
- The only model that works for agentic tasks is sonnet 4. Doesn't matter what cli I use. I've been using opencode with sonnet 4 via my copilot subscription and it works well.

- 100% not Gemini CLI. It was embedding hidden binary code and corrupting my files.

- ## [Google introduces Gemini CLI, a light open-source AI agent that brings Gemini directly into the terminal : r/singularity _202506](https://www.reddit.com/r/singularity/comments/1lk5h19/google_introduces_gemini_cli_a_light_opensource/)
- 
- 

- ## [Gemini CLI: your open-source AI agent | Lobsters _202506](https://lobste.rs/s/f9xdsg/gemini_cli_your_open_source_ai_agent)
- While the free tier is generous, there are these privacy concerns.
  - By default, Anthropic does not train generative models using code or prompts that are sent to Claude Code.

- ## [Gemini CLI: your open-source AI agent | Hacker News _202506](https://news.ycombinator.com/item?id=44373754)
- The biggest diffs from Claude code (the current champion): 
  1. Generous free tier (60 RPM!) 
  2. Open Source Apache (Standard after OAI Codex did the same)

# discuss-ide-ai
- ## 

- ## 

- ## [ACP: All AI edits are applied instantly without any diff view or approval : r/ZedEditor _202602](https://www.reddit.com/r/ZedEditor/comments/1r979j3/acp_all_ai_edits_are_applied_instantly_without/)
  - [Switch over to built-in Claude Code tools · Pull Request · zed-industries/claude-agent-acp](https://github.com/zed-industries/claude-agent-acp/pull/316)
  - Given a number of recent issues stemming from Claude Code using more subagents that don't play nicely with our custom mcp server, plus some slowly diverging behavior, we made the decision to just switch back over to the built-in tools and do more processing on the tool input/output

- ## 🤼 So maybe forking VS Code wasn’t the right move after all
- https://x.com/jayair/status/2007537887235969465
- Forking VS Code was never the real mistake. The mistake is underestimating how attached devs are to their 57 extensions and years of muscle memory.

- Do people actually use VS Code for languages other than JS / TS and Node?
  - It's so popular because it's easier to get VSCode working with the language you want than it is to install a full IDE that's probably better for the task. At uni people use it for LaTeX, C/C++, robotics, Jupiter notebook, etc. it's hard to find anyone using anything else

- I think forking opencode might be smarter

- Cursor's tab completion is still worth the $20, but I increasingly find myself not opening an IDE at all so I'm not sure how long that subscription makes sense

- ## [昨天试了一下阿里新出的 Qoder AI 编译器。效果竟然还行 - V2EX _202508](https://www.v2ex.com/t/1154911)
- 灵码并没有 deepseek 模型

- ## [Jules: An asynchronous coding agent | Hacker News _202505](https://news.ycombinator.com/item?id=44034918)
- This has been proposed/exlored in 2023 already: ChatDev: Communicative Agents for Software Development - https://arxiv.org/abs/2307.07924

- Google’s ability to offer inference for free is a massive competitive advantage vs everyone else
  - > Yes, for now, Jules is free of charge. Jules is in beta and available without payment while we learn from usage. In the future, we expect to introduce pricing, but our focus right now is improving the developer experience.

- Can it resolve merge conflicts for me? My least favorite programming task and one I haven't seen automated yet.
  - Claude Code has been creating and cleaning up lots of Git messes for me.

- Any coding solution that doesn’t offer the ability to edit the code in an IDE is nonsense. Why would I ever want this over cursor? The sync thing is kinda cool but I basically already do this with cursor

- Notice how no-one (up until now) mentioned "Devin" or compared it to any other AI agent?

- ## [Microsoft Open Sources Copilot | Hacker News _202505](https://news.ycombinator.com/item?id=44031344)
- Is there a good way to replicate cursor tab in VS code? I don’t mean the interaction model, but how accurate it is. What model does Cursor use? It’s quite good AND fast.

- So they make "building your own Cursor" easier. But at the same time they ban your fork from using Extension Marketplace.

- ## 👾 [VS Code: Open Source Copilot : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kqhljr/vs_code_open_source_copilot/)
- One of the biggest downsides for extensions vs. fork was the lack of access to UI. This will work towards better integration for all extensions. I like it.

- The biggest downside, to date, is not being able to officially use it in Code Server which arguably should have been a first class thing for enterprise customers.
- Yes and no, MCP and local models are not supported yet for enterprise customers (through vscode) and also since we can't easily install copilot in Code Server, the entirely of the functionality is non-existent.

- ## 💰 Windsurf revealed today that they have 500k+ active users and ~1M messages sent a day.
- https://x.com/deedydas/status/1893040524287971437
  - That’s 2% of the global software developer market of ~30M.

- Did you see Bolt hit 3 million users? I think the number of software developers is going to 10x to ~300 million thanks to vibe coding.

- I'm a PM that uses Windsurf, am I counted in 30M or is the market bigger because of people like me getting into programming?
- GitHub alone has over 100M MAUs, so the global software developer market is likely much larger than ~30M.

- interesting numbers, keeping in mind their top-down approach compared to the bottom-up growth trajectory of Cursor.
  - i wonder when they will hit the ceiling -> early adopters are already opinionated on any of these solutions.

- ## 🌰 Tiny teams are the future:
- https://x.com/benln/status/1889388151770325427
  • Cursor: 0 to $100M ARR in 21 months w/ 20 people
  • Bolt: 0 to $20M ARR in 2 months w/ 15 people
  • Lovable: 0 to $10M ARR in 2 months w/ 15 people
  • Mercor: 0 to $50M ARR in 2 years w/ 30 people
  • ElevenLabs: 0 to $100M ARR in 2 years w/ 50 people

- Yes! Mobile had this but smaller.
  • Vine – 0 to 1M users in 3 months w/ <10 people
  • Instagram – 0 to 30M users in 18 months w/ 12 people 
  • Snapchat – 0 to 100M users in 3 years w/ 50 people
  • WhatsApp – 0 to $1B revenue w/ 55 people
  - Measured in users not ARR

- https://x.com/benln/status/1890413609768956015
  - I can't wait to see how churn and revenue retention looks like for each of those companies in a few years.

- ## 为啥字节有了 MarsCode 还要推出一个新的叫 Trae 的 IDE？还是资源太丰富了，内卷的厉害
- https://x.com/_hisriver/status/1881210064083808393
- MarsCode 的重点和基因是 Cloud IDE + Playground，延续了 LLM 时代之前的 Cloud IDE 项目， 可以对标 Replit
  - Trae 对标的当然是 Cursor，对标 Bolt/v0 的也快了
  - 在早期探索阶段，这些不同的现有产品形态如果混在一起从原有产品上「升级」出来，是很容易背历史包袱互相扯后腿的，容易走偏搞错重点

- ## 🚀 Announcing GitHub Copilot Free _20241219
- https://x.com/code/status/1869449373995708703
  - No trial. No subscription. No credit card required.
  - main benefits of Copilot Pro are more models and unlimited requests quota.

- Does it not work through SSH?
  - It should. 

- ## [Show HN: Windsurf – Agentic IDE | Hacker News _202411](https://news.ycombinator.com/item?id=42127882)
- I've been using Cursor Composer heavily and it's great but buggy, and could be more agentic.
  - After about an hour with Windsurf, I find myself frustrated with how it deals with context. If you add a directory to your Cascade, it's reluctant to actually read all the files in the directory.
- 
- 
- 

- ## [Show HN: Aide, an open-source AI native IDE | Hacker News _202411](https://news.ycombinator.com/item?id=42063346)
- 
- 
- 

- ## Windsurf by Codeium which is a Cursor killer which is a vs code + copilot killer which is killing me keeping up with these _20241114
- https://x.com/wesbos/status/1856806422899822999
- Can't wait for Zed to become the standard. Then we will see Zed forks with AI features

- how much did YC invest in this one?
  - 250m is VC funding so far

- ## Bolt New 的产品和销售数据出来了！ 4周时间，从0到400万美金的 ARR！
- https://x.com/oran_ge/status/1856492253902258304
  - 这种爆发式的增长，核心是因为它解决了一个一直以来的行业难题： Web 是世界上使用最广泛的平台，但开发者却无法在浏览器中构建 Web 应用。
  - 通过开创性的 WebContainers 技术和先进的 AI Coder 解决了这个问题。

- ## StackBlitz 推出 bolt. new，可以看作 Artfacts V0 和 Replit 的结合体。
- https://x.com/op7418/status/1842034898317746328
  - 支持提示、编辑、部署的全栈流程
  - 带有完整的开发环境
  - 可以实时预览生产结果。
  - 最重要的是免费。

- "完整的开发环境" 这个不准确，他们的运行环境使用的是 WebContainer 近端容器技术，只支持 JavaScript 技术栈，是一个几乎零成本的 IDE 解决方案，处理不太复杂的前端项目绰绰有余，可以确保 bolt 在线运行环境和真实本地环境一致。相比于 v0 可以零成本做一个完整的项目。

- 测试了一下，图片识别有点弱，我上传了界面参考图，它一点都不参考。但是速度确实快

- 这个赛道有门槛吗？感觉推陈出新太快了。

- ## 🚀 Introducing http://bolt.new, by StackBlitz _202410
- https://x.com/stackblitz/status/1841873251313844631
  - What if AI dev products (Claude, v0, etc) let you install packages, run backends & edit code?
  - Prompt, edit, run & deploy fullstack apps
  - Full dev env (npm, Vite, Next.js, …) w/ frontier AI
  - bolt․new can create beautiful, production ready multi-page apps with backends and DBs like @Supabase .
  - That's because every chat can run a prod build & deploy it to @Netlify (and @Cloudflare) — no login required

- how does bolt․new run in a browser tab without virtual machines?
  - The secret sauce is WebContainers, our micro-OS that runs a full web development environment inside your browser tab. 

- ## 🚀 [Show HN: Void - open source Cursor AI code editor | Hacker News _202409](https://news.ycombinator.com/item?id=41523197)
- [Show HN: Void, an open-source Cursor/GitHub Copilot alternative | Hacker News _202409](https://news.ycombinator.com/item?id=41563958)

- I'm Andrew, one of the creators of Void. 
  - we're building Void as a fork of vscode. The repo has great documentation for extensions, but going deeper gets pretty involved. All of the code is OOP-based, and they mount DOM nodes the old-school way (which is what React was supposed to solve..). So adding new UI features isn't exactly trivial. 
  - Microsoft also made its extension marketplace closed-source 

- As someone who has recently tried to refactor our app atop of VSCode (treating it like a platform), we got burned by the UI design decisions that are not straightforward to overcome, let alone maintain. The closed-source MS marketplace did not help either towards our OSS goals.

- I remember Atom was refactored to use manual DOM updates because the performance penalty of using React wasn't worth it. By the way, isn't OOP by far the most popular paradigm for building desktop UIs? I imagine VS Code is a difficult codebase to work with that has a lot of intricate code 
  - I have spent a great deal of time wading through the VS Code codebase and it takes OOP to the extreme. There are mile long inheritance chains, everything is a class, and it is a giant bowl of spaghetti. To some extent, I understand why they used that development approach. It doesn't use a UI framework, just DOM APIs, so classes make sense in lieu of components, but it's still bonkers.
  - My day job is desktop development (with Electron), and I avoid OOP as much as I can and try to use a functional approach. After jumping all over the VS Code codebase to try to understand how some of this stuff works, and seeing how hard it is to navigate, I think heavy OOP is a bad idea.

- Always interesting to hear such claims when graphic editors like Penpot, which have much tighter perf requirements than editors, are so fast while using React.

- ## Introducing Zed AI, in collaboration with @anthropicAI . _20240821
- https://x.com/zeddotdev/status/1825967812629631034
  - Zed AI brings LLMs directly into your editor with an extensible, text-centric approach.
  - We're also piloting @anthropicAI 's new Fast Edit mode for Claude 3.5 Sonnet with a small set of Zed users.

- ## Introducing LlamaCoder! An open source Claude Artifacts app that can generate full React apps and components with Llama 3.1 405B. 100% free and open source.
- https://x.com/nutlope/status/1819445838705578091
- https://x.com/nutlope/status/1820299682331107371
  - Just put together an architecture diagram for how LlamaCoder works!

- ## 我已经是第二 tier 的付费用户好久好久了，见人就安利 cursor。
- https://x.com/wey_gu/status/1820678802646978674
  - copilot ++ 特别快
  - block selection 之后的逐行change/apply 执行是第一个碾压的创新，非常好用
  - chat 中的灵活引用上下文是 sota 的
  - 用了 sonnet 替换 gpt-4 之后 chat 中的答案直接 apply 到代码，提升了一个台阶
  - 最近的 composer（需要开启）又推向了一个新的水平，直接跨文件改东西

- 这个功能绑定编辑器吗？
  - 是，neovim 没发用，如果原来 vscode 好一点

- ## @LangChainAI 宣布推出第一个本地的 Agent IDE - LangGraph Studio
- https://x.com/tuturetom/status/1819190219788447805
  - 基于 LangGraph Studio 在本地运行，基于代码开发 Agentic Workflow 并可视化交互运行、调试
  - 与 LangSmith 集成，追踪 Agent 运行堆栈
  - 支持 JS/Python，提供持久化层

- 大量程序员使用vim和Emacs，甚至markdown的广泛使用，已经说明高产程序员根本不需要这种可视化

- ## we are launching @wordware_ai ! Wordware is the first IDE solely focused on building your AI with Natural Language Programming
- https://x.com/kozerafilip/status/1819302298944000142
  - 👾 Having built a bunch of AI agents we realised three things:
  1. It’s prompts all the way down
  2. Making AI Apps work requires a bunch of iterations
  3. It’s much faster when the person developing the agent can judge the quality of the outputs
  - So, having spent the last ten years building in AI with my co-founder, we thought from first principles: “If prompting is the new programming, what should the tools be?”
  - The results: A user-friendly, beautiful editor that enables the user to use simple natural language to create complex AI Agents and iterate on them 20x faster than in code.

- what is the added value compared to using the chat apps for all kinds of llms?
  - We are more focused on building the flow once and then having an ability to call into it via an API
  - So it a little like you don't have to have the same conversation with the chatbot every time and you get to make the inside info on how to lead that convo into a product.

- ## 🌰 [AI Assisted Coding · vizhub-core/vzcode _202303](https://github.com/vizhub-core/vzcode/issues/73)
- First pass done in #282

- ## AI 补全工具可能只是冲击传统编程方式的第一步。 AI 设计 / AI CodeGen / AI 文档 / AI TDD / AI Lint 可能还在路上。
- https://x.com/hylarucoder/status/1791807537995747459

- ## [大语言模型加速信创软件 IDE 技术革新 _华为_QCon全球软件开发大会 _202312](https://www.infoq.cn/article/vg9loxtgp3ehdpddec49)
- 「智能化信创软件 IDE」专题，邀请到华为云开发工具和效率领域首席专家、华为软件开发生产线 CodeArts 首席技术总监王亚伟担任专题出品人
- 相比“信创”，“智能化”在过去 5 年中被业界反复提起，智能化技术的发展必然会使诸如 IDE 这样的软件开发工具更加强大。
- 随着大语言模型的诞生，IDE 除了可以自动地完成一些重复性工作之外，还可以协助开发人员在软件的设计和开发过程中完成更多创新性的工作，比如：
  - 自动化重构：将一段复杂的代码分解为更小、更易于管理的函数或类。开发者可以描述他想要实现的重构目标，然后让模型生成相应的代码
  - 代码翻译：大语言模型可以将一种编程语言的代码翻译成另一种编程语言，再配合 IDE 的语法高亮和错误检查功能，可以帮助开发者使用不熟悉的编程语言编写代码
  - 自动化文档生成和更新：大语言模型可以根据代码和注释生成相应的文档，或者在修改代码时自动更新文档。大语言模型是 IDE 的智能化加速度

- ## [AutoDev for VSCode 预览版：精准 AI 编程提示词与编辑器的完美融合 - 知乎 _20240506](https://zhuanlan.zhihu.com/p/696080970)
- 我们将 AutoDev for Intellij IDEA 平台的非凡开发者体验带到了 VSCode 平台。在 IDEA 版本中通过构建非常精准的提示词，以及与编辑器的完美融合， 以帮助开发者更好地编写代码。
- 在设计 IDEA 版本时，我们一直致力于避免使用聊天窗口，以提供更好的用户体验。在 VSCode 版本中，我们将这一理念继续发扬光大。
- 不断地重构我们的架构，以实现精准测试生成所需要的上下文件：
  - 输出准确的测试文件路径
  - 与编辑器的完美融合
  - 函数的相关代码类（输入和输出）表示
  - 基于依赖工具的测试框架分析
- 如下是基于上述的设计理念的 Prompt 示例：
  - 通过读取依赖文件，如build.gradle，我们能够准确地知道项目的依赖，以及测试框架的使用。
  - 通过对函数的上下文分析，我们能够准确地知道函数的输入和输出，以及函数的相关代码类。
  - 通过精准的上下文，可以有非常高的信心直接生成测试代码。

- 在当前的 VSCode 0.1.0 版本中，我们实现了以下的核心功能：
  - 自定义 AI 指令，即通过自定义 prompt 来实现自定义的 AI 指令。
  - 测试生成，即通过 AI 生成测试代码。
  - 注释生成，即通过 AI 生成注释。
  - 语义化搜索核心逻辑，尚未集成到功能中。

- ## [花了四个月，打造了一个满意的大模型 IDE 智能插件 - 知乎 _202308](https://zhuanlan.zhihu.com/p/648598153)
- 围绕开发者体验，设计三种辅助模式
- 自动模式：规范化的代码生成
  - 触发方式：自动模式都在 Context Actions 下，即与上下文相关的 actions。方式自然是那个那能的快捷键：⌥⏎ (macOS) 或者 Alt+Enter (Windows/Linux)。
  - 自动 CRUD。
  - 自动生成测试。
  - 自动代码补全。
- 伴随模式：围绕日常体验设计
  - 伴随模式都需要等待 LLM 返回结果，所以就都扔到 AutoDev Chat 模式下了
  - 在 JetBrains AI Assistant 出来之后，它成了 AutoDev 的最大竞争对手，当然也是参考对象。
- 聊天模式：一个边缘的功能
- AutoDev 的思想是将 LLM（Large Language Model）作为辅助开发者的 Copilot，通过提供辅助工具来解决一些繁琐的任务，让工程师能够更专注于有创造性的设计和思考。

# discuss-coding-ai
- ## 

- ## 

- ## 

- ## 现在各种编程的Vibe CLI多到程序和程序员都不够了。我列下，还来不及进行ranking。 _202510
- https://x.com/mranti/status/1981381099889840358
  - 1）CC系的：Claude、Deepseek、GLM（包月）、Kimi、KAT-coder（限免）；
  - 2）Codex
  - 3）Gemini系的：Gemini、Qwen Code（限免）、iflow（限免）、Qodercli（限免）、Cursor-Agent。
- 不同的开源方法啊，CC是开放了大模型接口，大家都可以接入。Gemini是开源了整个框架，所以大家都学了。

- 你漏了：Droid、AmpCode、Opencode

- 本质上还是自己用的舒服的，然后对自己学习和工作效率提升最高的就行，没啥必要太关注ranking，如果觉得他们做的不好也可以自己手搓一个，对context engineering有更加深入的理解
  - 数千个meta prompt, 自己手搓不太现实吧。再说，个人没有那么多数据和资源进行系统测试。
- 是的是的，但是大致构建一个类似的会对coding agent有更好地理解，会去更好地使用，光看anthropic或者其他blog不去做就有点虚空索敌的感觉

- Cli开发其实不是特别适合开发者，调用工具和上下文累计消耗的token太快，不如按次计费的ai ide，Claude code我放弃了可能是因为成本，即使是接入glm4.6到cc也不能是长期之举，写代码一天消耗个几百万token，成本都快超过6美元

- GitHub Copilot CLI 算哪一系？
  - 简单试了下copilot cli，工具本身少了cc经常用的plan mode，还有checkpoint对代码或聊天的回滚，好像也没有多chat session的管理，没有安全感。cc更新太勤快了又有先发优势，目前感觉其他家还抄不过来
- CC 的 checkpoint 实在太好用了。Session 的支持好像在计划中了。

- ## [ValTown - What we learned copying all the best code assistants _202501](https://blog.val.town/blog/fast-follow)
- Looking back over 2024, our efforts have mostly been a series of fast-follows, copying the innovation of others.
  - This article is a historical account of our efforts, giving credit where it is due.
- it still feels like there’s a lot to be gained with a fully-integrated web AI code editor experience in Val Town – even if we can only get 80% of the features that the big dogs have, and a couple months later. It doesn’t take that much work to copy the best features we see in other tools. The benefits to a fully integrated experience seems well worth that cost. In short, we’ve had a lot of success fast-following so far, and think it’s worth continuing to do so.

- ## 🚀 Augment Code: We spent the past few months building a production-grade AI coding agent from scratch. _202504
- https://x.com/augmentcode/status/1915049816268366268 
  - we learned what actually matters—and open-sourced the whole stack.

- We built the agent to handle real codebase tasks end-to-end:
  - Navigate a repo
  - Reproduce a bug
  - Plan a fix
  - Edit source files
  - Validate with tests
  - Stay within scope

- The architecture is clean:
  - Docker-based runs
  - Planning, file-editing, and bash tools
  - Optimized prompts
  - Simple majority-vote ensembling
- We forked and extended the best ideas from Anthropic’s SWE-bench blog post.

- We didn’t use our own fine-tuned models for this run. The goal was to create a strong, open baseline that others could build on, test against, or tweak. The agent is fast, reproducible, and easy to run.
- If you're working on agents—or just exploring what’s possible—we open-sourced everything
  - https://github.com/augmentcode/augment-swebench-agent

- ## 🎯 Introducing Devin 2.0: a new agent-native IDE experience. _20250404
- https://x.com/cognition_labs/status/1907836719061451067
  - Spin up parallel Devins to take on multiple tasks at once. Each Devin works autonomously and you can jump in any time on the details that need your expertise.
  - Devin creates detailed architecture diagrams, links to sources, documentation, and more for all your repos in Devin Wiki.

- ## ai辅助编程， 经历过几乎所有的工具之后， 我最终确认的顶级配置：
- https://x.com/BadUncleX/status/1900394535408304207
  - aider architect (r1 + sonnet 3.5)
  - warp console (enable ai) 
  - 辅助:  cline (plan/act模式, r1 + sonnet 3.5) 
  - 结论： 单模型， 即使是sonnet 3.7也没法和组合模型打。上面方案接近完美，性价比几乎最高。 agent华而不实.

- 还有一个包月的方案， 还没有验证， 先记录一下，就是不使用api, 改用claude 订阅。 
  - 1. 使用claude desktop，集成mcp， 访问本地项目代码。 
  - 2. 使用ClaudeSync将本地文件同步到claude projects. 
  - MCP现阶段使用似乎是比较容易超出上下文长度， 但仍然值得关注。

- ## 发布 Devv Playground：智能代码生成的利器
- https://x.com/forrestzh_/status/1846451160678650338
  • 实时预览：Devv 理解您的需求，即时生成并展示代码。
  • 边聊边编程：聊天窗旁的 Playground 让搜索和代码更新无缝衔接。
  • 即用即得：生成的代码完整独立，可直接应用到项目中。
  • GitHub 模式加持：结合最新代码库，极大提升开源项目的开发效率。
  • 准确可靠：依托最新、最精准的信息，确保代码质量。
  - Playground 为开发者打造了一个高效、直观的编程环境，让复杂的编码过程变得轻松愉快。
  - 生成代码后即时运行，目前已支持前端代码 & Python。
  - 直接基于 GitHub Repo 来修改 & 生成代码

- ## 🚀 Github Copilot Chat for Repo 全面开放，免费使用
- https://x.com/tuturetom/status/1843648749324865879
  - 对任意 Github 仓库进行语义提问，全局可用，动动嘴就能学习项目源码的时代正式到来
  - https://github.com/copilot

- ## [What's the different between replit agent which is just released and cursor? : r/replit _202409](https://www.reddit.com/r/replit/comments/1fabsow/whats_the_different_between_replit_agent_which_is/)
- ReplitAgents is a MVP builder. Don't expect any sophisticated from it

- Replit agents seem to be limited to a few technologies - Python, Flask, vanilla JavaScript, Postgres, etc. in the Flask ecosystem. It can quickly stub app ideas out, but isn't advanced enough to do complex apps so far. 
  - Cursor doesn't try to act as a full agent, but gives AI tools to move quickly in the development process.

- Replit Agent stops working after 20 minutes. I assume that is the main difference.

- ## Could Replit Agent potentially 30x Replit's market size? 
- https://x.com/taratan/status/1832102411856703795
  - It's idea-to-deployment in minutes. While still buggy at the moment (my app was caught in a pesky OAuth error that it couldn't get out of ), it points to a world where Replit’s customers grow beyond developers (20M today) into truly, anyone with an idea. 
  - This positions Replit closer to a Canva (general public) with 185M users versus a Figma (professional/ semi-professional) with 4M users.
  - As @lennysan notes, Canva generates more revenue than Figma, Miro, and Webflow combined.
  - There has been a number of new players in the battle for AI code generation — like Copilot, Codeium, Claude, Cursor AI. 
  - But Replit has a unique insight that gives them an edge: a great user experience. Experience might just be the differentiator that gives them the winning edge.
- Replit has the potential to become a "Canva for coding" by lowering the barrier to entry for non-developers who have ideas but lack the technical skills to execute them. Much like Canva did for design, Replit can simplify the creation process for apps, offering intuitive tools

- i am pretty sure @github copilot will have something similar once this catches on. @Replit needs to ship and ship fast.

- We all have seen this movie before. It goes no where because AI agents don’t work. The moment you leave the “getting started” project it blows in your face. We need at least 2 more generations of AI models with more comprehensive coding capabilities to make it work as promised.

- ## 🚀 Announcing Replit Agent in early access—available today for subscribers _20240906
- https://x.com/amasad/status/1831730911685308857
  - AI is incredible at writing code. But that's not enough to create software. You need to set up a dev environment, install packages, configure DB, and, if lucky, deploy. It's time to automate all this.
  - idea to software all on your phone
  - Replit clone w/ Agent

- Aider in Replit is still super useful as they serve slightly different use cases.

- ## after using replit's coding agent i think...its over for a lot of traditional saas
- https://x.com/SullyOmarr/status/1832102375257178290
  - wanted slack notifications when customers subscribed/cancelled, Zapier was 30/mo JUST to add a price filter
  - instead replit's agent built & deployed one in < 5 mins, with tests. 1/10 of the cost
- their Agent is only available for the same $20 ($30 CAD)/mo

- Yep, software or SaaS is race to the bottom. There is going to lots of new software that will be built. I doubt we will ever get to 8B people building their own software, but in a decade  20-30M people will be building it. Relevant comment from another discussion.
  - similiar to youtube probably

- I think you forget that most businesses don’t want to go and build their own things. They just want to grab something off the shelf and move on with their core product
- It’s over for no code

- Yes can you even build a software moat anymore?
  - data moat tbh

- fine for toys, but when it gets confused or does bad things you have to fix it

- replit only for multiplay like Google docs for code. Toy usage for me and pair programming

- The average Zapier user has no clue how to code nor prompt. That’s why Zapier exists
  - Would you recommend Replit's tech over Zapier for automation?

- ## devv.ai 的 GitHub Mode 已经支持前端仓库了。 _202406
- https://x.com/forrestzh_/status/1802871846871920676
  - 效果是，在搜索引擎的界面直接解释代码的实现逻辑，并提供文件路径
- 请问有没有支持CPP/Rust仓库的计划？
  - in the progress
- 请问有没有支持同时多个仓库的计划？

- ## 🎯 Devin 2.0 _20240504
- https://x.com/itsandrewgao/status/1786613503471829485
  - Launch Interactive mode to help Devin navigate the web. Really useful if it gets stuck on something like a CAPTCHA.
  - One of my biggest gripes with Devin was not being able to intervene and edit code. You can now do so by launching a web VSCode.
  - Another super exciting update is Cookies which enables Devin to log in to websites for your account **without needing to give Devin your password**.
  - Machine snapshots let you save the state of Devin so when the server shuts down, you can start up again

- ## 👾 [Replit's new Code LLM: Open Source, 77% smaller than Codex, trained in 1 week | Hacker News _202305](https://news.ycombinator.com/item?id=35803435)
- thank you for open sourcing this! It's a real gift to the community to have a model intended for "commercial use" that's actually licensed as such.

- The model is way too small, comparing it to Codex feels disingenous. Sure it's 77% smaller, it's also 77% worse. Although, it's a cool project nonetheless.

- my favorite learning is how they are pushing the state of the art - openai’s HumanEval is the industry standard benchmark for code LLMs, but Reza kindly went above and beyond to show how they use “AmjadEval” - using coder intuition to capture human preference on what output is more helpful to coders

- No Clojure. No Julia. No Haskell. No Racket. No Scheme. No Common Lisp. No OCaml. And, as much as I despise Microsoft, No C#. No F#. No Swift. No Objective-C. No Perl. No Datalog. A glaringly lacking choice of languages.
  - I hate to admit, but Python, C, Java, and JS cover most of the modern programming. But not supporting C# sounds like a bad idea.

- ## [AI -> Code 一些产品体验 - 知乎](https://zhuanlan.zhihu.com/p/695066426)

- [AI*Lowcode 的一些结合场景 - 知乎 _202309](https://zhuanlan.zhihu.com/p/658219081)

- ## [如何利用AI工具提高程序员的编码效率？ - 知乎](https://www.zhihu.com/question/645556922)
- 推荐三个开源的AI编程工具：Devika、Open-Devin和SWE Agent。它们不仅仅是代码的生成者，更是软件工程领域的创新者。

-
-
-

- ## [面向程序员的编程大模型AI | 微言码道 _202403](https://taoofcoding.tech/blogs/2024-03-10/the-code-ai-for-develope)
- Github Copilot是一个由微软, Github以及OpenAI合作开发的专门面向编程的AI工具.
  - Github Copilot的核心功能包括:
  - 代码补全: 根据上下文及你的要求, 补全代码
  - 生成代码片段: 帮你生成测试代码或文档注释等
  - 代码检查: 帮助你检查你的代码的问题
  - 帮助你做代码风格检查, 代码重构, 调试等
- 阿里有自己的大模型通义千问, 甚至还开源了QWen大模型. 做为国内前沿的科技公司, 阿里也推出了通义灵码, 也就是类似Github Copilot的AI工具.
  - 通义灵码针对个人免费
- CodeWhisperer Amazon出品的编程AI工具. 对个人免费
  - 更针对Amazon 云服务有关的编程, 如果你编程主要是使用的Amazon的各种云服务或SDK, 那CodeWhisperer是你约会的AI助手

- CodeLlama 70B是700亿参数, 对GPU内存的要求非常高, 这个硬件要求, 一般人或公司整不起.
  - 如果真想部署一个本地的编程大模型, 可能starCoder2是更具可行性的选择. starcoder2的bigcode训练的开源大模型
# discuss-ai-lowcode
- ##

- ##

- ## 体验了 http://Wegic.ai 的AI建站，UI设计和交互都很惊艳、简洁，整体流程丝滑，很不错的解决了多数低代码、模板库给用户带来的选择困难症、部署困难。
- https://x.com/zQwQs/status/1793216048759754879
  - 看实现像是预定义了少量的组件(可替换文本/图片/动画容器等)，然后让AI生成页面区块，写React组件(Hero/Gallery等)和props，用AI对话去编辑
  - 基于这个想法，使用 gpt-4o + tailwind + Vue + esbuild-wasm 做了个「网页生成器」，还有按区块调整的能力。。 属于是低配山寨版 wegic 了（纯做着玩儿的PoC
  - 还有一个告诉ai接口，然后自动写页面的

# discuss-codebase-search/rag
- ## 

- ## 

- ## 
# discuss-debug
- ## 

- ## 

- ## 

- ## [Launch HN: Patchwork (YC S24) – Automatically add structured logs to your code | Hacker News _202408](https://news.ycombinator.com/item?id=41391931)
  - Big picture: we are building a next generation logging and observability platform which gives engineers the rich debugging context they need.

- On the topic of structured logs, can anyone point me towards where I might learn more about what people have learned over time? I'm new to the world of querying through my logs, but I can already see a benefit to logging with JSON...
  - Structured/JSON saves a tonne of time building regex parsers. The regex parsing at query-time is also pretty expensive. This is where Splunk excels - dealing with the noise with powerful querying. ClickHouse is also very performant at this, we hear. It's an expensive task though (computationally and cost wise)
  - Charity, CTO of Honeycomb has strong views (which we enjoy a lot): https://charity.wtf/tag/observability-2-0/ - they come at it from a tracing/OT angle which is Honeycomb's forte, but we agree a lot on the intended outcomes - actionable (not spammy/noisy) + make it easy to gather the variable/state context in the context of a single event.

- OneUptime.com already does it with the copilot feature. It also fixes exceptions, add structured logs, optimizes functions / spans that take a long time to complete and integrates with OpenTelemetry natively. It's also 100% open-source.
# discuss-pm-ai-devops
- ## 

- ## 

- ## 软件开发的矛盾，已经从 “写代码费时费力”, 转换成了 “海量高质量代码，跑得通 且有一点小问题，但很难 review 和修改”
- https://x.com/real_kai42/status/2017066919464227263
  - 我觉得下一代 IDE (或许就不是 IDE 形态)，应该是一个更好的促进人和 agent 的协作的形态，如何让人类 review 海量代码，并且有信心的去交付 Agent 的产出，这个形态肯定不是 CLI。

- IDE 是给“写代码”的人准备的。 Agent 时代的交互核心绝不是帮助人类更快地 “Review 代码”，而是建立一套自动化 “Verify 结果” 的机制。 如果你还在试图逐行 Review AI 生成的海量代码，那说明你的工作流还在石器时代。未来的程序员不是主编，而是写 Test Case 的 QA 和定义目标的产品经理。

- 有种感觉：以前写代码像亲手做饭，现在像验收外卖

- 我觉得不止是代码，现在有点信息爆炸了，我看一个报告的信息量处理，不低于以前看一本教材，尤其是不熟悉的领域，基本都要丢给 ai 和我一起看

- 

- 不不

软件开发的矛盾

从机器码时代开始就是：
跑得通 且有一点小问题，但很难 review 和修改

无非以前的问题，后来靠
汇编
高级语言
软件工程
IDE 智能提示，语言服务
CI/CD
AI

逐渐缓解，但是从来没有解决本质问题

核心是人不应该review代码
这是绝对错误的事情

- ## cursor 有没有可能让我在等待AI生成的时候，强制看广告，让我来赚钱token？
- https://x.com/yihui_indie/status/1902958928142667805
  - 1. 付费会员免广告 
  - 2. 普通用户看广告
- 看 60 秒广告可以免费使用 thinking 一次, 需要看 10 个广告集齐 sonnet max 才能抽卡一次 SSR 代码。
- 广告就太 low 了，等待时间可能会让你做图片识别来训练AI用，以换取 token

- 广告就太 low 了，等待时间可能会让你做图片识别来训练AI用，以换取 token

- 首行代码免广告，每一个人通过你的邀请码加入，你每次看广告时间缩短0.01秒
# discuss-code-review
- ## 

- ## 

- ## 

- ## [How do you balance AI and human review in PR workflows? : r/codereview _202602](https://www.reddit.com/r/codereview/comments/1ra6q2e/how_do_you_balance_ai_and_human_review_in_pr/)
  - we’ve been using an AI code review tool for a cpuple of months now. It works fine, but we’ve been running into some issues like, noisy comments, missing context and suggestions that are technically correct but miss the bigger picture.
- We have copilot reviews turned on by default. It cannot approve code but it runs on a different model and different harness to the ones we’re used in code gen so it’s still likely to pick up stuff we or the coding agents missed. Copilot cannot see or respond to your comments on its comments. It’s really just flagging stuff for you and the human reviewer(s) to consider.
  - Agents cannot approve PRs. We’re a pretty ai forward company but I don’t see that changing. Ultimately we’re still responsible for the ai assisted code that we commit, approve, or merge.

- ## [change my mind: automated code review tools are better than human code review in 70% of cases : r/ExperiencedDevs _202601](https://www.reddit.com/r/ExperiencedDevs/comments/1q525yn/change_my_mind_automated_code_review_tools_are/)
  - Most PRs are just checking for: syntax issues, naming conventions, obvious bugs, test coverage, security vulnerabilities, code style consistency. stuff a machine does in seconds.

- I don't review code that doesn't pass the linter check, so I see what you are talking about but I see that as an already solved problem.
  - And if I disagree on the code style? Well that's another issue that is best discussed outside of code review, so again it doesn't slow me down.
  - And, I'll go even further: on the last 30% that matter, I tend to think that design shouldn't be a point of contention in a review, as it should be decided before the code is even produced.

- You are missing the part that all the stuff you said are part of CI pipelines and do not compete at all with what a human should do when reviewing code. The only controversial part of your take are your arbitrary percentages.

- I’ve been seeing AI code reviews as a “good first pass” instead of a replacement for human eyes. It can catch all the stupid things so I can focus on more structural issues

- The real problem with automated code review is false precision.
  - Static analyzers + diff-aware checks & system-level reviewers (we’ve used CodeQL, Danger, and Kavia in different setups) work best when they frame uncertainty instead of pretending to be a senior engineer.

- ## [Here are the AI code review tools I've been looking at, which one is best? : r/webdev _202602](https://www.reddit.com/r/webdev/comments/1quz7wh/here_are_the_ai_code_review_tools_ive_been/)
- we use coderabbit at work, it's fine but very noisy, you'll spend time configuring what rules to turn off

- tried greptile for a few months, good for understanding codebase but the review comments were kinda generic

- ## 🎯 [Qodo Launches Version 2.0 with Top Accuracy in AI Code Reviews : r/aicuriosity _202602](https://www.reddit.com/r/aicuriosity/comments/1qvpxp9/qodo_launches_version_20_with_top_accuracy_in_ai/)
  - The biggest highlight comes from their own testing. On a set of 580 real bugs injected into 100 pull requests from live open-source projects, Qodo 2.0 reached a 60.1% F1 score. That beats the next closest competitor by 9 percentage points.
  - Qodo 2.0 moves away from a single general-purpose reviewer. Instead it uses several focused specialist agents that handle different jobs: Spotting critical bugs Finding duplicated code Detecting changes that could break things Enforcing custom coding rules Checking alignment with ticket requirements
  - Each agent pulls in the full repository plus pull request history so suggestions stay relevant and cut through the clutter.

- ## [Anyone using Qodo for diff-aware code reviews across? : r/codereview _202510](https://www.reddit.com/r/codereview/comments/1oey60f/anyone_using_qodo_for_diffaware_code_reviews/)
- at my work we have an absolute monster of a legacy codebase. AI review tools don't seem to grasp our in-house tools or libraries. It does make some suggestions to use standard C++ libraries, but can't seem to figure out that it should be using our in house custom std functions.
  - It's kind of like an eager junior. Being wrong with incredible speed.

- we're in a similar stage of exploration. we're a relatively small codebase, mostly python. I'm thinking we can leverage gitlab mcp to perform ai generated coode reviews using bedrock models and maintain context files for each repository. 

- I used Qodo for a while. It’s clean and has good diff visualization but our workflow needed tighter repo integration so we eventually switched. Right now we’re using CodeRabbit. It automatically reviews PRs with context from previous commits and project structure. It's able to spot subtle inconsistencies before they make it to testing.

- What helped our team was treating AI as another reviewer rather than a replacement. Static checks and tests still run in CI, then Qodo reviews each PR with repo context, posts a short summary, and highlights a few higher‑risk issues instead of commenting on every line. That kept review quality the same while cutting the time we spend on obvious problems

- ## [Anyone here using Qodo for AI-powered code reviews? : r/codereview _202508](https://www.reddit.com/r/codereview/comments/1mi0z28/anyone_here_using_qodo_for_aipowered_code_reviews/)
  - We’ve been using Qodo to automate the first pass of PRs it pulls in Jira context, past PRs, and even flags missing tests or edge cases.

- What I like most is that it doesn’t just look at the code in isolation it actually pulls in context from Jira tickets, past PRs, surrounding files, and even test coverage. So it’s not just “hey, this is poorly written, ” but more like “this logic doesn’t match what you did in a similar PR two weeks ago” or “you added new logic here but didn’t write tests for this branch.” Feels more like a thoughtful dev doing a first review than just an LLM copy editor.
  - The agent stuff is cool too. We’ve got it set up so one agent helps while writing code (suggests missing tests, highlights edge cases), and another one kicks in during PRs - adds inline comments, flags things that might break conventions, that kind of thing. And we’ve been able to add some custom rules, like blocking PRs if new logic doesn’t have test coverage or if it’s not linked to a Jira ticket.
  - Tried Copilot and CodeRabbit before, but Qodo feels more team-aware and opinionated in a good way. Curious how others are setting it up too - are you just using the default flows or customizing it a bit?

- yup been running Qodo in our workflow for a bit. the jira + past pr context is huge, makes the comments feel way less generic. what i like most tho is how it ties review with test gen, so if it flags a gap it can spin up a starter test right there. feels more like an extra teammate than just a lint bot.

- ## [What's the best AI code review tool? : r/codereview _202512](https://www.reddit.com/r/codereview/comments/1pqgmv4/whats_the_best_ai_code_review_tool/)
- Here are my top 5:
  - Graphite
  - Bito's AI Code Review Agent
  - GitHub Copilot
  - Seer (by Sentry)
  - CodeRabbit
  - My next project is to create a fresh 2026 benchmarking report of the best AI code review tools. I'm planning to add Greptile, Qodo, and Bugbot to the list.

- Graphite has been acquired by Cursor a few days ago I think. However, since I'm working with the Kilo Code team on some tasks, I use Kilo Code Review. 

- We ended up valuing low noise more than anything else. Static checks stay in CI, and Qodo joins as an extra reviewer on each PR, reading related files and history, then leaving a short summary and a few higher‑risk comments. That has been easier to work with than tools that add many tiny remarks.

- ## [Best AI code review tools in your experience? : r/AskProgramming _202511](https://www.reddit.com/r/AskProgramming/comments/1p1cymk/best_ai_code_review_tools_in_your_experience/)
- What I’ve seen is that different AI reviewers target different layers.
  - Snyk Code focuses on vulnerability detection and static analysis. OTOH Qodo Merge and CodeRabbit analyze flow and semantics.
  - For me personally, I’d take CodeRabbit since it’s really unique in its approach when it comes to function-level context, and it doesn’t really work with token windows which is a good thing. That’s why it catches side-effects or mismatched logic where others fail. Of course, latency and cost aren’t as economical once you scale it to big repos.
- Yeah, that’s pretty much what we ran into too. Once the repo gets big enough, token limits start chopping context like crazy. CodeRabbit’s function-level parsing fixes most of that. It seems to be really good at holding the thread between files, even across services where Bito or Qodo Merge just blank out, you know? 
  - We dropped it into our CI pipeline one late night and the first flag it threw was a mismatched type conversion. Pandas join against a NumPy array. No one caught it during manual review, which was a bit humbling. 
- We did a controlled rollout on one of our ETL repos, and CodeRabbit flagged a subtle leak between two Airflow DAGs that would’ve broken downstream transformations. None of our static tools caught it.

- We ran a 3-month evaluation across our dev squads last year. Our team tried Bito, Qodo Merge, DeepCode, and CodeRabbit, but the one that stayed was CodeRabbit, mostly because it handled large diffs without crashing and gave context-aware suggestions instead of just restating variable names.
  - Code review backlog dropped by around 25% after we added automated pre-checks from Rabbit. It doesn’t replace humans, that would take some time, but it triages things fast.
  - Qodo Merge was good too, but it required more setup and struggled when multiple branches touched the same dependency.

- in my experience, the best tools are the ones teams keep enabled long term. That usually means fewer comments, better context, and learning from past reviews. Qodo’s been one of the few that didn’t get muted after a few weeks because its feedback stayed relevant

- ## 📌 [AI code review tools : r/AI_Agents _202510](https://www.reddit.com/r/AI_Agents/comments/1og3vjm/ai_code_review_tools/)
- [State of AI Code Review Tools in 2025 _202510](https://www.devtoolsacademy.com/blog/state-of-ai-code-review-tools-2025/)
  - CLI Based Reviewers: CodeRabbit
  - IDE Native Reviewers (In-Editor Assistants)
  - PR-Based Review Bots (GitHub/GitLab Integrations): CodeRabbit, Greptile, Graphite, Qodo Merge
  - Hybrid & Security-Focused Review Platforms: DeepCode, CodePeer, HackerOne
  - Open-Source and Community-Driven Reviewers: 

- We went down a similar path, building a simple diff reviewer with an LLM. It's surprisingly effective for catching low-hanging fruit and enforcing basic style.
  - The main difference we found with paid tools isn't always the core AI suggestion on a single line of code. It's everything around it. The paid tools are usually much better at understanding the full repository context, not just the diff, so they can catch more complex bugs that span multiple files.
  - A lot of them also bundle in security scanning which is a huge value-add and a pain to build and maintain yourself. Plus, the workflow integration is just smoother managing suggestions, dismissing false positives, and having a UI that isn't another thing your team has to build.
  - Your custom tool is probably great for your very specific, in-house rules. Might be worth running a trial of a paid tool on one repo to see if the security and whole-repo context features catch things yours doesn't.

- im not sure if you meant qodo or a different tool. Most feel the same until you add repo memory. For code quality, Qodo stood out by pulling history and related files, then proposing focused fixes. it reduces reviewer fatigue on larger changes.

- The main advantage of something like qudo or polarity is they're built specifically for this so they handle edge cases better and have context understanding that goes beyond just diff analysis. Like they track patterns across your entire codebase and learn from your team's feedback over time which is hard to replicate in a homegrown tool without significant investment We started with smth similar to what you built but at the end switched to polarity bc maintaining our internal tool became its own project and the accuracy just wasn't there for more complex logic issues. The paid tools also integrate better with workflows and dont require constant tweaking when your stack changes or gitlab updates their api or whatever. 

- Paid tools like Qudo often come with advanced features such as:
  - Comprehensive analysis of coding standards and best practices.
  - Integration with various CI/CD pipelines and project management tools.
  - Continuous updates and support from the vendor.
- Custom solutions, like the one you've developed, can be tailored specifically to your team's workflow and coding standards, which might provide a more personalized experience.

- most of the value comes from how much context the tool has. Diff only reviews don’t add much. Tools that understand repo structure and patterns feel more useful long term. That’s why I’ve kept Qodo in the workflow, since its feedback stays relevant instead of noisy

- ## [any self hostable alternatives for code rabbit?? : r/devops _202510](https://www.reddit.com/r/devops/comments/1oheri0/any_self_hostable_alternatives_for_code_rabbit/)
- Not advisable unless your team can handle constant maintenance and model updates. Coderabbit is optimized for reliability across repos and languages which is hard to replicate. Even with startup credits, you’d likely spend more time managing infrastructure than getting reviews. Keeping Coderabbit is the safer long-term choice.

- I am not aware of any self hosted free alternative and I am looking to incorporate code rabbit as well but I do want to say if you’re doing this, you’re probably doing many other things where you’re trying to cut corners for cost.
  - You’re ignoring the cost of your development and DevOps team’s time. Eventually, you’ll be spending more on dev time keeping up these services than just paying the $40/mo/dev keeping it up.

- it will be headache for your team to manage those services. As team we should focus on what is primary domain to deliver. Any engineering can self host any solutions but that will unnecessarily defocusing on primary goal. I will prefer to use coderabbit solutions directly and if cost is concern can use initially for free tier or VS Code extension.

- CodeRabbit also has a self-hosted version. You get a container image from them that you can run wherever you want but of course it will still need a CodeRabbit license.

- ## [Looking for a Free/Open Source AI Code Review Tool – Suggestions? : r/developersIndia _202507](https://www.reddit.com/r/developersIndia/comments/1lrrsvl/looking_for_a_freeopen_source_ai_code_review_tool/)
- for FOSS, try CodeRabbit OSS tier, Review Bot, or self-hosted options like SonarQube plus Semgrep rules. if you want a one-click repo report, most “free” tools cap usage. 
  - Qodo also has some open source components and a free plan for small teams and does PR reviews with summaries and test suggestions

# discuss
- ## 

- ## 

- ## 

- ## 
