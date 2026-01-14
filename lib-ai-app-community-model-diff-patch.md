---
title: lib-ai-app-community-model-diff-patch
tags: [community, diff, diff-match-patch, editor, large-language-model]
created: 2025-10-08T06:33:26.386Z
modified: 2025-10-10T02:45:45.941Z
---

# lib-ai-app-community-model-diff-patch

# guide
- tips
  - llm-edit-pattern: editing-prompts > changes > applying-changes
  - 可直接参考主流编辑器已实现的方案，如codemirror/monaco

- 使用markdown格式作为ai编辑的输入输出优点是ai擅长markdown，缺点是markdown扩展标准不统一
  - 另一种思路是用prompt指示ai输出html, 各种富文本编辑器对html的复制粘贴都很成熟

- ⚖️ aider-diff-search/replace format prompt
  - local-models: qwen3-14b, gpt-oss-20b
  - 几乎都支持: gpt, claude, gemini, deepseek, qwen, glm, kimi, minimax
  - 失败率较高: qwen3-coder, glm-4.6, mimimax-m2
  - https://github.com/asadm/vibemode/blob/main/source/editor.js
  - https://github.com/sorendunn/Agentless-Lite/blob/main/agentless_lite/repair.py
  - https://github.com/profullstack/ai/blob/master/lib/enhanced-agent.js
  - https://github.com/wheeyls/remote-pair-programmer/blob/main/src/prompts/codeModification.txt
  - https://github.com/ggml-org/llama.vscode/blob/master/src/prompts.ts
  - https://github.com/XAI-liacs/LLaMEA/blob/main/llamea/llamea.py

- ⚖️ openai v4a diff format 多尝试几种测试用例来判断成功率; 不如aider-diff流行
  - local-models: qwen3-14b-no_think, gpt-oss-20b
  - supported: gpt-4.1-mini, claude 3.7+, gemini-2.5-pro, deepseek-v3.1, kimi-k2, minimax-m2
  - no-support: qwen3-coder-480b, qwen3-235b-a22b-thinking/instruct, glm-4.6(有时会成功), longcat-flash
  - https://github.com/openai/codex/blob/main/codex-rs/core/prompt.md
    - https://github.com/openai/codex/blob/main/codex-rs/apply-patch/src/parser.rs
  - https://github.com/microsoft/vscode-copilot-chat/blob/main/src/extension/tools/node/applyPatchTool.tsx
  - https://github.com/sst/opencode/blob/dev/packages/opencode/src/patch/index.ts
  - https://github.com/buchuleaf/fry-cli/blob/master/src/tools.tsx
  - https://github.com/khpbvo/SingleAgent/blob/main/scripts/apply_patch_prompt.py
  - https://github.com/computabeast/qernel/blob/main/src/exe/core/src/tool_apply_patch.rs

- 考虑编辑的场景
  - shorter/longer/improve/check/translate 都可实现为对明确输入范围内容的 一次性替换

- [Fast-Apply API Research Summary · edobry/minsky](https://github.com/edobry/minsky/blob/main/docs/phase1-fast-apply-api-research.md)
  - Integration Architecture Recommendations
  - ApplyProvider Abstraction Layer
  - Fallback Strategy
  - Session Integration
  - https://colab.research.google.com/drive/1BNCab4oK-xBqwFQD4kCcjKc7BPKivkm1?usp=sharing

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
- https://github.com/vizhub-core/editcodewithai /3Star/MIT/202509/ts
  - A lightweight, flexible library for AI-powered code editing.
  - The core idea is that you can feed this system a set of source code files and high level instructions, and it will return the edited code after some time. 
  - It provides a simple interface to send code files and instructions to an LLM (Large Language Model) and receive edited code in return.
  - 依赖langchain、llm-code-format
  - The library is designed to be model-agnostic, allowing you to use any LLM provider
  - Edit formats inspired by Aider. This library supports several "edit formats" that instruct the LLM on how to specify file changes.
    - Different models may perform better with different formats. 
    - You can specify the format using the `editFormat` parameter 

- https://github.com/deepaste-ai/partial-edit /202504/ts/inactive/NoDeps
  - This project is a TypeScript implementation of the approach described in OpenAI's GPT-4.1 prompting guide
  - 一个纯 TypeScript 工具，用于应用人类可读的伪差异补丁文件，具有由 LLM 驱动的部分编辑功能。
  - 依赖langchain、@langchain/core
  - 提供了cli示例
  - Patch Processing: Apply human-readable pseudo-diff patches to text files
  - Partial Editing: Make context-aware edits to code using LLM
  - DeePaste 应用补丁的方式与 OpenAI 的 GPT-4.1 提示指南中讨论的技术类似。该指南提到，在代码修改任务中，同时提供需要替换的确切代码和带有明确分隔符的替换代码可以产生高成功率。像伪差异这样不依赖行号的格式对于 LLM 驱动的代码编辑特别有效。
  - [GPT-4.1 Prompting Guide Appendix: Generating and Applying File Diffs](https://cookbook.openai.com/examples/gpt4-1_prompting_guide#appendix-generating-and-applying-file-diffs)

- https://github.com/Rolilink/unshallow/tree/main/src/core/patch-diff /202507/ts
  - Unshallow is being rebuilt as a CLI tool for migrating Enzyme tests to React Testing Library
  - The patch-diff system provides a robust, context-based approach to applying code changes using the V4A (Version 4A) diff format
  - The system automatically handles Unicode variants
  - Context matching uses a 3-pass algorithm

- https://github.com/talesofai/python_replace_string /MIT/202508/python/inactive
  - 从kilo的ts代码中获取replace_string功能，由kilo编辑器迁移到python实现
  - 字符串替换: 支持精确匹配、正则表达式 和 模糊匹配(基于 Levenshtein 距离的相似度计算)
  - 完整兼容 Kilo Code 的 apply_diff 工具格式
  - 支持并发和顺序批量任务执行

- https://github.com/tokenring-ai/apply-patch /apache2/202510/ts
  - a TypeScript implementation of the OpenAI Codex file-oriented diff format for safe code editing. 
  - It converts the original Rust implementation to native TypeScript
  - File Safety: Operations are atomic where possible
  - Path Handling: Only relative paths supported for security
  - 侧重文件操作: it uses native Node.js APIs for file operations.

- https://github.com/nocapro/apply-multi-diff /202509/ts/NoDeps
  - library to apply standard unified diffs or semantic search-and-replace patches to source files with fuzzy-matching, indentation-preserving insertions, and hunk-splitting fallbacks.
  - for Node.js and browser environments
  - TL; DR for agents
    - Use Search-Replace when you want precise, targeted edits (add import, rename function, delete block). 
    - Use Standard Diff when you have a complete diff from git (multi-hunk, moved code). 
    - When in doubt, start with Search-Replace—its fuzzy matcher is more forgiving of small source drift.

- https://github.com/theluk/llm-patcher /apache2/2022406/ts/inactive
  - https://llm-patcher.vercel.app/
  - An open-source AI find-and-replace workflow template built with Next.js, the Vercel AI SDK and OpenAI.
  - Whenever we provide a text to an LLM and ask it to do some changes, it will always stream the full text back to us. This is not ideal for large texts, as it can be slow and expensive. 
  - This project aims to solve this problem by providing a way to stream only the changes made by the LLM back to the user.
  - How does it work?
    - The user provides a text and a find-and-replace query.
    - The text is split into lines and sentences.
    - Each line and sentence is then prefixed with a identifier that looks like `<l1s1>` for `line 1, sentence 1`.
    - The LLM is then asked to find-and-replace the query in each line and sentence.
    - The changes are then streamed back to the user in the form of a diff(e.g., `<r:l1s1> string to find || string to replace`).
  - [How to use LLM for efficient text outputs longer than 4k tokens? - DEV Community _202406](https://dev.to/theluk/how-to-use-llm-for-efficient-text-outputs-longer-than-4k-tokens-1glc)

- https://github.com/dceluis/ln-diff /MIT/202411/prompt/inactive
  - The ln-diff format is a specialized diff format designed for precise line-based code modifications. 
  - It uses "editblocks" to explicitly define code changes while maintaining strict line number references.
  - ln-diff stands for line-number-diff. 
  - 🤔 基于line-number的方案要取舍
  - If you are working with LLMs and to generate code, you have probably faced the challenge that while they may be good at generating new code, they struggle much more to apply it to existing files and codebases. 
  - Having tried multiple approaches like instructing it to generate edits in the well known unidiff format or some variation of diff-match-patch. These formats are too algorithmically complex for LLMs
  - I propose a different approach here: to leverage LLMs strong recitation capabilities to generate patches that apply cleanly to the source format and provide enough it with enough context for generating high-quality replacements.
  - Line numbers in both the source and editblocks helps llms recite(背诵；列举) the exact line more accurately.
    - Source files need to be prefixed the line numbers so that the lines to REMOVE can be recited accurately and sequentially.
  - A[ The "pipe" symbol used is not your regular keyboard pipe but actually unicode's U+2502 called "Box drawings light vertical". This is a common symbol used to draw lines in text-only applications and may be understood by LLMs (TODO: verify this) to be the divider between the line number and the actual line contents. Alignment may help with reducing indentation errors in generated code.
  - https://github.com/dceluis/kznllm.nvim/tree/dev/lua/kznllm/lndiff /lua

- https://github.com/NeaByteLab/AI-NES /MIT/prompt
  - Next Edit Suggestion (NES) - A conceptual methodology for AI coding assistants that learn from editing patterns and predict the next logical edit using `unified diff format` and real-time streaming.
  - Instead of just completing what you're typing, the LLM learns from your editing patterns and predicts what you'll want to change next in your coding workflow.
  - Pattern Learning: The environment sends context to the LLM (Large Language Model) by analyzing what should be edited. 
  - Streams suggestions as you work

- https://github.com/paradite/ai-file-edit /14Star/MIT/202506/ts/inactive
  - A library for editing files using AI models such as GPT, Claude, and Gemini.
  - Edit files using natural language
  - 提供了cli示例
  - Overwrite existing files
  - Support for multiple file edits in a single operation
  - 🆚 The tool generates both forward and reverse diffs for all file changes. 
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
- https://github.com/waleedkadous/edit_trick /202504/python
  - This project demonstrates the "edit trick" - a more efficient approach to using LLMs for document modification tasks that reduces token usage, processing time, and handles longer documents.

## ai-edit-papers

- https://github.com/kortix-ai/fast-apply /apache2/202509/python
  - Fast Apply: Pipeline for Data Generation & Fine-Tuning Qwen2.5 Coder Models
  - Update Sept 2025: For production-grade throughput, we use Morph (the hosted Fast Apply API powering SoftGen AI).
  - 🌰 [Fast Apply](https://github.com/jedi4ever/devoxx-workshop-testing/blob/main/lessons/01-prompt-and-llm/04-fast-apply.ipynb)
  - 🍴 forks
  - https://github.com/dat-lequoc/fast-apply
- https://github.com/betmoar/FastApply-MCP /202509/python
  - Code Intelligence Platform with semantic search, AI-powered transformations, and enterprise security. 
  - FastApply MCP Server delivers comprehensive code analysis through local model execution and intelligent pattern recognition.
  - Local Model Architecture: Uses edit_file functionality like MorphLLM through (Kortix/FastApply-1.5B-v1.0_GGUF)
- https://github.com/jianghoucheng/AnyEdit /MIT/202510/python
  - AnyEdit: Edit Any Knowledge Encoded in Language Models, ICML 2025
  - [AnyEdit: Edit Any Knowledge Encoded in Language Models | USTC Lab for Data Science _202505](https://data-science.ustc.edu.cn/_upload/tpl/15/04/5380/template5380/publication/icml25-jhc.html)
    - Current model editing methods, however, struggle with long-form knowledge in diverse formats, such as poetry, code snippets, and mathematical derivations. These limitations arise from their reliance on editing a single token’s hidden state, a limitation we term efficacy barrier. 
    - To solve this, we propose AnyEdit, a new autoregressive editing paradigm. It decomposes long-form knowledge into sequential chunks and iteratively edits the key token in each chunk, ensuring consistent and accurate outputs. 
    - AnyEdit serves as a plug-and-play framework, enabling current editing methods to update knowledge with arbitrary length and format, significantly advancing the scope and practicality of LLM knowledge editing.
- https://github.com/SalesforceAIResearch/inksync /apache2/202408/python/inactive
  - [[2309.15337] Beyond the Chat: Executable and Verifiable Text-Editing with LLMs](https://arxiv.org/abs/2309.15337)
  - To give the author more agency when editing with an LLM, we present InkSync, an editing interface that suggests executable edits directly within the document being edited. 
  - Because LLMs are known to introduce factual errors, Inksync also supports a 3-stage approach to mitigate this risk: Warn authors when a suggested edit introduces new information, help authors Verify the new information’s accuracy through external search, and allow an auditor to perform an a-posteriori verification by Auditing the document via a trace of all auto-generated content. 
- https://github.com/Banner-Z/G-SPEED /apache2/202310/python/inactive
  - The official repository of paper G-SPEED: General SParse Efficient Editing MoDel (Findings of EMNLP-2023).
  - [[2310.10480] G-SPEED: General SParse Efficient Editing MoDel](https://arxiv.org/abs/2310.10480)
- https://github.com/zjunlp/EasyEdit /MIT/202510/python
  - https://zjunlp.github.io/project/KnowEdit
  - [ACL 2024] An Easy-to-use Knowledge Editing Framework for LLMs.
- more-editing-solutions
  - [EfficientEdit: Accelerating Code Editing via Edit-Oriented Speculative Decoding | Abstract _202506](https://arxiv.org/abs/2506.02780v2)
  - [[2502.13358] Bridging the Editing Gap in LLMs: FineEdit for Precise and Targeted Text Modifications](https://arxiv.org/abs/2502.13358)

## diff-utils

- https://github.com/ace-diff/ace-diff /MIT/202507/js/inactive
  - https://ace-diff.github.io/ace-diff/
  - A diff/merging wrapper for Ace Editor built on google-diff-match-patch
  - This is a wrapper for Ace Editor to provide a 2-panel diffing/merging tool that visualizes differences in two documents and allows users to copy changes from to the other.
  - It's built on top of google-diff-match-patch library. That lib handles the hard part: the computation of the document diffs. `ace-diff` just visualizes that information as line-diffs in the editors.
- https://github.com/davidkjeremiah/patchai /MIT/202510/python
  - LLM-powered structured file editor - edit JSON/YAML with natural language, see diffs, use any AI model
  - PatchAI lets you edit JSON, YAML, and config files using natural language instructions.
  - Visual Diff - See exactly what changed with beautiful unified or side-by-side diffs
  - Undo/Reset - Full history tracking with easy undo
- https://github.com/radekstepan/apply-llm-changes /202510/ts
  - A command-line tool that applies file changes from LLM output to your local filesystem.
  - AI-Powered Path Detection: Uses LLM to determine file paths from markdown code blocks
  - Preserves code context and formatting

- https://github.com/PyneSys/patch-file-mcp /MIT/202504/python/inactive
  - An MCP Server to patch existing files using block format. This allows AI agents (like Claude) to make precise changes to files in your projects.
  - You can include multiple search-replace blocks in a single request
  - 依赖fastmcp实现
  - `patch_file(file_path: str, patch_content: str)`

- https://github.com/ucsb-mlsec/PatchPilot /MIT/202506/python/inactive
  - A Stable and Cost-Efficient Agentic Patching Framework
  - PatchPilot is an innovative rule-based planning patching tool that strikes the excellent balance between patching efficacy, stability, and cost-efficiency.

- https://github.com/trailofbits/graphtage /2.4kStar/LGPL/202512/python
  - a command-line utility and underlying library for semantically comparing and merging tree-like structures, such as JSON, XML, HTML, YAML, plist, and CSS files.
  - Graphtage performs an analysis on an intermediate representation of the trees that is divorced from the filetypes of the input files. This means, for example, that you can diff a JSON file against a YAML file
  - By default, Graphtage will format the output diff in the same file format as the first input file. But one could, for example, diff two JSON files and format the output in YAML. 
  - By default, Graphtage tries to match all possible pairs of elements in a dictionary.
  - Diffing tree-like structures with unordered elements is tough. Say you want to compare two JSON files. There are limited tools available

## diff-vscode

- https://github.com/dsj7419/patch-pilot /MIT/202505/ts/inactive
  - PatchPilot turns raw diffs—whether hand-written, auto-generated by AI, or copied from code reviews—into perfectly-applied patches inside VS Code, even when line numbers have drifted or files have shifted. 
  - [I built a VS Code extension — "PatchPilot" — for smarter AI diff patching (free tool) : r/ClaudeAI _202504](https://www.reddit.com/r/ClaudeAI/comments/1kae13r/i_built_a_vs_code_extension_patchpilot_for/)
    - Supports multi-file diffs, not just single files.
    - Offline-first: No data ever leaves your machine.

## diff-toolchain

- https://github.com/chen893/agent-x /202507/ts/inactive
  - 基于 T3 Stack 构建的智能 AI 代码生成平台，集成多个大语言模型，提供从需求分析到代码实现的全流程自动化开发体验。
  - tRPC, Prisma, NextAuth.js

- https://github.com/asadm/vibemode /apache2/202505/js/inactive
  - Pack your entire repository (or selected files) into an AI-friendly format and also apply AI suggested changes back with ease, all from your terminal.
  - vibemode is a CLI-based code companion to help when you are coding 
  - Take the diff-like output provided by an AI (in any format it gives it back to you) and apply those changes directly back to your local files using the Gemini API.
  - I usually resort to using the model directly using the official UI they provide by copying relevant (or all) my code into the chat UI. The model then suggests changes in chat. I then want to apply the suggested changes back to my repo. vibemode is the missing glue for this workflow!

- https://github.com/sorendunn/Agentless-Lite /MIT/202504/python/inactive
  - RAG-based SWE-Bench software engineering scaffold
  - lightweight adaptation of the Agentless framework for solving software development issues
  - https://github.com/OpenAutoCoder/Agentless /MIT/202412/inactive
    - Agentless is an agentless approach to automatically solve software development problems. 
    - To solve each issue, Agentless follows a simple three phase process: localization, repair, and patch validation.
  - https://github.com/Dylan-Harden3/Agentless
    - Refactor model to use gemini api
  - https://github.com/huyuelin/agentless_MCTS
    - 将MCTS蒙特卡洛树决策算法和agentless结合，添加了定位文件名、定位函数、定位行数、修复四个action，以及在每一步action后会有一步self evaluation给这一步评分。每一步都需要gpt-4o的api。
  - https://github.com/OmmyPatalonian/proggtagentless
    - Add ground truth testing functionality as a replacement for synthetic tests

- https://github.com/yoshiko-pg/difit /1.5kStar/MIT/202511/ts
  - difit is a CLI tool that lets you view and review local git diffs with a GitHub-style viewer
  - command-line tool that spins up a local web server to display Git commit diffs in a GitHub-like Files changed view
- https://github.com/255BITS/gptdiff /MIT/202508/python
  - Make changes to your project with natural language using diffs (generated and smartapplied). 
  - CLI and API available.
- https://github.com/afnanenayet/diffsitter /MIT/202510/rust
  - A tree-sitter based AST difftool to get meaningful semantic diffs
- https://github.com/ilyagr/diffedit3 /apache2/202510/rust
  - The tool in this repo is a UI for editing diffs in a three-pane view. 
  - It is meant to be used with `jj`, and the core of it will hopefully become a part of jj.
# blogs-llm-editing

## 💡 [GPT-4.1 Prompting Guide - Generating and Applying File Diffs](https://cookbook.openai.com/examples/gpt4-1_prompting_guide#appendix-generating-and-applying-file-diffs)

- the GPT-4.1 family features substantially improved diff capabilities relative to previous GPT models.
- we open-source here one recommended diff format, on which the model has been extensively trained.
  - a prompt that applies our recommended tool call correctly
  - a reference implementation of the `apply_patch` tool that we used as part of model training. 
- 👀 Note, that we do not use line numbers in this diff format, as the context is enough to uniquely identify code. 
- If you want to try using a different diff format, we found in testing that the SEARCH/REPLACE diff format used in Aider’s polyglot benchmark, as well as a pseudo-XML format with no internal escaping, both had high success rates.
- These diff formats share two key aspects: 
  - (1) they do not use line numbers, and 
  - (2) they provide both the exact code to be replaced, and the exact code with which to replace it, with clear delimiters between the two.

## 📌 [Code Surgery: How AI Assistants Make Precise Edits to Your Files - Fabian Hertwig’s Blog _202504](https://fabianhertwig.com/blog/coding-assistants-file-edits/)

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

- OpenAI’s Codex CLI utilizes a relatively simple, structured patch format. 
  - Its effectiveness stems partly from OpenAI’s ability to train its models specifically to generate this format reliably.
- ⚖️ The Codex Patch Format(LLM communicates changes using this structure)
  - With the release of GPT-4.1 (April 2025), OpenAI published a “prompt cookbook” detailing this recommended patch format and a reference implementation (`apply_patch.py`). 
  - They indicated significant training effort for GPT-4.1 on this format, contributing to its effective use within the Codex CLI ecosystem.

```diff
*** Begin Patch
*** [Operation] File: [filepath]
@@ [text matching a line near the change]
  [context line (unchanged, starts with space)]
- [line to remove (starts with -)]
+ [line to add (starts with +)]
  [another context line]
*** End Patch
```

- `@@`: Followed by text content from a line near the edit (e.g., function/class definition) used for locating the change. Crucially, this avoids direct reliance on line numbers.
  - The system attempts to match the @@ line and context lines exactly.
  - If this fails, it employs fallback strategies: first matching with trimmed line endings, then matching with all whitespace trimmed.
  - A single patch can contain multiple @@ sections to target different parts of a file.
- With the release of GPT-4.1 (April 2025), OpenAI published a “prompt cookbook” detailing this recommended patch format and a reference implementation (apply_patch.py).
  - They indicated significant training effort for GPT-4.1 on this format, contributing to its effective use within the Codex CLI ecosystem.
- OpenAI’s commentary highlighted that successful formats often avoid line numbers and clearly provide both the code to be replaced and its replacement, using distinct delimiters. 
  - This suggests core principles for reliable AI-driven editing. OpenAI’s ability to co-develop the LLM and the editing tool allows for tight integration and optimization.

### Aider: A Multi-Format Editing System

- Aider employs a more flexible approach, supporting multiple edit formats.
  - It can select the format best suited to the task or the specific LLM being used.
- Aider uses a system of “coder” classes, each responsible for handling a specific edit format
  - This modular design allows for easy extension and selection of different editing strategies.
- EditBlock Format (Search/Replace):

```diff
file.py
<<<<<<< SEARCH
# Code block to find
=======
# Code block to replace with
>>>>>>> REPLACE
```

- Unified Diff Format (udiff): Standard diff format (diff -U0 style)

```diff
--- file.py
+++ file.py
@@ -10,7 +10,7 @@
 def some_function():
-    return "old value"
+    return "new value"
```

- OpenAI Patch Format

```diff
*** Begin Patch
*** Update File: file.py
@@ class MyClass:
    def some_function():
-        return "old"
+        return "new"
*** End Patch
```

- Additional Formats:
  - diff-fenced: filename is inside the code fence (```), used with models like Gemini.
  - editor-diff / editor-whole: Streamlined versions for specific internal modes.

- Aider excels at providing highly informative feedback when edits fail

### OpenHands: Blending Traditional and AI-Assisted Editing

- OpenHands primarily relies on traditional edit application methods while also incorporating an optional LLM-based editing capability.

- OpenHands primarily uses traditional editing approaches. 
  - It has built-in support for detecting different patch formats – including unified diffs, git diffs, context diffs, ed scripts, and RCS ed scripts – using regular expression patterns. 
  - Based on the detected format, it applies the appropriate parsing and application logic. 
- The system supports several traditional editing methods
  - String replacement.
  - Line-based operations (by number).
  - Standard patch application utilities.

- Optional LLM-Based Editing Feature
- OpenHands allows configuring a separate “draft editor” LLM for a distinct editing workflow
  - Target Identification: The primary LLM specifies the target line range for the edit.
  - Content Extraction: The tool extracts this specific code section.
  - LLM Rewrite: The extracted section and a description of the desired change are sent to the specialized “draft editor” LLM. 
  - File Reconstruction: The tool receives the modified section from the editor LLM and integrates it back into the file, replacing the original lines.

### RooCode: Advanced Search and Format Preservation

- RooCode utilizes the search/replace block format. 
  - Its strengths lie in its advanced search algorithm for locating the target block and its meticulous handling of code formatting during replacement.
- When an exact match for the search block fails, RooCode employs a ‘middle-out’ fuzzy matching approach via its MultiSearchReplaceDiffStrategy
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
# discuss-stars
- ## 

- ## 

- ## Use OpenAI's apply patch tool to let GPT-5.2 create, update, and delete files using structured diffs. _202512
- https://x.com/aisdk/status/2001297605775749312
- 

- ## 💡 [How I Built An Agent that can edit DOCX/PDF files perfectly. : r/aiagents _202510](https://www.reddit.com/r/aiagents/comments/1ogwhwn/how_i_built_an_agent_that_can_edit_docxpdf_files/)
- The `find_and_replace` tool
  - My first try. I thought I could map simple document edits to tools like `add_paragraph` . It failed fast - the agent couldn’t see the document, messed up formatting, and needed too many tools ( `add_bullet_point` , etc.). I still think this is one of the best options, though.
- Direct XML edits
  - Terrible idea. Editing DOCX XML is painful - it used tons of context and rarely worked. The main issue is that document styles are inherited (just like in the DOM) so you never really know how edits will turn out.
- Code editing agent
  - I tried this next (this is how the new Claude agent edits files). But again, the agent couldn’t see the document, so wrote code that made bad edits / broke formatting. It was also v slow because I needed to spin up a code sandbox every time the agent needed to edit the file.
- How I built a solution
  - I realised I needed to finetune one of the open source models, specifically a VLM. I collected lots of examples of natural language edit requests and their corresponding file changes (including what they looked like). Then I built a system that fuzzy-matches where the edit should occur (grabbing the relevant XML chunks), rendered those parts of the document, and sent the rendered images, plus the edit instruction and chunks, to the model. The model returns the updated XML chunks, which I then use to patch the raw XML content of the document.
  - So far, this approach has worked extremely well - well enough that I decided to release it as a dev tool so others can build their own agents. If you’d like to try the model or need your agent to edit DOCX/PDF files, you can check it out here: https://www.agentoffice.dev/
  - The main thing skipped is the fact that I wrote a lossless HTML-like mapping from XML for the model to suggest edits in.
- I didn't fully understand what is the flow when using your API. I load the docx, request and edition, and it returns me a new docx with the editions?
  - Not quite. You load the docx. After that, you can request as many editions as you want (they are applied sequentially (FCFS). You can download the document through a separate endpoint at any given time.
  - This setup allows the API to support both live document editing (for use in a GUI editor) and asynchronous editing (for agents or background processes). But thanks for flagging I will try and make it a more clear. 
- Make one for Microsoft Excel
- ## 🧩 [What is `git diff --patience` for? - Stack Overflow](https://stackoverflow.com/questions/4045017/what-is-git-diff-patience-for)
- The patience diff algorithm is a slower diff algorithm that shows better results in some cases.
  - Patience Diff, instead, focuses its energy on the low-frequency high-content lines which serve as markers or signatures of important content in the text. 
  - It is still an LCS-based diff at its core, but with an important difference, as it only considers the longest common subsequence of the signature lines
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
  - The key to this magic is building on `Automerge` , a data sync / collaboration library developed in our lab which optimizes for version control use cases by efficiently storeing the entire granular history of every document, and handling merging of concurrent branches with CRDT algorithms.
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
- ## [feat: Introduce Patch tool for applying unified diffs · Pull Request · google-gemini/gemini-cli _202509](https://github.com/google-gemini/gemini-cli/pull/7642)
  - For LLM-generated code to converge on large projects, the model must make focused changes rather than attempting full rewrites. This patch-based approach is key to iterative refinement.
  - the existing `replace` tool is fundamentally brittle from an engineering perspective. It forces the LLM to simultaneously manage two distinct concerns: the complex syntax of the code itself (like Python indentation) and the formatting characters of the string literal (like `\n` ) when composing a single, multi-line string.
  - This commit replaces the existing 'replace' tool with a new `patch` tool that applies standard unified diffs directly. This creates a proper separation of concerns, allowing the LLM to focus on generating correct code while the agent handles the mechanical application.
  - this tool is never designed to be used alone -- LLM generated 'standard unified diff mode patch' is not 100% reliable, as you can see from your test result -- in that case, the `patch` tool fails correctly, and pass the correct error message back to LLM -- in that case, LLM is supposed to fix it by improve the patch, or calling the `replace` tool as last remediate, or calling `writeFile` as last resort -- This is its 'self-healing' process.
- ## [Why don’t we have tiny, single-purpose LLMs that just output search-and-replace rules? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nhqxzl/why_dont_we_have_tiny_singlepurpose_llms_that/)
  - Why can't I find any LLM fine-tuned solely to produce search-and-replace blocks (regex or structured patterns + replacement templates). 
  - Almost each editing workflow comes down to some flavor of “find X, replace with Y, ” even if the syntax varies.
- I think they’re looking for a semantic regex, e.g. “find all instances of typical dog names and replace them with an English Literature character’s name”.
  - TBH out of the box small models perform fairly well on this type of thing. OP: you can create a benchmark and see how the LLMs compare.
- I think the problem is duplication, if the larger model can handle it perfectly well, there's no need to have a dedicated search-and-replacer do the task for it.
  - That's the thing. I don't want larger general-purpose model to handle this. I'm gonna create the plan first, and then I just want a smaller niche model to execute it (i.e. generate the edits)
- Nearly every tool like codex or Claude code do this all day long. Structured output and tool calling, not just hoping a model tuned for one very specific purpose is the way to go
- If it's a procedural task, shouldn't a script/application handle the job--instead of a language model?
  - Manipulating strings directly is significantly less complicated than having a language model try to recite blocks of text verbatim from context.
- ## [How do LLM-powered tools in IDEs edit files? · community · Discussion _202508](https://github.com/orgs/community/discussions/171782)
- diffs over overwrites 
  - they generate targeted diffs to edit specific lines, not overwrite whole files. keeps unrelated code safe. IDEs use ASTs or text diffs for precision.
  - safety stuff Git for rollbacks, sandboxed temp buffers, and syntax checks to catch dumb mistakes.
- Patch / Diff Generation
  - Most implementations generate a diff (similar to a Git patch) rather than rewriting the whole file. This ensures only the intended section changes, which reduces the risk of clobbering unrelated code.
  - For example, some editors capture the current buffer → send a slice of it to the LLM → apply a unified diff back into the editor.
- under the hood it’s really a careful orchestration of: capture → prompt → generate → diff → apply → let Git/editor handle undo.
- Different tools may vary, but the pattern is mostly consistent: LLM as a suggester, IDE/plugin as the executor, Git/editor as the safety net.
- ## 🌰 [Generating and editing structured output (JSON) with LLM's _202505](https://www.devhelpr.com/technical-articles/generating-and-editing-structured-output-with-llms/)
- llm can also output JSON directly according to a JSON schema, which makes it much more reliable.
- One step further is to use the LLM to edit existing JSON data. 
  - JSON data can be edited with the JSON Patch standard RFC 6902. This is a standard for editing JSON data in a structured way. 
  - The LLM can be used to create a JSON Patch based on a description of the changes that need to be made to the JSON data. This way you can use the LLM to edit existing JSON data in a structured way.
- ## [CoEdIT: State-of-the-Art Text Editing With Fewer Parameters | Grammarly _202312](https://www.grammarly.com/blog/engineering/coedit-text-editing/)
  - https://github.com/vipulraheja/coedit
  - CoEdIT, an instruction-tuned LLM for text editing. 
  - CoEdIT is an open-source LLM that is not only up to 60 times smaller than popular LLMs like GPT-3-Edit (175 billion parameters) and ChatGPT, it also outperforms them on a range of writing assistance tasks.
- We thought that fine-tuning LLMs using text editing tasks, rather than a broader list of general tasks, could do a lot to address the gaps we identified
- ## 🌰💡 [The Edit Trick: Efficient LLM Annotation of Documents _202504](https://waleedk.medium.com/the-edit-trick-efficient-llm-annotation-of-documents-d078429faf37)
- TL; DR: The “edit trick”, like many good ideas, is simultaneously obvious and not. When annotating documents using LLMs, don’t send the whole document in and generate a modified version. Rather, generate a list of edits that are applied to the original document. It’s much faster and cheaper.
- https://github.com/waleedkadous/edit_trick /202504/python
  - This project demonstrates the "edit trick" - a more efficient approach to using LLMs for document modification tasks that reduces token usage, processing time, and handles longer documents.
- 🤔 what happens when you want Claude to add section headings to a 5, 000-word article? The obvious approach involves sending the entire document and asking for the whole thing back with headings added. But that’s not the best way to do it. 
- The issue boils down to three critical bottlenecks:
  - Token usage (and therefore cost) skyrockets
  - Processing time drags on unnecessarily
  - Context window limitations become a real headache.
- I decided to build a small project to demonstrate a much better approach I’ve used a few times now. 
  - I didn’t invent this, I reverse-engineered it from watching Claude Code, but realized it had much broader applicability. 
  - The concept is simple yet powerful: why have the LLM regurgitate the entire document when all you need are the edits?
- Here’s how the “edit trick” works:
  - Send your document to the LLM
  - Instead of asking for the modified document back, ask for a list of specific edits in sed-like format (or json if you prefer)
  - Apply those edits locally without requiring the LLM to generate duplicate content
- The syntax is beautifully straightforward: `s/unique text marker/## Heading Text\n\n$0/` ; 
  - Where the unique text marker identifies where to add the heading, and $0 preserves the original text. Of course you have to make sure that your edit is totally unique, but you can prompt the LLM to make sure that it really is.
- I created a small benchmark to measure the difference between the traditional approach and the edit trick.
  - I tested both approaches on the same document — adding section headings to a 7, 000-character article. The numbers don’t lie — the results were striking
  - That’s an 86% reduction in output tokens! Since output tokens are typically more expensive than input tokens, this translates to dramatic cost savings — almost 70% cheaper.
- The edit trick shines in several scenarios:
  - Any task where the original content mostly stays intact
  - Document formatting tasks (adding headings, standardizing formatting)
  - Text enhancement (expanding sections, adding citations)
  - Content organization (restructuring paragraphs, adding section breaks)
- Implementing It Yourself
  - The implementation is surprisingly simple. A sed-like edit pattern gives you tremendous flexibility while keeping the LLM’s task focused. 
- The key is crafting a clear prompt that instructs the LLM to:
  - Identify positions in the document that need modification
  - Generate specific edit commands rather than the full document
  - Use a consistent format that’s easy to parse programmatically
- I found this works remarkably well across different LLMs, though Claude’s precision makes it particularly suited for generating these kinds of targeted edits.
- The edit trick isn’t just about saving tokens — it’s about developing a more thoughtful, precise approach to working with LLMs
- The next time you’re about to send a large document to an LLM for modification, ask yourself: “Do I need the entire document back, or just the changes?” Your users — and your budget — will thank you.

- ## 🌰 [When LLMs give *almost* correct code, fix it with targeted line edits instead of a full rewrite  _202505](https://medium.com/@pYdeas/when-llms-give-almost-correct-code-fix-it-with-targeted-line-edits-instead-of-a-full-rewrite-af3329e42010)
- This idea came from [Introducing FixIt: an unreasonably effective AI error fixer for SQL - MotherDuck Blog _202401](https://motherduck.com/blog/introducing-fixit-ai-sql-error-fixer/) and adapted with Python to work with not just SQL, but text in general
- 
- 
- 

- ## [How to generate automatically applicable file diffs with ChatGPT? - Prompting - OpenAI Developer Community _202305](https://community.openai.com/t/how-to-generate-automatically-applicable-file-diffs-with-chatgpt/227822)
  - Have any of you succeeded to have ChatGPT output suggested changes to a file in a way that can be automatically applied to the file?

- Using diff implies numbers and cartesian logic, and GPT doesn’t perform well in these fields. It will -very often- output broken diff.
  - The more I look at this problem, the more I think about using a structured approach instead. i.e. Pushing a very rigid JSON schema to the function parameter in the prompt, and forcing GPT to create methods, variables, etc, that are strong because they respect this very specific JSON schema.

- [Feature Request: Enhanced Diff Format Support in ChatGPT for Streamlined Code Integration - Prompting - OpenAI Developer Community _202312 ](https://community.openai.com/t/feature-request-enhanced-diff-format-support-in-chatgpt-for-streamlined-code-integration/545910/9)
- I think it’s a good idea. However, the diff format involves numbers and some logic to them. From my experience, the LLM is not very good at stating exact line numbers and this produces invalid diffs. It’d be interesting to think of a solution to that.

- This is precisely what the project does behind the scenes: GitHub - paul-gauthier/aider 

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
- ## 🌰 [Roo Code 3.4 with NEW Lightning Fast DIFF Edits : r/ChatGPTCoding _202501](https://www.reddit.com/r/ChatGPTCoding/comments/1ibsich/roo_code_34_with_new_lightning_fast_diff_edits/)
- Are they doing what aider does?
  - That is a very broad question. Yes it is doing a search and replace like they are doing but they do so much differently. Aider is truly an amazing piece of software.
- You know what I like best about roo is there is less issue with truncation. Cline will delete huge blocks of code and I have the manually move the valid code over with copy paste because the new code Cline made literally is smack dab in the middle of a current code block. How were you able to figure this out when Cline people still haven't figured that out? 
  - The trick Roo uses is to ask the model to both write out the full content of the file AND include the total number of lines in the file. They’re not perfect at counting lines, but in cases where the number of lines predicted versus the number of lines returned differ significantly, we assume the write was truncated.
- get the ai to generate a patchfile and then apply the patch using old fashioned patch application - im not too sure how to do it in vscode but intellij has patch applier as a shortcut
- my Roo Code is still very slow, just like the one on the left. Any idea when we’ll get the lightning-fast version? Adding the following line to the global rules fixed the issue for me: "Prefer using the apply_diff tool to make changes.". I wonder why it defaults to slow line-by-line editing without this line? 
  - It does not always default to that way without those lines but it depends on the models. For some reason it does sometimes the model itself choose write to file over apply diff and we're working on a fix for that.
- ## 🚀 [Introducing Fast Apply - Replicate Cursor's Instant Apply model : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1ga25gj/introducing_fast_apply_replicate_cursors_instant/)
  - This project was inspired by Cursor's blog post (now deleted). 
  - When using tools like Aider, updating long files with SEARCH/REPLACE blocks can be very slow and costly. Fast Apply addresses this by allowing large models to focus on writing the actual code updates without the need to repeat the entire file.
- Is there a reason this couldn't generate diff style patches? Would automatically work with many existing tools and work flows.
  - The diff format includes line numbers which are hard to predict for llms. Aider blog expands more on this
  - If you really need the diff, you can always create it from the output file compared to the original file.
- This just gave an idea: What if we could make the system smart enough to handle simple fixes locally while pushing more complex problems to larger LLMs? And maybe a way to implement it is to create synthetic training data with complexity ratings from 0-10.
- I'm very interested in implementing this in my project, but unfortunately, I can't seem to find a way to make it work on any sort of larger files, not to mention that it's extremely slow for me. File edit on 500+ lines code takes a while, and even the Colab example with free GPU on Colab with such a small edit takes solid 14+ seconds... Also tried with dedicated huggingface endpoints, and an edit of 100 lines still takes about 8 seconds, which is far more than FastApply from cursor.
- Any insights on how can I make it apply edits faster and with ability to handle larger files...
  - Yeah, I know the speed is definitely the bottleneck here for practical usage.
  - You could try deploying the 1.5B model with Fireworks, as I mentioned above, which might help with the speed.
  - OpenAl just rolled out Speculative Decoding. You could try GPT-4o mini with predicted outputs--it should hit around 150 tokens per second without any setup. Honestly, it feels like this feature just made FastApply obsolete. (I'm crying)
- I haven't tested a lot with large file (how many tokens?), although it's designed for this purpose. The context window is 8192 tokens. => The file should be like 4k tokens, as full length = original + update + final.
  - I think you should retrain the model, while scaling the context size depend on what you need. All the data pipeline + notebook are on github.
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
- If you don’t get double lead, nobody is switching for 2% rate that may be within error margins

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
- ## 💡 [How do I get an LLM to edit a few lines of code? : r/ChatGPTCoding _202502](https://www.reddit.com/r/ChatGPTCoding/comments/1ivnqmd/how_do_i_get_an_llm_to_edit_a_few_lines_of_code/)
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
  - That is, it provides a standard interface for turning code into an AST and then making that AST available to clients like editors and diff tools. Instead of a neat tool like this having to support dozens of languages, it can just support tree-sitter and automatically work with anything that tree-sitter supports. And if you're developing a new language, you can create a tree-sitter parser for it, and now every tool that speaks tree-sitter knows how to support your language.
- 
- 
- 

# discuss-edit-format/protocol ⚖️
- ## 
- ## 
- ## 
- ## 
- ## ⚖️ [RFC: Token-Efficient and Consistent AI Code Generation Through GNU Unified Diff _202411](https://medium.com/@zackisland/rfc-token-efficient-and-consistent-ai-code-generation-through-gnu-unified-diff-md-a07f676c975a)
- A strategy to enhance AI-driven code editing in multi-agent systems using the GNU unified diff format. This format standardizes output from code-generating language models. In testing, diff-based changes reduced output tokens and speed of inference by up to 90%.
- Why?
  - Token Efficiency: Maximize output token utility, optimizing performance and costs
  - Structured Output: Maintain output consistency over multiple iterations or across large code bases with many files
  - Modularity: Standardization of output for models to operate independently, creating patches that can be directly applied or processed by other agents or even integrated directly with git
- What?
  - GNU Unified Patch Output Prompt: An XML (or JSON) context to be appended to a larger `<System Prompt>` that generates text or code. The appended context configures the model’s output structure as a GNU unified patch, outputting only the diff change needed for the generated code (as opposed to returning the entire file/text block). Handles: new files, edits to existing files, and deletions to files, and works for simulated files in memory and real files.
  - (Optional) Patch Command: JavaScript implementation of the `patch` command that can be used for the tool call out if the agent doesn’t have access to native `patch` in Unix or Windows systems, or if custom patching is required (e.g in a virtualized environment such as a sandbox for agent execution).
- NOTE: This prompt has been optimized and tested against Claude 3.5 Sonnet Beta, and ChatGPT 4o + with virtually 100% consistent output. You must only ensure these prompts are appended to a genuine system prompt. 
- a JavaScript implementation of the patch command is provided. This function can be invoked either by a) the AI agent generating the code through a tool call to apply the diffs generated by the AI code generating agent or b) through a virtualized terminal shell provided to the agent or another agent tasked with applying changes to files.
  - The function reads the diff from the JSON output, parses it, and applies the changes to the target file, handling all edge cases such as path issues, line endings, and cross-platform compatibility.
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

- ## 为啥对 ACP 不上心，就是搞 avante.nvim 的 ACP 支持的时候弄伤了，ACP 你行行好吧， _202601
- https://x.com/yetone/status/2008165234805198888
  - 有的是 permission_request 里 merge 了 tool call，有的是 permission_request 之前会发送 tool call，而且 tool call 的 title 每个 ACP server 实现都不一样，有的一大坨像屎一样，行行好吧
- 这种混乱典型的体现了协议初期 "Spec is just a suggestion" 的草莽阶段。permission_request 和 tool_call 的耦合或者是时序颠倒，本质上是服务端为了节省往返 (RTT) 而破坏了协议的原子性。建议在 Client 端加一层 Middleware Adapter，不要直接透传 Payload，而是强制用 Zod 或 TypeBox 做一层 Strict Schema Validation，把那些“像屎一样”的数据结构清洗成标准化的中间表示 (IR) 再喂给 Avante 的渲染层，否则 Lua 的动态类型如果不做防守，panic 是早晚的事。

- 我的偏见认为是 Gemini CLI 不直接提供 API 的锅 = = Gemini 的 Subscription 实在是迷一样的操作，Gemini CLI / Google Code Assistant 跟 AI Studio 的 API Key 是分开计费甚至完全不同的计费路径。但是 AI Studio 有 Gemini Subscription 又可以用它的工作台交互。真是人都麻了。

- claude-code-acp 就是封装了 claude SDK，做了下 nodejs stream 到 web stream 的转换
- 原来 claude code sdk 是支持 streaming text 啊，不过这样的话 claude-code-acp 岂不是违反了 Anthropic 的规定，会有封号风险吧
- 像 opencode/crush 啥的不也都可以支持 claude 账号登陆么
  - 所以 opencode 用户被封号了

- 其实可以搞个更通用的，不要局限于coding agent，现在acp太个性化了

- acp推出两个月了，每周都在变

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

# discuss-proofreading
- ## 

- ## 

- ## 

- ## [I built a text refinement prompt that might even be better than any proofreading prompts : r/ChatGPTPromptGenius _202505](https://www.reddit.com/r/ChatGPTPromptGenius/comments/1kiz7ko/i_built_a_text_refinement_prompt_that_might_even/)
  - I created a text refinement tool that works similarly to prompt optimization tools. You provide a piece of text (whether a prompt or a draft), and it gives you two improved versions-each one tweaked for clarity, tone, and structure.
  - But here's the cool part: you can give feedback on the revisions, and the tool will keep learning and getting better over time. It's a bit like collaborating with a personal editor who adapts to your style.
  - Basically, it becomes a feedback loop to help you lock in the most effective version of your text.
  - Tip: To get the best results from the beginning, always start by telling it the purpose of your writing-like, "This is for a persuasive speech" or "I want this to sound casual but informative." It makes the whole refinement process smarter.

- ## [Tracking changes, is it standard practice for proofreading? : r/TranslationStudies _202301](https://www.reddit.com/r/TranslationStudies/comments/10cyqnb/tracking_changes_is_it_standard_practice_for/)
  - Just turned in a big proofreading/editing job, but I didn't have change tracking enabled in my CAT tool (MARSCat). I assumed the tool was tracking changes by default, but apparently not? My question is, track changes standard or at PM request/editor preference?
- Usually they are requested from me, however I forget occasionally and PMs don’t say anything. If necessary, they can compare the two versions (pre- and post- proofreading) to generate a tracked version with redline changes, so I wouldn’t worry

- I consider tracking changes to be standard for any proofreading or editing work, but as u/sxb1394 mentioned, you can either turn tracking changes on while doing the editing or compare the pre- and post-editing versions. AFAIK, the resulting file is identical no matter which method you use.

- I always ask before starting the proofing. Some clients expressly request it not be turned on, I think because it can make some small unwanted changes to the document, such as misplacing punctuation.

- ## 🆚 [Is there any tool for for manual proofreading of video transcriptions, with ability to check original audio and to maintain a list (dictionary) of text entities? : r/LanguageTechnology _202404](https://www.reddit.com/r/LanguageTechnology/comments/1c3qfii/is_there_any_tool_for_for_manual_proofreading_of/)
- https://gooey.ai/speech offers a bunch of ASR models (google USM, meta-large, whisper v3) and the ability to define a dictionary as a google sheet.

- I'm not sure this is actually an NLP problem. Everything you want here can be done with standard text editors and databases and probably some audio software, you just want an app that puts all of that together. The actual NLP task of transcribing the audio is the part you're doing manually, rather than delegating it to an algorithm to do automatically.
# discuss-rich-text-editing ✏️
- ## 

- ## 

- ## 

- ## [ai快速排版word文章的一个通用思路，字体/字号/缩进什么的都可以 - 开发调优 - LINUX DO](https://linux.do/t/topic/1217729)
  - 让 AI 写大几千字的内容，把它直接复制粘贴到 Word 文档里时，格式，字体，字号，缩进全都是乱七八糟的（相较于 word 前文的排版）
  - 用 AI 节省了文章撰写的时间，但还续花了大把时间在手动调整 word 格式排版上 
  - 在这里我分享一个 “利用 ai 生成 HTML 代码来解决 Word 排版问题” 的思路，能让你 AI 生成内容可以直接复制粘贴到 word 中，并且是一键完成 “格式，字体，字号，缩进” 的排版
  - 直接把 AI 生成的文本粘贴到 Word，本质上是在粘贴 “纯文本” 或 “Markdown”，Word 对这些格式的兼容性并不完美，所以你粘贴进去的东西大概率和前文的内容排版完全对不上。 但是，Word 和 HTML 的底层富文本结构是有极高通用性的
  - ✨ 那么思路就是不让 AI 直接给文本，而是让 AI 生成 “带有排版样式的 HTML 代码”，然后在浏览器中打开 HTML 文件，在浏览器界面全选复制，就可以直接保留所有的排版样式直接粘贴到 word 中
  - 这里根据不同需要有不一样的提示，例子如下：完成课题报告中要填写的内容，新加的内容的字体为宋体小 4 号（要不要加粗由你决定）其他已有的文本的格式不要改变，然后生成带有排版样式的 HTML 代码
  - 总之，这些提示词都有个共同点就是要求 “生成带有排版样式的 HTMl 代码”
  - 将 AI 生成的 HTML 代码复制下来， 在电脑上新建一个文本文档，粘贴代码然后将后缀名改为 html, 在浏览器里看到一篇具有排版的文章
  - 在浏览器页面中全选然后复制, 回到 Word 文档在对应位置按粘贴（如果发现没有粘贴文本格式的话，可以到左上角的这个粘贴界面展开，选择保留原格式粘贴）
  - 这个方法的本质就是利用了 HTML 可以完美渲染 word 富文本内容的功能，将 HTML 作为文本复制的中介以及 ai 看 word 排版的方式，来让 ai 可以输出排版合理且可以快速粘贴到 word 中的文本

- 思路挺不错的，如果有一些大量的内容，排完之后还是要仔细的校对

- 另一种思路，在google-docs侧边栏聊天生成内容后，直接点击apply将带格式的内容插入文档中的光标位置

- 如果遇到公式如何处理呢？我前端时间也在研究如何用 ai 进行排版，我的思路是写一个 python，把 WORD 内容不布局提交给 ai，ai 思考之后下发指令给本地程序去调控每个内容块的位置大小等属性，但因为时间原因，目前还来得及弄了

- ## [Can I get advice on how to work with streaming AI LLMs? - Yjs Community _202404](https://discuss.yjs.dev/t/can-i-get-advice-on-how-to-work-with-streaming-ai-llms/2604)
  - I’m building an editor that assists you with the help of an AI LLM.
  - TipTap Editor (which uses y-prosemirror bindings), for the editor
  - LiveBlocks for the synchronization of the Yjs doc.
  - However, I’m having a bit of trouble figuring out exactly how to make the LLM streaming feature work with Liveblocks and a TipTap editor.
  - The LLM streams markdown content to my backend. From there I need to find a way to sync that content to the Yjs doc that’s hosted in LiveBlocks.
  - However the conversion to a Yjs doc is not straightforward at all. Or at least I’m not figuring out the exact sequence of steps on how to convert a chunk of markdown (which may be invalid still, because remember it’s just a chunk for now!) to the correct yXmlFragment, and from there to push it to liveblocks.
- I think the only viable solution right now is to:
  - 1. Have my users get the streamed markdown from the backend into their browser’s client
  - 2. Automatically populating the TipTap editor content with the setContent hook. Which will then do all the heavy lifting, transform it to a valid Yjs doc and push it to LiveBlocks (thanks to the Collaboration extension)
- HOWEVER, this latter approach blocks the ability of generating content in the background. Meaning that if one of my users close the editor’s tab. The content stops being pushed to LiveBlocks.
- Is there a correct or recommended way to stream content (markdown) from an LLM into an existing Yjs doc?
- Sure, you can insert Y. XmlElements directly into the Yjs document. However, it really depends on your setup how to insert content.
  - Let’s say, you want to insert LLM content as paragraphs using the paragraph block type. 
  - I recommend stripping the markdown part for now.
  - If you want to keep it, you could parse the markdown content (you need a parser for that, you can’t do that manually) and transform it to the delta format (a rich-text format that Y. Text understands, it supports bold, italic, etc…). TipTap should be able to pick-up the richtext from Y. Text. The formatting attributes in Yjs will be picked up by TipTap as “marks”.
- My main issue with parsing markdown in a streamed way is that I can’t know whether we’ve finished a block.
  - One idea that I had was to keep a string in memory of the whole article that the LLM streams to my server. 
  - Meaning, as soon as the LLM sends a new text chunk I do `let fullArticle += newTextChunk` ; 
  - Then each time we get an update I’d like to completely erase the Yjs doc, and replace it with the new contents of fullArticle on its entirety.
- You can replace the `Y.XmlElement` that contains the current LLM answer with a new one. That sounds like a good idea. Then it shouldn’t be a problem to have temporary parsing issues.
  - However, you shouldn’t replace the whole Yjs document on every change, that might lead to some issues down the line. 
  - For once, there is no method to erase all content in Yjs. 
  - Furthermore, large amounts of generated text will result in a lot of overhead (especially for Yjs) that can easily be avoided. 
  - Also, the client has to rerender everything on every LLM update (which is unnecessary, if the previous paragraph didn’t change).
- ## [Can't figure out how to stream markdown into tiptap _202408](https://github.com/ueberdosis/tiptap/discussions/5563)
  - I am having a hard time figuring out how to stream markdown generated from an LLM into tiptap.
  - If I insert content as it comes, it fails in many ways. If I wait til the result is complete and just insert the full string, it works perfectly.
  - I have been trying a middle ground, spliting the markdown by lines, so I make sure format like bold are handled correctly.
- It is very difficult to get streaming of formatted content into the editor it took me two weeks to get everything right for the content Ai pro extension. I would not say that there is an easy answer to this at all. 
  - 💡 I would recommend streaming into a preview element instead and only inserting the content into the editor afterwards.
- I will try your approach, I am going to stream HTML instead of markdown, directly into a decorator, and replace with the final content when complete. Does that make sense?
  - Yea into a decoration sounds like a good plan
- if the LLM is returning markdown content, you can use a markdown to html converter and pass the results to setContent
- ## 🔡 [LLM stream to generate markdown text and insert to editor · facebook/lexical _202404](https://github.com/facebook/lexical/discussions/5967)
  - I'm quite new to Lexical and have been experimenting with using AI streams to create markdown text in an editor.
- What you might need is a markdown to lexical state transformer and vice versa (optional). As the text streams in markdown, the editors internal state can be constructed.
- For anyone else trying to implement this, I got a version working that supports markdown with tables using lexical's HTML converter and showdown, and vercel AI sdk
- maybe you can do by separating streamed markdown into blocks and insert as Element Node.
  - This will help how to separate blocks.
  - https://github.com/vercel/streamdown/blob/main/packages/streamdown/lib/parse-blocks.tsx

# discuss-llm-streaming
- ## 
- ## 
- ## 
- ## 
- ## Introducing Streamdown - A drop-in replacement for react-markdown _20250820
- https://x.com/haydenbleasel/status/1957851370381553880
- Does this also include the added link sanitizations? Like in the hardened react markdown? 
  - Yes it does! All domains are enabled by default, then you can choose to opt-in by specifying an allowlist. 
- does it also support smooth streaming or is there a plan to add that?
  - We’re exploring it currently. The trick is in finding a solution that doesn’t increase the overall response time
- is it possible to disable the streaming part? I know that sounds funny but i have a lot of non-streaming AI (+ other non-AI) use cases for this where streaming is not needed.
  - It will still work fine with regular, non-streamed Markdown
- What is I have static content being rendered (like an html code block that’s not streamed in)? Can I still use this?
  - You can certainly use it with non-streamed Markdown responses e.g. from AI SDK `generateText()` !
- Does it also allow to render custom blocks as well, e.g. how ChatGPT shows a link preview block when I hover over a link? or this does too require involving something like unified.js
  - You can do this with some system prompt magic
- Is there any plan to support mdx or add plugins to it, so that the AI can generate UI elements as JSX and I can display them to the user? Like code sandboxes, callouts, etc.?
  - Currently it feels like the best way to do it is with a specific system prompt detailing a "custom HTML component" that you can then render in `components` , but still exploring.
- Does it support memoization per Markdown block?
  - Yes it does! We haven't listed it on the website yet though as we're looking for a way to reliably test, measure and demonstrate it first.
  - current implementation is good, but not good enough. especially when it comes to code block, it will still render the whole syntax highlighter. If AI elements/streamdown from vercel can optimize it to only render per words, even better.
- ## 📝 [How streaming LLM APIs work | Simon Willison’s TILs _202409](https://til.simonwillison.net/llms/streaming-llm-apis)
- I decided to have a poke around and see if I could figure out how the HTTP streaming APIs from the various hosted LLM providers actually worked. Here are my notes so far.
- All three of the APIs I investigated worked roughly the same: they return data with a `content-type: text/event-stream` header, which matches the server-sent events mechanism, then stream blocks separated by `\r\n\r\n` . Each block has a `data: ` JSON line. Anthropic also include a `event:` line with an event type.
  - Annoyingly these can't be directly consumed using the browser `EventSource` API because that only works for GET requests, and these APIs all use POST.
- ## [How streaming LLM APIs work | Hacker News _202409](https://news.ycombinator.com/item?id=41615404)
- When you ask to return JSON data using streaming, you will notice that the response is incomplete and unparseable by JSON libraries, resulting in malformed errors. 
  - You will have to wait for the entire stream to complete. 
  - To solve this problem I tried to define a spec and built a lib for it: 
  - [lib] https://github.com/st3w4r/openai-partial-stream /MIT/202406/ts/inactive
  - Turn a stream of token into a parsable JSON object as soon as possible. Enable Streaming UI for AI app based on LLM.
- Why do you wait for the entire stream to be complete? Some objects in the JSON structure can be shown to be complete before the stream ends.
  - Yeah, it's an interesting problem to solve. The library is designed to parse incomplete json without waiting for the stream to finish.
- I have been working with streaming LLMs and Server Sent Events. It provides a very simple interface to work with, but you can feel SSE was never designed for this use case. As mentioned in the blog post:
  - > Annoyingly these can't be directly consumed using the browser EventSource API because that only works for GET requests, and these APIs all use POST.
  - It is not designed to send data to open a connection. You will then struggle to work with this streaming approach using frameworks and libraries that are based on the EventSource API.
- EventSource is really really limited. However, you can instead use Fetch via something like https://github.com/Azure/fetch-event-source to consume SSEs.
- OpenAI streaming has many peculiarities at production scale. e.g. you will get “half-chunks” occasionally which are not parseable on their own and must be concatenated with the previous or subsequent chunk for parsing.
- should really be titled streaming output, as full duplex streaming isn't mentioned at all. that'd be necessary for things low latency things like speech etc.

# discuss
- ## 
- ## 
- ## 
- ## 
- ## [Text Editing, AI and Problems that Go Away _202508](https://terrycrowley.medium.com/text-editing-ai-and-problems-that-go-away-ad73a4993ca4)
- The standard best-practice architecture for an interactive application (since the mid-seventies with full-screen display applications like emacs and VI and continuing into the GUI and web/mobile era of today) is one where the application maintains a data model that is rendered into a view. 
- A rich component makes this basic architecture unworkable. 
  - In order to leverage the rich editing capabilities of the component, the application needs to map its data model on to the rich components data model. Then, user editing actions either are directly interpreted by the component, resulting in changes to its data model, or follow the more standard path from application data model to the components model. 
  - So sometimes editing changes flow from the component to the application and sometimes from the application to the component. This two-way flow is really hard to get right (“sync is hard”), and really hard to keep stable over time as component and application capabilities evolve.
- ## [How LLMs Are Transforming Rich Text Editors | Built In _202407](https://builtin.com/articles/llms-transforming-rich-text-editors)
- how integrating LLMs can improve RTEs:
  - Enhanced content creation.
  - Improved content quality.
  - Personalized recommendations. 

    - LLMs can provide tailored suggestions based on the writer’s style, audience and purpose

  - Efficient research and fact-checking. 
- Challenges in Integrating LLMs into RTEs
  - Writing Effective Prompts

    - Users often struggle to create prompts that generate accurate and useful AI responses, leading to suboptimal outputs.
    - Solution: Empower users with a curated library of pre-engineered prompts designed for common writing scenarios. For example, CKEditor’s AI Assistant offers intuitive options

  - Unpredictable Responses

    - LLM outputs can be inconsistent, sometimes straying from the intended context or purpose.
    - Solution: Implement continuous testing and refinement. Analyze usage logs and user feedback to iteratively improve the prompt-response mechanism. 
    - For instance, if your RTE’s “Summarize” feature is underperforming, adjust the prompt to emphasize brevity and A/B test the new prompt against the original.

  - Inconsistent Response Formatting

    - Solution: Embed format specifications directly into AI prompts. 
    - Markdown for Developers: “Explain this concept in a code block, using Markdown triple backticks for formatting.”
    - Structured Data: “Generate a product description and return it as a JSON object with ‘title’, ‘description’, and ‘key_features’ fields.”

  - Understanding and Handling Errors

    - Solution: Provide clear, jargon-free explanations and actionable next steps for errors. For instance, instead of displaying a cryptic “Error 429,” present a user-friendly message like: “Oops! We’ve reached our AI usage limit for the moment. "

  - Lack of Standardized AI UI

    - Solution: Integrate AI functionalities that complement existing user workflows. 
    - Context-aware suggestions
    - Smart formatting tools
    - Intelligent autocomplete
    - AI-powered revision assistant
    - Dynamic style guide enforcement

  - Differentiating in a Crowded Market

    - Solution: Focus on adding unique value rather than merely listing AI as a feature.
    - Industry-specific intelligence: Tailor AI to understand sector-specific jargon and style.
    - Adaptive learning: Implement AI that evolves with each user, learning their writing quirks and preferences.
    - Workflow optimization: Create AI features that streamline users’ specific processes.
    - Collaborative intelligence: Develop AI features that enhance team collaboration.

- Key strategies for effective LLM integration include:
  - Offering intuitive, accessible AI tools
  - Implementing continuous refinement based on user feedback
  - Seamlessly embedding AI into existing workflows
  - Developing industry-specific, value-adding features
  - Balancing AI capabilities with human creativity
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
- ## ⏳ [Fifty Years of Diff | Hacker News _202406](https://news.ycombinator.com/item?id=40692926)
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
