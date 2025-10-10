---
title: lib-editor-app-community-diff-patch
tags: [community, diff, diff-match-patch, editor]
created: 2025-10-08T06:33:26.386Z
modified: 2025-10-08T06:34:09.600Z
---

# lib-editor-app-community-diff-patch

# guide

- tips
  - 可直接参考已有编辑器的方案，如codemirror

- 考虑编辑的场景
  - shorter/longer/improve/check/translate 都可实现为 一次性替换

- [Edit formats | aider](https://aider.chat/docs/more/edit-formats.html)
  - Aider uses various “edit formats” to let LLMs edit source files. 
    - Different models work better or worse with different edit formats. 
    - Aider is configured to use the optimal format for most popular, common models
  - 🧩 The “whole” edit format is the simplest possible editing format. 
    - The LLM is instructed to return a full, updated copy of each source file that needs changes. 
    - While simple, it can be slow and costly because the LLM has to return the entire file even if just a few lines are edited.
  - 🧩 The “diff” edit format asks the LLM to specify file edits as a series of search/replace blocks. 
    - This is an efficient format, because the model only needs to return parts of the file which have changes.
    - Edits are formatted using a syntax similar to the git merge conflict resolution markings, with the file path right before a fenced block
  - The “diff-fenced” edit format is based on the diff format, but the file path is placed inside the fence. 
    - It is primarily used with the Gemini family of models, which often fail to conform to the fencing approach specified in the diff format.
  - 🧩 The “udiff” edit format is based on the widely used unified diff format, but modified and simplified. 
    - This is an efficient format, because the model only needs to return parts of the file which have changes.
    - It was mainly used to the GPT-4 Turbo family of models, because it reduced their “lazy coding” tendencies. 
  - editor-diff and editor-whole
    - These are streamlined versions of the diff and whole formats, intended to be used with --editor-edit-format when using architect mode. 
    - The actual edit format is the same, but aider uses a simpler prompt that is more narrowly focused on just editing the file as opposed to solving the coding task.
# examples-ai-editing
- https://github.com/paradite/ai-file-edit /14Star/MIT/202506/ts
  - A library for editing files using AI models such as GPT, Claude, and Gemini.
  - Edit files using natural language
  - Overwrite existing files
  - Support for multiple file edits in a single operation
  - The tool generates both forward and reverse diffs for all file changes. 
    - The forward diff shows what was changed, while the reverse diff can be used to revert the changes.
  - Limitations
    - Cannot delete files
    - Cannot edit too many files at once (> 3 files)
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 🌵🆚 better diff views for AI agents _202506
- https://x.com/geoffreylitt/status/1938239983464140920
  - To work well with AI agents, we need better diff views! your ability to check the agent's work is the bottleneck.
- here are some ideas for how to do that, based on our research at @inkandswitch 
- ✨ Zoomed out diffs: show the forest, not just the trees. Is it one big change? 100 tiny changes? Where did they happen?
  - this requires a stable "map" of the entire project, with familiar landmarks. My biggest frustration with many code diff views is that it's hard to get a feeling for where changes live in a project, and what order to review them in.
  - As an example of providing landmarks, we prototyped this view of diffs on an essay -- using section headings to anchor where change is happening. It's fairly similar to the within-scrollbar diff view in some IDEs. 
- ✨ Diffs in the editor, not somewhere else: it's quite disorienting(迷惑人的，令人思路混乱的) to see diffs in a totally separate place from where you're used to working. 
  - when diffs display in an existing editor instead, you can lean on familiar ways of seeing and locating information.
  - One example of this is in coding IDEs—I prefer to see diff views in a powerful text editor with syntax highlighting, a folder tree, LSP integration, etc. Hard for any terminal or web diff UI to compete with the level of polish that has gone into that experience.
  - Similarly, something we've been working on is diffs for game dev. Too often, people have to leave their game engine and look at a bunch of cryptic text diffs in GitHub to know what's going on. We're prototyping built-in diffing for the Godot engine
- ✨ Edit rationale/suggest: individual edits should have explanations attached. (This is reminiscent(引起联想的) of comments on Google Docs suggestions, for example). 
  - You should also be able to group related edits together into little mini-groups -- if you do a find-replace in a doc, that should be one bundle of change, not 100 isolated ones.
  - Notably, this is too much work to ask of humans—they don't have time to laboriously explain each part of the change, group together related changes, etc. But AIs can totally spare the time! Tokens spent on explaining the edits and easing review are well worth it for saving time on human review. When an AI agent suggests some work, we should demand highly polished walkthroughs of what changed and why.
- ✨ Branching/speculation: To allow agents to try out possibilities, you need the ability to fork your data into parallel isolated copies, let the agent go wild, and then review / merge back together.
  - In code, git branches do a decent job at this, although the interplay with versioning AI agent work -- especially in parallel agents -- can get pretty awkward.
  - most software doesn't even have git branches! TBH I don't see a viable path to using an AI agent with most software until speculation / diffs / merging are well supported in that piece of software.
  - In our work we've prototyped a "simple branching" model which gives a really lightweight way to fork/merge branches on any kind of document in a web-based collaboration environment - like branches on this essay

- ✨ Diffs as platform infra: Unfortunately is a ton of work for app devs to implement in order to support AI agents well -- diff views, branching, comments...
  - As a concrete demo of this: in our `Patchwork` environment, you can view diffs on any kind of data using the same generic tooling. The UI dev has to define just a few domain-specific things like how to render diffs in their editor. And then the surrounding environment does the rest: supporting parallel branches, computing diffs, etc.
  - The key to this magic is building on `Automerge`, a data sync / collaboration library developed in our lab which optimizes for version control use cases by efficiently storeing the entire granular history of every document, and handling merging of concurrent branches with CRDT algorithms.

- I like to say "collaboration with AI is a version control problem". 
  - An increasing part of everyone's job is going to be reviewing work from untrustworthy robots.
  - The way to solve that is with tools in the domain of "version control" - things like branching, diffing, history, and commenting tools that make it easier to collaborate on shared work.
  - Historically most creative professionals haven't had very good version control tools -- but now with AI in the mix, the motivation to build them has dramatically increased.
  - A side effect I'm optimistic for is that this will also yield better tools for collaborating among humans.

- this needs 3D to visualize so much data and relationship   in ways you can drill down or pull up between scales and sources

- Beyond version control, Diff is also important when AI agents are capable of providing multiple suggestions. A clear Diff view can let users easily compare the alternatives.

- While Diff views have been well explored for code & writing, visual mediums like video are a new ground. We recently prototyped a visual diff that lines up AI-suggested edits for videos
  - [[2502.10190] VideoDiff: Human-AI Video Co-Creation with Alternatives](https://arxiv.org/abs/2502.10190)

- can these tools work with difficult data formats like word or PowerPoint?
# discuss-ai-editing
- ## 

- ## 

- ## 

- ## 🌰 [Improving Diff Edits by 10% - Cline Blog _202506](https://cline.bot/blog/improving-diff-edits-by-10)
  - https://github.com/cline/cline/tree/main/evals/diff-edits

- When it comes to modifying code, Cline has two primary methods in its toolkit: 
  - 1. write_to_file for creating or overwriting entire files, and 
  - 2. replace_in_file for making surgical, targeted changes (diff edits).
- We call these targeted changes "diff edits, " and their reliability is fundamental to the agent's performance.

- We recently released a new diff-apply algorithm and model-specific prompt changes that have improved the diffEditSuccess rate by over 10% on average across all models.
- To achieve this, we built an open-source evaluation system to rigorously test every component of the diff-editing pipeline. 
  - This system allows us to systematically alter each component – including the system prompt, parsing logic, and the diff-apply algorithm itself – and test them against a suite of real-world user scenarios we've collected internally.

- Our evaluation framework quickly uncovered a common and frustrating failure case: many LLMs, despite being explicitly prompted to produce diffs in the correct order, would often return them out of sequence. This is a fundamental problem of improper instruction-following.

- Our solution was two-fold. 
- First, we developed a new, "order-invariant multi-diff apply" algorithm. 
  - In simple terms, it can correctly apply the series of search-and-replace blocks even when the model provides them in the wrong order. 
- Second, we added support for multiple diff formats to account for model-specific quirks.
  - For example, Anthropic's models are optimized for `---/+++` markers, while Gemini and xAI models perform better with `>>>/<<<` blocks.
  - Our system now handles both, ensuring higher reliability regardless of the user's chosen model. These changes together have had a significant impact on reliability.

- By building tools to evaluate our own systems, we can move beyond anecdotal evidence and make data-driven decisions that result in a more capable and reliable agent for everyone.

- ## 📌✏️ [Code Surgery: How AI Assistants Make Precise Edits to Your Files - Fabian Hertwig’s Blog _202504](https://fabianhertwig.com/blog/coding-assistants-file-edits/)
- Applying code changes generated by AI assistants directly to files is a core capability, yet it often proves surprisingly difficult. 
- Users of tools like GitHub Copilot, Aider, or RooCode may have observed these struggles: edits failing to locate the correct insertion point, incorrect indentation, or the tool ultimately requesting manual application.

- This post examines the file editing mechanisms of several coding assistant systems: Codex, Aider, OpenHands, RooCode, and Cursor. 
  - For the open-source systems (Codex, Aider, OpenHands, RooCode), the insights presented here are derived from analyzing their respective codebases. 
  - For Cursor, which is closed-source, the insights come from public discussions and interviews with their team. 
  - We will explore their approaches, presented roughly in order of increasing complexity, while noting that their development involved parallel evolution and mutual influence.
- For each system, we will analyze:
  - How it receives edit instructions from the AI.
  - How it interprets and processes these instructions.
  - How it applies the changes to files.
  - How it handles errors and edge cases.
  - How it provides feedback on the outcome.

### The File Editing Workflow & Challenges

- Most AI code editing systems follow a general workflow:
  - LLM (generates change description) → Tool (interprets & applies) → File System (state change) → Feedback (Tool reports outcome) → LLM (processes feedback)

- The fundamental challenge lies in the indirect nature of the operation: Large Language Models (LLMs) lack direct file system access. 
  - They must describe intended changes via specialized tools or APIs, which then interpret these instructions and attempt execution. 
  - This handoff between the LLM’s representation and the file system state is a frequent source of complications.

- several challenges arise in practice:
  - Challenge 1: Locating the Edit Target
  - Challenge 2: Handling Multi-File Changes
  - Challenge 3: Maintaining Code Style
  - Challenge 4: Managing Failures

- AI systems use various formats to communicate intended changes:
  - Patches: Detailed add/delete instructions, often based on standard patch formats.
  - Diffs: Showing differences between original and desired states.
  - Search/Replace Blocks: Explicitly defining find/replace operations.
  - Line Operations: Specifying edits by line number (less common due to fragility).
  - AI-Assisted Application: Employing a secondary AI model specifically for applying complex changes.

### Codex: A Straightforward Patch-Based System

- OpenAI’s Codex CLI utilizes a relatively simple, structured patch format. Its effectiveness stems partly from OpenAI’s ability to train its models specifically to generate this format reliably.
- The Codex Patch Format
  - With the release of GPT-4.1 (April 2025), OpenAI published a “prompt cookbook” detailing this recommended patch format and a reference implementation (`apply_patch.py`). 
  - They indicated significant training effort for GPT-4.1 on this format, contributing to its effective use within the Codex CLI ecosystem.
- OpenAI’s commentary highlighted that successful formats often avoid line numbers and clearly provide both the code to be replaced and its replacement, using distinct delimiters. 
  - This suggests core principles for reliable AI-driven editing. OpenAI’s ability to co-develop the LLM and the editing tool allows for tight integration and optimization.

### Aider: A Multi-Format Editing System

- Aider employs a more flexible approach, supporting multiple edit formats.
  - It can select the format best suited to the task or the specific LLM being used.
- Aider uses a system of “coder” classes, each responsible for handling a specific edit format
  - This modular design allows for easy extension and selection of different editing strategies.

- Aider supports several formats, choosing based on the model or user configuration (--edit-format):
- EditBlock Format (Search/Replace): Intuitive format clearly showing search/replace blocks.
  - When applying Search/Replace blocks, Aider attempts multiple matching strategies sequentially
  - This layered approach increases the likelihood of successfully applying edits even with minor imperfections in the SEARCH block.
- Unified Diff Format (udiff): Standard diff format (diff -U0 style), suitable for complex changes.
- OpenAI Patch Format: Aider implemented OpenAI’s reference format, leveraging GPT-4.1’s training on this syntax.

### OpenHands: Blending Traditional and AI-Assisted Editing

- OpenHands primarily relies on traditional edit application methods while also incorporating an optional LLM-based editing capability.
- OpenHands primarily uses traditional editing approaches. 
  - It has built-in support for detecting different patch formats – including unified diffs, git diffs, context diffs, ed scripts, and RCS ed scripts – using regular expression patterns. 
  - Based on the detected format, it applies the appropriate parsing and application logic. 
- The system supports several traditional editing methods
  - String replacement.
  - Line-based operations (by number).
  - Standard patch application utilities.

- Optional LLM-Based Editing FeaturePermalink
  - OpenHands allows configuring a separate “draft editor” LLM for a distinct editing workflow
  - Target Identification: The primary LLM specifies the target line range for the edit.
  - Content Extraction: The tool extracts this specific code section.
  - LLM Rewrite: The extracted section and a description of the desired change are sent to the specialized “draft editor” LLM. 
  - File Reconstruction: The tool receives the modified section from the editor LLM and integrates it back into the file, replacing the original lines.

### RooCode: Advanced Search and Format Preservation

- RooCode utilizes the search/replace block format. 
  - Its strengths lie in its advanced search algorithm for locating the target block and its meticulous handling of code formatting during replacement.
- Advanced Search Strategy: Middle-Out Fuzzy Matching
- This strategy is effective for large files or when line numbers are slightly inaccurate, providing robustness against minor context shifts.
- Incorrect indentation is a common frustration with automated edits. RooCode implements a sophisticated system to preserve formatting

### Cursor: Specialized AI for Change Application

- While other systems refine edit formats or matching algorithms, Cursor introduces a dedicated AI model specifically for the application step of the edit process.
- Cursor’s approach involves a two-step AI process:
  - Sketching: A primary, powerful LLM generates the intended change, focusing on the core logic rather than perfect diff syntax. This might be a code block or a rough description.
  - Applying: A separate, custom-trained “Apply” model receives this sketch. This specialized model is trained to intelligently integrate the sketch into the existing codebase, handling nuances of context, structure, and potential imperfections in the input sketch. It performs more than simple text matching; it aims for intelligent code integration.

### Evolution and Convergence of Edit Formats 

- Examining these systems reveals interesting patterns in format development:
  - Search/Replace Lineage: Aider’s EditBlock format (`<<<<<<</>>>>>>>`) established an intuitive approach later adopted by Cline, which RooCode then built upon.
  - OpenAI’s Patch Influence: The specific patch format released with GPT-4.1 gained traction due to focused model training. Used natively by Codex, it was also adopted as an option by Aider.
  - Underlying Principles: Despite different origins, successful formats converge on key ideas noted by OpenAI: avoiding line numbers and clearly delimiting the original and replacement code. These features appear fundamental for reliable AI-driven editing.

- Format Matters: Formats avoiding line numbers and clearly separating before/after code (like OpenAI’s patch or search/replace blocks) are prevalent and effective, especially when models are trained on them.
- Robust Matching is Essential: Successful systems employ layered matching strategies (exact, then increasingly fuzzy) to balance precision with the ability to handle minor discrepancies.
- Indentation Integrity is Crucial: Careful preservation of whitespace and indentation (as emphasized by RooCode) is vital for code correctness and developer acceptance.
- Informative Feedback Enables Correction: Detailed error messages (like Aider’s) are critical for enabling the AI (or user) to diagnose and fix failed edits effectively.
- Specialization Shows Promise: Using dedicated AI models for specific sub-tasks like change application (Cursor) represents an advanced approach to improving reliability.

- Developing robust AI editing tools involves several considerations:
  - Implement Layered Matching: Start with strict matching and add fallback fuzzy strategies.
  - Prioritize Indentation Preservation: Invest effort in accurately maintaining formatting.
  - Design Actionable Error Feedback: Provide specific, informative error messages.
  - Leverage Existing Formats and Implementations: Consider established formats and study open-source systems (Aider, OpenHands, RooCode/Cline).

- ## [What we learned copying all the best code assistants | Hacker News _202501](https://news.ycombinator.com/item?id=42586042)
- I'm interested in what stopped you from finishing diffs and diff based editing. I built an AI software engineering assistant at my last company and we got decent results with Aider's method (and prompts, and hidden conversation starter etc). I did have to have a fallback to raw output, and a way to ask it to try again. But for the most part it worked well and unlocked editing large files (and quickly).
  - We just didn't have the resources at the time on our small team to invest in getting it to be good enough to be default on. We had to move on to other more core platform features.
  - Though I'm really eager to get back to it. When using Windsurf last week, I was impressed by their diffs on Sonnet. Seems like they work well. I would love to view their system prompt!
  - I hope that when we have time to resume work on this (maybe in Feb) that we'll be able to get it done. But then again, maybe just patience (and more fast-following) is the right strategy, given how fast things are moving...

- An interesting alternative to diffs appears to be straightforward find and replace.
  - Claude Artifacts uses that: they have a tool where the LLM can say "replace this exact text with this" to update an Artifat without having to output the whole thing again.
  - ChatGPT's new Canvas feature apparently does a more sophisticated version of that using regular expressions as opposed to simple text matching: https://twitter.com/sh_reya/status/1875227816993943823
- How about looking at an ast-based method for making changes across code base? https://www.reddit.com/r/Python/comments/17tvm06/astgrep_and...
  - I think this is going to be the answer eventually.
  - Once one of the AI companies figures out a decent (probably treesitter-based) language to express code selections and code changes in, and then trains a good model on it, they're going to blow everyone else out of the water.
  - This would help with "context management" tremendously, as it would let the LLM ask for things like "all functions that are callers of this function", without having to load in entire files. Some simpler refactorings could also be performed by just writing smart queries.

- Oh that is super interesting! I wonder if they track how often it succeeds in matching and replacing, I'd love to see those numbers in aggregate.
  - I worked on this for a bit for a research-level-code code editor (system paper to come soon, fingers crossed!) and found that basic find-and-replace was pretty brittle. I also had to be confident the source appears only once (not always the case for my use case), and there was a tradeoff of fuzziness of match / likelihood of perfectly correct source.
  - But yeah, diffs are super hard because the format requires far context and accurate mathematical computation.

- adding line numbers on each line is one of the ideas we've been considering trying

- Aider actually prompts the LLM to use search/replace blocks rather than actual diffs. And then has a bunch of regex, fuzzy search, indent fixing etc code to handle inconsistent respnses.
  - Aider's author has a bunch of benchmarks and found this to work best with modern models.
- What we found was that error handling on the client side was also very important. There's a bunch of that in Aider too for inspiration. Fuzzy search, indent fixing, that kind of stuff.
  - And also just to clarify, aider landed on search/replace blocks for gpt-4o and claude rather than actual diffs. We followed suit. And then we showed those in a diff UI client side

- ## [Windsurf Cascade Leaked System prompt!! : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1h7sjyt/windsurf_cascade_leaked_system_prompt/)
- this system prompt is obscenely long and would just confuse the fuck out of the model, but I am a huge fan of windsurf so they must be doing something right.
  - that's like 5000 tokens

- `"NEVER lie or make things up."` - I'm curious how they came up with this piece.
  - Open AI has been telling its enterprise customers that placing this prompt at the start does work 
- Personally I prefer to use "if you don't know something, admit it". Worked well with many models.

- This is actually very similar to Cline - which is Open Source. I've been exploring Cline's source code and using Gemini Flash to answer questions about it. I find it also works incredibly well, and it too has a long system prompt (less though).

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

- ## 

- ## [Diff Models – A New Way to Edit Code | Hacker News _202301](https://news.ycombinator.com/item?id=34556688)
- From the safety perspective (may get important soon), it is perhaps a very bad idea to allow easy execution/injection of arbitrary code into random places with little review.
  - When designing such systems, please do keep that in mind. Make sure code changes are properly signed and the originating models are traceable.
  - Same applies to datasets generated by models.

- My understanding is you have in training dataset the original code, diff + commit message. So you train the LM to: Input: code+commit output: diff
