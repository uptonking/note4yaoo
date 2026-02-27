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

- ## 

- ## 

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

- ## 

- ## [System environment prompt causes cache invalidation _202512](https://github.com/anomalyco/opencode/issues/5224)
  - I've noticed that the environment() function in system.ts fetches 200 files from the current git working directory. This means that when files are added or removed in the directory, this portion of the system environment prompt is likely to change, resulting in context invalidation and increased API costs.

# discuss-internals
- ## 

- ## 

- ## 

- ## 

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
