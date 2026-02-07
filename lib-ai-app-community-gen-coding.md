---
title: lib-ai-app-community-gen-coding
tags: [coding, community, large-language-model]
created: 2025-09-01T07:58:14.529Z
modified: 2025-09-01T07:58:29.058Z
---

# lib-ai-app-community-gen-coding

# guide

- tips
  - 🤔 模型选择: 不用纠结是否要用thinking/reasoning模型，参考成熟的方案来选架构和改进
    - thinking+coding(单模型方案) vs plan+coding(双模型方案), 可参考流行工具的默认值
  - 🤔 工具选择: 不必纠结于工具cline/aider, 模型能力提升后，工具里的体验也会自动提升
    - github copilot扩展开始支持本地model了
    - 甚至针对场景的微调模型，如ios/android, mobile-responsive
  - 🏠 continue.dev相对于cline/aider更擅长inline-autocomplete, 但架构设计可以参考rag/embedding/rerank

- dev-xp
  - ui细节问题有时难以向AI描述清楚, 复现场景、光标问题的细节如何让AI理解
  - 难以稳定复现的问题, ai也很难分析解决

- prompts-coding
  - https://github.com/tallesborges/agentic-system-prompts
    - A curated collection of system prompts and tool definitions from production AI coding agents

- leaderboard-pm
  - [LLM Rankings | OpenRouter](https://openrouter.ai/rankings?view=month)
# discuss-stars
- ## 

- ## 

- ## [System Prompts When Using Claude Code and Codex with Local Models : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qdcaol/system_prompts_when_using_claude_code_and_codex/)
  - Claude Code: 16.5K tokens
  - Codex: 6.5K tokens
  - Gemini-cli: 5.5K tokens
- the Claude Code prompt is absolutely massive - 16.5k tokens is like eating up a quarter of most local models' context before you even start coding
  - The smaller models probably just get confused trying to juggle all those instructions at once. Codex being shorter makes total sense why it works better, especially on something like qwen3-coder which is already pretty solid for its size

- Claude models are multimodal.
- Qwen3 Coder isn’t multimodal, so you should probably remove the multimodal stuff from the system prompt before you use Qwen3 coder with it. (PDF & Image related file formats and capabilities)

- ## [Agentic coding tools with smaller system prompts? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mu6a9s/agentic_coding_tools_with_smaller_system_prompts/)
  - The problem is, all the tools I listed above start out pretty snappy, but get slow after just a few questions. I'm pretty sure this is because of the prompt that each of these tools sends along with each user message -- it's gigantic, includes e.g. the full definition of every tool available to the LLM with several examples each, etc. This fills up the context quickly and I think is why it gets slow.
  - has anyone done any exploration into a "lite" mode for these tools or something, such that that can be functional without enormous context?
  - 💡: 可以尝试手动压缩context, 可以尝试实现claude-code最近开始用的 tool-search/skill(不将tool描述放入context)

- Any coding agent require a lot of context because they need to read many chunks of the project to understand how and where to implement something or make changes, the easiest solution for this is start a new chat after a correct implementation, this can also benefit the output quality.
  - Other thing you can do if not already doing is use flash attention and kv cache quantization.
  - About the agents, from my experience, Kilo Code is the most efficient agent in terms of context
  - Roo Code is very hangry on context but has a function to `compress` when you are getting close from the limit, this helps a lot when you dont have memory for more than ~32k context

- ### [I created a coding tool that produce prompts simple enough for smaller, local models : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p3qxj4/i_created_a_coding_tool_that_produce_prompts/)
  - This design choice makes messages very simple, as all the model sees are hand-picked files and simple instructions. In the example above, I didn't have to tell the model I wanted to edit "checkpoints" feature, as this is the only feature attached in context.
  - This simple approach makes it fully viable to code with smaller, locally hosted models like Qwen 32B.
- https://github.com/robertpiosik/CodeWebChat /GPL/202601/ts
  - open-source AI coding toolkit. You can use CWC in VS Code family of editors (Cursor, Antigravity, VSCodium etc.) for a much faster and cost efficient* development experience.
  - Apply responses—interactive edits integration with checkpoints for state restoration
  - Fully-featured—code completions, commit messages, checkpoints, skills, and more
  - zero-overhead prompts optimized for prompt caching
  - 100% local operation

- Glad it works with VSCodium too.

- Is this for modifying existing code in your own repo or for creating new functions by prompt suggestion? It’s not really clear what this is intended to accomplish?
  - It edits selected files in context based on instructions. It always sends only one message, multi-file edits are handled by parsing code blocks from a single response.
- Regarding seeing response during generation, you can use command "Toggle Developer Tools" and go to Console. I think I can add streamed response preview to the bottom pane.

- Well it's equally good for big models too, in my experience senior devs rarely use agentic coding and tend to delegate single-context oneshot tasks to ai. So this is useful.

- ## 🆚 [Testing LLM ability to port code - Comparison and Evaluation : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q1fo4p/testing_llm_ability_to_port_code_comparison_and/)
  - prompt:
  - Please port this short program to [insert language here]. The resulting program must have identical behavior (including bugs and unusual behavior). That is, given identical input, it should produce identical output. The rewrite cannot use any 3rd party libraries, but can incorporate any idiomatic changes (including from the standard library) that would make it more "natural" or performant in the target language. The original JS program is executed using the Bun runtime.

- For those wanting something more graphical.
  - Looks like C++ was the easiest language to target, with Haskell being the hardest (well, except for Oberon7). 
  - Python got close a few times but stack issues kept it from passing. 
  - I went back and looked over some of the reasoning output and it's strange - DeepSeek noticed that the stack would be a problem, but assumed that since it worked fine in JS, it should work in Python as well since neither have TCO. It then mentioned that I ran it in Bun, but went forward with a recursive solution. I asked it separately if Bun had TCO and it said that it did (but that Node and Deno do not - correct on all three). So it should have changed this into a regular loop. But did not.
  - K2 was the most consistent in changing the recursion to a loop (handling that in both Python and Rust but leaving it in C++ where the compiler should implement TCO on something so simple).

- Have it write unit tests based on the code in the new language, and a spec, THEN code.

- That's why vibed code creates a bunch of technical debt landmines waiting for the next bunch of devs to step on. You can get a program that runs but there could be insidious logic errors that slip by.

- ## [is GTX 3090 24GB GDDR6 good for local coding? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o11udk/is_gtx_3090_24gb_gddr6_good_for_local_coding/)
- Local models are nowhere near the performance of top-tier closed-source models. And even the best local ones (eg GLM-4.5/4.6) are too big to be hosted locally at reasonable speeds. So no, a 3090 is definitely a bad investment if the goal is to replace Codex-CLI.

- I have a 5090 and i mostly use qwen coder 30b almost everyday. It's realy capable model but with my gpu i am using 110k context and i can't go above that. For coding i think minimum around 50k context length you gonna need. So i don't know.maybe you can get smaller quant.but from my exprience even 4bit is not enough for coding.

- 3090 24GB is highly versatile. Especially if you have at least 128 GB system RAM or even 256 GB and it's DDR5. You can run coding models such as qwen 3 30B A3B coder on the 3090 at 4-bit quant with high context and high speed. Or OSS 20B or devstral 24B etc. But other coding models are larger MoE so would spill into system RAM and consequently be far slower.

- ## [My experience trying out coding agents -- Qwen2.5-coder-tools/Sonnet 3.5 on Cline and Github Copilot agent mode : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ilza8m/my_experience_trying_out_coding_agents/)
  - trying out the preview copilot agent feature against cline using both a specialized version of Qwen2.5 through Cline and the Sonnet 3.5 (copilot API) through Cline and copilot

- For aider at least, benchmarks show the absolute best way to use it is with a reasoning model like r1 as the architect and sonnet 3.5 as the coder. Curious to see if that helps you and jumps over the usefulness / competency barrier for your usecase. 
  - Just `aider --architect --model r1 --editor-model sonnet` should work after configuring relevant APIs, I think?

- This is my exact experience, I have spend over 100 usd on API fees through OpenRouter, OpenAI and Deepseek and tried many models with both Cline and Roocode and you really get various results. Sometimes you can end up in endless loops trying to solve a problem no matter how many times you start a new task with the same LLM then you switch to another LLM and you can get past that point or you get a situation where it wants to go on another totally different tangent. Ive had similar issues with local LLMs and even still have issues with them even working with Roocode and Cline. Ive even tried Bolt.diy which is a fork of Bolt.new, similar issues. Ive started writing my own coder to hopefully solve a few of my concerns but its likely we will end up with the same issues.

- I’ve been having similar issues with all local models. I’m using Qwen-2.5-coder 7B on MacBook M3 Pro and I’ve come to the conclusion that Cline’s context size is too large to be performant. I use the same model with Continue.dev and everything works quickly.
# discuss-ai-coding-internals
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Using LLMs for Code Generation: A Guide to Improving Accuracy and Addressing Common Issues _202508](https://www.prompthub.us/blog/using-llms-for-code-generation-a-guide-to-improving-accuracy-and-addressing-common-issues)
- Some of the most common problems are:
  - Logical Errors: LLMs often misinterpret the logical requirements of a task, leading to incorrect or nonsensical code behavior.
  - Incomplete Code: Important sections of code can be left out
  - Misunderstanding Context: Models may fail to grasp the full context of the prompt, causing them to generate code that doesn't align with the intended use

- ## 📌 [Yek: Serialize your code repo (or part of it) to feed into any LLM | Hacker News _202501](https://news.ycombinator.com/item?id=42753302)
- There are a lot of them. I collected a list of cli tools that does this: https://prompt.16x.engineer/cli-tools

- Here is a benchmark comparing it to [Repomix] serializing the Next.js project
- Maybe I don't understand the usecase but I'm curious why speed matters given that LLMs are so slow (?)

- you might be interested in seeing how tools like Aider do their "repo serializing" (they call it a repomap), which tries to be more intelligent by only including "important lines" (like function definitions but not bodies).

- i guess I shouldn’t be surprised that many of us have approached this in different ways. it’s neat to see already multiple replies of the sort I’m going to make too, which is to share the approach I’ve been taking, which is to concatenate or to “summarize” the code, with particular attention on dependency resolution. [chimeracat](https://github.com/scottvr/chimeracat)

- Adding my take to the mix, which has been working well for me: https://github.com/ClaireGSB/project-context.
  - It outputs both a file tree of your repo, a list of the dependancies, and a select list of files you want to include in your prompt for the LLM, in a single xml file. 

- How does this compare to a tool like RepoPrompt? https://repoprompt.com

- https://github.com/simonw/files-to-prompt/ seems to work fine especially for Claude as it follows the recommendations and format.

- There is also https://repo2txt.simplebasedomain.com/local.html which doesn't require to download anything

- I have to add https://github.com/simonw/files-to-prompt as a marker guid.

- Like many people, I built something similar, llmctx, but the chunking feature seems really interesting, I have to look into that for llmctx.

- i wrote something similar https://github.com/dwrtz/sink

- You can do this all in the browser: https://dropnread.io/

- https://gitingest.com/

- ## 🆚🏠 [why does cline not apply multiple agent approach? : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mtnwgp/why_does_cline_not_apply_multiple_agent_approach/)
  - Roo has default 5 agents, and has more agents in mode market, including code techear and document writer, that's cool when the modes are managed by orchestrator.
  - why does cline not take this way?

- This approach is a key difference from Roo. Personally, I operate in a plan/act mode, whether for feature development, debugging, or writing documentation.

- all the additional prompting can even create conflicts and reduce performance

- they're just different system prompts. you could switch your active rules files and get most of the way there. 

- ## [RooFlow, RooCommander, SPARC, etc. What frameworks are you still using? : r/RooCode _202508](https://www.reddit.com/r/RooCode/comments/1mz96of/rooflow_roocommander_sparc_etc_what_frameworks/)
  - A few months ago there was an explosion of frameworks coming out to improve RooCode - RooFlow, RooCommander, SPARC, etc. 
- I tried some of them, but then I realized I didn't need them.
  - Same, the native functionality (modes, to do lists etc) plus the models became a lot better so there is much less need for the (well appreciated!) bandages.
  - Nevertheless, sometimes I still take inspiration from it for a workflow or way of documenting. Orchestrator is good, but it very quickly goes to coder instead of researcher etc. Think before you do could be personal preference.

- I just use plain roo.. but only because I don’t need more (yet). Would be nice if there were presets for different tech stacks, like coder-node-react or coder-cplus coder-serverless etc. as I’m sure things for me would be smoother if I took the time to add guardrails around the stacks I’m using

- SPARC enabled me to do one complex project and taught me so much about system architecture/design. That being said, now that I developed my own understanding of how to architect, I no longer need it.
# discuss-coding-tools/tricks
- ## 

- ## 

- ## 

- ## 

- ## 🤔 I've used AI to write 100% of my code for 1+ year as an engineer. 13 no-bs lessons
- https://www.reddit.com/r/ClaudeCode/comments/1qxvobt/ive_used_ai_to_write_100_of_my_code_for_1_year_as/
  - 1 year ago I posted "12 lessons from 100% AI-generated code" that hit 1M+ views. Some of those points evolved into agents.md, claude.md, plan mode, and context7 MCP. This is the 2026 version, learned from shipping products to production.
1- The first few thousand lines determine everything

When I start a new project, I obsess over getting the process, guidelines, and guardrails right from the start. Whenever something is being done for the first time, I make sure it's done clean. Those early patterns are what the agent replicates across the next 100, 000+ lines. Get it wrong early and the whole project turns to garbage.

2- Parallel agents, zero chaos

I set up the process and guardrails so well that I unlock a superpower. Running multiple agents in parallel while everything stays on track. This is only possible because I nail point 1.

3- AI is a force multiplier in whatever direction you're already going

If your codebase is clean, AI makes it cleaner and faster. If it's a mess, AI makes it messier faster. The temporary dopamine hit from shipping with AI agents makes you blind. You think you're going fast, but zoom out and you actually go slower because of constant refactors from technical debt ignored early.

4- The 1-shot prompt test

One of my signals for project health: when I want to do something, I should be able to do it in 1 shot. If I can't, either the code is becoming a mess, I don't understand some part of the system well enough to craft a good prompt, or the problem is too big to tackle all at once and needs breaking down.

5- Technical vs non-technical AI coding

There's a big difference between technical and non-technical people using AI to build production apps. Engineers who built projects before AI know what to watch out for and can detect when things go sideways. Non-technical people can't. Architecture, system design, security, and infra decisions will bite them later.

6- AI didn't speed up all steps equally

Most people think AI accelerated every part of programming the same way. It didn't. For example, choosing the right framework, dependencies, or database schema, the foundation everything else is built on, can't be done by giving your agent a one-liner prompt. These decisions deserve more time than adding a feature.

7- Complex agent setups suck

Fancy agents with multiple roles and a ton of .md files? Doesn't work well in practice. Simplicity always wins.

8- Agent experience is a priority

Treat the agent workflow itself as something worth investing in. Monitor how the agent is using your codebase. Optimize the process iteratively over time.

9- Own your prompts, own your workflow

I don't like to copy-paste some skill/command or install a plugin and use it as a black box. I always change and modify based on my workflow and things I notice while building.

10- Process alignment becomes critical in teams

Doing this as part of a team is harder than doing it yourself. It becomes critical that all members follow the same process and share updates to the process together.

11- AI code is not optimized by default

AI-generated code is not optimized for security, performance, or scalability by default. You have to explicitly ask for it and verify it yourself.

12- Check git diff for critical logic

When you can't afford to make a mistake or have hard-to-test apps with bigger test cycles, review the git diff. For example, the agent might use created_at as a fallback for birth_date. You won't catch that with just testing if it works or not.

13- You don't need an LLM call to calculate 1+1

It amazes me how people default to LLM calls when you can do it in a simple, free, and deterministic function. But then we're not "AI-driven" right?

- 👥

- one lesson i would add from my own year of 100% AI code: invest heavily in your test suite early. the AI is incredible at generating code but mediocre at verifying correctness. having a solid test framework means you catch regressions immediately when the AI makes a change. i treat my test suite as the source of truth and the generated code as disposable.

- Nice write-up and I agree with almost all of it. #7 I feel that multiple agents with a single task/role is a must. Multiple checks with different roles are more likely to produce quality code than a single agent with multiple roles.

- ## AI Coding：我从传统的单元测试全面迁移到 BDD（行为驱动测试）上了，让 AI 写 BDD 测试。
- https://x.com/waylybaye/status/2018890382462087348
  - 因为 BDD 的测试结果更可读，很容易验收 AI 的代码。比如我下面截图，一眼就能看出来 AI 是否完成了需求。
  - BDD 不只是集成测试或 E2E 测试，单元测试采用面向行为的描述也是 BDD。BDD 关注点在行为而非实现。核心区别是交付视角的变化：
  - TDD 侧重验证逻辑，交付的是代码，测试是代码正确的证明。
  - BDD 侧重验证需求，交付的是行为证明，代码是实现行为的赠品。

- 
- 

- https://x.com/geniusvczh/status/2018997878153523704
  - 专门学习了一下BDD，感觉就是user story / 从需求导出测试 / 敏捷开发那一套换个语言重新说了一遍，最后弄出来一堆e2e test。不过众所周知，e2e只能解决一小部分的bug，因为相同的覆盖下，他膨胀的速度比unit test快太多，而unit test膨胀的速度也比编译期验证快太多，成本太高
- 90% 单元测试 + 10% BDD(主要流程)，目前挺好的。
- 用 AI 去修 e2e test 的问题，然后涌现出更多问题

- ## For really complex work, AI writes thousands of lines of working code within an hour
- https://x.com/flybayer/status/2007487747469054228
  - But then I spend 1-3 days to fully understand, prompt deep refactors, improve end user UX, and ensure all edge cases are working and tested. 
  - That’s even after crafting a long, detailed plan document at the start. Because with complex stuff, you can’t foresee and address everything up front. 
  - A lot of times this is foundational stuff that is critical to get right in order to not cripple your future self.

- this is a hard, underdiscussed problem. especially if you're doing something that there isn't great prior art in your existing codebase.
  - at best i've found that AI handling the work at the LoC-level makes it easier to think deeply about design questions

- I’ve started running some parallel during refactor phase that are working on different parts

- once you get good scaffolding set up it gets much, much easier. 

- ## dhh: I had no idea that local model dictation had gotten this good and this fast
- https://x.com/dhh/status/2007498242561593535
  - I'm blown away by how good hyprwhspr with Omarchy is just using a base model backed by the CPU. Unbelievably accurate.
  - This is on my Framework desktop. It's a pretty powerful CPU (not even using the GPU!). I need to test it on lesser machines and see if it works as well. But I'd be surprised if it's still not quite good.
- Why not the AMD hardware acceleration for the speech to text model? I use hyprwispr for a week now, with the AMD hardware on Framework Desktop, works great
  - I tried rocm version first. Seemed slower? I don't think rocm is great on Strix Point yet. But it also just didn't seem to matter. From the CPU alone, I'm getting what seems like 100ms dication.

- ## 🌰 dhh--ruby: You can't let the slop and cringe deny you the wonder of AI. This is the most exciting thing we've made computers do since we connected them to the internet. _202601
- https://x.com/dhh/status/2007503687745490976
  - If you spent 2025 being pessimistic or skeptical on AI, why not give the start of 2026 a try with optimism and curiosity?
  - Just this past summer, I spoke with @lexfridman about not letting AI write any code directly, but it turns out half the resistance was simply that the models weren't good enough yet! I spent more time rewriting what it wrote than if I'd done it from scratch. That has now flipped.
  - I still write plenty of code by hand. Both out of necessity (the models aren't hitting what I want) and out of joy (writing code is fun!), but I've embraced the idea that getting a good draft really does speed things up quite often.

- AI promised to cure cancer and create new forms of energy. But all we got is will smith eating spaghetti, undressed kids and a bunch of halucinated false information. And all this comes at a very high price for the average Joe, who no longer can afford a computer

- ## 🌰 vczh: 我对macos的objc++ GUI程序开发基本是一无所知的，但是借助opus 4.5，不做任何context/prompt engineering，他自己吭哧吭哧就给我把之前整了一半的移植工作给搞定了，更新到了GacUI的最新版。_202601
- https://x.com/geniusvczh/status/2007443230481059954
  - 现在hello world已经跑起来了，我还没测试FullControlTest。opus 4.5太强了
- Opus 之所以能搞定 ObjC++，核心在于它正确理解了 .mm 文件中 C++ RAII 和 Objective-C ARC（自动引用计数）的混合内存管理模型。但对于 GacUI 这种自绘引擎，真正的隐形坑在于 RunLoop 的桥接。建议检查一下生成的代码是否正确将 GacUI 的 Message Pump 挂载到了 NSRunLoop 的 observer 回调里，否则一旦窗口失去焦点或者进入模态对话框（Modal Loop），整个 UI 线程很容易死锁。
  - 没仔细看，不过这部分应该是以前就解决了的，毕竟上一个能跑的macos版本就在GacUI 1.0，当时已经是这样了。后面我编译FullControlTest demo的时候会把所有功能再试一遍 

- 真香定律

- 

- ## 最近走通了三种并行开发的方式：
- https://x.com/leeoxiang/status/1990040466486911031
  - 1、本地开多个 worktree，每个 worktree 分配一个 agent，最后生成一个 PR; 
  - 2、远程开多个环境，每个环境一个 session，每个 session 的产出会生成一个 PR; 
  - 3、在 github 中每个 issue 启动一个 workflow 启动一个 claude code 进行异步开发。

- 佩服大佬，我到现在都仍然坚持古法单线程 copilot 式用 agent

- 不行，太伤神了。我尝试过 5 开(A 机 3 后端 session B 机 2 前端 session) 本地配好 gitlab cli 直接让 cc 从上面领任务，然后都配了 MCP feedback 增强的那个工具，一个任务完了或者有问题都必须弹窗提醒我，于是 duangduangduang，仅一天我就被干成贤者了

- ## 认同这个CLAUDE md 实践，就两条：
- https://x.com/9hills/status/1995308023578042844
  - 1. 保持简短（不超过60行）
  - 2. 将复杂的指令放到单独目录下，然后在 CLAUDE md 中增加索引（类似于 SKILL 的概念）

- 第三条：不要用 /init
  - 要分语言吧

- ## [Does anyone use spec-driven development? : r/ChatGPTCoding _202511](https://www.reddit.com/r/ChatGPTCoding/comments/1otf3xc/does_anyone_use_specdriven_development/)
- Yes, this has been my approach since May-ish. You have to review and adjust, though. You can't just generate a spec and then copy/paste without looking at anything.

- Yes, people who build software for a living have long realized having requirements before you start is helpful. Same with things like testing, intentional design of data schemas, and more. 

- ## [What's the best way to get the most out of LLMs for "vibe coding"? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n8kadm/whats_the_best_way_to_get_the_most_out_of_llms/)
- I like creating a product requirement document and then use AI to expand, analyse and refine it ( 2 or 3 rounds, using diferent llms) and  creating a file with a list of tasks/functions that need to be coded to create the script. After that i ask them to implement a task and review the code

- Add one feature per chat.
  - But you should really use an IDE with an agentic coding assistant, since copy-pasting code from one chat to another wastes a lot of time. This will also provide static analysis to catch basic code errors your or the AI might introduce.
  - Also, (learn to) use git for version control. Some of the AI extensions will even write commit messages for you so no thinking is required.

- You could have ChatGPT make a proof of concept script, with the functions you need and some suggestions. Then you could use VSCode with a free Gemini API to refine and debug. When it starts forgetting stuff just restart the conversation and tell it what files to use as context. Just remember to save your versions because it will break stuff.

- The problem you're describing is super common - ChatGPT "forgets" parts of your script as the conversation gets longer because it's literally running out of memory space. I'd suggest you try out Kilo Code in VS Code (disclaimer: I'm working with their team). Its memory bank learns your patterns and preferences over time, so it remembers how you like to structure projects. Way cleaner than going back and forth for hours trying to keep everything in one conversation thread.

- ## [How to tell cline must use recent documentation for a python lib? : r/CLine](https://www.reddit.com/r/CLine/comments/1nw95t9/how_to_tell_cline_must_use_recent_documentation/)
- The context7 MCP server is tailored made for this.
  - Add context7 mcp. Then add a global rule to fetch lastest docs before planning.

- Create your own documentation and put it in a docs folder. And then @ the file in your prompt. EZPZ

- is it going to create a rag or context injection?
  - Just context injection.

- ## [I tried vibe coding for 4 weeks, here’s why I’m dialing it back : r/vibecoding](https://www.reddit.com/r/vibecoding/comments/1nu8s3y/i_tried_vibe_coding_for_4_weeks_heres_why_im/)
  - And honestly? The first week felt incredible. I was in the zone, shipping features fast, and it felt like I was finaly coding for fun again.
  - But as the weeks went on, the cracks started to show.
- The Upside:
  - Super fast for prototyping.
  - Way less friction to just start building.
  - It did bring back that “hacking for fun” feeling.
- The Downside:
  - Code chaos: By week 3, I had no idea why certain functions worked or if they’d break something else.
  - Debuging nightmare: AI suggestions + zero structure = hours wasted chasing sily bugs.
  - Feature whiplash: I kept adding things randomly, which meant ripping out work a few days later.
  - Momentum drop: Without a roadmap, I started losing motivation once the shiny feeling wore off.
- What I Learned:
  - Vibe coding is amazing for exploration and quick hacks.
  - But if you actually want to scale a project, you need at least some structure (docs, tests, basic planning).
  - For me, the balance is: vibe code the prototype → switch to structured dev once the core idea works.
- So yeah… vibe coding was fun, but I don’t think I could rely on it for anything bigger than a proof of concept.

- Who said you should vibe code without a roadmap ?

- ## 🤔 [Hot take: ALL Coding tools are bullsh\*t : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nu6kjc/hot_take_all_coding_tools_are_bullsht/)
- We have these incredible language models—DeepSeek 3.2, GLM-4.5, Qwen 3 Coder—that can understand complex problems, reason through edge cases, and generate genuinely good code. And what did we do? We wrapped them in so many layers of bullshit that they can barely function.
- The Scam: Every coding tool follows the same playbook:
  - Inject a 20, 000 token system prompt explaining how to use tools
  - Add tool-calling ceremonies for every filesystem operation
  - Send timezone, task lists, environment info with EVERY request
  - Read the same files over and over and over
  - Make tiny edits one at a time
  - Re-read everything to "verify"
  - Repeat until you've burned 50, 000 tokens
  - And then they market this as "agentic" and "autonomous" and charge you $20/month.
- The Reality:
  - The model spends 70% of its context window reading procedural garbage it's already seen five times. It's not thinking about your problem—it's playing filesystem navigator. It's not reasoning deeply—it's pattern matching through the noise because it's cognitively exhausted.
  - You ask it to fix a bug. It reads the file (3k tokens). Checks the timezone (why?). Reviews the task list (who asked?). Makes a one-line change. Reads the file AGAIN to verify. Runs a command. Reads the output. And somehow the bug still isn't fixed because the model never had enough clean context to actually understand the problem.
- The Insanity:
  - What you can accomplish in 15, 000 tokens with a direct conversation—problem explained, context provided, complete solution generated—these tools spread across 50, 000 tokens of redundant slop.
  - And the worst part? It gives worse results. The solutions are half-assed because the model is working with a fraction of its actual reasoning capacity. Everything else is burned on ceremonial bullshit.
- The Market Dynamics:
  - VCs threw millions at "AI coding agents." Companies rushed to ship agentic frameworks. Everyone wanted to be the "autonomous" solution. So they added more tools, more features, more automation.
  - They optimized for demos, not for actual utility. Because in a demo, watching the tool "autonomously" read files and run commands looks impressive. In reality, you're paying 3x the API costs for 0.5x the quality.
- The Simple Truth:
  - Just upload your fucking files to a local chat interface like LobeHub (Open Source). Explain the problem. Let the model think. Get your code in one artifact. Copy it. Done.
  - No tool ceremonies. No context pollution. No reading the same file seven times. No timezone updates nobody asked for.
  - The model's full intelligence goes toward your problem, not toward navigating a filesystem through an API. You get better code, faster, for less money.
- The Irony:
  - We spent decades making programming languages more expressive so humans could think at a higher level. Then we built AI that can understand natural language and reason about complex systems.
  - And then we forced it back down into the machine-level bullsh*t of "read file, edit line 47, write file, run command, read output."
  - We took reasoning engines and turned them into glorified bash scripts.
- The Future:
  - I hope we look back at this era and laugh. The "agentic coding tool" phase where everyone was convinced that more automation meant better results. Where we drowned AI in context pollution and called it progress.
  - The tools that will win aren't the ones with the most features or the most autonomy. They're the ones that get out of the model's way and let it do what it's actually good at: thinking.
  - Until then, I'll be over here using the chat interface like a sane person, getting better results for less money, while the rest of you pay for the privilege of context r*pe.

- Can you share the prompt & model used to generate this post? thxbye

- that's exactly what aider is doing. So there is one coding tool that is not bullshit?
- It doesn't have any tools and repo map is disabled with a single argument. 2k tokens for system prompt is nothing for modern models. However tool calling agentic tools are still more minimal then this because they can break down task into smaller steps and solve them separately in new context not connected to initial one.

- Qwen code (free 2000 api) has been an extremely valuable cli agent that I've been using geting it to do desktop tasks fast and raw. Its cost vs a human person per hour is still cheaper when you know the scope of the task. How big of a code base are you using that copy pasting is sufficient and all in a single file? Seems like you are a very basic end user or doing things with limited scope putting an entire framework into one file.

- models are stateless, so you are sending all initial context plus sliding context on each request. optimization can happen if it can output a summarized context that is still relevant for the next request.

- Integration at the IDE level allows the LLM to go find these links itself rather than putting the onus on you. It saves time.

- ## [Sometimes I feel like Architecture mode is a waste of tokens. Am I using it wrong? : r/RooCode _202509](https://www.reddit.com/r/RooCode/comments/1nmsu61/sometimes_i_feel_like_architecture_mode_is_a/)
  - I've seen many people saying how architecture mode is a life saver and it does wonders, however in my experience it hasn't yielded much results, here's why:
  - I generally do small incremental development steps. For example: 1- build the database schema, 2 - build the seed, 3- use the schema to builde api endpoints, etc. etc..
  - I feel like Architecture mode is great if you're trying to one-shot a small app with a not very detailed prompt. It designs the whole thing and then you switch to coding mode to build it. However the adjustment and debugging later is massive. Incrementally just ask for coding has made more sense to me so far.
  - Am I doing this wrong? How do you guys use architecture mode in your workflows to get good results?

- I've used it to build documentation if I'm writing a markdown file. But typically, I just go and use the ask mode.

- ## [Do local LLMs do almost as well with code generation as the big boys? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1naiud3/do_local_llms_do_almost_as_well_with_code/)
- You can run qwen 3 coder with 512GB M3 ultra easily.
  - Not the 480 though I dont think. Read and a few responses indicate that + context would need about 1TB of ram.
- The best model that's open source right now i think is still Qwen 3 Coder 480B; in my experience it codes pretty close to Sonnet 4 after having used both pretty extensively. But you're going to want it in 16-bit which would need about 1TB just to load. 

- Coding may be more sensitive, but anything above q6 is not really noticeable. 
  - Some of the best models are trained at q8 such as DeepSeek, Kimi and GLM 4.5. GPT OSS is 4 bit natively. I use gpt oss 120b every day for coding and I run it local. 
  - FP16 is for training. It has no place in inference.

- Absolute not. I have a Mac M3 Ultra 512gb, and it can run Kimi, Qwen480, Deepseek, GLM 4.5... but the thing most people don't understand is if you try and feed it a prompt with 100k tokens it's going to take 5-10 minutes just to process that, even if you get 20 t/s after that.
  - It's basically unusable for coding (which often times requires many prompts of larger context).

- ## [Is there a way to use 2 models at once? Deepcoder nor phi-4 doesn't generate use tool available to it's disposal just tells user what to do. Like an interpretation model. : r/RooCode _202504](https://www.reddit.com/r/RooCode/comments/1k936cu/is_there_a_way_to_use_2_models_at_once_deepcoder/)
- A lot of models don't do tool calling natively. 
- Try Qwen2.5-Coder 14b can do

- ## 🤔 [getting lost in the speed of model updates. What is best for the planning phase, what is best for the coding phase : r/CLine _202502](https://www.reddit.com/r/CLine/comments/1iji10g/getting_lost_in_the_speed_of_model_updates_what/)
- Here’s an Aider blog post making the rounds stating that R1 for Architect and Sonnet for Editor (roughly equivalent to Cline’s Plan/Act I believe) is their new SOTA for their polyglot benchmark.
  - [R1+Sonnet set SOTA on aider’s polyglot benchmark | aider _202501](https://aider.chat/2025/01/24/r1-sonnet.html)

- A common pattern is:
  - DeepSeek R1 for Planning (R1 is a reasoning model)
  - 3.5 Sonnet for Acting (3.5 Sonnet is best coder)
  - DeepSeek V3 is also solid for coding

- Reasoning model to architect the solution, standard/cheaper model for execution

- TLDR: For cost efficiency: I would use R1 for the architect and whatever the best Gemini model is for coding as the editor

- ## [Which model combinations have you tried for the best performance (also cost rationally) in Plan and Act mode, especially working with memory bank in a large project? : r/CLine _202503](https://www.reddit.com/r/CLine/comments/1j8e7ji/which_model_combinations_have_you_tried_for_the/)
- If you're looking at the Aider LLM Benchmarks for coding stuff, the best value for tricky coding tasks right now is using DeepSeek R1 for plan-mode and Claude 3.5 Sonnet for act-mode. If you're doing something simpler, DeepSeek Chat V3 is a cheaper option.

- I've been using Gemini 2.0 flash for planning/architecture and then implementation with Claude 3.5 sonnet. I don't really know if I get better results than with deepseek, but I had so much waiting time with deepseek r1 it was practically unusable. 

- I see a lot of people advocating for using Claude for act mode and another llm to plan. The issue I have with this is that the plan stage uses a relatively small amount of tokens compared to act, so you aren't really saving much money relative to using Claude for everything.

- ## [Is Plan / Act Conceptually Broken or am I using it wrong? : r/CLine _202503](https://www.reddit.com/r/CLine/comments/1jd9nuf/is_plan_act_conceptually_broken_or_am_i_using_it/)
  - I really liked the idea of Plan and Act modes, especially using a cheap model (R1) for planning and reserving premium model (Sonnet) for Act mode, however......
  - by having these two modes in the same chat and switching between them you end up carrying massive amounts of context/message history (which was cheap to accumulate with planning model) into your messages with your 'Acting' model, and the costs suddenly jump up for every message.
  - if you were providing the Act mode with an actual plan it shouldn't need all that historical context, it should be given something far more distilled, with just enough context to complete the task you are asking of it
  - I think theres great potential in this plan/act division but I think its currently not modelled correctly in Cline - I guess Im essentially suggesting this should be 2 agents instead of 1..... with the 'Act' agent able to feed back to the 'Plan' agent and ask for more info etc.

- I think you might be using it backwards. You're supposed to use a smarter model to do planning and then pass that plan to a smaller model to execute.
  - I experimented this weekend switching back and forth between a cheaper model and a more expensive model for act and plan. I think the current version of Cline needs some tuning still.
  - The feature is going to save a lot of cost once it's dialed in. But right now I've found doing it manually gets great results.

- Not a smarter model. A reasoning model. R1 architect and Claude coding is top of the list in terms of price/performance and is very close to the top in pure performance

- In times when you use prompt caching, it makes little sense to use different models in my opinion. But yes, use the best model for planning

- act mode shares the cache from plan mode, it preloads the plan (you can test this by having a chat with plan mode, switch to act and asking it what it knows about xyz)
  - So all you do is get the best language model for your task (aka Opus for coding) to explain to you a plan, how to implement, best implementation principles, and examples of code etc.
  - then switch to Act where you're using a cheaper model, and tell it do the thing. this way you will get the claude-3-5-haiku-20241022 model to make some surprisingly acceptable code for peanuts.

- Plan, chat with it until you happy then save to MD. Load MD in act and do the job.
  - You can extend this with Roo, it has sub tasks which run in separate context and return result to main task
  - Subtasks are not silver bullet but its very handy addition

- Can Cline write to Memory Bank without going into Act mode?
  - Yes it can. Its md files
  - We save it in MD so we can reset context and you can edit it a bit before running code/act mode

- I don’t switch back and forth. Just Plan once, the act until the task is done. You can give it feedback in act. I use Somnet for both, because the cost isn’t more than paying someone else to do it.

- ## [Strategy for Coding : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1nf8o7d/strategy_for_coding/)
  - Qwen 3 Coder can benefit from the thinking output of another model. If you copy/paste your prompt and the thinking output from something like Qwen 3 Thinking, it seems to perform better than simply giving either the prompt alone.

- Wonder if you could fake it in the prompt by asking Coder to write a document discussing the problem and creating a to do list before anything else
  - sorta but it's not as good as actually using another qwen. the other qwen doesn't even have to be that big

- I guess you're not using a tool like Cline where you enter into Plan or Act mode.
  - Plan mode lets you chat to the LLM (I prefer a thinking one instead of instruct) about the requirements. During this mode, it can ask to look at files in the project to generate a better plan. The final part of Plan Mode is asking the User if they want to proceed with the generated plan and enter Act Mode.
  - In Act Mode, will perform creating files, updating files, deleting. And can also run/validate the code if you configure your rules properly.
  - Another cool thing about cline is you can actually have two different LLMs for the Plan and Act modes. In Plan mode, i'll leverage Qwen3 4B thinking for rapid back and forth on the requirements. Then when Act mode is enabled, use Qwen3 Coder 30B A3B to consume the plan and do the work.

- ## [What is your system prompt for Qwen-2.5 Coder 32B Instruct : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gqagzg/what_is_your_system_prompt_for_qwen25_coder_32b/)
- Start your system prompt with You are Qwen, created by Alibaba Cloud. You are a helpful assistant. - and write anything you want after that. Looks like model is underperforming without this first line.

- for the 7B version, my Qwen coder suddenly started working better with LM Studio blank preset. Increased the context length, lowered temperature to 0.2, works great.
  - any system prompt made the generation worse. That said, any errors in prompt seem to break something, but that's probably the 7B model only.

- ## [What do you use on 12GB vram? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nd1tqf/what_do_you_use_on_12gb_vram/)
- Qwen3-coder-30B, qwen3-30b, gpt-oss-20b - you can keep the KV cache on GPU and offload MOE layers to CPU, and it will work reasonably fast on most modern systems.
- And you can bring some of those MOE layers back to GPU to really fill out the VRAM, which will also provide a great boost overall. 
  - Don't forget the `--batch-size` and `--ubatch-size` , make those 2048 or even bigger, which will provide much faster prompt processing but at additional VRAM cost which may require a compromise in context size, depending on what's most important. 
  - I have a machine with 11GB VRAM and I can get it to about 65k context with 2048 ubatch/batch size for Qwen30b MOE. I get about 600 t/s PP and maybe like 15t/s generation, which isn't bad at all. I kept all MOE layers on CPU to get that context and ubatch up though.

- ## [Just bought an M4-Pro MacBook Pro (48 GB unified RAM) and tested Qwen3-coder (30B). Any tips to squeeze max performance locally? : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1naqdl5/just_bought_an_m4pro_macbook_pro_48_gb_unified/)
- I use mlx with lm-studio. Look for DWQ mlx quants for best quality. Mlx will always be faster than a comparable gguf quant because it is native metal framework.

- You might want to try the unsloth fine tune of Qwen 3. It might perform better on local devices.
  - I’ve been digging into Unsloth’s fine-tune pipeline. Their Dynamic 2.0 quants deliver up to 2× speed, 70% less VRAM, and up to 8× larger context windows ! That makes running Qwen-3-Coder incredibly efficient on local machines like mine.

- ## 💡 [Recommendation for getting the most out of Qwen3 Coder? : r/LocalLLM _202508](https://www.reddit.com/r/LocalLLM/comments/1mrzi5x/recommendation_for_getting_the_most_out_of_qwen3/)
  - I was already running the model at the full context 262k with my setup. It was just slow. 
  - Now I'm experimenting with different versions and settings to find the best compromise/trade-off. 
  - Currently I'm testing `Qwen3-Coder-30B-A3B-Instruct-Q3_K_L.gguf` with 81k context, K/V Cache Quantization set to Q4_0 and I'm getting 110 tok/s at the start of the chat and still getting a rather respectable 40 tok/s with 55% of the available context used. I haven't done rigorous quality assessment on this yet though. It might be better than Quen2.5 Coder though.

- The cause of the slowness is large context sent to the model, typically 10-20k at the beginning. Have you measured your prompt processing speed? Usually, the issue is solved with prefix caching, vLLM supports it, llama.cpp to some extent, ollama has troubles with it, and I don't know about LLM Studio. 
  - K/V cache quantization Q4 may hurt model performance heavier then parameter quantization, I would not go lower Q8 for K/V cache.

- Keep tasks under 100k context including prompt and output. Reset once you go about that to avoid hallucinations.

- You may want to explore using Jupyter Notebook or JupyterLab with Qwen3 Coder. They offer integration with various coding languages and can handle larger scripts interactively.

- My 5090 runs at only 25 tks/s speed with 256k context, so the slowdown is normal

- ## 🤔 [Qwen3-Coder-480B Q2_K_XL same speed as Qwen3-235b-instruct Q3_K_XL WHY? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n7ket1/qwen3coder480b_q2_k_xl_same_speed_as/)
  - i am running two models and got unusual result of speed inference:
  - Qwen3-235B-A22B-Instruct-2507-UD-Q3_K_XL.gguf - got 23-24 token/s for 104GB model size from Unsloth
  - Qwen3-Coder-480B-A35B-Instruct-UD-Q2_K_XL.gguf - got 23-25 token/s for 180GB model size from Unsloth.

- Nope this seems about right
  - 22B @ 3bpw = ~8.25 GB of active parameters
  - 35B @ 2bpw = ~8.75 GB of active parameters
  - The ratios of the active / total parameters between Qwen 235B A22B and Qwen Coder 480B A35B changes such that coder requires less active parameters compared to its total size.

- Something similar happens to me. I'm running gpt oss 120B f16 almost at the same speed as qwen coder 3 30B Q4 in 3xMi50 32gb. 
  - GPT OSS 120B is 5.1B Active and natively Q4 even if youre running the fp16 weights. Qwen 3 Coder is 3B Active. OSS 120B will only be about ~20% slower aslong as you have enough vram to fit it so it doesnt have to fallback to system ram

- ## [Qwen 3 30B a3b on a Intel NUC is impressive : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1nbxkqh/qwen_3_30b_a3b_on_a_intel_nuc_is_impressive/)
- These models you're running are MoE, which makes them more CPU friendly, resulting in an increase in performance, they are built for local hardware without much potency, so that is expected.
  - I am running Qwen3-Coder-30B-A3B-Instruct-GGUF on 12vram and I can set 64k context window and I get 23t/s

- the speed is because at any given time activated parameters are only 3.3b, so computationally it's not like a 30b model, this is a clever thing about moe models.

- Also keep the Thinking and Coder models at hand. They could edge in situations where Instruct may not be able to solve.

- ## [Why does Qwen3-30B-A3B-Instruct-2507 Q8_0 work on my machine and no others come close? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1msy01r/why_does_qwen330ba3binstruct2507_q8_0_work_on_my/)
  - I'm surprised that having a machine with 8GB of VRAM and 32GB of RAM can run this LLM. Slow, yes, but it runs and gives good answers. Why isn't there another one like it? Why not a DeepSeek R1, for example?

- Because it's a MoE model, it's kinda like running a small model, during inference it first find which experts it should use and they're very small, it's quite different from running a dense model where it will go through all 30B params.
  - If you want similar models, look for gpt-oss 20b, Ernie 21b, SmallThinker 21b, those are MoE models too.
- MoE makes a huge difference. What I’ve noticed is that Qwen’s routing feels more efficient than a lot of other MoE setups, so even on low VRAM it doesn’t get bogged down as badly. Dense 30B models on the same hardware feel like night and day in comparison

- Is there anything in the name that gives away that it's a MoE?
  - yes the 30B is the total size, A3B = Active 3B, which means that only a part of model is active at time, like Qwen3 235B-A22B, but it's not a rule, gpt-oss 20B does not have it on the name, but if you search it's a 20B-A3.6B

- Dense 32B model, on the other hand, would be around an order of magnitude slower since in dense models active parameter count is equal to the total parameter count.

- ## 🤔 [Best coding model for 12gb VRAM and 32gb of RAM? : r/LocalLLM _202509](https://www.reddit.com/r/LocalLLM/comments/1n7fn2t/best_coding_model_for_12gb_vram_and_32gb_of_ram/)
- when i tried qwen coder 30b with lm studio it was reaaaallly slow, if u find a way to optimize it let us know or maybe it's lm studio the problem
  - When I use chat directly in LM Studio with Qwen 3 coder 30b, it’s quite fast! I’m on RTX 3060 12Gb. However, when I hook it up to VS Code, via Continue plugin, it becomes a tad bit slow but still fine. Then, when I switch it to agent mode it just becomes unusable. 
- Switching to `Llama Server` feels like night and day for me. When I was using LM Studio, I tried everything, but it was mostly very slow.

- I've got 12tps on a single 5060ti on the same Qwen3-Coder-30B-A3B-Instruct-Q6_K model but with much smaller context 16K

- Don't go beyond 100k context window with these as they're useless above it, as I have them as daily drivers with capacity to run full context.
  - Alternatively balanced, yet faster, you have GPT-OSS-20B from Unsloth. Either quants will work due to how it was optimised, just choose one you can fit. Even with offloading it's an efficient performer.

- ## [Is it true that all tools like Cline/Copilot Agent/Roo Code/Windsurf/Claude Code/Cursor are roughly the same thing? : r/ChatGPTCoding _202505](https://www.reddit.com/r/ChatGPTCoding/comments/1kumywl/is_it_true_that_all_tools_like_clinecopilot/)
- Yes - it’s essentially a big prompt (32k context window) and their tools. There is no magic except some have different workflows
  - Different models, better or worse at what to put in the context, RAG approaches…but yeah it’s generally the same.

- There are mainly three category of Coding assistants:
- 1️⃣ IDEs or IDE plugins with subscription model
  - VSCode+GH Copilot; Windsurf. AI; Cursor. AI; etc
  - All this assistants use their own set of prompts and tools, so even when you select the same AI model you can get other results. 
  - This editos are "cheaper" because they provide a monthly fee, but they also do brokeage between you and the AI services provider, and within that brokerage they can fundamentally cripple how the AI is used to reduce the context and maximize their profit
- 2️⃣ IDEs or IDE plugins with Bring-Your-Own-Key
  - Cline/RooCode/Kilo, etc .
  - Same different as category 1 (different prompts, tools), but they use the API directly, not reducing the inteligence to save money
- 3️⃣ Command line interfaces
  - Claude Code, OpenAI Codex, Janito, Aider, etc
  - This are typically better for natural language programming (prompting more, coding less), because they operate directly on files without the overhead of providing the editor context, (which files are opens, which file tab is open etc).
- While the model itself available on each of this tools is important, the result can be quite different depending on the optimization of the tools.

- Subscription tools (Cursor, Windsurf) need to balance what you pay vs their inference costs, so they use caps, context optimization, and throttling to manage margins. That's not a bug, it's how the economics work.
  - Cline/ClaudeCode/Roo (Cline fork) use direct API access with zero markup or throttling. You pay more for inference, but get unfiltered model capability. Different tools optimize for different outcomes.
  - Many devs use both -- subscription tools for autocomplete, Cline/others for complex tasks where you want maximum AI capability.

- Cline has a vector db like cursor and Windsurf now, it’s free and open source and you can see it in the code.
  - I think its a terrible idea, because it adds complexity and local search for code, which is mostly structured wording, unlike the generic text which benefits from vectorizing.
- I have also seen this option being made by other colleagues at my job, I think overall this is a disputed topic. To index or not code using a vector db.

- no Cline does not have a vector db. We're actually very against the notion of it from both a performance and security perspective.
  - [Why Cline Doesn't Index Your Codebase (And Why That's a Good Thing) - Cline Blog _202505](https://cline.bot/blog/why-cline-doesnt-index-your-codebase-and-why-thats-a-good-thing)
- why is it calling indexes all over the place in the "new" context management while your post says its not indexing?
  - "Index" here refers to array positions for organizing conversation history in memory, not database indexing or vector embeddings -- it's just basic data structure navigation.

- ## [It is almost May of 2025. What do you consider to be the best coding tools? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k0nxlb/it_is_almost_may_of_2025_what_do_you_consider_to/)
- As for what we use on our team, we're doing some server work and a lot of work in Unity and building lots of tools. We largely use Cline or Roo Code for the editor and then Sonnet 3.7 and Gemini 2.5 Pro mixed in. 

- Aider + Gemini 2.0 are responsible for most of my github activity starting from February.

- I do not use any IDE/editor's AI feature for coding. They feel pretty much useless even with full context. My personal opinion is, a developer should fully understand their code before committing, AI powered editors destroys this habit

- I’ve had much better luck with keeping the AI open in a browser and chatting with it, then manually editing the code in an IDE. 
# discuss-gen-ui
- ## 

- ## 

- ## 我现在越来越不担心 Vibe Coding 或者 AI 可以抢走高级程序员的工作了。
- https://x.com/brucexu_eth/status/2016481007286002067
  - 比如遇到一个富文本编辑器的光标拖拽不见了的 bug，AI 只会不停的调整 drop cursor 得 CSS，加上 zIndex 和 !important，但就是不出现。
  - 我打开 Devtools 熟悉的定位到那个 DOM，看了下 styles 和渲染位置，给 AI 增加了一些额外信息，然后它才知道原来是因为 transform 会导致 position fixed 失效，而光标拖拽是使用了 position fixed 导致的。我也恍然大悟了，transform 导致 position fixed 失效的问题我在 13 年的时候写过一篇文章专门研究过。
- 让AI用agent-browser或者chrome-devtool有可能能解决吗
  - 解决不了，因为看到这个渲染位置，需要找到这个元素，手动修改 css，然后通过视觉看到它的渲染位置。目前 AI 是很难做到的
- 我觉得你可能小看 devtools MCP 了，AI 可以通过它运行调试脚本通过 getClientBoundingRect 来获取各个元素的位置来分析的。我几个月前就遇到一处 transition 不生效的问题，Codex 用 devtools MCP 反复写了不同脚本测试找出了没有生效的原因。
- 连 chrome 的 mcp 就行了，类似的前端问题我用 ai 已经解决了很多，他会看 css，改完了还会模拟点击截图看效果，你说的视觉问题它截图就处理完了

- 你让 ai 接浏览器直接调了吗，还是只是描述现象，然后让它猜病灶。我倾向于认为很多很细节的问题不好调主要还是因为反馈回路没有调顺
  - 给ai提示不好的话，最后一步解决方案可能变成问1+1等于几，就像带一个刚入门的新同事，这时问答的异步沟通和等待成本，已经超出人工独立解决的成本，要考虑规避这种问题。

- 我觉得解决这个问题只差一个chrome connector

- 这种和高不高级程序员没太大关系, 后端的逻辑非常复杂它可以很快理清楚, 一旦 UI 揉进来它看不见摸不着就会这样, 一个小孩子能看到说出来的东西, 它看不见, 不要说它可以读 element 元素或者截图, 现阶段它就是很难"看"到
  - Gemini可以看视频做分析，我前几天遇到一个UI问题，语音没法描述清楚，我录了段视频给Gemini, 它就帮我解决了。
- 写了一大堆其实卵用没有，因为其实很简单你让AI添加log定位问题，就可以解决99%的问题

- 通识简单问题能解决的很好，冷门疑难问题还是需要给他一些方向，不然会一直尝试各种无效方法，毕竟他知道的解决问题的方法太多了

- 我之前也遇到过一个类似的问题：在地图上拖拽一个形状时，有可能会产生 ghost effect，但这种情况只有在特定拖拽速度才会出现，AI就一直很难在没有我的描述下解决这个问题。
  - Gemini已经可以理解screen recording 了，我前几天录屏让Gemini 帮我解决了一个问题。

- 当你把这个 debug 方法教给了 AI，下次其他人再遇到这个问题，它也会开始尝试用这个方法来解决。当 AI 用于 Vibe Coding 的范围足够广，它迟早能把这些边缘 case 的解法都学到。所以，一切都只是时间问题，可能高级程序员能活得稍微久一点。
- 这个问题要不了多久就会被其他老师傅指导 AI 学会的，还会做成可以到处分发的 skills 

- 我前些日子就遇到一个，文本页面加不上选择复制功能，给我讲了一通什么qt插件，现代化UI之类的…哦，我是小白，不会编程，我的解决方案就是…彻底舍弃，从头开始…AI很死心眼的，反复调试不如重来

- ## Where your product UI is dynamically generated, based on user intent and context.
- https://x.com/Prathkum/status/1988172654872834204
  - 演示效果不错
  - C1 API by @thesysdev is building the infra to make this possible.
  - C1 fixes this by turning LLM responses into an adaptive, interactive UI in real time.
  - cards, charts, table, forms

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [New to local, vibe coding recommendations? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nh16ft/new_to_local_vibe_coding_recommendations/)
- I still prefer Aider. Their system messages are under 2k. Crush is like 10k iirc. Idk about cursor/roo.
  - Sure it's not agentic but I prefer going one step at a time with the bot. Plenty of /undo's and /clear's.

- Keep using Cursor. 12GB VRAM is too low. The Vibe code part starts around 16GB but BARELY.

- ## 🧑‍🏫 [Engineer's Guide to Local LLMs with LLaMA.cpp and QwenCode on Linux : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nhh1v1/engineers_guide_to_local_llms_with_llamacpp_and/)
  - I will share my local AI setup on Ubuntu that I use for my personal projects as well as professional workflows (local chat, agentic workflows, coding agents, data analysis, synthetic dataset generation, etc).
  - Compile LlamaCPP on your machine, set it up in your PATH
  - Use `llama-server` to serve local models with very fast inference speeds
  - Setup `llama-swap` to automate model swapping on the fly and use it as your OpenAI compatible API endpoint.
  - ntegrate local AI in Agent Mode into your terminal with QwenCode/OpenCode
  - Test some local agentic workflows in Python with CrewAI 

- ## [Are you using local LLMs to power Cline, RooCode, Cursor etc.? What is your experience? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ivhrbn/are_you_using_local_llms_to_power_cline_roocode/)
- I use Qwen Coder 14b/32b for code refactoring and Qwen Coder 3b for autocomplete with the Continue.dev extension for VSCode. It's not quite on par with Github Copilot or Cursor, but it works well enough.

- One nice feature of continue.dev is the drop down for selecting a model. I have qwen coder 7b or 14b running locally and a selection of models via Openrouter. When my local models isn't up to the task, it just takes a second to switch to something more powerful.
  - I have qwen coder 7b for auto complete and it does really well. The number of times it gets it right is kind of amazing.

- Most of these tools use a temperature of 0. Small local models need to be controlled to avoid looping. In tabbyAPI, you can force the temperature and other settings to what you please

- Deepseek Coder (and coder V2 Lite) is a very old weak model. Qwen2.5 Coder 7b is a starting point for a useful model. 

- ## [Aider's Architect/Editor approach sets new SOTA for AI code editing, achieving 85% pass rate : r/ChatGPTCoding _202409](https://www.reddit.com/r/ChatGPTCoding/comments/1fshzxl/aiders_architecteditor_approach_sets_new_sota_for/)
- This method separates code reasoning and editing tasks between two models:
  - Architect model: Focuses on solving the coding problem
  - Editor model: Translates the solution into well-formatted code edits
  - Best combination: OpenAI's o1-preview (Architect) with DeepSeek or o1-mini (Editor)
- If you look at the llm.logs in aider, the architect always writes out the code, the editor model will merge the code with the diffs. So the architect model does the entire thing with code output.
  - So if you are using o3mini, as architect, it is the main code generator as well, and if you are using Sonnet 3.7 as the editor model, it actually wastes the code generation powess of that model, because it only uses it to "Edit" the code back into your files.
  - This is where I'm confused on how it "architects". I would call it Code generator model, and a Code patch model.

- you're responding to a 7 month old comment. Even Paul G himself doesn't use Architect mode anymore!

- This is the way to do it. 
  - AutoGen did this years ago but it's a PITA. CrewAI is mostly OK but it's more designed for process instead of code generation

- ## 🤔 [Should I use reasoning for coding? : r/DeepSeek _202503](https://www.reddit.com/r/DeepSeek/comments/1jnzdb3/should_i_use_reasoning_for_coding/)
- no, Deepseek V3 writes code much better than R1.
  - In programming, R1 makes sense to use for planning, precisely..when you need to reason... 
  - That is, when you are planning something very complex, a model like V3 simply gets confused, wants clear instructions, is not very good with "but, however" .. then you use R1 which does the reasoning and spits out a sensible plan...then for the actual implementation, use V3 anyway...it is cheaper and if it is just about coding, it works better.
- If V3 is better why is R1 ranked higher for coding benchmarks? And why is it that the best coding models are all reasoning?
  - You are probably right and I expressed myself badly, although in my specific case V3 literally wrote better code than R1

- ## 🏠 [Has anyone successfully used "thinking" models for large coding projects? : r/ClaudeAI _202502](https://www.reddit.com/r/ClaudeAI/comments/1ifgtrz/has_anyone_successfully_used_thinking_models_for/)
  - The reason I ask is because I don't know if I'm just missing something when it comes to thinking models, but aside from the early code drafts and/or project planning. I just cannot successfully complete a project with them.
  - I'm starting to think that maybe models with this type of design paradigm just isn't compatible with complex programs given how many "reasoning" loops it has to reflect on, and thus it seems to constantly muddy up the context window with what it "thinks" it should do. Rather than what it is directed to do.
  - Everytime I try one of these models it starts off great, but then in a few hours I'm right back to Claude after it just becomes too frustrating.

- The problem I've observed was typically through using aider (where I have a $700+ in API costs from this project alone) where Claude incessantly recommends "improvements" that adds complexity and breaks things
  - But I noticed that happens significantly less when I use code mode in Roo Code
  - I think some of that rabbit-hole behavior might be due to the system prompt as I noticed Roo Code doesn't tend to "suggest" improvements that I never asked for.
  - The fundamental limitation IMO is that you really need to be fully capable of doing the entire project yourself without the use of AI. Then at that point AI becomes a force multiplier.

- I typically use reasoning models like you, then shift to Sonnet as wel

- For what it’s worth, this is the exact kind of workflow Aider (open source console-based dev tool) encourages.
  - Basically you use the thinking model to prototype the code (in Aider this is called “architect” mode), then when it comes to outputting actual code, you use a different “coder” mode that leverages a simpler chat model to write the code (like Sonnet, GPT4o). The chat model operates on the back of the notes and specs written out by the reasoning model to write the code to spec.
  - The Aider dev did a bit of research and iirc discovered this works better than just using the reasoning model for everything. And is obviously more affordable, too. It’s very interesting.
  - Anecdotally, this vibes with how I’ve used gen AI in my coding workflow before reasoning models even came to be. I’d write up a detailed technical spec of how it should be done, then let Claude or GPT4o write up the first draft of code, and iterate from there

- ## 🤔 [Why is Qwen 2.5 the most used models in research? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kyrhr7/why_is_qwen_25_the_most_used_models_in_research/)
- We tuned qwen 2.5 7b in our paper, general choice reasons - sota for their size, strong multilingual support, 7b variant is good for restricted compute resources while being smart enough for tasks. And no unexpected tricks are expected from the qwen team, like models are not overly tuned on some style/emojis in response, not overly guarded like early Gemma was etc.
  - For next experiments we want to try falcon h1 models and qwen3, but qwen3 being half thinking makes it harder to tune(you kind of need both reasoning and non-reasoning samples in your dataset), so choice will depend on how the data processing will go.

- For a while there it seemed like everything was Llama 2.

- May be related to how well it works with RL in general, so well that using random rewards increases the performance.. https://www.interconnects.ai/p/reinforcement-learning-with-random

- What I like about Qwen is that they come in all sizes. There is a Qwen model for every hardware.

- ## [Difference between Qwen2.5 and Qwen2.5-Coder for NON coding tasks? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i1jlop/difference_between_qwen25_and_qwen25coder_for_non/)
- 14b coder lose about 10% on mmlu and ifeval compared to 14b normal. 

- If you can go up to a larger model then I recommend Sky T1, it's a finetune of Qwen 2.5 32b non coder, so it has all of the non coder versions capabilities but is also better at coding than the coder version in my experience.

- ## [How much worse is Qwen2.5-Coder for non-coding tasks? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1inazl9/how_much_worse_is_qwen25coder_for_noncoding_tasks/)
- Qwen-Coder at least produces sensible output and tries its best, but in my experience is still a very poor model for this especially consider its size.

- About 4 LiveBench percentage points worse. I'd recommend switching models based on the task at hand.

- ## [Wow anthropic and Google losing coding share bc of qwen 3 coder : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1msrnqq/wow_anthropic_and_google_losing_coding_share_bc/)
- qwen coder is free
  - so people use anthropic and google models as architects, and then qwen coder for the coding
  - the result is qwen giving people free inference in exchange of anthropic and google outputs , to make next qwen better planner and more compatible to anthropic and google outputs
  - and the other result is anthropic and google losing income and power.

- Qwen 2.5 variants were already high on my capabilities tests, and qw3 is even better.

- GPT-OSS is a competent coder but it's vendor knowledge is waaay behind Qwen so 235b does out code it.

- 
- 

- ## 🧩 [What is the current best FIM model that I can run on a single 3090? Still using Qwen 2.5 Coder : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1miuctw/what_is_the_current_best_fim_model_that_i_can_run/)
- For the best Fill-in-the-Middle (FIM) performance on a 3090 with continue.dev, go with Codestral-22B due to its specific FIM optimization and official integration; 
  - for more complex, repo-level agentic tasks, Qwen3-Coder-30B is a strong alternative.

- I'm kinda new to this "FIM model" concept, is it the go-to type of model for code auto-completion? I am developing a auto-completion feature and I am trying to figure out if it'd be worth trying out FIM models. Also, is Qwen 2.5 Coder good?
  - 1. Yes
  - 2. You should indeed use FIM models. You can see continue.dev for an example: they have autosuggestion feature and recommends qwen coder in local deployment
  - 3. Yes, good enough for my needs

- ## [(Noob here) gpt-oss:20b vs qwen3:14b/qwen2.5-coder:14b which is best at tool calling? and which is performance effiecient? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mjz1ow/noob_here_gptoss20b_vs_qwen314bqwen25coder14b/)
- gpt is generally better at tool calling https://gorilla.cs.berkeley.edu/leaderboard.html
  - general knowledge is harder to gauge, ask it some questions in your field and see if it gets it right. Heard gpt-oss is bad at front end
  - Most importantly: Try it yourself. Also try the Qwen3 30b MOE, it's a little larger but the benchmarks place it close with the 20b MOE
- gpt-oss is MOE 20b/3b active, so it (should be) faster. You can try it yourself to make sure it's right on your system
