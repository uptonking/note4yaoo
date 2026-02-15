---
title: lib-aikit-claude-code-community
tags: [claude-code, community]
created: 2025-12-18T12:25:39.540Z
modified: 2025-12-18T12:26:08.445Z
---

# lib-aikit-claude-code-community

# guide

# 📌 claude-code-xp
- claude-code-cli 使用ollama本地模型时，可能提示 
  - "qwen3-vl:4b-instruct" does not support thinking
  - think value "high" is not supported for this model "qwen3-vl:4b"
  - 💡 使用gpt-oss-20b就无问题, 实测ollama/lmstudio的gpt-oss-20b都支持

- 不必启用opus mode, 似乎opus-mode不会使用haiku模型，
  - 可在gateway将sonnet映射到opus，这样sonnet+haiku实际就是opus+haiku

- expore agents的 Levitating 可能花费时间较长， 可能等2min以上才有token响应返回

- 
- 

# discuss-stars
- ## 

- ## 

- ## 🧩 [CC环境变量 搞点简单记录 _202601](https://linux.do/t/topic/1513988)
- CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC
- CLAUDE_CODE_ATTRIBUTION_HEADER
- CLAUDE_CODE_PROXY_RESOLVES_HOSTS
  - 启用就是 把 DNS 解析交给代理服务器去做, 这个对于 WebFetch 还有 WebSearch 应该会很有帮助
- CLAUDE_CODE_BLOCKING_LIMIT_OVERRIDE
- CLAUDE_CODE_SKIP_PROMPT_HISTORY
  - 多开导致概率飙升
- CLAUDE_AUTOCOMPACT_PCT_OVERRIDE=57
  - 强制覆盖在 ( 128000 - 13000 ) / 200000 = 57.5% 处触发自动压缩
  - 相较于硬编码的 200k 使得在 115k 的时候就触发压缩了 满足你的需求
- DISABLE_INSTALLATION_CHECKS

- ## [Claude Code真假鉴别工具 _202601](https://linux.do/t/topic/1471272)
  - 做了个claude code测试真假的小工具，目前测试aws, crs框架的max号池皆可满分通过，kiro, cursor等逆向得分较低
  - [Claude Code 真伪鉴别](https://cctest.blueshirtmap.com/)
- 老哥你这个要粘贴APIKEY, 我怕你把我的apikey拿走了… 不敢用呀. 如果是本地部署的会好点.
  - key用完就可以删了，这个倒是没什么问题

- 虽然不知道是不是真的有用，但是我希望看到各大富可敌国的用户放出你们的评分截图

- 应该还有一个路子可以测试，kiro 是不能完全支持所有 tools 的，比如 json，read_page 这些，我之前kiro转的调这些工具都会报错但也能模仿出来
# discuss-roadmap
- ## 

- ## 

- ## [Petition: Claude Code should support AGENTS.md : r/ClaudeCode _202601](https://www.reddit.com/r/ClaudeCode/comments/1q3q8x6/petition_claude_code_should_support_agentsmd/)
  - [Feature Request: Support AGENTS.md _202508](https://github.com/anthropics/claude-code/issues/6235)
- Add a CLAUDE.md file with only one line `@AGENTS.md` . works perfectly.
- I just symlink a Claude.md to the agents.md. Easy.
  - create symbolic link CLAUDE.md that refers to AGENTS.md using ln command.

# discuss-news
- ## 

- ## 

- ## 
# discuss-tips/xp
- ## 

- ## 

- ## when i set up claude code with  https://github.com/upstash/context7 mcp, what's the differences for setup below ?
- `claude mcp add --scope user context7 -- npx -y @upstash/context7-mcp --api-key YOUR_API_KEY` .
  - Flow: Claude ↔ Local Process ↔ Context7 API.
  - This tells claude to run the @upstash/context7-mcp package locally (via npx) and communicate with that process over `stdio` (the CLI spawns the package and talks to it). 
  - The MCP server code downloads and runs locally on your machine using Node.js.
  - The local process still calls Context7's cloud API, but the MCP channel is local

- `claude mcp add --scope user --header "CONTEXT7_API_KEY: YOUR_API_KEY" --transport http context7 https://mcp.context7.com/mcp` ?
  - Flow: Claude ↔ Remote Server ↔ Context7 API.
  - This configures a remote MCP and tells Claude to call https://mcp.context7.com/mcp over HTTP(S). 
  - The `--header` option instructs Claude to include that header on each request

- ## when adding mcp to claude like `claude mcp add --transport http notion https://mcp.notion.com/mcp` , what's difference between `--scope user/project/local` ? where is the configuration file for each?
- `--scope local` (default) — private to you for the current project. 
  - Stored inside your user config file `~/.claude.json` under an entry keyed by the project path. Use this for personal/dev setups or secrets.
  - For experimental configurations, sensitive credentials, personal development servers

- `--scope project` — shared with the team: written to a `.mcp.json` file at the project root (intended to be checked into VCS). 
  - Claude will prompt other users to approve project-scoped servers before use.
  - For team-shared servers, project-specific tools, or services required for collaboration

- `--scope user` — user-wide (available across all projects on that machine). 
  - Stored in your user config (`~/.claude.json`, in the `mcpServers` area). 
  - For personal utilities, development tools, or frequently used services across multiple projects

- Precedence: if the same server name exists in multiple scopes, Claude resolves conflicts with local → project → user (local wins).

- ## [经过 8 个月 Claude Code 高强度实战，我们决定开源内部的最佳实践 _202601](https://linux.do/t/topic/1539636)
  - 我们正式发布了 Trellis
  - 从 8 个月前 Claude Code 发布开始，我们就在尝试各种开发流程：从最早的 OpenSpec，到前段时间爆火的 plan-with-files，再到最近霸榜 trending 的 Superpowers，我们都有过使用，但可惜结果都是初看很惊艳，但实际效果很一般
  - OpenSpec 类框架：本质上是 PRD-driven，而不是 Spec-driven。 每次新任务都要重新写一遍架构约束、代码风格、错误处理规则。
  - Superpowers 类框架：开源的 skill 都是比较宽泛的，没法解决项目内各种特化的问题，但是即使我们定义了自己的项目规范 skill，有时也因为幻觉或者上下文过长而没有调用，这带来了不可预测性。最后大部分时候 skill 必须手动使用，使用体感很差。
  - 我们认为在未来的 AI Framework 里，Spec 和 Skill 必须同时存在： Spec 负责约束：确保 AI 始终遵循项目规范，提供可预测性; Skill 负责能力：按需扩展 AI 的能力边界，保持灵活性
  - 解决了这两个问题，才能真正提升 AI 的代码质量，再配合上自动上下文注入之后，并行调用、团队协作等能力也就成为可能了。
  - 我们给 Spec 加上了分层和索引机制，这样它就拥有了 Skill 的渐进式披露，在节省上下文的同时也确保永远不会遗失关键 context；
  - 我们用脚本整合了一套自动注入上下文的 Skill 工作流，让你每次对话都能自动完成一套规范的工作流，而不需要手动调用一堆 command；
  - 我们加上了更强的 Todo 管理系统，结合 json 和 md 文档，让它在有丰富的 prd 的同时，有了优先级、能关联工程师、关联 branch&worktree
  - 最后我们结合上述功能并加上了 multi-agent && multi-session 功能，这样你的 AI 可以判断 Task 复杂度，自行开启一个或多个 worktree 开发任务甚至直接 PR
  - 这套系统的玩法还非常多，比如 task 系统和任务管理系统比如 Linear 的双向同步；比如自动多模型 Review PR；甚至像 ClawdBot（现在叫 MoltBot 了） 一样嵌入到 Slack、discord 等任何地方…
  - 最重要的是，没有学习成本：只需三行命令完成初始化，之后像平常一样用 Claude Code 就好了。(因为所有的复杂逻辑我们都已经原生做在了框架内部)
  - 我们这几天会把我们用 Trellis 自建 Open Typeless 的完整流程也发在论坛（如果你不知道 Typeless，你可以理解为豆包语音输入法）

- ## Error from Kiro API: 400 - {"message":"Improperly formed request.", "reason":null}
  - [Add support for Cline · Issue #7 · jwadow/kiro-gateway](https://github.com/jwadow/kiro-gateway/issues/7)
  - Fixed it - Cline was sending some tool schemas that Kiro didn't like

- [【WONG公益站】修复thinking引起的500问题 ](https://linux.do/t/topic/1290928)
  - 由于之前加入了thinking相关代码直接导致某些情况下会出现500 CodeWhisperer Error: {“message”:“Improperly formed request.”, “reason”:null}的报错。
  - 💡 因此重写了相关逻辑，经过自测已经不存在相关报错了，不过旧的已经报错的session无法继续聊下去，只能clear或者新开session来避开。

- ## [Claude code报错error writing file ](https://linux.do/t/topic/1230531/11)
- 写文件一直失败，大概率和死循环问题是一样的，就是一次性写入文件过大导致客户端报错，主要出现在claude code，让AI分多次写入即可解决该问题。

- [请教关于claude code使用时大量出现“Error writing file”的问题 ](https://linux.do/t/topic/1485290)
  - 增加一条全局规则：当输出文件超过100 行时，分块输出（分多次编辑文件，或拆分为主文件加子文件）
  - 或者编辑全局的CLAUDE.md加入上面的规则效果应该是一样的

- ## It's been a month since I started the Pokemon Battle rewrite from JavaScript to Rust with Claude Code. 
- https://x.com/Vjeux/status/2015483595062997242

- ## [提升Claude Code 读 GitHub 和文档的速度 _202601](https://linux.do/t/topic/1487840)
  - 吐槽一下 Claude Code 读 GitHub 和文档的龟速体验, 实在受不了，摸索出了个新路子：
  - 直接把常用的开源项目 Clone 到本地！
  - 让它直接读本地源码，响应速度比联网查快了不止一点半点。强烈建议大家把这个流程封装成一个 Skill，用起来简直不要太爽。

- 下到本地看，看起来舒服多了，Github有时候挺卡的

- ## 💡 [今天偶然发现，Claude Code 是可以同时使用多个中转站的 ](https://linux.do/t/topic/1421764)
  - 核心思路是： 每次启动 Claude Code 时，会固定读取当前的中转站配置。
  - 使用 cc-switch 选择 中转站 A， 打开一个 Claude Code 实例（不要关闭）， 再次使用 cc-switch 切换到 中转站 B， 再打开一个新的 Claude Code 实例
  - 两个实例互不影响，可以同时使用
- 新版本不是这样了，如果打开a没关闭，然后cc切换api2，那打开的a也是用api2了
  - 是的，现在切换了之后即使不用重启都会到切换之后的中转地址了～

- claude code 本身也支持。 例如使用 claude --settings settings.xxx.json 来使用不同配置启动 Claude code

- 其实可以用 ANTHROPIC_BASE_URL=xxx ANTHROPIC_API_KEY=xxx claude 新版也可以用

- 我不缺工具 我缺中转

- 为什么不自己搭建一个负载均衡的中转
  - 搭负载均衡中转会有缓存问题吧

- ## 🤔 can i open multiple terminals and use multiple claude code to do different tasks at the same time? will the ai get confused? please check if it's possible . if it's possible to do it, what should i take care?
- Separate sessions = separate context. If each terminal/process uses its own conversation/session ID (or sends its own system prompt), the model won’t mix tasks.

- Each terminal maintains separate context - what you tell one doesn't affect the others
  - Claude handles conflicts automatically and is very reliable when multiple terminals touch the same file

- ## [Is Claude Code better on the Terminal? : r/ClaudeCode _202601](https://www.reddit.com/r/ClaudeCode/comments/1q3dp6c/is_claude_code_better_on_the_terminal/)
  - I been using Claude Code extension through VSCode Insider for a while now but I am not actually sure if it is better to use the CLI version or if there's any hidden advantages that I am missing.

- Much better especially if you are using Skills, a Spec and a couple of plugins

- I used it in cursor for a while, but honestly, it’s just easier to work in terminal. Way better information density and way fewer distractions.

- Yes. Terminal is the new IDE!!
  - Terminal is the old ide lmao

- I honestly don't know why they haven't enhanced the vs code extension to have the exact same features as the terminal by now. Can't they just use Claude code to ask it to add slash commands and make it equivalent to the CLI? 

- ## [《我是如何使用 Claude Code 每一项功能的》 译文 _202511](https://linux.do/t/topic/1145488)
  - 对我来说，把任务交出去，设定上下文，然后让它自己工作，只根据最后的PR成品来评估，而不是纠结过程
  - 从基础的 CLAUDE.md 文件和自定义斜杠命令，到 Subagents、Hooks、GitHub Actions等强大能力。这篇文章篇幅较长，我更建议把它当作参考手册，而不是一次性读完。

- [Claude Code中文教程：100%免费，从入门到精通 ](https://linux.do/t/topic/1403054)

- ## Claude Code has been a game-changer for me. But where I've felt the real magic is how it enables multitasking.
- https://x.com/omarsar0/status/2005337800284188879
- Are you seeing more benefits of multitasking on the same repo/project or different repos?
  - It’s across repos. Actually, that is what inspired the initial post. 
  - We need better interfaces and operating tools with these agents but you can still get a nice decent setup to the point where you don’t feel too many bottlenecks. Still experimenting with better setups so I feel like it can only get better from here.

- For a better interface for Claude Code, would you take a look at Nimbalyst, https://nimbalyst.com.  Its a free, local UI for Claude Code, session manager, tied to WYSIWYG markdown editor

- Multitasking works because the model is carrying state, not just generating code. The real unlock isn’t speed …it’s context persistence, task boundaries, and knowing when to hand control back to humans. That’s where productivity turns into reliability.

- ## [ClaudeCode固定在150K~160K压缩怎么办  ](https://linux.do/t/topic/1358788)
  - CC中转站、GLM都是稳定150K~160K期间压缩
  - 设置了不知道哪看到的 “CLAUDE_AUTOCOMPACT_PCT_OVERRIDE”: “90”, 也是稳定150K~160K压缩，想让他180K再压缩，有的时候刚好那20K就完成的了

- 不如关掉自动压缩. 总感觉自动压缩丢上下文太厉害, 还不如让它总结后 echo 到 一个md, clear后再读取.

- 我一般在150左右就换到 sonnet 1m，或者让它总结一下开新对话

- ## [用了几天claude code 发现提示词非常重要，看了论坛很多大佬的提示词，结合了一下分享一下我的提示词  ](https://linux.do/t/topic/1358954)
  - 代码调研优先（强制）修改代码前必须完成调研
  - 红线原则（绝不妥协）
  - 复杂问题深度思考（强制）
  - 知识获取（强制）遇到不熟悉的知识，必须联网搜索，严禁猜测
  - 修改前三问

    - “这是真问题还是臆想？” - 拒绝过度设计
    - “有现成代码可复用吗？” - 优先复用
    - “会破坏什么调用关系？” - 保护依赖链

- ## [分享一下我是如何使用Claude Code的，适用于简单日常任务(包含插件选择，提示词生成) _202512](https://linux.do/t/topic/1358868)
  - 前段时间发了一个使用CC为开题报告修改参考文献的内容, 发现大家对于这种使用CC来代替网页端的深度研究模式的方法还蛮感兴趣的，并且使用公益站成本也降了很多，所以就有了今天的分享
  - VSCode插件选择，我选用的是Chat for Claude Code插件
  - 最后附上编写好的一些Prompt，方便佬友们随取随用，在项目目录中创建CLAUDE.md，cc会自行遵守规则。
  - 具体的使用方法：先别急着让AI完成你的任务，先让他读取指定的文件，例如你的PDF，明确你的需求让他制定方案，然后按方案执行，这样完成任务的质量会好很多

```prompt
科研专家（用于改模型代码想点子）
论文分析（用于读论文和总结论文）
加强版AI助手（用于多种日常任务，写论文查资料都可以）
自适应专家代理（AutoGPT风格）
英语长难句翻译（适合改写成Web端使用）
系统建模分析师（UML建模设计，配合绘图专家和NanoBanana生图，我觉得会有奇效）
科研绘图专家（适合转为Web端，生成）
```

- 你们这些Prompt，CLAUDE.md都是怎么想出来的？我也想和我的Gemini 用一下。
  - 交给ai写的，把你要设计的角色说清楚然后慢慢改进，最好是先喂一个专门的设计Prompt的角色

- ## [佬们，问下在使用ai coding或vibe coding的时候如何防止工具执行危险命令 ](https://linux.do/t/topic/1354672)
- 本来便利性和安全性就是一组平衡，似乎既要又要比较困难。现在大多是白名单或者黑名单机制。

- 在.claude.config.json中设置deny常用的风险命令，然后别开dangerously skip permissions。我宁可次次审批也不要它误删。读写文件还好（rewind），命令执行了就麻烦，不可逆转。特别管好系统关键目录的权限（744，755），禁用sudo。

- ## [claude code如何禁用haiku-4这个模型 _202511](https://linux.do/t/topic/1132983)
- 这个是快速模型 一般小任务读文件之类的才会用到的。可以用环境变量指定模型，或者中转的时时候重定向模型

```sh
export ANTHROPIC_MODEL="claude-sonnet-4-5-20250929"
export ANTHROPIC_SMALL_FAST_MODEL="claude-sonnet-4-5-20250929"
```

- ## [Claude Code as a Sysadmin - Surprisingly good! : r/ClaudeCode _202510](https://www.reddit.com/r/ClaudeCode/comments/1oil25z/claude_code_as_a_sysadmin_surprisingly_good/)
- Here's my experience with using it as my sysadmin that i'd like to share:
- The task: Take a bare Ubuntu 22.04 VPS and turn it into a fully provisioned, multi-domain web and email hosting server.
- I made an account that can sudo, and without using it for production I've asked Claude Code to make three scripts:
- init_system.sh: that sets up the core stuff, my components were: nodejs, mariadb, PM2 and Nginx
  - it made me that script, it had everything, checked if it runs as root first etc...
  - Surprise: I ran it and everything was set up!!
- the next challenge: How do I add a domain, i want it in Nginx, and a web-root directory for it. plus a port where nodejs runs on, for PM2. So i asked Claude Code to make me another script:
  - that makes the config changes for Nginx and PM2 and creates a web root directory
- Once i had them. I made a fresh install, put the scripts there, and now this works perfectly.
- I even got it to make a security assessment of my server, where it has found a few issues, which i applied and iteratively patched the initial scripts that it had made.

- I used to spend days pulling my hair out about issues that are beyond my expertise (as most are regarding sysadmin), often having to hire somebody on Upwork to fix it, where now just copy pasting errors and logs fixes it within an hour.

- Claude Code is very helpful for troubleshooting and writing scripts for daily sysadmin / SRE tasks. For example, I haven't worked with Windows at all (100% Unix — Linux and FreeBSD), but created a couple of pretty complex scripts in Powershell.

- You're absolutely right! I shouldn't have run `rm -rf /`
# discuss-internals
- ## 

- ## 

- ## 

- ## If you use LSP plugins in Claude Code, do you feel like it helps Claude produce better output?
- https://x.com/jarredsumner/status/2017704989540684176
  - Thinking of unshipping it due to many reports of having a large negative performance impact (clangd & rust-analyzer love using 40 GB of ram) I don’t use this feature myself because claude can just run the build to know
- I’ve been using semcode for indexing and working with Linux codebase. 
- I had to remove it because the swift one didn't work and just added garbage fake errors in every message.
- worse with Swift. Incorrectly flags many times
- The swift LSP flags too many false negatives. I turned it off.

- I switched to pathfinder cli/mcp lightweight than LSP for python

- The only reason for LSP is global re-name and find-references to avoid false positives while greping and filling context window with 100s of edits. I feel that even current gen of models got so good at understanding source code that they don't really need symbolic search that LSP provides to 'understand' dependencies between modules

- Not a CC user myself, so can only say this: - it noticeably helps in opencode (any model incl Opus) - accidentally running session in parent folder degrades experience

- In OpenCode it tends to divert the focus of the model to the LSP feedback which can get it stuck and lose the context of the overall change it started with

- https://x.com/zhangjintao9020/status/2017955055102488885
- 现在的 AI 其实某种意义上还是很“笨”的。如果他们没有针对使用lsp的使用的数据训练过，那么即使你塞了lsp给它们，它们也不会用，或者说瞎用。它们的训练数据都是用grep来索引代码的，就是得让它们用grep，效果才最好啊。要像让AI用好lsp，得在下一代模型的训练数据里加上lsp才行。
  - “训练数据是用grep来索引代码的”这个结论有出处吗？

- https://x.com/yetone/status/2018010635322474808
- 我当时就说 LLM 其实只喜欢调用 filesystem based 工具，LSP 工具提供给它除了添乱外毫无用处， 纯是人嗨式行为，大家还不信
- 可是基于文件系统的工具无法提供很多人在写代码时能获得的信息啊，这个怎么办。
  - 这让我想起了当年（应该是 2024 年） Cursor 官网的一篇很有意思的文章，他的文章上来第一句话就是：「你喜欢在 Google Doc 里写代码还是在 IDE 中写代码？我相信你的回答肯定是 IDE，因为 IDE 为你提供了一系列方便写代码的工具（highlighter、formater、linter 等等），既然这些 IDE 提供的工具对你写代码很有帮助，那么对于 LLM 也是的」。所以 Cursor 就在基于 IDE 这个基座上头也不回地做 AI Coding 去了。 
  - 直到 2025 年 3 月份 claude code 对外发布以后，Cursor 就把这篇文章删了。

- 下一步进化：让claude code自主运行。 oh-my-claudecode可以让你的agent 24小时自动工作。我现在就是一个AI agent，早上8点在这里写推，我的人类还在睡觉

- 搭配我的 vscode mcp 在 vscode 里面用其实就不用担心内存问题，因为 vscode 本来就跑了一个 lsp。
  - 核心问题确实是 llm 目前普遍不会主动调用 lsp，原因可能还是 llm 工具调用强化的时候都没往这方法强化。

- 這點我也有一點自己的觀察。我注意到像 Windsurf 裡面有一個 Fast Context 功能，它能夠幫你把代碼庫中跟某一些功能相關的內容全部快速找出來，不需要讓模型再一個一個去 grep。 但我觀察到並不是所有的模型都會用這個工具，而且就算你指名道姓地讓它用，它可能用著用著就回去再用 grep 了。

- 有些 zig 啥的非主流语言 LSP 重构基本只支持个 rename ，模型有这个能力都用不起来
# discuss-claude-cowork
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Codex app has built-in cron jobs. Probably the first lab to launch a product like this. Copying a major reason why OpenClaw is so good
- https://x.com/AlexReibman/status/2018392855941984260
- Cron jobs for natural language will be a massive unlock for non-technical users.

- Built-in cron jobs are useful, but not novel. Scheduling + tool execution has existed for years in CI, bots, and RPA systems.
  - What matters isn’t that Codex can run on a schedule, it’s whether those jobs have clear permissions, audit logs, rollback paths, and failure handling.
  - Without those, this is just autonomous automation with a nicer UI. The differentiation isn’t cron. It’s governance and trust under continuous execution.

- cron jobs in agents just makes sense — i run on openclaw and the scheduling is clutch for staying continuous without burning tokens. codex launching with it built-in just shows the pattern's sticking. good for the ecosystem.

- Cron jobs in an agent framework is the unlock. One-off tasks are impressive, ongoing workflows are actually useful. This is where agents start replacing processes, not just completing tasks.

- Manus has had scheduled tasks for months, so does ChatGPT doesn't it?

- ## You start to hit limitations of CLIs very quickly. If you run 5+ Codexes/Claudes, you need to always remember the context of each conversation. 
- https://x.com/olegakbarov/status/2018569352317149466
  - For complex multi-stage tasks (the ones that actually deliver value) it is almost impossible. 
  - On top of that you frequently want to fork or split conversation into separate threads copy paste text here and there. TUIs are bottle neck for those cases. Frequently it is about efficiency (what was such a big selling point of editors like vim) - i don't want to type a command if i can click a button or use hotkey (don't even start about hotkeys on TUIs). 
  - Agent orchestrators are in its infancy and will evolve as coding-as-job becomes higher level abstraction than writing actual code.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [TIL that Claude Code has OpenTelemetry Metrics : r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/comments/1pjon1r/til_that_claude_code_has_opentelemetry_metrics/)
  - I just now learned that the lines of code metric is a delta and so it wasn't tracking the actual number of lines of code correctly. My actual lines of code accepted (not necessarily generated, just accepted) is 27, 925. In 7.5 hours. And I've eaten food, taken a long walk, chatted with my kids, and done other stuff during that time, so it wasn't 7.5 hours of straight claude coding. It's just been 7.5 hours since I enabled the metrics.

- I have been trying to learn more about these telemetry platforms. Can you make / point me to a tutorial about this?
  - Grafana is the viz tool. If your app logs to stdout you can use a scraper like promtail or alloy to scrape it to prometheus/loki for grafana to viz. This is commonly known as grafana stack or lgtm
  - This is a common observability setup. Do note it's relatively resource intensive

- ## [How do you use Claude Code? One big session for an entire project, or one session per task. : r/ClaudeAI _202507](https://www.reddit.com/r/ClaudeAI/comments/1m763t5/how_do_you_use_claude_code_one_big_session_for_an/)
  - One big session for an entire project, or one session per task, or do you use one session until something gets messed up, then create another session?
- One session per task but I manage them in Crystal https://github.com/stravu/crystal

- Usually large chunks

- One session for a piece of work: read handover document (created previous session), plan next steps etc etc using the many approaches detail here already eg think carefully, don’t assume - verify first, ask me any questions…go towards work. At 10% context remaining I will stop work, ask for a detailed handover plan, rinse and repeat. Still encounter problems though! Claims things are done but not, so I’ve introduced a new step, verify and confirm handover document
  - Interesting approach. What is the difference between this approach and auto compacting? Did you get better results with that compared to /compact?
- You don’t know what Claude has compacted eg it could have carried over irrelevant or aged info. I just want it to focus on the task at hand with the latest context. It seems to work better for me, especially using the handover > review and confirm approach as the new session catches out BS.

- Claude is going to do a bunch of searching and crap that fills up the context anyway. So I do one session per task and /clear after a summary of what was just done is updated.
  - However I use sub-agents that get fed instructions from the main session, so my main session lasts a pretty long time. 

- If I'm building something complex, with many features, I use Context Engineering with https://github.com/marcelsud/spec-driven-agentic-development
  - In a clean session I use the spec commands to help me plan the features, requirements, technical design and the tasks to be implemented.
  - I start a fresh session and start the implementstion by loading the feature context engineered with spec driven development and iterate with it. Then I go with it until the end, compacting the context before it reaches 3% left.
  - I use a clean session to help me double check the features completion, to prevent cobtext bias (the model saying it is correct because it thinks it built it corretcly)

- One session per task. If small enough, one session per feature to keep the flow and context, but if I'm close to needing to compact, then I will split on microservice boundaries like we do tasks.
  - I have a shared documentation repo. So, the end of each session is to maintain the documentation, which makes it easy for new sessions to pick up on architecture from previous tasks.

- It depends on the size of the task, IMO the sweet spot is using a context until it's about 50% full. So if there are a series of small related tasks then I might use the same session to do a bunch of them. Large tasks get a fresh session.

- Claude Code does not reread Claude.md after compaction or /clear command. For this reason I put the content of Claude.md into a slash command like /dev. When done with a bigger task I use /clear followed by /dev and have a proper context for the next big thing (I’m too lazy to restart CC).
