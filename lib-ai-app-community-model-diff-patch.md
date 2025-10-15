---
title: lib-ai-app-community-model-diff-patch
tags: [community, diff, diff-match-patch, editor, large-language-model]
created: 2025-10-08T06:33:26.386Z
modified: 2025-10-10T02:45:45.941Z
---

# lib-ai-app-community-model-diff-patch

# guide

- tips
  - 可直接参考已有编辑器的方案，如codemirror

- 考虑编辑的场景
  - shorter/longer/improve/check/translate 都可实现为对明确输入范围内容的 一次性替换

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
- https://github.com/theluk/llm-patcher /apache2/2022406/ts/inactive
  - https://llm-patcher.vercel.app/
  - An open-source AI find-and-replace workflow template built with Next.js, the Vercel AI SDK and OpenAI.
  - Whenever we provide a text to an LLM and ask it to do some changes, it will always stream the full text back to us. This is not ideal for large texts, as it can be slow and expensive. 
  - This project aims to solve this problem by providing a way to stream only the changes made by the LLM back to the user.
  - How does it work?
    - The user provides a text and a find-and-replace query.
    - The text is split into lines and sentences.
    - Each line and sentence is then prefixed with a identifier that looks like `<l1s1>` for line 1, sentence 1.
    - The LLM is then asked to find-and-replace the query in each line and sentence.
    - The changes are then streamed back to the user in the form of a diff. The diff looks like `<r:l1s1>` string to find || string to replace.
  - [How to use LLM for efficient text outputs longer than 4k tokens? - DEV Community _202406](https://dev.to/theluk/how-to-use-llm-for-efficient-text-outputs-longer-than-4k-tokens-1glc)

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

- https://github.com/jlevy/chopdiff /MIT/202508/python 
  - chopdiff is a small library of tools I've developed to make it easier to do fairly complex transformations of text documents, especially for LLM applications
  - it lets you parse, diff, and transform text at the level of words, sentences, paragraphs, and "chunks" (paragraphs grouped in an HTML tag like a `<div>`). It aims to have minimal dependencies.
  - All this is done very simply in memory, and with only regex or basic Markdown parsing to keep things simple and with few dependencies.
  - Filter diffs: Diff two documents and only accept changes that fit a specific filter. For example, you can ask an LLM to edit a transcript, only inserting paragraph breaks but enforcing that the LLM can't do anything except insert whitespace. Or let it only edit punctuation, whitespace, and lemma variants of words. Or only change one word at a time (e.g. for spell checking).
  - Backfill information: Match edited text against a previous version of a document (using a word-level LCS diff), then pull information from one doc to another. For example, say you have a timestamped transcript and an edited summary. You can then backfill timestamps of each paragraph into the edited text.
  - Windowed transforms: Walk through a large document N paragraphs, N sentences, or N tokens at a time, processing the results with an LLM call, then "stitching together" the results, even if the chunks overlap.
  - 🤔 There are full-blown Markdown and HTML parsing libs (such as Marko and BeautifulSoup) but these tend to focus specifically on fully parsing documents as parse trees. On the other end of the spectrum, there are NLP libraries (like spaCy) that do more expensive, full language parsing and sentence segmentation.
    - This is a lightweight alternative to those approaches when you are just focusing on processing text, don't want a big dependency (like a full XML parser or NLP toolkit) 

- https://github.com/kordless/gnosis-evolve/blob/main/contrib_tools/core/file_diff_editor.py
  - Gnosis Evolve turns Claude Desktop from a passive assistant into an active developer
  - Extend Claude's capabilities via natural language
  - The File Diff Editor can be run separately from Gnosis Evolve! This powerful tool provides sophisticated file editing capabilities with regex support, fuzzy matching, and versioning. Perfect for precise code modifications and bulk operations.
  - [File Diff Editor - Advanced Pattern-Based File Editing Tool](https://github.com/kordless/gnosis-evolve/blob/main/FILE_DIFF_EDITOR_HOWTO.md)
    - The File Diff Editor v2.1.1 is a revolutionary MCP (Model Context Protocol) tool that provides advanced file editing capabilities with powerful regex support, fuzzy matching, and enterprise-grade versioning

- https://github.com/jianghoucheng/AnyEdit /MIT/202510/python
  - AnyEdit: Edit Any Knowledge Encoded in Language Models, ICML 2025
  - [AnyEdit: Edit Any Knowledge Encoded in Language Models | USTC Lab for Data Science _202505](https://data-science.ustc.edu.cn/_upload/tpl/15/04/5380/template5380/publication/icml25-jhc.html)
    - Current model editing methods, however, struggle with long-form knowledge in diverse formats, such as poetry, code snippets, and mathematical derivations. These limitations arise from their reliance on editing a single token’s hidden state, a limitation we term efficacy barrier. 
    - To solve this, we propose AnyEdit, a new autoregressive editing paradigm. It decomposes long-form knowledge into sequential chunks and iteratively edits the key token in each chunk, ensuring consistent and accurate outputs. 
    - AnyEdit serves as a plug-and-play framework, enabling current editing methods to update knowledge with arbitrary length and format, significantly advancing the scope and practicality of LLM knowledge editing.

- https://github.com/Banner-Z/G-SPEED /apache2/202310/python/inactive
  - The official repository of paper G-SPEED: General SParse Efficient Editing MoDel (Findings of EMNLP-2023).
  - [[2310.10480] G-SPEED: General SParse Efficient Editing MoDel](https://arxiv.org/abs/2310.10480)

## diff-toolchain

- https://github.com/afnanenayet/diffsitter /MIT/202510/rust
  - A tree-sitter based AST difftool to get meaningful semantic diffs
# discuss-stars
- ## 

- ## 

- ## 

- ## 🧩 [What is `git diff --patience` for? - Stack Overflow](https://stackoverflow.com/questions/4045017/what-is-git-diff-patience-for)
- The patience diff algorithm is a slower diff algorithm that shows better results in some cases.
  - Patience Diff, instead, focuses its energy on the low-frequency high-content lines which serve as markers or signatures of important content in the text. It is still an LCS-based diff at its core, but with an important difference, as it only considers the longest common subsequence of the signature lines

- You can also use it for merges (worked really well here for some XML conflicts)

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

- ## 

- ## [The Edit Trick: Efficient LLM Annotation of Documents _202504](https://waleedk.medium.com/the-edit-trick-efficient-llm-annotation-of-documents-d078429faf37)
- 
- 
- 
- 
- 
- 
- 

- ## 🌰 [When LLMs give *almost* correct code, fix it with targeted line edits instead of a full rewrite  _202505](https://medium.com/@pYdeas/when-llms-give-almost-correct-code-fix-it-with-targeted-line-edits-instead-of-a-full-rewrite-af3329e42010)
- This idea came from [Introducing FixIt: an unreasonably effective AI error fixer for SQL - MotherDuck Blog _202401](https://motherduck.com/blog/introducing-fixit-ai-sql-error-fixer/) and adapted with Python to work with not just SQL, but text in general

- 
- 
- 
- 

- ## [How to generate automatically applicable file diffs with ChatGPT? - Prompting - OpenAI Developer Community _202305](https://community.openai.com/t/how-to-generate-automatically-applicable-file-diffs-with-chatgpt/227822)
  - Have any of you succeeded to have ChatGPT output suggested changes to a file in a way that can be automatically applied to the file?

- 
- 
- 
- 
- 
- 
- 
- 
- 

- ## 🚀 [Launch HN: Morph (YC S23) – Apply AI code edits at 4, 500 tokens/sec | Hacker News _202507](https://news.ycombinator.com/item?id=44490863)
  - We’ve built a blazing-fast model for applying AI-generated code edits directly into your files at 4, 500+ tokens/sec. No more slow full-file rewrites or brittle search-and-replace hacks.
- Morph's approach:
  - Your agent outputs edits “lazily”, referencing unmodified lines in the existing file (ex: // ...existing code...)
  - Morph instantly applies these edits to a file using our Fast Apply model + speculative decoding against the original file, making AI patches fast, reliable, and production-ready.
  - This approach was pioneered by Cursor last year, but their models aren’t available as APIs—so we built Morph for developers everywhere (with a large free tier!)
  - We have 2 Fast Apply models: morph-v3-fast - 4500+ tok/sec, and morph-v3-large - 2500+ tok/sec. These models power Fast Apply at create.xyz, databutton, continue.dev, and more!

- Morph is a tool for integrating the output of other LLMs and not an LLM itself? It doesn't generate 4500 tok/sec, it can edit 4500 tok/sec?
  - Correct, but morph is a LLM as well. In practice its basically Big LLM using small LLM as a tool call
- It's more expensive than Gemini flash which can actually write pretty decent code (not just apply a diff). Fast AI edit application is definitely great but that's pretty expensive
  - Morph v3 fast: Input: $1.20 / M tokens, Output $2.70 / M tokens
  - Gemini 2.5 Flash: $0.30 / M tokens, Output $2.50 / M tokens
  - (Source: OpenRouter)
- Thats for 0 data retention - on the Morph website its: 0.80 /1M token input, $1.20 /1M token output. We have discounts for large volumes/reserved instances as well

- Edit speed is definitely not a bottleneck for dev UX, quality is.
- I would happily take 10 tok/sec of a correct answer instead of wasting an hour curating 4500 tok/sec throwaway answers. Benchmark performance matters 100x more than your latency.

- Really impressive. I'm in the market for such a solution for our internal AI coding systems - how do you compare to the opensource https://huggingface.co/osmosis-ai/Osmosis-Apply-1.7B?
  - You should give both a try! key difference is our models are faster and more accurate by a large margin

- I’d just like to put a pitch in here for someone to do “smart rebase+merge” with AI. Now THAT would really speed up development
  - You can do that with Claude Code. Just tell it to merge in another branch and fix the merge conflicts.

- For anyone more curious about how this works, Fireworks wrote a blog post about it last year (I think): https://fireworks.ai/blog/cursor

- I'm also really curious about the XML tool calls in the documentation. I have not heard of this being the norm for tools like Cursor. Is that still the case? 
  - Its true - Cursor, Cline, and many others still use xml for tool calls. In JSON, the model needs to "focus" on escaping characters correctly while also sampling from a reduced token distribution.
  - https://aider.chat/2024/08/14/code-in-json.html

- This is what I use and it's free for anyone to use individually: https://github.com/kordless/gnosis-evolve/blob/main/contrib_tools/core/file_diff_editor.py

- Is there anyway to bring this into Claude Code?
  - Make an MCP server, and turn off the Write|Edit|MultiEdit tools?
  - Actually - that's what this company should do. It should be an MCP server so anyone could plug it into any agent with a url and an API key.

- Can't you ask these LLMs to simply output a patch file? https://man7.org/linux/man-pages/man1/patch.1.html
  - you can - but they dont work reliably in practice. Common issues include search match fails, missing commas in replaced items (model doesnt have surround context while replacing), and a few other error cases. This issues are much worse for scattered edits across a file from real world queries (ex: make this page look nicer). Patches tend to work fine for single line or extremely focused edits though - Cursor uses s&r/patches for single line edits
  - https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/main/Cursor%20Prompts/Agent%20Prompt%20v1.2.txt

- How does this compare to Google Diffusion? Diffusion writes out at seemingly the speed of thought.
  - we're quite a bit faster and specifically training for merging code edits.
  - Google diffusion is a swing at a generalist model. Super cool work nonetheless

- Is this similar to Gemini Diffusion? Thanks
  - No, we use autoregressive llms. Diffusion models would be super interesting here. Mercury is doing some interesting work with diffusion in code gen but still too early to tell if it'll get good enough for production usage

- ## [Does Claude Code use diff-based editing like Cline, or does it have a specialized model like Cursor? : r/ClaudeAI _202506](https://www.reddit.com/r/ClaudeAI/comments/1lhouua/does_claude_code_use_diffbased_editing_like_cline/)
- The built in tool uses the line number then a search replace based on exact match. Plenty of MCP options if you want diffs.
  - Install `rg (ripgrep)` and tell it to use that, it's much faster than grep and it uses it often.
  - I also have `ast-grep` which is much more powerful than rg and it also knows how to use it, but it requires a more complex setup and instructions... but can be worth it on a large codebase.

- ## [Why can't Cline edit a file and instead rewrites all lines? : r/CLine _202503](https://www.reddit.com/r/CLine/comments/1jgwao7/why_cant_cline_edit_a_file_and_instead_rewrites/)
  - When I ask Claude to add just one or two lines of code, it rewrites the entire thing instead of just adding those few lines , is that normal and any way to fix it?

- CLINE works like this:
  - It instructs Claude to use the `replace-in-file` tool, which is the efficient one.
  - When Claude tells CLINE to make a change using this tool, CLINE makes the change and then compares the previous / current versions to make sure there were changes.
  - If CLINE detects no changes, then CLINE assumes something went wrong and tells Claude again to make whatever change was needed and use the `write-file` tool instead, which is more expensive indeed, but then again - we want the task delivered.

- I noticed Cline would do this when my files were getting too large, like over 500 lines. You have to be careful when it rewrites entire files because sometimes it overwrites important code and breaks your app. Whenever it starts rewriting, I'll stop it and tell it to use `replace_in_file` tool instead.

- Cline does make pointed edits like you are describing, but not every time.
  - Basically -- making those pointed edits is more complicated under the hood, and Cline will often default to writing the whole file (which is actually much more accurate).
  - We're still improving on this process as it's one of the core tenets of AI coding.

- I keep getting my files cut off randomly at 834 lines or so
  - You're hitting an output cap on the model. Thats not Cline doing it, but the underlying LLM running out of output tokens.
- If you use Claude 3.7 with extended output on you can generate up to 64k tokens.

- ## [Roo Code 3.4 with NEW Lightning Fast DIFF Edits : r/ChatGPTCoding _202501](https://www.reddit.com/r/ChatGPTCoding/comments/1ibsich/roo_code_34_with_new_lightning_fast_diff_edits/)
- Are they doing what aider does?
  - That is a very broad question. Yes it is doing a search and replace like they are doing but they do so much differently. Aider is truly an amazing piece of software.

- You know what I like best about roo is there is less issue with truncation. Cline will delete huge blocks of code and I have the manually move the valid code over with copy paste because the new code Cline made literally is smack dab in the middle of a current code block. How were you able to figure this out when Cline people still haven't figured that out? 
  - The trick Roo uses is to ask the model to both write out the full content of the file AND include the total number of lines in the file. They’re not perfect at counting lines, but in cases where the number of lines predicted versus the number of lines returned differ significantly, we assume the write was truncated.

- get the ai to generate a patchfile and then apply the patch using old fashioned patch application - im not too sure how to do it in vscode but intellij has patch applier as a shortcut

- my Roo Code is still very slow, just like the one on the left. Any idea when we’ll get the lightning-fast version? Adding the following line to the global rules fixed the issue for me: "Prefer using the apply_diff tool to make changes.". I wonder why it defaults to slow line-by-line editing without this line? 
  - It does not always default to that way without those lines but it depends on the models. For some reason it does sometimes the model itself choose write to file over apply diff and we're working on a fix for that.

- ## [🚀 Introducing Fast Apply - Replicate Cursor's Instant Apply model : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1ga25gj/introducing_fast_apply_replicate_cursors_instant/)
- 
- 
- 
- 

- ## [I made LLMs respond with diff patches rather than standard code blocks and the result is simply amazing! : r/Jetbrains _202506](https://www.reddit.com/r/Jetbrains/comments/1l1r0o7/i_made_llms_respond_with_diff_patches_rather_than/)
- I've been developing a coding assistant called ProxyAI (previously CodeGPT), and I wanted to experiment with an idea where LLM is instructed to produce diffs as opposed to regular code blocks, which ProxyAI then applies directly to your project.

- All other solutions done this and better. Why this one?

- ## [Looking for diffing tools : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hfzrv9/looking_for_diffing_tools/)
  - I’m curious how tools like cursor and Lovable do their code diffing where the LLM suggests a change to some code and when approved it only changes the specific snippet rather than rewriting the full code file.

- One option was posted here: Introducing Fast Apply - Replicate Cursor's Instant Apply model

- Prompt engineering and Formatting, lots and lots of formatting. And then a “parser” of some sorts that will decode your custom formatting syntax into the patched changes into the file. Of course this means that whatever method you use to modify a file you need to be able to extract the parameters/data from your formatted content.
  - https://github.com/mckaywrigley/o1-xml-parser

- 💡 I made an open source parallel code editor tool (think codex but open source) recently, and I found that unified diffs + Google's diff-match-patch (this locally applies a diff using the line numbers and a fuzzy search... which helps when the LLM messes up line numbers) works well. You can also have the LLM output a full new file. In practice I expose both options to the LLM and carefully prompt it on when to use each.
  - You can see the prompts I use for this here: https://github.com/cairn-dev/cairn

- ## 💡 [advise on agent text editing : r/LLMDevs _202509](https://www.reddit.com/r/LLMDevs/comments/1nd330j/advise_on_agent_text_editing/)
  - I’m using ProseMirror (TipTap) to build an LLM edit feature. 
  - The hardest part is handling diff and preview in rich text (Markdown/HTML). 
  - In code editors like Cursor or Windsurf, the line-by-line structure makes this straightforward. 
  - But in a rich-text editor, mapping cursor positions and highlighting changes is far trickier.
  - Even OpenAI, in its canvas, refreshes the entire document instead of showing granular diffs, which I think misses the skeuomorphic experience writers actually need. Notion has only partly addressed this, and even then just for chunks of text, it doesn’t handle long docs really well

- 🤔 hey i had implemented this and it worked reasonably well. you need to look into json patching. you can use ai to generate the edit patch

- ## [GLM-4.6 and other models tested on diff edits - data from millions of Cline operations : r/ChatGPTCoding _202510](https://www.reddit.com/r/ChatGPTCoding/comments/1nwj7zq/glm46_and_other_models_tested_on_diff_edits_data/)
  - If you're not familiar with what "diff edits" are, it's when an LLM needs to modify existing code rather than write from scratch. 
  - An important caveat is that diff edits aren't everything. Models might excel at other tasks like debugging, explaining code, or architectural decisions. This is just one metric we can measure at scale.

- ## [[D] Better system prompt for generating coding diffs? : r/ChatGPTCoding _202501](https://www.reddit.com/r/ChatGPTCoding/comments/1ht88xx/d_better_system_prompt_for_generating_coding_diffs/)
- many projects require repeated modification of a python file.
  - Generating python code in unified diff format seems to be pretty crappy in gemini, and marginally better in claude.

- Have you checked out Aider? It uses several diff formats for applying patches to files. It’s open-source, so you can review the system prompts. Additionally, their blog provides statistics on how different models perform with various formats.

- Generating diffs are hard directly from an LLM given an un-deterministic nature of output unless they have the capability to run the code.
  - 💡 What I found working really effective is to let an LLM generate the full implementation of the smallest understandable unit of code. It could be a function or class depending on your code structure. Then you could apply it yourself or generate diff if required.
- Please note that this works very well with Python so please adapt if any change is required for a different language.

```prompt
As instructed before
If a change is required in an existing code.
Identify all the methods where change is required.
Then you should display the output like this.
List all imports first if needed
Then For each method
Display the method name along with the class name if that method belongs to a class.
Display FULL source code of the method even if the change is miniscule.

If the method belongs to a class then make sure to indent it to help the user paste it directly in the IDE

Do not add any explanation at the end. Keep it as concise as possible and always answer in English

Example When Imports are not needed and Change is in a method belonging to a class

Class: Foo
Method: Bar

"""
Code
"""

Example When Imports are not needed and Change is in a method which doesn't belong to a class

Class: None
Method: Bar

"""
Code
"""

```

- Here is a cool nugget from the aider codebase u/temofey and others: https://github.com/Aider-AI/aider/blob/37ad4758a1bca2ce5001cf7212c2d7ff49b49845/aider/website/docs/unified-diffs.md?plain=1#L213C16-L213C31 But I am unable to find where in the code base the system prompt actually encourages such a separation of +'s and -'s so well.

- ## [[D] Best way to make LLMs return a valid code diff : r/MachineLearning _202502](https://www.reddit.com/r/MachineLearning/comments/1iklsoo/d_best_way_to_make_llms_return_a_valid_code_diff/)
- Counting is hard for LLMs. You might have more success asking for the code that's on the line where the changes start, and the code that is on the line where the replacements end.
- Basically what I think will help is not relying on counting but on something LLMs are typically good at - language, words. So instead of trusting the numbers from the LLM, you would ask for the actual lines of code and triangulate from there. Duplicate lines are something you can detect in your triangulation code, and then ask the LLM for more context ("This line is repeated in the code. What is the line before this line?").
  - I think if you can feed both the line numbers and the code in the same prompt, then your chances are much better. If the LLM already has access to the line numbers and just has to select the correct start and end, it doesn't actually need to rely on counting, so that will probably yield good results.

- Instead of having it generate diffs directly, tell it to output the old code block before the edit, then write a program that converts that to a diff by finding the original block in the code file.
  - +1 that having instead provide a full code section and then post-process this into a diff is going be much more effective.
  - This is similar to how Cursor (and my IDE sparkstack.app) does it.

- My best approach till now is to give numbered lines. Ask to return numbered lines with edited content

- ## [How do I get an LLM to edit a few lines of code? : r/ChatGPTCoding _202502](https://www.reddit.com/r/ChatGPTCoding/comments/1ivnqmd/how_do_i_get_an_llm_to_edit_a_few_lines_of_code/)
- What everyone seems to be doing (and I'm working on my own version of this) is using multiple partial diffs. 
  - for each fragment you want to replace. On your client, you can do find-and-replace. 
  - Make this more precise by embedding line numbers
  - Then you can rely on Levenshtein Distance matching to give a bit of flexibility to the (old code) searching, and presto, you're golden. (Though when I say 'presto', it doesn't seem like anyone has this perfect yet, so...)

- Using partial diffs is a great idea but I think that still wouldn't work if you're editing lines which are not unique in the source code.
  - Although as I'm writing this I realize one option could be to tell the LLM to include more lines to the diff if the code portion to be edited is not unique. Not sure if this is a good option at all though.
- I'm thinking you'd use something like tree-sitter (which Aider uses to provide code maps to the LLMs) to tag entities like functions with hashes/ids behind the scenes before sending. Then only do diffs on whole individual functions.

- Just replying as I have also been searching for this for over a year, and finally found the answer: I started testing Claude for the first time this week and it looks like it has this functionality built in by default.
  - If you ask it to modify something that requires changing only a single paragraph of code, it will leave the rest of the codebase untouched and edit only what it needs to.
  - It's insane that that the majority of LLM's and frontends out there can't do this yet. Even Google's Gemini 2.5 pro fails dysmally.

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

- Aider actually prompts the LLM to use search/replace blocks rather than actual diffs. And then has a bunch of regex, fuzzy search, indent fixing etc code to handle inconsistent responses.
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

- Applying instructions/changes to an existing codebase is by far the hardest part of making something like Cursor. The Cursor guys notoriously trained their own model for this. That's why you can't use your own API keys to have the Apply button work in Cursor. Using Claude/ChatGPT for complex instructions and multiple code edits in one pass just doesn't work.
  - I know because I'm making a Cursor competitor myself and tried that. My first iteration of applying changes used this prompt to formalize changes. It did not work well.
  - prompt  https://pastebin.com/2fx4miv0
  - I never really tried using actual diff formats like you suggest - I saw Aider did that and their Apply Changes results weren't great either.
  - My latest version I'm trying to break up code into 'top level scopes' using `Treesitter` AST parser, and match the first line of those top level scopes to lines in files in the existing codebase. Once I have those I make sliding windows to tell the LLM just focus on changing this code in this file in this window keeping everything else in this snippet working but making the appropriate changes. But breaking up changes is rough - there are so many unexpected cases of what the LLM gives you, I've been writing edge cases for months now. It's a rough problem. I don't think anyone is getting great results for complex diffs - even Cursor messes up often and they have a team of MIT grads working full-time on this.

- I've done a bit of work trying to generate diffs. I think you have no other choice than to get hands on and try what works.
  - In my experience, trying to get an output "in 1 shot" that is composed of changes to a piece of code and also have this be in a correctly formatted diff... Failed more often than not.
  - It either ignored part of the instructions that it needed to follow or it generated erroneous diff. 
  - Asking to get the code right, and then, making that code a diff, was better. Trying to use chain of thought to keep it in one prompt didn't make a difference, as it would say it was gonna do x, y, z... But then suck at some of the steps.
  - With Claude, giving info in XML tags worked very well (to classify parts of the prompt as "original code" "instructions" and so). My attempts to use JSON and function calling were less successful, I felt it "dumbed down" the coding part when asking for that. But your mileage(用处, 好处) may vary and I may have been doing something wrong. In another project the JSON/function calling works without issues (but what I ask sonnet 3.5 is simpler, not much "thinking" needed).
# discuss-toolchain-diff
- ## 

- ## 

- ## 

- ## [Difftastic, a structural diff tool that understands syntax | Hacker News _202403](https://news.ycombinator.com/item?id=39778412)
- For those who don't already know, this is built on tree-sitter which does for parsing what LSP does for analysis. 
  - 
  - That is, it provides a standard interface for turning code into an AST and then making that AST available to clients like editors and diff tools. Instead of a neat tool like this having to support dozens of languages, it can just support tree-sitter and automatically work with anything that tree-sitter supports. And if you're developing a new language, you can create a tree-sitter parser for it, and now every tool that speaks tree-sitter knows how to support your language.

- 
- 
- 

# discuss-edit-format/protocol ⚖️
- ## 

- ## 

- ## 

- ## 

- ## 

- ## ⚖️ [DiffX – Next-Generation Extensible Diff Format | Hacker News _202506](https://news.ycombinator.com/item?id=44176737)
- I really don’t like the highly hierarchical format, that there’s a “..meta” and a “…meta” somewhere else. I can imagine we want to annotate the whole diff, each file and each chunk. That’s a total of 3 levels of depth. Let’s just give them distinct names and not go full yaml with a format for once?
  - This helps with readability (if one of the “meta” blocks is missing, for example, I could still tell at a glance what it refers to without counting dots), and is less error prone (it make little sense to me why the metadata associated with a whole diff should have the same fields as the metadata of a file).
  - Furthermore, why do we have two formats? Json and key=value pairs? Having a single structure makes it much easier to write parsers or integrate with existing tooling (grep, sed or jq - but not both at once)
- In the early drafts, we played with a number of approaches for the structure. Things like "commit-meta", etc. In the end, we broke it down into `#<section_level><section_type>` , just to simplify the parsing requirements. Every meta block is a meta block, and knowing what section level you're supposed to be in and comparing to what section level you get become a matter of "count the dots".
  - The header formats are meant to be very simple key/value pairs that are known by the parser, and not free-form bits of metadata. That's what the "meta" blocks are for. The parsing rules for the header are intentionally very simple
  - JSON was chosen after a lot of discussion between us and outside parties and after experimentation with other grammars. The header for a meta block can specify a format used to serialize the data, in case down the road something supplants JSON in a meaningful way. We didn't want to box ourselves in, but we also don't want to just let any format sit in there

- diffs are inherently splittable. I can grab half of a diff and apply it. How does your format influence that? I guess it breaks because I would need to copy the preamble, then skip 20 lines, then copy the block I need?
  - If your goal is to simply feed to GNU patch (or similar), you can still split it. This extra data is in the Unified Diff "garbage" areas, so they'll be ignored anyway (so long as they don't conflict, and we take care to ensure that in our recommendations on encoding).
  - If your goal is to split into two DiffX files, it does become more complicated in that you'd need to re-add the leading headers.
  - That said, not all diff formats used in the wild can be split and still retain all metadata. Mercurial diffs, for example, have a header that must be present at the top to indicate parent commit information. You can remove that and still feed to GNU patch, but Mercurial (or tools supporting the format) will no longer have the information on the parent commit.
  

- A staggering amount of unnecessary and counterproductive scope creep in just 4 items:
  - A single diff can’t represent a list of commits
  - There’s no standard way to represent binary patches
  - Diffs don’t know about text encodings (which is more of a problem than you might think)
  - Diffs don’t have any standard format for arbitrary metadata, so everyone implements it their own way.
  - Of these, only a notation for binary patches would be a reasonable generalization of diff files. Everything else is the internal data structure or protocol of some specific revision control system, only exchanged between its clients and servers and backups.

- 💡 The patch format addresses all of these issues, no? https://git-scm.com/docs/git-format-patch
  - It might solve it for git, but this looks like something the Review Board team came up with, and they have to integrate with many other version control systems like SVN, CVS, Perforce..etc
  - Seems like this is meant to address supporting many different version control systems with a single format.

- So, self-delimitered format (JSON) is embedded in format with lengths? I change one space in JSON, JSOM is valid, whole DiffX file is invalid.
  - Format looks very clunky and messy, to be honest, mixture of self-invented headers and JSON payloads, strange structure (without comments here I will not notice different number of dots in `.meta`), need essentialy two parsers.

- One of my issues that remains unsolved with diff tools is they are dependent on new line attributes. Reviewing changes on a long line (like compressed json or long array) is too difficult.
  - Absolutely agree. I think there's a lot of avenues to explore for better diff representations for structured data (which would also be great for ASTs, something we've been thinking about).
  - This format is meant to be an extension of Unified Diffs (much like the diff formats of most SCMs), and not something entirely new and focusing on other areas. But if more specific diff formats become widespread, we could directly support encoding them within DiffX as well, as we do for binary diffs formats.
  
  

- 💡 git does have word diffing if you need something more granular than line diffing, the default delimiter being whitespace.
  - I didnt' realize that. that seems pretty close to what I want, but the git tools (cli or Github Desktop) still print the entire line.
  - For line diffing, it clips to only show the ~3 line before and after the change. But the word diff still prints the entire line and you have to scroll to find the change in the line wrapping.
- You can use `delta` as a diff pager and it includes word-diff-syntax-highlight.

  
  

- The most general and unambiguous way to represent a diff is to just include the contents of the two files. It's more data, but that's rarely an issue these days. There's really no need to ever transmit a diff and deal with all the format vagaries when you can just send the two files.
  - A diff between two files isn’t unique, meaning there can be better or worse diffs between the same two versions of a file, depending on the file format and possibly the purpose of the diff. Similarly, there can be different strategies for applying a diff as a patch.
  - Having a diff format allows decoupling the implementation of diff creation from the implementation of diff application, turning a potential n*m problem into an n+m problem.
  
  

- difftastic: https://difftastic.wilfred.me.uk/ uses tree-sitter for better diff-info, and is, imho, superior to this.
  - difftastic is great! This isn't a tool for viewing changes to files or to ASTs. 
  - This is a way of being able to generate a single diff file for processing or patching that addresses the kinds of problems we've encountered in over 20 years of building diff parsing tooling and working with over a dozen SCMs with varying levels of completeness or brokenness of bespoke custom diff formats. 
  - It's not an end user tool, but a useful format for tools like code review products to use.
- This looks great. The diff is quite inefficient for patching with the C preprocessor branches.
  - Since it patches the code, looking at its tree structure, is the diff human readable, and can it be edited directly? This is a major contributor to why I opt for sed for patching.

- One of the interesting point of diff files is that all commands are on single lines. You can easily parse or manipulate with simple shell tools just stripping lines out.

- > They don’t standardize encodings, revisions, metadata, or even how filenames or paths are represented!
  - Sure, but some unified diffs, e.g. the ones produced by git, are quite regular. It's also common practice to express diffs as RFC822 email messages (often because they come that way), with headers and descriptive text.
  - I can't see DiffX getting traction. It's too alien. Too divorced from present practice, no matter how theoretically robust. It's like XHTML2.
  

- They could have built on top of git’s header syntax for metadata (which itself is based on email headers) instead of reinventing it in a new flavour of pseudo-JSON.

- For stuff like commit histories or complex changes, isn't the real power in the tools around the diff (think Git itself, or code review platforms) rather than trying to cram everything into one super-format?
  - It is. However, first the tools need to be able to grab the necessary information from the diff to, say, locate that file or its metadata in a repository.

- This is trying to do multiple things (commit info & file diff) in one. Not a good idea. Commit info should live in the repo metadata (no matter which form this takes), and diff should be its own thing.
  - The repository metadata absolutely should own the commit information.
  - Diff files are there to represent a delta state of the repository, a difference between a range of changes. Those may be one or more commits, or one more changes across individual files (not all SCMs manage state in terms of atomic commits). File changes, file attribute changes, SCM-specific metadata changes, and commit history information.
  - That delta state should be able to be applied to another tree in order to get the same end result. This is what diff files are ultimately there for.
  - Git diffs do this today, and they do it well (but they're pretty Git-specific). Many SCMs (and there are a lot of them) don't include a format on that level, or a format at all. Hence DiffX.

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

- ## [Automated Patch Diff Analysis using LLMs | SySS Tech Blog _202509](https://blog.syss.com/posts/automated-patch-diff-analysis-using-llms/)
- https://github.com/SySS-Research/diffalayze /MIT/202509/python
  - diffalayze is a versatile toolkit for automating patch diffing of binary targets and enriching the results with deep-dive analysis from large language models (LLMs). 
  - It is designed for reverse engineers, vulnerability researchers, and security teams who need to track software changes

- Patch diffing is great for finding what changed between two versions of a binary, but the volume on typical patch days is high and manual triage costs a lot of time. 
  - The shown approach pipelines a binary diff, extracts the relevant changes, and lets an LLM score and summarize security relevance so a researcher can focus on the promising parts first.

- Patch diffing is a powerful technique for identifying code changes and understanding what a patch actually affects. While diffing with access to source code is relatively straightforward, it becomes much more challenging when working with native binaries.
- Fortunately, several tools exist to address this problem and support binary-level diffing, for example BinDiff, Diaphora, or ghidriff. ghidriff is a great open-source tool developed by clearbluejar, which combines multiple techniques to detect and visualize code differences in binaries.
- However, there is an obvious bottleneck: finding the needle in the haystack. On a typical Mictrosoft Patch Tuesday, thousands of lines of code (LOC) change across many binaries. Manually skimming all diffs is time-consuming and this is where LLMs can help with triage.

- ## [The evolution of a structural code editor | Hacker News _202501](https://news.ycombinator.com/item?id=42608923)
- for diffing syntax trees, I've been trying out diffsitter, and it feels pretty good so far https://github.com/afnanenayet/diffsitter

- Plain Text diffing has some obvious drawbacks:
  1. If you rearrange your functions you will see a lot of additions and deletions while semantically there is no change in the program. It's just noise.
  2. If you rename a variable you don't really have any actual change in places where it is referenced but text diff will again show a lot of noise. But the code references is still the same code.

- ## [Fifty Years of Diff | Hacker News _202406](https://news.ycombinator.com/item?id=40692926)
- I wish more engineering tools had an equivalent of diff. Manually redlining schematics and drawings is such a pain.
  - that's a really interesting idea. Many formats representing drawings like SVG and Kicad Schematics are text formats, not binary. They can be diffed, and it's a matter of rendering the diff as part of the drawing, not as text. I wonder if anyone is working on such a thing.

- AllSpice.io provides graphical diffs for KiCad schematic and PCB files (and others) in a Gitea-based forge: https://allspice.io/. Disclosure: I work there (mostly on binary formats), it's a paid service

- ## [Developer tool 'diff' is 40 years old: can it be improved? | Hacker News _202408](https://news.ycombinator.com/item?id=41360874)
- https://github.com/dandavison/delta is nice for a prettier presentation of the same information as `git diff` .
  - This may or may not qualify, since I think GNU diff supports it with an option, as does Git diff, but "Color-words" diff can be nice, where changes in the middle of the line are highlighted and whitespace is ignored.
  - Somebody already recommended https://github.com/Wilfred/difftastic, which I second. It uses treesitter and is very interesting. Surprisingly, in practice difftastic is not always noticeably better than color words diff (don't expect miracles), but occasionally it is much better.

- Difftastic's wiki has more related tools: https://github.com/Wilfred/difftastic/wiki/Structural-Diffs.

- ## [Editing text files with LLMs : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o592o0/editing_text_files_with_llms/)
- It's about tools. Make file editing tools, tools to open/create a file, edit a file, rename/delete a file, search a file, etc. 
  - If your stuff has MCP, you can download tons of mcp file editing tools, 
  - if you want to implement yours, you can peek at the source of a few of those, plenty python and javascript examples to inspire you.

- Any of the current agentic coders work fine for this - claude code, crush, codex cli, gemini cli, qwen code, etc. You can make a simple python file as well that can call an API and take the returned text and save it to a text file if you wanted to get right down to the metal with it.

- Personally, I use the Obsidian MCP server with Claude Desktop. This way Claude has full access to my notes — it can search, add, edit, summarize, and more. 
  - Since Obsidian uses plain text Markdown files, you can simply use MCP Filesystem (or Desktop Commander) and point it to your Obsidian folder ("vault").

- Easiest way is to write an MCP to edit files and let your LLM have tool access to it. I do the same with a SQL database so that my LLM can do arbitrary reads to the database to pull information.

- ## 🆚 [Unified versus Split Diff | Hacker News _202310](https://news.ycombinator.com/item?id=37995155)
- A third (fourth?) option worth mentioning here is difftastic, which uses "structural" diffing (as opposed to line diffing) for more granular diff highlighting.
- A fourth (fifth?) option worth mentioning is patdiff: https://opensource.janestreet.com/patdiff/ From what I remember, it sometimes (35%) made diffs easier to read, usually (60%) made no difference, and rarely (5%) made them harder to read. The only reason I stopped using it was because I started using magit for git diffs.
  - Based on Bram Cohen’s patience diff algorithm, patdiff is optimized for diffing code and config files.
  - Patdiff includes both an OCaml library (Patdiff_lib) as well as a command-line tool (patdiff).
  - Word-level refinement: Rather than displaying a small change to a line as a wholesale removal and addition of that line, patdiff shows the word-level diff of that line.
  - Recursive diffing of directories
  - Whitespace-aware diffing
- I agree that the patience diff algorithm generally produces better results, but you don’t need the patdiff tool for that. You can configure Git’s own diffs to use patience
  - patdiff also provides word-level diffing. You could instead get that feature with `git diff --word-diff` or Delta (https://github.com/dandavison/delta).
  
- Git doesn't store diffs on logical level. Git operates on snapshots of trees. Commit is not "a collection of changes", it's a snapshot of a tree with attached predecessor of it.
  - Then the another layer (which can be git, but also can be any other tool, adding custom diff tool to git is very easy) uses that to generate diffs.
  - There is zero stopping anyone from adding contextual diffs to Git. Just ask it for content of both commits and feed it to the algorithm.
  - Yes, git underneath stores data as diffs but they are only vaguely related to logical structure of commits
- And that's why we call that lower level compression trick "delta", not "diff".

- Wonder if something like that can be used to make git cleverer about merges for example.
  - Git’s merge algorithm looks at three versions of the code: the two branch tips being merged, and their common ancestor. It might be better at resolving conflicts if it looked at some of the intermediate commits as well, but I don’t know of anything that does so.
- Merge part isn't pluggable like that IIRC. Would be interesting if that was given stable interface, then supposed "smart merge" tool could iterate with few ways to merge code while running tests to check which one produces least/no errors

- ediff in emacs does this. Refine is what highlights the words that are different.

- Meld works pretty well for these use cases. https://meldmerge.org/
- A honorable mention is also https://kdiff3.sourceforge.net/ which has a lot of nice views.
  - https://invent.kde.org/sdk/kdiff3
- I often hear KDiff3 recommended in these cases. There are many graphical diff visualizers. I often use the ediff functions in Emacs.

- Looks a lot like FileMerge, which comes with the Apple developer tools.

- For me, it's always unified diff if i'm making changes to entire blocks of code, but split, if it's just parts of it. Easier to read, in my opinion
- In my experience unified diff is good for small changes. Split diff like meld is good for many changes in a long file. Many diffs in a long long file, you should not have such a file.

- What the author wants is git blame with highlights. IntelliJ does this very good. On the margin to your left you can see the age of each line. Recent changes - the one you are reviewing - will be be bright white, while older proven code more faded. All inside the already powerful editor you need to navigate bigger pieces of code. 
  - Except that will not show you removed lines. Forget it, just use the diff feature.
  
  
- The only real solution to this is "avoid big diffs at all cost". This is why the industry as a whole has mostly dropped git flow and moved back to trunk based development.

- ## [Diff Models – A New Way to Edit Code | Hacker News _202301](https://news.ycombinator.com/item?id=34556688)
- From the safety perspective (may get important soon), it is perhaps a very bad idea to allow easy execution/injection of arbitrary code into random places with little review.
  - When designing such systems, please do keep that in mind. Make sure code changes are properly signed and the originating models are traceable.
  - Same applies to datasets generated by models.

- It would have been helpful to show some example generations of the model, unless I've missed them.
- [CarperAI/diff-codegen-6b-v2 · Hugging Face _202301](https://huggingface.co/CarperAI/diff-codegen-6b-v2)
  - diff-codegen-6b-v2 is a diff model for code generation, released by CarperAI. A diff model is an autoregressive language model trained on edits to a piece of text, formatted in Unified Diff Format. 
- My understanding is you have in training dataset the original code, diff + commit message. So you train the LM to: Input: code+commit output: diff
