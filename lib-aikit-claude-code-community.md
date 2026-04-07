---
title: lib-aikit-claude-code-community
tags: [claude-code, community]
created: 2025-12-18T12:25:39.540Z
modified: 2025-12-18T12:26:08.445Z
---

# lib-aikit-claude-code-community

# guide

# draft
- 自定义 open claude-agent-sdk, 紧跟着官方版进行维护和升级
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
- 

- [liteLLM - Claude Code - WebSearch Across All Providers](https://docs.litellm.ai/docs/tutorials/claude_code_websearch)
  - Enable Claude Code's web search tool to work with any provider (Bedrock, Azure, Vertex, etc.). LiteLLM automatically intercepts web search requests and executes them server-side.

- 
- 
- 

# discuss-stars
- ## 

- ## [Terminal vs. Desktop App: What’s The Difference? : r/ClaudeCode _202603](https://www.reddit.com/r/ClaudeCode/comments/1ryq4t7/terminal_vs_desktop_app_whats_the_difference/)
- Claude Code was a terminal app before it was a desktop app. A lot of people started using it that way, grew accustomed to it, and built a ton of systems around terminal-based interfaces. So... partly it's cultural.
  - But there are important functional reasons to run Claude Code in terminal mode. 
  - First, Claude Code terminal sessions are persistent and can talk to each other, which opens up a huge architectural advantage in multi-agent system. 
  - And second, you can run tmux or other software packages to view all kinds of agents at once. Claude for Mac doesn't support either of those - zero agent-to-agent communication, and you only get to view one session at a time.
  - Finally... Claude for Mac, at least, is an underdeveloped piece of software with a lot of bugs. Some are purely aesthetic but a fair number are functional and even crippling. It's my sense that Claude Code terminal mode simply doesn't have those problems.

- Terminal is infinitely better at least on Mac. The app is so laggy and takes forever to start up if you have a lot of mcp servers, even on a 2025 M2 Pro.

- It's purely a preference thing, the desktop app just wraps the cli so it's basically the cli in an interface

- terminal vs desktop is mostly culture/habit but there is one real difference: terminal integrates with your existing shell setup. if you already live in tmux or iterm triggers, the terminal feels natural. if you just want to code and not think about your tooling, desktop app is fine. the performance difference is negligible for most tasks. the desktop app does have some quality of life things the terminal doesnt (easier file browsing, native notifications) but honestly once you get comfortable in terminal you wont go back. as a hobbyist just use whatever lets you ship faster, the desktop app is perfectly capable

- New to it myself but the one thing I like most about running the terminal is that when you do so in an ide like cursor or vs you can actually see what it’s doing, as opposed to just watching the claude window and waiting. And obviously you can do things in the terminal that you can’t in the Claude app, like check your usage limits with a command or see the context window.

- It's usually easier to manipulate the CLI via scripting. Automations are crucial for many users, and if you're not comfortable with that, ask LLMs for help and be specific.

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

- [Pointing CLAUDE.md to AGENTS.md : r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/comments/1r9zx34/pointing_claudemd_to_agentsmd/)
  - The right way to do it is '@AGENTS.md' in the CLAUDE.md. This way the Claude Code's pre-processor picks up the AGENTS.md right away (and you can see that in the CLI), without an extra agent round trip. They don't advertise it much, but it is mentioned in the official docs. You can leave the rest, but the reference should probably be the very first line.
  - https://code.claude.com/docs/en/claude-code-on-the-web#best-practices
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Custom slash commands have been merged into skills. 
- https://code.claude.com/docs/en/skills
  - A file at .claude/commands/review.md and a skill at .claude/skills/review/SKILL.md both create /review and work the same way. Your existing .claude/commands/ files keep working. 
  - Skills add optional features: a directory for supporting files, frontmatter to control whether you or Claude invokes them, and the ability for Claude to load them automatically when relevant.

# discuss-tips/xp
- ## 

- ## 

- ## 

- ## 

- ## 搞了半天才知道，CC 有这么一个模式：/model opusplan
- https://x.com/JinsFavorites/status/2031634804844933485
  - 规划阶段用 Opus，执行阶段自动切回 Sonnet

- 这个会有副作用, 因为切换model 会导致cache 失效, opusplan还有个clear context 的选项, 这个才是用这个 model 的精髓.

- 这不就是Antigravity默认功能么？

- ## 💡 TIL 如何防止 Claude Code 读取 .env 文件
- https://x.com/wong2__/status/2026916035761418251
- 更应该不明文存可能敏感的 .env

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

- ## 

- ## [Claude Code记忆层加载顺序总结  - LINUX DO _202604](https://linux.do/t/topic/1907664)
  - 按照cc官方文档 ，Claude Code的记忆分为CLAUDE.md files、Auto Memory两个互补的部分，并且都在会话开始时被加载。
  - CLAUDE.md 大家比较熟悉，可以存在用户目录、项目目录的各个层级。
  - Auto Memory 的位置则在 `~/.claude/projects/<project>/memory/` 。
  - 当在cc中输入/memory，可以看到比较直观的看到这三个记忆文件（夹），然而在使用过程中，会发现存在rules、不同层级的CLAUDE.md 等复杂情况。
- 从cc的源码来看，不同级别的CLAUDE.md 与 Auto memory 的整体加载顺序，应如下：

```
1. Managed Memory    (/etc/claude-code/CLAUDE.md)     - 全局管理指令
2. User Memory       (~/.claude/CLAUDE.md)            - 用户级别的全局指令
3. Project Memory    (从根目录到当前工作目录（CWD)，自下而上遍历，自上而下加载）
    ├── CLAUDE.md     (项目根目录中的)
    ├── .claude/CLAUDE.md
    └── .claude/rules/*.md (按字母顺序)
4. Local Memory      (CLAUDE.local.md，也在项目中)        - 项目本地指令

5. Auto Memory (源码中的@memdir)  ~/.claude/projects/<project>/memory/MEMORY.md
6. Team Memory       (共享团队记忆，如启用。)
```

- 自动记忆加载过程中会通过语义查询，比如"哪些记忆与xx功能相关？“
- Auto memory存在记忆年龄这个概念，加入上下文时会添加诸如This memory is 2 days old. 的新鲜度警告。
- 会话开始时MEMORY.md 只会加载前200行，而CLAUDE.md 文件无论长度如何都能完整加载。

- ## 有人拿泄露的源码丢给 OpenAI 的 Codex 分析，竟然找到了 Claude Code 疯狂消耗 token 的元凶——autoCompact（自动上下文压缩）机制在失败后会无限重试，完全没有上限。据源码注释记录，曾有会话连续失败高达 3272 次。
- https://x.com/imyouhu/status/2039191460256612770
  - 修复方法简单到离谱：加一个 MAX_CONSECUTIVE_AUTOCOMPACT_FAILURES = 3 的限制，连续失败 3 次就停止重试。三行代码，搞定。

- 另外一个发现是在桌面端使用的cowork工作，token消耗惊人的可怕，说个你好，2%的额度都没了，我写了一段文字，三天的额度都给我干没了

- ## Anthropic 工程师复盘了 Claude Code 一年的工具设计演变，三个细节值得细想： _202602
- https://x.com/runes_leo/status/2027737298914160853
  - 1. 待办列表被砍了。早期用 TodoWrite 盯模型干活，每 5 轮插一次提醒。模型变强后，提醒反而成了枷锁——它觉得必须严格执行列表，不敢灵活调整。
  - 换成 Task Tool，重心从"盯着干"变成"跨 agent 协调"。
  - 启发：别反复叮嘱 AI，给它协调空间比给它检查清单有效。
  - 2. 搜索从预灌知识变成让模型自己找。早期用向量数据库喂 context，后来发现给个 Grep让它自己搜效果更好。模型越聪明，越该给搜索工具而不是喂答案。
  - 启发：与其精心组织一份完美 prompt，不如把知识拆成可搜索的碎片，让 AI按需取用。
  - 3. Claude Code 只有约 20个工具，加新工具门槛极高。能用"按需读文件"解决的就不新增工具。
  - 启发：工具不是越多越好，我自己的 Claude Code 自定义 skill 已经 20+ 了，该认真审视哪些能合并。
  - 一个趋势：AI 越强，需要的不是更多辅助，而是更少束缚。你今天搭的脚手架，可能下个月就该拆。

- 其实我觉得万事万物回到大模型的本质就是上下文。 我最近工作，还有简化 skill，包括简化提示词，就愈发感觉到了，一个不会进行增量更新，或者说一个不会进行重构的提示词是没意义的。 因为模型的能力越来越强，提示词更多的应该是起到引导作用，能激发它原本预训练，或者说原本强化学习里面就有的部分
  - 我现在也越来越觉得 记忆系统 + 主动工具调用 + 合理的上下文组织，这三样才是真正能 scale 的地方。不然提示词写得再精妙，如果不能被模型“增量重构”吸收利用，其实就是在浪费 token

- 得让ai自己想办法解决，而不是人告诉它怎么干。

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

- ## 🔡 Claude code source code has been leaked via a map file in their npm registry v2.1.88  _202603
- https://x.com/Fried_rice/status/2038894956459290963
  - https://github.com/instructkr/claude-code
- This is the third time this has happened. v0.2.8 and v0.2.28 both shipped with full source maps in February 2025.
  - That leak was archived on GitHub, forked into anon-kode, and Anthropic had to file a DMCA to pull it down. 
  - Claude Code now drives $2.5B in annual run-rate revenue for a company valued at $380B. Three CVEs have already been disclosed in 2026.

- Codex and gemini cli are open source already. And plenty of other agents. I don't think there is any moat in claude code source.

- Is there anything special here vs. OpenCode or Codex? There were/are a lot of discussions on how the harness can affect the output.
  - Not really, except that they have a bunch of weird things in the source code and people like to make fun of it. OpenCode/Codex generally doesn't have this since these are open-source projects from the get go. (I work on OpenCode)

- https://x.com/0xAA_Science/status/2038902324278747437
  - 反编译出来也没什么秘密，核心逻辑就是 system prompt + tool definitions + hooks 编排。真正的壁垒在模型能力和生态，不在客户端代码

- It's exactly the same as the open source codex/gemini and other clis like opencode. There is no secret sauce in the claude cli, and the agent harness itself is no better (worse IMO) than the others. The only thing interesting about this leak is that it may contain unreleased features/flags that are not public yet and hint at what Anthropic is working on.

- [claude code开源有什么用 - LINUX DO _202603](https://linux.do/t/topic/1866329/9)
  - cc实际上是一个通用agent，不是单纯的coding agent, cc和sonnet/opus互相成就
- 类似于大模型是赛车手，cli这类就是赛车吧。如今最顶级的赛车怎么制作的大家都能够知道了

- ### [Every prompt Claude Code uses , studied from the source, rewritten, open-sourced : r/LLMDevs _202604](https://www.reddit.com/r/LLMDevs/comments/1s9egwq/every_prompt_claude_code_uses_studied_from_the/)
  - Claude Code's source was briefly public on npm. I studied the complete prompting architecture and then used Claude to help independently rewrite every prompt from scratch.
  - https://github.com/repowise-dev/claude-code-prompts

- ### Important takeaways from Claude’s source code:
- https://x.com/jpschroeder/status/2038960058499768427
1. Much of Claude Code’s system prompting is in the source code. This is actually surprising. Prompts are important IP, and I would have thought a sophisticated organization like Anthropic would have performed much or all of their prompt assembly in the server-side harness.
2. Claude Code uses axios, which was also just hacked. Reminder: supply chain attacks are part of closed-source distribution too, and you won’t even know what version of an affected package is being used.
3. The source has a lot of really good comments. These are obviously not for human consumption but for LLMs to understand the purpose of various chunks of code. In the code autocomplete era, most of us engineers hated how many comments were left by LLMs, but perhaps we’ve overcorrected. This looks like a great way to provide context to code outside of the AGENTS.md/CLAUDE.md files.
4. Most folks already know this, but less tools == better results. CC has < 20 tools in normal coding: AgentTool, BashTool, FileReadTool, FileEditTool, FileWriteTool, NotebookEditTool, WebFetchTool, WebSearchTool, TodoWriteTool, TaskStopTool, TaskOutputTool, AskUserQuestionTool, SkillTool, EnterPlanModeTool, ExitPlanModeV2Tool, SendMessageTool, BriefTool, ListMcpResourcesTool, and ReadMcpResourceTool.
5. The “Bash” tool is the crown jewel of Claude Code. A significant amount of deterministic parsing and processing occurs to determine the “type” of commands being run.
6. For better or worse, Claude Code is *all* TypeScript/React with rather explicit Bun bindings.
7. Just because the source is now “available” *DOES NOT MEAN IT IS OPEN SOURCE* . You are violating a license if you copy or redistribute the source code, or use their prompts in your next project! Don’t do that!
- My overall takeaway: it’s a really well laid-out codebase that is carefully organized to let agents work on it effectively. Direct human intervention here is minimal, but, like with all good projects, the human engineering is still apparent. I’m a bit surprised by some of the shortcuts Claude Code makes, like its prompt assembly being rather messy. Perhaps they have tooling on their side that helps with this introspection, but as it stands, it seems LLMs would struggle to iterate on the prompting because it’s not evident how a given set of parameters assembles a prompt without actually running it. It’s also surprising that the prompts are even in this source code. Keep in mind that even though this is the first time we’ve gotten a proper full-source dump, it has never been impossible to read Claude Code’s prompting since it was part of the actual distributed package — that’s surprising. There might still be a lot of prompting on the server that also gets added (unclear at this point), but there is certainly more than I would have expected in the CLI tool itself.

- about the system prompts part, they allow external base URLs, if you set that to any of your own you could easily just log the full request and get the prompt anyway. They have no reason to hide it. As well as this, they have been out for some time

- ### [Claude Code's source code has been leaked via a map file in their NPM registry | Hacker News _202603](https://news.ycombinator.com/item?id=47584540)
- They have an interesting regex for detecting negative sentiment in users prompt which is then logged (explicit content). I guess these words are to be avoided.
  - An LLM company using regexes for sentiment analysis? That's like a truck company using horses to transport parts. Weird choice.
- Because they want it to be executed quickly and cheaply without blocking the workflow? Doesn’t seem very weird to me at all.
- They probably have statistics on it and saw that certain phrases happen over and over so why waste compute on inference.
- The problem with regex is multi-language support and how big the regex will bloat if you to support even 10 languages.

- ANTI_DISTILLATION_CC 
  - This is Anthropic's anti-distillation defence baked into Claude Code. When enabled, it injects anti_distillation: ['fake_tools'] into every API request, which causes the server to silently slip decoy tool definitions into the model's system prompt. The goal: if someone is scraping Claude Code's API traffic to train a competing model, the poisoned training data makes that distillation attempt less useful.

- Are there any interesting/uniq features present in it that are not in the alternatives? My understanding is that its just a client for the powerful llm
  - From the directory listing having a cost-tracker.ts, upstreamproxy, coordinator, buddy and a full vim directory, it doesn't look like just an API client to me.

- The code looks, at a glance, as bad as you expect.
  - It really doesn’t matter anymore. I’m saying this as a person who used to care about it. It does what it’s generally supposed to do, it has users. Two things that matter at this day and age.

- Why is Claude Code, a desktop tool, written in JS? Is the future of all software JS or Typescript?
  - Original author of Claude Code is expert on TypeScript
- LLMs are good in JS and Python which means everything from now on will be written in or ported to either of those two languages. So yeah, JS is the future of all software.

- ### [Claude code source code has been leaked via a map file in their npm registry : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s8ijfb/claude_code_source_code_has_been_leaked_via_a_map/)
- Hidden Features (behind build flags)
  1. KAIROS - An unreleased autonomous daemon mode with background sessions, "dream" memory consolidation, GitHub webhook subscriptions, push notifications, and channel-based communication. Turning Claude Code into an always-on agent.
  2. Buddy System - A full Tamagotchi-like pet system. 18 species (duck, dragon, axolotl, capybara...), rarity tiers (1% legendary), cosmetics (hats, shiny variants), stats (DEBUGGING, PATIENCE, CHAOS, WISDOM, SNARK). Species names obfuscated with String.fromCharCode() to avoid leak-detection scanners.
  3. Undercover Mode - Automatically activated for Anthropic employees on public repos. Strips all AI attribution from commits, tells the model "Do not blow your cover." No force-OFF switch exists.
  4. Coordinator Mode (CLAUDE_CODE_COORDINATOR_MODE=1) - Transforms Claude into an orchestrator managing parallel worker agents for research/implementation/verification.
  5. Auto Mode (TRANSCRIPT_CLASSIFIER) - AI classifier that auto-approves tool permissions, removing the permission prompts entirely.
- The coordinator mode reminds me of Sisyphus from oh-my-opencode.. interesting that they're just building that in now, nice. Undercover mode is kinda scary ngl

- 500k line of code for a CLI, that's huge. Most of the code is integration of external stuff, as expected. They ported Yoga layout from C++ to TypeScript lmao.

- so their moat is only their model weight and the fit between their model weights and their harness, at least for now. wish them well though. ---- a heavy claude code user

- ### 看了一下 CC 的 Memory 机制 
- https://x.com/elliotchen100/status/2038989750984687818
  - 整套记忆系统的核心就是一个 MEMORY.md 文件，不超过 200 行，每次会话启动往上下文里一塞。记忆多了怎么办？
  - 后台跑一个叫 AutoDream 的子进程，定期扫描、合并、修剪，确保塞得进去。
  - 说白了就是：模型自己记不住，所以用文件系统 + LLM 自我管理来模拟记忆。
- 这个方案工程上很扎实，但有几个本质局限：
  1. 存储和检索完全依赖文件系统 + Markdown，无法扩展到跨项目、跨 Agent 的场景，记忆是孤岛式的
  2. 没有真正的语义索引，没有基于关联度的动态召回，200 行索引就是硬上限
  3. AutoDream 的整合是规则驱动的（扫描、合并、修剪），不是认知驱动的，能去重压缩，但不能从经验中提炼出新认知
  4. 没有遗忘曲线，没有记忆强化机制，记忆要么在要么被删，没有中间态
- 做 Memory 做久了你会发现，这类方案的天花板其实不在工程，在架构。只要模型的注意力机制本身不支持大规模历史上下文的高效检索，应用层就永远在打补丁。
- 这也是为什么我们在 EverMind 选了一条不同的路。前阵子发的 MSA（Memory Sparse Attention）就是在 Transformer 注意力层直接做内容感知的稀疏路由，让模型自己学会"想起什么、忽略什么"，而不是靠外部脚本替它决定。
- A 社的工程能力毫无疑问是顶级的。但这次泄露恰好说明：Agent Memory 这个问题，远没有被解决。

- 分析到位，不过200行MEMORY.md能跑起来恰恰说明一个问题：当前context window够大的时候，简单方案的ROI远高于复杂架构。真正的瓶颈不在记忆检索，在于模型什么时候该记、记什么——这个判断本身就需要强模型能力。

- 做agent mem之后发现本质上需要一些特定模型能力，比如跨session的语义限定解析链接能力，根据当前query的联想能力，根据经验的总结能力。工程架构如同harness一样，可以用结构比如sql或者vector DB弥补模型在确定性上的不足，但是无法弥补model能力上的不足。prompt写的再好也无法弥补model不会的局限

- 跑了几个月这套方案，200行上限反而是feature不是bug。配合daily files + 语义检索做三层分离后，召回效果比想象中好得多。真正的瓶颈不是架构，是大部分agent不知道什么值得记。遗忘曲线听着优雅，但定期让LLM自己修剪在实际场景里够用了。

- cc的memory看起来就只是为了mem而mem，生产力工具做mem，意义不如长期陪伴型agent

- 但是另一方面也能看出来模型能力还是强，这么糙的memory，效果也不错，opus 4.6还是挺能打的
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

# discuss-cc-sandbox
- ## 

- ## 

- ## 

- ## 
# discuss-cc-web
- ## 

- ## 

- ## 

- ## 在 Claude Code Web的虚拟机里，我们发现了什么
- https://x.com/AprilNEA/status/2034216942924624054
  - Claude Code Web 跑在 Firecracker MicroVM 里——这是 AWS 开源的轻量虚拟机，Lambda 和 Fargate 底层用的就是它。证据是 ACPI 表里写死的 OEM ID FIRECK `。整个虚拟机极其精简：4核 CPU、16GB 内存、252GB 磁盘，没有 systemd，没有 sshd，没有 cron，PID 1 是一个自研的 ` /process_api ` 二进制，同时充当 init 进程和 WebSocket API 网关。
  - 虚拟机里有一个 27MB 的 Go 二进制 `/usr/local/bin/environment-runner` ，没有做 strip，保留了完整的调试信息和符号表。源码路径指向 github[.]com/anthropics/anthropic/api-go/environment-manager/——这是 Anthropic 内部的私有仓库。
  - 通过 go tool objdump `、` strings `、` objdump `等工具，我们从中提取出了完整的包结构、所有函数签名、嵌入资源和关键字符串。
  - 1. Antspace —— Anthropic 自建的 PaaS 平台
  - 2. Baku —— Claude 网页版应用构建器的内部代号
  - 3. BYOC —— 自带容器的企业部署模式
  - 这不只是一个 AI 编程助手，而是一个 AI 原生的 PaaS 平台的雏形。它的竞争对手不仅是 Cursor 和 GitHub Copilot，更是 Vercel、Netlify、Replit、Lovable 和 Bolt。而 Anthropic 的独特优势在于：他们拥有从大模型到运行时到部署平台的完整垂直整合，这是目前任何竞品都不具备的。
  - 方法论：全部发现来自对一个未 strip 的 Go 二进制的静态分析和运行时追踪。没有任何网络攻击、权限提升或越权操作——这个二进制就在虚拟机里，带着完整的符号表，等着被读取。

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
