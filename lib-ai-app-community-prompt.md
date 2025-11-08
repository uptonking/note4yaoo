---
title: lib-ai-app-community-prompt
tags: [ai, prompt]
created: 2024-09-08T18:56:59.800Z
modified: 2024-09-08T18:57:12.231Z
---

# lib-ai-app-community-prompt

# guide

# blogs
- 🧑‍🏫 [OpenAI 官方 GPT-4.1 Prompt 指南 - 知乎 _202504](https://zhuanlan.zhihu.com/p/1895544303784294231)
# discuss-stars
- ## 

- ## 

- ## 

- ## [Spent 6 months deep in prompt engineering. Here's what actually moves the needle: : r/PromptEngineering _202510](https://www.reddit.com/r/PromptEngineering/comments/1ny2pff/spent_6_months_deep_in_prompt_engineering_heres/)
- Examples beat instructions 
  - Wasted weeks writing perfect instructions. Then tried 3-4 examples and got instant results. 
  - Models pattern-match better than they follow rules (except reasoning models like o1)
- Version control your prompts like code 
  - One word change broke our entire system. Now I git commit prompts, run regression tests, track performance metrics. Treat prompts as production code
- Test coverage matters more than prompt quality 
  - Built a test suite with 100+ edge cases. Found my "perfect" prompt failed 30% of the time. 
  - Now use automated evaluation with human-in-the-loop validation
- Domain expertise > prompt tricks 
  - Your medical AI needs doctors writing prompts, not engineers. 
  - Subject matter experts catch nuances that destroy generic prompts
- Temperature tuning is underrated 
  - Everyone obsesses over prompts. Meanwhile adjusting temperature from 0.7 to 0.3 fixed our consistency issues instantly
- Model-specific optimization required 
  - GPT-4o prompt ≠ Claude prompt ≠ Llama prompt. 
  - Each model has quirks. What makes GPT sing makes Claude hallucinate
- Chain-of-thought isn't always better 
  - Complex reasoning chains often perform worse than direct instructions. 
  - Start simple, add complexity only when metrics improve
- Use AI to write prompts for AI 
  - Meta but effective: Claude writes better Claude prompts than I do. Let models optimize their own instructions
- System prompts are your foundation 
  - 90% of issues come from weak system prompts. Nail this before touching user prompts
- Prompt injection defense from day one 
  - Every production prompt needs injection testing. One clever user input shouldn't break your entire system

- The biggest revelation: prompt engineering isn't about crafting perfect prompts. It's systems engineering that happens to use LLMs

- When I said prompt injection I meant more to when you are using AI inside your app and the user can talk to it (via a bot or smth similar). The two ways (as far as I know & tried) you can implement prompt injection defense are:
  - Giving very solid instruction inside your templated-prompt you are using for your LLM.
  - Fine tune your AI model to train it against prompt injections, but this a lot more time & resources, yet it's way more effective than any templated prompt.

- Examples are good, however small models will overuse them and they can really ruin the output so you have to be tactical where you use them.
  - I have a system in place that randomly picks examples from a larger set so you have more variety while keeping prompts lean.
- Nice! I’ve a number of workarounds, my favourite is using unrelated examples that the LLM would never actually use - so it copies the structure but uses the context for the actual content.

- Don’t make prompts static. Dynamically write the prompt in chain so you don’t have to craft a fucking system message that matters just preload hard rules and soft code other rules in the dynamic creating.
  - You guys don’t think right. System prompts are not what you think. They are not rules for the system. It’s stargate.
  - You dial up your destination with your user prompts. The system message is your origin. Your perspective it’s the things you believe as the environment.
# discuss-known
- ## 

- ## 

- ## 

- ## 亚马逊 aws 开源了生成生产级别  Claude Prompt 的 Prompt 生成器 「Meta Prompt 」
- https://x.com/tuturetom/status/1832289213171298811
  - 基于 Human-in-the-Loop 的理念，从初始 Prompt 开始，结合人类和 AI 反馈打分优化，迭代 Prompt 架构和填充优化召回示例
- 怎样用啊？
  - 作为 System  Prompt 传入，然后可以提需求，这样可以生成你想要的 Prompt

# discuss-context
- ## 

- ## 

- ## 

- ## 

- ## [LM Studio and Context Caching (for API) : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1npatw9/lm_studio_and_context_caching_for_api/)
  - I'm running a Mac, so LM Studio with their MLX support is my go-to for using local models. 
  - When using the LM Studio as a local LLM server that integrates with tools and IDEs (like Zed, Roo, Cline, etc.), things get a bit annoying with the long-context slowdown. 
  - As I understand, it happens for 2 reasons:
  - The previous messages are reprocessed, the more messages, the longer it takes.
  - Especially on the Macs, the longer the context, the slower the generation speed.

# discuss-prompt-usecases
- ## 

- ## 

- ## 

- ## [My go-to prompt for analyzing stocks. Share yours! : r/PromptEngineering](https://www.reddit.com/r/PromptEngineering/comments/1oqa30m/my_goto_prompt_for_analyzing_stocks_share_yours/)
- Act as a senior equity research analyst. Your task is to compile a comprehensive investment analysis report on [Company Name] (Ticker: [Ticker Symbol]). The report should be detailed, objective, and data-driven, using financial data from the last five full fiscal years and the most recent trailing twelve months (TTM).

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [哪些令你惊艳的AI大语言模型提示词（prompt）？ - 知乎](https://www.zhihu.com/question/5415393695)
- 提示词大致分为下面几个部份：
  - 引导语或指示语：告诉模型需要处理什么样的任务，扮演什么样的角色。因为是一个超级大的语言库，先给定一个标签。让大模型知道是哪个领域的。方便后续的回复。
  - 上下文信息：提供足够的背景信息，以便模型能够更好地理解和处理请求。上下文信息可能包括具体情景、相关数据、历史对话信息等内容。历史内容：告诉大模型之前做了什么。
  - 任务描述：明确地描述你期望模型执行的任务。在处理复杂情况下，一两句说不清楚就需要对任务进行分层描述。
  - 输出格式指示：如果你对输出结果有特定的格式要求，可以给出一个输出示例。让大模型照着输出示例输出就行。
  - 限制条件：设置一些约束条件，可以是风格的约束，也可以是逻辑的约束。
  - 样例输出：提供一个或多个例子可以帮助LLM理解所期望的输出类型和质量。
  - 结束语：如果有必要，可以使用结束语来标示prompt的结束，尤其是在连续的对话或者交互中。
- 并非每个提示都要包含所有要素。根据实际需求和场景，恰当地组合它们，可以大大提高LLM返回结果的质量和相关性。
