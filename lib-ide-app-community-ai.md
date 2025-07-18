---
title: lib-ide-app-community-ai
tags: [ai, community, ide, pm]
created: 2024-05-10T06:17:15.244Z
modified: 2024-08-24T16:28:20.515Z
---

# lib-ide-app-community-ai

# guide
- pm-ai-coding
  - ai编程类热门产品可以在各大ide的插件市场搜索排序

- products
  - [Top 6 Devin AI Alternatives for Developer to Automate Codings](https://analyticsindiamag.com/top-6-devin-alternatives-to-automate-your-coding-tasks/)
# ide-ai-pm
- ai工作使用服务端架构的优点
  - 方便实现关闭页面或刷新页面后，也能看到ai工作结果的效果
  - 方便实现多个ai并行执行多个任务的效果，提高效率
- devin偏服务端方案而偏向创作力工作，cursor偏向工具
# ide-ai-xp
- ide的自动补全和多人实时协作似乎是冲突的

- ai生成的代码的缩进有时与原代码不同
  - 解决方案是在服务端执行 prettier ?

- 
- 
- 

# codellama
- https://github.com/meta-llama/codellama /202401/python
  - Code Llama is a family of large language models for code based on Llama 2 providing state-of-the-art performance among open models, infilling capabilities, support for large input contexts, and zero-shot instruction following ability for programming tasks.
  - We provide multiple flavors to cover a wide range of applications: foundation models (Code Llama), Python specializations (Code Llama - Python), and instruction-following models (Code Llama - Instruct) with 7B, 13B and 34B parameters each.
  - Code Llama was developed by fine-tuning Llama 2 using a higher sampling of code.
  - Our model and weights are licensed for both researchers and commercial entities, upholding(维护，支持) the principles of openness.

- [Introducing Code Llama, a state-of-the-art large language model for coding _202308](https://ai.meta.com/blog/code-llama-large-language-model-coding/)

- [codellama](https://ollama.com/library/codellama)
  - instruct	Fine-tuned to generate helpful and safe answers in natural language
  - python	A specialized variation of Code Llama further fine-tuned on 100B tokens of Python code
  - code	Base model for code completion
  - Fill-in-the-middle (FIM) is a special prompt format supported by the code completion model can complete code between two already written code blocks.

- [codellama (Code Llama) huggingface](https://huggingface.co/codellama)
  - This is an unofficial organization for the Code Llama models in the Hugging Face Transformers format.
  - https://huggingface.co/spaces/codellama/codellama-playground
  - https://huggingface.co/spaces/codellama/codellama-13b-chat
  - Code Llama in Hugging Chat: This is an end-to-end application in which you can use the 34B Instruct-tuned model.
- [CodeLlama huggingface](https://huggingface.co/docs/transformers/en/model_doc/code_llama)
  - The Llama2 family models, on which Code Llama is based, were trained using bfloat16, but the original inference uses float16
# code-ai
- https://github.com/WisdomShell/codeshell
  - http://se.pku.edu.cn/kcl
  - CodeShell是北京大学知识计算实验室联合四川天府银行AI团队研发的多语言代码大模型基座。
  - CodeShell具有70亿参数，在五千亿Tokens进行了训练，上下文窗口长度为8192。
  - 在权威的代码评估Benchmark（HumanEval与MBPP）上，CodeShell取得同等规模最好的性能。
  - CodeShell CPP：CodelShell对话模型CPP版本，支持开发者在没有GPU的个人电脑中使用。注意，CPP版本同样支持量化操作，用户可以在最小内存为8G的个人电脑中运行CodeShell。

- https://github.com/princeton-nlp/SWE-bench /MIT/202405/jupyter
  - https://www.swebench.com/
  - [ICLR 2024] SWE-Bench: Can Language Models Resolve Real-world Github Issues?
  - SWE-bench is a benchmark for evaluating large language models on real world software issues collected from GitHub.
    - Given a codebase and an issue, a language model is tasked with generating a patch that resolves the described problem.
  - We have released SWE-agent, which sets the state-of-the-art on the full SWE-bench test set
  - https://x.com/jyangballin/status/1775114444370051582 /20240402
    - SWE-agent is our new system for autonomously solving issues in GitHub repos. It gets similar accuracy to Devin on SWE-bench, takes 93 seconds on avg + it's open source
    - We designed a new agent-computer interface to make it easy for GPT-4 to edit+run code
    - SWE-agent works by interacting with a specialized terminal, which allows it to: Open, scroll and search through files; Edit specific lines w/ automatic syntax check; Write and execute tests
  - https://github.com/princeton-nlp/SWE-agent /MIT/202405/python
    - https://swe-agent.com/
    - SWE-agent takes a GitHub issue and tries to automatically fix it, using GPT-4, or your LM of choice.
    - It solves 12.29% of bugs in the SWE-bench evaluation set and takes just 1.5 minutes to run.
# discuss-stars
- ## 

- ## 

- ## wish cursor, windsurf, jetbrains junie, and all the ai vibe coders editors out there could just agree on one .rules file format
- https://x.com/enunomaduro/status/1918373761381752871
- Next project idea! Make a global .rules format compiler to all vibe coding editor.

- ## 📌 AI辅助编程的几类产品
- https://x.com/idoubicc/status/1888042418446139837
  1. AI代码编辑器，面向职业程序员，辅助写代码，debug，设计技术方案。代表产品：cursor, windsurf, trae
  2. 一句话生成项目，面向产品经理，输入 idea，快速实现一个 MVP，支持在线发布，快速验证需求，能实现简单的交互功能。代表产品：bolt, lovable, v0
  3. 指定品牌名生成落地页，面向电商卖家 / 独立创作者，快速为自己的商品或品牌生成一个 landing page , 支持在线编辑，一键发布。代表产品：pagen, wegic
  4. 输入 URL 或上传截图，快速复刻项目/组件，面向开发者，参考目标网站写页面的场景。代表产品：screenshottocode, copycoder 
  5. 其他辅助场景：一句话生成桌面/移动 App， 一句话生成管理后台，一句话生成 SQL 语句，一句话生成 API

- 尝试了一下落地页 AI 辅助工具，真心不错。

- 还有一类openhands，devin

- 几乎都在用

- ## 🤔 How Cline works 这两天一直在看 Cline 的源码，探究当前 AI Coding 编辑器背后的神秘技术。 _202501
- https://x.com/xiaokedada/status/1882697004670992774
  - [AI Coding 编辑器没有那么神秘 - How Cline works _202501](https://www.nazha.co/posts/how-cline-works)
  - Cline 的核心是依赖系统提示词以及大语言模型的指令遵循能力。在编程任务启动的时，收集系统提示词、用户自定义提示、用户的输入、以及所在项目的环境信息（哪些文件、打开的 Tab 等等），提交给 LLM。
  - LLM 按照指令输出解决方案和操作。
  - Cline 通过解析返回的操作指令（比如 `<execute_command />、<read_file />` ），调用编写好的 Tool Use 能力进行处理，并将处理结果再次交给 LLM 处理。
  - 也分析了为啥 Cline 会如此消耗 token，它是如何摆脱大语言模型的窗口限制的，@ 操作为啥起作用了...

- https://github.com/caicongyang/mini-cline
  - [Cline AI Agent 核心实现分析](https://github.com/caicongyang/mini-cline/blob/main/docs/core-implementation-analysis.md)

- cline非常棒，经典的react agent模式
  - cline一个很大的缺点就是system prompt实在太长了，例如MCP在我的场景里根本不需要，但是它也携带了，浪费很多token(不知道新版本优化了没有？)。

- cline能用本地的deepseek R1，例如7B，32B直接参与编程么？
  - 可以，他是开源的，你甚至可以自己修改相关的处理逻辑

- cline没有用tool calling吗？而是用解析特殊标识来实现调用工具的？
  - xml, 类似这样的格式。我自己写的agent就是几乎照搬了cline的格式。
  - function calling
- 我个人认为function call并不合适复杂处理过程。当然，cline目前这种系统提示词里all in one的模式似乎也不是很优雅
# discuss-autocomplete/ai
- ## 

- ## Introducing the next evolution of completions in GitHub Copilot: Next Edit Suggestions (preview). _20250213
- https://x.com/code/status/1889742273572737247
  - Also called, "NES" for short.

- GitHub Co-Pilot is the new internet explorer

- ## 💡 [LSP-AI: open-source language server serving as back end for AI code assistance | Hacker News _202406](https://news.ycombinator.com/item?id=40617082)
  - LSP-AI abstracts complex implementation details like maintaining document / context parity and providing different LLM backends.
  - Most editors should let you use multiple language severs at once, they merge the results together which can be annoying.

- Currently, whether multiple language servers can be active in one buffer is up to the language client. In Emacs for example, Eglot (built-in) doesn’t support this but LSP-mode (bolt-on) does.

- It would be very interesting to leverage this to edit documents as much as code. Obviously editor-dependent due to the language server.
- Isn't the entire point behind "language server" (guess it's referring to LSP - Language Server Protocol) that it gets rid of editor-dependent stuff?

- 🤔 Are there any text editors that use LSPs for non-coding tasks?
  - It's not really about the editor. The editor (the LSP client) just provides support for telling the server what the user wants a definition for, and how to display that back to the user.
  - Other non-coding uses of LSP that I'm aware of are spell-checking and grammar suggestions (LSP clients can display diagnostics), semantic syntax highlighting (e.g. for highlighting a markdown document), and projects like the one discussed here which just integrate more general-purpose AI.

- Very interesting approach. The folks at rift worked on LSP as an integration point for AI coding. But I think they are focusing on other things now.
  - My project aider provides a pair-programming UX, which allows complex interactions like asking for a change that will modify multiple files. Could LSP servers support more general AI coding like this?
- The problem with aider for me is that it works in the terminal, where as coding happens in the editor, where I most likely already have the file open I want to transform with LLM. I probably even have my cursor on the thing or can at least easily select the function etc. that needs to be changed.
  - CopilotChat.nvim solves this somewhat elegantly for neovim, providing a streamlined UI to interact with an LLM in a way that allows accepting suggested diffs to your currently open buffer. The problem however is that it only works with GitHub's Copilot chat, as the name suggests. Not sure how well Copilot stacks up against gpt-4o for example but I'd imagine not that well.
  - This is pretty much the kind of UI I'd want for interacting with LLMs, aside from the typical Copilot style ghost autocomplete.

- I want an LLM which uses an LSP to gather more context.
  - Aider uses Treesitter to improve code generation.
# discuss-terminal-ai
- ## 

- ## 

- ## 

- ## [Google introduces Gemini CLI, a light open-source AI agent that brings Gemini directly into the terminal : r/singularity _202506](https://www.reddit.com/r/singularity/comments/1lk5h19/google_introduces_gemini_cli_a_light_opensource/)
- 
- 

- ## [Gemini CLI: your open-source AI agent | Lobsters _202506](https://lobste.rs/s/f9xdsg/gemini_cli_your_open_source_ai_agent)
- While the free tier is generous, there are these privacy concerns.
  - By default, Anthropic does not train generative models using code or prompts that are sent to Claude Code.

- ## [Gemini CLI: your open-source AI agent | Hacker News _202506](https://news.ycombinator.com/item?id=44373754)
- The biggest diffs from Claude code (the current champion): 
  1. Generous free tier (60 RPM!) 
  2. Open Source Apache (Standard after OAI Codex did the same)

# discuss-ide-ai
- ## 

- ## 

- ## [Jules: An asynchronous coding agent | Hacker News _202505](https://news.ycombinator.com/item?id=44034918)
- This has been proposed/exlored in 2023 already: ChatDev: Communicative Agents for Software Development - https://arxiv.org/abs/2307.07924

- Google’s ability to offer inference for free is a massive competitive advantage vs everyone else
  - > Yes, for now, Jules is free of charge. Jules is in beta and available without payment while we learn from usage. In the future, we expect to introduce pricing, but our focus right now is improving the developer experience.

- Can it resolve merge conflicts for me? My least favorite programming task and one I haven't seen automated yet.
  - Claude Code has been creating and cleaning up lots of Git messes for me.

- Any coding solution that doesn’t offer the ability to edit the code in an IDE is nonsense. Why would I ever want this over cursor? The sync thing is kinda cool but I basically already do this with cursor

- Notice how no-one (up until now) mentioned "Devin" or compared it to any other AI agent?

- ## [Microsoft Open Sources Copilot | Hacker News _202505](https://news.ycombinator.com/item?id=44031344)
- Is there a good way to replicate cursor tab in VS code? I don’t mean the interaction model, but how accurate it is. What model does Cursor use? It’s quite good AND fast.

- So they make "building your own Cursor" easier. But at the same time they ban your fork from using Extension Marketplace.

- ## 👾 [VS Code: Open Source Copilot : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kqhljr/vs_code_open_source_copilot/)
- One of the biggest downsides for extensions vs. fork was the lack of access to UI. This will work towards better integration for all extensions. I like it.

- The biggest downside, to date, is not being able to officially use it in Code Server which arguably should have been a first class thing for enterprise customers.
- Yes and no, MCP and local models are not supported yet for enterprise customers (through vscode) and also since we can't easily install copilot in Code Server, the entirely of the functionality is non-existent.

- ## 💰 Windsurf revealed today that they have 500k+ active users and ~1M messages sent a day.
- https://x.com/deedydas/status/1893040524287971437
  - That’s 2% of the global software developer market of ~30M.

- Did you see Bolt hit 3 million users? I think the number of software developers is going to 10x to ~300 million thanks to vibe coding.

- I'm a PM that uses Windsurf, am I counted in 30M or is the market bigger because of people like me getting into programming?
- GitHub alone has over 100M MAUs, so the global software developer market is likely much larger than ~30M.

- interesting numbers, keeping in mind their top-down approach compared to the bottom-up growth trajectory of Cursor.
  - i wonder when they will hit the ceiling -> early adopters are already opinionated on any of these solutions.

- ## 🌰 Tiny teams are the future:
- https://x.com/benln/status/1889388151770325427
  • Cursor: 0 to $100M ARR in 21 months w/ 20 people
  • Bolt: 0 to $20M ARR in 2 months w/ 15 people
  • Lovable: 0 to $10M ARR in 2 months w/ 15 people
  • Mercor: 0 to $50M ARR in 2 years w/ 30 people
  • ElevenLabs: 0 to $100M ARR in 2 years w/ 50 people

- Yes! Mobile had this but smaller.
  • Vine – 0 to 1M users in 3 months w/ <10 people
  • Instagram – 0 to 30M users in 18 months w/ 12 people 
  • Snapchat – 0 to 100M users in 3 years w/ 50 people
  • WhatsApp – 0 to $1B revenue w/ 55 people
  - Measured in users not ARR

- https://x.com/benln/status/1890413609768956015
  - I can't wait to see how churn and revenue retention looks like for each of those companies in a few years.

- ## 为啥字节有了 MarsCode 还要推出一个新的叫 Trae 的 IDE？还是资源太丰富了，内卷的厉害
- https://x.com/_hisriver/status/1881210064083808393
- MarsCode 的重点和基因是 Cloud IDE + Playground，延续了 LLM 时代之前的 Cloud IDE 项目， 可以对标 Replit
  - Trae 对标的当然是 Cursor，对标 Bolt/v0 的也快了
  - 在早期探索阶段，这些不同的现有产品形态如果混在一起从原有产品上「升级」出来，是很容易背历史包袱互相扯后腿的，容易走偏搞错重点

- ## 🚀 Announcing GitHub Copilot Free _20241219
- https://x.com/code/status/1869449373995708703
  - No trial. No subscription. No credit card required.
  - main benefits of Copilot Pro are more models and unlimited requests quota.

- Does it not work through SSH?
  - It should. 

- ## [Show HN: Windsurf – Agentic IDE | Hacker News _202411](https://news.ycombinator.com/item?id=42127882)
- I've been using Cursor Composer heavily and it's great but buggy, and could be more agentic.
  - After about an hour with Windsurf, I find myself frustrated with how it deals with context. If you add a directory to your Cascade, it's reluctant to actually read all the files in the directory.
- 
- 
- 

- ## [Show HN: Aide, an open-source AI native IDE | Hacker News _202411](https://news.ycombinator.com/item?id=42063346)
- 
- 
- 

- ## Windsurf by Codeium which is a Cursor killer which is a vs code + copilot killer which is killing me keeping up with these _20241114
- https://x.com/wesbos/status/1856806422899822999
- Can't wait for Zed to become the standard. Then we will see Zed forks with AI features

- how much did YC invest in this one?
  - 250m is VC funding so far

- ## Bolt New 的产品和销售数据出来了！ 4周时间，从0到400万美金的 ARR！
- https://x.com/oran_ge/status/1856492253902258304
  - 这种爆发式的增长，核心是因为它解决了一个一直以来的行业难题： Web 是世界上使用最广泛的平台，但开发者却无法在浏览器中构建 Web 应用。
  - 通过开创性的 WebContainers 技术和先进的 AI Coder 解决了这个问题。

- ## StackBlitz 推出 bolt. new，可以看作 Artfacts V0 和 Replit 的结合体。
- https://x.com/op7418/status/1842034898317746328
  - 支持提示、编辑、部署的全栈流程
  - 带有完整的开发环境
  - 可以实时预览生产结果。
  - 最重要的是免费。

- "完整的开发环境" 这个不准确，他们的运行环境使用的是 WebContainer 近端容器技术，只支持 JavaScript 技术栈，是一个几乎零成本的 IDE 解决方案，处理不太复杂的前端项目绰绰有余，可以确保 bolt 在线运行环境和真实本地环境一致。相比于 v0 可以零成本做一个完整的项目。

- 测试了一下，图片识别有点弱，我上传了界面参考图，它一点都不参考。但是速度确实快

- 这个赛道有门槛吗？感觉推陈出新太快了。

- ## 🚀 Introducing http://bolt.new, by StackBlitz _202410
- https://x.com/stackblitz/status/1841873251313844631
  - What if AI dev products (Claude, v0, etc) let you install packages, run backends & edit code?
  - Prompt, edit, run & deploy fullstack apps
  - Full dev env (npm, Vite, Next.js, …) w/ frontier AI
  - bolt․new can create beautiful, production ready multi-page apps with backends and DBs like @Supabase .
  - That's because every chat can run a prod build & deploy it to @Netlify (and @Cloudflare) — no login required

- how does bolt․new run in a browser tab without virtual machines?
  - The secret sauce is WebContainers, our micro-OS that runs a full web development environment inside your browser tab. 

- ## 🚀 [Show HN: Void - open source Cursor AI code editor | Hacker News _202409](https://news.ycombinator.com/item?id=41523197)
- [Show HN: Void, an open-source Cursor/GitHub Copilot alternative | Hacker News _202409](https://news.ycombinator.com/item?id=41563958)

- I'm Andrew, one of the creators of Void. 
  - we're building Void as a fork of vscode. The repo has great documentation for extensions, but going deeper gets pretty involved. All of the code is OOP-based, and they mount DOM nodes the old-school way (which is what React was supposed to solve..). So adding new UI features isn't exactly trivial. 
  - Microsoft also made its extension marketplace closed-source 

- As someone who has recently tried to refactor our app atop of VSCode (treating it like a platform), we got burned by the UI design decisions that are not straightforward to overcome, let alone maintain. The closed-source MS marketplace did not help either towards our OSS goals.

- I remember Atom was refactored to use manual DOM updates because the performance penalty of using React wasn't worth it. By the way, isn't OOP by far the most popular paradigm for building desktop UIs? I imagine VS Code is a difficult codebase to work with that has a lot of intricate code 
  - I have spent a great deal of time wading through the VS Code codebase and it takes OOP to the extreme. There are mile long inheritance chains, everything is a class, and it is a giant bowl of spaghetti. To some extent, I understand why they used that development approach. It doesn't use a UI framework, just DOM APIs, so classes make sense in lieu of components, but it's still bonkers.
  - My day job is desktop development (with Electron), and I avoid OOP as much as I can and try to use a functional approach. After jumping all over the VS Code codebase to try to understand how some of this stuff works, and seeing how hard it is to navigate, I think heavy OOP is a bad idea.

- Always interesting to hear such claims when graphic editors like Penpot, which have much tighter perf requirements than editors, are so fast while using React.

- ## Introducing Zed AI, in collaboration with @anthropicAI . _20240821
- https://x.com/zeddotdev/status/1825967812629631034
  - Zed AI brings LLMs directly into your editor with an extensible, text-centric approach.
  - We're also piloting @anthropicAI 's new Fast Edit mode for Claude 3.5 Sonnet with a small set of Zed users.

- ## Introducing LlamaCoder! An open source Claude Artifacts app that can generate full React apps and components with Llama 3.1 405B. 100% free and open source.
- https://x.com/nutlope/status/1819445838705578091
- https://x.com/nutlope/status/1820299682331107371
  - Just put together an architecture diagram for how LlamaCoder works!

- ## 我已经是第二 tier 的付费用户好久好久了，见人就安利 cursor。
- https://x.com/wey_gu/status/1820678802646978674
  - copilot ++ 特别快
  - block selection 之后的逐行change/apply 执行是第一个碾压的创新，非常好用
  - chat 中的灵活引用上下文是 sota 的
  - 用了 sonnet 替换 gpt-4 之后 chat 中的答案直接 apply 到代码，提升了一个台阶
  - 最近的 composer（需要开启）又推向了一个新的水平，直接跨文件改东西

- 这个功能绑定编辑器吗？
  - 是，neovim 没发用，如果原来 vscode 好一点

- ## @LangChainAI 宣布推出第一个本地的 Agent IDE - LangGraph Studio
- https://x.com/tuturetom/status/1819190219788447805
  - 基于 LangGraph Studio 在本地运行，基于代码开发 Agentic Workflow 并可视化交互运行、调试
  - 与 LangSmith 集成，追踪 Agent 运行堆栈
  - 支持 JS/Python，提供持久化层

- 大量程序员使用vim和Emacs，甚至markdown的广泛使用，已经说明高产程序员根本不需要这种可视化

- ## we are launching @wordware_ai ! Wordware is the first IDE solely focused on building your AI with Natural Language Programming
- https://x.com/kozerafilip/status/1819302298944000142
  - 👾 Having built a bunch of AI agents we realised three things:
  1. It’s prompts all the way down
  2. Making AI Apps work requires a bunch of iterations
  3. It’s much faster when the person developing the agent can judge the quality of the outputs
  - So, having spent the last ten years building in AI with my co-founder, we thought from first principles: “If prompting is the new programming, what should the tools be?”
  - The results: A user-friendly, beautiful editor that enables the user to use simple natural language to create complex AI Agents and iterate on them 20x faster than in code.

- what is the added value compared to using the chat apps for all kinds of llms?
  - We are more focused on building the flow once and then having an ability to call into it via an API
  - So it a little like you don't have to have the same conversation with the chatbot every time and you get to make the inside info on how to lead that convo into a product.

- ## 🌰 [AI Assisted Coding · vizhub-core/vzcode _202303](https://github.com/vizhub-core/vzcode/issues/73)
- First pass done in #282

- ## AI 补全工具可能只是冲击传统编程方式的第一步。 AI 设计 / AI CodeGen / AI 文档 / AI TDD / AI Lint 可能还在路上。
- https://x.com/hylarucoder/status/1791807537995747459

- ## [大语言模型加速信创软件 IDE 技术革新 _华为_QCon全球软件开发大会 _202312](https://www.infoq.cn/article/vg9loxtgp3ehdpddec49)
- 「智能化信创软件 IDE」专题，邀请到华为云开发工具和效率领域首席专家、华为软件开发生产线 CodeArts 首席技术总监王亚伟担任专题出品人
- 相比“信创”，“智能化”在过去 5 年中被业界反复提起，智能化技术的发展必然会使诸如 IDE 这样的软件开发工具更加强大。
- 随着大语言模型的诞生，IDE 除了可以自动地完成一些重复性工作之外，还可以协助开发人员在软件的设计和开发过程中完成更多创新性的工作，比如：
  - 自动化重构：将一段复杂的代码分解为更小、更易于管理的函数或类。开发者可以描述他想要实现的重构目标，然后让模型生成相应的代码
  - 代码翻译：大语言模型可以将一种编程语言的代码翻译成另一种编程语言，再配合 IDE 的语法高亮和错误检查功能，可以帮助开发者使用不熟悉的编程语言编写代码
  - 自动化文档生成和更新：大语言模型可以根据代码和注释生成相应的文档，或者在修改代码时自动更新文档。大语言模型是 IDE 的智能化加速度

- ## [AutoDev for VSCode 预览版：精准 AI 编程提示词与编辑器的完美融合 - 知乎 _20240506](https://zhuanlan.zhihu.com/p/696080970)
- 我们将 AutoDev for Intellij IDEA 平台的非凡开发者体验带到了 VSCode 平台。在 IDEA 版本中通过构建非常精准的提示词，以及与编辑器的完美融合， 以帮助开发者更好地编写代码。
- 在设计 IDEA 版本时，我们一直致力于避免使用聊天窗口，以提供更好的用户体验。在 VSCode 版本中，我们将这一理念继续发扬光大。
- 不断地重构我们的架构，以实现精准测试生成所需要的上下文件：
  - 输出准确的测试文件路径
  - 与编辑器的完美融合
  - 函数的相关代码类（输入和输出）表示
  - 基于依赖工具的测试框架分析
- 如下是基于上述的设计理念的 Prompt 示例：
  - 通过读取依赖文件，如build.gradle，我们能够准确地知道项目的依赖，以及测试框架的使用。
  - 通过对函数的上下文分析，我们能够准确地知道函数的输入和输出，以及函数的相关代码类。
  - 通过精准的上下文，可以有非常高的信心直接生成测试代码。

- 在当前的 VSCode 0.1.0 版本中，我们实现了以下的核心功能：
  - 自定义 AI 指令，即通过自定义 prompt 来实现自定义的 AI 指令。
  - 测试生成，即通过 AI 生成测试代码。
  - 注释生成，即通过 AI 生成注释。
  - 语义化搜索核心逻辑，尚未集成到功能中。

- ## [花了四个月，打造了一个满意的大模型 IDE 智能插件 - 知乎 _202308](https://zhuanlan.zhihu.com/p/648598153)
- 围绕开发者体验，设计三种辅助模式
- 自动模式：规范化的代码生成
  - 触发方式：自动模式都在 Context Actions 下，即与上下文相关的 actions。方式自然是那个那能的快捷键：⌥⏎ (macOS) 或者 Alt+Enter (Windows/Linux)。
  - 自动 CRUD。
  - 自动生成测试。
  - 自动代码补全。
- 伴随模式：围绕日常体验设计
  - 伴随模式都需要等待 LLM 返回结果，所以就都扔到 AutoDev Chat 模式下了
  - 在 JetBrains AI Assistant 出来之后，它成了 AutoDev 的最大竞争对手，当然也是参考对象。
- 聊天模式：一个边缘的功能
- AutoDev 的思想是将 LLM（Large Language Model）作为辅助开发者的 Copilot，通过提供辅助工具来解决一些繁琐的任务，让工程师能够更专注于有创造性的设计和思考。

# discuss-code-ai
- ## 

- ## 

- ## 🚀 Augment Code: We spent the past few months building a production-grade AI coding agent from scratch. _202504
- https://x.com/augmentcode/status/1915049816268366268 
  - we learned what actually matters—and open-sourced the whole stack.

- We built the agent to handle real codebase tasks end-to-end:
  - Navigate a repo
  - Reproduce a bug
  - Plan a fix
  - Edit source files
  - Validate with tests
  - Stay within scope

- The architecture is clean:
  - Docker-based runs
  - Planning, file-editing, and bash tools
  - Optimized prompts
  - Simple majority-vote ensembling
- We forked and extended the best ideas from Anthropic’s SWE-bench blog post.

- We didn’t use our own fine-tuned models for this run. The goal was to create a strong, open baseline that others could build on, test against, or tweak. The agent is fast, reproducible, and easy to run.
- If you're working on agents—or just exploring what’s possible—we open-sourced everything
  - https://github.com/augmentcode/augment-swebench-agent

- ## 🎯 Introducing Devin 2.0: a new agent-native IDE experience. _20250404
- https://x.com/cognition_labs/status/1907836719061451067
  - Spin up parallel Devins to take on multiple tasks at once. Each Devin works autonomously and you can jump in any time on the details that need your expertise.
  - Devin creates detailed architecture diagrams, links to sources, documentation, and more for all your repos in Devin Wiki.

- ## ai辅助编程， 经历过几乎所有的工具之后， 我最终确认的顶级配置：
- https://x.com/BadUncleX/status/1900394535408304207
  - aider architect (r1 + sonnet 3.5)
  - warp console (enable ai) 
  - 辅助:  cline (plan/act模式, r1 + sonnet 3.5) 
  - 结论： 单模型， 即使是sonnet 3.7也没法和组合模型打。上面方案接近完美，性价比几乎最高。 agent华而不实.

- 还有一个包月的方案， 还没有验证， 先记录一下，就是不使用api, 改用claude 订阅。 
  - 1. 使用claude desktop，集成mcp， 访问本地项目代码。 
  - 2. 使用ClaudeSync将本地文件同步到claude projects. 
  - MCP现阶段使用似乎是比较容易超出上下文长度， 但仍然值得关注。

- ## 发布 Devv Playground：智能代码生成的利器
- https://x.com/forrestzh_/status/1846451160678650338
  • 实时预览：Devv 理解您的需求，即时生成并展示代码。
  • 边聊边编程：聊天窗旁的 Playground 让搜索和代码更新无缝衔接。
  • 即用即得：生成的代码完整独立，可直接应用到项目中。
  • GitHub 模式加持：结合最新代码库，极大提升开源项目的开发效率。
  • 准确可靠：依托最新、最精准的信息，确保代码质量。
  - Playground 为开发者打造了一个高效、直观的编程环境，让复杂的编码过程变得轻松愉快。
  - 生成代码后即时运行，目前已支持前端代码 & Python。
  - 直接基于 GitHub Repo 来修改 & 生成代码

- ## 🚀 Github Copilot Chat for Repo 全面开放，免费使用
- https://x.com/tuturetom/status/1843648749324865879
  - 对任意 Github 仓库进行语义提问，全局可用，动动嘴就能学习项目源码的时代正式到来
  - https://github.com/copilot

- ## [What's the different between replit agent which is just released and cursor? : r/replit _202409](https://www.reddit.com/r/replit/comments/1fabsow/whats_the_different_between_replit_agent_which_is/)
- ReplitAgents is a MVP builder. Don't expect any sophisticated from it

- Replit agents seem to be limited to a few technologies - Python, Flask, vanilla JavaScript, Postgres, etc. in the Flask ecosystem. It can quickly stub app ideas out, but isn't advanced enough to do complex apps so far. 
  - Cursor doesn't try to act as a full agent, but gives AI tools to move quickly in the development process.

- Replit Agent stops working after 20 minutes. I assume that is the main difference.

- ## Could Replit Agent potentially 30x Replit's market size? 
- https://x.com/taratan/status/1832102411856703795
  - It's idea-to-deployment in minutes. While still buggy at the moment (my app was caught in a pesky OAuth error that it couldn't get out of ), it points to a world where Replit’s customers grow beyond developers (20M today) into truly, anyone with an idea. 
  - This positions Replit closer to a Canva (general public) with 185M users versus a Figma (professional/ semi-professional) with 4M users.
  - As @lennysan notes, Canva generates more revenue than Figma, Miro, and Webflow combined.
  - There has been a number of new players in the battle for AI code generation — like Copilot, Codeium, Claude, Cursor AI. 
  - But Replit has a unique insight that gives them an edge: a great user experience. Experience might just be the differentiator that gives them the winning edge.
- Replit has the potential to become a "Canva for coding" by lowering the barrier to entry for non-developers who have ideas but lack the technical skills to execute them. Much like Canva did for design, Replit can simplify the creation process for apps, offering intuitive tools

- i am pretty sure @github copilot will have something similar once this catches on. @Replit needs to ship and ship fast.

- We all have seen this movie before. It goes no where because AI agents don’t work. The moment you leave the “getting started” project it blows in your face. We need at least 2 more generations of AI models with more comprehensive coding capabilities to make it work as promised.

- ## 🚀 Announcing Replit Agent in early access—available today for subscribers _20240906
- https://x.com/amasad/status/1831730911685308857
  - AI is incredible at writing code. But that's not enough to create software. You need to set up a dev environment, install packages, configure DB, and, if lucky, deploy. It's time to automate all this.
  - idea to software all on your phone
  - Replit clone w/ Agent

- Aider in Replit is still super useful as they serve slightly different use cases.

- ## after using replit's coding agent i think...its over for a lot of traditional saas
- https://x.com/SullyOmarr/status/1832102375257178290
  - wanted slack notifications when customers subscribed/cancelled, Zapier was 30/mo JUST to add a price filter
  - instead replit's agent built & deployed one in < 5 mins, with tests. 1/10 of the cost
- their Agent is only available for the same $20 ($30 CAD)/mo

- Yep, software or SaaS is race to the bottom. There is going to lots of new software that will be built. I doubt we will ever get to 8B people building their own software, but in a decade  20-30M people will be building it. Relevant comment from another discussion.
  - similiar to youtube probably

- I think you forget that most businesses don’t want to go and build their own things. They just want to grab something off the shelf and move on with their core product
- It’s over for no code

- Yes can you even build a software moat anymore?
  - data moat tbh

- fine for toys, but when it gets confused or does bad things you have to fix it

- replit only for multiplay like Google docs for code. Toy usage for me and pair programming

- The average Zapier user has no clue how to code nor prompt. That’s why Zapier exists
  - Would you recommend Replit's tech over Zapier for automation?

- ## devv.ai 的 GitHub Mode 已经支持前端仓库了。 _202406
- https://x.com/forrestzh_/status/1802871846871920676
  - 效果是，在搜索引擎的界面直接解释代码的实现逻辑，并提供文件路径
- 请问有没有支持CPP/Rust仓库的计划？
  - in the progress
- 请问有没有支持同时多个仓库的计划？

- ## 🎯 Devin 2.0 _20240504
- https://x.com/itsandrewgao/status/1786613503471829485
  - Launch Interactive mode to help Devin navigate the web. Really useful if it gets stuck on something like a CAPTCHA.
  - One of my biggest gripes with Devin was not being able to intervene and edit code. You can now do so by launching a web VSCode.
  - Another super exciting update is Cookies which enables Devin to log in to websites for your account **without needing to give Devin your password**.
  - Machine snapshots let you save the state of Devin so when the server shuts down, you can start up again

- ## 👾 [Replit's new Code LLM: Open Source, 77% smaller than Codex, trained in 1 week | Hacker News _202305](https://news.ycombinator.com/item?id=35803435)
- thank you for open sourcing this! It's a real gift to the community to have a model intended for "commercial use" that's actually licensed as such.

- The model is way too small, comparing it to Codex feels disingenous. Sure it's 77% smaller, it's also 77% worse. Although, it's a cool project nonetheless.

- my favorite learning is how they are pushing the state of the art - openai’s HumanEval is the industry standard benchmark for code LLMs, but Reza kindly went above and beyond to show how they use “AmjadEval” - using coder intuition to capture human preference on what output is more helpful to coders

- No Clojure. No Julia. No Haskell. No Racket. No Scheme. No Common Lisp. No OCaml. And, as much as I despise Microsoft, No C#. No F#. No Swift. No Objective-C. No Perl. No Datalog. A glaringly lacking choice of languages.
  - I hate to admit, but Python, C, Java, and JS cover most of the modern programming. But not supporting C# sounds like a bad idea.

- ## [AI -> Code 一些产品体验 - 知乎](https://zhuanlan.zhihu.com/p/695066426)

- [AI*Lowcode 的一些结合场景 - 知乎 _202309](https://zhuanlan.zhihu.com/p/658219081)

- ## [如何利用AI工具提高程序员的编码效率？ - 知乎](https://www.zhihu.com/question/645556922)
- 推荐三个开源的AI编程工具：Devika、Open-Devin和SWE Agent。它们不仅仅是代码的生成者，更是软件工程领域的创新者。

-
-
-

- ## [面向程序员的编程大模型AI | 微言码道 _202403](https://taoofcoding.tech/blogs/2024-03-10/the-code-ai-for-develope)
- Github Copilot是一个由微软, Github以及OpenAI合作开发的专门面向编程的AI工具.
  - Github Copilot的核心功能包括:
  - 代码补全: 根据上下文及你的要求, 补全代码
  - 生成代码片段: 帮你生成测试代码或文档注释等
  - 代码检查: 帮助你检查你的代码的问题
  - 帮助你做代码风格检查, 代码重构, 调试等
- 阿里有自己的大模型通义千问, 甚至还开源了QWen大模型. 做为国内前沿的科技公司, 阿里也推出了通义灵码, 也就是类似Github Copilot的AI工具.
  - 通义灵码针对个人免费
- CodeWhisperer Amazon出品的编程AI工具. 对个人免费
  - 更针对Amazon 云服务有关的编程, 如果你编程主要是使用的Amazon的各种云服务或SDK, 那CodeWhisperer是你约会的AI助手

- CodeLlama 70B是700亿参数, 对GPU内存的要求非常高, 这个硬件要求, 一般人或公司整不起.
  - 如果真想部署一个本地的编程大模型, 可能starCoder2是更具可行性的选择. starcoder2的bigcode训练的开源大模型
# discuss-ai-lowcode
- ##

- ##

- ## 体验了 http://Wegic.ai 的AI建站，UI设计和交互都很惊艳、简洁，整体流程丝滑，很不错的解决了多数低代码、模板库给用户带来的选择困难症、部署困难。
- https://x.com/zQwQs/status/1793216048759754879
  - 看实现像是预定义了少量的组件(可替换文本/图片/动画容器等)，然后让AI生成页面区块，写React组件(Hero/Gallery等)和props，用AI对话去编辑
  - 基于这个想法，使用 gpt-4o + tailwind + Vue + esbuild-wasm 做了个「网页生成器」，还有按区块调整的能力。。 属于是低配山寨版 wegic 了（纯做着玩儿的PoC
  - 还有一个告诉ai接口，然后自动写页面的

# discuss-codebase-search/rag
- ## 

- ## 

- ## 
# discuss-debug
- ## 

- ## 

- ## 

- ## [Launch HN: Patchwork (YC S24) – Automatically add structured logs to your code | Hacker News _202408](https://news.ycombinator.com/item?id=41391931)
  - Big picture: we are building a next generation logging and observability platform which gives engineers the rich debugging context they need.

- On the topic of structured logs, can anyone point me towards where I might learn more about what people have learned over time? I'm new to the world of querying through my logs, but I can already see a benefit to logging with JSON...
  - Structured/JSON saves a tonne of time building regex parsers. The regex parsing at query-time is also pretty expensive. This is where Splunk excels - dealing with the noise with powerful querying. ClickHouse is also very performant at this, we hear. It's an expensive task though (computationally and cost wise)
  - Charity, CTO of Honeycomb has strong views (which we enjoy a lot): https://charity.wtf/tag/observability-2-0/ - they come at it from a tracing/OT angle which is Honeycomb's forte, but we agree a lot on the intended outcomes - actionable (not spammy/noisy) + make it easy to gather the variable/state context in the context of a single event.

- OneUptime.com already does it with the copilot feature. It also fixes exceptions, add structured logs, optimizes functions / spans that take a long time to complete and integrates with OpenTelemetry natively. It's also 100% open-source.
# discuss-pm-ai-devops
- ## 

- ## 

- ## 

- ## cursor 有没有可能让我在等待AI生成的时候，强制看广告，让我来赚钱token？
- https://x.com/yihui_indie/status/1902958928142667805
  - 1. 付费会员免广告 
  - 2. 普通用户看广告
- 看 60 秒广告可以免费使用 thinking 一次, 需要看 10 个广告集齐 sonnet max 才能抽卡一次 SSR 代码。
- 广告就太 low 了，等待时间可能会让你做图片识别来训练AI用，以换取 token

- 广告就太 low 了，等待时间可能会让你做图片识别来训练AI用，以换取 token

- 首行代码免广告，每一个人通过你的邀请码加入，你每次看广告时间缩短0.01秒
# discuss
- ##

- ##

- ##

- ##
