---
title: lib-editor-app-community-diff-patch
tags: [community, diff, diff-match-patch, editor]
created: 2025-10-08T06:33:26.386Z
modified: 2025-10-08T06:34:09.600Z
---

# lib-editor-app-community-diff-patch

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-ai-editing
- ## 

- ## 

- ## 

- ## 🤔 [Ask HN: Best practices for AI-generated code diff outputs? : r/ChatGPTCoding _202408](https://www.reddit.com/r/ChatGPTCoding/comments/1f4oaj3/ask_hn_best_practices_for_aigenerated_code_diff/)
  - I'm developing a system that uses Claude to automatically generate small patches for C# codebases. I'm looking for state-of-the-art practices to ensure the AI produces correctly structured output for code diffs.
  - What format should the diffs be in? (e.g., unified diff, context diff, git diff)
  - How can I ensure the AI generates syntactically correct diffs?
  - Are there any best practices for prompting the AI to produce high-quality, minimal diffs?
  - What are some potential pitfalls or edge cases I should be aware of?
  - Has anyone implemented something similar? What were your experiences?

- Applying instructions/changes to an existing codebase is by far the hardest part of making something like Cursor. The Cursor guys notoriously trained their own model for this. That's why you can't use your own API keys to have the Apply button work in Cursor.
  - I never really tried using actual diff formats like you suggest - I saw Aider did that and their Apply Changes results weren't great either.
  - My latest version I'm trying to break up code into 'top level scopes' using `Treesitter` AST parser, and match the first line of those top level scopes to lines in files in the existing codebase. Once I have those I make sliding windows to tell the LLM just focus on changing this code in this file in this window keeping everything else in this snippet working but making the appropriate changes. But breaking up changes is rough - there are so many unexpected cases of what the LLM gives you, I've been writing edge cases for months now. It's a rough problem. I don't think anyone is getting great results for complex diffs - even Cursor messes up often and they have a team of MIT grads working full-time on this.

- I've done a bit of work trying to generate diffs. I think you have no other choice than to get hands on and try what works.
  - In my experience, trying to get an output "in 1 shot" that is composed of changes to a piece of code and also have this be in a correctly formatted diff... Failed more often than not.
  - It either ignored part of the instructions that it needed to follow or it generated erroneous diff. 
  - Asking to get the code right, and then, making that code a diff, was better. Trying to use chain of thought to keep it in one prompt didn't make a difference, as it would say it was gonna do x, y, z... But then suck at some of the steps.
  - With Claude, giving info in XML tags worked very well (to classify parts of the prompt as "original code" "instructions" and so). My attempts to use JSON and function calling were less successful, I felt it "dumbed down" the coding part when asking for that. But your mileage(用处, 好处) may vary and I may have been doing something wrong. In another project the JSON/function calling works without issues (but what I ask sonnet 3.5 is simpler, not much "thinking" needed).
# discuss-edit-format/protocol ⚖️
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## JetBrains is adopting ACP.
- https://x.com/zeddotdev/status/1975241285796552816
  - Every @jetbrains IDE will support any ACP-compatible agent. Combined with Zed, Neovim, and Emacs, that's one protocol implementation reaching developers everywhere.
- Please add call hierarchy feature and may be a type hierarchy as well. The first is important for many languages than the second

- https://x.com/jetbrains/status/1975531714060398739
  - Huge move. Vendor agnostic? IDE of my choice? I'm in. 

- ## [ACP Brings JetBrains on Board — Zed's Blog _202510](https://zed.dev/blog/jetbrains-on-acp)
  - [JetBrains × Zed: Open Interoperability for AI Coding Agents in Your IDE | The JetBrains Blog _202510](https://blog.jetbrains.com/ai/2025/10/jetbrains-zed-open-interoperability-for-ai-coding-agents-in-your-ide/)

- JetBrains has announced it will co-develop the Agent Client Protocol with zed. They plan to bring ACP support to their entire IDE lineup – IntelliJ IDEA, PyCharm, WebStorm
- When we launched ACP a few months ago with Google and Gemini CLI, our goal was simple: create an open standard so any agent could work with any editor
  - JetBrains changes the equation. They're going beyond adoption to actively shape the future of ACP with us. 
  - With JetBrains committed, ACP is becoming a real standard for agents to work with UI.
- Implementing ACP is a no-brainer for agents. One protocol implementation gets you in front of Zed, Neovim, Emacs, and millions of JetBrains users. Now is the time to get on board.

- ACP separates agents from editors. Agents implement one protocol and work everywhere. Editors adopt one protocol and support every agent.
  - For agent developers, this means focusing on what matters: your agent's intelligence and capabilities. No custom integrations to maintain for each editor. No one-off deals with every IDE. Implement ACP once and your agent runs wherever developers work
  - For users, it means no vendor lock-in. No compromises. Just your preferred agent(s) in your favorite UI(s).

- We're building ACP to reduce duplicated work, enable smooth interoperability, and give developers real choice in their tools. 

- ## 📝 [Bring Your Own Agent to Zed — Featuring Gemini CLI — Zed's Blog _202508](https://zed.dev/blog/bring-your-own-agent-to-zed)
- You can now interact with third-party agents directly within Zed. 
  - To make this possible, we created the Agent Client Protocol (ACP), and we've partnered with Google to integrate Gemini CLI as the initial reference implementation.
- Because software developers rely on diverse tools in a variety of different tech stacks, we see room for multiple agents competing to solve problems in different domains. 
- Just as the Language Server Protocol unbundled language intelligence from monolithic IDEs, our goal with the Agent Client Protocol is to enable you to switch between multiple agents without switching your editor. 
  - If you're an agent developer, we're also giving you a fast and convenient user interface inside an IDE, so you can focus on building the best possible agent rather than forking VS Code.

- Command-line agents are cool because their simplicity makes them easy to run anywhere—including as a subprocess of another application.
- Zed was already running Gemini CLI inside our embedded terminal emulator, but we needed a more structured way of communicating than ANSI escape codes. 
  - So we defined a minimal set of JSON-RPC endpoints to relay user requests to the agent and render its responses. 
  - The result is the Agent Client Protocol, a lean framework that lets any client talk to any agent

- By running the same Gemini CLI as a subprocess speaking ACP, we surface the same underlying capabilities of the terminal-based experience, but tightly integrated into an environment that's purpose-built for software development. 
- This unlocks features that are difficult to achieve outside of an editor, such as real-time edit visualization, multi-buffer reviews, and fluid navigation between code and agent interactions.

- ACP lets developers choose the tools that work best for their workflow. Any agent that speaks ACP can plug into a powerful UI, where the user can follow the agent around the codebase as it works, control its access to tools and MCP servers, and review all of its changes in a multi-buffer with full syntax highlighting and language server support. 
  - When you interact with third-party agents, nothing touches our servers, and we don't have access to your code. 
  - As with all Zed features and services, we never store or train on your data without your explicit consent.

- ## [Bring Your Own Agent to Zed – Featuring Gemini CLI | Hacker News _202508](https://news.ycombinator.com/item?id=45038710)
- To me this (coupled with their DeltaDB announcement) feels like Zed trying to get out of the business that Cursor is in, and maybe even kicking them on the way out, if the protocol helps bring-your-own-agent take off.

- This in theory means you can use QwenCoder too since it’s a fork of Gemini CLI?

- similar to https://eca.dev/ ?
  - https://github.com/editor-code-assistant/eca /404Star/apache2/202510/clojure
  - https://eca.dev/
  - Editor Code Assistant (ECA) - AI pair programming capabilities agnostic of editor
  - A Free and OpenSource editor-agnostic tool that aims to easily link LLMs <-> Editors
  - Editor-agnostic: protocol for any editor to integrate.
  - Single configuration: Configure eca making it work the same in any editor via global or local configs.
  - Multi models: Login to OpenAI, Anthropic, Copilot, Ollama local models and many more
  - OpenTelemetry: Export metrics of tools, prompts, server usage
  - The server is written in Clojure and heavily inspired by the LSP protocol which is a success case for this kind of integration.
  - How it works: Editors spawn the server via `eca server` and communicate via stdin/stdout, similar to LSPs. Supported editors already download latest server on start and require no extra configuration.

- ## ⚖️🚀 [Agent Client Protocol (ACP) | Hacker News _202508](https://news.ycombinator.com/item?id=45074147)
- IBM announced in March 2025 its Agent Communication Protocol (ACP) but is now abandoning the ACP name and merging ACP efforts with Google’s Agent2Agent (A2A) protocol at the Linux Foundation. The ACP team is winding down as the industry backs A2A for open, community-driven AI agent interoperability under Linux Foundation governance. This move aims to unify protocols and avoid fragmentation in AI agent standards.

- Zed is awesome, but the absence of side-by-side diffs just drives me crazy, so I'm back to Cursor / VSCode. Turns out I can't work without it.

- The big question is why it can't be just a LSP server or extension to the LSP protocol to provide all that might be needed by the LLM.
  - Because there is no ai hype in LSP. AI is literally going through the same phase as early javascript libraries did. An explosion of tools, completely ignoring/bypassing previous accumulated knowledge, solving the wrong problems with the wrong tools.
- The question doesn't even make sense, there is no overlap between LSP and ACP

- In languages with strong compile-time checks (like say rust) the obvious problems can mostly be solved by having the agent try to compile the program as a last step, and most agents now do that on their own. 
  - In cases where that doesn't work (more permissive languages like python, or http APIs) you can have the AI write tests and execute them. 
  - Or ask the AI to prototype and test features separately before adding them to the codebase. Adding MCP servers with documentation also helps a ton.
- The real issues I'm struggling with are more subtle, like unnecessary code duplication, code that seems useful but is never called, doing the right work but in the wrong place, security issues, performance issues, not implementing the prompt correctly when it's not straight forward, implementing the prompt verbatim when a closer inspection of the libraries and technologies used reveals a much better way, etc. Mostly things you will catch in code review if you really pay attention. But whether that's faster than doing the task yourself greatly depends on the task at hand

- The new models are much better at reading the codebase first, and sticking to "use the APIs / libraries already included". Also, for new libraries there's context7 that brings in up-to-date docs. Again, newer models know how to use it (even gpt5-mini works fine with it).

- I love this idea; I hope it gains traction. One thing that is not clear to me is file search vs unsaved files. It's common for agents to use, e.g., ripgrep to search the file system. But if the communication protocol includes read/write access to unsaved files, there is a desync in terms of accuracy.. rg can't search unsaved files.

- Claude, come up with a protocol for communicating between AI agents and IDEs/editors. Create node, python and rust libraries. Create a website with a landing page

- The protocol for interacting with code is files and text. You need to define an interface for Ai to click buttons? Or to create keyboard macros that simulate clicking buttons? We are all doomed!
  - There's a long history of REPL interaction protocols decoupling development environments from tools and making things nicer overall. This thing is an empty in the same tradition. (That said, I'm not convinced its author knew the tradition existed.)
  - It's like the Jupyter protocol, from which people do derive utility.
- I’m afraid you missed a bit the mark :( This is the equivalent of LSP but for coding agents. So any editor does not have to rebuild an interface to support each and every new one.

- I don’t see why we need so many protocols. In such a greenfield tech, many are eager to define rules. There’s already a protocol called AG-UI that does the similar thing, but even its purpose isn’t entirely clear to me.
  - I don't know about other protocols but for this one it's because AI vendors decided to ship their agents in the form of TUIs, which are not programmable. They need to be wrapped into something to be build on top of.
- One great reason is to avoid M*N problem: https://matklad.github.io/2022/04/25/why-lsp.html

- I would love it, but please don't add JSON-RPC to the world... It's too heavy for editor.
  - To write that JSON-RPC is "too heavy for editor", you have to not only misunderstand the cost of JSON encoding (trivial) but also the frequency of editor-tool interaction (seldom) and volume of data transferred (negligible). In addition, you have to look at LSP, MCP, and other JSON-y protocols and say "yep. There's where the UI latency is. Got it.". (Nope)
# discuss
- ## 

- ## 

- ## 

- ## better diff views for AI agents _202506
- https://x.com/geoffreylitt/status/1938239983464140920
  - To work well with AI agents, we need better diff views! your ability to check the agent's work is the bottleneck.
- here are some ideas for how to do that, based on our research at @inkandswitch 
- Zoomed out diffs: show the forest, not just the trees. Is it one big change? 100 tiny changes? Where did they happen?
  - this requires a stable "map" of the entire project, with familiar landmarks. My biggest frustration with many code diff views is that it's hard to get a feeling for where changes live in a project, and what order to review them in.
  - As an example of providing landmarks, we prototyped this view of diffs on an essay -- using section headings to anchor where change is happening.
- Diffs in the editor, not somewhere else:  it's quite disorienting to see diffs in a totally separate place from where you're used to working. when diffs display in an existing editor instead, you can lean on familiar ways of seeing and locating information.
  - One example of this is in coding IDEs—I prefer to see diff views in a powerful text editor with syntax highlighting, a folder tree, LSP integration, etc. Hard for any terminal or web diff UI to compete with the level of polish that has gone into that experience.
  - Similarly, something we've been working on is diffs for game dev. Too often, people have to leave their game engine and look at a bunch of cryptic text diffs in GitHub to know what's going on. We're prototyping built-in diffing for the Godot engine
- Edit rationale: individual edits should have explanations attached. (This is reminiscent(引起联想的) of comments on Google Docs suggestions, for example). You should also be able to group related edits together into little mini-groups -- if you do a find-replace in a doc, that should be one bundle of change, not 100 isolated ones.
  - Notably, this is too much work to ask of humans—they don't have time to laboriously explain each part of the change, group together related changes, etc. But AIs can totally spare the time! Tokens spent on explaining the edits and easing review are well worth it for saving time on human review. When an AI agent suggests some work, we should demand highly polished walkthroughs of what changed and why.
- Branching/speculation: To allow agents to try out possibilities, you need the ability to fork your data into parallel isolated copies, let the agent go wild, and then review / merge back together.

- Diffs as platform infra: Unfortunately is a ton of work for app devs to implement in order to support AI agents well -- diff views, branching, comments... 

- 
- 
- 
- 
- 
- 
- 
- 
