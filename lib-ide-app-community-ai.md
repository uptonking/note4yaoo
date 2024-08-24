---
title: lib-ide-app-community-ai
tags: [ai, community, ide, pm]
created: 2024-05-10T06:17:15.244Z
modified: 2024-08-24T16:28:20.515Z
---

# lib-ide-app-community-ai

# guide

- products
  - [Top 6 Devin AI Alternatives for Developer to Automate Codings](https://analyticsindiamag.com/top-6-devin-alternatives-to-automate-your-coding-tasks/)
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
# code-ai-ide
- https://github.com/ishaan1013/sandbox /MIT/202406/ts
  - A cloud-based code editing environment with an AI copilot and real-time collaboration.
  - It's an OSS code editor with AI code autocompletion and real-time multiplayer collaboration (powered by @liveblocks )
  - Built with @nextjs + @clerkdev + @shadcn UI by @ishaandey_ and it's fully self-hostable via @docker
  - https://x.com/steventey/status/1796352490100896149
    - How is it fully self-hostable if it relies on three SaaS services? Seems more like partially self-hostable?
# discuss-stars
- ##

- ##

- ##
# discuss-ide-ai
- ##

- ##

- ##

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

# discuss
- ##

- ##

- ##

- ##
