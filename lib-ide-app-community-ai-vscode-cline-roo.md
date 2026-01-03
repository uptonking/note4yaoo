---
title: lib-ide-app-community-ai-vscode-cline-roo
tags: [ai-coding, cline, roocode, vscode]
created: 2025-10-28T20:01:51.110Z
modified: 2025-10-28T20:02:16.727Z
---

# lib-ide-app-community-ai-vscode-cline-roo

# guide

- cli-coding-pros
  - ide-agnostic, no ide ui restriction
  - lightweight and fast, less RAM requirement
  - easier to implement parallel agents
  - 限制少，更容易实现模型/厂商无关

- cli-coding-cons
  - gui has less features
  - very hard to support LSP

- cline-pros
  - stable with less features
  - 支持本地模式下高强度压缩context, 本地运行更友好
  - cline cli with client/server architecture as ai infra
  - 架构上更解耦，提供了不依赖vs code而standalone运行的产物
  - voice coding
  - Adds `/smol` command to condense conversation history

- cline-cons
  - reject github contributions
  - plan/act 只支持切换同一provider的不同model，不支持不同provider的不同model

- features-cline

- who is using #cline
  - ?

- roo-pros
  - rich features and more github contributions
  - model profile switching is easy
  - codebase indexing
  - 支持手动 condense conversation history

- roo-cons
  - token cost more
  - Roomote Control is available in paid plans

- features-roocode

- who is using #roocode
  - ?
# draft
- cline + acp(agent-client-protocol)
# ide-ai-pm
- ai工作使用服务端架构的优点
  - 方便实现关闭页面或刷新页面后，也能看到ai工作结果的效果
  - 方便实现多个ai并行执行多个任务的效果，提高效率
- devin偏服务端方案而偏向创作力工作，cursor偏向工具
# ide-ai-xp
- ai-llm
  - 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型

- ide的自动补全和多人实时协作似乎是冲突的

- ai生成的代码的缩进有时与原代码不同
  - 解决方案是在服务端执行 prettier ?

- 
- 
- 

# docs-cline
- [CLI Reference - Cline](https://docs.cline.bot/cline-cli/cli-reference)
  - cline is a command-line interface for orchestrating multiple Cline AI coding agents.  
  - Cline is an autonomous AI agent who can read, write, and execute code across your projects.  
  - 🏠 He operates through a client-server architecture where Cline Core runs as a standalone service, and the CLI acts as a scriptable interface for managing tasks, instances, and agent interactions. 
  - The CLI is designed for both interactive use and automation, making it ideal for CI/CD pipelines, parallel task execution, and terminal-based workflows.  
  - Multiple frontends (CLI, VSCode, JetBrains) can attach to the same Cline Core instance, enabling seamless task handoff between environments.
# docs-RooCode
- Can Roo Code access the internet?
  - Yes, if you are using a provider with a model that support web browsing. Be mindful of the security implications of allowing this.

- Codebase Indexing creates a semantic search index of your project using AI embeddings. 
  - This enables Roo Code to better understand and navigate large codebases by finding relevant code based on meaning rather than just keywords.

- Roo Code made changes I didn't want. How do I undo them?
  - Roo Code uses VS Code's built-in file editing capabilities. You can use the standard "Undo" command (Ctrl/Cmd + Z) to revert changes. 
  - Also, if experimental checkpoints are enabled, Roo can revert changes made to a file.
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-kilocode
- ## 

- ## 

- ## 

- ## [kilo code这么飞快的吗，同一个模型比roo code还快 ](https://linux.do/t/topic/1401468)
  - 我一开始觉得可能是模型原因，毕竟不是控制一个变量。kilo我用的是gemini-3-flash，而claude code则是AWS的claude。然而在我把模型都换成了glm-4.7之后发现kilo code的速度依旧很快。
  - 朋友之前一直用的roo code，听我这么一说不信，于是也换成了kilo code，结果也是快了不少。roocode还在想的时候kilo code就已经干完活了。
  - 其实我还想继续用claude code继续这个任务的，但是上下文已经不够用了，而且经过了几次压缩之后就已经完全不能用了（cli工具一般我是完成一个任务最好就赶紧新开一个窗口，能不压缩最好不要压缩）所以最后也是没有做出来

- kilo还有个问题，经常会出现循环出不来的情况，就很捉急
# discuss-cline
- ## 

- ## 

- ## We've migrated our system prompt tool calling format to native tool calling and split that out for different model families. _202511
- https://x.com/cline/status/1984334385626411397  
  - Here's why this results in a better experience using Cline
  - Models now return tool calls in their native JSON format, which they were specifically trained to produce. You'll notice fewer "invalid API response" errors - this particularly improves gpt-5-codex performance with significant reduction in failed operations.
  - Parallel tool execution is now enabled. When Cline needs to read three files, it can execute them simultaneously instead of sequentially. System prompts are also smaller since tool definitions moved to API parameters, reducing token usage by approximately 15% per request.
  - Native tool calling is currently supported for next-generation models: Claude 4+, Gemini 2.5, Grok 4, Grok Code, and GPT-5 (excluding gpt-5-chat) across supporting providers including Cline, Anthropic, Gemini, OpenRouter, xAI, OpenAI-native, and Vercel AI Gateway.

- Roo lacking behind now officially

- Native tool calling with model-specific formats should significantly improve response quality and reduce parsing errors.

- ## Is there any advantage to using the CLI over the IDE extension?
- https://discord.com/channels/1275535550845292637/1392662920982171738/1431071030725709824
- you can use CLI in scripts, for automation, CI/CD, benchmarks ...  Also some people prefer CLI UX
- On the CLI. I suspect core would give me more flexibility

- ## Do we also have any examples how to setup project Indexing?
- https://discord.com/channels/1275535550845292637/1392662920982171738/1393446018795704464
- Cline does not currently do indexing of the codebase, he just searches around using `ripgrep`

- ## 🏠 已合并pr [Run the cline extension as a standalone process outside of vscode. by sjf · Pull Request · cline/cline _202505](https://github.com/cline/cline/pull/3535)
  - Adds a new build target npm run compile-standalone for the standalone version of the cline extension. 
  - The standalone cline server runs a gRPC service that provides the protobus API.

- ## [We're releasing a scriptable CLI (Preview) that turns Cline into infrastructure you can build on (+ subagents) : r/CLine](https://www.reddit.com/r/CLine/comments/1o8c6zw/were_releasing_a_scriptable_cli_preview_that/)
  - Use it standalone in the terminal for any coding task
  - Run multiple Clines in parallel terminals -- like having each tackle a different GitHub issue
  - Build it into your operations -- Slack bots, GitHub Actions, webhooks -- via the gRPC API
  - Use it as subagents from IDE Cline (VS Code & JetBrains) for codebase research
  - Have IDE Cline spawn CLI agents to handle specific tasks
  - Spawn subagents with fresh context windows to explore your codebase and report back
- The scriptability is what makes this different. You can pipe output, chain commands, integrate with your existing toolchain. Cline becomes a building block, not just another tool.

- Yeah since Claude code did it. Does it. Like yeah a long time ago.
  - Vendor lock in cough. 

- Can you comment on how it might compare with Claude Code?
  - you get Cline's support for all its providers 
  - you get cline's agentic and tool calling approach vs CC
  - CC & Cline both sub-agents. Cline's can be headless
  - CC uses 1 model for plan and another for act

- How does it work to reconnect a cli session via VSCode? Wondering if there is some data stored on the cloud or if this can be serverless like typical Cline.
  - There's no cloud / server, it's all local as usual. Right now, there's no way to "dive in" to a subagent/cli task in VSCode, but this does work with JetBrains. The task the subagent runs become part of your task history, and then you can just open it and continue where you left off. We'll be rolling that out to VSCode after we carefully test some very spooky migrations code

- ## ✨📝 [Cline CLI: Return to the primitives - Cline Blog _20251015](https://cline.bot/blog/cline-cli-return-to-the-primitives)
- AI coding is fractured: most tools are tied to single models, closed architectures, or both.
  - Context never leaves the tool that created it. Teams pilot multiple options, but each tool hoards(储藏，积存) its understanding of the codebase. A PR review started in one agent can't continue in another.
- This isn't just inefficiency; it's structural. When context can't travel between tools, teams can't leverage the best model for each task. 

- The Cline CLI (Preview) is a scriptable agent powered by Cline Core, the same loop behind our VS Code and JetBrains extensions. 
  - it's infrastructure you can automate and build on, launching today for Linux and macOS.
  - Because it shares that persistent loop, the CLI hands tasks to VS Code, JetBrains, CI, or webhooks without losing context, and it drives subagents in our IDE extensions so Cline can spawn focused subprocesses for things like deep repo exploration without muddying the parent state. 

- Here's how you can use the CLI
  - Start debugging with cline "fix this production error", attach to the same task in JetBrains when you need the IDE with cline task open [task-id], then continue in CI with identical state.
  - Drop Cline CLI into your deployment pipeline with full audit trails, approval gates, and governance hooks for enterprise compliance.
  - These patterns show what's possible when your agent loop is infrastructure, not just another tool. 
  - This same approach works for any webhook-driven workflow, from customer support tickets to data pipeline monitoring.

- The advances of frontier models have made building presentation layers for coding agents more accessible. 
  - What's hard is the foundation underneath—the agent loop that makes everything work.
  - Without a maintained loop, teams reinvent the same infrastructure: state handling across tool boundaries, model routing based on task complexity, prompt optimization for each model's characteristics, governance hooks for audit trails, lifecycle orchestration for complex workflows.

- Fortune 100 engineering teams are already building on this architecture. Salesforce built APEX coding agent on Cline, validating that leading technology organizations are investing in this approach. 
- When teams need agents that work across their entire stack, they're choosing Cline's open architecture.
- We provide the primitive stack—context persistence, execution bridges, lifecycle hooks, structured logging—so you can focus on your presentation layer.

- The future isn't one AI coding tool to rule them all. It's an ecosystem where everyone builds what works for them, on top of a shared agent loop that continually improves. While we're starting with AI coding, the primitives we're building (file operations, browser control, task persistence) are the foundation for agents that work like humans do. We're providing that foundation starting today.

- ## 📝 [Cline CLI & My Undying Love of Cline Core - Cline Blog _202510](https://cline.bot/blog/cline-cli-my-undying-love-of-cline-core)
- Cline CLI Preview is available & open source now! When I started working on Cline, he was a tightly integrated VS Code extension, and it's taken months to liberate him into a standalone service that can be embedded into any environment.
- That's Cline Core. Cline for JetBrains was built on top of this service, and now I'm really excited to be able to use Cline CLI in the terminal too.
- Our focus in the CLI has been scriptability. One of my catchphrases is that "LLMs convert unstructured data into structured data" – and this is incredibly helpful in scripts.

- the CLI is designed to manage many agents running in parallel, provide full scriptability, and offer a convenient chat interface.
- IDE Cline (like in VS Code & JetBrains) can call the Cline CLI to delegate tasks with a fresh context window. 
  - In this first version, Cline is instructed to use one sub-cline at a time, and to wait until the sub-cline completes.

- Multiheaded Cline Hydra
  - Our architecture allows for multiple frontends to be attached to a running task. It would be quite doable today to create a mobile app that remote controls your desktop Cline instance. 

- The Architecture of Cline Core
  - The scheme is that Cline Core runs as a simple node process, exposing a gRPC API that allows him to be integrated into anything the community can imagine.
  - It's also possible to attach multiple frontends at the same time, do it over the network, and pass tasks around.
  - The "Presentation Layer" (aka user interface) connects as a gRPC client to Cline Core and tells him what to do. Cline Core sends back a subscription of state changes & LLM messages, which allows the presentation layer to display stuff.
  - Cline Core connects as a gRPC client to the "Host Provider Layer" which implements integration into what he's being embedded into. So, for example, Cline Core can ask VS Code to provide the linter output.

- ## [Cline for JetBrains IDEs is GA : r/CLine _202509](https://www.reddit.com/r/CLine/comments/1njjjku/cline_for_jetbrains_ides_is_ga/)
  - Cline has always been model agnostic and inference agnostic. Today we're completing the picture: platform agnosticism. Cline is now available for all JetBrains IDEs.
  - we rebuilt Cline using cline-core, a headless process that communicates through gRPC messaging. This gives us true native integration with JetBrains APIs.
  - The cline-core architecture is our path to ubiquity. This same foundation will power our upcoming CLI, an SDK for embedding Cline in internal tools, and expansion to additional development environments. One brain, many interfaces. We're not just adding IDE support; we're building true platform agnosticism.

- ## 👷🏠 Over the past 6 months, we've rearchitected @cline 's agentic loop into a standalone "cline core" gRPC service that runs independently of any editor. _202509
- https://x.com/pashmerepat/status/1969076772575629799
- This enabled us to decouple from VS code and build  
  - JetBrains (released in GA this week)
  - CLI built in Go (releasing soon)
- The CLI is our newest product and will ship without a TUI. 
  - Our focus is to release a true primitive. something close to the metal that pipes cleanly into RL environments, CI/CD systems, scripts, and automation workflows.
  - Any "presentation layer" mentioned above can connect to the same running cline core - maintaining full feature parity (e.g. checkpoints, settings, api configurations), context, and conversation state.
  - There's an SQLite-based instance and file/directory lock registry that prevents port conflicts and coordinates graceful shutdowns between paired processes - so you can start up thousands of cline instances in parallel with no conflicts or dangling processes.
  - What's remarkable is that this cline core architecture opens Cline to any interface imaginable: mobile apps, web dashboards, custom tools - all powered by the same intelligent core that understands your codebase.

- have any plans for a cline SDK? something I can plugin to my existing system and it just... works?
  - SDK will come soon after the CLI is released

- Do you plan to support ACP from @zeddotdev ?

- so like @opencode server model?

- ## [Is the Memory Bank pattern deprecated/superceded now? : r/CLine _202510](https://www.reddit.com/r/CLine/comments/1ny9zpz/is_the_memory_bank_pattern_deprecatedsuperceded/)
  - Not sure with all the updates Cline has had if this usage pattern is still recommended? u/nick-baumann was suggesting deprecating it a while back

- No, and it's still extremely useful imo, i have different rules i use for different vertical slices and tasks that can get a new session up-to-speed very quickly. The ability to turn those rules on and off easily is a huge timesaver and Clines recent other improvements have done nothing to deprecate this use-case

- I believe that post was just asking for options if it should be deprecated and he suggested that the focus chain https://docs.cline.bot/features/focus-chain might provide a better workflow now.

- You gotta remember, memory bank works with your custom instructions, even with the updates even though we can't access those at the GUI in VSCode, it currently still refers to it as that file lives in /cline/rules... technically you don't even need Cline, just any LLM with a filesystem MCP server.

- ## [What happened to context compression every 6 prompts? : r/CLine _202509](https://www.reddit.com/r/CLine/comments/1np8vjk/what_happened_to_context_compression_every_6/)

- ## 🏠 [Why Cline cannot edit multiple files at once? : r/CLine _202509](https://www.reddit.com/r/CLine/comments/1njhygc/why_cline_cannot_edit_multiple_files_at_once/)

- RooCode can do multi-file reads and edits.

- This is actually a fundamental architectural constraint, not a performance oversight. The sequential approach exists because:
  - Context consistency - LLMs work with potentially outdated file states. Parallel edits would create conflicting contexts the model can't reconcile.
  - Dependency management - Code files have complex interdependencies. When refactoring a class name across multiple files, you need to ensure all references update consistently.
  - Error handling - When a diff edit fails (which happens), sequential processing allows immediate feedback and correction before issues cascade.
- The workflow is fundamentally: LLM generates change → Tool applies → File system updates → Feedback → Next decision. Each step needs the previous one to complete for the model to make informed decisions about what to do next.

- Cline has instructed the model in its system prompt to execute only one tool at a time.
  - I would guess that back then it really worked far better. Even today it works very well.
  - But indeed - it has its drawbacks - speed, and expensive (for those paying per request)
  - Can cline do better on this front ? I’d say definitely - Claude Code does very well , while supporting executing multiple tools in a single call. And it makes Claude Code dramatically faster, with the same provider and model compared to Cline.
- Cursor also executes multiple tools at once.

- ## 🧠🤼 [Should we deprecate Memory Bank? Looking for some feedback from the Cline Community. : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1mu4lej/should_we_deprecate_memory_bank_looking_for_some/)
  - memory bank is a prompt that I wrote (and to some degree have maintained) over the last year or so. 
  - It's original purpose was to instruct Cline to create/edit/read these context files that gave it an understanding of the project and where it was headed. 
  - And to do this via a single prompt that any user could paste into Cline and have work out of the box.
  - Here are the main benefits I see: - keeps the agent on track - creates project context that persists between tasks - useful documentation across teams
  - However, it does bloat the context quite a bit. And with our most recent Focus Chain feature, I'm not sure where/how it fits.
  - What parts of Memory Bank are actually useful to you? What is not useful? What does the ideal version of Memory Bank look like for you?

- My favorite part of memory bank was the tracking of progress. It knew what was done. What still had to be done. How certain parts were set to work. Etc.
- is this not covered by the focus chain & its todo list?
  - Only for a task basis. The memory bank keeps the context about the whole project and work which has been done recently. It allows me to start a new task with a description of what's needed and in which parts of the repo. Cline will find everything necessary on its own (mostly), and I can refine it.
  - It's also super helpful when using plan mode or deep planning to basically get everything pulled into the task.

- Focus chain is for a single Cline task/conversation.
  - Memory bank is to share basis about the project, the service, the roles, , between Cline conversations, so I do not have to remind it about it everytime my task needs a lot of context to be shared.

- I stopped using the Memory Bank a while ago. It ate too many tokens and no model was very good at keeping it updated. Instead, I have a markdown file that I keep in Obsidian that I manually keep updated, and keep brief for the times when I think the AI needs some more context.

- I love the memory bank, and still consider it a major strength of Cline. The progress is my most used file by far, and I heavily rely on it. Though the product and project contexts are also both helpful.

- in my work, Plan leans heavily on Memory Bank.

- In terms of context usage, memory bank is wasteful, it's mostly the reason I do not use it anymore, though I still create manually specs files and use rules.

- Sharing context with another dev to take up can be super handy.
# discuss-cline-roadmap
- ## 

- ## 

- ## 

- ## 🤔 if there is any other way of invoking cline installed in vscode as extension remotely? _20250822
- https://discord.com/channels/1275535550845292637/1392662920982171738/1408510775726706950
- Not currently, but that's in the pipeline as well. 
  - We're moving our architecture onto a new way of doing things, in particular: the VSC extension used to be a tightly interwoven thing with VSC, but now we have Cline Core, which can be run standalone. 
  - Our new IDE integrations are using this Cline Core server directly to build their features over gRPC. 
  - 📡 Eventually we'll have to move VSC onto this paradigm as well, at which point you'll be able to directly connect to VSC's underlying Cline Core and add extra UIs/remote control

- Will cline core  cli have a command line interactive mode like other cli ?or only `cline <command>`  ? 
  - We may do a TUI in a following phase, but I acutally think that scriptability is way more exciting than putting user interfaces into terminal -- since we already have real UIs. 
  - Of course, you'll be able to easily have two terminals open, one that is a live feed of Cline's output (cline task follow), and one that you're using to send commands into it (cline task send)

- https://discord.com/channels/1275535550845292637/1392662920982171738/1402304912628514857
- are there any plans for Cline to also run via CLI? 
  - Yes! Check this out

- ## the cline-core system is pretty mature now. Here's some rough info, and lmk if you need further support: _20250828
- https://discord.com/channels/1275535550845292637/1392662920982171738/1410324327445827686
  - 1) Use npm run compile-standalone to be able to run node ./dist-standalone/cline-core.js
  - 2) There are three parts to a working Cline integration: (a) the presentation layer defined in ./proto/cline (b) Cline Core (c) the host provider defined in ./proto/host
  - 3) Cline Core acts as (a) a gRPC server that the presentation layer can connect to (b) a gRPC client that connects to the host provider
  - 4) The host provider is effectively the equivalent of the vscode apis that are provided by VSCode. You need to implement stuff like the diff-edit experience, read/write, showing error messages etc
  - 5) The presentation layer mostly just receives state using subscribeToState and can send commands like newTask

- If you wait about another month, we should have an early release of the Cline CLI, which can act as both reference code for these elements, and provide a generic host implementation that you could use. The CLI can also be a base layer for integration, and includes Go versions of the protos & clients you would need

- ## Right now, it takes a lot of knowledge to be able to do something useful with Cline Core, since you have to control it using the gRPC APIs. 
- https://discord.com/channels/1275535550845292637/1392662920982171738/1400977345447465000
  - But the direct answer is `cd dist-standalone && node cline-core.js` after you do the build. 
  - It's possible to use Postman or something like that to manually control it

- Is there going to be an API server for the core? 
  - there is an API already

- Is there a way to implement a version of cline for libreoffice / openoffice / onlyoffice? 
  - Yes, that'll totally be possible with Cline Core, and those less obvious usecases are very exciting to me. Same thing goes for embedding Cline into note taking systems
  -  I want the core to be flexible enough to create various kinds of agents with it, though right now it's certainly very coding oriented. But there's a lot of overlap to editing notes/documents and code, it's kinda the same read/write idea ... instead of folders you have notebooks, etc. It'll take a while for our system to be fully customizable like that, but I think it's a worthy goal

- https://discord.com/channels/1275535550845292637/1392662920982171738/1392942543813083176 _20250711
- here's the gist of the WIP Cline Core system:
  - 1) Check out `npm run compile-standalone` -- this packages a Cline that runs as a node.js process
  - 2) To communicate with Cline Core, we have two gRPC bridges, one that runs from the presentation layer (ex webview, cli) to Cline Core, and one that runs from Cline Core to the host environment (ex vscode, neovim, etc). This means that the presentation layer can trigger actions in CC (ex. newTask), and CC can trigger actions in the host environment (ex. showWarningDialog). Check out the ./proto folder for all the definitions of the Cline API and Host API
  - 3) Settings are now stored in `~/.cline` as JSON for CC
  - 4) We're currently working on implementations of JetBrains & a generic CLI 

- to the best of your knowledge, is this the first library that implements this concept with CC? or are you following the lead of others elsewhere?
  - Afaik we’re the only ones using grpc, but the pattern is fairly common for agents that need to interface with many different hosts and presentation layers. Different flavors of the same architecture
- Continue & Cody has something similar, i don’t think claude code does.

- ## ☁️ [Cline outside VSCode? : r/CLine _202508](https://www.reddit.com/r/CLine/comments/1n0w4x4/cline_outside_vscode/)
  - Are there ways to let Cline run in the cloud / plans that would enable the described UX?

- 👷 it's Pash from the Cline team. Yep, this is exactly what Cline Core is for. 
  - Cline core is the standalone gRPC-based engine that lets Cline run outside VSCode. 
  - It already exists in a WIP form, and you could write your own integration with it now, but the team’s advice has been to hold off on building serious integrations until the upcoming CLI release, since that’ll give you a stable, scriptable surface for exactly these async/cloud/mobile workflows.
  - If you’re interested in the latest progress and roadmap, the `#cline-core` channel in Discord is the place to watch (Andrei is leading the initiative, posting CLI specs, integration details, and answering questions there).

- ## [Standalone Cline? : r/CLine _202505](https://www.reddit.com/r/CLine/comments/1kfcid1/standalone_cline/)
  - Is the only option with this library to run it in Vscode? Can it be run in a standalone mode where one can interact with it via a different pipe? Perhaps using protocol buffers?

- After investigating this in cline repo, there appears to be heavy coupling to vscode in cline's core. It doesn't seem to be feasible to run it independently, and this seems like a much better option.

- ## [Expose API/CLI for Remote Control · cline/cline _202504](https://github.com/cline/cline/discussions/2622)
- I build an extension to do so from the beginning of this month, and just released a version on VS Marketplace. I intended to build it on Cline. 
  - However due to the limitation to capture the event messages from Cline, I had to shift the focus on the support for Roo Code which exposes the event listener of sidebar provider.
  - https://github.com/Joouis/agent-maestro /MIT/ts

- Triggering batch tasks on a remote VM is a common scenario. Or a small team needs to demo an in‑development MCP tool with minimal setup.
  - If you're targeting a large‑scale, production‑grade workflow, the most robust approach is to decouple Cline's core logic from VS Code. I think that's outside the scope of current discussion.

- I spent a day experimenting with decoupling the Cline webview-ui from the VS Code window. My goal was to see if the existing interface could be run externally, and I was able to get the webview-ui's React components running in a standalone web server, communicating directly with the extension's backend in VS Code. The setup maintains a live gRPC connection, granting the external UI full access to the workspace context. To demonstrate that the connection is solid, I'm currently using a simplified version of the UI, but the experiment confirms that it's possible to make the original components work in this new context. 
  - The primary motivation was to enable remote control, and this experiment confirms that you can create a mobile-friendly interface to interact with your development environment. While it's just a WIP/quick test, It makes the idea of being truly productive on a phone feel suddenly within reach.

- are you planning on making vscode not a requirement by any chance? I would love for cline to be a standalone tool that I can use in my scripts instead of having to install vscode.
  - looking at src/standalone/ source code, this seems to be the case

- https://discord.com/channels/1275535550845292637/1392662920982171738/1403858110166339616
- vscode cline remote connection for anyone still interested
  - https://github.com/0xlws2/cline/tree/vscode-remote

- ## [External API Integration for Cline [Feature proposal] _202507](https://github.com/cline/cline/issues/4886)
- this functionality is already covered by our gRPC system (which supersedes the need for websockets and json). It's already pretty easy to tap into, and can function to provide multiple UIs to a vscode cline instance (running in vscode + a remote control for example). 
  - As we get closer to a standalone implementation with a CLI remote control, it'll be easy to simply write a shell script around the CLI to do features like this telegram integration very easily. 

# discuss-Roo
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Roomote suggestions : r/RooCode _202509](https://www.reddit.com/r/RooCode/comments/1ndiqly/roomote_suggestions/)
- i feel the logic of remote is quite reverse or retard(使减速; 妨碍, 阻碍). The host is users vscode, so it requires your personal machine to be running to remote control it.
  - Why not a cli based or sdk logic. Observer pattern : cli/sdk is a host so this can be run in any machine e.g. linux. Then from vscode and to roo remote app, users can enter ws api to listen to that host/server. But i believe this requires major architectural refactoring.
  - i believe cline is moving towards to this path. I think they are planning to use cline sdk into the vscode extension as a core. So it's flexible to many features including remote controlling.
  - I hope roo follows that path, you can build roo sdk, then it can be used to vscode, terminal agent etc it has so many possible applications.

- Developers currently use VS Code to work on their code so this compliments their existing use of Roo Code. Not backwards at all.
  - In terms of Roomote Cloud Agents, they’re coming. We don’t need a CLI to achieve this.

- ## [Monitoring Roo Code while afk? : r/RooCode _202505](https://www.reddit.com/r/RooCode/comments/1kdzesz/monitoring_roo_code_while_afk/)
- So you’re looking for Roomote control?

- You can install VSCode/Codium in a docker container for remote access

- There’s someone on the roo code discord who started looking at a roo code - websocket - telegram integration. I didn’t try it out yet though.
- https://github.com/wolverin0/Roo-web-socket /apache2/202504/ts/inactive
  - a fork of the original Roo Code project, modified to include a Telegram notification and interaction system.
  - The primary goal of this fork is to enable Roo Code tasks running within VS Code to: Notify a user via Telegram when a task requires input or confirmation.
  - Receive a response from the user via Telegram.

- I use the pushover mcp server to send me a notification when a long running task completes. Roo even adds some details for you so you know if you need to get back or not. After you start the task, you proceed while running and then ask to send you a notification when it's done. The only thing is Roo will want to keep going doing busy work so you have to tell it to wait.

- ## [Claude Code hangs at API Request on VsCode/Code-Server · Issue  · RooCodeInc/Roo-Code _202506](https://github.com/RooCodeInc/Roo-Code/issues/5097)
  - I use roo on Trae with Claude Code and doesnt have this problem. Every command is executed and API Reqeustr works
  - On Code-Server - VsCode, Roo just hangs when using claude code and once in a while it manage to completes the task, but most of the time it just hangs at API Request and nothing happens.
  - Code-Server VSCode on my server accessed through browser.
  - Im running debian

- I created a PR that solves this issue on my machine. The cause was (in Windows using Claude Code through the WSL) trying to send all the context as part of the command-line arguments, and Windows PowerShell wouldn't accept more than 8191 characters, which was being vastly outstripped. The PR changes the approach to use stdin and Claude Code's expected schema. There is a lot being passed in just the system prompts, and that alone was hitting that limit on my machine, never mind any open files.
# discuss-Roo-roadmap
- ## 

- ## 

- ## [Feature Suggestion: Enhancing Extensibility with a Modular Framework : r/RooCode _202511](https://www.reddit.com/r/RooCode/comments/1ot7qwp/feature_suggestion_enhancing_extensibility_with_a/)
  - Observing the ecosystem, agents like Claude Code are leveraging skills, sub-agents, and plugins, while tools like cline have implemented hooks. These mechanisms are proving to be crucial for extending the core functionality of coding agents.
  - I would like to suggest that roo code consider adopting a similar modular approach to enhance its extensibility.

- ## [[ENHANCEMENT] Text size setting for Roo UI (Small/Medium/Large, no VS Code zoom) _202509](https://github.com/RooCodeInc/Roo-Code/issues/8100)

- ## [Preliminary Work for Roo Code to Support JetBrains and CLI _202504](https://github.com/RooCodeInc/Roo-Code/discussions/2536)
  - Currently, the Roo Code project is only a VS Code extension and is tightly coupled with the VS Code platform
  - To move in this direction, a few tasks are required:
  - Refactor the project structure: keep webview-ui and src, and add a plugins/ directory.
  - Add implementations for plugins/jetbrains or plugins/cli.

- 202508: Just open-sourced the plugin that enables Roo Code to run within JetBrains IDEs.
  - https://github.com/wecode-ai/RunVSAgent /apache2/kotlin
  - Run VSCode-based coding agents and extensions seamlessly within other IDE platforms - bridging the gap between VSCode ecosystem and other development environment.

- ## ✨ [Plans for CLI? : r/RooCode _202510](https://www.reddit.com/r/RooCode/comments/1o8cztn/plans_for_cli/)
  - Now that cline has one, can this be ported into Roo? 

- No. Why would we want a CLI? We have cloud agents coming out Monday.

- Many valuable use cases for scripting / CI, multiagent etc.
  - Our Roo Code cloud agents will allow for CI workflows.
  - I don’t understand what you mean by multiagent. I currently run 10+ instances of Roo working on the same repo using work trees and subagents are basically subtasks that Roo already has (though we could improve our subtask/subagents to be able to work in parallel).
- cloud agents sounds like a product like codex cloud / jules, etc, is that right? i'm thinking more about a drop in replacement for the 'headless' capabilities of gemini cli, claude code, etc.
  - They both have vs code plugins for a reason.

- If you need one, tell Roo to give you one.

- ## [Roo Code CLI : r/RooCode](https://www.reddit.com/r/RooCode/comments/1laswrx/roo_code_cli/)
  - Roo code is really great, so I wanted to extend its capabilities to more automated flows. So, has anyone tried to use it in a containerised environment to parallelise multiple tasks? Has anyone figured out ways to interact with Roo using CLI?

- Yep. I have it running in a code-server container. I spent a shitload of time getting it to take actions via the Unix socket but that was fragile AF. I just got a vs code extension setup with a simple rest end point take takes actions and passes them to the the roo-api.
  - Once I get the vs code extension too-api/ roo-code interface happy, I plan on adding a MCP server as input and exploring a websocket interface. My ultimate goal is to have an input as a GitHub runner like I have working well in Claude code.

- Roo has an evals system that runs multiple instances of VSCode headlessly in parallel inside of Docker 
  - Roo is controlled remotely via an IPC socket that exposes a simple API for running tasks and listening for events.
  - Here's a basic demonstration of that: https://github.com/cte/roo-cli
  - If I were going to build a proper cli for Roo I would create a mapping between cli commands and the internal API and spawn containers to run tasks and then communicate with them via IPC.

- ## [Official Re-Integration of Gemini CLI · Issue · RooCodeInc/Roo-Code _202508](https://github.com/RooCodeInc/Roo-Code/issues/7353)
  - If RooCode provides proper library-based integration, it will meet the needs of users who want to use Gemini CLI in a secure and sustainable way.

- [Add Gemini-CLI provider · Issue · RooCodeInc/Roo-Code](https://github.com/RooCodeInc/Roo-Code/issues/6043)
  - This was already present in Roo and was removed due to licensing issues, so not likely.
  - the Gemini team themselves asked us to remove it.

- [feat: add Gemini CLI provider integration by roomote[bot] · Pull Request · RooCodeInc/Roo-Code](https://github.com/RooCodeInc/Roo-Code/pull/7516)
  - Still not approved by the Gemini team

- ## ✏️ [Unnecessary Full-File Edits for Small Code Changes · Issue · cline/cline _202410](https://github.com/cline/cline/issues/583)
  - I’ve noticed a behavior that feels like a bug when working with large code files. When I need to make small changes—perhaps modifying only a few dozen lines—cline often invokes the `edit file` tool to update the entire file from the beginning, even when 99% of the file doesn’t need any changes.
  - this behavior of editing the entire file seems unnecessary and inefficient when only small parts are being modified.
- My previous experience with patch file syntax is less than ideal - tricky to manage, tricky for the LLM's to get right, so I've been playing around with an alternative implementation, inspired by Aider's logic, added two tools: Search And Replace and Insert Code Block to try to work around this issue.
  - As a side note, it seems the previous PR #158 is stale, since it used the previous JSON Schema style of tools - should be simple to adapt to the new XML notation though, haven't tested it - it uses the patch logic, could also work.

- I've experimented with structured output like editing certain lines or unified diff format like aider, but I've found the results aren't nearly as good as whole file outputs. 
  - The reason is these models are trained on significantly more whole code files than say diff patches, and there's been studies showing drops in performance whenever you force the models to output in a structured way ie diff or json.
  - OpenAI just released a new API featured called predicted outputs that would fix this issue entirely.

- I don't understand how you expect this to be solved by OpenAI's upcoming API feature. This project is meant to be compatible with most models, whether hosted locally or by dedicated providers.

- ## ⚡️ [Add a 'compact prompt' option for local LLMs · Issue · RooCodeInc/Roo-Code _202508](https://github.com/RooCodeInc/Roo-Code/issues/7550)
  - When using Roocode with local llm providers (like LM Studio ), API requests regularly stall and hit the 300s timeout This happens with browser/mcp tools disabled
  - The cause seems to be that roo always builds a very large prompt/context, which local models (running at 7–10 tok/sec) cannot process fast enough
  - Other Vscode extensions i tested (Cline, Void, Kilocode) remain usable under the same conditions because they send by default a more compact prompt, Cline also introduced a 'compact prompt' option that reduces context size when a local provider is selected

- This is a complex and interesting proposal. We do not have enough internal conviction to commit right now.
  - If someone in the community can put together a small MVP, we will revisit.

- ## [Support for Alternative Vector Databases in Codebase Indexing _202507](https://github.com/RooCodeInc/Roo-Code/issues/6223)
  - Users are limited to Qdrant as the only vector database option for codebase indexing
- thank you for the proposal. At the moment, we're not looking to add in-process vector storage solutions. However, we are open to supporting external vector stores like ChromaDB.

- That makes perfect sense - external vector stores are definitely the better approach for production environments and offer much more flexibility and scalability.
- Phase 1: Core Architecture
  Implementation of a generic vector store adapter/interface
  Initial concrete implementation for Qdrant as reference
  Corresponding tests and documentation
- Phase 2+: Additional Stores (separate PRs)
  ChromaDB integration
  Further vector stores as needed (Pinecone, Weaviate, etc.)
- This incremental approach will allow us to refine the interface based on learnings from the first implementation and review each integration in isolation.

- [Add Sqlite with sqlite-vec as an alternative for Codebase Indexing _202508](https://github.com/RooCodeInc/Roo-Code/discussions/7280)
  - What you need is already there, but you have to wait

- ## [Indexing Code Base _202501](https://github.com/RooCodeInc/Roo-Code/discussions/411)
  - Is it possible to have an indexing codebase feature, similar like Cursor. This allows analyzing & Grep searching of codebase files much more efficiently and super fast too. 
- Perhaps MCP could be adapted for this? There is an MCP sever for qdrant - perhaps we could use a script to periodically ingest the codebase (and preferred documentation?) into Qdrant, and Cline could reference it using MCP?

- it could be done, but glob search is easier, but only useful for finding related files based on task.
  - the problem is we need to maintain this embed somewhere, we could potentially provide it via 3rd party.
  - but MCP server is good option for now to do this 

- Why Not just use LanceDB like Continue.dev? or Sqlite3 with Vector Extensions? or TursoDB which has Vector Embeddings Support?

- ## [Layered and modular memory management _202508](https://github.com/RooCodeInc/Roo-Code/issues/6602)
  - Currently, Roo Code’s memory mechanism suffers from the following issues:
  - When using a prompt-based “memory bank, ” two problems arise: • When the AI is expected to read memories automatically, it often skips or fails to retrieve relevant memories because of prompt-compliance failures or retrieval shortcomings. If the entire memory bank (or all documents) is placed directly in .roocode/rules/, every memory is forcibly sent to the AI. This wastes tokens
  - The RAG-based code-semantic indexing feature is worth mentioning, After a few initial trials I abandoned it because retrieval quality was poor

- This isn’t currently on the Roo Code roadmap
  - this behavior can be closely replicated using [custom modes](docs.roocode.com/features/custom-modes). You can define a workflow that reads memory files based on directory structure, giving you most of the hierarchical memory functionality described here.

- ## [Roo Memories feature and Internal Memory Bank feature _202505](https://github.com/RooCodeInc/Roo-Code/discussions/3264)
- Check the MCPs, there are too many options for "memory bank" as a concept in general
  - but direct integration would be nice rather than mcps

- [Please Add Memory Bank  ](https://github.com/RooCodeInc/Roo-Code/discussions/1954)
  - Please add a memory bank feature—like “cline” and Roo Code Memory Bank—that stores code snippets and context across sessions. This would help users quickly reuse important info and streamline development.
- If it is an MCP, better to find ways to optimize the link between Cline/RooCode and different tools... even Task Masters don't link well with memory tools, including the graph-based ones, and that is slightly frustrating

- ## 🧠🏠 [Implement memory bank directly in Roo Code instead of configuring system instructions _202505](https://github.com/RooCodeInc/Roo-Code/issues/3312)
  - Memory bank (See here: GreatScottyMac/roo-code-memory-bank) helps Roo code have a better project understanding by writing a detailed project brief. This way, Roo code has more context about your project. The memory bank is also updated on the fly. 
  - The problem is that you need to go out and configure Roo's system instructions (You have per mode instructions) and initialize Memory bank by asking Roo code to do it for you. 
  - You also need to add the memory bank directory to your .gitignore.

- I have avoided using any of the various memory bank solutions. While things like this do work and do improve the experience of using Roo, if anything is going to be officially supported by Roo, I would hope that it would be some kind of `Vector/Graph RAG` storage system, something that isn't just shuffling around `.md` files. It would certainly reap long term benefits for Roo and the Roo Community .

- While a full-blown RAG would be awesome, an optional memory bank with a somewhat standardized structure is a step in the right direction. I'm using Roo within something like a DDD (documentation-driven development) and have to implement something like this with custom prompts.

- 💡 I think of the memory bank `.md` as a notepad for a person with amnesia. In that it does not solve the problem but provides a meaningful workaround at the expense of maintenance cost and time. Real memory solutions (ones closer to human long-term memory) will exist alongside documentation.
  - Likely all the difficult things (competing in memory benchmarks, etc.) can be offloaded to memory providers and all Roo needs to do is connect with API credentials. Roo avoids rolling its own and focuses efforts on meaningful integration.

- I'm about to release a type of memory MCP server that works along with custom instructions for the LLM. The custom instructions can be tailored to many different IDE extensions and agentic AI interfaces.
  - There's a chance that this might work well enough so that Roo Code could use a dedicated "Documentarian" mode which will handle all interactions with the MCP. For instance, when another mode is ready to attempt completion, it will instead switch to documentarian, which will determine what if any data should be logged from that task. The it will do the attempt completion.

- I don't think adding memory bank to Roo is/will be necessary with some features that are being worked on recently like codebase indexing the Roo Marketplace.

- Playing with multiple "project memory" frameworks, and ending up inventing my own version anyway, I've come to believe that any implementation (i.e. what to consider important enough to keep in the memory and how to categorize it) will by definition be very opinionated. I think this shouldn't be a part of the general-purpose system such as Roo.

- ## [[Feature Request] Improve Code Index search results by implementing Reranking _202507](https://github.com/RooCodeInc/Roo-Code/discussions/5539)
  - Proposal to implement a robust, efficient reranking module. Building on the momentum from completing Code Index, the objective is to enhance search result precision, optimize token usage, and implement yet another common feature that is implemented in other mature tools.
  - Reranking is the logical next step to undertake after completion of the Code Index project.

- if you wanna use a massive model to do the work of what a smaller model can do more effectively--the brute force method always suits.
  - But embed+rerank model pairs are still being released (see Qwen3-Embedding and Qwen3-Reranker as just one SOTA example, and currently top of MTEB leaderboard).
  - I mean so many other parts of this project are about really finessing the actual instruction and context given to each task, so there really isn't a reason not to do rerank next.

- ## 🤔 [autocomplete function cannot used · Issue · RooCodeInc/Roo-Code _202509](https://github.com/RooCodeInc/Roo-Code/issues/7591)
- Roo Code is a chat-based AI assistant that helps with coding tasks through a sidebar interface. It doesn't provide inline code autocomplete/IntelliSense features like some other extensions do.

- We have no plans to implement something like this at the moment

- ## [Add features from the Continue project: Autocomplete, Embeding indexing, Rerank _202503](https://github.com/RooCodeInc/Roo-Code/discussions/2004)
- Autocomplete & here so I can choose a different model for this task such as Qwen Coder or Codestral.
  - Embed model for indexing local files and context retreval.
  - Reranking model to improve Embedding retreval quality.

- ## [Add Autocomplete support · RooCodeInc/Roo-Code _202501](https://github.com/RooCodeInc/Roo-Code/discussions/446)
  - Is it possible to add autocomplete support?
  - And ability to configure a separate (weak) model for that.

- just like Continue but with a better UI/UX 

- In general soe of the Continue's features are helpefull in addition to Autocomplete: Embedding for indexing local files ad retreval for context & Reranking to improve the embed.

- auto-complete requires utilising a good FIM model.
# discuss-vscode-ext-ai
- ## 

- ## 

- ## 

- ## 

- ## [Anyone tried Cline, Roo code, Kilo Code. Which was the best and productive among them? : r/CLine _202509](https://www.reddit.com/r/CLine/comments/1nqy92m/anyone_tried_cline_roo_code_kilo_code_which_was/)
- I like Roo for the different custom modes and the codebase indexing myself. And the Copilot experimental integration. It burns more tokens on the 1x models, but works well on the 0x.

- kilo works best for my needs. I've primarily stuck with free models for Development, and Kilo's plug-in is the only one that seems to reliably detect when Chutes is rate limiting and retries with an exponential backoff.

- Tried Roo Code then migrated to Cline. Feels too many knobs to turn in Roo to get satisfying result, Cline is just work out of the box.

- Cline just added voice transcription which is pretty cool.

- Roo seems to follow rules better and encounters fewer errors related to context window overflow. I like how easy it is to set up different model profiles.
  - Although Cline seems to be able to transfer context to a new task more easily and roll back to an earlier point in the task to clear context more easily.

- Been a cline user for a long time. I have been using Copilot more and more - with the addition to automatic task tracking, it's gotten much better.
  - yes, tested cline for a while but ultimately switched back to Github Copilot. In the end it was faster and more efficient. Cline always patches / edits were slow and error prone

- For pure coding tasks I like codex. For tasks that require a mix of some "devops" as well, I prefer Cline. I try Roo every so often, because it looks like it has all kinds of cool features. But in the end Cline is just that more robust.

- ## [Experiences Using Cline and Roocode with Different AI Models : r/RooCode _202508](https://www.reddit.com/r/RooCode/comments/1mxxiob/experiences_using_cline_and_roocode_with/)
- I’ve been working the past few months with both Cline and Roocode at the same time.
- Using the same modes, I’ve also tested which AI engine handles tasks better. Here’s the trend I noticed:
- Gemini: does better at documentation and analysis, 
  - but its problem-solving is often convoluted or doesn’t respect the style of the existing codebase (classes, internal functions, etc.).
- ChatGPT (4.1): executes tasks well, but when documenting through MCP it doesn’t update ClickUp. 
  - Instead, it creates .md files on how documentation should look, but never pushes it to ClickUp. 
  - It also tends to redevelop functions that already exist, or write new ones and then not use them—yet it marks the task as done.
- DeepSeek: not great at problem analysis, but it integrates smoothly with ClickUp. 
  - It assigns correctly, creates modification plans (.md files) and then deletes them (unlike ChatGPT, which leaves them hanging). 
  - Its problem-solving also keeps the same coding style consistent with the surrounding context (class, function, workspace).
- As for Cline, I find it great for seeing how tokens are managed, and in general it’s faster at resolutions. But it feels limited for analysis and refactoring.

- Deepseek 3.1 works really well with tool calls. I've actually never had it fail a tool call across many different front ends.

- I noticed that models from Claude are superior to others in real coding in a large (even medium) code base. When working with a chat (outside of IDE), all are about equally good. But when the request is inside IDE, Claude has much fewer errors that require improvement.

- ## [Recommendations for Local LLMs (Under 70B) with Cline/Roo Code : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lco9ik/recommendations_for_local_llms_under_70b_with/)
- For me Devstral q8 works well in Cline's planning mode with tool calls. For code mode I like to use Qwen coder 32b q8. This works only on Cline for me; I could not get anything useful out of Roo Code with these models: it is always running into loops

- devstral without quants works , but you need 40k context size I would guess.

- why not try the qwen2.5-coder variants instead of the general Qwen 3?
  - I tried!!! Not a good experience, but is very capable when ask to code a specific function direct in webui chat

- ## [Cline vs Roo Code - currently? : r/ChatGPTCoding _202506](https://www.reddit.com/r/ChatGPTCoding/comments/1ljlpei/cline_vs_roo_code_currently/)
- Roo has eclipsed Cline in just about every way. If you don't mind spending though, Claude code. Then take it ome step further and use Claude code with Roo
- I still use and prefer Cline — the plan/act mode is just more straightforward and easier to work with.
  - Doesn't Roo have equivalent modes though?
- Not quite. Roo has more and it has a decent set built in with "boomerang" tasks. You can create your own custom modes. Plenty of flexibility.

- ## [Cline vs Roo : r/CLine _202505](https://www.reddit.com/r/CLine/comments/1kgy185/cline_vs_roo/)
- Roo has grown more powerful and configurable than Cline. But this embrace of complexity has made Roo less approachable for beginners, I suspect.
- I’m switching from cline to roo now and it’s a small learning curve. I do prefer Roo more now due to the better UI and boomerang mode. I miss the /newtask amd /smol commands from cline though.
  - Roo does this automatically when the it reaches the end of the context window
- FYI you can create a .clinerule that tells Cline to "use the new_task tool when reaching 50% of the context window"

- Aider much more better it use less token if you are experienced programmer that can include all context correctly.

- ## [Which is best( Cline or Roo code or Kilocode) : r/CLine _202507](https://www.reddit.com/r/CLine/comments/1m307gr/which_is_best_cline_or_roo_code_or_kilocode/)
- Roo is hands-down the best tool I’ve ever used. I’ve tried Cursor, Windsurf (you name it) but nothing comes close. 

- Roo Code. Cline feels too restrictive. It's the best for learning, but as soon as you know how to use LLM code generation, then Roo feels more powerful.

- I second this while I can agree to other opinions especially about Cline's rather stable releases. Personally I prefer Roo Code's adventurous/agile updates but YMMV.

- I recently switched to Roo for one reason--they added embedding for search in the codebase and I had Azure credits to burn. That made it worth the switch for me and I had moved away from using memory-bank. I'm liking Roo but I feel like there's a complexity level that doesn't always provide a best fit depending on your situation.

- I think Roo is best, but the system prompt has mistakes/is not ideal, so you have to fork it, change it and compile it yourself or you will get a very annoying yellow banner which makes the ui ugly af.

- Cline: is best for small changes or changes that edit 1-2 files. It isnt too good for complex that requires to edit 2-4 files
  - Roo code: 1- It is best for complex tasks that needs to edit multiple files as it uses to do list but its burning tokens when the task is small. 
  - 2- its best for debugging without any doubt 
  - 3- ask mode is veryyyy useful 
  - 4- it gives you best experience if you use too many models or trying to stay on free side as it has profiles that you can set ( multiple google accounts = multiple api keys) u can change them easily with profiles as you hit the limits

- ## 🆚 [RooCode vs Cline  : r/RooCode _202503](https://www.reddit.com/r/RooCode/comments/1jn372q/roocode_vs_cline_updated_march_29/?share_id=8QGnCavUI2VCyv7oNIryz&utm_content=2&utm_medium=ios_app&utm_name=ioscss&utm_source=share&utm_term=1)
- Features Roo Code offers that Cline doesn't:
  - Diff Mode Toggle**: Enable or disable diff editing
  - Diff Match Precision**: Control how precisely (1-100) code sections must match when applying diffs
  - Wildcard Command Auto-Approval**: Use * to auto-approve all command executions (use with caution).
  - Boomerang Tasks (task orchestration / subtasks): Create new tasks from within existing ones, allowing for automatic context continuation. Child tasks can return summaries to parent tasks upon completion ("Boomerang"). Includes option for automatic approval.
  - Temperature Control**: Configure model temperature per Provider Configuration.
  - Custom Rate Limiting**: Configure minimum delay between API requests to prevent provider overload.
  - Auto-Retry Failed API Requests**: Configure automatic retries with customizable delays between attempts.
  - Human Relay Provider**: Manually relay information between Roo Code and external Web AIs.
  - Footgun Prompting (Overriding System Prompt)**: Allows advanced users to completely replace the default system prompt for a specific Roo Code mode.
  - Terminal Output Control: Limit terminal lines passed to the model to prevent context overflow.

- Features Cline offers that Roo Code doesn't YET:
  - MCP Marketplace: Browse, discover, and install MCP servers directly within the extension interface
  - Notifications: Optional system notifications for task completion.

- ## [Roo Code vs Cline - Feature Comparison : r/ChatGPTCoding _202502](https://www.reddit.com/r/ChatGPTCoding/comments/1imtvv4/roo_code_vs_cline_feature_comparison/)
- hy is Roo a fork vs. pushing improvements into Cline
  - Different approach. Cline focuses on making like a more polished and tested product while roo code is focused on the speed of improvement accepting a lot of PRs from contributors. Which makes sense since Cline guys are working also on the enterprise version (at least they say so in their website)
- because cline is not community friendly for devs who have provided PRs, only 5% of all PR get implemented. Roo is developer friendly.

- Aider is much different but an amazing piece of software. Less autopilot and more manual involvement. Also aider uses way less tokens.

- ## [Does Cline do tab autocompletion? : r/ChatGPTCoding _202501](https://www.reddit.com/r/ChatGPTCoding/comments/1id5pcm/does_cline_do_tab_autocompletion/)
- it looks like they do not
  - [Tab Autocomplete (line-autocomplete, such as Cursor Tab) · cline/cline _202412](https://github.com/cline/cline/discussions/1083)
  - it looks like I can configure continue.dev to use openrouter and put some of those credits I initially bought for cline to good use.

- You can also try Supermaven, which is quite good for a free offering.
  - I second Supermaven. I used to use continue.dev with the free codestral api, but I’ve found it to not be very comparable to Cursor.
- It looks like Supermaven is acquired by Cursor:

- ## [Cline Vs Roo Code is the only comparison that makes sense if code quality is important for you, IMO : r/ChatGPTCoding _202504](https://www.reddit.com/r/ChatGPTCoding/comments/1k3q8z7/cline_vs_roo_code_is_the_only_comparison_that/)
- I work with 7k C++ and 3k Java files, and I see little difference between Cursor/Windsurf/Cline/Roo. Currently, I use the Windsurf plugin in IntelliJ.
  - I switched to Cline from Cursor because I didn't like Cursor's handling of external file changes. However, I saw little to no improvement in code generation. But I lost autocomplete, which is incredibly useful at times

- try Gemini 2.5 Pro in Plan + DeepSeek V3 in Act mode. Very good cost benefit.

- RooCode Boomerang + Memory Bank makes lots of different. I tried Windsurf during 4.1 free week & it generate codes with limited context or search. 

- you can run vscode + roo code in a webpage using code-server

- I have really gotten to like the Github Copilot way of handling file edits in agent mode. It saves the files, so you can test if everything works, but there is an immediate rollback button. It's also very clear which files in lines in them are modified. This is I think the main reason for me to use it over Roo. 
  - Roo does have a rollback button but I have to do some digging to see what has been altered where and how to roll back a specific change.

- ## [My experience with Cursor vs Cline after 3 months of daily use : r/ChatGPTCoding _202502](https://www.reddit.com/r/ChatGPTCoding/comments/1inyt2s/my_experience_with_cursor_vs_cline_after_3_months/)
- Cline doesnt understand shit by default. But once you add memory bank and populate it + keep each file under ~250 lines of code it works like magic
  - You can also utilise google gemini think for writing complex tasks for cline. Repopack code + memory bank and load into ai studio. Tell it to write MD plan for your task
  - PS Keep each module (isolated part) of your project under 100k tokens
- You cant optimize much. Disable MCP, keep memory bank under 15k tokens, keep project modularized and low coupled

- Should add “keep each file under ~250 lines of code” to the rules
  - Now its different. Even flash thinking can handle 500-1000 lines files
  - I mostly use task-master -> claude-code / roo code (2.5 flash think as orchestrator, 4.1 as code from VS LM API)

- Cline , Roo Cline an Even Cool Cline are abased off Cline.

- I've had a lot of luck with gemini flash, but yeah claude still seems to be the best for complex coding tasks

- ## [I Use Cline for AI Engineering | Hacker News _202502](https://news.ycombinator.com/item?id=42900137) 
- I think Aider, Cline and Cursor are not far from each other in their capabilities.
  - Cursor was probably the most polished experience - especially their `Tab` autocomplete.
  - Cline does the job really well if you're in VSCode. Aider is great if you prefer terminal based workflow
  - Another great thing in Aider is `//AI!` comment. You can start Aider in --watch-files mode and it will watch for instructions, and start executing them. This way I can work in my preferred editor and have a tool in the background performing AI tasks.
- How has no one pointed out the business models are different and result in entirely different products and priorities?
  - Cursor charges $20/mo. So their whole business model revolves around using less than $20 worth of tokens and cheaper models.
  - With Cline, you pay for your own tokens and can choose whichever model you like (uses openrouter).
  - You can see the difference almost immediately - everything is better. Context management isn’t kneecapped, edits are comprehensive, cline reads every file that is relevant into the context, and the UX is intuitive.

- The architect mode in aider is basically a one step planning pass.
  - RA. Aid goes way beyond this. It will run fuzzy find, ripgrep, directory listings, web search via, ask the expert (reasoning models), multiple task planning, execution of shell commands and unit tests, etc.
  - It essentially follows a research, planning, and implementation cycle much like a human SWE would.
- As far as I can tell aider does most, if not all, of that as well. The only things I'm unsure about is "ask the expert" and "multiple task planning"

- Roo Code (formerly Roo Cline) is a fork of Cline that gets rave reviews
  - People (well, me in that case) were asking for more fine grained options like per project instructions, and the Cline author's response was basically "not interested in the added complexity but feel free to fork". So somebody did.
- I find RooCodes mode selector drop down inferior to the way Cline handles Plan and Act mode.
# discuss-web-coding
- ## 

- ## 

- ## [Remote management options : r/CLine _202502](https://www.reddit.com/r/CLine/comments/1ixke6k/remote_management_options/)
  - I am looking for the ability to interact with cline running on my local computer via my cellphone. I am using cline heavily, and often have it confirm its changes are working by running a testing suite.

- Vnc has worked for me

- Get a server (Contabo as low as $5 per month) > Install Docker > Install VS Code Sever > install Cline Extension > Set reverse proxy on your VS Code Server (e, g code-server.mydomain.com) > Access it on any browser > Do your thing!

- ## [Can I run a relay for cline or roo etc for web chat. Anyone done this? : r/vscode _202509](https://www.reddit.com/r/vscode/comments/1nn8x2d/can_i_run_a_relay_for_cline_or_roo_etc_for_web/)
  - I’m wondering if anyone has success or experience in running a relay to code extension like cline or roo to a external web chat etc.

- Yep—people are doing this, but the paths differ:
  - Roo Code: Easiest. Use Roo Cloud (Roomote Control) — it gives you a web chat that talks to your local Roo in VS Code. No extra glue needed.
  - Cline: No built-in web chat/relay. Two workarounds:
    - OpenAI-compatible proxy (LiteLLM, Vercel AI Gateway, Portkey, OpenRouter). Point both Cline and your external web chat at the same proxy → shared models, centralized keys/rate limits/logs. Doesn’t “control” Cline UI, just unifies the backend.
    - DIY bridge via MCP (Model Context Protocol). Run/make an MCP server that your web chat talks to, and wire it to Cline/browser-use. Works, but you’ll write glue code and handle auth/state yourself.
- If you want true remote control (start tasks, see plan, approve steps) without touching VS Code, Roo’s cloud is the clean option today. For Cline, it’s proxy or DIY.
# discuss-internals-coding
- ## 

- ## 

- ## 

- ## 

- ## because we built opencode as a client/server model from day one, 100% of it's functionality is available as an API _20251026
- https://x.com/thdxr/status/1982129382106816535
  - this includes non-LLM functionality like searching for files

- All logic server side. Deploy it locally for free use => Land & Expand on dev laptops
  - The same API can be deployed as a SaaS product or self-hosted enterprise for governance
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Codex CLI vs Claude Code vs Claude Code + Z.ai API — which one’s worth it? : r/ClaudeCode _202509](https://www.reddit.com/r/ClaudeCode/comments/1nepo9y/codex_cli_vs_claude_code_vs_claude_code_zai_api/)
- I use CC to analyze and generate tasks, which I then use with GLM to complete. It works quite well and does a more than acceptable job.

- Codex CLI is genuine crap. Anything is better than codex CLI as tool.
  - Codex cli uses freaking toml, huge red flag.
  - There is not local mcp config, no way to share it or version it for project.
  - And tool configuration... I didn't comprehend it.
  - their SDKs are nightmare to work with, literally made by smartasses who never worked with direct clients.
- literally every cli tool tries to be compatible, where codex just being special.

- ## [Cline vs Claude Code with the same model? Which one wins? : r/CLine _202510](https://www.reddit.com/r/CLine/comments/1nvvt81/cline_vs_claude_code_with_the_same_model_which/)
  - So cline (or roocode) vs claude code cli - while using sonnet of GLM4.5 - is there a difference between using the same model with different tools?

- Between the VSCode extensions and the CLIs, I find CLIs more practical. 
  - They do native tool calling, use fewer API calls - which means lower cost - and they're much faster when doing the same task with the same model and provider. 
  - Out of all the CLIs, I like Claude Code the most. When I run it from VSCode's built-in terminal, it can open the code changes right inside the editor, so I can check what's been changed before I accept it. 
- From the group of VSCode extensions, I go for Cline. 
  - RooCode and especially KiloCode offer more features, but for some reason, Cline seems more reliable when editing files. RooCode and KiloCode sometimes fail, which is odd since the are all similar  - especially since KiloCode has a feature called MorphLLM that's meant to make edits more accurate and quicker when enabled, but I still run into issues even with it turned on.
- The fast apply (morph) is just another opportunity for the diff edit to fail and is a relic of the pre-3.5 sonnet era. I don't understand why they did that
  - So they could say they did something.

- Usually I open multi repos workspace and Cline is bad on this. Also the way it preset context. It confuse more the model rather than help.
  - Cline leverage greatly LSP and the files you open. That works great if you do that. But I don't do that usually more used to point to files independant from what's open. It's a design. I can disable that in Roo Code at least.
  - Also Cline will tend to confuse root workspace with project root.

- For history Cline is not the same as RooCode. RooCode consumes 2-3x the tokens Cline or Claude Code will use for the same task.
  - I wish it was false as I used to be a RooCode fan. Not any more. Using Coder or Architect is 2x on Sonnet via VertexAI, 3x on GLM 4.6 via their Subscription (used 2 days ago) and not only that, using Requesty with Grok-Code-4-Fast is consistent 3x on every request. Even requests like analyze this repo.

- Parallel agents is the best part of Claude code

- I havent used CC but it seems that it needs more work to correctly set it up and get the most out of it. Meanwhile Cline seems way easier to get started with.

- ## [Why do most people prefer CLI over VSCode extension? : r/ChatGPTCoding _202510](https://www.reddit.com/r/ChatGPTCoding/comments/1o2y0uf/why_do_most_people_prefer_cli_over_vscode/)
- Because it makes it IDE-agnostic.

- I don’t like vscode

- why not both, I tend to let long running processes run in a cli in a dedicated window and work in an ide in separate section.

- Because CLI (at least Claude Code, and probably others) has an `/ide` setting which shows the diff in the IDE -- and there's nothing to prevent you from using both CLI and IDE extension anyway.

- Because currently most of the extension have to live within the sandbox of what vs code allow you to extend off so it is restrictive, if you want more control you have to fork like cursor and the like. 
  - But cli basically bypass most of the restriction and it is mostly a much cleaner UI.

- [Why do most people prefer CLI over VSCode extension? : r/codex](https://www.reddit.com/r/codex/comments/1o2xzkx/why_do_most_people_prefer_cli_over_vscode/)

- I can easily run in parallel

- I see 3 reasons -
  - for pure vibe coding you don’t need to see diffs and code in general at all - and terminal serves better in that case
  - For hardcore devs (who code manually a lot) - terminal is still a very natural experience and easier to do with keyboard only
  - Run in parallel

- I also prefer the VSCode extension. One HUGE advantage is that I can easily go back to previous conversations.

- the CLI is more powerful, more customizable, and the IDE GUI is already optimized for what it contains, adding another always open window adds unnecessary clutter.

- Why would I use vscode when I have the superior vim?

- Devs mostly prefer CLIs because they're used to command lines, non-devs prefer extensions because they're used to GUIs

- ## 🆚🤔 [Why CLI is better than IDE? : r/RooCode _202507](https://www.reddit.com/r/RooCode/comments/1lqgu3j/why_cli_is_better_than_ide/)
- You don't get it because you don't know Claude code has a diff window in VSCode and you can do exactly what you described maybe ? 

- You can place a CLI tool in a pipeline, on a remote server, you can call it with a web hook. IDE integration is just another layer of abstraction

- You can use the CLI based tool in a CICD pipeline for example

- I like both but one of the biggest constraints is automation. CLI tools just make this easier.

- They’re not better. Lighter weight. Claude code is popular because it’s so cheap.

- Some people appreciate that a CLI is lightweight and feels like a regular Unix tool.
  - Personally, I strongly prefer using an IDE. Anything you can do in a CLI, you can also do in an IDE, often more comfortably. The ability to navigate and edit files immediately during or after changes is extremely convenient. I can work on configuration files alongside the project itself, and I still have access to all my usual VS Code extensions.
  - I still use Claude Code for batch operations, but otherwise, Roo Code (especially with InferSwitch in additon to Roo modes) has been by far the most convenient and productive toolchain I’ve found.

- Those focus is a lot less on code where in your ide the editor and file explorer are taking up 70 percent or more of the viewable space. Where the cli is more focused on the prompting and following the agents flow.

- I'm not a CLI guy, I usually use my IDE and do everything UI based, but I prefer Claude Code because:
  - What is done in the terminal visually is not bad, actually better than some bad UI, but I miss selecting my own text or using the mouse to navigate my own prompt.
  - It still integrates with VS Code and I can see the diff view when making changes to files.
  - Sometimes less is more. It forces me to use it more instead of tinkering more. I have a tendency to overthink and optimize everything. With CC, it feels like I have to just trust CC with how it manages agents in the background, and it works.

- Gemini CLI can just run in a terminal within VS Code and now there's even a Gemini Code Assist extension for VS Code that works similar to RooCode and enables Code agents. Gemini CLI can also use MCP servers. The main benefit to using it is you get a lot of usage for free

- Because it's trendy and people believe (wrongly) that it produces better results than other options.

- As far as I understand it, code code is not better because it's in the CLI, it's (potentially?) better for some tasks because of the way Anthropic have built its tool use in conjunction with its own model. There have been chatbots interfaces released recently like 'Claudia'/opcode, which give you Claude code in a chat UI

- It is annoying that IDE tools take over the entire editor and I can’t do anything but watch it. A cli tool can make edits in the background while I’m also working in the editor.
