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

- ## [Forked Google's Gemini CLI to work with local LLMs (MLX, llama.cpp, vLLM) : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pn0gpa/forked_googles_gemini_cli_to_work_with_local_llms/)
  - So i forked the gemini cli and added local llm support, no google account needed, runs offline.

- ## [Looking for an alternative to ClaudeCode. Is OpenCode + GLM 4.7 my best bet? : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1q8bcsg/looking_for_an_alternative_to_claudecode_is/)
- I tried OpenCode + GLM 4.7 and honestly GLM 4.7 has been pretty error-prone for Android work (Gradle/Kotlin DSL quirks, shaky API assumptions, and fixes that don’t compile on the first try).

- glm 4.7 + cc >>>>>> glm 4.7 + opencode

- [Looking for an alternative to ClaudeCode. Is OpenCode + GLM 4.7 my best bet? : r/opencodeCLI](https://www.reddit.com/r/opencodeCLI/comments/1q8bcsg/looking_for_an_alternative_to_claudecode_is/)
  - i tried glm 4.7 with opencode coming from claude code with opus but tbh it felt like bit retarded junior dev compared to cc with opus or sonnet, especially with rust. i wouldnt say its bad, prolly just my expectations that it might come close to what i got used to with cc/opus were maybe just too high, also the language support (slovak) with glm is just bad

- ## [Opencode vs Codex CLI: Same Prompt, Clearer Output — Why? : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1qdujsl/opencode_vs_codex_cli_same_prompt_clearer_output/)
- Coding agent clients (sometimes referred to as harnesses) have their own prompt engineering flows. those include the system prompt, compacting strategies, context lookups, code indexing and more. Behind the scenes you plugged them to the same model with the same user prompt, but the model received a whole lot of different prompt that just happens to include a part of it that is identical
  - opencode system prompts are open

- ## [OpenCode with GPT is next level : r/codex _202601](https://www.reddit.com/r/codex/comments/1qee31p/opencode_with_gpt_is_next_level/)
- How is OpenCode better than Codex CLI?
  - Interface. Speed. Sub agents. LSP.
- From my experience Codex CLI still offers the best experience. I’d really like to replace it with Opencode but it’s missing the precision I value so much with the Codex harness. Unfortunately.
  - Codex CLI is better at understanding my intent and is conservative with solutions. While Opencode thinks more, writes more code and brings more work to the table I did not intent. Therefore I have to do more iterations which often just makes it worse.
  - I understand this is probably caused by the fact that OpenAI has locked the system prompt to Codex for ChatGPT subscribers. Which Opencode then has to amend with instructions specific to Opencode. The experience with an API key might be totally different.

- what's the biggest different and benefits of using that over Codex CLI? Is that mainly I can switch models or something else?
  - Ease of use, speed, sub-agents, LSP.

- ## [I tested Claude 4.5, GPT-5.1 Codex, and Gemini 3 Pro on real code (not benchmarks) : r/ChatGPTCoding _202511](https://www.reddit.com/r/ChatGPTCoding/comments/1p9vpyz/i_tested_claude_45_gpt51_codex_and_gemini_3_pro/)
- I tried both Sonnet 4.5 and Gemini 3 Pro High to build a site from scratch. Sonnet’s UI is way cleaner, almost no layout issues. Gemini, on the other hand, had some pretty obvious problems, like everything getting stuck to the left instead of being centered

- ## [I tried Gemini 3 for a couple of days ... Codex is still the best. By far.. : r/codex _202512](https://www.reddit.com/r/codex/comments/1pf7pc1/i_tried_gemini_3_for_a_couple_of_days_codex_is/)
- i use codex for backend and cleaning up code from the others, opus to do both frontend/backend if i run out of antigravity/codex, and gemini for front end. they have their niches but overall opus is the most flexible ime

- Gemini sucks at anything agentic. It ignores instructions, it’s lazy and it can’t handle large contexts. It’s a benchmaxxed mess.

- I am paying both of the memberships but I will keep the OpenAI one. Gemini takes too much decisions by itself when I give clear instructions.

- I just used gemini 4+ hours yesterday and when the context gets too big it start hallucinating like hell. That never happened with codex.

- I find the same.. Gemini 3 made so many mistakes it’s just not worth the hassle… also if you leave it alone it looped on me several times. Codex and Claude simply never give me issues like that.

- ## [Gemini CLI is impressive, but Claude Code is acting like the real senior engineer : r/ClaudeCode _202512](https://www.reddit.com/r/ClaudeCode/comments/1pdyq6z/gemini_cli_is_impressive_but_claude_code_is/)
- I tried most agents and I still find Claude Code to be the most capable and reliable one. There are certain cases where I would use another agent to aid solving problems that Claude Code might get stuck in but usually it is the main agent I use. 
  - Collaborative agents are going to be the future where a team of agents can work on a task or a task would be assigned to the most reliable and efficient agent capable of solving it.

- Opus is superior. However, tou will drastically increase your output quality if you use both (one as the driver, one as the reviewer). Sometimes if its a really complex task I'll even use two reviewers. I actually built an open-source tool to automate this

- I have tested Gemini 3 Pro Preview and Claude Opus 4.5 multiple times having each generate security audit report on multiple popular GitHub projects (Cherry Studio, Chatbox, Jan, etc). Claude has consistently found more issues than Gemini even though it has less than a quarter of the context window as Gemini. When I ask Gemini whether Claude’s additional issues found were accurate, Gemini has consistently responded that they were accurate.

- Gemini is great at looking at everything and Codex is pretty good for finding weird logic flow bugs. But Opus 4.5, gets it right most of the time. If you tell it to follow a plan, enforce code-quality checks, and test-driven development, basically the same stuff I force myself to do but don't want to. It creates shippable code with few iterations; sometimes straight out of the gate.

- ## [Gemini 3.0 Pro has been out for long enough. For those who have tried all three, how does it (in Gemini CLI) shape up compared to Codex CLI and Claude Code (both CLI and models)? : r/ChatGPTCoding _202512](https://www.reddit.com/r/ChatGPTCoding/comments/1pi4ojr/gemini_30_pro_has_been_out_for_long_enough_for/)
- gemini sometimes one shots things that take "workhorse" codex forever to figure out, but it is a fickle beast. it has moments of brilliance and occasional periods of insanity

- Codex is stupidly slow. It sometimes gets stuck on harder things and basically implements nothing. But pretty good and reliable for basic stuff and never seems to hit limits. It sometimes surprises me with clever solutions.
  - Claude is good for making project wide changes while still being in control. But the sessions limits are absolutely ridiculous
  - Gemini seems pretty good in analyzing the project. But when it uses 2.5 instead of 3 it can get quite stupid more often than Claude or Codex do.
  - At least for my uses cases they are all somewhat similar. Transparency, speed, limits and ease of use matter more to me. Sometimes Claude gets stuck on a problem, sometimes it's Codex, sometimes it's Gemini, and then the other agents somehow manage to solve it. Managing the context matters in that as well, I guess, and in some it's just better or easier.

- I have the max plan for all 3. 
  - Gemini produces the best UI but is the worst at following instructions. 
  - Codex is the best at code review, debugging, and architectural decisions / implementing new architecture, but requires handholding and requires you to prompt it to continue working. 
  - Opus 4.5 is the best actual daily driver, amazing at following instructions, best general "assistant" outside of coding (e.g. LLM cofounder esque activities), and goes without saying also great at coding

- the Gemini CLI with Gemini 3 is excellent for user interfaces. Neither Claude Code nor Codex CLI focuses on that, but Gemini builds much better interfaces.

- Gemini simply doesn’t follow instructions properly like codex

- ## [Best AI Coding Tool: Gemini CLI, Codex, or Claude Code : r/vibecoding _202510](https://www.reddit.com/r/vibecoding/comments/1oa9d5o/best_ai_coding_tool_gemini_cli_codex_or_claude/)
- Sadly, there is no best. They all seem to excel at different things. 
  - In my experience, Codex is a strong backend developer. 
  - Claude seems better at UI/UX. 
  - I use Gemini for planning and research given its huge context window and obvious search ties. But its implementation is terrible.
  - You also want to get in the habit of having the AI double and triple check each others work. If you only use one company’s LLM, use different sessions with separate context and different agents to analyze the work and catch bugs.
  - The reality is that every new generation of model is likely to surpass the last, so don’t get locked into one company. They are all staggered now it seems so every 2-3 months there is a new SOTA frontier model - use that one.

- ## [Codex、GeminiCLI真的弱于Claude Code吗 _202601](https://linux.do/t/topic/1420013)
  - 两个都体验过后，发现都还是不如CC, 这是事实吗？还是我自己的使用方式不对
- GEMINI CLI不知道，CODEX CLI强的一批
- CODEX CLI 非前端任务无敌。前端就是默认的审美一般，提示词到位也不错。

- codex非常强，使用体验甚至比cc好

- 看场景吧，前端页面GeminiCLI很强，修bug、做服务端的话Codex很强
- 弄Java的话，Codex根本不输CC啊，只是有点慢而已，我反而更喜欢Codex
  - +1，我现在每天是把codex蹬完再用cc，中间要改页面就切到gemini
- gemini做做前端还可以 codex不逊色cc

- 我的体验 codex 5.2 xh > claude opus 4.5, opus 4.5经常偷懒

- 我现在用 cx 写代码, cc 用来解释代码, cc 解释代码比较详细一点, 也快一些

- 在嵌入式领域， claudecode 不如 codex 一根

- codex挺强的，就是gpt太慢了
- 复杂任务codex强过cc就是实在是太慢了

- codex真的强，特别是配置GPT-5.2-HIGTH

- gemini-cli 虽然介面用起来，至少调色不错，体验也还行。 但是缺东缺西的，适配 skills 也是最慢的才弄好的，而且常常调用它 2.5-flash-lite 的去选择模型发任务的时候，竟然是 2.5-flash-lite 开始无限轮回，卡在那边不会动

- gemin cli是真不行，每次codex忙的时候让他干点复杂的就容易寄
  - codex是真可以，如果不是额度不够真的啥都直接交给他就行
  - 改改页面什么的确实gemini的审美还算能看

- gemini cli最好的用法就是2api出来做对话

- ## [使用同样的大模型，Claude code 、Google Gemini CLI、Qwen CLI 区别大吗 _202601](https://linux.do/t/topic/1443293)
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

- ## 

- ## 

- ## 

- ## [Does Oh-My-Opencode really provide an advantage? : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1q425mn/does_ohmyopencode_really_provide_an_advantage/)
- I tested it with a few feature implementations, in parallel with vanilla Opencode and Claude Code, and I didn't like how it performed. It used a ton more tokens and I didnt find the work any better. YMMV. I do have very detailed plans so maybe it negates some of what its supposed to bring

- I have similar observations — everything from ohmyopencode runs fast at first, but after 2–3 tasks the tokens are gone for 4 hours. I had the same issue with my own sub-agents (architect–builder–reviewer). The orchestrator rarely used the subtasks with cheaper models.
  - I’m starting to think that a simple plan/build setup with MCP for documentation and web search might actually solve things better and cheaper.

- Dude you are not wrong. I also tried it and I was being carless found out quickly that both my Opus, GLM and codex had downgraded ALOT from their respective original CLIS. The systemprompting in OH my Opencode is shit it is based on a bible of instructions and other weird rules LLMs in general should followi. And all this without any backup about evidence in LLM productivity. The models will become less intelligent unless you dont rewrite it all but theb you could just make your own setup.

- I think no. Most of the heavy lifting lies in the model capability itself nowadays. With just 200K context, doing extra fancy things just hurt the performance and gain you nothing but being rate limited imo. The Keep It Simple Stupid principle always stand.

- ## [OpenCode + OpenWebUi? : r/opencodeCLI _202511](https://www.reddit.com/r/opencodeCLI/comments/1oljb0k/opencode_openwebui/)
  - Is There a way to integrate opencode with a web interface instead of using it via TUI?

- Opencode has sdk to interact with opencode server. TUI actualy client of the server. So I think its possible to build web client for it

- You can use official desktop package
  - it’s also a web client

- ## [Codex in OpenCode : r/codex _202512](https://www.reddit.com/r/codex/comments/1pz5p2r/codex_in_opencode/)
- When comparing opencode with another tool, it's better to compare it with CC than codex, as a TUI. Because opencode is so ahead of codex in feature parity and trades blows with CC in QOL features. I use it as my daily driver and it has nearly all the features I want and if not, there are plugins. The automatic LSP and formatter integrations will save you a lot of compilation errors because the agent automatically gets the errors fed back to it when it makes syntax errors or similar, which is very valuable. Automatic formatting will make your code cleaner, the codex team have instructions in their AGENTS.md for how to run just fmt after every step to ensure formatting etc, this comes automatically in opencode, something that even CC doesn't have. They're now adding native LSP tools like symbol searching, renaming etc so soon the agent will not be globing and rg-ing its way around

- Would you say that after switching to using Codex in/with OpenCode you can’t see yourself using pure Codex Cli alone because it’s just better (an upgrade) to use OpenCode on top? 
  - I return to codex sometimes to just see what's up but their development is very slow in comparison with competitors and honestly opencode is the main cli tool that is very active, not vibe coding targeting, that's actually using good engineering in its making that's provider agnostic. Subagents are implemented via a native tool called task, it spawns a subagent that you can zoom in to see its context which is a better UX than CC. There's a built-in subagent for exploration, read-only. But you can create subagents as you want, also main agents are a thing, they're translated to modes that you can tab between. Slash commands can spawn subagents with extra context which is powerful if you want an agent that's focused and not polluted by your chat's context, that's the system for their review slash command. They added skills support lately which is awesome as well
- i just run multiple codex instances and then have them read and write to a md file or a database if they need ot memorize stuff....like all these things are super simple and dont require more complexity is my opinion.

- there are also people who love the simplicity of Codex

- I use both Codex CLI and OpenCode; OpenCode has some cool features (switching agents with different models and different briefings), sub-agents etc. I rarely use more than a planning agent and an edit agent in OpenCode; most of the time I just use Codex CLI TBH. I'm using OpenCode with the OAuth plugin to use my subscription which works very well.

- ## [coming as a CC user, what does OpenCode has that's got everyone raving about? : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1qa4h9e/coming_as_a_cc_user_what_does_opencode_has_thats/)
- While one of the biggest differences is that OpenCode not bind with models from one company. You can choose any models you want. Every agent can have its own model so you can choose the best model in different tasks

- No flickering.
  - Copy and paste works reliably.
  - LSP
  - Clear view of the task list.
  - Sub-agents from different providers for better self-checking.
  - It's faster.
  - Better content management.
- Copy and paste doesn't work for me at all in WSL lol. In CC it works fine though

- haven't used cc for a while, but really like the /undo OpenCode command that reverts last AI changes.
  - CC has /revert or double Esc for this
- I still wonder how many vibecoders don't know that git basically exists.
  - Using the same git for human and AI sucks. I want the main git to only record "verified" changes and a separate temporary history for all the random AI generated intermediate steps. I don't even want the agent to be able to modify the main git without permission. I think Roo code uses a "shadow git", which might be the better option.

- Lsp integration is nice

- flexibility with your workflow, you can set any model and customize it to any extent like max token window, thinking, etc there is so many settings good for nerds or newbs
  - fast support from the team, discord always active
  - most important of all, context management is superior compared to cc, output are better. i one shotted my real work tasks as RND in my company 95% of the times.

- Agents, scripts as tools for agents

- ## [Why is opencode so popular? : r/vibecoding _202601](https://www.reddit.com/r/vibecoding/comments/1qf0u10/why_is_opencode_so_popular/)
  - It looks cool, it can use literally any model, it's got plugins for providers, it's super customizable
  - But I'm struggling to get into it because:
  - There's no sandbox option
  - There are two primary agents by default in OpenCode. Build mode is basically yolo. It edits and runs commands freely with zero permission.

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
# discuss-qwen-code
- ## 

- ## 

- ## 
# discuss-gemini-cli
- ## 

- ## 

- ## [gemini-cli 太弱了 _202601](https://linux.do/t/topic/1476572)
  - 我个人很喜欢在终端上工作，所以也尝试了各种CLI。其中明显感觉gemini的这个CLI明明交互很好，整体UI看着也很舒服，但实际上一输出内容，经常就是不看上下文瞎编。。antigravity里就还好些
- 模型不同，Antigravity里面用的是opus

- 同感。有时候我感觉google他们家的ai coding领域的工具和理念自成一派，甚至会怀疑是不是自己不会用，怎么会这么难用。
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
