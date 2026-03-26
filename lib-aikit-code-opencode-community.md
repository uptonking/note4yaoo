---
title: lib-aikit-code-opencode-community
tags: [community, opencode]
created: 2026-01-17T22:41:11.548Z
modified: 2026-01-17T22:41:25.867Z
---

# lib-aikit-code-opencode-community

# guide

# discuss-stars
- ## 

- ## 🐛 [OpenCode concerns (not truely local) : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rv690j/opencode_concerns_not_truely_local/)
  - when you run opencode serve and use the web UI --> opencode will proxy all requests internally to https://app.opencode.ai!
  - There is currently no option to change this behavior, no startup flag, nothing. You do not have the option to serve the web app locally, using `opencode web` just automatically opens the browser with the proxied web app, not a true locally served UI.
  - There are a lot of open PRs and issues regarding this problem

- They've shown other questionable practices as well; refusing to merge PRs that show tokens-per-second metrics and with OpenCode Zen (different product from OpenCode but one of their monetization avenues), providing no transparency about their providers, quantization, or rate limits.
  - There's a lot of VC money behind OpenCode, so don't forget about that.
  - And regarding yourt post, locking down their default plan/build prompts and requiring a rebuild of the app has always struck me as a weird design choice.

- I understand it only concerns the webui?
  - yes, as far as I can tell TUI is unaffected
- How is it with the OpenCode Desktop app?

- The other thing is I believe without building from source there is no way to customize/override the system prompts right?
  - Last time i checked they had a really long and obnoxious system prompt for qwen which made it keep reasoning circularly.

- Take a look at nanocoder. It’s a project for a truly open source claude code. https://github.com/Nano-Collective/nanocoder

- Also please be aware that the very first thing that the TUI does is to upload your initial prompt to their servers at https://opencode.ai/zen/v1/responses in order to generate a title. It does this regardless of whether you are using a local model or not, unless you explicitly disable the titling feature or specify a different small_model. You should assume that they are doing anything and everything they want with this data. I wouldn't be surprised if later they decide that for a better user experience they will regenerate the title once there is more prompt available.

- I had the same concerns and found RolandCode. It's a fork of OpenCode with telemetry and other anti-privacy features removed. https://github.com/standardnguyen/rolandcode

- ## OpenCode's codebase is very high quality. Which is unusual for an app built with AI. This makes me curious how @thdxr uses AI to code. _202603
- https://x.com/kianmckenn/status/2030087262239592690
- @kitlangton has a good metaphor. it's like tending a garden. can let ai code grow but you have to aggressively clean up after it and be diligent about architecture and patterns. codebase is ok it will get better
- https://x.com/thdxr/status/2018051250785272127
  - now i can actually refactor everything when we find a better way of doing something
  - before shitty code just lingered forever

- spend more time weeding than planting these days. the ai output is fast but the cleanup compounds if you skip it for even a day

- ## 🚀 [Kilo CLI 1.0 just launched - built on OpenCode as its open-source foundation : r/opencodeCLI _202602](https://www.reddit.com/r/opencodeCLI/comments/1qvo002/kilo_cli_10_just_launched_built_on_opencode_as/)
  - [Kilo CLI 1.0: Built for Kilo Speed _202602](https://blog.kilo.ai/p/kilo-cli)
  - Kilo CLI 1.0 just dropped, and it's built directly on the OpenCode server as its foundation.
  - The original Kilo CLI was built on top of the VS Code extension architecture, which had dependencies that slowed iteration. Terminal-native tools deserve terminal-native foundations, and that's why the foundation turned out to be OpenCode.
  - Instead of creating a thin wrapper around extension capabilities, Kilo CLI is now deeply integrated into the Kilo platform while preserving everything that makes OpenCode great. And the commitment is real - open source works because people give back, so improvements and bug fixes will be contributed upstream.

- what's the difference between this and using opencode directly?
  - Looks like it integrates back with the other kilo apps on your desktop
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## 🧊 james has achieved distributed opencode
- https://x.com/thdxr/status/2036925457417822299
  - agents can run on your laptop, on a remote server, in a cloud sandbox provider
  - shut your laptop and things keep running
  - open it back up and all the data syncs
  - delete the sandbox nothing is lost

- are you making opensandbox or using some existing provider?
  - it's pluggable, we support anything that provides the concept of running an agent - sandbox (e2b, daytona, cloudflare, vercel, etc) - local git worktree - docker - etc

- https://x.com/jlongster/status/2036924361379037224
  - OpenCode is about to get more powerful with remote sandboxes

- we can sync sqlite databases for you, just saying wink wink
  - our needs are extremely simplistic, the big one being that we only need to allow one writer. it's very basic event-sourcing style with a sequence id per session
  - we have users who also desire to control where the data lives, so they could stream these in and persist to something like postgres
  - so this solve the immediate pain point, but it could change in the future if we need more powerful syncing

- the edge case handling is what separates a demo from a real product. been dealing with similar issues — what happens when the sandbox dies mid-task and you have uncommitted state? curious how you're persisting session state across sandbox restarts

- ## 🌰🎯 [Kilo built on OpenCode server : r/RooCode _202603](https://www.reddit.com/r/RooCode/comments/1rsgtes/kilo_built_on_opencode_server/)
  - [We've completely rebuilt the Kilo Code extension for VS Code. Join the beta test. _202603](https://blog.kilo.ai/p/we-completely-rebuilt-the-kilo-vs-code-extension)
  - Last month, we shipped a renewed Kilo CLI built on OpenCode server—a portable, open-source core that isn’t tied to any single editor. The VS Code extension was always going to be next. Today it’s here.
  - Why We Rebuilt
  - originally, under the hood, every surface—CLI, JetBrains, Cloud Agents—was still running VS Code internals, whether it needed them or not. The clearest example was JetBrains, where we were running VS Code internals inside a JetBrains IDE. Developers felt it.
  - When we rebuilt the CLI on OpenCode server, we saw the opportunity to fix this at the root. Instead of patching around VS Code dependencies, we built a portable core that runs natively on every surface. The new VS Code extension shares the same engine as Kilo CLI.
  - Cross-Platform Sessions

- I think RooCode stagnated a bit, it seems logical for them to switch bases. For example there is no parallel subagent capability
  - Totally agree. The lack of parallel subagent capability in RooCode is a major bottleneck. Switching to OpenCode gives us more room to implement these advanced features

- ## once we hit a bit more stability my goal is to have opencode running as a service(i mean running as an OS service on your machine
)
- https://x.com/thdxr/status/2030292138466939214
  - so when you launch tui, web, desktop it's all just connecting to a same process
  - if you can assume there's an agent always running ready for work, a lot of interesting things can be built on top

- doesnt it work like that already with the server?
  - yeah you can set it up that way i just meant having it work like this out of the box (ala docker)
- right now you have to create a different server for every repository
  - you actually don't have to do that - can run one and set `x-opencode-directory` as a header
- oh with the launchd and stuff. that'd be cool

- this will be much better for http://kimaki.xyz openclaw on top of opencode

- Are you thinking there'd be a way for service process to have access to the environment on the client device? I would love it if opencode runs as a service on a server/cloud, but that as needed it could have access to MCPs/tools/files etc on my laptop.
  - opencode 2.0 splits the server into a control plane and workers
  - allows for interesting configurations - can run control plane in server but then add your laptop as a worker
- Do you see this as personal server <> personal workers, or potentially something larger scale in future? Many companies are trying to figure out the right way to scale out remote agents and mostly building their own for internal use. The labs aren’t making self-hostable options
- Vscode does this today with remote workspaces..we need in opencode for sure

- Not a fan of my terminal process and agent process being the same. As agents gain more agency, their ability to work in the background is important, with several terminals concurrently communicating with a single agent process.
  - If you want to check out my harness framework, it has a few proven use-cases for task planning and tool calls. The architecture is based on Anthropic's intializer-updater flow.

- persistent daemon architecture is the key. cold starts kill agent workflows - you lose context every time. with an always-on process you get: filesystem watching, log monitoring, cron triggers, all hitting the same memory. no more spinning up new instances for every task.

- the transition from a "session-based" tool to a persistent daemon architecture is where the real agentic power lives. 
  - if the process is always running, it can handle asynchronous observers—it doesn't wait for your command; it watches the filesystem, monitors the logs, and prepares the fix before you even open the TUI. 
  - by standardizing the communication layer between the service and the various frontends (Web, Desktop, TUI), you’re effectively building a local-first operating system for intent. persistence is the missing link in autonomous workflows.

- the real gain isn't availability — it's continuity of context. an agent 'always ready for work' is only useful if it remembers what work means in this codebase, right now. persistence is harder than uptime.

- ## we are bringing workspaces in as a first-class concept: agents will be able to run anywhere: local directory/container/worktree, remote sandbox, or anything. 
- https://x.com/jlongster/status/2028616190004740366
  - instead of having a single server that only knows about local directories, the server will act as a "control plane" that routes prompts to where they should go
  - it will manage all of the sessions across these environments and provide a unified layer for all clients to interact with them
  - we will be smart about this: it's not *only* about routing. we will sync all data from remote environments into the local control plane server. this means the remote env can be destroyed, and we will be able to later recreate a new env with exactly the same state. it's reproducible
- I thought a lot about syncing when I built @actualbudget and and a whole CRDT system. wasn't expecting to be working in that space again (though very different) and I'm excited to tackle this problem. this time we'll probably do something like event sourcing. It's a lot simpler than distributed syncing; we don't need to support multiple writers

- Workspace abstraction is the right move. Biggest friction with coding agents today is the assumption that "local directory" = "where you work." Once you decouple the workspace from the filesystem, you unlock patterns like branching agent sessions, persistent context across projects, and safe sandboxed execution.

- I've been a bit resistant to remote sandboxes because I have a perfectly good computer sitting right here. but maybe with this I can see the light and be able to offload heavy conversations.
  - honestly me too, but this same architecture could route it into a local sandbox that uses just-bash or containers or  something
  - or if you just use worktrees, that's cool too
  - but it'll all work the same for others who want remote stuff

- I built my own version of this using opencode serve with a custom plugin that sends session logs to a centralized observability plane. Super stoked this is gonna be first class in opencode.

- with event sourcing, when you destroy + recreate a remote env — are you replaying the full event log or snapshotting? curious how that scales for long sessions

- https://x.com/thdxr/status/2028621778218557519
  - could have prompted a git worktree feature into existence a while ago. 
  - but we put in the time to design a system that can also support docker containers, remote sandboxes, etc
  - with sync that can tolerate going offline

- how does this come into play for people using the sdk?
  - it'll all be possible to orchestrate from the sdk. all of our products use the sdk so nothing is ever missing there

- ## in the next release of @opencode there is a new experimental server route "Global Session List"
- https://x.com/ryanvogel/status/2024921007291785629
  - If you run an opencode server from a top-level directory (e.g., ~), custom clients can now list all recent sessions across directories.

- "What did we do last week?" Now can be answered.

- Any parent can access it's child session right?

- ## v1.2.0 of opencode includes our migration to sqlite - if anything goes wrong don't worry, your original data is not yet deleted _202602
- https://x.com/thdxr/status/2022562561732812841
  - you can clear out `opencode.db*` files in %APPDATA% or ~/.local/share/opencode folder and it'll rerun

- Why sqlite if I may ask?
  - opencode produces a lot of data and we need query flexibility beyond what flatfiles in folders gives us

- Given you're using drizzle for this, are you open to other database types in the future. Would love to centrally manage my opencode sessions across sandboxes
  - we're going to solve that problem in a different way
  - we are just going to make distributed opencode a native thing

- https://x.com/LukeParkerDev/status/2023915692404400536
  - anecdotally opencode now sits at max 700mb of memory usage, rather than memory explosion of 14gb of ram, fixed for me as of the 1.2.0+ versions that swapped to `sqlite`.
# discuss-roadmap
- ## 

- ## 

- ## [Is there a way to edit code in OpenCode app? : r/opencodeCLI _202603](https://www.reddit.com/r/opencodeCLI/comments/1rtfybx/is_there_a_way_to_edit_code_in_opencode_app/)
- It’s not an editor. You’re right to be afraid, it’s not easy to make a good editor and there are many great ones already out there

- ## [System environment prompt causes cache invalidation _202512](https://github.com/anomalyco/opencode/issues/5224)
  - I've noticed that the environment() function in system.ts fetches 200 files from the current git working directory. This means that when files are added or removed in the directory, this portion of the system environment prompt is likely to change, resulting in context invalidation and increased API costs.

# discuss-internals
- ## 

- ## 

- ## 

- ## Features in OpenCode itself will be internal plugins and can be activated/deactivated at runtime. Same as external plugins. 
- https://x.com/thdxr/status/2036954434727555095
  - This will allow for reloading plugins at runtime. 
  - Trying to tweak the DX a little more. Almost ready to go.

- I think you guys will have a powerful agent platform not just for coding if you make everything modular with a good plugin SDK. Built in support switching between group of plugins would be nice.

- ## 🔍 we've taken the first steps in eliminating opencode's ripgrep dependency 
- https://x.com/thdxr/status/2021422750385176905
  - https://github.com/dmtrKovalenko/fff.nvim /rust
  - wrapped it up into a nice native dep for us
  - avoids having to install and call into ripgrep as a separate process and is more performant
  - there's a lot of underlying functionality that depends on finding files so the indexing + access tracking system will help in a number of places

- What does native dep mean here? It's still a Rust program in a typescript/zig thingy?
  - direct function calls instead of a subprocess essentially
- instead of spawning a new process they'll be natively calling functions with bun:ffi 

- ripgrep, fast only when burning through all cores, but limping when using 1-2 cores.
  - rg is 4x faster than grep at 8x the resource usage!

- Just want to mention one potential bug: ripgrep by default respect gitignore (which usually includes secrets files like .env and build artifact). Just want to make sure that the native dep can do similar functionality.

- ## [Am I the Only One Using GUI? and is the CLI Better? : r/opencodeCLI](https://www.reddit.com/r/opencodeCLI/comments/1r13qup/am_i_the_only_one_using_gui_and_is_the_cli_better/)
- The CLI and GUI are identical in how they interact with the model. Both are just a way to communicate with the underlying opencode server.

- ## [What's the point of Opencode's built-in clipboard? : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1qquefr/whats_the_point_of_opencodes_builtin_clipboard/)
  - Why does Opencode have a built-in clipboard that overrides your terminal's clipboard, and doesn't let you paste out of it? It's very frustrating.
  - Even for simple things, like copying a block of a conversation for documentation seems impossible with Opencode, outside of a clunky screenshot. So I assume I'm missing something and Opencode's documentation is horrible.

- Have you tried ctrl-shift-c and ctrl-shift-v? There's also ctrl-ins and shift-ins
  - Supposedly you can run 'opencode export' from the command line too for a raw text dump (saw a GitHub issue yesterday, haven't tried it yet).
  - And finally there's tmux's copy mode (albeit opencode's scrolling behaviour limits its usefulness to only what's on the screen, and adds some indentation)

- OpenCode has a text entry box, a sidebar, and a header that you PROBABLY don't want to copy. You may also want to be able to copy more than is visible on the screen, so you need OpenCode to be able to scroll back to let you select more stuff. It feels a little screen or tmux adjacent.

- I have been using Linux for months and copy and paste are completely and utterly broken anyway.

- ## opencode’s client/server architecture is very very clever, they’re planning on sneaking into every app _202512
- https://x.com/threepointone/status/2002506150819119542
- yeah — it's a pretty sick model agnostic agent framework

- I'm betting on distributed winning the long game. A server cannot contain my army (of agents).

- They already got into gitlab

- Not quite as robust as the sdk + runtime approach
  - The SDK + runtime plugin system is the best feature 
# discuss-sandbox
- ## 

- ## 

- ## 

- ## been messing around with @daytonaio sandboxes while running @opencode as a server rather than a headless instance
- https://x.com/ryanvogel/status/2022495102615326850
  - i built a package called that wraps the sandbox provider and manages resumability & instance storage

- have you guys thought about how you would isolate sandboxes to a session while maintaining a static server URL?

- This is the right direction. Long-lived agent server + sandbox resumability is where things stop feeling like demos.
  - Biggest pain I keep hitting is state sync: filesystem + env + “what tools ran” so you can replay safely.
  - How are you persisting instance storage here, snapshotting whole sandboxes or doing diffs/checkpoints?
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## [I have 2, 004 AI skills installed. Here's how I reduced my startup context from ~80K tokens to ~255 tokens (99.7% reduction) : r/opencodeCLI _202602](https://www.reddit.com/r/opencodeCLI/comments/1rfwlzk/i_have_2004_ai_skills_installed_heres_how_i/)
  - The problem: AI agents use a 3-level progressive disclosure system to load skills. Level 1 loads the name + description of every skill into the system prompt at startup. With 2, 004 skills, that's ~80, 000 tokens consumed before I even type a prompt - roughly 40% of a 200K context window.
  - The fix: [SkillPointer](https://github.com/blacksiders/SkillPointer)
  - It's not a plugin or library. It's an organizational pattern that works with native skills:
  - Move all 2, 004 raw skills to a hidden vault directory (outside the agent's scan path)
  - Replace them with 35 lightweight "category pointer" skills
  - Each pointer tells the AI: "use list_dir and view_file to browse the vault and find the exact skill you need"
  - The AI still accesses every skill - it just discovers them on-demand using file tools it already has, instead of loading all descriptions at startup.

- Cloudflare released code mode to target this issue: Code Mode
  - Nice! Code Mode is super interesting, thanks for linking it. It’s tackling the same core problem (too much MCP/API surface in context).

- Okay so I absolutely love this from a technical standpoint, I've seen several mini patterns like this and written a few- but mostly for chaining not condensing context!
  - However, this feels pretty perfectly situated for rag or even just a database lookup right? Then again, I don't think you can actually best text lookup at this scale, if you are willing to be militant on organization and policing descriptions
- > The commenter recognizes the "SkillPointer" method as a clever design pattern. However, they note that they usually see this logic used for chaining (linking multiple AI tasks together in a sequence) rather than condensing context (shrinking the amount of data the AI has to "read" at the start of a session).
  - > RAG (Retrieval-Augmented Generation) is the industry standard for this exact problem. Usually, if you have 2, 000 items, you put them in a database and let the AI search for what it needs. The commenter is essentially asking: "Why build this manual 'pointer' system instead of just using a standard database?"
  - > if a human is "militant" (extremely strict) about how they name and describe their files, a simple text-based file search is often faster and accurate
- 👷 You absolutely nailed the dilemma, but you actually read my mind, I'm not skipping vector search entirely, I’m just layering it.
  - I use FAISS+Langchain and a custom Qdrant MCP at different layers under the hood (since Cursor/VS Code have built-in indexers by default anyway).
  - The problem with pure RAG/Vector DB lookups at the top level is semantic failure. If I ask a pure RAG setup to 'Build a stretchy IK arm', it pulls the IK node and all connected if you know those DBS can have up to 700+ vrctors, but misses the 'Naming Conventions' file because the mathematical overlap just isn't there.
  - So I use SkillPointer as a strict text router to force a custom dependency map first. This mixed, layer-by-layer approach saves massive tokens. Once inside the routed skill, the AI can trigger the Qdrant MCP for semantic search if it actually needs to deep-dive into the docs.
  - By putting SkillPointer's strict text routing in front, I shield the AI from that MCP bloat. The AI only loads the schema for the one tool it actually needs at that exact moment, rather than choking on the entire protocol dictionary.
  - In the end, it's all about ruthlessly optimizing context limits to prevent hallucinations in complex tasks.

- Ever get misroutes where a skill could fit like 2-3 categories? How does the agent decide which pointer to hit?"
  - Right now, the Heuristic Engine just assigns it to the first matching category in my priority dictionary. Code of idea is open and you can see examples and improve them for your specific needs.
  - But the real safeguard is the AI itself. Because the Pointers are incredibly token-cheap (just a few sentences), the agent will naturally trigger multiple pointers simultaneously if a task is ambiguous. But it also can skip most of them, depends on approach and rules llm follows.

- I do something different, and I've seen the Convex skill do the same: I create matter skills which have subskills as references. Also, just install your skills per project.
  - Cool! Matter skills + subskill refs (Convex style, just checked their page) nests nicely. Looks like everyone who see the problem in scale diggin into this issue. I think it will be resolved on higher level soon!

- I think the problem is having four digit number of skills. You just need to delete ones that are not used

- Sorry but skills do not meaningfully change the code quality. It’s all over engineering.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [What would be the best memory-bank in Opencode, coming from Roo Code with MemoryBank injected in the prompts. : r/opencodeCLI _202601](https://www.reddit.com/r/opencodeCLI/comments/1qe28fd/what_would_be_the_best_memorybank_in_opencode/)
- Simple Memory Plugin from @knikolovx. It is a very simple plugin, but also very effective. And it was created with programming in mind. https://github.com/cnicolov/opencode-plugin-simple-memory

- Ive written my own. I've used a meta tool pattern to keep tools down to three and got various connectivity guides/templates but I always encourage people to try and adapt something or build something suited to their workflow. https://github.com/ScottRBK/forgetful
